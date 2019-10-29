# 5 Stopping and Continuing

[Go Back](./README.md)

----

The principal purposes of using a debugger are so that you can stop your program before it terminates; or so that, if your program runs into trouble, you can investigate and find out why.

Inside GDB, your program may stop for any of several reasons, such as a signal, a breakpoint, or reaching a new line after a GDB command such as step. You may then examine and change variables, set new breakpoints or remove old ones, and then continue execution. Usually, the messages shown by GDB provide ample explanation of the status of your program—but you can also explicitly request this information at any time.

```
info program
```
Display information about the status of your program: whether it is running or not, what process it is, and why it stopped.


-----


[Breakpoints: Breakpoints, watchpoints, and catchpoints ](./5_1_Breakpoints_Watchpoints_Catchpoints.md)<br />
[Continuing and Stepping: Resuming execution](./5_2_Continuing_and_Stepping.md)<br />
[Skipping Over Functions and Files: Skipping over functions and files](./5_3_Skipping_Over_Functions_and_Files.md)<br />
