---
tip: translate by openai@2023-06-23 16:54:37
...
---
description: Active Targets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Active Targets (Debugging with GDB)
lang: en
resource-type: document
title: Active Targets (Debugging with GDB)
------------------------------------------

::: header
Next: [Target Commands](Target-Commands.html#Target-Commands)]
:::

---

### 19.1 Active Targets

There are multiple classes of targets such as: processes, executable files or recording sessions. Core files belong to the process class, making core file and process mutually exclusive. Otherwise, [GDB] can work concurrently on multiple active targets, one in each class. This allows you to (for example) start a process and inspect its activity, while still having access to the executable file after the process finishes. Or if you start process recording (see [Reverse Execution](Reverse-Execution.html#Reverse-Execution)) and `reverse-step` there, you are presented a virtual layer of the recording target, while the process target remains stopped at the chronologically last point of the process execution.

> 有多种类型的目标，例如：进程、可执行文件或录制会话。核心文件属于进程类，使得核心文件和进程互斥。否则，[GDB] 可以同时在多个活动目标上工作，每个类别一个。这样，您就可以（例如）启动一个进程并检查其活动，而在进程完成后仍然可以访问可执行文件。或者，如果您启动进程记录（参见[反向执行](Reverse-Execution.html#Reverse-Execution)) 并 `反向步进`，则会显示录制目标的虚拟层，而进程目标仍处于进程执行的时间上最后一点的停止状态。

Use the `core-file` and `exec-file` commands to select a new core file or executable target (see [Commands to Specify Files](Files.html#Files)). To specify as a target a process that is already running, use the `attach` command (see [Debugging an Already-running Process](Attach.html#Attach)).

> 使用 `core-file` 和 `exec-file` 命令选择新的核心文件或可执行目标（参见[指定文件命令](Files.html#Files)）。要将已运行的进程指定为目标，请使用 `attach` 命令（参见[调试运行中的进程](Attach.html#Attach)）。
