# 2.2 Quitting GDB

[Go Back](./README.md)

----

```
quit [expression]
q
```

To exit GDB, use the **quit** command _(abbreviated **q**)_, or type an _end-of-file_ character _(usually **Ctrl-d**)_. If you do not supply expression, GDB will terminate normally; otherwise it will terminate using the result of expression as the error code.

An interrupt (often Ctrl-c) does not exit from GDB, but rather terminates the action of any GDB command that is in progress and returns to GDB command level. It is safe to type the interrupt character at any time because GDB does not allow it to take effect until a time when it is safe.

If you have been using GDB to control an attached process or device, you can release it with the **detach** command.
