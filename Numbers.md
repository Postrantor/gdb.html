---
description: Numbers (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Numbers (Debugging with GDB)
lang: en
resource-type: document
title: Numbers (Debugging with GDB)
---
::: header
Next: [ABI](ABI.html#ABI)]
:::

---

### 22.6 Numbers

You can always enter numbers in octal, decimal, or hexadecimal in [GDB]' are, by default, entered in base 10; likewise, the default display for numbers---when no particular format is specified---is base 10. You can change the default base for both input and output with the commands described below.

`set input-radix base`

Set the default base for numeric input. Supported choices for `base` are decimal 8, 10, or 16. The base must itself be specified either unambiguously or using the current input radix; for example, any of

::: smallexample

```bash
set input-radix 012
set input-radix 10.
set input-radix 0xa
```

:::

sets the input base to decimal. On the other hand, '`set input-radix 10`' is interpreted in hex, i.e. as 16 decimal, which doesn't change the radix.

`set output-radix base`

Set the default base for numeric display. Supported choices for `base` are decimal 8, 10, or 16. The base must itself be specified either unambiguously or using the current input radix.

`show input-radix`

Display the current default base for numeric input.

`show output-radix`

Display the current default base for numeric display.

`set radix [base]`

`show radix`

These commands set and show the default base for both input and output of numbers. `set radix` sets the radix of input and output to the same base; without an argument, it resets the radix back to its default value of 10.

---

::: header
Next: [ABI](ABI.html#ABI)]
:::
