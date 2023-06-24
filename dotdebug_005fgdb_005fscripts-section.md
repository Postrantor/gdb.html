---
tip: translate by openai@2023-06-23 20:42:25
...
---
description: dotdebug_gdb_scripts section (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: dotdebug_gdb_scripts section (Debugging with GDB)
lang: en
resource-type: document
title: dotdebug_gdb_scripts section (Debugging with GDB)
---
::: header
Next: [Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f)]
:::

---

#### 23.5.2 The `.debug_gdb_scripts` section


For systems using file formats like ELF and COFF, when [GDB] loads a new object file it will look for a special section named `.debug_gdb_scripts`. If this section exists, its contents is a list of null-terminated entries specifying scripts to load. Each entry begins with a non-null prefix byte that specifies the kind of entry, typically the extension language and whether the script is in a file or inlined in `.debug_gdb_scripts`.

> 对于使用ELF和COFF等文件格式的系统，当[GDB]加载新的对象文件时，它将查找名为`.debug_gdb_scripts`的特殊部分。如果此部分存在，其内容是指定要加载脚本的以null结尾的条目列表。每个条目都以非空前缀字节开头，该字节指定条目的类型，通常是扩展语言以及脚本是在文件中还是在`.debug_gdb_scripts`中内联。

The following entries are supported:

`SECTION_SCRIPT_ID_PYTHON_FILE = 1`

`SECTION_SCRIPT_ID_SCHEME_FILE = 3`

`SECTION_SCRIPT_ID_PYTHON_TEXT = 4`

`SECTION_SCRIPT_ID_SCHEME_TEXT = 6`

#### 23.5.2.1 Script File Entries


If the entry specifies a file, [GDB] is not searched, since the compilation directory is not relevant to scripts.

> 如果条目指定了文件，则不会搜索GDB，因为编译目录与脚本无关。


File entries can be placed in section `.debug_gdb_scripts` with, for example, this GCC macro for Python scripts.

> 文件条目可以放置在 `.debug_gdb_scripts` 节中，例如，使用GCC宏为Python脚本提供支持。

::: example

```example
/* Note: The "MS" section flags are to remove duplicates.  */
#define DEFINE_GDB_PY_SCRIPT(script_name) \
  asm("\
.pushsection \".debug_gdb_scripts\", \"MS\",@progbits,1\n\
.byte 1 /* Python */\n\
.asciz \"" script_name "\"\n\
.popsection \n\
");
```

:::


For Guile scripts, replace `.byte 1` with `.byte 3`. Then one can reference the macro in a header or source file like this:

> 对于Guile脚本，将`.byte 1`替换为`.byte 3`。然后可以像这样在头文件或源文件中引用宏：

::: example

```example
DEFINE_GDB_PY_SCRIPT ("my-app-scripts.py")
```

:::

The script name may include directories if desired.


Note that loading of this script file also requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

> 注意，加载此脚本文件还需要相应配置的“自动加载安全路径”（参见[自动加载安全路径](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)）。


If the macro invocation is put in a header, any application or library using this header will get a reference to the specified script, and with the use of `"MS"` attributes on the section, the linker will remove duplicates.

> 如果宏调用放在头文件中，使用该头文件的任何应用程序或库都将获得对指定脚本的引用，并且使用该节点上的“MS”属性，链接器将删除重复项。

#### 23.5.2.2 Script Text Entries


Script text entries allow to put the executable script in the entry itself instead of loading it from a file. The first line of the entry, everything after the prefix byte and up to the first newline (`0xa`) character, is the script name, and must not contain any kind of space character, e.g., spaces or tabs. The rest of the entry, up to the trailing null byte, is the script to execute in the specified language. The name needs to be unique among all script names, as [GDB] executes each script only once based on its name.

> 脚本文本条目允许将可执行脚本放入条目本身，而不是从文件加载它。条目的第一行，从前缀字节开始到第一个换行符（\x0a）之间的所有内容，是脚本名称，不能包含任何空格字符，例如空格或制表符。条目的其余部分，直到尾随的null字节，是要在指定语言中执行的脚本。名称需要在所有脚本名称中唯一，因为[GDB]根据其名称只执行每个脚本一次。

Here is an example from file `py-section-script.c` testsuite.

::: example

```example
#include "symcat.h"
#include "gdb/section-scripts.h"
asm(
".pushsection \".debug_gdb_scripts\", \"MS\",@progbits,1\n"
".byte " XSTRING (SECTION_SCRIPT_ID_PYTHON_TEXT) "\n"
".ascii \"gdb.inlined-script\\n\"\n"
".ascii \"class test_cmd (gdb.Command):\\n\"\n"
".ascii \"  def __init__ (self):\\n\"\n"
".ascii \"    super (test_cmd, self).__init__ ("
    "\\\"test-cmd\\\", gdb.COMMAND_OBSCURE)\\n\"\n"
".ascii \"  def invoke (self, arg, from_tty):\\n\"\n"
".ascii \"    print (\\\"test-cmd output, arg = %s\\\" % arg)\\n\"\n"
".ascii \"test_cmd ()\\n\"\n"
".byte 0\n"
".popsection\n"
);
```

:::


Loading of inlined scripts requires a properly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)). The path to specify in `auto-load safe-path` is the path of the file containing the `.debug_gdb_scripts` section.

> 加载内联脚本需要正确配置`auto-load safe-path`（参见[自动加载安全路径](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)）。在`auto-load safe-path`中指定的路径是包含`.debug_gdb_scripts`部分的文件的路径。

---

::: header
Next: [Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f)]
:::
