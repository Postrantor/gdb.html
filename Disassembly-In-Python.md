---
tip: translate by openai@2023-06-23 20:35:46
...
---
description: Disassembly In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Disassembly In Python (Debugging with GDB)
lang: en
resource-type: document
title: Disassembly In Python (Debugging with GDB)
---
::: header
Previous: [TUI Windows In Python](TUI-Windows-In-Python.html#TUI-Windows-In-Python)]
:::

---

#### 23.3.2.38 Instruction Disassembly In Python


[GDB]'s builtin disassembler can be extended, or even replaced, using the Python API. The disassembler related features are contained within the `gdb.disassembler` module:

> GDB的内置反汇编器可以使用Python API进行扩展甚至替换。反汇编相关功能包含在`gdb.disassembler`模块中：

class: **gdb.disassembler.DisassembleInfo**


:   Disassembly is driven by instances of this class. Each time [GDB] needs to disassemble an instruction, an instance of this class is created and passed to a registered disassembler. The disassembler is then responsible for disassembling an instruction and returning a result.

> 拆解由此类的实例驱动。每次[GDB]需要拆解指令时，都会创建一个此类的实例，并将其传递给注册的拆解器。然后，拆解器负责拆解指令并返回结果。

```
Instances of this type are usually created within [GDB], however, it is possible to create a copy of an instance of this type, see the description of `__init__` for more details.

This class has the following properties and methods:

Variable: **DisassembleInfo.address**

:   A read-only integer containing the address at which [GDB] wishes to disassemble a single instruction.

Variable: **DisassembleInfo.architecture**

:   The `gdb.Architecture` (see [Architectures In Python](Architectures-In-Python.html#Architectures-In-Python)) for which [GDB] is currently disassembling, this property is read-only.

Variable: **DisassembleInfo.progspace**

:   The `gdb.Progspace` (see [Program Spaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)) for which [GDB] is currently disassembling, this property is read-only.

Function: **DisassembleInfo.is_valid** *()*

:   Returns `True` if the `DisassembleInfo` object is valid, `False` if not. A `DisassembleInfo` object will become invalid once the disassembly call for which the `DisassembleInfo` was created, has returned. Calling other `DisassembleInfo` methods, or accessing `DisassembleInfo` properties, will raise a `RuntimeError` exception if it is invalid.

Function: **DisassembleInfo.__init__** *(info)*

:   This can be used to create a new `DisassembleInfo` object that is a copy of `info`.

    This method exists so that sub-classes of `DisassembleInfo` can be created, these sub-classes must be initialized as copies of an existing `DisassembleInfo` object, but sub-classes might choose to override the `read_memory` method, and so control what [GDB] sees when reading from memory (see [builtin_disassemble](#builtin_005fdisassemble)).

Function: **DisassembleInfo.read_memory** *(length, offset)*

:   This method allows the disassembler to read the bytes of the instruction to be disassembled. The method reads `length` from `DisassembleInfo.address`.

    It is important that the disassembler read the instruction bytes using this method, rather than reading inferior memory directly, as in some cases [GDB] disassembles from an internal buffer rather than directly from inferior memory, calling this method handles this detail.

    Returns a buffer object, which behaves much like an array or a string, just as `Inferior.read_memory` does (see [Inferior.read_memory](Inferiors-In-Python.html#gdbpy_005finferior_005fread_005fmemory)). The length of the returned buffer will always be exactly `length`.

    If [GDB] is unable to read the required memory then a `gdb.MemoryError` exception is raised (see [Exception Handling](Exception-Handling.html#Exception-Handling)).

    This method can be overridden by a sub-class in order to control what [GDB] sees when reading from memory (see [builtin_disassemble](#builtin_005fdisassemble)). When overriding this method it is important to understand how `builtin_disassemble` makes use of this method.

    While disassembling a single instruction there could be multiple calls to this method, and the same bytes might be read multiple times. Any single call might only read a subset of the total instruction bytes.

    If an implementation of `read_memory` is unable to read the requested memory contents, for example, if there's a request to read from an invalid memory address, then a `gdb.MemoryError` should be raised.

    Raising a `MemoryError` inside `read_memory` does not automatically mean a `MemoryError` will be raised by `builtin_disassemble`. It is possible the [GDB]'s builtin disassembler is probing to see how many bytes are available. When `read_memory` raises the `MemoryError` the builtin disassembler might be able to perform a complete disassembly with the bytes it has available, in this case `builtin_disassemble` will not itself raise a `MemoryError`.

    Any other exception type raised in `read_memory` will propagate back and be re-raised by `builtin_disassemble`.

Function: **DisassembleInfo.text_part** *(style, string)*

:   Create a new `DisassemblerTextPart` representing a piece of a disassembled instruction. `string` should be an appropriate style constant (see [Disassembler Style Constants](#Disassembler-Style-Constants)).

    Disassembler parts are used when creating a `DisassemblerResult` in order to represent the styling within an instruction (see [DisassemblerResult Class](#DisassemblerResult-Class)).

Function: **DisassembleInfo.address_part** *(address)*

:   Create a new `DisassemblerAddressPart`. `address` is the value of the absolute address this part represents. A `DisassemblerAddressPart` is displayed as an absolute address and an associated symbol, the address and symbol are styled appropriately.
```

class: **gdb.disassembler.Disassembler**


:   This is a base class from which all user implemented disassemblers must inherit.

> 这是一个基类，所有用户实现的反汇编器必须从中继承。

```
Function: **Disassembler.__init__** *(name)*

:   The constructor takes `name`, a string, which should be a short name for this disassembler.

Function: **Disassembler.__call__** *(info)*

:   The `__call__` method must be overridden by sub-classes to perform disassembly. Calling `__call__` on this base class will raise a `NotImplementedError` exception.

    The `info` wants disassembling.

    If this function returns `None`, this indicates to [GDB] will then use its builtin disassembler to perform the disassembly.

    Alternatively, this function can return a `DisassemblerResult` that represents the disassembled instruction, this type is described in more detail below.

    The `__call__` method can raise a `gdb.MemoryError` exception (see [Exception Handling](Exception-Handling.html#Exception-Handling)) to indicate to [GDB] within the disassembler output.

    Ideally, the only three outcomes from invoking `__call__` would be a return of `None`, a successful disassembly returned in a `DisassemblerResult`, or a `MemoryError` indicating that there was a problem reading memory.

    However, as an implementation of `__call__` could fail due to other reasons, e.g. some external resource required to perform disassembly is temporarily unavailable, then, if `__call__` raises a `GdbError`, the exception will be converted to a string and printed at the end of the disassembly output, the disassembly request will then stop.

    Any other exception type raised by the `__call__` method is considered an error in the user code, the exception will be printed to the error stream according to the [set python print-stack]](Python-Commands.html#set_005fpython_005fprint_005fstack)).
```

class: **gdb.disassembler.DisassemblerResult**


:   This class represents the result of disassembling a single instruction. An instance of this class will be returned from `builtin_disassemble` (see [builtin_disassemble](#builtin_005fdisassemble)), and an instance of this class should be returned from `Disassembler.__call__` (see [Disassembler Class](#Disassembler-Class)) if an instruction was successfully disassembled.

> 这个类代表着单个指令拆解的结果。从`builtin_disassemble`（参见[builtin_disassemble]（#builtin_005fdisassemble））返回的实例，以及从`Disassembler.__call__`（参见[Disassembler Class]（#Disassembler-Class））返回的实例，如果指令被成功拆解，应该返回这个类的实例。

```
It is not possible to sub-class the `DisassemblerResult` class.

The `DisassemblerResult` class has the following properties and methods:

Function: **DisassemblerResult.__init__** *(length, string, parts)*

:   Initialize an instance of this class, `length` is the length of the disassembled instruction in bytes, which must be greater than zero.

    Only one of `string` should be used to initialize a new `DisassemblerResult`; the other one should be passed the value `None`. Alternatively, the arguments can be passed by name, and the unused argument can be ignored.

    The `string` will style the result as a single `DisassemblerTextPart` with `STYLE_TEXT` style (see [Disassembler Styling Parts](#Disassembler-Styling-Parts)).

    The `parts`](Output-Styling.html#style_005fdisassembler_005fenabled)).

Variable: **DisassemblerResult.length**

:   A read-only property containing the length of the disassembled instruction in bytes, this will always be greater than zero.

Variable: **DisassemblerResult.string**

:   A read-only property containing a non-empty string representing the disassembled instruction. The `string` property.

    If this instance was initialized using separate `DisassemblerPart` objects, the `string` value is created by concatenating the `DisassemblerPart.string` values of each component part (see [Disassembler Styling Parts](#Disassembler-Styling-Parts)).

Variable: **DisassemblerResult.parts**

:   A read-only property containing a non-empty sequence of `DisassemblerPart` objects. Each `DisassemblerPart` object contains a small part of the instruction along with information about how that part should be styled. [GDB]](Output-Styling.html#style_005fdisassembler_005fenabled)).

    If this instance was initialized using a single string rather than with a sequence of `DisassemblerPart` objects, the `parts` property will hold a sequence containing a single `DisassemblerTextPart` object, the string of which will represent the entire instruction, and the style of which will be `STYLE_TEXT`.
```

class: **gdb.disassembler.DisassemblerPart**


:   This is a parent class from which the different part sub-classes inherit. Only instances of the sub-classes detailed below will be returned by the Python API.

> 这是一个父类，不同的子类从中继承。只有下面详细描述的子类的实例才能由Python API返回。

```
It is not possible to directly create instances of either this parent class, or any of the sub-classes listed below. Instances of the sub-classes listed below are created by calling `builtin_disassemble` (see [builtin_disassemble](#builtin_005fdisassemble)) and are returned within the `DisassemblerResult` object, or can be created by calling the `text_part` and `address_part` methods on the `DisassembleInfo` class (see [DisassembleInfo Class](#DisassembleInfo-Class)).

The `DisassemblerPart` class has a single property:

Variable: **DisassemblerPart.string**

:   A read-only property that contains a non-empty string representing this part of the disassembled instruction. The string within this property doesn't include any styling information.
```

```
<!-- -->
```

class: **gdb.disassembler.DisassemblerTextPart**


:   The `DisassemblerTextPart` class represents a piece of the disassembled instruction and the associated style for that piece. Instances of this class can't be created directly, instead call `DisassembleInfo.text_part` to create a new instance of this class (see [DisassembleInfo Class](#DisassembleInfo-Class)).

> 类`DisassemblerTextPart`表示被反汇编指令的一部分及其相关样式。不能直接创建此类的实例，而是调用`DisassembleInfo.text_part`来创建此类的新实例（参见[DisassembleInfo类](#DisassembleInfo-Class)）。

```
As well as the properties of its parent class, the `DisassemblerTextPart` has the following additional property:

Variable: **DisassemblerTextPart.style**

:   A read-only property that contains one of the defined style constants. [GDB] will use this style when styling this part of the disassembled instruction (see [Disassembler Style Constants](#Disassembler-Style-Constants)).
```

```
<!-- -->
```

class: **gdb.disassembler.DisassemblerAddressPart**


:   The `DisassemblerAddressPart` class represents an absolute address within a disassembled instruction. Using a `DisassemblerAddressPart` instead of a `DisassemblerTextPart` with `STYLE_ADDRESS` is preferred, [GDB] will display the address as both an absolute address, and will look up a suitable symbol to display next to the address. Using `DisassemblerAddressPart` also ensures that user settings such as `set print max-symbolic-offset` are respected.

> `DisassemblerAddressPart`类表示解析指令中的绝对地址。使用`DisassemblerAddressPart`而不是具有`STYLE_ADDRESS`的`DisassemblerTextPart`更可取，[GDB]将显示该地址作为绝对地址，并将查找适当的符号显示在地址旁边。使用`DisassemblerAddressPart`还可以确保用户设置（如`set print max-symbolic-offset`）得到尊重。

```
Here is an example of an x86-64 instruction:

::: smallexample
``` smallexample
call   0x401136 <foo>
```

:::

In this instruction the `0x401136 <foo>` was generated from a single `DisassemblerAddressPart`. The `0x401136` will be styled with `STYLE_ADDRESS`, and `foo` will be styled with `STYLE_SYMBOL`. The `<` and `>` will be styled as `STYLE_TEXT`.

If the inclusion of the symbol name is not required then a `DisassemblerTextPart` with style `STYLE_ADDRESS` can be used instead.

Instances of this class can't be created directly, instead call `DisassembleInfo.address_part` to create a new instance of this class (see [DisassembleInfo Class](#DisassembleInfo-Class)).

As well as the properties of its parent class, the `DisassemblerAddressPart` has the following additional property:

Variable: **DisassemblerAddressPart.address**

:   A read-only property that contains the `address` passed to this object's `__init__` method.

```




The following table lists all of the disassembler styles that are available. [GDB].

> 以下表格列出所有可用的反汇编器样式[GDB]。



`gdb.disassembler.STYLE_TEXT` 


This is the default style used by [GDB] styles text with this style using its default style.

> 这是GDB默认使用的样式，使用它的默认样式对文本进行样式化。



`gdb.disassembler.STYLE_MNEMONIC` 


This style is used for styling the primary instruction mnemonic, which usually appears at, or near, the start of the disassembled instruction string.

> 这种样式用于为首要指令助记符进行样式化，通常出现在反汇编指令字符串的开头或附近。


[GDB] styles text with this style using the `disassembler mnemonic` style setting.

> GDB使用`汇编指令`样式设置来对文本进行样式渲染。



`gdb.disassembler.STYLE_SUB_MNEMONIC` 


This style is used for styling any sub-mnemonics within a disassembled instruction. A sub-mnemonic is any text within the instruction that controls the function of the instruction, but which is disjoint from the primary mnemonic (which will have styled `STYLE_MNEMONIC`).

> 这种样式用于样式化拆解指令中的任何子助记符。子助记符是指令中控制指令功能的任何文本，但与主助记符（将具有样式“STYLE_MNEMONIC”）不相关。

As an example, consider this AArch64 instruction:

::: smallexample

```bash
add   w16, w7, w1, lsl #1
```

:::


The `add` is the primary instruction mnemonic, and would be given style `STYLE_MNEMONIC`, while `lsl` is the sub-mnemonic, and would be given the style `STYLE_SUB_MNEMONIC`.

> `add`是主指令助记符，应使用`STYLE_MNEMONIC`样式，而`lsl`是子助记符，应使用`STYLE_SUB_MNEMONIC`样式。


[GDB] styles text with this style using the `disassembler mnemonic` style setting.

> GDB使用`反汇编指令`样式设置来对文本进行样式化。

`gdb.disassembler.STYLE_ASSEMBLER_DIRECTIVE`


Sometimes a series of bytes doesn't decode to a valid instruction. In this case the disassembler may choose to represent the result of disassembling using an assembler directive, for example:

> 有时，一系列字节无法解码为有效指令。在这种情况下，反汇编器可能会选择使用汇编器指令来表示反汇编的结果，例如：

::: smallexample

```bash
.word 0x1234
```

:::


In this case, the `.word` would be give the `STYLE_ASSEMBLER_DIRECTIVE` style. An assembler directive is similar to a mnemonic in many ways but is something that is not part of the architecture's instruction set.

> 在这种情况下，`.word`将被指定`STYLE_ASSEMBLER_DIRECTIVE`样式。组合指令在许多方面与操作码类似，但不属于架构的指令集。


[GDB] styles text with this style using the `disassembler mnemonic` style setting.

> 使用`反汇编指令`样式设置，GDB用这种样式格式化文本。

`gdb.disassembler.STYLE_REGISTER`


This style is used for styling any text that represents a register name, or register number, within a disassembled instruction.

> 这种样式用于为解析指令中表示寄存器名称或寄存器号的任何文本进行样式化。


[GDB] styles text with this style using the `disassembler register` style setting.

> 使用`反汇编寄存器`样式设置，GDB用这种样式格式化文本。

`gdb.disassembler.STYLE_ADDRESS`


This style is used for styling numerical values that represent absolute addresses within the disassembled instruction.

> 这种样式用于样式化表示拆解指令中的绝对地址的数值。


When creating a `DisassemblerTextPart` with this style, you should consider if a `DisassemblerAddressPart` would be more appropriate. See [Disassembler Styling Parts](#Disassembler-Styling-Parts) for a description of what each part offers.

> 当使用这种样式创建一个`DisassemblerTextPart`时，您应该考虑是否`DisassemblerAddressPart`更合适。有关每个部分提供的内容的描述，请参阅[Disassembler Styling Parts](#Disassembler-Styling-Parts)。


[GDB] styles text with this style using the `disassembler address` style setting.

> 使用`反汇编地址`样式设置，[GDB]使用这种样式来格式化文本。

`gdb.disassembler.STYLE_ADDRESS_OFFSET`


This style is used for styling numerical values that represent offsets to addresses within the disassembled instruction. A value is considered an address offset when the instruction itself is going to access memory, and the value is being used to offset which address is accessed.

> 这种样式用于为解析指令中的地址偏移量进行样式化。当指令本身要访问内存时，将值视为地址偏移量，并使用值偏移要访问的地址。


For example, an architecture might have an instruction that loads from memory using an address within a register. If that instruction also allowed for an immediate offset to be encoded into the instruction, this would be an address offset. Similarly, a branch instruction might jump to an address in a register plus an address offset that is encoded into the instruction.

> 例如，架构可能有一条指令使用寄存器中的地址从内存中加载。如果该指令还允许将立即偏移量编码到指令中，则这将是一个地址偏移量。类似地，分支指令可能会跳转到寄存器中的地址加上指令中编码的地址偏移量。


[GDB] styles text with this style using the `disassembler immediate` style setting.

> GDB使用`disassembler immediate`样式设置来对文本进行样式化。

`gdb.disassembler.STYLE_IMMEDIATE`


Use `STYLE_IMMEDIATE` for any numerical values within a disassembled instruction when those values are not addresses, address offsets, or register numbers (The styles `STYLE_ADDRESS`, `STYLE_ADDRESS_OFFSET`, or `STYLE_REGISTER` can be used in those cases).

> 使用`STYLE_IMMEDIATE`来标记解析指令中的任何数值，如果这些数值不是地址、地址偏移量或寄存器编号（在这些情况下可以使用`STYLE_ADDRESS`、`STYLE_ADDRESS_OFFSET`或`STYLE_REGISTER`样式）。


[GDB] styles text with this style using the `disassembler immediate` style setting.

> [GDB] 使用 `disassembler immediate` 样式设置来给文本添加此样式。

`gdb.disassembler.STYLE_SYMBOL`


This style is used for styling the textual name of a symbol that is included within a disassembled instruction. A symbol name is often included next to an absolute address within a disassembled instruction to make it easier for the user to understand what the address is referring too. For example:

> 这种样式用于对反汇编指令中包含的符号的文本名称进行样式化。符号名称通常附加在反汇编指令的绝对地址旁边，以便用户更容易理解地址指的是什么。例如：

::: smallexample

```bash
call   0x401136 <foo>
```

:::


Here `foo` is the name of a symbol, and should be given the `STYLE_SYMBOL` style.

> 这里，`foo`是一个符号的名称，应该给予`STYLE_SYMBOL`样式。


Adding symbols next to absolute addresses like this is handled automatically by the `DisassemblerAddressPart` class (see [Disassembler Styling Parts](#Disassembler-Styling-Parts)).

> 加入符号到绝对地址旁边，像这样，可以由`DisassemblerAddressPart`类自动处理（参见[反汇编样式部件]（#Disassembler-Styling-Parts））。


[GDB] styles text with this style using the `disassembler symbol` style setting.

> 使用`disassembler symbol`样式设置，GDB用这种样式格式化文本。

`gdb.disassembler.STYLE_COMMENT_START`


This style is used to start a line comment in the disassembly output. Unlike other styles, which only apply to the single `DisassemblerTextPiece` to which they are applied, the comment style is sticky, and overrides the style of any further pieces within this instruction.

> 这种样式用于在反汇编输出中开始一行注释。与其他样式不同，它们只适用于应用了它们的单个`DisassemblerTextPiece`，注释样式是粘性的，并覆盖此指令中的任何进一步片段的样式。


This means that, after a `STYLE_COMMENT_START` piece has been seen, [GDB] will apply the comment style until the end of the line, ignoring the specific style within a piece.

> 这意味着，在看到一个`STYLE_COMMENT_START`片段之后，[GDB]会在行尾应用注释样式，忽略片段内的特定样式。


[GDB] styles text with this style using the `disassembler comment` style setting.

> GDB使用“反汇编注释”样式设置来对文本进行样式化。


The following functions are also contained in the `gdb.disassembler` module:

> 以下功能也包含在`gdb.disassembler`模块中：

Function: **register_disassembler** *(disassembler, architecture)*


:   The `disassembler` must be a sub-class of `gdb.disassembler.Disassembler` or `None`.

> 解码器必须是gdb.disassembler.Disassembler的子类或者为None。

```
The optional `architecture`, as returned either from `gdb.Architecture.name` (see [gdb.Architecture.name](Architectures-In-Python.html#gdbpy_005farchitecture_005fname)), or from `gdb.architecture_names` (see [gdb.architecture_names](Basic-Python.html#gdb_005farchitecture_005fnames)).

The `disassembler` will be installed as a global disassembler for use by all architectures.



[GDB] value. The previous disassembler is returned.

If `disassembler` is deregistered and returned.

When [GDB] set to `None`). Only one disassembler is called to perform disassembly, so, if there is both an architecture specific disassembler, and a global disassembler registered, it is the architecture specific disassembler that will be used.

[GDB] tracks the architecture specific, and global disassemblers separately, so it doesn't matter in which order disassemblers are created or registered; an architecture specific disassembler, if present, will always be used in preference to a global disassembler.

You can use the [maint info python-disassemblers] command (see [maint info python-disassemblers](Maintenance-Commands.html#maint-info-python_002ddisassemblers)) to see which disassemblers have been registered.
```

Function: **builtin_disassemble** *(info)*


:   This function calls back into [GDB], an instance, or sub-class, of `DisassembleInfo`.

> 这个函数回调[GDB]，一个`DisassembleInfo`的实例或子类。

```
When the builtin disassembler needs to read memory the `read_memory` method on `info` will be called. By sub-classing `DisassembleInfo` and overriding the `read_memory` method, it is possible to intercept calls to `read_memory` from the builtin disassembler, and to modify the values returned.

It is important to understand that, even when `DisassembleInfo.read_memory` raises a `gdb.MemoryError`, it is the internal disassembler itself that reports the memory error to [GDB]. The reason for this is that the disassembler might probe memory to see if a byte is readable or not; if the byte can't be read then the disassembler may choose not to report an error, but instead to disassemble the bytes that it does have available.

If the builtin disassembler is successful then an instance of `DisassemblerResult` is returned from `builtin_disassemble`, alternatively, if something goes wrong, an exception will be raised.

A `MemoryError` will be raised if `builtin_disassemble` is unable to read some memory that is required in order to perform disassembly correctly.

Any exception that is not a `MemoryError`, that is raised in a call to `read_memory`, will pass through `builtin_disassemble`, and be visible to the caller.

Finally, there are a few cases where [GDB]'s builtin disassembler can fail for reasons that are not covered by `MemoryError`. In these cases, a `GdbError` will be raised. The contents of the exception will be a string describing the problem the disassembler encountered.
```


Here is an example that registers a global disassembler. The new disassembler invokes the builtin disassembler, and then adds a comment, `## Comment`, to each line of disassembly output:

> 这里有一个注册全局反汇编器的例子。新的反汇编器会调用内置反汇编器，并在每一行反汇编输出后添加注释 `## Comment`。

::: smallexample

```bash
class ExampleDisassembler(gdb.disassembler.Disassembler):
    def __init__(self):
        super().__init__("ExampleDisassembler")

    def __call__(self, info):
        result = gdb.disassembler.builtin_disassemble(info)
        length = result.length
        text = result.string + "\t## Comment"
        return gdb.disassembler.DisassemblerResult(length, text)

gdb.disassembler.register_disassembler(ExampleDisassembler())
```

:::


The following example creates a sub-class of `DisassembleInfo` in order to intercept the `read_memory` calls, within `read_memory` any bytes read from memory have the two 4-bit nibbles swapped around. This isn't a very useful adjustment, but serves as an example.

> 以下示例创建了一个DisassembleInfo的子类，以拦截read_memory调用，在read_memory中，从内存读取的任何字节都会交换两个4位的豆腐块。 这不是一个非常有用的调整，但可以作为示例。

::: smallexample

```bash
class MyInfo(gdb.disassembler.DisassembleInfo):
    def __init__(self, info):
        super().__init__(info)

    def read_memory(self, length, offset):
        buffer = super().read_memory(length, offset)
        result = bytearray()
        for b in buffer:
            v = int.from_bytes(b, 'little')
            v = (v << 4) & 0xf0 | (v >> 4)
            result.append(v)
        return memoryview(result)

class NibbleSwapDisassembler(gdb.disassembler.Disassembler):
    def __init__(self):
        super().__init__("NibbleSwapDisassembler")

    def __call__(self, info):
        info = MyInfo(info)
        return gdb.disassembler.builtin_disassemble(info)

gdb.disassembler.register_disassembler(NibbleSwapDisassembler())
```

:::

---

::: header
Previous: [TUI Windows In Python](TUI-Windows-In-Python.html#TUI-Windows-In-Python)]
:::
