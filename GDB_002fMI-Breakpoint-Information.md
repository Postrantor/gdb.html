---
tip: translate by openai@2023-06-23 21:48:55
...
---
description: GDB/MI Breakpoint Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Breakpoint Information (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Breakpoint Information (Debugging with GDB)
---
::: header
Next: [GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information)]
:::

---

#### 27.5.4 [GDB/MI]


When [GDB] reports information about a breakpoint, a tracepoint, a watchpoint, or a catchpoint, it uses a tuple with the following fields:

> 当GDB报告关于断点、跟踪点、监视点或捕获点的信息时，它使用具有以下字段的元组：

`number`

:   The breakpoint number.

`type`


:   The type of the breakpoint. For ordinary breakpoints this will be '`breakpoint`', but many values are possible.

> 断点的类型。对于普通断点，这将是'断点'，但是可能有很多不同的值。

`catch-type`


:   If the type of the breakpoint is '`catchpoint`', then this indicates the exact type of catchpoint.

> 如果断点的类型是“catchpoint”，那么这就表明了确切的捕获点类型。

`disp`


:   This is the breakpoint disposition---either '`del`', meaning that the breakpoint will not be deleted.

> 这是断点布置---要么是'del'，意思是断点不会被删除。

`enabled`


:   This indicates whether the breakpoint is enabled, in which case the value is '`y`'. Note that this is not the same as the field `enable`.

> 这表明断点是否启用，如果启用，值为“y”。请注意，这与字段“enable”不同。

`addr`


:   The address of the breakpoint. This may be a hexidecimal number, giving the address; or the string '`<PENDING>`', for a breakpoint with multiple locations. This field will not be present if no address can be determined. For example, a watchpoint does not have an address.

> 断点的地址。这可能是十六进制数字，给出地址；或者字符串'<PENDING>'，用于具有多个位置的断点。如果无法确定地址，此字段将不会出现。例如，监视点没有地址。

`addr_flags`


:   Optional field containing any flags related to the address. These flags are architecture-dependent; see [Architectures](Architectures.html#Architectures) for their meaning for a particular CPU.

> 可选字段，包含与地址相关的任何标志。这些标志取决于架构；有关特定CPU的含义，请参见[架构](Architectures.html#Architectures)。

`func`


:   If known, the function in which the breakpoint appears. If not known, this field is not present.

> 如果知道，断点出现的函数。如果不知道，此字段不存在。

`filename`


:   The name of the source file which contains this function, if known. If not known, this field is not present.

> 如果已知，此函数所在的源文件的名称。如果不知道，此字段不存在。

`fullname`


:   The full file name of the source file which contains this function, if known. If not known, this field is not present.

> 如果已知，此功能所在的源文件的完整文件名；如果不知道，则此字段不存在。

`line`


:   The line number at which this breakpoint appears, if known. If not known, this field is not present.

> 这个断点出现的行号，如果已知的话。如果不知道，这个字段不存在。

`at`


:   If the source file is not known, this field may be provided. If provided, this holds the address of the breakpoint, possibly followed by a symbol name.

> 如果源文件未知，可以提供此字段。如果提供，这将包含断点的地址，可能会跟随一个符号名称。

`pending`


:   If this breakpoint is pending, this field is present and holds the text used to set the breakpoint, as entered by the user.

> 如果这个断点是挂起的，那么这个字段就会出现，并保存用户输入来设置断点的文本。

`evaluated-by`

:   Where this breakpoint's condition is evaluated, either '`host`'.

`thread`


:   If this is a thread-specific breakpoint, then this identifies the thread in which the breakpoint can trigger.

> 如果这是一个特定于线程的断点，那么它就可以确定在哪个线程中触发断点。

`task`


:   If this breakpoint is restricted to a particular Ada task, then this field will hold the task identifier.

> 如果这个断点限制在特定的Ada任务上，那么这个字段将保存任务标识符。

`cond`

:   If the breakpoint is conditional, this is the condition expression.

`ignore`

:   The ignore count of the breakpoint.

`enable`

:   The enable count of the breakpoint.

`traceframe-usage`

:   FIXME.

`static-tracepoint-marker-string-id`

:   For a static tracepoint, the name of the static tracepoint marker.

`mask`

:   For a masked watchpoint, this is the mask.

`pass`

:   A tracepoint's pass count.

`original-location`


:   The location of the breakpoint as originally specified by the user. This field is optional.

> 用户最初指定的断点位置。此字段为可选项。

`times`

:   The number of times the breakpoint has been hit.

`installed`


:   This field is only given for tracepoints. This is either '`y`', meaning that it is not.

> 这个字段只给予跟踪点。这要么是'`y`'，意思是它不是。

`what`

:   Some extra data, the exact contents of which are type-dependent.

`locations`


:   This field is present if the breakpoint has multiple locations. It is also exceptionally present if the breakpoint is enabled and has a single, disabled location.

> 此字段存在，如果断点有多个位置。如果断点已启用且只有一个禁用的位置，它也会特别存在。

```
The value is a list of locations. The format of a location is described below.
```


A location in a multi-location breakpoint is represented as a tuple with the following fields:

> 一个多位置断点中的位置用元组表示，其中包括以下字段：

`number`


:   The location number as a dotted pair, like '`1.2`'. The first digit is the number of the parent breakpoint. The second digit is the number of the location within that breakpoint.

> 位置号以点号分隔的对，像'1.2'。第一位数字是父断点的编号。第二位数字是该断点内的位置编号。

`enabled`

:   There are three possible values, with the following meanings:

```
`y`

:   The location is enabled.

`n`

:   The location is disabled by the user.

`N`

:   The location is disabled because the breakpoint condition is invalid at this location.
```

`addr`

:   The address of this location as an hexidecimal number.

`addr_flags`


:   Optional field containing any flags related to the address. These flags are architecture-dependent; see [Architectures](Architectures.html#Architectures) for their meaning for a particular CPU.

> 可选字段，包含与地址相关的任何标志。这些标志取决于架构；有关特定CPU的含义，请参阅[架构](Architectures.html#Architectures)。

`func`


:   If known, the function in which the location appears. If not known, this field is not present.

> 如果已知，则包含位置的函数。如果不知道，此字段不存在。

`file`


:   The name of the source file which contains this location, if known. If not known, this field is not present.

> 如果已知，这个位置所在的源文件的名称。如果不知道，则此字段不存在。

`fullname`


:   The full file name of the source file which contains this location, if known. If not known, this field is not present.

> 如果已知，此位置所在的源文件的完整文件名。如果不知道，则此字段不存在。

`line`


:   The line number at which this location appears, if known. If not known, this field is not present.

> 此位置所在的行号，如果已知，则会显示。如果未知，则不会出现此字段。

`thread-groups`

:   The thread groups this location is in.


For example, here is what the output of `-break-insert` (see [GDB/MI Breakpoint Commands](GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands)) might be:

> 例如，这就是`-break-insert`的输出（参见[GDB/MI断点命令]（GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands））：

::: smallexample

```bash
-> -break-insert main
<- ^done,bkpt={number="1",type="breakpoint",disp="keep",
    enabled="y",addr="0x08048564",func="main",file="myprog.c",
    fullname="/home/nickrob/myprog.c",line="68",thread-groups=["i1"],
    times="0"}
<- (gdb)
```

:::

---

::: header
Next: [GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information)]
:::
