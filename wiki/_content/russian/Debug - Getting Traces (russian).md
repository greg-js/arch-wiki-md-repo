Ссылки по теме

*   [Устранение часто встречающихся неполадок](/index.php/%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%87%D0%B0%D1%81%D1%82%D0%BE_%D0%B2%D1%81%D1%82%D1%80%D0%B5%D1%87%D0%B0%D1%8E%D1%89%D0%B8%D1%85%D1%81%D1%8F_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA "Устранение часто встречающихся неполадок")
*   [Указания по созданию отчета об ошибке](/index.php/%D0%A3%D0%BA%D0%B0%D0%B7%D0%B0%D0%BD%D0%B8%D1%8F_%D0%BF%D0%BE_%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D1%8E_%D0%BE%D1%82%D1%87%D0%B5%D1%82%D0%B0_%D0%BE%D0%B1_%D0%BE%D1%88%D0%B8%D0%B1%D0%BA%D0%B5 "Указания по созданию отчета об ошибке")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")

Эта статья описывает создание отладочного пакета и получение с его помощью отладочной информации для отправки разработчикам в отчётах об ошибках.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Package names](#Package_names)
*   [2 PKGBUILD](#PKGBUILD)
*   [3 Compilation settings](#Compilation_settings)
    *   [3.1 Qt](#Qt)
    *   [3.2 KDE applications](#KDE_applications)
*   [4 Building and installing the package](#Building_and_installing_the_package)
*   [5 Трассирование](#Трассирование)
*   [6 См. также](#См._также)

## Package names

Во время отладки, при получении backtrace (пример ниже):

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

строки вида `??` и `(no debugging symbols found)` показывают, что необходимая отладочная информация, такая, как названия функций, файлов, библиотек, отсутствует в отлаживаемом файле. Проверить, какому пакету принадлежит исполняемый файл или библиотека можно, например, с помощью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"):

```
# pacman -Qo /lib/libthread_db.so.1
/lib/libthread_db.so.1 is owned by *glibc* 2.5-8

```

Пакет [glibc](https://www.archlinux.org/packages/?name=glibc) версии 2.5-8\. Следует составить список пакетов, которые необходимо заменить для отладки.

## PKGBUILD

Чтобы собрать пакет из исходного кода нужно получить файл PKGBUILD. См. [ABS](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") для пакетов из [официальных репозиториев](/index.php/Official_repositories "Official repositories") и [AUR#Acquire build files](/index.php/AUR#Acquire_build_files "AUR") для пакетов из [AUR](/index.php/AUR "AUR").

## Compilation settings

pacman получает параметры компиляции с отладочной информацией из переменных `DEBUG_CFLAGS` и `DEBUG_CXXFLAGS`. Чтобы включить отладку, нужно включить опцию makepkg `debug` и выключить опцию `strip`.

Если нужно собрать всего один пакет с отладочной информацией, достаточно внести в его файл PKGBUILD

```
options=(debug !strip)

```

Если же нужно собирать много пакетов, или makepkg не будет использоваться без отладочной информации, то можно внести в файл `/etc/makepkg.conf`

```
OPTIONS+=(debug !strip)

```

Также, можно включить одновременно обе опции `debug` и `strip`, в таком случае отладочная информация бует удалена из пакета, и будет помещена в отдельный пакет `*foo*-debug`.

**Note:** Просто установить отдельный пакет с отладочной информацией недостаточно, поскольку отладчику придётся искать отладочные символы непосредственно в отлаживаемом файле. Нужно установить оба перекомпилированных пакета. Отладочные символы помещаются в `/usr/lib/debug`. Информацию об отладочных пакетах см. в [документации GDB](https://sourceware.org/gdb/onlinedocs/gdb/Separate-Debug-Files.html) .

Некоторые пакеты, такие как *glibc*, очищаются независимо. В таком случае, для сохранения информации нужно найти в PKGBUILD секцию наподобие:

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

и удалить, там, где это возможно.

### Qt

В дополнение к этому нужно добавить в `configure` файла `PKGBUILD` опцию `-developer-build`. По-умолчанию, `-developer-build` указывает компилятору опцию `-Werror`, что может привести к ошибке компиляци. Чтобы избежать этого, может понадобиться также добавить `-no-warnings-are-errors`.

**Note:**

При компилировании Qt при установленном [qtwebkit](https://aur.archlinux.org/packages/qtwebkit/) могут возникнуть ошибки. Может понадобиться временно удалить пакет qtwebkit. Чтобы система игнорировала зависимости, используйте команду

```
# pacman -Rdd qtwebkit

```

Не забудьте установить qtwebkit после компиляции Qt, иначе зависящие от него программы не будут работать!

### KDE applications

[KDE](/index.php/KDE "KDE") использует для сборки [cmake](https://www.archlinux.org/packages/?name=cmake). Замените `-DCMAKE_BUILD_TYPE` на `Debug`.

## Building and installing the package

Сборка пакета осуществляется из директории, содержащей PKGBUILD, командой `makepkg`. Это может занять некоторое время:

```
# makepkg

```

Установка собранного пакета:

```
# pacman -U имя-пакета.tar.gz

```

## Трассирование

Текущий backtrace (or stack trace) может быть получен, например, с помощью [gdb](https://www.archlinux.org/packages/?name=gdb), (GNU Debugger). Запуск осуществляется так:

```
# gdb /path/to/file

```

или:

```
# gdb
(gdb) exec /path/to/file

```

Если путь присутствует в `$PATH`, его можно не указывать.

В `gdb`, введите `run` и аргументы для передачи запускаемому файлу:

```
(gdb) run --no-daemon --verbose

```

После запуска выполните действия, приводящие к возникновению бага. Также можно включить логгирование происходящего командой:

```
(gdb) set logging file trace.log
(gdb) set logging on

```

Чтобы сохранить текущий backtrace в файл trace.log в текущей директории, введите:

```
(gdb) thread apply all bt full

```

Выход осуществляется так:

```
(gdb) set logging off
(gdb) quit

```

**Tip:** Отладка приложений на Python:
```
# gdb /usr/bin/python
(gdb) run <python application>

```

Также, можно отлаживать и уже запущенные приложения, зная их PID:

```
 # gdb --pid=$(pidof firefox)
 (gdb) continue

```

## См. также

*   [Gentoo Wiki - Backtraces with Gentoo](https://wiki.gentoo.org/wiki/Project:Quality_Assurance/Backtraces)
*   [Fedora - StackTraces](http://fedoraproject.org/wiki/StackTraces)
*   [GNOME - Getting Stack Traces](https://wiki.gnome.org/Community/GettingInTouch/Bugzilla/GettingTraces/Details#obtain-a-stacktrace)
*   [gdb mini intro](http://linux.bytesex.org/gdb.html)