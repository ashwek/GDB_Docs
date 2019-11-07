# 9.2.3 Address Locations

----

Address locations indicate a specific program address. They have the generalized form *address.

For line-oriented commands, such as ``list`` and ``edit``, this specifies a source line that contains address. For ``break`` and other breakpoint-oriented commands, this can be used to set breakpoints in parts of your program which do not have debugging information or source files.

Here address may be any expression valid in the current working language that specifies a code address. In addition, as a convenience, GDB extends the semantics of expressions used in locations to cover several situations that frequently occur during debugging. Here are the various forms of address:

```
expression
```
Any expression valid in the current working language.

```
funcaddr
```
An address of a function or procedure derived from its name. In C, C++, Objective-C, Fortran, minimal, and assembly, this is simply the function’s name function. This form specifies the address of the function’s first instruction, before the stack frame and arguments have been set up.

```
'filename':funcaddr
```
Like funcaddr above, but also specifies the name of the source file explicitly. This is useful if the name of the function does not specify the function unambiguously, e.g., if there are several functions with identical names in different source files.
