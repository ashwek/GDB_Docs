# 10.9.1 Pretty-Printer Introduction

----

When GDB prints a value, it first sees if there is a pretty-printer registered for the value. If there is then GDB invokes the pretty-printer to print the value. Otherwise the value is printed normally.

Pretty-printers are normally named. This makes them easy to manage. The ``info pretty-printer`` command will list all the installed pretty-printers with their names. If a pretty-printer can handle multiple data types, then its subprinters are the printers for the individual data types. Each such subprinter has its own name. The format of the name is _printer-name;subprinter-name_.

Pretty-printers are installed by registering them with GDB. Typically they are automatically loaded and registered when the corresponding debug information is loaded, thus making them available without having to do anything special.

There are three places where a pretty-printer can be registered.

 - Pretty-printers registered globally are available when debugging all inferiors.
 - Pretty-printers registered with a program space are available only when debugging that program.
 - Pretty-printers registered with an objfile are loaded and unloaded with the corresponding objfile.
