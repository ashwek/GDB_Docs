# 5.1.8 Dynamic Printf

----

The dynamic printf command ``dprintf`` combines a breakpoint with formatted printing of your program’s data to give you the effect of inserting ``printf`` calls into your program on-the-fly, without having to recompile it.

In its most basic form, the output goes to the GDB console. However, you can set the variable dprintf-style for alternate handling. For instance, you can ask to format the output by calling your program’s printf function. This has the advantage that the characters go to the program’s output device, so they can recorded in redirects to files and so forth.

```
dprintf location,template,expression[,expression…]
```
Whenever execution reaches _location_, print the values of one or more _expressions_ under the control of the string _template_. To print several values, separate them with commas.
