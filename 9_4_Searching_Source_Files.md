# 9.4 Searching Source Files

----

There are two commands for searching through the current source file for a regular expression.

```
forward-search regexp
search regexp
```
The command ``forward-search regexp`` checks each line, starting with the one following the last line listed, for a match for _regexp_. It lists the line that is found. You can use the synonym ``search regexp``.

```
reverse-search regexp
```
The command ``reverse-search regexp`` checks each line, starting with the one before the last line listed and going backward, for a match for _regexp_. It lists the line that is found.
