# 2.4 Logging Output

----

You may want to save the output of GDB commands to a file. There are several commands to control GDB’s logging.

```
set logging on
```
Enable logging.

```
set logging off
```
Disable logging.

``
set logging file file
``
Change the name of the current logfile. The default logfile is _**gdb.txt**_.

```
set logging overwrite [on|off]
```
By default, _GDB will append to the logfile_. Set overwrite if you want set logging on to overwrite the logfile instead.

```
set logging redirect [on|off]
```
By default, GDB output will go to both the terminal and the logfile. Set redirect if you want output to go only to the log file.

```
set logging debugredirect [on|off]
```
By default, GDB debug output will go to both the terminal and the logfile. Set debugredirect if you want debug output to go only to the log file.

```
show logging
```
Show the current values of the logging settings. You can also redirect the output of a GDB command to a shell command using pipe.


_Example:_
```
Reading symbols from a.out...done.

(gdb) set logging off
Done logging to gdb.txt.
(gdb) show logging
Future logs will be written to gdb.txt.
Logs will be appended to the log file.
Output will be logged and displayed.


(gdb) set logging on
Copying output to gdb.txt.
(gdb) show logging
Currently logging to "gdb.txt".
Logs will be appended to the log file.
Output will be logged and displayed.


(gdb) run
Starting program: /home/ashwek/GitHub/a.out


Hello World

[Inferior 1 (process 7944) exited normally]


(gdb) !cat gdb.txt
Currently logging to "gdb.txt".
Logs will be appended to the log file.
Output will be logged and displayed.
Starting program: /home/ashwek/GitHub/a.out
[Inferior 1 (process 7944) exited normally]
(gdb)
```
