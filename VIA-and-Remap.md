(This page is still a draft)

## Valid version

0.9.14+

## Basic usage

### keymap.rb

Let's configure [meishi2](https://github.com/picoruby/prk_meishi2) for example.

This is the minimum content of `keymap.rb` to use the VIA feature:

```ruby
require "via"

kbd = Keyboard.new

kbd.init_pins(
  [ 6, 7 ],   # row0, row1
  [ 28, 27 ]  # col0, col1
)

via = VIA.new
via.layer_count = 1
via.rows_size = 2
via.cols_size = 2
kbd.append via

kbd.start!
```

Don't forget writing `require "via"` at the top of the script.
It loads the VIA module that makes `VIA.new` available.

### via-conf.txt

You need to prepare `via-conf.txt` so that Remap can recognize the keyboard.

The format of the content is `[VID]:[PID]:[ProductName]`.
You can get those values in the catalog page of Remap.

At first, search "meishi2" in the catalog page of Remap: ([https://remap-keys.app/catalog?keyword=meishi2](https://remap-keys.app/catalog?keyword=meishi2))

![](images/remap.png)

Then copy VID, PID and name of the keyboard and paste them into `via-conf.txt`.

```
0xBC42:0x0003:meishi2
```

Note that the file must NOT include any other letter.

Eventually, your "PRKFirmware" drive should look like this:

![](images/via-conf.png)

### Reboot

Rebooting the microcontroller applies `via-conf.txt`.

### Remap

The configure page of Remap ([https://remap-keys.app/configure](https://remap-keys.app/configure)) will identify your keyboard. Enjoy!

![](images/remap2.png)

## Advanced usage

[TBD]

