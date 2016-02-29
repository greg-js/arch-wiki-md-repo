[Tcc](http://bellard.org/tcc/) is a small and fast C compiler.

## Installation

Install [tcc](https://www.archlinux.org/packages/?name=tcc) from the [Official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Tcc is similar to *gcc*, but because of the increased speed of *tcc* it can be useful to compile the code and run it immediately:

```
 $ tcc -run foo.c

```

You can make a C source file executed by *tcc* by adding a shebang:

```
 #!/usr/bin/tcc -run

```

## See also

*   [Wikipedia article about tcc](https://en.wikipedia.org/wiki/Tiny_C_Compiler "wikipedia:Tiny C Compiler")
*   [Clang](/index.php/Clang "Clang")