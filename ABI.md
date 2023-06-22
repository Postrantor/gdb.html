---
description: ABI (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: ABI (Debugging with GDB)
lang: en
resource-type: document
title: ABI (Debugging with GDB)
---
::: header
Next: [Auto-loading](Auto_002dloading.html#Auto_002dloading)]
:::

---

### 22.7 Configuring the Current ABI

[GDB]'s view of the current ABI.

One [GDB]/Linux) which does not have the same identifying marks that the standard C library for your platform provides.

When [GDB] C library. The "Newlib" OS ABI can be selected by `set osabi Newlib`.

`show osabi`

:   Show the OS ABI currently in use.

`set osabi`

:   With no argument, show the list of registered available OS ABI's.

`set osabi abi`

:   Set the current OS ABI to `abi`.

Generally, the way that an argument of type `float` is passed to a function depends on whether the function is prototyped. For a prototyped (i.e. ANSI/ISO style) function, `float` arguments are passed unchanged, according to the architecture's convention for `float`. For unprototyped (i.e. K&R style) functions, `float` arguments are first promoted to type `double` and then passed.

Unfortunately, some forms of debug information do not reliably indicate whether a function is prototyped. If [GDB].

`set coerce-float-to-double`

`set coerce-float-to-double on`

Arguments of type `float` will be promoted to `double` when passed to an unprototyped function. This is the default setting.

`set coerce-float-to-double off`

Arguments of type `float` will be passed directly to unprototyped functions.

`show coerce-float-to-double`

Show the current setting of promoting `float` to `double`.

[GDB] which ABI to use. Currently supported ABI's include "gnu-v2", for `g++` versions before 3.0, "gnu-v3", for `g++` versions 3.0 and later, and "hpaCC" for the HP ANSI C++ compiler. Other C++ compilers may use the "gnu-v2" or "gnu-v3" ABI's as well. The default setting is "auto".

`show cp-abi`

:   Show the C++ ABI currently in use.

`set cp-abi`

:   With no argument, show the list of supported C++ ABI's.

`set cp-abi abi`
`set cp-abi auto`

:   Set the current C++ ABI to `abi`, or return to automatic detection.

---

::: header
Next: [Auto-loading](Auto_002dloading.html#Auto_002dloading)]
:::
