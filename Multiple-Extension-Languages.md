---
description: Multiple Extension Languages (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Multiple Extension Languages (Debugging with GDB)
lang: en
resource-type: document
title: Multiple Extension Languages (Debugging with GDB)
---
::: header
Previous: [Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions)]
:::

---

### 23.6 Multiple Extension Languages

The Guile and Python extension languages do not share any state, and generally do not interfere with each other. There are some things to be aware of, however.

#### 23.6.1 Python comes first

Python was [GDB] maintains a list of enabled extension languages, and when it makes a call to an extension language, (say to pretty-print a value), it tries each in turn until an extension language indicates it has performed the request (e.g., has returned the pretty-printed form of a value). This extends to errors while performing such requests: If an error happens while, for example, trying to pretty-print an object then the error is reported and any following extension languages are not tried.
