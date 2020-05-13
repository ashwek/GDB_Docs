# 15 Using GDB with Different Languages

----

## 15.2 Displaying the Language

```
show language
```
Display the current working language. This is the language you can use with commands such as ``print`` to build and compute expressions that may involve variables in your program.

----

## 15.4 Supported Languages

GDB supports
 - C
 - C++
 - D
 - Go
 - Objective-C
 - Fortran
 - QpenCL C
 - Pascal
 - Rust
 - assembly
 - Modula-2
 - Ada

Some GDB features may be used in expressions regardless of the language you use.
