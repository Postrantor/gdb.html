---
description: Inferiors Connections and Programs (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Inferiors Connections and Programs (Debugging with GDB)
lang: en
resource-type: document
title: Inferiors Connections and Programs (Debugging with GDB)
---
::: header
Next: [Threads](Threads.html#Threads)]
:::

---

### 4.9 Debugging Multiple Inferiors Connections and Programs

[GDB] may even let you debug several programs simultaneously on different remote systems. In the most general case, you can have multiple threads of execution in each of multiple processes, launched from multiple executables, running on different machines.

[GDB] represents the state of each program execution with an object called an *inferior*. An inferior typically corresponds to a process, but is more general and applies also to targets that do not have processes. Inferiors may be created before a process runs, and may be retained after a process exits. Inferiors have unique identifiers that are different from process ids. Usually each inferior will also have its own distinct address space, although some embedded targets may have several inferiors running in different parts of a single address space. Each inferior may in turn have multiple threads running in it.

The commands `info inferiors` and `info connections`, which will be introduced below, accept a space-separated *ID list* as their argument specifying one or more elements on which to operate. A list element can be either a single non-negative number, like '`5`'.

To find out what inferiors exist at any moment, use `info inferiors`:

`info inferiors`

Print a list of all inferiors currently being managed by [GDB]... can be used to limit the display to just the requested inferiors.

[GDB] displays for each inferior (in this order):

1. the inferior number assigned by [GDB]
2. the target system's inferior identifier
3. the target connection the inferior is bound to, including the unique connection number assigned by [GDB], and the protocol used by the connection.
4. the name of the executable the inferior is running.

An asterisk '`*` inferior number indicates the current inferior.

For example,

::: smallexample

```bash
(gdb) info inferiors
  Num  Description       Connection                      Executable
* 1    process 3401      1 (native)                      goodbye
  2    process 2307      2 (extended-remote host:10000)  hello
```

:::

To get information about the current inferior, use `inferior`:

`inferior`

Shows information about the current inferior.

For example,

::: smallexample

```bash
(gdb) inferior
[Current inferior is 1 [process 3401] (helloworld)]
```

:::

To find out what open target connections exist at any moment, use `info connections`:

`info connections`

Print a list of all open target connections currently being managed by [GDB]... can be used to limit the display to just the requested connections.

[GDB] displays for each connection (in this order):

1. the connection number assigned by [GDB].
2. the protocol used by the connection.
3. a textual description of the protocol used by the connection.

An asterisk '`*`' preceding the connection number indicates the connection of the current inferior.

For example,

::: smallexample

```bash
(gdb) info connections
  Num  What                        Description
* 1    extended-remote host:10000  Extended remote serial target in gdb-specific protocol
  2    native                      Native process
  3    core                        Local core dump file
```

:::

To switch focus between inferiors, use the `inferior` command:

`inferior infno`

Make inferior number `infno`' display.

The debugger convenience variable '`$_inferior`' contains the number of the current inferior. You may find this useful in writing breakpoint conditional expressions, command scripts, and so forth. See [Convenience Variables](Convenience-Vars.html#Convenience-Vars), for general information on convenience variables.

You can get multiple executables into a debugging session via the `add-inferior` and `clone-inferior` commands. On some systems [GDB] can add inferiors to the debug session automatically by following calls to `fork` and `exec`. To remove inferiors from the debugging session use the `remove-inferiors` command.

`add-inferior [ -copies n ] [ -exec executable ] [-no-connection ]`

Adds `n` defaults to 1. If no executable is specified, the inferiors begins empty, with no program. You can still assign or change the program assigned to the inferior at any time by using the `file` command with the executable name as its argument.

By default, the new inferior begins connected to the same target connection as the current inferior. For example, if the current inferior was connected to `gdbserver` with `target remote`, then the new inferior will be connected to the same `gdbserver` instance. The '`-no-connection`' option starts the new inferior with no connection yet. You can then for example use the `target remote` command to connect to some other `gdbserver` instance, use `run` to spawn a local program, etc.

`clone-inferior [ -copies n ] [ infno ]`

Adds `n` properties from the current inferior to the new one. It also propagates changes the user made to environment variables using the `set environment` and `unset environment` commands. This is a convenient command when you want to run another instance of the inferior you are debugging.

::: smallexample

```bash
(gdb) info inferiors
  Num  Description       Connection   Executable
* 1    process 29964     1 (native)   helloworld
(gdb) clone-inferior
Added inferior 2.
1 inferiors added.
(gdb) info inferiors
  Num  Description       Connection   Executable
* 1    process 29964     1 (native)   helloworld
  2    <null>            1 (native)   helloworld
```

:::

You can now simply switch focus to inferior 2 and run it.

`remove-inferiors infno…`

Removes the inferior or inferiors `infno`.... It is not possible to remove an inferior that is running with this command. For those, use the `kill` or `detach` command first.

To quit debugging one of the running inferiors that is not the current inferior, you can either detach from it by using the `detach inferior` command (allowing it to run independently), or kill it using the `kill inferiors` command:

`detach inferior infno…`

Detach from the inferior or inferiors identified by [GDB]'.

`kill inferiors infno…`

Kill the inferior or inferiors identified by [GDB]'.

After the successful completion of a command such as `detach`, `detach inferiors`, `kill` or `kill inferiors`, or after a normal process exit, the inferior is still valid and listed with `info inferiors`, ready to be restarted.

To be notified when inferiors are started or exit under [GDB]'s control use `set print inferior-events`:

`set print inferior-events`

`set print inferior-events on`

`set print inferior-events off`

The `set print inferior-events` command allows you to enable or disable printing of messages when [GDB] notices that new inferiors have started or that inferiors have exited or have been detached. By default, these messages will be printed.

`show print inferior-events`

Show whether messages will be printed when [GDB] detects that inferiors have started, exited or have been detached.

Many commands will work the same with multiple programs as with a single program: e.g., `print myglobal` will simply display the value of `myglobal` in the current inferior.

Occasionally, when debugging [GDB] itself, it may be useful to get more info about the relationship of inferiors, programs, address spaces in a debug session. You can do that with the `maint info program-spaces` command.

`maint info program-spaces`

Print a list of all program spaces currently being managed by [GDB].

[GDB] displays for each program space (in this order):

1. the program space number assigned by [GDB]
2. the name of the executable loaded into the program space, with e.g., the `file` command.
3. the name of the core file loaded into the program space, with e.g., the `core-file` command.

An asterisk '`*` program space number indicates the current program space.

In addition, below each program space line, [GDB] prints extra information that isn't suitable to display in tabular form. For example, the list of inferiors bound to the program space.

::: smallexample

```bash
(gdb) maint info program-spaces
  Id   Executable        Core File
* 1    hello
  2    goodbye
        Bound inferiors: ID 1 (process 21561)
```

:::

Here we can see that no inferior is running the program `hello`, while `process 21561` is running the program `goodbye`. On some targets, it is possible that multiple inferiors are bound to the same program space. The most common example is that of debugging both the parent and child processes of a `vfork` call. For example,

::: smallexample

```bash
(gdb) maint info program-spaces
  Id   Executable        Core File
* 1    vfork-test
        Bound inferiors: ID 2 (process 18050), ID 1 (process 18045)
```

:::

Here, both inferior 2 and inferior 1 are running in the same program space as a result of inferior 1 having executed a `vfork` call.

---

::: header
Next: [Threads](Threads.html#Threads)]
:::
