# 4.4 Your Program’s Environment

[Go Back](./4_Running_Programs_Under_GDB.md)

----

The environment consists of a set of environment variables and their values. Environment variables conventionally record such things as your _user name_, _your home directory_, _your terminal type_, and _your search path_ for programs to run. Usually you set up environment variables with the shell and they are inherited by all the other programs you run. When debugging, it can be useful to try running your program with a modified environment without having to start GDB over again.

```
path directory
```
Add directory to the front of the ``PATH`` environment variable (the search path for executables) that will be passed to your program. The value of PATH used by GDB does not change. You may specify several directory names, separated by whitespace or by a system-dependent separator character (‘:’ on Unix, ‘;’ on MS-DOS and MS-Windows). If directory is already in the path, it is moved to the front, so it is searched sooner.

```
show paths
```
Display the list of search paths for executables.

```
show environment [varname]
```
Print the value of environment variable _varname_ to be given to your program when it starts. If you do not supply varname, print the names and values of all environment variables to be given to your program. You can abbreviate environment as env.

```
set environment varname [=value]
```
Set environment variable _varname_ to _value_. The value changes for your program, not for GDB itself. The value may be any string; the values of environment variables are just strings, and any interpretation is supplied by your program itself. The value parameter is optional; if it is eliminated, the variable is set to a null value.

```
unset environment varname
```
Remove variable _varname_ from the environment to be passed to your program. This is different from ``set env varname =``; unset environment removes the variable from the environment, rather than assigning it an empty value.
