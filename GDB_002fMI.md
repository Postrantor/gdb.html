---
tip: translate by openai@2023-06-23 22:34:13
...
---
description: GDB/MI (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI (Debugging with GDB)
---
::: header
Next: [Annotations](Annotations.html#Annotations)]
:::

---

## 27 The [GDB/MI]

---


• [GDB/MI General Design](GDB_002fMI-General-Design.html#GDB_002fMI-General-Design):                                         

> • [GDB/MI设计概述](GDB_002fMI-General-Design.html#GDB_002fMI-General-Design)：

• [GDB/MI Command Syntax](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax):                                         

> • [GDB/MI 命令语法](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax):

• [GDB/MI Compatibility with CLI](GDB_002fMI-Compatibility-with-CLI.html#GDB_002fMI-Compatibility-with-CLI):                 

> • [GDB/MI 与 CLI 的兼容性](GDB_002fMI-Compatibility-with-CLI.html#GDB_002fMI-Compatibility-with-CLI):

• [GDB/MI Development and Front Ends](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends):     

> • [GDB / MI 开发和前端](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends):

• [GDB/MI Output Records](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records):                                         

> • [GDB / MI 输出记录](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records):

• [GDB/MI Simple Examples](GDB_002fMI-Simple-Examples.html#GDB_002fMI-Simple-Examples):                                      

> • [GDB/MI 简单示例](GDB_002fMI-Simple-Examples.html#GDB_002fMI-Simple-Examples):

• [GDB/MI Command Description Format](GDB_002fMI-Command-Description-Format.html#GDB_002fMI-Command-Description-Format):     

> • [GDB/MI 命令描述格式](GDB_002fMI-Command-Description-Format.html#GDB_002fMI-Command-Description-Format):

• [GDB/MI Breakpoint Commands](GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands):                          

> • [GDB/MI断点命令](GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands):

• [GDB/MI Catchpoint Commands](GDB_002fMI-Catchpoint-Commands.html#GDB_002fMI-Catchpoint-Commands):                          

> • [GDB/MI捕获点命令](GDB_002fMI-Catchpoint-Commands.html#GDB_002fMI-Catchpoint-Commands):

• [GDB/MI Program Context](GDB_002fMI-Program-Context.html#GDB_002fMI-Program-Context):                                                     

> • [GDB/MI 程序上下文](GDB_002fMI-Program-Context.html#GDB_002fMI-Program-Context):

• [GDB/MI Thread Commands](GDB_002fMI-Thread-Commands.html#GDB_002fMI-Thread-Commands):                                                     

> • [GDB/MI 线程命令](GDB_002fMI-Thread-Commands.html#GDB_002fMI-Thread-Commands):

• [GDB/MI Ada Tasking Commands](GDB_002fMI-Ada-Tasking-Commands.html#GDB_002fMI-Ada-Tasking-Commands):                                      

> • [GDB/MI Ada任务命令](GDB_002fMI-Ada-Tasking-Commands.html#GDB_002fMI-Ada-Tasking-Commands):

• [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution):                                               

> • [GDB/MI 程序执行](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution):

• [GDB/MI Stack Manipulation](GDB_002fMI-Stack-Manipulation.html#GDB_002fMI-Stack-Manipulation):                                            

> • [GDB/MI 栈操作](GDB_002fMI-Stack-Manipulation.html#GDB_002fMI-Stack-Manipulation): 提取

• [GDB/MI Variable Objects](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects):                                                  

> • [GDB / MI变量对象](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects):

• [GDB/MI Data Manipulation](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation):                                               

> • [GDB/MI 数据操作](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation):

• [GDB/MI Tracepoint Commands](GDB_002fMI-Tracepoint-Commands.html#GDB_002fMI-Tracepoint-Commands):                                         

> • [GDB/MI 跟踪点命令](GDB_002fMI-Tracepoint-Commands.html#GDB_002fMI-Tracepoint-Commands):

• [GDB/MI Symbol Query](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query):                                                              

> • [GDB / MI符号查询](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query):

• [GDB/MI File Commands](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands):                                                           

> • [GDB/MI 文件命令](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands):

• [GDB/MI Target Manipulation](GDB_002fMI-Target-Manipulation.html#GDB_002fMI-Target-Manipulation):                                         

> • [GDB/MI 目标操作](GDB_002fMI-Target-Manipulation.html#GDB_002fMI-Target-Manipulation):

• [GDB/MI File Transfer Commands](GDB_002fMI-File-Transfer-Commands.html#GDB_002fMI-File-Transfer-Commands):                                

> • [GDB/MI 文件传输命令](GDB_002fMI-File-Transfer-Commands.html#GDB_002fMI-File-Transfer-Commands):

• [GDB/MI Ada Exceptions Commands](GDB_002fMI-Ada-Exceptions-Commands.html#GDB_002fMI-Ada-Exceptions-Commands):                             

> • [GDB / MI Ada异常命令](GDB_002fMI-Ada-Exceptions-Commands.html#GDB_002fMI-Ada-Exceptions-Commands):

• [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands):                                                  

> • [GDB/MI 支持命令](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands):

• [GDB/MI Miscellaneous Commands](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands):                                

> • [GDB/MI杂项命令](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands):

---

### Function and Purpose


[GDB/MI] command line option (see [Mode Options](Mode-Options.html#Mode-Options)). It is specifically intended to support the development of systems which use the debugger as just one small component of a larger system.

> [GDB/MI] 命令行选项（见[模式选项](Mode-Options.html#Mode-Options)），专门用于支持开发将调试器作为整个系统的一个小组件的系统。


This chapter is a specification of the [GDB/MI] interface. It is written in the form of a reference manual.

> 本章是[GDB/MI]接口的规范。它以参考手册的形式编写。


Note that [GDB/MI] Development and Front Ends](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends)).

> 注意[GDB/MI]开发和前端（GDB / MI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends））。

### Notation and Terminology

This chapter uses the following notation:

- `|` separates two alternatives.
- `[ something ]` indicates that `something` is optional: it may or may not be given.
- `( group )*` means that `group` inside the parentheses may repeat zero or more times.
- `( group )+` means that `group` inside the parentheses may repeat one or more times.
- `( group )` means that `group` inside the parentheses occurs exactly once.
- `"string"` means a literal `string`.

---


• [GDB/MI General Design](GDB_002fMI-General-Design.html#GDB_002fMI-General-Design):                                         

> • [GDB/MI 设计总体](GDB_002fMI-General-Design.html#GDB_002fMI-General-Design):

• [GDB/MI Command Syntax](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax):                                         

> • [GDB/MI 命令语法](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax):

• [GDB/MI Compatibility with CLI](GDB_002fMI-Compatibility-with-CLI.html#GDB_002fMI-Compatibility-with-CLI):                 

> • [GDB/MI 与 CLI 的兼容性](GDB_002fMI-Compatibility-with-CLI.html#GDB_002fMI-Compatibility-with-CLI):

• [GDB/MI Development and Front Ends](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends):     

> • [GDB/MI 开发和前端](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends):

• [GDB/MI Output Records](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records):                                         

> • [GDB / MI 输出记录](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records):

• [GDB/MI Simple Examples](GDB_002fMI-Simple-Examples.html#GDB_002fMI-Simple-Examples):                                      

> • [GDB / MI简单示例](GDB_002fMI-Simple-Examples.html#GDB_002fMI-Simple-Examples):

• [GDB/MI Command Description Format](GDB_002fMI-Command-Description-Format.html#GDB_002fMI-Command-Description-Format):     

> • [GDB/MI 命令描述格式](GDB_002fMI-Command-Description-Format.html#GDB_002fMI-Command-Description-Format):

• [GDB/MI Breakpoint Commands](GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands):                          

> • [GDB/MI断点命令](GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands):

• [GDB/MI Catchpoint Commands](GDB_002fMI-Catchpoint-Commands.html#GDB_002fMI-Catchpoint-Commands):                          

> • [GDB/MI 捕获点命令](GDB_002fMI-Catchpoint-Commands.html#GDB_002fMI-Catchpoint-Commands):

• [GDB/MI Program Context](GDB_002fMI-Program-Context.html#GDB_002fMI-Program-Context):                                                     

> • [GDB/MI 程序上下文](GDB_002fMI-Program-Context.html#GDB_002fMI-Program-Context)：

• [GDB/MI Thread Commands](GDB_002fMI-Thread-Commands.html#GDB_002fMI-Thread-Commands):                                                     

> • [GDB/MI 线程命令](GDB_002fMI-Thread-Commands.html#GDB_002fMI-Thread-Commands):

• [GDB/MI Ada Tasking Commands](GDB_002fMI-Ada-Tasking-Commands.html#GDB_002fMI-Ada-Tasking-Commands):                                      

> • [GDB/MI Ada 任务命令](GDB_002fMI-Ada-Tasking-Commands.html#GDB_002fMI-Ada-Tasking-Commands):

• [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution):                                               

> • [GDB/MI程序执行](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution)：

• [GDB/MI Stack Manipulation](GDB_002fMI-Stack-Manipulation.html#GDB_002fMI-Stack-Manipulation):                                            

> • [GDB/MI 栈操作](GDB_002fMI-Stack-Manipulation.html#GDB_002fMI-Stack-Manipulation): 提取

• [GDB/MI Variable Objects](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects):                                                  

> • [GDB/MI 变量对象](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects):

• [GDB/MI Data Manipulation](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation):                                               

> • [GDB/MI 数据操作](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation):

• [GDB/MI Tracepoint Commands](GDB_002fMI-Tracepoint-Commands.html#GDB_002fMI-Tracepoint-Commands):                                         

> • [GDB/MI 跟踪点命令](GDB_002fMI-Tracepoint-Commands.html#GDB_002fMI-Tracepoint-Commands):

• [GDB/MI Symbol Query](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query):                                                              

> • [GDB/MI 符号查询](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query):

• [GDB/MI File Commands](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands):                                                           

> • [GDB/MI 文件命令](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands):

• [GDB/MI Target Manipulation](GDB_002fMI-Target-Manipulation.html#GDB_002fMI-Target-Manipulation):                                         

> • [GDB / MI目标操纵](GDB_002fMI-Target-Manipulation.html#GDB_002fMI-Target-Manipulation):

• [GDB/MI File Transfer Commands](GDB_002fMI-File-Transfer-Commands.html#GDB_002fMI-File-Transfer-Commands):                                

> • [GDB/MI 文件传输命令](GDB_002fMI-File-Transfer-Commands.html#GDB_002fMI-File-Transfer-Commands):

• [GDB/MI Ada Exceptions Commands](GDB_002fMI-Ada-Exceptions-Commands.html#GDB_002fMI-Ada-Exceptions-Commands):                             

> • [GDB/MI Ada 异常命令](GDB_002fMI-Ada-Exceptions-Commands.html#GDB_002fMI-Ada-Exceptions-Commands):

• [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands):                                                  

> • [GDB/MI 支持命令](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands):

• [GDB/MI Miscellaneous Commands](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands):                                

> • [GDB/MI杂项命令](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands):

---

---

::: header
Next: [Annotations](Annotations.html#Annotations)]
:::
