# 10.5 Output Formats

----

By default, GDB prints a value according to its data type. Sometimes this is not what you want. For example, you might want to print a number in hex, or a pointer in decimal. Or you might want to view data in memory at a certain address as a character string or as an instruction. To do these things, specify an output format when you print a value.

The simplest use of output formats is to say how to print a value already computed. This is done by starting the arguments of the ``print`` command with a slash and a format letter. The format letters supported are:

 - **x** : Regard the bits of the value as an integer, and print the integer in hexadecimal.
 - **d** : Print as integer in signed decimal.
 - **u** : Print as integer in unsigned decimal.
 - **o** : Print as integer in octal.
 - **t** : Print as integer in binary. The letter ‘t’ stands for “two”.
 - **a** : Print as an address, both absolute in hexadecimal and as an offset from the nearest preceding symbol. You can use this format used to discover where (in what function) an unknown address is located.
 - **c** : Regard as an integer and print it as a character constant.
 - **f** : Regard the bits of the value as a floating point number and print using typical floating point syntax.
 - **s** : Regard as a string, if possible. With this format, pointers to single-byte data are displayed as null-terminated strings and arrays of single-byte data are displayed as fixed-length strings. Other values are displayed in their natural types.
 - **z** : Like ``x`` formatting, the value is treated as an integer and printed as hexadecimal, but leading zeros are printed to pad the value to the size of the integer type.
 - **r** : Print using the ‘raw’ formatting. By default, GDB will use a Python-based pretty-printer, if one is available. This typically results in a higher-level display of the value’s contents.

To reprint the last value in the value history with a different format, you can use the print command with just a format and no expression. For example, ‘p/x’ reprints the last value in hex.


*Example :*
```
(gdb) print num
$12 = 66
(gdb) print/x num
$13 = 0x42
(gdb) print/d num
$14 = 66
(gdb) print/u num
$15 = 66
(gdb) print/o num
$16 = 0102
(gdb) print/t num
$17 = 1000010
(gdb) print/c num
$19 = 66 'B'
(gdb) print/f num
$20 = 9.24856986e-44
(gdb) print/s num
$21 = 66
(gdb) print/z num
$22 = 0x00000042
(gdb) print/r num
$23 = 0x00000042

(gdb) print main
$26 = {int ()} 0x555555554625 <main>
(gdb) print/a 0x555555554625
$28 = 0x555555554625 <main>
(gdb) print/a 0x555555554626
$29 = 0x555555554626 <main+1>
(gdb) print/a 0x555555554627
$30 = 0x555555554627 <main+2>
```
