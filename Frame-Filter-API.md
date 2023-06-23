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

Only commands that print a backtrace, or, in the case of [GDB/MI] commands (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)), those that return a collection of frames are affected. The commands that work with frame filters are:

`backtrace` (see [The backtrace command](Backtrace.html#backtrace_002dcommand)), `-stack-list-frames` (see [The -stack-list-frames command](GDB_002fMI-Stack-Manipulation.html#g_t_002dstack_002dlist_002dframes)), `-stack-list-variables` (see [The -stack-list-variables command](GDB_002fMI-Stack-Manipulation.html#g_t_002dstack_002dlist_002dvariables)), `-stack-list-arguments` see [The -stack-list-arguments command](GDB_002fMI-Stack-Manipulation.html#g_t_002dstack_002dlist_002darguments)) and `-stack-list-locals` (see [The -stack-list-locals command](GDB_002fMI-Stack-Manipulation.html#g_t_002dstack_002dlist_002dlocals)).

A frame filter works by taking an iterator as an argument, applying actions to the contents of that iterator, and returning another iterator (or, possibly, the same iterator it was provided in the case where the filter does not perform any operations). Typically, frame filters utilize tools such as the Python's `itertools` module to work with and create new iterators from the source iterator. Regardless of how a filter chooses to apply actions, it must not alter the underlying [GDB]. Frame filters are executed on a priority basis and care should be taken that some frame filters may have been executed before, and that some frame filters will be executed after.

An important consideration when designing frame filters, and well worth reflecting upon, is that frame filters should avoid unwinding the call stack if possible. Some stacks can run very deep, into the tens of thousands in some cases. To search every frame when a frame filter executes may be too expensive at that step. The frame filter cannot know how many frames it has to iterate over, and it may have to iterate through them all. This ends up duplicating effort as [GDB] performs this iteration when it prints the frames. If the filter can defer unwinding frames until frame decorators are executed, after the last filter has executed, it should. See [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API), for more information on decorators. Also, there are examples for both frame decorators and filters in later chapters. See [Writing a Frame Filter](Writing-a-Frame-Filter.html#Writing-a-Frame-Filter), for more information.

The Python dictionary `gdb.frame_filters` contains key/object pairings that comprise a frame filter. Frame filters in this dictionary are called `global` frame filters, and they are available when debugging all inferiors. These frame filters must register with the dictionary directly. In addition to the `global` dictionary, there are other dictionaries that are loaded with different inferiors via auto-loading (see [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)). The two other areas where frame filter dictionaries can be found are: `gdb.Progspace` which contains a `frame_filters` dictionary attribute, and each `gdb.Objfile` object which also contains a `frame_filters` dictionary attribute.

When a command is executed from [GDB] then prunes any frame filter whose `enabled` attribute is `False`. This pruned list is then sorted according to the `priority` attribute in each filter.

Once the dictionaries are combined, pruned and sorted, [GDB] creates an iterator which wraps each frame in the call stack in a `FrameDecorator` object, and calls each filter in order. The output from the previous filter will always be the input to the next filter, and so on.

Frame filters have a mandatory interface which each frame filter must implement, defined here:

Function: **FrameFilter.filter** *(iterator)*

:   [GDB] will call this method on a frame filter when it has reached the order in the priority list for that filter.

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

```

<!-- -->

```

Variable: **FrameFilter.enabled**

:   The `enabled` attribute must be Python boolean. This attribute indicates to [GDB] whether the frame filter is enabled, and should be considered when frame filters are executed. If `enabled` is `True`, then the frame filter will be executed when any of the backtrace commands detailed earlier in this chapter are executed. If `enabled` is `False`, then the frame filter will not be executed. This attribute is mandatory.

```

<!-- -->

```

Variable: **FrameFilter.priority**

:   The `priority` attribute must be Python integer. This attribute controls the order of execution in relation to other frame filters. There are no imposed limits on the range of `priority` other than it must be a valid integer. The higher the `priority` attribute, the sooner the frame filter will be executed in relation to other frame filters. Although `priority` can be negative, it is recommended practice to assume zero is the lowest priority that a frame filter can be assigned. Frame filters that have the same priority are executed in unsorted order in that priority slot. This attribute is mandatory. 100 is a good default priority.

---

::: header
Next: [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API)]
:::
```
