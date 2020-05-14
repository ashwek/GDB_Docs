# 16 Examining the Symbol Table

----

The commands described in this chapter allow you to inquire about the symbols _(names of variables, functions and types)_ defined in your program. This information is inherent in the text of your program and does not change as your program executes.

Occasionally, you may need to refer to symbols that contain unusual characters, which GDB ordinarily treats as word delimiters. The most frequent case is in referring to static variables in other source files. File names are recorded in object files as debugging symbols, but GDB would ordinarily parse a typical file name, like ``foo.c``, as the three words ``foo`` ``.`` ``c``. To allow GDB to recognize ``foo.c`` as a single symbol, enclose it in single quotes; for example,
```
p 'foo.c'::x
```
looks up the value of ``x`` in the scope of the file ``foo.c``.


```
set print type methods
set print type methods on
set print type methods off
```
Normally, when GDB prints a class, it displays any methods declared in that class. You can control this behavior either by passing the appropriate flag to ``ptype``, or using ``set print type methods``. Specifying ``on`` will cause GDB to display the methods; this is the default. Specifying ``off`` will cause GDB to omit the methods.

```
info address symbol
```
Describe where the data for ``symbol`` is stored.

```
info symbol addr
```
Print the name of a symbol which is stored at the address ``addr``. If no symbol is stored exactly at ``addr``, GDB prints the nearest symbol and an offset from it
```
(gdb) info symbol 0x54320
_initialize_vx + 396 in section .text
```

<br />

```
whatis[/flags] [arg]
```
Print the data type of ``arg``, which can be either an expression or a name of a data type. With no argument, print the data type of ``$``, the last value in the value history.

If ``arg`` is an expression, it is not actually evaluated, and any side-effecting operations inside it do not take place.

```
ptype[/flags] [arg]
```
``ptype`` accepts the same arguments as ``whatis``, but prints a detailed description of the type, instead of just the name of the type.

Contrary to ``whatis``, ``ptype`` always unrolls any typedefs in its argument declaration, whether the argument is a variable, expression, or a data type. This means that ptype of a variable or an expression will not print literally its type as present in the source code—use ``whatis`` for that.

```
info scope location
```
List all the variables local to a particular scope. This command accepts a location argument - a function name, a source line, or an address preceded by a ‘\*’, and prints all the variables local to the scope defined by that location.

```
info source

(gdb) info source
Current source file is Cpp_Prog.cpp
Compilation directory is /home/user/Directory
Located in /home/user/Directory/Cpp_Prog.cpp
Contains 52 lines.
Source language is c++.
Producer is GNU C++14 7.5.0 -mtune=generic -march=x86-64 -ggdb -fstack-protector-strong.
Compiled with DWARF 2 debugging format.
Does not include preprocessor macro info.
```
Show information about the current source file - that is, the source file for the function containing the current point of execution:
 - the name of the source file, and the directory containing it
 - the directory it was compiled in
 - its length, in lines
 - which programming language it is written in
 - if the debug information provides it, the program that compiled the file
 - whether the executable includes debugging information for that file, and if so, what format the information is in (e.g., STABS, Dwarf 2, etc.)
 - whether the debugging information includes information about preprocessor macros


```
maint info symtabs [ regexp ]
maint info psymtabs [ regexp ]
```
List the ``struct symtab`` or ``struct partial_symtab`` structures whose names match ``regexp``. If regexp is not given, list them all. The output includes expressions which you can copy into a GDB debugging this one to examine a particular structure in more detail.
