**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Важная заметка](#Важная_заметка)
*   [2 Совместимость версий](#Совместимость_версий)
*   [3 Сборка кросс-компилятора](#Сборка_кросс-компилятора)
*   [4 Наименование пакета](#Наименование_пакета)
*   [5 Размещение файлов](#Размещение_файлов)
*   [6 пример](#пример)
*   [7 Как и почему](#Как_и_почему)
    *   [7.1 Почему бы не устанавливать в /opt](#Почему_бы_не_устанавливать_в_/opt)
    *   [7.2 What is that *out-of-path executables* thing?](#What_is_that_out-of-path_executables_thing?)
*   [8 Поиск проблемы](#Поиск_проблемы)
    *   [8.1 Что делать, если компиляция не удалась без четкого сообщения?](#Что_делать,_если_компиляция_не_удалась_без_четкого_сообщения?)
    *   [8.2 Что означает эта ошибка [error message]?](#Что_означает_эта_ошибка_[error_message]?)
    *   [8.3 Почему файлы устанавливаются в неправильных местах?](#Почему_файлы_устанавливаются_в_неправильных_местах?)
*   [9 Смотрите также](#Смотрите_также)

**Совет:** В качестве альтернативы для создания кросс-компиляторных пакетов вы можете использовать [crosstool-ng](http://crosstool-ng.org/) и создайте свой собственный набор инструментов полностью автоматизированным способом. crosstool-ng можно найти на [crosstool-ng](https://aur.archlinux.org/packages/crosstool-ng/).

## Важная заметка

На этой странице описан новый принцип работы, основанный на следующих пакетах:

*   [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/) и другие пакеты из `mingw-w64-*` серии
*   [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc) и другие пакеты из `arm-none-eabi-*` серии
*   [arm-wince-cegcc-gcc](https://aur.archlinux.org/packages/arm-wince-cegcc-gcc/) и другие пакеты из `arm-wince-cegcc-*` серии

## Совместимость версий

**Warning:** Использование несовместимых версий пакетов для компиляции цепочек инструментов приводит к неизбежным сбоям. По умолчанию считают **все** версии несовместимыми.

Следующая стратегия позволяют выбирать совместимые версии gcc, binutils, ядра и библиотеки C:

*   Основные правила:
    *   существует корреляция между выпусками gcc и binutils, используйте одновременно выпущенные версии;
    *   лучше использовать последние заголовки ядра для компиляции libc, но использовать переключатель `--enable-kernel` (специфично для glibc, другие библиотеки C могут использовать другие соглашения) для обеспечения работы на старых ядрах;
*   [Официальные репозитории](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8 "Официальные репозитории"): вам, возможно, придется использовать дополнительные исправления и хаки, для версий используемых в Arch Linux (или специфичные ответвления для архитектуры), скорее всего, созданные для совместной работы;
*   Документация по программному обеспечению: все программное обеспечение GNU `README` и `NEWS` файлы, документирующие такие вещи, как минимально необходимые зависимости;
*   Другие дистрибутивы: они тоже делают кросс-компиляцию
*   [http://clfs.org](http://clfs.org) описывает шаги, необходимые для построения кросс-компилятора, и упоминает несколько актуальных версий зависимостей.

## Сборка кросс-компилятора

Общий подход к созданию кросс-компилятора:

1.  binutils: Создание cross-binutils, которая связывает и обрабатывает для целевой архитектуры
2.  headers: Установите набор библиотеки C и заголовками ядра для целевой архитектуры
    1.  используйте [linux-api-headers](https://www.archlinux.org/packages/?name=linux-api-headers) в качестве ссылки и передайте `ARCH=*target-architecture*` для **make**
    2.  создать пакет заголовков libc (описан процесс для Glibc [here](http://sources.redhat.com/ml/crossgcc/2003-06/msg00170.html))
3.  gcc-stage-1: Создайте базовый (этап 1) gcc кросс-компилятор. Будет использоваться для компиляции библиотеки C. Он не сможет построить почти еще ни чего (потому что он не может связываться с библиотекой C, которой у него нет).
4.  libc: Создайте библиотеку C кросс-компилятора (используя кросс-компилятор этапа 1).
5.  gcc-stage-2: Сборка полного кросс-компилятора C (этап 2)

Источник заголовков и libc будет отличаться для разных платформ.

**Совет:** Точная процедура может сильно варьировать, в зависимости от ваших потребностей. Например, если вы хотите создать «клон» системы Arch Linux с теми же версиями ядра и glibc, вы можете пропустить сборку заголовков и передать `--with-build-sysroot=/` в `configure`.

## Наименование пакета

В имени пакета **не** должно быть префикса со словом `cross-` (было предложено ранее, но не было принято в официальных пакетах, возможно, из-за дополнительной длины имен), и должно состоять из имени пакета с префиксом [GNU triplet](https://wiki.debian.org/Multiarch/Tuples "debian:Multiarch/Tuples") без поля поставщика или со значением "unknown" в поле поставщика; пример: `arm-linux-gnueabihf-gcc`. Если существует более короткое соглашение об именах (например, `mips-gcc`), его можно использовать, но это не рекомендуется.

## Размещение файлов

Последние версии gcc и binutils используют не конфликтующие пути для sysroot и библиотек. Исполняемые файлы должны быть помещены в `/usr/bin/`, чтобы предотвратить возникновение конфликтов, перед всеми ними необходимо указать префикс имени архитектуры.

Правило, `./configure` будет иметь по крайней мере следующие параметры:

```
_target=*your_target*
_sysroot=/usr/lib/${_target}
...
./configure \
    --prefix=${_sysroot} \
    --sysroot=${_sysroot} \
    --bindir=/usr/bin
```

где `*your_target*` может быть, например, "i686-pc-mingw32".

## пример

Это PKGBUILD для binutils для MinGW. Вещи, на которые стоит обратить внимание:

*   указание корневого каталога кросс-окружения
*   использование переменных `${_pkgname}` , `${_target}` и `${_sysroot}` , чтобы сделать код более читабельным
*   удаление дублированных / конфликтующих файлов

```
# Maintainer: Allan McRae <allan@archlinux.org>

# cross toolchain build order: binutils, headers, gcc (pass 1), w32api, mingwrt, gcc (pass 2)

_target=i686-pc-mingw32
_sysroot=/usr/lib/${_target}

pkgname=${_target}-binutils
_pkgname=binutils
pkgver=2.19.1
pkgrel=1
pkgdesc="MinGW Windows binutils"
arch=('i686' 'x86_64')
url="http://www.gnu.org/software/binutils/"
license=('GPL')
depends=('glibc>=2.10.1' 'zlib')
options=('!libtool' '!distcc' '!ccache')
source=(http://ftp.gnu.org/gnu/${_pkgname}/${_pkgname}-${pkgver}.tar.bz2)
md5sums=('09a8c5821a2dfdbb20665bc0bd680791')

build() {
  cd ${srcdir}/${_pkgname}-${pkgver}
  mkdir binutils-build && cd binutils-build

  ../configure --prefix=${_sysroot} --bindir=/usr/bin \
    --with-sysroot=${_sysroot} \
    --build=$CHOST --host=$CHOST --target=${_target} \
    --with-gcc --with-gnu-as --with-gnu-ld \
    --enable-shared --without-included-gettext \
    --disable-nls --disable-debug --disable-win32-registry
  make
  make DESTDIR=${pkgdir}/ install

  # clean-up cross compiler root
  rm -r ${pkgdir}/${_sysroot}/{info,man}
}

```

**Примечание:** Во время построения кросс-цепочки всегда выполняйте команды `configure` и **make** из определенного каталога (так называемая компиляция вне дерева) и удаляйте весь каталог `src` после малейшего изменения в [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

## Как и почему

### Почему бы не устанавливать в `/opt`

Две причины:

1.  Во-первых, согласно Стандарту Файловой Иерархии, эти файлы просто принадлежат `/usr`. Период.
2.  Во-вторых, установка в `/opt` является последней мерой, когда другой опции нет.

### What is that *out-of-path executables* thing?

This weird thing allows easier cross-compiling. Sometimes, project Makefiles do not use `CC` & co. variables and instead use **gcc** directly. If you just want to try to cross-compile such project, editing the Makefile could be a very lengthy operation. However, changing the `$PATH` to use "our" executables first is a very quick solution. You would then run `PATH=/usr/*arch*/bin/:$PATH make` instead of `make`.

## Поиск проблемы

### Что делать, если компиляция не удалась без четкого сообщения?

Если ошибка возникла во время выполнения `configure`, прочитайте `$srcdir/*pkgname*-build/config.log`. Для ошибки, произошедшей во время компиляции, прокрутите консоль, войдите в систему или найдите слово "error".

### Что означает эта ошибка [error message]?

Скорее всего, вы допустили некоторые неочевидные ошибки:

*   Слишком много или слишком мало флагов конфигурации. Попробуйте использовать уже проверенный набор флагов.
*   Зависимости повреждены. Например, неуместные или отсутствующие файлы binutils могут привести к загадочной ошибке во время настройки gcc.
*   Вы не добавили `export CFLAGS=""` в свою функцию `build()` (см. [bug 25672](http://gcc.gnu.org/bugzilla/show_bug.cgi?id=25672) в GCC Bugzilla).
*   Для некоторых комбинаций `--prefix`/`--with-sysroot` может потребоваться, чтобы каталоги были доступны для записи (что не очевидно из руководства clfs).
*   В sysroot нет ни заголовков ядра или libc.
*   Если google не помогает, отмените текущую конфигурацию и попробуйте более стабильную/проверенную.

### Почему файлы устанавливаются в неправильных местах?

Различные методы запуска `make install` приводят к разным результатам. Например, некоторые цели make могут не обеспечивать поддержку `DESTDIR`, а вместо этого требуют использования `install_root`. То же самое для `tooldir`, `prefix` и других подобных аргументов. Иногда предоставление параметров в качестве аргументов вместо переменных среды, например

```
./configure CC=arm-elf-gcc

```

вместо

```
CC=arm-elf-gcc ./configure

```

и наоборот, может привести к различным результатам (часто вызванным рекурсивным самовывозом configure/make).

## Смотрите также

*   [http://wiki.osdev.org/GCC_Cross-Compiler](http://wiki.osdev.org/GCC_Cross-Compiler)