---
tip: translate by openai@2023-06-23 18:28:47
...
---
description: Bug Reporting (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Bug Reporting (Debugging with GDB)
lang: en
resource-type: document
title: Bug Reporting (Debugging with GDB)
---
::: header
Previous: [Bug Criteria](Bug-Criteria.html#Bug-Criteria)]
:::

---

### 32.2 How to Report Bugs


A number of companies and individuals offer support for [GNU] from a support organization, we recommend you contact that organization first.

> 许多公司和个人都为[GNU]提供支持，我们建议您首先联系该组织。


You can find contact information for many support companies and individuals in the file `etc/SERVICE` Emacs distribution.

> 你可以在Emacs发行版的`etc/SERVICE`文件中找到许多支持公司和个人的联系信息。


In any event, we also recommend that you submit bug reports for [GDB] to [https://www.gnu.org/software/gdb/bugs/](https://www.gnu.org/software/gdb/bugs/).

> 在任何情况下，我们也建议您将GDB的错误报告提交至https://www.gnu.org/software/gdb/bugs/。


The fundamental principle of reporting bugs usefully is this: **report all the facts**. If you are not sure whether to state a fact or leave it out, state it!

> 報告錯誤有用的基本原則是：**報告所有事實**。如果您不確定是否要陳述事實或把它拿掉，就要陳述它！


Often people omit facts because they think they know what causes the problem and assume that some details do not matter. Thus, you might assume that the name of the variable you use in an example does not matter. Well, probably it does not, but one cannot be sure. Perhaps the bug is a stray memory reference which happens to fetch from the location where that name is stored in memory; perhaps, if the name were different, the contents of that location would fool the debugger into doing the right thing despite the bug. Play it safe and give a specific, complete example. That is the easiest thing for you to do, and the most helpful.

> 经常有人会因为他们认为自己知道是什么导致了问题而忽略了一些细节。因此，你可能会认为在例子中使用的变量名并不重要。可能的确不重要，但是也不能确定。也许这个 bug 是一个莫名其妙的内存引用，它会从内存中存储该名称的位置获取数据；或许，如果这个名称不一样，那么这个位置的内容会使调试器做出正确的事情，尽管有 bug。为了安全起见，给出一个特定的、完整的例子。这对你来说是最容易的，也是最有帮助的。


Keep in mind that the purpose of a bug report is to enable us to fix the bug. It may be that the bug has been reported previously, but neither you nor we can know that unless your bug report is complete and self-contained.

> 记住，提交错误报告的目的是为了让我们能够修复错误。可能之前已经报告过这个错误，但除非你的错误报告完整且独立，否则你我都不知道。


Sometimes people give a few sketchy facts and ask, "Does this ring a bell?" Those bug reports are useless, and we urge everyone to *refuse to respond to them* except to chide the sender to report bugs properly.

> 有时人们提供一些粗略的事实，然后问：“这有点熟悉吗？”这些错误报告毫无用处，我们敦促每个人*拒绝回应这些报告*，除了责备发送者正确报告错误。


To enable us to fix the bug, you should include all these things:

> 为了让我们能够修复这个 bug，你应该包括所有这些东西：


- The version of [GDB] announces it if you start with no arguments; you can also print it at any time using `show version`.

> 如果您没有参数启动[GDB]，它会宣布版本号；您也可以使用“show version”随时打印出它。


  Without this, we will not know whether there is any point in looking for the bug in the current version of [GDB].

> 没有这个，我们就不知道[GDB]当前版本中是否有必要寻找错误。
- The type of machine you are using, and the operating system name and version number.
- The details of the [GDB]'s prompt.
- What compiler (and its version) was used to compile [GDB]---e.g. "gcc--2.8.1".

- What compiler (and its version) was used to compile the program you are debugging---e.g. "gcc--2.8.1", or "HP92453-01 A.10.32.03 HP C Compiler". For [GCC] to get this information; for other compilers, see the documentation for those compilers.

> - 你正在调试的程序使用了什么编译器（以及它的版本）来编译？例如："GCC-2.8.1"，或者"HP92453-01 A.10.32.03 HP C Compiler"。对于[GCC]来获取这些信息；对于其他编译器，请参阅相应的文档。

- The command arguments you gave the compiler to compile your example and observe the bug. For example, did you use '`-O`'? To guarantee you will not omit something important, list them all. A copy of the Makefile (or the output from make) is sufficient.

> 给编译器编译示例时使用的命令参数，以观察错误。例如，您是否使用了“-O”？为了确保不会遗漏重要内容，请列出所有参数。Makefile的副本（或make的输出）就足够了。


  If we were to try to guess the arguments, we would probably guess wrong and then we might not encounter the bug.

> 如果我们试图猜测参数，我们可能会猜错，这样就可能遇不到这个 bug。
- A complete input script, and all necessary source files, that will reproduce the bug.

- A description of what behavior you observe that you believe is incorrect. For example, "It gets a fatal signal."

> 你观察到的行为描述，你认为不正确。例如：“它收到了致命的信号。”


  Of course, if the bug is that [GDB] gets a fatal signal, then we will certainly notice it. But if the bug is incorrect output, we might not notice unless it is glaringly wrong. You might as well not give us a chance to make a mistake.

> 当然，如果出现的错误是[GDB]收到致命信号，我们肯定会注意到它。但如果错误的输出不明显，我们可能不会注意到。最好不要给我们留下错误的机会。


  Even if the problem you experience is a fatal signal, you should still say so explicitly. Suppose something strange is going on, such as, your copy of [GDB] is out of synch, or you have encountered a bug in the C library on your system. (This has happened!) Your copy might crash and ours would not. If you told us to expect a crash, then when ours fails to crash, we would know that the bug was not happening for us. If you had not told us to expect a crash, then we would not be able to draw any conclusion from our observations.

> 即使你遇到的问题是一个致命的信号，你仍然应该明确地说出来。假设发生了一些奇怪的事情，比如你的[GDB]副本已经失去同步，或者你在系统上遇到了C库的一个错误（这种情况已经发生过！）你的副本可能会崩溃，而我们的副本不会。如果你告诉我们有可能会崩溃，那么当我们的副本没有崩溃时，我们就知道这个错误对我们来说不存在。如果你没有告诉我们会崩溃，那么我们就无法从观察中得出任何结论。


  To collect all this information, you can use a session recording program such as `script`, which is available on many Unix systems. Just run your [GDB] file with your bug report.

> 你可以使用诸如script之类的会话记录程序来收集所有这些信息，这种程序在许多Unix系统上都可以使用。只需使用您的[GDB]文件运行您的错误报告即可。


  Another way to record a [GDB] inside Emacs and then save the entire buffer to a file.

> 另一种在Emacs中记录[GDB]并将整个缓冲区保存到文件的方法。
- If you wish to suggest changes to the [GDB] source, refer to it by context, not by line number.


  The line numbers in our development sources will not match those in your sources. Your line numbers would convey no useful information to us.

> 行号在我们的开发源代码中不会与您的源代码中的行号相匹配。您的行号对我们没有任何有用的信息。


Here are some things that are not necessary:

> 这里有一些不必要的东西：

- A description of the envelope of the bug.


  Often people who encounter a bug spend a lot of time investigating which changes to the input file will make the bug go away and which changes will not affect it.

> 经常有人在遇到错误时，会花很多时间研究哪些输入文件的改变会使错误消失，哪些改变不会影响它。


  This is often time consuming and not very useful, because the way we will find the bug is by running a single example under the debugger with breakpoints, not by pure deduction from a series of examples. We recommend that you save your time for something else.

> 这通常耗费时间而且没有多大用处，因为我们要找到bug的方法是在调试器下运行单个示例并设置断点，而不是仅仅从一系列示例中推断出来。我们建议你把时间用在别的事情上。


  Of course, if you can find a simpler example to report *instead* of the original one, that is a convenience for us. Errors in the output will be easier to spot, running under the debugger will take less time, and so on.

> 当然，如果你能找到一个比原来的更简单的例子来报告，那对我们来说是很方便的。在调试器中运行时，输出中的错误将更容易发现，而且耗费的时间也会减少等等。


  However, simplification is not vital; if you do not want to do this, report the bug anyway and send us the entire test case you used.

> 然而，简化并不是必须的; 如果你不想这样做，也可以报告这个 bug，并把你使用的完整测试用例发给我们。
- A patch for the bug.


  A patch for the bug does help us if it is a good one. But do not omit the necessary information, such as the test case, on the assumption that a patch is all we need. We might see problems with your patch and decide to fix the problem another way, or we might not understand it at all.

> 一个好的补丁可以帮助我们解决错误。但是不要假定只有补丁就可以解决问题，请不要省略必要的信息，比如测试用例。我们可能会发现你提供的补丁存在问题，或者根本无法理解，因此决定采取其他方式解决问题。


  Sometimes with a program as complicated as [GDB] it is very hard to construct an example that will make the program follow a certain path through the code. If you do not send us the example, we will not be able to construct one, so we will not be able to verify that the bug is fixed.

> 有时，像[GDB]这样复杂的程序很难构建一个可以使程序沿着代码的某一路径运行的示例。如果您不发送示例给我们，我们就无法构建出示例，因此我们将无法验证该错误是否已经修复。


  And if we cannot understand what bug you are trying to fix, or why your patch should be an improvement, we will not install it. A test case will help us to understand.

> 如果我们无法理解您要修复的 bug 是什么，或者为什么您的补丁应该有所改进，我们将不会安装它。一个测试用例可以帮助我们理解。
- A guess about what the bug is or what it depends on.


  Such guesses are usually wrong. Even we cannot guess right about such things without first using the debugger to find the facts.

> 这样的猜测通常是错误的。即使我们在没有使用调试器来查找事实的情况下，也无法正确猜测这些事情。

---

::: header
Previous: [Bug Criteria](Bug-Criteria.html#Bug-Criteria)]
:::
