## Prerequisite

As far as the author knows, building a PRK binary, or to be exact, preparing a build environment can be done in only Linux. WSL2 should work, too.

If you are a macOS user, try docker instead. (See [[Docker]])

## Binary without keymap

- Make sure you have CRuby (MRI) because "Static type checking" by [Steep](https://github.com/soutaro/steep) will be invoked in the build process

- Setup Raspberry Pi Pico C/C++ SDK

  - Follow the instructions on [https://github.com/raspberrypi/pico-sdk#quick-start-your-own-project](https://github.com/raspberrypi/pico-sdk#quick-start-your-own-project)
    - Additionally, you need to run `git submodule update --init` in `pico-sdk` directory so that `tinyusb` submodule locates in it
    - Make sure you have `PICO_SDK_PATH` environment variable


- Clone the `prk_firmware` wherever you like

    (be sure to add `--recursive`)

    ```sh
    git clone --recursive https://github.com/picoruby/prk_firmware.git
    ```

- Setup (for the first time only)

    ```sh
    cd prk_firmware/
    rake setup
    ```

- Build

    ```sh
    rake
    ```

    Now you should have `prk_firmware-[version]-[date]-[hash].uf2` file in `prk_firmware/build/` directory.

## Binary with keymap (without mass storage)

You may want PRK Firmware not to be a mass storage device in case that your employer doesn't allow you to bring a USB memory 🙈

If so, you can build a binary including your keymap.rb in this way:

- Clone a keymap repository, for example, "meishi2" which is a 2x2 matrix card-shaped keyboard in `prk_firmware/keyboards` directory

    ```sh
    cd keyboards
    git clone https://github.com/picoruby/prk_meishi2.git
    ```

- Build

    ```sh
    cd .. # back to prk_firmware/
    rake build_with_keymap[prk_meishi2]
    ```

    Now you should have `prk_firmware-[version]-[date]-no_msc.uf2` file in `prk_firmware/keyboards/prk_meishi2/build/` directory which includes your keymap in code.

## Files you should learn

You are likely having problems while developing PRK.

These files may give you a clue regarding PRK build system:

```
prk_firmware
 ├── CMakeLists.txt
 ├── Rakefile
 ├── lib
 │    └── CMakeLists.txt
 └── src
      └── ruby
           └── Rakefile
```

### Resources

- CMake: https://cmake.org/documentation/
- Rake: https://ruby.github.io/rake/
