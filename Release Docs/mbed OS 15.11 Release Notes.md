# mbed OS 15.11 Technology Preview Release Note

This is the first public Technology Preview of mbed OS and associated tools. We're
actively working on mbed OS and we expect to make exciting changes in the next six
months. We're making this technology preview available so you can see the trajectory
we're on. Our focus in this release is on laying the foundation for mbed OS
development and collaboration, particularly core tools, technology and testing.

We expect mbed OS developers to be able to access, build and run example projects
and to explore the underlying code.

If you're already using earlier versions of mbed, please note that mbed OS is a
new operating system; although it shares some code with mbed Classic, it has its
own structure, tools, APIs and philosophy. We recommend reading the links below
to understand how mbed OS differs from mbed Classic and what you need to do to
take full advantage of mbed OS.

## About this release

Note that this is a technology preview release, offering you early access to key
features and innovations enabling you to test functionality. This release is not
yet suitable for volume production use. The software is still maturing, and a number
of things will change, including module names, repository URLs, APIs, header file
names and configuration parameters. We'll try to mitigate the impact that these
changes have on your code where possible, but please expect backwards-incompatible
changes.

Note that in this release we're changing our version numbering scheme for mbed
OS releases, to a calendar-based (year and month YY.MM) scheme. This release (15.11)
has previously been called 3.0 in some communications.

## Collaboration

We're building mbed OS as a collaborative project, bringing together industry and
open source community contributions. If you'd like to work on mbed OS with us, we'd
encourage you to pitch in. With this technology preview we're ready to start receiving
contributions back from the community.

## Documentation

To get started with mbed OS, please visit our Getting Started Guides, which describe
the tools you need to use mbed OS, how to build and run your
[first mbed OS program](https://docs.mbed.com/docs/getting-started-mbed-os/en/latest/FirstProjectmbedOS/)
and where to find
[a few more examples](https://docs.mbed.com/docs/getting-started-mbed-os/en/latest/GetTheCode/).

To find out more about how mbed OS is structured and the services currently available
in mbed OS, please visit the mbed OS repository on GitHub. It contains a list of
the code repositories used in mbed OS, a list of the currently supported targets
and other useful information.

## Feature Readiness

The following features are currently experimental:

* `sal-stack-nanostack`
  * The mbed mesh networking stack includes an implementation of the Thread 1.0
    specification that is considered experimental. ARM intends to provide full
    production support for Thread following completion of the Thread standard.
* `mbed-mesh-api`
  * The mbed-mesh-api, which allows using 6LoWPAN mesh networks, currently uses
    static configuration. It does not provide an API for selecting the node operating
    mode, security option, radio channel or other options that are needed for
    connecting to 6LoWPAN networks. Configuration support will be available in later
    releases.
* *mbed TLS*
  * Support for EC J-PAKE is experimental and the Thread specification which requires
    it is itself not yet final. Random number generation is not yet suitable for
    use in production.
* `mbed-drivers`
  * Various APIs (including the asynchronous ones) are a work in progress; their
    signatures are expected to evolve over the next few releases.
* `mbed-hal`
  * The mbed HAL APIs are subject to change. The current HAL APIs are an evolution
    of the blocking APIs from mbed Classic, and have a number of limitations. In
    particular, the current APIs lack robust error handling (a requirement for
    production use), as well as consistent use of clock and power management and
    DMA and  documented implementation criteria and acceptance tests. We have big
    plans for the HAL. As with all other parts of the OS, we will signal
    incompatible changes to the HAL through the use of semantic versioning.
* `uvisor`
  * This version of the uVisor is an early tech preview, which has partial
    implementation of the security features that will be present in future versions.
    Please use this release for ensuring compatibility with uVisor (interrupt handling,
    memory protection model etc) but do not rely on it for security.

If you have any questions or comments about the readiness of features, please post
in the mbed forum.

## Target Availability

Currently the only target device officially supported by the ARM mbed team is the
Freescale FRDM-K64F board (yotta targets: `frdm-k64f-gcc` and `frdm-k64f-armcc`).

The following targets have experimental support:

* NXP JN5179
* ST Nucleo F401 and DISCO-F429I
* Nordic nRF51 DK and nRF51822-mKIT.
* BBC micro:bit.
* SiLabs EFM32 Giant Gecko and EFM32 Happy Gecko

This document will be updated shortly with instructions on how to use mbed OS on
these targets.

## Changes since the last release

This section documents the changes between this release and the earlier
mbed OS Beta (15.09) release.

### Core libraries

* `minar`
  * Fixed a bug that forced some callbacks to be scheduled in the past.
  * Removed dependency on `mbed-drivers`.
* `ualloc`
  * All headers are now in the `ualloc` header (`mbed-alloc` folder deprecated).
* `core-util`
  * `FunctionPointer` and `Event` are now in `core-util`.
* `mbed-drivers`
  * `Event` and `FunctionPointer` moved to `core-util` module.
  * `mbed_sdk_init` renamed to `hal_init`.
  * In SPI, we replaced the asynchronous API with a "fluent API" (to allow easier
    selection of optional parameters).
  * All headers are now in `mbed-drivers` directory (`mbed` directory deprecated).

### HAL and CMSIS

* `mbed-hal`
  * Pin maps can now be specified using `yotta config`.
  * Serial: The bit width of the transfer word is now deprecated and will be
    removed in the future.
  * STM32: Fixed prescaler computation for LPTMR. HSE config can now be
    specified through yotta config. Asynchronous SPI implementation.

### Networking

#### 6LoWPAN/Thread stack

* UDP socket connect, send, close and bind functionality changed to match mbed OS
  C++ Socket API.
* Interoperability improvements against Thread 1.0 specification.
* 6LoWPAN stack documentation published to
  [docs.mbed.com](https://docs.mbed.com/docs/arm-ipv66lowpan-stack/en/latest/).
* Added configuration for different operating modes.
* Various bug fixes.

#### Networking Libraries

* `sal`
  * Switched to dependency based on `yotta config`.
  * Added `get_options` and `set_options` to the API.
  * Moved include files to `sal/`.
  * `sal-stack-lwip`: Moved include files to `sal-stack-lwip`.
  * `sockets`: Moved include files to `sockets/`.

### Tools

#### yotta

The full yotta changelog can be found [here](https://github.com/ARMmbed/yotta/releases).
This release requires yotta 0.9.1 or greater.

#### Test Tools

* `greentea`
  * Added better support to latest yotta versions.
  * Changed application workflow to support one mbed target test execution for
    every specified target.
  * Added support for pylint scans.
* `htrun`
  * Small improvements to host OS support and documentation.
  * Added command line switch `-b` to send break command to devices.
  * Added support for pylint scans.
* `mbed-ls`
  * Added `--mock` command line switch; useful when prototyping and detecting new
    targets.
  * Fixed issue related to target detection on Ubuntu and Mac OS X.
  * Added support for pylint scans.

#### uVisor

The main new feature of this release is support for STM32F4 ARM Cortex-M4 devices
using the ARM architected memory protection unit (MPU). In this release we support
the two following target platforms for uVisor:

* Freescale FRDM-K64F (GCC ARM Embedded toolchain).
* ST STM32F429I-DISCO (GCC ARM Embedded toolchain).

The previous beta release (15.09) demonstrated the creation of a sandbox that
allocates private memories and requests individual access to security critical
system peripherals using access control lists (ACLs) and demonstrating
unprivileged interrupts. In this release we updated our example code with
MINAR eventing.

We also added secure box contexts to provide efficient box-specific secure memories.
These can be used for storing box-specific class instances, or other
security-critical data that needs to be restricted to individual boxes.

To demonstrate µVisor we created a simple exploit demo: when pressing a switch on
the development board, the main mbed box attempts to read a secured password. The
µVisor will intercept that attempt and deny access by halting the code (five red
blinks). The error handling will be
[improved in future releases](https://github.com/ARMmbed/uvisor#word-of-caution)
by supporting configurable debug channels.

Most complete information about the µVisor component can be found in the
[µVisor GitHub repository](https://github.com/ARMmbed/uvisor) and
[known issues](https://github.com/ARMmbed/uvisor/issues?q=is%3Aopen+is%3Aissue+label%3Aissue)
list.

#### mbed TLS

This release is based on mbed TLS 2.2.0, while the mbed OS Beta (15.09) release
was based on mbed TLS 2.1.0. Major changes between those versions include:

A new integrated C++ class library for TLS connections (currently only TLS clients)
in the companion module
[mbed-tls-sockets](http://yotta.mbed.com/#/module/mbed-tls-sockets/0.1.0).
Experimental support for the EC J-PAKE key exchange as defined in the Thread 1.0.0
draft specification. This support is disabled by default as the specification is
not stable yet. See the
[README](https://github.com/ARMmbed/mbedtls/blob/f7a46882574804d1939d48341ecc8b87e3efd651/yotta/data/README.md#configuring-mbed-tls-features)
for instructions to enable it.
Fixes for security issues, including
[CVE-2015-5291](https://tls.mbed.org/tech-updates/security-advisories/mbedtls-security-advisory-2015-01).
Various bug fixes and improvements.

More details can be found in the [changelog](https://github.com/ARMmbed/mbedtls/blob/development/ChangeLog).

Currently the only officially supported target platform for mbed TLS in mbed OS is
the Freescale FRDM-K64F board (yotta targets: `frdm-k64f-gcc` and `frdm-k64f-armcc`).
We do not recommend using this release of mbed TLS in production, because the port
for the Freescale FRDM-K64F board does not yet provide an adequate source of random
numbers necessary for the cryptographic functions.

### Bluetooth Low Energy

This release reintroduces the mbed Classic Bluetooth Low Energy (BLE) APIs into mbed
OS. These APIs abstract vendors' BLE implementations, including single-chip and external
peripheral configurations. Currently there is reference support for targets based
on Nordic's nRF51 family of MCUs, as well as experimental support for ST BLE shields
on other target boards.

The Bluetooth API is hosted on [GitHub](https://github.com/ARMmbed/ble). It comes
with reference implementations for some Bluetooth-SIG specified GATT profiles and
services; documented example applications can be found
[here](https://github.com/ARMmbed/ble-examples).

### mbed Client API

This release contains the following new features:

* Securely connect to mbed Device Server (mbed DS) over TCP connection through
  TLS. The supported secure connection includes Certificate mode. We still support
  non-secure connection mode for fast development and debugging.
* New LWM2M Firmware Object class preview for application development.

## Known issues

The known issues for this release are described [here](mbed OS 15.11 Known Issues.md).

## Other ways of accessing this release

We prefer that you access and collaborate with mbed OS here on GitHub and on
[mbed.com](https://www.mbed.com). However, the release may also be downloaded as
an archive
[on mbed.com](https://www.mbed.com/en/development/software/mbed-os/releases/mbed-os1511/).
For further information, please start with the README in the root directory of the
archive.

## Module versions in this release

We use [semantic versioning](http://semver.org) for the modules in mbed OS. This
means that you can tell from the version number of a module what's changed: an
increase in the major version indicates a backwards incompatible change, and the
minor and patch versions are used for backwards compatible features and bug-fixes
respectively. When you use yotta to build an application that depends on a module,
you can specify which sort of updates you will allow updates to. For more
information on how yotta uses version specifications, see the
[yotta documentation](http://yottadocs.mbed.com/reference/module.html#dependencies).

This release comprises the following yotta modules and their versions:

| Module                             | Version |
|------------------------------------|---------|
| `atmel-rf-driver`                  |   1.0.1 |
| `ble`                              |   2.0.3 |
| `BLE_URIBeacon`                    |   0.0.1 |
| `BLE_Thermomether`                 |   0.0.1 |
| `BLE_HeartRate`                    |   0.0.1 |
| `BLE_EddystoneObserver`            |   0.0.1 |
| `BLE_EddystoneBeacon`              |   0.0.1 |
| `BLE_Beacon`                       |   0.0.1 |
| `ble-nrf51822`                     |   2.0.2 |
| `cmsis-core`                       |   1.0.1 |
| `cmsis-core-freescale`             |   1.0.0 |
| `cmsis-core-k64f`                  |   1.0.0 |
| `cmsis-core-nordic`                |   1.0.1 |
| `cmsis-core-nrf51822`              |   1.0.1 |
| `cmsis-core-st`                    |   1.0.0 |
| `cmsis-core-stm32f4`               |   1.0.2 |
| `cmsis-core-stm32f429xi`           |   1.0.2 |
| `compiler-polyfill`                |   1.1.1 |
| `core-util`                        |   1.0.1 |
| `dlmalloc`                         |   1.0.0 |
| `example-asynch-i2c`               |   1.0.1 |
| `example-asynch-serial`            |   1.0.0 |
| `example-asynch-spi`               |   1.0.1 |
| `example-mbedos-blinky`            |   1.0.0 |
| `helloyotta`                       |   0.0.0 |
| `mbed-6lowpan-eventloop-adaptor`   |   1.0.2 |
| `mbed-client`                      |   1.2.1 |
| `mbed-client-c`                    |   1.1.1 |
| `mbed-client-example-6lowpan`      |   0.0.2 |
| `mbed-client-examples`             |   1.1.0 |
| `mbed-client-libservice`           |   3.0.8 |
| `mbed-client-mbed-os`              |   1.1.0 |
| `mbed-client-mbed-tls`             |   1.0.9 |
| `mbed-client-randlib`              |   1.0.0 |
| `mbed-drivers`                     |  0.11.1 |
| `mbed-example-network`             |   1.0.1 |
| `mbed-hal`                         |   1.0.5 |
| `mbed-hal-frdm-k64f`               |   1.0.0 |
| `mbed-hal-freescale`               |   1.0.0 |
| `mbed-hal-k64f`                    |   1.0.1 |
| `mbed-hal-ksdk-mcu`                |   1.0.3 |
| `mbed-hal-mkit`                    |   1.0.0 |
| `mbed-hal-nordic`                  |   1.0.0 |
| `mbed-hal-nrf51822-mcu`            |   1.0.5 |
| `mbed-hal-nrf51dk`                 |   1.0.1 |
| `mbed-hal-st`                      |   1.0.0 |
| `mbed-hal-st-stm32cubef4`          |   1.0.2 |
| `mbed-hal-st-stm32f4`              |   1.0.3 |
| `mbed-hal-st-stm32f429zi`          |   1.0.3 |
| `mbed-mesh-api`                    |   1.0.1 |
| `mbed-tls-sockets`                 |   0.1.0 |
| `mbedtls`                          |   2.2.0 |
| `minar`                            |   1.0.1 |
| `minar-platform`                   |   1.0.0 |
| `minar-platform-mbed`              |   1.0.0 |
| `sal`                              |   1.0.2 |
| `sal-driver-lwip-k64f-eth`         |   1.0.2 |
| `sal-iface-6lowpan`                |   1.0.7 |
| `sal-iface-eth`                    |   1.0.1 |
| `sal-stack-lwip`                   |   1.0.2 |
| `sal-stack-nanostack`              |   3.0.5 |
| `sal-stack-nanostack-eventloop`    |   1.0.3 |
| `sockets`                          |   1.0.2 |
| `target-frdm-k64f-armcc`           |   1.0.0 |
| `target-frdm-k64f-gcc`             |   1.0.1 |
| `target-kinetis-k64-armcc`         |   1.0.0 |
| `target-kinetis-k64-gcc`           |   1.0.0 |
| `target-mbed-armcc`                |   0.1.2 |
| `target-mbed-gcc`                  |   0.1.3 |
| `target-nordic-nrf51822-16k-armcc` |  0.0.11 |
| `target-nordic-nrf51822-32k-armcc` |  0.0.11 |
| `target-nordic-nrf51822-16k-gcc`   |  0.0.11 |
| `target-nordic-nrf51822-32k-gcc`   |   0.0.8 |
| `target-nrf51dk-armcc`             |   0.0.4 |
| `target-nrf51dk-gcc`               |   0.0.4 |
| `target-st-stm32f429i-disco`       |  0.0.15 |
| `ualloc`                           |   1.0.2 |
| `unity`                            |   1.0.0 |
| `uvisor-helloworld`                |   0.7.3 |
| `uvisor-lib`                       |   1.0.6 |


