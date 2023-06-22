---
description: Varying Target Capabilities (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Varying Target Capabilities (Debugging with GDB)
lang: en
resource-type: document
title: Varying Target Capabilities (Debugging with GDB)
---
::: header
Next: [Rationale](Rationale.html#Rationale)]
:::

---

### F.4 Varying Target Capabilities

Some targets don't support floating-point, and some would rather not have to deal with `long long` operations. Also, different targets will have different stack sizes, and different bytecode buffer lengths.

Thus, GDB needs a way to ask the target about itself. We haven't worked out the details yet, but in general, GDB should be able to send the target a packet asking it to describe itself. The reply should be a packet whose length is explicit, so we can add new information to the packet in future revisions of the agent, without confusing old versions of GDB, and it should contain a version number. It should contain at least the following information:

- whether floating point is supported
- whether `long long` is supported
- maximum acceptable size of bytecode stack
- maximum acceptable length of bytecode expressions
- which registers are actually available for collection
- whether the target supports disabled tracepoints
