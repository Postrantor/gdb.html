---
tip: translate by openai@2023-06-23 19:37:03
...
---
description: Context management (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Context management (Debugging with GDB)
lang: en
resource-type: document
title: Context management (Debugging with GDB)
---
::: header
Next: [Asynchronous and non-stop modes](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes)]
:::

---

#### 27.1.1 Context management

#### 27.1.1.1 Threads and Frames


In most cases when [GDB] via a single terminal, so no confusion is possible as to what thread and frame are the current ones.

> 在大多数情况下，使用单个终端来使用GDB，因此不会有关于当前线程和帧的混淆。


In the case of MI, the concept of selected thread and frame is less useful. First, a frontend can easily remember this information itself. Second, a graphical frontend can have more than one window, each one used for debugging a different thread, and the frontend might want to access additional threads for internal purposes. This increases the risk that by relying on implicitly selected thread, the frontend may be operating on a wrong one. Therefore, each MI command should explicitly specify which thread and frame to operate on. To make it possible, each MI command accepts the '`--thread` global identifier for thread and frame to operate on.

> 在MI的情况下，选择线程和帧的概念不太有用。首先，前端可以轻松记住这些信息。其次，图形前端可以拥有多个窗口，每个窗口用于调试不同的线程，前端可能想要访问其他线程用于内部目的。这增加了依赖隐式选择线程的风险，前端可能操作了错误的线程。因此，每个MI命令都应该明确指定要操作的线程和帧。为此，每个MI命令都接受'--thread'全局标识符，用于操作线程和帧。


Usually, each top-level window in a frontend allows the user to select a thread and a frame, and remembers the user selection for further operations. However, in some cases [GDB]' notification.

> 通常，前端中的每个顶层窗口都允许用户选择一个线程和一个框架，并且记住用户的选择以便进行进一步的操作。然而，在某些情况下，[GDB]会发出通知。


Note that historically, MI shares the selected thread with CLI, so frontends used the `-thread-select` to execute commands in the right context. However, getting this to work right is cumbersome. The simplest way is for frontend to emit `-thread-select` command before every command. This doubles the number of commands that need to be sent. The alternative approach is to suppress `-thread-select` if the selected thread in [GDB]' options.

> 历史上，MI与CLI共享所选择的线程，因此前端使用“-thread-select”来在正确的上下文中执行命令。但是，要正确使用它是麻烦的。最简单的方法是前端在每个命令之前发出“-thread-select”命令。这将需要发送的命令数量加倍。另一种方法是如果[GDB]中的选定线程选项，则抑制“-thread-select”。

#### 27.1.1.2 Language


The execution of several commands depends on which language is selected. By default, the current language (see [show language](Show.html#show-language)) is used. But for commands known to be language-sensitive, it is recommended to use the '`--language`' option. This option takes one argument, which is the name of the language to use while executing the command. For instance:

> 执行多个命令取决于所选择的语言。默认情况下，使用当前语言（参见[show language](Show.html#show-language)）。但是，对于已知敏感语言的命令，建议使用“--language”选项。此选项需要一个参数，即在执行命令时使用的语言的名称。例如：

::: smallexample

```bash
-data-evaluate-expression --language c "sizeof (void*)"
^done,value="4"
(gdb) 
```

:::


The valid language names are the same names accepted by the '`set language`'.

> 有效的语言名称与“设置语言”所接受的名称相同。

---

::: header
Next: [Asynchronous and non-stop modes](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes)]
:::
