# 17 Altering Execution

----

Once you think you have found an error in your program, you might want to find out for certain whether correcting the apparent error would lead to correct results in the rest of the run. You can find the answer by experiment, using the GDB features for altering execution of the program.

----

## 17.1 Assignment to Variables

To alter the value of a variable, evaluate an assignment expression.
```
print x=4
```
stores the value `4` into the variable `x`, and then prints the value of the assignment expression.

If you are not interested in seeing the value of the assignment, use the ``set`` command instead of the ``print`` command.
```
(gdb) set var width=47
```

----

## 17.2 Continuing at a Different Address

Ordinarily, when you continue your program, you do so at the place where it stopped, with the ``continue`` command. You can instead continue at an address of your own choosing, with the following commands:
```
jump location
j location
```
Resume execution at location. Execution stops again immediately if there is a breakpoint there.

On many systems, you can get much the same effect as the ``jump`` by storing a new value into the register ``$pc``. The difference is that this does not start your program running; it only changes the address of where it will run when you continue. For example,
```
set $pc = 0x485

```
makes the next continue command or stepping command execute at address 0x485, rather than at the address where your program stopped.

The most common occasion to use the jump command is to back up—perhaps with more breakpoints set—over a portion of a program that has already executed, in order to examine its execution in more detail.

----

## 17.3 Giving your Program a Signal

```
signal signal
```
Resume execution where your program is stopped, but immediately give it the signal ``signal``. The _signal_ can be the name or the number of a signal. For example, on many systems signal 2 and signal ``SIGINT`` are both ways of sending an interrupt signal.

Alternatively, if signal is zero, continue execution without giving a signal. This is useful when your program stopped on account of a signal and would ordinarily see the signal when resumed with the continue command; ‘signal 0’ causes it to resume without a signal.

```
queue-signal signal
```
Queue signal to be delivered immediately to the current thread when execution of the thread resumes. The signal can be the name or the number of a signal.

----

## 17.4 Returning from a Function

```
return
return expression
```
You can cancel execution of a function call with the ``return`` command. If you give an expression argument, its value is used as the function’s return value.

When you use return, GDB discards the selected stack frame (and all frames within it). You can think of this as making the discarded frame return prematurely. If you wish to specify a value to be returned, give that value as the argument to return.

----

## 17.5 Calling Program Functions

```
print expr
```
Evaluate the expression _expr_ and display the resulting value. The expression may include calls to functions in the program being debugged.
call expr

You can use this variant of the ``print`` command if you want to execute a function from your program that does not return anything, but without cluttering the output with void returned values that GDB will otherwise print. If the result is not void, it is printed and saved in the value history.

It is possible for the function you call via the ``print`` or ``call`` command to generate a signal. What happens in that case is controlled by the ``set unwindonsignal`` command.

----

## 17.6 Patching Programs

By default, GDB opens the file containing your program’s executable code read-only. This prevents accidental alterations to machine code; but it also prevents you from intentionally patching your program’s binary.

If you’d like to be able to patch the binary, you can specify that explicitly with the ``set write`` command. For example, you might want to turn on internal debugging flags, or even to make emergency repairs.
```
set write on
set write off
```
If you specify ``set write on``, GDB opens executable and core files for both reading and writing; if you specify ``set write off`` (the default), GDB opens them read-only.

If you have already loaded a file, you must load it again (using the ``exec-file`` or ``core-file`` command) after changing ``set write``, for your new setting to take effect.
