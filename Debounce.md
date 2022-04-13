## Valid version

0.9.13+

## Debounce types
|Type|Default|Algorithm|RAM usage|w/ Matrix scan|w/ Direct scan|
| ---- | :--: | ---- | :--: | :--: | :--: |
|:per_row|Yes|Symmetric eager debounce per row|Small|✔|🙅|
|:per_key|No|Symmetric eager debounce per key|Big|✔|✔|
|:none|No|No debounce|Almost zero|✔|✔|

- `:per_key` is the most recommended one unless your firmware causes an "Out of Memory" error
- `:per_row` will not work well with `:direct` scan mode while it's the default one. Use `:per_key` instead. See [[Keyscan matrix]] abount scan modes
- If you are confident your switches never bounce mechanically and you are a PC game enthusiast, use `:none` which doesn't cancel any bounce and performs maximum

## Usage

```ruby
kbd = Keyboard.new
kbd.set_debounce(:per_key)
kbd.set_debounce_threshold(70) # Optional. 40(ms) by default
```

- If you didn't call `set_debounce`, `:per_row` debouncer will be used by default
- When you'll call `set_debounce_threshold`, you should call `set_debounce` in advance even if you use the default `:per_row` algorithm

## What do "symmetric", "eager" and "per row/key" mean?

See QMK's document: [https://docs.qmk.fm/#/feature_debounce_type](https://docs.qmk.fm/#/feature_debounce_type)
