## Valid version

0.9.[TBD]+

## Usage

This example is going to configure a gamepad that has a 2D analog stick and four buttons:

```ruby
require “joystick”

kbd = Keyboard.new

joystick = Joystick.new(
  {
    :x => 26,
    :y => 27
  }
)
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
 - Available GPIO pins: `26`, `27`, `28`, and `29`
  
Thus, you can configure up to four axes.

## D-pad

A four-way digital cross, so-called “D-pad”, can be configured like this:

```
kbd.add_layer :default, [
  :JS_HAT_LEFT, :JS_HAT_DOWN, :JS_HAT_UP, :JS_HAT_RIGHT
]
```

In addition to that, you always need to append `joystick` initialized with a hash object even if you don’t have any analog stick as the code shows:

```
# Caution:
# Eliminating a parenthesis doesn’t work due to syntax rule of Ruby
#   Joystick.new {}
#   => raises an error
joystick = Joystick.new({})
kbd.append joystick
```

## Debounce

Depending on the game you play, you may want the debounce algorithm not to work.

```ruby
kbd.set_debounce :none
```

Above code turns off the debouncer.

See [[Debounce]] for details.
