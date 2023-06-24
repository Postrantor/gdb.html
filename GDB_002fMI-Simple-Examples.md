---
tip: translate by openai@2023-06-23 22:09:32
...
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

> 此子节提供了几个使用[GDB/MI]的简单交互示例。


Note the line breaks shown in the examples are here only for readability, they don't appear in the real output.

> 在示例中显示的换行仅用于可读性，实际输出中不会出现。

#### Setting a Breakpoint


Setting a breakpoint generates synchronous output which contains detailed information of the breakpoint.

> 设置断点会生成同步输出，其中包含有关断点的详细信息。

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

> 程序执行生成异步记录，MI给出了执行停止的原因。

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
