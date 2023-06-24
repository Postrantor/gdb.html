---
tip: translate by openai@2023-06-23 16:53:02
...
---
description: ABI (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: ABI (Debugging with GDB)
lang: en
resource-type: document
title: ABI (Debugging with GDB)
-------------------------------

::: header
Next: [Auto-loading](Auto_002dloading.html#Auto_002dloading)]
:::

---

### 22.7 Configuring the Current ABI

[GDB]'s view of the current ABI.

> GDB 对当前 ABI 的视图。

One [GDB]/Linux) which does not have the same identifying marks that the standard C library for your platform provides.

> 一个没有和您的平台标准 C 库提供的相同标识的[GDB]/Linux)。

When [GDB] C library. The "Newlib" OS ABI can be selected by `set osabi Newlib`.

> 当使用 GDB C 库时，可以通过输入 `set osabi Newlib` 来选择“Newlib” OS ABI。

`show osabi`

:   Show the OS ABI currently in use.

> 显示当前正在使用的操作系统 ABI。

`set osabi`

:   With no argument, show the list of registered available OS ABI's.

> 没有参数，显示已注册的可用操作系统 ABI 列表。

`set osabi abi`

:   Set the current OS ABI to `abi`.

> 将当前操作系统 ABI 设置为 `abi`。

Generally, the way that an argument of type `float` is passed to a function depends on whether the function is prototyped. For a prototyped (i.e. ANSI/ISO style) function, `float` arguments are passed unchanged, according to the architecture's convention for `float`. For unprototyped (i.e. K&R style) functions, `float` arguments are first promoted to type `double` and then passed.

> 一般来说，float 类型的参数传递给函数的方式取决于函数是否有原型。对于有原型（即 ANSI/ISO 样式）的函数，float 参数根据架构的 float 约定而不变地传递。对于没有原型（即 K&R 样式）的函数，float 参数首先会被提升为 double 类型，然后再传递。

Unfortunately, some forms of debug information do not reliably indicate whether a function is prototyped. If [GDB].

> 不幸的是，有些调试信息形式不能可靠地表明函数是否有原型。如果[GDB]。

`set coerce-float-to-double`

`set coerce-float-to-double on`

Arguments of type `float` will be promoted to `double` when passed to an unprototyped function. This is the default setting.

> 当将类型为 `float` 的参数传递给未定义原型的函数时，它将被提升为 `double`。这是默认设置。

`set coerce-float-to-double off`

Arguments of type `float` will be passed directly to unprototyped functions.

> 浮點型的參數將直接傳遞給未被原型定義的函數。

`show coerce-float-to-double`

Show the current setting of promoting `float` to `double`.

> 显示将浮点数提升为双精度的当前设置。

[GDB] which ABI to use. Currently supported ABI's include "gnu-v2", for `g++` versions before 3.0, "gnu-v3", for `g++` versions 3.0 and later, and "hpaCC" for the HP ANSI C++ compiler. Other C++ compilers may use the "gnu-v2" or "gnu-v3" ABI's as well. The default setting is "auto".

> GDB 使用哪个 ABI？目前支持的 ABI 包括“gnu-v2”，用于 3.0 以前的 g++ 版本，“gnu-v3”，用于 3.0 及以后的 g++ 版本，以及 HP ANSI C++ 编译器的“hpaCC”。其他 C++ 编译器也可以使用“gnu-v2”或“gnu-v3”ABI。默认设置为“auto”。

`show cp-abi`

:   Show the C++ ABI currently in use.

> 显示当前使用的 C++ ABI。

`set cp-abi`

:   With no argument, show the list of supported C++ ABI's.

> 没有参数时，显示支持的 C++ ABI 列表。

`set cp-abi abi`
`set cp-abi auto`

:   Set the current C++ ABI to `abi`, or return to automatic detection.

> 将当前的 C++ ABI 设置为 `abi`，或者返回自动检测。

---

::: header
Next: [Auto-loading](Auto_002dloading.html#Auto_002dloading)]
:::
