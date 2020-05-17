# 19 Specifying a Debugging Target

----

A target is the execution environment occupied by your program.

Often, GDB runs in the same host environment as your program; in that case, the debugging target is specified as a side effect when you use the ``file`` or ``core`` commands.

When you need more flexibility—for example, running GDB on a physically separate host, or controlling a standalone system over a serial port or a realtime system over a TCP/IP connection—you can use the ``target`` command to specify one of the target types configured for GDB.

It is possible to build GDB for several different target architectures. When GDB is built like that, you can choose one of the available architectures with the ``set architecture`` command.

```
set architecture arch
```
This command sets the current target architecture to _arch_. The value of arch can be "auto", in addition to one of the supported architectures.

```
set processor
processor
```
These are alias commands for, respectively, ``set architecture`` and ``show architecture``.

----

# 19.3 Choosing Target Byte Order

Some types of processors, such as the MIPS, PowerPC, and Renesas SH, offer the ability to run either big-endian or little-endian byte orders. Usually the executable or symbol will include a bit to designate the endian-ness, and you will not need to worry about which to use. However, you may still find it useful to adjust GDB’s idea of processor endian-ness manually.

```
set endian big
set endian little
set endian auto
show endian
```
