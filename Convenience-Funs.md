---
description: Convenience Funs (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Convenience Funs (Debugging with GDB)
lang: en
resource-type: document
title: Convenience Funs (Debugging with GDB)
---
::: header
Next: [Registers](Registers.html#Registers)]
:::

---

### 10.13 Convenience Functions

[GDB].

These functions do not require [GDB] to be configured with `Python` support, which means that they are always available.

`$_isvoid (expr)`

Return one if the expression `expr` is `void`. Otherwise it returns zero.

A `void` expression is an expression where the type of the result is `void`. For example, you can examine a convenience variable (see [Convenience Variables](Convenience-Vars.html#Convenience-Vars)) to check whether it is `void`:

::: smallexample

```bash
(gdb) print $_exitcode
$1 = void
(gdb) print $_isvoid ($_exitcode)
$2 = 1
(gdb) run
Starting program: ./a.out
[Inferior 1 (process 29572) exited normally]
(gdb) print $_exitcode
$3 = 0
(gdb) print $_isvoid ($_exitcode)
$4 = 0
```

:::

In the example above, we used `$_isvoid` to check whether `$_exitcode` is `void` before and after the execution of the program being debugged. Before the execution there is no exit code to be examined, therefore `$_exitcode` is `void`. After the execution the program being debugged returned zero, therefore `$_exitcode` is zero, which means that it is not `void` anymore.

The `void` expression can also be a call of a function from the program being debugged. For example, given the following function:

::: smallexample

```bash
void
foo (void)
{
}
```

:::

The result of calling it inside [GDB] is `void`:

::: smallexample

```bash
(gdb) print foo ()
$1 = void
(gdb) print $_isvoid (foo ())
$2 = 1
(gdb) set $v = foo ()
(gdb) print $v
$3 = void
(gdb) print $_isvoid ($v)
$4 = 1
```

:::

`$_gdb_setting_str (setting)`

Return the value of the [GDB] is any setting that can be used in a `set` or `show` command (see [Controlling GDB](Controlling-GDB.html#Controlling-GDB)).

::: smallexample

```bash
(gdb) show print frame-arguments
Printing of non-scalar frame arguments is "scalars".
(gdb) p $_gdb_setting_str("print frame-arguments")
$1 = "scalars"
(gdb) p $_gdb_setting_str("height")
$2 = "30"
(gdb)
```

:::

`$_gdb_setting (setting)`

Return the value of the [GDB]. The type of the returned value depends on the setting.

The value type for boolean and auto boolean settings is `int`. The boolean values `off` and `on` are converted to the integer values `0` and `1`. The value `auto` is converted to the value `-1`.

The value type for integer settings is either `unsigned int` or `int`, depending on the setting.

Some integer settings accept an `unlimited` value. Depending on the setting, the `set` command also accepts the value `0` or the value `-1` as a synonym for `unlimited`. For example, `set height unlimited` is equivalent to `set height 0`.

Some other settings that accept the `unlimited` value use the value `0` to literally mean zero. For example, `set history size 0` indicates to not record any [GDB] commands in the command history. For such settings, `-1` is the synonym for `unlimited`.

See the documentation of the corresponding `set` command for the numerical value equivalent to `unlimited`.

The `$_gdb_setting` function converts the unlimited value to a `0` or a `-1` value according to what the `set` command uses.

::: smallexample

```bash
(gdb) p $_gdb_setting_str("height")
$1 = "30"
(gdb) p $_gdb_setting("height")
$2 = 30
(gdb) set height unlimited
(gdb) p $_gdb_setting_str("height")
$3 = "unlimited"
(gdb) p $_gdb_setting("height")
$4 = 0
```

```bash
(gdb) p $_gdb_setting_str("history size")
$5 = "unlimited"
(gdb) p $_gdb_setting("history size")
$6 = -1
(gdb) p $_gdb_setting_str("disassemble-next-line")
$7 = "auto"
(gdb) p $_gdb_setting("disassemble-next-line")
$8 = -1
(gdb)
```

:::

Other setting types (enum, filename, optional filename, string, string noescape) are returned as string values.

`$_gdb_maint_setting_str (setting)`

Like the `$_gdb_setting_str` function, but works with `maintenance set` variables.

`$_gdb_maint_setting (setting)`

Like the `$_gdb_setting` function, but works with `maintenance set` variables.

`$_shell (command-string)`

Invoke a shell to execute `command-string` is a host signal number, not a target signal number. If you're native debugging, they will be the same, but if cross debugging, the host vs target signal numbers may be completely unrelated. Please consult your host operating system's documentation for the mapping between host signal numbers and signal names. The shell to run is determined in the same way as for the `shell` command. See [Shell Commands](Shell-Commands.html#Shell-Commands).

::: smallexample

```bash
(gdb) print $_shell("true")
$1 = 0
(gdb) print $_shell("false")
$2 = 1
(gdb) p $_shell("echo hello")
hello
$3 = 0
(gdb) p $_shell("foobar")
bash: line 1: foobar: command not found
$4 = 127
```

:::

This may also be useful in breakpoint conditions. For example:

::: smallexample

```bash
(gdb) break function if $_shell("some command") == 0
```

:::

In this scenario, you'll want to make sure that the shell command you run in the breakpoint condition takes the least amount of time possible. For example, avoid running a command that may block indefinitely, or that sleeps for a while before exiting. Prefer a command or script which analyzes some state and exits immediately. This is important because the debugged program stops for the breakpoint every time, and then [GDB] evaluates the breakpoint condition. If the condition is false, the program is re-resumed transparently, without informing you of the stop. A quick shell command thus avoids significantly slowing down the debugged program unnecessarily.

Note: unlike the `shell` command, the `$_shell` convenience function does not affect the `$_shell_exitcode` and `$_shell_exitsignal` convenience variables.

The following functions require [GDB] to be configured with `Python` support.

`$_memeq(buf1, buf2, length)`

Returns one if the `length` are equal. Otherwise it returns zero.

`$_regex(str, regex)`

Returns one if the string `str`. Otherwise it returns zero. The syntax of the regular expression is that specified by `Python`'s regular expression support.

`$_streq(str1, str2)`

Returns one if the strings `str1` are equal. Otherwise it returns zero.

`$_strlen(str)`

Returns the length of string `str`.

`$_caller_is(name[, number_of_frames])`

Returns one if the calling function's name is equal to `name`. Otherwise it returns zero.

If the optional argument `number_of_frames` is provided, it is the number of frames up in the stack to look. The default is 1.

Example:

::: smallexample

```bash
(gdb) backtrace
#0  bottom_func ()
    at testsuite/gdb.python/py-caller-is.c:21
#1  0x00000000004005a0 in middle_func ()
    at testsuite/gdb.python/py-caller-is.c:27
#2  0x00000000004005ab in top_func ()
    at testsuite/gdb.python/py-caller-is.c:33
#3  0x00000000004005b6 in main ()
    at testsuite/gdb.python/py-caller-is.c:39
(gdb) print $_caller_is ("middle_func")
$1 = 1
(gdb) print $_caller_is ("top_func", 2)
$1 = 1
```

:::

`$_caller_matches(regexp[, number_of_frames])`

Returns one if the calling function's name matches the regular expression `regexp`. Otherwise it returns zero.

If the optional argument `number_of_frames` is provided, it is the number of frames up in the stack to look. The default is 1.

`$_any_caller_is(name[, number_of_frames])`

Returns one if any calling function's name is equal to `name`. Otherwise it returns zero.

If the optional argument `number_of_frames` is provided, it is the number of frames up in the stack to look. The default is 1.

This function differs from `$_caller_is` in that this function checks all stack frames from the immediate caller to the frame specified by `number_of_frames`.

`$_any_caller_matches(regexp[, number_of_frames])`

Returns one if any calling function's name matches the regular expression `regexp`. Otherwise it returns zero.

If the optional argument `number_of_frames` is provided, it is the number of frames up in the stack to look. The default is 1.

This function differs from `$_caller_matches` in that this function checks all stack frames from the immediate caller to the frame specified by `number_of_frames`.

`$_as_string(value)`

This convenience function is considered deprecated, and could be removed from future versions of [GDB]' format specifier instead (see [%V Format Specifier](Output.html#g_t_0025V-Format-Specifier)).

Return the string representation of `value`.

This function is useful to obtain the textual label (enumerator) of an enumeration value. For example, assuming the variable `node` is of an enumerated type:

::: smallexample

```bash
(gdb) printf "Visiting node of type %s\n", $_as_string(node)
Visiting node of type NODE_INTEGER
```

:::

`$_cimag(value)`

`$_creal(value)`

Return the imaginary (`$_cimag`) or real (`$_creal`) part of the complex number `value`.

The type of the imaginary or real part depends on the type of the complex number, e.g., using `$_cimag` on a `float complex` will return an imaginary part of type `float`.

[GDB] provides the ability to list and get help on convenience functions.

`help function`

:

```
Print a list of all convenience functions.
```

---

::: header
Next: [Registers](Registers.html#Registers)]
:::
