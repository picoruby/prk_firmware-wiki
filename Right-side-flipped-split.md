## Valid version

0.9.4+

## Description

Some split-type keyboards have a circuit that can be called "right side flipped".

eg:

- Zink
- Let's split

PRK Firmware supports those keyboards by `:right_side_flipped_split` attribute.

```ruby
# Example keymap for Zink
kbd = Keyboard.new
kbd.split = true

kbd.split_style = :right_side_flipped_split

kbd.init_pins(
  [ 27, 26, 22, 20 ],
  [ 29, 4, 5, 6, 7, 8 ]
)
kbd.add_layer :default, %i[
  KC_TAB  KC_Q   KC_W    KC_E      KC_R  KC_T     KC_Y     KC_U   KC_I     KC_O     KC_P      KC_BSPACE
  CTL_ESC KC_A   KC_S    KC_D      KC_F  KC_G     KC_H     KC_J   KC_K     KC_L     KC_SCOLON KC_QUOTE
  KC_LSFT KC_Z   KC_X    KC_C      KC_V  KC_B     KC_N     KC_M   KC_COMMA KC_DOT   KC_SLASH  KC_RSFT
  KC_ESC  ADJUST KC_LALT CMD_LANG2 RAISE KC_SPACE KC_ENTER LOWER ALT_LANG1 KC_DOWN  KC_UP     KC_RGHT
]
```
