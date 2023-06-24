---
tip: translate by openai@2023-06-23 23:44:00
...
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

> 本章记录了GDB的即时编译接口。JIT编译器是一种在运行时生成本机可执行代码并执行的程序或库，通常是为了在保持平台独立性的同时实现良好的性能。


Programs that use JIT compilation are normally difficult to debug because portions of their code are generated at runtime, instead of being loaded from object files, which is where [GDB] at runtime.

> 程序使用JIT编译通常很难调试，因为它们的代码的部分是在运行时生成的，而不是从对象文件加载，这是[GDB]在运行时处理的。


If you are using [GDB] to debug a program that uses this interface, then it should work transparently so long as you have not stripped the binary. If you are developing a JIT compiler, then the interface is documented in the rest of this chapter. At this time, the only known client of this interface is the LLVM JIT.

> 如果你使用GDB来调试使用这个接口的程序，那么只要你没有剥离二进制文件，它就应该能透明地工作。如果你正在开发一个JIT编译器，那么本章剩下的部分就会对这个接口进行文档化。目前，这个接口唯一已知的客户端是LLVM JIT。


Broadly speaking, the JIT interface mirrors the dynamic loader interface. The JIT compiler communicates with [GDB] attaches, it reads a linked list of symbol files from the global variable to find existing code, and puts a breakpoint in the function so that it can find out about additional code.

> 总的来说，JIT接口反映了动态加载器接口。JIT编译器与[GDB]附加，它从全局变量中读取符号文件的链表以查找现有代码，并在函数中放置断点，以便了解其他代码。

---


• [Declarations](Declarations.html#Declarations):                          Relevant C struct declarations

> • [声明](Declarations.html#Declarations)：相关的C结构声明

• [Registering Code](Registering-Code.html#Registering-Code):              Steps to register code

> • [注册码](Registering-Code.html#Registering-Code):              注册码步骤

• [Unregistering Code](Unregistering-Code.html#Unregistering-Code):        Steps to unregister code

> • [取消注册代码](Unregistering-Code.html#Unregistering-Code):   步骤取消注册代码

• [Custom Debug Info](Custom-Debug-Info.html#Custom-Debug-Info):           Emit debug information in a custom format

> • [自定义调试信息](Custom-Debug-Info.html#Custom-Debug-Info): 以自定义格式发出调试信息

---

---

::: header
Next: [In-Process Agent](In_002dProcess-Agent.html#In_002dProcess-Agent)]
:::
