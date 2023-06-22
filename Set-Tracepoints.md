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

For each tracepoint, you can specify, in advance, some arbitrary set of data that you want the target to collect in the trace buffer when it hits that tracepoint. The collected data can include registers, local variables, or global data. Later, you can use [GDB] commands to examine the values these data had at the time the tracepoint was hit.

Tracepoints do not support every breakpoint feature. Ignore counts on tracepoints have no effect, and tracepoints cannot run [GDB] commands when they are hit. Tracepoints may not be thread-specific either.

Some targets may support *fast tracepoints*, which are inserted in a different way (such as with a jump instead of a trap), that is faster but possibly restricted in where they may be installed.

Regular and fast tracepoints are dynamic tracing facilities, meaning that they can be used to insert tracepoints at (almost) any location in the target. Some targets may also support controlling *static tracepoints* from [GDB] static tracepoint on an instrumentation point, or marker, is referred to as *probing* a static tracepoint marker.

`gdbserver` supports tracepoints on some target systems. See [Tracepoints support in `gdbserver`](Server.html#Server).

This section describes commands to set tracepoints and associated conditions and actions.

---

• [Create and Delete Tracepoints](Create-and-Delete-Tracepoints.html#Create-and-Delete-Tracepoints):                                   
• [Enable and Disable Tracepoints](Enable-and-Disable-Tracepoints.html#Enable-and-Disable-Tracepoints):                                
• [Tracepoint Passcounts](Tracepoint-Passcounts.html#Tracepoint-Passcounts):                                                           
• [Tracepoint Conditions](Tracepoint-Conditions.html#Tracepoint-Conditions):                                                           
• [Trace State Variables](Trace-State-Variables.html#Trace-State-Variables):                                                           
• [Tracepoint Actions](Tracepoint-Actions.html#Tracepoint-Actions):                                                                    
• [Listing Tracepoints](Listing-Tracepoints.html#Listing-Tracepoints):                                                                 
• [Listing Static Tracepoint Markers](Listing-Static-Tracepoint-Markers.html#Listing-Static-Tracepoint-Markers):                       
• [Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments):     
• [Tracepoint Restrictions](Tracepoint-Restrictions.html#Tracepoint-Restrictions):                                                                    

---

---

::: header
Next: [Analyze Collected Data](Analyze-Collected-Data.html#Analyze-Collected-Data)]
:::
