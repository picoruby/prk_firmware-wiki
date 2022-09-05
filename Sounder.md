## Valid version

|Feature|Version|
|----|----|
|Sounder|0.9.18+|

## Description

PRK can not only make a beep sound but also play music.

As of 0.9.18, Piezoelectric sounder is supported by `Sounder` class.

## Basic usage

```ruby
require "sounder"
sounder = Sounder.new(2) # A pin number that connecs to the sounder
sounder.play "c d e f g a b < c"
```

This plays "Do Re Mi Fa So La Ti Do"

## API

### Sounder#compile

It creates a new song but doesn't play it.

```ruby
sounder.compile "c e g f e f d c"
```

You can also pass variable-length arguments like this:

```ruby
sounder.compile "c e g f", "e f d c"
```

### Sounder#replay

It plays the last played (compiled) song.

```ruby
sounder.replay
```

### Sounder#play

A wrapper method for `Sounder#compile` and `Sounder#replay`.
As in, it accepts variable-length arguments of String.

```ruby
sounder.play "c e g f", "e f d c"
```

### Sounder#add_song

See [Examles](#examples).

## Preset songs

The list of preset songs:

|Name|
|----|
|beepo|
|pobeep|
|beepbeep|
|oneup|

```ruby
sounder.play :beepo
```

## Examples

### Plays the intro of Super Mario Bros. when the keyboard starts up

```ruby
sounder = Sounder.new(2)
sounder.play "T200 L8 O5 e16. r32 e r e r c e r g r4. > g"
```

You can add your song to the list:

```ruby
sounder = Sounder.new(2)
sounder.add_songs :mario, "T200 L8 O5 e16. r32 e r e r c e r g r4. > g"
sounder.play :mario
```

### Beeps every time you hit a key

```ruby
sounder = Sounder.new(2)

kbd.before_report do
  if kbd.key_pressed?
    sounder.play :beepo
    sounder.lock
  else
    sounder.unlock
  end
end
```

`sounder.lock` and `sounder.unlock` are for preventing another playback while playing.

## BTW, how to write a song?

See [[Music Macro Language]].

## Advanced example

### Both halves of split-type have a sounder

```ruby
#
# You only can get the right answer from `Keyboard#anchor?` inside the `Keyboard#on_start`
# callback because anchor or not is undecided until the kbd starts.
#
# The song is split into 2 parts because memory is short if it's united.
#
kbd.on_start do
  if kbd.anchor?
    sounder.add_song :dq_1,
      "T120 L8 Q5 e.e16eddd cdefed efga<c>a gfed.d16d e.e16eece Q8 d2."
    sounder.add_song :dq_2,
      "T148 Q7 L4 r2g8.g16 <cdef g<c2>b8.a16 a.g8r8f+8f+8a8 ge2>e8.e16 eef+g+ a2r8a8b8<c8",
      "d2r8>a8a8<c8 c>bag <Q8e2Q7r8f8e8d8 c2>a<c Q8d2Q7r8e8d8c8 c2>bg <Q8g2Q7r8e8f8g8 Q8a2Q7r8>a8b8<c8f2e2 c2"
  else
    sounder.add_song :dq_1,
      "T120 L8 Q5 c.c16c>ggg eg<cdc>g <cdefaf edc>g.g16g <c.c16cc>e<c Q8 g2."
    sounder.add_song :dq_2,
      "T150 Q7 L4 r2f8.f16 >c>bb-a e2f2 <c>gc<c >c<eg>c e2e2 a<e>c>a",
      "<f+a<d>f+ g2gb eg+be ab<c>a f+a<d>d gg<df ec+>a<e >defd <e>g<e>g <c>gd"
  end
end

kbd.add_layer :default, %i[ KC_A KC_B KC_C DRANGONQUEST ]

song = :dq_1

#
# When you tap :DRANGONQUEST key, the sounder will play the song's first half.
# When you tap it again, you should hear the second part.
#
kbd.define_mode_key :DRANGONQUEST,
  [
    Proc.new do
      sounder.play song
      song = (song == :dq_1 ? :dq_2 : :dq_1)
    end,
    nil, 300, nil
  ]

kbd.signal_partner :DRANGONQUEST do
  sounder.play song
  song = (song == :dq_1 ? :dq_2 : :dq_1)
end
```
