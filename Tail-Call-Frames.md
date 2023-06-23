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

During execution of function `C`, there will be no indication in the function call stack frames that it was tail-called from `B`. If function `A` regularly calls function `B` which tail-calls function `C`, then [GDB] can determine that `C` was tail-called from `B`, and it will then create fictitious call frame for that, with the return address set up as if `B` called `C` normally.

This functionality is currently supported only by DWARF 2 debugging format and the compiler has to produce '`DW_TAG_call_site` during compilation, to get this information.

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

`set debug entry-values`

When set to on, enables printing of analysis messages for both frame argument values at function entry and tail calls. It will show all the possible valid tail calls code paths it has considered. It will also print the intersection of them with the final unambiguous (possibly partial or even empty) code path result.

`show debug entry-values`

Show the current state of analysis messages printing for both frame argument values at function entry and tail calls.

The analysis messages for tail calls can for example show why the virtual tail call frame for function `c` has not been recognized (due to the indirect reference by variable `x`):

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

`initial:` state shows some random possible calling sequence [GDB] has found. It then finds another possible calling sequence - that one is prefixed by `compare:`. The non-ambiguous intersection of these two is printed as the `reduced:` calling sequence. That one could have many further `compare:` and `reduced:` statements as long as there remain any non-ambiguous sequence entries.

For the frame of function `b` in both cases there are different possible `$pc` values (`0x4004cc` or `0x4004ce`), therefore this frame is also ambiguous. The only non-ambiguous frame is the one for function `a`, therefore this one is displayed to the user while the ambiguous frames are omitted.

There can be also reasons why printing of frame argument values at function entry may fail:

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

---

::: header
Previous: [Inline Functions](Inline-Functions.html#Inline-Functions)]
:::
