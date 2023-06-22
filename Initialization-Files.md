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

To display the list of initialization files loaded by [GDB].

The *early initialization* file is loaded very early in [GDB] starts up.

Commands that can be placed into an early initialization file will be documented as such throughout this manual. Any command that is not documented as being suitable for an early initialization file should instead be placed into a general initialization file. Command files passed to `--early-init-command` or `-eix` are also early initialization files, with the same command restrictions. Only commands that can appear in an early initialization file should be passed to `--early-init-eval-command` or `-eiex`.

In contrast, the *general initialization* files are processed later, after [GDB] has finished its own internal initialization process, any valid command can be used in these files.

Throughout the rest of this document the term *initialization file* refers to one of the general initialization files, not the early initialization file. Any discussion of the early initialization file will specifically mention that it is the early initialization file being discussed.

As the system wide and home directory initialization files are processed before most command line options, changes to settings (e.g. '`set complaints`') can affect subsequent processing of command line options and operands.

The following sections describe where [GDB] looks for the early initialization and initialization files, and the order that the files are searched for.

#### 2.1.4.1 Home directory early initialization files

[GDB] will load the first file that it finds, and subsequent locations will not be checked.

On non-macOS hosts the locations searched are:

- The file `gdb/gdbearlyinit` within the directory pointed to by the environment variable `XDG_CONFIG_HOME`, if it is defined.
- The file `.config/gdb/gdbearlyinit` within the directory pointed to by the environment variable `HOME`, if it is defined.
- The file `.gdbearlyinit` within the directory pointed to by the environment variable `HOME`, if it is defined.

By contrast, on macOS hosts the locations searched are:

- The file `Library/Preferences/gdb/gdbearlyinit` within the directory pointed to by the environment variable `HOME`, if it is defined.
- The file `.gdbearlyinit` within the directory pointed to by the environment variable `HOME`, if it is defined.

It is possible to prevent the home directory early initialization file from being loaded using the '`-nx`' command line options, see [Choosing Modes](Mode-Options.html#Mode-Options).

#### 2.1.4.2 System wide initialization files

There are two locations that are searched for system wide initialization files. Both of these locations are always checked:

`system.gdbinit`

:   This is a single system-wide initialization file. Its location is specified with the `--with-system-gdbinit` configure option (see [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)). It is loaded first when [GDB] starts, before command line options have been processed.

`system.gdbinit.d`

:   This is the system-wide initialization directory. Its location is specified with the `--with-system-gdbinit-dir` configure option (see [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)). Files in this directory are loaded in alphabetical order immediately after `system.gdbinit` will not recurse into any subdirectories of this directory.

It is possible to prevent the system wide initialization files from being loaded using the '`-nx`' command line option, see [Choosing Modes](Mode-Options.html#Mode-Options).

#### 2.1.4.3 Home directory initialization file

After loading the system wide initialization files [GDB] will load the first file that it finds, and subsequent locations will not be checked.

On non-Apple hosts the locations searched are:

`$XDG_CONFIG_HOME/gdb/gdbinit`

`$HOME/.config/gdb/gdbinit`

`$HOME/.gdbinit`

While on Apple hosts the locations searched are:

`$HOME/Library/Preferences/gdb/gdbinit`

`$HOME/.gdbinit`

It is possible to prevent the home directory initialization file from being loaded using the '`-nx`' command line options, see [Choosing Modes](Mode-Options.html#Mode-Options).

The DJGPP port of [GDB] file in your home directory, it warns you about that and suggests to rename the file to the standard name.

#### 2.1.4.4 Local directory initialization file

[GDB] has been loaded, see [Choosing Files](File-Options.html#File-Options).

If the file in the current directory was already loaded as the home directory initialization file then it will not be loaded a second time.

It is possible to prevent the local directory initialization file from being loaded using the '`-nx`' command line option, see [Choosing Modes](Mode-Options.html#Mode-Options).

::: footnote

---

#### Footnotes

### [(1)](#DOCF1)

On DOS/Windows systems, the home directory is the one pointed to by the `HOME` environment variable.

### [(2)](#DOCF2)

On DOS/Windows systems, the home directory is the one pointed to by the `HOME` environment variable.
:::

---

::: header
Previous: [Startup](Startup.html#Startup)]
:::
