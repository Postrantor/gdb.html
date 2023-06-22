---
description: Commands In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Commands In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Commands In Guile (Debugging with GDB)
---
::: header
Next: [Parameters In Guile](Parameters-In-Guile.html#Parameters-In-Guile)]
:::

---

#### 23.4.3.11 Commands In Guile

You can implement new [GDB] from `make-command`.

There is no support for multi-line commands, that is commands that consist of multiple lines and are terminated with `end`.

*

:   The argument `name` consists of multiple words, then the initial words are looked for as prefix commands. In this case, if one of the prefix commands does not exist, an exception is raised.

```
The result is the `<gdb:command>` object representing the command. The command is not usable until it has been registered with [GDB] with `register-command!`.

The rest of the arguments are optional.

The argument `invoke` `error` call. Otherwise, the return value is ignored.

The argument `command-class` how to categorize the new command in the help system. The default is `COMMAND_NONE`.

The argument `completer` how to perform completion for this command. If not provided or if the value is `#f`, then no completion is performed on the command.

The argument `prefix` is a boolean flag indicating whether the new command is a prefix command; sub-commands of this command may be registered.

The argument `doc-string` is help text for the new command. If no documentation string is provided, the default value "This command is not documented." is used.
```

```
<!-- -->
```

Scheme Procedure: **register-command!** *command*

:   Add `command`'s list of commands. It is an error to register a command more than once. The result is unspecified.

```
<!-- -->
```

Scheme Procedure: **command?** *object*

:   Return `#t` if `object` is a `<gdb:command>` object. Otherwise return `#f`.

Scheme Procedure: **dont-repeat**

:   By default, a [GDB] command is repeated when the user enters a blank line at the command prompt. A command can suppress this behavior by invoking the `dont-repeat` function. This is similar to the user command `dont-repeat`, see [dont-repeat](Define.html#Define).

```
<!-- -->
```

Scheme Procedure: **string-\>argv** *string*

:   Convert a string to a list of strings split up according to [GDB]'s argv parsing rules. It is recommended to use this for consistency. Arguments are separated by spaces and may be quoted. Example:

```
::: smallexample
``` smallexample
scheme@(guile-user)> (string->argv "1 2\\ \\\"3 '4 \"5' \"6 '7\"")
$1 = ("1" "2 \"3" "4 \"5" "6 '7")
```

:::

```

```

<!-- -->

```

Scheme Procedure: **throw-user-error** *message . args*

:   Throw a `gdb:user-error` exception. The argument `message`.

```

This is used when the command detects a user error of some kind, say a bad command argument.

::: smallexample

```bash
(gdb) guile (use-modules (gdb))
(gdb) guile
(register-command! (make-command "test-user-error"
  #:command-class COMMAND_OBSCURE
  #:invoke (lambda (self arg from-tty)
    (throw-user-error "Bad argument ~a" arg))))
end
(gdb) test-user-error ugh
ERROR: Bad argument ugh
```

:::

```



completer: **self** *text word*

:   If the `completer` holds the last word of the command line; this is computed using a word-breaking heuristic.

```

All forms of completion are handled by this function, that is, the TAB and M-? key bindings (see [Completion](Completion.html#Completion)), and the `complete` command (see [complete](Help.html#Help)).

This procedure can return several kinds of values:

- If the return value is a list, the contents of the list are used as the completions. It is up to `completer` to ensure that the contents actually do complete the word. An empty list is allowed, it means that there were no completions available. Only string elements of the list are used; other elements in the list are ignored.
- If the return value is a `<gdb:iterator>` object, it is iterated over to obtain the completions. It is up to `completer-procedure` to ensure that the results actually do complete the word. Only string elements of the result are used; other elements in the sequence are ignored.
- All other results are treated as though there were no available completions.

```

When a new command is registered, it will have been declared as a member of some general class of commands. This is used to classify top-level commands in the on-line help system; note that prefix commands are not listed under their own category but rather that of their top-level command. The available classifications are represented by constants defined in the `gdb` module:

`COMMAND_NONE` 

:   The command does not belong to any particular class. A command in this category will not be displayed in any of the help categories. This is the default.

`COMMAND_RUNNING` 

:   The command is related to running the inferior. For example, `start`, `step`, and `continue` are in this category. Type [help running] prompt to see a list of commands in this category.

`COMMAND_DATA` 

:   The command is related to data or variables. For example, `call`, `find`, and `print` are in this category. Type [help data] prompt to see a list of commands in this category.

`COMMAND_STACK` 

:   The command has to do with manipulation of the stack. For example, `backtrace`, `frame`, and `return` are in this category. Type [help stack] prompt to see a list of commands in this category.

`COMMAND_FILES` 

:   This class is used for file-related commands. For example, `file`, `list` and `section` are in this category. Type [help files] prompt to see a list of commands in this category.

`COMMAND_SUPPORT` 

:   This should be used for "support facilities", generally meaning things that are useful to the user when interacting with [GDB] prompt to see a list of commands in this category.

`COMMAND_STATUS` 

:   The command is an '`info` prompt to see a list of commands in this category.

`COMMAND_BREAKPOINTS` 

:   The command has to do with breakpoints. For example, `break`, `clear`, and `delete` are in this category. Type [help breakpoints] prompt to see a list of commands in this category.

`COMMAND_TRACEPOINTS` 

:   The command has to do with tracepoints. For example, `trace`, `actions`, and `tfind` are in this category. Type [help tracepoints] prompt to see a list of commands in this category.

`COMMAND_USER` 

:   The command is a general purpose command for the user, and typically does not fit in one of the other categories. Type [help user-defined] prompt to see a list of commands in this category, as well as the list of gdb macros (see [Sequences](Sequences.html#Sequences)).

`COMMAND_OBSCURE` 

:   The command is only used in unusual circumstances, or is not of general interest to users. For example, `checkpoint`, `fork`, and `stop` are in this category. Type [help obscure] prompt to see a list of commands in this category.

`COMMAND_MAINTENANCE` 

:   The command is only useful to [GDB] prompt to see a list of commands in this category.

A new command can use a predefined completion function, either by specifying it via an argument at initialization, or by returning it from the `completer` procedure. These predefined completion constants are all defined in the `gdb` module:

`COMPLETE_NONE` 

:   This constant means that no completion should be done.

`COMPLETE_FILENAME` 

:   This constant means that filename completion should be performed.

`COMPLETE_LOCATION` 

:   This constant means that location completion should be done. See [Location Specifications](Location-Specifications.html#Location-Specifications).

`COMPLETE_COMMAND` 

:   This constant means that completion should examine [GDB] command names.

`COMPLETE_SYMBOL` 

:   This constant means that completion should be done using symbol names as the source.

`COMPLETE_EXPRESSION` 

:   This constant means that completion should be done on expressions. Often this means completing on symbol names, but some language parsers also have support for completing on field names.

The following code snippet shows how a trivial CLI command can be implemented in Guile:

::: smallexample

```bash
(gdb) guile
(register-command! (make-command "hello-world"
  #:command-class COMMAND_USER
  #:doc "Greet the whole world."
  #:invoke (lambda (self args from-tty) (display "Hello, World!\n"))))
end
(gdb) hello-world
Hello, World!
```

:::

---

::: header
Next: [Parameters In Guile](Parameters-In-Guile.html#Parameters-In-Guile)]
:::
