---
tip: translate by openai@2023-06-23 23:16:32
...
---
description: Index Section Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Index Section Format (Debugging with GDB)
lang: en
resource-type: document
title: Index Section Format (Debugging with GDB)
---
::: header
Next: [Debuginfod](Debuginfod.html#Debuginfod)]
:::

---

## Appendix J `.gdb_index` section format


This section documents the index section that is created by `save gdb-index` (see [Index Files](Index-Files.html#Index-Files)). The index section is DWARF-specific; some knowledge of DWARF is assumed in this description.

> 这一节文档描述了由`save gdb-index`创建的索引节（参见[索引文件](Index-Files.html#Index-Files)）。该索引节是DWARF特定的；在这里的描述中，假定了一定的DWARF知识。


The mapped index file format is designed to be directly `mmap` able on any architecture. In most cases, a datum is represented using a little-endian 32-bit integer value, called an `offset_type`. Big endian machines must byte-swap the values before using them. Exceptions to this rule are noted. The data is laid out such that alignment is always respected.

> 文件索引映射格式旨在在任何架构上直接`mmap`可用。在大多数情况下，一个数据使用小端32位整数值，称为`offset_type`表示。大端机器必须在使用它们之前进行字节交换。对此规则的例外情况将被提及。数据布局方式始终遵循对齐原则。

A mapped index consists of several areas, laid out in order.


1. The file header. This is a sequence of values, of `offset_type` unless otherwise noted:

> 1. 文件头。除非另有说明，否则这是一系列`offset_type`的值：


   1. The version number, currently 8. Versions 1, 2 and 3 are obsolete. Version 4 uses a different hashing function from versions 5 and 6. Version 6 includes symbols for inlined functions, whereas versions 4 and 5 do not. Version 7 adds attributes to the CU indices in the symbol table. Version 8 specifies that symbols from DWARF type units ('`DW_TAG_type_unit`') using the type.

> 版本号现在是8。1、2和3已经过时了。4版本使用不同的散列函数，与5、6版本不同。6版本添加了内联函数的符号，而4、5版本没有。7版本在符号表中为CU指数添加了属性。8版本指定使用类型的DWARF类型单元（'DW_TAG_type_unit'）的符号。

      [GDB] will only read version 4, 5, or 6 indices by specifying `set use-deprecated-index-sections on`. GDB has a workaround for potentially broken version 7 indices so it is currently not flagged as deprecated.
   2. The offset, from the start of the file, of the CU list.

   3. The offset, from the start of the file, of the types CU list. Note that this area can be empty, in which case this offset will be equal to the next offset.

> 文件开始处的偏移量，用于CU列表类型。注意，此区域可能为空，在这种情况下，此偏移量将等于下一个偏移量。
   4. The offset, from the start of the file, of the address area.
   5. The offset, from the start of the file, of the symbol table.
   6. The offset, from the start of the file, of the constant pool.

2. The CU list. This is a sequence of pairs of 64-bit little-endian values, sorted by the CU offset. The first element in each pair is the offset of a CU in the `.debug_info` section. The second element in each pair is the length of that CU. References to a CU elsewhere in the map are done using a CU index, which is just the 0-based index into this table. Note that if there are type CUs, then conceptually CUs and type CUs form a single list for the purposes of CU indices.

> 2. CU 列表。这是一系列64位小端值对，按CU偏移量排序。每个对中的第一个元素是`.debug_info`部分中CU的偏移量。每个对中的第二个元素是该CU的长度。在地图中其他位置引用CU时，使用CU索引，它只是此表的基于0的索引。请注意，如果存在类型CU，则概念上CU和类型CU形成单个列表，用于CU索引。

3. The types CU list. This is a sequence of triplets of 64-bit little-endian values. In a triplet, the first value is the CU offset, the second value is the type offset in the CU, and the third value is the type signature. The types CU list is not sorted.

> 这是一个64位小端值的三元组序列，称为CU列表。在一个三元组中，第一个值是CU偏移量，第二个值是CU中的类型偏移量，第三个值是类型签名。CU列表没有排序。

4. The address area. The address area consists of a sequence of address entries. Each address entry has three elements:

> 4. 地址区域。地址区域由一系列地址条目组成。每个地址条目有三个元素：

   1. The low address. This is a 64-bit little-endian value.

   2. The high address. This is a 64-bit little-endian value. Like `DW_AT_high_pc`, the value is one byte beyond the end.

> 2.高地址。这是一个64位小端值。像`DW_AT_high_pc`一样，该值比结尾多一个字节。
   3. The CU index. This is an `offset_type` value.

5. The symbol table. This is an open-addressed hash table. The size of the hash table is always a power of 2.

> 这是一个开放地址哈希表。哈希表的大小总是2的幂次方。


   Each slot in the hash table consists of a pair of `offset_type` values. The first value is the offset of the symbol's name in the constant pool. The second value is the offset of the CU vector in the constant pool.

> 每个哈希表中的槽都包含一对`offset_type`值。第一个值是符号名称在常量池中的偏移量。第二个值是CU向量在常量池中的偏移量。


   If both values are 0, then this slot in the hash table is empty. This is ok because while 0 is a valid constant pool index, it cannot be a valid index for both a string and a CU vector.

> 如果两个值都是0，那么哈希表中的这个槽就是空的。这是可以的，因为虽然0是一个有效的常量池索引，但它不能作为字符串和CU向量的有效索引。


   The hash value for a table entry is computed by applying an iterative hash function to the symbol's name. Starting with an initial value of `r = 0`, each (unsigned) character '`c`' in the string is incorporated into the hash using the formula depending on the index version:

> 哈希值的计算是通过将迭代哈希函数应用于符号名称来计算的。以初始值`r = 0`开始，字符串中的每个（无符号）字符'`c`'都根据索引版本使用以下公式包含在哈希中：

   Version 4

   :   The formula is `r = r * 67 + c - 113`.

   Versions 5 to 7

   :   The formula is `r = r * 67 + tolower (c) - 113`.

   The terminating '`\0`' is not incorporated into the hash.


   The step size used in the hash table is computed via `((hash * 17) & (size - 1)) | 1`, where '`hash`' is the size of the hash table. The step size is used to find the next candidate slot when handling a hash collision.

> 哈希表中使用的步长是通过`((hash * 17) & (size - 1)) | 1`计算的，其中'`hash`'是哈希表的大小。步长用于处理哈希冲突时找到下一个候选槽。


   The names of C++ symbols in the hash table are canonicalized. We don't currently have a simple description of the canonicalization algorithm; if you intend to create new index sections, you must read the code.

> 哈希表中的C++符号的名称被规范化了。我们目前没有一个简单的规范化算法的描述；如果您打算创建新的索引部分，您必须阅读代码。

6. The constant pool. This is simply a bunch of bytes. It is organized so that alignment is correct: CU vectors are stored first, followed by strings.

> 常量池。这只是一堆字节。它组织得很正确：CU向量存储在前面，接着是字符串。


   A CU vector in the constant pool is a sequence of `offset_type` values. The first value is the number of CU indices in the vector. Each subsequent value is the index and symbol attributes of a CU in the CU list. This element in the hash table is used to indicate which CUs define the symbol and how the symbol is used. See below for the format of each CU index+attributes entry.

> 在常量池中的CU向量是一个`offset_type`值序列。第一个值是CU索引的数量。每个后续值都是CU列表中CU的索引和符号属性。此哈希表中的元素用于指示哪些CU定义了符号以及如何使用符号。有关每个CU索引+属性条目的格式，请参见下面。

   A string in the constant pool is zero-terminated.


Attributes were added to CU index values in `.gdb_index` version 7. If a symbol has multiple uses within a CU then there is one CU index+attributes value for each use.

> 在`gdb_index`版本7中，属性被添加到CU索引值中。如果一个符号在CU中有多种用途，则每个用途都有一个CU索引+属性值。

The format of each CU index+attributes entry is as follows (bit 0 = LSB):

Bits 0-23

:   This is the index of the CU in the CU list.

Bits 24-27

:   These bits are reserved for future purposes and must be zero.

Bits 28-30

:   The kind of the symbol in the CU.

```
0

:   This value is reserved and should not be used. By reserving zero the full `offset_type` value is backwards compatible with previous versions of the index.

1

:   The symbol is a type.

2

:   The symbol is a variable or an enum value.

3

:   The symbol is a function.

4

:   Any other kind of symbol.

5,6,7

:   These values are reserved.
```

Bit 31

:   This bit is zero if the value is global and one if it is static.

```
The determination of whether a symbol is global or static is complicated. The authorative reference is the file `dwarf2read.c` sources.
```


This pseudo-code describes the computation of a symbol's kind and global/static attributes in the index.

> 这段伪代码描述了在索引中计算符号种类及全局/静态属性的计算。

::: smallexample

```bash
is_external = get_attribute (die, DW_AT_external);
language = get_attribute (cu_die, DW_AT_language);
switch (die->tag)
  {
  case DW_TAG_typedef:
  case DW_TAG_base_type:
  case DW_TAG_subrange_type:
    kind = TYPE;
    is_static = 1;
    break;
  case DW_TAG_enumerator:
    kind = VARIABLE;
    is_static = language != CPLUS;
    break;
  case DW_TAG_subprogram:
    kind = FUNCTION;
    is_static = ! (is_external || language == ADA);
    break;
  case DW_TAG_constant:
    kind = VARIABLE;
    is_static = ! is_external;
    break;
  case DW_TAG_variable:
    kind = VARIABLE;
    is_static = ! is_external;
    break;
  case DW_TAG_namespace:
    kind = TYPE;
    is_static = 0;
    break;
  case DW_TAG_class_type:
  case DW_TAG_interface_type:
  case DW_TAG_structure_type:
  case DW_TAG_union_type:
  case DW_TAG_enumeration_type:
    kind = TYPE;
    is_static = language != CPLUS;
    break;
  default:
    assert (0);
  }
```

:::

---

::: header
Next: [Debuginfod](Debuginfod.html#Debuginfod)]
:::
