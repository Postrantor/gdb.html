---
tip: translate by openai@2023-06-23 13:15:45
...
---
description: Show (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Show (Debugging with GDB)
lang: en
resource-type: document
title: Show (Debugging with GDB)
---
::: header
Next: [Checks](Checks.html#Checks)]
:::

---

### 15.2 Displaying the Language


The following commands help you find out which language is the working language, and also what language source files were written in.

> 以下命令可以帮助您查找当前使用的语言以及源文件所使用的语言。

`show language`

:

```
Display the current working language. This is the language you can use with commands such as `print` to build and compute expressions that may involve variables in your program.
```

`info frame`

:

```
Display the source language for this frame. This language becomes the working language if you use an identifier from this frame. See [Information about a Frame](Frame-Info.html#Frame-Info), to identify the other information listed here.
```

`info source`

:

```
Display the source language of this source file. See [Examining the Symbol Table](Symbols.html#Symbols), to identify the other information listed here.
```


In unusual circumstances, you may have source files with extensions not in the standard list. You can then set the extension associated with a language explicitly:

> 在不寻常的情况下，您可能会有具有不在标准列表中的扩展名的源文件。然后，您可以明确设置与语言关联的扩展名：

`set extension-language ext language`

:

```
Tell [GDB].
```

`info extensions`

:

```
List all the filename extensions and the associated languages.
```
