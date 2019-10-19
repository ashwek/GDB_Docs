# 3.4 Command options

[Go Back](./README.md)

----

Some commands accept options starting with a leading dash. For example, ``print -pretty``. Similarly to command names, you can abbreviate a GDB option to the first few letters of the option name, if that abbreviation is unambiguous, and you can also use the _TAB_ key to get GDB to fill out the rest of a word in an option.

Some options are described as accepting an argument which can be either **on** or **off**. These are known as _boolean options_. Similarly to boolean settings commands - *on* and _off_ are the typical values, but any of *1*, _yes_ and _enable_ can also be used as “true” value, and any of *0*, *no* and _disable_ can also be used as “false” value. You can also omit a “true” value, as it is implied by default.

For example, these are equivalent:
```
(gdb) print -object on -pretty off -element unlimited -- *myptr
(gdb) p -o -p 0 -e u -- *myptr
```
