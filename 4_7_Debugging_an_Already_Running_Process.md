# 4.7 Debugging an Already-running Process

[Go Back](./4_Running_Programs_Under_GDB.md)

----

```
attach process-id
```
This command attaches to a running process - one that was started outside GDB. The command takes as argument a _process ID_.

``attach`` does not repeat if you press ``RET`` a second time after executing the command.

To use ``attach``, your program must be running in an environment which supports processes; for example, attach does not work for programs on bare-board targets that lack an operating system. You must also have permission to send the process a signal.

When you use ``attach``, the debugger finds the program running in the process first by looking in the current working directory, then (if the program is not found) by using the source file search path (see Specifying Source Directories). You can also use the file command to load the program.

The first thing GDB does after arranging to debug the specified process is to stop it. You can examine and modify an attached process with all the GDB commands that are ordinarily available when you start processes with ``run``. You can insert breakpoints; you can step and continue; you can modify storage. If you would rather the process continue running, you may use the ``continue`` command after attaching GDB to the process.

```
detach
```
When you have finished debugging the attached process, you can use the detach command to release it from GDB control. Detaching the process continues its execution. After the ``detach`` command, that process and GDB become completely independent once more, and you are ready to attach another process or start one with ``run``. ``detach`` does not repeat if you press RET again after executing the command.

If you exit GDB while you have an attached process, you detach that process. If you use the ``run`` command, you kill that process. By default, GDB asks for confirmation if you try to do either of these things; you can control whether or not you need to confirm by using the set confirm command.
