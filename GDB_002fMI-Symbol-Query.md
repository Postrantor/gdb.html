---
description: GDB/MI Symbol Query (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Symbol Query (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Symbol Query (Debugging with GDB)
---
::: header
Next: [GDB/MI File Commands](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands)]
:::

---

### 27.18 [GDB/MI]

#### The `-symbol-info-functions` Command

#### Synopsis

::: smallexample

```bash
 -symbol-info-functions [--include-nondebug]
                        [--type type_regexp]
                        [--name name_regexp]
                        [--max-results limit]
```

:::

Return a list containing the names and types for all global functions taken from the debug information. The functions are grouped by source file, and shown with the line number on which each function is defined.

The `--include-nondebug` option causes the output to include code symbols from the symbol table.

The options `--type` and `--name` allow the symbols returned to be filtered based on either the name of the function, or the type signature of the function.

The option `--max-results` restricts the command to return no more than `limit` results are returned then there might be additional results available if a higher limit is used.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-symbol-info-functions
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      symbols=[{line="36", name="f4", type="void (int *)",
                description="void f4(int *);"},
               {line="42", name="main", type="int ()",
                description="int main();"},
               {line="30", name="f1", type="my_int_t (int, int)",
                description="static my_int_t f1(int, int);"}]},
     {filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      symbols=[{line="33", name="f2", type="float (another_float_t)",
                description="float f2(another_float_t);"},
               {line="39", name="f3", type="int (another_int_t)",
                description="int f3(another_int_t);"},
               {line="27", name="f1", type="another_float_t (int)",
                description="static another_float_t f1(int);"}]}]}
```

```bash
(gdb)
-symbol-info-functions --name f1
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      symbols=[{line="30", name="f1", type="my_int_t (int, int)",
                description="static my_int_t f1(int, int);"}]},
     {filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      symbols=[{line="27", name="f1", type="another_float_t (int)",
                description="static another_float_t f1(int);"}]}]}
```

```bash
(gdb)
-symbol-info-functions --type void
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      symbols=[{line="36", name="f4", type="void (int *)",
                description="void f4(int *);"}]}]}
```

```bash
(gdb)
-symbol-info-functions --include-nondebug
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      symbols=[{line="36", name="f4", type="void (int *)",
                description="void f4(int *);"},
               {line="42", name="main", type="int ()",
                description="int main();"},
               {line="30", name="f1", type="my_int_t (int, int)",
                description="static my_int_t f1(int, int);"}]},
     {filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      symbols=[{line="33", name="f2", type="float (another_float_t)",
                description="float f2(another_float_t);"},
               {line="39", name="f3", type="int (another_int_t)",
                description="int f3(another_int_t);"},
               {line="27", name="f1", type="another_float_t (int)",
                description="static another_float_t f1(int);"}]}],
   nondebug=
    [,
     ,
      ...
    ]}
```

:::

#### The `-symbol-info-module-functions` Command

#### Synopsis

::: smallexample

```bash
 -symbol-info-module-functions [--module module_regexp]
                               [--name name_regexp]
                               [--type type_regexp]
```

:::

Return a list containing the names of all known functions within all know Fortran modules. The functions are grouped by source file and containing module, and shown with the line number on which each function is defined.

The option `--module` only returns results for modules matching `module_regexp`.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-symbol-info-module-functions
^done,symbols=
  [{module="mod1",
    files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
            fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
            symbols=[{line="21",name="mod1::check_all",type="void (void)",
                      description="void mod1::check_all(void);"}]}]},
    {module="mod2",
     files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
             fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
             symbols=[{line="30",name="mod2::check_var_i",type="void (void)",
                       description="void mod2::check_var_i(void);"}]}]},
    {module="mod3",
     files=[{filename="/projec/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
             fullname="/projec/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
             symbols=[{line="21",name="mod3::check_all",type="void (void)",
                       description="void mod3::check_all(void);"},
                      {line="27",name="mod3::check_mod2",type="void (void)",
                       description="void mod3::check_mod2(void);"}]}]},
    {module="modmany",
     files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
             fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
             symbols=[{line="35",name="modmany::check_some",type="void (void)",
                       description="void modmany::check_some(void);"}]}]},
    {module="moduse",
     files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
             fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
             symbols=[{line="44",name="moduse::check_all",type="void (void)",
                       description="void moduse::check_all(void);"},
                      {line="49",name="moduse::check_var_x",type="void (void)",
                       description="void moduse::check_var_x(void);"}]}]}]
```

:::

#### The `-symbol-info-module-variables` Command

#### Synopsis

::: smallexample

```bash
 -symbol-info-module-variables [--module module_regexp]
                               [--name name_regexp]
                               [--type type_regexp]
```

:::

Return a list containing the names of all known variables within all know Fortran modules. The variables are grouped by source file and containing module, and shown with the line number on which each variable is defined.

The option `--module` only returns results for modules matching `module_regexp`.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-symbol-info-module-variables
^done,symbols=
  [{module="mod1",
    files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
            fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
            symbols=[{line="18",name="mod1::var_const",type="integer(kind=4)",
                      description="integer(kind=4) mod1::var_const;"},
                     {line="17",name="mod1::var_i",type="integer(kind=4)",
                      description="integer(kind=4) mod1::var_i;"}]}]},
   {module="mod2",
    files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
            fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
            symbols=[{line="28",name="mod2::var_i",type="integer(kind=4)",
                      description="integer(kind=4) mod2::var_i;"}]}]},
   {module="mod3",
    files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
            fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
            symbols=[{line="18",name="mod3::mod1",type="integer(kind=4)",
                      description="integer(kind=4) mod3::mod1;"},
                     {line="17",name="mod3::mod2",type="integer(kind=4)",
                      description="integer(kind=4) mod3::mod2;"},
                     {line="19",name="mod3::var_i",type="integer(kind=4)",
                      description="integer(kind=4) mod3::var_i;"}]}]},
   {module="modmany",
    files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
            fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
            symbols=[{line="33",name="modmany::var_a",type="integer(kind=4)",
                      description="integer(kind=4) modmany::var_a;"},
                     {line="33",name="modmany::var_b",type="integer(kind=4)",
                      description="integer(kind=4) modmany::var_b;"},
                     {line="33",name="modmany::var_c",type="integer(kind=4)",
                      description="integer(kind=4) modmany::var_c;"},
                     {line="33",name="modmany::var_i",type="integer(kind=4)",
                      description="integer(kind=4) modmany::var_i;"}]}]},
   {module="moduse",
    files=[{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
            fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
            symbols=[{line="42",name="moduse::var_x",type="integer(kind=4)",
                      description="integer(kind=4) moduse::var_x;"},
                     {line="42",name="moduse::var_y",type="integer(kind=4)",
                      description="integer(kind=4) moduse::var_y;"}]}]}]
```

:::

#### The `-symbol-info-modules` Command

#### Synopsis

::: smallexample

```bash
 -symbol-info-modules [--name name_regexp]
                      [--max-results limit]
```

:::

Return a list containing the names of all known Fortran modules. The modules are grouped by source file, and shown with the line number on which each modules is defined.

The option `--name` allows the modules returned to be filtered based the name of the module.

The option `--max-results` restricts the command to return no more than `limit` results are returned then there might be additional results available if a higher limit is used.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-symbol-info-modules
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
      fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
      symbols=[,
               ,
     {filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
      fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
      symbols=[,
               ,
               
```

```bash
(gdb)
-symbol-info-modules --name mod[123]
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
      fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules-2.f90",
      symbols=[,
               ,
     {filename="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
      fullname="/project/gdb/testsuite/gdb.mi/mi-fortran-modules.f90",
      symbols=[
```

:::

#### The `-symbol-info-types` Command

#### Synopsis

::: smallexample

```bash
 -symbol-info-types [--name name_regexp]
                    [--max-results limit]
```

:::

Return a list of all defined types. The types are grouped by source file, and shown with the line number on which each user defined type is defined. Some base types are not defined in the source code but are added to the debug information by the compiler, for example `int`, `float`, etc.; these types do not have an associated line number.

The option `--name` allows the list of types returned to be filtered by name.

The option `--max-results` restricts the command to return no more than `limit` results are returned then there might be additional results available if a higher limit is used.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-symbol-info-types
^done,symbols=
  {debug=
     [{filename="gdb.mi/mi-sym-info-1.c",
       fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
       symbols=[,
                ,
                ,
      {filename="gdb.mi/mi-sym-info-2.c",
       fullname="/project/gdb.mi/mi-sym-info-2.c",
       symbols=[,
                ,
                ,
                
```

```bash
(gdb)
-symbol-info-types --name _int_
^done,symbols=
  {debug=
     [{filename="gdb.mi/mi-sym-info-1.c",
       fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
       symbols=[,
      {filename="gdb.mi/mi-sym-info-2.c",
       fullname="/project/gdb.mi/mi-sym-info-2.c",
       symbols=[
```

:::

#### The `-symbol-info-variables` Command

#### Synopsis

::: smallexample

```bash
 -symbol-info-variables [--include-nondebug]
                        [--type type_regexp]
                        [--name name_regexp]
                        [--max-results limit]
```

:::

Return a list containing the names and types for all global variables taken from the debug information. The variables are grouped by source file, and shown with the line number on which each variable is defined.

The `--include-nondebug` option causes the output to include data symbols from the symbol table.

The options `--type` and `--name` allow the symbols returned to be filtered based on either the name of the variable, or the type of the variable.

The option `--max-results` restricts the command to return no more than `limit` results are returned then there might be additional results available if a higher limit is used.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-symbol-info-variables
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      symbols=[{line="25",name="global_f1",type="float",
                description="static float global_f1;"},
               {line="24",name="global_i1",type="int",
                description="static int global_i1;"}]},
     {filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      symbols=[{line="21",name="global_f2",type="int",
                description="int global_f2;"},
               {line="20",name="global_i2",type="int",
                description="int global_i2;"},
               {line="19",name="global_f1",type="float",
                description="static float global_f1;"},
               {line="18",name="global_i1",type="int",
                description="static int global_i1;"}]}]}
```

```bash
(gdb)
-symbol-info-variables --name f1
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      symbols=[{line="25",name="global_f1",type="float",
                description="static float global_f1;"}]},
     {filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      symbols=[{line="19",name="global_f1",type="float",
                description="static float global_f1;"}]}]}
```

```bash
(gdb)
-symbol-info-variables --type float
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      symbols=[{line="25",name="global_f1",type="float",
                description="static float global_f1;"}]},
     {filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      symbols=[{line="19",name="global_f1",type="float",
                description="static float global_f1;"}]}]}
```

```bash
(gdb)
-symbol-info-variables --include-nondebug
^done,symbols=
  {debug=
    [{filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-1.c",
      symbols=[{line="25",name="global_f1",type="float",
                description="static float global_f1;"},
               {line="24",name="global_i1",type="int",
                description="static int global_i1;"}]},
     {filename="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      fullname="/project/gdb/testsuite/gdb.mi/mi-sym-info-2.c",
      symbols=[{line="21",name="global_f2",type="int",
                description="int global_f2;"},
               {line="20",name="global_i2",type="int",
                description="int global_i2;"},
               {line="19",name="global_f1",type="float",
                description="static float global_f1;"},
               {line="18",name="global_i1",type="int",
                description="static int global_i1;"}]}],
   nondebug=
    [,
     
      ...
    ]}
```

:::

#### The `-symbol-list-lines` Command

#### Synopsis

::: smallexample

```bash
 -symbol-list-lines filename
```

:::

Print the list of lines that contain code and their associated program addresses for the given source filename. The entries are sorted in ascending PC order.

#### [GDB]

There is no corresponding [GDB] command.

#### Example

::: smallexample

```bash
(gdb)
-symbol-list-lines basics.c
^done,lines=
(gdb)
```

:::

---

::: header
Next: [GDB/MI File Commands](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands)]
:::
