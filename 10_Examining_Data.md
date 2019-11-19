# 10 Examining Data

----

The usual way to examine data in your program is with the ``print`` command, or its synonym ``inspect``. It evaluates and prints the value of an expression of the language your program is written in. It may also print the expression using a Python-based pretty-printer.

```
print [[options] --] expr
print [[options] --] /f expr
```
_expr_ is an expression (in the source language). By default the value of _expr_ is printed in a format appropriate to its data type; you can choose a different format by specifying ‘/f’, where f is a letter specifying the format.

The ``print`` command supports a number of options that allow overriding relevant global print settings as set by ``set print`` subcommands:

```
-address [on|off]
```
Set printing of addresses. Related setting: ``set print address``

```
-array [on|off]
```
Pretty formatting of arrays. Related setting: ``set print array``.

```
-array-indexes [on|off]
```
Set printing of array indexes. Related setting: ``set print array-indexes``.

```
-pretty [on|off]
```
Set pretty formatting of structures. Related setting: ``set print pretty``.

```
-union [on|off]
```
Set printing of unions interior to structures. Related setting: ``set print union``.


A more low-level way of examining data is with the ``x`` command. It examines data in memory at a specified address and prints it in a specified format.

If you are interested in information about types, or about how the fields of a struct or a class are declared, use the ``ptype exp`` command rather than ``print``.

Another way of examining values of expressions and type information is through the Python extension command ``explore``.

----

[Expressions: Expressions](./10_1_Expressions.md)<br />
[Ambiguous Expressions: Ambiguous Expressions](./10_2_Ambiguous_Expressions.md)<br />
[Variables: Program variables](./10_3_Program_Variables.md)<br />
[Arrays: Artificial arrays](./10_4_Artificial_Arrays.md)<br />
[Output Formats: Output formats](./10_5_Output_Formats.md)<br />
[Memory: Examining memory](./10_6_Examining_Memory.md)<br />
