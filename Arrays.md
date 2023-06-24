---
tip: translate by openai@2023-06-23 17:35:02
...
---
description: Arrays (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Arrays (Debugging with GDB)
lang: en
resource-type: document
title: Arrays (Debugging with GDB)
---
::: header
Next: [Output Formats](Output-Formats.html#Output-Formats)]
:::

---

### 10.4 Artificial Arrays


It is often useful to print out several successive objects of the same type in memory; a section of an array, or an array of dynamically determined size for which only a pointer exists in the program.

> 常常有用的是打印出内存中同一类型的多个连续对象；一个数组的一部分，或者一个程序中只存在指针的动态大小的数组。


You can do this by referring to a contiguous span of memory as an *artificial array*, using the binary operator '`@`' should be the first element of the desired array and be an individual object. The right operand should be the desired length of the array. The result is an array value whose elements are all of the type of the left argument. The first element is actually the left argument; the second element comes from bytes of memory immediately following those that hold the first element, and so on. Here is an example. If a program says

> 你可以通过将连续的内存范围引用为*人工数组*来实现这一点，使用二进制运算符'@'应该是所需数组的第一个元素，并且是一个单独的对象。右操作数应该是所需数组的长度。结果是一个数组值，其元素都是左边参数的类型。第一个元素实际上是左边的参数；第二个元素来自存储第一个元素的内存字节之后的内存字节，依此类推。这是一个例子。如果一个程序说

::: smallexample

```bash
int *array = (int *) malloc (len * sizeof (int));
```

:::


you can print the contents of `array` with

> 你可以使用打印数组的内容。

::: smallexample

```bash
p *array@len
```

:::


The left operand of '`@`' in this way behave just like other arrays in terms of subscripting, and are coerced to pointers when used in expressions. Artificial arrays most often appear in expressions via the value history (see [Value History](Value-History.html#Value-History)), after printing one out.

> 左操作数的'@'就像其他数组一样在下标访问中表现出来，并且在表达式中被强制转换为指针。人造数组通常通过值历史（参见[值历史]（Value-History.html#Value-History））在表达式中出现，打印出一个之后。


Another way to create an artificial array is to use a cast. This re-interprets a value as if it were an array. The value need not be in memory:

> 另一种创建人工数组的方法是使用转换。这会重新解释一个值，就好像它是一个数组一样。该值不一定需要在内存中：

::: smallexample

```bash
(gdb) p/x (short[2])0x12345678
$1 = 
```

:::


As a convenience, if you leave the array length out (as in '`(type)value`':

> 作为方便起见，如果你省略了数组长度（如'（类型）值'）：

::: smallexample

```bash
(gdb) p/x (short)0x12345678
$2 = 
```

:::


Sometimes the artificial array mechanism is not quite enough; in moderately complex data structures, the elements of interest may not actually be adjacent---for example, if you are interested in the values of pointers in an array. One useful work-around in this situation is to use a convenience variable (see [Convenience Variables](Convenience-Vars.html#Convenience-Vars)) as a counter in an expression that prints the first interesting value, and then repeat that expression via RET. For instance, suppose you have an array `dtab` of pointers to structures, and you are interested in the values of a field `fv` in each structure. Here is an example of what you might type:

> 有时人工数组机制还不够用；在中等复杂的数据结构中，感兴趣的元素可能不是相邻的---例如，如果您对数组中的指针值感兴趣。在这种情况下，一种有用的解决方案是使用方便变量（请参见[方便变量]（Convenience-Vars.html#Convenience-Vars））作为表达式中的计数器，以打印第一个有趣的值，然后通过RET重复该表达式。例如，假设您有一个指向结构的指针数组`dtab`，您对每个结构中的字段`fv`的值感兴趣。这是您可能输入的示例：

::: smallexample

```bash
set $i = 0
p dtab[$i++]->fv
RET
RET
…
```

:::

---

::: header
Next: [Output Formats](Output-Formats.html#Output-Formats)]
:::
