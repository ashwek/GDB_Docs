# 5.1.1 Setting Breakpoints

----

Breakpoints are set with the ``break`` command.

```
break location
```
Set a breakpoint at the given _location_, which can specify a function name, a line number, or an address of an instruction. The breakpoint will stop your program just before it executes any of the code in the specified location.

```
break
```
When called without any arguments, ``break`` sets a breakpoint at the next instruction to be executed in the selected stack frame.

```
break … if cond
```
Set a breakpoint with condition _cond_; evaluate the expression _cond_ each time the breakpoint is reached, and stop only if the value is nonzero—that is, if cond evaluates as true.

```
tbreak args
```
Set a breakpoint enabled only for one stop. The _args_ are the same as for the break command, and the breakpoint is set in the same way, but the breakpoint is automatically deleted after the first time your program stops there.

```
hbreak args
```
Set a hardware-assisted breakpoint. The args are the same as for the ``break`` command and the breakpoint is set in the same way, but the breakpoint requires hardware support and some target hardware may not have this support.

```
thbreak args
```
Set a hardware-assisted breakpoint enabled only for one stop.

```
rbreak regex
```
Set breakpoints on all functions matching the regular expression regex. This command sets an unconditional breakpoint on all matches, printing a list of all breakpoints it set. Once these breakpoints are set, they are treated just like the breakpoints set with the break command.

```
info breakpoints [list…]
info break [list…]
```
Print a table of all breakpoints, watchpoints, and catchpoints set and not deleted. Optional argument _n_ means print information only about the specified breakpoint(s) (or watchpoint(s) or catchpoint(s)).

For each breakpoint, following columns are printed:
 - Breakpoint Numbers
 - Type (Breakpoint, watchpoint, or catchpoint)
 - Disposition (Whether the breakpoint is marked to be disabled or deleted when hit)
 - Enabled or Disabled (Enabled breakpoints are marked with ‘y’. ‘n’ marks breakpoints that are not enabled)
 - Address (Where the breakpoint is in your program, as a memory address)
 - What (Where the breakpoint is in the source for your program, as a file and line number)

``info break`` displays a count of the number of times the breakpoint has been hit. This is especially useful in conjunction with the ``ignore`` command. You can ignore a large number of breakpoint hits, look at the breakpoint info to see how many times the breakpoint was hit, and then run again, ignoring one less than that number. This will get you quickly to the last hit of that breakpoint.

It is possible that a breakpoint corresponds to several locations in your program. Examples of this situation are:
 - Multiple functions in the program may have the same name.
 - For a C++ constructor, the GCC compiler generates several instances of the function body, used in different cases.
 - For a C++ template function, a given line in the function can correspond to any number of instantiations.
 - For an inlined function, a given source line can correspond to several places where that function is inlined.

In all those cases, GDB will insert a breakpoint at all the relevant locations.

A breakpoint with multiple locations is displayed in the breakpoint table using several rows—one header row, followed by one row for each breakpoint location. The header row has ‘<MULTIPLE>’ in the address column. The rows for individual locations contain the actual addresses for locations, and show the functions to which those locations belong.

For example:
```
Num     Type           Disp Enb  Address    What
1       breakpoint     keep y    <MULTIPLE>
        stop only if i==1
        breakpoint already hit 1 time
1.1                         y    0x080486a2 in void foo<int>() at t.cc:8
1.2                         y    0x080486ca in void foo<double>() at t.cc:8
```

GDB normally implements breakpoints by replacing the program code at the breakpoint address with a special instruction, which, when executed, given control to the debugger. By default, the program code is so modified only when the program is resumed. As soon as the program stops, GDB restores the original instructions. This behaviour guards against leaving breakpoints inserted in the target should gdb abrubptly disconnect. However, with slow remote targets, inserting and removing breakpoint can reduce the performance.

GDB handles conditional breakpoints by evaluating these conditions when a breakpoint breaks. If the condition is true, then the process being debugged stops, otherwise the process is resumed.

GDB itself sometimes sets breakpoints in your program for special purposes, such as proper handling of longjmp (in C programs). These internal breakpoints are assigned negative numbers, starting with -1; ‘info breakpoints’ does not display them. You can see these breakpoints with the GDB maintenance command ``maint info breakpoints``.
