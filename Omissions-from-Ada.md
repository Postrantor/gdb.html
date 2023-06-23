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
  - \- \'Access, \'Unchecked_Access, and \'Unrestricted_Access (a GNAT extension).
  - \- \'Address.
- The names in `Characters.Latin_1` are not available.
- Equality tests ('`=`') on arrays test for bitwise equality of representations. They will generally work correctly for strings and arrays whose elements have integer or enumeration types. They may not work correctly for arrays whose element types have user-defined equality, for arrays of real values (in particular, IEEE-conformant floating point, because of negative zeroes and NaNs), and for arrays whose elements contain unused bits with indeterminate values.
- The other component-by-component array operations (`and`, `or`, `xor`, `not`, and relational tests other than equality) are not implemented.
- There is limited support for array and record aggregates. They are permitted only on the right sides of assignments, as in these examples:

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

::: smallexample

```bash
type Rec (Len : Small_Integer := 0) is record
    Id : Integer;
    Vals : IntArray (1 .. Len);
end record;
```

:::

you can assign a value with a different size of `Vals` with two assignments:

::: smallexample

```bash
(gdb) set A_Rec.Len := 4
(gdb) set A_Rec := (Id => 42, Vals => (1, 2, 3, 4))
```

:::

As this example also illustrates, [GDB] is very loose about the usual rules concerning aggregates. You may leave out some of the components of an array or record aggregate (such as the `Len` component in the assignment to `A_Rec` above); they will retain their original values upon assignment. You may freely use dynamic values as indices in component associations. You may even use overlapping or redundant component associations, although which component values are assigned in such cases is not defined.

- Calls to dispatching subprograms are not implemented.
- The overloading algorithm is much more limited (i.e., less selective) than that of real Ada. It makes only limited use of the context in which a subexpression appears to resolve its meaning, and it is much looser in its rules for allowing type matches. As a result, some function calls will be ambiguous, and the user will be asked to choose the proper resolution.
- The `new` operator is not implemented.
- Entry calls are not implemented.
- Aside from printing, arithmetic operations on the native VAX floating-point formats are not supported.
- It is not possible to slice a packed array.
- The names `True` and `False`, when not part of a qualified name, are interpreted as if implicitly prefixed by `Standard`, regardless of context. Should your program redefine these names in a package or procedure (at best a dubious practice), you will have to use fully qualified names to access their new definitions.
- Based real literals are not implemented.

---

::: header
Next: [Additions to Ada](Additions-to-Ada.html#Additions-to-Ada)]
:::
