---
description: Connections In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Connections In Python (Debugging with GDB)
lang: en
resource-type: document
title: Connections In Python (Debugging with GDB)
---
::: header
Next: [TUI Windows In Python](TUI-Windows-In-Python.html#TUI-Windows-In-Python)]
:::

---

#### 23.3.2.36 Connections In Python

[GDB]'. See [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs).

Connections in [GDB] are represented as instances of `gdb.TargetConnection`, or as one of its sub-classes. To get a list of all connections use `gdb.connections` (see [gdb.connections](Basic-Python.html#gdbpy_005fconnections)).

To get the connection for a single `gdb.Inferior` read its `gdb.Inferior.connection` attribute (see [gdb.Inferior.connection](Inferiors-In-Python.html#gdbpy_005finferior_005fconnection)).

Currently there is only a single sub-class of `gdb.TargetConnection`, `gdb.RemoteTargetConnection`, however, additional sub-classes may be added in future releases of [GDB]. As a result you should avoid writing code like:

::: smallexample

```bash
conn = gdb.selected_inferior().connection
if type(conn) is gdb.RemoteTargetConnection:
  print("This is a remote target connection")
```

:::

as this may fail when more connection types are added. Instead, you should write:

::: smallexample

```bash
conn = gdb.selected_inferior().connection
if isinstance(conn, gdb.RemoteTargetConnection):
  print("This is a remote target connection")
```

:::

A `gdb.TargetConnection` has the following method:

Function: **TargetConnection.is_valid** *()*

:   Return `True` if the `gdb.TargetConnection` object is valid, `False` if not. A `gdb.TargetConnection` will become invalid if the connection no longer exists within [GDB], this might happen when no inferiors are using the connection, but could be delayed until the user replaces the current target.

```
Reading any of the `gdb.TargetConnection` properties will throw an exception if the connection is invalid.
```

A `gdb.TargetConnection` has the following read-only properties:

Variable: **TargetConnection.num**

:   An integer assigned by [GDB]' column of the `info connections` command output (see [info connections](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)).

```
<!-- -->
```

Variable: **TargetConnection.type**

:   A string that describes what type of connection this is. This string will be one of the valid names that can be passed to the `target` command (see [target command](Target-Commands.html#Target-Commands)).

```
<!-- -->
```

Variable: **TargetConnection.description**

:   A string that gives a short description of this target type. This is the same string that is displayed in the '`Description`' column of the `info connection` command output (see [info connections](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)).

```
<!-- -->
```

Variable: **TargetConnection.details**

:   An optional string that gives additional information about this connection. This attribute can be `None` if there are no additional details for this connection.

```
An example of a connection type that might have additional details is the '`remote`' that was used to connect to the remote target.
```

The `gdb.RemoteTargetConnection` class is a sub-class of `gdb.TargetConnection`, and is used to represent '`remote`' connections. In addition to the attributes and methods available from the `gdb.TargetConnection` base class, a `gdb.RemoteTargetConnection` has the following method:

Function: **RemoteTargetConnection.send_packet** *(packet)*

:   This method sends `packet` should either be a `bytes` object, or a `Unicode` string.

```
If `packet` codec. If the string can't be encoded then an `UnicodeError` is raised.

If `packet` is empty then a `ValueError` is raised.

The response is returned as a `bytes` object. For Python 3 if it is known that the response can be represented as a string then this can be decoded from the buffer. For example, if it is known that the response is an [ASCII] string:

::: smallexample
``` smallexample
remote_connection.send_packet("some_packet").decode("ascii")
```

:::

In Python 2 `bytes` and `str` are aliases, so the result is already a string, if the response includes non-printable characters, or null characters, then these will be present in the result, care should be taken when processing the result to handle this case.

The prefix, suffix, and checksum (as required by the remote serial protocol) are automatically added to the outgoing packet, and removed from the incoming packet before the contents of the reply are returned.

This is equivalent to the `maintenance packet` command (see [maint packet](Maintenance-Commands.html#maint-packet)).

```

---

::: header
Next: [TUI Windows In Python](TUI-Windows-In-Python.html#TUI-Windows-In-Python)]
:::
```
