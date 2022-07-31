## Valid version

0.9.[TBD]+

## Usage

At the top of `keymap.rb`,

```ruby
require "mouse_key"
```

Then, these attributes are added to Keyboard class:

```ruby
Keyboad#mouse_cursor_speed
Keyboad#vertical_wheel_speed
Keyboad#horizontal_wheel_speed
```

So you can write like this:

```ruby
# Default values
kbd.mouse_cursor_speed     = 10
kbd.vertical_wheel_speed   = 10
kbd.horizontal_wheel_speed = 10
# Adjust values
kbd.add_layer :default, %i(CURSOR_SPD_INC CURSOR_SPD_DEC WHEEL_SPD_INC WHEEL_SPD_DEC)
kbd.define_mode_key :CURSOR_SPD_INC, [ Proc.new{ kbd.mouse_cursor_speed     += 5 }, nil, 200, nil ]
kbd.define_mode_key :CURSOR_SPD_DEC, [ Proc.new{ kbd.mouse_cursor_speed     -= 5 }, nil, 200, nil ]
kbd.define_mode_key :WHEEL_SPD_INC,  [ Proc.new{ kbd.vertical_wheel_speed   += 5
                                                 kbd.horizontal_wheel_speed += 5 }, nil, 200, nil ]
kbd.define_mode_key :WHEEL_SPD_DEC,  [ Proc.new{ kbd.vertical_wheel_speed   -= 5
                                                 kbd.horizontal_wheel_speed -= 5 }, nil, 200, nil ]
```

## Keycodes

| Symbol | Alias | Description |
|----|----|----|
| :KC_MS_UP | :KC_MS_U | Move cursor up |
| :KC_MS_DOWN | :KC_MS_D | Move cursor down |
| :KC_MS_LEFT | :KC_MS_L | Move cursor left |
| :KC_MS_RIGHT | :KC_MS_R | Move cursor right |
| :KC_MS_BTN1 | :KC_BTN1 | Press button 1 |
| :KC_MS_BTN2 | :KC_BTN2 | Press button 2 |
| :KC_MS_BTN3 | :KC_BTN3 | Press button 3 |
| :KC_MS_BTN4 | :KC_BTN4 | Press button 4 |
| :KC_MS_BTN5 | :KC_BTN5 | Press button 5 |
| :KC_MS_WH_UP | :KC_WH_U | Move wheel up |
| :KC_MS_WH_DOWN | :KC_WH_D | Move wheel down |
| :KC_MS_WH_LEFT | :KC_WH_L | Move wheel left |
| :KC_MS_WH_RIGHT | :KC_WH_R | Move wheel right |

