---
description: Source Path (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Source Path (Debugging with GDB)
lang: en
resource-type: document
title: Source Path (Debugging with GDB)
---
::: header
Next: [Machine Code](Machine-Code.html#Machine-Code)]
:::

---

### 9.5 Specifying Source Directories

Executable programs sometimes do not record the directories of the source files from which they were compiled, just the names. Even when they do, the directories could be moved between the compilation and your debugging session. [GDB] wants a source file, it tries all the directories in the list, in the order they are present in the list, until it finds a file with the desired name.

For example, suppose an executable references the file `/usr/src/foo-1.0/lib/foo.c` would look for the source file in the following locations:

1. `/usr/src/foo-1.0/lib/foo.c`
2. `/mnt/cross/usr/src/foo-1.0/lib/foo.c`
3. `/mnt/cross/foo.c`

If the source file is not present at any of the above locations then an error is printed. [GDB].

Plain file names, relative file names with leading directories, file names containing dots, etc. are all treated as described above, except that non-absolute file names are not looked up literally. If the *source path* is `/mnt/cross` will search in the following locations:

1. `/mnt/cross/../lib/foo.c`
2. `/mnt/cross/foo.c`

The *source path* will always include two special entries '`$cdir`', these refer to the compilation directory (if one is recorded) and the current working directory respectively.

'`$cdir`' is ignored.

'`$cwd` session, while the latter is immediately expanded to the current directory at the time you add an entry to the source path.

If a compilation directory is recorded in the debug information, and [GDB] will combine the compilation directory and the filename, and then search for the source file again using the *source path*.

For example, if the executable records the source file as `/usr/src/foo-1.0/lib/foo.c` will search for the source file in the following locations:

1. `/usr/src/foo-1.0/lib/foo.c`
2. `/mnt/cross/usr/src/foo-1.0/lib/foo.c`
3. `/project/build/usr/src/foo-1.0/lib/foo.c`
4. `/home/user/usr/src/foo-1.0/lib/foo.c`
5. `/mnt/cross/project/build/usr/src/foo-1.0/lib/foo.c`
6. `/project/build/project/build/usr/src/foo-1.0/lib/foo.c`
7. `/home/user/project/build/usr/src/foo-1.0/lib/foo.c`
8. `/mnt/cross/foo.c`
9. `/project/build/foo.c`
10. `/home/user/foo.c`

If the file name in the previous example had been recorded in the executable as a relative path rather than an absolute path, then the first look up would not have occurred, but all of the remaining steps would be similar.

When searching for source files on MS-DOS and MS-Windows, where absolute paths start with a drive letter (e.g. `C:/project/foo.c` will search in the following locations for the source file:

1. `C:/project/foo.c`
2. `D:/mnt/cross/project/foo.c`
3. `D:/mnt/cross/foo.c`

Note that the executable search path is *not* used to locate the source files.

Whenever you reset or rearrange the source path, [GDB] clears out any information it has cached about where source files are found and where each line is in the file.

When you start [GDB]', in that order. To add other directories, use the `directory` command.

The search path is used to find both program source files and [GDB]' command).

In addition to the source path, [GDB] at the start of the directory part of the source file name, and uses that result instead of the original file name to look up the sources.

Using the previous example, suppose the `foo-1.0`. To define a source path substitution rule, use the `set substitute-path` command (see [set substitute-path](#set-substitute_002dpath)).

To avoid unexpected substitution results, a rule is applied only if the `from` either.

In many cases, you can achieve the same result using the `directory` command. However, `set substitute-path` can be more efficient in the case where the sources are organized in a complex tree with multiple subdirectories. With the `directory` command, you need to add each subdirectory of your project. If you moved the entire tree while preserving its internal organization, then `set substitute-path` allows you to direct the debugger to all the sources with one single command.

`set substitute-path` is also more than just a shortcut command. The source path is only used if the file at the original location no longer exists. On the other hand, `set substitute-path` modifies the debugger behavior to look at the rewritten location instead. So, if for any reason a source file that is not relevant to your executable is located at the original location, a substitution rule is the only method available to point [GDB] at the new location.

You can configure a default source path substitution rule by configuring [GDB], libraries or executables with debug information and corresponding source code are being moved together.

`directory dirname …`
`dir dirname …`

:   Add directory `dirname` searches it sooner.

```
The special strings '`$cdir` searches them sooner.
```

`directory`

:   Reset the source path to its default value ('`$cdir:$cwd`' on Unix systems). This requires confirmation.

`set directories path-list`

:

```
Set the source path to `path-list`' are added if missing.
```

`show directories`

:

```
Print the source path: show which directories it contains.


```

`set substitute-path from to`

:

```
Define a source path substitution rule, and add it at the end of the current list of existing substitution rules. If a rule with the same `from` was already defined, then the old rule is also deleted.

For example, if the file `/foo/bar/baz.c`, then the command

::: smallexample
``` smallexample
(gdb) set substitute-path /foo/bar /mnt/cross
```

:::

will tell [GDB] even though it was moved.

In the case when more than one substitution rule have been defined, the rules are evaluated one by one in the order where they have been defined. The first one matching, if any, is selected to perform the substitution.

For instance, if we had entered the following commands:

::: smallexample

```bash
(gdb) set substitute-path /usr/src/include /mnt/include
(gdb) set substitute-path /usr/src /mnt/src
```

:::

[GDB].

```

`unset substitute-path [path]`

:   

```

If a path is specified, search the current list of substitution rules for a rule that would rewrite that path. Delete that rule if found. A warning is emitted by the debugger if no rule could be found.

If no path is specified, then all substitution rules are deleted.

```

`show substitute-path [path]`

:   

```

If a path is specified, then print the source path substitution rule which would rewrite that path, if any.

If no path is specified, then print all existing source path substitution rules.

```

If your source path is cluttered with directories that are no longer of interest, [GDB] may sometimes cause confusion by finding the wrong versions of source. You can correct the situation as follows:

1. Use `directory` with no argument to reset the source path to its default value.
2. Use `directory` with suitable arguments to reinstall the directories you want in the source path. You can add all the directories in one command.

---

::: header
Next: [Machine Code](Machine-Code.html#Machine-Code)]
:::
```
