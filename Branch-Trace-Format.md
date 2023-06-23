---
description: Branch Trace Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Branch Trace Format (Debugging with GDB)
lang: en
resource-type: document
title: Branch Trace Format (Debugging with GDB)
---
::: header
Next: [Branch Trace Configuration Format](Branch-Trace-Configuration-Format.html#Branch-Trace-Configuration-Format)]
:::

---

### E.19 Branch Trace Format

In order to display the branch trace of an inferior thread, [GDB] needs to obtain the list of branches. This list is represented as list of sequential code blocks that are connected via branches. The code in each block has been executed sequentially.

This list is obtained using the '`qXfer:btrace:read`' (see [qXfer btrace read](General-Query-Packets.html#qXfer-btrace-read)) packet and is an XML document.

[GDB] must be linked with the Expat library to support XML traceframe info discovery. See [Expat](Requirements.html#Expat).

The top-level structure of the document is shown below:

::: smallexample

```bash
<?xml version="1.0"?>
<!DOCTYPE btrace
          PUBLIC "+//IDN gnu.org//DTD GDB Branch Trace V1.0//EN"
                 "http://sourceware.org/gdb/gdb-btrace.dtd">
<btrace>
   block...
</btrace>
```

:::

- A block of sequentially executed instructions starting at `begin`:

  ::: smallexample

  ```bash
  <block begin="begin" end="end"/>
  ```

  :::

The formal DTD for the branch trace format is given below:

::: smallexample

```bash
<!ELEMENT btrace  (block* | pt) >
<!ATTLIST btrace  version CDATA   #FIXED "1.0">

<!ELEMENT block        EMPTY>
<!ATTLIST block        begin  CDATA   #REQUIRED
                       end    CDATA   #REQUIRED>

<!ELEMENT pt (pt-config?, raw?)>

<!ELEMENT pt-config (cpu?)>

<!ELEMENT cpu EMPTY>
<!ATTLIST cpu vendor   CDATA #REQUIRED
              family   CDATA #REQUIRED
              model    CDATA #REQUIRED
              stepping CDATA #REQUIRED>

<!ELEMENT raw (#PCDATA)>
```

:::
