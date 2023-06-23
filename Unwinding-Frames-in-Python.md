---
tip: translate by openai@2023-06-23 15:16:33
...
---
description: Unwinding Frames in Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Unwinding Frames in Python (Debugging with GDB)
lang: en
resource-type: document
title: Unwinding Frames in Python (Debugging with GDB)
------------------------------------------------------

::: header
Next: [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python)]
:::

---

#### 23.3.2.12 Unwinding Frames in Python

In [GDB] mantains a list of the unwinders and calls each unwinder's sniffer in turn until it finds the one that recognizes the current frame. There is an API to register an unwinder.

> 在 GDB 中，维护一个解开器列表，并依次调用每个解开器的嗅探器，直到找到识别当前帧的解开器。有一个 API 来注册解开器。

The unwinders that come with [GDB] unwinders. You can write Python code that can handle such custom frames.

> 搭配[GDB]的解开器。你可以编写 Python 代码来处理这类自定义框架。

You implement a frame unwinder in Python as a class with which has two attributes, `name` and `enabled`, with obvious meanings, and a single method `__call__`, which examines a given frame and returns an object (an instance of `gdb.UnwindInfo class)` describing it. If an unwinder does not recognize a frame, it should return `None`. The code in [GDB] core asks for them.

> 你用 Python 实现了一个类来构建一个帧拆解器，它有两个属性 `name` 和 `enabled`，意义显而易见，还有一个方法 `__call__`，它检查给定的帧并返回一个对象（`gdb.UnwindInfo` 类的实例）来描述它。如果拆解器无法识别帧，它应该返回 `None`。[GDB]核心中的代码要求它们。

An unwinder should do as little work as possible. Some otherwise innocuous operations can cause problems (even crashes, as this code is not not well-hardened yet). For example, making an inferior call from an unwinder is unadvisable, as an inferior call will reset [GDB]'s stack unwinding process, potentially causing re-entrant unwinding.

> 一个解开器应该尽可能少的做工作。一些看似无害的操作可能会引起问题（甚至崩溃，因为这段代码尚未经过坚固的保护）。例如，从解开器中进行下级调用是不可取的，因为下级调用会重置 GDB 的堆栈解开过程，可能会导致重入式解开。

#### Unwinder Input

An object passed to an unwinder (a `gdb.PendingFrame` instance) provides a method to read frame's registers:

> 一个传递给解开器（一个 `gdb.PendingFrame` 实例）的对象提供了一种读取帧寄存器的方法：

Function: **PendingFrame.read_register** *(register)*

> 功能：**PendingFrame.read_register**（寄存器）

:   This method returns the contents of `register` does not name a register for the current architecture, this method will throw an exception.

> 这个方法返回 `register` 的内容，如果没有为当前架构命名一个寄存器，这个方法将抛出一个异常。

```
Note that this method will always return a `gdb.Value` for a valid register name. This does not mean that the value will be valid. For example, you may request a register that an earlier unwinder could not unwind---the value will be unavailable. Instead, the `gdb.Value` returned from this method will be lazy; that is, its underlying bits will not be fetched until it is first used. So, attempting to use such a value will cause an exception at the point of use.

The type of the returned `gdb.Value` depends on the register and the architecture. It is common for registers to have a scalar type, like `long long`; but many other types are possible, such as pointer, pointer-to-function, floating point or vector types.
```

It also provides a factory method to create a `gdb.UnwindInfo` instance to be returned to [GDB]:

> 它还提供了一个工厂方法来创建一个 `gdb.UnwindInfo` 实例，以供[GDB]返回。

Function: **PendingFrame.create_unwind_info** *(frame_id)*

> 功能：**PendingFrame.create_unwind_info**（帧 ID）

:   Returns a new `gdb.UnwindInfo` instance identified by given `frame_id`:

> 返回一个通过给定的 `frame_id` 标识的新的 `gdb.UnwindInfo` 实例

```
`sp, pc`

:   The frame is identified by the given stack address and PC. The stack address must be chosen so that it is constant throughout the lifetime of the frame, so a typical choice is the value of the stack pointer at the start of the function---in the DWARF standard, this would be the "Call Frame Address".

    This is the most common case by far. The other cases are documented for completeness but are only useful in specialized situations.

`sp, pc, special`

:   The frame is identified by the stack address, the PC, and a "special" address. The special address is used on architectures that can have frames that do not change the stack, but which are still distinct, for example the IA-64, which has a second stack for registers. Both `sp` must be constant throughout the lifetime of the frame.

`sp`

:   The frame is identified by the stack address only. Any other stack frame with a matching `sp` will be considered to match this frame. Inside gdb, this is called a "wild frame". You will never need this.

Each attribute value should either be an instance of `gdb.Value` or an integer.

A helper class is provided in the `gdb.unwinder` module that can be used to represent a frame-id (see [gdb.unwinder.FrameId](#gdb_002eunwinder_002eFrameId)).
```

```

```

Function: **PendingFrame.architecture** *()*

> 功能：**PendingFrame.architecture** *（）*

:   Return the `gdb.Architecture` (see [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python)) for this `gdb.PendingFrame`. This represents the architecture of the particular frame being unwound.

> 返回此 `gdb.PendingFrame` 的 `gdb.Architecture`（参见 [Python 中的架构](Architectures-In-Python.html#Architectures-In-Python)）。这代表正在展开的特定帧的架构。

```

```

Function: **PendingFrame.level** *()*

> 功能：**PendingFrame.level** *（）*

:   Return an integer, the stack frame level for this frame. See [Stack Frames](Frames.html#Frames).

> 返回一个整数，这个帧的堆栈帧级别。参见[堆栈帧](Frames.html#Frames)。

```

```

Function: **PendingFrame.name** *()*

> 功能：**PendingFrame.name** *（）*

:   Returns the function name of this pending frame, or `None` if it can't be obtained.

> 返回此挂起帧的函数名称，如果无法获得，则返回 `None`。

```

```

Function: **PendingFrame.is_valid** *()*

> 功能：**PendingFrame.is_valid** *（）*

:   Returns true if the `gdb.PendingFrame` object is valid, false if not. A pending frame object becomes invalid when the call to the unwinder, for which the pending frame was created, returns.

> 返回 true 如果 `gdb.PendingFrame` 对象有效，如果无效则返回 false。当调用解开器（为其创建了待处理帧）返回时，待处理帧对象将变得无效。

```
All `gdb.PendingFrame` methods, except this one, will raise an exception if the pending frame object is invalid at the time the method is called.
```

```

```

Function: **PendingFrame.pc** *()*

> 功能：**PendingFrame.pc** *（）*

:   Returns the pending frame's resume address.

> 返回挂起帧的恢复地址。

```

```

Function: **PendingFrame.block** *()*

> 功能：**PendingFrame.block** *（）*

:   Return the pending frame's code block (see [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python)). If the frame does not have a block -- for example, if there is no debugging information for the code in question -- then this will raise a `RuntimeError` exception.

> 返回待处理帧的代码块（参见 [Python 中的块](Blocks-In-Python.html#Blocks-In-Python)）。如果帧没有块--例如，如果没有相关代码的调试信息--那么这将引发 `RuntimeError` 异常。

```

```

Function: **PendingFrame.function** *()*

> 函数：**PendingFrame.function** *（）*

:   Return the symbol for the function corresponding to this pending frame. See [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python).

> 返回与此待处理框架对应的函数的符号。请参阅 [Python 中的符号](Symbols-In-Python.html#Symbols-In-Python)。

```

```

Function: **PendingFrame.find_sal** *()*

> 功能：**PendingFrame.find_sal** *（）*

:   Return the pending frame's symtab and line object (see [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)).

> 返回挂起帧的符号表和行对象（参见 [Python 中的符号表](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)）。

```

```

Function: **PendingFrame.language** *()*

> 功能：**PendingFrame.language**（）

:   Return the language of this frame, as a string, or None.

> 返回此框架的语言，作为字符串，或无。

#### Unwinder Output: UnwindInfo

Use `PendingFrame.create_unwind_info` method described above to create a `gdb.UnwindInfo` instance. Use the following method to specify caller registers that have been saved in this frame:

> 使用上面描述的 `PendingFrame.create_unwind_info` 方法创建一个 `gdb.UnwindInfo` 实例。使用以下方法指定在此帧中已保存的调用方寄存器：

Function: **gdb.UnwindInfo.add_saved_register** *(register, value)*

> 功能：**gdb.UnwindInfo.add_saved_register**（寄存器，值）

:   `register` is a register value (a `gdb.Value` object).

> 注册是一个注册值（一个 gdb.Value 对象）。

#### The `gdb.unwinder` Module

[GDB] comes with a `gdb.unwinder` module which contains the following classes:

> [GDB] 包含一个 `gdb.unwinder` 模块，其中包含以下类：

class: **gdb.unwinder.Unwinder**

> 类：**gdb.unwinder.Unwinder**

:   The `Unwinder` class is a base class from which user created unwinders can derive, though it is not required that unwinders derive from this class, so long as any user created unwinder has the required `name` and `enabled` attributes.

> 类 `Unwinder` 是一个基类，用户可以从中派生出解开器，但不要求解开器必须从这个类派生，只要用户创建的解开器具有所需的 `name` 和 `enabled` 属性即可。

```
Function: **gdb.unwinder.Unwinder.__init__(name)**

:   The `name` commands (see [Managing Registered Unwinders](#Managing-Registered-Unwinders)).

Variable: **gdb.unwinder.name**

:   A read-only attribute which is a string, the name of this unwinder.

Variable: **gdb.unwinder.enabled**

:   A modifiable attribute containing a boolean; when `True`, the unwinder is enabled, and will be used by [GDB]. When `False`, the unwinder has been disabled, and will not be used.
```

class: **gdb.unwinder.FrameId**

> 类：**gdb.unwinder.FrameId**

:   This is a class suitable for being used as the frame-id when calling `gdb.PendingFrame.create_unwind_info`. It is not required to use this class, any class with the required attribute (see [gdb.PendingFrame.create_unwind_info](#gdb_002ePendingFrame_002ecreate_005funwind_005finfo)) will be accepted, but in most cases this class will be sufficient.

> 这是一个适合用作调用 `gdb.PendingFrame.create_unwind_info` 时的 frame-id 的类。不需要使用这个类，任何具有所需属性（请参阅 [gdb.PendingFrame.create_unwind_info](#gdb_002ePendingFrame_002ecreate_005funwind_005finfo)）的类都将被接受，但在大多数情况下，这个类将足够。

```
`gdb.unwinder.FrameId` has the following method:

Function: **gdb.unwinder.FrameId.__init__(sp,** *pc, special = `None`)*

:   The `sp` arguments are required and should be either a `gdb.Value` object, or an integer.

    The `special` argument is optional; if specified, it should be a `gdb.Value` object, or an integer.

`gdb.unwinder.FrameId` has the following read-only attributes:

Variable: **gdb.unwinder.sp**

:   The `sp` value passed to the constructor.

Variable: **gdb.unwinder.pc**

:   The `pc` value passed to the constructor.

Variable: **gdb.unwinder.special**

:   The `special` value passed to the constructor, or `None` if no such value was passed.
```

#### Registering an Unwinder

Object files and program spaces can have unwinders registered with them. In addition, you can register unwinders globally.

> 可以为对象文件和程序空间注册解开器。此外，您还可以全局注册解开器。

The `gdb.unwinders` module provides the function to register an unwinder:

> `gdb.unwinders` 模块提供注册解开器的功能。

Function: **gdb.unwinder.register_unwinder** *(locus, unwinder, replace=False)*

> 功能：**gdb.unwinder.register_unwinder** *（位置，解开器，替换=否*

:   `locus` is `True`, in which case the old unwinder is deleted and the new unwinder is registered in its place.

> 如果 `locus` 为 `真`，则删除旧的解开器，并将新的解开器注册到其位置。

```
[GDB].
```

#### Unwinder Skeleton Code

Here is an example of how to structure a user created unwinder:

> 这里是一个用户创建解开器的结构示例：

::: smallexample

```bash
from gdb.unwinder import Unwinder, FrameId

class MyUnwinder(Unwinder):
    def __init__(self):
        super().__init___("MyUnwinder_Name")

    def __call__(self, pending_frame):
        if not <we recognize frame>:
            return None

        # Create a FrameID.  Usually the frame is identified by a
        # stack pointer and the function address.
        sp = ... compute a stack address ...
        pc = ... compute function address ...
        unwind_info = pending_frame.create_unwind_info(FrameId(sp, pc))

        # Find the values of the registers in the caller's frame and
        # save them in the result:
        unwind_info.add_saved_register(<register-number>, <register-value>)
        ....

        # Return the result:
        return unwind_info

gdb.unwinder.register_unwinder(<locus>, MyUnwinder(), <replace>)
```

:::

#### Managing Registered Unwinders

[GDB] defines 3 commands to manage registered unwinders. These are:

> [GDB]定义了三个命令来管理已注册的卸载器。它们是：

`info unwinder [ locus [ name-regexp ] ]`

:   Lists all registered unwinders. Arguments `locus` are both optional and can be used to filter which unwinders are listed.

> 列出所有已注册的卸载程序。参数 `locus` 是可选的，可用于筛选要列出的卸载程序。

```
The `locus`, or the name of an object file. Only unwinders registered for the specified locus will be listed.

The `name-regexp` in quotes.
```

`disable unwinder [ locus [ name-regexp ] ]`

:   The `locus` above, but instead of listing the matching unwinders, all of the matching unwinders are disabled. The `enabled` field of each matching unwinder is set to `False`.

> 在上面的 `locus` 中，所有匹配的 unwinder 都被禁用。每个匹配的 unwinder 的 `enabled` 字段被设置为 `False`。

`enable unwinder [ locus [ name-regexp ] ]`

:   The `locus` above, but instead of listing the matching unwinders, all of the matching unwinders are enabled. The `enabled` field of each matching unwinder is set to `True`.

> 上面的 `locus`，但不是列出匹配的卸载程序，而是启用所有匹配的卸载程序。每个匹配的卸载程序的 `enabled` 字段设置为 `True`。

---

::: header
Next: [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python)]
:::
