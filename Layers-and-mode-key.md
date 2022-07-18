## Valid version

|Feature|Version|
|----|----|
|Layer feature|0.9.0+|
|[Changing default layer](#changing-default-layer)|0.9.15+|

## Description

IMHO, layer is the most important feature in DIY-keyboard.
PRK implements the layer feature in `Keyboard#define_mode_key` method.

Read this page carefully because the mode-key's behavior is little bit tricky.

## Usage

```ruby
puts "An example for meishi2"

kbd = Keyboard.new

kbd.init_pins(
  [ 6, 7 ],   # row0, row1
  [ 28, 27 ]  # col0, col1
)

#                          key1       key2  key3  key4
kbd.add_layer :default, %i(SPC_LAYER1 KC_A  KC_B  CTR_ENT_LAYER2) # :default layer should be added at first
kbd.add_layer :layer1,  %i(SPC_LAYER1 KC_1  KC_2  CTR_ENT_LAYER2)
kbd.add_layer :layer2,  %i(SPC_LAYER1 KC_F1 KC_F2 CTR_ENT_LAYER2)

kbd.define_mode_key :SPC_LAYER1,    [ :KC_SPACE,            :layer1, 200, 200 ]
kbd.define_mode_key :CTR_ENT_LAYER2,[ %i(KC_RCTL KC_ENTER), :layer2, 300, 150 ]
#                                     ^^^^^^^^^^^^^^^^^^^^  ^^^^^^^  ^^^  ^^^
#                                     (1)                   (2)      (3)  (4)
# (1): Symbol of a keycode, Array of multiple keycodes, or Proc which is going
#      to be called when you tap.
# (2): Symbol of a keycode (only a modifier), Symbol of a layer to be held, or
#      Proc.
# (3): Release-time threshold(ms). If you release the key within the time,
#      (1) key is going to be invoked once.
# (4): Re-push time threshold(ms). Under the state of (3), if you re-push the
#      key within the time, (1) key is going to be kept pressed

kbd.start!
```

- If you tap "key1" (then release it within 200ms), "SPACE" is going to be sent to the host PC
- If you tap "key2" while holding key1, "1" is going to be sent
- If you tap "key3" while holding key4, "F2" is going to be sent
- If you tap "key4" then release it within 300ms then re-push it within 150ms and hold it, "CTRL+ENTER" is going to be sent continuously

## Changing default layer

Let's say you are using both a Windows and a macOS with a KVM switch, you may want a key to alternate between GUI and CTRL according to the OS.
You can switch the default layer by taking advantage of `Keyboard#define_mode_key`.

```
kbd = Keyboard.new

kbd.add_layer :default_mac, %i[ :TO_WIN :RAISE :KC_LGUI :KC_X :KC_C :KC_V ]
kbd.add_layer :default_win, %i[ :TO_MAC :RAISE :KC_LCTL :KC_X :KC_C :KC_V ]
kbd.add_layer :raise,       %i[ :KC_NO  :RAISE :KC_1    :KC_2 :KC_3 :KC_4 ]

kbd.define_mode_key :RAISE, [ :KC_SPACE, :raise, 200, 200 ]

kbd.define_mode_key :TO_WIN, [ Proc.new { kbd.default_layer = :default_win }, :KC_NO, 200, nil]
kbd.define_mode_key :TO_MAC, [ Proc.new { kbd.default_layer = :default_mac }, :KC_NO, 200, nil]
```

## Proc in `Keyboard#define_mode_key`

[TBD]

## Limitations

- You can't expect tapping "key1" while holding "key4" works and vice versa
- There are some other limitations. Find more by yourself

## Common mistakes

### Default layer name

```ruby
kbd.add_layer :layer1, %i(SPC_LAYER2 KC_1  KC_2  KC_3)
kbd.add_layer :layer2, %i(SPC_LAYER2 KC_A  KC_B  KC_C)
```

Above code doesn't work well because the layer name which is added at first has to be `:default`.

### `:XXXXXXX` doesn't work as a transparent keycode

```ruby
kbd.add_layer :default, %i(SPC_LAYER1 KC_A  KC_B  KC_C)
kbd.add_layer :layer1,  %i(XXXXXXX    KC_1  KC_2  KC_3)
kbd.define_mode_key :SPC_LAYER1, [ :KC_SPACE, :layer1, 200, 200 ]
```

This keymap goes back and forth between :default and :layer1 rapidly when you hold the `:SPC_LAYER1` key.
The effect of holding `:SPC_LAYER1` immediately disappears right after the layer changes to `:layer1` because the key you are currently holding is `:XXXXXXX` which does NOT produce any side effect, so the layer was already back to `:default`

