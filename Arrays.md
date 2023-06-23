---
description: Arrays (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Arrays (Debugging with GDB)
lang: en
resource-type: document
title: Arrays (Debugging with GDB)
---
::: header
Next: [Output Formats](Output-Formats.html#Output-Formats)]
:::

---

### 10.4 Artificial Arrays

It is often useful to print out several successive objects of the same type in memory; a section of an array, or an array of dynamically determined size for which only a pointer exists in the program.

You can do this by referring to a contiguous span of memory as an *artificial array*, using the binary operator '`@`' should be the first element of the desired array and be an individual object. The right operand should be the desired length of the array. The result is an array value whose elements are all of the type of the left argument. The first element is actually the left argument; the second element comes from bytes of memory immediately following those that hold the first element, and so on. Here is an example. If a program says

::: smallexample

```bash
int *array = (int *) malloc (len * sizeof (int));
```

:::

you can print the contents of `array` with

::: smallexample

```bash
p *array@len
```

:::

The left operand of '`@`' in this way behave just like other arrays in terms of subscripting, and are coerced to pointers when used in expressions. Artificial arrays most often appear in expressions via the value history (see [Value History](Value-History.html#Value-History)), after printing one out.

Another way to create an artificial array is to use a cast. This re-interprets a value as if it were an array. The value need not be in memory:

::: smallexample

```bash
(gdb) p/x (short[2])0x12345678
$1 = 
```

:::

As a convenience, if you leave the array length out (as in '`(type)value`':

::: smallexample

```bash
(gdb) p/x (short)0x12345678
$2 = 
```

:::

Sometimes the artificial array mechanism is not quite enough; in moderately complex data structures, the elements of interest may not actually be adjacent---for example, if you are interested in the values of pointers in an array. One useful work-around in this situation is to use a convenience variable (see [Convenience Variables](Convenience-Vars.html#Convenience-Vars)) as a counter in an expression that prints the first interesting value, and then repeat that expression via RET. For instance, suppose you have an array `dtab` of pointers to structures, and you are interested in the values of a field `fv` in each structure. Here is an example of what you might type:

::: smallexample

```bash
set $i = 0
p dtab[$i++]->fv
RET
RET
…
```

:::

---

::: header
Next: [Output Formats](Output-Formats.html#Output-Formats)]
:::
