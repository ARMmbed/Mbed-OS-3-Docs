# mbed OS 15.11 Known Issues

## About this document

This is the list of known issues for the 15.11 release of
[mbed OS](https://github.com/ARMmbed/mbed-os). We publish mbed OS as a collection
of modules in GitHub, and track open issues as tickets in each repository. That
makes for an easy development flow, but doesn’t make it very easy for you to get
a single view of all the issues that affect the whole release.

The purpose of this document is to provide that single view of all the key issues
we are aware of. It isn’t a complete list; it’s a filtered and reviewed list,
focusing on the issues we thought you’d want to be aware of. Each item explains
the problem, as well as workarounds if those are possible. For items filed through
GitHub, we’ve included a link to the issue so that you can follow the discussion
and code - or even suggest a solution.

For more information about an issue, contact us on the [forums](forums.mbed.com).

### Other information not in this document

We’re still very actively building mbed OS and the 15.11 release is a technology
preview. As such there are some other limitations of the release that you can
find described in the
[release note](https://www.mbed.com/en/development/software/mbed-os/releases/mbed-os1511).
This document doesn’t provide a complete list of known issues for experimental
features, such as Thread; those will be published in subsequent releases.

Other tools such as [yotta](https://github.com/ARMmbed/yotta) and
[greentea](https://github.com/ARMmbed/greentea) also have their own lists, which
you can see in their public GitHub repositories.

#### Important Note for Windows Users

If you are using this release on Microsoft Windows, please be advised that
because of the way Windows handles filename and paths, you may have problems
if you attempt to use this in a deep directory hierarchy with a long
path name (e.g. `C:\some_long_directory_over_one_hundred_characters_long\`). If
you experience problems unpacking or building this release, please try it in a
location with a shorter path before filing a bug. Thanks.

***

### `mbed-client-example-6lowpan` does not work with armcc 5.03 in Thread mode

*Description*: When building the example application using armcc compiler
version 5.03, it does not join the Thread network anymore.

*Workaround*: None

*Reported Issue*: https://github.com/ARMmbed/mbed-client-example-6lowpan/issues/35

*Priority*: Critical

### Mesh network is insecure

*Description*: Mesh network is insecure:

* `mbed-mesh-api` does not provide an API for changing the security settings.
* gateway binary releases are currently operating in insecure mode.

*Workaround*: None

*Reported Issue*: ARM internal reference ONME-2076

*Priority*: Critical

### core-util allocators should not be copiable

*Description*: PoolAllocator and ExtendablePoolAllocator are currently copiable.
This is not desirable because copying either of these structures could lead to
broken behaviour, such as double-allocations and double-frees.  This also affects
BinaryHeap indirectly, since it is built on top of ExtendablePoolAllocator.

*Workaround*: Until PoolAllocator, ExtendablePoolAllocator, and BinaryHeap are
fixed, care should be taken to ensure that they are only ever passed by reference
and that no assignments are done to objects of either of these classes.

*Reported Issue*: https://github.com/ARMmbed/core-util/issues/11

*Priority*: Critical

### BLE service discovery procedure may fail with long UUIDs

*Description*: When a BLE API Gatt Client launches a discovery procedure, it can
fail if the client discovers a server which uses long UUIDs. Such failure will leave
the BLE stack in an inconsistent state.

*Workaround*: None

*Reported Issue*: https://github.com/ARMmbed/ble-nrf51822/issues/27

*Priority*: Critical

### uVisor cannot be enabled on targets built with armcc

*Description*: Some uVisor APIs rely on complex inline assembly, which is not
fully supported by the ARM Compiler 5. Their implementation requires a completely
different approach, which we are working on. For this release though, we will not
support armcc.

*Workaround*: All targets that support uVisor and are built with armcc will still
compile and work, but the security features of uVisor will not be available. uVisor
APIs will still be available, but no security measure will be enabled.

*Reported Issue*: https://github.com/ARMmbed/uvisor/issues/89

*Priority*: Critical

### ICMP ping fails to last hop, which radio packet MTU size (127) allows to join network

*Description*: When radio packet MTU is 127 bytes, the ICMP ping reaches only nodes
that are at maximum nine hops away.

*Workaround*: None

*Reported Issue*: ARM internal reference ONME-1611

*Priority*: Major

### Multicast (MPL) ping does not work over seven hops

*Description*: Multicast (MPL) ICMPv6 echo packets do not get forwarded after six hops.

*Workaround*: None

*Reported Issue*: ARM internal reference ONME-1686

*Priority*: Major

### RPL: On routing loop, an error flag is not set in the Hop-by-hop RPL option

*Description*: Routing loop is not detected with data packets in a three-node loop.
Data packets get forwarded but no proper flag is set.

*Workaround*: None

*Reported Issue*: ARM internal reference ONME-2017

*Priority*: Major

### 6LoWPAN socket adaptation layer does not support DNS

*Description*: 6LoWPAN socket adaptation layer does not support DNS.

*Workaround*: IPv6 addresses must be given in ASCII format.

*Reported Issue*: https://github.com/ARMmbed/sal-iface-6lowpan/issues/12

*Priority*: Major

### 6LoWPAN socket adaptation layer has incomplete C++ API

*Description*: The following mbed C++ Socket API methods are not implemented
in `sal-iface-6lowpan`:

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

*Workaround*: None

*Reported Issue*: https://github.com/ARMmbed/sal-iface-6lowpan/issues/11

*Priority*: Major

### RPL does not select secondary parent when switching primary parent.

*Description*: When mesh network is set up using 6LoWPAN-ND mode, the networking
stack automatically selects the RPL primary parent for routing. When a better
primary parent candidate appears in the network, it is selected - but the previous
primary is not delegated to be a secondary parent. This is non-optimal behaviour
for an RPL mesh network.

*Workaround*: None

*Reported Issue*:

*Priority*: Major

### Only a single sal-stack can be used with the socket API

*Description*: The mbed OS socket API handles the periodic task provided by the
SAL incorrectly. Because of this, only a single stack can be used at a time.

*Workaround*: Use the SAL to extract the periodic function
(`void (*task)() = socket_get_api(STACK_ID)->periodic_task()`) and periodic interval
(`uint32_t interval = socket_get_api(STACK_ID)->periodic_interval()`), then schedule
a recurring callback in MINAR for each stack
(`minar::Scheduler::postCallback(task).period(minar::milliseconds(interval)`).

*Reported Issue*: https://github.com/ARMmbed/sockets/issues/36

*Priority*: Major

### Weak symbols are not overridden

*Description*: Weak symbols compiled using yotta with a mbed-gcc derived target are
not overridden.  This is because linking is done through archives, not object files.
When ld finds a weak symbol in an archive, it is only overridden if it finds a strong
symbol in an object file.  If a strong symbol exists in an archive, it is not used
because archives are only inspected if a symbol is missing and weak symbols are not
strictly missing.  The most obvious effect of this defect is that `mbed_mac_address`
is not overridden.

*Workaround*: Currently, there is no workaround.  It is possible that one could be
implemented with yotta config, specifically for mbed_mac_address, but there is no
obvious general solution other than migrating code away from using weak symbols.

*Reported Issue*: https://github.com/ARMmbed/mbed-hal-frdm-k64f/issues/3

*Priority*: Major

### Distinguish between read and write access faults in uVisor

*Description*: When creating a read-only region in uVisor, write access will create an
access fault as expected, but it needs to avoid configuring the corresponding MPU
region again. The intended behavior is to fault with a security exception.

*Workaround*: Do not write to read-only memory regions.

*Reported Issue*: https://github.com/ARMmbed/uvisor/issues/68

*Priority*: Major

### Hardware floating point is currently disabled

*Description*: uVisor has not yet implemented full handling of the FPU register
file and exception model. Until the FPU is fully supported in uVisor, mbed OS must
be used with hardware floating point disabled.

*Workaround*: Soft-floating point can be used (providing complete functionality,
but with a performance and power impact compared to hard-FP).

*Reported Issue*: https://github.com/ARMmbed/uvisor/issues/88

*Priority*: Major

### mbed Client will occasionally disconnect from LWM2M Server because of network errors

*Description*: If mbed Client is kept running for long durations (over 24 hours)
with long lifetime values, it occasionally  goes offline due to unstable network
conditions - and doesn't send periodic updates to LWM2M server.

*Workaround*: Set the periodic lifetime value to less than 15 minutes if you want
to run stability tests. Also, implement a network error handling mechanism on the
application side, to handle `error()` callbacks received from the mbed-client library.

*Reported Issue*: ARM internal reference IOTCLT-206

*Priority*: Major

### mbed Client might experience a memory leak when running for long durations

*Description*: mbed Client might have memory leak issues when left running for
longer than 12 hours.

*Workaround*: None

*Reported Issue*: ARM internal reference IOTCLT-290

*Priority*: Major

### mbed Client API may not be fully interoperable with other LWM2M servers.

*Description*: mbed Client API is OMA LWM2M compatible. However, some features may
not be fully interoperable against other open source LWM2M servers. This is the
first release version and more features will be made interoperable over coming releases.

*Workaround*: mbed Client is compatible with mbed Device Connector Service, which
can be tested at [https://connector.mbed.com](https://connector.mbed.com).

*Reported Issue*: ARM internal reference IOTCLT-366

*Priority*: Major

### DTLS datagram drop on single record header epoch failure

*Description*: When mbed TLS is acting as a client, it will resend the last five
datagrams packet after a server reply is lost. When working with some implementations,
there is a risk that invalid datagrams could be generated by mbed TLS which could
lead to further packet loss and failed connections. This will only occur with some
implementations of DTLS on lossy networks.

*Workaround*: We recommend application code should retry the handshake on timeout
of a successful handshake.

*Reported Issue*: https://github.com/ARMmbed/mbedtls/issues/345

*Priority*: Major

### Static IPv6 mode is not supported with current mesh gateway binary images

*Description*: Currently provided binaries for mbed mesh gateway do not support
statically set IPv6 addresses.

*Workaround*: Dynamic IPv6 bootstrap must be used. It relies on ICMPv6 router
advertisements from ethernet segment.

*Reported Issue*: https://github.com/ARMmbed/mbed-client-example-6lowpan/issues/38

*Priority*: Minor

### LwIP does not use random source port and sequence number in TCP connections

*Description*: LwIP should use random source ports and sequence numbers in TCP
connections.  Failing to do so means that remote hosts can ignore connection
requests by a device running LwIP when a connection is improperly closed and
reopened, for example by a reset.

*Workaround*: Manually bind a socket to a random port before connecting to a
remote host.  Suggested source of randomness is mbed TLS's entropy pool and
random number generator.

*Reported Issue*: https://github.com/ARMmbed/sockets/issues/17

*Priority*: Minor

### Floating point format is not supported in printf()

*Description*: If floating point data is passed to printf(), a blank space will
be displayed.

*Workaround*: None

*Reported Issue*: https://github.com/ARMmbed/target-mbed-gcc/issues/17

*Priority*: Minor

