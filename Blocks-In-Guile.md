---
tip: translate by openai@2023-06-23 12:10:37
...
---
description: Blocks In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Blocks In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Blocks In Guile (Debugging with GDB)
---
::: header
Next: [Symbols In Guile](Symbols-In-Guile.html#Symbols-In-Guile)]
:::

---

#### 23.4.3.16 Accessing blocks from Guile.


In [GDB], symbols are stored in blocks. A block corresponds roughly to a scope in the source code. Blocks are organized hierarchically, and are represented individually in Guile as an object of type `<gdb:block>`. Blocks rely on debugging information being available.

> 在GDB中，符号存储在块中。一个块大致对应源代码中的一个范围。块以层次结构组织，并以Guile中的<gdb:block>类型的对象表示。块依赖于可用的调试信息。


A frame has a block. Please see [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile), for a more in-depth discussion of frames.

> 一个框架有一个块。请参考[Guile中的框架](Frames-In-Guile.html#Frames-In-Guile)，以获取更深入的讨论。


The outermost block is known as the *global block*. The global block typically holds public global variables and functions.

> 最外层的块被称为全局块。全局块通常包含公共的全局变量和函数。


The block nested just inside the global block is the *static block*. The static block typically holds file-scoped variables and functions.

> 全局块内部嵌套的块就是静态块。静态块通常包含文件范围的变量和函数。


[GDB] provides a method to get a block's superblock, but there is currently no way to examine the sub-blocks of a block, or to iterate over all the blocks in a symbol table (see [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)).

> [GDB]提供了一种方法来获取块的超块，但目前没有办法检查块的子块，或者遍历符号表中的所有块（参见[Guile中的符号表](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)）。


Here is a short example that should help explain blocks:

> 这里有一个简短的例子，可以帮助解释块：

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


The following block-related procedures are provided by the `(gdb)` module:

> `(gdb)` 模块提供以下与块相关的程序：


Scheme Procedure: **block?** *object*

> 方案程序：**block？** *对象*


:   Return `#t` if `object` is a `<gdb:block>` object. Otherwise return `#f`.

> 如果对象是<gdb:block>对象，则返回#t，否则返回#f。


Scheme Procedure: **block-valid?** *block*

> 方案程序：**block-valid？** *block*


:   Returns `#t` if `<gdb:block>` `block` is valid, `#f` if not. A block object can become invalid if the block it refers to doesn't exist anymore in the inferior. All other `<gdb:block>` methods will throw an exception if it is invalid at the time the procedure is called. The block's validity is also checked during iteration over symbols of the block.

> 返回`#t`如果`<gdb:block>`块`block`是有效的，`#f`如果不是。如果在次级中不再存在块所引用的块，则块对象可能无效。在调用过程时，所有其他`<gdb:block>`方法都会抛出异常，如果它是无效的。在迭代块的符号时也会检查块的有效性。


Scheme Procedure: **block-start** *block*

> 方案程序：**block-start** *block*


:   Return the start address of `<gdb:block>` `block`.

> 返回<gdb:block>块的起始地址。


Scheme Procedure: **block-end** *block*

> 方案程序：**块结束** *块*


:   Return the end address of `<gdb:block>` `block`.

> 返回<gdb:block>块的结束地址。


Scheme Procedure: **block-function** *block*

> 方案程序：** block-function ** * block *


:   Return the name of `<gdb:block>` `block` represented as a `<gdb:symbol>` object. If the block is not named, then `#f` is returned.

> 返回<gdb:block>块表示的<gdb:symbol>对象的名称。如果块没有命名，则返回#f。

```
For ordinary function blocks, the superblock is the static block. However, you should note that it is possible for a function block to have a superblock that is not the static block -- for instance this happens for an inlined function.
```


Scheme Procedure: **block-superblock** *block*

> 方案程序：**块-超级块** *块*


:   Return the block containing `<gdb:block>` `block`. If the parent block does not exist, then `#f` is returned.

> 如果父块不存在，则返回包含'<gdb:block>'块的块。如果父块不存在，则返回#f。


Scheme Procedure: **block-global-block** *block*

> 方案程序：**块全局块** *块*


:   Return the global block associated with `<gdb:block>` `block`.

> 返回与`<gdb:block>` `block`相关联的全局块。


Scheme Procedure: **block-static-block** *block*

> 方案程序：**静态块块** *块*


:   Return the static block associated with `<gdb:block>` `block`.

> 返回与`<gdb:block>` `block`相关联的静态块。


Scheme Procedure: **block-global?** *block*

> 方案程序：**block-global？** *block*


:   Return `#t` if `<gdb:block>` `block` is a global block. Otherwise return `#f`.

> 如果`<gdb:block>` `block`是一个全局块，则返回`#t`。否则返回`#f`。


Scheme Procedure: **block-static?** *block*

> 方案程序：** block-static？** *block*


:   Return `#t` if `<gdb:block>` `block` is a static block. Otherwise return `#f`.

> 如果<gdb:block>块是一个静态块，则返回#t，否则返回#f。


Scheme Procedure: **block-symbols**

> 方案程序：**块符号**


:   Return a list of all symbols (as \<gdb:symbol\> objects) in `<gdb:block>` `block`.

> 返回`block`中所有符号（以<gdb:symbol>对象）的列表。


Scheme Procedure: **make-block-symbols-iterator** *block*

> 制作块符号迭代器：**make-block-symbols-iterator** *block*


:   Return an object of type `<gdb:iterator>` that will iterate over all symbols of the block. Guile programs should not assume that a specific block object will always contain a given symbol, since changes in [GDB] features and infrastructure may cause symbols move across blocks in a symbol table. See [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile).

> 返回一个类型为`<gdb:iterator>`的对象，它将遍历块中的所有符号。Guile程序不应假定特定的块对象总是包含给定的符号，因为[GDB]功能和基础结构的变化可能会导致符号在符号表中移动。请参阅[Guile中的迭代器](Iterators-In-Guile.html#Iterators-In-Guile)。


Scheme Procedure: **block-symbols-progress?**

> 方案程序：**块符号进展？**


:   Return #t if the object is a \<gdb:block-symbols-progress\> object. This object would be obtained from the `progress` element of the `<gdb:iterator>` object returned by `make-block-symbols-iterator`.

> 如果对象是<gdb:block-symbols-progress>对象，则返回#t。此对象可从`make-block-symbols-iterator`返回的`<gdb:iterator>`对象的`progress`元素获得。


Scheme Procedure: **lookup-block** *pc*

> 方案程序：**lookup-block** *pc*


:   Return the innermost `<gdb:block>` containing the given `pc` value specified, the function will return `#f`.

> 如果指定的PC值没有包含在最内层的<gdb:block>中，函数将返回#f。

---

::: header
Next: [Symbols In Guile](Symbols-In-Guile.html#Symbols-In-Guile)]
:::
