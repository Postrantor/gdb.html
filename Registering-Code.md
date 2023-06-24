---
tip: translate by openai@2023-06-24 02:00:01
...
---
description: Registering Code (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Registering Code (Debugging with GDB)
lang: en
resource-type: document
title: Registering Code (Debugging with GDB)
---
::: header
Next: [Unregistering Code](Unregistering-Code.html#Unregistering-Code)]
:::

---

### 30.2 Registering Code

To register code with [GDB], the JIT should follow this protocol:


- Generate an object file in memory with symbols and other desired debug information. The file must include the virtual addresses of the sections.

> 生成一个内存中的对象文件，其中包含符号和其他所需的调试信息。该文件必须包含节的虚拟地址。
- Create a code entry for the file, which gives the start and size of the symbol file.
- Add it to the linked list in the JIT descriptor.
- Point the relevant_entry field of the descriptor at the entry.
- Set `action_flag` to `JIT_REGISTER` and call `__jit_debug_register_code`.


When [GDB] to attach to a running process and still find the symbol files.

> 当使用GDB附加到一个正在运行的进程时，仍然可以找到符号文件。
