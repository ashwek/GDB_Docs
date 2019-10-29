# 5.4 Signals

----

A signal is an _asynchronous_ event that can happen in a program. The OS defines the possible kinds of signals, and gives each kind a name and a number. For example, in Unix _SIGINT_ is the signal a program gets when you type an interrupt character (often Ctrl-c); _SIGSEGV_ is the signal a program gets from referencing a place in memory far away from all the areas in use; _SIGALRM_ occurs when the alarm clock timer goes off (which happens only if your program has requested an alarm).

Some signals, including _SIGALRM_, are a normal part of the functioning of your program. Others, such as _SIGSEGV_, indicate errors; these signals are fatal (they kill your program immediately) if the program has not specified in advance some other way to handle the signal. _SIGINT_ does not indicate an error in your program, but it is normally fatal so it can carry out the purpose of the interrupt: to kill the program.

GDB has the ability to detect any occurrence of a signal in your program. You can tell GDB in advance what to do for each kind of signal.

Normally, GDB is set up to let the non-erroneous signals like _SIGALRM_ be silently passed to your program but to stop your program immediately whenever an error signal happens. You can change these settings with the handle command.

```
info signals
info handle
```
Print a table of all the kinds of signals and how GDB has been told to handle each one. You can use this to see the signal numbers of all the defined types of signals.

```
info signals sig
```
Similar, but print information only about the specified signal number.

``info handle`` is an alias for ``info signals``

```
catch signal [signal… | ‘all’]
```
Set a catchpoint for the indicated signals.

```
handle signal [keywords…]
```
Change the way GDB handles _signal_ signal. The _signal_ can be the number of a signal or its name (with or without the ‘SIG’ at the beginning); a list of signal numbers of the form ‘low-high’; or the word ‘all’, meaning all the known signals. Optional arguments keywords, described below, say what change to make.

The keywords allowed by the ``handle`` command can be abbreviated. Their full names are:

```
nostop
```
GDB should not stop your program when this signal happens. It may still print a message telling you that the signal has come in.

```
stop
```
GDB should stop your program when this signal happens. This implies the print keyword as well.

```
print
```
GDB should print a message when this signal happens.

```
noprint
```
GDB should not mention the occurrence of the signal at all. This implies the nostop keyword as well.

```
pass
noignore
```
GDB should allow your program to see this signal; your program can handle the signal, or else it may terminate if the signal is fatal and not handled. ``pass`` and ``noignore`` are synonyms.

```
nopass
ignore
```
GDB should not allow your program to see this signal. ``nopass`` and ``ignore`` are synonyms.

When a signal stops your program, the signal is not visible to the program until you continue. Your program sees the signal then, if ``pass`` is in effect for the signal in question at that time. In other words, after GDB reports a signal, you can use the handle command with pass or nopass to control whether your program sees that signal when you continue.

The default is set to ``nostop``, ``noprint``, ``pass`` for non-erroneous signals such as _SIGALRM_, _SIGWINCH_ and _SIGCHLD_, and to ``stop``, ``print``, ``pass`` for the erroneous signals.

You can also use the ``signal`` command to prevent your program from seeing a signal, or cause it to see a signal it normally would not see, or to give it any signal at any time.

For example, if your program stopped due to some sort of memory reference error, you might store correct values into the erroneous variables and continue, hoping to see more execution; but your program would probably terminate immediately as a result of the fatal signal once it saw the signal. To prevent this, you can continue with ``signal 0``.

GDB optimizes for stepping the mainline code. If a signal that has ``handle nostop`` and ``handle pass`` set arrives while a stepping command (e.g., stepi, step, next) is in progress, GDB lets the signal handler run and then resumes stepping the mainline code once the signal handler returns. In other words, GDB steps over the signal handler. This prevents signals that you’ve specified as not interesting from changing the focus of debugging unexpectedly. Note that the signal handler itself may still hit a breakpoint, stop for another signal that has ``handle stop`` in effect, or for any other event that normally results in stopping the stepping command sooner. Also note that GDB still informs you that the program received a signal if handle print is set.

If you set ``handle pass`` for a signal, and your program sets up a handler for it, then issuing a stepping command, such as ``step`` or ``stepi``, when your program is stopped due to the signal will step into the signal handler.
