---
tip: translate by openai@2023-06-24 02:25:37
...
---
description: Separate Debug Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Separate Debug Files (Debugging with GDB)
lang: en
resource-type: document
title: Separate Debug Files (Debugging with GDB)
---
::: header
Next: [MiniDebugInfo](MiniDebugInfo.html#MiniDebugInfo)]
:::

---

### 18.3 Debugging Information in Separate Files


[GDB] to find and load the debugging information automatically. Since debugging information can be very large---sometimes larger than the executable code itself---some systems distribute debugging information for their executables in separate files, which users can install only when they need to debug a problem.

> GDB可以自动查找和加载调试信息。由于调试信息可能非常大，有时甚至比可执行代码本身还要大，一些系统将调试信息分发到单独的文件中，用户只有在需要调试问题时才能安装这些文件。

[GDB] supports two ways of specifying the separate debug info file:


- The executable contains a *debug link* that specifies the name of the separate debug info file. The separate debug file's name is usually `executable.debug` uses to validate that the executable and the debug file came from the same build.

> 可执行文件包含一个*调试链接*，指定单独的调试信息文件的名称。单独的调试文件的名称通常是`executable.debug`，用来验证可执行文件和调试文件来自同一次构建。

- command-line option in [Command Line Options](http://sourceware.org/binutils/docs/ld/Options.html#Options) in The GNU Linker. The debug info file's name is not specified explicitly by the build ID, but can be computed from the build ID, see below.

> 在GNU链接器中的[命令行选项](http://sourceware.org/binutils/docs/ld/Options.html#Options)中的命令行选项。调试信息文件的名称不是由构建ID明确指定的，但可以从构建ID计算出来，详见下文。


Depending on the way the debug info file is specified, [GDB] uses two different methods of looking for the debug file:

> 根据调试信息文件的指定方式，[GDB]使用两种不同的查找调试文件的方法：

- For the "debug link" method, [GDB], because Windows filesystems disallow colons in file names.)

- For the "build ID" method, [GDB] can automatically query `debuginfod` servers using build IDs in order to download separate debug files that cannot be found locally. For more information see [Debuginfod](Debuginfod.html#Debuginfod).

> 对于“构建ID”方法，[GDB]可以自动查询`debuginfod`服务器，使用构建ID来下载无法在本地找到的单独的调试文件。有关更多信息，请参见[Debuginfod](Debuginfod.html#Debuginfod)。


So, for example, suppose you ask [GDB] will look for the following debug information files, in the indicated order:

> 例如，假设你问[GDB]将按照以下顺序查找以下调试信息文件：

- \- `/usr/lib/debug/.build-id/ab/cdef1234.debug`
- \- `/usr/bin/ls.debug`
- \- `/usr/bin/.debug/ls.debug`
- \- `/usr/lib/debug/usr/bin/ls.debug`.


If the debug file still has not been found and `debuginfod` (see [Debuginfod](Debuginfod.html#Debuginfod)) is enabled, [GDB] will attempt to download the file from `debuginfod` servers.

> 如果调试文件仍未找到，且启用了`debuginfod`（请参阅[Debuginfod](Debuginfod.html#Debuginfod)），[GDB]将尝试从`debuginfod`服务器下载该文件。


Global debugging info directories default to what is set by [GDB] is currently using.

> 全局调试信息目录默认设置为[GDB]当前正在使用的设置。

`set debug-file-directory directories`


Set the directories which [GDB]. Multiple path components can be set concatenating them by a path separator.

> 设置[GDB]的目录。可以通过路径分隔符将多个路径组件连接在一起。

`show debug-file-directory`


Show the directories [GDB] searches for separate debugging information files.

> 显示[GDB]搜索独立调试信息文件的目录。


A debug link is a special section of the executable file named `.gnu_debuglink`. The section must contain:

> 调试链接是可执行文件中名为`.gnu_debuglink`的特殊部分。该部分必须包含：

- A filename, with any leading directory components removed, followed by a zero byte,

- zero to three bytes of padding, as needed to reach the next four-byte boundary within the section, and

> 零到三个字节的填充，根据需要在该节内达到下一个四字节边界。

- a four-byte CRC checksum, stored in the same endianness used for the executable file itself. The checksum is computed on the debugging information file's full contents by the function given below, passing zero as the `crc` argument.

> CRC校验和，存储在与可执行文件本身相同的字节序中，由下面给出的函数计算调试信息文件的全部内容，将零作为'crc'参数。


Any executable file format can carry a debug link, as long as it can contain a section named `.gnu_debuglink` with the contents described above.

> 任何可执行文件格式都可以携带调试链接，只要它能够包含名为`.gnu_debuglink`的部分，其内容符合上述描述。


The build ID is a special section in the executable file (and in other ELF binary files that [GDB] may consider). This section is often named `.note.gnu.build-id`, but that name is not mandatory. It contains unique identification for the built files---the ID remains the same across multiple builds of the same build tree. The default algorithm SHA1 produces 160 bits (40 hexadecimal characters) of the content for the build ID string. The same section with an identical value is present in the original built binary with symbols, in its stripped variant, and in the separate debugging information file.

> 构建ID是可执行文件（以及GDB可能会考虑的其他ELF二进制文件）中的一个特殊部分。该部分通常被命名为`.note.gnu.build-id`，但这不是强制性的。它包含了构建文件的唯一标识符-ID在相同构建树的多次构建中保持不变。默认的算法SHA1为构建ID字符串生成160位（40个十六进制字符）的内容。具有相同值的相同部分存在于原始构建的带符号的二进制文件中，在其剥离变体中，以及在单独的调试信息文件中。


The debugging information file itself should be an ordinary executable, containing a full set of linker symbols, sections, and debugging information. The sections of the debugging information file should have the same names, addresses, and sizes as the original file, but they need not contain any data---much like a `.bss` section in an ordinary executable.

> 调试信息文件本身应该是一个普通的可执行文件，包含完整的链接符号、段和调试信息。调试信息文件的段应该具有与原始文件相同的名称、地址和大小，但它们不需要包含任何数据——就像一个普通可执行文件中的`.bss`段一样。


The [GNU]' utility that can produce the separated executable / debugging information file pairs using the following commands:

> GNU 的实用程序可以使用以下命令生成分离的可执行/调试信息文件对：

::: smallexample

```bash
objcopy --only-keep-debug foo foo.debug
strip -g foo
```

:::


These commands remove the debugging information from the executable file `foo`. You can use the first, second or both methods to link the two files:

> 这些命令可以从可执行文件`foo`中移除调试信息。您可以使用第一种、第二种或两种方法来链接这两个文件：


- The debug link method needs the following additional command to also leave behind a debug link in `foo`:

> 调试链接方法需要以下附加命令来在`foo`中留下调试链接：

  ::: smallexample

  ```bash
  objcopy --add-gnu-debuglink=foo.debug foo
  ```

  :::


  Ulrich Drepper's `elfutils` has the same functionality as the two `objcopy` commands and the `ln -s` command above, together.

> Ulrich Drepper的`elfutils`具有与上述两个`objcopy`命令和`ln -s`命令相同的功能。

- Build ID gets embedded into the main executable using `ld --build-id` or the [GCC] binary utilities (Binutils) package since version 2.18.

> 使用`ld --build-id`或[GCC]二进制实用程序（Binutils）软件包（自2.18版本起）将构建ID嵌入到主可执行文件中。


The CRC used in `.gnu_debuglink` is the CRC-32 defined in IEEE 802.3 using the polynomial:

> CRC在`gnu_debuglink`中使用的是IEEE 802.3定义的CRC-32，使用的多项式是：

::: display

```display
 x32 + x26 + x23 + x22 + x16 + x12 + x11
 + x10 + x8 + x7 + x5 + x4 + x2 + x + 1
```

:::


The function is computed byte at a time, taking the least significant bit of each byte first. The initial pattern `0xffffffff` is used, to ensure leading zeros affect the CRC and the final result is inverted to ensure trailing zeros also affect the CRC.

> 函数是一次计算一个字节，先处理每个字节的最低有效位。使用初始模式`0xffffffff`，以确保前导零也会影响CRC，最终结果取反，以确保尾部零也会影响CRC。


*Note:* This is the same CRC polynomial as used in handling the *Remote Serial Protocol* `qCRC` packet (see [qCRC packet](General-Query-Packets.html#qCRC-packet)). However in the case of the Remote Serial Protocol, the CRC is computed *most* significant bit first, and the result is not inverted, so trailing zeros have no effect on the CRC value.

> *注意：* 这是与处理*远程串行协议* `qCRC` 包（参见[qCRC 包](General-Query-Packets.html#qCRC-packet)）相同的CRC多项式。但是在远程串行协议的情况下，CRC是以*最*重要的位首先计算的，结果也不会取反，因此尾随的零对CRC值没有影响。


To complete the description, we show below the code of the function which produces the CRC used in `.gnu_debuglink`. Inverting the initially supplied `crc` argument means that an initial call to this function passing in zero will start computing the CRC using `0xffffffff`.

> 为了完成描述，我们下面展示了生成`.gnu_debuglink`中使用的CRC的函数代码。 将最初提供的`crc`参数取反意味着对此函数的初始调用传入零将开始使用`0xffffffff`计算CRC。

::: smallexample

```bash
unsigned long
gnu_debuglink_crc32 (unsigned long crc,
                     unsigned char *buf, size_t len)
{
  static const unsigned long crc32_table[256] =
    {
      0x00000000, 0x77073096, 0xee0e612c, 0x990951ba, 0x076dc419,
      0x706af48f, 0xe963a535, 0x9e6495a3, 0x0edb8832, 0x79dcb8a4,
      0xe0d5e91e, 0x97d2d988, 0x09b64c2b, 0x7eb17cbd, 0xe7b82d07,
      0x90bf1d91, 0x1db71064, 0x6ab020f2, 0xf3b97148, 0x84be41de,
      0x1adad47d, 0x6ddde4eb, 0xf4d4b551, 0x83d385c7, 0x136c9856,
      0x646ba8c0, 0xfd62f97a, 0x8a65c9ec, 0x14015c4f, 0x63066cd9,
      0xfa0f3d63, 0x8d080df5, 0x3b6e20c8, 0x4c69105e, 0xd56041e4,
      0xa2677172, 0x3c03e4d1, 0x4b04d447, 0xd20d85fd, 0xa50ab56b,
      0x35b5a8fa, 0x42b2986c, 0xdbbbc9d6, 0xacbcf940, 0x32d86ce3,
      0x45df5c75, 0xdcd60dcf, 0xabd13d59, 0x26d930ac, 0x51de003a,
      0xc8d75180, 0xbfd06116, 0x21b4f4b5, 0x56b3c423, 0xcfba9599,
      0xb8bda50f, 0x2802b89e, 0x5f058808, 0xc60cd9b2, 0xb10be924,
      0x2f6f7c87, 0x58684c11, 0xc1611dab, 0xb6662d3d, 0x76dc4190,
      0x01db7106, 0x98d220bc, 0xefd5102a, 0x71b18589, 0x06b6b51f,
      0x9fbfe4a5, 0xe8b8d433, 0x7807c9a2, 0x0f00f934, 0x9609a88e,
      0xe10e9818, 0x7f6a0dbb, 0x086d3d2d, 0x91646c97, 0xe6635c01,
      0x6b6b51f4, 0x1c6c6162, 0x856530d8, 0xf262004e, 0x6c0695ed,
      0x1b01a57b, 0x8208f4c1, 0xf50fc457, 0x65b0d9c6, 0x12b7e950,
      0x8bbeb8ea, 0xfcb9887c, 0x62dd1ddf, 0x15da2d49, 0x8cd37cf3,
      0xfbd44c65, 0x4db26158, 0x3ab551ce, 0xa3bc0074, 0xd4bb30e2,
      0x4adfa541, 0x3dd895d7, 0xa4d1c46d, 0xd3d6f4fb, 0x4369e96a,
      0x346ed9fc, 0xad678846, 0xda60b8d0, 0x44042d73, 0x33031de5,
      0xaa0a4c5f, 0xdd0d7cc9, 0x5005713c, 0x270241aa, 0xbe0b1010,
      0xc90c2086, 0x5768b525, 0x206f85b3, 0xb966d409, 0xce61e49f,
      0x5edef90e, 0x29d9c998, 0xb0d09822, 0xc7d7a8b4, 0x59b33d17,
      0x2eb40d81, 0xb7bd5c3b, 0xc0ba6cad, 0xedb88320, 0x9abfb3b6,
      0x03b6e20c, 0x74b1d29a, 0xead54739, 0x9dd277af, 0x04db2615,
      0x73dc1683, 0xe3630b12, 0x94643b84, 0x0d6d6a3e, 0x7a6a5aa8,
      0xe40ecf0b, 0x9309ff9d, 0x0a00ae27, 0x7d079eb1, 0xf00f9344,
      0x8708a3d2, 0x1e01f268, 0x6906c2fe, 0xf762575d, 0x806567cb,
      0x196c3671, 0x6e6b06e7, 0xfed41b76, 0x89d32be0, 0x10da7a5a,
      0x67dd4acc, 0xf9b9df6f, 0x8ebeeff9, 0x17b7be43, 0x60b08ed5,
      0xd6d6a3e8, 0xa1d1937e, 0x38d8c2c4, 0x4fdff252, 0xd1bb67f1,
      0xa6bc5767, 0x3fb506dd, 0x48b2364b, 0xd80d2bda, 0xaf0a1b4c,
      0x36034af6, 0x41047a60, 0xdf60efc3, 0xa867df55, 0x316e8eef,
      0x4669be79, 0xcb61b38c, 0xbc66831a, 0x256fd2a0, 0x5268e236,
      0xcc0c7795, 0xbb0b4703, 0x220216b9, 0x5505262f, 0xc5ba3bbe,
      0xb2bd0b28, 0x2bb45a92, 0x5cb36a04, 0xc2d7ffa7, 0xb5d0cf31,
      0x2cd99e8b, 0x5bdeae1d, 0x9b64c2b0, 0xec63f226, 0x756aa39c,
      0x026d930a, 0x9c0906a9, 0xeb0e363f, 0x72076785, 0x05005713,
      0x95bf4a82, 0xe2b87a14, 0x7bb12bae, 0x0cb61b38, 0x92d28e9b,
      0xe5d5be0d, 0x7cdcefb7, 0x0bdbdf21, 0x86d3d2d4, 0xf1d4e242,
      0x68ddb3f8, 0x1fda836e, 0x81be16cd, 0xf6b9265b, 0x6fb077e1,
      0x18b74777, 0x88085ae6, 0xff0f6a70, 0x66063bca, 0x11010b5c,
      0x8f659eff, 0xf862ae69, 0x616bffd3, 0x166ccf45, 0xa00ae278,
      0xd70dd2ee, 0x4e048354, 0x3903b3c2, 0xa7672661, 0xd06016f7,
      0x4969474d, 0x3e6e77db, 0xaed16a4a, 0xd9d65adc, 0x40df0b66,
      0x37d83bf0, 0xa9bcae53, 0xdebb9ec5, 0x47b2cf7f, 0x30b5ffe9,
      0xbdbdf21c, 0xcabac28a, 0x53b39330, 0x24b4a3a6, 0xbad03605,
      0xcdd70693, 0x54de5729, 0x23d967bf, 0xb3667a2e, 0xc4614ab8,
      0x5d681b02, 0x2a6f2b94, 0xb40bbe37, 0xc30c8ea1, 0x5a05df1b,
      0x2d02ef8d
    };
  unsigned char *end;

  crc = ~crc & 0xffffffff;
  for (end = buf + len; buf < end; ++buf)
    crc = crc32_table[(crc ^ *buf) & 0xff] ^ (crc >> 8);
  return ~crc & 0xffffffff;
}
```

:::

This computation does not apply to the "build ID" method.

---

::: header
Next: [MiniDebugInfo](MiniDebugInfo.html#MiniDebugInfo)]
:::
