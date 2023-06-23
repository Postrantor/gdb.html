---
description: Protocol Basics (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Protocol Basics (Debugging with GDB)
lang: en
resource-type: document
title: Protocol Basics (Debugging with GDB)
---
::: header
Next: [The F Request Packet](The-F-Request-Packet.html#The-F-Request-Packet)]
:::

---

#### E.13.2 Protocol Basics

The File-I/O protocol uses the `F` packet as the request as well as reply packet. Since a File-I/O system call can only occur when [GDB] to call the appropriate host system call:

- A unique identifier for the requested system call.
- All parameters to the system call. Pointers are given as addresses in the target memory address space. Pointers to strings are given as pointer/length pair. Numerical values are given as they are. Numerical control flags are given in a protocol-specific representation.

At this point, [GDB] has to perform the following actions.

- If the parameters include pointer values to data needed as input to a system call, [GDB] requests this data from the target with a standard `m` packet request. This additional communication has to be expected by the target implementation and is handled as any other `m` packet.
- [GDB] translates all value from protocol representation to host representation as needed. Datatypes are coerced into the host types.
- [GDB] calls the system call.
- It then coerces datatypes back to protocol representation.
- If the system call is expected to return data in buffer space specified by pointer parameters to the call, the data is transmitted to the target using a `M` or `X` packet. This packet has to be expected by the target implementation and is handled as any other `M` or `X` packet.

Eventually [GDB] replies with another `F` packet which contains all necessary information for the target to continue. This at least contains

- Return value.
- `errno`, if has been changed by the system call.
- "Ctrl-C" flag.

After having done the needed type and value coercion, the target continues the latest continue or step action.

---

::: header
Next: [The F Request Packet](The-F-Request-Packet.html#The-F-Request-Packet)]
:::
