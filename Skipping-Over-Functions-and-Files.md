---
description: Skipping Over Functions and Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Skipping Over Functions and Files (Debugging with GDB)
lang: en
resource-type: document
title: Skipping Over Functions and Files (Debugging with GDB)
---
::: header
Next: [Signals](Signals.html#Signals)]
:::

---

### 5.3 Skipping Over Functions and Files

The program you are debugging may contain some functions which are uninteresting to debug. The `skip` command lets you tell [GDB] to skip a function, all functions in a file or a particular function in a particular file when stepping.

For example, consider the following C function:

::: smallexample

```bash
101     int func()
102     {
103         foo(boring());
104         bar(boring());
105     }
```

:::

Suppose you wish to step into the functions `foo` and `bar`, but you are not interested in stepping through `boring`. If you run `step` at line 103, you'll enter `boring()`, but if you run `next`, you'll step over both `foo` and `boring`!

One solution is to `step` into `boring` and use the `finish` command to immediately exit it. But this can become tedious if `boring` is called from many places.

A more flexible solution is to execute [skip boring] never to step into `boring`. Now when you execute `step` at line 103, you'll step over `boring` and directly into `foo`.

Functions may be skipped by providing either a function name, linespec (see [Location Specifications](Location-Specifications.html#Location-Specifications)), regular expression that matches the function's name, file name or a `glob`-style pattern that matches the file name.

On Posix systems the form of the regular expression is "Extended Regular Expressions". See for example '`man 7 regex`/Linux systems for a description of `glob`-style patterns.

`skip [options]`

The basic form of the `skip` command takes zero or more options that specify what to skip. The `options` argument is any useful combination of the following:

`-file file`
`-fi file`

:   Functions in `file` will be skipped over when stepping.

`-gfile file-glob-pattern`
`-gfi file-glob-pattern`

:

```
Functions in files matching `file-glob-pattern` will be skipped over when stepping.

::: smallexample
``` smallexample
(gdb) skip -gfi utils/*.c
```

:::

```

`-function linespec`
`-fu linespec`

:   Functions named by `linespec` will be skipped over when stepping. See [Location Specifications](Location-Specifications.html#Location-Specifications).

`-rfunction regexp`
`-rfu regexp`

:   

```

Functions whose name matches `regexp` will be skipped over when stepping.

This form is useful for complex function names. For example, there is generally no need to step into C++ `std::string` constructors or destructors. Plus with C++ templates it can be hard to write out the full name of the function, and often it doesn't matter what the template arguments are. Specifying the function to be skipped as a regular expression makes this easier.

::: smallexample

```bash
(gdb) skip -rfu ^std::(allocator|basic_string)<.*>::~?\1 *\(
```

:::

If you want to skip every templated C++ constructor and destructor in the `std` namespace you can do:

::: smallexample

```bash
(gdb) skip -rfu ^std::([a-zA-z0-9_]+)<.*>::~?\1 *\(
```

:::

```

If no options are specified, the function you're currently debugging will be skipped.



`skip function [linespec]`

After running this command, the function named by `linespec` will be skipped over when stepping. See [Location Specifications](Location-Specifications.html#Location-Specifications).

If you do not specify `linespec`, the function you're currently debugging will be skipped.

(If you have a function called `file` that you want to skip, use [skip function file].)



`skip file [filename]`

After running this command, any function whose source lives in `filename` will be skipped over when stepping.

::: smallexample

```bash
(gdb) skip file boring.c
File boring.c will be skipped when stepping.
```

:::

If you do not specify `filename`, functions whose source lives in the file you're currently debugging will be skipped.

Skips can be listed, deleted, disabled, and enabled, much like breakpoints. These are the commands for managing your list of skips:

`info skip [range]`

Print details about the specified skip(s). If `range` is not specified, print a table with details about all functions and files marked for skipping. `info skip` prints the following information about each skip:

*Identifier*

:   A number identifying this skip.

*Enabled or Disabled*

:   Enabled skips are marked with '`y`'.

*Glob*

:   If the file name is a '`glob`'.

*File*

:   The name or '`glob`'.

*RE*

:   If the function name is a '`regular expression`'.

*Function*

:   The name or regular expression of the function to skip. If no function is specified this is '`<none>`'.

`skip delete [range]`

Delete the specified skip(s). If `range` is not specified, delete all skips.

`skip enable [range]`

Enable the specified skip(s). If `range` is not specified, enable all skips.

`skip disable [range]`

Disable the specified skip(s). If `range` is not specified, disable all skips.

`set debug skip [on|off]`

Set whether to print the debug output about skipping files and functions.

`show debug skip`

Show whether the debug output about skipping files and functions is printed.

---

::: header
Next: [Signals](Signals.html#Signals)]
:::
