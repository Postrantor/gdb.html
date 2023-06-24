---
tip: translate by openai@2023-06-24 01:02:52
...
---
description: Parameters In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Parameters In Python (Debugging with GDB)
lang: en
resource-type: document
title: Parameters In Python (Debugging with GDB)
---
::: header
Next: [Functions In Python](Functions-In-Python.html#Functions-In-Python)]
:::

---

#### 23.3.2.22 Parameters In Python


You can implement new [GDB] parameters using Python. A new parameter is implemented as an instance of the `gdb.Parameter` class.

> 你可以使用Python来实现新的[GDB]参数。新参数作为`gdb.Parameter`类的一个实例实现。


Parameters are exposed to the user via the `set` and `show` commands. See [Help](Help.html#Help).

> 参数可以通过`设置`和`显示`命令向用户公开。请参见[帮助](Help.html#Help)。


There are many parameters that already exist and can be set in [GDB]. Similarly, you can define parameters that can be used to influence behavior in custom Python scripts and commands.

> 在[GDB]中已经存在许多可以设置的参数。同样，你可以定义参数，用于影响自定义Python脚本和命令的行为。

)*


:   The object initializer for `Parameter` registers the new parameter with [GDB]. This initializer is normally invoked from the subclass' own `__init__` method.

> 参数的对象初始化器会将新参数注册到GDB中。这个初始化器通常从子类的`__init__`方法中调用。

```
`name` as `set print foo`.

If `name` consists of multiple words, and no prefix parameter group can be found, an exception is raised.

`command_class` how to categorize the new parameter in the help system.

`parameter_class` the type of the new parameter; this information is used for input validation and completion.

If `parameter_class` must be a sequence of strings. These strings represent the possible values for the parameter.

If `parameter_class` is not `PARAM_ENUM`, then the presence of a fourth argument will cause an exception to be thrown.

The help text for the new parameter includes the Python documentation string from the parameter's class, if there is one. If there is no documentation string, a default value is used. The documentation string is included in the output of the parameters `help set` and `help show` commands, and should be written taking this into account.
```

```
<!-- -->
```

Variable: **Parameter.set_doc**


:   If this attribute exists, and is a string, then its value is used as the first part of the help text for this parameter's `set` command. The second part of the help text is taken from the documentation string for the parameter's class, if there is one.

> 如果这个属性存在，并且是一个字符串，那么它的值将被用作这个参数`set`命令的帮助文本的第一部分。帮助文本的第二部分来自参数类的文档字符串（如果有的话）。

```
The value of `set_doc` should give a brief summary specific to the set action, this text is only displayed when the user runs the `help set` command for this parameter. The class documentation should be used to give a fuller description of what the parameter does, this text is displayed for both the `help set` and `help show` commands.

The `set_doc` value is examined when `Parameter.__init__` is invoked; subsequent changes have no effect.
```

```
<!-- -->
```

Variable: **Parameter.show_doc**


:   If this attribute exists, and is a string, then its value is used as the first part of the help text for this parameter's `show` command. The second part of the help text is taken from the documentation string for the parameter's class, if there is one.

> 如果这个属性存在，并且是一个字符串，那么它的值将被用作此参数`show`命令的帮助文本的第一部分。 第二部分帮助文本来自参数类的文档字符串（如果有）。

```
The value of `show_doc` should give a brief summary specific to the show action, this text is only displayed when the user runs the `help show` command for this parameter. The class documentation should be used to give a fuller description of what the parameter does, this text is displayed for both the `help set` and `help show` commands.

The `show_doc` value is examined when `Parameter.__init__` is invoked; subsequent changes have no effect.
```

```
<!-- -->
```

Variable: **Parameter.value**


:   The `value` attribute holds the underlying value of the parameter. It can be read and assigned to just as any other attribute. [GDB] does validation when assignments are made.

> 属性`value`保存参数的底层值。它可以像其他属性一样读取和赋值。[GDB]在进行赋值时会进行验证。


There are two methods that may be implemented in any `Parameter` class. These are:

> 在任何`参数`类中可以实现两种方法。它们是：

Function: **Parameter.get_set_string** *(self)*

:   If this method exists, [GDB] will present it to the user.

```
If this method raises the `gdb.GdbError` exception (see [Exception Handling](Exception-Handling.html#Exception-Handling)), then [GDB] will print the exception's string and the `set` command will fail. Note, however, that the `value` attribute will not be reset in this case. So, if your parameter must validate values, it should store the old value internally and reset the exposed value, like so:

::: smallexample
``` smallexample
class ExampleParam (gdb.Parameter):
   def __init__ (self, name):
      super (ExampleParam, self).__init__ (name,
                   gdb.COMMAND_DATA,
                   gdb.PARAM_BOOLEAN)
      self.value = True
      self.saved_value = True
   def validate(self):
      return False
   def get_set_string (self):
      if not self.validate():
        self.value = self.saved_value
        raise gdb.GdbError('Failed to validate')
      self.saved_value = self.value
      return ""
```

:::

```

```

<!-- -->

```

Function: **Parameter.get_show_string** *(self, svalue)*


:   [GDB]). The argument `svalue` receives the string representation of the current value. This method must return a string.

> `svalue` 参数接收当前值的字符串表示。此方法必须返回一个字符串。


When a new parameter is defined, its type must be specified. The available types are represented by constants defined in the `gdb` module:

> 当定义一个新参数时，必须指定它的类型。可用类型由`gdb`模块中定义的常量表示。



`gdb.PARAM_BOOLEAN`


The value is a plain boolean. The Python boolean values, `True` and `False` are the only valid values.

> 值是一个普通布尔值。Python布尔值True和False是唯一有效的值。



`gdb.PARAM_AUTO_BOOLEAN`


The value has three possible states: true, false, and '`auto`' is represented using `None`.

> 值有三种可能的状态：true，false，以及用`None`表示的`auto`。



`gdb.PARAM_UINTEGER`


The value is an unsigned integer. The value of `None` should be interpreted to mean "unlimited" (literal `'unlimited'` can also be used to set that value), and the value of 0 is reserved and should not be used.

> 值为无符号整数。值`None`应解释为“无限”（字面上的`'unlimited'`也可以用来设置该值），值0被保留，不应使用。



`gdb.PARAM_INTEGER`


The value is a signed integer. The value of `None` should be interpreted to mean "unlimited" (literal `'unlimited'` can also be used to set that value), and the value of 0 is reserved and should not be used.

> 值是一个有符号整数。`None`的值应被解释为“无限”（字面上的`'unlimited'`也可以用来设置该值），0的值是保留的，不应该使用。



`gdb.PARAM_STRING`


The value is a string. When the user modifies the string, any escape sequences, such as '`\t`', and octal escapes, are translated into corresponding characters and encoded into the current host charset.

> 值是一个字符串。当用户修改字符串时，所有转义序列（如'\t'）和八进制转义序列都会被转换成对应的字符，并编码成当前主机的字符集。



`gdb.PARAM_STRING_NOESCAPE`


The value is a string. When the user modifies the string, escapes are passed through untranslated.

> 值是一个字符串。当用户修改字符串时，转义符将原样传递。



`gdb.PARAM_OPTIONAL_FILENAME`

The value is a either a filename (a string), or `None`.



`gdb.PARAM_FILENAME`


The value is a filename. This is just like `PARAM_STRING_NOESCAPE`, but uses file names for completion.

> 值是一个文件名。这就像'PARAM_STRING_NOESCAPE'一样，但使用文件名来完成。



`gdb.PARAM_ZINTEGER`


The value is a signed integer. This is like `PARAM_INTEGER`, except that 0 is allowed and the value of `None` is not supported.

> 值是一个带符号的整数。这类似于`PARAM_INTEGER`，但是允许0，而不支持`None`的值。



`gdb.PARAM_ZUINTEGER`


The value is an unsigned integer. This is like `PARAM_UINTEGER`, except that 0 is allowed and the value of `None` is not supported.

> 值是一个无符号整数。这类似于`PARAM_UINTEGER`，但允许0，而不支持`None`的值。



`gdb.PARAM_ZUINTEGER_UNLIMITED`


The value is a signed integer. This is like `PARAM_INTEGER` including that the value of `None` should be interpreted to mean "unlimited" (literal `'unlimited'` can also be used to set that value), except that 0 is allowed, and the value cannot be negative, except the special value -1 is returned for the setting of "unlimited".

> 值是一个带符号的整数，这就像`PARAM_INTEGER`，其中`None`的值应被解释为“无限”（字面上的`'unlimited'`也可以用来设置该值），但允许0，并且该值不能为负，除非特殊值-1用于设置“无限”。



`gdb.PARAM_ENUM`


The value is a string, which must be one of a collection string constants provided when the parameter is created.

> 值是字符串，必须是在创建参数时提供的字符串常量集合之一。

---

::: header
Next: [Functions In Python](Functions-In-Python.html#Functions-In-Python)]
:::
```
