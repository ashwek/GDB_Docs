# 5.1 Breakpoints, Watchpoints, and Catchpoints

----

A **breakpoint** makes your program stop whenever a certain point in the program is reached. For each breakpoint, you can add conditions to control in finer detail whether your program stops. You can set breakpoints with the ``break`` command and its variants, to specify the place where your program should stop by line number, function name or exact address in the program.

On some systems, you can set breakpoints in shared libraries before the executable is run.

A **watchpoint** is a special breakpoint that stops your program when the value of an expression changes. The expression may be a value of a variable, or it could involve values of one or more variables combined by operators, such as ‘a + b’. This is sometimes called _**data breakpoints**_. You must use a different command to set watchpoints, but aside from that, you can manage a watchpoint like any other breakpoint: you enable, disable, and delete both breakpoints and watchpoints using the same commands.

You can arrange to have values from your program displayed automatically whenever GDB stops at a breakpoint.

A **catchpoint** is another special breakpoint that stops your program when a certain kind of event occurs, such as the throwing of a C++ exception or the loading of a library. As with watchpoints, you use a different command to set a catchpoint, but aside from that, you can manage a catchpoint like any other breakpoint.

GDB assigns a number to each breakpoint, watchpoint, or catchpoint when you create it; these numbers are successive integers starting with one. In many of the commands for controlling various features of breakpoints you use the breakpoint number to say which breakpoint you want to change. Each breakpoint may be enabled or disabled; if disabled, it has no effect on your program until you enable it again.

Some GDB commands accept a space-separated list of breakpoints on which to operate. A list element can be either a single breakpoint number, like ‘5’, or a range of such numbers, like ‘5-7’. When a breakpoint list is given to a command, all breakpoints in that list are operated on.

----

[Set Breaks: Setting breakpoints](./5_1_1_Setting_Breakpoints.md)<br />
[Set Watchpoints: Setting watchpoints](./5_1_2_Setting_Watchpoints.md)<br />
