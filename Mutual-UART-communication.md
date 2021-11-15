## Valid version

0.9.6+

## Feature
- Syncs RGB blinking between both halves
- Keycodes related to RGB (see [RGB-feature](https://github.com/picoruby/prk_firmware/wiki/RGB-feature)) work on the partner half

## In your `keymap.rb`

```
kbd = Keyboard.new
kbd.split = true
kbd.mutual_uart_at_my_own_risk = true
```

## Caution❗
- Turning on `Keyboard#mutual_uart_at_my_own_risk` is an **experimental** feature
  - It may make the keyboard unstable and may **break your chip**🔥
- Make sure to disconnect the TRS(TRRS) cable when you change this option. Reconnect it after changing BOTH halves
- Keys RGB_xxx are working on the partner half only when you use this option
