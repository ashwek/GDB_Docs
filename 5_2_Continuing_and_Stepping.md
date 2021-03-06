# 5.2 Continuing and Stepping

----

**Continuing** means resuming program execution until your program completes normally. In contrast, **stepping** means executing just one more “step” of your program, where “step” may mean either one line of source code, or one machine instruction. Either when continuing or when stepping, your program may stop even sooner, due to a breakpoint or a signal.

```
continue [ignore-count]
c [ignore-count]
fg [ignore-count]
```
Resume program execution, at the address where your program last stopped; any breakpoints set at that address are bypassed. The optional argument ignore-count allows you to specify a further number of times to ignore a breakpoint at this location; its effect is like that of ignore.

The argument ignore-count is meaningful only when your program stopped due to a breakpoint. At other times, the argument to continue is ignored.

The synonyms ``c`` and ``fg`` (for foreground, as the debugged program is deemed to be the foreground program) are provided purely for convenience, and have exactly the same behavior as ``continue``.

To resume execution at a different place, you can use ``return`` to go back to the calling function; or ``jump`` to go to an arbitrary location in your program.

A typical technique for using stepping is to set a breakpoint at the beginning of the function or the section of your program where a problem is believed to lie, run your program until it stops at that breakpoint, and then step through the suspect area, examining the variables that are interesting, until you see the problem happen.

```
step
```
**Continue running your program until control reaches a different source line**, then stop it and return control to GDB. This command is abbreviated ``s``.

The ``step`` command only stops at the first instruction of a source line. This prevents the multiple stops that could otherwise occur in switch statements, for loops, etc. ``step`` continues to stop if a function that has debugging information is called within the line. In other words, step steps inside any functions called within the line.

```
step count
```
Continue running as in step, but do so count times. If a breakpoint is reached, or a signal not related to stepping occurs before count steps, stepping stops right away.

```
next [count]
```
Continue to the next source line **in the current stack frame**. This is similar to ``step``, but function calls that appear within the line of code are executed without stopping. Execution stops when control reaches a different line of code at the original stack level that was executing when you gave the next command. This command is abbreviated _n_.

The ``next`` command only stops at the first instruction of a source line. This prevents multiple stops that could otherwise occur in switch statements, for loops, etc.

```
finish
```
Continue running until just after function in the selected stack frame returns. Print the returned value (if any). This command can be abbreviated as ``fin``.

```
until
u
```
Continue running until a source line past the current line, in the current stack frame, is reached. _This command is used to avoid single stepping through a loop more than once._ It is like the ``next`` command, except that when ``until`` encounters a jump, it automatically continues execution until the program counter is greater than the address of the jump.

This means that when you reach the end of a loop after single stepping though it, ``until`` makes your program continue execution until it exits the loop. In contrast, a ``next`` command at the end of a loop simply steps back to the beginning of the loop, which forces you to step through the next iteration. ``until`` always stops your program if it attempts to exit the current stack frame.

```
stepi
stepi arg
si
```
Execute one machine instruction, then stop and return to the debugger.

```
nexti
nexti arg
ni
```
Execute one machine instruction, but if it is a function call, proceed until the function returns. 
