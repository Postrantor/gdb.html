---
tip: translate by openai@2023-06-24 03:18:16
...
---
description: Static Probe Points (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Static Probe Points (Debugging with GDB)
lang: en
resource-type: document
title: Static Probe Points (Debugging with GDB)
---
::: header
Next: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::

---

#### 5.1.10 Static Probe Points


[GDB] supports *SDT* probes in the code. SDT stands for Statically Defined Tracing, and the probes are designed to have a tiny runtime code and data footprint, and no dynamic relocations.

> [GDB] 支持在代码中使用*SDT*探针。SDT代表静态定义跟踪，这些探针旨在具有微小的运行时代码和数据足迹，没有动态重定位。


Currently, the following types of probes are supported on ELF-compatible systems:

> 目前，在ELF兼容系统上支持以下类型的探头：


- `SystemTap` ([http://sourceware.org/systemtap/](http://sourceware.org/systemtap/)) SDT probes[^5^](#FOOT5).

> SystemTap（[http://sourceware.org/systemtap/](http://sourceware.org/systemtap/)）SDT 探针[^5^](#FOOT5)。

- `DTrace` ([http://oss.oracle.com/projects/DTrace](http://oss.oracle.com/projects/DTrace)) USDT probes. `DTrace` probes are usable from C and C++ languages.

> DTrace（http://oss.oracle.com/projects/DTrace）USDT探针。DTrace探针可以从C和C++语言中使用。


Some `SystemTap` probes have an associated semaphore variable; for instance, this happens automatically if you defined your probe using a DTrace-style `.d` will not automatically set the semaphore. `DTrace` probes do not support semaphores.

> 一些SystemTap探针有关联的信号量变量；例如，如果你使用DTrace样式的.d定义你的探针，它就会自动设置信号量。而DTrace探针不支持信号量。


You can examine the available static static probes using `info probes`, with optional arguments:

> 你可以使用`info probes`查看可用的静态探针，可选参数：

`info probes [type] [provider [name [objfile]]]`


If given, `type` is either `stap` for listing `SystemTap` probes or `dtrace` for listing `DTrace` probes. If omitted all probes are listed regardless of their types.

> 如果提供，`type`可以是`stap`列出`SystemTap`探针，或者是`dtrace`列出`DTrace`探针。如果省略，所有探针都会被列出，不论它们的类型。


If given, `provider` is a regular expression used to match against provider names when selecting which probes to list. If omitted, probes by all probes from all providers are listed.

> 如果提供，`provider`是一个用于匹配提供者名称的正则表达式，以便选择要列出的探测器。如果省略，则会列出所有提供者的所有探测器。


If given, `name` is a regular expression to match against probe names when selecting which probes to list. If omitted, probe names are not considered when deciding whether to display them.

> 如果给出，`name`是一个正则表达式，用于在选择要列出的探针时进行匹配。如果省略，则在决定是否显示探针时不会考虑探针名称。


If given, `objfile` is a regular expression used to select which object files (executable or shared libraries) to examine. If not given, all object files are considered.

> 如果给出，`objfile`是一个正则表达式，用于选择要检查的哪些对象文件（可执行文件或共享库）。如果没有给出，则认为所有对象文件都考虑。

`info probes all`

List the available static probes, from all types.


Some probe points can be enabled and/or disabled. The effect of enabling or disabling a probe depends on the type of probe being handled. Some `DTrace` probes can be enabled or disabled, but `SystemTap` probes cannot be disabled.

> 有些探针可以启用或禁用。启用或禁用探针的效果取决于处理的探针类型。一些DTrace探针可以启用或禁用，但SystemTap探针不能禁用。


You can enable (or disable) one or more probes using the following commands, with optional arguments:

> 您可以使用以下命令（可选参数）启用（或禁用）一个或多个探针：

`enable probes [provider [name [objfile]]]`


If given, `provider` is a regular expression used to match against provider names when selecting which probes to enable. If omitted, all probes from all providers are enabled.

> 如果提供，`provider`是一个用于选择要启用哪些探测器时匹配提供商名称的正则表达式。如果省略，则会启用所有提供商的所有探测器。


If given, `name` is a regular expression to match against probe names when selecting which probes to enable. If omitted, probe names are not considered when deciding whether to enable them.

> 如果提供了`name`，它是一个用于在选择要启用的探针时与之匹配的正则表达式。如果省略，则在决定是否启用探针时不考虑探针名称。


If given, `objfile` is a regular expression used to select which object files (executable or shared libraries) to examine. If not given, all object files are considered.

> 如果给出，`objfile`是一个用于选择要检查哪些对象文件（可执行文件或共享库）的正则表达式。如果没有给出，则认为所有对象文件都是可以考虑的。

`disable probes [provider [name [objfile]]]`


See the `enable probes` command above for a description of the optional arguments accepted by this command.

> 见上面的`启用探针`命令，了解此命令接受的可选参数的描述。


A probe may specify up to twelve arguments. These are available at the point at which the probe is defined---that is, when the current PC is at the probe's location. The arguments are available using the convenience variables (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) `$_probe_arg0`...`$_probe_arg11`. In `SystemTap` probes each probe argument is an integer of the appropriate size; types are not preserved. In `DTrace` probes types are preserved provided that they are recognized as such by [GDB]; otherwise the value of the probe argument will be a long integer. The convenience variable `$_probe_argc` holds the number of arguments at the current probe point.

> 一个探针可以指定多达十二个参数。这些参数可以在定义探针的点上使用，也就是当前PC处于探针位置时。参数可以使用便利变量（参见[便利变量]（Convenience-Vars.html＃Convenience-Vars）） `$_probe_arg0`... `$_probe_arg11`获得。在SystemTap探针中，每个探针参数都是适当大小的整数；类型不会被保留。在DTrace探针中，如果被GDB识别为类型，则类型会被保留；否则探针参数的值将是一个长整数。便利变量`$_probe_argc`保存当前探针点的参数数量。


These variables are always available, but attempts to access them at any location other than a probe point will cause [GDB] to give an error message.

> 这些变量总是可用的，但如果在探测点以外的任何位置尝试访问它们，[GDB]将会给出错误消息。

::: footnote

---

#### Footnotes

### [(5)](#DOCF5)


See [http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps](http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps) for more information on how to add `SystemTap` SDT probes in your applications.

> 查看[http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps](http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps)了解如何在您的应用程序中添加`SystemTap` SDT探针的更多信息。

### [(6)](#DOCF6)


See [http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation](http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation) for a good reference on how the SDT probes are implemented.

> 请参考[http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation](http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation)了解SDT探针的实现方法。
:::

---

::: header
Next: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::
