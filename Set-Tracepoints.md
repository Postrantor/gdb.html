---
tip: translate by openai@2023-06-24 02:47:25
...
---
description: Set Tracepoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Set Tracepoints (Debugging with GDB)
lang: en
resource-type: document
title: Set Tracepoints (Debugging with GDB)
---
::: header
Next: [Analyze Collected Data](Analyze-Collected-Data.html#Analyze-Collected-Data)]
:::

---

### 13.1 Commands to Set Tracepoints


Before running such a *trace experiment*, an arbitrary number of tracepoints can be set. A tracepoint is actually a special type of breakpoint (see [Set Breaks](Set-Breaks.html#Set-Breaks)), so you can manipulate it using standard breakpoint commands. For instance, as with breakpoints, tracepoint numbers are successive integers starting from one, and many of the commands associated with tracepoints take the tracepoint number as their argument, to identify which tracepoint to work on.

> 在运行这样的跟踪实验之前，可以设置任意数量的跟踪点。跟踪点实际上是特殊类型的断点（参见[设置断点]（Set-Breaks.html#Set-Breaks）），因此可以使用标准断点命令来操纵它。例如，与断点一样，跟踪点号从一开始是连续的整数，与跟踪点相关的许多命令都将跟踪点号作为其参数，以标识要处理哪个跟踪点。


For each tracepoint, you can specify, in advance, some arbitrary set of data that you want the target to collect in the trace buffer when it hits that tracepoint. The collected data can include registers, local variables, or global data. Later, you can use [GDB] commands to examine the values these data had at the time the tracepoint was hit.

> 对于每个跟踪点，您可以提前指定您希望目标在触及该跟踪点时收集跟踪缓冲区中的某些任意数据集。收集的数据可以包括寄存器、局部变量或全局数据。稍后，您可以使用[GDB]命令检查跟踪点被触及时这些数据的值。


Tracepoints do not support every breakpoint feature. Ignore counts on tracepoints have no effect, and tracepoints cannot run [GDB] commands when they are hit. Tracepoints may not be thread-specific either.

> 跟踪点不支持每一个断点特性。跟踪点上的忽略计数没有效果，当跟踪点被触发时，也不能运行GDB命令。跟踪点也可能不是特定的线程。


Some targets may support *fast tracepoints*, which are inserted in a different way (such as with a jump instead of a trap), that is faster but possibly restricted in where they may be installed.

> 一些目标可能支持*快速跟踪点*，它们以不同的方式插入（例如使用跳转而不是陷阱），速度更快，但可能受到安装位置的限制。


Regular and fast tracepoints are dynamic tracing facilities, meaning that they can be used to insert tracepoints at (almost) any location in the target. Some targets may also support controlling *static tracepoints* from [GDB] static tracepoint on an instrumentation point, or marker, is referred to as *probing* a static tracepoint marker.

> 普通和快速跟踪点是动态跟踪设施，意味着它们可以用于在目标中（几乎）任何位置插入跟踪点。一些目标也可能支持从[GDB]静态跟踪点控制静态跟踪点，称为静态跟踪点标记的探测。

`gdbserver` supports tracepoints on some target systems. See [Tracepoints support in `gdbserver`](Server.html#Server).


This section describes commands to set tracepoints and associated conditions and actions.

> 这一节描述了设置跟踪点及其相关条件和动作的命令。

---


• [Create and Delete Tracepoints](Create-and-Delete-Tracepoints.html#Create-and-Delete-Tracepoints):                                   

> • [创建和删除跟踪点](Create-and-Delete-Tracepoints.html#Create-and-Delete-Tracepoints):

• [Enable and Disable Tracepoints](Enable-and-Disable-Tracepoints.html#Enable-and-Disable-Tracepoints):                                

> • [启用和禁用跟踪点](Enable-and-Disable-Tracepoints.html#Enable-and-Disable-Tracepoints):

• [Tracepoint Passcounts](Tracepoint-Passcounts.html#Tracepoint-Passcounts):                                                           

> • [跟踪点通过计数](Tracepoint-Passcounts.html#Tracepoint-Passcounts):

• [Tracepoint Conditions](Tracepoint-Conditions.html#Tracepoint-Conditions):                                                           

> • [跟踪点条件](Tracepoint-Conditions.html#Tracepoint-Conditions):

• [Trace State Variables](Trace-State-Variables.html#Trace-State-Variables):                                                           

> • [追踪状态变量](Trace-State-Variables.html#Trace-State-Variables):

• [Tracepoint Actions](Tracepoint-Actions.html#Tracepoint-Actions):                                                                    

> • [跟踪点操作](Tracepoint-Actions.html#Tracepoint-Actions):

• [Listing Tracepoints](Listing-Tracepoints.html#Listing-Tracepoints):                                                                 

> • [列出跟踪点](Listing-Tracepoints.html#Listing-Tracepoints):

• [Listing Static Tracepoint Markers](Listing-Static-Tracepoint-Markers.html#Listing-Static-Tracepoint-Markers):                       

> • [列出静态跟踪点标记](Listing-Static-Tracepoint-Markers.html#Listing-Static-Tracepoint-Markers):

• [Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments):     

> • [开始和停止跟踪实验](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments):

• [Tracepoint Restrictions](Tracepoint-Restrictions.html#Tracepoint-Restrictions):                                                                    

> • [跟踪点限制](Tracepoint-Restrictions.html#Tracepoint-Restrictions):

---

---

::: header
Next: [Analyze Collected Data](Analyze-Collected-Data.html#Analyze-Collected-Data)]
:::
