---
tip: translate by openai@2023-06-23 20:28:35
...
---
description: Declarations (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Declarations (Debugging with GDB)
lang: en
resource-type: document
title: Declarations (Debugging with GDB)
---
::: header
Next: [Registering Code](Registering-Code.html#Registering-Code)]
:::

---

### 30.1 JIT Declarations


These are the relevant struct declarations that a C program should include to implement the interface:

> 这些是实现接口所需的相关结构声明：

::: smallexample

```bash
typedef enum
{
  JIT_NOACTION = 0,
  JIT_REGISTER_FN,
  JIT_UNREGISTER_FN
} jit_actions_t;

struct jit_code_entry
{
  struct jit_code_entry *next_entry;
  struct jit_code_entry *prev_entry;
  const char *symfile_addr;
  uint64_t symfile_size;
};

struct jit_descriptor
{
  uint32_t version;
  /* This type should be jit_actions_t, but we use uint32_t
     to be explicit about the bitwidth.  */
  uint32_t action_flag;
  struct jit_code_entry *relevant_entry;
  struct jit_code_entry *first_entry;
};

/* GDB puts a breakpoint in this function.  */
void __attribute__((noinline)) __jit_debug_register_code() ;

/* Make sure to specify the version statically, because the
   debugger may check the version before we can set it.  */
struct jit_descriptor __jit_debug_descriptor = ;
```

:::


If the JIT is multi-threaded, then it is important that the JIT synchronize any modifications to this global data properly, which can easily be done by putting a global mutex around modifications to these structures.

> 如果JIT是多线程的，那么重要的是JIT通过在这些结构的修改周围放置一个全局互斥量来正确同步对这些全局数据的任何修改。
