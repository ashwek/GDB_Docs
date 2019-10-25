# 4.9 Debugging Multiple Inferiors and Programs

[Go Back](./4_Running_Programs_Under_GDB.md)

----

GDB lets you run and debug multiple programs in a single session. In addition, GDB on some systems may let you run several programs simultaneously. In the most general case, you can have multiple threads of execution in each of multiple processes, launched from multiple executables.

GDB represents the state of each program execution with an object called an **inferior**. An inferior typically corresponds to a process, but is more general and applies also to targets that do not have processes. Inferiors may be created before a process runs, and may be retained after a process exits. Inferiors have unique identifiers that are different from process ids. Usually each inferior will also have its own distinct address space, although some embedded targets may have several inferiors running in different parts of a single address space. Each inferior may in turn have multiple threads running in it.

To find out what inferiors exist at any moment, use ``info inferiors``:

```
info inferiors
```
Print a list of all inferiors currently being managed by GDB. By default all inferiors are printed, but the argument id… – a space separated list of inferior numbers – can be used to limit the display to just the requested inferiors.

GDB displays for each inferior (in this order):
 1. the inferior number assigned by GDB
 2. the target system’s inferior identifier
 3. the name of the executable the inferior is running.

An asterisk ‘\*’ preceding the GDB inferior number indicates the current inferior.

For example,
```
(gdb) info inferiors
      Num  Description       Executable
      2    process 2307      hello
    * 1    process 3401      goodbye
```
To switch focus between inferiors, use the ``inferior`` command:

```
inferior infno
```
Make inferior number _infno_ the current inferior. The argument _infno_ is the inferior number assigned by GDB, as shown in the first field of the ``info inferiors`` display.

You can get multiple executables into a debugging session via the ``add-inferior`` and ``clone-inferior`` commands. On some systems GDB can add inferiors to the debug session automatically by following calls to fork and exec. To remove inferiors from the debugging session use the ``remove-inferiors`` command.

```
add-inferior [ -copies n ] [ -exec executable ]
```
Adds _n_ inferiors to be run using _executable_ as the executable; _n_ defaults to 1. If no executable is specified, the inferiors begins empty, with no program. You can still assign or change the program assigned to the inferior at any time by using the ``file`` command with the executable name as its argument.

```
clone-inferior [ -copies n ] [ infno ]
```
Adds _n_ inferiors ready to execute the same program as inferior _infno_; _n_ defaults to 1, and _infno_ defaults to the number of the current inferior. This is a convenient command when you want to run another instance of the inferior you are debugging.

```
remove-inferiors infno…
```
Removes the _infno_ inferior. It is not possible to remove an inferior that is running with this command. For those, use the ``kill`` or ``detach`` command first.

To quit debugging one of the running inferiors that is not the current inferior, you can either detach from it by using the ``detach inferior`` command, or kill it using the ``kill inferiors`` command:

```
detach inferior infno…
```
Detach from the _infno_ inferior. Note that the inferior’s entry still stays on the list of inferiors shown by info inferiors, but its Description will show ‘<null>’.

```
kill inferiors infno…
```
Kill the _infno_ inferior. Note that the inferior’s entry still stays on the list of inferiors shown by info inferiors, but its Description will show ‘<null>’.

After the successful completion of a command such as ``detach``, ``detach inferiors``, ``kill`` or ``kill inferiors``, or after a normal process exit, the inferior is still valid and listed with ``info inferiors``, ready to be restarted.

To be notified when inferiors are started or exit under GDB’s control use ``set print inferior-events``:

```
set print inferior-events
set print inferior-events on
set print inferior-events off
```
The ``set print inferior-events`` command allows you to enable or disable printing of messages when GDB notices that new inferiors have started or that inferiors have exited or have been detached. By default, these messages will not be printed.

```
show print inferior-events
```
Show whether messages will be printed when GDB detects that inferiors have started, exited or have been detached.

```
maint info program-spaces
```
Print a list of all program spaces currently being managed by GDB.

GDB displays for each program space (in this order):
 1. the program space number assigned by GDB
 2. the name of the executable loaded into the program space, with e.g., the ``file command``.

An asterisk ‘*’ preceding the GDB program space number indicates the current program space.
