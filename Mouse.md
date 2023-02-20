## Valid version

0.9.21+

## Description

`Mouse` class in PRK Firmware drives an HID mouse.
You can use various hardware such as Trackball, Pointing stick, Touchpad, and even Joystick.
You need to write a bunch of low-level code by using one of the peripheral classes between `I2C`, `SPI` and `ADC`.
PicoRuby ecosystem doesn't support a specific sensor in a form of a core library though, it is not such a difficult thing to write a mouse code (I wish you'll agree).

## Examples

### I2C

- Trackball: AZ1UBALL or PIM447

```
require "i2c"
require "mouse"

i2c = I2C.new
mouse = Mouse.new(driver: i2c)
```

### SPI

- Sensor: PWM3360DM-T2QU

```
require "spi"
require "mouse"

spi = SPI.new
mouse = Mouse.new(driver: spi)
```

### ADC and Joystick

- Joystick: RKJXV122400R

```
require "adc"
require "mouse"

adc_x = ADC.new
adc_y = ADC.new
mouse = Mouse.new(driver: [adc_x, adc_y])
mouse.task do |keyboard, mouse|
  # PicoRuby still can't compile `.map(&:read)`. Sorry!
  x, y = mouse.driver.map { |adc| adc.read }
end
```

## Keycodes

Configure mouse keys in your keymap through `Keyboard#add_layer`.
See [[Layers and mode key]]

Generally, `:KC_MS_BTN1` and `:KC_MS_BTN2` should work as "left click" and "right click" respectively.

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


## Split-type

If your keyboard is a split-type along with a trackpad(s), it won't work if it's on the partner half.

See also [[Split-type keyboard]].
