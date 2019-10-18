# 2.1 Invoking GDB

[Go Back](./README.md)

<a href="#2_1_1">2.1.1 Choosing Files</a><br />
<a href="#2_1_2">2.1.2 Choosing Modes</a><br />
<a href="#2_1_3">2.1.3 What GDB Does During Startup</a>

----

Invoke GDB by running the program **gdb**. Once started, GDB reads commands from the terminal until you tell it to exit.

You can also run gdb with a variety of arguments and options, to specify more of your debugging environment at the outset. The command-line options described here are designed to cover a variety of situations; in some environments, some of these options may effectively be unavailable.

The most usual way to start GDB is with one argument, _specifying an executable program_:
```
gdb program
```

You can also start with both an _executable program and a core file_ specified:
```
gdb program core
```

You can, instead, specify a _process ID_ as a second argument or use option _-p_, if you want to debug a running process:
```
gdb program 1234
gdb -p 1234
```
would attach GDB to process 1234. With option _-p_ you can omit the program filename.

You can run gdb without printing the front material, which describes GDB’s non-warranty, by specifying ``--silent`` (or ``-q/--quiet``):
```
gdb --silent
```

You can further control how GDB starts up by using command-line options. GDB itself can remind you of the options available.
```
gdb -help
```
to display all available options and briefly describe their use.

All options and command line arguments you give are processed in sequential order.

## 2.1.1 Choosing Files <a name="2_1_1"></a>

Many options have both long and short forms; both are shown in the following list. GDB also recognizes the long forms if you truncate them, so long as enough of the option is present to be unambiguous.
```
-symbols file
-s file

```
Read symbol table from ``file`` file.

```
-exec file
-e file
```
Use ``file`` file as the executable file to execute when appropriate, and for examining pure data in conjunction with a core dump.

```
-se file
```
Read symbol table from ``file`` file and use it as the executable file.

```
-core file
-c file
```
Use ``file`` file as a core dump to examine.

```
-pid number
-p number
```
Connect to process ID number, as with the attach command.

```
-command file
-x file
```
Execute commands from ``file`` file. The contents of this file is evaluated exactly as the source command would. See Command files.

```
-eval-command command
-ex command
```
Execute a single GDB command.

This option may be used multiple times to call multiple commands. It may also be interleaved with ‘-command’ as required.
```
    gdb -ex 'target sim' -ex 'load' \
       -x setbreakpoints -ex 'run' a.out
```

```
-init-command file
-ix file
```
Execute commands from file file before loading the inferior (but after loading gdbinit files). See Startup.

```
-init-eval-command command
-iex command
```
Execute a single GDB command before loading the inferior (but after loading gdbinit files). See Startup.

```
-directory directory
-d directory
```
Add directory to the path to search for source and script files.

```
-r
-readnow
```
Read each symbol file’s entire symbol table immediately, rather than the default, which is to read it incrementally as it is needed. This makes startup slower, but makes future operations faster.

```
--readnever
```
Do not read each symbol file’s symbolic debug information. This makes startup faster but at the expense of not being able to perform symbolic debugging. DWARF unwind information is also not read, meaning backtraces may become incomplete or inaccurate. One use of this is when a user simply wants to do the following sequence: attach, dump core, detach. Loading the debugging information in this case is an unnecessary cause of delay.

## 2.1.2 Choosing Modes <a name="2_1_2"></a>

You can run GDB in various alternative modes—for example, in batch mode or quiet mode.

```
-nx
-n
```
Do not execute commands found in any **initialization file**. There are three init files, loaded in the following order:

 - **system.gdbinit** This is the system-wide init file. Its location is specified with the _--with-system-gdbinit_ configure option. It is loaded first when GDB starts, before command line options have been processed.

 - **~/.gdbinit** This is the init file in your home directory. It is loaded next, after _system.gdbinit_, and before command options have been processed.

 - **./.gdbinit** This is the init file in the current directory. It is loaded last, after command line options other than -x and -ex have been processed. Command line options -x and -ex are processed last, after ./.gdbinit has been loaded.

``
-nh
``
Do not execute commands found in _~/.gdbinit_, the init file in your home directory.

```
-quiet
-silent
-q
```
“Quiet”. Do not print the introductory and copyright messages. These messages are also suppressed in batch mode.

```
-batch
```
Run in batch mode. Exit with status 0 after processing all the command files specified with ‘-x’. Exit with nonzero status if an error occurs in executing the GDB commands in the command files. Batch mode also disables pagination, sets unlimited terminal width and height see Screen Size, and acts as if set confirm off were in effect (see Messages/Warnings).

```
-batch-silent
```
Run in batch mode exactly like ‘-batch’, but totally silently. All GDB output to stdout is prevented. This is much quieter than ‘-silent’ and would be useless for an interactive session. This is particularly useful when using targets that give ‘Loading section’ messages, for example. Note that targets that give their output via GDB, as opposed to writing directly to stdout, will also be made silent.

```
-return-child-result
```
The return code from GDB will be the return code from the child process.

```
-nowindows
-nw
```
“No windows”. If GDB comes with a graphical user interface (GUI) built in, then this option tells GDB to only use the command-line interface. If no GUI is available, this option has no effect.

```
-windows
-w
```
If GDB includes a GUI, then this option requires it to be used if possible.

```
-cd directory
```
Run GDB using directory as its working directory, instead of the current directory.

```
-data-directory directory
-D directory
```
Run GDB using directory as its data directory. The data directory is where GDB searches for its auxiliary files. See Data Files.

```
-fullname
-f
```
GNU Emacs sets this option when it runs GDB as a subprocess. It tells GDB to output the full file name and line number in a standard, recognizable fashion each time a stack frame is displayed (which includes each time your program stops). This recognizable format looks like two ‘\032’ characters, followed by the file name, line number and character position separated by colons, and a newline. The Emacs-to-GDB interface program uses the two ‘\032’ characters as a signal to display the source code for the frame.

```
-annotate level
```
This option sets the annotation level inside GDB. Its effect is identical to using ‘set annotate level’. The annotation level controls how much information GDB prints together with its prompt, values of expressions, source lines, and other types of output. Level 0 is the normal, level 1 is for use when GDB is run as a subprocess of GNU Emacs, level 3 is the maximum annotation suitable for programs that control GDB, and level 2 has been deprecated. The annotation mechanism has largely been superseded by GDB/MI (see GDB/MI).

```
--args
```
Change interpretation of command line so that arguments following the executable file are passed as command line arguments to the inferior. This option stops option processing.

```
-baud bps
-b bps
```
Set the line speed (baud rate or bits per second) of any serial interface used by GDB for remote debugging.

```
-l timeout
```
Set the timeout (in seconds) of any communication used by GDB for remote debugging.

```
-tty device
-t device
```
Run using device for your program’s standard input and output.

```
-tui
```
Activate the Text User Interface when starting. The Text User Interface manages several text windows on the terminal, showing source, assembly, registers and GDB command outputs (see GDB Text User Interface). Do not use this option if you run GDB from Emacs (see Using GDB under GNU Emacs).

```
-interpreter interp
```
Use the interpreter interp for interface with the controlling program or device. This option is meant to be set by programs which communicate with GDB using it as a back end. See Command Interpreters.

```
-write
```
Open the executable and core files for both reading and writing. This is equivalent to the ‘set write on’ command inside GDB (see Patching).

```
-statistics
```
This option causes GDB to print statistics about time and memory usage after it completes each command and returns to the prompt.

```
-version
```
This option causes GDB to print its version number and no-warranty blurb, and exit.

```
-configuration
```
This option causes GDB to print details about its build-time configuration parameters, and then exit. These details can be important when reporting GDB bugs (see GDB Bugs).


## 2.1.3 What GDB Does During Startup <a name="2_1_3"></a>

Here’s the description of what GDB does during session startup:

1. Sets up the command interpreter as specified by the command line.
2. Reads the system-wide init file (if --with-system-gdbinit was used when building GDB) and executes all the commands in that file.
3. Reads the init file (if any) in your home directory and executes all the commands in that file.
4. Executes commands and command files specified by the ‘-iex’ and ‘-ix’ options in their specified order. Usually you should use the ‘-ex’ and ‘-x’ options instead, but this way you can apply settings before GDB init files get executed and before inferior gets loaded.
5. Processes command line options and operands.
6. Reads and executes the commands from init file (if any) in the current working directory as long as ‘set auto-load local-gdbinit’ is set to ‘on’. This is only done if the current directory is different from your home directory. Thus, you can have more than one init file, one generic in your home directory, and another, specific to the program you are debugging, in the directory where you invoke GDB.
7. If the command line specified a program to debug, or a process to attach to, or a core file, GDB loads any auto-loaded scripts provided for the program or for its loaded shared libraries.
8. Executes commands and command files specified by the ‘-ex’ and ‘-x’ options in their specified order. See Command Files, for more details about GDB command files.
9. Reads the command history recorded in the history file. See Command History, for more details about the command history and the files where GDB records it.

Init files use the same syntax as command files and are processed by GDB in the same way. The init file in your home directory can set options that affect subsequent processing of command line options and operands. Init files are not executed if you use the ‘-nx’ option.

The GDB init files are normally called .gdbinit. The DJGPP port of GDB uses the name gdb.ini, due to the limitations of file names imposed by DOS filesystems. The Windows port of GDB uses the standard name, but if it finds a gdb.ini file in your home directory, it warns you about that and suggests to rename the file to the standard name.
