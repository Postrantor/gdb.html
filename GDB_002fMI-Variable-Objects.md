---
tip: translate by openai@2023-06-23 22:24:56
...
---
description: GDB/MI Variable Objects (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Variable Objects (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Variable Objects (Debugging with GDB)
---
::: header
Next: [GDB/MI Data Manipulation](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation)]
:::

---

### 27.15 [GDB/MI]

#### Introduction to Variable Objects


Variable objects are \"object-oriented\" MI interface for examining and changing values of expressions. Unlike some other MI interfaces that work with expressions, variable objects are specifically designed for simple and efficient presentation in the frontend. A variable object is identified by string name. When a variable object is created, the frontend specifies the expression for that variable object. The expression can be a simple variable, or it can be an arbitrary complex expression, and can even involve CPU registers. After creating a variable object, the frontend can invoke other variable object operations---for example to obtain or change the value of a variable object, or to change display format.

> 变量对象是一种面向对象的MI接口，用于检查和更改表达式的值。与一些其他针对表达式工作的MI接口不同，变量对象专门设计用于在前端进行简单高效的呈现。变量对象由字符串名称标识。当创建变量对象时，前端指定该变量对象的表达式。表达式可以是简单的变量，也可以是任意复杂的表达式，甚至可以涉及CPU寄存器。创建变量对象后，前端可以调用其他变量对象操作——例如获取或更改变量对象的值，或者更改显示格式。


Variable objects have hierarchical tree structure. Any variable object that corresponds to a composite type, such as structure in C, has a number of child variable objects, for example corresponding to each element of a structure. A child variable object can itself have children, recursively. Recursion ends when we reach leaf variable objects, which always have built-in types. Child variable objects are created only by explicit request, so if a frontend is not interested in the children of a particular variable object, no child will be created.

> 变量对象具有层次树结构。任何对应于复合类型（如C中的结构）的变量对象都有许多子变量对象，例如对应于结构的每个元素。子变量对象本身可以有子对象，这是递归的。当我们到达叶变量对象时，递归结束，这些变量对象总是具有内置类型。子变量对象只有在明确请求时才会被创建，因此，如果前端对特定变量对象的子对象不感兴趣，则不会创建子对象。


For a leaf variable object it is possible to obtain its value as a string, or set the value from a string. String value can be also obtained for a non-leaf variable object, but it's generally a string that only indicates the type of the object, and does not list its contents. Assignment to a non-leaf variable object is not allowed.

> 对于叶变量对象，可以将其值作为字符串获取，或者从字符串设置值。也可以为非叶变量对象获取字符串值，但通常是一个仅指示对象类型的字符串，而不列出其内容。不允许对非叶变量对象进行赋值。


A frontend does not need to read the values of all variable objects each time the program stops. Instead, MI provides an update command that lists all variable objects whose values has changed since the last update operation. This considerably reduces the amount of data that must be transferred to the frontend. As noted above, children variable objects are created on demand, and only leaf variable objects have a real value. As result, gdb will read target memory only for leaf variables that frontend has created.

> 前端在程序停止时不需要读取所有变量对象的值。相反，MI提供了一个更新命令，它列出了自上次更新操作以来值发生变化的所有变量对象。这大大减少了必须传输到前端的数据量。如上所述，子变量对象是按需创建的，只有叶变量对象才有真实值。因此，GDB只会为前端创建的叶变量读取目标内存。


The automatic update is not always desirable. For example, a frontend might want to keep a value of some expression for future reference, and never update it. For another example, fetching memory is relatively slow for embedded targets, so a frontend might want to disable automatic update for the variables that are either not visible on the screen, or "closed". This is possible using so called "frozen variable objects". Such variable objects are never implicitly updated.

> 自动更新并不总是可取的。例如，前端可能想要保留某个表达式的值以供将来参考，并且永不更新它。另一个例子是，对于嵌入式目标来说，获取内存相对较慢，因此前端可能希望禁用不可见或“关闭”的变量的自动更新。这可以使用所谓的“冻结变量对象”来实现。这种变量对象永远不会被隐式更新。


Variable objects can be either *fixed* or *floating*. For the fixed variable object, the expression is parsed when the variable object is created, including associating identifiers to specific variables. The meaning of expression never changes. For a floating variable object the values of variables whose names appear in the expressions are re-evaluated every time in the context of the current frame. Consider this example:

> 可变对象可以是固定的或浮动的。对于固定变量对象，在创建变量对象时就会解析表达式，包括将标识符关联到特定变量。表达式的意义永远不会改变。对于浮动变量对象，表达式中出现的变量的值每次都会根据当前帧的上下文重新计算。例如：

::: smallexample

```bash
void do_work(...)
{
        struct work_state state;

        if (...)
           do_work(...);
}
```

:::


If a fixed variable object for the `state` variable is created in this function, and we enter the recursive call, the variable object will report the value of `state` in the top-level `do_work` invocation. On the other hand, a floating variable object will report the value of `state` in the current frame.

> 如果在这个函数中创建了一个固定的变量对象`state`，并且我们进入递归调用，那么变量对象将报告顶级`do_work`调用中`state`的值。另一方面，浮动变量对象将报告当前帧中`state`的值。


If an expression specified when creating a fixed variable object refers to a local variable, the variable object becomes bound to the thread and frame in which the variable object is created. When such variable object is updated, [GDB] makes sure that the thread/frame combination the variable object is bound to still exists, and re-evaluates the variable object in context of that thread/frame.

> 如果在创建固定变量对象时指定的表达式引用了本地变量，则该变量对象将绑定到创建变量对象的线程和框架中。当这样的变量对象被更新时，[GDB]确保变量对象绑定的线程/框架组仍然存在，并在该线程/框架的上下文中重新评估变量对象。


The following is the complete set of [GDB/MI] operations defined to access this functionality:

> 以下是访问此功能所定义的完整 GDB/MI 操作集：

---

**Operation**                 **Description**
`-enable-pretty-printing`     enable Python-based pretty-printing
`-var-create`                 create a variable object
`-var-delete`                 delete the variable object and/or its children
`-var-set-format`             set the display format of this variable
`-var-show-format`            show the display format of this variable
`-var-info-num-children`      tells how many children this object has
`-var-list-children`          return a list of the object's children
`-var-info-type`              show the type of this variable object
`-var-info-expression`        print parent-relative expression that this variable object represents
`-var-info-path-expression`   print full expression that this variable object represents
`-var-show-attributes`        is this variable editable? does it exist here?
`-var-evaluate-expression`    get the value of this variable
`-var-assign`                 set the value of this variable
`-var-update`                 update the variable and its children
`-var-set-frozen`             set frozenness attribute
`-var-set-update-range`       set range of children to display on update

---


In the next subsection we describe each operation in detail and suggest how it can be used.

> 在下一小节中，我们将详细描述每项操作，并提出如何使用它们的建议。

#### Description And Use of Operations on Variable Objects

#### The `-enable-pretty-printing` Command

::: smallexample

```bash
-enable-pretty-printing
```

:::


[GDB] allows Python-based visualizers to affect the output of the MI variable object commands. However, because there was no way to implement this in a fully backward-compatible way, a front end must request that this functionality be enabled.

> [GDB]允许基于Python的可视化器影响MI变量对象命令的输出。但是，由于没有办法以完全向后兼容的方式实现这一功能，前端必须请求启用此功能。

Once enabled, this feature cannot be disabled.


Note that if Python support has not been compiled into [GDB], this command will still succeed (and do nothing).

> 如果GDB中没有编译进Python支持，这个命令仍然会成功（但不做任何事情）。

#### The `-var-create` Command

#### Synopsis

::: smallexample

```bash
 -var-create 
     expression
```

:::


This operation creates a variable object, which allows the monitoring of a variable, the result of an expression, a memory cell or a CPU register.

> 这个操作创建了一个变量对象，它允许监视变量、表达式的结果、内存单元或CPU寄存器。


The `name` of that format. The command fails if a duplicate name is found.

> 那种格式的名称。如果发现重复的名称，命令将失败。


The frame under which the expression should be evaluated can be specified by `frame-addr`' indicates that a floating variable object must be created.

> `frame-addr` 指定的框架下可以评估表达式，这意味着必须创建一个浮动变量对象。

`expression`'), or one of the following:

- '`*addr` is the address of a memory cell
- '`*addr-addr`' --- a memory address range (TBD)
- '`$regname`' --- a CPU register name


A varobj's contents may be provided by a Python-based pretty-printer. In this case the varobj is known as a *dynamic varobj*. Dynamic varobjs have slightly different semantics in some cases. If the `-enable-pretty-printing` command is not sent, then [GDB] will never create a dynamic varobj. This ensures backward compatibility for existing clients.

> 一个varobj的内容可能由基于Python的格式化程序提供。在这种情况下，varobj被称为*动态varobj*。动态varobjs在某些情况下具有稍微不同的语义。如果没有发送`-enable-pretty-printing`命令，那么[GDB]永远不会创建动态varobj。这确保了现有客户端的向后兼容性。

#### Result

This operation returns attributes of the newly-created varobj. These are:

'`name`'

:   The name of the varobj.

'`numchild`'


:   The number of children of the varobj. This number is not necessarily reliable for a dynamic varobj. Instead, you must examine the '`has_more`' attribute.

> varobj的孩子数量。对于一个动态varobj来说，这个数字不一定可靠。你必须检查'has_more'属性。

'`value`'


:   The varobj's scalar value. For a varobj whose type is some sort of aggregate (e.g., a `struct`), this value will not be interesting. For a dynamic varobj, this value comes directly from the Python pretty-printer object's `to_string` method.

> 变量对象的标量值。对于某种聚合类型（例如`struct`）的变量对象，这个值不会很有趣。对于动态变量对象，这个值直接来自Python美化打印对象的`to_string`方法。

'`type`'


:   The varobj's type. This is a string representation of the type, as would be printed by the [GDB]' (see [set print object](Print-Settings.html#Print-Settings)) is set to `on`, the *actual* (derived) type of the object is shown rather than the *declared* one.

> 这个varobj的类型。如果[GDB]的[set print object]（见[Print Settings]）设置为“on”，则显示的是实际（派生）类型而不是声明的类型，这是一个字符串表示。

'`thread-id`'


:   If a variable object is bound to a specific thread, then this is the thread's global identifier.

> 如果一个变量对象绑定到特定的线程，那么这就是该线程的全局标识符。

'`has_more`'


:   For a dynamic varobj, this indicates whether there appear to be any children available. For a non-dynamic varobj, this will be 0.

> 对于动态varobj，这表明是否似乎有可用的子项。对于非动态varobj，这将为0。

'`dynamic`'


:   This attribute will be present and have the value '`1`' if the varobj is a dynamic varobj. If the varobj is not a dynamic varobj, then this attribute will not be present.

> 这个属性如果varobj是一个动态varobj，将会出现并具有值'1'。如果varobj不是动态varobj，那么这个属性将不会出现。

'`displayhint`'


:   A dynamic varobj can supply a display hint to the front end. The value comes directly from the Python pretty-printer object's `display_hint` method. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API).

> 动态varobj可以向前端提供显示提示。该值直接来自Python pretty-printer对象的`display_hint`方法。请参阅[Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)。

Typical output will look like this:

::: smallexample

```bash
 name="name",numchild="N",type="type",thread-id="M",
  has_more="has_more"
```

:::

#### The `-var-delete` Command

#### Synopsis

::: smallexample

```bash
 -var-delete [ -c ] name
```

:::


Deletes a previously created variable object and all of its children. With the '`-c`' option, just deletes the children.

> 删除之前创建的变量对象及其所有子对象。使用 '-c' 选项，只删除子对象。

Returns an error if the object `name` is not found.

#### The `-var-set-format` Command

#### Synopsis

::: smallexample

```bash
 -var-set-format name format-spec
```

:::

Sets the output format for the value of the object `name`.

The syntax for the `format-spec` is as follows:

::: smallexample

```bash
 format-spec →
 
```

:::


The natural format is the default format choosen automatically based on the variable type (like decimal for an `int`, hex for pointers, etc.).

> 默认格式是根据变量类型（如int的十进制，指针的十六进制等）自动选择的自然格式。


The zero-hexadecimal format has a representation similar to hexadecimal but with padding zeroes to the left of the value. For example, a 32-bit hexadecimal value of 0x1234 would be represented as 0x00001234 in the zero-hexadecimal format.

> 零十六进制格式具有与十六进制类似的表示形式，但在值的左侧填充零。例如，32位十六进制值0x1234将以零十六进制格式表示为0x00001234。


For a variable with children, the format is set only on the variable itself, and the children are not affected.

> 对于一个具有子变量的变量，格式只能设置在变量本身上，子变量不受影响。

#### The `-var-show-format` Command

#### Synopsis

::: smallexample

```bash
 -var-show-format name
```

:::

Returns the format used to display the value of the object `name`.

::: smallexample

```bash
 format →
 format-spec
```

:::

#### The `-var-info-num-children` Command

#### Synopsis

::: smallexample

```bash
 -var-info-num-children name
```

:::

Returns the number of children of a variable object `name`:

::: smallexample

```bash
 numchild=n
```

:::


Note that this number is not completely reliable for a dynamic varobj. It will return the current number of children, but more children may be available.

> 注意，对于动态varobj，这个数字并不完全可靠。它会返回当前的子元素数量，但可能还有更多的子元素可用。

#### The `-var-list-children` Command

#### Synopsis

::: smallexample

```bash
 -var-list-children [print-values] name [from to]
```

:::


Return a list of the children of the specified variable object and create variable objects for them, if they do not already exist. With a single argument or if `print-values` is 1 or `--all-values`, also print their values; and if it is 2 or `--simple-values` print the name and value for simple data types and just the name for arrays, structures and unions.

> 返回指定变量对象的子对象列表，如果这些子对象不存在，则创建它们的变量对象。如果只有一个参数，或者`print-values`为1或`--all-values`，则还会打印它们的值；如果它是2或`--simple-values`，则只会为简单数据类型打印名称和值，而对于数组、结构和联合类型只打印名称。

`from` will be reported.


If a child range is requested, it will only affect the current call to `-var-list-children`, but not future calls to `-var-update`. For this, you must instead use `-var-set-update-range`. The intent of this approach is to enable a front end to implement any update approach it likes; for example, scrolling a view may cause the front end to request more children with `-var-list-children`, and then the front end could call `-var-set-update-range` with a different range to ensure that future updates are restricted to just the visible items.

> 如果请求子范围，它只会影响对`-var-list-children`的当前调用，而不会影响对`-var-update`的未来调用。为此，您必须使用`-var-set-update-range`。此方法的目的是使前端可以实现任何更新方法；例如，滚动视图可能会导致前端使用`-var-list-children`请求更多的子项，然后前端可以使用不同的范围调用`-var-set-update-range`，以确保未来的更新仅限于可见项目。

For each child the following results are returned:

`name`

:   Name of the variable object created for this child.

`exp`


:   The expression to be shown to the user by the front end to designate this child. For example this may be the name of a structure member.

> 给用户显示的表达式，用来指定这个孩子。例如，这可能是结构成员的名称。

```
For a dynamic varobj, this value cannot be used to form an expression. There is no way to do this at all with a dynamic varobj.

For C/C++ structures there are several pseudo children returned to designate access qualifiers. For these pseudo children `exp`'. In this case the type and value are not present.

A dynamic varobj will not report the access qualifying pseudo-children, regardless of the language. This information is not available at all with a dynamic varobj.
```

`numchild`


:   Number of children this child has. For a dynamic varobj, this will be 0.

> 这个孩子有多少个孩子？对于一个动态的varobj，这将是0。

`type`


:   The type of the child. If '`print object`' (see [set print object](Print-Settings.html#Print-Settings)) is set to `on`, the *actual* (derived) type of the object is shown rather than the *declared* one.

> 子类型。如果设置了“打印对象”（参见[设置打印对象]（Print-Settings.html#Print-Settings）），则显示实际（派生）类型而不是声明的类型。

`value`

:   If values were requested, this is the value.

`thread-id`


:   If this variable object is associated with a thread, this is the thread's global thread id. Otherwise this result is not present.

> 如果这个变量对象与线程相关联，这是线程的全局线程ID。否则，此结果不存在。

`frozen`


:   If the variable object is frozen, this variable will be present with a value of 1.

> 如果变量对象被冻结，这个变量将以1的值出现。

`displayhint`


:   A dynamic varobj can supply a display hint to the front end. The value comes directly from the Python pretty-printer object's `display_hint` method. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API).

> 动态varobj可以向前端提供显示提示。该值直接来自Python pretty-printer对象的“display_hint”方法。请参见[Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)。

`dynamic`


:   This attribute will be present and have the value '`1`' if the varobj is a dynamic varobj. If the varobj is not a dynamic varobj, then this attribute will not be present.

> 这个属性将会存在，并且具有值'1'，如果varobj是一个动态varobj。如果varobj不是一个动态varobj，那么这个属性将不会存在。

The result may have its own attributes:

'`displayhint`'


:   A dynamic varobj can supply a display hint to the front end. The value comes directly from the Python pretty-printer object's `display_hint` method. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API).

> 动态varobj可以为前端提供显示提示。该值直接来自Python pretty-printer对象的`display_hint`方法。请参阅[Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)。

'`has_more`'


:   This is an integer attribute which is nonzero if there are children remaining after the end of the selected range.

> 这是一个整数属性，如果在所选范围结束后仍有子元素，则该属性值不为零。

#### Example

::: smallexample

```bash
(gdb)
 -var-list-children n
 ^done,numchild=n,children=[child={name=name,exp=exp,
 numchild=n,type=type},(repeats N times)]
(gdb)
 -var-list-children --all-values n
 ^done,numchild=n,children=[child={name=name,exp=exp,
 numchild=n,value=value,type=type},(repeats N times)]
```

:::

#### The `-var-info-type` Command

#### Synopsis

::: smallexample

```bash
 -var-info-type name
```

:::

Returns the type of the specified variable `name` CLI:

::: smallexample

```bash
 type=typename
```

:::

#### The `-var-info-expression` Command

#### Synopsis

::: smallexample

```bash
 -var-info-expression name
```

:::


Returns a string that is suitable for presenting this variable object in user interface. The string is generally not valid expression in the current language, and cannot be evaluated.

> 返回一个适合在用户界面中展示此变量对象的字符串。该字符串通常不是当前语言中的有效表达式，也无法求值。


For example, if `a` is an array, and variable object `A` was created for `a`, then we'll get this output:

> 例如，如果`a`是一个数组，并且为`a`创建了变量对象`A`，那么我们将得到这样的输出：

::: smallexample

```bash
(gdb) -var-info-expression A.1
^done,lang="C",exp="1"
```

:::


Here, the value of `lang` is the language name, which can be found in [Supported Languages](Supported-Languages.html#Supported-Languages).

> 这里，`lang` 的值是语言名称，可以在[支持的语言](Supported-Languages.html#Supported-Languages)中找到。


Note that the output of the `-var-list-children` command also includes those expressions, so the `-var-info-expression` command is of limited use.

> 注意，`-var-list-children` 命令的输出也包括那些表达式，因此 `-var-info-expression` 命令的用处有限。

#### The `-var-info-path-expression` Command

#### Synopsis

::: smallexample

```bash
 -var-info-path-expression name
```

:::


Returns an expression that can be evaluated in the current context and will yield the same value that a variable object has. Compare this with the `-var-info-expression` command, which result can be used only for UI presentation. Typical use of the `-var-info-path-expression` command is creating a watchpoint from a variable object.

> 返回一个可以在当前上下文中求值的表达式，其结果与变量对象具有相同的值。与`-var-info-expression`命令进行比较，其结果仅可用于UI呈现。`-var-info-path-expression`命令的典型用途是从变量对象创建断点。


This command is currently not valid for children of a dynamic varobj, and will give an error when invoked on one.

> 此命令目前不适用于动态varobj的子类，在其上调用时会出错。


For example, suppose `C` is a C++ class, derived from class `Base`, and that the `Base` class has a member called `m_size`. Assume a variable `c` is has the type of `C` and a variable object `C` was created for variable `c`. Then, we'll get this output:

> 例如，假设`C`是从类`Base`派生的C++类，而`Base`类具有名为`m_size`的成员。假设变量`c`的类型为`C`，并且为变量`c`创建了一个`C`类型的对象。那么，我们将得到以下输出：

::: smallexample

```bash
(gdb) -var-info-path-expression C.Base.public.m_size
^done,path_expr=((Base)c).m_size)
```

:::

#### The `-var-show-attributes` Command

#### Synopsis

::: smallexample

```bash
 -var-show-attributes name
```

:::

List attributes of the specified variable object `name`:

::: smallexample

```bash
 status=attr [ ( ,attr )* ]
```

:::

where `attr``.

#### The `-var-evaluate-expression` Command

#### Synopsis

::: smallexample

```bash
 -var-evaluate-expression [-f format-spec] name
```

:::


Evaluates the expression that is represented by the specified variable object and returns its value as a string. The format of the string can be specified with the '`-f`' option is not specified, the current display format will be used. The current display format can be changed using the `-var-set-format` command.

> 用指定的变量对象评估表达式，并将其结果以字符串形式返回。如果没有指定'-f'选项，则将使用当前的显示格式。可以使用'-var-set-format'命令更改当前的显示格式。

::: smallexample

```bash
 value=value
```

:::


Note that one must invoke `-var-list-children` for a variable before the value of a child variable can be evaluated.

> 注意，在评估子变量的值之前，必须调用`-var-list-children`来获取变量。

#### The `-var-assign` Command

#### Synopsis

::: smallexample

```bash
 -var-assign name expression
```

:::


Assigns the value of `expression`'. If the variable's value is altered by the assign, the variable will show up in any subsequent `-var-update` list.

> 将`表达式`的值分配给变量，如果变量的值被分配改变，该变量将在任何后续的`-var-update`列表中显示。

#### Example

::: smallexample

```bash
(gdb)
-var-assign var1 3
^done,value="3"
(gdb)
-var-update *
^done,changelist=
(gdb)
```

:::

#### The `-var-update` Command

#### Synopsis

::: smallexample

```bash
 -var-update [print-values] 
```

:::


Reevaluate the expressions corresponding to the variable object `name`' option, to reduce the number of MI commands needed on each program stop.

> 重新评估与变量对象`name`相关的表达式，以减少每个程序停止时需要的MI命令数量。


With the '`*`' parameter, if a variable object is bound to a currently running thread, it will not be updated, without any diagnostic.

> 使用'*'参数，如果变量对象绑定到当前正在运行的线程，则不会更新，没有任何诊断信息。


If `-var-set-update-range` was previously used on a varobj, then only the selected range of children will be reported.

> 如果之前在varobj上使用了`-var-set-update-range`，那么只会报告所选范围的子项。

`-var-update` reports all the changed varobjs in a tuple named '`changelist`'.

Each item in the change list is itself a tuple holding:

'`name`'

:   The name of the varobj.

'`value`'


:   If values were requested for this update, then this field will be present and will hold the value of the varobj.

> 如果此更新需要请求值，那么此字段将会出现，并保存varobj的值。

'`in_scope`'

:

```
This field is a string which may take one of three values:

`"true"`

:   The variable object's current value is valid.

`"false"`

:   The variable object does not currently hold a valid value but it may hold one in the future if its associated expression comes back into scope.

`"invalid"`

:   The variable object no longer holds a valid value. This can occur when the executable file being debugged has changed, either through recompilation or by using the [GDB] `file` command. The front end should normally choose to delete these variable objects.

In the future new values may be added to this list so the front should be prepared for this possibility. See [[GDB/MI] Development and Front Ends](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends).
```

'`type_changed`'


:   This is only present if the varobj is still valid. If the type changed, then this will be the string '`true`'.

> 如果varobj仍然有效，则会出现这个。如果类型改变了，那么这将是字符串“true”。

```
When a varobj's type changes, its children are also likely to have become incorrect. Therefore, the varobj's children are automatically deleted when this attribute is '`true`'. Also, the varobj's update range, when set using the `-var-set-update-range` command, is unset.
```

'`new_type`'


:   If the varobj's type changed, then this field will be present and will hold the new type.

> 如果varobj的类型发生改变，那么这个字段将会出现，并保存新的类型。

'`new_num_children`'


:   For a dynamic varobj, if the number of children changed, or if the type changed, this will be the new number of children.

> 对于一个动态的varobj，如果子节点数量发生变化，或者类型发生变化，这将是新的子节点数量。

```
The '`numchild` knows about, but because dynamic varobjs lazily instantiate their children, this will not reflect the number of children which may be available.

The '`new_num_children`. This is the only way to detect whether an update has removed children (which necessarily can only happen at the end of the update range).
```

'`displayhint`'

:   The display hint, if any.

'`has_more`'


:   This is an integer value, which will be 1 if there are more children available outside the varobj's update range.

> 这是一个整数值，如果varobj更新范围之外有更多的孩子可用，那么它将为1。

'`dynamic`'


:   This attribute will be present and have the value '`1`' if the varobj is a dynamic varobj. If the varobj is not a dynamic varobj, then this attribute will not be present.

> 这个属性如果varobj是一个动态varobj，那么它将会出现并且具有值“1”。如果varobj不是一个动态varobj，那么这个属性将不会出现。

'`new_children`'


:   If new children were added to a dynamic varobj within the selected update range (as set by `-var-set-update-range`), then they will be listed in this attribute.

> 如果在所选择的更新范围内（由`-var-set-update-range`设定）添加了新的子节点到动态varobj中，那么它们将在此属性中列出。

#### Example

::: smallexample

```bash
(gdb)
-var-assign var1 3
^done,value="3"
(gdb)
-var-update --all-values var1
^done,changelist=[{name="var1",value="3",in_scope="true",
type_changed="false"}]
(gdb)
```

:::

#### The `-var-set-frozen` Command

#### Synopsis

::: smallexample

```bash
 -var-set-frozen name flag
```

:::


Set the frozenness flag on the variable object `name`' to make it unfrozen. If a variable object is frozen, then neither itself, nor any of its children, are implicitly updated by `-var-update` of a parent variable or by `-var-update *`. Only `-var-update` of the variable itself will update its value and values of its children. After a variable object is unfrozen, it is implicitly updated by all subsequent `-var-update` operations. Unfreezing a variable does not update it, only subsequent `-var-update` does.

> 将变量对象`name`上的冻结标志设置为不冻结。如果变量对象被冻结，那么它本身和它的子对象都不会被父变量的`-var-update`或`-var-update *`隐式更新。只有变量本身的`-var-update`才能更新它的值和子值。变量对象被解冻后，将被所有后续的`-var-update`操作隐式更新。解冻变量不会更新它，只有后续的`-var-update`才会更新它。

#### Example

::: smallexample

```bash
(gdb)
-var-set-frozen V 1
^done
(gdb)
```

:::

#### The `-var-set-update-range` command

#### Synopsis

::: smallexample

```bash
 -var-set-update-range name from to
```

:::


Set the range of children to be returned by future invocations of `-var-update`.

> 设置将在未来调用 `-var-update` 时返回的子级范围。

`from` will be reported.

#### Example

::: smallexample

```bash
(gdb)
-var-set-update-range V 1 2
^done
```

:::

#### The `-var-set-visualizer` command

#### Synopsis

::: smallexample

```bash
 -var-set-visualizer name visualizer
```

:::

Set a visualizer for the variable object `name`.

`visualizer`' means to disable any visualizer in use.


If not '`None` as an argument (this is done so that the same Python pretty-printing code can be used for both the CLI and MI). When called, this object must return an object which conforms to the pretty-printing interface (see [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)).

> 如果没有作为参数传入'None'（这样做是为了可以使用相同的Python美化打印代码为CLI和MI服务），调用此对象时必须返回符合美化打印接口的对象（参见[美化打印API](Pretty-Printing-API.html#Pretty-Printing-API)）。


The pre-defined function `gdb.default_visualizer` may be used to select a visualizer by following the built-in process (see [Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters)). This is done automatically when a varobj is created, and so ordinarily is not needed.

> 函数`gdb.default_visualizer`可以用来通过内置流程（参见[选择Pretty-Printers]（Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters））来选择可视化器。当创建varobj时会自动执行此操作，因此通常不需要。


This feature is only available if Python support is enabled. The MI command `-list-features` (see [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands)) can be used to check this.

> 此功能仅在启用Python支持时可用。可以使用MI命令`-list-features`（参见[GDB / MI支持命令] (GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands)）来检查此项。

#### Example

Resetting the visualizer:

::: smallexample

```bash
(gdb)
-var-set-visualizer V None
^done
```

:::

Reselecting the default (type-based) visualizer:

::: smallexample

```bash
(gdb)
-var-set-visualizer V gdb.default_visualizer
^done
```

:::


Suppose `SomeClass` is a visualizer class. A lambda expression can be used to instantiate this class for a varobj:

> 假设`SomeClass`是一个可视化类。可以使用lambda表达式为varobj实例化此类：

::: smallexample

```bash
(gdb)
-var-set-visualizer V "lambda val: SomeClass()"
^done
```

:::

---

::: header
Next: [GDB/MI Data Manipulation](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation)]
:::
