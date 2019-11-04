# 8.2 Backtraces

----

A backtrace is a summary of how your program got where it is. It shows one line per frame, for many frames, starting with the currently executing frame (frame zero), followed by its caller (frame one), and on up the stack.

To print a backtrace of the entire stack, use the ``backtrace`` command, or its alias ``bt``. This command will print one line per frame for frames in the stack. By default, all stack frames are printed. You can stop the backtrace at any time by typing the system interrupt character, normally _Ctrl-c_.

```
backtrace [option]… [qualifier]… [count]
bt [option]… [qualifier]… [count]
```
Print the backtrace of the entire stack.

The optional _count_ can be one of the following:

```
n
n
```
Print only the innermost _n_ frames, where _n_ is a positive number.

```
-n
-n
```
Print only the outermost _n_ frames, where _n_ is a positive number.

_Options:_

```
-full
```
Print the values of the local variables also. This can be combined with the optional _count_ to limit the number of frames shown.

```
-no-filters
```
Do not run Python frame filters on this backtrace.

```
-hide
```
A Python frame filter might decide to “elide” some frames. Normally such elided frames are still printed, but they are indented relative to the filtered frames that cause them to be elided.

The names ``where`` and ``info stack`` are additional aliases for ``backtrace``.

In a multi-threaded program, GDB by default shows the backtrace only for the current thread. To display the backtrace for several or all of the threads, use the command ``thread apply``. For example, if you type ``thread apply all backtrace``, GDB will display the backtrace for all the threads; this is handy when you debug a core dump of a multi-threaded program.

Each line in the backtrace shows the frame number and the function name. The program counter value is also shown—unless you use set ``print address off``. The backtrace also shows the source file name and line number, as well as the arguments to the function. The program counter value is omitted if it is at the beginning of the code for that line number.

Here is an example of a backtrace of a program to recursively find factorial.

```
(gdb) bt
#0  fact (num=2) at Xu.c:4
#1  0x000055555555466f in fact (num=3) at Xu.c:5
#2  0x000055555555466f in fact (num=4) at Xu.c:5
#3  0x000055555555466f in fact (num=5) at Xu.c:5
#4  0x000055555555468e in main () at Xu.c:11
```

If your program was compiled with optimizations, some compilers will optimize away arguments passed to functions if those arguments are never used after the call. Such optimizations generate code that passes arguments through registers, but doesn’t store those arguments in the stack frame. GDB has no way of displaying such arguments in stack frames other than the innermost one.

The values of arguments that were not saved in their stack frames are shown as ``<optimized out>``.
