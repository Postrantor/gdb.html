---
tip: translate by openai@2023-06-23 19:29:41
...
---
description: Configure Options (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Configure Options (Debugging with GDB)
lang: en
resource-type: document
title: Configure Options (Debugging with GDB)
---
::: header
Next: [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)]
:::

---

### C.5 `configure`

Here is a summary of the `configure`.

::: smallexample

```bash
configure [--help]
          [--prefix=dir]
          [--exec-prefix=dir]
          [--srcdir=dirname]
          [--target=target]
```

:::

You may introduce options with a single '`-`'.

`--help`

:   Display a quick summary of how to invoke `configure`.

`--prefix=dir`


:   Configure the source to install programs and files under directory `dir`.

> 配置源以在目录'dir'下安装程序和文件。

`--exec-prefix=dir`

:   Configure the source to install programs under directory `dir`.

`--srcdir=dirname`


:   Use this option to make configurations in directories separate from the [GDB].

> 使用此选项可以将配置与[GDB]分离到不同的目录。

`--target=target`

:   Configure [GDB] itself.

```
There is no convenient way to generate a list of all available targets. Also see the `--enable-targets` option, below.
```


There are many other options that are specific to [GDB]. This lists just the most common ones; there are some very specialized options not described here.

> 有许多其他特定于[GDB]的选项。这里只列出了最常见的选项；这里没有描述一些非常专业的选项。

`--enable-targets=[target]…`
`--enable-targets=all`


:   Configure [GDB] for debugging programs running on any target it supports.

> 配置GDB以调试运行在它支持的任何目标上的程序。

`--with-gdb-datadir=path`

:   Set the [GDB]' (which can be set using `--datadir`).

`--with-relocated-sources=dir`


:   Sets up the default source path substitution rule so that directory names recorded in debug information will be automatically adjusted for any directory under `dir`'s configured prefix, the one mentioned in the `--prefix` or `--exec-prefix` options to configure. This option is useful if GDB is supposed to be moved to a different place after it is built.

> 设置默认的源路径替换规则，以便调试信息中记录的目录名称将自动调整为`dir`配置前缀下的任何目录，即`--prefix`或`--exec-prefix`选项中提到的前缀。如果在构建GDB之后需要将其移动到其他位置，则此选项非常有用。

`--enable-64-bit-bfd`

:   Enable 64-bit support in BFD on 32-bit hosts.

`--disable-gdbmi`


:   Build [GDB] without the GDB/MI machine interface (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)).

> 建立GDB而不使用GDB/MI机器接口（参见GDB/MI）。

`--enable-tui`


:   Build [GDB] with the text-mode full-screen user interface (TUI). Requires a curses library (ncurses and cursesX are also supported).

> 编译[GDB]时使用文本模式的全屏用户界面（TUI）。需要curses库（也支持ncurses和cursesX）。

`--with-curses`


:   Use the curses library instead of the termcap library, for text-mode terminal operations.

> 使用curses库而不是termcap库来进行文本模式终端操作。

`--with-debuginfod`


:   Build [GDB] is installed and found at configure time. For more information regarding `debuginfod` see [Debuginfod](Debuginfod.html#Debuginfod).

> 编译[GDB]已安装，并在配置时发现。有关`debuginfod`的更多信息，请参阅[Debuginfod](Debuginfod.html#Debuginfod)。

`--with-libunwind-ia64`


:   Use the libunwind library for unwinding function call stack on ia64 target platforms. See [http://www.nongnu.org/libunwind/index.html](http://www.nongnu.org/libunwind/index.html) for details.

> 使用libunwind库在ia64目标平台上解开函数调用堆栈。有关详细信息，请参阅[http://www.nongnu.org/libunwind/index.html](http://www.nongnu.org/libunwind/index.html)。

`--with-system-readline`


:   Use the readline library installed on the host, rather than the library supplied as part of [GDB]. Readline 7 or newer is required; this is enforced by the build system.

> 使用安装在主机上的Readline库，而不是作为[GDB]的一部分提供的库。需要Readline 7或更高版本；构建系统将强制执行此要求。

`--with-system-zlib`


:   Use the zlib library installed on the host, rather than the library supplied as part of [GDB].

> 使用安装在主机上的zlib库，而不是作为[GDB]的一部分提供的库。

`--with-expat`


:   Build [GDB]. If your host does not have libexpat installed, you can get the latest version from [http://expat.sourceforge.net](http://expat.sourceforge.net).

> 构建[GDB]。如果您的主机没有安装libexpat，您可以从[http://expat.sourceforge.net](http://expat.sourceforge.net)获取最新版本。

`--with-libiconv-prefix[=dir]`


:   Build [GDB] with GNU libiconv, a character set encoding conversion library. This is not done by default, as on GNU systems the `iconv` that is built in to the C library is sufficient. If your host does not have a working `iconv`, you can get the latest version of GNU iconv from [https://www.gnu.org/software/libiconv/](https://www.gnu.org/software/libiconv/).

> 编译GDB时使用GNU libiconv，这是一个字符集编码转换库。默认情况下，在GNU系统中，C库中内置的`iconv`已经足够使用。如果您的主机没有一个可用的`iconv`，您可以从[https://www.gnu.org/software/libiconv/](https://www.gnu.org/software/libiconv/)获取最新版本的GNU iconv。

```
[GDB]'s build system also supports building GNU libiconv as part of the overall build. See [Requirements](Requirements.html#Requirements).
```

`--with-lzma`


:   Build [GDB]'s \"mini debuginfo\" feature, which is only useful on platforms using the ELF object file format. If your host does not have liblzma installed, you can get the latest version from [https://tukaani.org/xz/](https://tukaani.org/xz/).

> 建立[GDB]的“小型调试信息”功能，该功能仅对使用ELF对象文件格式的平台有用。如果您的主机没有安装liblzma，您可以从[https://tukaani.org/xz/]获取最新版本。

`--with-python[=python]`


:   Build [GDB] is used to find the Python headers and libraries. It can be either the name of a Python executable, or the name of the directory in which Python is installed.

> 使用构建[GDB]来查找Python头文件和库。它可以是Python可执行文件的名称，也可以是安装Python的目录的名称。

`--with-guile[=guile]`


:   Build [GDB] can be a version number, which will cause `configure` to try to use that version of Guile; or the file name of a `pkg-config` executable, which will be queried to find the information needed to compile and link against Guile.

> 编译[GDB]可以是一个版本号，这会导致`configure`尝试使用该版本的Guile；或者是`pkg-config`可执行文件的文件名，将查询该文件以获取编译和链接Guile所需的信息。

`--without-included-regex`


:   Don't use the regex library included with [GDB] (as part of the libiberty library). This is the default on hosts with version 2 of the GNU C library.

> 不要使用随[GDB]一起提供的正则库（作为libiberty库的一部分）。这是GNU C库版本2的默认设置。

`--with-sysroot=dir`

:   Use `dir` is moved to a different location.

`--with-system-gdbinit=file`


:   Configure [GDB] is moved to another location after being built, the location of the system-wide init file will be adjusted accordingly.

> 配置[GDB]在构建后被移动到另一个位置，系统初始文件的位置将相应调整。

`--with-system-gdbinit-dir=directory`


:   Configure [GDB] is moved to another location after being built, the location of the system-wide init directory will be adjusted accordingly.

> 配置[GDB]在构建后被移动到另一个位置，系统全局初始化目录的位置将相应地调整。

`--enable-build-warnings`


:   When building the [GDB] sources, ask the compiler to warn about any code which looks even vaguely suspicious. It passes many different warning flags, depending on the exact version of the compiler you are using.

> 在构建[GDB]源代码时，请求编译器警告任何看起来有点可疑的代码。根据您使用的编译器的确切版本，它传递了许多不同的警告标志。

`--enable-werror`


:   Treat compiler warnings as errors. It adds the `-Werror` flag to the compiler, which will fail the compilation if the compiler outputs any warning messages.

> 将编译器警告视为错误。它会向编译器添加`-Werror`标志，如果编译器输出任何警告消息，则编译将失败。

`--enable-ubsan`


:   Enable the GCC undefined behavior sanitizer. This is disabled by default, but passing `--enable-ubsan=yes` or `--enable-ubsan=auto` to `configure` will enable it. The undefined behavior sanitizer checks for C++ undefined behavior. It has a performance cost, so if you are looking at [GDB]'s performance, you should disable it. The undefined behavior sanitizer was first introduced in GCC 4.9.

> 启用GCC未定义行为检测器。这是默认禁用的，但是将`--enable-ubsan=yes`或`--enable-ubsan=auto`传递给`configure`将启用它。未定义行为检测器检查C++未定义行为。它有性能成本，因此，如果您正在查看[GDB]的性能，则应禁用它。未定义行为检测器最早于GCC 4.9中引入。

---

::: header
Next: [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)]
:::
