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

`set debuginfod enabled off`

[GDB] will not attempt to query `debuginfod` servers when missing debug info or source files. By default, `debuginfod enabled` is set to `off` for non-interactive sessions.

`set debuginfod enabled ask`

[GDB] will prompt the user to enable or disable `debuginfod` before attempting to perform the next query. By default, `debuginfod enabled` is set to `ask` for interactive sessions.

`show debuginfod enabled`

Display whether `debuginfod enabled` is set to `on`, `off` or `ask`.

`set debuginfod urls`

`set debuginfod urls urls`

Set the space-separated list of URLs that `debuginfod` will attempt to query. Only `http://`, `https://` and `file://` protocols should be used. The default value of `debuginfod urls` is copied from the `DEBUGINFOD_URLS` environment variable.

`show debuginfod urls`

Display the list of URLs that `debuginfod` will attempt to query.

`set debuginfod verbose`

`set debuginfod verbose n`

Enable or disable `debuginfod`-related output. Use a non-zero value to enable and `0` to disable. `debuginfod` output is shown by default.

`show debuginfod verbose`

Show the current verbosity setting.
