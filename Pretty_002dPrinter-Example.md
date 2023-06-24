---
tip: translate by openai@2023-06-24 01:10:51
...
---
description: Pretty-Printer Example (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Pretty-Printer Example (Debugging with GDB)
lang: en
resource-type: document
title: Pretty-Printer Example (Debugging with GDB)
---
::: header
Next: [Pretty-Printer Commands](Pretty_002dPrinter-Commands.html#Pretty_002dPrinter-Commands)]
:::

---

#### 10.10.2 Pretty-Printer Example

Here is how a C++ `std::string` looks without a pretty-printer:

::: smallexample

```bash
(gdb) print s
$1 = {
  static npos = 4294967295, 
  _M_dataplus = {
    <std::allocator<char>> = {
      <__gnu_cxx::new_allocator<char>> = {
        <No data fields>}, <No data fields>
      },
    members of std::basic_string<char, std::char_traits<char>,
      std::allocator<char> >::_Alloc_hider:
    _M_p = 0x804a014 "abcd"
  }
}
```

:::

With a pretty-printer for `std::string` only the contents are printed:

::: smallexample

```bash
(gdb) print s
$2 = "abcd"
```

:::
