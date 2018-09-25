Ниже приведен список часто задаваемых вопросов об Arch Linux 64.

## Contents

*   [1 Как узнать, является ли мой процессор x86_64 совместимым?](#.D0.9A.D0.B0.D0.BA_.D1.83.D0.B7.D0.BD.D0.B0.D1.82.D1.8C.2C_.D1.8F.D0.B2.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.D0.BB.D0.B8_.D0.BC.D0.BE.D0.B9_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.BE.D1.80_x86_64_.D1.81.D0.BE.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.B8.D0.BC.D1.8B.D0.BC.3F)
    *   [1.1 Пользователи Linux](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B8_Linux)
    *   [1.2 Пользователи Windows](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B8_Windows)
*   [2 Какую версию Arch мне использовать - 32-битную или 64-битную?](#.D0.9A.D0.B0.D0.BA.D1.83.D1.8E_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D1.8E_Arch_.D0.BC.D0.BD.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_-_32-.D0.B1.D0.B8.D1.82.D0.BD.D1.83.D1.8E_.D0.B8.D0.BB.D0.B8_64-.D0.B1.D0.B8.D1.82.D0.BD.D1.83.D1.8E.3F)
*   [3 Как установить Arch64?](#.D0.9A.D0.B0.D0.BA_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C_Arch64.3F)
*   [4 Насколько полноценным является порт?](#.D0.9D.D0.B0.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BF.D0.BE.D0.BB.D0.BD.D0.BE.D1.86.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D1.8F.D0.B2.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D1.80.D1.82.3F)
*   [5 Будут ли доступны все пакеты из моего окружения Arch32?](#.D0.91.D1.83.D0.B4.D1.83.D1.82_.D0.BB.D0.B8_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.BD.D1.8B_.D0.B2.D1.81.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B_.D0.B8.D0.B7_.D0.BC.D0.BE.D0.B5.D0.B3.D0.BE_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_Arch32.3F)
*   [6 Почему 64-бита?](#.D0.9F.D0.BE.D1.87.D0.B5.D0.BC.D1.83_64-.D0.B1.D0.B8.D1.82.D0.B0.3F)
*   [7 Какие репозитории я должен использовать в pacman?](#.D0.9A.D0.B0.D0.BA.D0.B8.D0.B5_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B8_.D1.8F_.D0.B4.D0.BE.D0.BB.D0.B6.D0.B5.D0.BD_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_.D0.B2_pacman.3F)
*   [8 Что я потеряю в Arch64?](#.D0.A7.D1.82.D0.BE_.D1.8F_.D0.BF.D0.BE.D1.82.D0.B5.D1.80.D1.8F.D1.8E_.D0.B2_Arch64.3F)
*   [9 Могу я запускать 32-битные приложения внутри Arch64?](#.D0.9C.D0.BE.D0.B3.D1.83_.D1.8F_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D1.82.D1.8C_32-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2.D0.BD.D1.83.D1.82.D1.80.D0.B8_Arch64.3F)
*   [10 Могу ли я собирать 32-битные пакеты для i686 используя Arch64?](#.D0.9C.D0.BE.D0.B3.D1.83_.D0.BB.D0.B8_.D1.8F_.D1.81.D0.BE.D0.B1.D0.B8.D1.80.D0.B0.D1.82.D1.8C_32-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B_.D0.B4.D0.BB.D1.8F_i686_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_Arch64.3F)
    *   [10.1 Репозиторий Multilib](#.D0.A0.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B9_Multilib)
    *   [10.2 Chroot](#Chroot)
*   [11 Могу я обновить/переключить мою систему с i686 на x86_64 без переустановки?](#.D0.9C.D0.BE.D0.B3.D1.83_.D1.8F_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C.2F.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D0.BC.D0.BE.D1.8E_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83_.D1.81_i686_.D0.BD.D0.B0_x86_64_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.B5.D1.80.D0.B5.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8.3F)

## Как узнать, является ли мой процессор x86_64 совместимым?

### Пользователи Linux

Запустите в терминале:

```
$ less /proc/cpuinfo

```

и просмотрите значение `flags` на наличие флага `lm`. Если он присутствует - ваш процессор является x86_64 совместимым.

Или попробуйте это:

```
$ grep -q "^flags.*\blm\b" /proc/cpuinfo && echo "x86_64" || echo "not x86_64"

```

### Пользователи Windows

Используя бесплатную утилиту [CPU-Z](http://www.cpuid.com/cpuz.php) вы сможете определить, является ли ваш процессор 64-бит совместимым. Процессоры с набором команд "AMD64" (для AMD) или "EM64T" (для Intel) должны быть совместимы с x86_64-релизами и бинарными пакетами.

## Какую версию Arch мне использовать - 32-битную или 64-битную?

Если ваш процессор поддерживает [x86_64](https://en.wikipedia.org/wiki/ru:X86-64 "wikipedia:ru:X86-64"), вам следует использовать Arch64.

## Как установить Arch64?

Просто используйте [официальный образ установочного CD](https://www.archlinux.org/download/).

## Насколько полноценным является порт?

Порт уже готов для повседневного использования в качестве рабочего стола или сервера.

## Будут ли доступны все пакеты из моего окружения Arch32?

Репозитории портированы и всё должно работать так, как ожидалось.

Изредка, для старых пакетов в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") указана только одна архитектура: `'i686'`, но обычно они могут работать и в 64-разрядной системе. Просто попробуйте добавить `'x86_64'`.

## Почему 64-бита?

В большинстве случаев это более быстрая работа системы, кроме того это немного безопаснее, в связи с [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/ru:Address_Space_Layout_Randomization "wikipedia:ru:Address Space Layout Randomization"), в комбинации с [Позиционно-независимым кодом (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") и [NX Bit](https://en.wikipedia.org/wiki/ru:NX_bit "wikipedia:ru:NX bit"), которые недоступны в стоковом i686 ядре за из-за отключенного [PAE](https://en.wikipedia.org/wiki/ru:PAE "wikipedia:ru:PAE"). Если ваш компьютер оснащён 4+ Гигабайтами оперативной памяти, вам следует использовать 64-битную архитектуру, так как 32-битная ОС не поддерживает такой объём.

Программисты также склонны меньше уделять внимания "устаревшей" 32-битной архитектуре, так как "новые" процессоры обычно поддерживают 64-битные расширения.

Существует намного больше доводов за использование 64-битной архитектуры, которые можно здесь перечислить. Но в наши дни столько разных вещей, которые 64-битная архитектура "делает" лучше, что составление этого списка просто не имеет смысла.

Для более подробной информации смотрите [различия пакетов](https://www.archlinux.org/packages/differences/). Там вы найдёте различия 32-/64-битных версий пакетов.

## Какие репозитории я должен использовать в pacman?

Для порта поддерживаются все репозитории.

## Что я потеряю в Arch64?

Ничего. Практически все приложения уже поддерживают x64.

Самой большой проблемой являются программы с закрытым исходным кодом и программы, содержащие x86-специфичный ассемблерный код (например, эмуляторы).

Эти приложения в прошлом имели проблемы, но сейчас доступны в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") и работают корректно.

*   Acrobat Reader не доступен в x64, но вы можете запустить 32-битную версию в режиме совместимости. Также имеется достаточно свободных альтернатив для чтения pdf-файлов.

Всё остальное должно работать. Если вам не хватает какого-то пакета из Arch32 в нашем порте и вы знаете что он собирается под x86_64 (например вы нашли его в другом 64-битном дистрибутиве, без использования lib32), просто свяжитесь с разработчиками.

## Могу я запускать 32-битные приложения внутри Arch64?

Да!

*   Вы можете установить `lib32-*` библиотеки из репозитория [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)").

Репозиторий содержит [Wine](/index.php/Wine_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wine (Русский)"), [Skype](/index.php/Skype_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Skype (Русский)"), Flashplugin, [Steam](/index.php/Steam_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Steam (Русский)") и др.

*   Или вы можете создать chroot-окружение с 32-битной системой (смотри [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")):

## Могу ли я собирать 32-битные пакеты для i686 используя Arch64?

Да. Вы можете использовать

*   версии библиотек из репозитория [multilib] или
*   chroot-окружение i686.

### Репозиторий [Multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)")

Чтобы использовать репозиторий [multilib] измените ваш `/etc/pacman.conf` и раскомментируйте строки:

```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

обновите вашу систему `pacman -Syu` и установите пакет [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib).

**Note:**

*   Если в системе установлена группа пакетов `base-devel`, вам необходимо заменить версии из репозитория [extra] на версии из репозитория [mutlilib], как показано ниже.
*   [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) способен собрать 32- и 64-разрядный код. Вы можете спокойно устанавливать `multilib-devel` на замену пакетов, как показано ниже, но вам все еще необходима группа `base-devel` для других пакетов. Смотри https://bbs.archlinux.org/viewtopic.php?id=102828 для подробной информации.

 `# pacman -S gcc-multilib` 
```
resolving dependencies...
warning: dependency cycle detected:
warning: lib32-gcc-libs will be installed before its gcc-libs-multilib dependency
looking for inter-conflicts...
:: gcc-libs-multilib and gcc-libs are in conflict. Remove gcc-libs? [y/N] y
:: binutils-multilib and binutils are in conflict. Remove binutils? [y/N] y
:: gcc-multilib and gcc are in conflict. Remove gcc? [y/N] y
:: libtool-multilib and libtool are in conflict. Remove libtool? [y/N] y

Remove (4): gcc-libs-4.6.1-1  binutils-2.21.1-1  gcc-4.6.1-1  libtool-2.4-4

Total Removed Size:   87.65 MB

Targets (7): lib32-glibc-2.14-4  lib32-gcc-libs-4.6.1-1  gcc-libs-multilib-4.6.1-1  binutils-multilib-2.21.1-1
             gcc-multilib-4.6.1-1  lib32-libtool-2.4-2  libtool-multilib-2.4-2

Total Download Size:    25.04 MB
Total Installed Size:   108.27 MB

Proceed with installation? [Y/n]
```

Сборка пакетов на x86_64-архитектуре для i686 проста: необходимо добавить следующие строки в файл альтернативной конфигурации (например `~/.makepkg.i686.conf`)

```
CARCH="i686"
CHOST="i686-pc-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"

```

и запустить makepkg командой

```
$ linux32 makepkg -src --config ~/.makepkg.i686.conf

```

### Chroot

Смотрите [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")

## Могу я обновить/переключить мою систему с i686 на x86_64 без переустановки?

Нет. Строго говоря, миграция предпологает что все или почти все пакеты должны быть переустановлены для новой архитектуры. Тем не менее возможно переместить вашу систему без переустановки на новую архитектуру. Об этом повествует [топик](https://bbs.archlinux.org/viewtopic.php?id=64485), в котором описаны базовые шаги, позволяющие успешно обновить 32-битную систему до 64-битной без потери данных. Имейте в виду, что для этого нужен носитель большого объема.

Впрочем, вы также можете загрузиться с установочного диска Arch64, примонтировать разделы, сделать резервные копии всего, что не является 32-битными исполняемыми файлами (например `/home` и `/etc`) и выполнить установку.

Возможно, вам также будет интересно почитать [Migrating Between Architectures Without Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling").