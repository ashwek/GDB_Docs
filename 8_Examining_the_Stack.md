# 8 Examining the Stack

----

When your program has stopped, the first thing you need to know is where it stopped and how it got there.

Each time your program performs a function call, information about the call is generated. That information includes the location of the call in your program, the arguments of the call, and the local variables of the function being called. The information is saved in a block of data called a _stack frame_. The stack frames are allocated in a region of memory called the call _stack_.

When your program stops, the GDB commands for examining the stack allow you to see all of this information.

One of the stack frames is selected by GDB and many GDB commands refer implicitly to the selected frame. In particular, whenever you ask GDB for the value of a variable in your program, the value is found in the selected frame. There are special GDB commands to select whichever frame you are interested in.

When your program stops, GDB automatically selects the currently executing frame and describes it briefly, similar to the ``frame`` command.

----

[Frames: Stack frames](./8_1_Stack_Frames.md)<br />
[Backtrace: Backtraces](./8_2_Backtrace.md)<br />
[Selection: Selecting a frame](./8_3_Selecting_a_Frame.md)<br />
[Frame Info: Information on a frame](./8_4_Information_About_a_Frame.md)<br />
