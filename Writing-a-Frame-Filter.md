---
tip: translate by openai@2023-06-23 15:44:33
...
---
description: Writing a Frame Filter (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Writing a Frame Filter (Debugging with GDB)
lang: en
resource-type: document
title: Writing a Frame Filter (Debugging with GDB)
---
::: header
Next: [Unwinding Frames in Python](Unwinding-Frames-in-Python.html#Unwinding-Frames-in-Python)]
:::

---

#### 23.3.2.11 Writing a Frame Filter


There are three basic elements that a frame filter must implement: it must correctly implement the documented interface (see [Frame Filter API](Frame-Filter-API.html#Frame-Filter-API)), it must register itself with [GDB]. In all cases, whether it works on the iterator or not, each frame filter must return an iterator. A bare-bones frame filter follows the pattern in the following example.

> 三个基本元素必须实现帧过滤器：它必须正确实现文档中定义的接口（参见[帧过滤器API] (Frame-Filter-API.html#Frame-Filter-API)），它必须向[GDB]注册自己。无论是否在迭代器上工作，每个帧过滤器都必须返回一个迭代器。最基本的帧过滤器遵循以下示例中的模式。

::: smallexample

```bash
import gdb

class FrameFilter():

    def __init__(self):
        # Frame filter attribute creation.
        #
        # 'name' is the name of the filter that GDB will display.
        #
        # 'priority' is the priority of the filter relative to other
        # filters.
        #
        # 'enabled' is a boolean that indicates whether this filter is
        # enabled and should be executed.

        self.name = "Foo"
        self.priority = 100
        self.enabled = True

        # Register this frame filter with the global frame_filters
        # dictionary.
        gdb.frame_filters[self.name] = self

    def filter(self, frame_iter):
        # Just return the iterator.
        return frame_iter
```

:::


The frame filter in the example above implements the three requirements for all frame filters. It implements the API, self registers, and makes a decision on the iterator (in this case, it just returns the iterator untouched).

> 例中的帧过滤器实现了所有帧过滤器的三个要求。它实现了API，自我注册，并对迭代器做出决定（在本例中，它只是原样返回迭代器）。


The first step is attribute creation and assignment, and as shown in the comments the filter assigns the following attributes: `name`, `priority` and whether the filter should be enabled with the `enabled` attribute.

> 第一步是属性创建和分配，正如注释中所示，过滤器将分配以下属性：`name`、`priority`以及是否使用`enabled`属性启用过滤器。


The second step is registering the frame filter with the dictionary or dictionaries that the frame filter has interest in. As shown in the comments, this filter just registers itself with the global dictionary `gdb.frame_filters`. As noted earlier, `gdb.frame_filters` is a dictionary that is initialized in the `gdb` module when [GDB] exits. To avoid filters that may conflict, it is generally better to register frame filters against the dictionaries that more closely align with the usage of the filter currently in question. See [Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading), for further information on auto-loading Python scripts.

> 第二步是将帧过滤器注册到帧过滤器感兴趣的字典或字典中。如注释所示，此过滤器只需注册到全局字典`gdb.frame_filters`中即可。前面提到，`gdb.frame_filters`是在[GDB]退出时在`gdb`模块中初始化的字典。为避免可能发生冲突的过滤器，通常最好将帧过滤器注册到与当前问题的过滤器使用更紧密相关的字典中。有关自动加载Python脚本的更多信息，请参阅[Python自动加载](Python-Auto_002dloading.html#Python-Auto_002dloading)。


[GDB] will display are those contained in the `name` attribute.

> GDB 将显示包含在“name”属性中的内容。


The final step of this example is the implementation of the `filter` method. As shown in the example comments, we define the `filter` method and note that the method must take an iterator, and also must return an iterator. In this bare-bones example, the frame filter is not very useful as it just returns the iterator untouched. However this is a valid operation for frame filters that have the `enabled` attribute set, but decide not to operate on any frames.

> 本例的最后一步是实现`filter`方法。正如示例注释中所示，我们定义`filter`方法，并注意该方法必须接受一个迭代器，也必须返回一个迭代器。在这个简陋的示例中，帧过滤器没有什么用，因为它只是原样返回迭代器。但是，对于具有“enabled”属性设置的帧过滤器来说，这是一个有效的操作，但它决定不对任何帧进行操作。


In the next example, the frame filter operates on all frames and utilizes a frame decorator to perform some work on the frames. See [Frame Decorator API](Frame-Decorator-API.html#Frame-Decorator-API), for further information on the frame decorator interface.

> 在下一个例子中，帧过滤器对所有帧进行操作，并使用帧装饰器来对帧执行一些工作。有关帧装饰器界面的更多信息，请参见[帧装饰器API](Frame-Decorator-API.html#Frame-Decorator-API)。


This example works on inlined frames. It highlights frames which are inlined by tagging them with an "\[inlined]" tag. By applying a frame decorator to all frames with the Python `itertools imap` method, the example defers actions to the frame decorator. Frame decorators are only processed when [GDB] prints the backtrace.

> 这个例子适用于内联框架。它通过用"\[inlined]"标记来突出内联框架。通过使用Python `itertools imap` 方法对所有框架应用框架装饰器，该示例将操作委托给框架装饰器。只有在[GDB]打印回溯时，才会处理框架装饰器。


This introduces a new decision making topic: whether to perform decision making operations at the filtering step, or at the printing step. In this example's approach, it does not perform any filtering decisions at the filtering step beyond mapping a frame decorator to each frame. This allows the actual decision making to be performed when each frame is printed. This is an important consideration, and well worth reflecting upon when designing a frame filter. An issue that frame filters should avoid is unwinding the stack if possible. Some stacks can run very deep, into the tens of thousands in some cases. To search every frame to determine if it is inlined ahead of time may be too expensive at the filtering step. The frame filter cannot know how many frames it has to iterate over, and it would have to iterate through them all. This ends up duplicating effort as [GDB] performs this iteration when it prints the frames.

> 这引入了一个新的决策主题：是在过滤步骤中执行决策操作，还是在打印步骤中执行决策操作。在本例的方法中，除了将帧装饰器映射到每个帧之外，不会在过滤步骤中执行任何过滤决策。这允许在打印每个帧时执行实际决策。这是一个重要的考虑因素，在设计帧过滤器时值得反思。帧过滤器应该避免的一个问题是尽可能避免展开堆栈。一些堆栈可能会非常深，在某些情况下可能会达到数万。在过滤步骤之前搜索每个帧可能太昂贵了。帧过滤器不知道它必须迭代多少帧，它必须迭代它们所有。这最终会重复[GDB]在打印帧时所做的迭代工作。


In this example decision making can be deferred to the printing step. As each frame is printed, the frame decorator can examine each frame in turn when [GDB] iterates. From a performance viewpoint, this is the most appropriate decision to make as it avoids duplicating the effort that the printing step would undertake anyway. Also, if there are many frame filters unwinding the stack during filtering, it can substantially delay the printing of the backtrace which will result in large memory usage, and a poor user experience.

> 在这个例子中，决策可以推迟到打印步骤。当[GDB]迭代时，每张框架都会被打印，框架装饰器可以逐一检查每个框架。从性能角度来看，这是最合适的决策，因为它避免了重复打印步骤所做的努力。此外，如果有许多帧过滤器在过滤堆栈期间解开，它可能会显著延迟回溯的打印，从而导致大量内存使用和差的用户体验。

::: smallexample

```bash
class InlineFilter():

    def __init__(self):
        self.name = "InlinedFrameFilter"
        self.priority = 100
        self.enabled = True
        gdb.frame_filters[self.name] = self

    def filter(self, frame_iter):
        frame_iter = itertools.imap(InlinedFrameDecorator,
                                    frame_iter)
        return frame_iter
```

:::


This frame filter is somewhat similar to the earlier example, except that the `filter` method applies a frame decorator object called `InlinedFrameDecorator` to each element in the iterator. The `imap` Python method is light-weight. It does not proactively iterate over the iterator, but rather creates a new iterator which wraps the existing one.

> 这个帧过滤器与前面的例子有些相似，除了`filter`方法将一个叫做`InlinedFrameDecorator`的帧装饰器对象应用于迭代器中的每个元素。`imap` Python方法是轻量级的，它不会主动遍历迭代器，而是创建一个新的迭代器，用来包装现有的迭代器。


Below is the frame decorator for this example.

> 以下是本例的框架装饰器。

::: smallexample

```bash
class InlinedFrameDecorator(FrameDecorator):

    def __init__(self, fobj):
        super(InlinedFrameDecorator, self).__init__(fobj)

    def function(self):
        frame = self.inferior_frame()
        name = str(frame.name())

        if frame.type() == gdb.INLINE_FRAME:
            name = name + " [inlined]"

        return name
```

:::


This frame decorator only defines and overrides the `function` method. It lets the supplied `FrameDecorator`, which is shipped with [GDB], perform the other work associated with printing this frame.

> 这个帧装饰器只定义和覆盖`function`方法。它允许提供的`FrameDecorator`（随[GDB]一起发货）执行与打印此帧相关的其他工作。


The combination of these two objects create this output from a backtrace:

> 这两个对象的组合产生了回溯的输出。

::: smallexample

```bash
#0  0x004004e0 in bar () at inline.c:11
#1  0x00400566 in max [inlined] (b=6, a=12) at inline.c:21
#2  0x00400566 in main () at inline.c:31
```

:::


So in the case of this example, a frame decorator is applied to all frames, regardless of whether they may be inlined or not. As [GDB] executes each frame decorator which then makes a decision on what to print in the `function` callback. Using a strategy like this is a way to defer decisions on the frame content to printing time.

> 在这个例子中，无论是否内联，帧装饰器都会应用于所有帧。当[GDB]执行每个帧装饰器时，它会在`function`回调中做出决定打印什么。使用这种策略可以将决定帧内容的决定推迟到打印时间。

#### Eliding Frames


It might be that the above example is not desirable for representing inlined frames, and a hierarchical approach may be preferred. If we want to hierarchically represent frames, the `elided` frame decorator interface might be preferable.

> 可能上面的示例不适合用于表示内联框架，可能更倾向于使用分层方法。如果我们想要以分层方式表示框架，可能更喜欢使用`elided`框架装饰器接口。


This example approaches the issue with the `elided` method. This example is quite long, but very simplistic. It is out-of-scope for this section to write a complete example that comprehensively covers all approaches of finding and printing inlined frames. However, this example illustrates the approach an author might use.

> 这个例子使用“省略”的方法来处理这个问题。这个例子很长，但非常简单。在本节中，不适合编写一个完整的例子来全面覆盖所有找到和打印内联帧的方法。但是，这个例子说明了作者可能使用的方法。


This example comprises of three sections.

> 这个例子包括三个部分。

::: smallexample

```bash
class InlineFrameFilter():

    def __init__(self):
        self.name = "InlinedFrameFilter"
        self.priority = 100
        self.enabled = True
        gdb.frame_filters[self.name] = self

    def filter(self, frame_iter):
        return ElidingInlineIterator(frame_iter)
```

:::


This frame filter is very similar to the other examples. The only difference is this frame filter is wrapping the iterator provided to it (`frame_iter`) with a custom iterator called `ElidingInlineIterator`. This again defers actions to when [GDB] prints the backtrace, as the iterator is not traversed until printing.

> 这个帧过滤器与其他示例非常相似。唯一的区别是它使用一个叫做ElidingInlineIterator的自定义迭代器包装提供给它的迭代器（`frame_iter`）。这又将行为推迟到[GDB]打印回溯时，因为在打印之前不会遍历迭代器。


The iterator for this example is as follows. It is in this section of the example where decisions are made on the content of the backtrace.

> 这个例子的迭代器如下所示。在这个例子的这部分，将对回溯内容做出决定。

::: smallexample

```bash
class ElidingInlineIterator:
    def __init__(self, ii):
        self.input_iterator = ii

    def __iter__(self):
        return self

    def next(self):
        frame = next(self.input_iterator)

        if frame.inferior_frame().type() != gdb.INLINE_FRAME:
            return frame

        try:
            eliding_frame = next(self.input_iterator)
        except StopIteration:
            return frame
        return ElidingFrameDecorator(eliding_frame, [frame])
```

:::


This iterator implements the Python iterator protocol. When the `next` function is called (when [GDB] prints each frame), the iterator checks if this frame decorator, `frame`, is wrapping an inlined frame. If it is not, it returns the existing frame decorator untouched. If it is wrapping an inlined frame, it assumes that the inlined frame was contained within the next oldest frame, `eliding_frame`, which it fetches. It then creates and returns a frame decorator, `ElidingFrameDecorator`, which contains both the elided frame, and the eliding frame.

> 这个迭代器实现了Python迭代器协议。当调用`next`函数时（当[GDB]打印每个帧时），迭代器会检查这个帧装饰器`frame`是否包装了一个内联帧。如果不是，它会原样返回现有的帧装饰器。如果它包装了一个内联帧，它假定内联帧包含在下一个最古老的帧`eliding_frame`中，它会获取它。然后它会创建并返回一个帧装饰器`ElidingFrameDecorator`，它包含被省略的帧和省略的帧。

::: smallexample

```bash
class ElidingInlineDecorator(FrameDecorator):

    def __init__(self, frame, elided_frames):
        super(ElidingInlineDecorator, self).__init__(frame)
        self.frame = frame
        self.elided_frames = elided_frames

    def elided(self):
        return iter(self.elided_frames)
```

:::


This frame decorator overrides one function and returns the inlined frame in the `elided` method. As before it lets `FrameDecorator` do the rest of the work involved in printing this frame. This produces the following output.

> 这个框架装饰器重写了一个函数，并在`elided`方法中返回内联框架。正如之前，它让`FrameDecorator`完成打印此框架所涉及的其余工作。这将产生以下输出。

::: smallexample

```bash
#0  0x004004e0 in bar () at inline.c:11
#2  0x00400529 in main () at inline.c:25
    #1  0x00400529 in max (b=6, a=12) at inline.c:15
```

:::


In that output, `max` which has been inlined into `main` is printed hierarchically. Another approach would be to combine the `function` method, and the `elided` method to both print a marker in the inlined frame, and also show the hierarchical relationship.

> 在那个输出中，内联到`main`中的`max`被层级地打印出来。另一种方法是结合`function`方法和`elided`方法，以便在内联框架中打印一个标记，并显示层级关系。

---

::: header
Next: [Unwinding Frames in Python](Unwinding-Frames-in-Python.html#Unwinding-Frames-in-Python)]
:::
