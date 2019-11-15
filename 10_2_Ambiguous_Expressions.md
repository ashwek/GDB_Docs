# 10.2 Ambiguous Expressions

----

Expressions can sometimes contain some ambiguous elements. For instance, some programming languages permit a single function name to be defined several times, for application in different contexts. This is called _overloading_. A generic package is similar to C++ templates and is typically instantiated several times, resulting in the same function name being defined in different contexts.

In some cases and depending on the language, it is possible to adjust the expression to remove the ambiguity. For instance in C++, you can specify the signature of the function you want to break on, as in ``break function(types)``.

When an ambiguity that needs to be resolved is detected, the debugger has the capability to display a menu of numbered choices for each possibility, and then waits for the selection with the prompt ‘>’. The first option is always ‘[0] cancel’, and typing ``0 RET`` aborts the current command. If the command in which the expression was used allows more than one choice to be selected, the next option in the menu is ‘[1] all’, and typing ``1 RET`` selects all possible choices.

For example, the following session excerpt shows an attempt to set a breakpoint at the overloaded symbol ``String::after``. We choose three particular definitions of that function name:

```
(gdb) break String::after
[0] cancel
[1] all
[2] file:String.cc; line number:867
[3] file:String.cc; line number:860
[4] file:String.cc; line number:875
[5] file:String.cc; line number:853
[6] file:String.cc; line number:846
[7] file:String.cc; line number:735
> 2 4 6
Breakpoint 1 at 0xb26c: file String.cc, line 867.
Breakpoint 2 at 0xb344: file String.cc, line 875.
Breakpoint 3 at 0xafcc: file String.cc, line 846.
Multiple breakpoints were set.
Use the "delete" command to delete unwanted
 breakpoints.
(gdb)
```

```
set multiple-symbols mode
```
This option allows you to adjust the debugger behavior when an expression is ambiguous.

By default, mode is set to all. If the command with which the expression is used allows more than one choice, then GDB automatically selects all possible choices. For instance, inserting a breakpoint on a function using an ambiguous name results in a breakpoint inserted on each possible match. However, if a unique choice must be made, then GDB uses the menu to help you disambiguate the expression.

```
show multiple-symbols
```
Show the current value of the multiple-symbols setting.
