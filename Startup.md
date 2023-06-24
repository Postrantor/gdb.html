---
tip: translate by openai@2023-06-24 03:17:03
...
---
description: Startup (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Startup (Debugging with GDB)
lang: en
resource-type: document
title: Startup (Debugging with GDB)
---
::: header
Next: [Initialization Files](Initialization-Files.html#Initialization-Files)]
:::

---

#### 2.1.3 What [GDB]

Here's the description of what [GDB] does during session startup:

1. Performs minimal setup required to initialize basic internal state.

2. Reads commands from the early initialization file (if any) in your home directory. Only a restricted set of commands can be placed into an early initialization file, see [Initialization Files](Initialization-Files.html#Initialization-Files), for details.

> 从您的主目录中的早期初始化文件（如果有）中读取命令。只有一组有限的命令可以放入早期初始化文件，详情请参见[初始化文件](Initialization-Files.html#Initialization-Files)。

3. Executes commands and command files specified by the '`-eiex`', see [Initialization Files](Initialization-Files.html#Initialization-Files), for details.

> 执行由 '-eiex' 指定的命令和命令文件，有关详细信息，请参阅[初始化文件](Initialization-Files.html#Initialization-Files)。

4. Sets up the command interpreter as specified by the command line (see [interpreter](Mode-Options.html#Mode-Options)).

> 设置命令解释器，按照命令行指定（参见[解释器](Mode-Options.html#Mode-Options)）。

5. Reads the system wide initialization file and the files from the system wide initialization directory, see [System Wide Init Files](Initialization-Files.html#System-Wide-Init-Files).

> 阅读系统级初始化文件和系统级初始化目录中的文件，请参见[系统级初始化文件](Initialization-Files.html#System-Wide-Init-Files)。

6. Reads the initialization file (if any) in your home directory and executes all the commands in that file, see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File).

> 阅读您的主目录中的初始化文件（如果有的话），并执行该文件中的所有命令，详见[主目录初始化文件](Initialization-Files.html#Home-Directory-Init-File)。

7. Executes commands and command files specified by the '`-iex` init files get executed and before inferior gets loaded.

> 7. 执行'-iex'指定的命令和命令文件，在加载次级之前执行初始文件。
8. Processes command line options and operands.

9. Reads and executes the commands from the initialization file (if any) in the current working directory as long as '`set auto-load local-gdbinit`. See [Init File in the Current Directory during Startup](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup).

> 读取并执行当前工作目录中的初始化文件（如果有的话），只要设定了`自动加载本地GDB INIT`。请参阅[启动时当前目录中的初始化文件](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup)。

10. If the command line specified a program to debug, or a process to attach to, or a core file, [GDB] loads any auto-loaded scripts provided for the program or for its loaded shared libraries. See [Auto-loading](Auto_002dloading.html#Auto_002dloading).

> 如果命令行指定了要调试的程序或要附加的进程或内核文件，[GDB]就会加载为该程序或其加载的共享库提供的任何自动加载的脚本。请参阅[自动加载](Auto_002dloading.html#Auto_002dloading)。

    If you wish to disable the auto-loading during startup, you must do something like the following:

    ::: smallexample

    ```bash
    $ gdb -iex "set auto-load python-scripts off" myprogram
    ```

    :::

    Option '`-ex`' does not work because the auto-loading is then turned off too late.

11. Executes commands and command files specified by the '`-ex` command files.

> 执行由 '-ex' 命令文件指定的命令和命令文件。

12. Reads the command history recorded in the *history file*. See [Command History](Command-History.html#Command-History), for more details about the command history and the files where [GDB] records it.

> 阅读存储在*历史文件*中的命令历史记录。有关命令历史记录及[GDB]记录它的文件的更多详细信息，请参见[命令历史记录](Command-History.html#Command-History)。

---

::: header
Next: [Initialization Files](Initialization-Files.html#Initialization-Files)]
:::
