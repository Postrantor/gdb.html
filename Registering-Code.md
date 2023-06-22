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
- Create a code entry for the file, which gives the start and size of the symbol file.
- Add it to the linked list in the JIT descriptor.
- Point the relevant_entry field of the descriptor at the entry.
- Set `action_flag` to `JIT_REGISTER` and call `__jit_debug_register_code`.

When [GDB] to attach to a running process and still find the symbol files.
