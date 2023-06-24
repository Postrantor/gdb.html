---
tip: translate by openai@2023-06-23 21:02:13
...
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

> 你可能需要指定可执行文件和内核转储文件的名称。通常的做法是在启动时使用[GDB]的参数(Invocation.html#Invocation)。


Occasionally it is necessary to change to a different file during a [GDB] commands to specify new files are useful.

> 有时有必要在[GDB]命令中更改到不同的文件，用于指定新文件是有用的。

`file filename`

Use `filename` and your program, using the `path` command.


You can load unlinked object `.o` can neither interpret nor modify relocations in this case, so branches and some initialized variables will appear to go to the wrong place. But this feature is still handy from time to time.

> 在这种情况下，无法解释或修改重定位，但可以加载未链接的对象`.o`，因此分支和一些初始化的变量会显示为走错了位置。但是这个功能还是偶尔很有用的。

`file`

`file` with no argument makes [GDB] discard any information it has on both executable file and the symbol table.

`exec-file [ filename ]`


Specify that the program to be run (but not the symbol table) is found in `filename` means to discard information on the executable file.

> 指定要运行的程序（但不包括符号表）位于`文件名`中，意味着抛弃可执行文件中的信息。

`symbol-file [ filename [ -o offset ]]`


Read symbol table information from file `filename`. `PATH` is searched when necessary. Use the `file` command to get both symbol table and program to run from the same file.

> 从文件`filename`读取符号表信息。必要时会搜索`PATH`。使用`file`命令从同一文件获取符号表和要运行的程序。


If an optional `offset` is specified, it is added to the start address of each section in the symbol file. This is useful if the program is relocated at runtime, such as the Linux kernel with kASLR enabled.

> 如果指定了可选的`offset`，则会将其添加到符号文件中每个部分的起始地址。这对于在运行时重新定位程序（例如启用了kASLR的Linux内核）很有用。

`symbol-file` with no argument clears out [GDB] information on your program's symbol table.

The `symbol-file` command causes [GDB].

`symbol-file` does not repeat if you press RET again after executing it once.


When [GDB] compilers; for example, using `GCC` you can generate debugging information for optimized code.

> 当使用GCC编译器时，可以为优化代码生成调试信息。


For most kinds of object files, with the exception of old SVR3 systems using COFF, the `symbol-file` command does not normally read the symbol table in full right away. Instead, it scans the symbol table quickly to find which source files and which symbols are present. The details are read later, one source file at a time, as they are needed.

> 对于大多数类型的对象文件，除了使用COFF的老SVR3系统外，`symbol-file`命令通常不会立即完全读取符号表。相反，它快速扫描符号表以查找哪些源文件和哪些符号存在。细节稍后按需要一次读取一个源文件。


The purpose of this two-stage reading strategy is to make [GDB] start up faster. For the most part, it is invisible except for occasional pauses while the symbol table details for a particular source file are being read. (The `set verbose` command can turn these pauses into messages if desired. See [Optional Warnings and Messages](Messages_002fWarnings.html#Messages_002fWarnings).)

> 此两阶段阅读策略的目的是使[GDB]启动更快。大多数情况下，它是不可见的，除了在读取特定源文件的符号表详细信息时偶尔出现的暂停。（可以使用`set verbose`命令将这些暂停转换为消息。请参阅[可选警告和消息](Messages_002fWarnings.html#Messages_002fWarnings)。）


We have not implemented the two-stage strategy for COFF yet. When the symbol table is stored in COFF format, `symbol-file` reads the symbol table data in full right away. Note that "stabs-in-COFF" still does the two-stage strategy, since the debug info is actually in stabs format.

> 我们还没有为COFF实施双阶段策略。当符号表以COFF格式存储时，`symbol-file`会立即完全读取符号表数据。请注意，"stabs-in-COFF"仍然使用双阶段策略，因为调试信息实际上是stabs格式。

`symbol-file [ -readnow ] filename`

`file [ -readnow ] filename`

You can override the [GDB] has the entire symbol table available.

`symbol-file [ -readnever ] filename`

`file [ -readnever ] filename`


You can instruct [GDB]' option. See [\--readnever](File-Options.html#g_t_002d_002dreadnever).

> 你可以指示GDB。参见[\--readnever](File-Options.html#g_t_002d_002dreadnever)。

`core-file [filename]`

`core`


Specify the whereabouts of a core dump file to be used as the "contents of memory". Traditionally, core files contain only some parts of the address space of the process that generated them; [GDB] can access the executable file itself for other parts.

> 指定要用作“内存内容”的核心转储文件的位置。传统上，核心文件只包含生成它们的进程的地址空间的某些部分；[GDB]可以访问可执行文件本身以访问其他部分。

`core-file` with no argument specifies that no core file is to be used.


Note that the core file is ignored when your program is actually running under [GDB]. So, if you have been running your program and you wish to debug a core file instead, you must kill the subprocess in which the program is running. To do this, use the `kill` command (see [Killing the Child Process](Kill-Process.html#Kill-Process)).

> 注意，当您的程序实际运行在GDB下时，核心文件将被忽略。因此，如果您一直在运行程序，并希望调试核心文件，则必须杀死程序正在运行的子进程。要执行此操作，请使用`kill`命令（请参阅[杀死子进程](Kill-Process.html#Kill-Process)）。

`add-symbol-file filename [ -readnow | -readnever ] [ -o offset ] [ textaddress ] [ -s section address … ]`


The `add-symbol-file` command reads additional symbol table information from the file `filename` can be given as an expression.

> 命令`add-symbol-file`从文件`filename`中读取附加符号表信息，可以作为一个表达式给出。


If an optional `offset` is specified, it is added to the start address of each section, except those for which the address was specified explicitly.

> 如果指定了可选的`offset`，它将被添加到每个部分的起始地址，除了那些明确指定地址的部分。


The symbol table of the file `filename` is added to the symbol table originally read with the `symbol-file` command. You can use the `add-symbol-file` command any number of times; the new symbol data thus read is kept in addition to the old.

> 文件`filename`的符号表被添加到原本通过`symbol-file`命令读取的符号表中。你可以多次使用`add-symbol-file`命令；新读取的符号数据将被保存在旧的数据之上。

Changes can be reverted using the command `remove-symbol-file`.

Although `filename` files, as long as:


- the file's symbolic information refers only to linker symbols defined in that file, not to symbols defined by other object files,

> 该文件的符号信息仅指该文件中定义的链接器符号，而不是其他对象文件定义的符号。

- every section the file's symbolic information refers to has actually been loaded into the inferior, as it appears in the file, and

> 每个文件的符号信息所指的部分都已经加载到低级中，就像它在文件中出现的那样。

- you can determine the address at which every section was loaded, and provide these to the `add-symbol-file` command.

> 你可以确定每个部分加载的地址，并将这些地址提供给 `add-symbol-file` 命令。


Some embedded operating systems, like Sun Chorus and VxWorks, can load relocatable files into an already running program; such systems typically make the requirements above easy to meet. However, it's important to recognize that many native systems use complex link procedures (`.linkonce` section factoring and C++ constructor table assembly, for example) that make the requirements difficult to meet. In general, one cannot assume that using `add-symbol-file` to read a relocatable object file's symbolic information will have the same effect as linking the relocatable object file into the program in the normal way.

> 一些嵌入式操作系统，如Sun Chorus和VxWorks，可以将可重定位文件加载到正在运行的程序中；这些系统通常使上述要求变得容易满足。但是，重要的是要认识到许多原生系统使用复杂的链接过程（例如，`linkonce`部分因素和C++构造函数表组装），使得这些要求难以满足。一般来说，不能假定使用`add-symbol-file`来读取可重定位对象文件的符号信息，其效果将与以正常方式将可重定位对象文件链接到程序中相同。

`add-symbol-file` does not repeat if you press RET after using it.

`remove-symbol-file filename`

`remove-symbol-file -a address`


Remove a symbol file added via the `add-symbol-file` command. The file to remove can be identified by its `filename` that lies within the boundaries of this symbol file in memory. Example:

> 移除通过`add-symbol-file`命令添加的符号文件。可以通过内存中该符号文件范围内的`文件名`来识别要移除的文件。例如：

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

> 从给定的地址加载动态加载的对象文件的符号，该图像直接映射到次级的内存中。例如，Linux内核将`syscall DSO`映射到每个进程的地址空间；此DSO为某些系统调用提供内核特定的代码。该参数可以是任何表达式，其计算结果为文件共享对象文件头的地址。要使此命令工作，您必须先使用`symbol-file`或`exec-file`命令。

`section section addr`


The `section` command changes the base address of the named `section`. This can be used if the exec file does not contain section addresses, (such as in the `a.out` format), or when the addresses specified in the file itself are wrong. Each section must be changed separately. The `info files` command, described below, lists all the sections and their addresses.

> 命令'section'用于改变指定'section'的基地址。这在执行文件不包含section地址（例如a.out格式）时会很有用，或者当文件本身指定的地址是错误的时候也会很有用。每个section都必须单独改变。下面描述的命令'info files'会列出所有的section和它们的地址。

`info files`

`info target`

`info files` and `info target` are synonymous; both print the current target (see [Specifying a Debugging Target](Targets.html#Targets)), including the names of the executable and core dump files currently in use by [GDB], and the files from which symbols were loaded. The command `help target` lists all possible targets rather than current ones.

`maint info sections [-all-objects] [filter-list]`


Another command that can give you extra information about program sections is `maint info sections`. In addition to the section information displayed by `info files`, this command displays the flags and file offset of each section in the executable and core dump files.

> 另一个可以给你提供有关程序段的额外信息的命令是`maint info sections`。除了`info files`显示的段信息外，该命令还显示可执行文件和核心转储文件中每个段的标志和文件偏移量。


When '`-all-objects`' is passed then sections from all loaded object files, including shared libraries, are printed.

> 当传入`-all-objects`时，将打印出所有已加载的对象文件（包括共享库）的部分内容。


The optional `filter-list` is a space separated list of filter keywords. Sections that match any one of the filter criteria will be printed. There are two types of filter:

> 可选的`filter-list`是一个用空格分隔的过滤关键字列表。符合任何一个过滤条件的部分将被打印出来。过滤器有两种类型：

`section-name`

:   Display information about any section named `section-name`.

`section-flag`


:   Display information for any section with `section-flag` currently knows about are:

> 显示任何有关`section-flag`的信息：

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

> 这个命令会打印出GDB维护的表格，其中包含了所有当前映射对象的可分配部分，以及有关该部分映射到哪里的信息。

`set trust-readonly-sections on`


Tell [GDB] can fetch values from these sections out of the object file, rather than from the target program. For some targets (notably embedded ones), this can be a significant enhancement to debugging performance.

> 告诉[GDB]可以从对象文件的这些部分获取值，而不是从目标程序获取。对于某些目标（尤其是嵌入式目标），这可以显著提高调试性能。

The default is off.

`set trust-readonly-sections off`


Tell [GDB] not to trust readonly sections. This means that the contents of the section might change while the program is running, and must therefore be fetched from the target when needed.

> 告诉GDB不要相信只读部分。这意味着该部分的内容可能在程序运行期间改变，因此必须在需要时从目标获取。

`show trust-readonly-sections`

Show the current setting of trusting readonly sections.


All file-specifying commands allow both absolute and relative file names as arguments. [GDB] always converts the file name to an absolute file name and remembers it that way.

> 所有文件指定命令都允许使用绝对文件名和相对文件名作为参数。[GDB]总是将文件名转换为绝对文件名并记住它。


[GDB]/Linux, MS-Windows, SunOS, Darwin/Mach-O, SVr4, IBM RS/6000 AIX, QNX Neutrino, FDPIC (FR-V), and DSBT (TIC6X) shared libraries.

> [GDB]/Linux、MS-Windows、SunOS、Darwin/Mach-O、SVr4、IBM RS/6000 AIX、QNX Neutrino、FDPIC (FR-V) 和 DSBT (TIC6X) 共享库。


On MS-Windows [GDB] must be linked with the Expat library to support shared libraries. See [Expat](Requirements.html#Expat).

> 在MS-Windows上，GDB必须链接到Expat库以支持共享库。参见[Expat](Requirements.html#Expat)。


[GDB] does not understand references to a function in a shared library, however---unless you are debugging a core file).

> GDB无法理解共享库中函数的引用，但除非你在调试内核文件。


There are times, however, when you may wish to not automatically load symbol definitions from shared libraries, such as when they are particularly large or there are many of them.

> 有时，你可能希望不自动从共享库加载符号定义，比如它们特别大或者有很多的时候。


To control the automatic loading of shared library symbols, use the commands:

> 使用以下命令控制共享库符号的自动加载：

`set auto-solib-add mode`


If `mode` is `off`, symbols must be loaded manually, using the `sharedlibrary` command. The default value is `on`.

> 如果模式设置为关闭，必须使用`sharedlibrary`命令手动加载符号。默认值为开启。


If your program uses lots of shared libraries with debug info that takes large amounts of memory, you can decrease the [GDB] is a regular expression that matches the libraries whose symbols you want to be loaded.

> 如果您的程序使用大量具有调试信息的共享库，而这些库占用大量内存，您可以减少[GDB]的使用，它是一个匹配您想要加载符号的库的正则表达式。

`show auto-solib-add`

Display the current autoloading mode.


To explicitly load shared library symbols, use the `sharedlibrary` command:

> 使用`sharedlibrary`命令显式加载共享库符号：

`info share regex`

`info sharedlibrary regex`


Print the names of the shared libraries which are currently loaded that match `regex` is omitted then print all shared libraries that are loaded.

> 打印当前已加载的与`regex`匹配的共享库的名称，如果省略`regex`，则打印所有已加载的共享库。

`info dll regex`

This is an alias of `info sharedlibrary`.

`sharedlibrary regex`

`share regex`


Load shared object library symbols for files matching a Unix regular expression. As with files loaded automatically, it only loads shared libraries required by your program for a core file or after typing `run`. If `regex` is omitted all shared libraries required by your program are loaded.

> 加载符合Unix正则表达式的共享对象库符号。与自动加载的文件一样，它只会在你的程序需要核心文件时或输入`run`后加载共享库。如果省略`regex`，则会加载你的程序所需的所有共享库。

`nosharedlibrary`


Unload all shared object library symbols. This discards all symbols that have been loaded from all shared libraries. Symbols from shared libraries that were loaded by explicit user requests are not discarded.

> 卸载所有共享对象库符号。这将放弃从所有共享库加载的所有符号。由用户显式请求加载的共享库的符号不会被丢弃。


Sometimes you may wish that [GDB] stops and gives you control when any of shared library events happen. The best way to do this is to use `catch load` and `catch unload` (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

> 有时候你可能希望当发生任何共享库事件时GDB停止并给你控制权。最好的方法是使用“catch load”和“catch unload”（参见[设置捕获点]（Set-Catchpoints.html#Set-Catchpoints））。


[GDB] also supports the `set stop-on-solib-events` command for this. This command exists for historical reasons. It is less useful than setting a catchpoint, because it does not allow for conditions or commands as a catchpoint does.

> GDB 也支持 `set stop-on-solib-events` 命令来实现这一目的。出于历史原因，这个命令存在。它比设置捕获点要不太有用，因为它不允许设置条件或命令，而捕获点可以。

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

> 共享库也支持许多跨系统或远程调试配置。[GDB]可以自动从目标设备获取库。如果提供了目标库的副本，它们需要与目标库相同，尽管目标上的副本可以被剥离，只要主机上的副本不被剥离。


For remote debugging, you need to tell [GDB] has two variables to specify the search directories for target libraries.

> 为了进行远程调试，你需要告诉GDB有两个变量用于指定目标库的搜索目录。

`set sysroot path`

Use `path`.

If `path`.


For targets with an MS-DOS based filesystem, such as MS-Windows, [GDB] converts all backslash directory separators into forward slashes, because the backslash is not a directory separator on Unix:

> 对于使用MS-DOS基于文件系统的目标，如MS-Windows，[GDB]将所有反斜杠目录分隔符转换为正斜杠，因为反斜杠在Unix上不是目录分隔符：

::: smallexample

```bash
  c:\foo\bar.dll ⇒ c:/foo/bar.dll
```

:::


Then, [GDB], and looks for the resulting file name in the host file system:

> 然后，使用[GDB]，在主机文件系统中查找生成的文件名。

::: smallexample

```bash
  c:/foo/bar.dll ⇒ /path/to/sysroot/c:/foo/bar.dll
```

:::


If that does not find the binary, [GDB]' character from the drive spec, both for convenience, and, for the case of the host file system not supporting file names with colons:

> 如果没有找到二进制文件[GDB]，为了方便起见，以及主机文件系统不支持带冒号的文件名的情况：

::: smallexample

```bash
  c:/foo/bar.dll ⇒ /path/to/sysroot/c/foo/bar.dll
```

:::


This makes it possible to have a system root that mirrors a target with more than one drive. E.g., you may want to setup your local copies of the target system shared libraries like so (note '`c`'):

> 这使得有可能拥有一个系统根目录，它可以镜像一个具有多个驱动器的目标。例如，您可能想要像这样设置目标系统共享库的本地副本（注意'c'）：

::: smallexample

```bash
 /path/to/sysroot/c/sys/bin/foo.dll
 /path/to/sysroot/c/sys/bin/bar.dll
 /path/to/sysroot/z/sys/bin/bar.dll
```

:::

and point the system root at `/path/to/sysroot`.


If that still does not find the binary, [GDB] tries removing the whole drive spec from the target file name:

> 如果仍然没有找到二进制文件，[GDB] 尝试从目标文件名中删除整个驱动器规格：

::: smallexample

```bash
  c:/foo/bar.dll ⇒ /path/to/sysroot/foo/bar.dll
```

:::


This last lookup makes it possible to not care about the drive name, if you don't want or need to.

> 这最后的查找使得你不用关心驱动器的名称，如果你不想要或不需要的话。

The `set solib-absolute-prefix` command is an alias for `set sysroot`.


You can set the default system root by using the configure-time '`--with-sysroot` is moved to a new location.

> 你可以通过使用配置时的'--with-sysroot'将默认系统根移动到新位置来设置默认系统根。

`show sysroot`

Display the current executable and shared library prefix.

`set solib-search-path path`


If this variable is set, `path`' is preferred; setting it to a nonexistent directory may interfere with automatic loading of shared library symbols.

> 如果设置了此变量，则优先考虑`path`；将其设置为不存在的目录可能会干扰共享库符号的自动加载。

`show solib-search-path`

Display the current shared library search path.

`set target-file-system-kind kind`

Set assumed file system kind for target reported file names.


Shared library file names as reported by the target system may not make sense as is on the system [GDB] tries to determine the appropriate file system variant based on the current target's operating system (see [Configuring the Current ABI](ABI.html#ABI)). The supported file system settings are:

> 系统报告的共享库文件名可能在[GDB]系统上没有意义，GDB会根据当前目标的操作系统来确定适当的文件系统变量（参见[配置当前ABI]（ABI.html#ABI））。支持的文件系统设置为：

`unix`


:   Instruct [GDB]') character are considered absolute, and the directory separator character is also the forward slash.

> 字符对GDB来说是绝对的，目录分隔符也是斜杠。

`dos-based`

:   Instruct [GDB]') characters are considered directory separators.

`auto`


:   Instruct [GDB] to use the file system kind associated with the target operating system (see [Configuring the Current ABI](ABI.html#ABI)). This is the default.

> 请求GDB使用与目标操作系统相关联的文件系统类型（参见[配置当前ABI]（ABI.html#ABI））。这是默认值。


When processing file names provided by the user, [GDB] to completely canonicalize each pair of file names it needs to compare. This will make file-name comparisons accurate, but at a price of a significant slowdown.

> 当处理用户提供的文件名时，GDB需要完全规范化每对文件名以进行比较。这会使文件名比较准确，但是会以显著减慢的速度为代价。

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

> 历史上，从远程系统检索二进制文件的功能是通过在路径前面加上“路径”来提供的。
:::

---

::: header
Next: [File Caching](File-Caching.html#File-Caching)]
:::
