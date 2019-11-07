# 9.1 Printing Source Lines

----

To print lines from a source file, use the ``list`` command. By default, 10 lines are printed. There are several ways to specify what part of the file you want to print.

Here are the forms of the list command most commonly used:

```
list linenum
```
Print lines centered around line number _linenum_ in the current source file.

```
list function
```
Print lines centered around the beginning of function _function_.

```
list
```
Print more lines. If the last lines printed were printed with a ``list`` command, this prints lines following the last lines printed; however, if the last line printed was a solitary line printed as part of displaying a stack frame, this prints lines centered around that line.

```
list -
```
Print lines just before the lines last printed.

By default, GDB prints ten source lines with any of these forms of the list command. You can change this using ``set listsize``:

```
set listsize count
set listsize unlimited
```
Make the ``list`` command display _count_ source lines. Setting _count_ to unlimited or 0 means there’s no limit.

```
show listsize
```
Display the number of lines that list prints.

Repeating a ``list`` command with ``RET`` discards the argument, so it is equivalent to typing just ``list``.

In general, the ``list`` command expects you to supply zero, one or two locations. Locations specify source lines; there are several ways of writing them, but the effect is always to specify some source line.

Here is a complete description of the possible arguments for list:

```
list location
```
Print lines centered around the line specified by _location_.

```
list first,last
```
Print lines from _first_ to _last_. Both arguments are locations. When a ``list`` command has two locations, and the source file of the second location is omitted, this refers to the same source file as the first location.

```
list ,last
```
Print lines ending with last.

```
list first,
```
Print lines starting with first.

```
list +
```
Print lines just after the lines last printed.

```
list -
```
Print lines just before the lines last printed.
