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

Function: **gdb.register_window_type** *(name, factory)*

:   Because TUI windows are created and destroyed depending on the layout the user chooses, new window types are implemented by registering a factory function with [GDB].

```
`name` should match the regular expression `[a-zA-Z][-_.a-zA-Z0-9]*`, it is an error to try and create a window with an invalid name.

`function` is a factory function that is called to create the TUI window. This is called with a single argument of type `gdb.TuiWindow`, described below. It should return an object that implements the TUI window protocol, also described below.
```

As mentioned above, when a factory function is called, it is passed an object of type `gdb.TuiWindow`. This object has these methods and attributes:

Function: **TuiWindow.is_valid** *()*

:   This method returns `True` when this window is valid. When the user changes the TUI layout, windows no longer visible in the new layout will be destroyed. At this point, the `gdb.TuiWindow` will no longer be valid, and methods (and attributes) other than `is_valid` will throw an exception.

```
When the TUI is disabled using `tui disable` (see [tui disable](TUI-Commands.html#TUI-Commands)) the window is hidden rather than destroyed, but `is_valid` will still return `False` and other methods (and attributes) will still throw an exception.
```

```
<!-- -->
```

Variable: **TuiWindow.width**

:   This attribute holds the width of the window. It is not writable.

```
<!-- -->
```

Variable: **TuiWindow.height**

:   This attribute holds the height of the window. It is not writable.

```
<!-- -->
```

Variable: **TuiWindow.title**

:   This attribute holds the window's title, a string. This is normally displayed above the window. This attribute can be modified.

```
<!-- -->
```

Function: **TuiWindow.erase** *()*

:   Remove all the contents of the window.

```
<!-- -->
```

)*

:   Write `string` will translate these as appropriate for the terminal.

```
If the `full_window` contains the full contents of the window. This is similar to calling `erase` before `write`, but avoids the flickering.
```

The factory function that you supply should return an object conforming to the TUI window protocol. These are the method that can be called on this object, which is referred to below as the "window object". The methods documented below are optional; if the object does not implement one of these methods, [GDB] guarantees that they will begin with a lower-case letter, so you can start implementation methods with upper-case letters or underscore to avoid any future conflicts.

Function: **Window.close** *()*

:   When the TUI window is closed, the `gdb.TuiWindow` object will be put into an invalid state. At this time, [GDB] will call `close` method on the window object.

```
After this method is called, [GDB] will discard any references it holds on this window object, and will no longer call methods on this object.
```

```
<!-- -->
```

Function: **Window.render** *()*

:   In some situations, a TUI window can change size. For example, this can happen if the user resizes the terminal, or changes the layout. When this happens, [GDB] will call the `render` method on the window object.

```
If your window is intended to update in response to changes in the inferior, you will probably also want to register event listeners and send output to the `gdb.TuiWindow`.
```

```
<!-- -->
```

Function: **Window.hscroll** *(num)*

:   This is a request to scroll the window horizontally. `num` is the amount by which to scroll, with negative numbers meaning to scroll right. In the TUI model, it is the viewport that moves, not the contents. A positive argument should cause the viewport to move right, and so the content should appear to move to the left.

```
<!-- -->
```

Function: **Window.vscroll** *(num)*

:   This is a request to scroll the window vertically. `num` is the amount by which to scroll, with negative numbers meaning to scroll backward. In the TUI model, it is the viewport that moves, not the contents. A positive argument should cause the viewport to move down, and so the content should appear to move up.

```
<!-- -->
```

Function: **Window.click** *(x, y, button)*

:   This is called on a mouse click in this window. `x` specifies which mouse button was used, whose values can be 1 (left), 2 (middle), or 3 (right).

---

::: header
Next: [Disassembly In Python](Disassembly-In-Python.html#Disassembly-In-Python)]
:::
