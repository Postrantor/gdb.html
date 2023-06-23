---
description: Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Files (Debugging with GDB)
lang: en
resource-type: document
title: Files (Debugging with GDB)
---
::: header
Next: [File Caching](File-Caching.html#File-Caching)]
:::

---

### 18.1 Commands to Specify Files

You may want to specify executable and core dump file names. The usual way to do this is at start-up time, using the arguments to [GDB]](Invocation.html#Invocation)).

Occasionally it is necessary to change to a different file during a [GDB] commands to specify new files are useful.

`file filename`

Use `filename` and your program, using the `path` command.

You can load unlinked object `.o` can neither interpret nor modify relocations in this case, so branches and some initialized variables will appear to go to the wrong place. But this feature is still handy from time to time.

`file`

`file` with no argument makes [GDB] discard any information it has on both executable file and the symbol table.

`exec-file [ filename ]`

Specify that the program to be run (but not the symbol table) is found in `filename` means to discard information on the executable file.

`symbol-file [ filename [ -o offset ]]`

Read symbol table information from file `filename`. `PATH` is searched when necessary. Use the `file` command to get both symbol table and program to run from the same file.

If an optional `offset` is specified, it is added to the start address of each section in the symbol file. This is useful if the program is relocated at runtime, such as the Linux kernel with kASLR enabled.

`symbol-file` with no argument clears out [GDB] information on your program's symbol table.

The `symbol-file` command causes [GDB].

`symbol-file` does not repeat if you press RET again after executing it once.

When [GDB] compilers; for example, using `GCC` you can generate debugging information for optimized code.

For most kinds of object files, with the exception of old SVR3 systems using COFF, the `symbol-file` command does not normally read the symbol table in full right away. Instead, it scans the symbol table quickly to find which source files and which symbols are present. The details are read later, one source file at a time, as they are needed.

The purpose of this two-stage reading strategy is to make [GDB] start up faster. For the most part, it is invisible except for occasional pauses while the symbol table details for a particular source file are being read. (The `set verbose` command can turn these pauses into messages if desired. See [Optional Warnings and Messages](Messages_002fWarnings.html#Messages_002fWarnings).)

We have not implemented the two-stage strategy for COFF yet. When the symbol table is stored in COFF format, `symbol-file` reads the symbol table data in full right away. Note that "stabs-in-COFF" still does the two-stage strategy, since the debug info is actually in stabs format.

`symbol-file [ -readnow ] filename`

`file [ -readnow ] filename`

You can override the [GDB] has the entire symbol table available.

`symbol-file [ -readnever ] filename`

`file [ -readnever ] filename`

You can instruct [GDB]' option. See [\--readnever](File-Options.html#g_t_002d_002dreadnever).

`core-file [filename]`

`core`

Specify the whereabouts of a core dump file to be used as the "contents of memory". Traditionally, core files contain only some parts of the address space of the process that generated them; [GDB] can access the executable file itself for other parts.

`core-file` with no argument specifies that no core file is to be used.

Note that the core file is ignored when your program is actually running under [GDB]. So, if you have been running your program and you wish to debug a core file instead, you must kill the subprocess in which the program is running. To do this, use the `kill` command (see [Killing the Child Process](Kill-Process.html#Kill-Process)).

`add-symbol-file filename [ -readnow | -readnever ] [ -o offset ] [ textaddress ] [ -s section address … ]`

The `add-symbol-file` command reads additional symbol table information from the file `filename` can be given as an expression.

If an optional `offset` is specified, it is added to the start address of each section, except those for which the address was specified explicitly.

The symbol table of the file `filename` is added to the symbol table originally read with the `symbol-file` command. You can use the `add-symbol-file` command any number of times; the new symbol data thus read is kept in addition to the old.

Changes can be reverted using the command `remove-symbol-file`.

Although `filename` files, as long as:

- the file's symbolic information refers only to linker symbols defined in that file, not to symbols defined by other object files,
- every section the file's symbolic information refers to has actually been loaded into the inferior, as it appears in the file, and
- you can determine the address at which every section was loaded, and provide these to the `add-symbol-file` command.

Some embedded operating systems, like Sun Chorus and VxWorks, can load relocatable files into an already running program; such systems typically make the requirements above easy to meet. However, it's important to recognize that many native systems use complex link procedures (`.linkonce` section factoring and C++ constructor table assembly, for example) that make the requirements difficult to meet. In general, one cannot assume that using `add-symbol-file` to read a relocatable object file's symbolic information will have the same effect as linking the relocatable object file into the program in the normal way.

`add-symbol-file` does not repeat if you press RET after using it.

`remove-symbol-file filename`

`remove-symbol-file -a address`

Remove a symbol file added via the `add-symbol-file` command. The file to remove can be identified by its `filename` that lies within the boundaries of this symbol file in memory. Example:

::: smallexample

```bash
(gdb) add-symbol-file /home/user/gdb/mylib.so 0x7ffff7ff9480
add symbol table from file "/home/user/gdb/mylib.so" at
    .text_addr = 0x7ffff7ff9480
(y or n) y
Reading symbols from /home/user/gdb/mylib.so...
(gdb) remove-symbol-file -a 0x7ffff7ff9480
Remove symbol table from file "/home/user/gdb/mylib.so"? (y or n) y
(gdb)
```

:::

`remove-symbol-file` does not repeat if you press RET after using it.

`add-symbol-file-from-memory address`

Load symbols from the given `address` in a dynamically loaded object file whose image is mapped directly into the inferior's memory. For example, the Linux kernel maps a `syscall DSO` into each process's address space; this DSO provides kernel-specific code for some system calls. The argument can be any expression whose evaluation yields the address of the file's shared object file header. For this command to work, you must have used `symbol-file` or `exec-file` commands in advance.

`section section addr`

The `section` command changes the base address of the named `section`. This can be used if the exec file does not contain section addresses, (such as in the `a.out` format), or when the addresses specified in the file itself are wrong. Each section must be changed separately. The `info files` command, described below, lists all the sections and their addresses.

`info files`

`info target`

`info files` and `info target` are synonymous; both print the current target (see [Specifying a Debugging Target](Targets.html#Targets)), including the names of the executable and core dump files currently in use by [GDB], and the files from which symbols were loaded. The command `help target` lists all possible targets rather than current ones.

`maint info sections [-all-objects] [filter-list]`

Another command that can give you extra information about program sections is `maint info sections`. In addition to the section information displayed by `info files`, this command displays the flags and file offset of each section in the executable and core dump files.

When '`-all-objects`' is passed then sections from all loaded object files, including shared libraries, are printed.

The optional `filter-list` is a space separated list of filter keywords. Sections that match any one of the filter criteria will be printed. There are two types of filter:

`section-name`

:   Display information about any section named `section-name`.

`section-flag`

:   Display information for any section with `section-flag` currently knows about are:

```
`ALLOC`

:   Section will have space allocated in the process when loaded. Set for all sections except those containing debug information.

`LOAD`

:   Section will be loaded from the file into the child process memory. Set for pre-initialized code and data, clear for `.bss` sections.

`RELOC`

:   Section needs to be relocated before loading.

`READONLY`

:   Section cannot be modified by the child process.

`CODE`

:   Section contains executable code only.

`DATA`

:   Section contains data only (no executable code).

`ROM`

:   Section will reside in ROM.

`CONSTRUCTOR`

:   Section contains data for constructor/destructor lists.

`HAS_CONTENTS`

:   Section is not empty.

`NEVER_LOAD`

:   An instruction to the linker to not output the section.

`COFF_SHARED_LIBRARY`

:   A notification to the linker that the section contains COFF shared library information.

`IS_COMMON`

:   Section contains common symbols.
```

`maint info target-sections`

This command prints [GDB] maintains a table containing the allocatable sections from all currently mapped objects, along with information about where the section is mapped.

`set trust-readonly-sections on`

Tell [GDB] can fetch values from these sections out of the object file, rather than from the target program. For some targets (notably embedded ones), this can be a significant enhancement to debugging performance.

The default is off.

`set trust-readonly-sections off`

Tell [GDB] not to trust readonly sections. This means that the contents of the section might change while the program is running, and must therefore be fetched from the target when needed.

`show trust-readonly-sections`

Show the current setting of trusting readonly sections.

All file-specifying commands allow both absolute and relative file names as arguments. [GDB] always converts the file name to an absolute file name and remembers it that way.

[GDB]/Linux, MS-Windows, SunOS, Darwin/Mach-O, SVr4, IBM RS/6000 AIX, QNX Neutrino, FDPIC (FR-V), and DSBT (TIC6X) shared libraries.

On MS-Windows [GDB] must be linked with the Expat library to support shared libraries. See [Expat](Requirements.html#Expat).

[GDB] does not understand references to a function in a shared library, however---unless you are debugging a core file).

There are times, however, when you may wish to not automatically load symbol definitions from shared libraries, such as when they are particularly large or there are many of them.

To control the automatic loading of shared library symbols, use the commands:

`set auto-solib-add mode`

If `mode` is `off`, symbols must be loaded manually, using the `sharedlibrary` command. The default value is `on`.

If your program uses lots of shared libraries with debug info that takes large amounts of memory, you can decrease the [GDB] is a regular expression that matches the libraries whose symbols you want to be loaded.

`show auto-solib-add`

Display the current autoloading mode.

To explicitly load shared library symbols, use the `sharedlibrary` command:

`info share regex`

`info sharedlibrary regex`

Print the names of the shared libraries which are currently loaded that match `regex` is omitted then print all shared libraries that are loaded.

`info dll regex`

This is an alias of `info sharedlibrary`.

`sharedlibrary regex`

`share regex`

Load shared object library symbols for files matching a Unix regular expression. As with files loaded automatically, it only loads shared libraries required by your program for a core file or after typing `run`. If `regex` is omitted all shared libraries required by your program are loaded.

`nosharedlibrary`

Unload all shared object library symbols. This discards all symbols that have been loaded from all shared libraries. Symbols from shared libraries that were loaded by explicit user requests are not discarded.

Sometimes you may wish that [GDB] stops and gives you control when any of shared library events happen. The best way to do this is to use `catch load` and `catch unload` (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

[GDB] also supports the `set stop-on-solib-events` command for this. This command exists for historical reasons. It is less useful than setting a catchpoint, because it does not allow for conditions or commands as a catchpoint does.

`set stop-on-solib-events`

:

```
This command controls whether [GDB] should give you control when the dynamic linker notifies it about some shared library event. The most common event of interest is loading or unloading of a new shared library.
```

`show stop-on-solib-events`

:

```
Show whether [GDB] stops and gives you control when shared library events happen.
```

Shared libraries are also supported in many cross or remote debugging configurations. [GDB] to automatically retrieve the libraries from the target. If copies of the target libraries are provided, they need to be the same as the target libraries, although the copies on the target can be stripped as long as the copies on the host are not.

For remote debugging, you need to tell [GDB] has two variables to specify the search directories for target libraries.

`set sysroot path`

Use `path`.

If `path`.

For targets with an MS-DOS based filesystem, such as MS-Windows, [GDB] converts all backslash directory separators into forward slashes, because the backslash is not a directory separator on Unix:

::: smallexample

```bash
  c:\foo\bar.dll ⇒ c:/foo/bar.dll
```

:::

Then, [GDB], and looks for the resulting file name in the host file system:

::: smallexample

```bash
  c:/foo/bar.dll ⇒ /path/to/sysroot/c:/foo/bar.dll
```

:::

If that does not find the binary, [GDB]' character from the drive spec, both for convenience, and, for the case of the host file system not supporting file names with colons:

::: smallexample

```bash
  c:/foo/bar.dll ⇒ /path/to/sysroot/c/foo/bar.dll
```

:::

This makes it possible to have a system root that mirrors a target with more than one drive. E.g., you may want to setup your local copies of the target system shared libraries like so (note '`c`'):

::: smallexample

```bash
 /path/to/sysroot/c/sys/bin/foo.dll
 /path/to/sysroot/c/sys/bin/bar.dll
 /path/to/sysroot/z/sys/bin/bar.dll
```

:::

and point the system root at `/path/to/sysroot`.

If that still does not find the binary, [GDB] tries removing the whole drive spec from the target file name:

::: smallexample

```bash
  c:/foo/bar.dll ⇒ /path/to/sysroot/foo/bar.dll
```

:::

This last lookup makes it possible to not care about the drive name, if you don't want or need to.

The `set solib-absolute-prefix` command is an alias for `set sysroot`.

You can set the default system root by using the configure-time '`--with-sysroot` is moved to a new location.

`show sysroot`

Display the current executable and shared library prefix.

`set solib-search-path path`

If this variable is set, `path`' is preferred; setting it to a nonexistent directory may interfere with automatic loading of shared library symbols.

`show solib-search-path`

Display the current shared library search path.

`set target-file-system-kind kind`

Set assumed file system kind for target reported file names.

Shared library file names as reported by the target system may not make sense as is on the system [GDB] tries to determine the appropriate file system variant based on the current target's operating system (see [Configuring the Current ABI](ABI.html#ABI)). The supported file system settings are:

`unix`

:   Instruct [GDB]') character are considered absolute, and the directory separator character is also the forward slash.

`dos-based`

:   Instruct [GDB]') characters are considered directory separators.

`auto`

:   Instruct [GDB] to use the file system kind associated with the target operating system (see [Configuring the Current ABI](ABI.html#ABI)). This is the default.

When processing file names provided by the user, [GDB] to completely canonicalize each pair of file names it needs to compare. This will make file-name comparisons accurate, but at a price of a significant slowdown.

`set basenames-may-differ`

:

```
Set whether a source file may have multiple base names.
```

`show basenames-may-differ`

:

```
Show whether a source file may have multiple base names.
```

::: footnote

---

#### Footnotes

### [(15)](#DOCF15)

Historically the functionality to retrieve binaries from the remote system was provided by prefixing `path`
:::

---

::: header
Next: [File Caching](File-Caching.html#File-Caching)]
:::
