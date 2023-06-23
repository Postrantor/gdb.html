---
description: Active Targets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Active Targets (Debugging with GDB)
lang: en
resource-type: document
title: Active Targets (Debugging with GDB)
---
::: header
Next: [Target Commands](Target-Commands.html#Target-Commands)]
:::

---

### 19.1 Active Targets

There are multiple classes of targets such as: processes, executable files or recording sessions. Core files belong to the process class, making core file and process mutually exclusive. Otherwise, [GDB] can work concurrently on multiple active targets, one in each class. This allows you to (for example) start a process and inspect its activity, while still having access to the executable file after the process finishes. Or if you start process recording (see [Reverse Execution](Reverse-Execution.html#Reverse-Execution)) and `reverse-step` there, you are presented a virtual layer of the recording target, while the process target remains stopped at the chronologically last point of the process execution.

Use the `core-file` and `exec-file` commands to select a new core file or executable target (see [Commands to Specify Files](Files.html#Files)). To specify as a target a process that is already running, use the `attach` command (see [Debugging an Already-running Process](Attach.html#Attach)).
