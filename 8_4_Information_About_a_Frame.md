# 8.4 Information About a Frame

----

There are several other commands to print information about the selected stack frame.

```
frame
f
```
When used without any argument, this command does not change which frame is selected, but prints a brief description of the currently selected stack frame. With an argument, this command is used to select a stack frame.

```
info frame
```
This command prints a verbose description of the selected stack frame, including:

 - _the address of the frame_
 - _the address of the next frame down (called by this frame)_
 - _the address of the next frame up (caller of this frame)_
 - _the language in which the source code corresponding to this frame is written_
 - _the address of the frame’s arguments_
 - _the address of the frame’s local variables_
 - _the program counter saved in it (the address of execution in the caller frame)_
 - _which registers were saved in the frame_


```
(gdb) select-frame 1
(gdb) info frame
Stack level 1, frame at 0x7fffffffdd60:
 rip = 0x55555555466f in fact (Xu.c:5); saved rip = 0x55555555466f
 called by frame at 0x7fffffffdd80, caller of frame at 0x7fffffffdd40
 source language c.
 Arglist at 0x7fffffffdd50, args: num=3
 Locals at 0x7fffffffdd50, Previous frame's sp is 0x7fffffffdd60
 Saved registers:
  rbp at 0x7fffffffdd50, rip at 0x7fffffffdd58
```

```
info frame [ frame-selection-spec ]
info f [ frame-selection-spec ]
```
Print a verbose description of the frame selected by _frame-selection-spec_. The _frame-selection-spec_ is the same as for the ``frame`` command.

```
info args [-q] [-t type_regexp] [regexp]
```
Like ``info args``, but only print the arguments selected with the provided _regexp_.

```
info locals [-q] [-t type_regexp] [regexp]
```
Like ``info locals``, but only print the local variables selected with the provided _regexp_.
