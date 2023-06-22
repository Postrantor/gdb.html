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

)*

:   Start a recording using the given `method` is given, the default method will be used. Returns a `gdb.Record` object on success. Throw an exception on failure.

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

```
<!-- -->
```

Function: **gdb.stop_recording** *()*

:   Stop the current recording. Throw an exception if no recording is currently active. All record objects become invalid after this call.

A `gdb.Record` object has the following attributes:

Variable: **Record.method**

:   A string with the current recording method, e.g. `full` or `btrace`.

```
<!-- -->
```

Variable: **Record.format**

:   A string with the current recording format, e.g. `bt`, `pts` or `None`.

```
<!-- -->
```

Variable: **Record.begin**

:   A method specific instruction object representing the first instruction in this recording.

```
<!-- -->
```

Variable: **Record.end**

:   A method specific instruction object representing the current instruction, that is not actually part of the recording.

```
<!-- -->
```

Variable: **Record.replay_position**

:   The instruction representing the current replay position. If there is no replay active, this will be `None`.

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

Variable: **Instruction.pc**

:   An integer representing this instruction's address.

```
<!-- -->
```

Variable: **Instruction.data**

:   A buffer with the raw instruction data. In Python 3, the return value is a `memoryview` object.

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

```
<!-- -->
```

Variable: **RecordInstruction.sal**

:   A `gdb.Symtab_and_line` object representing the associated symtab and line of this instruction. May be `None` if no debug information is available.

```
<!-- -->
```

Variable: **RecordInstruction.is_speculative**

:   A boolean indicating whether the instruction was executed speculatively.

If an error occurred during recording or decoding a recording, this error is represented by a `gdb.RecordGap` object in the instruction list. It has the following attributes:

Variable: **RecordGap.number**

:   An integer identifying this gap. `number` corresponds to the numbers seen in `record instruction-history` (see [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)).

```
<!-- -->
```

Variable: **RecordGap.error_code**

:   A numerical representation of the reason for the gap. The value is specific to the current recording method.

```
<!-- -->
```

Variable: **RecordGap.error_string**

:   A human readable string with the reason for the gap.

A `gdb.RecordFunctionSegment` object has the following attributes:

Variable: **RecordFunctionSegment.number**

:   An integer identifying this function segment. `number` corresponds to the numbers seen in `record function-call-history` (see [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)).

```
<!-- -->
```

Variable: **RecordFunctionSegment.symbol**

:   A `gdb.Symbol` object representing the associated symbol. May be `None` if no debug information is available.

```
<!-- -->
```

Variable: **RecordFunctionSegment.level**

:   An integer representing the function call's stack level. May be `None` if the function call is a gap.

```
<!-- -->
```

Variable: **RecordFunctionSegment.instructions**

:   A list of `gdb.RecordInstruction` or `gdb.RecordGap` objects associated with this function call.

```
<!-- -->
```

Variable: **RecordFunctionSegment.up**

:   A `gdb.RecordFunctionSegment` object representing the caller's function segment. If the call has not been recorded, this will be the function segment to which control returns. If neither the call nor the return have been recorded, this will be `None`.

```
<!-- -->
```

Variable: **RecordFunctionSegment.prev**

:   A `gdb.RecordFunctionSegment` object representing the previous segment of this function call. May be `None`.

```
<!-- -->
```

Variable: **RecordFunctionSegment.next**

:   A `gdb.RecordFunctionSegment` object representing the next segment of this function call. May be `None`.

The following example demonstrates the usage of these objects and functions to create a function that will rewind a record to the last time a function in a different file was executed. This would typically be used to track the execution of user provided callback functions in a library which typically are not visible in a back trace.

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
