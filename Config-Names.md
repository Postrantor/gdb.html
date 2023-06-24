---
tip: translate by openai@2023-06-23 19:28:51
...
---
description: Config Names (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Config Names (Debugging with GDB)
lang: en
resource-type: document
title: Config Names (Debugging with GDB)
---
::: header
Next: [Configure Options](Configure-Options.html#Configure-Options)]
:::

---

### C.4 Specifying Names for Hosts and Targets


The specifications used for hosts and targets in the `configure` script are based on a three-part naming scheme, but some short predefined aliases are also supported. The full naming scheme encodes three pieces of information in the following pattern:

> 配置脚本中用于主机和目标的规格基于三部分命名方案，但也支持一些简短的预定义别名。完整的命名方案以以下模式编码三个信息：

::: smallexample

```bash
architecture-vendor-os
```

:::

For example, you can use the alias `sun4` as a `host`'.


The `configure` calls the Bourne shell script `config.sub` to map abbreviations to full names; you can read the script, if you wish, or you can use it to test your guesses on abbreviations---for example:

> 配置调用 Bourne Shell 脚本config.sub将缩写映射为完整名称；您可以阅读脚本，如果您愿意，也可以使用它来测试您对缩写的猜测---例如：

::: smallexample

```bash
% sh config.sub i386-linux
i386-pc-linux-gnu
% sh config.sub alpha-linux
alpha-unknown-linux-gnu
% sh config.sub hp9k700
hppa1.1-hp-hpux
% sh config.sub sun4
sparc-sun-sunos4.1.1
% sh config.sub sun3
m68k-sun-sunos4.1.1
% sh config.sub i986v
Invalid configuration `i986v': machine `i986v' not recognized
```

:::

`config.sub` is also distributed in the [GDB], for version 14.0.50.20230622-git).
