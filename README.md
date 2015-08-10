# ARM mbed OS

Welcome to ARM mbed OS, a new operating system for ARM microcontrollers,
designed for the Internet of Things.

mbed OS is comprised of a number of software components, combined together and
built using [yotta](http://docs.yottabuild.org/). This means code lives in a
number of repositories. This repository serves as an entry point for mbed OS,
and as a central location for documentation, and for filing bugs which span
multiple components.

The code for mbed OS can be found in these repos:

* [atmel-rf-driver](https://github.com/ARMmbed/atmel-rf-driver)
* [ble](https://github.com/ARMmbed/ble)
* [ble-nrf51822](https://github.com/ARMmbed/ble-nrf51822)
* [cmsis-core](https://github.com/ARMmbed/cmsis-core)
* [cmsis-core-freescale](https://github.com/ARMmbed/cmsis-core-freescale)
* [cmsis-core-k64f](https://github.com/ARMmbed/cmsis-core-k64f)
* [cmsis-core-nordic](https://github.com/ARMmbed/cmsis-core-nordic)
* [cmsis-core-nrf51822](https://github.com/ARMmbed/cmsis-core-nrf51822)
* [cmsis-core-st](https://github.com/ARMmbed/cmsis-core-st)
* [cmsis-core-stm32f4](https://github.com/ARMmbed/cmsis-core-stm32f4)
* [cmsis-core-stm32f429xi](https://github.com/ARMmbed/cmsis-core-stm32f429xi)
* [compiler-polyfill](https://github.com/ARMmbed/compiler-polyfill)
* [core-util](https://github.com/ARMmbed/core-util)
* [cpputest](https://github.com/ARMmbed/cpputest)
* [dlmalloc](https://github.com/ARMmbed/dlmalloc)
* [helloyotta](https://github.com/ARMmbed/helloyotta)
* [mbed-client](https://github.com/ARMmbed/mbed-client)
* [mbed-client-c](https://github.com/ARMmbed/mbed-client-c)
* [mbed-client-mbed-os](https://github.com/ARMmbed/mbed-client-mbed-os)
* [mbed-client-mbedtls](https://github.com/ARMmbed/mbed-client-mbedtls)
* [mbed-drivers](https://github.com/ARMmbed/mbed-drivers)
* [mbed-hal](https://github.com/ARMmbed/mbed-hal)
* [mbed-hal-frdm-k64f](https://github.com/ARMmbed/mbed-hal-frdm-k64f)
* [mbed-hal-freescale](https://github.com/ARMmbed/mbed-hal-freescale)
* [mbed-hal-k64f](https://github.com/ARMmbed/mbed-hal-k64f)
* [mbed-hal-ksdk-mcu](https://github.com/ARMmbed/mbed-hal-ksdk-mcu)
* [mbed-hal-mkit](https://github.com/ARMmbed/mbed-hal-mkit)
* [mbed-hal-nordic](https://github.com/ARMmbed/mbed-hal-nordic)
* [mbed-hal-nrf51822-mcu](https://github.com/ARMmbed/mbed-hal-nrf51822-mcu)
* [mbed-hal-st](https://github.com/ARMmbed/mbed-hal-st)
* [mbed-hal-st-stm32cubef4](https://github.com/ARMmbed/mbed-hal-st-stm32cubef4)
* [mbed-hal-st-stm32f4](https://github.com/ARMmbed/mbed-hal-st-stm32f4)
* [mbed-hal-st-stm32f429zi](https://github.com/ARMmbed/mbed-hal-st-stm32f429zi)
* [mbed-ls](https://github.com/ARMmbed/mbed-ls)
* [mbed-mesh-api](https://github.com/ARMmbed/mbed-mesh-api)
* [mbedtls](https://github.com/ARMmbed/mbedtls)
* [minar](https://github.com/ARMmbed/minar)
* [minar-platform](https://github.com/ARMmbed/minar-platform)
* [minar-platform-mbed](https://github.com/ARMmbed/minar-platform-mbed)
* [sal](https://github.com/ARMmbed/sal)
* [sal-driver-lwip-k64f-eth](https://github.com/ARMmbed/sal-driver-lwip-k64f-eth)
* [sal-iface-6lowpan](https://github.com/ARMmbed/sal-iface-6lowpan)
* [sal-iface-eth](https://github.com/ARMmbed/sal-iface-eth)
* [sal-stack-lwip](https://github.com/ARMmbed/sal-stack-lwip)
* [sal-stack-nanostack](https://github.com/ARMmbed/sal-stack-nanostack)
* [sal-stack-nanostack](https://github.com/ARMmbed/sal-stack-nanostack)
* [sal-stack-nanostack-eventloop](https://github.com/ARMmbed/sal-stack-nanostack-eventloop)
* [sockets](https://github.com/ARMmbed/sockets)
* [ualloc](https://github.com/ARMmbed/ualloc)
* [uvisor](https://github.com/ARMmbed/uvisor)
* [uvisor-helloworld](https://github.com/ARMmbed/uvisor-helloworld)
* [uvisor-lib](https://github.com/ARMmbed/uvisor-lib)

The following modules define the [yotta targets](http://docs.yottabuild.org/tutorial/targets.html)
we support building mbed OS for:

* [target-frdm-k64f-armcc](https://github.com/ARMmbed/target-frdm-k64f-armcc)
* [target-frdm-k64f-gcc](https://github.com/ARMmbed/target-frdm-k64f-gcc)
* [target-mbed-armcc](https://github.com/ARMmbed/target-mbed-armcc)
* [target-mbed-gcc](https://github.com/ARMmbed/target-mbed-gcc)
* [target-st-stm32f429i-disco](https://github.com/ARMmbed/target-st-stm32f429i-disco)

We also have a number of examples to help you get started:

* [mbed-client-examples](https://github.com/ARMmbed/mbed-client-examples)
* [mbed-example-network](https://github.com/ARMmbed/mbed-example-network)
* [mbedtls-examples](https://github.com/ARMmbed/mbedtls-examples)
* [example-asynch-i2c](https://github.com/ARMmbed/example-asynch-i2c)
* [example-asynch-serial](https://github.com/ARMmbed/example-asynch-serial)
* [example-asynch-spi](https://github.com/ARMmbed/example-asynch-spi)
* [mbed-client-example-6lowpan](https://github.com/ARMmbed/mbed-client-example-6lowpan)
