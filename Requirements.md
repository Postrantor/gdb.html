---
tip: translate by openai@2023-06-24 02:09:35
...
---
description: Requirements (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Requirements (Debugging with GDB)
lang: en
resource-type: document
title: Requirements (Debugging with GDB)
---
::: header
Next: [Running Configure](Running-Configure.html#Running-Configure)]
:::

---

### C.1 Requirements for Building [GDB]


Building [GDB] requires various tools and packages to be available. Other packages will be used only if they are found.

> 建立[GDB]需要各种工具和软件包可用。如果发现其他软件包，也会使用它们。

### Tools/Packages Necessary for Building [GDB]

C++11 compiler


:   [GDB] is written in C++11. It should be buildable with any recent C++11 compiler, e.g. GCC.

> [GDB]是用C++11编写的。它应该可以使用任何最新的C++11编译器，例如GCC来构建。

GNU make


:   [GDB]'s build system relies on features only found in the GNU make program. Other variants of `make` will not work.

> GDB的构建系统依赖于只能在GNU make程序中找到的功能。其他版本的'make'将不起作用。

Libraries


:   The following libraries are mandatory for building [GDB]. See [Configure Options](Configure-Options.html#Configure-Options). We mention below the home site of each library, so that you could download and install them if your system doesn't already include them.

> 以下库是构建[GDB]的必需库。请参阅[配置选项](Configure-Options.html#Configure-Options)。下面我们提到每个库的主页，以便您可以下载和安装它们，如果您的系统中尚不包含它们。

```
GMP (The GNU Multiple Precision arithmetic library)

:   [GDB] uses GMP to perform some of its extended-precision arithmetics. The latest version of GMP is available from <https://gmplib.org/>.

    

MPFR (The GNU Multiple-precision floating-point library)

:   [GDB] uses MPFR to emulate the target floating-point arithmetics during expression evaluation, if the target uses different floating-point formats than the host. The latest version of MPFR is available from <http://www.mpfr.org>.
```

### Tools/Packages Optional for Building [GDB]

The tools/packages and libraries listed below are optional; [GDB].

Python


:   [GDB] to specify the non-standard directory where Python is installed.

> 指定Python安装的非标准目录的GDB。

Guile

:   [GDB] to specify the Guile version to include in the build.

```

```

Expat

:   If available, [GDB] uses XML files for the following functionalities:

```
-   Remote protocol memory maps (see [Memory Map Format](Memory-Map-Format.html#Memory-Map-Format))
-   Target descriptions (see [Target Descriptions](Target-Descriptions.html#Target-Descriptions))
-   Remote shared library lists (See [Library List Format](Library-List-Format.html#Library-List-Format), or alternatively see [Library List Format for SVR4 Targets](Library-List-Format-for-SVR4-Targets.html#Library-List-Format-for-SVR4-Targets))
-   MS-Windows shared libraries (see [Shared Libraries](Files.html#Shared-Libraries))
-   Traceframe info (see [Traceframe Info Format](Traceframe-Info-Format.html#Traceframe-Info-Format))
-   Branch trace (see [Branch Trace Format](Branch-Trace-Format.html#Branch-Trace-Format), see [Branch Trace Configuration Format](Branch-Trace-Configuration-Format.html#Branch-Trace-Configuration-Format))

The latest version of Expat is available from <http://expat.sourceforge.net>. Use the `--with-libexpat-prefix` to specify non-standard installation places for Expat.
```

iconv

:   [GDB] to specify where to find the `iconv` program.

```
On systems without `iconv`, you can install the GNU Libiconv library; its latest version can be found on <https://ftp.gnu.org/pub/gnu/libiconv/> if your system doesn't provide it. Use the `--with-libiconv-prefix` to specify non-standard installation place for it.

Alternatively, [GDB]'.


```

lzma

:   [GDB] option to specify its non-standard location.

zlib


:   [GDB]', it will be able to read the debug information in such binaries.

> [GDB]可以读取这些二进制文件中的调试信息。

```
The '`zlib`' library is likely included with your operating system distribution; if it is not, you can get the latest version from <http://zlib.net>.
```

---

::: header
Next: [Running Configure](Running-Configure.html#Running-Configure)]
:::
