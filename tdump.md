---
description: tdump (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: tdump (Debugging with GDB)
lang: en
resource-type: document
title: tdump (Debugging with GDB)
---
::: header
Next: [save tracepoints](save-tracepoints.html#save-tracepoints)]
:::

---

#### 13.2.2 `tdump`

This command takes no arguments. It prints all the data collected at the current trace snapshot.

::: smallexample

```bash
(gdb) trace 444
(gdb) actions
Enter actions for tracepoint #2, one per line:
> collect $regs, $locals, $args, gdb_long_test
> end

(gdb) tstart

(gdb) tfind line 444
#0  gdb_test (p1=0x11, p2=0x22, p3=0x33, p4=0x44, p5=0x55, p6=0x66)
at gdb_test.c:444
444        printp( "%s: arguments = 0x%X 0x%X 0x%X 0x%X 0x%X 0x%X\n", )

(gdb) tdump
Data collected at tracepoint 2, trace frame 1:
d0             0xc4aa0085       -995491707
d1             0x18     24
d2             0x80     128
d3             0x33     51
d4             0x71aea3d        119204413
d5             0x22     34
d6             0xe0     224
d7             0x380035 3670069
a0             0x19e24a 1696330
a1             0x3000668        50333288
a2             0x100    256
a3             0x322000 3284992
a4             0x3000698        50333336
a5             0x1ad3cc 1758156
fp             0x30bf3c 0x30bf3c
sp             0x30bf34 0x30bf34
ps             0x0      0
pc             0x20b2c8 0x20b2c8
fpcontrol      0x0      0
fpstatus       0x0      0
fpiaddr        0x0      0
p = 0x20e5b4 "gdb-test"
p1 = (void *) 0x11
p2 = (void *) 0x22
p3 = (void *) 0x33
p4 = (void *) 0x44
p5 = (void *) 0x55
p6 = (void *) 0x66
gdb_long_test = 17 '\021'

(gdb)
```

:::

`tdump` works by scanning the tracepoint's current collection actions and printing the value of each expression listed. So `tdump` can fail, if after a run, you change the tracepoint's actions to mention variables that were not collected during the run.

Also, for tracepoints with `while-stepping` loops, `tdump` uses the collected value of `$pc` to distinguish between trace frames that were collected at the tracepoint hit, and frames that were collected while stepping. This allows it to correctly choose whether to display the basic list of collections, or the collections from the body of the while-stepping loop. However, if `$pc` was not collected, then `tdump` will always attempt to dump using the basic collection list, and may fail if a while-stepping frame does not include all the same data that is collected at the tracepoint hit.

---

::: header
Next: [save tracepoints](save-tracepoints.html#save-tracepoints)]
:::
