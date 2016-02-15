[Pacbuilder](http://code.google.com/p/pacbuilder/) 一个小巧强大的脚本，可以自动 编译整个系统、一个源或者单个软件包。在修改了/etc/makepkg.conf 中CFLAGS的时候非常有用。

CFLAGS 的设置请参考[Makepkg - 架构和编译指令](/index.php/Makepkg#Architecture.2C_compile_flags "Makepkg")。

查看实际使用的 CFLAGS 和 CXXFLAGS:

```
pacbuilder --gccinfo

```

最常用命令:

```
pacbuilder --builddeps --keepdeps --verbose --noconfirm --install $packagename

```

和

```
pacbuilder -Sbkvn $packagename

```

### 帮助

```
$ pacbuilder -h
------------------------------- 
 PacBuilder, by Andrea Cimitan                                                                                    
-------------------------------                                                                                   

A tool to massively recompile packages from sources                                                               
It currently fetches both ABS and AUR                                                                             

USAGE:
  pacbuilder [options] package|repository

OPTIONS:
  General:
    --help                  print this help
    --clean                 remove previous log
    --gccinfo               print current compilation flags
    --nocolor               do not use any color           
    --notitle               do not print the title         
    --noresume              do not resume                  
  Install:                                                 
  (-S),    --install        build specified packages
  (-S) -b, --builddeps      build and install the dependencies
  (-S) -e, --edit           be verbose and edit PKGBUILD
  (-S) -f, --force          force install, overwrite conflicting files
  (-S) -k, --keepdeps       keep makedepends after install
  (-S) -s, --search <regex> search for packages matching <regex>
  (-S) -u, --sysupgrade     build the updated packages
  (-S) -v, --verbose        print makepkg output
  Additional parameters:
    -p, --pretend           print the final list of packages to be installed
    -n, --noconfirm         do not ask for any confirmation
    -m, --match <regex>     only install packages matching <regex>
    -d, --deplist           recursively list all dependencies first
        --export <dir>      copy packages into a dir after build
  Type:
    --world                 recompile both deps and explicit
    --explicit              recompile explicitely installed packages
    --devel                 recompile only installated devel packages
  Target repository:
    --core                  recompile packages in core
    --extra                 recompile packages in extra
    --testing               recompile packages in testing
    --community             recompile packages in community
    --aur                   recompile packages in aur

```