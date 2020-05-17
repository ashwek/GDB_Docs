# 18 GDB Files

----

# 18.1 Commands to Specify Files

You may want to specify executable and core dump file names. The usual way to do this is at start-up time, using the arguments to GDB’s start-up commands.

Occasionally it is necessary to change to a different file during a GDB session. Or you may run GDB and forget to specify a file you want to use.

```
file filename
```
Use _filename_ as the program to be debugged. It is read for its symbols and for the contents of pure memory. It is also the program executed when you use the ``run`` command.

You can load unlinked object _.o_ files into GDB using the ``file`` command. You will not be able to “run” an object file, but you can disassemble functions and inspect variables.

```
file
```
``file`` with no argument makes GDB discard any information it has on both executable file and the symbol table.

```
exec-file [ filename ]
```
Specify that the program to be run is found in _filename_.

```
core-file [filename]
core
```
Specify the whereabouts of a core dump file to be used as the “contents of memory”. Traditionally, core files contain only some parts of the address space of the process that generated them; GDB can access the executable file itself for other parts. core-file with no argument specifies that no core file is to be used.

```
info files
info target
```
``info files`` and ``info target`` are synonymous; both print the current target, including the names of the executable and core dump files currently in use by GDB, and the files from which symbols were loaded. The command help target lists all possible targets rather than current ones.

----

# 18.3 Debugging Information in Separate Files

GDB allows you to put a program’s debugging information in a file separate from the executable itself, in a way that allows GDB to find and load the debugging information automatically.

GDB supports two ways of specifying the separate debug info file:
 - The executable contains a debug link that specifies the name of the separate debug info file. The separate debug file’s name is usually _executable.debug_, where executable is the name of the corresponding executable file without leading directories.
 - The executable contains a build ID, a unique bit string that is also present in the corresponding debug info file.
