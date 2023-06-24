---
tip: translate by openai@2023-06-23 21:25:48
...
---
description: Frames In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frames In Python (Debugging with GDB)
lang: en
resource-type: document
title: Frames In Python (Debugging with GDB)
---
::: header
Next: [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python)]
:::

---

#### 23.3.2.26 Accessing inferior stack frames from Python


When the debugged program stops, [GDB] will throw a `gdb.error` exception (see [Exception Handling](Exception-Handling.html#Exception-Handling)).

> 当调试的程序停止时，[GDB]会抛出一个`gdb.error`异常（参见[异常处理](Exception-Handling.html#Exception-Handling)）。


Two `gdb.Frame` objects can be compared for equality with the `==` operator, like:

> 两个gdb.Frame对象可以使用'=='操作符进行比较，如：

::: smallexample

```bash
(gdb) python print gdb.newest_frame() == gdb.selected_frame ()
True
```

:::

The following frame-related functions are available in the `gdb` module:

Function: **gdb.selected_frame** *()*


:   Return the selected frame object. (see [Selecting a Frame](Selection.html#Selection)).

> 返回所选择的帧对象（参见[选择帧](Selection.html#Selection)）。

Function: **gdb.newest_frame** *()*

:   Return the newest frame object for the selected thread.

```
<!-- -->
```

Function: **gdb.frame_stop_reason_string** *(reason)*


:   Return a string explaining the reason why [GDB] code (an integer, see the `unwind_stop_reason` method further down in this section).

> 返回一个字符串来解释[GDB]代码（一个整数，请参见本节下面的`unwind_stop_reason`方法）的原因。

Function: **gdb.invalidate_cached_frames**


:   [GDB] internally keeps a cache of the frames that have been unwound. This function invalidates this cache.

> GDB在内部维护一个已经展开的帧的缓存。此函数将使这个缓存失效。

```
This function should not generally be called by ordinary Python code. It is documented for the sake of completeness.
```

A `gdb.Frame` object has the following methods:

Function: **Frame.is_valid** *()*


:   Returns true if the `gdb.Frame` object is valid, false if not. A frame object can become invalid if the frame it refers to doesn't exist anymore in the inferior. All `gdb.Frame` methods will throw an exception if it is invalid at the time the method is called.

> 如果`gdb.Frame`对象有效，则返回true，如果无效则返回false。如果框架它所指的在下级中不再存在，那么框架对象可能会变得无效。如果在调用方法时无效，则所有`gdb.Frame`方法都会抛出异常。

```
<!-- -->
```

Function: **Frame.name** *()*


:   Returns the function name of the frame, or `None` if it can't be obtained.

> 返回该帧的函数名，如果无法获取则返回`None`。

```
<!-- -->
```

Function: **Frame.architecture** *()*


:   Returns the `gdb.Architecture` object corresponding to the frame's architecture. See [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python).

> 返回与帧架构对应的`gdb.Architecture`对象。请参阅[Python中的架构](Architectures-In-Python.html#Architectures-In-Python)。

```
<!-- -->
```

Function: **Frame.type** *()*

:   Returns the type of the frame. The value can be one of:

```
`gdb.NORMAL_FRAME`

:   An ordinary stack frame.

`gdb.DUMMY_FRAME`

:   A fake stack frame that was created by [GDB] when performing an inferior function call.

`gdb.INLINE_FRAME`

:   A frame representing an inlined function. The function was inlined into a `gdb.NORMAL_FRAME` that is older than this one.

`gdb.TAILCALL_FRAME`

:   A frame representing a tail call. See [Tail Call Frames](Tail-Call-Frames.html#Tail-Call-Frames).

`gdb.SIGTRAMP_FRAME`

:   A signal trampoline frame. This is the frame created by the OS when it calls into a signal handler.

`gdb.ARCH_FRAME`

:   A fake stack frame representing a cross-architecture call.

`gdb.SENTINEL_FRAME`

:   This is like `gdb.NORMAL_FRAME`, but it is only used for the newest frame.
```

```
<!-- -->
```

Function: **Frame.unwind_stop_reason** *()*


:   Return an integer representing the reason why it's not possible to find more frames toward the outermost frame. Use `gdb.frame_stop_reason_string` to convert the value returned by this function to a string. The value can be one of:

> 返回一个整数，表示为什么无法找到更多朝外部框架的帧。使用`gdb.frame_stop_reason_string`将此函数返回的值转换为字符串。该值可以是以下之一：

```
`gdb.FRAME_UNWIND_NO_REASON`

:   No particular reason (older frames should be available).

`gdb.FRAME_UNWIND_NULL_ID`

:   The previous frame's analyzer returns an invalid result. This is no longer used by [GDB], and is kept only for backward compatibility.

`gdb.FRAME_UNWIND_OUTERMOST`

:   This frame is the outermost.

`gdb.FRAME_UNWIND_UNAVAILABLE`

:   Cannot unwind further, because that would require knowing the values of registers or memory that have not been collected.

`gdb.FRAME_UNWIND_INNER_ID`

:   This frame ID looks like it ought to belong to a NEXT frame, but we got it for a PREV frame. Normally, this is a sign of unwinder failure. It could also indicate stack corruption.

`gdb.FRAME_UNWIND_SAME_ID`

:   This frame has the same ID as the previous one. That means that unwinding further would almost certainly give us another frame with exactly the same ID, so break the chain. Normally, this is a sign of unwinder failure. It could also indicate stack corruption.

`gdb.FRAME_UNWIND_NO_SAVED_PC`

:   The frame unwinder did not find any saved PC, but we needed one to unwind further.

`gdb.FRAME_UNWIND_MEMORY_ERROR`

:   The frame unwinder caused an error while trying to access memory.

`gdb.FRAME_UNWIND_FIRST_ERROR`

:   Any stop reason greater or equal to this value indicates some kind of error. This special value facilitates writing code that tests for errors in unwinding in a way that will work correctly even if the list of the other values is modified in future [GDB] versions. Using it, you could write:

    ::: smallexample
    ``` smallexample
    reason = gdb.selected_frame().unwind_stop_reason ()
    reason_str =  gdb.frame_stop_reason_string (reason)
    if reason >=  gdb.FRAME_UNWIND_FIRST_ERROR:
        print ("An error occurred: %s" % reason_str)
    ```
    :::
```

```
<!-- -->
```

Function: **Frame.pc** *()*

:   Returns the frame's resume address.

```
<!-- -->
```

Function: **Frame.block** *()*


:   Return the frame's code block. See [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python). If the frame does not have a block -- for example, if there is no debugging information for the code in question -- then this will throw an exception.

> 返回框架的代码块。参见[Python中的块](Blocks-In-Python.html#Blocks-In-Python)。如果框架没有块 - 例如，如果没有相关代码的调试信息 - 那么这将引发异常。

```
<!-- -->
```

Function: **Frame.function** *()*


:   Return the symbol for the function corresponding to this frame. See [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python).

> 请查看[Python中的符号](Symbols-In-Python.html#Symbols-In-Python)，返回与此框架对应的函数的符号。

```
<!-- -->
```

Function: **Frame.older** *()*


:   Return the frame that called this frame. If this is the oldest frame, return `None`.

> 返回调用此框架的框架。如果这是最旧的框架，则返回“无”。

```
<!-- -->
```

Function: **Frame.newer** *()*


:   Return the frame called by this frame. If this is the newest frame, return `None`.

> 返回此帧调用的帧。如果这是最新的帧，则返回`None`。

```
<!-- -->
```

Function: **Frame.find_sal** *()*


:   Return the frame's symtab and line object. See [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python).

> 返回框架的符号表和行对象。参见[Python中的符号表](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)。

Function: **Frame.read_register** *(register)*

:   Return the value of `register` argument must be one of the following:

```
1.  A string that is the name of a valid register (e.g., `'sp'` or `'rax'`).
2.  A `gdb.RegisterDescriptor` object (see [Registers In Python](Registers-In-Python.html#Registers-In-Python)).
3.  A [GDB] source tree.

Using a string to access registers will be slightly slower than the other two methods as [GDB] must look up the mapping between name and internal register number. If performance is critical consider looking up and caching a `gdb.RegisterDescriptor` object.
```

```
<!-- -->
```

)*

:   Return the value of `variable` must be a `gdb.Block` object.

```
<!-- -->
```

Function: **Frame.select** *()*


:   Set this frame to be the selected frame. See [Examining the Stack](Stack.html#Stack).

> 将此帧设置为所选帧。请参见[检查堆栈](Stack.html#Stack)。

```
<!-- -->
```

Function: **Frame.level** *()*


:   Return an integer, the stack frame level for this frame. See [Stack Frames](Frames.html#Frames).

> 返回一个整数，这个帧的堆栈帧级别。请参阅[堆栈帧](Frames.html#Frames)。

```
<!-- -->
```

Function: **Frame.language** *()*

:   Return a string, the source language for this frame.

---

::: header
Next: [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python)]
:::
