---
description: File Options (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: File Options (Debugging with GDB)
lang: en
resource-type: document
title: File Options (Debugging with GDB)
---
::: header
Next: [Mode Options](Mode-Options.html#Mode-Options)]
:::

---

#### 2.1.1 Choosing Files

When [GDB].

If [GDB] has not been configured to included core file support, such as for most embedded targets, then it will complain about a second argument and ignore it.

For the '`-s`' options, and their long form equivalents, the method used to search the file system for the symbol and/or executable file is the same as that used by the `file` command. See [file](Files.html#Files).

Many options have both long and short forms; both are shown in the following list. [GDB]', though we illustrate the more usual convention.)

`-symbols file`
`-s file`

:

```
Read symbol table from file `file`.
```

`-exec file`
`-e file`

:

```
Use file `file` as the executable file to execute when appropriate, and for examining pure data in conjunction with a core dump.
```

`-se file`

:

```
Read symbol table from file `file` and use it as the executable file.
```

`-core file`
`-c file`

:

```
Use file `file` as a core dump to examine.
```

`-pid number`
`-p number`

:

```
Connect to process ID `number`, as with the `attach` command.
```

`-command file`
`-x file`

:

```
Execute commands from file `file`. The contents of this file is evaluated exactly as the `source` command would. See [Command files](Command-Files.html#Command-Files).
```

`-eval-command command`
`-ex command`

:

```
Execute a single [GDB] command.

This option may be used multiple times to call multiple commands. It may also be interleaved with '`-command`' as required.

::: smallexample
``` smallexample
gdb -ex 'target sim' -ex 'load' \
   -x setbreakpoints -ex 'run' a.out
```

:::

```

`-init-command file`
`-ix file`

:   

```

Execute commands from file `file` before loading the inferior (but after loading gdbinit files). See [Startup](Startup.html#Startup).

```

`-init-eval-command command`
`-iex command`

:   

```

Execute a single [GDB] command before loading the inferior (but after loading gdbinit files). See [Startup](Startup.html#Startup).

```

`-early-init-command file`
`-eix file`

:   

```

Execute commands from `file` very early in the initialization process, before any output is produced. See [Startup](Startup.html#Startup).

```

`-early-init-eval-command command`
`-eiex command`

:   

```

Execute a single [GDB] command very early in the initialization process, before any output is produced.

```

`-directory directory`
`-d directory`

:   

```

Add `directory` to the path to search for source and script files.

```

`-r`
`-readnow`

:   

```

Read each symbol file's entire symbol table immediately, rather than the default, which is to read it incrementally as it is needed. This makes startup slower, but makes future operations faster.

```

`--readnever`

:   

```

Do not read each symbol file's symbolic debug information. This makes startup faster but at the expense of not being able to perform symbolic debugging. DWARF unwind information is also not read, meaning backtraces may become incomplete or inaccurate. One use of this is when a user simply wants to do the following sequence: attach, dump core, detach. Loading the debugging information in this case is an unnecessary cause of delay.

```

---

::: header
Next: [Mode Options](Mode-Options.html#Mode-Options)]
:::
```
