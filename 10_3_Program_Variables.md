# 10.3 Program Variables

----

The most common kind of expression to use is the name of a variable in your program.

Variables in expressions are understood in the selected stack frame; they must be either:
 - global (or file-static)
 - visible according to the scope rules of the programming language from the point of execution in that frame

You can refer to a variable or function whose scope is a single source file even if the current execution point is not in this file. But it is possible to have more than one such variable or function with the same name (in different source files). If that happens, referring to that name has unpredictable effects. If you wish, you can specify a static variable in a particular function or file by using the colon-colon (::) notation:

```
file::variable
function::variable
```
Here _file_ or _function_ is the name of the context for the static variable. In the case of file names, you can use quotes to make sure GDB parses the file name as a single word—for example, to print a global value of _x_ defined in _f2.c_:
```
(gdb) p 'f2.c'::x
```

The **::** notation is normally used for referring to static variables, since you typically disambiguate uses of local variables in functions by selecting the appropriate frame and using the simple name of the variable. However, you may also use this notation to refer to local variables in frames enclosing the selected frame:

```c
void foo (int a) {
  if (a < 10) bar (a);
  else process (a); /* stop here */
}

int bar (int a) {
  foo (a + 5);
}
```
For example, if there is a breakpoint at the commented line, here is what you might see when the program stops after executing the call ``bar(0)``:

```
(gdb) p a
$1 = 10
(gdb) p bar::a
$2 = 5
(gdb) up 2
#2  0x080483d0 in foo (a=5) at foobar.c:12
(gdb) p a
$3 = 5
(gdb) p bar::a
$4 = 0
```
These uses of **::** are very rarely in conflict with the very similar use of the same notation in C++. When they are in conflict, the C++ meaning takes precedence.

For example, suppose the program is stopped in a method of a class that has a field named includefile, and there is also an include file named includefile that defines a variable, some_global.

```
(gdb) p includefile
$1 = 23
(gdb) p includefile::some_global
A syntax error in expression, near `'.
(gdb) p 'includefile'::some_global
$2 = 27
```
