---
tip: translate by openai@2023-06-24 03:46:42
...
---
description: Target Description Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Target Description Format (Debugging with GDB)
lang: en
resource-type: document
title: Target Description Format (Debugging with GDB)
---
::: header
Next: [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)]
:::

---

### G.2 Target Description Format


A target description annex is an [XML](http://www.w3.org/XML/) document which complies with the Document Type Definition provided in the [GDB]. This means you can use generally available tools like `xmllint` to check that your feature descriptions are well-formed and valid. However, to help people unfamiliar with XML write descriptions for their targets, we also describe the grammar here.

> 附件目标描述是一个符合[GDB]提供的文档类型定义的[XML](http://www.w3.org/XML/)文档。这意味着您可以使用通用的工具，如`xmllint`来检查您的特征描述是否良好形成和有效的。但是，为了帮助不熟悉XML的人编写他们目标的描述，我们还在这里描述语法。


Target descriptions can identify the architecture of the remote target and (for some architectures) provide information about custom register sets. They can also identify the OS ABI of the remote target. [GDB] can use this information to autoconfigure for your target, or to warn you if you connect to an unsupported target.

> 目标描述可以识别远程目标的体系结构，并（对于某些体系结构）提供有关自定义寄存器集的信息。它们还可以识别远程目标的OS ABI。[GDB]可以使用此信息自动配置您的目标，或者如果您连接到不受支持的目标，则发出警告。

Here is a simple target description:

::: smallexample

```bash
<target version="1.0">
  <architecture>i386:x86-64</architecture>
</target>
```

:::


This minimal description only says that the target uses the x86-64 architecture.

> 这个最小的描述只说明目标使用x86-64体系结构。


A target description has the following overall form, with \[ ] marking optional elements and ... marking repeatable elements. The elements are explained further below.

> 目标描述的整体形式如下，\[ ] 标记可选元素，... 标记可重复元素，元素的详细解释在下面。

::: smallexample

```bash
<?xml version="1.0"?>
<!DOCTYPE target SYSTEM "gdb-target.dtd">
<target version="1.0">
  [architecture]
  [osabi]
  [compatible]
  [feature…]
</target>
```

:::


The description is generally insensitive to whitespace and line breaks, under the usual common-sense rules. The XML version declaration and document type declaration can generally be omitted ([GDB], they will detect and report the version mismatch.

> 描述通常对空格和换行符不敏感，根据通常的常识规则。 XML版本声明和文档类型声明通常可以省略（[GDB]，它们将检测并报告版本不匹配。

#### G.2.1 Inclusion


It can sometimes be valuable to split a target description up into several different annexes, either for organizational purposes, or to share files between different possible target descriptions. You can divide a description into multiple files by replacing any element of the target description with an inclusion directive of the form:

> 有时将目标描述分成几个不同的附件可能是有价值的，无论是出于组织目的，还是为了在不同可能的目标描述之间共享文件。您可以通过使用形式如下的包含指令来将描述分成多个文件：

::: smallexample

```bash
<xi:include href="document"/>
```

:::


When [GDB] as a file in the same directory where it found the original description.

> 当[GDB]作为文件存放在与原始描述相同的目录中时。

#### G.2.2 Architecture

An '`<architecture>`' element has this form:

::: smallexample

```bash
  <architecture>arch</architecture>
```

:::

`arch` is one of the architectures from the set accepted by `set architecture` (see [Specifying a Debugging Target](Targets.html#Targets)).

#### G.2.3 OS ABI

This optional field was introduced in [GDB] ignore it.

An '`<osabi>`' element has this form:

::: smallexample

```bash
  <osabi>abi-name</osabi>
```

:::

`abi-name` is an OS ABI name from the same selection accepted by `set osabi` (see [Configuring the Current ABI](ABI.html#ABI)).

#### G.2.4 Compatible Architecture

This optional field was introduced in [GDB] ignore it.

A '`<compatible>`' element has this form:

::: smallexample

```bash
  <compatible>arch</compatible>
```

:::

`arch` is one of the architectures from the set accepted by `set architecture` (see [Specifying a Debugging Target](Targets.html#Targets)).

A '`<compatible>`' is as follows:

::: smallexample

```bash
  <architecture>powerpc:common</architecture>
  <compatible>spu</compatible>
```

:::

#### G.2.5 Features

Each '`<feature>`' element has this form:

::: smallexample

```bash
<feature name="name">
  [type…]
  reg…
</feature>
```

:::


Each feature's name should be unique within the description. The name of a feature does not matter unless [GDB] has some special knowledge of the contents of that feature; if it does, the feature should have its standard name. See [Standard Target Features](Standard-Target-Features.html#Standard-Target-Features).

> 每个特征的名称应该在描述中是唯一的。特征的名称并不重要，除非GDB对该特征的内容有特殊的了解；如果有，该特征应具有其标准名称。请参见[标准目标特征](Standard-Target-Features.html#Standard-Target-Features)。

#### G.2.6 Types


Any register's value is a collection of bits which [GDB] (see [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)), and the description can define additional composite and enum types.

> 任何寄存器的值都是[GDB](参见[预定义目标类型](Predefined-Target-Types.html#Predefined-Target-Types))的一组位，描述可以定义额外的复合类型和枚举类型。


Each type element must have an '`id`') name to the type. Types must be defined before they are used.

> 每个类型元素必须有一个'id'名称。类型必须在使用之前定义。


Some targets offer vector registers, which can be treated as arrays of scalar elements. These types are written as '`<vector>`:

> 一些目标提供向量寄存器，可以视为标量元素的数组。这些类型被写为'<vector>':

::: smallexample

```bash
<vector id="id" type="type" count="count"/>
```

:::


If a register's value is usefully viewed in multiple ways, define it with a union type containing the useful representations. The '`<union>`:

> 如果一个寄存器的值可以以多种有用的方式查看，请使用包含有用表示的联合类型来定义它。 '<union>'：

::: smallexample

```bash
<union id="id">
  <field name="name" type="type"/>
  …
</union>
```

:::


If a register's value is composed from several separate values, define it with either a structure type or a flags type. A flags type may only contain bitfields. A structure type may either contain only bitfields or contain no bitfields. If the value contains only bitfields, its total size in bytes must be specified.

> 如果寄存器的值由几个单独的值组成，可以使用结构类型或标志类型来定义它。标志类型只能包含位域。结构类型可以只包含位域，也可以不包含位域。如果值只包含位域，则必须指定它的总大小（以字节为单位）。

Non-bitfield values have a `name`.

::: smallexample

```bash
<struct id="id">
  <field name="name" type="type"/>
  …
</struct>
```

:::

Both `name` values are required. No implicit padding is added.

Bitfield values have a `name`.

::: smallexample

```bash
<struct id="id" size="size">
  <field name="name" start="start" end="end" type="type"/>
  …
</struct>
```

:::

::: smallexample

```bash
<flags id="id" size="size">
  <field name="name" start="start" end="end" type="type"/>
  …
</flags>
```

:::


The `name`', in which case the field is "filler" and its value is not printed. Not all bits need to be specified, so "filler" fields are optional.

> 这个名称（填充字段），其值不会被打印出来，不是所有的位都需要被指定，因此这个填充字段是可选的。

The `start`, and zero represents the least significant bit.


The default value of `type` is `bool` for single bit fields, and an unsigned integer otherwise.

> 默认值为单位比特字段的`type`是`bool`，其他情况为无符号整数。

Which to choose? Structures or flags?

Registers defined with '`flags`':

- Arithmetic may be performed on them as if they were integers.
- They are printed in a more readable fashion.

Registers defined with '`struct`':

- One can fetch individual fields like in '`C`'.

  ::: smallexample

  ```bash
  (gdb) print $my_struct_reg.field3
  $1 = 42
  ```

  :::

#### G.2.7 Registers

Each register is represented as an element with this form:

::: smallexample

```bash
<reg name="name"
     bitsize="size"
     [regnum="num"]
     [save-restore="save-restore"]
     [type="type"]
     [group="group"]/>
```

:::

The components are as follows:

`name`

:   The register's name; it must be unique within the target description.

`bitsize`

:   The register's size, in bits.

`regnum`


:   The register's number. If omitted, a register's number is one greater than that of the previous register (either in the current feature or in a preceding feature); the first register in the target description defaults to zero. This register number is used to read or write the register; e.g. it is used in the remote `p` and `P` packets, and registers appear in the `g` and `G` packets in order of increasing register number.

> 注册号。如果省略，则注册号比当前功能或前一个功能中的前一个注册号大1；目标描述中的第一个注册号默认为零。此注册号用于读取或写入寄存器；例如，它用于远程`p`和`P`数据包，并且寄存器按照增加的寄存器号出现在`g`和`G`数据包中。

`save-restore`


:   Whether the register should be preserved across inferior function calls; this must be either `yes` or `no`. The default is `yes`, which is appropriate for most registers except for some system control registers; this is not related to the target's ABI.

> 是否应该在次级函数调用中保留寄存器；必须是`yes`或`no`。默认是`yes`，这适用于大多数寄存器，但不适用于某些系统控制寄存器；这与目标的ABI无关。

`type`


:   The type of the register. It may be a predefined type, a type defined in the current feature, or one of the special types `int` and `float`. `int` is an integer type of the correct size for `bitsize`. The default is `int`.

> 注册的类型。它可以是预定义类型、当前特征定义的类型，或特殊类型`int`和`float`之一。`int`是与`bitsize`相匹配的整数类型。默认值为`int`。

`group`


:   The register group to which this register belongs. It can be one of the standard register groups `general`, `float`, `vector` or an arbitrary string. Group names should be limited to alphanumeric characters. If a group name is made up of multiple words the words may be separated by hyphens; e.g. `special-group` or `ultra-special-group`. If no `group` will not display the register in `info registers`.

> 这个寄存器属于哪个注册组。它可以是标准注册组`general`、`float`、`vector`之一，也可以是任意字符串。组名应该仅限于字母数字字符。如果组名由多个单词组成，可以用连字符分隔，例如`special-group`或`ultra-special-group`。如果没有`group`，将不会在`info registers`中显示该寄存器。

---

::: header
Next: [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)]
:::
