## Valid version

|Feature|Version|
|----|----|
|RGB Matrix|0.9.18+|

## Effect modes:

- `:circle`

Send a PR if you could add a new effect!

## RGB Matrix

To take advantage of the RGB Matrix feature, you need to configure the physical LED positions similar to "LED Index to Physical Position" in the QMK's document ([link](https://docs.qmk.fm/#/feature_rgb_matrix?id=common-configuration)).

The API of PRK looks like this:

```ruby
rgb = RGB.new(0, 0, 6)

[
  [188, 16], [187, 48], [149, 64], [112, 64], [37, 48], [38, 16]
].each do |p|
  rgb.add_pixel(p[0], p[1])
end
```

Each LED position represents the LED’s physical [ x, y ] position on the keyboard.
The expected range of values for [ x, y ] is the inclusive range [ 0..224, 0..64 ].

## Example

[Amatelus73](https://shop.yushakobo.jp/en/products/consign_amatelus73) has 74 LEDs that starts from top right of the board
(The "73" in the name means 73 keys while there are 74 LEDs).
The LED chain goes like a snake as illustrated below:

```
#                           starts from here
#                           👇
# LED16 LED15 … <- … LED2  LED1  (right to left) num:16
#   |
# LED17 LED18 … -> … LED31 LED32 (left to right) num:16
#                            |
# LED47 LED46 … <- … LED34 LED33 (right to left) num:15
#   |
# LED48 LED49 … -> … LED62 LED63 (left to right) num:16
#                            |
# LED74 LED73 … <- … LED65 LED64 (right to left) num:11
```

The points are

- The first, third and fifth rows run from right to left. In short, they are reversed
- The number of LEDs in the third and fifth rows is less than in the others

Totalizing the above, you can dynamically calculate the physical position in the keymap.rb like this:

```ruby
# 16 * 5 => 80 which is 6 larger than 74
RGB_COL_COUNT = 16
RGB_ROW_COUNT = 5

# So we'll have to exclude 6 of them
# (Compare with the photo of the Amatelus73)
EXCLUDE_POS = [
  # Exclude one LED position from the third row
  [0, 2],
  # Exclude five LED positions from the fifth row
  [2, 4], [3, 4], [4, 4], [11, 4], [12, 4]
]

ROW_REVERSED = [
  true,   # First row
  false,
  true,   # Third row
  false,
  true    # Fifth row
]

def x_pos(col)
  224 / (RGB_COL_COUNT - 1) * col
end

def y_pos(row)
  64 / (RGB_ROW_COUNT - 1) * row
end

rgb = RGB.new(0, 0, 74)

RGB_ROW_COUNT.times do |row_index|
  RGB_COL_COUNT.times do |col|
    col_index = ROW_REVERSED[row_index] ? (RGB_COL_COUNT - col - 1) : col
    unless EXCLUDE_POS.include?([col_index, row_index])
      rgb.add_pixel(x_pos(col_index), y_pos(row_index))
    end
  end
end

rgb.effect = :circle
rgb.speed = 22

kbd.append rgb
```

Instead of a dynamic calculation above, you can also write a static value of the coordinate.

The code below is equivalent:

```ruby
#
# Comment lines indicate the EXCLUDE_POS
#
[
  [210, 0], [196, 0], [182, 0], [168, 0], [154, 0], [140, 0], [126, 0], [112, 0], [ 98, 0], [ 84, 0], [ 70, 0], [ 56, 0], [ 42, 0], [ 28, 0], [ 14, 0], [  0, 0],
  [  0,16], [ 14,16], [ 28,16], [ 42,16], [ 56,16], [ 70,16], [ 84,16], [ 98,16], [112,16], [126,16], [140,16], [154,16], [168,16], [182,16], [196,16], [210,16],
  [210,32], [196,32], [182,32], [168,32], [154,32], [140,32], [126,32], [112,32], [ 98,32], [ 84,32], [ 70,32], [ 56,32], [ 42,32], [ 28,32], [ 14,32],
#                                                                                                                                                       ^^^^^^^^
#                                                                                                                                                        [0, 2]
  [  0,48], [ 14,48], [ 28,48], [ 42,48], [ 56,48], [ 70,48], [ 84,48], [ 98,48], [112,48], [126,48], [140,48], [154,48], [168,48], [182,48], [196,48], [210,48],
  [210,64], [196,64], [182,64],                     [140,64], [126,64], [112,64], [ 98,64], [ 84,64], [ 70,64],                               [ 14,64], [  0,64],
#                               ^^^^^^^^  ^^^^^^^^                                                              ^^^^^^^^  ^^^^^^^^  ^^^^^^^^
#                               [12, 4]   [11, 4]                                                                [4, 4]    [3, 4]    [2, 4]
].each do |p|
  rgb.add_pixel(p[0], p[1])
end
```

It's tricky because the third row and the fifth row are *reversed* and have *excluded positions*.

Take a close look at the pretty-print above and the photo below.

![](https://swanmatch.github.io/amatelus73/images/gallery/swan.jpg)
