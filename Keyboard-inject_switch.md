## Valid version

0.9.18+

## Usage

`Keyboard#inject_switch` will inject a switch position of the matrix as if it was tapped:

```ruby
kbd.inject_switch(1, 0)
#                 ^  ^row position
#                 |
#                 col position
```

Let's say you have a 1x4 matrix macro pad that has a rotary encoder:

```ruby
kbd.init_pins(
  [1],
  [10, 11, 12, 13]
)
kbd.add_layer :default, %i[
  KC_LEFT KC_DOWN KC_UP KC_RIGHT
]
encoder = RotaryEncoder.new(15, 16)
encoder.clockwise do
  kbd.send_key :KC_VOLU
end
encoder.counterclockwise do
  kbd.send_key :KC_VOLD
end
kbd.append encoder
```

It works. But you can also use `inject_switch` with "vacant" matrix:

```diff
 kbd.init_pins(
-  [1],
+  [1, 2], # (*) See the footnote
   [10, 11, 12, 13]
 )
 kbd.add_layer :default, %i[
   KC_LEFT KC_DOWN KC_UP KC_RIGHT
+  KC_VOLU KC_VOLD KC_NO KC_NO
 ]
 encoder = RotaryEncoder.new(15, 16)
 encoder.clockwise do
-  kbd.send_key :KC_VOLU
+  kbd.inject_switch(0, 1)
 end
 encoder.counterclockwise do
-  kbd.send_key :KC_VOLD
+  kbd.inject_switch(1, 1)
 end
 kbd.append encoder
```

The advantage of this method is that you can re-assign keycodes to the encoder by VIA/Remap.

See also [[Rotary encoder]] and [[VIA and Remap]].

----

(*) Generally, GPIO 2 should be just floated from the circuit because it is internally pulled up.

