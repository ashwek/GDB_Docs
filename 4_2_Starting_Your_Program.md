# 4.2 Starting your Program

[Go Back](./4_Running_Programs_Under_GDB.md)

----

```
run
r
```
Use the ``run`` command to start your program under GDB. You must first specify the program name with an argument to GDB, or by using the ``file`` or ``exec-file`` command.

If you are running your program in an execution environment that supports processes, ``run`` creates an inferior process and makes that process run your program. In some environments without processes, ``run`` jumps to the start of your program.

The execution of a program is affected by certain information it receives from its superior. GDB provides ways to specify this information, which you must do before starting your program. (You can change it after starting your program, but such changes only affect your program the next time you start it.) This information may be divided into four categories:

 - _The arguments_

 Specify the arguments to give your program as the arguments of the ``run`` command.

 - _The environment_

 Your program normally inherits its environment from GDB, but you can use the GDB commands ``set environment`` and ``unset environment`` to change parts of the environment that affect your program.

 - _The working directory_

 You can set your program’s working directory with the command ``set cwd``. If you do not set any working directory, your program will inherit GDB’s working directory if native debugging, or the remote server’s working directory if remote debugging.

 - _The standard input and output_

 Your program normally uses the same device for standard input and standard output as GDB is using. You can redirect input and output in the run command line, or you can use the tty command to set a different device for your program. See Your Program’s Input and Output.


When you issue the ``run`` command, your program begins to execute immediately. If the modification time of your symbol file has changed since the last time GDB read its symbols, GDB discards its symbol table, and reads it again. When it does this, GDB tries to retain your current breakpoints.

```
start
```
The name of the main procedure can vary from language to language. With C or C++, the main procedure name is always main, but other languages such as Ada do not require a specific name for their main procedure. The debugger provides a convenient way to start the execution of the program and to stop at the beginning of the main procedure, depending on the language used.

The ``start`` command does the equivalent of setting a temporary breakpoint at the beginning of the main procedure and then invoking the ``run`` command.
