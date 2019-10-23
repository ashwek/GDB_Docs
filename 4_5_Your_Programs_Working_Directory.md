# 4.5 Your Program’s Working Directory

[Go Back](./4_Running_Programs_Under_GDB.md)

----

Each time you start your program with ``run``, the inferior will be initialized with the current working directory specified by the ``set cwd`` command. If no directory has been specified by this command, then the inferior will inherit GDB’s current working directory as its working directory if native debugging, or it will inherit the remote server’s current working directory if remote debugging.

```
set cwd [directory]
```
Set the inferior’s working directory to _directory_, which will be glob-expanded in order to resolve tildes (~). If no argument has been specified, the command clears the setting and resets it to an empty state. This setting has no effect on GDB’s working directory, and it only takes effect the next time you start the inferior.

```
show cwd
```
Show the inferior’s working directory.

```
cd [directory]
```
Set the GDB working directory to _directory_. If not given, directory uses '~'.

```
pwd
```
Print the GDB working directory.

It is generally impossible to find the current working directory of the process being debugged (since a program can change its directory during its run). If you work on a system where GDB supports the ``info proc`` command, you can use the ``info proc`` command to find out the current working directory of the debuggee.
