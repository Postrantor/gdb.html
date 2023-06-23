---
description: GDB/MI Simple Examples (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Simple Examples (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Simple Examples (Debugging with GDB)
---
::: header
Next: [GDB/MI Command Description Format](GDB_002fMI-Command-Description-Format.html#GDB_002fMI-Command-Description-Format)]
:::

---

### 27.6 Simple Examples of [GDB/MI]

This subsection presents several simple examples of interaction using the [GDB/MI].

Note the line breaks shown in the examples are here only for readability, they don't appear in the real output.

#### Setting a Breakpoint

Setting a breakpoint generates synchronous output which contains detailed information of the breakpoint.

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

#### Program Execution

Program execution generates asynchronous records and MI gives the reason that execution stopped.

::: smallexample

```bash
-> -exec-run
<- ^running
<- (gdb)
<- *stopped,reason="breakpoint-hit",disp="keep",bkptno="1",thread-id="0",
   frame={addr="0x08048564",func="main",
   args=,
   file="myprog.c",fullname="/home/nickrob/myprog.c",line="68",
   arch="i386:x86_64"}
<- (gdb)
-> -exec-continue
<- ^running
<- (gdb)
<- *stopped,reason="exited-normally"
<- (gdb)
```

:::

#### Quitting [GDB]

Quitting [GDB]'.

::: smallexample

```bash
-> (gdb)
<- -gdb-exit
<- ^exit
```

:::

Please note that '`^exit` if it fails to exit in reasonable time.

#### A Bad Command

Here's what happens if you pass a non-existent command:

::: smallexample

```bash
-> -rubbish
<- ^error,msg="Undefined MI command: rubbish"
<- (gdb)
```

:::
