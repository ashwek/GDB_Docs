# 10.9.2 Pretty-Printer Example

----

Here is how a C++ ``std::string`` looks without a pretty-printer:

```
(gdb) print s
$1 = {
  static npos = 4294967295,
  _M_dataplus = {
    <std::allocator<char>> = {
      <__gnu_cxx::new_allocator<char>> = {
        <No data fields>}, <No data fields>
      },
    members of std::basic_string<char, std::char_traits<char>,
      std::allocator<char> >::_Alloc_hider:
    _M_p = 0x804a014 "abcd"
  }
}
```

With a pretty-printer for ``std::string`` only the contents are printed:

```
(gdb) print s
$2 = "abcd"
```
