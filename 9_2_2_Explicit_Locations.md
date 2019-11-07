# 9.2.2 Explicit Locations

----

Explicit locations allow the user to directly specify the source location’s parameters using option-value pairs.

Explicit locations are useful when several functions, labels, or file names have the same name in the program’s sources. In these cases, explicit locations point to the source line you meant more accurately and unambiguously. Also, using explicit locations might be faster in large programs.

For example, the _linespec_ ‘foo:bar’ may refer to a function _bar_ defined in the file named _foo_ or the label _bar_ in a function named _foo_. GDB must search either the file system or the symbol table to know.

The list of valid explicit location options is summarized in the following table:

```
-source filename
```
The value specifies the source file name. To differentiate between files with the same base name, prepend as many directories as is necessary to uniquely identify the desired file, e.g., foo/bar/baz.c. Otherwise GDB will use the first file it finds with the given base name. This option requires the use of either -function or -line.

```
-function function
```
The value specifies the name of a function. Operations on function locations unmodified by other options (such as -label or -line) refer to the line that begins the body of the function. In C, for example, this is the line with the open brace.

```
-qualified
```
This flag makes GDB interpret a function name specified with ``-function`` as a complete fully-qualified name.

```
-label label
```
The value specifies the name of a label. When the function name is not specified, the label is searched in the function of the currently selected stack frame.

```
-line number
```
The value specifies a line offset for the location. The offset may either be absolute (-line 3) or relative (-line +3), depending on the command. When specified without any other options, the line offset is relative to the current line.
