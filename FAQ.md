### Q: My computer sometimes doesn't recognize a PRK keyboard. Why?

That happens when you plug the USB connector *slowly*. You don't believe it happens, do you? Just try various speeds of plugging!

### Q: Can I use Sparkfun Pro Micro RP2040 as a drop-in replacement instead of a Pro Micro without having to modify the CRKBD PCB?

Yes you can! However, note that exising LEDs on your CRKBD may not blink ~~RGBLED feature is still not implemented on PRK. And don't expect your existing CRKBS's LEDs will blink even if the feature is ready~~ because the logic voltage of RP2040 is 3.3V while 5V on "normal Pro Micro". It depends on the specificaion of LED.

In terms of 3.3V, you should **be very careful** of the same thing which is warned on Proton C: https://qmk.fm/proton-c/

> Some of the PCBs compatible with Pro Micro have VCC (3.3V) and RAW (5V) pins connected (shorted) on the pcb. Using the Proton C will short 5V power from USB and regulated 3.3V which is connected directly to the MCU. Shorting those pins may damage the MCU on the Proton C.
>
> So far, it appears that this is only an issue on the Gherkin PCBs, but other PCBs may be affected in this way.
>
> In this case, you may want to not hook up the RAW pin at all.

We saw some cases where the RP2040 broke due to a circuit that shorts RAW and VCC. HelixPico is another example.

### Q: "PRKFirmware" drive is no longer mounted after installing the newest release, why?

The data in the flash ROM of RP2040 occasionally brakes for some reason.
This is not a specific issue of PRK Firmware.
It seems to happen commonly (and unexpectedly) on RP2040.

To fix it, download `flash_nuke.uf2` from the following page and install it in "RPI-RP2" drive (not "PRKFirmware" drive).

[https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html#resetting-flash-memory](https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html#resetting-flash-memory)

`flash_nuke.uf2` initializes the flash ROM and possibly solves your problem.

### Q: The newest release of PRK Firmware no longer works well while it seems to boot successfully, why?

PRK Firmware might get a breaking change. Take a good look at [CHANGELOG.md](https://github.com/picoruby/prk_firmware/blob/master/CHANGELOG.md)
