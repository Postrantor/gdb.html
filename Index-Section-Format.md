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

The mapped index file format is designed to be directly `mmap` able on any architecture. In most cases, a datum is represented using a little-endian 32-bit integer value, called an `offset_type`. Big endian machines must byte-swap the values before using them. Exceptions to this rule are noted. The data is laid out such that alignment is always respected.

A mapped index consists of several areas, laid out in order.

1. The file header. This is a sequence of values, of `offset_type` unless otherwise noted:

   1. The version number, currently 8. Versions 1, 2 and 3 are obsolete. Version 4 uses a different hashing function from versions 5 and 6. Version 6 includes symbols for inlined functions, whereas versions 4 and 5 do not. Version 7 adds attributes to the CU indices in the symbol table. Version 8 specifies that symbols from DWARF type units ('`DW_TAG_type_unit`') using the type.

      [GDB] will only read version 4, 5, or 6 indices by specifying `set use-deprecated-index-sections on`. GDB has a workaround for potentially broken version 7 indices so it is currently not flagged as deprecated.
   2. The offset, from the start of the file, of the CU list.
   3. The offset, from the start of the file, of the types CU list. Note that this area can be empty, in which case this offset will be equal to the next offset.
   4. The offset, from the start of the file, of the address area.
   5. The offset, from the start of the file, of the symbol table.
   6. The offset, from the start of the file, of the constant pool.
2. The CU list. This is a sequence of pairs of 64-bit little-endian values, sorted by the CU offset. The first element in each pair is the offset of a CU in the `.debug_info` section. The second element in each pair is the length of that CU. References to a CU elsewhere in the map are done using a CU index, which is just the 0-based index into this table. Note that if there are type CUs, then conceptually CUs and type CUs form a single list for the purposes of CU indices.
3. The types CU list. This is a sequence of triplets of 64-bit little-endian values. In a triplet, the first value is the CU offset, the second value is the type offset in the CU, and the third value is the type signature. The types CU list is not sorted.
4. The address area. The address area consists of a sequence of address entries. Each address entry has three elements:

   1. The low address. This is a 64-bit little-endian value.
   2. The high address. This is a 64-bit little-endian value. Like `DW_AT_high_pc`, the value is one byte beyond the end.
   3. The CU index. This is an `offset_type` value.
5. The symbol table. This is an open-addressed hash table. The size of the hash table is always a power of 2.

   Each slot in the hash table consists of a pair of `offset_type` values. The first value is the offset of the symbol's name in the constant pool. The second value is the offset of the CU vector in the constant pool.

   If both values are 0, then this slot in the hash table is empty. This is ok because while 0 is a valid constant pool index, it cannot be a valid index for both a string and a CU vector.

   The hash value for a table entry is computed by applying an iterative hash function to the symbol's name. Starting with an initial value of `r = 0`, each (unsigned) character '`c`' in the string is incorporated into the hash using the formula depending on the index version:

   Version 4

   :   The formula is `r = r * 67 + c - 113`.

   Versions 5 to 7

   :   The formula is `r = r * 67 + tolower (c) - 113`.

   The terminating '`\0`' is not incorporated into the hash.

   The step size used in the hash table is computed via `((hash * 17) & (size - 1)) | 1`, where '`hash`' is the size of the hash table. The step size is used to find the next candidate slot when handling a hash collision.

   The names of C++ symbols in the hash table are canonicalized. We don't currently have a simple description of the canonicalization algorithm; if you intend to create new index sections, you must read the code.
6. The constant pool. This is simply a bunch of bytes. It is organized so that alignment is correct: CU vectors are stored first, followed by strings.

   A CU vector in the constant pool is a sequence of `offset_type` values. The first value is the number of CU indices in the vector. Each subsequent value is the index and symbol attributes of a CU in the CU list. This element in the hash table is used to indicate which CUs define the symbol and how the symbol is used. See below for the format of each CU index+attributes entry.

   A string in the constant pool is zero-terminated.

Attributes were added to CU index values in `.gdb_index` version 7. If a symbol has multiple uses within a CU then there is one CU index+attributes value for each use.

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
