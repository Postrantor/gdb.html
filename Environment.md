---
tip: translate by openai@2023-06-23 20:51:06
...
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

> 环境由一组环境变量及其值组成。环境变量通常记录用户名、家目录、终端类型和程序运行的搜索路径等信息。通常，你可以使用shell设置环境变量，并且其他程序可以继承这些变量。在调试时，可以使用修改后的环境来运行程序，而不必重新启动[GDB]。

`path directory`


Add `directory` is already in the path, it is moved to the front, so it is searched sooner.

> 将`directory`添加到路径中，它已经被移动到前面，因此会更早地被搜索到。

You can use the string '`$cwd` to the search path.

`show paths`


Display the list of search paths for executables (the `PATH` environment variable).

> 显示可执行文件的搜索路径列表（`PATH`环境变量）。

`show environment [varname]`


Print the value of environment variable `varname`, print the names and values of all environment variables to be given to your program. You can abbreviate `environment` as `env`.

> 打印环境变量`varname`的值，打印给你的程序的所有环境变量的名称和值。你可以将`environment`简写为`env`。

`set environment varname [=value]`


Set environment variable `varname` parameter is optional; if it is eliminated, the variable is set to a null value.

> 如果省略`varname`参数，则设置环境变量为空值。

For example, this command:

::: smallexample

```bash
set env USER = foo
```

:::


tells the debugged program, when subsequently run, that its user is named '`foo`' are used for clarity here; they are not actually required.)

> 告诉调试后的程序，当它被运行时，它的用户名是'foo'（这里仅仅是为了清晰起见而使用，实际上不是必需的）。


Note that on Unix systems, [GDB]' program as a wrapper instead of using `set environment`. See [set exec-wrapper](Starting.html#set-exec_002dwrapper), for an example doing just that.

> 在Unix系统上，可以使用[GDB]程序作为一个包装器，而不是使用`set environment`。有关使用[set exec-wrapper]做到这一点的示例，请参阅Starting.html#set-exec_002dwrapper。


Environment variables that are set by the user are also transmitted to `gdbserver` to be used when starting the remote inferior. see [QEnvironmentHexEncoded](General-Query-Packets.html#QEnvironmentHexEncoded).

> 用户设置的环境变量也会传递给`gdbserver`，以便在启动远程子程序时使用。参见[QEnvironmentHexEncoded](General-Query-Packets.html#QEnvironmentHexEncoded)。

`unset environment varname`


Remove variable `varname`'; `unset environment` removes the variable from the environment, rather than assigning it an empty value.

> 移除变量`varname`；`unset environment` 将变量从环境中移除，而不是为其赋值为空值。


Environment variables that are unset by the user are also unset on `gdbserver` when starting the remote inferior. see [QEnvironmentUnset](General-Query-Packets.html#QEnvironmentUnset).

> 用户未设置的环境变量，在启动远程子程序时也会在`gdbserver`上未设置。请参阅[QEnvironmentUnset](General-Query-Packets.html#QEnvironmentUnset)。

*Warning:* On Unix systems, [GDB].

---

::: header
Next: [Working Directory](Working-Directory.html#Working-Directory)]
:::
