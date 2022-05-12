You can see debug print on a "USB Serial Port" (so-called "COM Port" in Windows) that will be helpful if your `keymap.rb` doesn't work well:

|Key         |Value |
|:----------:|:----:|
|Baud        |115200|
|Data bits   |8     |
|Parity      |None  |
|Stop bits   |1     |
|Flow control|None  |

![](images/serial_port.png)

## PicoRubyVM.print_alloc_stats

(Valid version: 0.9.14+)

PRK has a built-in method, `PicoRubyVM.print_alloc_stats`, which prints memory statistics of the PicoRuby virtual machine.

You can assign this method to a key as below:

```ruby
kbd.add_layer :default, %i(STATS KC_A KC_B KC_C)
kbd.define_mode_key :STATS, [ Proc.new { PicoRubyVM.print_alloc_stats }, nil, 300, nil ]
```

Tapping *STATS* key shows current statistics in the serial console like this:

```
ALLOC STATS
 TOTAL 204800
 USED   67700
 FREE  136756
 FRAG      55
```

FRAG stands for the count of fragmentation.
The other three values are in bytes.
