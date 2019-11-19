# 10.4 Artificial Arrays

----

It is often useful to print out several successive objects of the same type in memory; a section of an array, or an array of dynamically determined size for which only a pointer exists in the program.

You can do this by _referring to a **contiguous** span of memory as an artificial array_, using the binary operator ``@``. The left operand of ``@`` should be the first element of the desired array and be an individual object. The right operand should be the desired length of the array. The result is an array value whose elements are all of the type of the left argument. The first element is actually the left argument; the second element comes from bytes of memory immediately following those that hold the first element, and so on. Here is an example. If a program says

```c
int *array = (int *) malloc (len * sizeof (int));
```

you can print the contents of array with
```
p *array@len
```

The left operand of ``@`` must reside in memory. Array values made with ``@`` in this way behave just like other arrays in terms of subscripting, and are coerced to pointers when used in expressions. Artificial arrays most often appear in expressions via the value history, after printing one out.

Sometimes the artificial array mechanism is not quite enough; in moderately complex data structures, the elements of interest may not actually be adjacent. One useful work-around in this situation is to use a convenience variable as a counter in an expression that prints the first interesting value, and then repeat that expression via ``RET``. For instance, suppose you have an array ``dtab`` of pointers to structures, and you are interested in the values of a field ``fv`` in each structure. Here is an example of what you might type:

```
set $i = 0
p dtab[$i++]->fv
RET
RET
```
