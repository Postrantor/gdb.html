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

`number`

:   The breakpoint number.

`type`

:   The type of the breakpoint. For ordinary breakpoints this will be '`breakpoint`', but many values are possible.

`catch-type`

:   If the type of the breakpoint is '`catchpoint`', then this indicates the exact type of catchpoint.

`disp`

:   This is the breakpoint disposition---either '`del`', meaning that the breakpoint will not be deleted.

`enabled`

:   This indicates whether the breakpoint is enabled, in which case the value is '`y`'. Note that this is not the same as the field `enable`.

`addr`

:   The address of the breakpoint. This may be a hexidecimal number, giving the address; or the string '`<PENDING>`', for a breakpoint with multiple locations. This field will not be present if no address can be determined. For example, a watchpoint does not have an address.

`addr_flags`

:   Optional field containing any flags related to the address. These flags are architecture-dependent; see [Architectures](Architectures.html#Architectures) for their meaning for a particular CPU.

`func`

:   If known, the function in which the breakpoint appears. If not known, this field is not present.

`filename`

:   The name of the source file which contains this function, if known. If not known, this field is not present.

`fullname`

:   The full file name of the source file which contains this function, if known. If not known, this field is not present.

`line`

:   The line number at which this breakpoint appears, if known. If not known, this field is not present.

`at`

:   If the source file is not known, this field may be provided. If provided, this holds the address of the breakpoint, possibly followed by a symbol name.

`pending`

:   If this breakpoint is pending, this field is present and holds the text used to set the breakpoint, as entered by the user.

`evaluated-by`

:   Where this breakpoint's condition is evaluated, either '`host`'.

`thread`

:   If this is a thread-specific breakpoint, then this identifies the thread in which the breakpoint can trigger.

`task`

:   If this breakpoint is restricted to a particular Ada task, then this field will hold the task identifier.

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

`times`

:   The number of times the breakpoint has been hit.

`installed`

:   This field is only given for tracepoints. This is either '`y`', meaning that it is not.

`what`

:   Some extra data, the exact contents of which are type-dependent.

`locations`

:   This field is present if the breakpoint has multiple locations. It is also exceptionally present if the breakpoint is enabled and has a single, disabled location.

```
The value is a list of locations. The format of a location is described below.
```

A location in a multi-location breakpoint is represented as a tuple with the following fields:

`number`

:   The location number as a dotted pair, like '`1.2`'. The first digit is the number of the parent breakpoint. The second digit is the number of the location within that breakpoint.

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

`func`

:   If known, the function in which the location appears. If not known, this field is not present.

`file`

:   The name of the source file which contains this location, if known. If not known, this field is not present.

`fullname`

:   The full file name of the source file which contains this location, if known. If not known, this field is not present.

`line`

:   The line number at which this location appears, if known. If not known, this field is not present.

`thread-groups`

:   The thread groups this location is in.

For example, here is what the output of `-break-insert` (see [GDB/MI Breakpoint Commands](GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands)) might be:

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
