---
description: Traceframe Info Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Traceframe Info Format (Debugging with GDB)
lang: en
resource-type: document
title: Traceframe Info Format (Debugging with GDB)
---
::: header
Next: [Branch Trace Format](Branch-Trace-Format.html#Branch-Trace-Format)]
:::

---

### E.18 Traceframe Info Format

To be able to know which objects in the inferior can be examined when inspecting a tracepoint hit, [GDB] needs to obtain the list of memory ranges, registers and trace state variables that have been collected in a traceframe.

This list is obtained using the '`qXfer:traceframe-info:read`' (see [qXfer traceframe info read](General-Query-Packets.html#qXfer-traceframe-info-read)) packet and is an XML document.

[GDB] must be linked with the Expat library to support XML traceframe info discovery. See [Expat](Requirements.html#Expat).

The top-level structure of the document is shown below:

::: smallexample

```bash
<?xml version="1.0"?>
<!DOCTYPE traceframe-info
          PUBLIC "+//IDN gnu.org//DTD GDB Memory Map V1.0//EN"
                 "http://sourceware.org/gdb/gdb-traceframe-info.dtd">
<traceframe-info>
   block...
</traceframe-info>
```

:::

Each traceframe block can be either:

- A region of collected memory starting at `addr` bytes from there:

  ::: smallexample

  ```bash
  <memory start="addr" length="length"/>
  ```

  :::
- A block indicating trace state variable numbered `number` has been collected:

  ::: smallexample

  ```bash
  <tvar id="number"/>
  ```

  :::

The formal DTD for the traceframe info format is given below:

::: smallexample

```bash
<!ELEMENT traceframe-info  (memory | tvar)* >
<!ATTLIST traceframe-info  version CDATA   #FIXED  "1.0">

<!ELEMENT memory        EMPTY>
<!ATTLIST memory        start   CDATA   #REQUIRED
                        length  CDATA   #REQUIRED>
<!ELEMENT tvar>
<!ATTLIST tvar          id      CDATA   #REQUIRED>
```

:::
