# 4.6 Your Program’s Input and Output

[Go Back](./4_Running_Programs_Under_GDB.md)

----

By default, the program you run under GDB does input and output to the same terminal that GDB uses. GDB switches the terminal to its own terminal modes to interact with you, but it records the terminal modes your program was using and switches back to them when you continue running your program.

```
info terminal
```
Displays information recorded by GDB about the terminal modes your program is using.

You can redirect your program’s input and/or output using _shell redirection_ with the ``run`` command. For example,
```
run > outfile
```
starts your program, diverting its output to the file _outfile_.

Another way to specify where your program should do input and output is with the ``tty`` command. This command accepts a file name as argument, and causes this file to be the default for future ``run`` commands. It also resets the controlling terminal for the child process, for future ``run`` commands. For example,
```
tty /dev/ttyb
```
directs that processes started with subsequent ``run`` commands default to do input and output on the terminal /dev/ttyb and have that as their controlling terminal.

An explicit redirection in ``run`` overrides the ``tty`` command’s effect on the input/output device, but not its effect on the controlling terminal.

When you use the ``tty`` command or redirect input in the ``run`` command, only the input for your program is affected. The input for GDB still comes from your terminal. ``tty`` is an alias for set ``inferior-tty``.

You can use the ``show inferior-tty`` command to tell GDB to display the name of the terminal that will be used for future runs of your program.

```
set inferior-tty [ tty ]
```
Set the ``tty`` for the program being debugged to tty. Omitting tty restores the default behavior, which is to use the same terminal as GDB.

```
show inferior-tty
```
Show the current tty for the program being debugged.
