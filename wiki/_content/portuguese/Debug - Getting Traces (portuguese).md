Esse artigo visa ajudar na criação de um pacote de depuração do Arch e usá-lo para fornecer informações de rastro e depuração para relatar bugs de software para desenvolvedores.

## Contents

*   [1 Nomes de pacotes](#Nomes_de_pacotes)
*   [2 PKGBUILD](#PKGBUILD)
*   [3 Configurações de compilação](#Configura.C3.A7.C3.B5es_de_compila.C3.A7.C3.A3o)
    *   [3.1 Geral](#Geral)
    *   [3.2 Qt4](#Qt4)
    *   [3.3 Qt5](#Qt5)
    *   [3.4 Aplicativos CMAKE (KDE)](#Aplicativos_CMAKE_.28KDE.29)
*   [4 Compilando e instalando o pacote](#Compilando_e_instalando_o_pacote)
*   [5 Obtendo o rastro](#Obtendo_o_rastro)
*   [6 Conclusão](#Conclus.C3.A3o)
*   [7 Veja também](#Veja_tamb.C3.A9m)

## Nomes de pacotes

Ao procurar por mensagens de depuração, tal como:

```
[...]
Backtrace was generated from '/usr/bin/epiphany'

**(no debugging symbols found)**
Using host libthread_db library "/lib/libthread_db.so.1".
**(no debugging symbols found)**
[Thread debugging using libthread_db enabled]
[New Thread -1241265952 (LWP 12630)]
(no debugging symbols found)
0xb7f25410 in __kernel_vsyscall ()
#0  0xb7f25410 in __kernel_vsyscall ()
#1  0xb741b45b in **??** () from /lib/libpthread.so.0
[...]

```

`??` mostra onde a informação de depuração está faltando, assim como o nome da biblioteca ou executável que chamou a função. Similarmente, quando `(no debugging symbols found)` aparece, você deve procurar pelos nomes de arquivos mencionados. Por exemplo, com [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"):

```
$ pacman -Qo /lib/libthread_db.so.1
/lib/libthread_db.so.1 pertence a *glibc* 2.5-8

```

O pacote é chamado [glibc](https://www.archlinux.org/packages/?name=glibc) na versão 2.5-8\. Repita essa etapa para todo pacote que precisa de depuração.

## PKGBUILD

Para compilar um pacote a partir do fonte, o arquivo PKGBUILD file é necessário. Veja [ABS (Português)](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") para pacotes nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"), e [AUR (Português)#Obtendo arquivos de compilação](/index.php/AUR_(Portugu%C3%AAs)#Obtendo_arquivos_de_compila.C3.A7.C3.A3o "AUR (Português)") para pacotes no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)").

## Configurações de compilação

Neste estágio, você pode modificar o arquivo de configuração global do `makepkg` se você for usá-lo apenas para propósito de depuração. Nos demais casos, você deve modificar o arquivo PKGBUILD do pacote apenas para cada pacote que você gostaria de recompilar.

### Geral

As of pacman 4.1, `/etc/makepkg.conf` has debug compilation flags in `DEBUG_CFLAGS` and `DEBUG_CXXFLAGS`. To use them, enable the `debug` makepkg option, and disable `strip`.

```
OPTIONS+=(debug !strip)

```

These settings will force compilation with debugging information and will disable the stripping of debug symbols from executables. To apply this setting to a single package, modify the PKGBUILD:

```
options=(debug !strip)

```

Alternatively you can put the debug information in a separate package by enabling both `debug` and `strip`, debugging information will then be stripped from the main package and placed in a separate `*foo*-debug` package.

**Note:** It is insufficient to simply install the newly compiled debug package, because the debugger will check that the file containing the debug symbols is from the same build as the associated library and executable. You must install both of the recompiled packages. In Arch, the debug symbols files are installed under `/usr/lib/debug`. See the [GDB documentation](https://sourceware.org/gdb/onlinedocs/gdb/Separate-Debug-Files.html) for more information about debug packages.

Note that certain packages such as *glibc* are stripped regardless. Check the PKGBUILD for sections such as:

```
strip $STRIP_BINARIES usr/bin/{gencat,getconf,getent,iconv,iconvconfig} \
                      usr/bin/{ldconfig,locale,localedef,nscd,makedb} \
                      usr/bin/{pcprofiledump,pldd,rpcgen,sln,sprof} \
                      usr/lib/getconf/*
[[ $CARCH = "i686" ]] && strip $STRIP_BINARIES usr/bin/lddlibc4

strip $STRIP_STATIC usr/lib/*.a

strip $STRIP_SHARED usr/lib/{libanl,libBrokenLocale,libcidn,libcrypt}-*.so \
                    usr/lib/libnss_{compat,db,dns,files,hesiod,nis,nisplus}-*.so \
                    usr/lib/{libdl,libm,libnsl,libresolv,librt,libutil}-*.so \
                    usr/lib/{libmemusage,libpcprofile,libSegFault}.so \
                    usr/lib/{audit,gconv}/*.so

```

And remove them where appropriate.

### Qt4

In addition to the previous general settings, pass `-developer-build` option to the `configure` script in the `PKGBUILD`. By default, `-developer-build` passes `-Werror` to the compiler, which may cause the compilation to fail. To avoid compilation errors, you may need pass `-no-warnings-are-errors`, too.

### Qt5

The [qt-debug](/index.php/Unofficial_user_repositories#qt-debug "Unofficial user repositories") repository contains pre-built Qt/PyQt packages with debug symbols. See also [upstream](http://doc.qt.io/qt-5/debug.html) instructions.

### Aplicativos CMAKE (KDE)

[KDE](/index.php/KDE "KDE") and related programs typically use [cmake](https://www.archlinux.org/packages/?name=cmake). To enable debug information and disable optimisations, change `-DCMAKE_BUILD_TYPE` to `Debug`. To enable debug information while keeping optimisations enabled, change `-DCMAKE_BUILD_TYPE` to `RelWithDebInfo`.

## Compilando e instalando o pacote

Build the package from source using `makepkg` while in the PKGBUILD's directory. This could take some time:

```
$ makepkg

```

Then install the built package:

```
# pacman -U glibc-2.5-8-i686.pkg.tar.gz

```

## Obtendo o rastro

The actual backtrace (or stack trace) can now be obtained via e.g. [gdb](https://www.archlinux.org/packages/?name=gdb), the GNU Debugger. Run it either via:

```
# gdb /path/to/file

```

or:

```
# gdb
(gdb) exec /path/to/file

```

The path is optional, if already set in the `$PATH` variable.

Then, within `gdb`, type `run` followed by any arguments you wish the program to start with, e.g.:

```
(gdb) run --no-daemon --verbose

```

to start execution of the file. Do whatever necessary to evoke the bug. For the actual log, type the lines:

```
(gdb) set logging file trace.log
(gdb) set logging on

```

and then:

```
(gdb) thread apply all bt full

```

to output the trace to `trace.log` into the directory `gdb` was started in. To exit, enter:

```
(gdb) set logging off
(gdb) quit

```

**Tip:** To debug an application written in python:
```
# gdb /usr/bin/python
(gdb) run <python application>

```

You can also debug an already running application, e.g.:

```
 # gdb --pid=$(pidof firefox)
 (gdb) continue

```

## Conclusão

Use the complete stack trace to inform developers of a bug you have discovered before. This will be highly appreciated by them and will help to improve your favorite program.

## Veja também

*   [Gentoo Wiki - Backtraces with Gentoo](https://wiki.gentoo.org/wiki/Project:Quality_Assurance/Backtraces)
*   [Fedora - StackTraces](http://fedoraproject.org/wiki/StackTraces)
*   [GNOME - Getting Stack Traces](https://wiki.gnome.org/Community/GettingInTouch/Bugzilla/GettingTraces/Details#obtain-a-stacktrace)
*   [gdb mini intro](http://linux.bytesex.org/gdb.html)