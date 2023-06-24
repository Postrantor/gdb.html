---
tip: translate by openai@2023-06-23 18:53:43
...
---
description: Checkpoint/Restart (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Checkpoint/Restart (Debugging with GDB)
lang: en
resource-type: document
title: Checkpoint/Restart (Debugging with GDB)
---
::: header
Previous: [Forks](Forks.html#Forks)]
:::

---

### 4.12 Setting a *Bookmark* to Return to Later


On certain operating systems[^4^](#FOOT4) is able to save a *snapshot* of a program's state, called a *checkpoint*, and come back to it later.

> 在某些操作系统上，可以保存一个程序状态的快照，称为检查点，以便稍后回头。


Returning to a checkpoint effectively undoes everything that has happened in the program since the `checkpoint` was saved. This includes changes in memory, registers, and even (within some limits) system state. Effectively, it is like going back in time to the moment when the checkpoint was saved.

> 回到检查点实际上可以撤销自从保存检查点以来程序中发生的一切。这包括内存、寄存器甚至（在一定范围内）系统状态的变化。实际上，这就像回到保存检查点时的那一刻。


Thus, if you're stepping thru a program and you think you're getting close to the point where things go wrong, you can save a checkpoint. Then, if you accidentally go too far and miss the critical statement, instead of having to restart your program from the beginning, you can just go back to the checkpoint and start again from there.

> 因此，如果你正在走过一个程序，你认为你快要到出错的地方了，你可以保存一个检查点。然后，如果你不小心走得太远，错过了关键的语句，你不必从头开始重新运行程序，而只需回到检查点，从那里重新开始即可。


This can be especially useful if it takes a lot of time or steps to reach the point where you think the bug occurs.

> 这在花费很多时间或步骤才能找到出错点的情况下尤其有用。


To use the `checkpoint`/`restart` method of debugging:

> 使用检查点/重启调试方法：

`checkpoint`


Save a snapshot of the debugged program's current execution state. The `checkpoint` command takes no arguments, but each checkpoint is assigned a small integer id, similar to a breakpoint id.

> 保存调试程序当前执行状态的快照。 `checkpoint` 命令不需要参数，但每个检查点都会分配一个小的整数ID，类似于断点ID。

`info checkpoints`


List the checkpoints that have been saved in the current debugging session. For each checkpoint, the following information will be listed:

> 列出当前调试会话中已保存的检查点。对于每个检查点，将列出以下信息：

`Checkpoint ID`

`Process ID`

`Code Address`

`Source line, or label`

`restart checkpoint-id`


Restore the program state that was saved as checkpoint number `checkpoint-id`. All program variables, registers, stack frames etc. will be returned to the values that they had when the checkpoint was saved. In essence, gdb will "wind back the clock" to the point in time when the checkpoint was saved.

> 恢复作为检查点编号`checkpoint-id`保存的程序状态。 所有程序变量，寄存器，堆栈帧等都将恢复为保存检查点时的值。 概括而言，GDB将“倒回时钟”至保存检查点时的时间点。


Note that breakpoints, [GDB] variables, command history etc. are not affected by restoring a checkpoint. In general, a checkpoint only restores things that reside in the program being debugged, not in the debugger.

> 注意，断点、[GDB]变量、命令历史等不受恢复检查点的影响。通常，检查点只恢复调试程序中的内容，而不是调试器中的内容。

`delete checkpoint checkpoint-id`


Delete the previously-saved checkpoint identified by `checkpoint-id`.

> 删除由“checkpoint-id”标识的先前保存的检查点。


Returning to a previously saved checkpoint will restore the user state of the program being debugged, plus a significant subset of the system (OS) state, including file pointers. It won't "un-write" data from a file, but it will rewind the file pointer to the previous location, so that the previously written data can be overwritten. For files opened in read mode, the pointer will also be restored so that the previously read data can be read again.

> 回到之前保存的检查点将恢复被调试程序的用户状态，以及系统（操作系统）状态的重要子集，包括文件指针。它不会“撤消”文件中的数据，但它会将文件指针重新指向先前的位置，以便可以覆盖先前写入的数据。对于以读取模式打开的文件，指针也将被恢复，以便可以重新读取先前读取的数据。


Of course, characters that have been sent to a printer (or other external device) cannot be "snatched back", and characters received from eg. a serial device can be removed from internal program buffers, but they cannot be "pushed back" into the serial pipeline, ready to be received again. Similarly, the actual contents of files that have been changed cannot be restored (at this time).

> 当然，已发送到打印机（或其他外部设备）的字符无法被“抢回”，从例如串行设备接收的字符可以从内部程序缓冲区中删除，但无法将其“推回”到串行管道中，以便再次接收。类似地，已更改的文件的实际内容无法恢复（目前）。


However, within those constraints, you actually can "rewind" your program to a previously saved point in time, and begin debugging it again --- and you can change the course of events so as to debug a different execution path this time.

> 然而，在这些限制条件下，您实际上可以将程序“倒带”到以前保存的时间点，并再次开始调试它---而且您可以改变事件的进程，以便这次调试不同的执行路径。


Finally, there is one bit of internal program state that will be different when you return to a checkpoint --- the program's process id. Each checkpoint will have a unique process id (or `pid`. If your program has saved a local copy of its process id, this could potentially pose a problem.

> 最后，当您返回检查点时，程序的内部状态会有所不同——程序的进程ID。每个检查点都有一个唯一的进程ID（或“PID”）。如果您的程序已经保存了它的进程ID的本地副本，这可能会带来问题。

#### 4.12.1 A Non-obvious Benefit of Using Checkpoints


On some systems such as [GNU]/Linux, address space randomization is performed on new processes for security reasons. This makes it difficult or impossible to set a breakpoint, or watchpoint, on an absolute address if you have to restart the program, since the absolute location of a symbol will change from one execution to the next.

> 在一些系统，比如[GNU]/Linux，为了安全原因，新进程会执行地址空间随机化。这使得如果你必须重启程序，在绝对地址上设置断点或者观察点变得困难或者不可能，因为符号的绝对位置会在不同的执行中发生变化。


A checkpoint, however, is an *identical* copy of a process. Therefore if you create a checkpoint at (eg.) the start of main, and simply return to that checkpoint instead of restarting the process, you can avoid the effects of address randomization and your symbols will all stay in the same place.

> 检查点是进程的完全相同的副本。因此，如果在（例如）主函数开始处创建一个检查点，并且只是返回该检查点而不是重新启动进程，就可以避免地址随机化的影响，您的符号将都保持在同一位置。

::: footnote

---

#### Footnotes

### [(4)](#DOCF4)


Currently, only [GNU]/Linux.

> 目前只有[GNU]/Linux。
:::

---

::: header
Previous: [Forks](Forks.html#Forks)]
:::
