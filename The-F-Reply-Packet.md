---
tip: translate by openai@2023-06-23 14:27:22
...
---
description: The F Reply Packet (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: The F Reply Packet (Debugging with GDB)
lang: en
resource-type: document
title: The F Reply Packet (Debugging with GDB)
---
::: header
Next: [The Ctrl-C Message](The-Ctrl_002dC-Message.html#The-Ctrl_002dC-Message)]
:::

---

#### E.13.4 The `F` Reply Packet


The `F` reply packet has the following format:

> `F` 应答包的格式如下：


'`Fretcode,errno,Ctrl-C flag;call-specific attachment`'

> 'Fretcode、errno、Ctrl-C 标志；特定调用的附件。


:   `retcode` is the return code of the system call as hexadecimal value.

> `retcode` 是以十六进制值表示的系统调用的返回码。

```
`errno` is the `errno` set by the call, in protocol-specific representation. This parameter can be omitted if the call was successful.

`Ctrl-C flag`':

::: smallexample
``` smallexample
F0,0,C
```

:::

or, if the call was interrupted before the host call has been performed:

::: smallexample

```bash
F-1,4,C
```

:::

assuming 4 is the protocol-specific representation of `EINTR`.

```
```
