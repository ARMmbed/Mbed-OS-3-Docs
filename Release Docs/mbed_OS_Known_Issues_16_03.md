# mbed OS Known Issues

## About this document

This is the list of known issues for the This is the list of known issues for the [16.03 release of mbed OS and related tools](Release_Note.md).

We publish mbed OS as a collection of modules on GitHub. Issues are raised in the specific repositories and then tracked internally. 

The purpose of this document is to provide a single view of the outstanding key issues that have not been addressed for this release. As such it is a filtered and reviewed list based on priority and potential impact. Each item summarises the problem and includes any known workarounds, along with a link to the GitHub issue (if applicable). We welcome any comments or proposed solutions.

For more information about an issue, contact us on the [forums](http://forums.mbed.com).

## Additional information

For further information regarding this release please refer to the release notes referenced above.

Other tools such as [yotta](https://github.com/ARMmbed/yotta) and [Greentea](https://github.com/ARMmbed/greentea) also have their own lists, which can be viewed in their public GitHub repositories.

# Known issues
## Device disconnects or crashes after 50 hours
* **Description**: After 50 hours online with mbed Client, device stops responding.
* **Workaround**: No workarounds.
* **Reported Issue**: [https://github.com/ARMmbed/sal-stack-nanostack/issues/7](https://github.com/ARMmbed/sal-stack-nanostack/issues/7)
* **Priority**: Critical

## mbed-client-example-6lowpan does not recover from network connection errors
* **Description**: If the border router is disconnected the mbed client ends up in an error loop and does not recover
* **Workaround**: None
* **Reported Issue**: ONME-2509
* **Priority**: Critical

## K64F border router and 6LoWPAN ND do not work with debug trace enabled
* **Description**: When debug trace is enabled the node either crashes or does not work properly.
* **Workaround**: None
* **Reported Issue**: [https://github.com/ARMmbed/sal-stack-nanostack-private/issues/341](https://github.com/ARMmbed/sal-stack-nanostack-private/issues/341)
* **Priority**: Critical

## Low power ticker overflow issue in MINAR
* **Description**: If the low power ticker overflows, MINAR might start executing periodic events faster than desired after it wakes up from sleep.
* **Workaround**: None
* **Reported Issue**: [https://github.com/ARMmbed/minar/issues/32](https://github.com/ARMmbed/minar/issues/32)
* **Priority**: Critical

## Only a single sal-stack can be used with the socket API
* **Description**: The mbed OS socket API handles the periodic task provided by the SAL incorrectly. Because of this, only a single stack can be used at a time.
* **Workaround**: Use the SAL to extract the periodic function (`void (*task)() = socket_get_api(STACK_ID)->periodic_task()`) and periodic interval (`uint32_t interval = socket_get_api(STACK_ID)->periodic_interval()`), then schedule a recurring callback in MINAR for each stack (`minar::Scheduler::postCallback(task).period(minar::milliseconds(interval)`)
* **Reported Issue**: [https://github.com/ARMmbed/sockets/issues/36](https://github.com/ARMmbed/sockets/issues/36)
* **Priority**: Major

## Distinguish between read and write access faults in uVisor
* **Description**: When creating a read-only region in uVisor, write access will create an access fault as expected, but it needs to avoid configuring the corresponding MPU region again. The intended behavior is to fault with a security exception.
* **Workaround**: Do not write to read-only memory regions.
* **Reported Issue**: [https://github.com/ARMmbed/uvisor/issues/68](https://github.com/ARMmbed/uvisor/issues/68)
* **Priority**: Major

## uVisor cannot be enabled on targets built with armcc
* **Description**: Some uVisor APIs rely on complex inline assembly, which is not fully supported by the ARM Compiler 5. Their implementation requires a completely different approach, which we are working on. For this release though, we will not support armcc.
* **Workaround**: All targets that support uVisor and are built with armcc will still compile and work, but the security features of uVisor will not be available. uVisor APIs will still be available, but no security measure will be enabled.
* **Reported Issue**: [https://github.com/ARMmbed/uvisor/issues/89](https://github.com/ARMmbed/uvisor/issues/89)
* **Priority**: Major

## Hardware floating point is currently disabled
* **Description**: uVisor has not yet implemented full handling of the FPU register file and exception model. Until the FPU is fully supported in uVisor, mbed OS must be used with hardware floating point disabled.
* **Workaround**: Soft-floating point can be used (providing complete functionality, but with a performance and power impact compared to hard-FP).
* **Reported Issue**: [https://github.com/ARMmbed/uvisor/issues/88](https://github.com/ARMmbed/uvisor/issues/88)
* **Priority**: Major

## 6LoWPAN socket adaptation layer does not support DNS
* **Description**: 6LoWPAN socket adaptation layer does not support DNS.
* **Workaround**: IPv6 addresses must be given in ASCII format.
* **Reported Issue**: [https://github.com/ARMmbed/sal-iface-6lowpan/issues/12](https://github.com/ARMmbed/sal-iface-6lowpan/issues/12)
* **Priority**: Minor

## 6LoWPAN socket adaptation layer has incomplete C++ API
* **Description**: The following mbed C++ Socket API methods are not implemented in `sal-iface-6lowpan`:
  * `socket_accept`
  * `socket_start_listen`
  * `socket_stop_listen`
  * `send_to` (for TCP sockets)
  * `recv_from` (for TCP sockets)
  * `set_option`
  * `get_option`
  * `is_bound`
  * `get_local_addr`
  * `get_remote_addr`
  * `get_local_port`
  * `get_remote_port`
* **Workaround**: None
* **Reported Issue**: [https://github.com/ARMmbed/sal-iface-6lowpan/issues/11](https://github.com/ARMmbed/sal-iface-6lowpan/issues/11)
* **Priority**: Minor

## Mesh network is insecure
* **Description**: Mesh network is insecure:
  * `mbed-mesh-api` does not provide an API for changing the security settings.
  * gateway binary releases are currently operating in insecure mode.
* **Workaround**: None
* **Reported Issue**: ARM internal reference ONME-2076
* **Priority**: Minor

## LwIP does not use random source port and sequence number in TCP connections
* **Description**: LwIP should use random source ports and sequence numbers in TCP connections.  Failing to do so means that remote hosts can ignore connection requests by a device running LwIP when a connection is improperly closed and reopened, for example by a reset.  Original issue: https://github.com/ARMmbed/sockets/issues/17
* **Workaround**: Manually bind a socket to a random port before connecting to a remote host.  Suggested source of randomness is mbed TLS's entropy pool and random number generator.
* **Reported Issue**: [https://github.com/ARMmbed/sockets/issues/17](https://github.com/ARMmbed/sockets/issues/17)
* **Priority**: Minor

## Floating point format is not supported in printf()
* **Description**: If floating point data is passed to printf(), a blank space will be displayed.
* **Workaround**: None
* **Reported Issue**: [https://github.com/ARMmbed/target-mbed-gcc/issues/17](https://github.com/ARMmbed/target-mbed-gcc/issues/17)
* **Priority**: Minor

## Kinetis K64F target claims RAM to be continuous.
* **Description**: Random Hard Faults may happen if misaligned memory access happens between SRAM_L and SRAM_U boundary.
* **Workaround**: No continuous objects in memory should cross 0x20000000 boundary.
* **Reported Issue**: [https://github.com/ARMmbed/target-kinetis-k64-gcc/issues/4](https://github.com/ARMmbed/target-kinetis-k64-gcc/issues/4)
* **Priority**: Critical

# Known issues for mbed Client

The mbed Client known issues list is available as [a separate document](../mbed_Client/Known_Issues.md).
