---
tip: translate by openai@2023-06-23 21:20:58
...
---
description: Frame Filter API (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frame Filter API (Debugging with GDB)
lang: en
resource-type: document
title: Frame Filter API (Debugging with GDB)
---
::: header
Next: [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API)]
:::

---

#### 23.3.2.9 Filtering Frames


Frame filters are Python objects that manipulate the visibility of a frame or frames when a backtrace (see [Backtrace](Backtrace.html#Backtrace)) is printed by [GDB].

> 框架过滤器是Python对象，当[GDB]打印出回溯（参见[Backtrace]（Backtrace.html#Backtrace））时，可以操作帧或帧的可见性。


Only commands that print a backtrace, or, in the case of [GDB/MI] commands (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)), those that return a collection of frames are affected. The commands that work with frame filters are:

> 只有打印回溯的命令，或者在[GDB/MI]命令（参见[GDB/MI]）的情况下，那些返回一组帧受到影响。使用帧过滤器的命令有：

`backtrace` (see [The backtrace command](Backtrace.html#backtrace_002dcommand)), `-stack-list-frames` (see [The -stack-list-frames command](GDB_002fMI-Stack-Manipulation.html#g_t_002dstack_002dlist_002dframes)), `-stack-list-variables` (see [The -stack-list-variables command](GDB_002fMI-Stack-Manipulation.html#g_t_002dstack_002dlist_002dvariables)), `-stack-list-arguments` see [The -stack-list-arguments command](GDB_002fMI-Stack-Manipulation.html#g_t_002dstack_002dlist_002darguments)) and `-stack-list-locals` (see [The -stack-list-locals command](GDB_002fMI-Stack-Manipulation.html#g_t_002dstack_002dlist_002dlocals)).


A frame filter works by taking an iterator as an argument, applying actions to the contents of that iterator, and returning another iterator (or, possibly, the same iterator it was provided in the case where the filter does not perform any operations). Typically, frame filters utilize tools such as the Python's `itertools` module to work with and create new iterators from the source iterator. Regardless of how a filter chooses to apply actions, it must not alter the underlying [GDB]. Frame filters are executed on a priority basis and care should be taken that some frame filters may have been executed before, and that some frame filters will be executed after.

> 帧过滤器通过将迭代器作为参数传递，对该迭代器的内容应用操作，并返回另一个迭代器（或者，在滤波器不执行任何操作的情况下，可能返回相同的迭代器）。通常，帧过滤器使用Python的`itertools`模块来处理和创建来自源迭代器的新迭代器。无论过滤器选择如何应用操作，它都不能改变底层[GDB]。帧过滤器按优先级执行，应该注意一些帧过滤器可能已经执行过，一些帧过滤器将在之后执行。


An important consideration when designing frame filters, and well worth reflecting upon, is that frame filters should avoid unwinding the call stack if possible. Some stacks can run very deep, into the tens of thousands in some cases. To search every frame when a frame filter executes may be too expensive at that step. The frame filter cannot know how many frames it has to iterate over, and it may have to iterate through them all. This ends up duplicating effort as [GDB] performs this iteration when it prints the frames. If the filter can defer unwinding frames until frame decorators are executed, after the last filter has executed, it should. See [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API), for more information on decorators. Also, there are examples for both frame decorators and filters in later chapters. See [Writing a Frame Filter](Writing-a-Frame-Filter.html#Writing-a-Frame-Filter), for more information.

> 设计帧过滤器时，一个重要的考虑因素，值得反思，是帧过滤器应尽量避免展开调用堆栈。某些堆栈可能很深，在某些情况下可能达到数万级。当帧过滤器执行时，搜索每个帧可能太昂贵了。帧过滤器无法知道它必须迭代多少帧，它可能必须迭代它们所有。这最终会复制[GDB]在打印帧时执行的工作。如果过滤器可以推迟展开帧，直到最后一个过滤器执行完毕并执行帧装饰器之后，它就应该这样做。有关装饰器的更多信息，请参阅[帧装饰器API]（Frame-Decorator-API.html#Frame-Decorator-API）。此外，后面几章中还有关于装饰器和过滤器的示例。有关更多信息，请参阅[编写帧过滤器]（Writing-a-Frame-Filter.html#Writing-a-Frame-Filter）。


The Python dictionary `gdb.frame_filters` contains key/object pairings that comprise a frame filter. Frame filters in this dictionary are called `global` frame filters, and they are available when debugging all inferiors. These frame filters must register with the dictionary directly. In addition to the `global` dictionary, there are other dictionaries that are loaded with different inferiors via auto-loading (see [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)). The two other areas where frame filter dictionaries can be found are: `gdb.Progspace` which contains a `frame_filters` dictionary attribute, and each `gdb.Objfile` object which also contains a `frame_filters` dictionary attribute.

> Python字典`gdb.frame_filters`包含键/对象对，构成一个帧过滤器。在调试所有次级时，这个字典中的帧过滤器被称为`全局`帧过滤器，它们必须直接注册到字典中。除了`全局`字典外，还有其他字典可以通过自动加载（参见[Python自动加载](Python-Auto_002dloading.html#Python-Auto_002dloading)）加载到不同的次级。另外两个可以找到帧过滤器字典的区域是：`gdb.Progspace`，它包含一个`frame_filters`字典属性，以及每个`gdb.Objfile`对象，它也包含一个`frame_filters`字典属性。


When a command is executed from [GDB] then prunes any frame filter whose `enabled` attribute is `False`. This pruned list is then sorted according to the `priority` attribute in each filter.

> 当从[GDB]执行命令时，将删除其`enabled`属性为`False`的任何帧过滤器。然后，根据每个过滤器中的`priority`属性对此删除的列表进行排序。


Once the dictionaries are combined, pruned and sorted, [GDB] creates an iterator which wraps each frame in the call stack in a `FrameDecorator` object, and calls each filter in order. The output from the previous filter will always be the input to the next filter, and so on.

> 一旦字典合并、修剪和排序，[GDB]就会创建一个迭代器，将调用堆栈中的每个帧包装在`FrameDecorator`对象中，并按顺序调用每个过滤器。上一个过滤器的输出将始终是下一个过滤器的输入，依此类推。


Frame filters have a mandatory interface which each frame filter must implement, defined here:

> 框架过滤器具有一个强制性的接口，每个框架过滤器必须实现，在这里定义：

Function: **FrameFilter.filter** *(iterator)*


:   [GDB] will call this method on a frame filter when it has reached the order in the priority list for that filter.

> 当GDB到达该过滤器的优先级列表中的顺序时，它将在帧过滤器上调用此方法。

```
For example, if there are four frame filters:

::: smallexample
``` smallexample
Name         Priority

Filter1      5
Filter2      10
Filter3      100
Filter4      1
```

:::

The order that the frame filters will be called is:

::: smallexample

```bash
Filter3 -> Filter2 -> Filter1 -> Filter4
```

:::

Note that the output from `Filter3` is passed to the input of `Filter2`, and so on.

This `filter` method is passed a Python iterator. This iterator contains a sequence of frame decorators that wrap each `gdb.Frame`, or a frame decorator that wraps another frame decorator. The first filter that is executed in the sequence of frame filters will receive an iterator entirely comprised of default `FrameDecorator` objects. However, after each frame filter is executed, the previous frame filter may have wrapped some or all of the frame decorators with their own frame decorator. As frame decorators must also conform to a mandatory interface, these decorators can be assumed to act in a uniform manner (see [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API)).

This method must return an object conforming to the Python iterator protocol. Each item in the iterator must be an object conforming to the frame decorator interface. If a frame filter does not wish to perform any operations on this iterator, it should return that iterator untouched.

This method is not optional. If it does not exist, [GDB] will raise and print an error.

```

```

<!-- -->

```

Variable: **FrameFilter.name**


:   The `name` attribute must be Python string which contains the name of the filter displayed by [GDB] (see [Frame Filter Management](Frame-Filter-Management.html#Frame-Filter-Management)). This attribute may contain any combination of letters or numbers. Care should be taken to ensure that it is unique. This attribute is mandatory.

> 该`name`属性必须是Python字符串，其中包含[GDB]显示的过滤器的名称（参见[帧过滤管理]（Frame-Filter-Management.html#Frame-Filter-Management））。此属性可以包含任何字母或数字的组合。应注意确保其唯一性。此属性是必需的。

```

<!-- -->

```

Variable: **FrameFilter.enabled**


:   The `enabled` attribute must be Python boolean. This attribute indicates to [GDB] whether the frame filter is enabled, and should be considered when frame filters are executed. If `enabled` is `True`, then the frame filter will be executed when any of the backtrace commands detailed earlier in this chapter are executed. If `enabled` is `False`, then the frame filter will not be executed. This attribute is mandatory.

> 属性`enabled`必须是Python布尔值。此属性指示[GDB]是否启用帧过滤器，并在执行帧过滤器时应考虑。如果`enabled`是`True`，则在执行本章前面详细介绍的任何回溯命令时将执行帧过滤器。如果`enabled`是`False`，则不会执行帧过滤器。此属性是必需的。

```

<!-- -->

```

Variable: **FrameFilter.priority**


:   The `priority` attribute must be Python integer. This attribute controls the order of execution in relation to other frame filters. There are no imposed limits on the range of `priority` other than it must be a valid integer. The higher the `priority` attribute, the sooner the frame filter will be executed in relation to other frame filters. Although `priority` can be negative, it is recommended practice to assume zero is the lowest priority that a frame filter can be assigned. Frame filters that have the same priority are executed in unsorted order in that priority slot. This attribute is mandatory. 100 is a good default priority.

> 属性`priority`必须是Python整数。此属性控制与其他帧过滤器相关的执行顺序。`priority`的范围没有强加的限制，只要是有效的整数即可。`priority`属性越高，帧过滤器将越早执行。尽管`priority`可以是负数，但建议认为零是帧过滤器可以被分配的最低优先级。具有相同优先级的帧过滤器将按照该优先级槽中无序执行。此属性是必需的。100是一个很好的默认优先级。

---

::: header
Next: [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API)]
:::
```
