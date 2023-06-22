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
3. Executes commands and command files specified by the '`-eiex`', see [Initialization Files](Initialization-Files.html#Initialization-Files), for details.
4. Sets up the command interpreter as specified by the command line (see [interpreter](Mode-Options.html#Mode-Options)).
5. Reads the system wide initialization file and the files from the system wide initialization directory, see [System Wide Init Files](Initialization-Files.html#System-Wide-Init-Files).
6. Reads the initialization file (if any) in your home directory and executes all the commands in that file, see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File).
7. Executes commands and command files specified by the '`-iex` init files get executed and before inferior gets loaded.
8. Processes command line options and operands.
9. Reads and executes the commands from the initialization file (if any) in the current working directory as long as '`set auto-load local-gdbinit`. See [Init File in the Current Directory during Startup](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup).
10. If the command line specified a program to debug, or a process to attach to, or a core file, [GDB] loads any auto-loaded scripts provided for the program or for its loaded shared libraries. See [Auto-loading](Auto_002dloading.html#Auto_002dloading).

    If you wish to disable the auto-loading during startup, you must do something like the following:

    ::: smallexample

    ```bash
    $ gdb -iex "set auto-load python-scripts off" myprogram
    ```

    :::

    Option '`-ex`' does not work because the auto-loading is then turned off too late.
11. Executes commands and command files specified by the '`-ex` command files.
12. Reads the command history recorded in the *history file*. See [Command History](Command-History.html#Command-History), for more details about the command history and the files where [GDB] records it.

---

::: header
Next: [Initialization Files](Initialization-Files.html#Initialization-Files)]
:::
