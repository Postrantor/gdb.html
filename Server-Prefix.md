---
description: Server Prefix (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Server Prefix (Debugging with GDB)
lang: en
resource-type: document
title: Server Prefix (Debugging with GDB)
---
::: header
Next: [Prompting](Prompting.html#Prompting)]
:::

---

### 28.2 The Server Prefix

If you prefix a command with '`server `'s notion of which command to repeat if RET is pressed on a line by itself. This means that commands can be run behind a user's back by a front-end in a transparent manner.

The `server ` prefix does not affect the recording of values into the value history; to print a value without recording it into the value history, use the `output` command instead of the `print` command.

Using this prefix also disables confirmation requests (see [confirmation requests](Messages_002fWarnings.html#confirmation-requests)).
