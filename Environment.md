---
description: Environment (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Environment (Debugging with GDB)
lang: en
resource-type: document
title: Environment (Debugging with GDB)
---
::: header
Next: [Working Directory](Working-Directory.html#Working-Directory)]
:::

---

### 4.4 Your Program's Environment

The *environment* consists of a set of environment variables and their values. Environment variables conventionally record such things as your user name, your home directory, your terminal type, and your search path for programs to run. Usually you set up environment variables with the shell and they are inherited by all the other programs you run. When debugging, it can be useful to try running your program with a modified environment without having to start [GDB] over again.

`path directory`

Add `directory` is already in the path, it is moved to the front, so it is searched sooner.

You can use the string '`$cwd` to the search path.

`show paths`

Display the list of search paths for executables (the `PATH` environment variable).

`show environment [varname]`

Print the value of environment variable `varname`, print the names and values of all environment variables to be given to your program. You can abbreviate `environment` as `env`.

`set environment varname [=value]`

Set environment variable `varname` parameter is optional; if it is eliminated, the variable is set to a null value.

For example, this command:

::: smallexample

```bash
set env USER = foo
```

:::

tells the debugged program, when subsequently run, that its user is named '`foo`' are used for clarity here; they are not actually required.)

Note that on Unix systems, [GDB]' program as a wrapper instead of using `set environment`. See [set exec-wrapper](Starting.html#set-exec_002dwrapper), for an example doing just that.

Environment variables that are set by the user are also transmitted to `gdbserver` to be used when starting the remote inferior. see [QEnvironmentHexEncoded](General-Query-Packets.html#QEnvironmentHexEncoded).

`unset environment varname`

Remove variable `varname`'; `unset environment` removes the variable from the environment, rather than assigning it an empty value.

Environment variables that are unset by the user are also unset on `gdbserver` when starting the remote inferior. see [QEnvironmentUnset](General-Query-Packets.html#QEnvironmentUnset).

*Warning:* On Unix systems, [GDB].

---

::: header
Next: [Working Directory](Working-Directory.html#Working-Directory)]
:::
