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
[Auto Display: Automatic display](./10_7_Automatic_Display.md)<br />
[Print Settings: Print settings](./10_8_Print_Settings.md)<br />
[Pretty Printing: Python pretty printing](./10_9_Pretty_Printing.md)<br />
[Value History: Value history](./10_10_Value_History.md)<br />
Convenience Vars: Convenience variables<br />
Convenience Funs: Convenience functions<br />
[Registers: Register](./10_13_Registers.md)<br />
Floating Point Hardware: Floating point hardware<br />
Vector Unit: Vector Unit<br />
[OS Information: Auxiliary data provided by operating system](./10_16_OS_Aux_Info.md)<br />
[Memory Region Attributes: Memory region attributes](./10_17_Memory_Region_Attributes.md)<br />
[Dump/Restore Files: Copy between memory and a file](./10_18_Copy_Between_Memory_and_a_File.md)<br />
[Core File Generation: Cause a program dump its core ](./10_19_Core_Files.md)<br />
Character Sets: Debugging programs that use a different character set than GDB does<br />
Caching Target Data: Data caching for targets<br />
[Searching Memory: Searching memory for a sequence of bytes](./10_22_Search_Memory.md)<br />
