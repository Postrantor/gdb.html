---
tip: translate by openai@2023-06-23 13:50:37
...
---
description: Symbols In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbols In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Symbols In Guile (Debugging with GDB)
--------------------------------------------

::: header
Next: [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)]
:::

---

#### 23.4.3.17 Guile representation of Symbols.

[GDB] with the `<gdb:symbol>` object.

> 使用 `<gdb:symbol>` 对象的 GDB。

The following symbol-related procedures are provided by the `(gdb)` module:

> `(gdb)` 模块提供以下与符号相关的程序：

Scheme Procedure: **symbol?** *object*

> 方案程序：** symbol？** *对象*

:   Return `#t` if `object` is an object of type `<gdb:symbol>`. Otherwise return `#f`.

> 如果对象是一个 [gdb:symbol](gdb:symbol) 类型的对象，则返回#t，否则返回#f。

```

```

Scheme Procedure: **symbol-valid?** *symbol*

> 模式过程：**symbol-valid?** *symbol*

:   Return `#t` if the `<gdb:symbol>` object is valid, `#f` if not. A `<gdb:symbol>` object can become invalid if the symbol it refers to does not exist in [GDB] any longer. All other `<gdb:symbol>` procedures will throw an exception if it is invalid at the time the procedure is called.

> 返回#t，如果 [gdb:symbol](gdb:symbol) 对象有效，返回#f，如果无效。如果 [gdb:symbol](gdb:symbol) 所指的符号在 GDB 中不再存在，则 [gdb:symbol](gdb:symbol) 对象可能会失效。如果在调用其他 [gdb:symbol](gdb:symbol) 过程时，它无效，则会抛出异常。

```

```

Scheme Procedure: **symbol-type** *symbol*

> 方案程序：**symbol-type** *symbol*

:   Return the type of `symbol` or `#f` if no type is recorded. The result is an object of type `<gdb:type>`. See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

> 返回 `symbol` 的类型或者如果没有记录则返回 `#f`。结果是 `<gdb:type>` 类型的对象。请参阅 [Guile 中的类型](Types-In-Guile.html#Types-In-Guile)。

```

```

Scheme Procedure: **symbol-symtab** *symbol*

> 方案程序：**symbol-symtab** *symbol*

:   Return the symbol table in which `symbol` appears. The result is an object of type `<gdb:symtab>`. See [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile).

> 返回包含 `符号` 的符号表。结果是类型为 `<gdb:symtab>` 的对象。请参阅 [Guile 中的符号表](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)。

```

```

Scheme Procedure: **symbol-line** *symbol*

> 方案程序：**symbol-line** *symbol*

:   Return the line number in the source code at which `symbol` was defined. This is an integer.

> 返回源代码中定义 `symbol` 的行号，这是一个整数。

```

```

Scheme Procedure: **symbol-name** *symbol*

> 方案程序：**symbol-name** *symbol*

:   Return the name of `symbol` as a string.

> 返回 `symbol` 的名称作为一个字符串。

```

```

Scheme Procedure: **symbol-linkage-name** *symbol*

> 符号链接名：**symbol-linkage-name** *符号*

:   Return the name of `symbol`, as used by the linker (i.e., may be mangled).

> 返回链接器使用的 `符号` 的名称（即可能被码化）。

```

```

Scheme Procedure: **symbol-print-name** *symbol*

> 方案程序：** symbol-print-name ** * symbol *

:   Return the name of `symbol` to display demangled or mangled names.

> 返回 `符号` 的名称以显示解码或编码的名称。

```

```

Scheme Procedure: **symbol-addr-class** *symbol*

> 程序设计方案：** symbol-addr-class ** * symbol *

:   Return the address class of the symbol. This classifies how to find the value of a symbol. Each address class is a constant defined in the `(gdb)` module and described later in this chapter.

> 返回符号的地址类。这将符号的值分类。每个地址类都是 `(gdb)` 模块中定义的常量，并在本章后面进行了描述。

```

```

Scheme Procedure: **symbol-needs-frame?** *symbol*

> 程序：**symbol-needs-frame?** *symbol*
> 符号需要框架？*符号*

:   Return `#t` if evaluating `symbol`'s value requires a frame (see [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile)) and `#f` otherwise. Typically, local variables will require a frame, but other symbols will not.

> 如果求取 `symbol` 的值需要一个框架（参见 [Guile 中的框架](Frames-In-Guile.html#Frames-In-Guile))，则返回 `#t`，否则返回 `#f`。通常，局部变量需要框架，但其他符号不需要。

```

```

Scheme Procedure: **symbol-argument?** *symbol*

> 程序设计：**symbol-argument?** *symbol*

:   Return `#t` if `symbol` is an argument of a function. Otherwise return `#f`.

> 如果 `symbol` 是函数的参数，则返回 `#t`，否则返回 `#f`。

```

```

Scheme Procedure: **symbol-constant?** *symbol*

> 方案程序：**symbol-constant？** *symbol*

:   Return `#t` if `symbol` is a constant. Otherwise return `#f`.

> 如果 `符号` 是一个常量，就返回 `#t`。否则返回 `#f`。

```

```

Scheme Procedure: **symbol-function?** *symbol*

> 函数名称：**symbol-function?** *symbol*

:   Return `#t` if `symbol` is a function or a method. Otherwise return `#f`.

> 如果 `symbol` 是一个函数或方法，则返回 `#t`，否则返回 `#f`。

```

```

Scheme Procedure: **symbol-variable?** *symbol*

> 方案程序：** symbol-variable？** *符号*

:   Return `#t` if `symbol` is a variable. Otherwise return `#f`.

> 如果符号是一个变量，则返回#t，否则返回#f。

```

```

*

:   Compute the value of `symbol` is invalid, then an exception is thrown.

> 计算 `符号` 的值无效，则会抛出异常。

```

```

*

:   This function searches for a symbol by name. The search scope can be restricted to the parameters defined in the optional domain and block arguments.

> 这个函数通过名称搜索符号。搜索范围可以限制为可选域和块参数中定义的参数。

```
`name` argument must be a domain constant defined in the `(gdb)` module and described later in this chapter.

The result is a list of two elements. The first element is a `<gdb:symbol>` object or `#f` if the symbol is not found. If the symbol is found, the second element is `#t` if the symbol is a field of a method's object (e.g., `this` in C++), otherwise it is `#f`. If the symbol is not found, the second element is `#f`.
```

```

```

*

:   This function searches for a global symbol by name. The search scope can be restricted by the domain argument.

> 这个函数通过名称搜索全局符号。搜索范围可以通过 domain 参数来限制。

```
`name` argument must be a domain constant defined in the `(gdb)` module and described later in this chapter.

The result is a `<gdb:symbol>` object or `#f` if the symbol is not found.
```

The available domain categories in `<gdb:symbol>` are represented as constants in the `(gdb)` module:

> `<gdb:symbol>` 模块中的可用域类别由 `(gdb)` 模块中的常量表示。

`SYMBOL_UNDEF_DOMAIN`

:   This is used when a domain has not been discovered or none of the following domains apply. This usually indicates an error either in the symbol information or in [GDB]'s handling of symbols.

> 这是在域未被发现或没有以下域适用时使用的。这通常表示符号信息中的错误或[GDB]处理符号时的错误。

`SYMBOL_VAR_DOMAIN`

:   This domain contains variables, function names, typedef names and enum type values.

> 这个域包含变量、函数名称、类型定义名称和枚举类型值。

`SYMBOL_STRUCT_DOMAIN`

:   This domain holds struct, union and enum type names.

> 此域名拥有结构体、联合体和枚举类型的名称。

`SYMBOL_LABEL_DOMAIN`

:   This domain contains names of labels (for gotos).

> 这个域包含了跳转的标签名称。

`SYMBOL_VARIABLES_DOMAIN`

:   This domain holds a subset of the `SYMBOLS_VAR_DOMAIN`; it contains everything minus functions and types.

> 这个域拥有 `SYMBOLS_VAR_DOMAIN` 的一个子集；它包含了除了函数和类型之外的所有内容。

`SYMBOL_FUNCTIONS_DOMAIN`

:   This domain contains all functions.

> 这个域包含所有的功能。

`SYMBOL_TYPES_DOMAIN`

:   This domain contains all types.

> 这个域包含所有类型。

The available address class categories in `<gdb:symbol>` are represented as constants in the `gdb` module:

> [gdb:symbol](gdb:symbol) 中可用的地址类别由 gdb 模块中的常量表示。

`SYMBOL_LOC_UNDEF`

:   If this is returned by address class, it indicates an error either in the symbol information or in [GDB]'s handling of symbols.

> 如果地址类返回此项，则表明符号信息中或 GDB 处理符号时存在错误。

`SYMBOL_LOC_CONST`

:   Value is constant int.

> 价值是恒定的整数。

`SYMBOL_LOC_STATIC`

:   Value is at a fixed address.

> 值固定在一个地址。

`SYMBOL_LOC_REGISTER`

:   Value is in a register.

> 值存储在寄存器中。

`SYMBOL_LOC_ARG`

:   Value is an argument. This value is at the offset stored within the symbol inside the frame's argument list.

> 这个值是一个参数。这个值存储在符号内的帧参数列表中的偏移量中。

`SYMBOL_LOC_REF_ARG`

:   Value address is stored in the frame's argument list. Just like `LOC_ARG` except that the value's address is stored at the offset, not the value itself.

> 值的地址存储在帧的参数列表中，就像 `LOC_ARG` 一样，只是值的地址存储在偏移量处，而不是值本身。

`SYMBOL_LOC_REGPARM_ADDR`

:   Value is a specified register. Just like `LOC_REGISTER` except the register holds the address of the argument instead of the argument itself.

> 值是一个指定的寄存器。就像 `LOC_REGISTER` 一样，但是寄存器保存的是参数的地址而不是参数本身。

`SYMBOL_LOC_LOCAL`

:   Value is a local variable.

> 值是一个局部变量。

`SYMBOL_LOC_TYPEDEF`

:   Value not used. Symbols in the domain `SYMBOL_STRUCT_DOMAIN` all have this class.

> 值未使用。域 `SYMBOL_STRUCT_DOMAIN` 中的符号都具有此类。

`SYMBOL_LOC_BLOCK`

:   Value is a block.

`SYMBOL_LOC_CONST_BYTES`

:   Value is a byte-sequence.

> 值是一个字节序列。

`SYMBOL_LOC_UNRESOLVED`

:   Value is at a fixed address, but the address of the variable has to be determined from the minimal symbol table whenever the variable is referenced.

> 值固定在一个地址上，但是每次引用变量时都必须从最小符号表中确定变量的地址。

`SYMBOL_LOC_OPTIMIZED_OUT`

:   The value does not actually exist in the program.

> 程序中实际上不存在该值。

`SYMBOL_LOC_COMPUTED`

:   The value's address is a computed location.

> 地址的值是一个计算出来的位置。

---

::: header
Next: [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)]
:::
