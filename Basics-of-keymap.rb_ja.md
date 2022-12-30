## 重要なポイント

- keymap.rb のエンコーディングは基本的に "ASCII" ですが、マルチバイト文字がコメント行でのみ使用される場合に限り "BOM無しUTF-8" も有効です
  - 言い換えれば、"BOM付きUTF-8"でエンコードされた keymap.rb の場合 PRK Firmware は機能しません
  - もしあなたの keymap.rb がBOMを含むかどうかわからなければ、["BOM チェック" をGoogle検索](https://www.google.com/search?q=bom+%E3%83%81%E3%82%A7%E3%83%83%E3%82%AF) してください

### 既知の問題

- PRK は、4 KB (4096 Bytes) 未満の keymap.rb のみ処理できます
  - `#` で始まるコメント行を消すとサイズを小さくすることができます

## keymap.rb のシンプルな例

例えば、この例のキーボードは5行12列の「通常マトリクス」で構成されています。

他のマトリクスやダイレクトスキャンについては、 [[Keyscan matrix]] を参照してください。

### キーボードの初期化

```ruby
kbd = Keyboard.new
```

### GPIO ピンの初期化

```ruby
kbd.init_pins(
  [ 1, 2, 3, 4, 5 ],                              # row0  row1 ... respectively
  [ 6, 7, 8, 9, 29, 28, 27, 26, 22, 20, 23, 21 ]  # col0  col1 ... respectively
)
```

### レイヤーの設定

```ruby
kbd.add_layer :default, %i(
  KC_GRV  KC_1    KC_2    KC_3    KC_4    KC_5    KC_6    KC_7    KC_8     KC_9     KC_0    KC_BSPC
  KC_ESC  KC_Q    KC_W    KC_E    KC_R    KC_T    KC_Y    KC_U    KC_I     KC_O     KC_P    KC_DEL
  KC_TAB  KC_A    KC_S    KC_D    KC_F    KC_G    KC_H    KC_J    KC_K     KC_L     KC_SCLN KC_QUOT
  KC_CAPS KC_Z    KC_X    KC_C    KC_V    KC_B    KC_N    KC_M    KC_COMM  KC_DOT   KC_SLSH KC_RSFT
  KC_LSFT KC_LCTL KC_LALT KC_LGUI LOWER   KC_SPC  KC_ENT  RAISE   KC_LEFT  KC_DOWN  KC_UP   KC_RIGHT
)
kbd.add_layer :raise, %i(
  KC_F1   KC_F2   KC_F3   KC_F4   KC_F5   KC_F6   KC_F7   KC_F8   KC_F9    KC_F10   KC_F11  KC_F12
  KC_GRV  KC_EXLM KC_AT   KC_HASH KC_DLR  KC_PERC KC_CIRC KC_AMPR KC_ASTER KC_LPRN  KC_RPRN KC_MINS
  KC_TAB  KC_LABK KC_LCBR KC_LBRC KC_LPRN KC_QUOT KC_LEFT KC_DOWN KC_UP    KC_RIGHT KC_UNDS KC_PIPE
  KC_LSFT KC_RABK KC_RCBR KC_RBRC KC_RPRN KC_DQUO KC_TILD KC_BSLS KC_COMMA KC_DOT   KC_SLSH KC_RSFT
  KC_LSFT KC_LCTL KC_LALT KC_LGUI LOWER   KC_SPC  KC_ENT  RAISE   KC_LEFT  KC_DOWN  KC_UP   KC_RIGHT
)
kbd.add_layer :lower, %i(
  KC_F1   KC_F2   KC_F3   KC_F4   KC_F5   KC_F6   KC_F7   KC_F8   KC_F9    KC_F10   KC_F11  KC_F12
  KC_ESC  KC_1    KC_2    KC_3    KC_4    KC_5    KC_6    KC_7    KC_8     KC_9     KC_0    KC_MINS
  KC_TAB  KC_F2   KC_F10  KC_F12  KC_LPRN KC_QUOT KC_DOT  KC_4    KC_5     KC_6     KC_PLUS KC_BSPC
  KC_LSFT KC_RABK KC_RCBR KC_RBRC KC_RPRN KC_DQUO KC_0    KC_1    KC_2     KC_3     KC_SLSH KC_COMMA
  KC_LSFT KC_LCTL KC_LALT KC_LGUI LOWER   KC_SPC  KC_ENT  RAISE   KC_LEFT  KC_DOWN  KC_UP   KC_RIGHT
)

kbd.define_mode_key :RAISE, [ nil, :raise, nil, nil ]
kbd.define_mode_key :LOWER, [ nil, :lower, nil, nil ]

kbd.define_composite_key :CAP_A, %i(KC_A KC_RSFT)
```

### キーボードの開始

```ruby
kbd.start!
```

## 参照
- [[Keycodes]]
- [[Layers and mode key]]
- [[Composite key]]
- [issues/86](https://github.com/picoruby/prk_firmware/issues/86)
