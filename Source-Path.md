---
tip: translate by openai@2023-06-23 16:22:28
...
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

> 可执行程序有时不会记录它们编译时所使用的源文件的目录，只记录文件名。即使它们记录了，目录也可能在编译和调试会话之间移动。[GDB]需要源文件时，它会按照列表中的顺序，尝试搜索所有目录，直到找到名称匹配的文件为止。


For example, suppose an executable references the file `/usr/src/foo-1.0/lib/foo.c` would look for the source file in the following locations:

> 例如，假设一个可执行文件引用文件`/usr/src/foo-1.0/lib/foo.c`，它将在以下位置查找源文件：


1. `/usr/src/foo-1.0/lib/foo.c`

> `/usr/src/foo-1.0/lib/foo.c`

2. `/mnt/cross/usr/src/foo-1.0/lib/foo.c`

> `2. /mnt/cross/usr/src/foo-1.0/lib/foo.c`
3. `/mnt/cross/foo.c`


If the source file is not present at any of the above locations then an error is printed. [GDB].

> 如果源文件不在以上任何位置，则会打印一个错误[GDB]。


Plain file names, relative file names with leading directories, file names containing dots, etc. are all treated as described above, except that non-absolute file names are not looked up literally. If the *source path* is `/mnt/cross` will search in the following locations:

> 简单的文件名、带有前导目录的相对文件名、包含点的文件名等，都按照上述方式处理，但非绝对文件名不会按字面意思查找。如果*源路径*是`/mnt/cross`，将会搜索以下位置：


1. `/mnt/cross/../lib/foo.c`

> /mnt/cross/../lib/foo.c
2. `/mnt/cross/foo.c`


The *source path* will always include two special entries '`$cdir`', these refer to the compilation directory (if one is recorded) and the current working directory respectively.

> 源路径总会包含两个特殊条目 '`$cdir`'，这些分别指编译目录（如果有记录）和当前工作目录。

'`$cdir`' is ignored.


'`$cwd` session, while the latter is immediately expanded to the current directory at the time you add an entry to the source path.

> `'$cwd'会话，当您向源路径添加条目时，后者会立即展开为当前目录。


If a compilation directory is recorded in the debug information, and [GDB] will combine the compilation directory and the filename, and then search for the source file again using the *source path*.

> 如果调试信息中记录了编译目录，[GDB]会将编译目录和文件名结合起来，然后使用*源路径*再次搜索源文件。


For example, if the executable records the source file as `/usr/src/foo-1.0/lib/foo.c` will search for the source file in the following locations:

> 例如，如果可执行文件记录源文件为`/usr/src/foo-1.0/lib/foo.c`，将会在以下位置搜索源文件：


1. `/usr/src/foo-1.0/lib/foo.c`

> `/usr/src/foo-1.0/lib/foo.c`

2. `/mnt/cross/usr/src/foo-1.0/lib/foo.c`

> 2. `/mnt/cross/usr/src/foo-1.0/lib/foo.c` 
2. `/mnt/cross/usr/src/foo-1.0/lib/foo.c`

3. `/project/build/usr/src/foo-1.0/lib/foo.c`

> `3. /项目/构建/usr/src/foo-1.0/lib/foo.c`

4. `/home/user/usr/src/foo-1.0/lib/foo.c`

> `/home/用户/usr/src/foo-1.0/lib/foo.c`

5. `/mnt/cross/project/build/usr/src/foo-1.0/lib/foo.c`

> `5. /mnt/cross/项目/构建/usr/src/foo-1.0/lib/foo.c`

6. `/project/build/project/build/usr/src/foo-1.0/lib/foo.c`

> 6. `/项目/构建/项目/构建/usr/src/foo-1.0/lib/foo.c`

7. `/home/user/project/build/usr/src/foo-1.0/lib/foo.c`

> /home/用户/项目/构建/usr/src/foo-1.0/lib/foo.c
8. `/mnt/cross/foo.c`

9. `/project/build/foo.c`

> `9. `/项目/构建/foo.c`
10. `/home/user/foo.c`


If the file name in the previous example had been recorded in the executable as a relative path rather than an absolute path, then the first look up would not have occurred, but all of the remaining steps would be similar.

> 如果在前面的例子中，文件名被记录在可执行文件中的是相对路径而不是绝对路径，那么第一次查找就不会发生，但其余的步骤都是相似的。


When searching for source files on MS-DOS and MS-Windows, where absolute paths start with a drive letter (e.g. `C:/project/foo.c` will search in the following locations for the source file:

> 当在MS-DOS和MS-Windows上搜索源文件时，绝对路径以驱动器字母开头（例如`C:/project/foo.c`），将在以下位置搜索源文件：

1. `C:/project/foo.c`

2. `D:/mnt/cross/project/foo.c`

> `2. D:/mnt/cross/项目/foo.c`
3. `D:/mnt/cross/foo.c`

Note that the executable search path is *not* used to locate the source files.


Whenever you reset or rearrange the source path, [GDB] clears out any information it has cached about where source files are found and where each line is in the file.

> 每当你重置或重新排列源路径时，[GDB]就会清除它缓存的关于源文件位置以及每行在文件中的位置的任何信息。


When you start [GDB]', in that order. To add other directories, use the `directory` command.

> 当你开始使用GDB时，要添加其它目录，请使用`directory`命令。


The search path is used to find both program source files and [GDB]' command).

> 搜索路径用于查找程序源文件和[GDB]’命令。


In addition to the source path, [GDB] at the start of the directory part of the source file name, and uses that result instead of the original file name to look up the sources.

> 除了源路径，[GDB]在源文件名的目录部分开始，并使用该结果而不是原始文件名来查找源文件。


Using the previous example, suppose the `foo-1.0`. To define a source path substitution rule, use the `set substitute-path` command (see [set substitute-path](#set-substitute_002dpath)).

> 使用前面的例子，假设有`foo-1.0`。要定义源路径替换规则，请使用`set substitute-path`命令（参见[set substitute-path](#set-substitute_002dpath)）。


To avoid unexpected substitution results, a rule is applied only if the `from` either.

> 为了避免意外的替换结果，只有当`来自`时，才会应用规则。


In many cases, you can achieve the same result using the `directory` command. However, `set substitute-path` can be more efficient in the case where the sources are organized in a complex tree with multiple subdirectories. With the `directory` command, you need to add each subdirectory of your project. If you moved the entire tree while preserving its internal organization, then `set substitute-path` allows you to direct the debugger to all the sources with one single command.

> 在许多情况下，您可以使用`directory`命令获得相同的结果。但是，如果源文件组织在一个复杂的树状结构中，具有多个子目录，则`set substitute-path`可能更有效。使用`directory`命令，您需要添加项目的每个子目录。如果您在保留其内部组织的同时移动了整个树，那么`set substitute-path`允许您使用一个单一的命令将调试器指向所有源文件。

`set substitute-path` is also more than just a shortcut command. The source path is only used if the file at the original location no longer exists. On the other hand, `set substitute-path` modifies the debugger behavior to look at the rewritten location instead. So, if for any reason a source file that is not relevant to your executable is located at the original location, a substitution rule is the only method available to point [GDB] at the new location.


You can configure a default source path substitution rule by configuring [GDB], libraries or executables with debug information and corresponding source code are being moved together.

> 您可以通过配置[GDB]来配置默认的源路径替换规则，具有调试信息的库或可执行文件将与相应的源代码一起移动。

`directory dirname …`
`dir dirname …`


:   Add directory `dirname` searches it sooner.

> 添加目录“dirname”，可以更快地搜索它。

```
The special strings '`$cdir` searches them sooner.
```

`directory`


:   Reset the source path to its default value ('`$cdir:$cwd`' on Unix systems). This requires confirmation.

> 重置源路径到其默认值（在Unix系统上为'$cdir:$cwd'）。此操作需要确认。

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

> (gdb) 设置替换路径 /foo/bar /mnt/cross
```

:::

will tell [GDB] even though it was moved.

In the case when more than one substitution rule have been defined, the rules are evaluated one by one in the order where they have been defined. The first one matching, if any, is selected to perform the substitution.

For instance, if we had entered the following commands:

::: smallexample

```bash

(gdb) set substitute-path /usr/src/include /mnt/include

> (gdb) 设置替换路径 /usr/src/include /mnt/include

(gdb) set substitute-path /usr/src /mnt/src

> (gdb) 设置替换路径 /usr/src /mnt/src
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

> 如果您的源路径中充满了不再有兴趣的目录，[GDB]有时可能会导致混乱，找到错误的源版本。您可以按照以下步骤纠正情况：


1. Use `directory` with no argument to reset the source path to its default value.

> 使用没有参数的`directory`来重置源路径到其默认值。

2. Use `directory` with suitable arguments to reinstall the directories you want in the source path. You can add all the directories in one command.

> 使用带有合适参数的`directory`重新安装源路径中你想要的目录。你可以一次性添加所有目录。

---

::: header
Next: [Machine Code](Machine-Code.html#Machine-Code)]
:::
```
