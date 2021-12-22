## Feature
- Supports split type keyboards

## In your `keymap.rb`

```ruby
kbd = Keyboard.new
kbd.split = true
kbd.uart_pin = 1
```

`kbd.uart_pin` is 1 by default, so you don't need to write it if you use GPIO1 for the other side serial communication.

The pins that can be set to kbd.uart_pin are those that have the function of "UART0 RX" on the RP2040.

- Raspberry Pi Pico: 1, 13 and 17
- Sparkfan Pro Micro RP2040: 1 and 29
- other RP2040-based microcontrollers: All or some of 1, 13, 17 and 29 

If you want to use the software-implemented UART instead of the hardware UART feature, please refer to the following:

- [Mutual UART communication](Mutual-UART-communication)

## Set keymap

This section explains how to write a keymap for the side where the USB cable is not connected.

For one hand side only, write as follows:

```ruby
kbd = Keyboard.new
kbd.init_pins(
  [ 3, 4 ],      # row0, row1,... respectively
  [ 29, 28, 27 ] # col0, col1,... respectively
)
kbd.add_layer :default  %i(
  KC_1  KC_2  KC_3 
  KC_4  KC_5  KC_6  
)
kbd.start!
```

If you connect the other hand side, write as follows:

```ruby
kbd = Keyboard.new
kbd.split = true
kbd.uart_pin = 1
kbd.init_pins(
  [ 3, 4 ],      # row0, row1,... respectively
  [ 29, 28, 27 ] # col0, col1,... respectively
)
kbd.add_layer :default  %i(
  KC_1  KC_2  KC_3  KC_A  KC_B  KC_C 
  KC_4  KC_5  KC_6  KC_D  KC_E  KC_F 
)
kbd.start!
```
