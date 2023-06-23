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

Support is also provided to view and manipulate breakpoints created outside of Guile.

The following breakpoint-related procedures are provided by the `(gdb)` module:

*

:   Create a new breakpoint at `location`, a string naming the location of the breakpoint, or an expression that defines a watchpoint. The contents can be any location recognized by the `break` command, or in the case of a watchpoint, by the `watch` command.

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

:   Add `breakpoint`'. It is an error to register an already registered breakpoint. The result is unspecified.

```
<!-- -->
```

Scheme Procedure: **delete-breakpoint!** *breakpoint*

:   Remove `breakpoint` object. Any further attempt to access the object will throw an exception.

```
If `breakpoint`, in which case the breakpoint becomes valid again.
```

```
<!-- -->
```

Scheme Procedure: **breakpoints**

:   Return a list of all breakpoints. Each element of the list is a `<gdb:breakpoint>` object.

```
<!-- -->
```

Scheme Procedure: **breakpoint?** *object*

:   Return `#t` if `object` is a `<gdb:breakpoint>` object, and `#f` otherwise.

```
<!-- -->
```

Scheme Procedure: **breakpoint-valid?** *breakpoint*

:   Return `#t` if `breakpoint` with `register-breakpoint!`. A `<gdb:breakpoint>` object can become invalid if the user deletes the breakpoint. In this case, the object still exists, but the underlying breakpoint does not. In the cases of watchpoint scope, the watchpoint remains valid even if execution of the inferior leaves the scope of that watchpoint.

```
<!-- -->
```

Scheme Procedure: **breakpoint-number** *breakpoint*

:   Return the breakpoint's number --- the identifier used by the user to manipulate the breakpoint.

```
<!-- -->
```

Scheme Procedure: **breakpoint-temporary?** *breakpoint*

:   Return `#t` if the breakpoint was created as a temporary breakpoint. Temporary breakpoints are automatically deleted after they've been hit. Calling this procedure, and all other procedures other than `breakpoint-valid?` and `register-breakpoint!`, will result in an error after the breakpoint has been hit (since it has been automatically deleted).

```
<!-- -->
```

Scheme Procedure: **breakpoint-type** *breakpoint*

:   Return the breakpoint's type --- the identifier used to determine the actual breakpoint type or use-case.

```
<!-- -->
```

Scheme Procedure: **breakpoint-visible?** *breakpoint*

:   Return `#t` if the breakpoint is visible to the user when hit, or when the '`info breakpoints`' command is run. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **breakpoint-location** *breakpoint*

:   Return the location of the breakpoint, as specified by the user. It is a string. If the breakpoint does not have a location (that is, it is a watchpoint) return `#f`.

```
<!-- -->
```

Scheme Procedure: **breakpoint-expression** *breakpoint*

:   Return the breakpoint expression, as specified by the user. It is a string. If the breakpoint does not have an expression (the breakpoint is not a watchpoint) return `#f`.

```
<!-- -->
```

Scheme Procedure: **breakpoint-enabled?** *breakpoint*

:   Return `#t` if the breakpoint is enabled, and `#f` otherwise.

```
<!-- -->
```

Scheme Procedure: **set-breakpoint-enabled!** *breakpoint flag*

:   Set the enabled state of `breakpoint`. If flag is `#f` it is disabled, otherwise it is enabled.

```
<!-- -->
```

Scheme Procedure: **breakpoint-silent?** *breakpoint*

:   Return `#t` if the breakpoint is silent, and `#f` otherwise.

```
Note that a breakpoint can also be silent if it has commands and the first command is `silent`. This is not reported by the `silent` attribute.
```

```
<!-- -->
```

Scheme Procedure: **set-breakpoint-silent!** *breakpoint flag*

:   Set the silent state of `breakpoint`. If flag is `#f` the breakpoint is made silent, otherwise it is made non-silent (or noisy).

```
<!-- -->
```

Scheme Procedure: **breakpoint-ignore-count** *breakpoint*

:   Return the ignore count for `breakpoint`.

```
<!-- -->
```

Scheme Procedure: **set-breakpoint-ignore-count!** *breakpoint count*

:   Set the ignore count for `breakpoint`.

```
<!-- -->
```

Scheme Procedure: **breakpoint-hit-count** *breakpoint*

:   Return hit count of `breakpoint`.

```
<!-- -->
```

Scheme Procedure: **set-breakpoint-hit-count!** *breakpoint count*

:   Set the hit count of `breakpoint` must be zero.

```
<!-- -->
```

Scheme Procedure: **breakpoint-thread** *breakpoint*

:   Return the global-thread-id for thread-specific breakpoint `breakpoint` is not thread-specific.

```
<!-- -->
```

Scheme Procedure: **set-breakpoint-thread!** *breakpoint global-thread-id\|#f*

:   Set the thread-id for `breakpoint` If set to `#f`, the breakpoint is no longer thread-specific.

```
<!-- -->
```

Scheme Procedure: **breakpoint-task** *breakpoint*

:   If the breakpoint is Ada task-specific, return the Ada task id. If the breakpoint is not task-specific (or the underlying language is not Ada), return `#f`.

```
<!-- -->
```

Scheme Procedure: **set-breakpoint-task!** *breakpoint task*

:   Set the Ada task of `breakpoint`. If set to `#f`, the breakpoint is no longer task-specific.

```
<!-- -->
```

Scheme Procedure: **breakpoint-condition** *breakpoint*

:   Return the condition of `breakpoint`, as specified by the user. It is a string. If there is no condition, return `#f`.

```
<!-- -->
```

Scheme Procedure: **set-breakpoint-condition!** *breakpoint condition*

:   Set the condition of `breakpoint`, which must be a string. If set to `#f` then the breakpoint becomes unconditional.

```
<!-- -->
```

Scheme Procedure: **breakpoint-stop** *breakpoint*

:   Return the stop predicate of `breakpoint`. See `set-breakpoint-stop!` below in this section.

```
<!-- -->
```

Scheme Procedure: **set-breakpoint-stop!** *breakpoint procedure\|#f*

:   Set the stop predicate of `breakpoint` takes one argument: the \<gdb:breakpoint\> object. If this predicate is set to a procedure then it is invoked whenever the inferior reaches this breakpoint. If it returns `#t`, or any non-`#f` value, then the inferior is stopped, otherwise the inferior will continue.

```
If there are multiple breakpoints at the same location with a `stop` predicate, each one will be called regardless of the return status of the previous. This ensures that all `stop` predicates have a chance to execute at that location. In this scenario if one of the methods returns `#t` but the others return `#f`, the inferior will still be stopped.

You should not alter the execution state of the inferior (i.e., step, next, etc.), alter the current frame context (i.e., change the current active frame), or alter, add or delete any breakpoint. As a general rule, you should not alter any data within [GDB] or the inferior at this time.

Example `stop` implementation:

::: smallexample
``` smallexample
(define (my-stop? bkpt)
  (let ((int-val (parse-and-eval "foo")))
    (value=? int-val 3)))
(define bkpt (make-breakpoint "main.c:42"))
(register-breakpoint! bkpt)
(set-breakpoint-stop! bkpt my-stop?)
```

:::

```

```

<!-- -->

```

Scheme Procedure: **breakpoint-commands** *breakpoint*

:   Return the commands attached to `breakpoint` as a string, or `#f` if there are none.

---

::: header
Next: [Lazy Strings In Guile](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile)]
:::
```
