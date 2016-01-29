# Heirloom

The [Heirloom project](http://heirloom.sourceforge.net/) mantains classical UNIX tools and utilities for modern open source operating systems.

## Contents

*   [1 Heirloom Bourne Shell](#Heirloom_Bourne_Shell)
*   [2 Heirloom Development Tools](#Heirloom_Development_Tools)
*   [3 Heirloom Toolchest](#Heirloom_Toolchest)
*   [4 Heirloom Documentation tools](#Heirloom_Documentation_tools)
*   [5 The Heirloom Packaging tools](#The_Heirloom_Packaging_tools)

## [Heirloom Bourne Shell](http://heirloom.sourceforge.net/sh.html)

The classical Bourne shell has been made available through the Heirloom project and is available as an [AUR(CVS)](https://aur.archlinux.org/packages.php?ID=44332) or as a static release [AUR](https://aur.archlinux.org/packages.php?ID=9909).

In this package, the Bourne shell is installed as

```
/usr/heirloom/bin/sh

```

and symlinked as

```
/usr/heirloom/bin/jsh

```

## [Heirloom Development Tools](http://heirloom.sourceforge.net/devtools.html)

The heirloom development tools provide tools like **yacc**, **lex**, **m4**, **make**, and **SCCS**. This package, together with the Bourne shell, form a dependency foundation for the rest of the Heirloom packages. The classical devtools ensures consistent behavior, independently of changes made to the corresponding GNU tools.

The [heirloom-devtools-cvs](https://aur.archlinux.org/packages/heirloom-devtools-cvs/)<sup><small>AUR</small></sup> [AUR](/index.php/AUR "AUR") package installs the following files:

 `/usr/heirloom/bin` 

```
admin  cdc  comb  delta  get  help  lex  m4  make  prs  prt  rmdel  sact  sccs  sccsdiff  unget  val  vc  what  yacc

```

 `/usr/heirloom/bin/posix/` 

```
m4 make

```

 `/usr/heirloom/lib` 

```
help  lex  libl.a  liby.a  svr4.make  yaccpar

```

## [Heirloom Toolchest](http://heirloom.sourceforge.net/tools.html)

This package contains classical UNIX binaries corresponding to GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils), [diffutils](https://www.archlinux.org/packages/?name=diffutils), tar and more. The binaries are organized according to the different UNIX releases, so that one can choose which generation of UNIX environment to run.

The Heirloom Toolchest is available as an [heirloom-cvs](https://aur.archlinux.org/packages/heirloom-cvs/)<sup><small>AUR</small></sup> [AUR](/index.php/AUR "AUR") package, which installs the following files:

 `/usr/heirloom/bin` 

```
apropos   catman  cpio     diff3    factor  grep    line      mkfifo   nl      pkill    pwd    shl      tabs   tr    uptime
awk       chgrp   csplit   dircmp   false   groups  listusers mknod    nohup   random   sleep  tail     true
users     banner  chmod    cut      dirname fgrep   hd        ln       more    oawk     renice sort     tape
tsort     w       basename chown    date    du      file      head     logins  mt       od     pr       rm     spell tapecntl
tty       wc      bc       cksum    dc      echo    find      hostname logname mv       page   printenv rmdir  split tar
whatis    bdiff   cmp      dd       ed      fmt     id        ls       mvdir   paste    printf stty     tcopy  ul    who
bfs       col     deroff   egrep    fmtmsg  install mail      nawk     pathchk priocntl sdiff  STTY     tee    uname
whoami    cal     comm     df       env     fold    join      man      newform pax      ps     sed      su     test
unexpand  whodo   calendar copy     dfspace expand  getconf   kill     mesg    news     pg     psrinfo  setpgrp
sum       time    uniq     xargs    cat     cp      diff      expr     getopt  lc       mkdir  nice     pgrep  ptime settime
sync      touch   units    yes

```

 `/usr/heirloom/bin/posix/` 

```
awk      chmod csplit du   ed    expr  file  getconf  id  ls    mv   nl    od  pg  ps rmdir sort touch wc
basename cp    date   echo egrep fgrep find  grep     ln  mkdir nawk nohup pax pr  rm sed   test tr
who

```

 `/usr/heirloom/bin/posix2001/` 

```
awk      chmod csplit du   ed    expr  file getconf id ls    mv   nl    od  pg ps rmdir sort touch  wc
basename cp    date   echo egrep fgrep find grep    ln mkdir nawk nohup pax pr rm sed   test tr
who

```

 `/usr/heirloom/bin/s42/` 

```
awk chmod    csplit du   ed   expr  file  getconf id   ln mkdir mv   nl   od    pax  pr ps       rmdir sort touch  
wc  basename cp     date echo egrep fgrep find    grep lc ls    more nawk nohup page pg priocntl rm
sed test     tr     who

```

 `/usr/heirloom/bin/ucb/` 

```
apropos catman   deroff du expand hostname ln      man printenv ps  sccs   sum   test  ul uptime   w
whoami  basename chown  df echo   groups   install ls  more     prt renice stty  tcopy tr unexpand
users   whatis

```

## [Heirloom Documentation tools](http://heirloom.sourceforge.net/doctools.html)

The Heirloom Documentation tools provides an alternative to **groff** with powerful capabilities, like open document compatibility etc. Building this package, which is avaliable as an [heirloom-doctools-cvs](https://aur.archlinux.org/packages/heirloom-doctools-cvs/)<sup><small>AUR</small></sup> [AUR](/index.php/AUR "AUR") package, requires the Heirloom shell, devtools and toolchest.

## [The Heirloom Packaging tools](http://heirloom.sourceforge.net/pkgtools.html)

The Heirloom packaging tools are a port of Sun SVR4's package management system, which was released as open source with opensolaris. This package requires the Heirloom shell, devtools and toolchest and is available as an [heirloom-pkgtools-cvs](https://aur.archlinux.org/packages/heirloom-pkgtools-cvs/)<sup><small>AUR</small></sup> [AUR](/index.php/AUR "AUR") package.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Heirloom&oldid=409682](https://wiki.archlinux.org/index.php?title=Heirloom&oldid=409682)"