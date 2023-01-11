## 有効なバージョン

0.9.[未定]+

## 使用方法

`keymap.rb` の最初に

```ruby
require "mouse_key"
```

と書くと、Keyboardクラスに以下の属性が追加されます。

```ruby
Keyboad#mouse_cursor_speed
Keyboad#vertical_wheel_speed
Keyboad#horizontal_wheel_speed
```

以下のように書くことができます。

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

## キーコード

| シンボル | エイリアス | 説明 |
|----|----|----|
| :KC_MS_UP | :KC_MS_U | マウスカーソルを上に移動 |
| :KC_MS_DOWN | :KC_MS_D | マウスカーソルを下に移動 |
| :KC_MS_LEFT | :KC_MS_L | マウスカーソルを左に移動 |
| :KC_MS_RIGHT | :KC_MS_R | マウスカーソルを右に移動 |
| :KC_MS_BTN1 | :KC_BTN1 | ボタン1を押す |
| :KC_MS_BTN2 | :KC_BTN2 | ボタン2を押す |
| :KC_MS_BTN3 | :KC_BTN3 | ボタン3を押す |
| :KC_MS_BTN4 | :KC_BTN4 | ボタン4を押す |
| :KC_MS_BTN5 | :KC_BTN5 | ボタン5を押す |
| :KC_MS_WH_UP | :KC_WH_U | ホイールを向こう側に回転 |
| :KC_MS_WH_DOWN | :KC_WH_D | ホイールを手前側に回転 |
| :KC_MS_WH_LEFT | :KC_WH_L | ホイールを左に倒す |
| :KC_MS_WH_RIGHT | :KC_WH_R | ホイールを右に倒す |

