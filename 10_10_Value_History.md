# 10.10 Value History

----

Values printed by the ``print`` command are saved in the GDB value history. This allows you to refer to them in other expressions. Values are kept until the symbol table is re-read or discarded. When the symbol table changes, the value history is discarded, since the values may contain pointers back to the types defined in the symbol table.

The values printed are given history numbers by which you can refer to them. These are successive integers starting with one. print shows you the history number assigned to a value by printing ``$num = `` before the value; here _num_ is the history number.

To refer to any previous value, use ``$`` followed by the value’s history number. The way ``print`` labels its output is designed to remind you of this. Just ``$`` refers to the most recent value in the history, and ``$$`` refers to the value before that. ``$$n`` refers to the nth value from the end; ``$$2`` is the value just prior to ``$$``, ``$$1`` is equivalent to ``$$``, and ``$$0`` is equivalent to ``$``.

For example, suppose you have just printed a pointer to a structure and want to see the contents of the structure. It suffices to type
```
p *$
```

If you have a chain of structures where the component next points to the next one, you can print the contents of the next one with this:
```
p *$.next
```

Note that the history _records values, not expressions_. If the value of ``x`` is ``4`` and you type these commands:
```
print x
set x=5
```
then the value recorded in the value history by the ``print`` command remains 4 even though the value of ``x`` has changed.

```
show values
```
Print the last *10* values in the value history, with their item numbers. This is like ``p $$9`` repeated ten times, except that show values does not change the history.

```
show values n
```
Print 10 history values centered on history item number _n_.

```
show values +
```
Print 10 history values just after the values last printed. If no more values are available, show values + produces no display.
