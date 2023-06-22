---
description: Introduction and Notation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Introduction and Notation (Debugging with GDB)
lang: en
resource-type: document
title: Introduction and Notation (Debugging with GDB)
---
::: header
Next: [Readline Interaction](Readline-Interaction.html#Readline-Interaction)]
:::

---

### 33.1 Introduction to Line Editing

The following paragraphs describe the notation used to represent keystrokes.

The text [C-k] is read as 'Control-K' and describes the character produced when the k key is pressed while the Control key is depressed.

The text [M-k] is read as 'Meta-K' and describes the character produced when the Meta key (if you have one) is depressed, and the k key is pressed. The Meta key is labeled ALT on many keyboards. On keyboards with two keys labeled ALT (usually to either side of the space bar), the ALT on the left side is generally set to work as a Meta key. The ALT key on the right may also be configured to work as a Meta key or may be configured as some other modifier, such as a Compose key for typing accented characters.

If you do not have a Meta or ALT key, or another key working as a Meta key, the identical keystroke can be generated by typing ESC *first*, and then typing k. Either process is known as *metafying* the k key.

The text [M-C-k].

In addition, several keys have their own names. Specifically, DEL, ESC, LFD, SPC, RET, and TAB all stand for themselves when seen in this text, or in an init file (see [Readline Init File](Readline-Init-File.html#Readline-Init-File)). If your keyboard lacks a LFD key, typing C-j will produce the desired character. The RET key may be labeled Return or Enter on some keyboards.

---

::: header
Next: [Readline Interaction](Readline-Interaction.html#Readline-Interaction)]
:::