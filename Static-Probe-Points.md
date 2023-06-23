---
description: Static Probe Points (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Static Probe Points (Debugging with GDB)
lang: en
resource-type: document
title: Static Probe Points (Debugging with GDB)
---
::: header
Next: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::

---

#### 5.1.10 Static Probe Points

[GDB] supports *SDT* probes in the code. SDT stands for Statically Defined Tracing, and the probes are designed to have a tiny runtime code and data footprint, and no dynamic relocations.

Currently, the following types of probes are supported on ELF-compatible systems:

- `SystemTap` ([http://sourceware.org/systemtap/](http://sourceware.org/systemtap/)) SDT probes[^5^](#FOOT5).
- `DTrace` ([http://oss.oracle.com/projects/DTrace](http://oss.oracle.com/projects/DTrace)) USDT probes. `DTrace` probes are usable from C and C++ languages.

Some `SystemTap` probes have an associated semaphore variable; for instance, this happens automatically if you defined your probe using a DTrace-style `.d` will not automatically set the semaphore. `DTrace` probes do not support semaphores.

You can examine the available static static probes using `info probes`, with optional arguments:

`info probes [type] [provider [name [objfile]]]`

If given, `type` is either `stap` for listing `SystemTap` probes or `dtrace` for listing `DTrace` probes. If omitted all probes are listed regardless of their types.

If given, `provider` is a regular expression used to match against provider names when selecting which probes to list. If omitted, probes by all probes from all providers are listed.

If given, `name` is a regular expression to match against probe names when selecting which probes to list. If omitted, probe names are not considered when deciding whether to display them.

If given, `objfile` is a regular expression used to select which object files (executable or shared libraries) to examine. If not given, all object files are considered.

`info probes all`

List the available static probes, from all types.

Some probe points can be enabled and/or disabled. The effect of enabling or disabling a probe depends on the type of probe being handled. Some `DTrace` probes can be enabled or disabled, but `SystemTap` probes cannot be disabled.

You can enable (or disable) one or more probes using the following commands, with optional arguments:

`enable probes [provider [name [objfile]]]`

If given, `provider` is a regular expression used to match against provider names when selecting which probes to enable. If omitted, all probes from all providers are enabled.

If given, `name` is a regular expression to match against probe names when selecting which probes to enable. If omitted, probe names are not considered when deciding whether to enable them.

If given, `objfile` is a regular expression used to select which object files (executable or shared libraries) to examine. If not given, all object files are considered.

`disable probes [provider [name [objfile]]]`

See the `enable probes` command above for a description of the optional arguments accepted by this command.

A probe may specify up to twelve arguments. These are available at the point at which the probe is defined---that is, when the current PC is at the probe's location. The arguments are available using the convenience variables (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) `$_probe_arg0`...`$_probe_arg11`. In `SystemTap` probes each probe argument is an integer of the appropriate size; types are not preserved. In `DTrace` probes types are preserved provided that they are recognized as such by [GDB]; otherwise the value of the probe argument will be a long integer. The convenience variable `$_probe_argc` holds the number of arguments at the current probe point.

These variables are always available, but attempts to access them at any location other than a probe point will cause [GDB] to give an error message.

::: footnote

---

#### Footnotes

### [(5)](#DOCF5)

See [http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps](http://sourceware.org/systemtap/wiki/AddingUserSpaceProbingToApps) for more information on how to add `SystemTap` SDT probes in your applications.

### [(6)](#DOCF6)

See [http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation](http://sourceware.org/systemtap/wiki/UserSpaceProbeImplementation) for a good reference on how the SDT probes are implemented.
:::

---

::: header
Next: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::
