---
description: Basic Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Basic Python (Debugging with GDB)
lang: en
resource-type: document
title: Basic Python (Debugging with GDB)
---
::: header
Next: [Exception Handling](Exception-Handling.html#Exception-Handling)]
:::

---

#### 23.3.2.1 Basic Python

At startup, [GDB]'s output-paging streams. A Python program which outputs to one of these streams may have its output interrupted by the user (see [Screen Size](Screen-Size.html#Screen-Size)). In this situation, a Python `KeyboardInterrupt` exception is thrown.

Some care must be taken when writing Python code to run in [GDB]. Two things worth noting in particular:

- [GDB] will most likely stop working correctly. Note that it is unfortunately common for GUI toolkits to install a `SIGCHLD` handler.
- [GDB] takes care to mark its internal file descriptors as close-on-exec. However, this cannot be done in a thread-safe way on all platforms. Your Python programs should be aware of this and should both create new file descriptors with the close-on-exec flag set and arrange to close unneeded file descriptors before starting a child process.

[GDB] automatically `import` s the `gdb` module for use in all scripts evaluated by the `python` command.

Some types of the `gdb` module come with a textual representation (accessible through the `repr` or `str` functions). These are offered for debugging purposes only, expect them to change over time.

Variable: **gdb.PYTHONDIR**

:   A string containing the python directory (see [Python](Python.html#Python)).

)*

:   Evaluate `command` runs, it is translated as described in [Exception Handling](Exception-Handling.html#Exception-Handling).

```
The `from_tty` ought to consider this command as having originated from the user invoking it interactively. It must be a boolean value. If omitted, it defaults to `False`.

By default, any output produced by `command` virtual terminal will be temporarily set to unlimited width and height, and its pagination will be disabled; see [Screen Size](Screen-Size.html#Screen-Size).
```

Function: **gdb.breakpoints** *()*

:   Return a sequence holding all of [GDB] version 7.11 and earlier, this function returned `None` if there were no breakpoints. This peculiarity was subsequently fixed, and now `gdb.breakpoints` returns an empty sequence in this case.

```
<!-- -->
```

)*

:   Return a Python list holding a collection of newly set `gdb.Breakpoint` objects matching function names defined by the `regex` keyword takes a Python iterable that yields a collection of `gdb.Symtab` objects and will restrict the search to those functions only contained within the `gdb.Symtab` objects.

Function: **gdb.parameter** *(parameter)*

:   Return the value of a [GDB]' is a valid parameter name.

```
If the named parameter does not exist, this function throws a `gdb.error` (see [Exception Handling](Exception-Handling.html#Exception-Handling)). Otherwise, the parameter's value is converted to a Python value of the appropriate type, and returned.
```

Function: **gdb.set_parameter** *(name, value)*

:   Sets the gdb parameter `name`. As with `gdb.parameter`, the parameter name string may contain spaces if the parameter has a multi-part name.

Function: **gdb.with_parameter** *(name, value)*

:   Create a Python context manager (for use with the Python `with` statement) that temporarily sets the gdb parameter `name`. On exit from the context, the previous value will be restored.

```
This uses `gdb.parameter` in its implementation, so it can throw the same exceptions as that function.

For example, it's sometimes useful to evaluate some Python code with a particular gdb language:

::: smallexample
``` smallexample
with gdb.with_parameter('language', 'pascal'):
  ... language-specific operations
```

:::

```



Function: **gdb.history** *(number)*

:   Return a value from [GDB] doesn't exist in the value history, a `gdb.error` exception will be raised.

```

If no exception is raised, the return value is always an instance of `gdb.Value` (see [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)).

```

```

<!-- -->

```

Function: **gdb.add_history** *(value)*

:   Takes `value` can't be converted to a `gdb.Value` then a `TypeError` is raised.

```

When a command implemented in Python prints a single `gdb.Value` as its result, then placing the value into the history will allow the user convenient access to those values via CLI history facilities.

```

```

<!-- -->

```

Function: **gdb.history_count** *()*

:   Return an integer indicating the number of values in [GDB]'s value history (see [Value History](Value-History.html#Value-History)).



Function: **gdb.convenience_variable** *(name)*

:   Return the value of the convenience variable (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) named `name`' that is used to mark a convenience variable in an expression. If the convenience variable does not exist, then `None` is returned.



Function: **gdb.set_convenience_variable** *(name, value)*

:   Set the value of the convenience variable (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) named `name` is not a `gdb.Value` (see [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)), it is is converted using the `gdb.Value` constructor.



)*

:   Parse `expression`, which must be a string, as an expression in the current language, evaluate it, and return the result as a `gdb.Value`.

```

`global_context`', meaning that the current frame or current static context should be used.

This function can be useful when implementing a new command (see [CLI Commands In Python](CLI-Commands-In-Python.html#CLI-Commands-In-Python), see [GDB/MI Commands In Python](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python)), as it provides a way to parse the command's argument as an expression. It is also useful simply to compute values.

```



Function: **gdb.find_pc_line** *(pc)*

:   Return the `gdb.Symtab_and_line` object corresponding to the `pc` is passed as an argument, then the `symtab` and `line` attributes of the returned `gdb.Symtab_and_line` object will be `None` and 0 respectively. This is identical to `gdb.current_progspace().find_pc_line(pc)` and is included for historical compatibility.



Function: **gdb.post_event** *(event)*

:   Put `event`.

```

[GDB] thread. `post_event` ensures this. For example:

::: smallexample

```bash
(gdb) python
>import threading
>
>class Writer():
> def __init__(self, message):
>        self.message = message;
> def __call__(self):
>        gdb.write(self.message)
>
>class MyThread1 (threading.Thread):
> def run (self):
>        gdb.post_event(Writer("Hello "))
>
>class MyThread2 (threading.Thread):
> def run (self):
>        gdb.post_event(Writer("World\n"))
>
>MyThread1().start()
>MyThread2().start()
>end
(gdb) Hello World
```

:::

```



)*

:   Print a string to [GDB]'s standard output stream. Possible stream values are:

:   

`gdb.STDOUT`

:   [GDB]'s standard output stream.

```

```

`gdb.STDERR`

:   [GDB]'s standard error stream.

```

```

`gdb.STDLOG`

:   [GDB]'s log stream (see [Logging Output](Logging-Output.html#Logging-Output)).

Writing to `sys.stdout` or `sys.stderr` will automatically call this function and will automatically direct the output to the relevant stream.



)*

:   Flush the buffer of a [GDB]'s standard output stream. Possible stream values are:

:   

`gdb.STDOUT`

:   [GDB]'s standard output stream.

```

```

`gdb.STDERR`

:   [GDB]'s standard error stream.

```

```

`gdb.STDLOG`

:   [GDB]'s log stream (see [Logging Output](Logging-Output.html#Logging-Output)).

Flushing `sys.stdout` or `sys.stderr` will automatically call this function for the relevant stream.



Function: **gdb.target_charset** *()*

:   Return the name of the current target character set (see [Character Sets](Character-Sets.html#Character-Sets)). This differs from `gdb.parameter('target-charset')` in that '`auto`' is never returned.



Function: **gdb.target_wide_charset** *()*

:   Return the name of the current target wide character set (see [Character Sets](Character-Sets.html#Character-Sets)). This differs from `gdb.parameter('target-wide-charset')` in that '`auto`' is never returned.



Function: **gdb.host_charset** *()*

:   Return a string, the name of the current host character set (see [Character Sets](Character-Sets.html#Character-Sets)). This differs from `gdb.parameter('host-charset')` in that '`auto`' is never returned.



Function: **gdb.solib_name** *(address)*

:   Return the name of the shared library holding the given `address` as a string, or `None`. This is identical to `gdb.current_progspace().solib_name(address)` and is included for historical compatibility.



)*

:   Return locations of the line specified by `expression`'s inbuilt `break` or `edit` commands do (see [Location Specifications](Location-Specifications.html#Location-Specifications)).

```

<!-- -->

```

Function: **gdb.prompt_hook** *(current_prompt)*

:   

```

If `prompt_hook`.

The parameter `current_prompt` contains the current [GDB] will continue to use the current prompt.

Some prompts cannot be substituted in [GDB]. Secondary prompts such as those used by readline for command input, and annotation related prompts are prohibited from being changed.

```



Function: **gdb.architecture_names** *()*

:   Return a list containing all of the architecture names that the current build of [GDB] supports. Each architecture name is a string. The names returned in this list are the same names as are returned from `gdb.Architecture.name` (see [Architecture.name](Architectures-In-Python.html#gdbpy_005farchitecture_005fname)).



Function: **gdb.connections**

:   Return a list of `gdb.TargetConnection` objects, one for each currently active connection (see [Connections In Python](Connections-In-Python.html#Connections-In-Python)). The connection objects are in no particular order in the returned list.

```

<!-- -->

```

)*

:   Return a string in the format '`addr <symbol+offset>` in decimal.

```

If no suitable `symbol` (see [Print Settings](Print-Settings.html#Print-Settings)).

Additionally, the returned string can include file name and line number information when [set print symbol-filename on]'.

The `progspace`, e.g. in order to determine the size of an address in bytes.

If neither `progspace` will use the program space and architecture of the currently selected inferior, thus, the following two calls are equivalent:

::: smallexample

```bash
gdb.format_address(address)
gdb.format_address(address,
                   gdb.selected_inferior().progspace,
                   gdb.selected_inferior().architecture())
```

:::

It is not valid to only pass one of `progspace`, either they must both be provided, or neither must be provided (and the defaults will be used).

This method uses the same mechanism for formatting address, symbol, and offset information as core [GDB].

Here are some examples of the possible string formats:

::: smallexample

```bash
0x00001042
0x00001042 <symbol+16>
0x00001042 <symbol+16 at file.c:123>
```

:::

```

```

<!-- -->

```

Function: **gdb.current_language** *()*

:   Return the name of the current language as a string. Unlike `gdb.parameter('language')`, this function will never return '`auto`'. If a `gdb.Frame` object is available (see [Frames In Python](Frames-In-Python.html#Frames-In-Python)), the `language` method might be preferable in some cases, as that is not affected by the user's language setting.

---

::: header
Next: [Exception Handling](Exception-Handling.html#Exception-Handling)]
:::
```
