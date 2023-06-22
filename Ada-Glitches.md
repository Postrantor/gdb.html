---
description: Ada Glitches (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Glitches (Debugging with GDB)
lang: en
resource-type: document
title: Ada Glitches (Debugging with GDB)
---
::: header
Previous: [Ada Source Character Set](Ada-Source-Character-Set.html#Ada-Source-Character-Set)]
:::

---

#### 15.4.10.11 Known Peculiarities of Ada Mode

Besides the omissions listed previously (see [Omissions from Ada](Omissions-from-Ada.html#Omissions-from-Ada)), we know of several problems with and limitations of Ada mode in [GDB], some of which will be fixed with planned future releases of the debugger and the GNU Ada compiler.

- Static constants that the compiler chooses not to materialize as objects in storage are invisible to the debugger.
- Named parameter associations in function argument lists are ignored (the argument lists are treated as positional).
- Many useful library packages are currently invisible to the debugger.
- Fixed-point arithmetic, conversions, input, and output is carried out using floating-point arithmetic, and may give results that only approximate those on the host machine.
- The GNAT compiler never generates the prefix `Standard` for any of the standard symbols defined by the Ada language. [GDB] knows about this: it will strip the prefix from names when you use it, and will never look for a name you have so qualified among local symbols, nor match against symbols in other packages or subprograms. If you have defined entities anywhere in your program other than parameters and local variables whose simple names match names in `Standard`, GNAT's lack of qualification here can cause confusion. When this happens, you can usually resolve the confusion by qualifying the problematic names with package `Standard` explicitly.

Older versions of the compiler sometimes generate erroneous debugging information, resulting in the debugger incorrectly printing the value of affected entities. In some cases, the debugger is able to work around an issue automatically. In other cases, the debugger is able to work around the issue, but the work-around has to be specifically enabled.

`set ada trust-PAD-over-XVS on`

:   Configure GDB to strictly follow the GNAT encoding when computing the value of Ada entities, particularly when `PAD` and `PAD___XVS` types are involved (see `ada/exp_dbug.ads` in the GCC sources for a complete description of the encoding used by the GNAT compiler). This is the default.

`set ada trust-PAD-over-XVS off`

:   This is related to the encoding using by the GNAT compiler. If [GDB] sometimes prints the wrong value for certain entities, changing `ada trust-PAD-over-XVS` to `off` activates a work-around which may fix the issue. It is always safe to set `ada trust-PAD-over-XVS` to `off`, but this incurs a slight performance penalty, so it is recommended to leave this setting to `on` unless necessary.

Internally, the debugger also relies on the compiler following a number of conventions known as the '`GNAT Encoding` in the GCC sources. This encoding describes how the debugging information should be generated for certain types. In particular, this convention makes use of *descriptive types*, which are artificial types generated purely to help the debugger.

These encodings were defined at a time when the debugging information format used was not powerful enough to describe some of the more complex types available in Ada. Since DWARF allows us to express nearly all Ada features, the long-term goal is to slowly replace these descriptive types by their pure DWARF equivalent. To facilitate that transition, a new maintenance option is available to force the debugger to ignore those descriptive types. It allows the user to quickly evaluate how well [GDB] works without them.

`maintenance ada set ignore-descriptive-types [on|off]`

Control whether the debugger should ignore descriptive types. The default is not to ignore descriptives types (`off`).

`maintenance ada show ignore-descriptive-types`

Show if descriptive types are ignored by [GDB].

---

::: header
Previous: [Ada Source Character Set](Ada-Source-Character-Set.html#Ada-Source-Character-Set)]
:::
