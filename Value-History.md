---
description: Value History (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Value History (Debugging with GDB)
lang: en
resource-type: document
title: Value History (Debugging with GDB)
---
::: header
Next: [Convenience Vars](Convenience-Vars.html#Convenience-Vars)]
:::

---

### 10.11 Value History

Values printed by the `print` command are saved in the [GDB] *value history*. This allows you to refer to them in other expressions. Values are kept until the symbol table is re-read or discarded (for example with the `file` or `symbol-file` commands). When the symbol table changes, the value history is discarded, since the values may contain pointers back to the types defined in the symbol table.

The values printed are given *history numbers* by which you can refer to them. These are successive integers starting with one. `print` shows you the history number assigned to a value by printing '`$num = ` is the history number.

To refer to any previous value, use '`$` th value from the end; `$$2` is the value just prior to `$$`, `$$1` is equivalent to `$$`, and `$$0` is equivalent to `$`.

For example, suppose you have just printed a pointer to a structure and want to see the contents of the structure. It suffices to type

::: smallexample

```bash
p *$
```

:::

If you have a chain of structures where the component `next` points to the next one, you can print the contents of the next one with this:

::: smallexample

```bash
p *$.next
```

:::

You can print successive links in the chain by repeating this command---which you can do by just typing RET.

Note that the history records values, not expressions. If the value of `x` is 4 and you type these commands:

::: smallexample

```bash
print x
set x=5
```

:::

then the value recorded in the value history by the `print` command remains 4 even though the value of `x` has changed.

`show values`

Print the last ten values in the value history, with their item numbers. This is like '`p $$9`' repeated ten times, except that `show values` does not change the history.

`show values n`

Print ten history values centered on history item number `n`.

`show values +`

Print ten history values just after the values last printed. If no more values are available, `show values +` produces no display.

Pressing RET to repeat `show values n` has exactly the same effect as '`show values +`'.

---

::: header
Next: [Convenience Vars](Convenience-Vars.html#Convenience-Vars)]
:::
