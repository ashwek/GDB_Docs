# 10.7 Automatic Display

----

If you find that you want to print the value of an expression frequently, you might want to add it to the automatic display list so that GDB prints its value each time your program stops. Each expression added to the list is given a number to identify it; to remove an expression from the list, you specify that number. The automatic display looks like this:

```
2: foo = 38
3: bar[5] = (struct hack *) 0x3804
```

This display shows item numbers, expressions and their current values. As with displays you request manually using ``x`` or ``print``, you can specify the output format you prefer; in fact, display decides whether to use ``print`` or ``x`` depending your format specification—it uses ``x`` if you specify either the 'i' or 's' format, or a unit size; otherwise it uses print.

```
display expr
```
Add the expression _expr_ to the list of expressions to display each time your program stops. ``display`` does not repeat if you press ``RET`` again after using it.

```
display/fmt expr
```
For _fmt_ specifying only a display format and not a size or count, add the expression _expr_ to the auto-display list but arrange to display it each time in the specified format _fmt_.

```
display/fmt addr
```
For _fmt_ 'i' 's', or including a unit-size or a number of units, add the expression _addr_ as a memory address to be examined each time your program stops.

```
undisplay dnums…
delete display dnums…
```
Remove items from the list of expressions to display. Specify the numbers of the displays that you want affected with the command argument _dnums_.

```
disable display dnums…
```
Disable the display of item numbers _dnums_. A disabled display item is not printed automatically, but is not forgotten. It may be enabled again later.

```
enable display dnums…
```
Enable display of item numbers _dnums_. It becomes effective once again in auto display of its expression, until you specify otherwise.

```
display
```
Display the current values of the expressions on the list, just as is done when your program stops.

```
info display
```
Print the list of expressions previously set up to display automatically, each one with its item number, but without showing the values. This includes disabled expressions, which are marked as such. It also includes expressions which would not be displayed right now because they refer to automatic variables not currently available.

If a display expression refers to local variables, then it does not make sense outside the lexical context for which it was set up. Such an expression is disabled when execution enters a context where one of its variables is not defined. For example, if you give the command display last_char while inside a function with an argument last_char, GDB displays this argument while your program continues to stop inside that function. When it stops elsewhere - where there is no variable last_char - the display is disabled automatically. The next time your program stops where last_char is meaningful, you can enable the display expression once again.
