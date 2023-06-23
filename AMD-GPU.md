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

#### 21.4.10.1 AMD GPU Architectures

The list of AMD GPU architectures supported by [GDB] depends on the version of the AMD Debugger API library used. See its [documentation](https://docs.amd.com/bundle/ROCDebugger_User_and_API) for more details.

#### 21.4.10.2 AMD GPU Device Driver and AMD ROCm Runtime

[GDB] will continue to function except no AMD GPU debugging will be possible.

[GDB] will continue to function except no AMD GPU debugging will be possible on the agent.

[GDB] will continue to function except no AMD GPU debugging will be possible.

#### 21.4.10.3 AMD GPU Wavefronts

An AMD GPU wavefront is represented in [GDB] as a thread.

Note that some AMD GPU architectures may have restrictions on providing information about AMD GPU wavefronts created when [GDB] is not attached (see [AMD GPU Attaching Restrictions](#AMD-GPU-Attaching-Restrictions)).

When scheduler-locking is in effect (see [set scheduler-locking](All_002dStop-Mode.html#set-scheduler_002dlocking)), new wavefronts created by the resumed thread (either CPU thread or GPU wavefront) are held in the halt state.

#### 21.4.10.4 AMD GPU Code Objects

The '`info sharedlibrary`' command will show the AMD GPU code objects as file or memory URIs, together with the host's shared libraries. For example:

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

For a '`memory` parameter is its size in bytes.

AMD GPU code objects are loaded into each AMD GPU device separately. The '`info sharedlibrary`' command may therefore show the same code object loaded multiple times. As a consequence, setting a breakpoint in AMD GPU code will result in multiple breakpoint locations if there are multiple AMD GPU devices.

#### 21.4.10.5 AMD GPU Entity Target Identifiers and Convenience Variables

The AMD GPU entities have the following target identifier formats:

Thread Target ID

:   The AMD GPU thread target identifier (`systag`) string has the following format:

```
::: smallexample
``` smallexample
AMDGPU Wave agent-id:queue-id:dispatch-id:wave-id (work-group-x,work-group-y,work-group-z)/work-group-thread-index
```

:::

```



#### 21.4.10.6 AMD GPU Signals 

For AMD GPU wavefronts, [GDB] maps target conditions to stop signals in the following way:

`SIGILL`

:   Execution of an illegal instruction.

`SIGTRAP`

:   Execution of a `S_TRAP` instruction other than:

```

- `S_TRAP 1` which is used by [GDB] to insert breakpoints.
- `S_TRAP 2` which raises `SIGABRT`.

```

`SIGABRT`

:   Execution of a `S_TRAP 2` instruction.

`SIGFPE`

:   Execution of a floating point or integer instruction detects a condition that is enabled to raise a signal. The conditions include:

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

`SIGSEGV`

:   Execution of an instruction that accessed a global memory page that is either not mapped or accessed with incompatible permissions.

If a single instruction raises more than one signal, they will be reported one at a time each time the wavefront is continued.



#### 21.4.10.7 AMD GPU Logging 

The '`set debug amd-dbgapi`' command displays the current setting. See [set debug amd-dbgapi](Debugging-Output.html#set-debug-amd_002ddbgapi).

The '`set debug amd-dbgapi-lib log-level level`' library log level. See [set debug amd-dbgapi-lib](Debugging-Output.html#set-debug-amd_002ddbgapi_002dlib).



#### 21.4.10.8 AMD GPU Restrictions 

1. When in non-stop mode, wavefronts may not hit breakpoints inserted while not stopped, nor see memory updates made while not stopped, until the wavefront is next stopped. Memory updated by non-stopped wavefronts may not be visible until the wavefront is next stopped.
2. The HIP runtime performs deferred code object loading by default. AMD GPU code objects are not loaded until the first kernel is launched. Before then, all breakpoints have to be set as pending breakpoints.

   If source line positions are used that only correspond to source lines in unloaded code objects, then [GDB] may not set pending breakpoints, and instead set breakpoints on the next following source line that maps to host code. This can result in unexpected breakpoint hits being reported. When the code object containing the source lines is loaded, the incorrect breakpoints will be removed and replaced by the correct ones. This problem can be avoided by only setting breakpoints in unloaded code objects using symbol or function names.

   Setting the `HIP_ENABLE_DEFERRED_LOADING` environment variable to `0` can be used to disable deferred code object loading by the HIP runtime. This ensures all code objects will be loaded when the inferior reaches the beginning of the `main` function.
3. If no CPU thread is running, then '`Ctrl-C`
4. By default, for some architectures, the AMD GPU device driver causes all AMD GPU wavefronts created when [GDB]'.

   This does not affect wavefronts created while [GDB] is attached which are always capable of reporting this information.

   If the `HSA_ENABLE_DEBUG` environment variable is set to '`1` was not attached.

---

::: header
Previous: [S12Z](S12Z.html#S12Z)]
:::
```
