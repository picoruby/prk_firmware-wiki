- Q: Can I use Sparkfun Pro Micro RP2040 as a drop-in replacement instead of a Pro Micro without having to modify the CRKBD PCB?

  A: Yes you can! However, note that exising LEDs on your CRKBD may not blink ~~RGBLED feature is still not implemented on PRK. And don't expect your existing CRKBS's LEDs will blink even if the feature is ready~~ because the logic voltage of RP2040 is 3.3V while 5V on "normal Pro Micro". It depends on the specificaion of LED.

  In terms of 3.3V, you should be careful of the same thing which is warned on Proton-C: https://qmk.fm/proton-c/

  > Some of the PCBs compatible with Pro Micro have VCC (3.3V) and RAW (5V) pins connected (shorted) on the pcb. Using the Proton C will short 5V power from USB and regulated 3.3V which is connected directly to the MCU. Shorting those pins may damage the MCU on the Proton C.
  >
  > So far, it appears that this is only an issue on the Gherkin PCBs, but other PCBs may be affected in this way.
  >
  > In this case, you may want to not hook up the RAW pin at all.

- Q: PRK Firmware no longer works after pulling the newest master branch, why?

  A: It likely happens when submodules like PicoRuby were also updated, try `git submodule update --recursive`. Besides, PRK may get a breaking change as it is still a beta version. Take a good look at [CHANGELOG.md](CHANGELOG.md)
