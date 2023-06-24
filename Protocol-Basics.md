---
tip: translate by openai@2023-06-24 01:34:50
...
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

> 文件I/O协议使用“F”数据包作为请求和回复数据包。由于文件I/O系统调用只有在[GDB]调用适当的主机系统调用时才会发生：

- A unique identifier for the requested system call.

- All parameters to the system call. Pointers are given as addresses in the target memory address space. Pointers to strings are given as pointer/length pair. Numerical values are given as they are. Numerical control flags are given in a protocol-specific representation.

> 所有参数都传递给系统调用。指针以目标内存地址空间中的地址形式提供。字符串指针以指针/长度对形式提供。数值以它们的原样提供。数值控制标志以协议特定的表示形式提供。

At this point, [GDB] has to perform the following actions.


- If the parameters include pointer values to data needed as input to a system call, [GDB] requests this data from the target with a standard `m` packet request. This additional communication has to be expected by the target implementation and is handled as any other `m` packet.

> 如果参数包含作为系统调用输入所需数据的指针值，[GDB]将使用标准“m”数据包请求从目标处请求此数据。目标实现必须预期这种附加通信，并将其处理为任何其他“m”数据包。
- [GDB] translates all value from protocol representation to host representation as needed. Datatypes are coerced into the host types.
- [GDB] calls the system call.
- It then coerces datatypes back to protocol representation.

- If the system call is expected to return data in buffer space specified by pointer parameters to the call, the data is transmitted to the target using a `M` or `X` packet. This packet has to be expected by the target implementation and is handled as any other `M` or `X` packet.

> 如果系统调用预期返回由指针参数指定的缓冲区中的数据，则将数据使用`M`或`X`数据包发送到目标。此数据包必须由目标实现预期并且处理为任何其他`M`或`X`数据包。


Eventually [GDB] replies with another `F` packet which contains all necessary information for the target to continue. This at least contains

> 最后，GDB回复另一个`F`数据包，其中包含目标继续执行所需的所有必要信息。 这至少包括

- Return value.
- `errno`, if has been changed by the system call.
- "Ctrl-C" flag.


After having done the needed type and value coercion, the target continues the latest continue or step action.

> 在完成所需的类型和值强制转换后，目标继续最新的继续或步骤操作。

---

::: header
Next: [The F Request Packet](The-F-Request-Packet.html#The-F-Request-Packet)]
:::
