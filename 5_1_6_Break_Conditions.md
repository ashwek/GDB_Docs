# 5.1.6 Break Conditions

----

The simplest sort of breakpoint breaks every time your program reaches a specified place. You can also specify a condition for a breakpoint. A condition is just a _Boolean expression_ in your programming language. A breakpoint with a condition evaluates the expression each time your program reaches it, and your program stops only if the condition is true.

Conditions are also accepted for watchpoints; you may not need them, since a watchpoint is inspecting the value of an expression anyhow—but it might be simpler, say, to just set a watchpoint on a variable name, and specify a condition that tests whether the new value is an interesting one.

Break conditions can have side effects, and may even call functions in your program. This can be useful, for example, to activate functions that log program progress, or to use your own print functions to format special data structures. The effects are completely predictable unless there is another enabled breakpoint at the same address. Note that breakpoint commands are usually more convenient and flexible than break conditions for the purpose of performing side effects when a breakpoint is reached.

Break conditions can be specified when a breakpoint is set, by using ``if`` in the arguments to the ``break`` command. They can also be changed at any time with the ``condition`` command.

You can also use the ``if`` keyword with the ``watch`` command. The ``catch`` command does not recognize the ``if`` keyword; condition is the only way to impose a further condition on a catchpoint.

```
condition bnum expression
```
Specify expression as the break condition for breakpoint, watchpoint, or catchpoint number _bnum_. After you set a condition, breakpoint _bnum_ stops your program only if the value of expression is true (nonzero, in C). When you use condition, GDB checks expression immediately for syntactic correctness, and to determine whether symbols in it have referents in the context of your breakpoint.

```
condition bnum
```
Remove the condition from breakpoint number _bnum_. It becomes an ordinary unconditional breakpoint.
