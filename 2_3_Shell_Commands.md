# 2.3 Shell Commands

[Go Back](./README.md)

----

_If you need to execute occasional shell commands during your debugging session, there is no need to leave or suspend GDB; you can just use the shell command._

```
shell command-string
!command-string
```

Invoke a standard shell to execute _command-string_. Note that no space is needed between **!** and _command-string_. If it exists, the environment variable _SHELL_ determines which shell to run. Otherwise GDB uses the default shell (/bin/sh on Unix systems, COMMAND.COM on MS-DOS, etc.).

The utility **make** is often needed in development environments. You do not have to use the shell command for this purpose in GDB:

```
make make-args
```
Execute the **make** program with the specified arguments. This is equivalent to ``shell make make-args``.

```
pipe [command] | shell_command
| [command] | shell_command
pipe -d delim command delim shell_command
| -d delim command delim shell_command
```

Executes _command_ and sends its output to _shell_command_. Note that no space is needed around **&#124;**. If no command is provided, the last command executed is repeated.
