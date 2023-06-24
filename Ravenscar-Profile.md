---
tip: translate by openai@2023-06-24 01:51:02
...
---
description: Ravenscar Profile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ravenscar Profile (Debugging with GDB)
lang: en
resource-type: document
title: Ravenscar Profile (Debugging with GDB)
---
::: header
Next: [Ada Source Character Set](Ada-Source-Character-Set.html#Ada-Source-Character-Set)]
:::

---

#### 15.4.10.9 Tasking Support when using the Ravenscar Profile


The *Ravenscar Profile* is a subset of the Ada tasking features, specifically designed for systems with safety-critical real-time requirements.

> 「渡鴉峰設定檔」是Ada任務功能的一個子集，特別針對具有安全關鍵時間要求的系統而設計。

`set ravenscar task-switching on`


Allows task switching when debugging a program that uses the Ravenscar Profile. This is the default.

> 允许在调试使用Ravenscar Profile的程序时进行任务切换，这是默认设置。

`set ravenscar task-switching off`


Turn off task switching when debugging a program that uses the Ravenscar Profile. This is mostly intended to disable the code that adds support for the Ravenscar Profile, in case a bug in either [GDB] from working properly. To be effective, this command should be run before the program is started.

> 在调试使用Ravenscar Profile的程序时，关闭任务切换。这主要是为了禁用添加支持Ravenscar Profile的代码，以防止[GDB]出现错误。为了起到有效的作用，这个命令应该在程序启动之前运行。

`show ravenscar task-switching`


Show whether it is possible to switch from task to task in a program using the Ravenscar Profile.

> 请帮助我翻译：使用Ravenscar Profile检查程序中是否可以在任务之间切换。


When Ravenscar task-switching is enabled, Ravenscar tasks are announced by [GDB] as if they were threads:

> 当启用Ravenscar任务切换时，Ravenscar任务将由GDB按照线程一样宣布。

::: smallexample

```bash
(gdb) continue
[New Ravenscar Thread 0x2b8f0]
```

:::


Both Ravenscar tasks and the underlying CPU threads will show up in the output of `info threads`:

> 在`info threads`的输出中，Ravenscar任务和底层的CPU线程都会显示出来。

::: smallexample

```bash
(gdb) info threads
  Id   Target Id                  Frame
  1    Thread 1 (CPU#0 [running]) simple () at simple.adb:10
  2    Thread 2 (CPU#1 [running]) 0x0000000000003d34 in __gnat_initialize_cpu_devices ()
  3    Thread 3 (CPU#2 [running]) 0x0000000000003d28 in __gnat_initialize_cpu_devices ()
  4    Thread 4 (CPU#3 [halted ]) 0x000000000000c6ec in system.task_primitives.operations.idle ()
* 5    Ravenscar Thread 0x2b8f0   simple () at simple.adb:10
  6    Ravenscar Thread 0x2f150   0x000000000000c6ec in system.task_primitives.operations.idle ()
```

:::


One known limitation of the Ravenscar support in [GDB] is that it isn't currently possible to single-step through the runtime initialization sequence. If you need to debug this code, you should use `set ravenscar task-switching off`.

> 在GDB中，Ravenscar支持的一个已知限制是目前无法单步调试运行时初始化序列。如果需要调试此代码，应使用“set ravenscar task-switching off”。

---

::: header
Next: [Ada Source Character Set](Ada-Source-Character-Set.html#Ada-Source-Character-Set)]
:::
