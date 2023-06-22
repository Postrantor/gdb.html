---
description: Frames In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frames In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Frames In Guile (Debugging with GDB)
---
::: header
Next: [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile)]
:::

---

#### 23.4.3.15 Accessing inferior stack frames from Guile.

When the debugged program stops, [GDB] will throw a `gdb:invalid-object` exception (see [Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling)).

Two `<gdb:frame>` objects can be compared for equality with the `equal?` function, like:

::: smallexample

```bash
(gdb) guile (equal? (newest-frame) (selected-frame))
#t
```

:::

The following frame-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **frame?** *object*

:   Return `#t` if `object` is a `<gdb:frame>` object. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **frame-valid?** *frame*

:   Returns `#t` if `frame` is valid, `#f` if not. A frame object can become invalid if the frame it refers to doesn't exist anymore in the inferior. All `<gdb:frame>` procedures will throw an exception if the frame is invalid at the time the procedure is called.

```
<!-- -->
```

Scheme Procedure: **frame-name** *frame*

:   Return the function name of `frame`, or `#f` if it can't be obtained.

```
<!-- -->
```

Scheme Procedure: **frame-arch** *frame*

:   Return the `<gdb:architecture>` object corresponding to `frame`'s architecture. See [Architectures In Guile](Architectures-In-Guile.html#Architectures-In-Guile).

```
<!-- -->
```

Scheme Procedure: **frame-type** *frame*

:   Return the type of `frame`. The value can be one of:

```
`NORMAL_FRAME`

:   An ordinary stack frame.

`DUMMY_FRAME`

:   A fake stack frame that was created by [GDB] when performing an inferior function call.

`INLINE_FRAME`

:   A frame representing an inlined function. The function was inlined into a `NORMAL_FRAME` that is older than this one.

`TAILCALL_FRAME`

:   A frame representing a tail call. See [Tail Call Frames](Tail-Call-Frames.html#Tail-Call-Frames).

`SIGTRAMP_FRAME`

:   A signal trampoline frame. This is the frame created by the OS when it calls into a signal handler.

`ARCH_FRAME`

:   A fake stack frame representing a cross-architecture call.

`SENTINEL_FRAME`

:   This is like `NORMAL_FRAME`, but it is only used for the newest frame.
```

```
<!-- -->
```

Scheme Procedure: **frame-unwind-stop-reason** *frame*

:   Return an integer representing the reason why it's not possible to find more frames toward the outermost frame. Use `unwind-stop-reason-string` to convert the value returned by this function to a string. The value can be one of:

```
`FRAME_UNWIND_NO_REASON`

:   No particular reason (older frames should be available).

`FRAME_UNWIND_NULL_ID`

:   The previous frame's analyzer returns an invalid result.

`FRAME_UNWIND_OUTERMOST`

:   This frame is the outermost.

`FRAME_UNWIND_UNAVAILABLE`

:   Cannot unwind further, because that would require knowing the values of registers or memory that have not been collected.

`FRAME_UNWIND_INNER_ID`

:   This frame ID looks like it ought to belong to a NEXT frame, but we got it for a PREV frame. Normally, this is a sign of unwinder failure. It could also indicate stack corruption.

`FRAME_UNWIND_SAME_ID`

:   This frame has the same ID as the previous one. That means that unwinding further would almost certainly give us another frame with exactly the same ID, so break the chain. Normally, this is a sign of unwinder failure. It could also indicate stack corruption.

`FRAME_UNWIND_NO_SAVED_PC`

:   The frame unwinder did not find any saved PC, but we needed one to unwind further.

`FRAME_UNWIND_MEMORY_ERROR`

:   The frame unwinder caused an error while trying to access memory.

`FRAME_UNWIND_FIRST_ERROR`

:   Any stop reason greater or equal to this value indicates some kind of error. This special value facilitates writing code that tests for errors in unwinding in a way that will work correctly even if the list of the other values is modified in future [GDB] versions. Using it, you could write:

    ::: smallexample
    ``` smallexample
    (define reason (frame-unwind-stop-readon (selected-frame)))
    (define reason-str (unwind-stop-reason-string reason))
    (if (>= reason FRAME_UNWIND_FIRST_ERROR)
        (format #t "An error occurred: ~s\n" reason-str))
    ```
    :::
```

```
<!-- -->
```

Scheme Procedure: **frame-pc** *frame*

:   Return the frame's resume address.

```
<!-- -->
```

Scheme Procedure: **frame-block** *frame*

:   Return the frame's code block as a `<gdb:block>` object. See [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile).

```
<!-- -->
```

Scheme Procedure: **frame-function** *frame*

:   Return the symbol for the function corresponding to this frame as a `<gdb:symbol>` object, or `#f` if there isn't one. See [Symbols In Guile](Symbols-In-Guile.html#Symbols-In-Guile).

```
<!-- -->
```

Scheme Procedure: **frame-older** *frame*

:   Return the frame that called `frame`.

```
<!-- -->
```

Scheme Procedure: **frame-newer** *frame*

:   Return the frame called by `frame`.

```
<!-- -->
```

Scheme Procedure: **frame-sal** *frame*

:   Return the frame's `<gdb:sal>` (symtab and line) object. See [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile).

```
<!-- -->
```

Scheme Procedure: **frame-read-register** *frame register*

:   Return the value of `register`'.

```
<!-- -->
```

*

:   Return the value of `variable` must be a `<gdb:block>` object.

```
<!-- -->
```

Scheme Procedure: **frame-select** *frame*

:   Set `frame` to be the selected frame. See [Examining the Stack](Stack.html#Stack).

```
<!-- -->
```

Scheme Procedure: **selected-frame**

:   Return the selected frame object. See [Selecting a Frame](Selection.html#Selection).

```
<!-- -->
```

Scheme Procedure: **newest-frame**

:   Return the newest frame object for the selected thread.

```
<!-- -->
```

Scheme Procedure: **unwind-stop-reason-string** *reason*

:   Return a string explaining the reason why [GDB] code (an integer, see the `frame-unwind-stop-reason` procedure above in this section).

---

::: header
Next: [Blocks In Guile](Blocks-In-Guile.html#Blocks-In-Guile)]
:::
