---
tip: translate by openai@2023-06-24 04:44:54
...
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

> 一些目标不支持浮点数，有些则不想处理`long long`操作。此外，不同的目标会有不同的堆栈大小和不同的字节码缓冲区长度。


Thus, GDB needs a way to ask the target about itself. We haven't worked out the details yet, but in general, GDB should be able to send the target a packet asking it to describe itself. The reply should be a packet whose length is explicit, so we can add new information to the packet in future revisions of the agent, without confusing old versions of GDB, and it should contain a version number. It should contain at least the following information:

> 因此，GDB需要一种方法来询问目标有关自身的信息。我们尚未完成细节，但一般来说，GDB应该能够向目标发送一个数据包，要求其描述自身。回复应该是一个具有明确长度的数据包，以便我们可以在未来的代理版本中添加新的信息，而不会混淆旧版本的GDB，并且它应该包含一个版本号。它至少应包含以下信息：

- whether floating point is supported
- whether `long long` is supported
- maximum acceptable size of bytecode stack
- maximum acceptable length of bytecode expressions
- which registers are actually available for collection
- whether the target supports disabled tracepoints
