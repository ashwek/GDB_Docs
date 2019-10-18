# 3.2 Command Settings

[Go Back](./README.md)

----

Many commands change their behavior according to command-specific variables or settings. These settings can be changed with the **set** subcommands. For example, the **print** command prints arrays differently depending on settings changeable with the commands ``set print elements NUMBER-OF-ELEMENTS`` and ``set print array-indexes``, among others.

You can change these settings to your preference in the _**gdbinit**_ files loaded at GDB startup.

The settings can also be changed interactively during the debugging session. For example, to change the limit of array elements to print, you can do the following:

```
(GDB) set print elements 10
(GDB) print some_array
$1 = {0, 10, 20, 30, 40, 50, 60, 70, 80, 90...}
```
The above ``set print elements 10`` command changes the number of elements to print from the default of _200_ to 10. If you only intend this limit of 10 to be used for printing some_array, then you must restore the limit back to 200, with set print elements 200.

Some commands allow overriding settings with command options. For example, the _print_ command supports a number of options that allow overriding relevant global print settings as set by set print subcommands. The example above could be rewritten as:

```
(GDB) print -elements 10 -- some_array
$1 = {0, 10, 20, 30, 40, 50, 60, 70, 80, 90...}
```
Alternatively, you can use the **with** command to change a setting temporarily, for the duration of a command invocation.

```
with setting [value] [-- command]
w setting [value] [-- command]
```
Temporarily set setting to value for the duration of command.
_setting_ is any setting you can change with the _set_ subcommands. _value_ is the value to assign to setting while running command.
If no _command_ is provided, the last command executed is repeated.
If a _command_ is provided, it must be preceded by a double dash (--) separator. This is required because some settings accept free-form arguments, such as expressions or filenames.
