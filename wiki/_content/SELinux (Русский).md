# SELinux (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**Информация в этой статье или разделе устарела**

**Причина:** rc.d references. Needs update, see [Systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). ([Обсудить](https://wiki.archlinux.org/index.php/Talk:SELinux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Security-Enhanced Linux (SELinux) это функция Linux, которая обеспечивает множество политик безопасности, включая U.S. Обязательные средства управления доступом (MAC, Mandatory Access Controls) стиля министерства обороны, с помощью Linux Security Modules (LSM) в ядре Linux. Это не дистрибутив Linux, а скорее ряд модификаций, которые могут быть применены к Unix-подобным операционным системам, таким как Linux и BSD. Её архитектура стремится оптимизировать объем программного обеспечения, обвиненного в осуществлении политики безопасности, которое является близко выровненное Trusted Computer System Evaluation Criteria (TCSEC, называемый Оранжевой книгой) требование для минимизации достоверной вычислительной базы (TCB) (применимый к классам B3 и A1 оценки), но довольно не связано с наименьшим количеством требования полномочия (B2, B3, A1), как часто требуется. Зародышевые понятия базовый SELinux могут быть прослежены до нескольких более ранних проектов американским Агентством национальной безопасности (NSA). [1]

Для выполнения SELinux под дистрибутивом Linux требуется: включить SELinux в ядро, инструменты SELinux Userspace и библиотеки, и SELinux Policies (главным образом на основе Reference Policy). Некоторые общие программы Linux должны также исправляться/компилироваться с функциями SELinux.

## Contents

*   [1 Обязательные требования](#.D0.9E.D0.B1.D1.8F.D0.B7.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.82.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [2 Установка необходимых пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [2.1 Описание пакета](#.D0.9E.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B0)
        *   [2.1.1 SELinux aware system utils](#SELinux_aware_system_utils)
        *   [2.1.2 Пространство пользователя SELinux](#.D0.9F.D1.80.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D1.81.D1.82.D0.B2.D0.BE_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_SELinux)
        *   [2.1.3 Политики SELinux](#.D0.9F.D0.BE.D0.BB.D0.B8.D1.82.D0.B8.D0.BA.D0.B8_SELinux)
        *   [2.1.4 Другие утилиты SELinux](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B_SELinux)
*   [3 Configuration](#Configuration)
    *   [3.1 Changing boot loader configuration](#Changing_boot_loader_configuration)
    *   [3.2 Mounting selinuxfs](#Mounting_selinuxfs)
    *   [3.3 Main SELinux configuration file](#Main_SELinux_configuration_file)
    *   [3.4 Set up PAM](#Set_up_PAM)
*   [4 Reference policy](#Reference_policy)
    *   [4.1 Installing a precompiled refpolicy](#Installing_a_precompiled_refpolicy)
    *   [4.2 Installing refpolicy from a source package](#Installing_refpolicy_from_a_source_package)
*   [5 Post-installation steps](#Post-installation_steps)
*   [6 Useful tools](#Useful_tools)
*   [7 References](#References)
*   [8 See also](#See_also)

## Обязательные требования

Поддерживаются только файловые системы ext2, ext3, ext4, JFS и XFS.

**Обратите внимание:** This is probably not needed anymore:

Пользователи XFS должны использовать 512 байтов inodes (значение по умолчанию 256). Использование SELinux расширяло атрибуты для того, чтобы сохранить метки безопасности в файлах. XFS хранит это в inode, и если inode слишком маленький, должен использоваться дополнительный блок, который тратит впустую много пространства и подвергается потерям производительности.

```
# mkfs.xfs -i size=512 /dev/sda1

```

## Установка необходимых пакетов

Должны быть установлены по крайней мере [linux-selinux](https://aur.archlinux.org/packages/linux-selinux/)<sup><small>AUR</small></sup>, [selinux-pam](https://aur.archlinux.org/packages/selinux-pam/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-pam)]</sup>, [selinux-usr-policycoreutils](https://aur.archlinux.org/packages/selinux-usr-policycoreutils/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-usr-policycoreutils)]</sup> и [selinux-refpolicy-src](https://aur.archlinux.org/packages/selinux-refpolicy-src/)<sup><small>AUR</small></sup>. Рекомендуется установить все пакеты, требуемые SELinux.

При замене пакетов [pam](https://www.archlinux.org/packages/?name=pam) и [coreutils](https://www.archlinux.org/packages/?name=coreutils) будьте особо внимательны, поскольку они жизненно важны для системы. Приготовьте Live CD или Live USB на случай, если придётся переустановить систему.

**Важно:** Установливая, например, [selinux-pam](https://aur.archlinux.org/packages/selinux-pam/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-pam)]</sup>, [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") сообщит о конфликте и предложит удалить [pam](https://www.archlinux.org/packages/?name=pam). Согласитесь, и [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") сам удалит и установит требуемые пакеты. При замене обращайте внимание на любые ошибки, если они будут

### Описание пакета

Все пакеты, принадлежащие к SELinux, находятся в группе _selinux_. В _selinux-userspace_ располагаются пакеты пользователтского пространства. В _selinux-policies_ - пакеты политик. Остальные пакеты находятся в _selinux-extras_.

#### SELinux aware system utils

[linux-selinux](https://aur.archlinux.org/packages/linux-selinux/)<sup><small>AUR</small></sup>

Активирует поддержку SELinux ядром. Компиляция модулей подобно Virtualbox

[selinux-coreutils](https://aur.archlinux.org/packages/selinux-coreutils/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-coreutils)]</sup>

Компиляция пакета [coreutils](/index.php/Core_utilities_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Core utilities (Русский)") с включенной поддержкой SELinux

[selinux-flex](https://aur.archlinux.org/packages/selinux-flex/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-flex)]</sup>

Версия _flex_, необходимая только для сборки checkpolicy. Текущий _flex_ имеет ошибку, вызывающую отказ в выполнении команды _checkmodule_

[selinux-pam](https://aur.archlinux.org/packages/selinux-pam/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-pam)]</sup>

Пакет PAM с `pam_selinux.so`

[selinux-systemd](https://aur.archlinux.org/packages/selinux-systemd/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-systemd)]</sup>

An SELinux aware version of [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). It replaces the [systemd](https://www.archlinux.org/packages/?name=systemd) package

[selinux-util-linux](https://aur.archlinux.org/packages/selinux-util-linux/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-util-linux)]</sup>

Версия [util-linux](https://www.archlinux.org/packages/?name=util-linux), скомпилированная с включенной поддержкой SELinux

[selinux-findutils](https://aur.archlinux.org/packages/selinux-findutils/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-findutils)]</sup>

Пропатченная версия [findutils](https://www.archlinux.org/packages/?name=findutils) с активированной поддержкой SELinux, необходимая для поиска файлов в указанном возможном контексте безопасности

[selinux-sudo](https://aur.archlinux.org/packages/selinux-sudo/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-sudo)]</sup>

Версия [sudo](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)") с активированной поддержкой SELinux для корректной устанавки контекста безопасности

[selinux-procps](https://aur.archlinux.org/packages/selinux-procps/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-procps)]</sup>

Исправления пакета procps на основе некоторых патчей Fedora

[selinux-psmisc](https://aur.archlinux.org/packages/selinux-psmisc/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-psmisc)]</sup>

Версия [psmisc](https://www.archlinux.org/packages/?name=psmisc) с активированной поддержкой SELinux. Добавляет опцию `-Z` к `killall`

[selinux-shadow](https://aur.archlinux.org/packages/selinux-shadow/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-shadow)]</sup>

Версия [shadow](https://www.archlinux.org/packages/?name=shadow) с активированной поддержкой SELinux. Содержит изменённый `/etc/pam.d/login` для корректной установки контекста безопасности после входа в систему

[selinux-cronie](https://aur.archlinux.org/packages/selinux-cronie/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-cronie)]</sup>

Vixie cron из дистрибутива Fedora с активированной поддержкой SELinux

[selinux-logrotate](https://aur.archlinux.org/packages/selinux-logrotate/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-logrotate)]</sup>

Версия [logrotate](/index.php/Logrotate "Logrotate") с активированной поддержкой SELinux

[selinux-openssh](https://aur.archlinux.org/packages/selinux-openssh/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-openssh)]</sup>

Версия [OpenSSH](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)") с активированной поддержкой SELinux, для установки контекста безопасности в течение многих сеансов пользователя

#### Пространство пользователя SELinux

[selinux-usr-checkpolicy](https://aur.archlinux.org/packages/selinux-usr-checkpolicy/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-usr-checkpolicy)]</sup>

Tools to build SELinux policy

[selinux-usr-libselinux](https://aur.archlinux.org/packages/selinux-usr-libselinux/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-usr-libselinux)]</sup>

Library for security-aware applications. [Python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)") bindings needed for _semanage_ and _setools_ now included

[selinux-usr-libsemanage](https://aur.archlinux.org/packages/selinux-usr-libsemanage/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-usr-libsemanage)]</sup>

Library for policy management. Python bindings needed for _semanage_ and _setools_ now included

[selinux-usr-libsepol](https://aur.archlinux.org/packages/selinux-usr-libsepol/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-usr-libsepol)]</sup>

Library for binary policy manipulation

[selinux-usr-policycoreutils](https://aur.archlinux.org/packages/selinux-usr-policycoreutils/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-usr-policycoreutils)]</sup>

SELinux core utils such as newrole, setfiles, etc.

[selinux-usr-sepolgen](https://aur.archlinux.org/packages/selinux-usr-sepolgen/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-usr-sepolgen)]</sup>

A Python library for parsing and modifying policy source

#### Политики SELinux

[selinux-refpolicy](https://aur.archlinux.org/packages/selinux-refpolicy/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-refpolicy)]</sup>

Precompiled modular-otherways-vanilla Reference policy with headers and documentation but without sources

[selinux-refpolicy-src](https://aur.archlinux.org/packages/selinux-refpolicy-src/)<sup><small>AUR</small></sup>

Reference policy sources

[selinux-refpolicy-arch](https://aur.archlinux.org/packages/selinux-refpolicy-arch/)<sup><small>AUR</small></sup>

Precompiled modular Reference policy with headers and documentation but without sources. Development Arch Linux Refpolicy patch included, but for now [February 2011] it only fixes some issues with `/etc/rc.d/*` labeling.

#### Другие утилиты SELinux

[selinux-setools](https://aur.archlinux.org/packages/selinux-setools/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-setools)]</sup>

CLI and GUI tools to manage SELinux

[audit](https://www.archlinux.org/packages/?name=audit)

User space utilities for storing and searching the audit records generated by the audit subsystem in the Linux kernel. SELinux (AVC) will log all denials using audit. Very useful in troubleshooting SELinux. Also audit2allow use log from this program.

**Обратите внимание:** If using proprietary drivers, such as [NVIDIA](/index.php/NVIDIA "NVIDIA") graphics drivers, you may need to [rebuild them](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA") for custom kernels.

## Configuration

После установки всех необходимых пакетов их необходимо настроить.

### Changing boot loader configuration

Добавьте в конфигурационный файл [GRUB](/index.php/GRUB "GRUB") `/boot/grub/menu.lst` следующие строки:

```
# (1) Arch Linux
title  Arch Linux (SELinux)
root   (hd0,0)
kernel **vmlinuz-linux-selinux** root=/dev/sda5 ro vga=775
initrd **initramfs-linux-selinux.img**

```

### Mounting selinuxfs

Добавьте в `/etc/fstab`:

```
none   /selinux   selinuxfs   noauto   0   0

```

Создайте папку /selinux:

```
mkdir /selinux

```

### Main SELinux configuration file

Основной конфигурационный файл SELLinux (`/etc/selinux/config`) является частью пакета [selinux-refpolicy](https://aur.archlinux.org/packages/selinux-refpolicy/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-refpolicy)]</sup>. Его содержимое по умолчанию:

```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#       enforcing - SELinux security policy is enforced.
#       permissive - SELinux prints warnings 
#                       instead of enforcing.
#       disabled - No SELinux policy is loaded.
SELINUX=permissive
# SELINUXTYPE= takes the name of SELinux policy to
# be used. Current options are:
#       refpolicy (vanilla reference policy)
#       refpolicy-arch (reference policy with 
#       Arch Linux patch)
SELINUXTYPE=refpolicy

```

**Обратите внимание:** Опция `SELINUX=permissive` подходит только для конфигурации. Это не увеличивает безопасность и после настройки измените её на `SELINUX=enforcing`. Опция `SELINUXTYPE=refpolicy` устанавливает имя используемой политики. Измените его на имя вашей политики. Если вы решили скомпилировать политику из исходников, вы должны самостоятельно создать файл.

### Set up PAM

Correctly set-up PAM is important to get a proper security context after login. If you installed [selinux-shadow](https://aur.archlinux.org/packages/selinux-shadow/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-shadow)]</sup>, there should be the following lines in `/etc/pam.d/login`:

```
# pam_selinux.so close should be the first session rule
session         required        pam_selinux.so close
# pam_selinux.so open should only be followed by sessions to be executed in the user context
session         required        pam_selinux.so open

```

If not, add them to the file. Similarly for logging in via [SSH](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)") in `/etc/pam.d/sshd`, which is part of [selinux-openssh](https://aur.archlinux.org/packages/selinux-openssh/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-openssh)]</sup> package.

If you want to use SELinux with GUI, you should add the aforementioned lines to other files such as `/etc/pam.d/kde`, `/etc/pam.d/kde-np`, ... depending on your login manager.

**Обратите внимание:** Running SELinux with GUI applications in Arch Linux is not much supported at the time being.

## Reference policy

There are currently two possible ways of installing reference policy: From a pre-compiled package ([selinux-refpolicy](https://aur.archlinux.org/packages/selinux-refpolicy/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-refpolicy)]</sup>) or from a source package ([selinux-refpolicy-src](https://aur.archlinux.org/packages/selinux-refpolicy-src/)<sup><small>AUR</small></sup>).

**Обратите внимание:** It is possible to have both the source and the binary package installed. If you plan to build from source in that case, you should probably change the name of policy in `build.conf` to avoid overwriting of selinux-refpolicy package files.

### Installing a precompiled refpolicy

Install [selinux-refpolicy](https://aur.archlinux.org/packages/selinux-refpolicy/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-refpolicy)]</sup>. This is a modular-otherways-vanilla refpolicy. This package includes policy headers (you can therefore compile your own modules), policy documentation and an install script which will load the policy for you and relabel your filesystem (which will likely take some time). It does not include the sources though.

This package also includes the main SELinux configuration file (`/etc/selinux/config`) defaulting to refpolicy and permissive SELinux enforcement for testing purposes.

You should verify that the policy was correctly loaded, that is if the file `/etc/selinux/refpolicy/policy/policy.24` has non-zero size. If so and if you have installed [selinux-sysvinit](https://aur.archlinux.org/packages/selinux-sysvinit/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-sysvinit)]</sup> and other needed packages, you are ready to reboot and make sure that everything works.

**Важно:** On newer kernels (eg. 3.0) policy in file `/etc/selinux/refpolicy/policy/policy.24` has zero bytes size, because it is used new version of policy from file: `/etc/selinux/refpolicy/policy/policy.26`

In case the policy was not correctly loaded you can as root use the following command inside of the `/usr/share/selinux/refpolicy` directory to do so:

```
/bin/ls *.pp | /bin/grep -Ev "base.pp|enableaudit.pp" | /usr/bin/xargs /usr/sbin/semodule -s refpolicy -b base.pp -i

```

To manually relabel your filesystem you can as root use:

```
/sbin/restorecon -r /

```

### Installing refpolicy from a source package

Install [selinux-refpolicy-src](https://aur.archlinux.org/packages/selinux-refpolicy-src/)<sup><small>AUR</small></sup> from AUR. Edit the file `/etc/selinux/refpolicy/src/policy/build.conf` to your liking.

**Обратите внимание:** Build configuration file `build.conf` is overwritten on every selinux-refpolicy-src package upgrade, so backup your configuration.

To build, install and load policy from source do the following. (For other possibilities consult the README file located in `/etc/selinux/refpolicy/src/policy/`.)

```
cd /etc/selinux/refpolicy/src/policy
make bare
make conf 
make load

```

Copy or link the compiled binary policy to `/etc/policy.bin` for sysvinit to find and install selinux-sysvinit:

```
ln -s /etc/selinux/refpolicy/policy/policy.21 /etc/policy.bin

```

At this moment files do not have any context, so you should relabel the whole filesystem, which will take a while:

```
make relabel

```

Create the main SELinux configuration file (`/etc/selinux/config`) according to the example in related section.

Now you are ready to reboot and make sure that everything works.

## Post-installation steps

**Важно:** Если _selinux-sysvinit_ не установлен, то SELinux не сможет запуститься и `/selinux` не будет смонтирован.

Выполните `sestatus` чтобы убедиться, что SELinux работает. Должно получиться что-то вроде этого:

```
SELinux status:                 enabled
SELinuxfs mount:                /selinux
Current mode:                   permissive
Mode from config file:          permissive
Policy version:                 26
Policy from config file:        refpolicy

```

To maintain correct context, you can use _restorecond_:

```
touch /etc/rc.d/restorecond
chmod ugo+x /etc/rc.d/restorecond

```

Which should contain:

```
#!/bin/sh
restorecond

```

**Обратите внимание:** Не забудьте добавить `restorecond` в список `DAEMONS` вашего `/etc/rc.conf`.

Чтобы переключиться на осуществление режима без перезагрузки, можете использовать:

```
echo 1 > /selinux/enforce

```

**Обратите внимание:** Если `SELINUX=enforcing` в `/etc/selinux/config` не работает, создайте `/etc/rc.d/selinux-enforce` содержащий предыдущую команду так же как с restorecond демоном.

## Useful tools

There are some tools/commands that can greatly help with SELinux.

restorecon

Restores the context of a file/directory (or recursively with `-R`) based on any policy rules

rlpkg

Relabels any files belonging to that Gentoo package to their proper security context (if they have one)

chcon

Change the context on a specific file

audit2allow

Reads in log messages from the AVC log file and tells you what rules would fix the error. Do not just add these rules without looking at them though, they cannot detect errors in other places (e.g. the application is running in the wrong context in the first place), or sometimes things will generate error messages but may maintain functionality so it would be better to add dontaudit to just ignore the access attempts.

## References

*   [Security Enhanced Linux](http://en.wikipedia.org/wiki/Security-Enhanced_Linux)
*   [Gentoo SELinux Handbook](http://www.gentoo.org/proj/en/hardened/selinux/selinux-handbook.xml)
*   [Fedora Project's SELinux Wiki](http://fedoraproject.org/wiki/SELinux)
*   [NSA's Official SELinux Homepage](http://www.nsa.gov/research/selinux/index.shtml)
*   [Reference Policy Homepage](http://oss.tresys.com/projects/refpolicy)
*   [SELinux Userspace Homepage](http://userspace.selinuxproject.org/trac/)
*   [SETools Homepage](http://oss.tresys.com/projects/setools)

## See also

*   [AppArmor](/index.php/AppArmor "AppArmor") (Similar to SELinux, much easier to configure, less features.)

Retrieved from "[https://wiki.archlinux.org/index.php?title=SELinux_(Русский)&oldid=415683](https://wiki.archlinux.org/index.php?title=SELinux_(Русский)&oldid=415683)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")
*   [Security (Русский)](/index.php/Category:Security_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Security (Русский)")
*   [Kernel (Русский)](/index.php/Category:Kernel_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Kernel (Русский)")