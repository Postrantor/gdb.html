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

::: smallexample

```bash
break create
```

:::

You must specify the complete method name, including any colons. If your program's source files contain more than one `create` method, you'll be presented with a numbered list of classes that implement that method. Indicate your choice by number, or type '`0`' to exit if none apply.

As another example, to clear a breakpoint established at the `makeKeyAndOrderFront:` method of the `NSWindow` class, enter:

::: smallexample

```bash
clear -[NSWindow makeKeyAndOrderFront:]
```

:::

---

::: header
Next: [The Print Command with Objective-C](The-Print-Command-with-Objective_002dC.html#The-Print-Command-with-Objective_002dC)]
:::
