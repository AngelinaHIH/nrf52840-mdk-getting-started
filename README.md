
The nrf52840-mdk can support Zephyr kernel.

## Download GNU ARM Tools

Download cross tool at:

https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads

Add the following environment variables to `~/.bash_profile`:

```
export GNUARMEMB_TOOLCHAIN_PATH="<path to install directory>/gcc-arm-none-eabi-6-2017-q2-update"
export ZEPHYR_TOOLCHAIN_VARIANT=gnuarmemb
```

## Download Zephyr

```
$ git clone https://github.com/zephyrproject-rtos/zephyr.git
$ brew install cmake ninja dfu-util doxygen qemu dtc python3 gperf
$ cd ~/zephyr
$ pip3 install --user -r scripts/requirements.txt
```

Add variable configs to `~/.bash_profile`:

```
export PATH="/usr/local/opt/ncurses/bin:$PATH"
export PATH="/usr/local/opt/sqlite/bin:$PATH"
```

## Install PyOCD

```
$ pip3 install -U pyocd
```

## Build IoT Application

```
$ cd <path-to-zephyr>
$ source zephyr-env.sh
```

Install Zephyr `west`:

```
$ pip3 install west --user
```

Download the official `nrf52840-mdk` sdk and initialize the `west` environment:

```
$ git clone https://github.com/makerdiary/nrf52840-mdk
$ cd <path-to-your-nrf52840-mdk>/nrf52840-mdk/examples/zephyr/blinky
$ west init
```

Create a `build` directory and start the project build:

``
$ mkdir build; cd build
$ cmake -GNinja -DBOARD=nrf52840_mdk ..
$ ninja
$ ninja flash
```

You can use `west` directly:

```
$ cd <path-to-your-nrf52840-mdk>/nrf52840-mdk/examples/zephyr/blinky
$ west init
$ west build -b nrf52840_mdk 
$ west flash
```

## Build JerryScript on Zephyr

```
$ cd jerryscript
$ make -f ./targets/zephyr/Makefile.zephyr BOARD=nrf52840_mdk
```
