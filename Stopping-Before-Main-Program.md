---
tip: translate by openai@2023-06-24 03:22:03
...
---
description: Stopping Before Main Program (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Stopping Before Main Program (Debugging with GDB)
lang: en
resource-type: document
title: Stopping Before Main Program (Debugging with GDB)
---
::: header
Next: [Ada Exceptions](Ada-Exceptions.html#Ada-Exceptions)]
:::

---

#### 15.4.10.5 Stopping at the Very Beginning


It is sometimes necessary to debug the program during elaboration, and before reaching the main procedure. As defined in the Ada Reference Manual, the elaboration code is invoked from a procedure called `adainit`. To run your program up to the beginning of elaboration, simply use the following two commands: `tbreak adainit` and `run`.

> 有时在编写过程中需要调试程序，在到达主程序之前。根据Ada参考手册的定义，编写代码是从一个叫做“adainit”的程序中调用的。要运行程序到编写开始，只需使用以下两个命令：“tbreak adainit”和“run”。
