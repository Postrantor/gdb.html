---
tip: translate by openai@2023-06-23 14:15:46
...
---
description: Tail Call Frames (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tail Call Frames (Debugging with GDB)
lang: en
resource-type: document
title: Tail Call Frames (Debugging with GDB)
---
::: header
Previous: [Inline Functions](Inline-Functions.html#Inline-Functions)]
:::

---

### 11.2 Tail Call Frames


Function `B` can call function `C` in its very last statement. In unoptimized compilation the call of `C` is immediately followed by return instruction at the end of `B` code. Optimizing compiler may replace the call and return in function `B` into one jump to function `C` instead. Such use of a jump instruction is called *tail call*.

> 函数B的最后一条语句可以调用函数C。在未优化的编译中，调用C之后立即在函数B的代码末尾返回指令。优化编译器可能会将函数B中的调用和返回替换为一个跳转到函数C的指令。这种使用跳转指令的方法称为尾调用。


During execution of function `C`, there will be no indication in the function call stack frames that it was tail-called from `B`. If function `A` regularly calls function `B` which tail-calls function `C`, then [GDB] can determine that `C` was tail-called from `B`, and it will then create fictitious call frame for that, with the return address set up as if `B` called `C` normally.

> 在执行函数C时，在函数调用堆栈帧中不会有任何指示它是从B尾调用的。如果函数A定期调用函数B，而B尾调用函数C，那么[GDB]可以确定C是从B尾调用的，然后它将为此创建虚构的调用帧，其返回地址设置为B正常调用C。


This functionality is currently supported only by DWARF 2 debugging format and the compiler has to produce '`DW_TAG_call_site` during compilation, to get this information.

> 此功能目前只由DWARF 2调试格式支持，编译器必须在编译期间产生“DW_TAG_call_site”才能获得此信息。

[info frame] output:

::: smallexample

```bash
(gdb) x/i $pc - 2
   0x40066b <b(int, double)+11>: jmp 0x400640 <c(int, double)>
(gdb) info frame
Stack level 1, frame at 0x7fffffffda30:
 rip = 0x40066d in b (amd64-entry-value.cc:59); saved rip 0x4004c5
 tail call frame, caller of frame at 0x7fffffffda30
 source language c++.
 Arglist at unknown address.
 Locals at unknown address, Previous frame's sp is 0x7fffffffda30
```

:::


The detection of all the possible code path executions can find them ambiguous. There is no execution history stored (possible [Reverse Execution](Reverse-Execution.html#Reverse-Execution) is never used for this purpose) and the last known caller could have reached the known callee by multiple different jump sequences. In such case [GDB] still tries to show at least all the unambiguous top tail callers and all the unambiguous bottom tail calees, if any.

> 检测所有可能的代码路径执行可能会让它们变得模糊不清。没有存储执行历史（永远不会用于此目的的可能[反向执行](Reverse-Execution.html#Reverse-Execution)），而最后一个已知的调用者可以通过多种不同的跳转序列到达已知的被调用者。在这种情况下，[GDB]仍然尝试显示至少所有不模糊的顶部尾调用者和所有不模糊的底部尾调用者（如果有）。

`set debug entry-values`


When set to on, enables printing of analysis messages for both frame argument values at function entry and tail calls. It will show all the possible valid tail calls code paths it has considered. It will also print the intersection of them with the final unambiguous (possibly partial or even empty) code path result.

> 当设置为“开启”时，可以在函数入口和尾调用时打印分析消息，它将显示所有可能的有效尾调用代码路径，并且它还会打印最终明确（可能是部分或者空的）代码路径结果的交集。

`show debug entry-values`


Show the current state of analysis messages printing for both frame argument values at function entry and tail calls.

> 显示函数入口和尾调用时两个框架参数值的分析消息打印的当前状态。


The analysis messages for tail calls can for example show why the virtual tail call frame for function `c` has not been recognized (due to the indirect reference by variable `x`):

> 分析尾调用的消息可以显示为什么函数`c`的虚拟尾调用框架没有被识别（由变量`x`间接引用）：

::: smallexample

```bash
static void __attribute__((noinline, noclone)) c (void);
void (*x) (void) = c;
static void __attribute__((noinline, noclone)) a (void) 
static void __attribute__((noinline, noclone)) c (void) 
int main (void) 

Breakpoint 1, DW_OP_entry_value resolving cannot find
DW_TAG_call_site 0x40039a in main
a () at t.c:3
3   static void __attribute__((noinline, noclone)) a (void) 
(gdb) bt
#0  a () at t.c:3
#1  0x000000000040039a in main () at t.c:5
```

:::


Another possibility is an ambiguous virtual tail call frames resolution:

> 另一种可能性是模糊的虚拟尾调用帧解析。

::: smallexample

```bash
int i;
static void __attribute__((noinline, noclone)) f (void) 
static void __attribute__((noinline, noclone)) e (void) 
static void __attribute__((noinline, noclone)) d (void) 
static void __attribute__((noinline, noclone)) c (void) 
static void __attribute__((noinline, noclone)) b (void)

static void __attribute__((noinline, noclone)) a (void) 
int main (void) 

tailcall: initial: 0x4004d2(a) 0x4004ce(b) 0x4004b2(c) 0x4004a2(d)
tailcall: compare: 0x4004d2(a) 0x4004cc(b) 0x400492(e)
tailcall: reduced: 0x4004d2(a) |
(gdb) bt
#0  f () at t.c:2
#1  0x00000000004004d2 in a () at t.c:8
#2  0x0000000000400395 in main () at t.c:9
```

:::


Frames #0 and #2 are real, #1 is a virtual tail call frame. The code can have possible execution paths `main→a→b→c→d→f` or `main→a→b→e→f`, [GDB] cannot find which one from the inferior state.

> 框架#0和#2是真实的，#1是虚拟尾调用框架。代码可能有可能的执行路径`main→a→b→c→d→f`或`main→a→b→e→f`，[GDB]无法从下级状态中找到其中的哪一个。

`initial:` state shows some random possible calling sequence [GDB] has found. It then finds another possible calling sequence - that one is prefixed by `compare:`. The non-ambiguous intersection of these two is printed as the `reduced:` calling sequence. That one could have many further `compare:` and `reduced:` statements as long as there remain any non-ambiguous sequence entries.


For the frame of function `b` in both cases there are different possible `$pc` values (`0x4004cc` or `0x4004ce`), therefore this frame is also ambiguous. The only non-ambiguous frame is the one for function `a`, therefore this one is displayed to the user while the ambiguous frames are omitted.

> 对于函数`b`的帧在两种情况下都有不同的可能的$pc值（0x4004cc或0x4004ce），因此这个帧也是模糊的。唯一不模糊的帧是函数`a`的帧，因此它被显示给用户，而模糊的帧被省略。


There can be also reasons why printing of frame argument values at function entry may fail:

> 也可能有原因导致在函数入口处打印框架参数值失败：

::: smallexample

```bash
int v;
static void __attribute__((noinline, noclone)) c (int i) 
static void __attribute__((noinline, noclone)) a (int i);
static void __attribute__((noinline, noclone)) b (int i) 
static void __attribute__((noinline, noclone)) a (int i)

int main (void) 

(gdb) bt
#0  c (i=i@entry=0) at t.c:2
#1  0x0000000000400428 in a (DW_OP_entry_value resolving has found
function "a" at 0x400420 can call itself via tail calls
i=<optimized out>) at t.c:6
#2  0x000000000040036e in main () at t.c:7
```

:::


[GDB] prints `<optimized out>` instead.

> GDB 打印出 `<优化掉>` 。

---

::: header
Previous: [Inline Functions](Inline-Functions.html#Inline-Functions)]
:::
