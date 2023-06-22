---
description: Branch Trace Configuration Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Branch Trace Configuration Format (Debugging with GDB)
lang: en
resource-type: document
title: Branch Trace Configuration Format (Debugging with GDB)
---
::: header
Previous: [Branch Trace Format](Branch-Trace-Format.html#Branch-Trace-Format)]
:::

---

### E.20 Branch Trace Configuration Format

For each inferior thread, [GDB]' (see [qXfer btrace-conf read](General-Query-Packets.html#qXfer-btrace_002dconf-read)) packet.

The configuration describes the branch trace format and configuration settings for that format. The following information is described:

`bts`

:   This thread uses the *Branch Trace Store* (BTS) format.

```
`size`

:   The size of the BTS ring buffer in bytes.
```

`pt`

:   This thread uses the *Intel Processor Trace* (Intel PT) format.

```
`size`

:   The size of the Intel PT ring buffer in bytes.
```

[GDB] must be linked with the Expat library to support XML branch trace configuration discovery. See [Expat](Requirements.html#Expat).

The formal DTD for the branch trace configuration format is given below:

::: smallexample

```bash
<!ELEMENT btrace-conf  (bts?, pt?)>
<!ATTLIST btrace-conf    version CDATA   #FIXED "1.0">

<!ELEMENT bts    EMPTY>
<!ATTLIST bts    size    CDATA   #IMPLIED>

<!ELEMENT pt EMPTY>
<!ATTLIST pt size    CDATA   #IMPLIED>
```

:::
