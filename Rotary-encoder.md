## Valid version

0.9.8+

## Description

For example, following keymap.rb will configure 2 rotary encoders.

`encoder_1` moves the cursor vertically.
`encoder_2` adjusts the glittering speed of LED.

```
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

rgb = RGB.new(0, 24, 0, false)
kbd.append rgb

kbd.start!
```
