---
description: Basic Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Basic Guile (Debugging with GDB)
lang: en
resource-type: document
title: Basic Guile (Debugging with GDB)
---
::: header
Next: [Guile Configuration](Guile-Configuration.html#Guile-Configuration)]
:::

---

#### 23.4.3.1 Basic Guile

At startup, [GDB]'s output-paging streams. A Guile program which outputs to one of these streams may have its output interrupted by the user (see [Screen Size](Screen-Size.html#Screen-Size)). In this situation, a Guile `signal` exception is thrown with value `SIGINT`.

Guile's history mechanism uses the same naming as [GDB].

[GDB] thread.

Some care must be taken when writing Guile code to run in [GDB]. Two things are worth noting in particular:

- [GDB] will most likely stop working correctly. Note that it is unfortunately common for GUI toolkits to install a `SIGCHLD` handler.
- [GDB] takes care to mark its internal file descriptors as close-on-exec. However, this cannot be done in a thread-safe way on all platforms. Your Guile programs should be aware of this and should both create new file descriptors with the close-on-exec flag set and arrange to close unneeded file descriptors before starting a child process.

[GDB] leaves the choice of how the `gdb` module is imported to the user. To simplify interactive use, it is recommended to add one of the following to your \~/.gdbinit.

::: smallexample

```bash
guile (use-modules (gdb))
```

:::

::: smallexample

```bash
guile (use-modules ((gdb) #:renamer (symbol-prefix-proc 'gdb:)))
```

:::

Which one to choose depends on your preference. The second one adds `gdb:` as a prefix to all module functions and variables.

The rest of this manual assumes the `gdb` module has been imported without any prefix. See the Guile documentation for `use-modules` for more information (see [Using Guile Modules](http://www.gnu.org/software/guile/manual/html_node/Using-Guile-Modules.html#Using-Guile-Modules) in GNU Guile Reference Manual).

Example:

::: smallexample

```bash
(gdb) guile (value-type (make-value 1))
ERROR: Unbound variable: value-type
Error while executing Scheme code.
(gdb) guile (use-modules (gdb))
(gdb) guile (value-type (make-value 1))
int
(gdb)
```

:::

The `(gdb)` module provides these basic Guile functions.

*

:   Evaluate `command` runs, it is translated as described in [Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling).

```
`from-tty` ought to consider this command as having originated from the user invoking it interactively. It must be a boolean value. If omitted, it defaults to `#f`.

By default, any output produced by `command` virtual terminal will be temporarily set to unlimited width and height, and its pagination will be disabled; see [Screen Size](Screen-Size.html#Screen-Size).
```

```
<!-- -->
```

Scheme Procedure: **history-ref** *number*

:   Return a value from [GDB] doesn't exist in the value history, a `gdb:error` exception will be raised.

```
If no exception is raised, the return value is always an instance of `<gdb:value>` (see [Values From Inferior In Guile](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile)).

*Note:* [GDB]'s command line and `$1` from Guile's history contains the result of evaluating an expression from Guile's command line.
```

```
<!-- -->
```

Scheme Procedure: **history-append!** *value*

:   Append `value`'s value history. Return its index in the history.

```
Putting into history values returned by Guile extensions will allow the user convenient access to those values via CLI history facilities.
```

```
<!-- -->
```

Scheme Procedure: **parse-and-eval** *expression*

:   Parse `expression` must be a string.

```
This function can be useful when implementing a new command (see [Commands In Guile](Commands-In-Guile.html#Commands-In-Guile)), as it provides a way to parse the command's arguments as an expression. It is also is useful when computing values. For example, it is the only way to get the value of a convenience variable (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) as a `<gdb:value>`.
```

---

::: header
Next: [Guile Configuration](Guile-Configuration.html#Guile-Configuration)]
:::
