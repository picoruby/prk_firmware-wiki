## Valid version

|Feature|Version|
|----|----|
|Loading prebuilt libraries|0.9.14+ (maybe)|
|Loading external libraries|0.9.23+|

This page explains the loading external libraries feature introduced in 0.9.23.

## Description

CRuby loads external libraries using `Kernel.#require` and `Kernel.#load`.
Likewise, PicoRuby has `require` and `load`.
You can reuse a Ruby script by those methods.

## Gist

- Put your library files in the `/lib` directory in "PRK DRIVE"
  - It may be easier to understand if you say `$LOAD_PATH` is `["/lib"]`
- The library file has to have `.rb` or `.mrb` extention. eg: `my_library.rb`
- `require` method supplements an extension, so just write `require "my_library"`
- `load` method only accepts a full path name. eg: `load "/path/to/my_library.rb"`
- `require` does not load the same library more than once while `load` does as many times as you call
- `.rb` file will be compiled into mruby VM code in microcontrller on the fly
  - A large Ruby file is more likely to cause Out of Memory
  - In such case, precompled mrb file will help
  - You can get `my_library.mrb` by `mrbc my_library.rb` or `picorbc my_library.rb`
    - Make sure to use the same version of the compiler as the PicoRuby in PRK
    - As of PRK 0.9.23, the corresponding version of mruby (picoruby) is 3.2.x

## Example

```ruby
# Library for ADNS-5050 optical sensor
# filepath: /lib/adns5050.rb
require "mouse"
require "spi"

class ADNS5050
  def initialize(sck_pin:, copi_pin:, cipo_pin:, cs_pin:)
    spi = SPI.new(unit: :BITBANG, sck_pin: sck_pin, copi_pin: copi_pin, cipo_pin: cipo_pin, cs_pin: cs_pin)
    mouse = Mouse.new(driver: spi)
    mouse.task do |mouse, keyboard|
      next if mouse.driver.power_down
      y, x = mouse.driver.select do |spi|
        spi.write(0x63) # Motion_Burst
        spi.read(2).bytes
      end
      if 0 < x || 0 < y
        x = 0x7F < x ? (~x & 0xff) + 1 : -x
        y = 0x7F < y ? (~y & 0xff) + 1 : -y
        if keyboard.layer == :lower
          x = 0 < x ? 1 : (x < 0 ? -1 : x)
          y = 0 < y ? 1 : (y < 0 ? -1 : y)
          USB.merge_mouse_report(0, 0, 0, y, -x)
        else
          mod = keyboard.modifier
          if 0 < mod & 0b00100010
            # Shift key pressed -> Horizontal or Vertical only
            x.abs < y.abs ? x = 0 : y = 0
          end
          if 0 < mod & 0b01000100
            # Alt key pressed -> Fix the move amount
            x = 0 < x ? 2 : (x < 0 ? -2 : x)
            y = 0 < y ? 2 : (y < 0 ? -2 : y)
          end
          USB.merge_mouse_report(0, y, x, 0, 0)
        end
      end
    end
    return mouse
  end
end
```

```ruby
# filepath: /keyboard.rb
require "adns5050"

kbd = Keyboard.new

kbd.append ADNS5050.new(sck_pin: 23, copi_pin: 8, cipo_pin: 8, cs_pin: 9)

kbd.start!
```

## Pro tip

When you make font data for OLED, in general, remember that String objects are more memory-effective than Array objects.

```ruby
# Array object
FONT_DATA = [
  0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
  0x3E, 0x5B, 0x4F, 0x5B, 0x3E, 0x00,
  ...
]
```

```ruby
# String object
FONT_DATA = "\x00\x00\x00\x00\x00\x00\x3E\x5B\x4F\x5B\x3E\x00..."
```

If OOM still occurs, splitting the data may work:

```ruby
# Split String objects
FONT_DATA_1 = "\x00\x00\x00\x00\x00\x00\x3E\x5B\x4F\x5B\x3E\x00..."
FONT_DATA_2 = "\xC0\x00\xDC\xD7\xDE\xDE\xDE\xD7\xDC\x00\xC0\x00..."
FONT_DATA = FONT_DATA_1 + FONT_DATA_2
```

Needless to say, precompiled `.mrb` is even more effective.

