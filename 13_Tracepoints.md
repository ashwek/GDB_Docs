# 13 Tracepoints

----

In some applications, it is not feasible for the debugger to interrupt the program’s execution long enough for the developer to learn anything helpful about its behavior. If the program’s correctness depends on its real-time behavior, delays introduced by a debugger might cause the program to change its behavior drastically, or perhaps fail, even when the code itself is correct. **It is useful to be able to observe the program’s behavior without interrupting it.**

Using GDB’s **trace** and **collect** commands, you can specify locations in the program, called _tracepoints_, and arbitrary expressions to evaluate when those tracepoints are reached. Later, using the **tfind** command, you can examine the values those expressions had when the program hit the tracepoints.

The expressions may also denote objects in memory - structures or arrays, for example - whose values GDB should record; while visiting a particular tracepoint, you may inspect those objects as if they were in memory at that moment. However, because GDB records these values without interacting with you, it can do so quickly and unobtrusively, hopefully not disturbing the program’s behavior.

The tracepoint facility is currently available only for _remote_ targets.
