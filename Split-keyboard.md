## Feature
- Supports split type keyboards

## In your `keymap.rb`

```ruby
kbd = Keyboard.new
kbd.split = true # This should happen before Keyboard#init_pins.
kbd.uart_pin = 1 # See below.
```

`kbd.uart_pin` is 1 by default, so you don't need to explicitly write it if you use GPIO1 for the connection.
In that case, all you have to do is to write `kbd.split = true` before `kbd.init_pins`.

The pins that can be set to kbd.uart_pin are those that have the function "UART0 RX" of the RP2040.

- Raspberry Pi Pico: 1, 13 and 17
- Sparkfan Pro Micro RP2040: 1 and 29
- Other RP2040-based microcontrollers: All or some of 1, 13, 17 and 29 depending on their spec

If you use a GPIO number other than above, you need to use the Mutual UART feature implemented in the software UART.

See [Mutual UART communication](Mutual-UART-communication)

## Anchor and Partner

In PRK firmware, the half that connects to USB is called the *anchor* while it is called the master in QMK.
The *partner* is the rest of the halves.

PRK Firmware requires the same keymap.rb on both anchor and partner.

## Making the right half anchor

The default assumption is that the USB connection is on the left half.

If you want to connect the USB cable to the right half, write as follows:

```ruby
kbd.set_anchor(:right) # This should happen before `Keyboard#init_pins`, too.
```

Also, the same line above has to be written on both sides' keymap.rb.

## Sample code

- [picoruby/prk_crkbd/keymap.rb](https://github.com/picoruby/prk_crkbd/blob/main/keymap.rb)

