# 5.1.3 Setting Catchpoints

----

You can use catchpoints to cause the debugger to stop for certain kinds of program events, such as C++ exceptions or the loading of a shared library. Use the catch command to set a catchpoint.

```
catch event
```
Stop when event occurs. The event can be any of the following:

```
throw [regexp]
rethrow [regexp]
catch [regexp]
```
The throwing, re-throwing, or catching of a C++ exception.
If _regexp_ is given, then only exceptions whose type matches the regular expression will be caught.
