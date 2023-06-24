---
tip: translate by openai@2023-06-24 00:43:36
...
---
description: Omissions from Ada (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Omissions from Ada (Debugging with GDB)
lang: en
resource-type: document
title: Omissions from Ada (Debugging with GDB)
---
::: header
Next: [Additions to Ada](Additions-to-Ada.html#Additions-to-Ada)]
:::

---

#### 15.4.10.2 Omissions from Ada

Here are the notable omissions from the subset:

- Only a subset of the attributes are supported:

  - \- \'First, \'Last, and \'Length on array objects (not on types and subtypes).
  - \- \'Min and \'Max.
  - \- \'Pos and \'Val.
  - \- \'Tag.

  - \- \'Range on array objects (not subtypes), but only as the right operand of the membership (`in`) operator.

> 数组对象（非子类型）的范围，但只能作为成员资格（`in`）操作符的右操作数。
  - \- \'Access, \'Unchecked_Access, and \'Unrestricted_Access (a GNAT extension).
  - \- \'Address.
- The names in `Characters.Latin_1` are not available.

- Equality tests ('`=`') on arrays test for bitwise equality of representations. They will generally work correctly for strings and arrays whose elements have integer or enumeration types. They may not work correctly for arrays whose element types have user-defined equality, for arrays of real values (in particular, IEEE-conformant floating point, because of negative zeroes and NaNs), and for arrays whose elements contain unused bits with indeterminate values.

> 数组上的等式测试（'='）检查表示的位级相等性。它们通常可以正确地工作于元素类型为整数或枚举类型的字符串和数组。它们可能不能正确地工作于元素类型拥有用户定义的等式的数组，实值数组（特别是IEEE兼容浮点数，因为负零和NaN），以及元素中包含未使用位且具有未确定值的数组。

- The other component-by-component array operations (`and`, `or`, `xor`, `not`, and relational tests other than equality) are not implemented.

> 其他组件分别的数组操作（`and`、`or`、`xor`、`not`以及除了等式以外的关系测试）尚未实现。

- There is limited support for array and record aggregates. They are permitted only on the right sides of assignments, as in these examples:

> 只支持有限的数组和记录聚合。它们只允许在赋值的右侧，如下例：

::: smallexample

```bash
(gdb) set An_Array := (1, 2, 3, 4, 5, 6)
(gdb) set An_Array := (1, others => 0)
(gdb) set An_Array := (0|4 => 1, 1..3 => 2, 5 => 6)
(gdb) set A_2D_Array := ((1, 2, 3), (4, 5, 6), (7, 8, 9))
(gdb) set A_Record := (1, "Peter", True);
(gdb) set A_Record := (Name => "Peter", Id => 1, Alive => True)
```

:::


Changing a discriminant's value by assigning an aggregate has an undefined effect if that discriminant is used within the record. However, you can first modify discriminants by directly assigning to them (which normally would not be allowed in Ada), and then performing an aggregate assignment. For example, given a variable `A_Rec` declared to have a type such as:

> 如果将聚合量赋值给鉴别量的值，则如果该鉴别量在记录中使用，则其效果就是未定义的。但是，您可以首先通过直接赋值来修改鉴别量（通常在Ada中是不允许的），然后执行聚合赋值。例如，给定一个声明具有如下类型的变量`A_Rec`：

::: smallexample

```bash
type Rec (Len : Small_Integer := 0) is record
    Id : Integer;
    Vals : IntArray (1 .. Len);
end record;
```

:::


you can assign a value with a different size of `Vals` with two assignments:

> 你可以用两个赋值来指定不同大小的Vals值：

::: smallexample

```bash
(gdb) set A_Rec.Len := 4
(gdb) set A_Rec := (Id => 42, Vals => (1, 2, 3, 4))
```

:::


As this example also illustrates, [GDB] is very loose about the usual rules concerning aggregates. You may leave out some of the components of an array or record aggregate (such as the `Len` component in the assignment to `A_Rec` above); they will retain their original values upon assignment. You may freely use dynamic values as indices in component associations. You may even use overlapping or redundant component associations, although which component values are assigned in such cases is not defined.

> 这个例子也表明，GDB对于聚合的通常规则非常宽松。您可以省略数组或记录聚合中的某些组件（例如上面对A_Rec的赋值中的'Len'组件）；它们在赋值时将保留其原始值。您可以自由地使用动态值作为组件关联中的索引。甚至可以使用重叠或冗余的组件关联，但在这种情况下分配哪些组件值尚不确定。

- Calls to dispatching subprograms are not implemented.

- The overloading algorithm is much more limited (i.e., less selective) than that of real Ada. It makes only limited use of the context in which a subexpression appears to resolve its meaning, and it is much looser in its rules for allowing type matches. As a result, some function calls will be ambiguous, and the user will be asked to choose the proper resolution.

> 算法的超载比真正的Ada要受限得多（即，选择性较弱）。它只有有限地利用子表达式出现的上下文来解释其意义，允许类型匹配的规则也要宽松得多。因此，一些函数调用会变得模棱两可，用户需要选择正确的解决方案。
- The `new` operator is not implemented.
- Entry calls are not implemented.

- Aside from printing, arithmetic operations on the native VAX floating-point formats are not supported.

> 除了打印，VAX原生浮点格式的算术操作不受支持。
- It is not possible to slice a packed array.

- The names `True` and `False`, when not part of a qualified name, are interpreted as if implicitly prefixed by `Standard`, regardless of context. Should your program redefine these names in a package or procedure (at best a dubious practice), you will have to use fully qualified names to access their new definitions.

> 真和假这两个名称，如果不是作为一个限定名称的一部分，将被解释为隐式地加上了Standard前缀，不管上下文如何。如果你的程序在一个包或过程中重新定义了这些名称（最好不要这么做），你将不得不使用完全限定的名称来访问它们的新定义。
- Based real literals are not implemented.

---

::: header
Next: [Additions to Ada](Additions-to-Ada.html#Additions-to-Ada)]
:::
