# 10.22 Search Memory

----

Memory can be searched for a particular sequence of bytes with the ``find`` command.

```
find [/sn] start_addr, +len, val1 [, val2, …]
find [/sn] start_addr, end_addr, val1 [, val2, …]
```
Search memory for the sequence of bytes specified by _val1_, _val2_, etc. The search begins at address _start\_addr_ and continues for either _len_ bytes or through to _end\_addr_ inclusive.

_s_ and _n_ are optional parameters. They may be specified in either order, apart or together.

 - s : search query size
 - n : maximum number of finds
