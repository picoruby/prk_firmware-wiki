## Valid version

0.9.8+

## Description

For example, following keymap.rb will configure 2 rotary encoders.

`encoder_1` moves the cursor vertically.
`encoder_2` adjusts the glittering speed of LED.

```ruby
kbd = Keyboard.new

encoder_1 = RotaryEncoder.new(28, 27)
encoder_1.clockwise do
  kbd.send_key :KC_DOWN
end
encoder_1.counterclockwise do
  kbd.send_key :KC_UP
end
kbd.append encoder_1

encoder_2 = RotaryEncoder.new(26, 22)
encoder_2.clockwise do
  kbd.send_key :RGB_SPI
end
encoder_2.counterclockwise do
  kbd.send_key :RGB_SPD
end
kbd.append encoder_2

# The usage of Keyboard#send_key in encoder_3
# and encoder_4 is valid on 0.9.17+

# Composite key
encoder_3 = RotaryEncoder.new(21, 20)
encoder_3.clockwise do
  kbd.send_key :KC_LALT, :KC_TAB
  #            ^^^^^^^^^^^^^^^^^
  #            Accepts multiple symbols
end
encoder_3.counterclockwise do
  kbd.send_key %i(KC_LALT KC_LSFT KC_TAB)
  #            ^^^^^^^^^^^^^^^^^^^^^^^^^^
  #            An array of symbols also works
end
kbd.append encoder_3

# Consumer (media) key
encoder_4 = RotaryEncoder.new(19, 18)
encoder_4.clockwise do
  kbd.send_key :KC_VOLU
end
encoder_4.counterclockwise do
  kbd.send_key :KC_VOLD
end
kbd.append encoder_4

kbd.start!
```

See also [[Consumer key]]
