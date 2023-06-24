---
tip: translate by openai@2023-06-24 03:30:18
...
---
description: Symbols In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbols In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Symbols In Guile (Debugging with GDB)
---
::: header
Next: [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)]
:::

---

#### 23.4.3.17 Guile representation of Symbols.

[GDB] with the `<gdb:symbol>` object.


The following symbol-related procedures are provided by the `(gdb)` module:

> `gdb` 模块提供以下与符号相关的程序：

Scheme Procedure: **symbol?** *object*


:   Return `#t` if `object` is an object of type `<gdb:symbol>`. Otherwise return `#f`.

> 如果对象是<gdb:symbol>类型的对象，则返回#t。否则返回#f。

```
<!-- -->
```

Scheme Procedure: **symbol-valid?** *symbol*


:   Return `#t` if the `<gdb:symbol>` object is valid, `#f` if not. A `<gdb:symbol>` object can become invalid if the symbol it refers to does not exist in [GDB] any longer. All other `<gdb:symbol>` procedures will throw an exception if it is invalid at the time the procedure is called.

> 返回#t，如果<gdb:symbol>对象有效，返回#f，如果无效。<gdb:symbol>对象会变得无效，如果它所引用的符号在GDB中不再存在。如果其他<gdb:symbol>过程在调用时无效，则会抛出异常。

```
<!-- -->
```

Scheme Procedure: **symbol-type** *symbol*


:   Return the type of `symbol` or `#f` if no type is recorded. The result is an object of type `<gdb:type>`. See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

> 返回`symbol`的类型，如果没有记录类型，则返回`#f`。结果是`<gdb:type>`类型的对象。参见[Guile中的类型](Types-In-Guile.html#Types-In-Guile)。

```
<!-- -->
```

Scheme Procedure: **symbol-symtab** *symbol*


:   Return the symbol table in which `symbol` appears. The result is an object of type `<gdb:symtab>`. See [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile).

> 返回包含`symbol`的符号表。结果是一个类型为`<gdb:symtab>`的对象。参见[Guile中的符号表](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)。

```
<!-- -->
```

Scheme Procedure: **symbol-line** *symbol*


:   Return the line number in the source code at which `symbol` was defined. This is an integer.

> 返回源代码中定义`符号`的行号。这是一个整数。

```
<!-- -->
```

Scheme Procedure: **symbol-name** *symbol*

:   Return the name of `symbol` as a string.

```
<!-- -->
```

Scheme Procedure: **symbol-linkage-name** *symbol*


:   Return the name of `symbol`, as used by the linker (i.e., may be mangled).

> 返回符号的链接器使用的名称（即可能被编码）。

```
<!-- -->
```

Scheme Procedure: **symbol-print-name** *symbol*

:   Return the name of `symbol` to display demangled or mangled names.

```
<!-- -->
```

Scheme Procedure: **symbol-addr-class** *symbol*


:   Return the address class of the symbol. This classifies how to find the value of a symbol. Each address class is a constant defined in the `(gdb)` module and described later in this chapter.

> 返回符号的地址类。这将符号的值分类。每个地址类都是`(gdb)`模块中定义的常量，在本章后面有详细描述。

```
<!-- -->
```

Scheme Procedure: **symbol-needs-frame?** *symbol*


:   Return `#t` if evaluating `symbol`'s value requires a frame (see [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile)) and `#f` otherwise. Typically, local variables will require a frame, but other symbols will not.

> 如果求取symbol的值需要一个帧（参见Guile中的帧），则返回#t，否则返回#f。通常，局部变量需要一个帧，但其他符号不需要。

```
<!-- -->
```

Scheme Procedure: **symbol-argument?** *symbol*


:   Return `#t` if `symbol` is an argument of a function. Otherwise return `#f`.

> 如果`symbol`是函数的参数，返回`#t`。否则返回`#f`。

```
<!-- -->
```

Scheme Procedure: **symbol-constant?** *symbol*

:   Return `#t` if `symbol` is a constant. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **symbol-function?** *symbol*


:   Return `#t` if `symbol` is a function or a method. Otherwise return `#f`.

> 如果符号是一个函数或方法，则返回#t。否则返回#f。

```
<!-- -->
```

Scheme Procedure: **symbol-variable?** *symbol*

:   Return `#t` if `symbol` is a variable. Otherwise return `#f`.

```
<!-- -->
```

*


:   Compute the value of `symbol` is invalid, then an exception is thrown.

> 计算无效的`符号`值时会抛出异常。

```
<!-- -->
```

*


:   This function searches for a symbol by name. The search scope can be restricted to the parameters defined in the optional domain and block arguments.

> 这个函数通过名称搜索符号。搜索范围可以通过可选的域和块参数进行限制。

```
`name` argument must be a domain constant defined in the `(gdb)` module and described later in this chapter.

The result is a list of two elements. The first element is a `<gdb:symbol>` object or `#f` if the symbol is not found. If the symbol is found, the second element is `#t` if the symbol is a field of a method's object (e.g., `this` in C++), otherwise it is `#f`. If the symbol is not found, the second element is `#f`.
```

```
<!-- -->
```

*


:   This function searches for a global symbol by name. The search scope can be restricted by the domain argument.

> 这个函数通过名称搜索全局符号。搜索范围可以通过domain参数来限制。

```
`name` argument must be a domain constant defined in the `(gdb)` module and described later in this chapter.

The result is a `<gdb:symbol>` object or `#f` if the symbol is not found.
```


The available domain categories in `<gdb:symbol>` are represented as constants in the `(gdb)` module:

> `<gdb:symbol>`模块中表示可用域类别的常量在`(gdb)`模块中：

`SYMBOL_UNDEF_DOMAIN`


:   This is used when a domain has not been discovered or none of the following domains apply. This usually indicates an error either in the symbol information or in [GDB]'s handling of symbols.

> 这通常表示符号信息中出现错误，或者[GDB]处理符号时出现错误，当域未被发现或者以下域都不适用时会使用这个。

`SYMBOL_VAR_DOMAIN`


:   This domain contains variables, function names, typedef names and enum type values.

> 这个域包含变量、函数名称、类型定义名称和枚举类型值。

`SYMBOL_STRUCT_DOMAIN`

:   This domain holds struct, union and enum type names.

`SYMBOL_LABEL_DOMAIN`

:   This domain contains names of labels (for gotos).

`SYMBOL_VARIABLES_DOMAIN`


:   This domain holds a subset of the `SYMBOLS_VAR_DOMAIN`; it contains everything minus functions and types.

> 这个域包含`SYMBOLS_VAR_DOMAIN`的一个子集；它包含除函数和类型之外的所有内容。

`SYMBOL_FUNCTIONS_DOMAIN`

:   This domain contains all functions.

`SYMBOL_TYPES_DOMAIN`

:   This domain contains all types.


The available address class categories in `<gdb:symbol>` are represented as constants in the `gdb` module:

> `<gdb:symbol>`中可用的地址类别由`gdb`模块中的常量表示。

`SYMBOL_LOC_UNDEF`


:   If this is returned by address class, it indicates an error either in the symbol information or in [GDB]'s handling of symbols.

> 如果地址类返回此内容，则表明符号信息中或GDB处理符号中存在错误。

`SYMBOL_LOC_CONST`

:   Value is constant int.

`SYMBOL_LOC_STATIC`

:   Value is at a fixed address.

`SYMBOL_LOC_REGISTER`

:   Value is in a register.

`SYMBOL_LOC_ARG`


:   Value is an argument. This value is at the offset stored within the symbol inside the frame's argument list.

> 值是一个参数。这个值存储在符号内部帧参数列表中的偏移量中。

`SYMBOL_LOC_REF_ARG`


:   Value address is stored in the frame's argument list. Just like `LOC_ARG` except that the value's address is stored at the offset, not the value itself.

> 地址值存储在帧的参数列表中。就像`LOC_ARG`一样，只是偏移处存储的是地址值而不是实际值。

`SYMBOL_LOC_REGPARM_ADDR`


:   Value is a specified register. Just like `LOC_REGISTER` except the register holds the address of the argument instead of the argument itself.

> 值是一个指定的寄存器。就像`LOC_REGISTER`一样，只是寄存器保存的是参数的地址而不是参数本身。

`SYMBOL_LOC_LOCAL`

:   Value is a local variable.

`SYMBOL_LOC_TYPEDEF`


:   Value not used. Symbols in the domain `SYMBOL_STRUCT_DOMAIN` all have this class.

> 值未使用。域`SYMBOL_STRUCT_DOMAIN`中的符号都具有此类。

`SYMBOL_LOC_BLOCK`

:   Value is a block.

`SYMBOL_LOC_CONST_BYTES`

:   Value is a byte-sequence.

`SYMBOL_LOC_UNRESOLVED`


:   Value is at a fixed address, but the address of the variable has to be determined from the minimal symbol table whenever the variable is referenced.

> 值固定在一个地址，但是变量的地址必须从最小符号表中确定，每当引用变量时。

`SYMBOL_LOC_OPTIMIZED_OUT`

:   The value does not actually exist in the program.

`SYMBOL_LOC_COMPUTED`

:   The value's address is a computed location.

---

::: header
Next: [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)]
:::
