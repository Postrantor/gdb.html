---
description: Unwinding Frames in Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Unwinding Frames in Python (Debugging with GDB)
lang: en
resource-type: document
title: Unwinding Frames in Python (Debugging with GDB)
---
::: header
Next: [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python)]
:::

---

#### 23.3.2.12 Unwinding Frames in Python

In [GDB] mantains a list of the unwinders and calls each unwinder's sniffer in turn until it finds the one that recognizes the current frame. There is an API to register an unwinder.

The unwinders that come with [GDB] unwinders. You can write Python code that can handle such custom frames.

You implement a frame unwinder in Python as a class with which has two attributes, `name` and `enabled`, with obvious meanings, and a single method `__call__`, which examines a given frame and returns an object (an instance of `gdb.UnwindInfo class)` describing it. If an unwinder does not recognize a frame, it should return `None`. The code in [GDB] core asks for them.

An unwinder should do as little work as possible. Some otherwise innocuous operations can cause problems (even crashes, as this code is not not well-hardened yet). For example, making an inferior call from an unwinder is unadvisable, as an inferior call will reset [GDB]'s stack unwinding process, potentially causing re-entrant unwinding.

#### Unwinder Input

An object passed to an unwinder (a `gdb.PendingFrame` instance) provides a method to read frame's registers:

Function: **PendingFrame.read_register** *(register)*

:   This method returns the contents of `register` does not name a register for the current architecture, this method will throw an exception.

```
Note that this method will always return a `gdb.Value` for a valid register name. This does not mean that the value will be valid. For example, you may request a register that an earlier unwinder could not unwind---the value will be unavailable. Instead, the `gdb.Value` returned from this method will be lazy; that is, its underlying bits will not be fetched until it is first used. So, attempting to use such a value will cause an exception at the point of use.

The type of the returned `gdb.Value` depends on the register and the architecture. It is common for registers to have a scalar type, like `long long`; but many other types are possible, such as pointer, pointer-to-function, floating point or vector types.
```

It also provides a factory method to create a `gdb.UnwindInfo` instance to be returned to [GDB]:

Function: **PendingFrame.create_unwind_info** *(frame_id)*

:   Returns a new `gdb.UnwindInfo` instance identified by given `frame_id`:

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
<!-- -->
```

Function: **PendingFrame.architecture** *()*

:   Return the `gdb.Architecture` (see [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python)) for this `gdb.PendingFrame`. This represents the architecture of the particular frame being unwound.

```
<!-- -->
```

Function: **PendingFrame.level** *()*

:   Return an integer, the stack frame level for this frame. See [Stack Frames](Frames.html#Frames).

```
<!-- -->
```

Function: **PendingFrame.name** *()*

:   Returns the function name of this pending frame, or `None` if it can't be obtained.

```
<!-- -->
```

Function: **PendingFrame.is_valid** *()*

:   Returns true if the `gdb.PendingFrame` object is valid, false if not. A pending frame object becomes invalid when the call to the unwinder, for which the pending frame was created, returns.

```
All `gdb.PendingFrame` methods, except this one, will raise an exception if the pending frame object is invalid at the time the method is called.
```

```
<!-- -->
```

Function: **PendingFrame.pc** *()*

:   Returns the pending frame's resume address.

```
<!-- -->
```

Function: **PendingFrame.block** *()*

:   Return the pending frame's code block (see [Blocks In Python](Blocks-In-Python.html#Blocks-In-Python)). If the frame does not have a block -- for example, if there is no debugging information for the code in question -- then this will raise a `RuntimeError` exception.

```
<!-- -->
```

Function: **PendingFrame.function** *()*

:   Return the symbol for the function corresponding to this pending frame. See [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python).

```
<!-- -->
```

Function: **PendingFrame.find_sal** *()*

:   Return the pending frame's symtab and line object (see [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)).

```
<!-- -->
```

Function: **PendingFrame.language** *()*

:   Return the language of this frame, as a string, or None.

#### Unwinder Output: UnwindInfo

Use `PendingFrame.create_unwind_info` method described above to create a `gdb.UnwindInfo` instance. Use the following method to specify caller registers that have been saved in this frame:

Function: **gdb.UnwindInfo.add_saved_register** *(register, value)*

:   `register` is a register value (a `gdb.Value` object).

#### The `gdb.unwinder` Module

[GDB] comes with a `gdb.unwinder` module which contains the following classes:

class: **gdb.unwinder.Unwinder**

:   The `Unwinder` class is a base class from which user created unwinders can derive, though it is not required that unwinders derive from this class, so long as any user created unwinder has the required `name` and `enabled` attributes.

```
Function: **gdb.unwinder.Unwinder.__init__(name)**

:   The `name` commands (see [Managing Registered Unwinders](#Managing-Registered-Unwinders)).

Variable: **gdb.unwinder.name**

:   A read-only attribute which is a string, the name of this unwinder.

Variable: **gdb.unwinder.enabled**

:   A modifiable attribute containing a boolean; when `True`, the unwinder is enabled, and will be used by [GDB]. When `False`, the unwinder has been disabled, and will not be used.
```

class: **gdb.unwinder.FrameId**

:   This is a class suitable for being used as the frame-id when calling `gdb.PendingFrame.create_unwind_info`. It is not required to use this class, any class with the required attribute (see [gdb.PendingFrame.create_unwind_info](#gdb_002ePendingFrame_002ecreate_005funwind_005finfo)) will be accepted, but in most cases this class will be sufficient.

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

The `gdb.unwinders` module provides the function to register an unwinder:

Function: **gdb.unwinder.register_unwinder** *(locus, unwinder, replace=False)*

:   `locus` is `True`, in which case the old unwinder is deleted and the new unwinder is registered in its place.

```
[GDB].
```

#### Unwinder Skeleton Code

Here is an example of how to structure a user created unwinder:

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

`info unwinder [ locus [ name-regexp ] ]`

:   Lists all registered unwinders. Arguments `locus` are both optional and can be used to filter which unwinders are listed.

```
The `locus`, or the name of an object file. Only unwinders registered for the specified locus will be listed.

The `name-regexp` in quotes.
```

`disable unwinder [ locus [ name-regexp ] ]`

:   The `locus` above, but instead of listing the matching unwinders, all of the matching unwinders are disabled. The `enabled` field of each matching unwinder is set to `False`.

`enable unwinder [ locus [ name-regexp ] ]`

:   The `locus` above, but instead of listing the matching unwinders, all of the matching unwinders are enabled. The `enabled` field of each matching unwinder is set to `True`.

---

::: header
Next: [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python)]
:::
