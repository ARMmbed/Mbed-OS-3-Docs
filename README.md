# ARM Mbed OS 3

**Please note: this is the Mbed OS 3 documentation source repo and is no longer maintained. For the latest Mbed OS documentation see the [Mbed OS 5 site](https://os.mbed.com/docs/).**

Welcome to [ARM mbed OS](http://www.mbed.com/en/development/software/mbed-os/),
the new operating system for ARM microcontrollers designed for the Internet of Things.

mbed OS is modular: its code base comprises  a number of software components, combined
together and built using [yotta](http://docs.yottabuild.org/). This means the code
lives in a number of repositories, each covering a distinct functionality.

This repository contains no code. Instead, we're using it as an entry point for
mbed OS, as well as a central location for release-related documentation (such as
Known Issues), and for filing bugs that span multiple components.

## Current release

Note that this is a technology preview release, offering you early access to key
features and innovations enabling you to test functionality. This release is not
yet suitable for volume production use. The software is still maturing, and a
number of things will change, including module names, repository URLs, APIs, header
file names and configuration parameters. We'll try to mitigate the impact that these
changes have on your code where possible, but please expect backwards-incompatible
changes.

Note that in this release we're changing our version numbering scheme for mbed OS
releases, to a calendar-based (year and month YY.MM) scheme. This release (15.11)
has previously been called 3.0 in some communications

## Getting Started

We have [getting started](https://docs.mbed.com/docs/getting-started-mbed-os/en/latest/)
documentation on our [docs.mbed.com](https://docs.mbed.com/) site. It includes
an installation guide, a quick start guide and a full developer guide.

We also have a number of examples to help you get started:

## Code

The code for mbed OS can be found in these repos:

* **Core OS modules**
  * [core-util](https://github.com/ARMmbed/core-util) -- core data structures
    and primitives for the OS.
  * [minar](https://github.com/ARMmbed/minar) -- MINAR, the mbed OS event
    scheduler.
    * [minar-platform](https://github.com/ARMmbed/minar-platform) --
      platform-specific adaptation for MINAR.
      * [minar-platform-mbed](https://github.com/ARMmbed/minar-platform-mbed) --
        generic MINAR platform adaptation using the mbed HAL.
  * [ualloc](https://github.com/ARMmbed/ualloc) -- memory allocation for mbed
    OS.
    * [dlmalloc](https://github.com/ARMmbed/dlmalloc) -- Doug Lea's legendary
      memory allocator.
  * [uvisor](https://github.com/ARMmbed/uvisor) -- the mbed OS uVisor, a
    supervisory kernel for security on mbed OS.
    * [uvisor-lib](https://github.com/ARMmbed/uvisor-lib) -- APIs for interacting
      with the uVisor and incorporating it into your system.
  * [compiler-polyfill](https://github.com/ARMmbed/compiler-polyfill) -- common
    compiler intrinsics and attributes made portable across toolchains.
* **Hardware Abstraction & Drivers**
  * [cmsis-core](https://github.com/ARMmbed/cmsis-core) -- CMSIS-Core, ARM's
    official low level hardware abstraction for Cortex-M.
    * [cmsis-core-freescale](https://github.com/ARMmbed/cmsis-core-freescale) --
      generic implementation of CMSIS-Core for Freescale devices.
      * [cmsis-core-k64f](https://github.com/ARMmbed/cmsis-core-k64f) --
        specific implementation for the Freescale K64F MCU family.
    * [cmsis-core-nordic](https://github.com/ARMmbed/cmsis-core-nordic) --
      generic implementation of CMSIS-Core for Nordic Semi devices.
      * [cmsis-core-nrf51822](https://github.com/ARMmbed/cmsis-core-nrf51822) --
        specific implementation for the Nordic nRF51 family.
    * [cmsis-core-st](https://github.com/ARMmbed/cmsis-core-st) -- generic
      implementation of CMSIS-Core for ST devices.
      * [cmsis-core-stm32f4](https://github.com/ARMmbed/cmsis-core-stm32f4) --
        generic implementation of CMSIS-Core for the STM32F4 family.
        * [cmsis-core-stm32f429xi](https://github.com/ARMmbed/cmsis-core-stm32f429xi)
          -- specific implementation of CMSIS-Core for the STM32F429.
    * [cmsis-core-silabs](https://github.com/ARMmbed/cmsis-core-silabs) --
      generic implementation of CMSIS-Core for Silicon Labs devices.
      * [cmsis-core-efm32gg](https://github.com/ARMmbed/cmsis-core-efm32gg)
        -- specific implementation of CMSIS-Core for the EFM32 Giant Gecko family of MCUs.
      * [cmsis-core-efm32hg](https://github.com/ARMmbed/cmsis-core-efm32hg)
        -- specific implementation of CMSIS-Core for the EFM32 Happy Gecko family of MCUs.
  * [mbed-drivers](https://github.com/ARMmbed/mbed-drivers) -- abstract drivers
    for common hardware peripherals and communications interfaces (SPI, I2C
    etc). Provides a higher level interface than the mbed HAL; these are the
    APIs that applications should use.
  * [mbed-hal](https://github.com/ARMmbed/mbed-hal) -- the mbed Hardware
    Abstraction Layer (HAL).
    * [mbed-hal-freescale](https://github.com/ARMmbed/mbed-hal-freescale) --
      implementation of the mbed HAL for Freescale devices.
      * [mbed-hal-ksdk-mcu](https://github.com/ARMmbed/mbed-hal-ksdk-mcu) --
        implementation for Freescale MCUs using Freescale KSDK.
      * [mbed-hal-k64f](https://github.com/ARMmbed/mbed-hal-k64f) --
        implementation for the K64F.
        * [mbed-hal-frdm-k64f](https://github.com/ARMmbed/mbed-hal-frdm-k64f) --
          specific implementation for the Frdm-K64F development board.
    * [mbed-hal-nordic](https://github.com/ARMmbed/mbed-hal-nordic) --
      implementation for Nordic Semi devices.
      * [mbed-hal-nrf51822-mcu](https://github.com/ARMmbed/mbed-hal-nrf51822-mcu)
        -- implementation for the nRF51822 wireless MCU.
        * [mbed-hal-mkit](https://github.com/ARMmbed/mbed-hal-mkit) --
          implementation for the Nordic nRF51822-mKIT development board.
    * [mbed-hal-st](https://github.com/ARMmbed/mbed-hal-st) -- implementation
      for ST devices
      * [mbed-hal-st-stm32f4](https://github.com/ARMmbed/mbed-hal-st-stm32f4) --
        implementation for the STM32F4 family.
        * [mbed-hal-st-stm32cubef4](https://github.com/ARMmbed/mbed-hal-st-stm32cubef4)
          -- implementation for ST MCUs using the STM32CubeF4 library.
          * [mbed-hal-st-stm32f429zi](https://github.com/ARMmbed/mbed-hal-st-stm32f429zi)
            -- implementation for the STM32F429.
    * [mbed-hal-silabs](https://github.com/ARMmbed/mbed-hal-silabs) --
      implementation for Silicon Labs devices.
      * [mbed-hal-efm32gg](https://github.com/ARMmbed/mbed-hal-efm32gg)
        -- implementation for the EFM32 Giant Gecko MCUs.
      * [mbed-hal-efm32hg](https://github.com/ARMmbed/mbed-hal-efm32hg)
        -- implementation for the EFM32 Happy Gecko MCUs.
  * [atmel-rf-driver](https://github.com/ARMmbed/atmel-rf-driver) -- PHY driver
    for the Atmel AT86RF2xx series of 802.15.4 radios, for mesh networking in
    mbed OS.
* **Networking & Connectivity**
  * [sal](https://github.com/ARMmbed/sal) -- mbed OS's socket abstraction layer
    (SAL). This enables the various ARM and partner networking stacks to have a
    common interface.
    * [sal-iface-eth](https://github.com/ARMmbed/sal-iface-eth) -- support for
      Ethernet interfaces.
    * [sal-iface-6lowpan](https://github.com/ARMmbed/sal-iface-6lowpan) --
      support for 6LoWPAN network interfaces.
    * [sal-stack-lwip](https://github.com/ARMmbed/sal-stack-lwip) -- the third
      party LwIP (lightweight IP) networking stack. Currently this only supports
      IPv4 over ethernet or WiFi, and will be replaced by a new IPv4/v6 unified
      stack in the future.
      * [sal-driver-lwip-k64f-eth](https://github.com/ARMmbed/sal-driver-lwip-k64f-eth)
        -- driver for the Freescale K64F ethernet interface in LwIP.
    * [sal-stack-nanostack](https://github.com/ARMmbed/sal-stack-nanostack) --
      ARM's NanoStack 6LoWPAN/mesh networking stack.
      * [sal-stack-nanostack-eventloop](https://github.com/ARMmbed/sal-stack-nanostack-eventloop)
        -- event loop integration for NanoStack.
  * [sockets](https://github.com/ARMmbed/sockets) -- high level portable socket
    layer (sitting on top of the SAL).
  * [ble](https://github.com/ARMmbed/ble) -- APIs for using Bluetooth Low
    Energy.
    * [ble-nrf51822](https://github.com/ARMmbed/ble-nrf51822) -- implementation
      of the BLE APIs for Nordic nRF51822.
  * [mbed-mesh-api](https://github.com/ARMmbed/mbed-mesh-api) -- APIs for
    initialising and using the mesh network.
  * [mbedtls](https://github.com/ARMmbed/mbedtls) -- [mbed TLS](https://tls.mbed.org/),
    the SSL/TLS stack (including cryptographic and certification handling
    functionality).
* **mbed Client** -- means for connecting to and managing mbed OS devices
  with mbed Device Server or mbed Device Connector. This includes the OMA
  LWM2M client, CoAP protocol implementations, and related functionality.
  * [mbed-client-c](https://github.com/ARMmbed/mbed-client-c) -- core library
    in C.
  * [mbed-client](https://github.com/ARMmbed/mbed-client) -- C++ API (use this
    one rather than the C one, as it's much easier to use correctly).
  * [mbed-client-mbed-os](https://github.com/ARMmbed/mbed-client-mbed-os) --
    mbed OS specific implementation for mbed Client.
  * [mbed-client-mbedtls](https://github.com/ARMmbed/mbed-client-mbedtls) --
    mbed TLS specific implementation for mbed Client.
* **Tools & Utilities**
  * [yotta](https://github.com/ARMmbed/yotta) -- component management, configuration
    and build. **Start here**, as you _need_ to get familiar with this tool to use
    mbed OS!
  * [helloyotta](https://github.com/ARMmbed/helloyotta) -- example project for yotta.
  * [greentea](https://github.com/ARMmbed/greentea) -- regression testing tool.
  * [htrun](https://github.com/ARMmbed/htrun) -- test runner for host-supervised
    tests.
  * [mbed-ls](https://github.com/ARMmbed/mbed-ls) -- utility for detecting and listing
    mbed Enabled development boards attached to the development host.
  * [utest](https://github.com/ARMmbed/utest) -- simple test harness for C++ with greentea integration.
  * [unity](https://github.com/ARMmbed/unity) -- utest compatible test macros from the unity test framework

The following modules define the [yotta targets](http://docs.yottabuild.org/tutorial/targets.html)
we support building mbed OS for. Currently we only support the following boards:

1. [Freescale FRDM-K64F](http://www.mbed.com/en/development/hardware/boards/freescale/frdm_k64f/)
   board -- a powerful and flexible development board based around the  Freescale
   K64F Kinetis MK64FN1M0VLL12 MCU. It has a high performance ARM® Cortex™-M4
   Core (with Floating point unit and DSP extensions), clocked at up to 120MHz,
   paired with 256KB RAM, 1MB FLASH and a wide array of peripherals. This is
   currently the best supported development board for mbed OS; networking
   (ethernet, and mesh with a 802.15.4 radio shield), cryptographic
   acceleration, and other features are supported already in this beta release.
   You can use either ARM's C/C++ compiler, or the open source GCC compiler.
  * [target-frdm-k64f-armcc](https://github.com/ARMmbed/target-frdm-k64f-armcc)
  * [target-frdm-k64f-gcc](https://github.com/ARMmbed/target-frdm-k64f-gcc)
1. [ST STM32F429I Discovery](http://www.st.com/web/catalog/tools/FM116/SC959/SS1532/PF259090)
   board -- based on the STM32F429ZIT6 microcontroller with 2 MB of Flash memory,
   256 KB of RAM, and a Cortex-M4 (with FPU and DSP) that can be clocked up to
   180 MHz. **Currently this board and MCU is not as well supported as the K64F,
   especially if you want to use uVisor, networking or mbed TLS (which are not yet
   supported).**
  * [target-st-stm32f429i-disco](https://github.com/ARMmbed/target-st-stm32f429i-disco)
  * NOTE: we don't yet support armcc for this target.
1. [Nordic nRF51-DK](https://developer.mbed.org/platforms/Nordic-nRF51-DK/)
   board -- based around the Nordic nRF51822 Bluetooth Smart/Low Energy device,
   this has a Cortex-M0 core, with 256 kB of flash and 16-32 kB of RAM. Due to
   much of the RAM being reserved for Nordic's "SoftDevice" BLE stack, only a
   small amount of RAM is available for mbed OS and your application, thus this
   board is best for simpler applications such as BLE peripherals.
  * [target-nrf51dk-gcc](https://github.com/rgrover/target-nrf51dk-gcc)
  * [target-nrf51dk-armcc](https://github.com/ARMmbed/target-nrf51dk-armcc)
1. [EFM32 Giant Gecko STK](https://www.mbed.com/en/development/hardware/boards/siliconlabs/efm32giantgecko/)
   board –- Low-power Cortex-M3 with 1 MB of flash, 128 kB of RAM and a lot of
   low-power peripherals. This board allows development of bigger applications
   with long battery life, such as wearables. **Currently this board and MCU is
   not as well supported as the K64F, especially if you want to use uVisor,
   networking or mbed TLS (which are not yet supported).**
  * [target-efm32gg-stk-gcc](https://github.com/ARMmbed/target-efm32gg-stk-gcc)
  * NOTE: we don't yet support armcc for this target.
1. [EFM32 Happy Gecko STK](https://www.mbed.com/en/development/hardware/boards/siliconlabs/efm32happygecko/)
   board –- Low-power Cortex-M0+ with 64 kB of flash and 8 kB of RAM and a lot
   of low-power peripherals. This board is better suited for development of
   smaller nodes with power and space constraints. **Currently this board and
   MCU is not as well supported as the K64F, especially if you want to use
   uVisor, networking or mbed TLS (which are not yet supported).**
  * [target-efm32hg-stk-gcc](https://github.com/ARMmbed/target-efm32hg-stk-gcc)
  * NOTE: we don't yet support armcc for this target.

Finally, there are a number of yotta targets that provide shared functionality:

* [target-mbed-armcc](https://github.com/ARMmbed/target-mbed-armcc)
* [target-mbed-gcc](https://github.com/ARMmbed/target-mbed-gcc)


* [mbed-client-examples](https://github.com/ARMmbed/mbed-client-examples)
* [mbed-example-network](https://github.com/ARMmbed/mbed-example-network)
* [example-asynch-i2c](https://github.com/ARMmbed/example-asynch-i2c)
* [example-asynch-serial](https://github.com/ARMmbed/example-asynch-serial)
* [example-asynch-spi](https://github.com/ARMmbed/example-asynch-spi)
* [mbed-client-example-6lowpan](https://github.com/ARMmbed/mbed-client-example-6lowpan)
* [uvisor-helloworld](https://github.com/ARMmbed/uvisor-helloworld)
* [ble-examples](https://github.com/ARMmbed/ble-examples)
