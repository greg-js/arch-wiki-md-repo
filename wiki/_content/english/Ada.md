[Ada](https://www.adaic.org/) is a general purpose, compiled programming language. It features strong static typing, packages, exceptions, generics, tasking, object-orientation and contracts.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Test your installation](#Test_your_installation)
*   [2 See also](#See_also)
    *   [2.1 Language](#Language)
    *   [2.2 Tools](#Tools)
    *   [2.3 Libraries](#Libraries)

## Installation

[Install](/index.php/Install "Install") the [gcc-ada](https://www.archlinux.org/packages/?name=gcc-ada) package. This will install the GNAT compiler, which is an Ada front-end for the [GNU Compiler Collection](/index.php/GNU_Compiler_Collection "GNU Compiler Collection") (GCC).

Additional packages:

*   [gprbuild](https://aur.archlinux.org/packages/gprbuild/) - GPRbuild build system
*   [xmlada](https://aur.archlinux.org/packages/xmlada/) - XML/Ada
*   [ada-web-server](https://aur.archlinux.org/packages/ada-web-server/) - Ada Web Server
*   [aunit](https://aur.archlinux.org/packages/aunit/) - Ada Unit Testing Framework
*   GNATColl - GNAT Components Collection
    *   [gnatcoll-core](https://aur.archlinux.org/packages/gnatcoll-core/)
    *   [gnatcoll-db2ada](https://aur.archlinux.org/packages/gnatcoll-db2ada/)
    *   [gnatcoll-gmp](https://aur.archlinux.org/packages/gnatcoll-gmp/)
    *   [gnatcoll-iconv](https://aur.archlinux.org/packages/gnatcoll-iconv/)
    *   [gnatcoll-postgres](https://aur.archlinux.org/packages/gnatcoll-postgres/)
    *   [gnatcoll-python](https://aur.archlinux.org/packages/gnatcoll-python/)
    *   [gnatcoll-readline](https://aur.archlinux.org/packages/gnatcoll-readline/)
    *   [gnatcoll-sql](https://aur.archlinux.org/packages/gnatcoll-sql/)
    *   [gnatcoll-sqlite](https://aur.archlinux.org/packages/gnatcoll-sqlite/)
    *   [gnatcoll-xref](https://aur.archlinux.org/packages/gnatcoll-xref/)

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

### Language

*   [Rationale for Ada 2012](http://www.ada-auth.org/standards/rationale12.html)
*   [Ada 2012 Language Reference Manual](http://www.ada-auth.org/standards/ada12_w_tc1.html)
*   [Ada Programming at Wikibooks](https://en.wikibooks.org/wiki/Ada_Programming)
*   [Interactive learning platform Learn.adacore.com](https://learn.adacore.com/)

### Tools

*   [GNAT User’s Guide for Native Platforms](https://gcc.gnu.org/onlinedocs/gnat_ugn/)
*   [GNAT Reference Manual](https://gcc.gnu.org/onlinedocs/gnat_rm/)
*   [GPRbuild and GPR Companion Tools User’s Guide](https://docs.adacore.com/live/wave/gprbuild/html/gprbuild_ug/gprbuild_ug.html)

### Libraries

*   [XML/Ada: The Unicode and XML Library for Ada](https://docs.adacore.com/live/wave/xmlada/html/xmlada_ug/index.html)
*   [AWS: The Ada Web Server](https://docs.adacore.com/live/wave/aws/html/aws_ug/index.html)
*   [AUnit Cookbook](https://docs.adacore.com/live/wave/aunit/html/aunit_cb/aunit_cb.html)
*   [GNAT Reusable Components](https://docs.adacore.com/live/wave/gnatcoll/html/gnatcoll_ug/index.html)