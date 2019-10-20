# 4.3 Your Program’s Arguments

[Go Back](./4_Running_Programs_Under_GDB.md)

----

The arguments to your program can be specified by the arguments of the ``run`` command. They are passed to a shell, which expands wildcard characters and performs redirection of I/O, and thence to your program. Your SHELL environment variable (if it exists) specifies what shell GDB uses. If you do not define SHELL, GDB uses the default shell (/bin/sh on Unix).

``run`` with no arguments **uses the same arguments used by the previous ``run``**, or those set by the ``set args`` command.

```
set args
```
Specify the arguments to be used the next time your program is run. If ``set args`` has no arguments, ``run`` executes your program with no arguments. Once you have run your program with arguments, using ``set args`` before the next run is the only way to run it again without arguments.

```
show args
```
Show the arguments to give your program when it is started.
