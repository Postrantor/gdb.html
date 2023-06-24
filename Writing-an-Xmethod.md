---
tip: translate by openai@2023-06-24 04:55:35
...
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

> 实现Python中的xmethods需要实现xmethod matchers和xmethod workers（参见[Xmethods In Python]（Xmethods-In-Python.html#Xmethods-In-Python））。考虑以下C ++类：

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

> 让我们为类`MyClass`定义两个xmethods，一个替换方法`geta`，另一个添加一个重载的`operator+`，它接受一个`MyClass`参数（上面的C++代码已经有一个重载的`operator+`，它接受一个`int`参数）。xmethod匹配器可以定义如下：

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

> 注意，`MyClassMatcher`的`match`方法会针对`geta`方法返回一个`MyClassWorker_geta`类型的工作者对象，针对`operator+`方法则返回一个`MyClassWorker_plus`类型的工作者对象。这是通过派生自`gdb.xmethod.XMethod`的辅助类间接完成的。在匹配器中不需要使用`methods`属性，因为它是可选的。但是，如果一个匹配器管理多个xmethod，最好将xmethods列在匹配器的`methods`属性中。这将有助于通过`enable/disable`命令启用和禁用各个xmethod。还要注意，只有当匹配器的`methods`属性中相应的条目被启用时，才会返回工作者对象。


The implementation of the worker classes returned by the matcher setup above is as follows:

> 以上匹配器返回的工人类的实现如下：

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

> 如果在C++代码中以下列方式初始化类型为MyClass的对象obj：

::: smallexample

```bash
MyClass obj(5);
```

:::


then, after loading the Python script defining the xmethod matchers and workers into [GDB], invoking the method `geta` or using the operator `+` on `obj` will invoke the xmethods defined above:

> 然后，在[GDB]中加载定义xmethod matchers和workers的Python脚本后，调用方法`geta`或在`obj`上使用运算符`+`将调用上述定义的xmethods：

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

> 让我们为上面的类实现一个xmethod，用作`footprint`方法的替代。xmethod workers和xmethod matchers的完整代码列表如下：

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

> 注意，在这个例子中，我们没有使用匹配器的`methods`属性，因为匹配器只管理一个xmethod。用户可以通过启用/禁用匹配器来启用/禁用此xmethod。

---

::: header
Next: [Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python)]
:::
