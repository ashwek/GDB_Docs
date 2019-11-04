# 8.1 Stack Frames

----

The call stack is divided up into contiguous pieces called _stack frames_, or frames for short; each _frame_ is the data associated with one call to one function. The frame contains the arguments given to the function, the function’s local variables, and the address at which the function is executing.

When your program is started, the stack has only one frame, that of the function main. This is called the _initial frame_ or the _outermost frame_. Each time a function is called, a new frame is made. Each time a function returns, the frame for that function invocation is eliminated. If a function is recursive, there can be many frames for the same function. The frame for the function in which execution is actually occurring is called the _innermost frame_. This is the most recently created of all the stack frames that still exist.

Inside your program, stack frames are identified by their addresses. A stack frame consists of many bytes, each of which has its own address; each kind of computer has a convention for choosing one byte whose address serves as the address of the frame. Usually this address is kept in a register called the _frame pointer register_ (see ``print $fp``) while execution is going on in that frame.

GDB labels each existing stack frame with a level, a number that is zero for the innermost frame, one for the frame that called it, and so on upward. These level numbers give you a way of designating stack frames in GDB commands. The terms _frame number_ and _frame level_ can be used interchangeably to describe this number.
