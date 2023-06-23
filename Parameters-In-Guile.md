---
description: Parameters In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Parameters In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Parameters In Guile (Debugging with GDB)
---
::: header
Next: [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile)]
:::

---

#### 23.4.3.12 Parameters In Guile

You can implement new [GDB].

There are many parameters that already exist and can be set in [GDB]. Similarly, you can define parameters that can be used to influence behavior in custom Guile scripts and commands.

A new parameter is defined with the `make-parameter` Guile function, and added to [GDB] from `make-parameter`.

Parameters are exposed to the user via the `set` and `show` commands. See [Help](Help.html#Help).

*

:   The argument `name` consists of multiple words, and no prefix parameter group can be found, an exception is raised.

```
The result is the `<gdb:parameter>` object representing the parameter. The parameter is not usable until it has been registered with [GDB] with `register-parameter!`.

The rest of the arguments are optional.

The argument `command-class` how to categorize the new parameter in the help system. The default is `COMMAND_NONE`.

The argument `parameter-type` the type of the new parameter; this information is used for input validation and completion. The default is `PARAM_BOOLEAN`.

If `parameter-type` must be a list of strings. These strings represent the possible values for the parameter.

If `parameter-type` will cause an exception to be thrown.

The argument `set-func`'. A non-empty string result should typically be used for displaying warnings and errors.

The argument `show-func` will add a trailing newline.

The argument `doc` is the help text for the new parameter. If there is no documentation string, a default value is used.

The argument `set-doc` is the help text for this parameter's `set` command.

The argument `show-doc` is the help text for this parameter's `show` command.

The argument `initial-value` specifies the initial value of the parameter. If it is a function, it takes one parameter, the `<gdb:parameter>` object and its result is used as the initial value of the parameter. The initial value must be valid for the parameter type, otherwise an exception is thrown.
```

```
<!-- -->
```

Scheme Procedure: **register-parameter!** *parameter*

:   Add `parameter`'s list of parameters. It is an error to register a parameter more than once. The result is unspecified.

```
<!-- -->
```

Scheme Procedure: **parameter?** *object*

:   Return `#t` if `object` is a `<gdb:parameter>` object. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **parameter-value** *parameter*

:   Return the value of `parameter` which may either be a `<gdb:parameter>` object or a string naming the parameter.

```
<!-- -->
```

Scheme Procedure: **set-parameter-value!** *parameter new-value*

:   Assign `parameter` does validation when assignments are made.

When a new parameter is defined, its type must be specified. The available types are represented by constants defined in the `gdb` module:

`PARAM_BOOLEAN`

:   The value is a plain boolean. The Guile boolean values, `#t` and `#f` are the only valid values.

`PARAM_AUTO_BOOLEAN`

:   The value has three possible states: true, false, and '`auto`' is represented using `#:auto`.

`PARAM_UINTEGER`

:   The value is an unsigned integer. The value of `#:unlimited` should be interpreted to mean "unlimited", and the value of '`0`' is reserved and should not be used.

`PARAM_ZINTEGER`

:   The value is an integer.

`PARAM_ZUINTEGER`

:   The value is an unsigned integer.

`PARAM_ZUINTEGER_UNLIMITED`

:   The value is an integer in the range '`[0, INT_MAX]`' is reserved and should not be used, and other negative numbers are not allowed.

`PARAM_STRING`

:   The value is a string. When the user modifies the string, any escape sequences, such as '`\t`', and octal escapes, are translated into corresponding characters and encoded into the current host charset.

`PARAM_STRING_NOESCAPE`

:   The value is a string. When the user modifies the string, escapes are passed through untranslated.

`PARAM_OPTIONAL_FILENAME`

:   The value is a either a filename (a string), or `#f`.

`PARAM_FILENAME`

:   The value is a filename. This is just like `PARAM_STRING_NOESCAPE`, but uses file names for completion.

`PARAM_ENUM`

:   The value is a string, which must be one of a collection of string constants provided when the parameter is created.

::: footnote

---

#### Footnotes

### [(20)](#DOCF20)

Note that [GDB] parameters must not be confused with Guileâ€™s parameter objects (see [Parameters](http://www.gnu.org/software/guile/manual/html_node/Parameters.html#Parameters) in GNU Guile Reference Manual).
:::

---

::: header
Next: [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile)]
:::
