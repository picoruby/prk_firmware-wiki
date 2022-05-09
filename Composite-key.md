## Valid version

0.9.10+

## Description

A composite key reports multiple keycodes at once.

## Usage

Let's say there is a five-keys pad. You can make the most useful (?) programming tool like this:

```ruby
kbd.add_layer :default, %i(KC_SPACE CUT COPY PASTE KC_ENTER)
kbd.define_composite_key :CUT,   %i(KC_LCTL KC_X)
kbd.define_composite_key :COPY,  %i(KC_LCTL KC_C)
kbd.define_composite_key :PASTE, %i(KC_LCTL KC_V)
```

Instead, you can also write the equivalent keymap in this way:

```ruby
kbd.add_layer :default, [ :KC_SPACE, %i(KC_LCTL KC_X), %i(KC_LCTL KC_C), %i(KC_LCTL KC_V), :KC_ENTER ]
```
