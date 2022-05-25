This page tells you to prepare a development environment on your host computer.

If you want to use docker instead, see [[Docker]].

## Prerequisites

### Ruby

You need CRuby (MRI) because "Static type checking" by [Steep](https://github.com/soutaro/steep) will be invoked in the build process.

See the page below and install CRuby if you don't have it yet:

[https://www.ruby-lang.org/en/downloads/](https://www.ruby-lang.org/en/downloads/)

### Raspberry Pi Pico C/C++ SDK

The following material includes everything you need:

[https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)

You need both `pico-sdk` cloned and toolchain for your platform.

#### Linux (WSL2)

- Follow the instruction on "Chapter 2. The SDK" of the material

#### macOS

- Follow the instruction on "9.1.1. Installing the Toolchain"
- In addition to that, you probably need to read "Chapter 2. The SDK" to grab the overall
- Preparing VSCode is optional. You don't need it if you just want to build PRK Firmware

#### Windows

- Follow the instruction on "9.2.1. Installing the Toolchain"
- In addition to that, you probably need to read "Chapter 2. The SDK" to grab the overall

### Checkpoints

Regardless of your platform, confirm that you have these requirements:

- Submodules of pico-sdk. Make sure to run `git submodule update --init` in `pico-sdk` directory
  - You will sometimes need to upgrade the SDK due to inconsistency between the SDK and the newest PRK Firmware:
    ```sh
    git pull origin master --recurse-submodules
    ```

- `PICO_SDK_PATH` environment variable. Read the material above again if you are not sure

## PRK Firmware

- Clone the `prk_firmware` wherever you like

    (be sure to add `--recursive`)

    ```sh
    git clone --recursive https://github.com/picoruby/prk_firmware.git
    ```

- Setup for the first time

    ```sh
    cd prk_firmware/
    rake setup
    ```

- Upgrading the PRK

    ```sh
    git pull origin master
    rake deep_clean
    rake setup
    ```

### Binary without keymap

A binary that doesn't include a keymap is the same format as the releases of PRK.

- Build

    ```sh
    rake
    ```

    Now you should have `prk_firmware-[version]-[date]-[hash].uf2` file in `prk_firmware/build/` directory.

- Clean the build

    ```sh
    rake clean
    ```

### Binary with keymap (without mass storage)

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

- Clean the build

    ```sh
    rake clean_with_keymap[prk_meishi2]
    ```

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
