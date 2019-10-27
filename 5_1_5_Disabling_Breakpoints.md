# 5.1.5 Disabling Breakpoints

----

Rather than deleting a breakpoint, watchpoint, or catchpoint, you might prefer to disable it. This makes the breakpoint inoperative as if it had been deleted, but remembers the information on the breakpoint so that you can enable it again later.

You disable and enable breakpoints, watchpoints, and catchpoints with the ``enable`` and ``disable`` commands, optionally specifying one or more breakpoint numbers as arguments. Use ``info break`` to print a list of all breakpoints, watchpoints, and catchpoints if you do not know which numbers to use.

Disabling and enabling a breakpoint that has multiple locations affects all of its locations.

A breakpoint, watchpoint, or catchpoint can have any of several different states of enablement:
 - _Enabled_ : The breakpoint stops your program. A breakpoint set with the break command starts out in this state.
 - _Disabled_ : The breakpoint has no effect on your program.
 - _Enabled once_ : The breakpoint stops your program, but then becomes disabled.
 - _Enabled for a count_ : The breakpoint stops your program for the next _N_ times, then becomes disabled.
 - _Enabled for deletion_ : The breakpoint stops your program, but immediately after it does so it is deleted permanently. A breakpoint set with the ``tbreak`` command starts out in this state.

You can use the following commands to enable or disable breakpoints, watchpoints, and catchpoints:

```
disable [breakpoints] [list…]
```
Disable the specified breakpoints - or all breakpoints, if none are listed.

```
enable [breakpoints] [list…]
```
Enable the specified breakpoints (or all defined breakpoints).

```
enable [breakpoints] once list…
```
Enable the specified breakpoints temporarily. GDB disables any of these breakpoints immediately after stopping your program.

```
enable [breakpoints] count count list…
```
Enable the specified breakpoints temporarily. GDB records count with each of the specified breakpoints, and decrements a breakpoint’s count when it is hit. When any count reaches 0, GDB disables that breakpoint.

```
enable [breakpoints] delete list…
```
Enable the specified breakpoints to work once, then die. GDB deletes any of these breakpoints as soon as your program stops there. Breakpoints set by the ``tbreak`` command start out in this state.
