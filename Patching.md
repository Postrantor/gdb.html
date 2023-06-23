---
description: Patching (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Patching (Debugging with GDB)
lang: en
resource-type: document
title: Patching (Debugging with GDB)
---
::: header
Next: [Compiling and Injecting Code](Compiling-and-Injecting-Code.html#Compiling-and-Injecting-Code)]
:::

---

### 17.6 Patching Programs

By default, [GDB] opens the file containing your program's executable code (or the corefile) read-only. This prevents accidental alterations to machine code; but it also prevents you from intentionally patching your program's binary.

If you'd like to be able to patch the binary, you can specify that explicitly with the `set write` command. For example, you might want to turn on internal debugging flags, or even to make emergency repairs.

`set write on`

`set write off`

If you specify '`set write on` opens them read-only.

If you have already loaded a file, you must load it again (using the `exec-file` or `core-file` command) after changing `set write`, for your new setting to take effect.

`show write`

Display whether executable files and core files are opened for writing as well as reading.
