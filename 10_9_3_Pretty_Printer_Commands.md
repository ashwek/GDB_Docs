# 10.9.3 Pretty-Printer Commands

----

```
info pretty-printer [object-regexp [name-regexp]]
```
Print the list of installed pretty-printers. This includes disabled pretty-printers, which are marked as such.

_object-regexp_ is a regular expression matching the objects whose pretty-printers to list. Objects can be global, the program space’s file, and the object files within that program space.

_name-regexp_ is a regular expression matching the name of the printers to list.

```
disable pretty-printer [object-regexp [name-regexp]]
```
Disable pretty-printers matching _object-regexp_ and _name-regexp_. A disabled pretty-printer is not forgotten, it may be enabled again later.

```
enable pretty-printer [object-regexp [name-regexp]]
```
Enable pretty-printers matching object-regexp and name-regexp.

Example:

Suppose we have three pretty-printers installed: one from library1.so named foo that prints objects of type foo, and another from library2.so named bar that prints two types of objects, bar1 and bar2.

```
(gdb) info pretty-printer
library1.so:
  foo
library2.so:
  bar
    bar1
    bar2

(gdb) info pretty-printer library2
library2.so:
  bar
    bar1
    bar2

(gdb) disable pretty-printer library1
1 printer disabled
2 of 3 printers enabled

(gdb) info pretty-printer
library1.so:
  foo [disabled]
library2.so:
  bar
    bar1
    bar2

(gdb) disable pretty-printer library2 bar;bar1
1 printer disabled
1 of 3 printers enabled

(gdb) info pretty-printer library2
library1.so:
  foo [disabled]
library2.so:
  bar
    bar1 [disabled]
    bar2

(gdb) disable pretty-printer library2 bar
1 printer disabled
0 of 3 printers enabled
(gdb) info pretty-printer library2
library1.so:
  foo [disabled]
library2.so:
  bar [disabled]
    bar1 [disabled]
    bar2
```
