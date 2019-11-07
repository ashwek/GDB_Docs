# 9.3 Editing Source Files

----

To edit the lines in a source file, use the ``edit`` command. The editing program of your choice is invoked with the current line set to the active line in the program. Alternatively, there are several ways to specify what part of the file you want to print if you want to see other parts of the program:

```
edit location
```
Edit the source file specified by _location_. Editing starts at that _location_, e.g., at the specified source line of the specified file.

```
edit number
```
Edit the current source file with _number_ as the active line number.

```
edit function
```
Edit the file containing _function_ at the beginning of its definition.


## 9.3.1 Choosing your Editor

You can customize GDB to use any editor you want. By default, it is ``/bin/ex``, but you can change this by setting the environment variable ``EDITOR`` before using GDB. For example, to configure GDB to use the ``vi`` editor, you could use these commands with the sh shell:

```
EDITOR=/usr/bin/vi
export EDITOR
gdb …
```
or in the csh shell,
```
setenv EDITOR /usr/bin/vi
gdb …
```
