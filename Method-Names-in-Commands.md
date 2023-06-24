---
tip: translate by openai@2023-06-24 10:38:51
...
---
description: Method Names in Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Method Names in Commands (Debugging with GDB)
lang: en
resource-type: document
title: Method Names in Commands (Debugging with GDB)
---
::: header
Next: [The Print Command with Objective-C](The-Print-Command-with-Objective_002dC.html#The-Print-Command-with-Objective_002dC)]
:::

---

#### 15.4.4.1 Method Names in Commands


The following commands have been extended to accept Objective-C method names as line specifications:

> 以下命令已扩展以接受Objective-C方法名作为行规范：

- `clear`
- `break`
- `info line`
- `jump`
- `list`

A fully qualified Objective-C method name is specified as

::: smallexample

```bash
-[Class methodName]
```

:::


where the minus sign is used to indicate an instance method and a plus sign (not shown) is used to indicate a class method. The class name `Class` are enclosed in brackets, similar to the way messages are specified in Objective-C source code. For example, to set a breakpoint at the `create` instance method of class `Fruit` in the program currently being debugged, enter:

> 在程序调试时，使用减号表示实例方法，而使用加号（未显示）表示类方法。类名称（Class）用括号括起来，类似于Objective-C源代码中指定消息的方式。例如，要在程序当前调试中的类`Fruit`的`create`实例方法处设置断点，请输入：

::: smallexample

```bash
break -[Fruit create]
```

:::

To list ten program lines around the `initialize` class method, enter:

::: smallexample

```bash
list +[NSText initialize]
```

:::


In the current version of [GDB], the plus or minus sign will be optional, but you can use it to narrow the search. It is also possible to specify just a method name:

> 在当前版本的GDB中，加号或减号是可选的，但你可以使用它来缩小搜索范围。也可以只指定一个方法名称：

::: smallexample

```bash
break create
```

:::


You must specify the complete method name, including any colons. If your program's source files contain more than one `create` method, you'll be presented with a numbered list of classes that implement that method. Indicate your choice by number, or type '`0`' to exit if none apply.

> 你必须指定完整的方法名，包括任何冒号。如果你程序的源文件包含多个`create`方法，你将会看到一个带有序号的实现该方法的类列表。通过序号指示你的选择，或者输入'`0`'退出，如果没有适用的。


As another example, to clear a breakpoint established at the `makeKeyAndOrderFront:` method of the `NSWindow` class, enter:

> 例如要清除在NSWindow类的makeKeyAndOrderFront:方法上设置的断点，请输入：

::: smallexample

```bash
clear -[NSWindow makeKeyAndOrderFront:]
```

:::

---

::: header
Next: [The Print Command with Objective-C](The-Print-Command-with-Objective_002dC.html#The-Print-Command-with-Objective_002dC)]
:::
