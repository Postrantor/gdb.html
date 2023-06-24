---
tip: translate by openai@2023-06-23 18:10:53
...
---
description: Breakpoints In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Breakpoints In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Breakpoints In Guile (Debugging with GDB)
---
::: header
Next: [Lazy Strings In Guile](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile)]
:::

---

#### 23.4.3.19 Manipulating breakpoints using Guile


Breakpoints in Guile are represented by objects of type `<gdb:breakpoint>`. New breakpoints can be created with the `make-breakpoint` Guile function, and then added to [GDB] from `make-breakpoint`.

> 在Guile中，断点由<gdb:breakpoint>类型的对象表示。可以使用`make-breakpoint` Guile函数创建新断点，然后从`make-breakpoint`添加到[GDB]。


Support is also provided to view and manipulate breakpoints created outside of Guile.

> 提供支持以查看和操作在Guile之外创建的断点。


The following breakpoint-related procedures are provided by the `(gdb)` module:

> `(gdb)` 模块提供以下与断点相关的程序：

*


:   Create a new breakpoint at `location`, a string naming the location of the breakpoint, or an expression that defines a watchpoint. The contents can be any location recognized by the `break` command, or in the case of a watchpoint, by the `watch` command.

> 在`location`处创建一个新的断点，`location`是一个字符串，表示断点的位置，或者是一个定义监视点的表达式。内容可以是`break`命令或`watch`命令所识别的任何位置。

```
The breakpoint is initially marked as '`invalid`'. The result is the `<gdb:breakpoint>` object representing the breakpoint.

The optional `type` denotes the breakpoint to create. This argument can be either `BP_BREAKPOINT` or `BP_WATCHPOINT`, and defaults to `BP_BREAKPOINT`.

The optional `wp-class` is `BP_WATCHPOINT`. If a watchpoint class is not provided, it is assumed to be a `WP_WRITE` class.

The optional `internal` argument allows the breakpoint to become invisible to the user. The breakpoint will neither be reported when registered, nor will it be listed in the output from `info breakpoints` (but will be listed with the `maint info breakpoints` command). If an internal flag is not provided, the breakpoint is visible (non-internal).

The optional `temporary` argument makes the breakpoint a temporary breakpoint. Temporary breakpoints are deleted after they have been hit, after which the Guile breakpoint is no longer usable (although it may be re-registered with `register-breakpoint!`).

When a watchpoint is created, [GDB] will try to create a hardware assisted watchpoint. If successful, the type of the watchpoint is changed from `BP_WATCHPOINT` to `BP_HARDWARE_WATCHPOINT` for `WP_WRITE`, `BP_READ_WATCHPOINT` for `WP_READ`, and `BP_ACCESS_WATCHPOINT` for `WP_ACCESS`. If not successful, the type of the watchpoint is left as `WP_WATCHPOINT`.

The available types are represented by constants defined in the `gdb` module:

`BP_BREAKPOINT` 

:   Normal code breakpoint.

`BP_WATCHPOINT` 

:   Watchpoint breakpoint.

`BP_HARDWARE_WATCHPOINT` 

:   Hardware assisted watchpoint. This value cannot be specified when creating the breakpoint.

`BP_READ_WATCHPOINT` 

:   Hardware assisted read watchpoint. This value cannot be specified when creating the breakpoint.

`BP_ACCESS_WATCHPOINT` 

:   Hardware assisted access watchpoint. This value cannot be specified when creating the breakpoint.

`BP_CATCHPOINT` 

:   Catchpoint. This value cannot be specified when creating the breakpoint.

The available watchpoint types are represented by constants defined in the `(gdb)` module:

`WP_READ` 

:   Read only watchpoint.

`WP_WRITE` 

:   Write only watchpoint.

`WP_ACCESS` 

:   Read/Write watchpoint.
```

```
<!-- -->
```


Scheme Procedure: **register-breakpoint!** *breakpoint*

> 注册断点！*断点*


:   Add `breakpoint`'. It is an error to register an already registered breakpoint. The result is unspecified.

> 添加断点。注册已经注册的断点是一个错误，结果是不确定的。

```
<!-- -->
```


Scheme Procedure: **delete-breakpoint!** *breakpoint*

> 方案程序：**删除断点！** *断点*


:   Remove `breakpoint` object. Any further attempt to access the object will throw an exception.

> 移除斷點對象。任何進一步訪問該對象的嘗試都會拋出異常。

```
If `breakpoint`, in which case the breakpoint becomes valid again.
```

```
<!-- -->
```


Scheme Procedure: **breakpoints**

> 方案程序：**断点**


:   Return a list of all breakpoints. Each element of the list is a `<gdb:breakpoint>` object.

> 返回所有断点的列表。列表的每个元素都是一个`<gdb:breakpoint>`对象。

```
<!-- -->
```


Scheme Procedure: **breakpoint?** *object*

> 方案程序：**断点？** *对象*


:   Return `#t` if `object` is a `<gdb:breakpoint>` object, and `#f` otherwise.

> 如果对象是<gdb:breakpoint>对象，则返回#t，否则返回#f。

```
<!-- -->
```


Scheme Procedure: **breakpoint-valid?** *breakpoint*

> 检查程序：**breakpoint-valid?** *breakpoint*


:   Return `#t` if `breakpoint` with `register-breakpoint!`. A `<gdb:breakpoint>` object can become invalid if the user deletes the breakpoint. In this case, the object still exists, but the underlying breakpoint does not. In the cases of watchpoint scope, the watchpoint remains valid even if execution of the inferior leaves the scope of that watchpoint.

> 如果使用register-breakpoint！设置断点，则返回#t。如果用户删除断点，<gdb:breakpoint>对象可能会失效。在这种情况下，对象仍然存在，但底层断点不存在。在监视点范围的情况下，即使下级执行离开该监视点的范围，监视点仍然有效。

```
<!-- -->
```


Scheme Procedure: **breakpoint-number** *breakpoint*

> 方案程序：**断点号** *断点*


:   Return the breakpoint's number --- the identifier used by the user to manipulate the breakpoint.

> 返回断点的编号 --- 用户用来操作断点的标识符。

```
<!-- -->
```


Scheme Procedure: **breakpoint-temporary?** *breakpoint*

> 断点暂时？断点


:   Return `#t` if the breakpoint was created as a temporary breakpoint. Temporary breakpoints are automatically deleted after they've been hit. Calling this procedure, and all other procedures other than `breakpoint-valid?` and `register-breakpoint!`, will result in an error after the breakpoint has been hit (since it has been automatically deleted).

> 如果断点是作为临时断点创建的，则返回“#t”。临时断点在被命中后会自动删除。除了“breakpoint-valid？”和“register-breakpoint！”之外，调用此过程以及其他所有过程都会在断点被命中后出现错误（因为它已被自动删除）。

```
<!-- -->
```


Scheme Procedure: **breakpoint-type** *breakpoint*

> 方案程序：**断点类型** *断点*


:   Return the breakpoint's type --- the identifier used to determine the actual breakpoint type or use-case.

> 返回断点的类型 --- 用于确定实际断点类型或用例的标识符。

```
<!-- -->
```


Scheme Procedure: **breakpoint-visible?** *breakpoint*

> 方案程序：**breakpoint-visible？** *断点*


:   Return `#t` if the breakpoint is visible to the user when hit, or when the '`info breakpoints`' command is run. Otherwise return `#f`.

> 如果断点被用户命中时可见，或者当运行“info breakpoints”命令时可见，则返回#t，否则返回#f。

```
<!-- -->
```


Scheme Procedure: **breakpoint-location** *breakpoint*

> 断点位置方案：**断点**


:   Return the location of the breakpoint, as specified by the user. It is a string. If the breakpoint does not have a location (that is, it is a watchpoint) return `#f`.

> 返回用户指定的断点的位置，它是一个字符串。如果断点没有位置（即它是一个监视点），则返回`#f`。

```
<!-- -->
```


Scheme Procedure: **breakpoint-expression** *breakpoint*

> 方程序：**断点表达式** *断点*


:   Return the breakpoint expression, as specified by the user. It is a string. If the breakpoint does not have an expression (the breakpoint is not a watchpoint) return `#f`.

> 返回由用户指定的断点表达式。它是一个字符串。如果断点没有表达式（断点不是观察点），则返回`#f`。

```
<!-- -->
```


Scheme Procedure: **breakpoint-enabled?** *breakpoint*

> 方案程序：**是否启用断点？** *断点*


:   Return `#t` if the breakpoint is enabled, and `#f` otherwise.

> 如果断点已启用，则返回#t，否则返回#f。

```
<!-- -->
```


Scheme Procedure: **set-breakpoint-enabled!** *breakpoint flag*

> 设置断点启用！*断点标志*


:   Set the enabled state of `breakpoint`. If flag is `#f` it is disabled, otherwise it is enabled.

> 设置断点的启用状态。如果标志为#f，则禁用，否则启用。

```
<!-- -->
```


Scheme Procedure: **breakpoint-silent?** *breakpoint*

> 断点静默？断点


:   Return `#t` if the breakpoint is silent, and `#f` otherwise.

> 如果断点是静默的，则返回#t，否则返回#f。

```
Note that a breakpoint can also be silent if it has commands and the first command is `silent`. This is not reported by the `silent` attribute.
```

```
<!-- -->
```


Scheme Procedure: **set-breakpoint-silent!** *breakpoint flag*

> 设置断点静默！*断点标志*


:   Set the silent state of `breakpoint`. If flag is `#f` the breakpoint is made silent, otherwise it is made non-silent (or noisy).

> 设置断点的静默状态。如果标志为#f，则断点将设为静默，否则将设为非静默（或嘈杂）。

```
<!-- -->
```


Scheme Procedure: **breakpoint-ignore-count** *breakpoint*

> 断点忽略计数：断点


:   Return the ignore count for `breakpoint`.

> 返回`断点`的忽略计数。

```
<!-- -->
```


Scheme Procedure: **set-breakpoint-ignore-count!** *breakpoint count*

> 设置断点忽略计数！*断点计数*


:   Set the ignore count for `breakpoint`.

> 设置断点的忽略计数。

```
<!-- -->
```


Scheme Procedure: **breakpoint-hit-count** *breakpoint*

> 断点击中计数：**断点**


:   Return hit count of `breakpoint`.

> 返回断点的命中次数。

```
<!-- -->
```


Scheme Procedure: **set-breakpoint-hit-count!** *breakpoint count*

> 设置断点击中次数！*断点计数*


:   Set the hit count of `breakpoint` must be zero.

> 设置断点的命中计数必须为零。

```
<!-- -->
```


Scheme Procedure: **breakpoint-thread** *breakpoint*

> 方程序：**断点-线程** *断点*


:   Return the global-thread-id for thread-specific breakpoint `breakpoint` is not thread-specific.

> 返回全局线程ID，用于特定线程的断点breakpoint不是特定线程的。

```
<!-- -->
```


Scheme Procedure: **set-breakpoint-thread!** *breakpoint global-thread-id\|#f*

> 设置断点线程！断点全局线程ID或#F


:   Set the thread-id for `breakpoint` If set to `#f`, the breakpoint is no longer thread-specific.

> 设置断点的线程ID。如果设置为#f，断点将不再是特定于线程的。

```
<!-- -->
```


Scheme Procedure: **breakpoint-task** *breakpoint*

> 方案程序：**断点任务** *断点*


:   If the breakpoint is Ada task-specific, return the Ada task id. If the breakpoint is not task-specific (or the underlying language is not Ada), return `#f`.

> 如果断点是Ada任务特定的，则返回Ada任务ID。如果断点不是特定于任务的（或底层语言不是Ada），则返回“＃f”。

```
<!-- -->
```


Scheme Procedure: **set-breakpoint-task!** *breakpoint task*

> 设定断点任务！断点任务


:   Set the Ada task of `breakpoint`. If set to `#f`, the breakpoint is no longer task-specific.

> 设置Ada任务的断点。如果设置为#f，断点将不再是特定任务。

```
<!-- -->
```


Scheme Procedure: **breakpoint-condition** *breakpoint*

> 断点条件：断点


:   Return the condition of `breakpoint`, as specified by the user. It is a string. If there is no condition, return `#f`.

> 返回用户指定的断点条件。它是一个字符串。如果没有条件，返回#f。

```
<!-- -->
```


Scheme Procedure: **set-breakpoint-condition!** *breakpoint condition*

> 设置断点条件！*断点条件*


:   Set the condition of `breakpoint`, which must be a string. If set to `#f` then the breakpoint becomes unconditional.

> 设置断点的条件，必须是一个字符串。如果设置为'#f'，那么断点就变成无条件的。

```
<!-- -->
```


Scheme Procedure: **breakpoint-stop** *breakpoint*

> 断点停止：断点


:   Return the stop predicate of `breakpoint`. See `set-breakpoint-stop!` below in this section.

> 请参阅本节的“set-breakpoint-stop！”，返回breakpoint的停止谓词。

```
<!-- -->
```


Scheme Procedure: **set-breakpoint-stop!** *breakpoint procedure\|#f*

> 设置断点停止！断点程序|#f


:   Set the stop predicate of `breakpoint` takes one argument: the \<gdb:breakpoint\> object. If this predicate is set to a procedure then it is invoked whenever the inferior reaches this breakpoint. If it returns `#t`, or any non-`#f` value, then the inferior is stopped, otherwise the inferior will continue.

> 设置breakpoint的停止谓词需要一个参数：<gdb:breakpoint>对象。如果将该谓词设置为过程，则每当下级到达该断点时就会调用该过程。如果它返回#t或任何非#f值，则下级将停止，否则下级将继续。

```
If there are multiple breakpoints at the same location with a `stop` predicate, each one will be called regardless of the return status of the previous. This ensures that all `stop` predicates have a chance to execute at that location. In this scenario if one of the methods returns `#t` but the others return `#f`, the inferior will still be stopped.

You should not alter the execution state of the inferior (i.e., step, next, etc.), alter the current frame context (i.e., change the current active frame), or alter, add or delete any breakpoint. As a general rule, you should not alter any data within [GDB] or the inferior at this time.

Example `stop` implementation:

::: smallexample
``` smallexample
(define (my-stop? bkpt)

  (let ((int-val (parse-and-eval "foo")))

> (let ((int-val (parse-and-eval "foo")))
    (value=? int-val 3)))

(define bkpt (make-breakpoint "main.c:42"))

> (定义 bkpt (创建断点 "main.c:42"))

(register-breakpoint! bkpt)

> (注册断点！bkpt)

(set-breakpoint-stop! bkpt my-stop?)

> 设置断点停止！断点我的停止？
```

:::

```

```

<!-- -->

```


Scheme Procedure: **breakpoint-commands** *breakpoint*

> 方案程序：**断点命令** *断点*


:   Return the commands attached to `breakpoint` as a string, or `#f` if there are none.

> 返回与`断点`关联的命令作为一个字符串，如果没有，则返回`#f`。

---

::: header
Next: [Lazy Strings In Guile](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile)]
:::
```
