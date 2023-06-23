---
tip: translate by openai@2023-06-23 14:19:09
...
---
description: Target Description Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Target Description Format (Debugging with GDB)
lang: en
resource-type: document
title: Target Description Format (Debugging with GDB)
-----------------------------------------------------

::: header
Next: [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)]
:::

---

### G.2 Target Description Format

A target description annex is an [XML](http://www.w3.org/XML/) document which complies with the Document Type Definition provided in the [GDB]. This means you can use generally available tools like `xmllint` to check that your feature descriptions are well-formed and valid. However, to help people unfamiliar with XML write descriptions for their targets, we also describe the grammar here.

> 附件描述是一个符合[GDB]中提供的文档类型定义的 [XML](http://www.w3.org/XML/) 文档。这意味着您可以使用通用的工具，如 `xmllint` 来检查您的功能描述是否完整有效。但是，为了帮助不熟悉 XML 的人编写目标描述，我们这里还描述了语法。

Target descriptions can identify the architecture of the remote target and (for some architectures) provide information about custom register sets. They can also identify the OS ABI of the remote target. [GDB] can use this information to autoconfigure for your target, or to warn you if you connect to an unsupported target.

> 目标描述可以识别远程目标的体系结构，并（对于某些体系结构）提供有关自定义寄存器集的信息。它们还可以识别远程目标的 OS ABI。[GDB]可以使用此信息来自动配置您的目标，或者如果您连接到不受支持的目标时发出警告。

Here is a simple target description:

> 这里有一个简单的目标描述：

::: smallexample

```bash
<target version="1.0">
  <architecture>i386:x86-64</architecture>
</target>
```

:::

This minimal description only says that the target uses the x86-64 architecture.

> 这个最小描述只说明目标使用 x86-64 架构。

A target description has the following overall form, with \[ ] marking optional elements and ... marking repeatable elements. The elements are explained further below.

> 目标描述的总体形式如下，\[ ] 标记可选元素，... 标记可重复元素，下面将对元素进行进一步解释。

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

> 描述通常对空格和换行不敏感，根据通常的常识规则。XML 版本声明和文档类型声明通常可以省略([GDB]，它们将检测并报告版本不匹配。

#### G.2.1 Inclusion

It can sometimes be valuable to split a target description up into several different annexes, either for organizational purposes, or to share files between different possible target descriptions. You can divide a description into multiple files by replacing any element of the target description with an inclusion directive of the form:

> 有时将目标描述分成几个附件可能是有价值的，无论是出于组织目的，还是为了在不同可能的目标描述之间共享文件。您可以通过使用以下形式的包含指令来将描述分成多个文件：

::: smallexample

```bash
<xi:include href="document"/>
```

:::

When [GDB] as a file in the same directory where it found the original description.

> 当 GDB 在同一目录中找到原始描述时，将其作为文件。

#### G.2.2 Architecture

An '`<architecture>`' element has this form:

> 一个'<architecture>'元素具有以下形式：

::: smallexample

```bash
  <architecture>arch</architecture>
```

:::

`arch` is one of the architectures from the set accepted by `set architecture` (see [Specifying a Debugging Target](Targets.html#Targets)).

#### G.2.3 OS ABI

This optional field was introduced in [GDB] ignore it.

> 这个可选字段是在[GDB]中引入的，忽略它。

An '`<osabi>`' element has this form:

> 一个'<osabi>'元素的形式是：

::: smallexample

```bash
  <osabi>abi-name</osabi>
```

:::

`abi-name` is an OS ABI name from the same selection accepted by `set osabi` (see [Configuring the Current ABI](ABI.html#ABI)).

#### G.2.4 Compatible Architecture

This optional field was introduced in [GDB] ignore it.

> 这个可选字段是在[GDB]中引入的，忽略它。

A '`<compatible>`' element has this form:

> 一个“兼容”元素的形式如下：

::: smallexample

```bash
  <compatible>arch</compatible>
```

:::

`arch` is one of the architectures from the set accepted by `set architecture` (see [Specifying a Debugging Target](Targets.html#Targets)).

A '`<compatible>`' is as follows:

> 一个'< 兼容 >'如下：

::: smallexample

```bash
  <architecture>powerpc:common</architecture>
  <compatible>spu</compatible>
```

:::

#### G.2.5 Features

Each '`<feature>`' element has this form:

> 每个'<feature>'元素都有这种形式：

::: smallexample

```bash
<feature name="name">
  [type…]
  reg…
</feature>
```

:::

Each feature's name should be unique within the description. The name of a feature does not matter unless [GDB] has some special knowledge of the contents of that feature; if it does, the feature should have its standard name. See [Standard Target Features](Standard-Target-Features.html#Standard-Target-Features).

> 每个特性的名称应该在描述中是唯一的。特征的名称并不重要，除非[GDB]对该特性的内容有特殊的了解；如果有，该特性应该有其标准名称。参见[标准目标特性](Standard-Target-Features.html#Standard-Target-Features)。

#### G.2.6 Types

Any register's value is a collection of bits which [GDB] (see [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)), and the description can define additional composite and enum types.

> 任何寄存器的值都是 GDB 所看到的预定义目标类型（参见预定义目标类型）的位集合，描述可以定义额外的复合类型和枚举类型。

Each type element must have an '`id`') name to the type. Types must be defined before they are used.

> 每种类型的元素必须有一个'id'名称。类型必须在使用前定义。

Some targets offer vector registers, which can be treated as arrays of scalar elements. These types are written as '`<vector>`:

> 一些目标提供向量寄存器，可以被当作标量元素的数组。这些类型被写作'< 向量 >':

::: smallexample

```bash
<vector id="id" type="type" count="count"/>
```

:::

If a register's value is usefully viewed in multiple ways, define it with a union type containing the useful representations. The '`<union>`:

> 如果寄存器的值有多种有用的视图，请使用包含有用表示的联合类型定义它。 '<union>':

::: smallexample

```bash
<union id="id">
  <field name="name" type="type"/>
  …
</union>
```

:::

If a register's value is composed from several separate values, define it with either a structure type or a flags type. A flags type may only contain bitfields. A structure type may either contain only bitfields or contain no bitfields. If the value contains only bitfields, its total size in bytes must be specified.

> 如果寄存器的值由几个独立的值组成，可以使用结构类型或标志类型来定义。标志类型只能包含位域。结构类型可以只包含位域，也可以不包含位域。如果值仅包含位域，则必须指定其总字节数。

Non-bitfield values have a `name`.

> 非位域值具有一个名称。

::: smallexample

```bash
<struct id="id">
  <field name="name" type="type"/>
  …
</struct>
```

:::

Both `name` values are required. No implicit padding is added.

> 两个 `name` 值都是必需的。不会添加隐式填充。

Bitfield values have a `name`.

> 位域值有一个名称。

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

> 这个名字（填充），其值不会被打印。不是所有的位都需要指定，因此“填充”字段是可选的。

The `start`, and zero represents the least significant bit.

> 开始，零代表最不重要的位。

The default value of `type` is `bool` for single bit fields, and an unsigned integer otherwise.

> 默认情况下，单位位字段的 `type` 的值为 `bool`，其他情况下为无符号整数。

Which to choose? Structures or flags?

> 哪个选择？结构还是旗帜？

Registers defined with '`flags`':

> 注册定义为'标志'：

- Arithmetic may be performed on them as if they were integers.
- They are printed in a more readable fashion.

Registers defined with '`struct`':

> 定义为“struct”的寄存器

- One can fetch individual fields like in '`C`'.

  ::: smallexample

  ```bash
  (gdb) print $my_struct_reg.field3
  $1 = 42
  ```

  :::

#### G.2.7 Registers

Each register is represented as an element with this form:

> 每个寄存器都用这种形式表示：

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

> 以下是组件：

`name`

:   The register's name; it must be unique within the target description.

> 注册器的名称；它必须在目标描述中是唯一的。

`bitsize`

:   The register's size, in bits.

> 寄存器大小，以位为单位。

`regnum`

:   The register's number. If omitted, a register's number is one greater than that of the previous register (either in the current feature or in a preceding feature); the first register in the target description defaults to zero. This register number is used to read or write the register; e.g. it is used in the remote `p` and `P` packets, and registers appear in the `g` and `G` packets in order of increasing register number.

> 如果省略，寄存器号码比前一个寄存器（当前特性或前面特性中的）大 1；在目标描述中，第一个寄存器的默认值为零。此寄存器号码用于读取或写入寄存器；例如，它用于远程‘p’和‘P’数据包中，并且寄存器按照增加的寄存器号码出现在‘g’和‘G’数据包中。

`save-restore`

:   Whether the register should be preserved across inferior function calls; this must be either `yes` or `no`. The default is `yes`, which is appropriate for most registers except for some system control registers; this is not related to the target's ABI.

> 是否应该在次级函数调用中保留寄存器; 这必须是 `是` 或 `否`。 默认值为 `是`，适用于大多数寄存器，但不适用于某些系统控制寄存器; 这与目标的 ABI 无关。

`type`

:   The type of the register. It may be a predefined type, a type defined in the current feature, or one of the special types `int` and `float`. `int` is an integer type of the correct size for `bitsize`. The default is `int`.

> 注册的类型。它可以是预定义的类型，在当前特征中定义的类型，或者是特殊类型 `int` 和 `float` 之一。`int` 是与 `bitsize` 相匹配的整数类型。默认为 `int`。

`group`

:   The register group to which this register belongs. It can be one of the standard register groups `general`, `float`, `vector` or an arbitrary string. Group names should be limited to alphanumeric characters. If a group name is made up of multiple words the words may be separated by hyphens; e.g. `special-group` or `ultra-special-group`. If no `group` will not display the register in `info registers`.

> 此寄存器所属的寄存器组。它可以是标准寄存器组 `general`、`float`、`vector` 之一，也可以是任意字符串。组名应限制为字母数字字符。如果组名由多个单词组成，则可以使用连字符分隔单词，例如 `special-group` 或 `ultra-special-group`。如果没有 `group`，则不会在 `info registers` 中显示该寄存器。

---

::: header
Next: [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)]
:::
