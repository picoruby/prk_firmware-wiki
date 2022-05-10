## Raspberry Pi Pico

<https://www.raspberrypi.com/products/raspberry-pi-pico>

- [PiPi Gherkin](https://github.com/picoruby/prk_pipigherkin) - Small and cute
- [Lunakey Pico](https://github.com/yoichiro/prk_lunakey_pico) - Split-type
- [Shotgun CherryPie](https://github.com/Taro-Hayashi/Shotgun-CherryPie/blob/main/README_EN.md) - Macro pad with rotary encoders and LED
- [Picobd](https://github.com/MachiaWorks/picobd) - 30% (close to 40%) small keyboard
- [cool836pico](https://github.com/telzo2000/cool836pico) - 30% alice layout keyboard
- [cool640](https://github.com/telzo2000/cool640) - 40% ortho splite keyboard

## SparkFun Pro Micro RP2040 (DEV-18288)

<https://www.sparkfun.com/products/18288>

- [meishi2](https://github.com/picoruby/prk_meishi2) - Four-keys macro pad
- [CRKBD (Corne)](https://github.com/picoruby/prk_crkbd) - Split-type with LED
- [Claw44](https://github.com/picoruby/prk_claw44) - Split-type
- [Helix rev3](https://github.com/picoruby/prk_helix_rev3) - Split-type with rotary encoders and LED
- [Amatelus73](https://gist.github.com/hasumikin/b693dcf56dcf1fffa46ec21d1129f7a0) - Duplex matrix with LED

## PICO Micro (rarely available)

<https://booth.pm/en/items/3214808>

- [Runner3680 5x7 version](https://gist.github.com/shugo/5f66fc93c01336e5d934b2bd10fc0d47) <sup>[1](#1)</sup> - Split-type

## Adafruit KB2040

<https://learn.adafruit.com/adafruit-kb2040>

- Tested with SU120

## SparkFun vs PICO Micro vs Adafruit

They are basically compatible regarding footprint but accessible GPIO numbers on the board are NOT the same.

Due to the difference, you may have to fix `keymap.rb` according to the microcontroller board you choose.

```
         USB-C                      USB-C
        ┌──────┐               ____┌──────┐____
    ┌───│      │───┐        D+ ╂   │      │   ╂ D-
  0 ╂   │      │   ╂RAW      0 ╂   │      │   ╂RAW
  1 ╂   └──────┘   ╂GND      1 ╂   └──────┘   ╂GND
 GND╂              ╂RST     GND╂              ╂RST
 GND╂              ╂VCC     GND╂              ╂VCC
  2 ╂              ╂ 29      2 ╂              ╂ 29
  3 ╂              ╂ 28      3 ╂              ╂ 28
  4 ╂              ╂ 27      4 ╂              ╂ 27
  5 ╂              ╂ 26      5 ╂              ╂ 26
  6 ╂              ╂ 22      6 ╂              ╂ 18 👀
  7 ╂              ╂ 20      7 ╂              ╂ 20
  8 ╂              ╂ 23      8 ╂              ╂ 19 👀
  9 ╂              ╂ 21      9 ╂              ╂ 10 👀
    └──────────────┘           └──────────────┘
    SparkFun RP2040            Adafruit KB2040
       PICO Micro
```

## XIAO RP2040

<https://wiki.seeedstudio.com/XIAO-RP2040>

- Tested with SU120 <sup>[2](#2)</sup>

## Waveshare RP2040-Zero 

<https://www.waveshare.com/rp2040-zero.htm> 

- [cool836rp](https://github.com/telzo2000/cool836rp) - 30% alice layout keyboard
----

<a id="1">1.</a> PICO Micro is equivalent to Pro Micro regarding footprint and capability. But the profile of Pro Micro RP2040 seems too big to be installed into Runner3680.

<a id="2">2.</a> SU120 is an expandable keyboard PCB with up to 120 keys. <https://github.com/e3w2q/su120-keyboard>

<img src="images/RP2040_boards.jpg" width="400" />

_(left: Raspberry Pi Pico / right: Sparkfun Pro Micro RP2040)_
