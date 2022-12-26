## Valid version

0.9.6+

### Deprecation

In 0.9.20, hardware one-way UART on split-type is deprecated. Instead, software mutual UART is now the default and the only option
Keyboard#mutual_uart_at_my_own_risk= no longer takes any effect


## Feature
- Syncs RGB blinking between both halves
- Keycodes related to RGB (see [RGB-feature](https://github.com/picoruby/prk_firmware/wiki/RGB-feature)) work on not only anchor but also partner half

## In your `keymap.rb`

```ruby
kbd = Keyboard.new
kbd.split = true

# In 0.9.20+, you dont' need write this line
kbd.mutual_uart_at_my_own_risk = true
```

## Caution❗
- ~~Turning on `Keyboard#mutual_uart_at_my_own_risk` is an **experimental** feature~~
  - It may make the keyboard unstable and may **break your chip**🔥 depending on your usage. See below
- Make sure to disconnect the TRS(TRRS) cable when you change this option. Reconnect it after changing BOTH halves
  1. Disconnect the USB cable and the TR(R)S cable
  2. Connect the USB cable to a half, flash prk_firmware-*.uf2 and your `keymap.rb` ~~that configures `mutual_uart_at_my_own_risk = true`~~
  3. Disconnect the USB cable
  4. Connect the USB cable to the other half, flash prk_firmware-*.uf2 and your `keymap.rb` ~~that configures `mutual_uart_at_my_own_risk = true`~~
  5. Disconnect the USB cable
  6. Connect the TR(R)S cable
  7. Eventually, connect the USB cable to the anchor half

### We know you feel messy

We have the plan to implement a new feature in order to make things simple: [issue/155](https://github.com/picoruby/prk_firmware/issues/155)

