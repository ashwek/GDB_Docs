# 5.3 Skipping Over Functions and Files

----

The program you are debugging may contain some functions which are uninteresting to debug. The ``skip`` command lets you tell GDB to skip a function, all functions in a file or a particular function in a particular file when stepping.

For example, consider the following C function:

```c
101     int func()
102     {
103         foo(boring());
104         bar(boring());
105     }
```

Suppose you wish to step into the functions _foo_ and _bar_, but you are not interested in stepping through _boring_. If you run ``step`` at line 103, you’ll enter _boring()_, but if you run ``next``, you’ll step over both _foo_ and _boring_!

One solution is to step into _boring_ and use the ``finish`` command to immediately exit it. But this can become tedious if _boring_ is called from many places.

A more flexible solution is to execute ``skip`` boring. This instructs GDB never to step into _boring_. Now when you execute ``step`` at line 103, you’ll step over _boring_ and directly into _foo_.

Functions may be skipped by providing either a function name, linespec, regular expression that matches the function’s name, file name or a glob-style pattern that matches the file name.

```
skip [options]
```
The basic form of the ``skip`` command takes zero or more options that specify what to skip. The options _argument_ is any useful combination of the following:

```
skip -file file
skip -fi file
```
Functions in _file_ will be skipped over when stepping.

```
skip -gfile file-glob-pattern
skip -gfi file-glob-pattern
```
Functions in _files_ matching _file-glob-pattern_ will be skipped over when stepping.

```
skip -rfunction regexp
skip -rfu regexp
```
Functions whose name matches _regexp will_ be skipped over when stepping.
This form is useful for complex function names. For example, there is generally no need to step into C++ std::string constructors or destructors. Plus with C++ templates it can be hard to write out the full name of the function, and often it doesn’t matter what the template arguments are. Specifying the function to be skipped as a regular expression makes this easier.

```
(gdb) skip -rfu ^std::(allocator|basic_string)<.*>::~?\1 *\(
```

```
skip function [linespec]
```
After running this command, the function named by _linespec_ or the function containing the line named by _linespec_ will be skipped over when stepping.

```
skip file [filename]
```
After running this command, any function whose source lives in filename will be skipped over when stepping.

If you do not specify filename, functions whose source lives in the file you’re currently debugging will be skipped.

Skips can be listed, deleted, disabled, and enabled, much like breakpoints. These are the commands for managing your list of skips:

```
info skip [range]
```
Print details about the specified skip. If range is not specified, print a table with details about all functions and files marked for skipping. ``info skip`` prints the following information about each skip:

 - Identifier (A number identifying this skip)
 - Enabled or Disabled (Enabled skips are marked with ‘y’. Disabled skips are marked with ‘n’)
 - Glob (If the file name is a ‘glob’ pattern this is ‘y’. Otherwise it is ‘n’)
 - File (The name or ‘glob’ pattern of the file to be skipped. If no file is specified this is ‘<none>’)
 - RE (If the function name is a ‘regular expression’ this is ‘y’. Otherwise it is ‘n’)
 - Function (The name or regular expression of the function to skip. If no function is specified this is ‘<none>’)

```
skip delete [range]
```
Delete the specified skip(s). If range is not specified, delete all skips.

```
skip enable [range]
```
Enable the specified skip(s). If range is not specified, enable all skips.

```
skip disable [range]
```
Disable the specified skip(s). If range is not specified, disable all skips.

```
set debug skip [on|off]
```
Set whether to print the debug output about skipping files and functions.

```
show debug skip
```
Show whether the debug output about skipping files and functions is printed.


_Example_

```
(gdb) start
Temporary breakpoint 1 at 0x729: file Xu.c, line 3.
Starting program: /home/ashwek/GitHub/a.out
Temporary breakpoint 1, main (argc=1, argv=0x7fffffffde88) at Xu.c:3
3       int main(int argc, char *argv[]){

(gdb) step
6               printf("Enter a number : ");

(gdb) step
__printf (format=0x555555554804 "Enter a number : ") at printf.c:28
28      printf.c: No such file or directory.
(gdb) step
32      in printf.c
(gdb) step
33      in printf.c
(gdb) step
32      in printf.c
(gdb) continue
Continuing.
Enter a number : 5
[Inferior 1 (process 26295) exited normally]


(gdb) skip -rfu printf
Function(s) printf will be skipped when stepping.
(gdb) skip -rfu scanf
Function(s) scanf will be skipped when stepping.


(gdb) start
Temporary breakpoint 9 at 0x555555554729: file Xu.c, line 3.
Starting program: /home/ashwek/GitHub/a.out
Temporary breakpoint 9, main (argc=1, argv=0x7fffffffde88) at Xu.c:3
3       int main(int argc, char *argv[]){
(gdb) step
6               printf("Enter a number : ");
(gdb) step
7               scanf("%d", &i);
(gdb) step
Enter a number : 8
9               return 0;
(gdb) step
10 }
```
