---
description: CLI Commands In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: CLI Commands In Python (Debugging with GDB)
lang: en
resource-type: document
title: CLI Commands In Python (Debugging with GDB)
---
::: header
Next: [GDB/MI Commands In Python](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python)]
:::

---

#### 23.3.2.20 CLI Commands In Python

You can implement new [GDB] CLI commands in Python. A CLI command is implemented using an instance of the `gdb.Command` class, most commonly using a subclass.

)*

:   The object initializer for `Command` registers the new command with [GDB]. This initializer is normally invoked from the subclass' own `__init__` method.

```
`name` consists of multiple words, then the initial words are looked for as prefix commands. In this case, if one of the prefix commands does not exist, an exception is raised.

There is no support for multi-line commands.

`command_class` how to categorize the new command in the help system.

`completer_class` will attempt to complete using the object's `complete` method (see below); if no such method is found, an error will occur when completion is attempted.

`prefix` is an optional argument. If `True`, then the new command is a prefix command; sub-commands of this command may be registered.

The help text for the new command is taken from the Python documentation string for the command's class, if there is one. If no documentation string is provided, the default value "This command is not documented." is used.
```

Function: **Command.dont_repeat** *()*

:   By default, a [GDB] command is repeated when the user enters a blank line at the command prompt. A command can suppress this behavior by invoking the `dont_repeat` method at some point in its `invoke` method (normally this is done early in case of exception). This is similar to the user command `dont-repeat`, see [dont-repeat](Define.html#Define).

```
<!-- -->
```

Function: **Command.invoke** *(argument, from_tty)*

:   This method is called by [GDB] when this command is invoked.

```
`argument` is a string. It is the argument to the command, after leading and trailing whitespace has been stripped.

`from_tty` is a boolean argument. When true, this means that the command was entered by the user at the terminal; when false it means that the command came from elsewhere.

If this method throws an exception, it is turned into a [GDB] `error` call. Otherwise, the return value is ignored.



To break `argument`'s internal argument lexer `buildargv`. It is recommended to use this for consistency. Arguments are separated by spaces and may be quoted. Example:

::: smallexample
``` smallexample
print gdb.string_to_argv ("1 2\ \\\"3 '4 \"5' \"6 '7\"")
['1', '2 "3', '4 "5', "6 '7"]
```

:::

```



Function: **Command.complete** *(text, word)*

:   This method is called by [GDB] when the user attempts completion on this command. All forms of completion are handled by this method, that is, the TAB and M-? key bindings (see [Completion](Completion.html#Completion)), and the `complete` command (see [complete](Help.html#Help)).

```

The arguments `text` holds the last word of the command line; this is computed using a word-breaking heuristic.

The `complete` method can return several values:

- If the return value is a sequence, the contents of the sequence are used as the completions. It is up to `complete` to ensure that the contents actually do complete the word. A zero-length sequence is allowed, it means that there were no completions available. Only string elements of the sequence are used; other elements in the sequence are ignored.
- If the return value is one of the '`COMPLETE_`-internal completion function is invoked, and its result is used.
- All other results are treated as though there were no available completions.

```

When a new command is registered, it must be declared as a member of some general class of commands. This is used to classify top-level commands in the on-line help system; note that prefix commands are not listed under their own category but rather that of their top-level command. The available classifications are represented by constants defined in the `gdb` module:



`gdb.COMMAND_NONE`

The command does not belong to any particular class. A command in this category will not be displayed in any of the help categories.



`gdb.COMMAND_RUNNING`

The command is related to running the inferior. For example, `start`, `step`, and `continue` are in this category. Type [help running] prompt to see a list of commands in this category.



`gdb.COMMAND_DATA`

The command is related to data or variables. For example, `call`, `find`, and `print` are in this category. Type [help data] prompt to see a list of commands in this category.



`gdb.COMMAND_STACK`

The command has to do with manipulation of the stack. For example, `backtrace`, `frame`, and `return` are in this category. Type [help stack] prompt to see a list of commands in this category.



`gdb.COMMAND_FILES`

This class is used for file-related commands. For example, `file`, `list` and `section` are in this category. Type [help files] prompt to see a list of commands in this category.



`gdb.COMMAND_SUPPORT`

This should be used for "support facilities", generally meaning things that are useful to the user when interacting with [GDB] prompt to see a list of commands in this category.



`gdb.COMMAND_STATUS`

The command is an '`info` prompt to see a list of commands in this category.



`gdb.COMMAND_BREAKPOINTS`

The command has to do with breakpoints. For example, `break`, `clear`, and `delete` are in this category. Type [help breakpoints] prompt to see a list of commands in this category.



`gdb.COMMAND_TRACEPOINTS`

The command has to do with tracepoints. For example, `trace`, `actions`, and `tfind` are in this category. Type [help tracepoints] prompt to see a list of commands in this category.



`gdb.COMMAND_TUI`

The command has to do with the text user interface (see [TUI](TUI.html#TUI)). Type [help tui] prompt to see a list of commands in this category.



`gdb.COMMAND_USER`

The command is a general purpose command for the user, and typically does not fit in one of the other categories. Type [help user-defined] prompt to see a list of commands in this category, as well as the list of gdb macros (see [Sequences](Sequences.html#Sequences)).



`gdb.COMMAND_OBSCURE`

The command is only used in unusual circumstances, or is not of general interest to users. For example, `checkpoint`, `fork`, and `stop` are in this category. Type [help obscure] prompt to see a list of commands in this category.



`gdb.COMMAND_MAINTENANCE`

The command is only useful to [GDB] prompt to see a list of commands in this category.

A new command can use a predefined completion function, either by specifying it via an argument at initialization, or by returning it from the `complete` method. These predefined completion constants are all defined in the `gdb` module:



`gdb.COMPLETE_NONE` 

This constant means that no completion should be done.



`gdb.COMPLETE_FILENAME` 

This constant means that filename completion should be performed.



`gdb.COMPLETE_LOCATION` 

This constant means that location completion should be done. See [Location Specifications](Location-Specifications.html#Location-Specifications).



`gdb.COMPLETE_COMMAND` 

This constant means that completion should examine [GDB] command names.



`gdb.COMPLETE_SYMBOL` 

This constant means that completion should be done using symbol names as the source.



`gdb.COMPLETE_EXPRESSION` 

This constant means that completion should be done on expressions. Often this means completing on symbol names, but some language parsers also have support for completing on field names.

The following code snippet shows how a trivial CLI command can be implemented in Python:

::: smallexample

```bash
class HelloWorld (gdb.Command):
  """Greet the whole world."""

  def __init__ (self):
    super (HelloWorld, self).__init__ ("hello-world", gdb.COMMAND_USER)

  def invoke (self, arg, from_tty):
    print ("Hello, World!")

HelloWorld ()
```

:::

The last line instantiates the class, and is necessary to trigger the registration of the command with [GDB], you may need to import the `gdb` module explicitly.

---

::: header
Next: [GDB/MI Commands In Python](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python)]
:::
