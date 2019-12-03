# 10.13 Registers

----

You can refer to machine register contents, in expressions, as variables with names starting with ‘$’. The names of registers are different for each machine; use ``info registers`` to see the names used on your machine.

```
info registers
```
Print the names and values of all registers except floating-point and vector registers (in the selected stack frame).

```
info all-registers
```
Print the names and values of all registers, including floating-point and vector registers (in the selected stack frame).

```
info registers reggroup …
```
Print the name and value of the registers in each of the specified _reggroups_. The reggroup can be any of those returned by ``maint print reggroups``.

```
info registers regname …
```
Print the relativized value of each specified register _regname_. As discussed in detail below, register values are normally relative to the selected stack frame. The _regname_ may be any register name valid on the machine you are using, with or without the initial ‘$’.

GDB has four “standard” register names that are available on most machines—whenever they do not conflict with an architecture’s canonical mnemonics for registers. The register names ``$pc`` and ``$sp`` are used for the program counter register and the stack pointer. ``$fp`` is used for a register that contains a pointer to the current stack frame, and ``$ps`` is used for a register that contains the processor status. For example, you could print the program counter in hex with

```
p/x $pc
```
or print the instruction to be executed next with

```
x/i $pc
```
or add four to the stack pointer11 with

```
set $sp += 4
```

Whenever possible, these four standard register names are available on your machine even though the machine has different canonical mnemonics, so long as there is no conflict. The ``info registers`` command shows the canonical names. For example, on the SPARC, ``info registers`` displays the processor status register as ``$psr`` but you can also refer to it as ``$ps``; and on x86-based machines ``$ps`` is an alias for the EFLAGS register.

GDB always considers the contents of an ordinary register as an integer when the register is examined in this way. Some machines have special registers which can hold nothing but floating point; these registers are considered to have floating point values. There is no way to refer to the contents of an ordinary register as floating point value.

Some machines have special registers whose contents can be interpreted in several different ways. For example, modern x86-based machines have SSE and MMX registers that can hold several values packed together in several different formats. GDB refers to such registers in struct notation:

```
(gdb) print $xmm1
$1 = {
  v4_float = {0, 3.43859137e-038, 1.54142831e-044, 1.821688e-044},
  v2_double = {9.92129282474342e-303, 2.7585945287983262e-313},
  v16_int8 = "\000\000\000\000\3706;\001\v\000\000\000\r\000\000",
  v8_int16 = {0, 0, 14072, 315, 11, 0, 13, 0},
  v4_int32 = {0, 20657912, 11, 13},
  v2_int64 = {88725056443645952, 55834574859},
  uint128 = 0x0000000d0000000b013b36f800000000
}
```

Normally, register values are relative to the selected stack frame. This means that you get the value that the register would contain if all stack frames farther in were exited and their saved registers restored. In order to see the true contents of hardware registers, you must select the innermost frame.
