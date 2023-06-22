---
description: JIT Interface (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: JIT Interface (Debugging with GDB)
lang: en
resource-type: document
title: JIT Interface (Debugging with GDB)
---
::: header
Next: [In-Process Agent](In_002dProcess-Agent.html#In_002dProcess-Agent)]
:::

---

## 30 JIT Compilation Interface

This chapter documents [GDB]'s *just-in-time* (JIT) compilation interface. A JIT compiler is a program or library that generates native executable code at runtime and executes it, usually in order to achieve good performance while maintaining platform independence.

Programs that use JIT compilation are normally difficult to debug because portions of their code are generated at runtime, instead of being loaded from object files, which is where [GDB] at runtime.

If you are using [GDB] to debug a program that uses this interface, then it should work transparently so long as you have not stripped the binary. If you are developing a JIT compiler, then the interface is documented in the rest of this chapter. At this time, the only known client of this interface is the LLVM JIT.

Broadly speaking, the JIT interface mirrors the dynamic loader interface. The JIT compiler communicates with [GDB] attaches, it reads a linked list of symbol files from the global variable to find existing code, and puts a breakpoint in the function so that it can find out about additional code.

---

• [Declarations](Declarations.html#Declarations):                          Relevant C struct declarations
• [Registering Code](Registering-Code.html#Registering-Code):              Steps to register code
• [Unregistering Code](Unregistering-Code.html#Unregistering-Code):        Steps to unregister code
• [Custom Debug Info](Custom-Debug-Info.html#Custom-Debug-Info):           Emit debug information in a custom format

---

---

::: header
Next: [In-Process Agent](In_002dProcess-Agent.html#In_002dProcess-Agent)]
:::
