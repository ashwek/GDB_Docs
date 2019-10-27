# 5.1.4 Deleting Breakpoints

----

It is often necessary to eliminate a breakpoint, watchpoint, or catchpoint once it has done its job and you no longer want your program to stop there. This is called deleting the breakpoint. A breakpoint that has been deleted no longer exists; it is forgotten.

With the ``clear`` command you can delete breakpoints according to where they are in your program. With the ``delete`` command you can delete individual breakpoints, watchpoints, or catchpoints by specifying their breakpoint numbers.

It is not necessary to delete a breakpoint to proceed past it. GDB automatically ignores breakpoints on the first instruction to be executed when you continue execution without changing the execution address.

```
clear
```
Delete any breakpoints at the next instruction to be executed in the selected stack frame.

```
clear location
```
Delete any breakpoints set at the specified location.

```
clear function
clear filename:function
```
Delete any breakpoints set at entry to the named _function_.

```
clear linenum
clear filename:linenum
```
Delete any breakpoints set at or within the code of the specified _linenum_ of the specified _filename_.

```
delete [breakpoints] [list…]
```
Delete the breakpoints, watchpoints, or catchpoints of the breakpoint list specified as argument. If no argument is specified, delete all breakpoints.
