---
tip: translate by openai@2023-06-23 23:01:57
...
---
description: Guile Exception Handling (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Exception Handling (Debugging with GDB)
lang: en
resource-type: document
title: Guile Exception Handling (Debugging with GDB)
---
::: header
Next: [Values From Inferior In Guile](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile)]
:::

---

#### 23.4.3.4 Guile Exception Handling


When executing the `guile` command, Guile exceptions uncaught within the Guile code are translated to calls to the [GDB] will terminate it and report the error according to the setting of the `guile print-stack` parameter.

> 当执行`guile`命令时，Guile代码中未捕获的Guile异常将被转换为对[GDB]的调用，它将终止并根据`guile print-stack`参数的设置报告错误。

The `guile print-stack` parameter has three settings:

`none`

:   Nothing is printed.

`message`


:   An error message is printed containing the Guile exception name, the associated value, and the Guile call stack backtrace at the point where the exception was raised. Example:

> 打印出一条错误信息，其中包含Guile异常名称、关联值以及异常被触发时的Guile调用堆栈回溯。例子：

```
::: smallexample
``` smallexample
(gdb) guile (display foo)
ERROR: In procedure memoize-variable-access!:
ERROR: Unbound variable: foo
Error while executing Scheme code.
```

:::

```

`full`

:   In addition to an error message a full backtrace is printed.

```

::: smallexample

```bash
(gdb) set guile print-stack full
(gdb) guile (display foo)
Guile Backtrace:
In ice-9/boot-9.scm:
 157: 10 [catch #t #<catch-closure 2c76e20> ...]
In unknown file:
   ?: 9 [apply-smob/1 #<catch-closure 2c76e20>]
In ice-9/boot-9.scm:
 157: 8 [catch #t #<catch-closure 2c76d20> ...]
In unknown file:
   ?: 7 [apply-smob/1 #<catch-closure 2c76d20>]
   ?: 6 [call-with-input-string "(display foo)" ...]
In ice-9/boot-9.scm:
2320: 5 [save-module-excursion #<procedure 2c2dc30 ... ()>]
In ice-9/eval-string.scm:
  44: 4 [read-and-eval #<input: string 27cb410> #:lang ...]
  37: 3 [lp (display foo)]
In ice-9/eval.scm:
 387: 2 [eval # ()]
 393: 1 [eval #<memoized foo> ()]
In unknown file:
   ?: 0 [memoize-variable-access! #<memoized foo> ...]

ERROR: In procedure memoize-variable-access!:
ERROR: Unbound variable: foo
Error while executing Scheme code.
```

:::

```


[GDB] commands invoked by Guile code are converted to Guile exceptions. The type of the Guile exception depends on the error.

> 当Guile代码调用[GDB]命令时，其会被转换为Guile异常。Guile异常的类型取决于错误类型。


Guile procedures provided by [GDB] can throw the standard Guile exceptions like `wrong-type-arg` and `out-of-range`.

> GDB提供的Guile过程可以抛出标准的Guile异常，比如`wrong-type-arg`和`out-of-range`。


User interrupt (via [C-c] at a pagination prompt) is translated to a Guile `signal` exception with value `SIGINT`.

> 用户中断（通过[C-c]在分页提示处）被转换为Guile的`signal`异常，值为`SIGINT`。

[GDB] Guile procedures can also throw these exceptions:

`gdb:error` 

:   This exception is a catch-all for errors generated from within [GDB].

`gdb:invalid-object` 


:   This exception is thrown when accessing Guile objects that wrap underlying [GDB] objects have become invalid. For example, a `<gdb:breakpoint>` object becomes invalid if the user deletes it from the command line. The object still exists in Guile, but the object it represents is gone. Further operations on this breakpoint will throw this exception.

> 这个异常会在访问封装了底层[GDB]对象的Guile对象时被抛出。例如，如果用户从命令行中删除了`<gdb:breakpoint>`对象，那么这个对象就会变得无效。该对象仍然存在于Guile中，但它代表的对象却不见了。对这个断点的进一步操作将会抛出此异常。

`gdb:memory-error` 


:   This exception is thrown when an operation tried to access invalid memory in the inferior.

> 这个异常被抛出时，操作试图访问次级无效的内存。

`gdb:pp-type-error` 


:   This exception is thrown when a Guile pretty-printer passes a bad object to [GDB].

> 这个异常会在Guile的美化打印机传递一个坏对象给GDB时抛出。


The following exception-related procedures are provided by the `(gdb)` module.

> 以下异常相关的程序由`(gdb)`模块提供。

Scheme Procedure: **make-exception** *key args*


:   Return a `<gdb:exception>` object given by its `key`, which are the standard Guile parameters of an exception. See the Guile documentation for more information (see [Exceptions](http://www.gnu.org/software/guile/manual/html_node/Exceptions.html#Exceptions) in GNU Guile Reference Manual).

> 返回一个给定key的<gdb:exception>对象，这是Guile异常的标准参数。有关更多信息，请参阅GNU Guile参考手册中的[异常](http://www.gnu.org/software/guile/manual/html_node/Exceptions.html#Exceptions)。

```

<!-- -->

```

Scheme Procedure: **exception?** *object*


:   Return `#t` if `object` is a `<gdb:exception>` object. Otherwise return `#f`.

> 如果对象是<gdb:exception>对象，则返回#t，否则返回#f。

```

<!-- -->

```

Scheme Procedure: **exception-key** *exception*

:   Return the `args` field of a `<gdb:exception>` object.

```

<!-- -->

```

Scheme Procedure: **exception-args** *exception*

:   Return the `args` field of a `<gdb:exception>` object.

---

::: header
Next: [Values From Inferior In Guile](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile)]
:::
```
