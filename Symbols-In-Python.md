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

```
`name` argument must be a domain constant defined in the `gdb` module and described later in this chapter.

The result is a tuple of two elements. The first element is a `gdb.Symbol` object or `None` if the symbol is not found. If the symbol is found, the second element is `True` if the symbol is a field of a method's object (e.g., `this` in C++), otherwise it is `False`. If the symbol is not found, the second element is `False`.
```

)*

:   This function searches for a global symbol by name. The search scope can be restricted to by the domain argument.

```
`name` argument must be a domain constant defined in the `gdb` module and described later in this chapter.

The result is a `gdb.Symbol` object or `None` if the symbol is not found.
```

)*

:   This function searches for a global symbol with static linkage by name. The search scope can be restricted to by the domain argument.

```
`name` argument must be a domain constant defined in the `gdb` module and described later in this chapter.

The result is a `gdb.Symbol` object or `None` if the symbol is not found.

Note that this function will not find function-scoped static variables. To look up such variables, iterate over the variables of the function's `gdb.Block` and check that `block.addr_class` is `gdb.SYMBOL_LOC_STATIC`.

There can be multiple global symbols with static linkage with the same name. This function will only return the first matching symbol that it finds. Which symbol is found depends on where [GDB] will search all object files in the order they appear in the debug information.
```

)*

:   Similar to `gdb.lookup_static_symbol`, this function searches for global symbols with static linkage by name, and optionally restricted by the domain argument. However, this function returns a list of all matching symbols found, not just the first one.

```
`name` argument must be a domain constant defined in the `gdb` module and described later in this chapter.

The result is a list of `gdb.Symbol` objects which could be empty if no matching symbols were found.

Note that this function will not find function-scoped static variables. To look up such variables, iterate over the variables of the function's `gdb.Block` and check that `block.addr_class` is `gdb.SYMBOL_LOC_STATIC`.
```

A `gdb.Symbol` object has the following attributes:

Variable: **Symbol.type**

:   The type of the symbol or `None` if no type is recorded. This attribute is represented as a `gdb.Type` object. See [Types In Python](Types-In-Python.html#Types-In-Python). This attribute is not writable.

```
<!-- -->
```

Variable: **Symbol.symtab**

:   The symbol table in which the symbol appears. This attribute is represented as a `gdb.Symtab` object. See [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python). This attribute is not writable.

```
<!-- -->
```

Variable: **Symbol.line**

:   The line number in the source code at which the symbol was defined. This is an integer.

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

```
<!-- -->
```

Variable: **Symbol.print_name**

:   The name of the symbol in a form suitable for output. This is either `name` or `linkage_name`, depending on whether the user asked [GDB] to display demangled or mangled names.

```
<!-- -->
```

Variable: **Symbol.addr_class**

:   The address class of the symbol. This classifies how to find the value of a symbol. Each address class is a constant defined in the `gdb` module and described later in this chapter.

```
<!-- -->
```

Variable: **Symbol.needs_frame**

:   This is `True` if evaluating this symbol's value requires a frame (see [Frames In Python](Frames-In-Python.html#Frames-In-Python)) and `False` otherwise. Typically, local variables will require a frame, but other symbols will not.

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

```
<!-- -->
```

)*

:   Compute the value of the symbol, as a `gdb.Value`. For functions, this computes the address of the function, cast to the appropriate type. If the symbol requires a frame in order to compute its value, then `frame` is invalid, then this method will throw an exception.

The available domain categories in `gdb.Symbol` are represented as constants in the `gdb` module:

`gdb.SYMBOL_UNDEF_DOMAIN`

This is used when a domain has not been discovered or none of the following domains apply. This usually indicates an error either in the symbol information or in [GDB]'s handling of symbols.

`gdb.SYMBOL_VAR_DOMAIN`

This domain contains variables, function names, typedef names and enum type values.

`gdb.SYMBOL_STRUCT_DOMAIN`

This domain holds struct, union and enum type names.

`gdb.SYMBOL_LABEL_DOMAIN`

This domain contains names of labels (for gotos).

`gdb.SYMBOL_MODULE_DOMAIN`

This domain contains names of Fortran module types.

`gdb.SYMBOL_COMMON_BLOCK_DOMAIN`

This domain contains names of Fortran common blocks.

The available address class categories in `gdb.Symbol` are represented as constants in the `gdb` module:

`gdb.SYMBOL_LOC_UNDEF`

If this is returned by address class, it indicates an error either in the symbol information or in [GDB]'s handling of symbols.

`gdb.SYMBOL_LOC_CONST`

Value is constant int.

`gdb.SYMBOL_LOC_STATIC`

Value is at a fixed address.

`gdb.SYMBOL_LOC_REGISTER`

Value is in a register.

`gdb.SYMBOL_LOC_ARG`

Value is an argument. This value is at the offset stored within the symbol inside the frame's argument list.

`gdb.SYMBOL_LOC_REF_ARG`

Value address is stored in the frame's argument list. Just like `LOC_ARG` except that the value's address is stored at the offset, not the value itself.

`gdb.SYMBOL_LOC_REGPARM_ADDR`

Value is a specified register. Just like `LOC_REGISTER` except the register holds the address of the argument instead of the argument itself.

`gdb.SYMBOL_LOC_LOCAL`

Value is a local variable.

`gdb.SYMBOL_LOC_TYPEDEF`

Value not used. Symbols in the domain `SYMBOL_STRUCT_DOMAIN` all have this class.

`gdb.SYMBOL_LOC_LABEL`

Value is a label.

`gdb.SYMBOL_LOC_BLOCK`

Value is a block.

`gdb.SYMBOL_LOC_CONST_BYTES`

Value is a byte-sequence.

`gdb.SYMBOL_LOC_UNRESOLVED`

Value is at a fixed address, but the address of the variable has to be determined from the minimal symbol table whenever the variable is referenced.

`gdb.SYMBOL_LOC_OPTIMIZED_OUT`

The value does not actually exist in the program.

`gdb.SYMBOL_LOC_COMPUTED`

The value's address is a computed location.

`gdb.SYMBOL_LOC_COMMON_BLOCK`

The value's address is a symbol. This is only used for Fortran common blocks.

---

::: header
Next: [Symbol Tables In Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)]
:::
