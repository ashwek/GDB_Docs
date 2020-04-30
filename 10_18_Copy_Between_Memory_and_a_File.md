# 10.18 Copy Between Memory and a File

----

You can use the commands ``dump``, ``append``, and ``restore`` to copy data between **target memory** and a **file**.

The ``dump`` and ``append`` commands _write_ data to a file, and the ``restore`` command _reads_ data from a file back into the inferior’s memory.

Files may be in
 - binary
 - Motorola S-record
 - Intel hex
 - Tektronix Hex
 - Verilog Hex format

GDB can only append to binary files, and cannot read from Verilog Hex files.

```
dump [format] memory filename start_addr end_addr
dump [format] value filename expr
```
Dump the contents of memory from _start\_addr_ to _end\_addr_, or the value of _expr_, to filename in the given format.

```
append [binary] memory filename start_addr end_addr
append [binary] value filename expr
```
Append the contents of memory from _start\_addr_ to _end\_addr_, or the value of _expr_, to the file _filename_, in raw binary form.

```
restore filename [binary] bias start end
```
Restore the contents of file _filename_ into memory. The ``restore`` command can automatically recognize any known BFD file format, except for raw binary. To restore a raw binary file you must specify the optional keyword **binary** after the filename.
