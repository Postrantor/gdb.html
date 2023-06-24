---
tip: translate by openai@2023-06-23 19:21:07
...
---
description: Compiling and Injecting Code (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Compiling and Injecting Code (Debugging with GDB)
lang: en
resource-type: document
title: Compiling and Injecting Code (Debugging with GDB)
---
::: header
Previous: [Patching](Patching.html#Patching)]
:::

---

### 17.7 Compiling and injecting code in [GDB]


[GDB] must be installed for this functionality to be enabled. This functionality is implemented with the following commands.

> 此功能需要安装[GDB]才能启用。这个功能使用以下命令实现。

`compile code source-code`

`compile code -raw -- source-code`


Compile `source-code` and any new types or variables you have defined will be deleted.

> 编译源代码，任何新定义的类型或变量都将被删除。


The command allows you to specify `source-code` in two ways. The simplest method is to provide a single line of code to the command. E.g.:

> 命令允许您以两种方式指定源代码。最简单的方法是向命令提供单行代码。例如：

::: smallexample

```bash
compile code printf ("hello world\n");
```

:::


If you specify options on the command line as well as source code, they may conflict. The '`--`' delimiter can be used to separate options from actual source code. E.g.:

> 如果您在命令行上指定选项以及源代码，它们可能会发生冲突。可以使用'--'分隔符来将选项与实际源代码分开。例如：

::: smallexample

```bash
compile code -r -- printf ("hello world\n");
```

:::


Alternatively you can enter source code as multiple lines of text. To enter this mode, invoke the '`compile code`' on its own line to exit the editor.

> 另外，您也可以将源代码输入为多行文本。要进入此模式，请在其自己的行上调用“编译代码”以退出编辑器。

::: smallexample

```bash
compile code
>printf ("hello\n");
>printf ("world\n");
>end
```

:::


Specifying '`-raw`' lines which may conflict with inferior symbols otherwise.

> 指定'-raw'行，以避免与较低符号发生冲突。

`compile file filename`

`compile file -raw filename`

Like `compile code`, but take the source code from `filename`.

::: smallexample

```bash
compile file /home/user/example.c
```

:::

`compile print [[options] --] expr`
`compile print [[options] --] /f expr`


:   Compile and execute `expr` is a letter specifying the format; see [Output Formats](Output-Formats.html#Output-Formats). The `compile print` command accepts the same options as the `print` command; see [print options](Data.html#print-options).

> 编译和执行`expr`是一个指定格式的信件；参见[输出格式](Output-Formats.html#Output-Formats)。`编译打印`命令接受与`打印`命令相同的选项；参见[打印选项](Data.html#print-options)。

`compile print [[options] --]`
`compile print [[options] --] /f`

:

```
Alternatively you can enter the expression (source code producing it) as multiple lines of text. To enter this mode, invoke the '`compile print`' command without any text following the command. This will start the multiple-line editor.
```

The process of compiling and injecting the code can be inspected using:

`set debug compile`


Turns on or off display of [GDB] process of compiling and injecting the code. The default is off.

> 开启或关闭[GDB]编译和注入代码的过程的显示，默认为关闭。

`show debug compile`


Displays the current state of displaying [GDB] process of compiling and injecting the code.

> 显示[GDB]编译和注入代码的当前状态。

`set debug compile-cplus-types`


Turns on or off the display of C++ type conversion debugging information. The default is off.

> 开启或关闭C++类型转换调试信息的显示。默认情况下是关闭的。

`show debug compile-cplus-types`


Displays the current state of displaying debugging information for C++ type conversion.

> 显示C++类型转换的调试信息的当前状态。

#### 17.7.1 Compilation options for the `compile` command

[GDB]'s injecting process.

The options used, in increasing precedence:

target architecture and OS options (`gdbarch`)


These options depend on target processor type and target operating system, usually they specify at least 32-bit (`-m32`) or 64-bit (`-m64`) compilation option.

> 这些选项取决于目标处理器类型和目标操作系统，通常它们至少指定32位（`-m32`）或64位（`-m64`）编译选项。

compilation options recorded in the target


[GCC] produces no DWARF. This feature is only relevant for platforms where `-g` produces DWARF by default, otherwise one may try to enforce DWARF by using `-gdwarf-4`.

> [GCC] 不会生成DWARF。这个特性只有在`-g`默认生成DWARF的平台上才有意义，否则可以尝试使用`-gdwarf-4`来强制生成DWARF。

compilation options set by `set compile-args`

You can override compilation options using the following command:

`set compile-args`

:

```
Set compilation options used for compiling and injecting code with the `compile` commands. These options override any conflicting ones from the target architecture and/or options stored during inferior compilation.
```

`show compile-args`


:   Displays the current state of compilation options override. This does not show all the options actually used during compilation, use [set debug compile](#set-debug-compile) for that.

> 显示编译选项覆盖的当前状态。 这不会显示编译期间实际使用的所有选项，请使用[set debug compile](#set-debug-compile)。

#### 17.7.2 Caveats when using the `compile` command


There are a few caveats to keep in mind when using the `compile` command. As the caveats are different per language, the table below highlights specific issues on a per language basis.

> 需要注意的是，在使用`编译`命令时有一些注意事项。由于每种语言的注意事项不同，下表按每种语言列出了特定问题。

C code examples and caveats

:   When the language in [GDB].

```
Below is a sample program that forms the basis of the examples that follow. This program has been compiled and loaded into [GDB], much like any other normal debugging session.

::: smallexample
``` smallexample
void function1 (void)
{
   int i = 42;
   printf ("function 1\n");
}

void function2 (void)
{
   int j = 12;
   function1 ();
}

int main(void)
{
   int k = 6;
   int *p;
   function2 ();
   return 0;
}
```

:::

For the purposes of the examples in this section, the program above has been compiled, loaded into [GDB] is awaiting input from the user.

To access variables and types for any program in [GDB], the program must be compiled and packaged with debug information. The `compile` command is not an exception to this rule. Without debug information, you can still use the `compile` command, but you will be very limited in what variables and types you can access.

So with that in mind, the example above has been compiled with debug information enabled. The `compile` command will have access to all variables and types (except those that may have been optimized out). Currently, as [GDB] has stopped the program in the `main` function, the `compile` command would have access to the variable `k`. You could invoke the `compile` command and type some source code to set the value of `k`. You can also read it, or do anything with that variable you would normally do in `C`. Be aware that changes to inferior variables in the `compile` command are persistent. In the following example:

::: smallexample

```bash
compile code k = 3;
```

:::

the variable `k` is now 3. It will retain that value until something else in the example program changes it, or another `compile` command changes it.

Normal scope and access rules apply to source code compiled and injected by the `compile` command. In the example, the variables `j` and `k` are not accessible yet, because the program is currently stopped in the `main` function, where these variables are not in scope. Therefore, the following command

::: smallexample

```bash
compile code j = 3;
```

:::

will result in a compilation error message.

Once the program is continued, execution will bring these variables in scope, and they will become accessible; then the code you specify via the `compile` command will be able to access them.

You can create variables and types with the `compile` command as part of your source code. Variables and types that are created as part of the `compile` command are not visible to the rest of the program for the duration of its run. This example is valid:

::: smallexample

```bash
compile code int ff = 5; printf ("ff is %d\n", ff);
```

:::

However, if you were to type the following into [GDB] after that command has completed:

::: smallexample

```bash
compile code printf ("ff is %d\n'', ff);
```

:::

a compiler error would be raised as the variable `ff` no longer exists. Object code generated and injected by the `compile` command is removed when its execution ends. Caution is advised when assigning to program variables values of variables created by the code submitted to the `compile` command. This example is valid:

::: smallexample

```bash
compile code int ff = 5; k = ff;
```

:::

The value of the variable `ff` is assigned to `k`. The variable `k` does not require the existence of `ff` to maintain the value it has been assigned. However, pointers require particular care in assignment. If the source code compiled with the `compile` command changed the address of a pointer in the example program, perhaps to a variable created in the `compile` command, that pointer would point to an invalid location when the command exits. The following example would likely cause issues with your debugged program:

::: smallexample

```bash
compile code int ff = 5; p = &ff;
```

:::

In this example, `p` would point to `ff` when the `compile` command is executing the source code provided to it. However, as variables in the (example) program persist with their assigned values, the variable `p` would point to an invalid location when the command exists. A general rule should be followed in that you should either assign `NULL` to any assigned pointers, or restore a valid location to the pointer before the command exits.

Similar caution must be exercised with any structs, unions, and typedefs defined in `compile` command. Types defined in the `compile` command will no longer be available in the next `compile` command. Therefore, if you cast a variable to a type defined in the `compile` command, care must be taken to ensure that any future need to resolve the type can be achieved.

::: smallexample

```bash
(gdb) compile code static struct a ; argv = &v;
(gdb) compile code printf ("%d\n", ((struct a *) argv)->a);

gdb command line:1:36: error: dereferencing pointer to incomplete type âstruct aâ

> 错误：解引用未完全类型的指针“struct a”，gdb命令行：1:36
Compilation failed.
(gdb) compile code struct a ; printf ("%d\n", ((struct a *) argv)->a);
42
```

:::

Variables that have been optimized away by the compiler are not accessible to the code submitted to the `compile` command. Access to those variables will generate a compiler error which [GDB] will print to the console.

```



#### 17.7.3 Compiler search for the `compile` command 


[GDB] command `set environment`). See [Environment](Environment.html#Environment).

> [GDB] 命令 `设置环境`。请参阅 [环境](Environment.html#Environment)。


Specifically `PATH` is searched for binaries matching regular expression `arch(-[^-]*)?-os-gcc` according to the inferior target being debugged. `arch` is currently supported only for pattern `linux(-gnu)?`.

> 具体来说，根据被调试的次级目标，会在`PATH`中搜索与正则表达式`arch(-[^-]*)?-os-gcc`匹配的二进制文件。目前仅支持`linux(-gnu)?`模式的`arch`。


On Posix hosts the compiler driver [GDB] is found according to the installation of the found compiler --- as possibly specified by the `set compile-gcc` command.

> 在Posix主机上，编译器驱动程序[GDB]根据发现的编译器的安装情况而被发现，可能由`set compile-gcc`命令指定。

`set compile-gcc`

:   

```

Set compilation command used for compiling and injecting code with the `compile` commands. If this option is not set (it is set to an empty string), the search described above will occur --- that is the default.

```

`show compile-gcc`

:   Displays the current compile command [GCC].

---

::: header
Previous: [Patching](Patching.html#Patching)]
:::
```
