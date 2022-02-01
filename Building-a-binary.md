## Binary without keymap

- Make sure you have CRuby (MRI) because "Static type checking" by [Steep](https://github.com/soutaro/steep) will be invoked in the build process

- Setup Raspberry Pi Pico C/C++ SDK

  - Follow the instructions on [https://github.com/raspberrypi/pico-sdk#quick-start-your-own-project](https://github.com/raspberrypi/pico-sdk#quick-start-your-own-project)
    - Make sure you have `PICO_SDK_PATH` environment variable


- Clone the `prk_firmware` wherever you like

    ```
    git clone --recursive https://github.com/picoruby/prk_firmware.git
    ```

    Don't forget `--recursive`

- Setup (for the first time only)

    ```
    cd prk_firmware/
    rake setup
    ```

- Build

    ```
    rake
    ```

    Now you should have `prk_firmware-[version]-[date]-[hash].uf2` file in `prk_firmware/build/` directory.

## Binary with keymap (without mass storage)

You may want PRK Firmware not to be a mass storage device in case that your employer doesn't allow you to bring a USB memory 🙈

If so, you can build a binary including your keymap.rb in this way:

- Clone a keymap repository, for example, "meishi2" which is a 2x2 matrix card-shaped keyboard in `keyboards` directory

    ```
    cd prk_firmware/keyboards
    git clone https://github.com/picoruby/prk_meishi2.git
    ```

    (Optional) Edit `prk_meishi2/keymap.rb` as you wish

    ```
    rake build_with_keymap[prk_meishi2]
    ```

    Now you should have `prk_firmware-[version]-[date]-no_msc.uf2` file in `prk_firmware/keyboards/prk_meishi2/build/` directory which includes your keymap in code.

### If you prefer to use docker

See `prk_firmware/Dockerfile` for details.
