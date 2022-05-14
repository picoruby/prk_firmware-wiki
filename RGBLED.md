## Valid version

0.9.6+

## Effect modes:
- `:swirl`
- `:rainbow_mood`
- `:breath`
- `:nokogiri`
 
## Keycodes:
|keycode|alias|functionality|swirl|rainbow_mood|breath|nokogiri|
| ---- | ---- | ---- | :--: | :--: | :--: | :--: |
|RGB_TOG||Toggle On and Off|||||
|RGB_MODE_FORWARD|RGB_MOD|Cycle through modes|||||
|RGB_MODE_REVERSE|RGB_RMOD|Reverse direction of _FORWARD|||||
|RGB_HUI||Increase hue (tone)|||✔|✔|
|RGB_HUD||Decrease hue|||✔|✔|
|RGB_SAI||Increase saturation (density)|✔|✔|✔|✔|
|RGB_SAD||Decrease saturation|✔|✔|✔|✔|
|RGB_VAI||Increase value (brightness)|✔|✔|✔|✔|
|RGB_VAD||Decrease value|✔|✔|✔|✔|
|RGB_SPI||Increase effect speed|✔|✔|✔|✔|
|RGB_SPD||Decrease effect speed|✔|✔|✔|✔|

## In your `keymap.rb`

```ruby
rgb = RGB.new(
  0,    # pin number
  6,    # size of underglow pixel
  21,   # size of backlight pixel
  false # 32bit data will be sent to a pixel if true while 24bit if false
)
rgb.effect     = :breath
rgb.speed      = 31  # 1-31  / default: 22
rgb.hue        = 10  # 0-100 / default: 0
rgb.saturation = 100 # 0-100 / default: 100
rgb.value      = 10  # 1-31  / default: 13

kbd.append rgb # `kbd` is an instance of Keyboard class that should be newed in advance
```
