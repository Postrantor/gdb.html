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

Scheme Procedure: **symbol?** *object*

:   Return `#t` if `object` is an object of type `<gdb:symbol>`. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **symbol-valid?** *symbol*

:   Return `#t` if the `<gdb:symbol>` object is valid, `#f` if not. A `<gdb:symbol>` object can become invalid if the symbol it refers to does not exist in [GDB] any longer. All other `<gdb:symbol>` procedures will throw an exception if it is invalid at the time the procedure is called.

```
<!-- -->
```

Scheme Procedure: **symbol-type** *symbol*

:   Return the type of `symbol` or `#f` if no type is recorded. The result is an object of type `<gdb:type>`. See [Types In Guile](Types-In-Guile.html#Types-In-Guile).

```
<!-- -->
```

Scheme Procedure: **symbol-symtab** *symbol*

:   Return the symbol table in which `symbol` appears. The result is an object of type `<gdb:symtab>`. See [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile).

```
<!-- -->
```

Scheme Procedure: **symbol-line** *symbol*

:   Return the line number in the source code at which `symbol` was defined. This is an integer.

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

```
<!-- -->
```

Scheme Procedure: **symbol-needs-frame?** *symbol*

:   Return `#t` if evaluating `symbol`'s value requires a frame (see [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile)) and `#f` otherwise. Typically, local variables will require a frame, but other symbols will not.

```
<!-- -->
```

Scheme Procedure: **symbol-argument?** *symbol*

:   Return `#t` if `symbol` is an argument of a function. Otherwise return `#f`.

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

```
<!-- -->
```

*

:   This function searches for a symbol by name. The search scope can be restricted to the parameters defined in the optional domain and block arguments.

```
`name` argument must be a domain constant defined in the `(gdb)` module and described later in this chapter.

The result is a list of two elements. The first element is a `<gdb:symbol>` object or `#f` if the symbol is not found. If the symbol is found, the second element is `#t` if the symbol is a field of a method's object (e.g., `this` in C++), otherwise it is `#f`. If the symbol is not found, the second element is `#f`.
```

```
<!-- -->
```

*

:   This function searches for a global symbol by name. The search scope can be restricted by the domain argument.

```
`name` argument must be a domain constant defined in the `(gdb)` module and described later in this chapter.

The result is a `<gdb:symbol>` object or `#f` if the symbol is not found.
```

The available domain categories in `<gdb:symbol>` are represented as constants in the `(gdb)` module:

`SYMBOL_UNDEF_DOMAIN`

:   This is used when a domain has not been discovered or none of the following domains apply. This usually indicates an error either in the symbol information or in [GDB]'s handling of symbols.

`SYMBOL_VAR_DOMAIN`

:   This domain contains variables, function names, typedef names and enum type values.

`SYMBOL_STRUCT_DOMAIN`

:   This domain holds struct, union and enum type names.

`SYMBOL_LABEL_DOMAIN`

:   This domain contains names of labels (for gotos).

`SYMBOL_VARIABLES_DOMAIN`

:   This domain holds a subset of the `SYMBOLS_VAR_DOMAIN`; it contains everything minus functions and types.

`SYMBOL_FUNCTIONS_DOMAIN`

:   This domain contains all functions.

`SYMBOL_TYPES_DOMAIN`

:   This domain contains all types.

The available address class categories in `<gdb:symbol>` are represented as constants in the `gdb` module:

`SYMBOL_LOC_UNDEF`

:   If this is returned by address class, it indicates an error either in the symbol information or in [GDB]'s handling of symbols.

`SYMBOL_LOC_CONST`

:   Value is constant int.

`SYMBOL_LOC_STATIC`

:   Value is at a fixed address.

`SYMBOL_LOC_REGISTER`

:   Value is in a register.

`SYMBOL_LOC_ARG`

:   Value is an argument. This value is at the offset stored within the symbol inside the frame's argument list.

`SYMBOL_LOC_REF_ARG`

:   Value address is stored in the frame's argument list. Just like `LOC_ARG` except that the value's address is stored at the offset, not the value itself.

`SYMBOL_LOC_REGPARM_ADDR`

:   Value is a specified register. Just like `LOC_REGISTER` except the register holds the address of the argument instead of the argument itself.

`SYMBOL_LOC_LOCAL`

:   Value is a local variable.

`SYMBOL_LOC_TYPEDEF`

:   Value not used. Symbols in the domain `SYMBOL_STRUCT_DOMAIN` all have this class.

`SYMBOL_LOC_BLOCK`

:   Value is a block.

`SYMBOL_LOC_CONST_BYTES`

:   Value is a byte-sequence.

`SYMBOL_LOC_UNRESOLVED`

:   Value is at a fixed address, but the address of the variable has to be determined from the minimal symbol table whenever the variable is referenced.

`SYMBOL_LOC_OPTIMIZED_OUT`

:   The value does not actually exist in the program.

`SYMBOL_LOC_COMPUTED`

:   The value's address is a computed location.

---

::: header
Next: [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)]
:::
