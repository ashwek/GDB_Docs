# 10.19 How to Produce a Core File from Your Program

----

A **core file** or **core dump** is a file that records the memory image of a running process and its process status (register values etc.). Its primary use is post-mortem debugging of a program that crashed while it ran outside a debugger.

A program that crashes automatically produces a core file, unless this feature is disabled by the user.

Occasionally, you may wish to produce a core file of the program you are debugging in order to preserve a snapshot of its state. GDB has a special command for that.

```
generate-core-file [file]
gcore [file]
```
Produce a core dump of the inferior process. The optional argument _file_ specifies the file name where to put the core dump. If not specified, the file name defaults to _core.pid_, where pid is the inferior process ID.

Note that this command is implemented only for some systems (as of this writing, GNU/Linux, FreeBSD, Solaris, and S390).
