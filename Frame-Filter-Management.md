---
tip: translate by openai@2023-06-23 21:22:57
...
---
description: Frame Filter Management (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frame Filter Management (Debugging with GDB)
lang: en
resource-type: document
title: Frame Filter Management (Debugging with GDB)
---
::: header
Previous: [Frame Apply](Frame-Apply.html#Frame-Apply)]
:::

---

### 8.6 Management of Frame Filters.


Frame filters are Python based utilities to manage and decorate the output of frames. See [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API), for further information.

> 框架过滤器是基于Python的实用程序，用于管理和装饰框架的输出。有关更多信息，请参见[框架过滤器API](Frame-Filter-API.html#Frame-Filter-API)。


Managing frame filters is performed by several commands available within [GDB], detailed here.

> 在[GDB]中可以使用几个命令来管理帧过滤器，详情参见此处。

`info frame-filter`


Print a list of installed frame filters from all dictionaries, showing their name, priority and enabled status.

> 打印出所有字典中安装的框架过滤器的列表，显示它们的名称、优先级和启用状态。

`disable frame-filter filter-dictionary filter-name`


Disable a frame filter in the dictionary matching `filter-dictionary`. A disabled frame-filter is not deleted, it may be enabled again later.

> 在字典匹配'filter-dictionary'中禁用框架过滤器。禁用的框架过滤器不会被删除，可以稍后再次启用。

`enable frame-filter filter-dictionary filter-name`

Enable a frame filter in the dictionary matching `filter-dictionary`.

Example:

::: smallexample

```bash
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      No       PrimaryFunctionFilter
  100       Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       Yes      BuildProgramFilter

(gdb) disable frame-filter /build/test BuildProgramFilter
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      No       PrimaryFunctionFilter
  100       Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       No       BuildProgramFilter

(gdb) enable frame-filter global PrimaryFunctionFilter
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      Yes      PrimaryFunctionFilter
  100       Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       No       BuildProgramFilter
```

:::

`set frame-filter priority filter-dictionary filter-name priority`

Set the `priority` is an integer.

`show frame-filter priority filter-dictionary filter-name`


Show the `priority` may be `global`, `progspace` or the name of the object file where the frame filter dictionary resides.

> 显示优先级可以是全局的、progspace的，或者是存放帧过滤字典的对象文件的名称。

Example:

::: smallexample

```bash
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      Yes      PrimaryFunctionFilter
  100       Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       No       BuildProgramFilter

(gdb) set frame-filter priority global Reverse 50
(gdb) info frame-filter

global frame-filters:
  Priority  Enabled  Name
  1000      Yes      PrimaryFunctionFilter
  50        Yes      Reverse

progspace /build/test frame-filters:
  Priority  Enabled  Name
  100       Yes      ProgspaceFilter

objfile /build/test frame-filters:
  Priority  Enabled  Name
  999       No       BuildProgramFilter
```

:::

---

::: header
Previous: [Frame Apply](Frame-Apply.html#Frame-Apply)]
:::
