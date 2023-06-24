---
tip: translate by openai@2023-06-23 23:42:56
...
---
description: Iterators In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Iterators In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Iterators In Guile (Debugging with GDB)
---
::: header
Previous: [Memory Ports in Guile](Memory-Ports-in-Guile.html#Memory-Ports-in-Guile)]
:::

---

#### 23.4.3.25 Iterators In Guile


A simple iterator facility is provided to allow, for example, iterating over the set of program symbols without having to first construct a list of all of them. A useful contribution would be to add support for SRFI 41 and SRFI 45.

> 提供了一个简单的迭代器工具，以便比如遍历程序符号集合，而无需首先构建它们的列表。有用的贡献将是添加对SRFI 41和SRFI 45的支持。

Scheme Procedure: **make-iterator** *object progress next!*


:   A `<gdb:iterator>` object is constructed with the `make-iterator` procedure. It takes three arguments: the object to be iterated over, an object to record the progress of the iteration, and a procedure to return the next element in the iteration, or an implementation chosen value to denote the end of iteration.

> 一个`<gdb:iterator>`对象是用`make-iterator`过程构造的。它需要三个参数：要迭代的对象、用于记录迭代进度的对象，以及一个返回迭代中下一个元素的过程，或者用来表示迭代结束的实现选择的值。

```
By convention, end of iteration is marked with `(end-of-iteration)`, and may be tested with the `end-of-iteration?` predicate. The result of `(end-of-iteration)` is chosen so that it is not otherwise used by the `(gdb)` module. If you are using `<gdb:iterator>` in your own code it is your responsibility to maintain this invariant.

A trivial example for illustration's sake:

::: smallexample
``` smallexample
(use-modules (gdb iterator))
(define my-list (list 1 2 3))
(define iter
  (make-iterator my-list my-list
                 (lambda (iter)
                   (let ((l (iterator-progress iter)))
                     (if (eq? l '())
                         (end-of-iteration)
                         (begin
                           (set-iterator-progress! iter (cdr l))
                           (car l)))))))
```

:::

Here is a slightly more realistic example, which computes a list of all the functions in `my-global-block`.

::: smallexample

```bash
(use-modules (gdb iterator))
(define this-sal (find-pc-line (frame-pc (selected-frame))))
(define this-symtab (sal-symtab this-sal))
(define this-global-block (symtab-global-block this-symtab))
(define syms-iter (make-block-symbols-iterator this-global-block))
(define functions (iterator-filter symbol-function? syms-iter))
```

:::

```

```

<!-- -->

```

Scheme Procedure: **iterator?** *object*


:   Return `#t` if `object` is a `<gdb:iterator>` object. Otherwise return `#f`.

> 如果对象是一个<gdb:iterator>对象，则返回#t。否则返回#f。

```

<!-- -->

```

Scheme Procedure: **iterator-object** *iterator*


:   Return the first argument that was passed to `make-iterator`. This is the object being iterated over.

> 返回传递给`make-iterator`的第一个参数。这是正在迭代的对象。

```

<!-- -->

```

Scheme Procedure: **iterator-progress** *iterator*

:   Return the object tracking iteration progress.

```

<!-- -->

```

Scheme Procedure: **set-iterator-progress!** *iterator new-value*

:   Set the object tracking iteration progress.

```

<!-- -->

```

Scheme Procedure: **iterator-next!** *iterator*


:   Invoke the procedure that was the third argument to `make-iterator`, passing it one argument, the `<gdb:iterator>` object. The result is either the next element in the iteration, or an end marker as implemented by the `next!` procedure. By convention the end marker is the result of `(end-of-iteration)`.

> 调用`make-iterator`的第三个参数传入一个参数`<gdb:iterator>`对象，结果是迭代的下一个元素，或者由`next!`过程实现的结束标记。按照惯例，结束标记是`(end-of-iteration)`的结果。

```

<!-- -->

```

Scheme Procedure: **end-of-iteration**

:   Return the Scheme object that denotes end of iteration.

```

<!-- -->

```

Scheme Procedure: **end-of-iteration?** *object*


:   Return `#t` if `object` is the end of iteration marker. Otherwise return `#f`.

> 如果对象是迭代结束标记，则返回#t，否则返回#f。


These functions are provided by the `(gdb iterator)` module to assist in using iterators.

> 这些函数由`（gdb迭代器）`模块提供，以帮助使用迭代器。

Scheme Procedure: **make-list-iterator** *list*

:   Return a `<gdb:iterator>` object that will iterate over `list`.

```

<!-- -->

```

Scheme Procedure: **iterator-\>list** *iterator*

:   Return the elements pointed to by `iterator` as a list.

```

<!-- -->

```

Scheme Procedure: **iterator-map** *proc iterator*


:   Return the list of objects obtained by applying `proc` and to each subsequent object.

> 返回通过对每个后续对象应用`proc`得到的对象列表。

```

<!-- -->

```

Scheme Procedure: **iterator-for-each** *proc iterator*

:   Apply `proc`. The result is unspecified.

```

<!-- -->

```

Scheme Procedure: **iterator-filter** *pred iterator*

:   Return the list of elements pointed to by `iterator`.

```

<!-- -->

```

Scheme Procedure: **iterator-until** *pred iterator*


:   Run `iterator` until the result of `(pred element)` is true and return that as the result. Otherwise return `#f`.

> 运行`迭代器`，直到`（pred element）`的结果为真，并将其作为结果返回。否则返回`#f`。

---

::: header
Previous: [Memory Ports in Guile](Memory-Ports-in-Guile.html#Memory-Ports-in-Guile)]
:::
```
