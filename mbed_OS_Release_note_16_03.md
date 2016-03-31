
# mbed OS 16.03 Release Note 

## About this release 

This document marks the availability of the 16.03 release of mbed OS and associated tools. Our focus in this release is on improving the core tools, underlying technologies and confidence through testing of the mbed OS 15.11 Technology Preview release. This release brings together improvements in the following key areas of the mbed technologies and tools:

* **Thread**: Added interoperability improvements for Thread certification and introduced Thread 1.0 features and experimental Thread 1.1 features. Added Sleepy End Device configuration support to work with mbed 6LoWPAN technologies.
* **6LoWPAN**: Updated Nanostack version 4.0 to introduce new APIs focused on Mesh Link Establishment (MLE) configuration and associated router management. Added guidance on updating modules for mbed 6LoWPAN implementation.
* **Bluetooth Low Energy (BLE)**: Introduced new APIs with experimental whitelisting support, optional higher security settings for connections and overall improvements in General Access Profile (GAP) module and behavior.
* **Infrastructure**: Updated the test environment to offer improved test coverage for the core OS and associated tools, which increases stability and reliability.
* **Security**: Improved the uVisor build system to offer efficient sandboxing for all platforms, reduced the need for target-specific modifications and added new APIs that improve applications using uVisor.
 
As an mbed OS developer, you have access to the code and can build and run the example projects. 

This release offers better test coverage and can be used to evaluate the latest capabilities of mbed OS. IoT use-cases are emergent and the current release does not provide full coverage of all production uses. The software is still maturing and we expect changes to a number of things including module names, repository URLs, APIs, header file names and configuration parameters. We'll try to mitigate the impact that these changes have on your code where possible, but please expect backwards-incompatible changes. 

If you’re already using earlier versions of mbed, please note that mbed OS has its own structure, tools, APIs and philosophy. We recommend reading the [mbed OS User Guide](https://docs.mbed.com/docs/getting-started-mbed-os/en/latest/). 

If you have any questions or comments, please post on the [mbed forums](http://forums.mbed.com). 
 
## Target availability 
 
Currently the only target device officially supported by the ARM mbed team is the NXP FRDM-K64F board (yotta target: `frdm-k64f-gcc`). 

In addition, there is partial and experimental support for the following target devices:

* Nordic nRF51-DK and nRF51822-mKIT boards for Bluetooth Low Energy (BLE) (yotta targets: `nrf51dk-gcc` and `mkit-gcc`).
* NXP JN5179 (yotta target: ‘nxpdk5-jn517x-gcc’).
* BBC micro:bit.
* ST Nucleo F401 and DISCO-F4291.

## Collaboration 
 
We're building mbed OS as a collaborative project, bringing together industry and open-source community contributions. If you’d like to work on mbed OS with us, we’d encourage you [to pitch in](https://github.com/ARMmbed/mbed-os/blob/master/CONTRIBUTING.md). 
 
# mbed OS core

## mbed-drivers 

### Feature readiness

This release includes version 1.3.0 of the mbed-drivers API. The mbed-drivers API is an evolution of the original mbed SDK and, as such, there are places where its design is not well suited to the event-driven programming model used in the rest of mbed OS. We anticipate significant changes in the mbed-drivers API in future releases, but we are publishing the current API as-is, so that developers can start working with mbed OS today.

From this point on, we will follow the familiar versioning rules described by [semver](http://semver.org) when publishing updates to ``mbed-drivers``. If we make a breaking change to the API, we will increase the major revision number. We will also aim to provide backwards compatibility by developing different versions of the API in different C++ namespaces.

### Changes since last release

* Added support for gcov output.
* Added default baud rate for stdio, derived from yotta config.
* Removed mbed_mac_address default implementation.
* Changed app_start linkage to C++ and remove app.h.
* Converted stdio serial to lazy initialization in order to save memory allocation when stdio is not used in an application.
* Updated mbed-drivers tests to new version of greentea-client.
* Move test_env.h to greentea-client.
* Added first version 2 driver (I2C). ``example-asynch-i2c`` has been updated to match this driver.

## core-util 

### Changes since last release

* Tests updated to use greentea-client.
* Comment out assert in the critical section.
* CriticalSectionLock to use the C based solution within the class.
* C critical section for NRF51 targets.
* C critical section for POSIX targets.
* Allocators aligned to 8.
* NRF51 critical section - fixes use with the SoftDevice disabled.
* mbed-drivers - update dependency to 1.0.0.
* C re-entrant critical section.
* sbrk - ensure that both positive and negative `sbrk` calls are aligned to the minimum `sbrk` size.
* Test function pointer - set baud rate removal.
* Add support for uninitialized data sections.
* Array, binaryHeap and pool allocators - forbid copying.
* Newline termination for runtime errors.
* Optimized specializations of atomic ops.
* Add missing template specialization prototypes.
* Shared pointer - API documentation.
* Function pointer - fix arguments (all types of arguments, including references).
* core-util.h renamed to assert.h.

##mbed-hal 

### Feature readiness

The mbed HAL APIs are subject to change. The current HAL APIs are an evolution of the blocking APIs from mbed Classic, and have a number of limitations. There are no notable changes to the mbed HAL APIs from the [mbed OS 15.11 release](../15_11/mbed_OS/Release_Note.md). As with all other parts of the OS, we will signal incompatible changes to the HAL through the use of semantic versioning. 

### Changes since last release 

* Clarified doxygen and generic documentation.
* K64F: 
 * Fixed bug related to SPI transfers.
 * Removed console specific code from mbed-hal-ksdk-mcu.
 * Use the baud rate defined in yotta config.
 * Use CRC to generate an Ethernet MAC address.

## minar 

### Changes since last release

* Runtime warnings turned on by default in debug builds.
* Clarified use of tolerance and the default value of tolerance.
* Updated tests.
 
## ualloc 

### Changes since last release

* Tests updated to use greentea-client.
* Enable memory tracing via yotta config.
* ualloc header file – API documentation addition.
* Handle -1 returns from krbs.
* Readme – extensive information added.

# Networking 

## Thread 

### Changes since last release

* Interoperability improvements for Thread Certification.
* Implemented Thread 1.0 features.
* Implemented experimental Thread 1.1 features for specification studies.
* Integrated mbed TLS ECJPAKE for Thread use.
* Added Sleepy End Device configuration support to mbed-client-example-6lowpan.

Since the Thread standard is still unapproved, this API is considered experimental.

## 6LoWPAN stack 

### Changes since last release

* Major version updated to 4.0.
* New APIs:
 * MLE router and host lifetime configuration API.
 * MLE neighbor limits configuration API.
 * MLE token bucket configuration API.
 * API for adding and deleting routers.
 * FHSS API.
* API changes:
 * Renamed the function `arm_nwk_6lowpan_link_scan_paramameter_set()` to `arm_nwk_6lowpan_link_scan_parameter_set()`. 
 * Changed channel mask settings API.
 * Changed the parameters of function `cca_start()`.

For instructions on updating your modules, see [https://docs.mbed.com/docs/arm-ipv66lowpan-stack/en/latest/api_changes_to_v4_0_0/index.html](https://docs.mbed.com/docs/arm-ipv66lowpan-stack/en/latest/api_changes_to_v4_0_0/index.html).

## Bluetooth Low Energy (BLE)

### Feature readiness

The whitelist API available in the GAP module is subject to change. All experimental types and functions have their documentation tagged with `@experimental`.

### Changes since last release

* Improved documentation.
* Improved callback management. It is now possible to remove a callback.
* Improved shutdown behavior. The BLE stack powers down fully and consistently with shutdown.The user can register hooks that will get called when the stack is shut down.
* Improved UUID construction.
* Add new APIs:
 * Handle characteristic descriptor discovery.
 * Allow whitelisting. This feature is still experimental.
 * Allow elevating security settings on a particular connection.
* Fix commit of advertisement payload.
* NRF51: 
 * Use Nordic SDK v10.
 * NRF51: Fix handles value of characteristics descriptors.
 * Fix update of GAP state.

## mbed-mesh-api 

### Feature readiness

The [mbed-mesh-api](https://github.com/ARMmbed/mbed-mesh-api), which allows using 6LoWPAN mesh networks, currently uses static configuration. It does not provide an API for selecting the node operating mode, security option, radio channel or other options that are needed for connecting to 6LoWPAN networks. Configuration support will be available in later releases.  

## sal

### Changes since last release

* Added inet_ntop and inet_pton support.
* Added a socket options API.

## sal-stack-nanostack 

### Feature readiness

The mbed mesh networking stack includes an implementation of the Thread 1.0 specification. It is experimental, because the Thread specification is still under development. ARM intends to provide full production support for Thread following completion of the Thread standard. 

## Sockets

### Changes since last release

* Added support for address parsing and formatting to the SocketAddr class.
* Added support for enabling and disabling Nagle’s algorithm.

# Security
 
## mbed TLS 

### Feature readiness

* Support for ECJPAKE is experimental and the Thread specification which requires it is itself not yet final. 
* Integration of the random number generation is not yet suitable for use in production. 
 
### Changes since last release

Disabled MD5 handshake signatures in TLS 1.2 by default, to prevent the SLOTH attack on TLS 1.2 server authentication. See [https://www.mitls.org/pages/attacks/SLOTH](https://www.mitls.org/pages/attacks/SLOTH).

### uVisor 

Porting uVisor to a whole range of devices has [been greatly simplified since the last release](https://docs.mbed.com/docs/uvisor-and-uvisor-lib-documentation/en/latest/Porting/): no target-specific headers or code-edits are required any more. Debugging is now delegated to unprivileged debug drivers. We also added box identity APIs, so boxes can identify API callers across security boundaries to impose caller-specific API restrictions.

#### Changes since last release

* Improved build system:
 * Reduced need for hardware-specific implementations.
 * Introducing uVisor configurations: A unified point for hardware-specific configuration details that defines a single uVisor release binary.
 * New centralized build system. A single make in the top folder builds all configurations for all platforms in release and debug mode.
 * See our [porting guide](https://github.com/ARMmbed/uvisor/blob/master/docs/PORTING.md) for updated information.
* New features:
 * [New APIs](https://github.com/ARMmbed/uvisor-lib/blob/master/DOCUMENTATION.md#box-identity) to read current box ID and caller box ID.
 * New concept of box namespaces to authorize cross-box/cross-device API communication.
 * Added context switching features in UVISOR_DISABLED mode.
 * Extended SVCall handler table.
 * Global vMPU configurations for ARMv7-M: Shared vs. Standalone SRAM.
 * MadeMake ACLs optional in secure box configuration.
 * Debug boxes (prototype).
* New platforms:
 * Now supporting the entire Cortex-M3 and Cortex-M4 based EFM32 family from Silicon Labs.
* Breaking APIs:
 * Applications using UVISOR_BOX_CONFIG(...) will not work after this update if they do not include a call to the UVISOR_BOX_NAMESPACE(...) as well. 
 * All other APIs are backwards compatible.
 * This update only affects applications actively using uVisor, not yotta modules depending on it.

#### Security disclaimer

This version of the mbed OS uVisor is an early tech preview, which has partial implementation of the security features that will be present in future versions. Please use this release for ensuring compatibility with uVisor (interrupt handling, memory protection model and so on), but do not rely on it for security.  

# Tools 

## yotta changes since last release

Many bugfixes and improvements, including:

* Improved support for generating IDE project files with -G option.
* New yotta shrinkwrap command for recording and subsequently installing specific versions of dependencies.
* Improved support for modules with custom CMake (including the ability to ignore custom CMake), the ability to define custom CMake in targets, and the option to specify the source directory to build automatically (making it easier to support existing libraries with yotta).
* Add useful information to the output of `yotta config` and `yotta outdated` commands.
* Modules and targets can now specify a dependency on the version of yotta they require.
* Many improved and additional warnings and diagnostic messages.

The full yotta changelog can be found at [https://github.com/ARMmbed/yotta/releases](https://github.com/ARMmbed/yotta/releases). 

This release requires yotta 0.15.2  or greater. 
 
## Test tools

### Greentea changes since last release

* Released “mbed-greentea” version 0.2.0 in PyPI (current release support).
* Released “mbed-greentea” version 0.1.x (for backward compatibility with mbed-drivers/test_env.h)
* Introduced a new test environment package: greentea-client. It is the Greentea device under test (DUT) counterpart.
* Added support for the asynchronous host test model.
* Added support for utest v1.10.0 onwards.
* Added test suite and test case support (also with utest v1.10.0 onwards).
* Added code coverage support for gcov/lcov reporting.
* Added support for hooks (used mainly by the gcov/lcov feature).
* Deprecated the use of mbed-drivers/test_env.h. See greentea-client notes below.
* Deprecated the --digest switch.

### greentea-client changes since last release

* DUT C++ Greentea client library.
* Deprecates mbed-drivers/test_env.h.
* Introduces stateless parser/tokenizer for simple key-value protocol between the host and DUT.
* This is the slave side of the Greentea framework.
* Released as “greentea-client” version 1.0.0 in the yotta Registry.

### htrun changes since last release

* Added support of the key-value protocol – asynchronous host test execution model.
* Added support of the key-value protocol callbacks.
* Added event state machine.
* Deprecated --digest switch.
* Released as “mbed-host-tests” version 0.2.0 in PyPI.

### mbed-ls changes since last release

* Added support for DAPlink version 0240.
* Added parsing for DETAIL.TXT.
* Added DAPlink version detection.
* Small improvements to the way we display data on the screen.
* Added more platforms to detection pool.
* Minor bugfixes.
* Released as “mbed-ls” version 0.2.0 in PyPI.

Please note that mbed-ls does not support OS X El Capitan.

# mbed Client

## Changes since last release

* New APIs:
 * Setting the max-age of a resource value. See [https://tools.ietf.org/html/draft-ietf-core-coap-09#section-5.10.6](https://tools.ietf.org/html/draft-ietf-core-coap-09#section-5.10.6).
 * Omitting registered resources' URI path from the registration message's body (which is sent from the client to the server). 
 * Allowing the client to send a delayed response to POST requests. See [https://tools.ietf.org/html/draft-ietf-core-coap-09#section-5.2.2](https://tools.ietf.org/html/draft-ietf-core-coap-09#section-5.2.2).
 * Getting Object and Object Instance information from Resource Object.
* Added a new class for handling arguments received from POST method for Resource. 
* Enabled CoAP Blockwise payload handling by client. See  [https://tools.ietf.org/html/draft-ietf-core-block-08#section-2](https://tools.ietf.org/html/draft-ietf-core-block-08#section-2).
* Added support for handling observation cancellation through a RESET message from Device Connector Server.
* Disabled Bootstrap API functionality from source code.

# Known issues 

The known issues list for this release is available as [a separate document](https://github.com/ARMmbed/mbed-os/blob/master/Release%20Docs/mbed_OS_Known_Issues_16_03.md)

# Other ways of accessing this release 

We prefer that you access and collaborate with mbed OS online. However, the release may also be downloaded [as an archive](https://mbed-media.mbed.com/filer_public/fc/1a/fc1a497b-ece4-4a60-bc91-b0bcf9abe1d5/mbedos-1603.zip). For further information, please start with the readme in the root directory of the archive. 

# Getting started

To get started with mbed OS, please visit our [Getting Started Guide](http://docs.mbed.org/docs/getting-started-mbed-os/en/latest/), which describes the tools you need to use mbed OS, how to build and run your [first mbed OS program](https://docs.mbed.com/docs/getting-started-mbed-os/en/latest/FirstProjectmbedOS/) and where to find [a few more examples](https://docs.mbed.com/docs/getting-started-mbed-os/en/latest/GetTheCode/). 

# Module versions in this release 
 
We use [semantic versioning](http://semver.org) for the modules in mbed OS. This means that you can tell from the version number of a module what’s changed: an increase in the major version indicates a backwards incompatible change, and the minor and patch versions are used for backwards compatible features and bug-fixes respectively. When you use yotta to build an application that depends on a module, you can specify which sort of updates you will allow updates to. For more information on how yotta uses version specifications, see the [yotta documentation](http://yottadocs.mbed.com/reference/module.html#dependencies). 
 
This release comprises the following yotta modules and their versions: 


| Module                         | Version  |
|--------------------------------|----------|
| async-util                     |  0.0.2   |
| atmel-rf-driver                |  2.0.3   |
| ble                            |  2.5.2   |
| ble-batterylevel               |  0.0.1   |
| ble-beacon                     |  0.0.1   |
| ble-button                     |  0.0.1   |
| ble-eddystoneobserver          |  0.0.1   |
| ble-gapbutton                  |  0.0.1   |
| ble-heartrate                  |  0.0.1   |
| ble-led                        |  0.0.1   |
| ble-ledblinker                 |  0.0.1   |
| ble-thermometer                |  0.0.1   |
| ble-uribeacon                  |  0.0.1   |
| ble-nrf51822                   |  2.5.3   |
| cmsis-core                     |  1.1.2   |
| cmsis-core-freescale           |  1.0.0   |
| cmsis-core-k64f                |  1.0.0   |
| cmsis-core-nordic              |  1.0.1   |
| cmsis-core-nrf51822            |  1.3.2   |
| coap-service                   |  2.1.0   |
| compiler-polyfill              |  1.2.1   |
| core-util                      |  1.7.1   |
| dlmalloc                       |  1.0.0   |
| example-asynch-i2c             |  1.1.0   |
| example-asynch-serial          |  2.0.0   |
| example-asynch-spi             |  3.0.0   |
| example-mbedos-blinky          |  1.0.0   |
| example-mbedos-interruptin     |  1.0.0   |
| greentea-client                |  1.0.0   |
| helloyotta                     |  0.0.0   |
| k64f-border-router             |  1.0.1   |
| mbed-6lowpan-eventloop-adaptor |  1.1.1   |
| mbed-client                    |  1.6.0   |
| mbed-client-c                  |  2.2.11  |
| mbed-client-example-6lowpan    |  0.0.2   |
| mbed-client-examples           |  1.1.0   |
| nanostack-libservice           |  3.1.1   |
| mbed-client-linux              |  1.1.9   |
| mbed-client-linux-example      |  1.1.0   |
| mbed-client-mbed-os            |  1.1.6   |
| mbed-client-mbedtls            |  1.0.16  |
| nanostack-randlib              |  1.0.0   |
| mbed-drivers                   |  1.4.0   |
| mbed-example-network           |  1.0.1   |
| mbed-hal                       |  1.2.2   |
| mbed-hal-frdm-k64f             |  1.0.2   |
| mbed-hal-freescale             |  1.0.0   |
| mbed-hal-k64f                  |  1.2.0   |
| mbed-hal-ksdk-mcu              |  1.1.0   |
| mbed-hal-mkit                  |  1.0.2   |
| mbed-hal-nordic                |  2.0.0   |
| mbed-hal-nrf51822-mcu          |  2.1.6   |
| mbed-hal-nrf51dk               |  2.0.0   |
| mbed-mesh-api                  |  2.2.0   |
| mbedtls                        |  2.2.2   |
| mbed-tls-sockets               |  0.1.1   |
| mbed-trace                     |  1.0.1   |
| minar                          |  1.2.0   |
| minar-platform                 |  1.0.0   |
| minar-platform-mbed            |  1.2.0   |
| nanostack-border-router        |  1.0.3   |
| nrf51-sdk                      |  2.2.1   |
| sal                            |  1.2.0   |
| sal-driver-lwip-k64f-eth       |  1.0.6   |
| sal-iface-6lowpan              |  2.0.1   |
| sal-iface-eth                  |  1.0.2   |
| sal-nanostack-driver-k64f-eth  |  1.0.5   |
| sal-stack-lwip                 |  1.3.1   |
| sal-stack-nanostack            |  4.0.3   |
| sal-stack-nanostack-eventloop  |  1.0.7   |
| sal-stack-nanostack-slip       |  1.0.3   |
| simplelog                      |  1.0.0   |
| sockets                        |  1.2.0   |
| target-frdm-k64f-gcc           |  2.0.0   |
| target-kinetis-k64-gcc         |  2.0.2   |
| target-linux-native            |  1.0.0   |
| target-mbed-gcc                |  1.2.0   |
| target-mkit-gcc                |  1.0.0   |
| target-nordic-nrf51822-gcc     |  1.0.0   |
| target-nrf51dk-gcc             |  1.0.0   |
| target-x86-linux-native        |  1.0.0   |
| ualloc                         |  1.2.0   |
| unity                          |  2.1.0   |
| utest                          |  1.11.0  |
| uvisor-helloworld              |  0.8.0   |
| uvisor-lib                     |  2.2.1   |

