# 6 Running programs backward

----

_GDB's built-in record and replay has severe limitations, e.g. no support for **AVX instructions**. Some builtins use AVX instructions so GDB might fail._

When you are debugging a program, it is not unusual to realize that you have gone too far, and some event of interest has already happened. If the target environment supports it, GDB can allow you to “rewind” the program by running it backward.

A target environment that supports reverse execution should be able to “undo” the changes in machine state that have taken place as the program was executing normally. Variables, registers etc. should revert to their previous values. Obviously this requires a great deal of sophistication on the part of the target environment; not all target environments can support reverse execution.

When a program is executed in reverse, the instructions that have most recently been executed are “un-executed”, in reverse order. The program counter runs backward, following the previous thread of execution in reverse. As each instruction is “un-executed”, the values of memory and/or registers that were changed by that instruction are reverted to their previous states. After executing a piece of source code in reverse, all side effects of that code should be “undone”, and all variables should be returned to their prior values6.

On some platforms, GDB has built-in support for reverse execution, activated with the ``record`` or ``record btrace`` commands.

If you are debugging in a target environment that supports reverse execution, GDB provides the following commands.

```
reverse-continue [ignore-count]
rc [ignore-count]
```
Beginning at the point where your program last stopped, start executing in reverse. Reverse execution will stop for breakpoints and synchronous exceptions (signals), just like normal execution. Behavior of asynchronous signals depends on the target environment.

```
reverse-step [count]
```
Run the program backward until control reaches the start of a different source line; then stop it, and return control to GDB.

Like the ``step`` command, ``reverse-step`` will only stop at the beginning of a source line. It “un-executes” the previously executed source line. If the previous source line included calls to debuggable functions, ``reverse-step`` will step (backward) into the called function, stopping at the beginning of the last statement in the called function.

```
reverse-stepi [count]
```
Reverse-execute one machine instruction.

```
reverse-next [count]
```
Run backward to the beginning of the previous line executed in the current (innermost) stack frame.

```
reverse-nexti [count]
```
Like ``nexti``, ``reverse-nexti`` executes a single instruction in reverse, except that called functions are “un-executed” atomically.

```
reverse-finish
```
Just as the ``finish`` command takes you to the point where the current function returns, ``reverse-finish`` takes you to the point where it was called. Instead of ending up at the end of the current function invocation, you end up at the beginning.

```
set exec-direction
```
Set the direction of target execution.

```
set exec-direction reverse
```
GDB will perform all execution commands in reverse, until the exec-direction mode is changed to “forward”. Affected commands include ``step``, ``stepi``, ``next``, ``nexti``, ``continue``, and ``finish``.

```
set exec-direction forward
```
GDB will perform all execution commands in the normal fashion. This is the default.

Note that some side effects are easier to undo than others. For instance, memory and registers are relatively easy, but device I/O is hard. Some targets may be able undo things like device I/O, and some may not.

The contract between GDB and the reverse executing target requires only that the target do something reasonable when GDB tells it to execute backwards, and then report the results back to GDB. Whatever the target reports back to GDB, GDB will report back to the user. GDB assumes that the memory and registers that the target reports are in a consistant state, but GDB accepts whatever it is given.


_Example_
```
### GDB Fails due to AVX instruction (at printf)
(gdb) start
Temporary breakpoint 1 at 0x642: file Xu.c, line 5.
Starting program: /home/ashwek/GitHub/a.out
Temporary breakpoint 1, main () at Xu.c:5
5		int i = 10;
(gdb) record
(gdb) n
7		printf("Hello \n");
(gdb)
Process record does not support instruction 0xc5 at address 0x7ffff7b72595.
Process record: failed to record execution log.

Program stopped.
__strlen_avx2 () at ../sysdeps/x86_64/multiarch/strlen-avx2.S:54
54	../sysdeps/x86_64/multiarch/strlen-avx2.S: No such file or directory.



### Without printf
(gdb) start
Temporary breakpoint 2 at 0x555555554642: file Xu.c, line 5.
Starting program: /home/ashwek/GitHub/a.out

Temporary breakpoint 2, main () at Xu.c:5
5		int i = 10;
(gdb) n
7		printf("Hello \n");
(gdb)
Hello
9		i = 45;
(gdb) record
(gdb) n
13		i = 90;
(gdb) info locals
i = 45
(gdb) n
15		return 0;
(gdb) info locals
i = 90
(gdb) reverse-next
13		i = 90;
(gdb) info locals
i = 45
(gdb) reverse-next

No more reverse-execution history.
main () at Xu.c:9
9		i = 45;
(gdb) info locals
i = 10
(gdb) next
13		i = 90;
(gdb) info locals
i = 45
```
