---
description: Writing an Xmethod (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Writing an Xmethod (Debugging with GDB)
lang: en
resource-type: document
title: Writing an Xmethod (Debugging with GDB)
---
::: header
Next: [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python)]
:::

---

#### 23.3.2.15 Writing an Xmethod

Implementing xmethods in Python will require implementing xmethod matchers and xmethod workers (see [Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python)). Consider the following C++ class:

::: smallexample

```bash
class MyClass
{
public:
  MyClass (int a) : a_(a) 

  int geta (void) 
  int operator+ (int b);

private:
  int a_;
};

int
MyClass::operator+ (int b)
{
  return a_ + b;
}
```

:::

Let us define two xmethods for the class `MyClass`, one replacing the method `geta`, and another adding an overloaded flavor of `operator+` which takes a `MyClass` argument (the C++ code above already has an overloaded `operator+` which takes an `int` argument). The xmethod matcher can be defined as follows:

::: smallexample

```bash
class MyClass_geta(gdb.xmethod.XMethod):
    def __init__(self):
        gdb.xmethod.XMethod.__init__(self, 'geta')
 
    def get_worker(self, method_name):
        if method_name == 'geta':
            return MyClassWorker_geta()
 
 
class MyClass_sum(gdb.xmethod.XMethod):
    def __init__(self):
        gdb.xmethod.XMethod.__init__(self, 'sum')
 
    def get_worker(self, method_name):
        if method_name == 'operator+':
            return MyClassWorker_plus()
 
 
class MyClassMatcher(gdb.xmethod.XMethodMatcher):
    def __init__(self):
        gdb.xmethod.XMethodMatcher.__init__(self, 'MyClassMatcher')
        # List of methods 'managed' by this matcher
        self.methods = [MyClass_geta(), MyClass_sum()]
 
    def match(self, class_type, method_name):
        if class_type.tag != 'MyClass':
            return None
        workers = 
        for method in self.methods:
            if method.enabled:
                worker = method.get_worker(method_name)
                if worker:
                    workers.append(worker)
 
        return workers
```

:::

Notice that the `match` method of `MyClassMatcher` returns a worker object of type `MyClassWorker_geta` for the `geta` method, and a worker object of type `MyClassWorker_plus` for the `operator+` method. This is done indirectly via helper classes derived from `gdb.xmethod.XMethod`. One does not need to use the `methods` attribute in a matcher as it is optional. However, if a matcher manages more than one xmethod, it is a good practice to list the xmethods in the `methods` attribute of the matcher. This will then facilitate enabling and disabling individual xmethods via the `enable/disable` commands. Notice also that a worker object is returned only if the corresponding entry in the `methods` attribute of the matcher is enabled.

The implementation of the worker classes returned by the matcher setup above is as follows:

::: smallexample

```bash
class MyClassWorker_geta(gdb.xmethod.XMethodWorker):
    def get_arg_types(self):
        return None

    def get_result_type(self, obj):
        return gdb.lookup_type('int')
 
    def __call__(self, obj):
        return obj['a_']
 
 
class MyClassWorker_plus(gdb.xmethod.XMethodWorker):
    def get_arg_types(self):
        return gdb.lookup_type('MyClass')

    def get_result_type(self, obj):
        return gdb.lookup_type('int')
 
    def __call__(self, obj, other):
        return obj['a_'] + other['a_']
```

:::

For [GDB] globally as follows:

::: smallexample

```bash
gdb.xmethod.register_xmethod_matcher(None, MyClassMatcher())
```

:::

If an object `obj` of type `MyClass` is initialized in C++ code as follows:

::: smallexample

```bash
MyClass obj(5);
```

:::

then, after loading the Python script defining the xmethod matchers and workers into [GDB], invoking the method `geta` or using the operator `+` on `obj` will invoke the xmethods defined above:

::: smallexample

```bash
(gdb) p obj.geta()
$1 = 5

(gdb) p obj + obj
$2 = 10
```

:::

Consider another example with a C++ template class:

::: smallexample

```bash
template <class T>
class MyTemplate
{
public:
  MyTemplate () : dsize_(10), data_ (new T [10]) 
  ~MyTemplate () 
 
  int footprint (void)
  {
    return sizeof (T) * dsize_ + sizeof (MyTemplate<T>);
  }
 
private:
  int dsize_;
  T *data_;
};
```

:::

Let us implement an xmethod for the above class which serves as a replacement for the `footprint` method. The full code listing of the xmethod workers and xmethod matchers is as follows:

::: smallexample

```bash
class MyTemplateWorker_footprint(gdb.xmethod.XMethodWorker):
    def __init__(self, class_type):
        self.class_type = class_type

    def get_arg_types(self):
        return None

    def get_result_type(self):
        return gdb.lookup_type('int')

    def __call__(self, obj):
        return (self.class_type.sizeof +
                obj['dsize_'] *
                self.class_type.template_argument(0).sizeof)
 
 
class MyTemplateMatcher_footprint(gdb.xmethod.XMethodMatcher):
    def __init__(self):
        gdb.xmethod.XMethodMatcher.__init__(self, 'MyTemplateMatcher')
 
    def match(self, class_type, method_name):
        if (re.match('MyTemplate<[ \t\n]*[_a-zA-Z][ _a-zA-Z0-9]*>',
                     class_type.tag) and
            method_name == 'footprint'):
            return MyTemplateWorker_footprint(class_type)
```

:::

Notice that, in this example, we have not used the `methods` attribute of the matcher as the matcher manages only one xmethod. The user can enable/disable this xmethod by enabling/disabling the matcher itself.

---

::: header
Next: [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python)]
:::
