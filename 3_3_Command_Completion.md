# 3.3 Command Completion

[Go Back](./README.md)

----

GDB can fill in the rest of a word in a command for you, if there is only one possibility; it can also show you what the valid possibilities are for the next word in a command, at any time.

Press the _TAB_ key whenever you want GDB to fill out the rest of a word. If there is only one possibility, GDB fills in the word, and waits for you to finish the command

If there is more than one possibility for the next word when you press TAB, GDB sounds a bell. You can either supply more characters and try again, or just press TAB a second time; GDB displays all the possible completions for that word.

If the number of possible completions is large, GDB will print as much of the list as it has collected, as well as a message indicating that the list may be truncated.
This behavior can be controlled with the following commands:

```
set max-completions limit
set max-completions unlimited
```
Set the maximum number of completion candidates. GDB will stop looking for more completions once it collects this many candidates. This is useful when completing on things like function names as collecting all the possible candidates can be time consuming. The default value is 200. A value of zero disables tab-completion. Note that setting either no limit or a very large limit can make completion slow.

```
show max-completions
```
Show the maximum number of candidates that GDB will collect and show during completion.

The completer can be confused by certain kinds of invalid expressions. Also, it only examines the static type of the expression, not the dynamic type.
