---
tip: translate by openai@2023-06-24 00:14:40
...
---
description: Memory Region Attributes (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Memory Region Attributes (Debugging with GDB)
lang: en
resource-type: document
title: Memory Region Attributes (Debugging with GDB)
---
::: header
Next: [Dump/Restore Files](Dump_002fRestore-Files.html#Dump_002fRestore-Files)]
:::

---

### 10.18 Memory Region Attributes


*Memory region attributes* allow you to describe special handling required by regions of your target's memory. [GDB] uses attributes to determine whether to allow certain types of memory accesses; whether to use specific width accesses; and whether to cache target memory. By default the description of memory regions is fetched from the target (if the current target supports this), but the user can override the fetched regions.

> *内存区域属性*允许您描述目标内存区域所需的特殊处理。[GDB]使用属性来确定是否允许某些类型的内存访问；是否使用特定宽度的访问；以及是否对目标内存进行缓存。默认情况下，将从目标获取内存区域的描述（如果当前目标支持此功能），但用户可以覆盖获取的区域。


Defined memory regions can be individually enabled and disabled. When a memory region is disabled, [GDB] uses the default attributes when accessing all memory.

> 定义的内存区域可以单独启用和禁用。当内存区域被禁用时，[GDB]在访问所有内存时使用默认属性。


When a memory region is defined, it is given a number to identify it; to enable, disable, or remove a memory region, you specify that number.

> 当定义一个内存区域时，会给它分配一个编号来标识它；要启用、禁用或删除内存区域，您只需指定该编号即可。

`mem lower upper attributes…`


Define a memory region bounded by `lower` == 0 is a special case: it is treated as the target's maximum memory address. (0xffff on 16 bit targets, 0xffffffff on 32 bit targets, etc.)

> 定义一个以`lower`等于0为界限的内存区域是一种特殊情况：它被视为目标的最大内存地址（16位目标的0xffff，32位目标的0xffffffff等）。

`mem auto`


Discard any user changes to the memory regions and use target-supplied regions, if available, or no regions if the target does not support.

> 放弃任何用户对内存区域的更改，如果可用，使用目标提供的区域，如果目标不支持，则不使用区域。

`delete mem nums…`

Remove memory regions `nums`.

`disable mem nums…`


Disable monitoring of memory regions `nums`.... A disabled memory region is not forgotten. It may be enabled again later.

> 禁用监控内存区域`nums`.... 禁用的内存区域不会被遗忘，以后可以再次启用。

`enable mem nums…`

Enable monitoring of memory regions `nums`....

`info mem`


Print a table of all defined memory regions, with the following columns for each region:

> 打印出所有已定义的内存区域的表格，每个区域有以下列：

*Memory Region Number*
*Enabled or Disabled.*

:   Enabled memory regions are marked with '`y`'.

*Lo Address*

:   The address defining the inclusive lower bound of the memory region.

*Hi Address*

:   The address defining the exclusive upper bound of the memory region.

*Attributes*

:   The list of attributes set for this memory region.

#### 10.18.1 Attributes

#### 10.18.1.1 Memory Access Mode


The access mode attributes set whether [GDB] may make read or write accesses to a memory region.

> 访问模式属性设置[GDB]是否可以对内存区域进行读取或写入访问。


While these attributes prevent [GDB] from performing invalid memory accesses, they do nothing to prevent the target system, I/O DMA, etc. from accessing memory.

> 虽然这些属性可以防止GDB执行无效的内存访问，但它们无法阻止目标系统、I/O DMA等访问内存。

`ro`

:   Memory is read only.

`wo`

:   Memory is write only.

`rw`

:   Memory is read/write. This is the default.

#### 10.18.1.2 Memory Access Size

The access size attribute tells [GDB] may use accesses of any size.

`8`

:   Use 8 bit memory accesses.

`16`

:   Use 16 bit memory accesses.

`32`

:   Use 32 bit memory accesses.

`64`

:   Use 64 bit memory accesses.

#### 10.18.1.3 Data Cache


The data cache attributes set whether [GDB] does not know about volatile variables or memory mapped device registers.

> 设置数据缓存属性决定[GDB]是否知道关于易失变量或内存映射设备寄存器。

`cache`

:   Enable [GDB] to cache target memory.

`nocache`

:   Disable [GDB] from caching target memory. This is the default.

#### 10.18.2 Memory Access Checking


[GDB] can be instructed to refuse accesses to memory that is not explicitly described. This can be useful if accessing such regions has undesired effects for a specific target, or to provide better error checking. The following commands control this behaviour.

> GDB可以被指示拒绝对未明确描述的内存的访问。如果对特定目标访问这些区域会产生不希望的效果，或者提供更好的错误检查，这可能是有用的。以下命令控制此行为。

`set mem inaccessible-by-default [on|off]`

If `on` is specified, make [GDB]

`show mem inaccessible-by-default`

Show the current handling of accesses to unknown memory.

---

::: header
Next: [Dump/Restore Files](Dump_002fRestore-Files.html#Dump_002fRestore-Files)]
:::
