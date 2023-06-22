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

Variable objects have hierarchical tree structure. Any variable object that corresponds to a composite type, such as structure in C, has a number of child variable objects, for example corresponding to each element of a structure. A child variable object can itself have children, recursively. Recursion ends when we reach leaf variable objects, which always have built-in types. Child variable objects are created only by explicit request, so if a frontend is not interested in the children of a particular variable object, no child will be created.

For a leaf variable object it is possible to obtain its value as a string, or set the value from a string. String value can be also obtained for a non-leaf variable object, but it's generally a string that only indicates the type of the object, and does not list its contents. Assignment to a non-leaf variable object is not allowed.

A frontend does not need to read the values of all variable objects each time the program stops. Instead, MI provides an update command that lists all variable objects whose values has changed since the last update operation. This considerably reduces the amount of data that must be transferred to the frontend. As noted above, children variable objects are created on demand, and only leaf variable objects have a real value. As result, gdb will read target memory only for leaf variables that frontend has created.

The automatic update is not always desirable. For example, a frontend might want to keep a value of some expression for future reference, and never update it. For another example, fetching memory is relatively slow for embedded targets, so a frontend might want to disable automatic update for the variables that are either not visible on the screen, or "closed". This is possible using so called "frozen variable objects". Such variable objects are never implicitly updated.

Variable objects can be either *fixed* or *floating*. For the fixed variable object, the expression is parsed when the variable object is created, including associating identifiers to specific variables. The meaning of expression never changes. For a floating variable object the values of variables whose names appear in the expressions are re-evaluated every time in the context of the current frame. Consider this example:

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

If an expression specified when creating a fixed variable object refers to a local variable, the variable object becomes bound to the thread and frame in which the variable object is created. When such variable object is updated, [GDB] makes sure that the thread/frame combination the variable object is bound to still exists, and re-evaluates the variable object in context of that thread/frame.

The following is the complete set of [GDB/MI] operations defined to access this functionality:

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

#### Description And Use of Operations on Variable Objects

#### The `-enable-pretty-printing` Command

::: smallexample

```bash
-enable-pretty-printing
```

:::

[GDB] allows Python-based visualizers to affect the output of the MI variable object commands. However, because there was no way to implement this in a fully backward-compatible way, a front end must request that this functionality be enabled.

Once enabled, this feature cannot be disabled.

Note that if Python support has not been compiled into [GDB], this command will still succeed (and do nothing).

#### The `-var-create` Command

#### Synopsis

::: smallexample

```bash
 -var-create 
     expression
```

:::

This operation creates a variable object, which allows the monitoring of a variable, the result of an expression, a memory cell or a CPU register.

The `name` of that format. The command fails if a duplicate name is found.

The frame under which the expression should be evaluated can be specified by `frame-addr`' indicates that a floating variable object must be created.

`expression`'), or one of the following:

- '`*addr` is the address of a memory cell
- '`*addr-addr`' --- a memory address range (TBD)
- '`$regname`' --- a CPU register name

A varobj's contents may be provided by a Python-based pretty-printer. In this case the varobj is known as a *dynamic varobj*. Dynamic varobjs have slightly different semantics in some cases. If the `-enable-pretty-printing` command is not sent, then [GDB] will never create a dynamic varobj. This ensures backward compatibility for existing clients.

#### Result

This operation returns attributes of the newly-created varobj. These are:

'`name`'

:   The name of the varobj.

'`numchild`'

:   The number of children of the varobj. This number is not necessarily reliable for a dynamic varobj. Instead, you must examine the '`has_more`' attribute.

'`value`'

:   The varobj's scalar value. For a varobj whose type is some sort of aggregate (e.g., a `struct`), this value will not be interesting. For a dynamic varobj, this value comes directly from the Python pretty-printer object's `to_string` method.

'`type`'

:   The varobj's type. This is a string representation of the type, as would be printed by the [GDB]' (see [set print object](Print-Settings.html#Print-Settings)) is set to `on`, the *actual* (derived) type of the object is shown rather than the *declared* one.

'`thread-id`'

:   If a variable object is bound to a specific thread, then this is the thread's global identifier.

'`has_more`'

:   For a dynamic varobj, this indicates whether there appear to be any children available. For a non-dynamic varobj, this will be 0.

'`dynamic`'

:   This attribute will be present and have the value '`1`' if the varobj is a dynamic varobj. If the varobj is not a dynamic varobj, then this attribute will not be present.

'`displayhint`'

:   A dynamic varobj can supply a display hint to the front end. The value comes directly from the Python pretty-printer object's `display_hint` method. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API).

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

The zero-hexadecimal format has a representation similar to hexadecimal but with padding zeroes to the left of the value. For example, a 32-bit hexadecimal value of 0x1234 would be represented as 0x00001234 in the zero-hexadecimal format.

For a variable with children, the format is set only on the variable itself, and the children are not affected.

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

#### The `-var-list-children` Command

#### Synopsis

::: smallexample

```bash
 -var-list-children [print-values] name [from to]
```

:::

Return a list of the children of the specified variable object and create variable objects for them, if they do not already exist. With a single argument or if `print-values` is 1 or `--all-values`, also print their values; and if it is 2 or `--simple-values` print the name and value for simple data types and just the name for arrays, structures and unions.

`from` will be reported.

If a child range is requested, it will only affect the current call to `-var-list-children`, but not future calls to `-var-update`. For this, you must instead use `-var-set-update-range`. The intent of this approach is to enable a front end to implement any update approach it likes; for example, scrolling a view may cause the front end to request more children with `-var-list-children`, and then the front end could call `-var-set-update-range` with a different range to ensure that future updates are restricted to just the visible items.

For each child the following results are returned:

`name`

:   Name of the variable object created for this child.

`exp`

:   The expression to be shown to the user by the front end to designate this child. For example this may be the name of a structure member.

```
For a dynamic varobj, this value cannot be used to form an expression. There is no way to do this at all with a dynamic varobj.

For C/C++ structures there are several pseudo children returned to designate access qualifiers. For these pseudo children `exp`'. In this case the type and value are not present.

A dynamic varobj will not report the access qualifying pseudo-children, regardless of the language. This information is not available at all with a dynamic varobj.
```

`numchild`

:   Number of children this child has. For a dynamic varobj, this will be 0.

`type`

:   The type of the child. If '`print object`' (see [set print object](Print-Settings.html#Print-Settings)) is set to `on`, the *actual* (derived) type of the object is shown rather than the *declared* one.

`value`

:   If values were requested, this is the value.

`thread-id`

:   If this variable object is associated with a thread, this is the thread's global thread id. Otherwise this result is not present.

`frozen`

:   If the variable object is frozen, this variable will be present with a value of 1.

`displayhint`

:   A dynamic varobj can supply a display hint to the front end. The value comes directly from the Python pretty-printer object's `display_hint` method. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API).

`dynamic`

:   This attribute will be present and have the value '`1`' if the varobj is a dynamic varobj. If the varobj is not a dynamic varobj, then this attribute will not be present.

The result may have its own attributes:

'`displayhint`'

:   A dynamic varobj can supply a display hint to the front end. The value comes directly from the Python pretty-printer object's `display_hint` method. See [Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API).

'`has_more`'

:   This is an integer attribute which is nonzero if there are children remaining after the end of the selected range.

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

For example, if `a` is an array, and variable object `A` was created for `a`, then we'll get this output:

::: smallexample

```bash
(gdb) -var-info-expression A.1
^done,lang="C",exp="1"
```

:::

Here, the value of `lang` is the language name, which can be found in [Supported Languages](Supported-Languages.html#Supported-Languages).

Note that the output of the `-var-list-children` command also includes those expressions, so the `-var-info-expression` command is of limited use.

#### The `-var-info-path-expression` Command

#### Synopsis

::: smallexample

```bash
 -var-info-path-expression name
```

:::

Returns an expression that can be evaluated in the current context and will yield the same value that a variable object has. Compare this with the `-var-info-expression` command, which result can be used only for UI presentation. Typical use of the `-var-info-path-expression` command is creating a watchpoint from a variable object.

This command is currently not valid for children of a dynamic varobj, and will give an error when invoked on one.

For example, suppose `C` is a C++ class, derived from class `Base`, and that the `Base` class has a member called `m_size`. Assume a variable `c` is has the type of `C` and a variable object `C` was created for variable `c`. Then, we'll get this output:

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

::: smallexample

```bash
 value=value
```

:::

Note that one must invoke `-var-list-children` for a variable before the value of a child variable can be evaluated.

#### The `-var-assign` Command

#### Synopsis

::: smallexample

```bash
 -var-assign name expression
```

:::

Assigns the value of `expression`'. If the variable's value is altered by the assign, the variable will show up in any subsequent `-var-update` list.

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

With the '`*`' parameter, if a variable object is bound to a currently running thread, it will not be updated, without any diagnostic.

If `-var-set-update-range` was previously used on a varobj, then only the selected range of children will be reported.

`-var-update` reports all the changed varobjs in a tuple named '`changelist`'.

Each item in the change list is itself a tuple holding:

'`name`'

:   The name of the varobj.

'`value`'

:   If values were requested for this update, then this field will be present and will hold the value of the varobj.

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

```
When a varobj's type changes, its children are also likely to have become incorrect. Therefore, the varobj's children are automatically deleted when this attribute is '`true`'. Also, the varobj's update range, when set using the `-var-set-update-range` command, is unset.
```

'`new_type`'

:   If the varobj's type changed, then this field will be present and will hold the new type.

'`new_num_children`'

:   For a dynamic varobj, if the number of children changed, or if the type changed, this will be the new number of children.

```
The '`numchild` knows about, but because dynamic varobjs lazily instantiate their children, this will not reflect the number of children which may be available.

The '`new_num_children`. This is the only way to detect whether an update has removed children (which necessarily can only happen at the end of the update range).
```

'`displayhint`'

:   The display hint, if any.

'`has_more`'

:   This is an integer value, which will be 1 if there are more children available outside the varobj's update range.

'`dynamic`'

:   This attribute will be present and have the value '`1`' if the varobj is a dynamic varobj. If the varobj is not a dynamic varobj, then this attribute will not be present.

'`new_children`'

:   If new children were added to a dynamic varobj within the selected update range (as set by `-var-set-update-range`), then they will be listed in this attribute.

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

The pre-defined function `gdb.default_visualizer` may be used to select a visualizer by following the built-in process (see [Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters)). This is done automatically when a varobj is created, and so ordinarily is not needed.

This feature is only available if Python support is enabled. The MI command `-list-features` (see [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands)) can be used to check this.

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
