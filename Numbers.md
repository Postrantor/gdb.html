---
tip: translate by openai@2023-06-24 00:37:03
...
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

> 你可以在GDB中以八进制、十进制或十六进制输入数字，默认情况下是以十进制输入的；同样，没有特定格式时，数字的默认显示也是十进制。你可以使用下面描述的命令更改输入和输出的默认基数。

`set input-radix base`


Set the default base for numeric input. Supported choices for `base` are decimal 8, 10, or 16. The base must itself be specified either unambiguously or using the current input radix; for example, any of

> 设置数字输入的默认基数。支持`base`的选择有十进制8、10或16。基数必须本身是明确的，或者使用当前的输入进制；例如，任何的

::: smallexample

```bash
set input-radix 012
set input-radix 10.
set input-radix 0xa
```

:::


sets the input base to decimal. On the other hand, '`set input-radix 10`' is interpreted in hex, i.e. as 16 decimal, which doesn't change the radix.

> 设置输入基数为十进制。另一方面，“set input-radix 10”被解释为十六进制，即16进制，这不会改变基数。

`set output-radix base`


Set the default base for numeric display. Supported choices for `base` are decimal 8, 10, or 16. The base must itself be specified either unambiguously or using the current input radix.

> 设置数字显示的默认基数。 `base` 支持的选择有十进制 8、10 或 16。 基数必须明确指定，或者使用当前的输入基数。

`show input-radix`

Display the current default base for numeric input.

`show output-radix`

Display the current default base for numeric display.

`set radix [base]`

`show radix`


These commands set and show the default base for both input and output of numbers. `set radix` sets the radix of input and output to the same base; without an argument, it resets the radix back to its default value of 10.

> 这些命令设置和显示数字的默认基数。 `set radix`将输入和输出的基数设置为相同的基数；如果没有参数，它将基数重置回默认值10。

---

::: header
Next: [ABI](ABI.html#ABI)]
:::
