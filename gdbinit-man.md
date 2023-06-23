---
description: gdbinit man (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gdbinit man (Debugging with GDB)
lang: en
resource-type: document
title: gdbinit man (Debugging with GDB)
---
::: header
Next: [gdb-add-index man](gdb_002dadd_002dindex-man.html#gdb_002dadd_002dindex-man)]
:::

---

#### gdbinit man

### gdbinit

::: format

```format

~/.config/gdb/gdbinit

~/.gdbinit

./.gdbinit
```

:::

These files contain [GDB] startup. The lines of contents are canned sequences of commands, described in [Sequences](Sequences.html#Sequences).

Please read more in [Startup](Startup.html#Startup).

`(not enabled with --with-system-gdbinit` during compilation)

:   System-wide initialization file. It is executed unless user specified [GDB] option `-nx` or `-n`. See more in

`(not enabled with --with-system-gdbinit-dir` during compilation)

:   System-wide initialization directory. All files in this directory are executed on startup unless user specified [GDB] option `-nx` or `-n`, as long as they have a recognized file extension. See more in [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration).

`~/.config/gdb/gdbinit or ~/.gdbinit`

:   User initialization file. It is executed unless user specified [GDB] options `-nx`, `-n` or `-nh`.

`.gdbinit`

:   Initialization file for current directory. It may need to be enabled with [GDB] security command `set auto-load local-gdbinit`. See more in [Init File in the Current Directory](Init-File-in-the-Current-Directory.html#Init-File-in-the-Current-Directory).
