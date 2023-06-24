---
tip: translate by openai@2023-06-23 18:04:28
...
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

> 在GDB中，符号存储在块中。一个块大致对应源代码中的一个范围。块以层次结构组织，并以Python中的`gdb.Block`表示。块依赖于可用的调试信息。


A frame has a block. Please see [Frames In Python](Frames-In-Python.html#Frames-In-Python), for a more in-depth discussion of frames.

> 一个框架有一个块。请参阅[Python中的框架](Frames-In-Python.html#Frames-In-Python)，了解更深入的讨论。


The outermost block is known as the *global block*. The global block typically holds public global variables and functions.

> 最外层的块被称为全局块。全局块通常包含公共的全局变量和函数。


The block nested just inside the global block is the *static block*. The static block typically holds file-scoped variables and functions.

> 全局块内部嵌套的块就是静态块。静态块通常包含文件范围内的变量和函数。


[GDB] provides a method to get a block's superblock, but there is currently no way to examine the sub-blocks of a block, or to iterate over all the blocks in a symbol table (see [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)).

> GDB提供了一种方法来获取块的超块，但目前没有办法检查块的子块，或遍历符号表中的所有块（请参阅Python中的符号表[Symbol Tables In Python]（Symbol-Tables-In-Python.html#Symbol-Tables-In-Python））。


Here is a short example that should help explain blocks:

> 这里有一个简短的例子，有助于解释块：

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

> 一个`gdb.Block`可以迭代。迭代器会返回本地块中的符号（参见[Python中的符号]（Symbols-In-Python.html#Symbols-In-Python））。Python程序不应该假设特定块对象总是包含给定的符号，因为[GDB]功能和基础设施的变化可能会导致符号在符号表中跨块移动。您还可以使用Python的*字典语法*来访问此块中的变量，例如：

::: smallexample

```bash
symbol = some_block['variable']  # symbol is of type gdb.Symbol
```

:::


The following block-related functions are available in the `gdb` module:

> `gdb` 模块中可用的以下块相关函数：


Function: **gdb.block_for_pc** *(pc)*

> 功能：**gdb.block_for_pc** *（pc）*


:   Return the innermost `gdb.Block` containing the given `pc` value specified, the function will return `None`. This is identical to `gdb.current_progspace().block_for_pc(pc)` and is included for historical compatibility.

> 返回包含给定的pc值的最内层的gdb.Block，该函数将返回None。这与gdb.current_progspace().block_for_pc(pc)相同，仅为历史兼容性而包含。


A `gdb.Block` object has the following methods:

> 一个`gdb.Block`对象具有以下方法：


Function: **Block.is_valid** *()*

> 功能：**Block.is_valid** *（）*


:   Returns `True` if the `gdb.Block` object is valid, `False` if not. A block object can become invalid if the block it refers to doesn't exist anymore in the inferior. All other `gdb.Block` methods will throw an exception if it is invalid at the time the method is called. The block's validity is also checked during iteration over symbols of the block.

> 如果gdb.Block对象有效，则返回True；如果无效，则返回False。如果其所引用的块在下级中不再存在，则块对象可能会失效。在调用方法时，还会检查块的有效性。在迭代块的符号时也会检查块的有效性。


A `gdb.Block` object has the following attributes:

> 一个`gdb.Block`对象具有以下属性：


Variable: **Block.start**

> 变量：**Block.start**


:   The start address of the block. This attribute is not writable.

> 这个块的起始地址。这个属性是不可写的。

```
<!-- -->
```

Variable: **Block.end**


:   One past the last address that appears in the block. This attribute is not writable.

> 最后一个地址出现在块中的下一个。这个属性是不可写的。

```
<!-- -->
```


Variable: **Block.function**

> 变量：**块.功能**


:   The name of the block represented as a `gdb.Symbol`. If the block is not named, then this attribute holds `None`. This attribute is not writable.

> 这个块的名字用`gdb.Symbol`表示。如果块没有命名，那么这个属性就是`None`。这个属性不可写。

```
For ordinary function blocks, the superblock is the static block. However, you should note that it is possible for a function block to have a superblock that is not the static block -- for instance this happens for an inlined function.
```

```
<!-- -->
```


Variable: **Block.superblock**

> 变量：** Block.superblock **


:   The block containing this block. If this parent block does not exist, this attribute holds `None`. This attribute is not writable.

> 这个块所包含的父块。如果这个父块不存在，这个属性将为“None”。这个属性是不可写的。

```
<!-- -->
```


Variable: **Block.global_block**

> 变量：**Block.global_block**


:   The global block associated with this block. This attribute is not writable.

> 这个块关联的全局块。这个属性是不可写的。

```
<!-- -->
```


Variable: **Block.static_block**

> 变量：**Block.static_block**


:   The static block associated with this block. This attribute is not writable.

> 这个块相关联的静态块。这个属性是不可写的。

```
<!-- -->
```


Variable: **Block.is_global**

> 变量：**Block.is_global**


:   `True` if the `gdb.Block` object is a global block, `False` if not. This attribute is not writable.

> 真的，如果`gdb.Block`对象是一个全局块，则为`False`。此属性不可写。

```
<!-- -->
```


Variable: **Block.is_static**

> 变量：**Block.is_static**


:   `True` if the `gdb.Block` object is a static block, `False` if not. This attribute is not writable.

> 真，如果`gdb.Block`对象是静态块；假，如果不是。此属性不可写。

---

::: header
Next: [Symbols In Python](Symbols-In-Python.html#Symbols-In-Python)]
:::
