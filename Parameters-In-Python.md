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

Parameters are exposed to the user via the `set` and `show` commands. See [Help](Help.html#Help).

There are many parameters that already exist and can be set in [GDB]. Similarly, you can define parameters that can be used to influence behavior in custom Python scripts and commands.

)*

:   The object initializer for `Parameter` registers the new parameter with [GDB]. This initializer is normally invoked from the subclass' own `__init__` method.

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

```
The value of `set_doc` should give a brief summary specific to the set action, this text is only displayed when the user runs the `help set` command for this parameter. The class documentation should be used to give a fuller description of what the parameter does, this text is displayed for both the `help set` and `help show` commands.

The `set_doc` value is examined when `Parameter.__init__` is invoked; subsequent changes have no effect.
```

```
<!-- -->
```

Variable: **Parameter.show_doc**

:   If this attribute exists, and is a string, then its value is used as the first part of the help text for this parameter's `show` command. The second part of the help text is taken from the documentation string for the parameter's class, if there is one.

```
The value of `show_doc` should give a brief summary specific to the show action, this text is only displayed when the user runs the `help show` command for this parameter. The class documentation should be used to give a fuller description of what the parameter does, this text is displayed for both the `help set` and `help show` commands.

The `show_doc` value is examined when `Parameter.__init__` is invoked; subsequent changes have no effect.
```

```
<!-- -->
```

Variable: **Parameter.value**

:   The `value` attribute holds the underlying value of the parameter. It can be read and assigned to just as any other attribute. [GDB] does validation when assignments are made.

There are two methods that may be implemented in any `Parameter` class. These are:

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

When a new parameter is defined, its type must be specified. The available types are represented by constants defined in the `gdb` module:



`gdb.PARAM_BOOLEAN`

The value is a plain boolean. The Python boolean values, `True` and `False` are the only valid values.



`gdb.PARAM_AUTO_BOOLEAN`

The value has three possible states: true, false, and '`auto`' is represented using `None`.



`gdb.PARAM_UINTEGER`

The value is an unsigned integer. The value of `None` should be interpreted to mean "unlimited" (literal `'unlimited'` can also be used to set that value), and the value of 0 is reserved and should not be used.



`gdb.PARAM_INTEGER`

The value is a signed integer. The value of `None` should be interpreted to mean "unlimited" (literal `'unlimited'` can also be used to set that value), and the value of 0 is reserved and should not be used.



`gdb.PARAM_STRING`

The value is a string. When the user modifies the string, any escape sequences, such as '`\t`', and octal escapes, are translated into corresponding characters and encoded into the current host charset.



`gdb.PARAM_STRING_NOESCAPE`

The value is a string. When the user modifies the string, escapes are passed through untranslated.



`gdb.PARAM_OPTIONAL_FILENAME`

The value is a either a filename (a string), or `None`.



`gdb.PARAM_FILENAME`

The value is a filename. This is just like `PARAM_STRING_NOESCAPE`, but uses file names for completion.



`gdb.PARAM_ZINTEGER`

The value is a signed integer. This is like `PARAM_INTEGER`, except that 0 is allowed and the value of `None` is not supported.



`gdb.PARAM_ZUINTEGER`

The value is an unsigned integer. This is like `PARAM_UINTEGER`, except that 0 is allowed and the value of `None` is not supported.



`gdb.PARAM_ZUINTEGER_UNLIMITED`

The value is a signed integer. This is like `PARAM_INTEGER` including that the value of `None` should be interpreted to mean "unlimited" (literal `'unlimited'` can also be used to set that value), except that 0 is allowed, and the value cannot be negative, except the special value -1 is returned for the setting of "unlimited".



`gdb.PARAM_ENUM`

The value is a string, which must be one of a collection string constants provided when the parameter is created.

---

::: header
Next: [Functions In Python](Functions-In-Python.html#Functions-In-Python)]
:::
```
