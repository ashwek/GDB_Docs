# 10.6 Examining Memory

----

You can use the command ``x`` (for "examine") to examine memory in any of several formats, independently of your program's data types.

```
x/nfu addr
x addr
x
```
Use the ``x`` command to examine memory.

*n*, *f*, and *u* are all optional parameters that specify _how much memory_ to display and _how to format_ it; _addr_ is an expression giving the address where you want to start displaying memory. If you use defaults for _nfu_, you need not type the slash '/'.

```
n, the repeat count
```
The repeat count is a decimal integer; the default is 1. It specifies how much memory (counting by units u) to display. If a negative number is specified, memory is examined backward from addr.

```
f, the display format
```
The display format is one of the formats used by ``print`` _(x, d, u, o, t, a, c, f, s)_, and in addition *i* (for machine instructions). The default is ‘x’ (hexadecimal) initially.

```
u, the unit size
```
The unit size is any of
 - b : Bytes
 - h : Halfwords (two bytes)
 - w : Words (four bytes)
 - g : Giant words (eight bytes)

Each time you specify a unit size with x, that size becomes the default unit the next time you use x.

```
addr, starting display address
```
_addr_ is the address where you want GDB to begin displaying memory. The expression need not have a pointer value; it is always interpreted as an integer address of a byte of memory

For example, ``x/3uh 0x54320`` is a request to display three halfwords (h) of memory, formatted as unsigned decimal integers (u), starting at address 0x54320. ``x/4xw $sp`` prints the four words (w) of memory.
