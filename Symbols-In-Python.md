---
tip: translate by openai@2023-06-24 03:33:05
...
---
description: Symbols In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Symbols In Python (Debugging with GDB)
lang: en
resource-type: document
title: Symbols In Python (Debugging with GDB)
---
::: header
Next: [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)]
:::

---

#### 23.3.2.28 Python representation of Symbols

[GDB] with the `gdb.Symbol` object.

The following symbol-related functions are available in the `gdb` module:

)*


:   This function searches for a symbol by name. The search scope can be restricted to the parameters defined in the optional domain and block arguments.

> 这个功能通过名称搜索符号。可以通过可选的域和块参数来限制搜索范围。

```
`name` argument must be a domain constant defined in the `gdb` module and described later in this chapter.

The result is a tuple of two elements. The first element is a `gdb.Symbol` object or `None` if the symbol is not found. If the symbol is found, the second element is `True` if the symbol is a field of a method's object (e.g., `this` in C++), otherwise it is `False`. If the symbol is not found, the second element is `False`.
```

)*


:   This function searches for a global symbol by name. The search scope can be restricted to by the domain argument.

> 这个函数通过名称搜索全局符号。搜索范围可以通过域参数进行限制。

```
`name` argument must be a domain constant defined in the `gdb` module and described later in this chapter.

The result is a `gdb.Symbol` object or `None` if the symbol is not found.
```

)*


:   This function searches for a global symbol with static linkage by name. The search scope can be restricted to by the domain argument.

> 这个函数通过名称搜索具有静态链接的全局符号。搜索范围可以通过domain参数限制。

```
`name` argument must be a domain constant defined in the `gdb` module and described later in this chapter.

The result is a `gdb.Symbol` object or `None` if the symbol is not found.

Note that this function will not find function-scoped static variables. To look up such variables, iterate over the variables of the function's `gdb.Block` and check that `block.addr_class` is `gdb.SYMBOL_LOC_STATIC`.

There can be multiple global symbols with static linkage with the same name. This function will only return the first matching symbol that it finds. Which symbol is found depends on where [GDB] will search all object files in the order they appear in the debug information.
```

)*


:   Similar to `gdb.lookup_static_symbol`, this function searches for global symbols with static linkage by name, and optionally restricted by the domain argument. However, this function returns a list of all matching symbols found, not just the first one.

> 类似于`gdb.lookup_static_symbol`，此函数通过名称搜索具有静态链接的全局符号，并可选择性地受域参数的限制。但是，此函数返回找到的所有匹配符号的列表，而不仅仅是第一个。

```
`name` argument must be a domain constant defined in the `gdb` module and described later in this chapter.

The result is a list of `gdb.Symbol` objects which could be empty if no matching symbols were found.

Note that this function will not find function-scoped static variables. To look up such variables, iterate over the variables of the function's `gdb.Block` and check that `block.addr_class` is `gdb.SYMBOL_LOC_STATIC`.
```

A `gdb.Symbol` object has the following attributes:

Variable: **Symbol.type**


:   The type of the symbol or `None` if no type is recorded. This attribute is represented as a `gdb.Type` object. See [Types In Python](Types-In-Python.html#Types-In-Python). This attribute is not writable.

> 这个符号的类型，如果没有记录，则为`None`。这个属性用`gdb.Type`对象表示。请参阅[Python中的类型](Types-In-Python.html#Types-In-Python)。这个属性是不可写的。

```
<!-- -->
```

Variable: **Symbol.symtab**


:   The symbol table in which the symbol appears. This attribute is represented as a `gdb.Symtab` object. See [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python). This attribute is not writable.

> 这个符号出现的符号表。这个属性用`gdb.Symtab`对象表示。请参见[Python中的符号表](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)。这个属性是不可写的。

```
<!-- -->
```

Variable: **Symbol.line**


:   The line number in the source code at which the symbol was defined. This is an integer.

> 在源代码中定义该符号的行号，这是一个整数。

```
<!-- -->
```

Variable: **Symbol.name**

:   The name of the symbol as a string. This attribute is not writable.

```
<!-- -->
```

Variable: **Symbol.linkage_name**


:   The name of the symbol, as used by the linker (i.e., may be mangled). This attribute is not writable.

> 名称，按链接器使用（即可能被编码）。此属性不可写。

```
<!-- -->
```

Variable: **Symbol.print_name**


:   The name of the symbol in a form suitable for output. This is either `name` or `linkage_name`, depending on whether the user asked [GDB] to display demangled or mangled names.

> 这个符号的名称以输出适当的形式提供。这取决于用户是否要求[GDB]显示解码或混淆的名称，这可以是`name`或`linkage_name`。

```
<!-- -->
```

Variable: **Symbol.addr_class**


:   The address class of the symbol. This classifies how to find the value of a symbol. Each address class is a constant defined in the `gdb` module and described later in this chapter.

> 这个符号的地址类。这可以分类如何找到一个符号的值。每个地址类都是`gdb`模块中定义的常量，稍后在本章中有描述。

```
<!-- -->
```

Variable: **Symbol.needs_frame**


:   This is `True` if evaluating this symbol's value requires a frame (see [Frames In Python](Frames-In-Python.html#Frames-In-Python)) and `False` otherwise. Typically, local variables will require a frame, but other symbols will not.

> 这个符号的值需要一个框架来评估时，这是真的（参见[Python中的框架]（Frames-In-Python.html#Frames-In-Python）），否则为假。通常，局部变量需要一个框架，但其他符号不需要。

```
<!-- -->
```

Variable: **Symbol.is_argument**

:   `True` if the symbol is an argument of a function.

```
<!-- -->
```

Variable: **Symbol.is_constant**

:   `True` if the symbol is a constant.

```
<!-- -->
```

Variable: **Symbol.is_function**

:   `True` if the symbol is a function or a method.

```
<!-- -->
```

Variable: **Symbol.is_variable**

:   `True` if the symbol is a variable.

A `gdb.Symbol` object has the following methods:

Function: **Symbol.is_valid** *()*


:   Returns `True` if the `gdb.Symbol` object is valid, `False` if not. A `gdb.Symbol` object can become invalid if the symbol it refers to does not exist in [GDB] any longer. All other `gdb.Symbol` methods will throw an exception if it is invalid at the time the method is called.

> 返回`True`如果`gdb.Symbol`对象有效，如果没有则返回`False`。如果它所指的符号在[GDB]中不再存在，`gdb.Symbol`对象可能会变得无效。如果调用该方法时它是无效的，其他所有`gdb.Symbol`方法都会抛出异常。

```
<!-- -->
```

)*


:   Compute the value of the symbol, as a `gdb.Value`. For functions, this computes the address of the function, cast to the appropriate type. If the symbol requires a frame in order to compute its value, then `frame` is invalid, then this method will throw an exception.

> 计算符号的值，作为一个`gdb.Value`。对于函数，这将计算函数的地址，转换为适当的类型。如果符号需要一个框架来计算其值，然后`frame`是无效的，那么这种方法将抛出异常。


The available domain categories in `gdb.Symbol` are represented as constants in the `gdb` module:

> `gdb.Symbol`中可用的域类别由`gdb`模块中的常量表示。

`gdb.SYMBOL_UNDEF_DOMAIN`


This is used when a domain has not been discovered or none of the following domains apply. This usually indicates an error either in the symbol information or in [GDB]'s handling of symbols.

> 这通常表示符号信息中出现错误，或者[GDB]处理符号时出现错误，当域未被发现或没有以下域适用时会使用它。

`gdb.SYMBOL_VAR_DOMAIN`


This domain contains variables, function names, typedef names and enum type values.

> 这个域包含变量、函数名称、类型定义名称和枚举类型值。

`gdb.SYMBOL_STRUCT_DOMAIN`

This domain holds struct, union and enum type names.

`gdb.SYMBOL_LABEL_DOMAIN`

This domain contains names of labels (for gotos).

`gdb.SYMBOL_MODULE_DOMAIN`

This domain contains names of Fortran module types.

`gdb.SYMBOL_COMMON_BLOCK_DOMAIN`

This domain contains names of Fortran common blocks.


The available address class categories in `gdb.Symbol` are represented as constants in the `gdb` module:

> 在`gdb.Symbol`中可用的地址类别由`gdb`模块中的常量表示：

`gdb.SYMBOL_LOC_UNDEF`


If this is returned by address class, it indicates an error either in the symbol information or in [GDB]'s handling of symbols.

> 如果地址类返回这个，它表明符号信息中或GDB处理符号时出现了错误。

`gdb.SYMBOL_LOC_CONST`

Value is constant int.

`gdb.SYMBOL_LOC_STATIC`

Value is at a fixed address.

`gdb.SYMBOL_LOC_REGISTER`

Value is in a register.

`gdb.SYMBOL_LOC_ARG`


Value is an argument. This value is at the offset stored within the symbol inside the frame's argument list.

> 值是一个参数。这个值存储在符号内的框架参数列表中的偏移量中。

`gdb.SYMBOL_LOC_REF_ARG`


Value address is stored in the frame's argument list. Just like `LOC_ARG` except that the value's address is stored at the offset, not the value itself.

> 在帧参数列表中存储了值地址，就像`LOC_ARG`一样，只是偏移量存储的是地址而不是值本身。

`gdb.SYMBOL_LOC_REGPARM_ADDR`


Value is a specified register. Just like `LOC_REGISTER` except the register holds the address of the argument instead of the argument itself.

> 值是一个指定的寄存器。就像`LOC_REGISTER`一样，只是寄存器保存的是参数的地址而不是参数本身。

`gdb.SYMBOL_LOC_LOCAL`

Value is a local variable.

`gdb.SYMBOL_LOC_TYPEDEF`


Value not used. Symbols in the domain `SYMBOL_STRUCT_DOMAIN` all have this class.

> 值未使用。在域`SYMBOL_STRUCT_DOMAIN`中的符号都具有此类。

`gdb.SYMBOL_LOC_LABEL`

Value is a label.

`gdb.SYMBOL_LOC_BLOCK`

Value is a block.

`gdb.SYMBOL_LOC_CONST_BYTES`

Value is a byte-sequence.

`gdb.SYMBOL_LOC_UNRESOLVED`


Value is at a fixed address, but the address of the variable has to be determined from the minimal symbol table whenever the variable is referenced.

> 值固定在一个地址上，但是每次引用变量时，必须从最小符号表中确定变量的地址。

`gdb.SYMBOL_LOC_OPTIMIZED_OUT`

The value does not actually exist in the program.

`gdb.SYMBOL_LOC_COMPUTED`

The value's address is a computed location.

`gdb.SYMBOL_LOC_COMMON_BLOCK`


The value's address is a symbol. This is only used for Fortran common blocks.

> 地址的值是一个符号。这只用于Fortran公共块。

---

::: header
Next: [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)]
:::
