---
tip: translate by openai@2023-06-23 22:09:55
...
---
description: GDB/MI Stack Manipulation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Stack Manipulation (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Stack Manipulation (Debugging with GDB)
---
::: header
Next: [GDB/MI Variable Objects](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects)]
:::

---

### 27.14 [GDB/MI]

#### The `-enable-frame-filters` Command

::: smallexample

```bash
-enable-frame-filters
```

:::


[GDB] allows Python-based frame filters to affect the output of the MI commands relating to stack traces. As there is no way to implement this in a fully backward-compatible way, a front end must request that this functionality be enabled.

> [GDB]允许基于Python的帧过滤器影响MI命令与堆栈跟踪的输出。由于没有完全向后兼容的方式来实现这一功能，前端必须请求启用此功能。

Once enabled, this feature cannot be disabled.


Note that if Python support has not been compiled into [GDB], this command will still succeed (and do nothing).

> 如果Python支持没有被编译进[GDB]，这个命令仍然会成功（但不会做任何事情）。

#### The `-stack-info-frame` Command

#### Synopsis

::: smallexample

```bash
 -stack-info-frame
```

:::

Get info on the selected frame.

#### [GDB]

The corresponding [GDB]' (without arguments).

#### Example

::: smallexample

```bash
(gdb)
-stack-info-frame
^done,frame={level="1",addr="0x0001076c",func="callee3",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="17",
arch="i386:x86_64"}
(gdb)
```

:::

#### The `-stack-info-depth` Command

#### Synopsis

::: smallexample

```bash
 -stack-info-depth [ max-depth ]
```

:::


Return the depth of the stack. If the integer argument `max-depth` frames.

> 返回堆栈的深度。如果整数参数'max-depth'帧。

#### [GDB]

There's no equivalent [GDB] command.

#### Example

For a stack with frame levels 0 through 11:

::: smallexample

```bash
(gdb)
-stack-info-depth
^done,depth="12"
(gdb)
-stack-info-depth 4
^done,depth="4"
(gdb)
-stack-info-depth 12
^done,depth="12"
(gdb)
-stack-info-depth 11
^done,depth="11"
(gdb)
-stack-info-depth 13
^done,depth="12"
(gdb)
```

:::

#### The `-stack-list-arguments` Command

#### Synopsis

::: smallexample

```bash
 -stack-list-arguments [ --no-frame-filters ] [ --skip-unavailable ] print-values
    [ low-frame high-frame ]
```

:::


Display a list of the arguments for the frames between `low-frame` may be larger than the actual number of frames, in which case only existing frames will be returned.

> 显示从“low-frame”到实际帧数可能超过实际帧数的参数列表，在这种情况下，只返回现有的帧。


If `print-values` is 0 or `--no-values`, print only the names of the variables; if it is 1 or `--all-values`, print also their values; and if it is 2 or `--simple-values`, print the name, type and value for simple data types, and the name and type for arrays, structures and unions. If the option `--no-frame-filters` is supplied, then Python frame filters will not be executed.

> 如果`print-values`为0或`--no-values`，只打印变量的名称；如果为1或`--all-values`，则还打印它们的值；如果为2或`--simple-values`，则打印简单数据类型的名称、类型和值，以及数组、结构和联合的名称和类型。如果提供了选项`--no-frame-filters`，则不会执行Python帧过滤器。


If the `--skip-unavailable` option is specified, arguments that are not available are not listed. Partially available arguments are still displayed, however.

> 如果指定了`--skip-unavailable`选项，则不会列出不可用的参数。但仍会显示部分可用的参数。


Use of this command to obtain arguments in a single frame is deprecated in favor of the '`-stack-list-variables`' command.

> 使用此命令以获取单个帧中的参数已被弃用，改用 '`-stack-list-variables`' 命令。

#### [GDB]

[GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-stack-list-frames
^done,
stack=[
frame={level="0",addr="0x00010734",func="callee4",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="8",
arch="i386:x86_64"},
frame={level="1",addr="0x0001076c",func="callee3",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="17",
arch="i386:x86_64"},
frame={level="2",addr="0x0001078c",func="callee2",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="22",
arch="i386:x86_64"},
frame={level="3",addr="0x000107b4",func="callee1",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="27",
arch="i386:x86_64"},
frame={level="4",addr="0x000107e0",func="main",
file="../../../devo/gdb/testsuite/gdb.mi/basics.c",
fullname="/home/foo/bar/devo/gdb/testsuite/gdb.mi/basics.c",line="32",
arch="i386:x86_64"}]
(gdb)
-stack-list-arguments 0
^done,
stack-args=[
frame=,
frame=,
frame=,
frame=,
frame=]
(gdb)
-stack-list-arguments 1
^done,
stack-args=[
frame=,
frame={level="1",
 args=[,
frame={level="2",args=[
,
,
{frame={level="3",args=[
,
,
,
frame=]
(gdb)
-stack-list-arguments 0 2 2
^done,stack-args=[frame=]
(gdb)
-stack-list-arguments 1 2 2
^done,stack-args=[frame={level="2",
args=[,
]
(gdb)
```

:::

#### The `-stack-list-frames` Command

#### Synopsis

::: smallexample

```bash
 -stack-list-frames [ --no-frame-filters low-frame high-frame ]
```

:::


List the frames currently on the stack. For each frame it displays the following info:

> 列出当前堆栈中的帧。对于每一帧，它显示以下信息：

'`level`'


:   The frame number, 0 being the topmost frame, i.e., the innermost function.

> 帧号，0代表最上面的帧，即最内层函数。

'`addr`'

:   The `$pc` value for that frame.

'`func`'

:   Function name.

'`file`'

:   File name of the source file where the function lives.

'`fullname`'

:   The full file name of the source file where the function lives.

'`line`'

:   Line number corresponding to the `$pc`.

'`from`'


:   The shared library where this function is defined. This is only given if the frame's function is not known.

> 这个函数定义在共享库中。只有当帧函数未知时才给出。

'`arch`'

:   Frame's architecture.


If invoked without arguments, this command prints a backtrace for the whole stack. If given two integer arguments, it shows the frames whose levels are between the two arguments (inclusive). If the two arguments are equal, it shows the single frame at the corresponding level. It is an error if `low-frame` may be larger than the actual number of frames, in which case only existing frames will be returned. If the option `--no-frame-filters` is supplied, then Python frame filters will not be executed.

> 如果没有参数调用，此命令会打印整个堆栈的回溯。如果给定两个整数参数，它会显示两个参数（包括）之间的帧。如果两个参数相等，则会显示相应级别的单个帧。如果`low-frame`可能大于实际帧数，则会出错，在这种情况下，只会返回现有帧。如果提供了选项`--no-frame-filters`，则不会执行Python帧过滤器。

#### [GDB]

The corresponding [GDB]'.

#### Example

Full stack backtrace:

::: smallexample

```bash
(gdb)
-stack-list-frames
^done,stack=
[frame={level="0",addr="0x0001076c",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="11",
  arch="i386:x86_64"},
frame={level="1",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="2",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="3",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="4",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="5",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="6",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="7",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="8",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="9",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="10",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="11",addr="0x00010738",func="main",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="4",
  arch="i386:x86_64"}]
(gdb)
```

:::

Show frames between `low_frame`:

::: smallexample

```bash
(gdb)
-stack-list-frames 3 5
^done,stack=
[frame={level="3",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="4",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"},
frame={level="5",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"}]
(gdb)
```

:::

Show a single frame:

::: smallexample

```bash
(gdb)
-stack-list-frames 3 3
^done,stack=
[frame={level="3",addr="0x000107a4",func="foo",
  file="recursive2.c",fullname="/home/foo/bar/recursive2.c",line="14",
  arch="i386:x86_64"}]
(gdb)
```

:::

#### The `-stack-list-locals` Command

#### Synopsis

::: smallexample

```bash
 -stack-list-locals [ --no-frame-filters ] [ --skip-unavailable ] print-values
```

:::


Display the local variable names for the selected frame. If `print-values` is 0 or `--no-values`, print only the names of the variables; if it is 1 or `--all-values`, print also their values; and if it is 2 or `--simple-values`, print the name, type and value for simple data types, and the name and type for arrays, structures and unions. In this last case, a frontend can immediately display the value of simple data types and create variable objects for other data types when the user wishes to explore their values in more detail. If the option `--no-frame-filters` is supplied, then Python frame filters will not be executed.

> 显示所选框架的本地变量名称。如果`print-values`为0或`--no-values`，则仅打印变量名称；如果为1或`--all-values`，则还打印它们的值；如果为2或`--simple-values`，则打印简单数据类型的名称、类型和值，以及数组、结构和联合的名称和类型。在这种情况下，前端可以立即显示简单数据类型的值，并在用户希望更详细地探索它们的值时创建变量对象。如果提供了选项`--no-frame-filters`，则不会执行Python框架过滤器。


If the `--skip-unavailable` option is specified, local variables that are not available are not listed. Partially available local variables are still displayed, however.

> 如果指定了`--skip-unavailable`选项，不会列出不可用的局部变量。 但仍会显示部分可用的局部变量。


This command is deprecated in favor of the '`-stack-list-variables`' command.

> 这个命令已经被弃用，建议使用'-stack-list-variables'命令。

#### [GDB]

'`info locals`' in `gdbtk`.

#### Example

::: smallexample

```bash
(gdb)
-stack-list-locals 0
^done,locals=[name="A",name="B",name="C"]
(gdb)
-stack-list-locals --all-values
^done,locals=[,
  ]
-stack-list-locals --simple-values
^done,locals=[,
  ]
(gdb)
```

:::

#### The `-stack-list-variables` Command

#### Synopsis

::: smallexample

```bash
 -stack-list-variables [ --no-frame-filters ] [ --skip-unavailable ] print-values
```

:::


Display the names of local variables and function arguments for the selected frame. If `print-values` is 0 or `--no-values`, print only the names of the variables; if it is 1 or `--all-values`, print also their values; and if it is 2 or `--simple-values`, print the name, type and value for simple data types, and the name and type for arrays, structures and unions. If the option `--no-frame-filters` is supplied, then Python frame filters will not be executed.

> 在所选择的帧中显示局部变量和函数参数的名称。如果`print-values`为0或`--no-values`，则只打印变量的名称；如果为1或`--all-values`，则还打印它们的值；如果为2或`--simple-values`，则打印简单数据类型的名称、类型和值，以及数组、结构和联合的名称和类型。如果提供了`--no-frame-filters`选项，则不会执行Python帧过滤器。


If the `--skip-unavailable` option is specified, local variables and arguments that are not available are not listed. Partially available arguments and local variables are still displayed, however.

> 如果指定了`--skip-unavailable`选项，则不会列出不可用的局部变量和参数。但仍会显示部分可用的参数和局部变量。

#### Example

::: smallexample

```bash
(gdb)
-stack-list-variables --thread 1 --frame 0 --all-values
^done,variables=
(gdb)
```

:::

#### The `-stack-select-frame` Command

#### Synopsis

::: smallexample

```bash
 -stack-select-frame framenum
```

:::


Change the selected frame. Select a different frame `framenum` on the stack.

> 更改所选框架。在堆栈上选择不同的框架`framenum`。


This command in deprecated in favor of passing the '`--frame`' option to every command.

> 这个命令已经不推荐使用，建议把'--frame'选项传递给每一个命令。

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-stack-select-frame 2
^done
(gdb)
```

:::

---

::: header
Next: [GDB/MI Variable Objects](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects)]
:::
