# 9 Examining Source Files

GDB can print parts of your program’s source, since the debugging information recorded in the program tells GDB what source files were used to build it. When your program stops, GDB spontaneously prints the line where it stopped. Likewise, when you select a stack frame, GDB prints the line where execution in that frame has stopped. You can print other portions of source files by explicit command.

----

[List: Printing source lines](./9_1_Printing_Source_Lines.md)<br />
[Specify Location: How to specify code locations](./9_2_Specifying_a_Location.md)<br />
