---
tip: translate by openai@2023-06-23 17:12:35
...
---
description: AMD GPU (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: AMD GPU (Debugging with GDB)
lang: en
resource-type: document
title: AMD GPU (Debugging with GDB)
---
::: header
Previous: [S12Z](S12Z.html#S12Z)]
:::

---

#### 21.4.10 AMD GPU


[GDB] presents host threads alongside GPU wavefronts, allowing debugging both the host and device parts of the program simultaneously.

> [GDB]可以同时显示主机线程和GPU波形，从而可以同时调试程序的主机和设备部分。

#### 21.4.10.1 AMD GPU Architectures


The list of AMD GPU architectures supported by [GDB] depends on the version of the AMD Debugger API library used. See its [documentation](https://docs.amd.com/bundle/ROCDebugger_User_and_API) for more details.

> AMD GPU的架构列表取决于所使用的AMD调试器API库的版本。有关更多信息，请参阅其[文档](https://docs.amd.com/bundle/ROCDebugger_User_and_API)。

#### 21.4.10.2 AMD GPU Device Driver and AMD ROCm Runtime


[GDB] will continue to function except no AMD GPU debugging will be possible.

> GDB仍将继续运行，但不能进行AMD GPU调试。


[GDB] will continue to function except no AMD GPU debugging will be possible on the agent.

> GDB仍然可以正常工作，但在代理上将不能进行AMD GPU调试。


[GDB] will continue to function except no AMD GPU debugging will be possible.

> GDB仍将正常运行，但不能进行AMD GPU调试。

#### 21.4.10.3 AMD GPU Wavefronts


An AMD GPU wavefront is represented in [GDB] as a thread.

> AMD GPU 波前在GDB中表示为一个线程。

Note that some AMD GPU architectures may have restrictions on providing information about AMD GPU wavefronts created when [GDB] is not attached (see [AMD GPU Attaching Restrictions](#AMD-GPU-Attaching-Restrictions)).


When scheduler-locking is in effect (see [set scheduler-locking](All_002dStop-Mode.html#set-scheduler_002dlocking)), new wavefronts created by the resumed thread (either CPU thread or GPU wavefront) are held in the halt state.

> 当调度锁定生效时（参见[设置调度锁定](All_002dStop-Mode.html#set-scheduler_002dlocking)），恢复的线程（无论是CPU线程还是GPU波前）创建的新波前将被保持在停止状态。

#### 21.4.10.4 AMD GPU Code Objects


The '`info sharedlibrary`' command will show the AMD GPU code objects as file or memory URIs, together with the host's shared libraries. For example:

> `info sharedlibrary` 命令可以显示 AMD GPU 代码对象作为文件或内存 URIs，连同主机的共享库一起。例如：

::: smallexample

```bash
(gdb) info sharedlibrary
From    To      Syms Read   Shared Object Library
0x1111  0x2222  Yes (*)     /lib64/ld-linux-x86-64.so.2
...
0x3333  0x4444  Yes (*)     /opt/rocm-4.5.0/.../libamd_comgr.so
0x5555  0x6666  Yes (*)     /lib/x86_64-linux-gnu/libtinfo.so.5
0x7777  0x8888  Yes         file:///tmp/a.out#offset=6477&size=10832
0x9999  0xaaaa  Yes (*)     memory://95557/mem#offset=0x1234&size=100
(*): Shared library is missing debugging information.
(gdb)
```

:::


For a '`file` parameter is the size of the code object in bytes. If omitted, it defaults to the size of the file.

> 对于`文件`参数，大小是以字节为单位的代码对象的大小。如果省略，则默认为文件的大小。


For a '`memory` parameter is its size in bytes.

> 对于一个“内存”参数，它的大小是以字节为单位。


AMD GPU code objects are loaded into each AMD GPU device separately. The '`info sharedlibrary`' command may therefore show the same code object loaded multiple times. As a consequence, setting a breakpoint in AMD GPU code will result in multiple breakpoint locations if there are multiple AMD GPU devices.

> AMD GPU代码对象分别加载到每个AMD GPU设备中。因此，“info sharedlibrary”命令可能会显示多次加载同一代码对象。因此，如果有多个AMD GPU设备，在AMD GPU代码中设置断点将会导致多个断点位置。

#### 21.4.10.5 AMD GPU Entity Target Identifiers and Convenience Variables


The AMD GPU entities have the following target identifier formats:

> AMD GPU实体具有以下目标标识符格式：

Thread Target ID


:   The AMD GPU thread target identifier (`systag`) string has the following format:

> AMD GPU线程目标标识符（`systag`）字符串具有以下格式：

```
::: smallexample
``` smallexample

AMDGPU Wave agent-id:queue-id:dispatch-id:wave-id (work-group-x,work-group-y,work-group-z)/work-group-thread-index

> AMDGPU 波代理ID：队列ID：调度ID：波ID（工作组X，工作组Y，工作组Z）/工作组线程索引
```

:::

```



#### 21.4.10.6 AMD GPU Signals 


For AMD GPU wavefronts, [GDB] maps target conditions to stop signals in the following way:

> 对于AMD GPU wavefront，[GDB]将目标条件映射到停止信号的方式如下：

`SIGILL`


:   Execution of an illegal instruction.

> 执行非法指令

`SIGTRAP`


:   Execution of a `S_TRAP` instruction other than:

> 执行除S_TRAP指令之外的其他指令

```

- `S_TRAP 1` which is used by [GDB] to insert breakpoints.
- `S_TRAP 2` which raises `SIGABRT`.

```

`SIGABRT`


:   Execution of a `S_TRAP 2` instruction.

> 执行一条S_TRAP 2指令。

`SIGFPE`


:   Execution of a floating point or integer instruction detects a condition that is enabled to raise a signal. The conditions include:

> 执行浮点或整数指令检测到可以引发信号的条件。这些条件包括：

```

- Floating point operation is invalid.
- Floating point operation had subnormal input that was rounded to zero.
- Floating point operation performed a division by zero.
- Floating point operation produced an overflow result. The result was rounded to infinity.
- Floating point operation produced an underflow result. A subnormal result was rounded to zero.
- Floating point operation produced an inexact result.
- Integer operation performed a division by zero.

By default, these conditions are not enabled to raise signals. The '`set $mode`' command can be used to inspect which conditions have been detected even if they are not enabled to raise a signal.

```

`SIGBUS`


:   Execution of an instruction that accessed global memory using an address that is outside the virtual address range.

> 执行使用超出虚拟地址范围的地址访问全局内存的指令。

`SIGSEGV`


:   Execution of an instruction that accessed a global memory page that is either not mapped or accessed with incompatible permissions.

> 执行访问全局存储页面的指令时，该页面要么未映射，要么使用的权限不兼容。


If a single instruction raises more than one signal, they will be reported one at a time each time the wavefront is continued.

> 如果一条指令引发多个信号，则每次波前继续时将一次报告一个信号。



#### 21.4.10.7 AMD GPU Logging 


The '`set debug amd-dbgapi`' command displays the current setting. See [set debug amd-dbgapi](Debugging-Output.html#set-debug-amd_002ddbgapi).

> 命令`set debug amd-dbgapi`显示当前设置。请参阅[set debug amd-dbgapi](Debugging-Output.html#set-debug-amd_002ddbgapi)。


The '`set debug amd-dbgapi-lib log-level level`' library log level. See [set debug amd-dbgapi-lib](Debugging-Output.html#set-debug-amd_002ddbgapi_002dlib).

> 设置debug amd-dbgapi-lib日志级别。参见[设置debug amd-dbgapi-lib](Debugging-Output.html#set-debug-amd_002ddbgapi_002dlib)。



#### 21.4.10.8 AMD GPU Restrictions 


1. When in non-stop mode, wavefronts may not hit breakpoints inserted while not stopped, nor see memory updates made while not stopped, until the wavefront is next stopped. Memory updated by non-stopped wavefronts may not be visible until the wavefront is next stopped.

> 当处于不停止模式时，波前可能不会击中插入的断点，也不会看到未停止时所做的内存更新，直到下一次波前停止。未停止的波前所做的内存更新可能无法被看到，直到波前下一次停止。

2. The HIP runtime performs deferred code object loading by default. AMD GPU code objects are not loaded until the first kernel is launched. Before then, all breakpoints have to be set as pending breakpoints.

> 默认情况下，HIP运行时通过延迟代码对象加载实现。在首次启动内核之前，不会加载AMD GPU代码对象。在此之前，所有断点都必须设为挂起断点。


   If source line positions are used that only correspond to source lines in unloaded code objects, then [GDB] may not set pending breakpoints, and instead set breakpoints on the next following source line that maps to host code. This can result in unexpected breakpoint hits being reported. When the code object containing the source lines is loaded, the incorrect breakpoints will be removed and replaced by the correct ones. This problem can be avoided by only setting breakpoints in unloaded code objects using symbol or function names.

> 如果只使用与未加载代码对象中的源行相对应的源行位置，那么[GDB]可能不会设置挂起的断点，而是在映射到主机代码的下一行源代码上设置断点。这可能会导致报告意外的断点命中。当加载包含源行的代码对象时，将会删除不正确的断点并替换为正确的断点。可以通过使用符号或函数名称来避免在未加载的代码对象中设置断点来避免这个问题。


   Setting the `HIP_ENABLE_DEFERRED_LOADING` environment variable to `0` can be used to disable deferred code object loading by the HIP runtime. This ensures all code objects will be loaded when the inferior reaches the beginning of the `main` function.

> 设置环境变量 `HIP_ENABLE_DEFERRED_LOADING` 为 `0` 可用于禁用 HIP 运行时的延迟代码对象加载。这样可以确保所有代码对象将在次要进程到达 `main` 函数开头时被加载。

3. If no CPU thread is running, then '`Ctrl-C`

> 如果没有CPU线程正在运行，那么按`Ctrl-C`

4. By default, for some architectures, the AMD GPU device driver causes all AMD GPU wavefronts created when [GDB]'.

> 默认情况下，对于某些架构，AMD GPU设备驱动程序会在[GDB]创建时导致所有AMD GPU波前。


   This does not affect wavefronts created while [GDB] is attached which are always capable of reporting this information.

> 这不会影响在附加[GDB]时创建的波前，它们总是能够报告这些信息。


   If the `HSA_ENABLE_DEBUG` environment variable is set to '`1` was not attached.

> 如果环境变量HSA_ENABLE_DEBUG设置为“1”，则未附加。

---

::: header
Previous: [S12Z](S12Z.html#S12Z)]
:::
```
