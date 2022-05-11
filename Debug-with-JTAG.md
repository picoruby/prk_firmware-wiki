The first section describes quick usage and the rest of the document are about preparation.

## Usage

- Open a PowerShell in administrator mode:
    ```sh
    usbipd wsl list
    ```
    Find a line looks like `3-2  2e8a:0004  Picoprobe, Picoprobe (Interface 2)   Not attached`.
    In this example, `3-2` is the "busid".
    ```sh
    usbipd wsl attach --busid 3-2
    ```

- Open an Ubuntu shell:
    ```sh
    sudo openocd -f interface/picoprobe.cfg -f target/rp2040.cfg
    ```

- Open one more Ubuntu shell:
    ```sh
    cd prk_firmware
    rake debug      # Builds a debug built then runs gdb-multiarch
    ```
  - In the console of gdb-multiarch:
    ```
    target remote localhost:3333  # Connects to picoprobe
    load                          # Installs prk_firmware-******.elf into the target RP2040
    continue                      # Starts PRK Firmware
    ```

## Preparation

### Prerequisites

- Ubuntu on WSL2
- Completed setup of [[Building a binary]]

Make sure that the kernel version is 5.10.60 or later.

```sh
uname -a
# for example,
# => Linux DESKTOP-FOEG8S2 5.10.102.1-microsoft-standard-WSL2 #1 SMP Wed Mar 2 00:30:59 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
#                          ^^^^^^^^
```

### Steps

- USBIPD
- Add UDEV rule
- OPENOCD
- PICOPROBE

#### USBIPD

Download and install USBIPD-WIN from [https://github.com/dorssel/usbipd-win/releases](https://github.com/dorssel/usbipd-win/releases)

Install dependencies:

(Not sure if this is the complete list or not)

```sh
sudo apt install libusb-1.0-0-dev libusb-dev gdb-multiarch libtool
```

Install the USBIP tools and hardware database:

(Valid tool version may differ at the point you see this document)

```sh
sudo apt install linux-tools-5.4.0-77-generic hwdata
sudo update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/5.4.0-77-generic/usbip 20
```

#### Add UDEV rule

```
echo 'SUBSYSTEM=="usb", ATTRS{idVendor}=="2e8a", ATTRS{idProduct}=="0004", MODE="0666"' | sudo tee /etc/udev/rules.d/60-rp2040.rules
sudo service udev restart
sudo udevadm trigger
```

#### OPENOCD

```sh
git clone https://github.com/raspberrypi/openocd.git --branch rp2040 --depth=1 --no-single-branch
cd openocd
./bootstrap
./configure --enable-picoprobe
make
sudo make install
```

#### PICOPROBE

```sh
git clone https://github.com/raspberrypi/picoprobe.git
mkdir build
cd build/
cmake ..
make
```

Install `build/picoprobe.uf2` into an RP2040 which you are using as the debugger.

## Wiring

|Target|Debugger|
|------|--------|
|SWDIO |GPIO3   |
|GND   |GND     |
|SWDCLK|GPIO2   |

Connect a USB cable to both target and debugger.

![](images/jtag-debug.png)

The example uses [RustyKeys](https://github.com/KOBA789/rusty-keys) though, you can use also a breadboard.
