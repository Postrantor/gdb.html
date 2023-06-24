---
tip: translate by openai@2023-06-24 01:57:29
...
---
description: Recordings In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Recordings In Python (Debugging with GDB)
lang: en
resource-type: document
title: Recordings In Python (Debugging with GDB)
---
::: header
Next: [CLI Commands In Python](CLI-Commands-In-Python.html#CLI-Commands-In-Python)]
:::

---

#### 23.3.2.19 Recordings In Python


The following recordings-related functions (see [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)) are available in the `gdb` module:

> 以下录音相关功能（参见[处理录音和重放](Process-Record-and-Replay.html#Process-Record-and-Replay)）可在`gdb`模块中使用：

)*


:   Start a recording using the given `method` is given, the default method will be used. Returns a `gdb.Record` object on success. Throw an exception on failure.

> 开始使用给定的`方法`录制，如果没有指定方法，将使用默认方法。成功时会返回一个`gdb.Record`对象。失败时抛出异常。

```
The following strings can be passed as `method`:

-   `"full"`
-   `"btrace"`: Possible values for `format`: `"pt"`, `"bts"` or leave out for default format.
```

```
<!-- -->
```

Function: **gdb.current_recording** *()*


:   Access a currently running recording. Return a `gdb.Record` object on success. Return `None` if no recording is currently active.

> 访问当前正在运行的记录。如果成功，返回一个`gdb.Record`对象。如果当前没有活动的记录，则返回`None`。

```
<!-- -->
```

Function: **gdb.stop_recording** *()*


:   Stop the current recording. Throw an exception if no recording is currently active. All record objects become invalid after this call.

> 停止当前录制。如果当前没有录制活动，则抛出异常。此调用后，所有记录对象都失效。

A `gdb.Record` object has the following attributes:

Variable: **Record.method**

:   A string with the current recording method, e.g. `full` or `btrace`.

```
<!-- -->
```

Variable: **Record.format**


:   A string with the current recording format, e.g. `bt`, `pts` or `None`.

> 一个包含当前录制格式的字符串，例如`bt`、`pts`或`无`。

```
<!-- -->
```

Variable: **Record.begin**


:   A method specific instruction object representing the first instruction in this recording.

> 一个特定于方法的指令对象，代表这次录音中的第一条指令。

```
<!-- -->
```

Variable: **Record.end**


:   A method specific instruction object representing the current instruction, that is not actually part of the recording.

> 一个特定于方法的指令对象，代表当前指令，但实际上不是录制的一部分。

```
<!-- -->
```

Variable: **Record.replay_position**


:   The instruction representing the current replay position. If there is no replay active, this will be `None`.

> 当前重放位置的指令。如果没有活动的重放，这将是“无”。

```
<!-- -->
```

Variable: **Record.instruction_history**

:   A list with all recorded instructions.

```
<!-- -->
```

Variable: **Record.function_call_history**

:   A list with all recorded function call segments.

A `gdb.Record` object has the following methods:

Function: **Record.goto** *(instruction)*

:   Move the replay position to the given `instruction`.


The common `gdb.Instruction` class that recording method specific instruction objects inherit from, has the following attributes:

> 通用的`gdb.Instruction`类，用于记录特定方法指令对象的继承，具有以下属性：

Variable: **Instruction.pc**

:   An integer representing this instruction's address.

```
<!-- -->
```

Variable: **Instruction.data**


:   A buffer with the raw instruction data. In Python 3, the return value is a `memoryview` object.

> 一个缓冲区，用来存储原始指令数据。在Python 3中，返回值是一个`memoryview`对象。

```
<!-- -->
```

Variable: **Instruction.decoded**

:   A human readable string with the disassembled instruction.

```
<!-- -->
```

Variable: **Instruction.size**

:   The size of the instruction in bytes.

Additionally `gdb.RecordInstruction` has the following attributes:

Variable: **RecordInstruction.number**


:   An integer identifying this instruction. `number` corresponds to the numbers seen in `record instruction-history` (see [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)).

> 一个整数标识这条指令。“数字”对应于在“记录指令历史”（参见“进程记录和重放”）中看到的数字。

```
<!-- -->
```

Variable: **RecordInstruction.sal**


:   A `gdb.Symtab_and_line` object representing the associated symtab and line of this instruction. May be `None` if no debug information is available.

> 一个`gdb.Symtab_and_line`对象代表这条指令相关的符号表和行号。如果没有调试信息可用，可能为`None`。

```
<!-- -->
```

Variable: **RecordInstruction.is_speculative**


:   A boolean indicating whether the instruction was executed speculatively.

> 布尔值，指示指令是否已经进行了推测性执行。


If an error occurred during recording or decoding a recording, this error is represented by a `gdb.RecordGap` object in the instruction list. It has the following attributes:

> 如果录制或解码录音时发生错误，此错误将由指令列表中的`gdb.RecordGap`对象表示。它具有以下属性：

Variable: **RecordGap.number**


:   An integer identifying this gap. `number` corresponds to the numbers seen in `record instruction-history` (see [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)).

> 一个整数标识这个间隙。`数字`对应于在`记录指令历史`中看到的数字（参见[过程记录和重放](Process-Record-and-Replay.html#Process-Record-and-Replay))。

```
<!-- -->
```

Variable: **RecordGap.error_code**


:   A numerical representation of the reason for the gap. The value is specific to the current recording method.

> 数字表示的缺口原因。该值与当前记录方法特定。

```
<!-- -->
```

Variable: **RecordGap.error_string**

:   A human readable string with the reason for the gap.

A `gdb.RecordFunctionSegment` object has the following attributes:

Variable: **RecordFunctionSegment.number**


:   An integer identifying this function segment. `number` corresponds to the numbers seen in `record function-call-history` (see [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)).

> 一个整数，用于标识此功能段。“number”对应于在“记录功能调用历史”（参见[进程记录和重放]（Process-Record-and-Replay.html＃Process-Record-and-Replay））中看到的数字。

```
<!-- -->
```

Variable: **RecordFunctionSegment.symbol**


:   A `gdb.Symbol` object representing the associated symbol. May be `None` if no debug information is available.

> 一个`gdb.Symbol`对象表示相关的符号。如果没有调试信息可用，可能为`None`。

```
<!-- -->
```

Variable: **RecordFunctionSegment.level**


:   An integer representing the function call's stack level. May be `None` if the function call is a gap.

> 一个整数表示函数调用的堆栈等级。如果函数调用是一个间隙，可能为`None`。

```
<!-- -->
```

Variable: **RecordFunctionSegment.instructions**


:   A list of `gdb.RecordInstruction` or `gdb.RecordGap` objects associated with this function call.

> 一个与此函数调用相关联的`gdb.RecordInstruction`或`gdb.RecordGap`对象列表。

```
<!-- -->
```

Variable: **RecordFunctionSegment.up**


:   A `gdb.RecordFunctionSegment` object representing the caller's function segment. If the call has not been recorded, this will be the function segment to which control returns. If neither the call nor the return have been recorded, this will be `None`.

> 一个`gdb.RecordFunctionSegment`对象代表调用者的函数段。如果调用没有被记录，这将是控制返回的函数段。如果调用和返回都没有被记录，这将是`None`。

```
<!-- -->
```

Variable: **RecordFunctionSegment.prev**


:   A `gdb.RecordFunctionSegment` object representing the previous segment of this function call. May be `None`.

> 一个`gdb.RecordFunctionSegment`对象表示这个函数调用的前一段。可能是`None`。

```
<!-- -->
```

Variable: **RecordFunctionSegment.next**


:   A `gdb.RecordFunctionSegment` object representing the next segment of this function call. May be `None`.

> 一个代表此函数调用的下一段的gdb.RecordFunctionSegment对象。可能是None。


The following example demonstrates the usage of these objects and functions to create a function that will rewind a record to the last time a function in a different file was executed. This would typically be used to track the execution of user provided callback functions in a library which typically are not visible in a back trace.

> 下面的示例演示了如何使用这些对象和函数来创建一个函数，该函数将记录重新定位到上次在另一个文件中执行的函数。这通常用于跟踪库中用户提供的回调函数的执行，这些函数通常在回溯中不可见。

::: smallexample

```bash
def bringback ():
    rec = gdb.current_recording ()
    if not rec:
        return

    insn = rec.instruction_history
    if len (insn) == 0:
        return

    try:
        position = insn.index (rec.replay_position)
    except:
        position = -1
    try:
        filename = insn[position].sal.symtab.fullname ()
    except:
        filename = None

    for i in reversed (insn[:position]):
    try:
            current = i.sal.symtab.fullname ()
    except:
            current = None

        if filename == current:
            continue

        rec.goto (i)
        return
```

:::


Another possible application is to write a function that counts the number of code executions in a given line range. This line range can contain parts of functions or span across several functions and is not limited to be contiguous.

> 另一种可能的应用是编写一个函数，计算给定行范围内代码执行的次数。此行范围可以包含函数的部分，或者跨越多个函数，而不局限于连续的行。

::: smallexample

```bash
def countrange (filename, linerange):
    count = 0

    def filter_only (file_name):
        for call in gdb.current_recording ().function_call_history:
            try:
                if file_name in call.symbol.symtab.fullname ():
                    yield call
            except:
                pass

    for c in filter_only (filename):
        for i in c.instructions:
            try:
                if i.sal.line in linerange:
                    count += 1
                    break;
            except:
                    pass

    return count
```

:::

---

::: header
Next: [CLI Commands In Python](CLI-Commands-In-Python.html#CLI-Commands-In-Python)]
:::
