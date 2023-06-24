---
tip: translate by openai@2023-06-24 02:02:50
...
---
description: Remote Configuration (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Remote Configuration (Debugging with GDB)
lang: en
resource-type: document
title: Remote Configuration (Debugging with GDB)
---
::: header
Next: [Remote Stub](Remote-Stub.html#Remote-Stub)]
:::

---

### 20.4 Remote Configuration


This section documents the configuration options available when debugging remote programs. For the options related to the File I/O extensions of the remote protocol, see [system-call-allowed](system.html#system).

> 这一节文档记录了调试远程程序时可用的配置选项。有关远程协议的文件I/O扩展的选项，请参见[system-call-allowed](system.html#system)。

`set remoteaddresssize bits`

:

```
Set the maximum size of address in a memory packet to the specified number of bits. [GDB] will mask off the address bits above that number, when it passes addresses to the remote target. The default value is the number of bits in the target's address.
```

`show remoteaddresssize`

:   Show the current value of remote address size in bits.

`set serial baud n`

:

```
Set the baud rate for the remote serial I/O to `n` baud. The value is used to set the speed of the serial port used for debugging remote targets.
```

`show serial baud`

:   Show the current speed of the remote connection.

`set serial parity parity`


:   Set the parity for the remote serial I/O. Supported values of `parity` are: `even`, `none`, and `odd`. The default is `none`.

> 设置远程串行I/O的奇偶校验。支持的`parity`值有：`even`，`none`和`odd`。默认值为`none`。

`show serial parity`

:   Show the current parity of the serial port.

`set remotebreak`

:

```
If set to on, [GDB]' as the interrupt signal.
```

`show remotebreak`

:   Show whether [GDB]' to interrupt the remote program.

`set remoteflow on`
`set remoteflow off`

:

```
Enable or disable hardware flow control (`RTS`/`CTS`) on the serial port used to communicate to the remote target.
```

`show remoteflow`

:

```
Show the current setting of hardware flow control.
```

`set remotelogbase base`


:   Set the base (a.k.a. radix) of logging serial protocol communications to `base` are: `ascii`, `octal`, and `hex`. The default is `ascii`.

> 设置日志串行协议通信的基数（也称为基数）为`base`：`ascii`、`octal`和`hex`。默认值为`ascii`。

`show remotelogbase`


:   Show the current setting of the radix for logging remote serial protocol.

> 显示远程串行协议的当前日志设置。

`set remotelogfile file`

:

```
Record remote serial communications on the named `file`. The default is not to record at all.
```

`show remotelogfile`


:   Show the current setting of the file name on which to record the serial communications.

> 显示用于记录串行通信的文件名的当前设置。

`set remotetimeout num`

:

```
Set the timeout limit to wait for the remote target to respond to `num` seconds. The default is 2 seconds.
```

`show remotetimeout`


:   Show the current number of seconds to wait for the remote target responses.

> 显示等待远程目标响应的当前秒数。

```

```

`set remote hardware-watchpoint-limit limit`
`set remote hardware-breakpoint-limit limit`


:   Restrict [GDB] can be set to 0 to disable hardware watchpoints or breakpoints, and `unlimited` for unlimited watchpoints or breakpoints.

> 可以将GDB的限制设置为0以禁用硬件断点或中断点，设置为`unlimited`可以拥有无限的断点或中断点。

`show remote hardware-watchpoint-limit`
`show remote hardware-breakpoint-limit`


:   Show the current limit for the number of hardware watchpoints or breakpoints that [GDB] can use.

> 请显示GDB可以使用的硬件断点或中断点的当前限制。

```

```

`set remote hardware-watchpoint-length-limit limit`


:   Restrict [GDB] of 0 disables hardware watchpoints and `unlimited` allows watchpoints of any length.

> 限制GDB的0禁用硬件断点，而unlimited允许任意长度的断点。

`show remote hardware-watchpoint-length-limit`


:   Show the current limit (in bytes) of the maximum length of a remote hardware watchpoint.

> 显示远程硬件断点的最大长度（以字节为单位）的当前限制。

`set remote exec-file filename`
`show remote exec-file`

:

```
Select the file used for `run` with `target extended-remote`. This should be set to a filename valid on the target system. If it is not set, the target will use a default filename (e.g. the last program run).
```

`set remote interrupt-sequence`

:

```
Allow the user to select one of '`Ctrl-C`', a.k.a Magic SysRq g. It is `BREAK` signal followed by character `g`.
```

`show remote interrupt-sequence`


:   Show which of '`Ctrl-C` to interrupt the remote program. `BREAK-g` is BREAK signal followed by `g` and also known as Magic SysRq g.

> 使用`Ctrl-C`中断远程程序。`BREAK-g`是BREAK信号后跟`g`，也称为Magic SysRq g。

`set remote interrupt-on-connect`

:

```
Specify whether interrupt-sequence is sent to remote target when [GDB].
```

`show remote interrupt-on-connect`


:   Show whether interrupt-sequence is sent to remote target when [GDB] connects to it.

> 检查[GDB]连接到远程目标时是否发送中断序列。

```

```

`set tcp auto-retry on`

:

```
Enable auto-retry for remote TCP connections. This is useful if the remote debugging agent is launched in parallel with [GDB] reattempts to establish the connection using the timeout specified by `set tcp connect-timeout`.
```

`set tcp auto-retry off`

:   Do not auto-retry failed TCP connections.

`show tcp auto-retry`

:   Show the current auto-retry setting.

`set tcp connect-timeout seconds`
`set tcp connect-timeout unlimited`

:

```
Set the timeout for establishing a TCP connection to the remote target to `seconds`. The default is 15 seconds.
```

`show tcp connect-timeout`

:   Show the current connection timeout setting.


The [GDB]'. For more information about each packet, see [Remote Protocol](Remote-Protocol.html#Remote-Protocol).

> [GDB] 是一种调试器。有关每个数据包的更多信息，请参见[远程协议](Remote-Protocol.html#Remote-Protocol)。


During normal use, you should not have to use any of these commands. If you do, that may be a bug in your remote debugging stub, or a bug in [GDB] developers.

> 在正常使用中，您不应该使用这些命令中的任何一个。如果您这样做，可能是您的远程调试存根中的一个错误，或者是[GDB]开发人员的一个错误。


For each packet `name`, the command to enable or disable the packet is `set remote name-packet`. If you configure a packet, the configuration will apply for all future remote targets if no target is selected. In case there is a target selected, only the configuration of the current target is changed. All other existing remote targets' features are not affected. The command to print the current configuration of a packet is `show remote name-packet`. It displays the current remote target's configuration. If no remote target is selected, the default configuration for future connections is shown. The available settings are:

> 对于每个数据包“name”，启用或禁用数据包的命令是“set remote name-packet”。如果您配置了一个数据包，则该配置将应用于所有未来的远程目标，如果没有选择目标。如果选择了目标，则仅更改当前目标的配置。不会影响其他现有远程目标的功能。打印数据包当前配置的命令是“show remote name-packet”。它显示当前远程目标的配置。如果没有选择远程目标，则显示未来连接的默认配置。可用设置为：

---


Command Name                             Remote Packet                         Related Features

> 命令名称                             远程数据包                         相关功能
`fetch-register`                         `p`                                   `info registers`
`set-register`                           `P`                                   `set`
`binary-download`                        `X`                                   `load`, `set`
`read-aux-vector`                        `qXfer:auxv:read`                     `info auxv`
`symbol-lookup`                          `qSymbol`                             Detecting multiple threads
`attach`                                 `vAttach`                             `attach`
`verbose-resume`                         `vCont`                               Stepping or resuming multiple threads
`run`                                    `vRun`                                `run`
`software-breakpoint`                    `Z0`                                  `break`
`hardware-breakpoint`                    `Z1`                                  `hbreak`
`write-watchpoint`                       `Z2`                                  `watch`
`read-watchpoint`                        `Z3`                                  `rwatch`
`access-watchpoint`                      `Z4`                                  `awatch`
`pid-to-exec-file`                       `qXfer:exec-file:read`                `attach`, `run`
`target-features`                        `qXfer:features:read`                 `set architecture`
`library-info`                           `qXfer:libraries:read`                `info sharedlibrary`
`memory-map`                             `qXfer:memory-map:read`               `info mem`
`read-sdata-object`                      `qXfer:sdata:read`                    `print $_sdata`
`read-siginfo-object`                    `qXfer:siginfo:read`                  `print $_siginfo`
`write-siginfo-object`                   `qXfer:siginfo:write`                 `set $_siginfo`
`threads`                                `qXfer:threads:read`                  `info threads`
`get-thread-local-storage-address`       `qGetTLSAddr`                         Displaying `__thread` variables
`get-thread-information-block-address`   `qGetTIBAddr`                         Display MS-Windows Thread Information Block.
`search-memory`                          `qSearch:memory`                      `find`
`supported-packets`                      `qSupported`                          Remote communications parameters
`catch-syscalls`                         `QCatchSyscalls`                      `catch syscall`
`pass-signals`                           `QPassSignals`                        `handle signal`
`program-signals`                        `QProgramSignals`                     `handle signal`
`hostio-close-packet`                    `vFile:close`                         `remote get`, `remote put`
`hostio-open-packet`                     `vFile:open`                          `remote get`, `remote put`
`hostio-pread-packet`                    `vFile:pread`                         `remote get`, `remote put`
`hostio-pwrite-packet`                   `vFile:pwrite`                        `remote get`, `remote put`
`hostio-unlink-packet`                   `vFile:unlink`                        `remote delete`
`hostio-readlink-packet`                 `vFile:readlink`                      Host I/O
`hostio-fstat-packet`                    `vFile:fstat`                         Host I/O
`hostio-setfs-packet`                    `vFile:setfs`                         Host I/O
`noack-packet`                           `QStartNoAckMode`                     Packet acknowledgment
`osdata`                                 `qXfer:osdata:read`                   `info os`
`query-attached`                         `qAttached`                           Querying remote process attach state.
`trace-buffer-size`                      `QTBuffer:size`                       `set trace-buffer-size`
`trace-status`                           `qTStatus`                            `tstatus`
`traceframe-info`                        `qXfer:traceframe-info:read`          Traceframe info
`install-in-trace`                       `InstallInTrace`                      Install tracepoint in tracing
`disable-randomization`                  `QDisableRandomization`               `set disable-randomization`
`startup-with-shell`                     `QStartupWithShell`                   `set startup-with-shell`
`environment-hex-encoded`                `QEnvironmentHexEncoded`              `set environment`
`environment-unset`                      `QEnvironmentUnset`                   `unset environment`
`environment-reset`                      `QEnvironmentReset`                   `Reset the inferior environment (i.e., unset user-set variables)`
`set-working-dir`                        `QSetWorkingDir`                      `set cwd`
`conditional-breakpoints-packet`         `Z0 and Z1`                           `Support for target-side breakpoint condition evaluation`
`multiprocess-extensions`                `multiprocess extensions`             Debug multiple processes and remote process PID awareness
`swbreak-feature`                        `swbreak stop reason`                 `break`
`hwbreak-feature`                        `hwbreak stop reason`                 `hbreak`
`fork-event-feature`                     `fork stop reason`                    `fork`
`vfork-event-feature`                    `vfork stop reason`                   `vfork`
`exec-event-feature`                     `exec stop reason`                    `exec`
`thread-events`                          `QThreadEvents`                       Tracking thread lifetime.
`no-resumed-stop-reply`                  `no resumed thread left stop reply`   Tracking thread lifetime.

---


The number of bytes per memory-read or memory-write packet for a remote target can be configured using the commands `set remote memory-read-packet-size` and `set remote memory-write-packet-size`. If set to '`0`' to enable it. Similar to the enabling and disabling of remote packets, the command applies to the currently selected target (if available). If no remote target is selected, it applies to all future remote connections. The configuration of the selected target can be displayed using the commands `show remote memory-read-packet-size` and `show remote memory-write-packet-size`. If no remote target is selected, the default configuration for future connections is shown.

> 可以使用命令“set remote memory-read-packet-size”和“set remote memory-write-packet-size”来配置远程目标的每次内存读取或内存写入数据包的字节数。如果设置为“0”以启用它。与启用和禁用远程数据包类似，该命令适用于当前选定的目标（如果可用）。如果没有选择远程目标，则它适用于所有未来的远程连接。可以使用命令“show remote memory-read-packet-size”和“show remote memory-write-packet-size”来显示所选择目标的配置。如果没有选择远程目标，则会显示未来连接的默认配置。

---

::: header
Next: [Remote Stub](Remote-Stub.html#Remote-Stub)]
:::
