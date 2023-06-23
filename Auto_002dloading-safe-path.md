---
tip: translate by openai@2023-06-23 11:53:14
...
---
description: Auto-loading safe path (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Auto-loading safe path (Debugging with GDB)
lang: en
resource-type: document
title: Auto-loading safe path (Debugging with GDB)
---
::: header
Next: [Auto-loading verbose mode](Auto_002dloading-verbose-mode.html#Auto_002dloading-verbose-mode)]
:::

---

#### 22.8.3 Security restriction for auto-loading


As the files of inferior can come from untrusted source (such as submitted by an application user) [GDB]' setting to list directories trusted for loading files not explicitly requested by user. Each directory can also be a shell wildcard pattern.

> 随着文件的来源可能来自不受信任的源（如由应用程序用户提交）[GDB]，设置列出受信任的目录以加载未明确请求的文件。每个目录也可以是shell通配符模式。


If the path is not set properly you will see a warning and the file will not get loaded:

> 如果路径没有正确设置，你会看到警告，文件将无法加载。

::: smallexample

```bash
$ ./gdb -q ./gdb
Reading symbols from /home/user/gdb/gdb...
warning: File "/home/user/gdb/gdb-gdb.gdb" auto-loading has been
         declined by your `auto-load safe-path' set
         to "$debugdir:$datadir/auto-load".
warning: File "/home/user/gdb/gdb-gdb.py" auto-loading has been
         declined by your `auto-load safe-path' set
         to "$debugdir:$datadir/auto-load".
```

:::


To instruct [GDB] like this:

> 按照这样来指导GDB：

::: smallexample

```bash
$ gdb -q -iex "set auto-load safe-path /home/user/gdb" ./gdb
```

:::


The list of trusted directories is controlled by the following commands:

> 以下命令控制受信任目录的列表：

`set auto-load safe-path [directories]`


Set the list of directories (and their subdirectories) trusted for automatic loading and execution of scripts. You can also enter a specific trusted file. Each directory can also be a shell wildcard pattern; wildcards do not match directory separator - see `FNM_PATHNAME` for system function `fnmatch` (see [fnmatch](http://www.gnu.org/software/libc/manual/html_node/Wildcard-Matching.html#Wildcard-Matching) in GNU C Library Reference Manual). If you omit `directories` compilation.

> 设置可信任的目录（及其子目录）列表，用于自动加载和执行脚本。您也可以输入一个特定的可信任文件。每个目录也可以是shell通配符模式；通配符不匹配目录分隔符 - 请参阅系统函数`fnmatch`的`FNM_PATHNAME`（参见GNU C库参考手册中的[fnmatch](http://www.gnu.org/software/libc/manual/html_node/Wildcard-Matching.html#Wildcard-Matching)）。如果省略`directories`编译。


The list of directories uses path separator ('`:`' on MS-Windows and MS-DOS) to separate directories, similarly to the `PATH` environment variable.

> 目录列表使用路径分隔符（在MS-Windows和MS-DOS上为“：”）来分隔目录，类似于`PATH`环境变量。

`show auto-load safe-path`


Show the list of directories trusted for automatic loading and execution of scripts.

> 显示可信任的自动加载和执行脚本的目录列表。

`add-auto-load-safe-path`


Add an entry (or list of entries) to the list of directories trusted for automatic loading and execution of scripts. Multiple entries may be delimited by the host platform path separator in use.

> 向可自动加载和执行脚本的受信任目录列表中添加一个（或多个）条目。多个条目可以使用当前主机平台的路径分隔符进行分隔。


This variable defaults to what `--with-auto-load-dir` has been configured to (see [with-auto-load-dir](objfile_002dgdbdotext-file.html#with_002dauto_002dload_002ddir)). `$debugdir`.

> 这个变量默认为`--with-auto-load-dir`已配置的值（请参阅[with-auto-load-dir](objfile_002dgdbdotext-file.html#with_002dauto_002dload_002ddir)）。`$debugdir`。


Setting this variable to `/`. This variable is supposed to be set to the system directories writable by the system superuser only. Users can add their source directories in init files in their home directories (see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File)). See also deprecated init file in the current directory (see [Init File in the Current Directory during Startup](Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup)).

> 设置此变量为"/”。此变量应设置为仅系统超级用户可写入的系统目录。用户可以在其主目录中的初始文件中添加其来源目录（参见[主目录初始文件]（Initialization-Files.html#Home-Directory-Init-File））。另请参阅启动时当前目录中的弃用初始文件（参见[启动时当前目录中的初始文件]（Initialization-Files.html#Init-File-in-the-Current-Directory-during-Startup））。


To force [GDB] to load the files it declined to load in the previous example, you could use one of the following ways:

> 要强制GDB加载前面例子中拒绝加载的文件，可以使用以下方法之一：

`~/.gdbinit`'


:   Specify this trusted directory (or a file) as additional component of the list. You have to specify also any existing directories displayed by by '`show auto-load safe-path`' in this example).

> 指定此受信任的目录（或文件）为此列表的附加组件。您还必须指定“show auto-load safe-path”在此示例中显示的任何现有目录。


[gdb -iex \"set auto-load safe-path /usr:/bin:\~/src/gdb\" ...]

> [gdb -iex "设置自动加载安全路径/usr：/bin：~/src/gdb" ...]


:   Specify this directory as in the previous case but just for a single [GDB] session.

> 指定此目录与之前的情况相同，但仅限于单个[GDB]会话。


[gdb -iex \"set auto-load safe-path /\" ...]

> [gdb -iex "设置自动加载安全路径/"...]


:   Disable auto-loading safety for a single [GDB] session will come from trusted sources.

> 禁用单个[GDB]会话的自动加载安全性，来自可信源。


[./configure \--without-auto-load-safe-path]

> [./configure \--without-auto-load-safe-path]

[./configure \--无自动加载安全路径]


:   During compilation of [GDB] come from trusted sources.

> 在编译[GDB]时，应从可信的来源获取。


On the other hand you can also explicitly forbid automatic files loading which also suppresses any such warning messages:

> 另一方面，您也可以明确禁止自动文件加载，这也会抑制任何此类警告消息：


[gdb -iex \"set auto-load no\" ...]

> [gdb -iex \"设置自动加载为否\" ...]


:   You can use [GDB] session.

> 你可以使用[GDB]会话。

`~/.gdbinit`'


:   Disable auto-loading globally for the user (see [Home Directory Init File](Initialization-Files.html#Home-Directory-Init-File)). While it is improbable, you could also use system init file instead (see [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)).

> 在用户级别全局禁用自动加载（参见[主目录初始文件](Initialization-Files.html#Home-Directory-Init-File)）。虽然不太可能，你也可以使用系统初始文件（参见[系统级配置](System_002dwide-configuration.html#System_002dwide-configuration)）。


This setting applies to the file names as entered by user. If no entry matches [GDB] already canonicalizes most of the filenames on its own before starting the comparison so a canonical form of directories is recommended to be entered.

> 此设置适用于用户输入的文件名。如果没有匹配项，[GDB]会自动在开始比较之前对大多数文件名进行规范化，因此建议输入规范化的目录。

---

::: header
Next: [Auto-loading verbose mode](Auto_002dloading-verbose-mode.html#Auto_002dloading-verbose-mode)]
:::
