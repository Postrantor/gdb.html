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

In the case of MI, the concept of selected thread and frame is less useful. First, a frontend can easily remember this information itself. Second, a graphical frontend can have more than one window, each one used for debugging a different thread, and the frontend might want to access additional threads for internal purposes. This increases the risk that by relying on implicitly selected thread, the frontend may be operating on a wrong one. Therefore, each MI command should explicitly specify which thread and frame to operate on. To make it possible, each MI command accepts the '`--thread` global identifier for thread and frame to operate on.

Usually, each top-level window in a frontend allows the user to select a thread and a frame, and remembers the user selection for further operations. However, in some cases [GDB]' notification.

Note that historically, MI shares the selected thread with CLI, so frontends used the `-thread-select` to execute commands in the right context. However, getting this to work right is cumbersome. The simplest way is for frontend to emit `-thread-select` command before every command. This doubles the number of commands that need to be sent. The alternative approach is to suppress `-thread-select` if the selected thread in [GDB]' options.

#### 27.1.1.2 Language

The execution of several commands depends on which language is selected. By default, the current language (see [show language](Show.html#show-language)) is used. But for commands known to be language-sensitive, it is recommended to use the '`--language`' option. This option takes one argument, which is the name of the language to use while executing the command. For instance:

::: smallexample

```bash
-data-evaluate-expression --language c "sizeof (void*)"
^done,value="4"
(gdb) 
```

:::

The valid language names are the same names accepted by the '`set language`'.

---

::: header
Next: [Asynchronous and non-stop modes](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes)]
:::
