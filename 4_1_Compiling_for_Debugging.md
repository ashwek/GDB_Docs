# 4.1 Compiling for Debugging

[Go Back](./4_Running_Programs_Under_GDB.md)

----

In order to debug a program effectively, you need to generate debugging information when you compile it. This debugging information is stored in the object file; it describes the data type of each variable or function and the correspondence between source line numbers and addresses in the executable code.

To request debugging information, specify the **-g** option when you run the compiler.

Programs that are to be shipped to your customers are compiled with optimizations, using the **-O** compiler option. However, some compilers are unable to handle the **-g** and **-O** options together. Using those compilers, you cannot generate optimized executables containing debugging information.

GCC, the GNU C/C++ compiler, supports ‘-g’ with or without ‘-O’, making it possible to debug optimized code.

GDB knows about preprocessor macros and can show you their expansion. Most compilers do not include information about preprocessor macros in the debugging information if you specify the -g flag alone. Version 3.1 and later of GCC, the GNU C compiler, provides macro information if you are using the DWARF debugging format, and specify the option -g3.
