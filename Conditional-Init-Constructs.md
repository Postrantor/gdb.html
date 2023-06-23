---
description: Conditional Init Constructs (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Conditional Init Constructs (Debugging with GDB)
lang: en
resource-type: document
title: Conditional Init Constructs (Debugging with GDB)
---
::: header
Next: [Sample Init File](Sample-Init-File.html#Sample-Init-File)]
:::

---

#### 33.3.2 Conditional Init Constructs

Readline implements a facility similar in spirit to the conditional compilation features of the C preprocessor which allows key bindings and variable settings to be performed as the result of tests. There are four parser directives used.

`$if`

:   The `$if` construct allows bindings to be made based on the editing mode, the terminal being used, or the application using Readline. The text of the test, after any comparison operator, extends to the end of the line; unless otherwise noted, no characters are required to isolate it.

```
`mode`

:   The `mode=` form of the `$if` directive is used to test whether Readline is in `emacs` or `vi` mode. This may be used in conjunction with the '`set keymap`' command, for instance, to set bindings in the `emacs-standard` and `emacs-ctlx` keymaps only if Readline is starting out in `emacs` mode.

`term`

:   The `term=` form may be used to include terminal-specific key bindings, perhaps to bind the key sequences output by the terminal's function keys. The word on the right side of the '`=`'. This allows `sun` to match both `sun` and `sun-cmd`, for instance.

`version`

:   The `version` test may be used to perform comparisons against specific Readline versions. The `version` expands to the current Readline version. The set of comparison operators includes '`=`'. The operator may be separated from the string `version` and from the version number argument by whitespace. The following example sets a variable if the Readline version being used is 7.0 or newer:

    ::: example
    ``` example
    $if version >= 7.0
    set show-mode-in-prompt on
    $endif
    ```
    :::

`application`

:   The `application`, and you can test for a particular value. This could be used to bind key sequences to functions useful for a specific program. For instance, the following command adds a key sequence that quotes the current or previous word in Bash:

    ::: example
    ``` example
    $if Bash
    # Quote the current or previous word
    "\C-xq": "\eb\"\ef\""
    $endif
    ```
    :::

`variable`

:   The `variable`. The following example is equivalent to the `mode=emacs` test described above:

    ::: example
    ``` example
    $if editing-mode == emacs
    set show-mode-in-prompt on
    $endif
    ```
    :::
```

`$endif`

:   This command, as seen in the previous example, terminates an `$if` command.

`$else`

:   Commands in this branch of the `$if` directive are executed if the test fails.

`$include`

:   This directive takes a single filename as an argument and reads commands and bindings from that file. For example, the following directive reads from `/etc/inputrc`:

```
::: example
``` example
$include /etc/inputrc
```

:::

```

---

::: header
Next: [Sample Init File](Sample-Init-File.html#Sample-Init-File)]
:::
```
