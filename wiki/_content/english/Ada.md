[Ada](https://www.adaic.org/) is a general purpose, compiled programming language. It features strong static typing, packages, exceptions, generics, tasking, object-orientation and contracts.

## Installation

[Install](/index.php/Install "Install") the [gcc-ada](https://www.archlinux.org/packages/?name=gcc-ada) package. This will install the GNAT compiler, which is an Ada front-end for the [GNU Compiler Collection](/index.php/GNU_Compiler_Collection "GNU Compiler Collection") (GCC).

### Test your installation

Check that GNAT is installed correctly by building a simple program, as follows:

 `hello.adb` 
```
with Ada.Text_IO;

procedure Hello is
begin
   Ada.Text_IO.Put_Line ("Hello, Arch!");
end Hello;

```

You can compile it with `gnatmake`:

 `$ gnatmake hello` 
```
gcc -c hello.adb
gnatbind -x hello.ali
gnatlink hello.ali

```

Then run it:

 `$ ./hello` 
```
Hello, Arch!

```

## See also

*   [Rationale for Ada 2012](http://www.ada-auth.org/standards/rationale12.html)
*   [Ada 2012 Language Reference Manual](http://www.ada-auth.org/standards/ada12_w_tc1.html)
*   [Ada Programming at Wikibooks](https://en.wikibooks.org/wiki/Ada_Programming)
*   [Interactive learning platform Learn.adacore.com](https://learn.adacore.com/)
*   [GNAT User’s Guide for Native Platforms](https://gcc.gnu.org/onlinedocs/gnat_ugn/)
*   [GNAT Reference Manual](https://gcc.gnu.org/onlinedocs/gnat_rm/)