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

`set ravenscar task-switching on`

Allows task switching when debugging a program that uses the Ravenscar Profile. This is the default.

`set ravenscar task-switching off`

Turn off task switching when debugging a program that uses the Ravenscar Profile. This is mostly intended to disable the code that adds support for the Ravenscar Profile, in case a bug in either [GDB] from working properly. To be effective, this command should be run before the program is started.

`show ravenscar task-switching`

Show whether it is possible to switch from task to task in a program using the Ravenscar Profile.

When Ravenscar task-switching is enabled, Ravenscar tasks are announced by [GDB] as if they were threads:

::: smallexample

```bash
(gdb) continue
[New Ravenscar Thread 0x2b8f0]
```

:::

Both Ravenscar tasks and the underlying CPU threads will show up in the output of `info threads`:

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

---

::: header
Next: [Ada Source Character Set](Ada-Source-Character-Set.html#Ada-Source-Character-Set)]
:::
