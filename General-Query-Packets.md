---
description: General Query Packets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: General Query Packets (Debugging with GDB)
lang: en
resource-type: document
title: General Query Packets (Debugging with GDB)
---
::: header
Next: [Architecture-Specific Protocol Details](Architecture_002dSpecific-Protocol-Details.html#Architecture_002dSpecific-Protocol-Details)]
:::

---

### E.4 General Query Packets

Packets starting with '`q`' are *general set packets*. General query and set packets are a semi-unified form for retrieving and sending information to and from the stub.

The initial letter of a query or set packet is followed by a name indicating what sort of thing the packet applies to. For example, [GDB]' packet to exchange symbol definitions with the stub. These packet names follow some conventions:

- The name must not contain commas, colons or semicolons.
- Most [GDB] query and set packets have a leading upper case letter.
- The names of custom vendor packets should use a company prefix, in lower case, followed by a period. For example, packets designed at the Acme Corporation might begin with '`qacme.foo`' (for setting bars).

The name of a query or set packet should be separated from any parameters by a '`:`.

Like the descriptions of the other packets, each description here has a template showing the packet's overall syntax, followed by an explanation of the packet's meaning. We include spaces in some of the templates for clarity; these are not part of the packet's syntax. No [GDB] packet uses spaces to separate its components.

Here are the currently defined query and set packets:

'`QAgent:1`'
'`QAgent:0`'

:   Turn on or off the agent as a helper to perform some debugging operations delegated from [GDB] (see [Control Agent](In_002dProcess-Agent.html#Control-Agent)).

'`QAllow:op:val…`'

:

```
Specify which operations [GDB] will not request the operation, or 1, indicating that it may. (The target can then use this to set up its own internals optimally, for instance if the debugger never expects to insert breakpoints, it may not need to install its own trap handler.)
```

'`qC`'

:

```
Return the current thread ID.

Reply:

'`QC thread-id`'

:   Where `thread-id` is a thread ID as documented in [thread-id syntax](Packets.html#thread_002did-syntax).

'`(anything else)`'

:   Any other reply implies the old thread ID.
```

'`qCRC:addr,length`'

:

```
Compute the CRC checksum of a block of memory using CRC-32 defined in IEEE 802.3. The CRC is computed byte at a time, taking the most significant bit of each byte first. The initial pattern code `0xffffffff` is used to ensure leading zeros affect the CRC.

*Note:* This is the same CRC used in validating separate debug files (see [Debugging Information in Separate Files](Separate-Debug-Files.html#Separate-Debug-Files)). However the algorithm is slightly different. When validating separate debug files, the CRC is computed taking the *least* significant bit of each byte first, and the final result is inverted to detect trailing zeros.

Reply:

'`E NN`'

:   An error (such as memory fault)

'`C crc32`'

:   The specified memory region's checksum is `crc32`.
```

'`QDisableRandomization:value`'

:

```
Some target operating systems will randomize the virtual address space of the inferior process as a security feature, but provide a feature to disable such randomization, e.g. to allow for a more deterministic debugging experience. On such systems, this packet with a `value` of 0 tells the target to enable address space randomization.

This packet is only available in extended mode (see [extended mode](Packets.html#extended-mode)).

Reply:

'`OK`'

:   The request succeeded.

'`E nn`'

:   An error occurred. The error number `nn` is given as hex digits.

'``'

:   An empty reply indicates that '`QDisableRandomization`' is not supported by the stub.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)). This should only be done on targets that actually support disabling address space randomization.
```

'`QStartupWithShell:value`'

:

```
On UNIX-like targets, it is possible to start the inferior using a shell program. This is the default behavior on both [GDB] and `gdbserver` (see [set startup-with-shell](Starting.html#set-startup_002dwith_002dshell)). This packet is used to inform `gdbserver` whether it should start the inferior using a shell or not.

If `value`', `gdbserver` will use a shell to start the inferior. All other values are considered an error.

This packet is only available in extended mode (see [extended mode](Packets.html#extended-mode)).

Reply:

'`OK`'

:   The request succeeded.

'`E nn`'

:   An error occurred. The error number `nn` is given as hex digits.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)). This should only be done on targets that actually support starting the inferior using a shell.

Use of this packet is controlled by the `set startup-with-shell` command; see [set startup-with-shell](Starting.html#set-startup_002dwith_002dshell).
```

'`QEnvironmentHexEncoded:hex-value`'

:

```
On UNIX-like targets, it is possible to set environment variables that will be passed to the inferior during the startup process. This packet is used to inform `gdbserver` of an environment variable that has been defined by the user on [GDB] (see [set environment](Environment.html#set-environment)).

The packet is composed by `hex-value` will not be present.

This packet is only available in extended mode (see [extended mode](Packets.html#extended-mode)).

Reply:

'`OK`'

:   The request succeeded.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)). This should only be done on targets that actually support passing environment variables to the starting inferior.

This packet is related to the `set environment` command; see [set environment](Environment.html#set-environment).
```

'`QEnvironmentUnset:hex-value`'

:

```
On UNIX-like targets, it is possible to unset environment variables before starting the inferior in the remote target. This packet is used to inform `gdbserver` of an environment variable that has been unset by the user on [GDB] (see [unset environment](Environment.html#unset-environment)).

The packet is composed by `hex-value`, an hex encoded representation of the name of the environment variable to be unset.

This packet is only available in extended mode (see [extended mode](Packets.html#extended-mode)).

Reply:

'`OK`'

:   The request succeeded.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)). This should only be done on targets that actually support passing environment variables to the starting inferior.

This packet is related to the `unset environment` command; see [unset environment](Environment.html#unset-environment).
```

'`QEnvironmentReset`'

:

```
On UNIX-like targets, this packet is used to reset the state of environment variables in the remote target before starting the inferior. In this context, reset means unsetting all environment variables that were previously set by the user (i.e., were not initially present in the environment). It is sent to `gdbserver` before the '`QEnvironmentHexEncoded`' (see [QEnvironmentUnset](#QEnvironmentUnset)) packets.

This packet is only available in extended mode (see [extended mode](Packets.html#extended-mode)).

Reply:

'`OK`'

:   The request succeeded.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)). This should only be done on targets that actually support passing environment variables to the starting inferior.
```

'`QSetWorkingDir:[directory]`'

:

```
This packet is used to inform the remote server of the intended current working directory for programs that are going to be executed.

The packet is composed by `directory` is an empty string, the remote server should reset the inferior's current working directory to its original, empty value.

This packet is only available in extended mode (see [extended mode](Packets.html#extended-mode)).

Reply:

'`OK`'

:   The request succeeded.
```

'`qfThreadInfo`'
'`qsThreadInfo`'

:

```
Obtain a list of all active thread IDs from the target (OS). Since there may be too many active threads to fit into one reply packet, this query works iteratively: it may require more than one query/reply sequence to obtain the entire list of threads. The first query of the sequence will be the '`qfThreadInfo`' query.

NOTE: This packet replaces the '`qL`' query (see below).

Reply:

'`m thread-id`'

:   A single thread ID

'`m thread-id,thread-id…`'

:   a comma-separated list of thread IDs

'`l`'

:   (lower case letter '`L`') denotes end of list.

In response to each query, the target will reply with a list of one or more thread IDs, separated by commas. [GDB] fields.

*Note: [GDB].*
```

'`qGetTLSAddr:thread-id,offset,lm`'

:

```
Fetch the address associated with thread local storage specified by `thread-id`.

`thread-id` is the thread ID associated with the thread for which to fetch the TLS address. See [thread-id syntax](Packets.html#thread_002did-syntax).

`offset` is the (big endian, hex encoded) offset associated with the thread local variable. (This offset is obtained from the debug information associated with the variable.)

`lm`/Linux system will pass the link map address of the shared object associated with the thread local storage under consideration. Other operating environments may choose to represent the load module differently, so the precise meaning of this parameter will vary.

Reply:

'`XX…`'

:   Hex encoded (big endian) bytes representing the address of the thread local storage requested.

'`E nn`'

:   An error occurred. The error number `nn` is given as hex digits.

'``'

:   An empty reply indicates that '`qGetTLSAddr`' is not supported by the stub.
```

'`qGetTIBAddr:thread-id`'

:

```
Fetch address of the Windows OS specific Thread Information Block.

`thread-id` is the thread ID associated with the thread.

Reply:

'`XX…`'

:   Hex encoded (big endian) bytes representing the linear address of the thread information block.

'`E nn`'

:   An error occurred. This means that either the thread was not found, or the address could not be retrieved.

'``'

:   An empty reply indicates that '`qGetTIBAddr`' is not supported by the stub.
```

'`qL startflag threadcount nextthread`'

:   Obtain thread information from RTOS. Where: `startflag`.

```
Don't use this packet; use the '`qfThreadInfo`' query instead (see above).

Reply:

'`qM count done argthread thread…`'

:   Where: `count` (eight hex digits), from the target. See `remote.c:parse_threadlist_response()`.
```

'`qMemTags:start address,length:type`'

:

```
Fetch memory tags of type `type`. The target is responsible for calculating how many tags will be returned, as this is architecture-specific.

`start address` is the starting address of the memory range.

`length` is the length, in bytes, of the memory range.

`type` is the type of tag the request wants to fetch. The type is a signed integer.

Reply:

'`mxx…`'

:   Hex encoded sequence of uninterpreted bytes, `xx`..., representing the tags found in the requested memory range.

'`E nn`'

:   An error occurred. This means that fetching of memory tags failed for some reason.

'``'

:   An empty reply indicates that '`qMemTags`'.
```

'`QMemTags:start address,length:type:tag bytes`'

:

```
Store memory tags of type `type`. The target is responsible for interpreting the type, the tag bytes and modifying the memory tag granules accordingly, given this is architecture-specific.

The interpretation of how many tags (`nt`) is also architecture-specific. The behavior is implementation-specific, but the following is suggested.

If the number of memory tags, `nt` tags will be stored.

If `nt` tags are stored.

`start address` is the starting address of the memory range. The address does not have any restriction on alignment or size.

`length` is the length, in bytes, of the memory range.

`type` is the type of tag the request wants to fetch. The type is a signed integer.

`tag bytes` is a sequence of hex encoded uninterpreted bytes which will be interpreted by the target. Each pair of hex digits is interpreted as a single byte.

Reply:

'`OK`'

:   The request was successful and the memory tag granules were modified accordingly.

'`E nn`'

:   An error occurred. This means that modifying the memory tag granules failed for some reason.

'``'

:   An empty reply indicates that '`QMemTags`'.
```

'`qOffsets`'

:

```
Get section offsets that the target used when relocating the downloaded image.

Reply:

'`Text=xxx;Data=yyy[;Bss=zzz]`'

:   Relocate the `Text` section by `xxx` will relocate entire segments by the supplied offsets.

    *Note: while a `Bss` offset may be included in the response, [GDB] ignores this and instead applies the `Data` offset to the `Bss` section.*

'`TextSeg=xxx[;DataSeg=yyy]`'

:   Relocate the first segment of the object file, which conventionally contains program code, to a starting address of `xxx` will report an error if the object file does not contain segment information, or does not contain at least as many segments as mentioned in the reply. Extra segments are kept at fixed offsets relative to the last relocated segment.
```

'`qP mode thread-id`'

:

```
Returns information on `thread-id` is a thread ID (see [thread-id syntax](Packets.html#thread_002did-syntax)).

Don't use this packet; use the '`qThreadExtraInfo`' query instead (see below).

Reply: see `remote.c:remote_unpack_thread_info_response()`.
```

'`QNonStop:1`'
'`QNonStop:0`'

:

```
Enter non-stop ('`QNonStop:1`') mode. See [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop), for more information.

Reply:

'`OK`'

:   The request succeeded.

'`E nn`'

:   An error occurred. The error number `nn` is given as hex digits.

'``'

:   An empty reply indicates that '`QNonStop`' is not supported by the stub.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)). Use of this packet is controlled by the `set non-stop` command; see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode).
```

'`QCatchSyscalls:1 [;sysno]…`'
'`QCatchSyscalls:0`'

:

```
Enable ('`QCatchSyscalls:1`') catching syscalls from the inferior process.

For '`QCatchSyscalls:1` is listed, every system call should be reported.

Note that if a syscall not in the list is reported, [GDB] will still filter the event according to its own list from all corresponding `catch syscall` commands. However, it is more efficient to only report the requested syscalls.

Multiple '`QCatchSyscalls:1`' list is completely replaced by the new list.

If the inferior process execs, the state of '`QCatchSyscalls`' is kept for the new process too. On targets where exec may affect syscall numbers, for example with exec between 32 and 64-bit processes, the client should send a new packet with the new syscall list.

Reply:

'`OK`'

:   The request succeeded.

'`E nn`'

:   An error occurred. `nn` are hex digits.

'``'

:   An empty reply indicates that '`QCatchSyscalls`' is not supported by the stub.

Use of this packet is controlled by the `set remote catch-syscalls` command (see [set remote catch-syscalls](Remote-Configuration.html#Remote-Configuration)). This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`QPassSignals: signal [;signal]…`'

:

```
Each listed `signal`'.

Reply:

'`OK`'

:   The request succeeded.

'`E nn`'

:   An error occurred. The error number `nn` is given as hex digits.

'``'

:   An empty reply indicates that '`QPassSignals`' is not supported by the stub.

Use of this packet is controlled by the `set remote pass-signals` command (see [set remote pass-signals](Remote-Configuration.html#Remote-Configuration)). This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`QProgramSignals: signal [;signal]…`'

:

```
Each listed `signal` may be delivered to the inferior process. Others should be silently discarded.

In some cases, the remote stub may need to decide whether to deliver a signal to the program or not without [GDB], and so the remote stub can use the signal list specified by this packet to know whether to deliver or ignore those pending signals.

This does not influence whether to deliver a signal as requested by a resumption packet (see [vCont packet](Packets.html#vCont-packet)).

Signals are numbered identically to continue packets and stop replies (see [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets)). Each `signal`' list is completely replaced by the new list.

Reply:

'`OK`'

:   The request succeeded.

'`E nn`'

:   An error occurred. The error number `nn` is given as hex digits.

'``'

:   An empty reply indicates that '`QProgramSignals`' is not supported by the stub.

Use of this packet is controlled by the `set remote program-signals` command (see [set remote program-signals](Remote-Configuration.html#Remote-Configuration)). This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).


```

'`QThreadEvents:1`'
'`QThreadEvents:0`'

:

```
Enable ('`QThreadEvents:1`' reply.

Reply:

'`OK`'

:   The request succeeded.

'`E nn`'

:   An error occurred. The error number `nn` is given as hex digits.

'``'

:   An empty reply indicates that '`QThreadEvents`' is not supported by the stub.

Use of this packet is controlled by the `set remote thread-events` command (see [set remote thread-events](Remote-Configuration.html#Remote-Configuration)).
```

'`qRcmd,command`'

:

```
`command`' console output packets. *Implementors should note that providing access to a stubs's interpreter may have security implications*.

Reply:

'`OK`'

:   A command response with no output.

'`OUTPUT`'

:   A command response with the hex encoded output string `OUTPUT`.

'`E NN`'

:   Indicate a badly formed request. The error number `NN` is given as hex digits.

'``'

:   An empty reply indicates that '`qRcmd`' is not recognized.

(Note that the `qRcmd` packet's name is separated from the command by a '`,`', contrary to the naming conventions above. Please don't use this packet as a model for new packets.)
```

'`qSearch:memory:address;length;search-pattern`'

:

```
Search `length` is a sequence of bytes, also hex encoded.

Reply:

'`0`'

:   The pattern was not found.

'`1,address`'

:   The pattern was found at `address`.

'`E NN`'

:   A badly formed request or an error was encountered while searching memory.

'``'

:   An empty reply indicates that '`qSearch:memory`' is not recognized.
```

'`QStartNoAckMode`'

:

```
Request that the remote stub disable the normal '`+`' protocol acknowledgments (see [Packet Acknowledgment](Packet-Acknowledgment.html#Packet-Acknowledgment)).

Reply:

'`OK`'

:   The stub has switched to no-acknowledgment mode. [GDB]' acknowledgments in the current connection.

'``'

:   An empty reply indicates that the stub does not support no-acknowledgment mode.
```

'`qSupported [:gdbfeature [;gdbfeature]… ]`'

:

```
Tell the remote stub about features supported by [GDB] which support increasing numbers of packets.

Reply:

'`stubfeature [;stubfeature]…`'

:   The stub supports or does not support each returned `stubfeature` (see below for the possible forms).

'``'

:   An empty reply indicates that '`qSupported`.

The allowed forms for each feature (either a `gdbfeature` in the response) are:

'`name=value`'

:   The remote protocol feature `name` depends on the feature, but it must not include a semicolon.

'`name+`'

:   The remote protocol feature `name` is supported, and does not need an associated value.

'`name-`'

:   The remote protocol feature `name` is not supported.

'`name?`'

:   The remote protocol feature `name` responses.

Whenever the stub receives a '`qSupported`.

The following values of `gdbfeature`) are defined:

'`multiprocess`'

:   This feature indicates whether [GDB]' reply. See [multiprocess extensions](#multiprocess-extensions), for details.

'`xmlRegisters`'

:   This feature indicates that [GDB]' with target specific strings separated by a comma, it will report register description.

'`qRelocInsn`'

:   This feature indicates whether [GDB]' packet (see [Relocate instruction reply packet](Tracepoint-Packets.html#Tracepoint-Packets)).

'`swbreak`'

:   This feature indicates whether [GDB] supports the swbreak stop reason in stop replies. See [swbreak stop reason](Stop-Reply-Packets.html#swbreak-stop-reason), for details.

'`hwbreak`'

:   This feature indicates whether [GDB] supports the hwbreak stop reason in stop replies. See [swbreak stop reason](Stop-Reply-Packets.html#swbreak-stop-reason), for details.

'`fork-events`'

:   This feature indicates whether [GDB]' reply.

'`vfork-events`'

:   This feature indicates whether [GDB]' reply.

'`exec-events`'

:   This feature indicates whether [GDB]' reply.

'`vContSupported`'

:   This feature indicates whether [GDB]' packet.

Stubs should ignore any unknown values for `gdbfeature` describes all the features it supports, and then the stub replies with all the features it supports.

Similarly, [GDB] will silently ignore unrecognized stub feature responses, as long as each response uses one of the standard forms.

Some features are flags. A stub which supports a flag feature should respond with a '`+`' form response.

Each feature has a default value, which [GDB]' response. The default values are fixed; a stub is free to omit any feature responses that match the defaults.

Not all features can be probed, but for those which can, the probing mechanism is useful: in some cases, a stub's internal architecture may not allow the protocol layer to know some information about the underlying target in advance. This is especially common in stubs which may be configured for multiple targets.

These are the currently defined stub features and their properties:

  -------------------------------------------- ---------------- ---------------- ---------------
  Feature Name                                 Value Required   Default          Probe Allowed
  '`PacketSize`'   No
  '`qXfer:auxv:read`'   Yes
  '`qXfer:btrace:read`'   Yes
  '`qXfer:btrace-conf:read`'   Yes
  '`qXfer:exec-file:read`'   Yes
  '`qXfer:features:read`'   Yes
  '`qXfer:libraries:read`'   Yes
  '`qXfer:libraries-svr4:read`'   Yes
  '`augmented-libraries-svr4-read`'   No
  '`qXfer:memory-map:read`'   Yes
  '`qXfer:sdata:read`'   Yes
  '`qXfer:siginfo:read`'   Yes
  '`qXfer:siginfo:write`'   Yes
  '`qXfer:threads:read`'   Yes
  '`qXfer:traceframe-info:read`'   Yes
  '`qXfer:uib:read`'   Yes
  '`qXfer:fdpic:read`'   Yes
  '`Qbtrace:off`'   Yes
  '`Qbtrace:bts`'   Yes
  '`Qbtrace:pt`'   Yes
  '`Qbtrace-conf:bts:size`'   Yes
  '`Qbtrace-conf:pt:size`'   Yes
  '`QNonStop`'   Yes
  '`QCatchSyscalls`'   Yes
  '`QPassSignals`'   Yes
  '`QStartNoAckMode`'   Yes
  '`multiprocess`'   No
  '`ConditionalBreakpoints`'   No
  '`ConditionalTracepoints`'   No
  '`ReverseContinue`'   No
  '`ReverseStep`'   No
  '`TracepointSource`'   No
  '`QAgent`'   No
  '`QAllow`'   No
  '`QDisableRandomization`'   No
  '`EnableDisableTracepoints`'   No
  '`QTBuffer:size`'   No
  '`tracenz`'   No
  '`BreakpointCommands`'   No
  '`swbreak`'   No
  '`hwbreak`'   No
  '`fork-events`'   No
  '`vfork-events`'   No
  '`exec-events`'   No
  '`QThreadEvents`'   No
  '`no-resumed`'   No
  '`memory-tagging`'   No
  -------------------------------------------- ---------------- ---------------- ---------------

These are the currently defined stub features, in more detail:
```

:

'`PacketSize=bytes`'

:   The remote stub can accept packets up to at least `bytes`' packet response.

'`qXfer:auxv:read`'

:   The remote stub understands the '`qXfer:auxv:read`' packet (see [qXfer auxiliary vector read](#qXfer-auxiliary-vector-read)).

'`qXfer:btrace:read`'

:   The remote stub understands the '`qXfer:btrace:read`' packet (see [qXfer btrace read](#qXfer-btrace-read)).

'`qXfer:btrace-conf:read`'

:   The remote stub understands the '`qXfer:btrace-conf:read`' packet (see [qXfer btrace-conf read](#qXfer-btrace_002dconf-read)).

'`qXfer:exec-file:read`'

:   The remote stub understands the '`qXfer:exec-file:read`' packet (see [qXfer executable filename read](#qXfer-executable-filename-read)).

'`qXfer:features:read`'

:   The remote stub understands the '`qXfer:features:read`' packet (see [qXfer target description read](#qXfer-target-description-read)).

'`qXfer:libraries:read`'

:   The remote stub understands the '`qXfer:libraries:read`' packet (see [qXfer library list read](#qXfer-library-list-read)).

'`qXfer:libraries-svr4:read`'

:   The remote stub understands the '`qXfer:libraries-svr4:read`' packet (see [qXfer svr4 library list read](#qXfer-svr4-library-list-read)).

'`augmented-libraries-svr4-read`'

:   The remote stub understands the augmented form of the '`qXfer:libraries-svr4:read`' packet (see [qXfer svr4 library list read](#qXfer-svr4-library-list-read)).

'`qXfer:memory-map:read`'

:   The remote stub understands the '`qXfer:memory-map:read`' packet (see [qXfer memory map read](#qXfer-memory-map-read)).

'`qXfer:sdata:read`'

:   The remote stub understands the '`qXfer:sdata:read`' packet (see [qXfer sdata read](#qXfer-sdata-read)).

'`qXfer:siginfo:read`'

:   The remote stub understands the '`qXfer:siginfo:read`' packet (see [qXfer siginfo read](#qXfer-siginfo-read)).

'`qXfer:siginfo:write`'

:   The remote stub understands the '`qXfer:siginfo:write`' packet (see [qXfer siginfo write](#qXfer-siginfo-write)).

'`qXfer:threads:read`'

:   The remote stub understands the '`qXfer:threads:read`' packet (see [qXfer threads read](#qXfer-threads-read)).

'`qXfer:traceframe-info:read`'

:   The remote stub understands the '`qXfer:traceframe-info:read`' packet (see [qXfer traceframe info read](#qXfer-traceframe-info-read)).

'`qXfer:uib:read`'

:   The remote stub understands the '`qXfer:uib:read`' packet (see [qXfer unwind info block](#qXfer-unwind-info-block)).

'`qXfer:fdpic:read`'

:   The remote stub understands the '`qXfer:fdpic:read`' packet (see [qXfer fdpic loadmap read](#qXfer-fdpic-loadmap-read)).

'`QNonStop`'

:   The remote stub understands the '`QNonStop`' packet (see [QNonStop](#QNonStop)).

'`QCatchSyscalls`'

:   The remote stub understands the '`QCatchSyscalls`' packet (see [QCatchSyscalls](#QCatchSyscalls)).

'`QPassSignals`'

:   The remote stub understands the '`QPassSignals`' packet (see [QPassSignals](#QPassSignals)).

'`QStartNoAckMode`'

:   The remote stub understands the '`QStartNoAckMode`' packet and prefers to operate in no-acknowledgment mode. See [Packet Acknowledgment](Packet-Acknowledgment.html#Packet-Acknowledgment).

'`multiprocess`'

:

```
The remote stub understands the multiprocess extensions to the remote protocol syntax. The multiprocess extensions affect the syntax of thread IDs in both packets and replies (see [thread-id syntax](Packets.html#thread_002did-syntax)), and add process IDs to the '`D`' request.
```

'`qXfer:osdata:read`'

:   The remote stub understands the '`qXfer:osdata:read`' packet ((see [qXfer osdata read](#qXfer-osdata-read)).

'`ConditionalBreakpoints`'

:   The target accepts and implements evaluation of conditional expressions defined for breakpoints. The target will only report breakpoint triggers when such conditions are true (see [Break Conditions](Conditions.html#Conditions)).

'`ConditionalTracepoints`'

:   The remote stub accepts and implements conditional expressions defined for tracepoints (see [Tracepoint Conditions](Tracepoint-Conditions.html#Tracepoint-Conditions)).

'`ReverseContinue`'

:   The remote stub accepts and implements the reverse continue packet (see [bc](Packets.html#bc)).

'`ReverseStep`'

:   The remote stub accepts and implements the reverse step packet (see [bs](Packets.html#bs)).

'`TracepointSource`'

:   The remote stub understands the '`QTDPsrc`' packet that supplies the source form of tracepoint definitions.

'`QAgent`'

:   The remote stub understands the '`QAgent`' packet.

'`QAllow`'

:   The remote stub understands the '`QAllow`' packet.

'`QDisableRandomization`'

:   The remote stub understands the '`QDisableRandomization`' packet.

'`StaticTracepoint`'

:

```
The remote stub supports static tracepoints.
```

'`InstallInTrace`'

:

```
The remote stub supports installing tracepoint in tracing.
```

'`EnableDisableTracepoints`'

:   The remote stub supports the '`QTEnable`' (see [QTDisable](Tracepoint-Packets.html#QTDisable)) packets that allow tracepoints to be enabled and disabled while a trace experiment is running.

'`QTBuffer:size`'

:   The remote stub supports the '`QTBuffer:size`' (see [QTBuffer-size](Tracepoint-Packets.html#QTBuffer_002dsize)) packet that allows to change the size of the trace buffer.

'`tracenz`'

:

```
The remote stub supports the '`tracenz`' bytecode for collecting strings. See [Bytecode Descriptions](Bytecode-Descriptions.html#Bytecode-Descriptions) for details about the bytecode.
```

'`BreakpointCommands`'

:

```
The remote stub supports running a breakpoint's command list itself, rather than reporting the hit to [GDB].
```

'`Qbtrace:off`'

:   The remote stub understands the '`Qbtrace:off`' packet.

'`Qbtrace:bts`'

:   The remote stub understands the '`Qbtrace:bts`' packet.

'`Qbtrace:pt`'

:   The remote stub understands the '`Qbtrace:pt`' packet.

'`Qbtrace-conf:bts:size`'

:   The remote stub understands the '`Qbtrace-conf:bts:size`' packet.

'`Qbtrace-conf:pt:size`'

:   The remote stub understands the '`Qbtrace-conf:pt:size`' packet.

'`swbreak`'

:   The remote stub reports the '`swbreak`' stop reason for memory breakpoints.

'`hwbreak`'

:   The remote stub reports the '`hwbreak`' stop reason for hardware breakpoints.

'`fork-events`'

:   The remote stub reports the '`fork`' stop reason for fork events.

'`vfork-events`'

:   The remote stub reports the '`vfork`' stop reason for vfork events and vforkdone events.

'`exec-events`'

:   The remote stub reports the '`exec`' stop reason for exec events.

'`vContSupported`'

:   The remote stub reports the supported actions in the reply to '`vCont?`' packet.

'`QThreadEvents`'

:   The remote stub understands the '`QThreadEvents`' packet.

'`no-resumed`'

:   The remote stub reports the '`N`' stop reply.

'`memory-tagging`'

:   The remote stub supports and implements the required memory tagging functionality and understands the '`qMemTags`' (see [QMemTags](#QMemTags)) packets.

```
For AArch64 GNU/Linux systems, this feature also requires access to the `/proc/pid/smaps`' requests.
```

'`qSymbol::`'

Notify the target that [GDB] is prepared to serve symbol lookup requests. Accept requests from the target for the values of symbols.

Reply:

'`OK`'

:   The target does not need to look up any (more) symbols.

'`qSymbol:sym_name`'

:   The target requests the value of symbol `sym_name`' message, described below.

'`qSymbol:sym_value:sym_name`'

Set the value of `sym_name`.

`sym_name` (hex encoded) is the name of a symbol whose value the target has previously requested.

`sym_value`, then this field will be empty.

Reply:

'`OK`'

:   The target does not need to look up any (more) symbols.

'`qSymbol:sym_name`'

:   The target requests the value of a new symbol `sym_name` will continue to supply the values of symbols (if available), until the target ceases to request them.

'`qTBuffer`'

'`QTBuffer`'

'`QTDisconnected`'

'`QTDP`'

'`QTDPsrc`'

'`QTDV`'

'`qTfP`'

'`qTfV`'

'`QTFrame`'

'`qTMinFTPILen`'

See [Tracepoint Packets](Tracepoint-Packets.html#Tracepoint-Packets).

'`qThreadExtraInfo,thread-id`'

Obtain from the target OS a printable string description of thread attributes for the thread `thread-id`'.

Reply:

'`XX…`'

:   Where '`XX…` data, comprising the printable string containing the extra information about the thread's attributes.

(Note that the `qThreadExtraInfo` packet's name is separated from the command by a '`,`', contrary to the naming conventions above. Please don't use this packet as a model for new packets.)

'`QTNotes`'

'`qTP`'

'`QTSave`'

'`qTsP`'

'`qTsV`'

'`QTStart`'

'`QTStop`'

'`QTEnable`'

'`QTDisable`'

'`QTinit`'

'`QTro`'

'`qTStatus`'

'`qTV`'

'`qTfSTM`'

'`qTsSTM`'

'`qTSTMat`'

See [Tracepoint Packets](Tracepoint-Packets.html#Tracepoint-Packets).

'`qXfer:object:read:annex:offset,length`'

Read uninterpreted bytes from the target's special data area identified by the keyword `object`; it can supply additional details about what data to access.

Reply:

'`m data`'

:   Data `data` in the request.

'`l data`'

:   Data `data` in the request.

'`l`'

:   The `offset` in the request is at the end of the data. There is no more data to be read.

'`E00`'

:   The request was malformed, or `annex` was invalid.

'`E nn`'

:   The offset was invalid, or there was an error encountered reading the data. The `nn` part is a hex-encoded `errno` value.

'``'

:   An empty reply indicates the `object` string was not recognized by the stub, or that the object does not support reading.

Here are the specific requests of this form defined so far. All the '`qXfer:object:read:…`' requests use the same reply formats, listed above.

'`qXfer:auxv:read::offset,length`'

:

```
Access the target's *auxiliary vector*. See [auxiliary vector](OS-Information.html#OS-Information). Note `annex` must be empty.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:btrace:read:annex:offset,length`'

:

```
Return a description of the current branch trace. See [Branch Trace Format](Branch-Trace-Format.html#Branch-Trace-Format). The annex part of the generic '`qXfer`' packet may have one of the following values:

`all`

:   Returns all available branch trace.

`new`

:   Returns all available branch trace if the branch trace changed since the last read request.

`delta`

:   Returns the new branch trace since the last read request. Adds a new block to the end of the trace that begins at zero and ends at the source location of the first branch in the trace buffer. This extra block is used to stitch traces together.

    If the trace buffer overflowed, returns an error indicating the overflow.

This packet is not probed by default; the remote stub must request it by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:btrace-conf:read::offset,length`'

:

```
Return a description of the current branch trace configuration. See [Branch Trace Configuration Format](Branch-Trace-Configuration-Format.html#Branch-Trace-Configuration-Format).

This packet is not probed by default; the remote stub must request it by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:exec-file:read:annex:offset,length`'

:

```
Return the full absolute name of the file that was executed to create a process running on the remote system. The annex specifies the numeric process ID of the process to query, encoded as a hexadecimal number. If the annex part is empty the remote stub should return the filename corresponding to the currently executing process.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:features:read:annex:offset,length`'

:

```
Access the *target description*. See [Target Descriptions](Target-Descriptions.html#Target-Descriptions). The annex specifies which XML document to access. The main description is always loaded from the '`target.xml`' annex.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:libraries:read:annex:offset,length`'

:

```
Access the target's list of loaded libraries. See [Library List Format](Library-List-Format.html#Library-List-Format). The annex part of the generic '`qXfer`' packet must be empty (see [qXfer read](#qXfer-read)).

Targets which maintain a list of libraries in the program's memory do not need to implement this packet; it is designed for platforms where the operating system manages the list of loaded libraries.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:libraries-svr4:read:annex:offset,length`'

:

```
Access the target's list of loaded libraries when the target is an SVR4 platform. See [Library List Format for SVR4 Targets](Library-List-Format-for-SVR4-Targets.html#Library-List-Format-for-SVR4-Targets). The annex part of the generic '`qXfer`' response (see [qXfer read](#qXfer-read), [qSupported](#qSupported)).

This packet is optional for better performance on SVR4 targets. [GDB] uses memory read packets to read the SVR4 library list otherwise.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).

If the remote stub indicates it supports the augmented form of this packet then the annex part of the generic '`qXfer`' arguments. The currently supported arguments are:

`start=address`

:   A hexadecimal number specifying the address of the '`struct link_map`' in the library list will be chosen as the starting point.

`prev=address`

:   A hexadecimal number specifying the address of the '`struct link_map`' exists prior to the starting point.

`lmid=lmid`

:   A hexadecimal number specifying a namespace identifier. This is currently only used together with '`start`'.

Arguments that are not understood by the remote stub will be silently ignored.
```

'`qXfer:memory-map:read::offset,length`'

:

```
Access the target's *memory-map*. See [Memory Map Format](Memory-Map-Format.html#Memory-Map-Format). The annex part of the generic '`qXfer`' packet must be empty (see [qXfer read](#qXfer-read)).

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:sdata:read::offset,length`'

:

```
Read contents of the extra collected static tracepoint marker information. The annex part of the generic '`qXfer`' packet must be empty (see [qXfer read](#qXfer-read)). See [Tracepoint Action Lists](Tracepoint-Actions.html#Tracepoint-Actions).

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:siginfo:read::offset,length`'

:

```
Read contents of the extra signal information on the target system. The annex part of the generic '`qXfer`' packet must be empty (see [qXfer read](#qXfer-read)).

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:threads:read::offset,length`'

:

```
Access the list of threads on target. See [Thread List Format](Thread-List-Format.html#Thread-List-Format). The annex part of the generic '`qXfer`' packet must be empty (see [qXfer read](#qXfer-read)).

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:traceframe-info:read::offset,length`'

:

```
Return a description of the current traceframe's contents. See [Traceframe Info Format](Traceframe-Info-Format.html#Traceframe-Info-Format). The annex part of the generic '`qXfer`' packet must be empty (see [qXfer read](#qXfer-read)).

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:uib:read:pc:offset,length`'

:

```
Return the unwind information block for `pc`. This packet is used on OpenVMS/ia64 to ask the kernel unwind information.

This packet is not probed by default.
```

'`qXfer:fdpic:read:annex:offset,length`'

:

```
Read contents of `loadmap`s on the target system. The annex, either '`exec`', specifies which `loadmap`, executable `loadmap` or interpreter `loadmap` to read.

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:osdata:read::offset,length`'

:

```
Access the target's *operating system information*. See [Operating System Information](Operating-System-Information.html#Operating-System-Information).
```

'`qXfer:object:write:annex:offset:data…`'

Write uninterpreted bytes into the target's special data area identified by the keyword `object`; it can supply additional details about what data to access.

Reply:

'`nn`'

:   `nn` (hex encoded) is the number of bytes written. This may be fewer bytes than supplied in the request.

'`E00`'

:   The request was malformed, or `annex` was invalid.

'`E nn`'

:   The offset was invalid, or there was an error encountered writing the data. The `nn` part is a hex-encoded `errno` value.

'``'

:   An empty reply indicates the `object` string was not recognized by the stub, or that the object does not support writing.

Here are the specific requests of this form defined so far. All the '`qXfer:object:write:…`' requests use the same reply formats, listed above.

'`qXfer:siginfo:write::offset:data…`'

:

```
Write `data`' packet must be empty (see [qXfer write](#qXfer-write)).

This packet is not probed by default; the remote stub must request it, by supplying an appropriate '`qSupported`' response (see [qSupported](#qSupported)).
```

'`qXfer:object:operation:…`'

Requests of this form may be added in the future. When a stub does not recognize the `object` keyword, the stub must respond with an empty packet.

'`qAttached:pid`'

Return an indication of whether the remote server attached to an existing process or created a new process. When the multiprocess protocol extensions are supported (see [multiprocess extensions](#multiprocess-extensions)), `pid`'.

This query is used, for example, to know whether the remote process should be detached or killed when a [GDB] session is ended with the `quit` command.

Reply:

'`1`'

:   The remote server attached to an existing process.

'`0`'

:   The remote server created a new process.

'`E NN`'

:   A badly formed request or an error was encountered.

'`Qbtrace:bts`'

Enable branch tracing for the current thread using Branch Trace Store.

Reply:

'`OK`'

:   Branch tracing has been enabled.

'`E.errtext`'

:   A badly formed request or an error was encountered.

'`Qbtrace:pt`'

Enable branch tracing for the current thread using Intel Processor Trace.

Reply:

'`OK`'

:   Branch tracing has been enabled.

'`E.errtext`'

:   A badly formed request or an error was encountered.

'`Qbtrace:off`'

Disable branch tracing for the current thread.

Reply:

'`OK`'

:   Branch tracing has been disabled.

'`E.errtext`'

:   A badly formed request or an error was encountered.

'`Qbtrace-conf:bts:size=value`'

Set the requested ring buffer size for new threads that use the btrace recording method in bts format.

Reply:

'`OK`'

:   The ring buffer size has been set.

'`E.errtext`'

:   A badly formed request or an error was encountered.

'`Qbtrace-conf:pt:size=value`'

Set the requested ring buffer size for new threads that use the btrace recording method in pt format.

Reply:

'`OK`'

:   The ring buffer size has been set.

'`E.errtext`'

:   A badly formed request or an error was encountered.

::: footnote

---

#### Footnotes

### [(22)](#DOCF22)

The '`qP`' packet has no arguments, but some existing stubs (e.g. RedBoot) are known to not check for the end of the packet.
:::

---

::: header
Next: [Architecture-Specific Protocol Details](Architecture_002dSpecific-Protocol-Details.html#Architecture_002dSpecific-Protocol-Details)]
:::
