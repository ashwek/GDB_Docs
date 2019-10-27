# 5.1.9 How to save breakpoints to a file

----

To save breakpoint definitions to a file use the ``save breakpoints`` command.

```
save breakpoints [filename]
```
This command saves all current breakpoint definitions together with their commands and ignore counts, into a file _filename_ suitable for use in a later debugging session. This includes all types of breakpoints (breakpoints, watchpoints, catchpoints, tracepoints). To read the saved breakpoint definitions, use the ``source`` command.
