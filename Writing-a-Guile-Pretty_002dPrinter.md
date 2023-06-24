---
tip: translate by openai@2023-06-24 04:51:55
...
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

> 一个漂亮的打印机由两个基本部分组成：一个查找函数来确定该类型是否受支持，以及打印机本身。


Here is an example showing how a `std::string` printer might be written. See [Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API), for details.

> 这里有一个示例，演示了如何编写`std::string`打印机。有关详细信息，请参阅[Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)。

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

> 这里有一个例子，展示了如何编写上面打印机示例的查找函数。

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

> 示例查找函数提取值的类型，并尝试将其匹配到可以美化打印的类型。如果它是打印机可以美化打印的类型，它将返回一个\<gdb:pretty-printer-worker\>对象。如果不是，它将返回`#f`。


We recommend that you put your core pretty-printers into a Guile package. If your pretty-printers are for use with a library, we further recommend embedding a version number into the package name. This practice will enable [GDB] to load multiple versions of your pretty-printers at the same time, because they will have different names.

> 我们建议您将核心可美化打印机放入Guile包中。如果您的可美化打印机用于库，我们进一步建议将版本号嵌入包名中。这种做法将使[GDB]能够同时加载多个版本的可美化打印机，因为它们将具有不同的名称。


You should write auto-loaded code (see [Guile Auto-loading](Guile-Auto_002dloading.html#Guile-Auto_002dloading)) such that it can be evaluated multiple times without changing its meaning. An ideal auto-load file will consist solely of `import` s of your printer modules, followed by a call to a register pretty-printers with the current objfile.

> 你应该编写自动加载的代码（参见[Guile自动加载](Guile-Auto_002dloading.html#Guile-Auto_002dloading)），使其可以多次评估而不改变其意义。理想的自动加载文件将仅由你的打印机模块的`import`组成，然后调用当前objfile的register pretty-printers。


Taken as a whole, this approach will scale nicely to multiple inferiors, each potentially using a different library version. Embedding a version number in the Guile package name will ensure that [GDB] will find the correct printers for the specific version of the library used by each inferior.

> 整体来看，这种方法可以很好地扩展到多个下属，每个下属可能使用不同的库版本。在Guile包名中嵌入版本号将确保[GDB]可以找到每个下属所使用的库版本的正确打印机。


To continue the `my::string` example, this code might appear in `(my-project my-library v1)`:

> 继续'my::string'示例，这段代码可能出现在'(my-project my-library v1)'中：

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

> 前面的例子演示了一个基本的漂亮打印机。可以进行改进的地方有几处。打印机只处理一种类型，而库通常有几种类型。可以为每个需要的类型安装一个查找函数，但也可以用一个查找函数来识别几种类型。后者是常规方式。如果一个漂亮打印机可以处理多种数据类型，那么它的*子打印机*就是单个数据类型的打印机。


The `(gdb printing)` module provides a formal way of solving this problem (see [Guile Printing Module](Guile-Printing-Module.html#Guile-Printing-Module)). Here is another example that handles multiple types.

> 模块(gdb printing)提供了一种正式的解决这个问题的方法（参见[Guile Printing Module](Guile-Printing-Module.html#Guile-Printing-Module)）。这里是另一个处理多种类型的示例。

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

> 这个例子不需要查找函数，这是由`(gdb printing)`模块处理的。取而代之的是提供了一个函数来构建处理查找的对象。

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
