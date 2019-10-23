# 4.8 Killing the Child Process

[Go Back](./4_Running_Programs_Under_GDB.md)

----

```
kill
```
Kill the child process in which your program is running under GDB.

This command is useful if you wish to debug a core dump instead of a running process. GDB ignores any core dump file while your program is running.

On some operating systems, a program cannot be executed outside GDB while you have breakpoints set on it inside GDB. You can use the ``kill`` command in this situation to permit running your program outside the debugger.

The ``kill`` command is also useful if you wish to recompile and relink your program, since on many systems it is impossible to modify an executable file while it is running in a process. In this case, when you next type ``run``, GDB notices that the file has changed, and reads the symbol table again.
