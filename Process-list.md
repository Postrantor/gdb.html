---
tip: translate by openai@2023-06-24 01:22:42
...
---
description: Process list (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Process list (Debugging with GDB)
lang: en
resource-type: document
title: Process list (Debugging with GDB)
---
::: header

Up: [Operating System Information](Operating-System-Information.html#Operating-System-Information)]

> 上：[操作系统信息](Operating-System-Information.html#Operating-System-Information)
:::

---

### H.1 Process list

When requesting the process list, the `annex`.

An example document is:

::: smallexample

```bash
<?xml version="1.0"?>
<!DOCTYPE target SYSTEM "osdata.dtd">
<osdata type="processes">
  <item>
    <column name="pid">1</column>
    <column name="user">root</column>
    <column name="command">/sbin/init</column>
    <column name="cores">1,2,3</column>
  </item>
</osdata>
```

:::

Each item should include a column whose name is '`pid` currently ignores.
