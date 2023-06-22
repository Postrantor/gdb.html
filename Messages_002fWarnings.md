---
description: Messages/Warnings (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Messages/Warnings (Debugging with GDB)
lang: en
resource-type: document
title: Messages/Warnings (Debugging with GDB)
---
::: header
Next: [Debugging Output](Debugging-Output.html#Debugging-Output)]
:::

---

### 22.9 Optional Warnings and Messages

By default, [GDB] tell you when it does a lengthy internal operation, so you will not think it has crashed.

Currently, the messages controlled by `set verbose` are those which announce that the symbol table for a source file is being read; see `symbol-file` in [Commands to Specify Files](Files.html#Files).

`set verbose on`

Enables [GDB] output of certain informational messages.

`set verbose off`

Disables [GDB] output of certain informational messages.

`show verbose`

Displays whether `set verbose` is on or off.

By default, if [GDB] encounters bugs in the symbol table of an object file, it is silent; but if you are debugging a compiler, you may find this information useful (see [Errors Reading Symbol Files](Symbol-Errors.html#Symbol-Errors)).

`set complaints limit`

Permits [GDB] to zero to suppress all complaints; set it to a large number to prevent complaints from being suppressed.

`show complaints`

Displays how many symbol complaints [GDB] is permitted to produce.

By default, [GDB] is cautious, and asks what sometimes seems to be a lot of stupid questions to confirm certain commands. For example, if you try to run a program which is already running:

::: smallexample

```bash
(gdb) run
The program being debugged has been started already.
Start it from the beginning? (y or n)
```

:::

If you are willing to unflinchingly face the consequences of your own commands, you can disable this "feature":

`set confirm off`

Disables confirmation requests. Note that running [GDB] option (see [-batch](Mode-Options.html#Mode-Options)) also automatically disables confirmation requests.

`set confirm on`

Enables confirmation requests (the default).

`show confirm`

Displays state of confirmation requests.

If you need to debug user-defined commands or sourced files you may find it useful to enable *command tracing*. In this mode each command will be printed as it is executed, prefixed with one or more '`+`' symbols, the quantity denoting the call depth of each command.

`set trace-commands on`

Enable command tracing.

`set trace-commands off`

Disable command tracing.

`show trace-commands`

Display the current state of command tracing.

---

::: header
Next: [Debugging Output](Debugging-Output.html#Debugging-Output)]
:::
