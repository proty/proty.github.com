---
title: Home
layout: default
---

## About

Proty is a prototype based, object oriented and dynamic programming
language. Proty uses [LLVM](http://llvm.org) as backend to either
compile any program to a small standalone executable or run it
directly using the LLVM-JIT.

Proty is still in alpha stage.

## Download

- Latest Release: [Version 0.3](http://ftp.proty.cc/proty/proty-0.3.tar.gz)
- Clone the HEAD: `git://github.com/proty/proty.git`

## Build

{% highlight bash %}
$ cd proty
$ mkdir build && cd build && cmake ..
$ make install
{% endhighlight %}

Dependencies: [LLVM](http://llvm.org), [clang](http://clang.llvm.org), [GNU Readline](http://www.gnu.org/software/readline/)

## Resources

- [Repository on **github**](https://github.com/proty/proty)
- [Issues](https://github.com/proty/proty/issues)
- [Mailing Lists](http://mail.proty.cc)
- [**#proty** on freenode](irc://chat.freenode.net/%23proty)

## License

GNU General Public License 3 - See [here](/license/).
