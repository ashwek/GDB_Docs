# 5.1.7 Breakpoint Command Lists

----

You can give any breakpoint (or watchpoint or catchpoint) a series of commands to execute when your program stops due to that breakpoint. For example, you might want to print the values of certain expressions, or enable other breakpoints.

```
commands [list…]
… command-list …
end
```
Specify a list of commands for the given breakpoints. The commands themselves appear on the following lines. Type a line containing just end to terminate the commands.

To remove all commands from a breakpoint, type commands and follow it immediately with end; that is, give no commands.

With no argument, ``commands`` refers to the last breakpoint, watchpoint, or catchpoint set. If the most recent breakpoints were set with a single command, then the commands will apply to all the breakpoints set by that command.

The commands ``echo``, ``output``, and ``printf`` allow you to print precisely controlled output, and are often useful in silent breakpoints.

For example, here is how you could use breakpoint commands to print the value of x at entry to foo whenever x is positive.

```
break foo if x>0
commands
silent
printf "x is %d\n",x
cont
end
```
