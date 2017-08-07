[Миграция между архитектурами](/index.php/%D0%9C%D0%B8%D0%B3%D1%80%D0%B0%D1%86%D0%B8%D1%8F_%D0%BC%D0%B5%D0%B6%D0%B4%D1%83_%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D0%B0%D0%BC%D0%B8 "Миграция между архитектурами") На этой странице описаны два возможных способа миграции установленных систем с 64-разрядных (32-разрядных) на x86_64 (64-разрядных) архитектуры. Методы избегают «полной» переустановки (т. Е. Очистки жесткого диска). Один метод использует liveCD, другой изменяет систему изнутри.

**Note:** Технически этот процесс по-прежнему включает «переустановку», поскольку каждый пакет в системе должен быть заменен. Эти методы просто пытаются сохранить как можно больше из вашей существующей системы.

**Warning:** Если не указано явно, все эти методы «непроверены» и могут нанести непоправимый урон вашей системе. Продолжайте на свой страх и риск.

## Contents

*   [1 Общая подготовка](#.D0.9E.D0.B1.D1.89.D0.B0.D1.8F_.D0.BF.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Проверить 64-битную архитектуру](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.B8.D1.82.D1.8C_64-.D0.B1.D0.B8.D1.82.D0.BD.D1.83.D1.8E_.D0.B0.D1.80.D1.85.D0.B8.D1.82.D0.B5.D0.BA.D1.82.D1.83.D1.80.D1.83)
    *   [1.2 Дисковое пространство](#.D0.94.D0.B8.D1.81.D0.BA.D0.BE.D0.B2.D0.BE.D0.B5_.D0.BF.D1.80.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D1.81.D1.82.D0.B2.D0.BE)
    *   [1.3 Источник питания](#.D0.98.D1.81.D1.82.D0.BE.D1.87.D0.BD.D0.B8.D0.BA_.D0.BF.D0.B8.D1.82.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [1.4 Пакеты резервных копий](#.D0.9F.D0.B0.D0.BA.D0.B5.D1.82.D1.8B_.D1.80.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.BD.D1.8B.D1.85_.D0.BA.D0.BE.D0.BF.D0.B8.D0.B9)
*   [2 Method 1: using the Arch LiveCD](#Method_1:_using_the_Arch_LiveCD)
*   [3 Method 2: from a running system](#Method_2:_from_a_running_system)
    *   [3.1 Package preparation](#Package_preparation)
        *   [3.1.1 Cache old packages](#Cache_old_packages)
        *   [3.1.2 Install busybox](#Install_busybox)
        *   [3.1.3 Change Pacman architecture](#Change_Pacman_architecture)
        *   [3.1.4 Download new packages](#Download_new_packages)
    *   [3.2 Package installation](#Package_installation)
        *   [3.2.1 Install kernel (64-bit)](#Install_kernel_.2864-bit.29)
        *   [3.2.2 Install lib32-glibc](#Install_lib32-glibc)
        *   [3.2.3 Reboot](#Reboot)
        *   [3.2.4 Switch to Console Terminal](#Switch_to_Console_Terminal)
        *   [3.2.5 Install Pacman](#Install_Pacman)
        *   [3.2.6 Install remaining packages](#Install_remaining_packages)
*   [4 Cleanup](#Cleanup)
    *   [4.1 Makepkg compiler flags](#Makepkg_compiler_flags)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Busybox](#Busybox)
    *   [5.2 Lib32-glibc](#Lib32-glibc)
    *   [5.3 KDE does not start after switching from 32-bit to 64-bit](#KDE_does_not_start_after_switching_from_32-bit_to_64-bit)
    *   [5.4 Mutt issues with cache enabled](#Mutt_issues_with_cache_enabled)
*   [6 See also](#See_also)

## Общая подготовка

### Проверить 64-битную архитектуру

Для запуска 64-разрядного программного обеспечения у вас должен быть 64-разрядный процессор. Большинство современных процессоров способны запускать 64-битное программное обеспечение. Вы можете проверить свой процессор с помощью следующей команды:

grep --color -w lm /proc/cpuinfo

Для процессоров, поддерживающих x86_64, это вернет `lm` flag (“long mode”). Остерегайтесь того, что 'lahf_lm' - это другой флаг и не указывает на 64-битные возможности.

### Дисковое пространство

Вы должны быть готовы к `/var/cache/pacman/pkg` увеличению размера, примерно в два раза превышает его текущий размер. Предполагается, что только пакеты, которые в настоящее время установлены, находятся в кеше, как будто “pacman -Sc” (clean) был недавно запущен. Увеличение дискового пространства связано с дублированием между версиями i686 и x86_64 каждого пакета.

Если у вас недостаточно диска, используйте [GParted](/index.php/GParted "GParted"), чтобы изменить размер соответствующего раздела или установить другой раздел в `/var/cache/pacman`.

Не удаляйте пакеты старой архитектуры из кеша, пока система не будет полностью работать в новой архитектуре. Снятие пакетов слишком рано может оставить вас неспособными отступить и вернуть изменения.

### Источник питания

Миграция может занять значительное количество времени, и было бы неудобно прерывать процесс. Вы должны планировать как минимум час, в зависимости от количества и размера установленных пакетов и скорости интернет-соединения (хотя вы можете загрузить все, прежде чем запускать критическую часть). Убедитесь, что вы подключены к стабильному источнику питания, предпочтительно с каким-либо отказоустойчивостью или резервным аккумулятором.

### Пакеты резервных копий

Если миграция завершилась неудачно, есть пакеты, которые могут помочь разобраться в ситуации, но они должны быть установлены до переноса основных пакетов. Подробнее об использовании их в разделе [#Troubleshooting](#Troubleshooting) ниже.

Один пакет [busybox](https://www.archlinux.org/packages/?name=busybox), который можно использовать для возврата изменений. Он статически связан и не зависит от каких-либо библиотек. Должна быть установлена 32-разрядная версия (i686).

Другой пакет [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc), из [Multilib](/index.php/Multilib "Multilib") x86_64 репозитория. Вероятно, это полезно, когда вы переносите «долой» из 32 бит; В любом случае вы можете безопасно пропустить этот пакет. Вы можете использовать пакет для запуска 32-битных программ, явно вызывая `/lib/ld-linux.so.2`.

## Method 1: using the Arch LiveCD

1.  [Download](https://www.archlinux.org/download/) and burn the latest Arch Linux ISO.
2.  Boot the Arch LiveCD in x86_64 mode.
3.  Configure your network on the LiveCD.
4.  Mount your existing installation. For example: `mount /dev/sda1 /mnt`.
5.  Edit the LiveCD `/etc/pacman.conf` repositories to match the existing `/mnt/etc/pacman.conf` repositories.
6.  Use the following commands to update the local pacman database and clear the cache directory.

```
 # pacman --root /mnt -Syy
 # pacman --root /mnt -Scc

```

	6\. You might first re-install the [base](https://www.archlinux.org/groups/x86_64/base/) group alone, then install any package that triggered an install error, identified using `pacman --root /mnt -Qo <error file>`. Then repeat the [base](https://www.archlinux.org/groups/x86_64/base/) group install, until it installs cleanly without errors.

```
 # pacman --root /mnt -S base

```

	7\. Use the following command to get a list of all your installed packages and then reinstall them.

```
 # pacman --root /mnt -Qnq | pacman --root /mnt -S -

```

	8\. You could run the command twice, because many packages fail to run their post-install scripts first time. This is due to sed, grep, perl, etc. being of the wrong architecture. Or you can make note of any individual package-re-install that throws an error and then go back after the upgrade completes to re-install just those packages. Also, if you see an error about not enough disk space, you can filter the package list alphabetically and upgrade in stages, with for instance `...| grep '^[a-k]' |...`, then perhaps `'^l'` and `'^[m-z]'`. In this case you would also have to run `pacman --root /mnt -Scc` after each install stage to free disk space.

	9\. Finally, run

```
 # arch-chroot /mnt 
 # mkinitcpio -p linux

```

	10\. Also, see if your boot loader needs to be migrated. For instance:

```
 # grub-install --recheck /dev/sda

```

	11\. After rebooting to your new 64-bit system, edit and then move `/etc/makepkg.conf.pacnew` to `/etc/makepkg.conf`, to migrate the cpu architecture. Then rebuild the "foreign" packages, which will include packages from the AUR.

	You might first want to remove certain orphaned foreign packages before trying to rebuild them. Run this command to find out what 32-bit binaries you still have and reinstall them:

```
 $ pacman -Qo `find /usr/bin -type f -exec bash -c 'file "{}" | grep 32-bit' \; | cut -d':' -f1` | cut -d' ' -f5 | sort | uniq | tee list

```

## Method 2: from a running system

Ensure that your system is fully updated and functioning before proceeding.

```
# pacman -Syu

```

### Package preparation

#### Cache old packages

**Note:** If you have any packages installed from the [AUR](/index.php/AUR "AUR") or third-party repositories without new architecture availability, pacman will let you know it cannot find a suitable replacement. Make a list of these packages so you may re-install them after the update process and then remove them using `pacman -Rsn package_name`.

If you do not have all your installed packages in your cache, download them (for the old architecture) for fallback purposes.

```
# pacman -Qqn | pacman -Sw -

```

or use bacman from [pacman](https://www.archlinux.org/packages/?name=pacman) package to generate them.

#### Install busybox

If you are migrating from 32 bits to 64 bits, now is the time to install 32-bit [busybox](https://www.archlinux.org/packages/?name=busybox).

```
# pacman -S busybox

```

#### Change Pacman architecture

Edit the `/etc/pacman.conf` file and change *Architecture* from `auto` to `x86_64`.

Make sure the server lists in `/etc/pacman.conf` and `/etc/pacman.d/mirrorlist` use `$arch` instead of explicitly specifying `i686` or `x86_64`. Now force Pacman to synchronize with the new repositories:

```
# pacman -Syy                     # force sync new architecture repositories

```

#### Download new packages

Download the new architecture versions of all our currently installed packages:

```
# pacman -Sw $(pacman -Qqn|sed '/^lib32-/ d')  # download new package versions

```

If migrating to 32 bits, install the 32-bit [busybox](https://www.archlinux.org/packages/?name=busybox) fallback now that Pacman has been configured with the 32-bit architecture.

**Warning:** Do not install the *lib32-glibc* package now. After a *ldconfig*, when you install *linux*, the generated image will have libraries like *librt.so* in '`/usr/lib32`, where binaries during boot will not search, resulting in a boot failure.

### Package installation

#### Install kernel (64-bit)

Upgrading the kernel to 64 bits (x86_64) is safe and straightforward: 32 bit and 64 bit applications run equally well under a 64-bit kernel.

Install the [linux](https://www.archlinux.org/packages/?name=linux) package.

```
# pacman -S linux

```

#### Install lib32-glibc

Install the [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc) fallback. You will need to add the [multilib](/index.php/Multilib "Multilib") repository in `/etc/pacman.conf` if you have not done so already.

```
# pacman -S lib32-glibc

```

**Note:** If this fails due to an existing file from a differently named package, use pacman's `--force` option.

#### Reboot

Verify that you are running the x86_64 architecture:

 `$ uname -m` 
```
x86_64

```

#### Switch to Console Terminal

Switch to a text-mode virtual console (e.g. Ctrl+Alt+F1) for the rest of the process, if possible. If you receive an error trying to use the 1st console, use the 2nd one (Ctrl-Alt+F2) instead. Pseudo-terminals like SSH should work, but direct access is recommended as a precaution. There will be several packages removed and replaced during the update process that may cause X11 desktops to become unstable and leave your system in an unbootable state.

#### Install Pacman

**Warning:** Once you start updating pacman and its dependencies it must not be interrupted! Pacman and all of its dependencies must be installed at the same time in a single command line.

**Warning:** Immediately following this command only Busybox, Bash and Pacman will be executable until the other packages are migrated below. If you are using sudo, you should obtain root previlige prior to next command

Use pactree to install Pacman and all its dependencies:

```
# pactree -l pacman | pacman -S -

```

Errors may be printed but they will not cause a problem as long as Pacman works.

**Warning:** You must not reboot your system until the following commands have been completed. If you failed to do so, you should continue installing by [chrooting](/index.php/Chroot "Chroot") from another linux environment(e.g. from live install medium)

#### Install remaining packages

Install all of the previously downloaded replacements for the new architecture. (Go get a drink and make a sandwich; this could take a while.)

```
# pacman -Qqn | pacman -S -

```

If some packages did not install correctly, you should now be able to reinstall them successfully; if you are lazy, you can just re-run the last command to reinstall everything.

After this step the migration in either direction should be complete and it should be safe to reboot the computer.

However, if you have any AUR packages on your system, you must reinstall all of them. A list of those can be obtained by executing:

```
$ pacman -Qqm

```

## Cleanup

You are now free to remove **busybox** and *lib32-glibc*.

#### Makepkg compiler flags

During the upgrade the new version of `/etc/makepkg.conf` may be stored as `/etc/makepkg.conf.pacnew`. If so, you will have to replace the old version or modify it in order to compile anything with [makepkg](/index.php/Makepkg "Makepkg") in the future.

```
# mv /etc/makepkg.conf /etc/makepkg.conf.backup && mv /etc/makepkg.conf.pacnew /etc/makepkg.conf

```

It might also be a good idea to just get a list of "new" additions to `/etc`. You can get a list with the following command:

```
# find /etc/ -type f -name \*.pac\*

```

## Troubleshooting

During the upgrade, when glibc is replaced by the new architecture version, old architecture versions of many programs will not run. If problems occur, you can solve them with [busybox](https://www.archlinux.org/packages/?name=busybox) and [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc).

### Busybox

In Arch, Busybox is statically linked; it can run without any libraries. There are many commands available to you. For example, to extract an i686 version of Pacman from a cached package:

```
# busybox tar xf /var/cache/pacman/pkg/pacman-3.3.2-1-i686.pkg.tar.gz -C <some folder>

```

### Lib32-glibc

Example run 32 bit `/bin/ls`:

```
# /lib/ld-linux.so.2 /bin/ls

```

### KDE does not start after switching from 32-bit to 64-bit

KDE will crash when starting after switching from 32-bit to 64-bit. The cause are some leftover cached files from the 32 bit KDE packages in /var/tmp To fix this remove all kdecache folders in with

```
# rm -rf /var/tmp/kdecache-*

```

### Mutt issues with cache enabled

If, after completion, you find that mutt hangs on opening mail folders, try renaming the cache directory. If this works, the renamed one can be deleted as mutt will have recreated a new one.

## See also

*   [Migrate installation to new hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware")