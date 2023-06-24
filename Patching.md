---
tip: translate by openai@2023-06-24 01:05:18
...
---
description: Patching (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Patching (Debugging with GDB)
lang: en
resource-type: document
title: Patching (Debugging with GDB)
---
::: header
Next: [Compiling and Injecting Code](Compiling-and-Injecting-Code.html#Compiling-and-Injecting-Code)]
:::

---

### 17.6 Patching Programs


By default, [GDB] opens the file containing your program's executable code (or the corefile) read-only. This prevents accidental alterations to machine code; but it also prevents you from intentionally patching your program's binary.

> 默认情况下，GDB以只读方式打开包含程序可执行代码（或内核文件）的文件。这可以防止意外更改机器代码；但也会阻止您有意修补程序的二进制文件。


If you'd like to be able to patch the binary, you can specify that explicitly with the `set write` command. For example, you might want to turn on internal debugging flags, or even to make emergency repairs.

> 如果您想要能够补丁二进制文件，可以使用`set write`命令明确指定。例如，您可能想打开内部调试标志，甚至进行紧急修复。

`set write on`

`set write off`

If you specify '`set write on` opens them read-only.


If you have already loaded a file, you must load it again (using the `exec-file` or `core-file` command) after changing `set write`, for your new setting to take effect.

> 如果您已经加载了一个文件，在更改`set write`后，必须使用`exec-file`或`core-file`命令重新加载它，以使新设置生效。

`show write`


Display whether executable files and core files are opened for writing as well as reading.

> 显示可执行文件和核心文件是否同时打开了读写功能。
