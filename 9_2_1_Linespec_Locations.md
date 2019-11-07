# 9.2.1 Linespec Locations

----

A linespec is a colon-separated list of source location parameters such as file name, function name, etc. Here are all the different ways of specifying a linespec:

```
linenum
```
Specifies the line number linenum of the current source file.

```
-offset
+offset
```
Specifies the _line offset_ lines before or after the current line. For the ``list`` command, the current line is the last one printed; for the ``breakpoint`` commands, this is the line at which execution stopped in the currently selected stack frame. When used as the second of the two linespecs in a ``list`` command, this specifies the line offset lines up or down from the first linespec.

```
filename:linenum
```
Specifies the line _linenum_ in the source file _filename_. If _filename_ is a relative file name, then it will match any source file name with the same trailing components. For example, if filename is ‘gcc/expr.c’, then it will match source file name of /build/trunk/gcc/expr.c, but not /build/trunk/libcpp/expr.c or /build/trunk/gcc/x-expr.c.

```
function
```
Specifies the line that begins the body of the function _function_. For example, in C, this is the line with the open brace.

See Explicit Locations.

```
function:label
```
Specifies the line where label appears in function.

```
filename:function
```
Specifies the line that begins the body of the function function in the file filename. You only need the file name with a function name to avoid ambiguity when there are identically named functions in different source files.

```
label
```
Specifies the line at which the label named label appears in the function corresponding to the currently selected stack frame. If there is no current selected stack frame, then GDB will not search for a label.
