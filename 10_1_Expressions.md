# 10.1 Expressions

----

``print`` and many other GDB commands accept an expression and compute its value. Any kind of constant, variable or operator defined by the programming language you are using is valid in an expression in GDB. This includes conditional expressions, function calls, casts, and string constants. It also includes preprocessor macros, if you compiled your program to include this information.

GDB supports array constants in expressions input by the user. The syntax is _{element, element...}_. For example, you can use the command ``print {1, 2, 3}`` to create an array of three integers. If you pass an array to a function or assign it to a program variable, GDB copies the array to memory that is malloced in the target program.

GDB supports these operators, in addition to those common to programming languages:

```
@
```
‘@’ is a binary operator for treating parts of memory as arrays.

```
::
```
‘::’ allows you to specify a variable in terms of the file or function where it is defined.

```
{type} addr
```
Refers to an object of type _type_ stored at address _addr_ in memory. The address _addr_ may be any expression whose value is an integer or pointer.
