---
tip: translate by openai@2023-06-23 21:19:58
...
---
description: Frame Decorator API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frame Decorator API (Debugging with GDB)
lang: en
resource-type: document
title: Frame Decorator API (Debugging with GDB)
---
::: header
Next: [Writing a Frame Filter](Writing-a-Frame-Filter.html#Writing-a-Frame-Filter)]
:::

---

#### 23.3.2.10 Decorating Frames


Frame decorators are sister objects to frame filters (see [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API)). Frame decorators are applied by a frame filter and can only be used in conjunction with frame filters.

> 框架装饰器是框架过滤器的姊妹对象（参见[框架过滤器 API](Frame-Filter-API.html#Frame-Filter-API))。框架装饰器由框架过滤器应用，只能与框架过滤器一起使用。


The purpose of a frame decorator is to customize the printed content of each `gdb.Frame` in commands where frame filters are executed. This concept is called decorating a frame. Frame decorators decorate a `gdb.Frame` with Python code contained within each API call. This separates the actual data contained in a `gdb.Frame` from the decorated data produced by a frame decorator. This abstraction is necessary to maintain integrity of the data contained in each `gdb.Frame`.

> 目的Frame Decorator是为了自定义每个gdb.Frame中的打印内容，在执行帧过滤器时。这个概念称为装饰帧。帧装饰器使用每个API调用中包含的Python代码装饰gdb.Frame。这将gdb.Frame中实际包含的数据与由帧装饰器产生的装饰数据分开。这种抽象是必要的，以维护每个gdb.Frame中包含的数据的完整性。

Frame decorators have a mandatory interface, defined below.


[GDB] already contains a frame decorator called `FrameDecorator`. This contains substantial amounts of boilerplate code to decorate the content of a `gdb.Frame`. It is recommended that other frame decorators inherit and extend this object, and only to override the methods needed.

> GDB已经包含一个名为FrameDecorator的框架装饰器。它包含大量的样板代码来装饰gdb.Frame的内容。建议其他框架装饰器继承并扩展此对象，并只覆盖所需的方法。

`FrameDecorator` is defined in the Python module `gdb.FrameDecorator`, so your code can import it like:

::: smallexample

```bash
from gdb.FrameDecorator import FrameDecorator
```

:::

Function: **FrameDecorator.elided** *(self)*


:   The `elided` method groups frames together in a hierarchical system. An example would be an interpreter, where multiple low-level frames make up a single call in the interpreted language. In this example, the frame filter would elide the low-level frames and present a single high-level frame, representing the call in the interpreted language, to the user.

> `elided`方法将帧组织到层次系统中。例如，解释器，其中多个低级帧构成解释语言中的单个调用。在这个例子中，帧过滤器将省略低级帧，并向用户呈现单个高级帧，表示解释语言中的调用。

```
The `elided` function must return an iterable and this iterable must contain the frames that are being elided wrapped in a suitable frame decorator. If no frames are being elided this function may return an empty iterable, or `None`. Elided frames are indented from normal frames in a `CLI` backtrace, or in the case of [GDB/MI], are placed in the `children` field of the eliding frame.

It is the frame filter's task to also filter out the elided frames from the source iterator. This will avoid printing the frame twice.
```

```
<!-- -->
```

Function: **FrameDecorator.function** *(self)*


:   This method returns the name of the function in the frame that is to be printed.

> 此方法返回要打印的帧中的函数名称。

```
This method must return a Python string describing the function, or `None`.

If this function returns `None`, [GDB] will not print any data for this field.
```

```
<!-- -->
```

Function: **FrameDecorator.address** *(self)*

:   This method returns the address of the frame that is to be printed.

```
This method must return a Python numeric integer type of sufficient size to describe the address of the frame, or `None`.

If this function returns a `None`, [GDB] will not print any data for this field.
```

```
<!-- -->
```

Function: **FrameDecorator.filename** *(self)*

:   This method returns the filename and path associated with this frame.

```
This method must return a Python string containing the filename and the path to the object file backing the frame, or `None`.

If this function returns a `None`, [GDB] will not print any data for this field.
```

```
<!-- -->
```

Function: **FrameDecorator.line** *(self):*


:   This method returns the line number associated with the current position within the function addressed by this frame.

> 此方法返回与此帧所指向的函数中当前位置相关联的行号。

```
This method must return a Python integer type, or `None`.

If this function returns a `None`, [GDB] will not print any data for this field.
```

```
<!-- -->
```

Function: **FrameDecorator.frame_args** *(self)*

:

```
This method must return an iterable, or `None`. Returning an empty iterable, or `None` means frame arguments will not be printed for this frame. This iterable must contain objects that implement two methods, described here.

This object must implement a `symbol` method which takes a single `self` parameter and must return a `gdb.Symbol` (see [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python)), or a Python string. The object must also implement a `value` method which takes a single `self` parameter and must return a `gdb.Value` (see [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)), a Python value, or `None`. If the `value` method returns `None`, and the `argument` method returns a `gdb.Symbol`, [GDB] will look-up and print the value of the `gdb.Symbol` automatically.

A brief example:

::: smallexample
``` smallexample
class SymValueWrapper():

    def __init__(self, symbol, value):
        self.sym = symbol
        self.val = value

    def value(self):
        return self.val

    def symbol(self):
        return self.sym

class SomeFrameDecorator()
...
...
    def frame_args(self):
        args = 
        try:
            block = self.inferior_frame.block()
        except:
            return None

        # Iterate over all symbols in a block.  Only add
        # symbols that are arguments.
        for sym in block:
            if not sym.is_argument:
                continue
            args.append(SymValueWrapper(sym,None))

        # Add example synthetic argument.
        args.append(SymValueWrapper(``foo'', 42))

        return args
```

:::

```

```

<!-- -->

```

Function: **FrameDecorator.frame_locals** *(self)*


:   This method must return an iterable or `None`. Returning an empty iterable, or `None` means frame local arguments will not be printed for this frame.

> 此方法必须返回一个可迭代对象或`None`。返回一个空的可迭代对象或`None`意味着此帧不会打印本地参数。

```

The object interface, the description of the various strategies for reading frame locals, and the example are largely similar to those described in the `frame_args` function, (see [The frame filter frame_args function](#frame_005fargs)). Below is a modified example:

::: smallexample

```bash
class SomeFrameDecorator()
...
...
    def frame_locals(self):
        vars = 
        try:
            block = self.inferior_frame.block()
        except:
            return None

        # Iterate over all symbols in a block.  Add all
        # symbols, except arguments.
        for sym in block:
            if sym.is_argument:
                continue
            vars.append(SymValueWrapper(sym,None))

        # Add an example of a synthetic local variable.
        vars.append(SymValueWrapper(``bar'', 99))

        return vars
```

:::

```

```

<!-- -->

```

Function: **FrameDecorator.inferior_frame** *(self):*


:   This method must return the underlying `gdb.Frame` that this frame decorator is decorating. [GDB] requires the underlying frame for internal frame information to determine how to print certain values when printing a frame.

> 此方法必须返回此帧装饰器装饰的基础`gdb.Frame`。[GDB]需要基础帧以获取内部帧信息，以确定在打印帧时如何打印某些值。

---

::: header
Next: [Writing a Frame Filter](Writing-a-Frame-Filter.html#Writing-a-Frame-Filter)]
:::
```
