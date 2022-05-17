## Valid version

0.9.14+

## Description

You can get a callback when the status of "Num Lock", "Caps Lock" and "Scroll Lock" in the host device is changed.

## Usage

### If you want an LED to turn on when Caps Lock turned on

```ruby
led_pin = 25 # It's the on-board LED of Raspi Pico
gpio_init led_pin
gpio_set_dir led_pin, Keyboard::GPIO_OUT
gpio_put led_pin, 0

kbd.output_report_changed do |output|
  gpio_put led_pin, (output & Keyboard::LED_CAPSLOCK > 0 ? 1 : 0)
end
```

### Likewise, if you want RGBLED to change its color

```ruby
rgb.effect = :breath
rgb.hue = 0
rgb.speed = 25
kbd.append rgb

kbd.output_report_changed do |output|
  if output & Keyboard::LED_CAPSLOCK > 0
    rgb.hue = 100
  else
    rgb.hue = 0
  end
end
```

See [[RGBLED]] for details.

## Coverage

The block variable `output` in the above examples has the status that you can extract by bit operation:

```
output: 0b11111
              ^ Num Lock
             ^  Caps Lock
            ^   Scroll Lock
           ^    Compose
          ^     Kana
```

If a bit is `1`, the corresponding function is locked in the host PC.

|Keycode       |Alias   |Mask constant           |Value  |
|--------------|--------|------------------------|-------|
|:KC_NUMLOCK   |:KC_NLCK|Keyboard::LED_NUMLOCK   |0b00001|
|:KC_CAPSLOCK  |:KC_CAPS|Keyboard::LED_CAPSLOCK  |0b00010|
|:KC_SCROLLLOCK|:KC_SLCK|Keyboard::LED_SCROLLLOCK|0b00100|
|N/A           |N/A     |Keyboard::LED_COMPOSE   |0b01000|
|N/A           |N/A     |Keyboard::LED_KANA      |0b10000|

LED_COMPOSE and LED_KANA are implemented according to the HID descriptor though, dev team hasn't check the actual function.

