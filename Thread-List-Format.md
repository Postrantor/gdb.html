---
description: Thread List Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Thread List Format (Debugging with GDB)
lang: en
resource-type: document
title: Thread List Format (Debugging with GDB)
---
::: header
Next: [Traceframe Info Format](Traceframe-Info-Format.html#Traceframe-Info-Format)]
:::

---

### E.17 Thread List Format

To efficiently update the list of threads and their attributes, [GDB]' packet (see [qXfer threads read](General-Query-Packets.html#qXfer-threads-read)) and obtains the XML document with the following structure:

::: smallexample

```bash
<?xml version="1.0"?>
<threads>
    <thread id="id" core="0" name="name">
    ... description ...
    </thread>
</threads>
```

:::

Each '`thread`' attribute, if present, is a hex encoded representation of the thread handle.
