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

#### The `-trace-find` Command

#### Synopsis

::: smallexample

```bash
 -trace-find mode [parameters…]
```

:::

Find a trace frame using criteria defined by `mode`. The following table lists permissible modes and their parameters. For details of operation, see [tfind](tfind.html#tfind).

'`none`'

:   No parameters are required. Stops examining trace frames.

'`frame-number`'

:   An integer is required as parameter. Selects tracepoint frame with that index.

'`tracepoint-number`'

:   An integer is required as parameter. Finds next trace frame that corresponds to tracepoint with the specified number.

'`pc`'

:   An address is required as parameter. Finds next trace frame that corresponds to any tracepoint at the specified address.

'`pc-inside-range`'

:   Two addresses are required as parameters. Finds next trace frame that corresponds to a tracepoint at an address inside the specified range. Both bounds are considered to be inside the range.

'`pc-outside-range`'

:   Two addresses are required as parameters. Finds next trace frame that corresponds to a tracepoint at an address outside the specified range. Both bounds are considered to be inside the range.

'`line`'

:   Location specification is required as parameter. See [Location Specifications](Location-Specifications.html#Location-Specifications). Finds next trace frame that corresponds to a tracepoint at the specified location.

If '`none`, the response does not have fields. Otherwise, the response may have the following fields:

'`found`'

:   This field has either '`0`' as the value, depending on whether a matching tracepoint was found.

'`traceframe`'

:   The index of the found traceframe. This field is present iff the '`found`'.

'`tracepoint`'

:   The index of the found tracepoint. This field is present iff the '`found`'.

'`frame`'

:   The information about the frame corresponding to the found trace frame. This field is present only if a trace frame was found. See [GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information), for description of this field.

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

The reported names can be used in the normal manner to create varobjs and inspect the objects themselves. The items returned by this command are categorized so that it is clear which is a variable, which is a register, which is a trace state variable, which is a memory range and which is a computed expression.

For instance, if the actions were

::: smallexample

```bash
collect myVar, myArray[myIndex], myObj.field, myPtr->field, myCount + 2
collect *(int*)0xaf02bef0@40
```

:::

the object collected in its entirety would be `myVar`. The object `myArray` would be partially collected, because only the element at index `myIndex` would be collected. The remaining objects would be computed expressions.

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

`computed-expressions`

:   The set of computed expressions that have been collected at the current trace frame. The `--comp-print-values` option affects this set like the `--var-print-values` option affects the `explicit-variables` set. See above.

`registers`

:   The registers that have been collected at the current trace frame. For each register collected, the name and current value are returned. The value is formatted according to the `--registers-format` option. See the `-data-list-register-values` command for a list of the allowed formats. The default is '`x`'.

`tvars`

:   The trace state variables that have been collected at the current trace frame. For each trace state variable collected, the name and current value are returned.

`memory`

:   The set of memory ranges that have been collected at the current trace frame. Its content is a list of tuples. Each tuple represents a collected memory range and has the following fields:

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

'`name`'

:   The name of the trace variable. This field is always present.

'`initial`'

:   The initial value. This is a 64-bit signed integer. This field is always present.

'`current`'

:   The value the trace variable has at the moment. This is a 64-bit signed integer. This field is absent iff current value is not defined, for example if the trace was never run, or is presently running.

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

By default, this command will save the trace in the tfile format. You can supply the optional '`-ctf`' argument to save it the CTF format. See [Trace Files](Trace-Files.html#Trace-Files) for more information about CTF.

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

'`supported`'

:   May have a value of either '`0`' when examining trace file. In the latter case, examining of trace frame is possible but new tracing experiement cannot be started. This field is always present.

'`running`'

:   May have a value of either '`0`'.

'`stop-reason`'

:   Report the reason why the tracing was stopped last time. This field may be absent iff tracing was never stopped on target yet. The value of '`request`'.

'`stopping-tracepoint`'

:   The number of tracepoint whose passcount as exceeded. This field is present iff the '`stop-reason`'.

'`frames`'
'`frames-created`'

:   The '`frames`' is the total created during the run, including ones that were discarded, such as when a circular trace buffer filled up. Both fields are optional.

'`buffer-size`'
'`buffer-free`'

:   These fields tell the current size of the tracing buffer and the remaining space. These fields are optional.

'`circular`'

:   The value of the circular trace buffer flag. `1` means that the trace buffer is circular and old trace frames will be discarded if necessary to make room, `0` means that the trace buffer is linear and may fill up.

'`disconnected`'

:   The value of the disconnected tracing flag. `1` means that tracing will continue after [GDB] disconnects, `0` means that the trace run will stop.

'`trace-file`'

:   The filename of the trace file being examined. This field is optional, and only present when examining a trace file.

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

#### [GDB]

The corresponding [GDB]'.

---

::: header
Next: [GDB/MI Symbol Query](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query)]
:::
