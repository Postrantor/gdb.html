---
tip: translate by openai@2023-06-23 13:34:18
...
---
description: Startup (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Startup (Debugging with GDB)
lang: en
resource-type: document
title: Startup (Debugging with GDB)
-----------------------------------

::: header
Next: [Initialization Files](Initialization-Files.html#Initialization-Files)]
:::

---

#### 2.1.3 What [GDB]

Here's the description of what [GDB] does during session startup:

> 这是[GDB]在会话启动时所做的描述：

1. Performs minimal setup required to initialize basic internal state.

> 执行最小的设置以初始化基本的内部状态。

2. Reads commands from the early initialization file (if any) in your home directory. Only a restricted set of commands can be placed into an early initialization file, see [Initialization Files](Initialization-Files.html#Initialization-Files), for details.

> 2. 如果您的家目录中有，则从早期初始化文件中读取命令（如果有）。只有一组受限的命令可以放入早期初始化文件，有关详细信息，请参见[初始化文件]（Initialization-Files.html#Initialization-Files）。

3. Executes commands and command files specified by the '`-eiex`', see [Initialization Files](Initialization-Files.html#Initialization-Files), for details.

> 执行由'-eiex'指定的命令和命令文件，有关详细信息，请参阅[初始化文件](Initialization-Files.html#Initialization-Files)。

4. Sets up the command interpreter as specified by the command line (see [interpreter](Mode-Options.html#Mode-Options)).

> 设置指定命令行的命令解释器（参见[解释器](Mode-Options.html#Mode-Options)）。

5. Reads the system wide initialization file and the files from the system wide initialization directory, see [System Wide Init Files](Initialization-Files.html#System-Wide-Init-Files).

> 阅读系统级初始化文件和系统级初始化目录中的文件，请参见[系统级初始化文件](Initialization-Files.html#System-Wide-Init-Files)。

6. Reads the initialization file (if any) in your home directory and executes all the commands in that file, see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File).

> 阅读您家目录中的初始化文件（如果有的话），并执行该文件中的所有命令，请参见[家目录初始文件](Initialization-Files.html#Home-Directory-Init-File)。

7. Executes commands and command files specified by the '`-iex` init files get executed and before inferior gets loaded.

> 7. 执行由'-iex'初始文件指定的命令和命令文件，在载入次级之前执行。

8. Processes command line options and operands.

> 处理命令行选项和操作数。

9. Reads and executes the commands from the initialization file (if any) in the current working directory as long as '`set auto-load local-gdbinit`. See [Init File in the Current Directory during Startup](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup).

> 从当前工作目录中的初始化文件（如果有）中读取并执行命令，只要设置了“自动加载本地 GDBINIT”。详见[启动时当前目录中的初始化文件](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup)。

10. If the command line specified a program to debug, or a process to attach to, or a core file, [GDB] loads any auto-loaded scripts provided for the program or for its loaded shared libraries. See [Auto-loading](Auto_002dloading.html#Auto_002dloading).

> 如果命令行指定了一个要调试的程序，或者要连接的进程，或者一个核心文件，[GDB]会加载为该程序或其加载的共享库提供的任何自动加载脚本。请参见[自动加载](Auto_002dloading.html#Auto_002dloading)。

```
If you wish to disable the auto-loading during startup, you must do something like the following:

::: smallexample

```bash
$ gdb -iex "set auto-load python-scripts off" myprogram
```

:::

Option '`-ex`' does not work because the auto-loading is then turned off too late.
```

11. Executes commands and command files specified by the '`-ex` command files.

> 执行由 '-ex' 命令文件指定的命令和命令文件。

12. Reads the command history recorded in the *history file*. See [Command History](Command-History.html#Command-History), for more details about the command history and the files where [GDB] records it.

> 读取记录在*历史文件*中的命令历史记录。有关命令历史记录及[GDB]记录它的文件的更多详细信息，请参阅[命令历史记录](Command-History.html#Command-History)。

---

::: header
Next: [Initialization Files](Initialization-Files.html#Initialization-Files)]
:::
