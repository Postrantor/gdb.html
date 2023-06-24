---
tip: translate by openai@2023-06-23 20:27:08
...
---
description: Debuginfod Settings (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Debuginfod Settings (Debugging with GDB)
lang: en
resource-type: document
title: Debuginfod Settings (Debugging with GDB)
---
::: header
Up: [Debuginfod](Debuginfod.html#Debuginfod)]
:::

---

### K.1 Debuginfod Settings

[GDB] provides the following commands for configuring `debuginfod`.

`set debuginfod enabled`

`set debuginfod enabled on`


[GDB] will attempt to query `debuginfod` servers when missing debug info or source files.

> GDB 在缺少调试信息或源文件时会尝试查询 `debuginfod` 服务器。

`set debuginfod enabled off`


[GDB] will not attempt to query `debuginfod` servers when missing debug info or source files. By default, `debuginfod enabled` is set to `off` for non-interactive sessions.

> GDB 默认情况下，非交互式会话时，不会尝试查询缺失的调试信息或源文件的 debuginfod 服务器，并且 debuginfod 启用设置默认为关闭状态。

`set debuginfod enabled ask`


[GDB] will prompt the user to enable or disable `debuginfod` before attempting to perform the next query. By default, `debuginfod enabled` is set to `ask` for interactive sessions.

> [GDB] 在尝试执行下一个查询之前，会提示用户启用或禁用debuginfod。 默认情况下，交互式会话中的“debuginfod enabled”设置为“询问”。

`show debuginfod enabled`

Display whether `debuginfod enabled` is set to `on`, `off` or `ask`.

`set debuginfod urls`

`set debuginfod urls urls`


Set the space-separated list of URLs that `debuginfod` will attempt to query. Only `http://`, `https://` and `file://` protocols should be used. The default value of `debuginfod urls` is copied from the `DEBUGINFOD_URLS` environment variable.

> 设置debuginfod将尝试查询的以空格分隔的URL列表。 只能使用`http：//`，`https：//`和`file：//`协议。 `debuginfod urls`的默认值是从`DEBUGINFOD_URLS`环境变量复制而来的。

`show debuginfod urls`

Display the list of URLs that `debuginfod` will attempt to query.

`set debuginfod verbose`

`set debuginfod verbose n`


Enable or disable `debuginfod`-related output. Use a non-zero value to enable and `0` to disable. `debuginfod` output is shown by default.

> 启用或禁用与`debuginfod`相关的输出。使用非零值来启用，使用`0`来禁用。默认情况下会显示`debuginfod`输出。

`show debuginfod verbose`

Show the current verbosity setting.
