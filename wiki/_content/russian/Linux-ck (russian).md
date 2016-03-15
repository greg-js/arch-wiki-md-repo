[Linux-ck](https://aur.archlinux.org/packages/Linux-ck/) — это пакет, доступный в [AUR](/index.php/AUR "AUR") и в [unofficial linux-ck repo](#2._Use_Pre-Compiled_Packages), который позволяет пользователям запускать ядро с набором патчей Кона Коливаса, включая "Brain Fuck Scheduler" (BFS).

## Contents

*   [1 Основная информация о пакете](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.B0.D1.8F_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F_.D0.BE_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B5)
*   [2 Варианты установки](#.D0.92.D0.B0.D1.80.D0.B8.D0.B0.D0.BD.D1.82.D1.8B_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [2.1 Компиляция из исходников](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F_.D0.B8.D0.B7_.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D0.BD.D0.B8.D0.BA.D0.BE.D0.B2)
    *   [2.2 Использование готовых пакетов](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
        *   [2.2.1 Виды пакетов](#.D0.92.D0.B8.D0.B4.D1.8B_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
        *   [2.2.2 Добавление репозитория в /etc/pacman.conf](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D1.8F_.D0.B2_.2Fetc.2Fpacman.conf)
        *   [2.2.3 Примеры установки](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
        *   [2.2.4 Предлагаемые пакеты](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BB.D0.B0.D0.B3.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
        *   [2.2.5 Как включить BFQ I/O Scheduler](#.D0.9A.D0.B0.D0.BA_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_BFQ_I.2FO_Scheduler)
            *   [2.2.5.1 Глобально](#.D0.93.D0.BB.D0.BE.D0.B1.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE)
            *   [2.2.5.2 Выборочно](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80.D0.BE.D1.87.D0.BD.D0.BE)
*   [3 Запуск VirtualBox](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_VirtualBox)
*   [4 Немного о BFS](#.D0.9D.D0.B5.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BE_BFS)
*   [5 Дополнительная информация](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F)
*   [6 Linux-ck Package Changelog](#Linux-ck_Package_Changelog)

## Основная информация о пакете

Linux-ck обычно следует за свежими версиями ядра.

Есть **два** изменения в конфигурационных файлах:

1.  Опции, которые включают/отключают сk patchset.
2.  Опции, которые необходимы для компиляции BFQ.

**Все остальные опции оставлены по умолчанию, как в основном ядре ARCH**

Смотрите также [ЧаВо по настройке BFS](http://ck.kolivas.org/patches/bfs/bfs-configuration-faq.txt).

## Варианты установки

**Примечание:** Если вы используете также другие ядра, вы должны самостоятельно отредактировать `/boot/grub/menu.lst` (если используете [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)")) или обновить `/boot/grub/grub.cfg` с помощью `grub-mkconfig -o /boot/grub/grub.cfg` (если используете [GRUB2](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)"))

**Важно:** Пользователи [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)"), прежде чем устанавливать пакет, должны удостовериться, что используют версию выше 1:1.99-5

Пакет можно установить одним из двух способов.

### Компиляция из исходников

Пакет [linux-ck](https://aur.archlinux.org/packages/linux-ck/) устанавливается так же, как и любой другой пакет. Пользователи могут настраивать пакет с помощью `PKBUILD`:

*   Использование nconfig для настройки
*   Компиляция минимального набора модулей с помощью *localmodconfig*
*   Использование стандартного *.config*
*   Включение BFQ I/O scheduler по умолчанию

Более подробная информация содержится в самом `PKBUILD` в виде комментариев.

**Примечание:** В AUR также находятся пакеты некоторых специфических модулей, таких как [nvidia-ck](https://aur.archlinux.org/packages/nvidia-ck/), [lirc-ck](https://aur.archlinux.org/packages/lirc-ck/) и [broadcom-wl-ck](https://aur.archlinux.org/packages/broadcom-wl-ck/)

### Использование готовых пакетов

Если вы не хотите компилировать пакет самостоятельно, можете установить его из неофициального репозитория пользователя [graysky](/index.php/User:Graysky "User:Graysky").

**Примечание:** В репозитории содержатся пакеты, в которых BFQ включен как модуль. О том, как включить его, читайте ниже

Для подписи пакета используется [публичный ключ Graysky](http://pgp.mit.edu:11371/pks/lookup?op=get&search=0x6D605D846176ED4B). *pacman* четвертой версии автоматически получит ключ, но если этого не произошло, вы можете сделать это вручную с помощью ссылки.

#### Виды пакетов

Репозиторий содержит generic пакет а также пакеты для конкретных CPU.

*GENERIC*

*   **ck-generic** ==> Подходит для любых процессоров как и основное ядро ARCH. будет работать как на intel так и на amd.

*CPU SPECIFIC AND OPTIMIZED*

*   **ck-atom** ==> Ядро оптимизированное для работы на Intel Atom.
*   **ck-corex** ==> Ядро оптимизированное для процессоров семейства Intel Core 2 (Core 2/Newer Xeon/Mobile Celeron based on Core2). А также Core i3/i5/i7 (Gulftown, Bloomfield, Lynnfield, Clarksfield, Arrendale, and Sandy/Ivybridge CPUs)

*   **ck-kx** ==> AMD K7 (Athlon/Athlon XP)/K8 (Athlon 64, Athlon 64 X2, 23xx Quad-Core Barcelona, Sempron, Sempron 64)/K10-family (Athlon X2 7x50, Phenom X3/X4, Phenom II, Athlon II X2/X3/X4, Sempron 64 (Socket AM3 only), 61xx Eight-Core Magny-Cours).
*   **ck-p4** ==> Ядро для процессоров Intel Pentium 4 (P4/P4-based Celeron/Pentium-4 M/Older Xeon).
*   **ck-pentm** ==> Ядро для Intel Pentium-M (Pentium-M notebook chips/not Pentium-4 M).

#### Добавление репозитория в `/etc/pacman.conf`

1) Добавьте в `/etc/pacman.conf` следующие строки:

```
[repo-ck]
Server = [http://repo-ck.com/$arch](http://repo-ck.com/$arch)

```

2) Обновитесь с помощью *pacman -Syy*

Чтобы увидеть содержимое репозитория используйте:

```
$ pacman -Sl repo-ck

```

#### Примеры установки

В репозитории есть 6 групп пакетов **ck-generic, ck-atom, ck-corex, ck-kx, ck-p4,** и **ck-pentm**. Для установки одной из них выполните:

```
# pacman -S ck-generic
:: There are 4 members in group ck-generic:
:: Repository repo-ck
   1) broadcom-wl-ck  2) linux-ck  3) linux-ck-headers  4) nvidia-ck

Enter a selection (default=all):
```

Также вы можете установить пакеты напрямую:

```
# pacman -S linux-ck linux-ck-headers

```

#### Предлагаемые пакеты

| **linux-ck and headers** | **Группа** | **x86_64** | **i686** | **Семейство процессоров** |
| [linux-ck](https://aur.archlinux.org/packages.php?ID=50911) | ck-generic | Yes | Yes | Compiled with generic optimizations suitable for *any* compatible CPU just like the official ARCH linux package. |
| linux-ck-atom | ck-atom | Yes | Yes | Intel Atom platform specific optimizations. |
| linux-ck-corex | ck-corex | Yes | Yes | Intel Core 2-family specific optimizations including Dual and Quads (Core 2/Newer Xeon/Mobile Celeron based on Core2) as well as Intel Core i3/i5/i7. |
| linux-ck-kx | ck-kx | Yes | Yes | AMD K7 (Athlon/Athlon XP), K8 (Athlon 64, Athlon 64 X2, 23xx Quad-Core Barcelona, Sempron, Sempron 64), and K10-family (Athlon X2 7x50, Phenom X3/X4, Phenom II, Athlon II X2/X3/X4, Sempron 64 (Socket AM3 only), 61xx Eight-Core Magny-Cours) specific optimizations. |
| linux-ck-p4 | ck-p4 | No | Yes | Intel Pentium-4 specific optimizations (P4/P4-based Celeron/Pentium-4 M/Older Xeon). |
| linux-ck-pentm | ck-pentm | N/A | Yes | Intel Pentium-M specific optimizations (Pentium-M notebook chips/not Pentium-4 M). |
| **Nvidia-ck Module** | **Group** | **x86_64** | **i686** | **Description** |
| [nvidia-ck](https://aur.archlinux.org/packages.php?ID=33305) | ck-generic | Yes | Yes | The matching nVidia kernel module based on 290.xx series of Official nVidia drivers for linux-ck. |
| nvidia-ck-atom | ck-atom | Yes | Yes |
| nvidia-ck-corex | ck-corex | Yes | Yes |
| nvidia-ck-kx | ck-kx | Yes | Yes |
| nvidia-ck-p4 | ck-p4 | No | Yes |
| nvidia-ck-pentm | ck-pentm | N/A | Yes |
| **Broadcom-wl-ck Module** | **Group** | **x86_64** | **i686** | **Description** |
| [broadcom-wl-ck](https://aur.archlinux.org/packages.php?ID=48740) | ck-generic | Yes | Yes | The matching Broadcom-wl-ck kernel module for linux-ck. |
| broadcom-wl-ck-atom | ck-atom | Yes | Yes |
| broadcom-wl-ck-corex | ck-corex | Yes | Yes |
| broadcom-wl-ck-kx | ck-kx | Yes | Yes |
| broadcom-wl-ck-p4 | ck-p4 | No | Yes |
| broadcom-wl-ck-pentm | ck-pentm | N/A | Yes |

*N/A = Недоступные.*

#### Как включить BFQ I/O Scheduler

##### Глобально

Добавьте "elevator=bfq" в строку параметров ядра в `/boot/grub/menu.lst` если используете grub или в `/etc/default/grub` под строкой **GRUB_CMDLINE_LINUX_DEFAULT="quiet"** с последующей генерацией `/boot/grub/grub.cfg` с помощью "grub-mkconfig -o /boot/grub/grub.cfg".

##### Выборочно

Можно указать ядру использовать BFQ для конкретнго устройства. Например чтобы включить его для `/dev/sda` напишите:

```
# echo bfq > /sys/block/sda/queue/scheduler

```

Чтобы убедиться что он включен введите:

```
# cat /sys/block/sda/queue/scheduler
noop deadline cfq [bfq] 

```

Учтите что при использовании этого способы параметры не сохранятся при перезагрузке. Чтобы вносить изменения автоматически при загрузке ,поместитье строку "echo" в `/etc/rc.local`

**Примечание:** Пользователи которые устанавливали пакет из AUR могут включить BFQ глобально с помощью PKBUILD

## Запуск VirtualBox

Virtualbox отлично работает с ядром linux-ck, для того чтобы сгенерировать модули установите virtualbox-source

```
# pacman -S virtualbox virtualbox-source

```

После этого выполните команду:

```
# /usr/bin/vboxbuild

```

## Немного о BFS

BFS — это аббревиатура от Brain Fuck Scheduler. Он представляет собой планировщик задач разработанный Con Kolivas. BFS орентирован на обеспечение большей производительности и отзывчивости системы, прежде всего на десктопах. Особенно эффективен на многоядерных процессорах.

## Дополнительная информация

*   [Con Kolivas' White Paper on the BFS](http://ck.kolivas.org/patches/bfs/sched-BFS.txt)
*   [Con Kolivas' BFS FAQ](http://ck.kolivas.org/patches/bfs/bfs-faq.txt)
*   [Wikipedia's BFS Article](https://en.wikipedia.org/wiki/Brain_Fuck_Scheduler "wikipedia:Brain Fuck Scheduler")
*   [Con Kolivas' Blog](http://ck-hack.blogspot.com/)

## [Linux-ck Package Changelog](/index.php/Linux-ck/Changelog "Linux-ck/Changelog")