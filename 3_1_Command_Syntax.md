# 3.1 Command Syntax

[Go Back](./README.md)

----

A GDB command is a single line of input. There is no limit on how long it can be. It starts with a command name, which is followed by arguments whose meaning depends on the command name. For example, the command **step** accepts an argument which is the number of times to _step_, as in ``step 5``. You can also use the _step_ command with no arguments. Some commands do not allow any arguments.

GDB command names may always be truncated if that abbreviation is unambiguous. In some cases, even ambiguous abbreviations are allowed; for example, **s** is specially defined as equivalent to **_step_** even though there are other commands whose names start with _s_.

_A blank line as input to GDB means to repeat the previous command._ Certain commands (for example, _**run**_) will not repeat this way; these are commands whose unintentional repetition might cause trouble and which you are unlikely to want to repeat. User-defined commands can disable this feature.

The **list** and **x** commands, when you repeat them with **RET**, construct new arguments rather than repeating exactly as typed. This permits easy scanning of source or memory.

GDB can also use _RET_ in another way: to partition lengthy output, in a way similar to the common utility more. Since it is easy to press one RET too many in this situation, GDB disables command repetition after any command that generates this sort of display.

Any text from a **#** to the end of the line is a comment; it does nothing. This is useful mainly in command files.

The **Ctrl-o** binding is useful for _repeating a complex **sequence** of commands_. This command accepts the current line, and then _fetches_ the next line relative to the current line from the history for editing.
