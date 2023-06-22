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

`compile code source-code`

`compile code -raw -- source-code`

Compile `source-code` and any new types or variables you have defined will be deleted.

The command allows you to specify `source-code` in two ways. The simplest method is to provide a single line of code to the command. E.g.:

::: smallexample

```bash
compile code printf ("hello world\n");
```

:::

If you specify options on the command line as well as source code, they may conflict. The '`--`' delimiter can be used to separate options from actual source code. E.g.:

::: smallexample

```bash
compile code -r -- printf ("hello world\n");
```

:::

Alternatively you can enter source code as multiple lines of text. To enter this mode, invoke the '`compile code`' on its own line to exit the editor.

::: smallexample

```bash
compile code
>printf ("hello\n");
>printf ("world\n");
>end
```

:::

Specifying '`-raw`' lines which may conflict with inferior symbols otherwise.

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

`compile print [[options] --]`
`compile print [[options] --] /f`

:

```
Alternatively you can enter the expression (source code producing it) as multiple lines of text. To enter this mode, invoke the '`compile print`' command without any text following the command. This will start the multiple-line editor.
```

The process of compiling and injecting the code can be inspected using:

`set debug compile`

Turns on or off display of [GDB] process of compiling and injecting the code. The default is off.

`show debug compile`

Displays the current state of displaying [GDB] process of compiling and injecting the code.

`set debug compile-cplus-types`

Turns on or off the display of C++ type conversion debugging information. The default is off.

`show debug compile-cplus-types`

Displays the current state of displaying debugging information for C++ type conversion.

#### 17.7.1 Compilation options for the `compile` command

[GDB]'s injecting process.

The options used, in increasing precedence:

target architecture and OS options (`gdbarch`)

These options depend on target processor type and target operating system, usually they specify at least 32-bit (`-m32`) or 64-bit (`-m64`) compilation option.

compilation options recorded in the target

[GCC] produces no DWARF. This feature is only relevant for platforms where `-g` produces DWARF by default, otherwise one may try to enforce DWARF by using `-gdwarf-4`.

compilation options set by `set compile-args`

You can override compilation options using the following command:

`set compile-args`

:

```
Set compilation options used for compiling and injecting code with the `compile` commands. These options override any conflicting ones from the target architecture and/or options stored during inferior compilation.
```

`show compile-args`

:   Displays the current state of compilation options override. This does not show all the options actually used during compilation, use [set debug compile](#set-debug-compile) for that.

#### 17.7.2 Caveats when using the `compile` command

There are a few caveats to keep in mind when using the `compile` command. As the caveats are different per language, the table below highlights specific issues on a per language basis.

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
Compilation failed.
(gdb) compile code struct a ; printf ("%d\n", ((struct a *) argv)->a);
42
```

:::

Variables that have been optimized away by the compiler are not accessible to the code submitted to the `compile` command. Access to those variables will generate a compiler error which [GDB] will print to the console.

```



#### 17.7.3 Compiler search for the `compile` command 

[GDB] command `set environment`). See [Environment](Environment.html#Environment).

Specifically `PATH` is searched for binaries matching regular expression `arch(-[^-]*)?-os-gcc` according to the inferior target being debugged. `arch` is currently supported only for pattern `linux(-gnu)?`.

On Posix hosts the compiler driver [GDB] is found according to the installation of the found compiler --- as possibly specified by the `set compile-gcc` command.

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
