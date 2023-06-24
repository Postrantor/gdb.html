---
tip: translate by openai@2023-06-23 20:18:19
...
---
description: Debugger Adapter Protocol (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Debugger Adapter Protocol (Debugging with GDB)
lang: en
resource-type: document
title: Debugger Adapter Protocol (Debugging with GDB)
---
::: header
Next: [JIT Interface](JIT-Interface.html#JIT-Interface)]
:::

---

## 29 Debugger Adapter Protocol


Generally, [GDB] implements the Debugger Adapter Protocol as written. However, in some cases, extensions are either needed or even expected.

> 一般来说，[GDB]实现了调试器适配器协议。但是，在某些情况下，需要或者甚至期望使用扩展功能。

[GDB] defines some parameters that can be passed to the `launch` request:

`args`


:   If provided, this should be an array of strings. These strings are provided as command-line arguments to the inferior, as if by `set args`. See [Arguments](Arguments.html#Arguments).

> 如果提供，这应该是一个字符串数组。这些字符串作为命令行参数提供给下级，就好像通过“set args”一样。请参阅[参数](Arguments.html#Arguments)。

`env`


:   If provided, this should be an object. Each key of the object will be used as the name of an environment variable; each value must be a string and will be the value of that variable. The environment of the inferior will be set to exactly as passed in. See [Environment](Environment.html#Environment).

> 如果提供，这应该是一个对象。该对象的每个键将用作环境变量的名称; 每个值必须是一个字符串，并且将是该变量的值。次级环境将被设置为完全按照传入的方式。请参阅[环境](Environment.html#Environment)。

`program`


:   If provided, this is a string that specifies the program to use. This corresponds to the `file` command. See [Files](Files.html#Files).

> 如果提供，这是一个指定要使用的程序的字符串。这对应于“file”命令。请参见[文件](Files.html#Files)。

`stopAtBeginningOfMainSubprogram`


:   If provided, this must be a boolean. When '`True` will set a temporary breakpoint at the program's main procedure, using the same approach as the `start` command. See [Starting](Starting.html#Starting).

> 如果提供，这必须是一个布尔值。当设置为“True”时，将使用与“start”命令相同的方法在程序的主程序处设置一个临时断点。参见[启动](Starting.html#Starting)。


[GDB] defines some parameters that can be passed to the `attach` request. One of these must be specified.

> GDB定义了一些可以传递给`attach`请求的参数，必须指定其中一个。

`pid`


:   The process ID to which [GDB] should attach. See [Attach](Attach.html#Attach).

> 该进程ID应除GDB附加。参见[附加](Attach.html#Attach)。

`target`


:   The target to which [GDB] should connect. This is a string and is passed to the `target remote` command. See [Connecting](Connecting.html#Connecting).

> 目标，[GDB]应该连接的目标。这是一个字符串，传递给`target remote`命令。请参阅[连接](Connecting.html#Connecting)。
