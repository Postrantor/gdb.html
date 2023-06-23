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

`--exec-prefix=dir`

:   Configure the source to install programs under directory `dir`.

`--srcdir=dirname`

:   Use this option to make configurations in directories separate from the [GDB].

`--target=target`

:   Configure [GDB] itself.

```
There is no convenient way to generate a list of all available targets. Also see the `--enable-targets` option, below.
```

There are many other options that are specific to [GDB]. This lists just the most common ones; there are some very specialized options not described here.

`--enable-targets=[target]…`
`--enable-targets=all`

:   Configure [GDB] for debugging programs running on any target it supports.

`--with-gdb-datadir=path`

:   Set the [GDB]' (which can be set using `--datadir`).

`--with-relocated-sources=dir`

:   Sets up the default source path substitution rule so that directory names recorded in debug information will be automatically adjusted for any directory under `dir`'s configured prefix, the one mentioned in the `--prefix` or `--exec-prefix` options to configure. This option is useful if GDB is supposed to be moved to a different place after it is built.

`--enable-64-bit-bfd`

:   Enable 64-bit support in BFD on 32-bit hosts.

`--disable-gdbmi`

:   Build [GDB] without the GDB/MI machine interface (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)).

`--enable-tui`

:   Build [GDB] with the text-mode full-screen user interface (TUI). Requires a curses library (ncurses and cursesX are also supported).

`--with-curses`

:   Use the curses library instead of the termcap library, for text-mode terminal operations.

`--with-debuginfod`

:   Build [GDB] is installed and found at configure time. For more information regarding `debuginfod` see [Debuginfod](Debuginfod.html#Debuginfod).

`--with-libunwind-ia64`

:   Use the libunwind library for unwinding function call stack on ia64 target platforms. See [http://www.nongnu.org/libunwind/index.html](http://www.nongnu.org/libunwind/index.html) for details.

`--with-system-readline`

:   Use the readline library installed on the host, rather than the library supplied as part of [GDB]. Readline 7 or newer is required; this is enforced by the build system.

`--with-system-zlib`

:   Use the zlib library installed on the host, rather than the library supplied as part of [GDB].

`--with-expat`

:   Build [GDB]. If your host does not have libexpat installed, you can get the latest version from [http://expat.sourceforge.net](http://expat.sourceforge.net).

`--with-libiconv-prefix[=dir]`

:   Build [GDB] with GNU libiconv, a character set encoding conversion library. This is not done by default, as on GNU systems the `iconv` that is built in to the C library is sufficient. If your host does not have a working `iconv`, you can get the latest version of GNU iconv from [https://www.gnu.org/software/libiconv/](https://www.gnu.org/software/libiconv/).

```
[GDB]'s build system also supports building GNU libiconv as part of the overall build. See [Requirements](Requirements.html#Requirements).
```

`--with-lzma`

:   Build [GDB]'s \"mini debuginfo\" feature, which is only useful on platforms using the ELF object file format. If your host does not have liblzma installed, you can get the latest version from [https://tukaani.org/xz/](https://tukaani.org/xz/).

`--with-python[=python]`

:   Build [GDB] is used to find the Python headers and libraries. It can be either the name of a Python executable, or the name of the directory in which Python is installed.

`--with-guile[=guile]`

:   Build [GDB] can be a version number, which will cause `configure` to try to use that version of Guile; or the file name of a `pkg-config` executable, which will be queried to find the information needed to compile and link against Guile.

`--without-included-regex`

:   Don't use the regex library included with [GDB] (as part of the libiberty library). This is the default on hosts with version 2 of the GNU C library.

`--with-sysroot=dir`

:   Use `dir` is moved to a different location.

`--with-system-gdbinit=file`

:   Configure [GDB] is moved to another location after being built, the location of the system-wide init file will be adjusted accordingly.

`--with-system-gdbinit-dir=directory`

:   Configure [GDB] is moved to another location after being built, the location of the system-wide init directory will be adjusted accordingly.

`--enable-build-warnings`

:   When building the [GDB] sources, ask the compiler to warn about any code which looks even vaguely suspicious. It passes many different warning flags, depending on the exact version of the compiler you are using.

`--enable-werror`

:   Treat compiler warnings as errors. It adds the `-Werror` flag to the compiler, which will fail the compilation if the compiler outputs any warning messages.

`--enable-ubsan`

:   Enable the GCC undefined behavior sanitizer. This is disabled by default, but passing `--enable-ubsan=yes` or `--enable-ubsan=auto` to `configure` will enable it. The undefined behavior sanitizer checks for C++ undefined behavior. It has a performance cost, so if you are looking at [GDB]'s performance, you should disable it. The undefined behavior sanitizer was first introduced in GCC 4.9.

---

::: header
Next: [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)]
:::
