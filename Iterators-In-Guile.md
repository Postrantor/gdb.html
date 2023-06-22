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

Scheme Procedure: **make-iterator** *object progress next!*

:   A `<gdb:iterator>` object is constructed with the `make-iterator` procedure. It takes three arguments: the object to be iterated over, an object to record the progress of the iteration, and a procedure to return the next element in the iteration, or an implementation chosen value to denote the end of iteration.

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

```

<!-- -->

```

Scheme Procedure: **iterator-object** *iterator*

:   Return the first argument that was passed to `make-iterator`. This is the object being iterated over.

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

These functions are provided by the `(gdb iterator)` module to assist in using iterators.

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

---

::: header
Previous: [Memory Ports in Guile](Memory-Ports-in-Guile.html#Memory-Ports-in-Guile)]
:::
```
