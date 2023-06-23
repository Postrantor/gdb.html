---
description: Bug Criteria (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Bug Criteria (Debugging with GDB)
lang: en
resource-type: document
title: Bug Criteria (Debugging with GDB)
---
::: header
Next: [Bug Reporting](Bug-Reporting.html#Bug-Reporting)]
:::

---

### 32.1 Have You Found a Bug?

If you are not sure whether you have found a bug, here are some guidelines:

- bug. Reliable debuggers never crash.
- produces an error message for valid input, that is a bug. (Note that if you're cross debugging, the problem may also be somewhere in the connection to the target.)
- does not produce an error message for invalid input, that is a bug. However, you should note that your idea of "invalid input" might be our idea of "an extension" or "support for traditional practice".
- If you are an experienced user of debugging tools, your suggestions for improvement of [GDB] are welcome in any case.
