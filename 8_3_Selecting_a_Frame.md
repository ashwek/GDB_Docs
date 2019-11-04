# 8.3 Selecting a Frame

----

Most commands for examining the stack and other data in your program work on whichever stack frame is selected at the moment. Here are the commands for selecting a stack frame; all of them finish by printing a brief description of the stack frame just selected.

```
frame [ frame-selection-spec ]
f [ frame-selection-spec ]
```
The ``frame`` command allows different stack frames to be selected. The _frame-selection-spec_ can be any of the following:

```
num
level num
```
Select frame level _num_. Recall that frame zero is the innermost (currently executing) frame, frame one is the frame that called the innermost one, and so on. The highest level frame is usually the one for main.

As this is the most common method of navigating the frame stack, the string _level_ can be omitted.

```
address stack-address
```
Select the frame with stack address _stack-address_. The stack-address for a frame can be seen in the output of ``info frame``, for example:

```
(gdb) info frame
Stack level 4, frame at 0x7fffffffddc0:
rip = 0x55555555468e in main (Xu.c:11); saved rip = 0x7ffff7a05b97
caller of frame at 0x7fffffffdda0
Arglist at 0x7fffffffddb0, args:
Locals at 0x7fffffffddb0, Previous frame's sp is 0x7fffffffddc0
Saved registers:
 rbp at 0x7fffffffddb0, rip at 0x7fffffffddb8
```
The stack-address for this frame is 0x7fffffffddc0.

```
function function-name
```
Select the stack frame for function _function-name_. If there are multiple stack frames for function _function-name_ then the inner most stack frame is selected.

```
view stack-address [ pc-addr ]
```
View a frame that is not part of GDB’s backtrace. The frame viewed has stack address _stack-addr_, and optionally, a program counter address of pc-addr.

```
up n
```
Move _n_ frames up the stack; _n_ defaults to 1. For positive numbers _n_, this advances toward the outermost frame, to higher frame numbers, to frames that have existed longer.

```
down n
```
Move _n_ frames down the stack; _n_ defaults to 1. For positive numbers _n_, this advances toward the innermost frame, to lower frame numbers, to frames that were created more recently.

```
select-frame [ frame-selection-spec ]
```
The ``select-frame`` command is a variant of frame that does not display the new frame after selecting it. This command is intended primarily for use in GDB command scripts.

```
up-silently n
down-silently n
```
These two commands are variants of ``up`` and ``down``, respectively; they differ in that they do their work silently, without causing display of the new frame.
