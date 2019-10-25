# 4.12 Setting a Bookmark to Return to Later

[Go Back](./4_Running_Programs_Under_GDB.md)

----

On certain operating systems, GDB is able to _save a snapshot of a program_’s state, called a **checkpoint**, and come back to it later.

Returning to a _checkpoint_ effectively undoes everything that has happened in the program since the checkpoint was saved. This includes changes in memory, registers, and even (within some limits) system state. Effectively, it is like going back in time to the moment when the checkpoint was saved.

Thus, if you’re stepping thru a program and you think you’re getting close to the point where things go wrong, you can save a checkpoint. Then, if you accidentally go too far and miss the critical statement, instead of having to restart your program from the beginning, you can just go back to the checkpoint and start again from there. This can be especially useful if it takes a lot of time or steps to reach the point where you think the bug occurs.

To use the checkpoint/restart method of debugging:

```
checkpoint
```
Save a snapshot of the debugged program’s current execution state. The ``checkpoint`` command takes no arguments, but each checkpoint is assigned a small integer id, similar to a breakpoint id.

```
info checkpoints
```
List the checkpoints that have been saved in the current debugging session. For each checkpoint, the following information will be listed: Checkpoint ID, Process ID, Code Address, Source line

```
restart checkpoint-id
```
Restore the program state that was saved as checkpoint number _checkpoint-id_. All program variables, registers, stack frames etc. will be returned to the values that they had when the checkpoint was saved. In essence, gdb will “wind back the clock” to the point in time when the checkpoint was saved.

```
delete checkpoint checkpoint-id
```
Delete the previously-saved checkpoint identified by checkpoint-id.

Returning to a previously saved checkpoint will restore the user state of the program being debugged, plus a significant subset of the system (OS) state, including file pointers. It won’t “un-write” data from a file, but it will rewind the file pointer to the previous location, so that the previously written data can be overwritten. For files opened in read mode, the pointer will also be restored so that the previously read data can be read again.

Of course, characters that have been sent to a printer (or other external device) cannot be “snatched back”, and characters received from eg. a serial device can be removed from internal program buffers, but they cannot be “pushed back” into the serial pipeline, ready to be received again. Similarly, the actual contents of files that have been changed cannot be restored (at this time).

Finally, there is one bit of internal program state that will be different when you return to a checkpoint — the program’s process id. _Each checkpoint will have a unique process id (or pid), and each will be different from the program’s original pid._ If your program has saved a local copy of its process id, this could potentially pose a problem.

### 4.12.1 A Non-obvious Benefit of Using Checkpoints

On some systems such as GNU/Linux, address space randomization is performed on new processes for security reasons. This makes it difficult or impossible to set a breakpoint, or watchpoint, on an absolute address if you have to restart the program, since the absolute location of a symbol will change from one execution to the next.

A checkpoint, however, is an identical copy of a process. Therefore if you create a checkpoint at (eg.) the start of main, and simply return to that checkpoint instead of restarting the process, you can avoid the effects of address randomization and your symbols will all stay in the same place.
