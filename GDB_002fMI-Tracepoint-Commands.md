---
tip: translate by openai@2023-06-23 22:20:38
...
---
description: GDB/MI Tracepoint Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Tracepoint Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Tracepoint Commands (Debugging with GDB)
---
::: header
Next: [GDB/MI Symbol Query](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query)]
:::

---

### 27.17 [GDB/MI]


The commands defined in this section implement MI support for tracepoints. For detailed introduction, see [Tracepoints](Tracepoints.html#Tracepoints).

> 本节定义的命令实现了MI对断点的支持。有关详细介绍，请参见[断点](Tracepoints.html#Tracepoints)。

#### The `-trace-find` Command

#### Synopsis

::: smallexample

```bash
 -trace-find mode [parameters…]
```

:::


Find a trace frame using criteria defined by `mode`. The following table lists permissible modes and their parameters. For details of operation, see [tfind](tfind.html#tfind).

> 使用`模式`定义的标准查找跟踪帧。以下表格列出了可接受的模式及其参数。有关操作的详细信息，请参阅[tfind](tfind.html#tfind)。

'`none`'

:   No parameters are required. Stops examining trace frames.

'`frame-number`'


:   An integer is required as parameter. Selects tracepoint frame with that index.

> 需要一个整数作为参数。使用该索引选择追踪点框架。

'`tracepoint-number`'


:   An integer is required as parameter. Finds next trace frame that corresponds to tracepoint with the specified number.

> 需要一个整数作为参数。查找与指定数字对应的跟踪点的下一个跟踪框架。

'`pc`'


:   An address is required as parameter. Finds next trace frame that corresponds to any tracepoint at the specified address.

> 需要一个地址作为参数。查找与指定地址上的任何跟踪点对应的下一个跟踪帧。

'`pc-inside-range`'


:   Two addresses are required as parameters. Finds next trace frame that corresponds to a tracepoint at an address inside the specified range. Both bounds are considered to be inside the range.

> 需要两个地址作为参数。 查找下一个跟踪帧，该帧对应于指定范围内地址处的跟踪点。 两个边界都被视为在范围内。

'`pc-outside-range`'


:   Two addresses are required as parameters. Finds next trace frame that corresponds to a tracepoint at an address outside the specified range. Both bounds are considered to be inside the range.

> 需要两个地址作为参数。查找下一个跟踪框架，该框架对应于指定范围外的断点地址。两个边界都被视为在范围内。

'`line`'


:   Location specification is required as parameter. See [Location Specifications](Location-Specifications.html#Location-Specifications). Finds next trace frame that corresponds to a tracepoint at the specified location.

> 需要将位置指定为参数。请参阅[位置规范](Location-Specifications.html#Location-Specifications)。查找与指定位置的跟踪点对应的下一个跟踪帧。


If '`none`, the response does not have fields. Otherwise, the response may have the following fields:

> 如果是"无"，响应没有字段。否则，响应可能具有以下字段：

'`found`'


:   This field has either '`0`' as the value, depending on whether a matching tracepoint was found.

> 这个字段的值取决于是否找到匹配的跟踪点，可以是“0”。

'`traceframe`'


:   The index of the found traceframe. This field is present iff the '`found`'.

> 找到的跟踪框架的索引。如果找到了'found'，这个字段就会出现。

'`tracepoint`'


:   The index of the found tracepoint. This field is present iff the '`found`'.

> 找到的跟踪点的索引。如果找到了'found'，此字段就会出现。

'`frame`'


:   The information about the frame corresponding to the found trace frame. This field is present only if a trace frame was found. See [GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information), for description of this field.

> 此字段仅在找到跟踪框架时才会出现，用于描述与找到的跟踪框架相关的信息。有关此字段的描述，请参阅[GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information)。

#### [GDB]

The corresponding [GDB]'.

#### The `-trace-define-variable` Command

#### Synopsis

::: smallexample

```bash
 -trace-define-variable name [ value ]
```

:::

Create trace variable `name`' character.

#### [GDB]

The corresponding [GDB]'.

#### The `-trace-frame-collected` Command

#### Synopsis

::: smallexample

```bash
 -trace-frame-collected
    [--var-print-values var_pval]
    [--comp-print-values comp_pval]
    [--registers-format regformat]
    [--memory-contents]
```

:::


This command returns the set of collected objects, register names, trace state variable names, memory ranges and computed expressions that have been collected at a particular trace frame. The optional parameters to the command affect the output format in different ways. See the output description table below for more details.

> 这个命令返回在特定跟踪帧上收集的对象集合、寄存器名称、跟踪状态变量名称、内存范围和计算表达式。命令的可选参数以不同方式影响输出格式。有关更多详细信息，请参见下面的输出描述表。


The reported names can be used in the normal manner to create varobjs and inspect the objects themselves. The items returned by this command are categorized so that it is clear which is a variable, which is a register, which is a trace state variable, which is a memory range and which is a computed expression.

> 报告的名称可以正常使用来创建varobjs并检查对象本身。此命令返回的项目被分类，以便清楚哪个是变量、哪个是寄存器、哪个是跟踪状态变量、哪个是内存范围和哪个是计算表达式。

For instance, if the actions were

::: smallexample

```bash
collect myVar, myArray[myIndex], myObj.field, myPtr->field, myCount + 2
collect *(int*)0xaf02bef0@40
```

:::


the object collected in its entirety would be `myVar`. The object `myArray` would be partially collected, because only the element at index `myIndex` would be collected. The remaining objects would be computed expressions.

> 整个收集的对象将是`myVar`。只有索引`myIndex`处的元素会被收集，因此`myArray`对象只会被部分收集。剩下的对象将是计算表达式。

An example output would be:

::: smallexample

```bash
(gdb)
-trace-frame-collected
^done,
  explicit-variables=,
  computed-expressions=[,
                        ,
                        ,
                        ,
                        ],
  registers=[,
             ,
             ,
             ...
             ],
  tvars=,
  memory=[,
          ]
(gdb)
```

:::

Where:

`explicit-variables`


:   The set of objects that have been collected in their entirety (as opposed to collecting just a few elements of an array or a few struct members). For each object, its name and value are printed. The `--var-print-values` option affects how or whether the value field is output. If `var_pval` is 0, then print only the names; if it is 1, print also their values; and if it is 2, print the name, type and value for simple data types, and the name and type for arrays, structures and unions.

> 这个集合包含了完整收集的对象（而不是仅仅收集数组的一些元素或结构的一些成员）。对于每个对象，都会输出它的名称和值。`--var-print-values`选项会影响输出值的方式或是否输出。如果`var_pval`为0，则只输出名称；如果为1，则还会输出它们的值；如果为2，则会输出简单数据类型的名称、类型和值，以及数组、结构和联合的名称和类型。

`computed-expressions`


:   The set of computed expressions that have been collected at the current trace frame. The `--comp-print-values` option affects this set like the `--var-print-values` option affects the `explicit-variables` set. See above.

> 当前跟踪帧收集的已计算表达式集合。 `--comp-print-values` 选项像 `--var-print-values` 选项一样影响 `explicit-variables` 集合。 请参见上文。

`registers`


:   The registers that have been collected at the current trace frame. For each register collected, the name and current value are returned. The value is formatted according to the `--registers-format` option. See the `-data-list-register-values` command for a list of the allowed formats. The default is '`x`'.

> 当前跟踪帧收集的寄存器。对于每个收集的寄存器，返回名称和当前值。该值按照`--registers-format`选项格式化。有效格式请参见`-data-list-register-values`命令。默认格式为'`x`'。

`tvars`


:   The trace state variables that have been collected at the current trace frame. For each trace state variable collected, the name and current value are returned.

> 当前跟踪帧收集的跟踪状态变量。对于收集的每个跟踪状态变量，返回其名称和当前值。

`memory`


:   The set of memory ranges that have been collected at the current trace frame. Its content is a list of tuples. Each tuple represents a collected memory range and has the following fields:

> 当前跟踪帧收集的内存范围集合。它的内容是一个元组列表。每个元组代表一个收集的内存范围，并具有以下字段：

```
`address`

:   The start address of the memory range, as hexadecimal literal.

`length`

:   The length of the memory range, as decimal literal.

`contents`

:   The contents of the memory block, in hex. This field is only present if the `--memory-contents` option is specified.
```

#### [GDB]

There is no corresponding [GDB] command.

#### Example

#### The `-trace-list-variables` Command

#### Synopsis

::: smallexample

```bash
 -trace-list-variables
```

:::


Return a table of all defined trace variables. Each element of the table has the following fields:

> 返回所有已定义的跟踪变量的表格。表中的每个元素具有以下字段：

'`name`'

:   The name of the trace variable. This field is always present.

'`initial`'


:   The initial value. This is a 64-bit signed integer. This field is always present.

> 初始值。这是一个64位带符号整数。这个字段总是存在的。

'`current`'


:   The value the trace variable has at the moment. This is a 64-bit signed integer. This field is absent iff current value is not defined, for example if the trace was never run, or is presently running.

> 当前跟踪变量的值。这是一个64位带符号整数。如果当前值未定义，例如跟踪从未运行过或目前正在运行，则此字段不存在。

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-trace-list-variables
^done,trace-variables={nr_rows="1",nr_cols="3",
hdr=[,
     ,
     ],
body=[variable=
      variable=
(gdb)
```

:::

#### The `-trace-save` Command

#### Synopsis

::: smallexample

```bash
 -trace-save [ -r ] [ -ctf ] filename
```

:::


Saves the collected trace data to `filename`' option the target is asked to perform the save.

> 将收集的跟踪数据保存到`文件名`，目标被要求执行保存。


By default, this command will save the trace in the tfile format. You can supply the optional '`-ctf`' argument to save it the CTF format. See [Trace Files](Trace-Files.html#Trace-Files) for more information about CTF.

> 默认情况下，此命令将跟踪信息以tfile格式保存。您可以提供可选的'-ctf'参数以CTF格式保存它。有关CTF的更多信息，请参见[跟踪文件](Trace-Files.html#Trace-Files)。

#### [GDB]

The corresponding [GDB]'.

#### The `-trace-start` Command

#### Synopsis

::: smallexample

```bash
 -trace-start
```

:::


Starts a tracing experiment. The result of this command does not have any fields.

> 开始跟踪实验。此命令的结果没有任何字段。

#### [GDB]

The corresponding [GDB]'.

#### The `-trace-status` Command

#### Synopsis

::: smallexample

```bash
 -trace-status
```

:::


Obtains the status of a tracing experiment. The result may include the following fields:

> 获取跟踪实验的状态。结果可能包括以下字段：

'`supported`'


:   May have a value of either '`0`' when examining trace file. In the latter case, examining of trace frame is possible but new tracing experiement cannot be started. This field is always present.

> 可以有一个值为“0”的值，当检查跟踪文件时。在后一种情况下，可以检查跟踪框架，但不能开始新的跟踪实验。该字段始终存在。

'`running`'

:   May have a value of either '`0`'.

'`stop-reason`'


:   Report the reason why the tracing was stopped last time. This field may be absent iff tracing was never stopped on target yet. The value of '`request`'.

> 报告上次停止跟踪的原因。如果目标尚未停止跟踪，此字段可能不存在。'请求'的值。

'`stopping-tracepoint`'


:   The number of tracepoint whose passcount as exceeded. This field is present iff the '`stop-reason`'.

> 超过passcount的跟踪点的数量。只有当'stop-reason'存在时，才会出现此字段。

'`frames`'
'`frames-created`'


:   The '`frames`' is the total created during the run, including ones that were discarded, such as when a circular trace buffer filled up. Both fields are optional.

> '帧'是在运行过程中创建的总数，包括被丢弃的，比如当循环跟踪缓冲区满了的时候。这两个字段都是可选的。

'`buffer-size`'
'`buffer-free`'


:   These fields tell the current size of the tracing buffer and the remaining space. These fields are optional.

> 这些字段告诉当前跟踪缓冲区的大小以及剩余空间。这些字段是可选的。

'`circular`'


:   The value of the circular trace buffer flag. `1` means that the trace buffer is circular and old trace frames will be discarded if necessary to make room, `0` means that the trace buffer is linear and may fill up.

> 标志循环跟踪缓冲区的值。`1`表示跟踪缓冲区是循环的，如果需要，可以丢弃旧的跟踪帧；`0`表示跟踪缓冲区是线性的，可能会填满。

'`disconnected`'


:   The value of the disconnected tracing flag. `1` means that tracing will continue after [GDB] disconnects, `0` means that the trace run will stop.

> 断开跟踪标志的值。`1`表示在[GDB]断开连接后跟踪将继续，`0`表示跟踪运行将停止。

'`trace-file`'


:   The filename of the trace file being examined. This field is optional, and only present when examining a trace file.

> 文件跟踪文件的文件名。此字段是可选的，仅在检查跟踪文件时出现。

#### [GDB]

The corresponding [GDB]'.

#### The `-trace-stop` Command

#### Synopsis

::: smallexample

```bash
 -trace-stop
```

:::


Stops a tracing experiment. The result of this command has the same fields as `-trace-status`, except that the '`supported`' fields are not output.

> 停止跟踪实验。此命令的结果与`-trace-status`相同，但不会输出“支持”字段。

#### [GDB]

The corresponding [GDB]'.

---

::: header
Next: [GDB/MI Symbol Query](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query)]
:::
