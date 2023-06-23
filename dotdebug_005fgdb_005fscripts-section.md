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

The following entries are supported:

`SECTION_SCRIPT_ID_PYTHON_FILE = 1`

`SECTION_SCRIPT_ID_SCHEME_FILE = 3`

`SECTION_SCRIPT_ID_PYTHON_TEXT = 4`

`SECTION_SCRIPT_ID_SCHEME_TEXT = 6`

#### 23.5.2.1 Script File Entries

If the entry specifies a file, [GDB] is not searched, since the compilation directory is not relevant to scripts.

File entries can be placed in section `.debug_gdb_scripts` with, for example, this GCC macro for Python scripts.

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

::: example

```example
DEFINE_GDB_PY_SCRIPT ("my-app-scripts.py")
```

:::

The script name may include directories if desired.

Note that loading of this script file also requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

If the macro invocation is put in a header, any application or library using this header will get a reference to the specified script, and with the use of `"MS"` attributes on the section, the linker will remove duplicates.

#### 23.5.2.2 Script Text Entries

Script text entries allow to put the executable script in the entry itself instead of loading it from a file. The first line of the entry, everything after the prefix byte and up to the first newline (`0xa`) character, is the script name, and must not contain any kind of space character, e.g., spaces or tabs. The rest of the entry, up to the trailing null byte, is the script to execute in the specified language. The name needs to be unique among all script names, as [GDB] executes each script only once based on its name.

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

---

::: header
Next: [Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f)]
:::
