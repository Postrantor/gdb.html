---
description: Writing a Guile Pretty-Printer (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Writing a Guile Pretty-Printer (Debugging with GDB)
lang: en
resource-type: document
title: Writing a Guile Pretty-Printer (Debugging with GDB)
---
::: header
Next: [Commands In Guile](Commands-In-Guile.html#Commands-In-Guile)]
:::

---

#### 23.4.3.10 Writing a Guile Pretty-Printer

A pretty-printer consists of two basic parts: a lookup function to determine if the type is supported, and the printer itself.

Here is an example showing how a `std::string` printer might be written. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for details.

::: smallexample

```bash
(define (make-my-string-printer value)
  "Print a my::string string"
  (make-pretty-printer-worker
   "string"
   (lambda (printer)
     (value-field value "_data"))
   #f))
```

:::

And here is an example showing how a lookup function for the printer example above might be written.

::: smallexample

```bash
(define (str-lookup-function pretty-printer value)
  (let ((tag (type-tag (value-type value))))
    (and tag
         (string-prefix? "std::string<" tag)
         (make-my-string-printer value))))
```

:::

Then to register this printer in the global printer list:

::: smallexample

```bash
(append-pretty-printer!
 (make-pretty-printer "my-string" str-lookup-function))
```

:::

The example lookup function extracts the value's type, and attempts to match it to a type that it can pretty-print. If it is a type the printer can pretty-print, it will return a \<gdb:pretty-printer-worker\> object. If not, it returns `#f`.

We recommend that you put your core pretty-printers into a Guile package. If your pretty-printers are for use with a library, we further recommend embedding a version number into the package name. This practice will enable [GDB] to load multiple versions of your pretty-printers at the same time, because they will have different names.

You should write auto-loaded code (see [Guile Auto-loading](Guile-Auto_002dloading.html#Guile-Auto_002dloading)) such that it can be evaluated multiple times without changing its meaning. An ideal auto-load file will consist solely of `import` s of your printer modules, followed by a call to a register pretty-printers with the current objfile.

Taken as a whole, this approach will scale nicely to multiple inferiors, each potentially using a different library version. Embedding a version number in the Guile package name will ensure that [GDB] will find the correct printers for the specific version of the library used by each inferior.

To continue the `my::string` example, this code might appear in `(my-project my-library v1)`:

::: smallexample

```bash
(use-modules (gdb))
(define (register-printers objfile)
  (append-objfile-pretty-printer!
   (make-pretty-printer "my-string" str-lookup-function)))
```

:::

And then the corresponding contents of the auto-load file would be:

::: smallexample

```bash
(use-modules (gdb) (my-project my-library v1))
(register-printers (current-objfile))
```

:::

The previous example illustrates a basic pretty-printer. There are a few things that can be improved on. The printer only handles one type, whereas a library typically has several types. One could install a lookup function for each desired type in the library, but one could also have a single lookup function recognize several types. The latter is the conventional way this is handled. If a pretty-printer can handle multiple data types, then its *subprinters* are the printers for the individual data types.

The `(gdb printing)` module provides a formal way of solving this problem (see [Guile Printing Module](Guile-Printing-Module.html#Guile-Printing-Module)). Here is another example that handles multiple types.

These are the types we are going to pretty-print:

::: smallexample

```bash
struct foo ;
struct bar ;
```

:::

Here are the printers:

::: smallexample

```bash
(define (make-foo-printer value)
  "Print a foo object"
  (make-pretty-printer-worker
   "foo"
   (lambda (printer)
     (format #f "a=<~a> b=<~a>"
             (value-field value "a") (value-field value "a")))
   #f))

(define (make-bar-printer value)
  "Print a bar object"
  (make-pretty-printer-worker
   "foo"
   (lambda (printer)
     (format #f "x=<~a> y=<~a>"
             (value-field value "x") (value-field value "y")))
   #f))
```

:::

This example doesn't need a lookup function, that is handled by the `(gdb printing)` module. Instead a function is provided to build up the object that handles the lookup.

::: smallexample

```bash
(use-modules (gdb printing))

(define (build-pretty-printer)
  (let ((pp (make-pretty-printer-collection "my-library")))
    (pp-collection-add-tag-printer "foo" make-foo-printer)
    (pp-collection-add-tag-printer "bar" make-bar-printer)
    pp))
```

:::

And here is the autoload support:

::: smallexample

```bash
(use-modules (gdb) (my-library))
(append-objfile-pretty-printer! (current-objfile) (build-pretty-printer))
```

:::

Finally, when this printer is loaded into [GDB]':

::: smallexample

```bash
(gdb) info pretty-printer
my_library.so:
  my-library
    foo
    bar
```

:::

---

::: header
Next: [Commands In Guile](Commands-In-Guile.html#Commands-In-Guile)]
:::
