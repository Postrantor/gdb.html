---
tip: translate by openai@2023-06-23 15:16:03
...
---
description: Unregistering Code (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Unregistering Code (Debugging with GDB)
lang: en
resource-type: document
title: Unregistering Code (Debugging with GDB)
----------------------------------------------

::: header
Next: [Custom Debug Info](Custom-Debug-Info.html#Custom-Debug-Info)]
:::

---

### 30.3 Unregistering Code

If code is freed, then the JIT should use the following protocol:

> 如果代码被释放，那么 JIT 应该使用以下协议：

- Remove the code entry corresponding to the code from the linked list.
- Point the `relevant_entry` field of the descriptor at the code entry.
- Set `action_flag` to `JIT_UNREGISTER` and call `__jit_debug_register_code`.

If the JIT frees or recompiles code without unregistering it, then [GDB] and the JIT will leak the memory used for the associated symbol files.

> 如果 JIT 没有取消注册就释放或重新编译代码，那么 GDB 和 JIT 将泄漏用于相关符号文件的内存。
