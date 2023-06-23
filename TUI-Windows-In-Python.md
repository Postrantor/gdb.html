---
tip: translate by openai@2023-06-23 14:56:17
...
---
description: TUI Windows In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: TUI Windows In Python (Debugging with GDB)
lang: en
resource-type: document
title: TUI Windows In Python (Debugging with GDB)
---
::: header
Next: [Disassembly In Python](Disassembly-In-Python.html#Disassembly-In-Python)]
:::

---

#### 23.3.2.37 Implementing new TUI windows


New TUI (see [TUI](TUI.html#TUI)) windows can be implemented in Python.

> 新的TUI（参见[TUI](TUI.html#TUI)）窗口可以用Python实现。


Function: **gdb.register_window_type** *(name, factory)*

> 功能：**gdb.register_window_type** *（名称，工厂）*


:   Because TUI windows are created and destroyed depending on the layout the user chooses, new window types are implemented by registering a factory function with [GDB].

> 由于TUI窗口取决于用户选择的布局而创建和销毁，因此通过在[GDB]中注册工厂函数来实现新的窗口类型。

```
`name` should match the regular expression `[a-zA-Z][-_.a-zA-Z0-9]*`, it is an error to try and create a window with an invalid name.

`function` is a factory function that is called to create the TUI window. This is called with a single argument of type `gdb.TuiWindow`, described below. It should return an object that implements the TUI window protocol, also described below.
```


As mentioned above, when a factory function is called, it is passed an object of type `gdb.TuiWindow`. This object has these methods and attributes:

> 如上所述，当调用工厂函数时，它会接收一个类型为`gdb.TuiWindow`的对象。该对象具有以下方法和属性：


Function: **TuiWindow.is_valid** *()*

> 功能：**TuiWindow.is_valid** *（）*


:   This method returns `True` when this window is valid. When the user changes the TUI layout, windows no longer visible in the new layout will be destroyed. At this point, the `gdb.TuiWindow` will no longer be valid, and methods (and attributes) other than `is_valid` will throw an exception.

> 这个方法在这个窗口有效时返回`True`。当用户更改TUI布局时，新布局中不再可见的窗口将被销毁。此时，`gdb.TuiWindow`将不再有效，除了`is_valid`之外的方法（和属性）将抛出异常。

```
When the TUI is disabled using `tui disable` (see [tui disable](TUI-Commands.html#TUI-Commands)) the window is hidden rather than destroyed, but `is_valid` will still return `False` and other methods (and attributes) will still throw an exception.
```

```

```


Variable: **TuiWindow.width**

> 变量：**TuiWindow.width**


:   This attribute holds the width of the window. It is not writable.

> 这个属性保存窗口的宽度。它不可写。

```

```


Variable: **TuiWindow.height**

> 变量：**TuiWindow.height**


:   This attribute holds the height of the window. It is not writable.

> 这个属性保存窗口的高度，它是不可写的。

```

```


Variable: **TuiWindow.title**

> 变量：**TuiWindow.title**


:   This attribute holds the window's title, a string. This is normally displayed above the window. This attribute can be modified.

> 这个属性保存窗口的标题，一个字符串。这通常显示在窗口上方。这个属性可以被修改。

```

```


Function: **TuiWindow.erase** *()*

> 功能：**TuiWindow.erase**（）


:   Remove all the contents of the window.

> 清除窗口中的所有内容。

```

```

)*


:   Write `string` will translate these as appropriate for the terminal.

> 写入`字符串`

```
If the `full_window` contains the full contents of the window. This is similar to calling `erase` before `write`, but avoids the flickering.
```


The factory function that you supply should return an object conforming to the TUI window protocol. These are the method that can be called on this object, which is referred to below as the "window object". The methods documented below are optional; if the object does not implement one of these methods, [GDB] guarantees that they will begin with a lower-case letter, so you can start implementation methods with upper-case letters or underscore to avoid any future conflicts.

> 您提供的工厂函数应返回符合TUI窗口协议的对象。 下面称之为“窗口对象”的对象可以调用以下方法。 下面文档中的方法是可选的; 如果对象未实现其中一个方法，[GDB]保证它们将以小写字母开头，因此您可以以大写字母或下划线开头以避免任何未来冲突。


Function: **Window.close** *()*

> 窗口.关闭()


:   When the TUI window is closed, the `gdb.TuiWindow` object will be put into an invalid state. At this time, [GDB] will call `close` method on the window object.

> 当TUI窗口关闭时，`gdb.TuiWindow`对象将处于无效状态。此时，[GDB]将在窗口对象上调用`close`方法。

```
After this method is called, [GDB] will discard any references it holds on this window object, and will no longer call methods on this object.
```

```

```


Function: **Window.render** *()*

> 功能：**Window.render** *（）*


:   In some situations, a TUI window can change size. For example, this can happen if the user resizes the terminal, or changes the layout. When this happens, [GDB] will call the `render` method on the window object.

> 在某些情况下，TUI窗口可以改变大小。例如，如果用户调整终端的大小或更改布局，就会发生这种情况。当这种情况发生时，[GDB]将调用窗口对象上的`render`方法。

```
If your window is intended to update in response to changes in the inferior, you will probably also want to register event listeners and send output to the `gdb.TuiWindow`.
```

```

```


Function: **Window.hscroll** *(num)*

> 功能：Window.hscroll（num）


:   This is a request to scroll the window horizontally. `num` is the amount by which to scroll, with negative numbers meaning to scroll right. In the TUI model, it is the viewport that moves, not the contents. A positive argument should cause the viewport to move right, and so the content should appear to move to the left.

> 这是一个要求水平滚动窗口的请求。`num`是滚动的量，负数表示向右滚动。在TUI模型中，是视口移动，而不是内容。正参数应使视口向右移动，因此内容应该出现向左移动的情况。

```

```


Function: **Window.vscroll** *(num)*

> 功能：**Window.vscroll** *（num）*


:   This is a request to scroll the window vertically. `num` is the amount by which to scroll, with negative numbers meaning to scroll backward. In the TUI model, it is the viewport that moves, not the contents. A positive argument should cause the viewport to move down, and so the content should appear to move up.

> 这是一个要求垂直滚动窗口的请求。`num`是滚动的量，负数表示向后滚动。在TUI模型中，是视口移动而不是内容。正参数应该使视口向下移动，因此内容应该看起来向上移动。

```

```


Function: **Window.click** *(x, y, button)*

> 功能：**Window.click** *（x，y，button）*


:   This is called on a mouse click in this window. `x` specifies which mouse button was used, whose values can be 1 (left), 2 (middle), or 3 (right).

> 这是在这个窗口中单击鼠标时调用的。 `x`指定使用的鼠标按钮，其值可以为1（左），2（中）或3（右）。

---

::: header
Next: [Disassembly In Python](Disassembly-In-Python.html#Disassembly-In-Python)]
:::
