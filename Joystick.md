## Valid version

0.9.15+

## Usage

This example is going to configure a gamepad that has a 2D analog stick and four buttons:

```ruby
require "joystick"

kbd = Keyboard.new

joystick = Joystick.new({
  :x => {
    pin: 26,       # Required: Pin number
    invert: false, # Optional: Inverts direction if true. Default: false
    magnify: 1.3   # Optional: Magnifies sensitivity. Default: 1.0
  },
  :y => {
    pin: 27
  }
})
kbd.append joystick

kbd.init_pins(
  [ 6, 7 ],   # row0, row1
  [ 8, 9 ]    # col0, col1
)
kbd.add_layer :default, [
  :JS_BUTTON0, :JS_BUTTON1,
  :JS_BUTTON2, :JS_BUTTON3
]

kbd.start!
```

Buttons are available up to 32 from `:JS_BUTTON0` to `:JS_BUTTON31`

## Analog joysticks

As the example shows, `Keyboard.new` accepts any pairs of axis symbol and GPIO pin listed below:

 - Available axis symbols: `:x`, `:y`, `:z`, `:rz`, `:rx`, and `:ry`
 - Available GPIO pins of RP2040: `26`, `27`, `28`, and `29`

Thus, you can configure up to four axes.

### Suppressing drift from the center

Analog sticks often have a drift that causes unwanted movement even when you aren't touching a stick.

PRK ignores a stick value that is less than a threshold named `drift_suppression`.

You can vary the value as follows:

```ruby
joystick.drift_suppression = 18  # Default: 5. Valid value: 0..100
```

In this case, an analog stick value within `-18..18` is going to be ignored.

The range of an analog stick value is from `-128` to `127`.
`0` is the center, accordingly.

#### A side effect of configuring `drift_suppression = 0`

If your game controller also has a keyboard function in addition to a joystick and you've configured `joystick.drift_suppression = 0` (or such a small value), you will probably have trouble with it.

Because an HID Game Controller status will be incessantly reported to the host PC due to drifting, reporting an HID Keyboard status is going to be considerably interrupted.

## D-pad

A four-way digital cross, so-called "D-pad", can be configured like this:

```ruby
kbd.add_layer :default, [
  :JS_HAT_LEFT, :JS_HAT_DOWN, :JS_HAT_UP, :JS_HAT_RIGHT
]
```

In addition to that, you always need to append `joystick` initialized without argument even if you don’t have an ANALOG stick:

```ruby
joystick = Joystick.new
kbd.append joystick
```

## Debounce

Depending on the game you play, you may want the debounce algorithm not to work.

```ruby
 kbd.set_debounce :none
#^^^
# Note that it's `kbd`, not `joystick`
```

Above code turns off the debouncer.

See [[Debounce]] for details.

## Split-type

If your keyboard is a split-type along with a joystick (are you sure?!), an analog stick won't work in case it's on the partner half.

See also [[Split-type keyboard]].
