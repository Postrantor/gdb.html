---
description: Unregistering Code (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Unregistering Code (Debugging with GDB)
lang: en
resource-type: document
title: Unregistering Code (Debugging with GDB)
---
::: header
Next: [Custom Debug Info](Custom-Debug-Info.html#Custom-Debug-Info)]
:::

---

### 30.3 Unregistering Code

If code is freed, then the JIT should use the following protocol:

- Remove the code entry corresponding to the code from the linked list.
- Point the `relevant_entry` field of the descriptor at the code entry.
- Set `action_flag` to `JIT_UNREGISTER` and call `__jit_debug_register_code`.

If the JIT frees or recompiles code without unregistering it, then [GDB] and the JIT will leak the memory used for the associated symbol files.
