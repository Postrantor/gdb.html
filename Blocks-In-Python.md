---
description: Blocks In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Blocks In Python (Debugging with GDB)
lang: en
resource-type: document
title: Blocks In Python (Debugging with GDB)
---
::: header
Next: [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python)]
:::

---

#### 23.3.2.27 Accessing blocks from Python

In [GDB], symbols are stored in blocks. A block corresponds roughly to a scope in the source code. Blocks are organized hierarchically, and are represented individually in Python as a `gdb.Block`. Blocks rely on debugging information being available.

A frame has a block. Please see [Frames In Python](Frames-In-Python.html#Frames-In-Python), for a more in-depth discussion of frames.

The outermost block is known as the *global block*. The global block typically holds public global variables and functions.

The block nested just inside the global block is the *static block*. The static block typically holds file-scoped variables and functions.

[GDB] provides a method to get a block's superblock, but there is currently no way to examine the sub-blocks of a block, or to iterate over all the blocks in a symbol table (see [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)).

Here is a short example that should help explain blocks:

::: smallexample

```bash
/* This is in the global block.  */
int global;

/* This is in the static block.  */
static int file_scope;

/* 'function' is in the global block, and 'argument' is
   in a block nested inside of 'function'.  */
int function (int argument)
{
  /* 'local' is in a block inside 'function'.  It may or may
     not be in the same block as 'argument'.  */
  int local;

  {
     /* 'inner' is in a block whose superblock is the one holding
        'local'.  */
     int inner;

     /* If this call is expanded by the compiler, you may see
        a nested block here whose function is 'inline_function'
        and whose superblock is the one holding 'inner'.  */
     inline_function ();
  }
}
```

:::

A `gdb.Block` is iterable. The iterator returns the symbols (see [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python)) local to the block. Python programs should not assume that a specific block object will always contain a given symbol, since changes in [GDB] features and infrastructure may cause symbols move across blocks in a symbol table. You can also use Python's *dictionary syntax* to access variables in this block, e.g.:

::: smallexample

```bash
symbol = some_block['variable']  # symbol is of type gdb.Symbol
```

:::

The following block-related functions are available in the `gdb` module:

Function: **gdb.block_for_pc** *(pc)*

:   Return the innermost `gdb.Block` containing the given `pc` value specified, the function will return `None`. This is identical to `gdb.current_progspace().block_for_pc(pc)` and is included for historical compatibility.

A `gdb.Block` object has the following methods:

Function: **Block.is_valid** *()*

:   Returns `True` if the `gdb.Block` object is valid, `False` if not. A block object can become invalid if the block it refers to doesn't exist anymore in the inferior. All other `gdb.Block` methods will throw an exception if it is invalid at the time the method is called. The block's validity is also checked during iteration over symbols of the block.

A `gdb.Block` object has the following attributes:

Variable: **Block.start**

:   The start address of the block. This attribute is not writable.

```
<!-- -->
```

Variable: **Block.end**

:   One past the last address that appears in the block. This attribute is not writable.

```
<!-- -->
```

Variable: **Block.function**

:   The name of the block represented as a `gdb.Symbol`. If the block is not named, then this attribute holds `None`. This attribute is not writable.

```
For ordinary function blocks, the superblock is the static block. However, you should note that it is possible for a function block to have a superblock that is not the static block -- for instance this happens for an inlined function.
```

```
<!-- -->
```

Variable: **Block.superblock**

:   The block containing this block. If this parent block does not exist, this attribute holds `None`. This attribute is not writable.

```
<!-- -->
```

Variable: **Block.global_block**

:   The global block associated with this block. This attribute is not writable.

```
<!-- -->
```

Variable: **Block.static_block**

:   The static block associated with this block. This attribute is not writable.

```
<!-- -->
```

Variable: **Block.is_global**

:   `True` if the `gdb.Block` object is a global block, `False` if not. This attribute is not writable.

```
<!-- -->
```

Variable: **Block.is_static**

:   `True` if the `gdb.Block` object is a static block, `False` if not. This attribute is not writable.

---

::: header
Next: [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python)]
:::
