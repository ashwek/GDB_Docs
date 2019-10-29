# 5.1.2 Setting Watchpoints

----

You can use a watchpoint to stop execution whenever the value of an expression changes, without having to predict a particular place where this may happen. The expression may be as simple as the value of a single variable, or as complex as many variables combined by operators.

You can set a watchpoint on an expression even if the expression can not be evaluated yet. For instance, you can set a watchpoint on _&#42;global&#95;ptr_ before _global&#95;ptr_ is initialized. GDB will stop when your program sets _global&#95;ptr_ and the expression produces a valid value. If the expression becomes valid in some other way than changing a variable (e.g. if the memory pointed to by ‘*global_ptr’ becomes readable as the result of a malloc call), GDB may not stop until the next time the expression changes.

Depending on your system, watchpoints may be implemented in _software_ or _hardware_. GDB does software watchpointing by single-stepping your program and testing the variable’s value each time, which is hundreds of times slower than normal execution. On some systems, such as most PowerPC or x86-based targets, GDB includes support for hardware watchpoints, which do not slow down the running of your program.

```
watch [-l|-location] expr [thread thread-id] [mask maskvalue]
```
Set a watchpoint for an expression. GDB will break when the expression _expr_ is written into by the program and its value changes. The simplest use of this command is to watch the value of a single variable:

```
(gdb) watch foo
```
Ordinarily a watchpoint respects the scope of variables in _expr_. The -location argument tells GDB to instead watch the memory referred to by _expr_. In this case, GDB will evaluate _expr_, take the address of the result, and watch the memory at that address. The type of the result is used to determine the size of the watched memory. If the expression’s result does not have an address, then GDB will print an error.

The [mask maskvalue] argument allows creation of masked watchpoints, if the current architecture supports this feature. A masked watchpoint specifies a mask in addition to an address to watch. The mask specifies that some bits of an address (the bits which are reset in the mask) should be ignored when matching the address accessed by the inferior against the watchpoint address. Thus, a masked watchpoint watches many addresses simultaneously—those addresses whose unmasked bits are identical to the unmasked bits in the watchpoint address. The mask argument implies -location.

Examples:
```
(gdb) watch foo mask 0xffff00ff
(gdb) watch *0xdeadbeef mask 0xffffff00
```

```
rwatch [-l|-location] expr [thread thread-id] [mask maskvalue]
```
Set a watchpoint that will break when the value of _expr_ is read by the program.

```
awatch [-l|-location] expr [thread thread-id] [mask maskvalue]
```
Set a watchpoint that will break when _expr_ is either read from or written into by the program.

```
info watchpoints [list…]
```
This command prints a list of watchpoints, using the same format as info break.

GDB sets a hardware watchpoint if possible. Hardware watchpoints execute very quickly, and the debugger reports a change in value at the exact instruction where the change occurs. If GDB cannot set a hardware watchpoint, it sets a software watchpoint, which executes more slowly and reports the change in value at the next statement, not the instruction, after the change occurs.


_Example_
```
Reading symbols from a.out...done.
(gdb) start
Temporary breakpoint 1 at 0x649: file Xu.c, line 5.
Starting program: /home/ashwek/GitHub/a.out
Temporary breakpoint 1, main (argc=1, argv=0x7fffffffde88) at Xu.c:5
5           int i = 0;

(gdb) watch i
Hardware watchpoint 2: i

(gdb) continue
Continuing.
Hello World

Hardware watchpoint 2: i

Old value = 0
New value = 10
main (argc=1, argv=0x7fffffffde88) at Xu.c:11
11          printf("Value changed \n");

(gdb) continue
Continuing.
Value changed

Hardware watchpoint 2: i

Old value = 10
New value = 36
main (argc=1, argv=0x7fffffffde88) at Xu.c:15
15          printf("Final\n");

(gdb) continue
Continuing.
Final

Watchpoint 2 deleted because the program has left the block in
which its expression is valid.

(gdb) continue
Continuing.
[Inferior 1 (process 14403) exited normally]
```
