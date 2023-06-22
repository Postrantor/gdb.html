---
description: Completion (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Completion (Debugging with GDB)
lang: en
resource-type: document
title: Completion (Debugging with GDB)
---
::: header
Next: [Command Options](Command-Options.html#Command-Options)]
:::

---

### 3.3 Command Completion

[GDB] subcommands, command options, and the names of symbols in your program.

Press the TAB key whenever you want [GDB] fills in the word, and waits for you to finish the command (or press RET to enter it). For example, if you type

::: smallexample

```bash
(gdb) info breTAB
```

:::

[GDB]':

::: smallexample

```bash
(gdb) info breakpoints
```

:::

You can either press RET at this point, to run the `info breakpoints` command, or backspace and enter something else, if '`breakpoints`', to exploit command abbreviations rather than command completion).

If there is more than one possibility for the next word when you press TAB, [GDB] just sounds the bell. Typing TAB again displays all the function names in your program that begin with those characters, for example:

::: smallexample

```bash
(gdb) b make_TAB
```

```bash
GDB sounds bell; press TAB again, to see:
```

```bash
make_a_section_from_file     make_environ
make_abs_section             make_function_type
make_blockvector             make_pointer_type
make_cleanup                 make_reference_type
make_command                 make_symbol_completion_list
(gdb) b make_
```

:::

After displaying the available possibilities, [GDB]' in the example) so you can finish the command.

If the command you are trying to complete expects either a keyword or a number to follow, then '`NUMBER`' will be shown among the available completions, for example:

::: smallexample

```bash
(gdb) print -elements TABTAB
NUMBER     unlimited
(gdb) print -elements 
```

:::

Here, the option expects a number (e.g., `100`), not literal `NUMBER`. Such metasyntactical arguments are always presented in uppercase.

If you just want to see the list of alternatives in the first place, you can press [M-?].

If the number of possible completions is large, [GDB] will print as much of the list as it has collected, as well as a message indicating that the list may be truncated.

::: smallexample

```bash
(gdb) b mTABTAB
main
<... the rest of the possible completions ...>
*** List may be truncated, max-completions reached. ***
(gdb) b m
```

:::

This behavior can be controlled with the following commands:

`set max-completions limit`

`set max-completions unlimited`

Set the maximum number of completion candidates. [GDB]

`show max-completions`

Show the maximum number of candidates that [GDB] will collect and show during completion.

Sometimes the string you need, while logically a "word", may contain parentheses or other characters that [GDB] commands.

A likely situation where you might need this is in typing an expression that involves a C++ symbol name with template parameters. This is because when completing expressions, GDB treats the '`<`' character as word delimiter, assuming that it's the less-than comparison operator (see [C and C++ Operators](C-Operators.html#C-Operators)).

For example, when you want to call a C++ template function interactively using the `print` or `call` commands, you may need to distinguish whether you mean the version of `name` that was specialized for `int`, `name<int>()`, or the version that was specialized for `float`, `name<float>()`. To use the word-completion facilities in this situation, type a single quote `'` at the beginning of the function name. This alerts [GDB] to request word completion:

::: smallexample

```bash
(gdb) p 'func<M-?
func<int>()    func<float>()
(gdb) p 'func<
```

:::

When setting breakpoints however (see [Location Specifications](Location-Specifications.html#Location-Specifications)), you don't usually need to type a quote before the function name, because [GDB] understands that you want to set a breakpoint on a function:

::: smallexample

```bash
(gdb) b func<M-?
func<int>()    func<float>()
(gdb) b func<
```

:::

This is true even in the case of typing the name of C++ overloaded functions (multiple definitions of the same function, distinguished by argument type). For example, when you want to set a breakpoint you don't need to distinguish whether you mean the version of `name` that takes an `int` parameter, `name(int)`, or the version that takes a `float` parameter, `name(float)`.

::: smallexample

```bash
(gdb) b bubble(M-?
bubble(int)    bubble(double)
(gdb) b bubble(douM-?
bubble(double)
```

:::

See [quoting names](Symbols.html#quoting-names) for a description of other scenarios that require quoting.

For more information about overloaded functions, see [C++ Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions). You can use the command `set overload-resolution off` to disable overload resolution; see [[GDB] Features for C++](Debugging-C-Plus-Plus.html#Debugging-C-Plus-Plus).

When completing in an expression which looks up a field in a structure, [GDB] to limit completions to the field names available in the type of the left-hand-side:

::: smallexample

```bash
(gdb) p gdb_stdout.M-?
magic                to_fputs             to_rewind
to_data              to_isatty            to_write
to_delete            to_put               to_write_async_safe
to_flush             to_read
```

:::

This is because the `gdb_stdout` is a variable of the type `struct ui_file` that is defined in [GDB] sources as follows:

::: smallexample

```bash
struct ui_file
{
   int *magic;
   ui_file_flush_ftype *to_flush;
   ui_file_write_ftype *to_write;
   ui_file_write_async_safe_ftype *to_write_async_safe;
   ui_file_fputs_ftype *to_fputs;
   ui_file_read_ftype *to_read;
   ui_file_delete_ftype *to_delete;
   ui_file_isatty_ftype *to_isatty;
   ui_file_rewind_ftype *to_rewind;
   ui_file_put_ftype *to_put;
   void *to_data;
}
```

:::

::: footnote

---

#### Footnotes

### [(3)](#DOCF3)

The completer can be confused by certain kinds of invalid expressions. Also, it only examines the static type of the expression, not the dynamic type.
:::

---

::: header
Next: [Command Options](Command-Options.html#Command-Options)]
:::
