**Состояние перевода:** На этой странице представлен перевод статьи [Tmpfs](/index.php/Tmpfs "Tmpfs"). Дата последней синхронизации: 25 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Tmpfs&diff=0&oldid=427657).

[tmpfs](https://en.wikipedia.org/wiki/ru:Tmpfs "wikipedia:ru:Tmpfs") это временная файловая система, которая находится в памяти и/или вашем разделе(ах) подкачки, в зависимости от того на сколько вы заполнили её. Монтирование каталогов как TMPFS, будет эффективным способом ускорения доступа к своим файлам, или для того, чтобы их содержимое автоматически удалялось при перезагрузке.

**Примечание:** При использовани [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), временные файлы в каталогах tmpfs могут быть пересозданы при загрузке используя [tmpfiles.d](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B "Systemd (Русский)").

## Contents

*   [1 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [2 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
*   [3 Отключить автоматическое монтирование](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Не получается открытие символьных ссылок в tmpfs от root](#.D0.9D.D0.B5_.D0.BF.D0.BE.D0.BB.D1.83.D1.87.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D1.81.D0.B8.D0.BC.D0.B2.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D1.81.D1.81.D1.8B.D0.BB.D0.BE.D0.BA_.D0.B2_tmpfs_.D0.BE.D1.82_root)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Использование

Some directories where tmpfs is commonly used are [/tmp](http://www.pathname.com/fhs/2.2/fhs-3.15.html), [/var/lock](http://www.pathname.com/fhs/2.2/fhs-5.9.html) and [/var/run](http://www.pathname.com/fhs/2.2/fhs-5.13.html). Do **not** use it on [/var/tmp](http://www.pathname.com/fhs/2.2/fhs-5.15.html), because that folder is meant for temporary files that are preserved across reboots.

Arch uses a tmpfs `/run` directory, with `/var/run` and `/var/lock` simply existing as symlinks for compatibility. It is also used for `/tmp` by the default systemd setup and does not require an entry in [fstab](/index.php/Fstab "Fstab") unless a specific configuration is needed.

[glibc](https://www.archlinux.org/packages/?name=glibc) 2.2 and above expects tmpfs to be mounted at `/dev/shm` for [POSIX shared memory](https://en.wikipedia.org/wiki/Shared_memory_(interprocess_communication)#Support_on_UNIX_platforms "wikipedia:Shared memory (interprocess communication)"). Mounting tmpfs at `/dev/shm` is handled automatically by [systemd](/index.php/Systemd "Systemd"), so manual configuration in [fstab](/index.php/Fstab "Fstab") is no longer necessary.

Generally, I/O intensive tasks and programs that run frequent read/write operations can benefit from using a tmpfs folder. Some applications can even receive a substantial gain by offloading some (or all) of their data onto the shared memory. For example, [relocating the Firefox profile into RAM](/index.php/Firefox_on_RAM "Firefox on RAM") shows a significant improvement in performance.

## Примеры

By default, a tmpfs partition has its maximum size set to half your total RAM, but this can be customized. Note that the actual memory/swap consumption depends on how much you fill it up, as tmpfs partitions do not consume any memory until it is actually needed.

To explicitly set a maximum size, in this example to override the default `/tmp` mount, use the `size` mount option:

 `/etc/fstab`  `tmpfs   /tmp         tmpfs   nodev,nosuid,size=2G          0  0` 

Here is a more advanced example showing how to add tmpfs mounts for users. This is useful for websites, mysql tmp files, `~/.vim/`, and more. It's important to try and get the ideal mount options for what you are trying to accomplish. The goal is to have as secure settings as possible to prevent abuse. Limiting the size, and specifying uid and gid + mode is very secure. For more information on this subject, follow the links listed in the [#See also](#See_also) section.

 `/etc/fstab`  `tmpfs   /www/cache    tmpfs  rw,size=1G,nr_inodes=5k,noexec,nodev,nosuid,uid=648,gid=648,mode=1700   0  0` 

See the `mount` command man page for more information. One useful mount option in the man page is the `default` option. At least understand that.

Reboot for the changes to take effect. Note that although it may be tempting to simply run `mount -a` to make the changes effective immediately, this will make any files currently residing in these directories inaccessible (this is especially problematic for running programs with lockfiles, for example). However, if all of them are empty, it should be safe to run `mount -a` instead of rebooting (or mount them individually).

After applying changes, you may want to verify that they took effect by looking at `/proc/mounts` and using `findmnt`:

 `$ findmnt --target /tmp` 
```
TARGET SOURCE FSTYPE OPTIONS
/tmp   tmpfs  tmpfs  rw,nosuid,nodev,relatime
```

The tmpfs can also be temporarily resized without the need to reboot, for example when a large compile job needs to run soon. In this case, you can run:

```
# mount -o remount,size=4G,noatime /tmp

```

## Отключить автоматическое монтирование

Under [systemd](/index.php/Systemd "Systemd"), `/tmp` may be automatically mounted as a tmpfs even though you have no entry for that in your `/etc/fstab`.

To disable the automatic mount, run:

```
# systemctl mask tmp.mount

```

Files will no longer be stored in a tmpfs, but your block device instead. The `/tmp` contents will now be preserved between reboots, which you might not want. To regain the previous behavior and clean the `/tmp` folder automatically when restarting your machine, consider using `tmpfiles.d(5)`:

 `/etc/tmpfiles.d/tmp.conf` 
```
# see tmpfiles.d(5)
# always enable /tmp folder cleaning
D! /tmp 1777 root root 0

# remove files in /var/tmp older than 10 days
D /var/tmp 1777 root root 10d

# namespace mountpoints (PrivateTmp=yes) are excluded from removal
x /tmp/systemd-private-*
x /var/tmp/systemd-private-*
X /tmp/systemd-private-*/tmp
X /var/tmp/systemd-private-*/tmp
```

## Решение проблем

### Не получается открытие символьных ссылок в tmpfs от root

Considering `/tmp` is using tmpfs, change the current directory to `/tmp`, then create a file and create a symlink to that file in the same `/tmp` directory. If you try to open the file you created via the symlink, you will get a permission denied error. This is expected as `/tmp` [has the sticky bit set](https://wiki.ubuntu.com/Security/Features#Symlink_restrictions).

This behaviour can be controlled via `/proc/sys/fs/protected_symlinks` or simply via sysctl: `sysctl -w fs.protected_symlinks=0`. See [Sysctl#Configuration](/index.php/Sysctl#Configuration "Sysctl") to make this permanent.

**Важно:** Changing this behaviour can lead to security issues! Disable it only if you know what you are doing.

## Смотрите также

*   [Linux kernel documentation](https://www.kernel.org/doc/Documentation/filesystems/tmpfs.txt)