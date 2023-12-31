---
tip: translate by openai@2023-06-23 20:57:11
...
---
description: Exception Handling (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Exception Handling (Debugging with GDB)
lang: en
resource-type: document
title: Exception Handling (Debugging with GDB)
---
::: header
Next: [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)]
:::

---

#### 23.3.2.2 Exception Handling


When executing the `python` command, Python exceptions uncaught within the Python code are translated to calls to [GDB] will terminate it and print an error message containing the Python exception name, the associated value, and the Python call stack backtrace at the point where the exception was raised. Example:

> 当执行`python`命令时，Python代码中未捕获的Python异常将被转换为对[GDB]的调用，这将终止它并打印一条包含Python异常名称、相关值和引发异常时的Python调用堆栈回溯的错误消息。例子：

::: smallexample

```bash
(gdb) python print foo
Traceback (most recent call last):
  File "<string>", line 1, in <module>
NameError: name 'foo' is not defined
```

:::


[GDB] commands invoked by Python code are converted to Python exceptions. The type of the Python exception depends on the error.

> Python代码调用的[GDB]命令会转换为Python异常。Python异常的类型取决于错误。

`gdb.error`

:   This is the base class for most exceptions generated by [GDB].

```
If an error occurring in [GDB] does not fit into some more specific category, then the generated exception will have this type.
```

`gdb.MemoryError`


:   This is a subclass of `gdb.error` which is thrown when an operation tried to access invalid memory in the inferior.

> 这是一个gdb.error的子类，当操作试图访问低级程序中的无效内存时会抛出异常。

`KeyboardInterrupt`


:   User interrupt (via [C-c] at a pagination prompt) is translated to a Python `KeyboardInterrupt` exception.

> 用户中断（通过[C-c]在分页提示符处）被转换为Python的`KeyboardInterrupt`异常。


In all cases, your exception handler will see the [GDB] error occurred as the traceback.

> 在所有情况下，您的异常处理程序都会将[GDB]发生的错误视为跟踪回溯。


When implementing [GDB] provides a special exception class that can be used for this purpose.

> 当实现[GDB]时，提供了一个特殊的异常类，可用于此目的。

`gdb.GdbError`


:   When thrown from a command or function, this exception will cause the command or function to fail, but the Python stack will not be displayed. [GDB] does not throw this exception itself, but rather recognizes it when thrown from user Python code. Example:

> 当从命令或函数抛出时，此异常将导致命令或函数失败，但不会显示Python堆栈。 [GDB]本身不会抛出此异常，而是在用户Python代码抛出时识别它。示例：

```
::: smallexample
``` smallexample
(gdb) python
>class HelloWorld (gdb.Command):
>  """Greet the whole world."""
>  def __init__ (self):
>    super (HelloWorld, self).__init__ ("hello-world", gdb.COMMAND_USER)
>  def invoke (self, args, from_tty):
>    argv = gdb.string_to_argv (args)
>    if len (argv) != 0:
>      raise gdb.GdbError ("hello-world takes no arguments")
>    print ("Hello, World!")
>HelloWorld ()
>end
(gdb) hello-world 42
hello-world takes no arguments
```

:::

```

---

::: header
Next: [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)]
:::
```
