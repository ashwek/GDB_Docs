# 3.5 Getting Help

[Go Back](./README.md)

----

You can always ask GDB itself for information on its commands, using the command ``help``.

```
help
h
```
You can use ``help`` with no arguments to display a short list of named classes of commands:
```
(gdb) help
List of classes of commands:

aliases -- Aliases of other commands
breakpoints -- Making program stop at certain points
data -- Examining data
files -- Specifying and examining files
internals -- Maintenance commands
obscure -- Obscure features
running -- Running the program
stack -- Examining the stack
status -- Status inquiries
support -- Support facilities
tracepoints -- Tracing of program execution without
               stopping the program
user-defined -- User-defined commands

Type "help" followed by a class name for a list of
commands in that class.
Type "help" followed by command name for full
documentation.
Command name abbreviations are allowed if unambiguous.
(gdb)
```

In addition to ``help``, you can use the GDB commands ``info`` and ``show`` to **_inquire about the state of your program, or the state of GDB itself_**.

```
info
```
This command (abbreviated _i_) is for describing the _state of your program_. For example, you can show the arguments passed to a function with ``info args``, list the registers currently in use with ``info registers``, or list the breakpoints you have set with ``info breakpoints``. You can get a complete list of the info sub-commands with ``help info``.

``
set
``
You can assign the result of an expression to an environment variable with ``set``. For example, you can set the GDB prompt to a $-sign with set prompt $.

```
show
```
In contrast to ``info``, ``show`` is for describing the _**state of GDB itself**_. You can change most of the things you can ``show``, by using the related command ``set``; for example, you can control what number system is used for displays with ``set radix``, or simply inquire which is currently in use with ``show radix``.

To display all the settable parameters and their current values, you can use ``show`` with no arguments; you may also use ``info set``. Both commands produce the same display.

Here are several miscellaneous ``show`` subcommands, all of which are exceptional in lacking corresponding ``set`` commands:

```
show version
```
Show what version of GDB is running.

```
show copying
info copying
```
Display information about permission for copying GDB.

```
show warranty
info warranty
```
Display the GNU “NO WARRANTY” statement, or a warranty, if your version of GDB comes with one.

```
show configuration
```
Display detailed information about the way GDB was configured when it was built.
