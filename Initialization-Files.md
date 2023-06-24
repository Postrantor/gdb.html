---
tip: translate by openai@2023-06-23 23:27:43
...
---
description: Initialization Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Initialization Files (Debugging with GDB)
lang: en
resource-type: document
title: Initialization Files (Debugging with GDB)
---
::: header
Previous: [Startup](Startup.html#Startup)]
:::

---

#### 2.1.4 Initialization Files


During startup (see [Startup](Startup.html#Startup)) [GDB] in the same way.

> 在启动时（参见[启动](Startup.html#Startup))，以相同的方式[GDB]。

To display the list of initialization files loaded by [GDB].

The *early initialization* file is loaded very early in [GDB] starts up.


Commands that can be placed into an early initialization file will be documented as such throughout this manual. Any command that is not documented as being suitable for an early initialization file should instead be placed into a general initialization file. Command files passed to `--early-init-command` or `-eix` are also early initialization files, with the same command restrictions. Only commands that can appear in an early initialization file should be passed to `--early-init-eval-command` or `-eiex`.

> 可以放入早期初始化文件中的命令将在本手册中有所提及。任何未被记载为适用于早期初始化文件的命令，应当放入一般初始化文件中。通过`--early-init-command`或`-eix`传递的命令文件也是早期初始化文件，具有相同的命令限制。只有可以出现在早期初始化文件中的命令才能被传递到`--early-init-eval-command`或`-eiex`中。


In contrast, the *general initialization* files are processed later, after [GDB] has finished its own internal initialization process, any valid command can be used in these files.

> 相反，一般初始化文件会在[GDB]完成自身内部初始化过程之后被处理，这些文件中可以使用任何有效的命令。


Throughout the rest of this document the term *initialization file* refers to one of the general initialization files, not the early initialization file. Any discussion of the early initialization file will specifically mention that it is the early initialization file being discussed.

> 在此文档的其余部分中，术语“初始化文件”指的是一般初始化文件，而不是早期初始化文件。任何关于早期初始化文件的讨论都会明确指出是早期初始化文件。


As the system wide and home directory initialization files are processed before most command line options, changes to settings (e.g. '`set complaints`') can affect subsequent processing of command line options and operands.

> 系统宽泛的和主目录的初始化文件会在大多数命令行选项之前处理，对设置的更改（例如“set complaints”）可能会影响随后处理命令行选项和操作数。


The following sections describe where [GDB] looks for the early initialization and initialization files, and the order that the files are searched for.

> 以下部分描述了GDB在哪里查找早期初始化和初始化文件，以及文件的搜索顺序。

#### 2.1.4.1 Home directory early initialization files


[GDB] will load the first file that it finds, and subsequent locations will not be checked.

> [GDB] 将加载第一个找到的文件，后续位置将不会被检查。

On non-macOS hosts the locations searched are:


- The file `gdb/gdbearlyinit` within the directory pointed to by the environment variable `XDG_CONFIG_HOME`, if it is defined.

> 文件`gdb/gdbearlyinit`在环境变量`XDG_CONFIG_HOME`指向的目录中，如果它被定义了。

- The file `.config/gdb/gdbearlyinit` within the directory pointed to by the environment variable `HOME`, if it is defined.

> 文件`.config/gdb/gdbearlyinit`在由环境变量`HOME`指向的目录中，如果它被定义了的话。

- The file `.gdbearlyinit` within the directory pointed to by the environment variable `HOME`, if it is defined.

> 如果定义了环境变量HOME指向的目录中有文件`.gdbearlyinit`。

By contrast, on macOS hosts the locations searched are:


- The file `Library/Preferences/gdb/gdbearlyinit` within the directory pointed to by the environment variable `HOME`, if it is defined.

> 文件 `Library/Preferences/gdb/gdbearlyinit` 在环境变量 `HOME` 指向的目录中，如果它被定义了的话。

- The file `.gdbearlyinit` within the directory pointed to by the environment variable `HOME`, if it is defined.

> 如果定义了环境变量HOME指向的目录中的文件`.gdbearlyinit`。


It is possible to prevent the home directory early initialization file from being loaded using the '`-nx`' command line options, see [Choosing Modes](Mode-Options.html#Mode-Options).

> 使用'-nx'命令行选项可以防止加载主目录初始化文件，详见[选择模式](Mode-Options.html#Mode-Options)。

#### 2.1.4.2 System wide initialization files


There are two locations that are searched for system wide initialization files. Both of these locations are always checked:

> 有两个位置被搜索用于系统范围的初始化文件。这两个位置总是被检查。

`system.gdbinit`


:   This is a single system-wide initialization file. Its location is specified with the `--with-system-gdbinit` configure option (see [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)). It is loaded first when [GDB] starts, before command line options have been processed.

> 这是一个系统范围内的初始化文件。其位置由`--with-system-gdbinit`配置选项指定（参见[系统范围配置](System_002dwide-configuration.html#System_002dwide-configuration)）。它在[GDB]启动时首先被加载，在处理命令行选项之前。

`system.gdbinit.d`


:   This is the system-wide initialization directory. Its location is specified with the `--with-system-gdbinit-dir` configure option (see [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)). Files in this directory are loaded in alphabetical order immediately after `system.gdbinit` will not recurse into any subdirectories of this directory.

> 这是系统级初始化目录。其位置由`--with-system-gdbinit-dir`配置选项指定（参见[系统级配置](System_002dwide-configuration.html#System_002dwide-configuration)）。该目录中的文件以字母顺序在`system.gdbinit`之后立即加载，不会递归进入该目录的任何子目录。


It is possible to prevent the system wide initialization files from being loaded using the '`-nx`' command line option, see [Choosing Modes](Mode-Options.html#Mode-Options).

> 使用'-nx'命令行选项可以防止系统范围的初始化文件被加载，详见[选择模式](Mode-Options.html#Mode-Options)。

#### 2.1.4.3 Home directory initialization file


After loading the system wide initialization files [GDB] will load the first file that it finds, and subsequent locations will not be checked.

> 在加载系统级初始化文件[GDB]后，它将加载第一个找到的文件，而之后的位置将不会被检查。

On non-Apple hosts the locations searched are:

`$XDG_CONFIG_HOME/gdb/gdbinit`

`$HOME/.config/gdb/gdbinit`

`$HOME/.gdbinit`

While on Apple hosts the locations searched are:

`$HOME/Library/Preferences/gdb/gdbinit`

`$HOME/.gdbinit`


It is possible to prevent the home directory initialization file from being loaded using the '`-nx`' command line options, see [Choosing Modes](Mode-Options.html#Mode-Options).

> 使用'-nx'命令行选项可以防止加载主目录初始化文件，详见[选择模式](Mode-Options.html#Mode-Options)。


The DJGPP port of [GDB] file in your home directory, it warns you about that and suggests to rename the file to the standard name.

> DJGPP端口的[GDB]文件在您的家目录中，它会警告您并建议将文件重命名为标准名称。

#### 2.1.4.4 Local directory initialization file


[GDB] has been loaded, see [Choosing Files](File-Options.html#File-Options).

> [GDB]已加载，请参阅[选择文件](File-Options.html#File-Options)。


If the file in the current directory was already loaded as the home directory initialization file then it will not be loaded a second time.

> 如果文件已经在当前目录中被加载作为主目录初始化文件，那么它将不会被再次加载。


It is possible to prevent the local directory initialization file from being loaded using the '`-nx`' command line option, see [Choosing Modes](Mode-Options.html#Mode-Options).

> 可以使用'-nx'命令行选项阻止加载本地目录初始化文件，详见[选择模式](Mode-Options.html#Mode-Options)。

::: footnote

---

#### Footnotes

### [(1)](#DOCF1)


On DOS/Windows systems, the home directory is the one pointed to by the `HOME` environment variable.

> 在DOS/Windows系统中，家目录是指由`HOME`环境变量指向的目录。

### [(2)](#DOCF2)


On DOS/Windows systems, the home directory is the one pointed to by the `HOME` environment variable.

> 在DOS/Windows系统中，家目录是由`HOME`环境变量指向的。
:::

---

::: header
Previous: [Startup](Startup.html#Startup)]
:::
