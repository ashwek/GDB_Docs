# 10.8 Print Settings

----

GDB provides the following ways to control how arrays, structures, and symbols are printed.

These settings are useful for debugging programs in any language:

```
set print address
set print address on
```
GDB prints memory addresses showing the location of stack traces, structure values, pointer values, breakpoints, and so forth, even when it also displays the contents of those addresses. The default is on.

```
set print address off
```
Do not print addresses when displaying their contents.

```
show print address
```
Show whether or not addresses are to be printed.

```
(gdb) set print address
(gdb) show print address
Printing of addresses is on.
(gdb) bt
#0  fact (num=3) at Xu.c:4
#1  0x000055555555468f in fact (num=4) at Xu.c:5
#2  0x000055555555468f in fact (num=5) at Xu.c:5
#3  0x00005555555546e0 in main () at Xu.c:13

(gdb) set print address off
(gdb) show print address
Printing of addresses is off.
(gdb) bt
#0  fact (num=3) at Xu.c:4
#1  fact (num=4) at Xu.c:5
#2  fact (num=5) at Xu.c:5
#3  main () at Xu.c:13
(gdb)
```

----

When GDB prints a symbolic address, it normally prints the closest earlier symbol plus an offset. If that symbol does not uniquely identify the address (for example, it is a name whose scope is a single source file), you may need to clarify. One way to do this is with ``info line``. Alternately, you can set GDB to print the source file and line number when it prints a symbolic address:

```
set print symbol-filename on
```
Tell GDB to print the source file name and line number of a symbol in the symbolic form of an address.

```
set print symbol-filename off
```
Do not print source file name and line number of a symbol. This is the default.

```
show print symbol-filename
```
Show whether or not GDB will print the source file name and line number of a symbol in the symbolic form of an address.

```
(gdb) set print symbol-filename on
(gdb) show print symbol-filename
Printing of source filename and line number with <symbol> is on.
(gdb) print main
$15 = {int ()} 0x555555554695 <main at Xu.c:9>
(gdb) print fact
$16 = {int (int)} 0x55555555466a <fact at Xu.c:3>
(gdb) info line fact
Line 3 of "Xu.c" starts at address 0x55555555466a <fact at Xu.c:3>
   and ends at 0x555555554675 <fact+11 at Xu.c:4>.

(gdb) set print symbol-filename off
(gdb) show print symbol-filename
Printing of source filename and line number with <symbol> is off.
(gdb) print main
$17 = {int ()} 0x555555554695 <main>
(gdb) print fact
$18 = {int (int)} 0x55555555466a <fact>
(gdb) info line fact
Line 3 of "Xu.c" starts at address 0x55555555466a <fact>
   and ends at 0x555555554675 <fact+11>.
```

----

```
set print symbol on
```
Tell GDB to print the symbol corresponding to an address, if one exists.

```
set print symbol off
```
Tell GDB not to print the symbol corresponding to an address. In this mode, GDB will still print the symbol corresponding to pointers to functions. This is the default.

```
show print symbol
```
Show whether GDB will display the symbol corresponding to an address.

----

Other settings control how different kinds of objects are printed:

```
set print array
set print array on
```
Pretty print arrays. This format is more convenient to read, but uses more space. The default is off.

```
set print array off
```
Return to compressed format for arrays.

```
show print array
```
Show whether compressed or pretty format is selected for displaying arrays.

```
(gdb) show print array
Pretty formatting of arrays is off.
(gdb) print arr
$41 = {1, 2, 3, 4, 5}

(gdb) set print array on
(gdb) print arr
$42 =   {1,
  2,
  3,
  4,
  5}
(gdb)
```

----

```
set print array-indexes
set print array-indexes on
```
Print the index of each element when displaying arrays. The default is off.

```
set print array-indexes off
```
Stop printing element indexes when displaying arrays.

```
show print array-indexes
```
Show whether the index of each element is printed when displaying arrays.

```
(gdb) show print array-indexes
Printing of array indexes is off.
(gdb) print arr
$46 = {1, 2, 3, 4, 5}

(gdb) set print array-indexes
(gdb) print arr
$47 = {[0] = 1, [1] = 2, [2] = 3, [3] = 4, [4] = 5}
(gdb)
```

----

```
set print elements number-of-elements
set print elements unlimited
```
Set a limit on how many elements of an array GDB will print. If GDB is printing a large array, it stops printing after it has printed the number of elements set by the set print elements command. This limit also applies to the display of strings. When GDB starts, this limit is set to 200. Setting number-of-elements to unlimited or zero means that the number of elements to print is unlimited.

```
show print elements
```
Display the number of elements of a large array that GDB will print. If the number is 0, then the printing is unlimited.

```
(gdb) show print elements
Limit on string chars or array elements to print is 200.
(gdb) print arr
$48 = {1, 2, 3, 4, 5}

(gdb) set print elements 2
(gdb) show print elements
Limit on string chars or array elements to print is 2.
(gdb) print arr
$49 = {1, 2...}
(gdb)
```

----

```
set print frame-arguments value
```
This command allows to control how the values of arguments are printed when the debugger prints a frame. The possible values are:

 - **all** : The values of all arguments are printed.
 - **scalars** : Print the value of an argument only if it is a scalar. The value of more complex arguments such as arrays, structures, unions, etc, is replaced by ``...``. This is the default.
 - **none** : None of the argument values are printed. Instead, the value of each argument is replaced by ….
 - **presence** : Only the presence of arguments is indicated by ….

By default, only scalar arguments are printed.

```
show print frame-arguments
```
Show how the value of arguments should be displayed when printing a frame.

```
(gdb) set print frame-arguments all
(gdb) bt
#0  fact (num=4, arr=0x7fffffffe030) at Xu.c:5
#1  0x000055555555469a in fact (num=5, arr=0x7fffffffe030) at Xu.c:5
#2  0x00005555555546fa in main () at Xu.c:15

(gdb) set print frame-arguments none
(gdb) bt
#0  fact (num=..., arr=...) at Xu.c:5
#1  0x000055555555469a in fact (num=..., arr=...) at Xu.c:5
#2  0x00005555555546fa in main () at Xu.c:15

(gdb) set print frame-arguments scalars
(gdb) bt
#0  fact (num=4, arr=0x7fffffffe030) at Xu.c:5
#1  0x000055555555469a in fact (num=5, arr=0x7fffffffe030) at Xu.c:5
#2  0x00005555555546fa in main () at Xu.c:15
(gdb)
```

----

```
set print entry-values value
```
Set printing of frame argument values at function entry. _In some cases_ GDB can determine the value of function argument which was passed by the function caller, even if the value was modified inside the called function and therefore is different. With optimized code, the current value could be unavailable, but the entry value may still be known.

The default value is ``default``. This functionality is currently supported only by DWARF 2 debugging format and the compiler has to produce ‘DW_TAG_call_site’ tags. With GCC, you need to specify -O -g during compilation, to get this information.

The value parameter can be one of the following:

- **no** : Print only actual parameter values, never print values from function entry point.
 - **only** : Print only parameter values from function entry point. The actual parameter values are never printed.
 - **preferred** : Print only parameter values from function entry point. If value from function entry point is not known while the actual value is known, print the actual value for such parameter.
 - **if-needed** : Print actual parameter values. If actual parameter value is not known while value from function entry point is known, print the entry point value for such parameter.
 - **both** : Always print both the actual parameter value and its value from function entry point, even if values of one or both are not available due to compiler optimizations.
 - **compact** : Print the actual parameter value if it is known and also its value from function entry point if it is known. If neither is known, print for the actual value <optimized out>.
 - **default** : Always print the actual parameter value. Print also its value from function entry point, but only if it is known. If both values are known and identical, print the shortened param=param@entry=VALUE notation.

```
(gdb) set print entry-values no
#0  equal (val=5)
(gdb) set print entry-values only
#0  equal (val@entry=5)
(gdb) set print entry-values preferred
#0  equal (val@entry=5)
(gdb) set print entry-values if-needed
#0  equal (val=5)
(gdb) set print entry-values both
#0  equal (val=5, val@entry=5)
(gdb) set print entry-values compact
#0  equal (val=val@entry=5)
(gdb) set print entry-values default
#0  equal (val=val@entry=5)
```

```
show print entry-values
```
Show the method being used for printing of frame argument values at function entry.

----

```
set print repeats number-of-repeats
set print repeats unlimited
```
Set the threshold for suppressing display of repeated array elements. When the number of consecutive identical elements of an array exceeds the threshold, GDB prints the string "<repeats n times>", where _n_ is the number of identical repetitions, instead of displaying the identical elements themselves. Setting the threshold to unlimited or zero will cause all elements to be individually printed. The default threshold is 10.

```
show print repeats
```
Display the current threshold for printing repeated identical elements.

```
(gdb) show print repeats
Threshold for repeated print elements is 10.
(gdb) print arr
$3 = {0 <repeats 20 times>}

(gdb) set print repeats 25
(gdb) print arr
$4 = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
(gdb)
```
----

```
set print null-stop
```
Cause GDB to stop printing the characters of an array when the first NULL is encountered. This is useful when large arrays actually contain only short strings. The default is off.

```
show print null-stop
```
Show whether GDB stops printing an array on the first NULL character.

```
(gdb) show print null-stop
Printing of char arrays to stop at first null char is off.
(gdb) print text
$9 = "hello\000\000\000\000"

(gdb) set print null-stop
(gdb) print text
$10 = "hello"
(gdb)
```

----

```
set print pretty on
```
Cause GDB to print structures in an indented format with one member per line.

```
set print pretty off
```
Cause GDB to print structures in a compact format.

```
show print pretty
```
Show which format GDB is using to print structures.

```
(gdb) show print pretty
Pretty formatting of structures is off.
(gdb) info locals
l1 = {b1 = {book_name = "Book 1\000\000\000", book_price = 100}, copies_available = 12}

(gdb) set print pretty
(gdb) info locals
l1 = {
  b1 = {
    book_name = "Book 1\000\000\000",
    book_price = 100
  },
  copies_available = 12
}
(gdb)
```

----

```
set print sevenbit-strings on
```
Print using only seven-bit characters; if this option is set, GDB displays any eight-bit characters using the notation \\nnn. This setting is best if you are working in English (ASCII) and you use the high-order bit of characters as a marker or "meta" bit.

```
set print sevenbit-strings off
```
Print full eight-bit characters. This allows the use of more international character sets, and is the default.

```
show print sevenbit-strings
```
Show whether or not GDB is printing only seven-bit characters.

----

```
set print union on
```
Tell GDB to print unions which are contained in structures and other unions. This is the default setting.

```
set print union off
```
Tell GDB not to print unions which are contained in structures and other unions. GDB will print "{...}" instead.

```
show print union
```
Ask GDB whether or not it will print unions which are contained in structures and other unions.

```
(gdb) show print union
Printing of unions interior to structures is on.
(gdb) info locals
l1 = {b1 = {book_name = "Book 1", book_price = 2.6687109603258062e-310}, copies_available = 12}

(gdb) set print union 0
(gdb) info locals
l1 = {b1 = {...}, copies_available = 12}
(gdb)
```

----

These settings are of interest when debugging C++ programs:

```
set print demangle
set print demangle on
```
Print C++ names in their source form rather than in the encoded form passed to the assembler and linker for type-safe linkage. The default is on.

```
show print demangle
```
Show whether C++ names are printed in mangled or demangled form.

----

```
set print asm-demangle
set print asm-demangle on
```
Print C++ names in their source form rather than their mangled form, even in assembler code printouts such as instruction disassemblies. The default is off.

```
show print asm-demangle
```
Show whether C++ names in assembly listings are printed in mangled or demangled form.

```
set demangle-style style
```
Choose among several encoding schemes used by different compilers to represent C++ names. If you omit style, you will see a list of possible formats. The default value is auto, which lets GDB choose a decoding style by inspecting your program.

```
show demangle-style
```
Display the encoding style currently in use for decoding C++ symbols.

----

```
set print object
set print object on
```
When displaying a pointer to an object, identify the actual (derived) type of the object rather than the declared type, using the virtual function table. Note that the virtual function table is required - this feature can only work for objects that have run-time type identification; a single virtual method in the object’s declared type is sufficient.

```
set print object off
```
Display only the declared type of objects, without reference to the virtual function table. This is the default setting.

```
show print object
```
Show whether actual, or declared, object types are displayed.


```
(gdb) next
30    Base *ptr = new Base();
(gdb) next

(gdb) show print object
Printing of object's derived type based on vtable info is off.
(gdb) print ptr
$1 = (Base *) 0x555555768e70
(gdb) print *ptr
$2 = {_vptr.Base = 0x555555755d68 <vtable for Base+16>, text = "Hello Base\000\000\000\000"}

(gdb) set print object on
(gdb) print ptr
$3 = (Base *) 0x555555768e70
(gdb) print *ptr
$4 = (Base) {_vptr.Base = 0x555555755d68 <vtable for Base+16>, text = "Hello Base\000\000\000\000"}

(gdb) next
32    ptr = new Child();

(gdb) set print object off
(gdb) print ptr
$5 = (Base *) 0x555555768e90
(gdb) print *ptr
$6 = {_vptr.Base = 0x555555755d50 <vtable for Child+16>, text = "Hello Base\000\000\000\000"}

(gdb) set print object on
(gdb) print ptr
$7 = (Child *) 0x555555768e90
(gdb) print *ptr
$8 = (Child) {<Base> = {_vptr.Base = 0x555555755d50 <vtable for Child+16>, text = "Hello Base\000\000\000\000"},
  text = "Hello Child\000\000\000"}
(gdb)
```

----

```
set print static-members
set print static-members on
```
Print static members when displaying a C++ object. The default is on.

```
set print static-members off
```
Do not print static members when displaying a C++ object.

```
show print static-members
```
Show whether C++ static members are printed or not.

```
(gdb) show print static-members
Printing of C++ static members is on.
(gdb) print obj
$2 = {static staticInt = 1, text = "Hello Base\000UU\000"}

(gdb) set print static-members 0
(gdb) print obj
$3 = {text = "Hello Base\000UU\000"}
(gdb)
```

----

```
set print vtbl
set print vtbl on
```
Pretty print C++ virtual function tables. The default is off.

```
set print vtbl off
```
Do not pretty print C++ virtual function tables.

```
show print vtbl
```
Show whether C++ virtual function tables are pretty printed, or not.

```
(gdb) set print vtbl

(gdb) print baseObj
$3 = {_vptr.Base = 0x555555755d68 <vtable for Base+16>}

(gdb) print childObj
$4 = {<Base> = {_vptr.Base = 0x555555755d48 <vtable for Child+16>}, <No data fields>}

(gdb) info vtbl baseObj
vtable for 'Base' @ 0x555555755d68 (subobject @ 0x7fffffffe038):
[0]: 0x555555554a1c <Base::virtualFunc1()>
[1]: 0x555555554a28 <Base::virtualFunc2()>

(gdb) info vtbl childObj
vtable for 'Child' @ 0x555555755d48 (subobject @ 0x7fffffffe040):
[0]: 0x555555554a5e <Child::virtualFunc1()>
[1]: 0x555555554a6a <Child::virtualFunc2()>
(gdb)
```
