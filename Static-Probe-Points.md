---
tip: translate by openai@2023-06-23 13:35:31
...
---
description: Static Probe Points (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Static Probe Points (Debugging with GDB)
lang: en
resource-type: document
title: Static Probe Points (Debugging with GDB)
-----------------------------------------------

::: header
Next: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::

---

#### 5.1.10 Static Probe Points

[GDB] supports *SDT* probes in the code. SDT stands for Statically Defined Tracing, and the probes are designed to have a tiny runtime code and data footprint, and no dynamic relocations.

> [GDB]支持代码中的 *SDT* 探针。SDT 代表静态定义跟踪，这些探针的设计具有微小的运行时代码和数据足迹，没有动态重定位。

Currently, the following types of probes are supported on ELF-compatible systems:

> 目前，在 ELF 兼容系统上支持以下类型的探针：

- `SystemTap` ([http://sourceware.org/systemtap/](http://sourceware.org/systemtap/)) SDT probes[^5^](#FOOT5).

> 系统钉（[http://sourceware.org/systemtap/](http://sourceware.org/systemtap/)）SDT 探针[^5^]（#FOOT5）。

- `DTrace` ([http://oss.oracle.com/projects/DTrace](http://oss.oracle.com/projects/DTrace)) USDT probes. `DTrace` probes are usable from C and C++ languages.

> DTrace（[http://oss.oracle.com/projects/DTrace](http://oss.oracle.com/projects/DTrace)）USDT 探针。DTrace 探针可以从 C 和 C++ 语言中使用。

Some `SystemTap` probes have an associated semaphore variable; for instance, this happens automatically if you defined your probe using a DTrace-style `.d` will not automatically set the semaphore. `DTrace` probes do not support semaphores.

> 一些 SystemTap 探针有一个相关的信号量变量; 例如，如果您使用 DTrace 样式的.d 定义探针，将自动设置信号量。 DTrace 探针不支持信号量。

You can examine the available static static probes using `info probes`, with optional arguments:

> 你可以使用 `info probes`，带上可选参数，检查可用的静态探针：

`info probes [type] [provider [name [objfile]]]`

If given, `type` is either `stap` for listing `SystemTap` probes or `dtrace` for listing `DTrace` probes. If omitted all probes are listed regardless of their types.

> 如果提供，`type` 可以是 `stap`，用于列出 `SystemTap` 探针，或 `dtrace`，用于列出 `DTrace` 探针。 如果省略，则无论其类型如何，都会列出所有探针。

If given, `provider` is a regular expression used to match against provider names when selecting which probes to list. If omitted, probes by all probes from all providers are listed.

> 如果提供，`provider` 是一个用于与提供商名称匹配以选择要列出的探针的正则表达式。如果省略，则会列出所有提供商的所有探针。

If given, `name` is a regular expression to match against probe names when selecting which probes to list. If omitted, probe names are not considered when deciding whether to display them.

> 如果提供了'name'，它是一个用于在选择哪些探针时与之匹配的正则表达式。如果省略，则在决定是否显示探针时不考虑探针名称。

If given, `objfile` is a regular expression used to select which object files (executable or shared libraries) to examine. If not given, all object files are considered.

> 如果提供了 `objfile`，它是一个正则表达式，用于选择要检查的可执行文件或共享库。如果没有提供，则会考虑所有对象文件。

`info probes all`

List the available static probes, from all types.

> 列出所有类型的可用静态探测器。

Some probe points can be enabled and/or disabled. The effect of enabling or disabling a probe depends on the type of probe being handled. Some `DTrace` probes can be enabled or disabled, but `SystemTap` probes cannot be disabled.

> 一些探针点可以启用或禁用。启用或禁用探针的效果取决于处理的探针类型。一些 DTrace 探针可以启用或禁用，但 SystemTap 探针不能禁用。

You can enable (or disable) one or more probes using the following commands, with optional arguments:

> 你可以使用以下命令（可选参数）启用（或禁用）一个或多个探针：

`enable probes [provider [name [objfile]]]`

If given, `provider` is a regular expression used to match against provider names when selecting which probes to enable. If omitted, all probes from all providers are enabled.

> 如果给出，`provider` 是一个正则表达式，用于匹配选择要启用的探针的提供商名称。如果省略，则启用所有提供商的所有探针。

If given, `name` is a regular expression to match against probe names when selecting which probes to enable. If omitted, probe names are not considered when deciding whether to enable them.

> 如果提供了 `name`，那么它是一个用于在选择要启用的探针时与之匹配的正则表达式。如果省略，则在决定是否启用探针时不考虑探针名称。

If given, `objfile` is a regular expression used to select which object files (executable or shared libraries) to examine. If not given, all object files are considered.

> 如果提供了 `objfile`，则它是一个正则表达式，用于选择要检查的可执行文件或共享库。如果没有提供，则考虑所有对象文件。

`disable probes [provider [name [objfile]]]`

See the `enable probes` command above for a description of the optional arguments accepted by this command.

> 查看上面的 `启用探针` 命令，了解此命令接受的可选参数的描述。

A probe may specify up to twelve arguments. These are available at the point at which the probe is defined---that is, when the current PC is at the probe's location. The arguments are available using the convenience variables (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) `$_probe_arg0`...`$_probe_arg11`. In `SystemTap` probes each probe argument is an integer of the appropriate size; types are not preserved. In `DTrace` probes types are preserved provided that they are recognized as such by [GDB]; otherwise the value of the probe argument will be a long integer. The convenience variable `$_probe_argc` holds the number of arguments at the current probe point.

> 一个探针可以指定多达十二个参数。这些参数可以在定义探针的点（也就是当前 PC 在探针位置时）得到。可以使用便利变量（参见[便利变量]）$_probe_arg0...$_probe_arg11 来获取这些参数。在 SystemTap 探针中，每个探针参数是适当大小的整数；类型不会被保留。在 DTrace 探针中，只要被 GDB 识别为正确的类型，类型就会被保留；否则探针参数的值将是一个长整数。便利变量 $_probe_argc 保存当前探针点的参数数量。

These variables are always available, but attempts to access them at any location other than a probe point will cause [GDB] to give an error message.

> 这些变量总是可用的，但尝试在探针点以外的任何位置访问它们会导致[GDB]出现错误消息。

::: footnote

---

#### Footnotes

### [(5)](#DOCF5)

See [http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps](http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps) for more information on how to add `SystemTap` SDT probes in your applications.

> 请参阅 [http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps](http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps)，了解如何在您的应用程序中添加 `SystemTap` SDT 探针的更多信息。

### [(6)](#DOCF6)

See [http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation](http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation) for a good reference on how the SDT probes are implemented.

> 参考 SDT 探针实现方式，请参阅 [http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation](http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation)。
> :::

---

::: header
Next: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::
