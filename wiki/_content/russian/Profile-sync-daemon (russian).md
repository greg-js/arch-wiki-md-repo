[Profile-sync-daemon](https://aur.archlinux.org/packages/Profile-sync-daemon/) (psd) — небольшой псевдо-демон, предназначенный для переноса профилей браузеров в tmpfs (ОЗУ) и синхронизации с постоянным хранилищем (HDD/SSD) используя rsync. Демон автоматически производит резервные копии на случай возникновения сбоев.

## Contents

*   [1 Преимущества psd](#.D0.9F.D1.80.D0.B5.D0.B8.D0.BC.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D0.B0_psd)
*   [2 Установка и настройка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Редактируем файл с конфигурацией](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D1.83.D0.B5.D0.BC_.D1.84.D0.B0.D0.B9.D0.BB_.D1.81_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B5.D0.B9)
*   [3 Поддерживаемые браузеры](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D1.8B)
*   [4 Использование psd](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_psd)
    *   [4.1 Проверка конфигурации](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.2 Режим чистки](#.D0.A0.D0.B5.D0.B6.D0.B8.D0.BC_.D1.87.D0.B8.D1.81.D1.82.D0.BA.D0.B8)
    *   [4.3 Запуск и завершение psd](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B8_.D0.B7.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_psd)
    *   [4.4 Supported distros](#Supported_distros)
    *   [4.5 Установка частоты синхронизации (опционально)](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.87.D0.B0.D1.81.D1.82.D0.BE.D1.82.D1.8B_.D1.81.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8_.28.D0.BE.D0.BF.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.29)
*   [5 FAQ](#FAQ)
    *   [5.1 What is overlayfs and why do I want to use it?](#What_is_overlayfs_and_why_do_I_want_to_use_it.3F)
    *   [5.2 Overlayfs needs more memory to accommodate my profile/profiles in /run/user/xxxx. How can I allocate more?](#Overlayfs_needs_more_memory_to_accommodate_my_profile.2Fprofiles_in_.2Frun.2Fuser.2Fxxxx._How_can_I_allocate_more.3F)
    *   [5.3 My system crashed and did not sync back. What do I do?](#My_system_crashed_and_did_not_sync_back._What_do_I_do.3F)
    *   [5.4 Where can I find this snapshot?](#Where_can_I_find_this_snapshot.3F)
    *   [5.5 How can I restore the snapshot?](#How_can_I_restore_the_snapshot.3F)
    *   [5.6 Can psd delete the snapshots automatically?](#Can_psd_delete_the_snapshots_automatically.3F)
*   [6 Поддержка](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0)
*   [7 psd в других дистрибутивах](#psd_.D0.B2_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85_.D0.B4.D0.B8.D1.81.D1.82.D1.80.D0.B8.D0.B1.D1.83.D1.82.D0.B8.D0.B2.D0.B0.D1.85)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Преимущества psd

Цели psd:

1.  Простота в использовании.
2.  Уменьшение износа жесткого диска.
3.  Увеличение скорости работы браузера.

Профили, кэш, и прочие пользовательские данные браузера переносятся с помощью psd в tmpfs (ОЗУ), соответственно операции ввода/вывода браузера перенаправляются в оперативную память. Таким образом, уменьшается износ жесткого диска, повышается отказоустойчивость и скорость работы браузера: время доступа к оперативной памяти составляет порядка наносекунд, в свою очередь, время доступа обычного жесткого диска приблизительно в 1,000,000 раз выше и составляет порядка миллисекунд.

**Примечание:** Такие браузеры как Chromium, Firefox, Midori и Rekonq хранят файлы кеша в **отдельном** от профиля каталоге. Изменение этого поведения программы не входит в задачи profile-sync-daemon. Пользователям рекомендуется обратиться к разделу [Chromium tweaks#Cache_in_tmpfs](/index.php/Chromium_tweaks#Cache_in_tmpfs "Chromium tweaks") для Chromium и к статье [Firefox Ramdisk](/index.php/Firefox_Ramdisk "Firefox Ramdisk") для Firefox, где описаны возможные решения проблемы. Наиболее простое решение будет переносом каталога с кешом (например, `/home/$USER/.cache/<browser>/<profile>/`) в каталог с профилем браузера, например `/home/$USER/.mozilla/firefox/<profile>/cache`, и создать символьную ссылку из стандартного пути в новый. Таким образом, profile-sync-daemon автоматически будет учитывать каталог с кешем.

## Установка и настройка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/).

### Редактируем файл с конфигурацией

Произведите первый запуск psd, это создаст файл `$XDG_CONFIG_HOME/psd/psd.conf`, который содержит все опции.

**Примечание:** Любые изменения произведённые в этом файле вступят в силу только после перезапуска psd посредством пользовательского systemd сервиса.

```
$ psd
First time running psd so please edit /home/facade/.config/psd/psd.conf to your liking and run again.

```

*   Опционально включите использование overlayfs для улучшения скорости синхронизации и уменьшить количество необходимой памяти. Для этого используйте переменную USE_OVERLAYFS. Пользователю понадобятся sudo права доступа к `/usr/bin/psd-overlay-helper` для использования этой опции, а также ядро должно поддерживать overlayfs версии 22 или новее. Смотрите FAQ ниже чтобы узнать подробности.
*   Опционально укажите названия веб-браузеров, профили которых необходимо перенести в ОЗУ, посредством массива BROWSERS. Если в этой переменной ничего не указано, по умолчанию перенесутся все найденные профили поддерживаемых браузеров.
*   По необходимости можете указать путь к tmpfs разделу с помощью переменной VOLATILE.
*   По необходимости можете выключить создание резервных копий профиля (не рекоммендуется) с помощью переменной USE_BACKUPS.

Пример: Допустим что у вас установлены браузеры Chromium, Opera и Midori, однако вы хотите перенести профили в ОЗУ только для Chromium и Opera:

```
# List browsers separated by spaces to include in the sync. Useful if you do not
# wish to have all possible browser profiles sync'ed.
#
# Possible values:
#  chromium
#  chromium-dev
#  conkeror.mozdev.org
#  epiphany
#  firefox
#  firefox-trunk
#  google-chrome
#  google-chrome-beta
#  google-chrome-unstable
#  heftig-aurora
#  icecat
#  luakit
#  midori
#  opera
#  opera-developer
#  opera-beta
#  qupzilla
#  palemoon
#  rekonq
#  seamonkey
#  vivaldi
#
# If the following is commented out (default), then all available/supported 
# browsers will be sync'ed, separated by comma
BROWSERS="chromium opera"

```

## Поддерживаемые браузеры

В настоящее время следующие браузеры поддерживаются:

*   [Chromium](/index.php/Chromium "Chromium")
*   [chromium-dev](/index.php/AUR "AUR")
*   [conkeror-git](https://aur.archlinux.org/packages/conkeror-git/)
*   [Epiphany](/index.php/Epiphany "Epiphany")
*   [Firefox](/index.php/Firefox "Firefox") (stable, beta и aurora)
*   [google-chrome](https://aur.archlinux.org/packages/google-chrome/)
*   [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)
*   [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)
*   [Версия Aurora от heftig](https://bbs.archlinux.org/viewtopic.php?id=117157)
*   [icecat](https://aur.archlinux.org/packages/icecat/)
*   [Luakit](/index.php/Luakit "Luakit")
*   [Midori](/index.php/Midori "Midori")
*   [Opera](/index.php/Opera "Opera")
*   Qupzilla
*   [rekonq](https://www.archlinux.org/packages/?name=rekonq)
*   [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)
*   [vivaldi](https://aur.archlinux.org/packages/vivaldi/)

## Использование psd

### Проверка конфигурации

Запуск с опцией 'parse' показывает что именно *psd* будет делать, основываясь на конфигурации в `$XDG_CONFIG_HOME/psd/psd.conf`, а также выведет прочую полезную информацию.

```
$ psd p
Profile-sync-daemon v6.03 on Arch Linux.

 Systemd service is currently active.
 Systemd resync service is currently active.
 Overlayfs v23 is currently active.

Psd will manage the following per /home/facade/.config/psd/psd.conf settings:

 browser/psname:  chromium/chromium
 owner/group:     facade/100
 sync target:     /home/facade/.config/chromium
 tmpfs dir:       /run/user/1000/facade-chromium
 profile size:    93M
 overlayfs size:  39M
 recovery dirs:   2 <- delete with the c option
  dir path/size:  /home/facade/.config/chromium-backup-crashrecovery-20150117_171359 (92M)
  dir path/size:  /home/facade/.config/chromium-backup-crashrecovery-20150119_112204 (93M)

 browser/psname:  firefox/firefox
 owner/group:     facade/100
 sync target:     /mnt/data/docs/facade/mozilla/firefox/f8cv8bfu.default
 tmpfs dir:       /run/user/1000/facade-firefox-f8cv8bfu.default
 profile size:    145M
 overlayfs size:  13M
 recovery dirs:   none

```

Как показано в выводе и указано выше, если в массиве BROWSERS не задан конкретный список браузеров, *psd* будет синхронизировать все профили поддерживаемых браузеров, которые он сможет найти для данного пользователя.

### Режим чистки

Режим чистки удалит все резервные копии. Запускайте этот режим только если вы уверенны что собранные резервные копии больше не понадобятся.

```
$ psd c

Profile-sync-daemon v6.03 on Arch Linux.

Deleting 2 crashrecovery dirs for profile /home/facade/.config/chromium
 /home/facade/.config/chromium-backup-crashrecovery-20150117_171359
 /home/facade/.config/chromium-backup-crashrecovery-20150119_112204

```

### Запуск и завершение psd

В последних версиях psd поддерживается только systemd как демон инициализации. Psd включает в себя пользовательский systemd сервис для запуска и завершения psd (psd.service).

Для пользователей, незнакомых с пользовательским режимом systemd, используйте следующую команду для запуска сервиса psd:

```
$ systemctl --user [option] psd.service

```

Доступные опции: start stop enable disable status

### Supported distros

Since psd is just a bash script with a systemd service, it should run on any flavor of Linux running systemd. Around a dozen distros provide an official package or user-maintained option to install psd. One can also build psd from source. See the official website for available packages and installation instructions.

### Установка частоты синхронизации (опционально)

Предоставленный с пакетом таймер настроен на синхронизацию с интервалом в один час. Пользователь может легко установить другой желаемый интервал, редактируя файл установок таймера. В примере ниже таймер установлен на сихронизацию с интервалом в 10 минут.

 `/etc/systemd/system/psd-resync.timer.d/frequency.conf` 
```
[Unit]
Description=Timer for Profile-sync-daemon - 10min

[Timer]
# Empty value resets the list of timers
OnUnitActiveSec=
OnUnitActiveSec=10min

```

См. `man systemd.timer` для получения дополнительной информации о настройке таймеров.

## FAQ

### What is overlayfs and why do I want to use it?

Overlayfs is a simple union file-system mainlined in the Linux kernel version 3.18.0\. Starting with psd version 5.54, overlayfs can be used to reduce the memory footprint of psd's tmpfs space and to speed up sync and unsync operations. The magic is in how the overlay mount only writes out data that has changed rather than the entire profile. The same recovery features psd uses in its default mode are also active when running in overlayfs mode. Overlayfs mode is enabled by uncommenting the USE_OVERLAYFS="yes" line in `$XDG_CONFIG_HOME/psd/psd.conf` followed by a restart of the daemon.

There are several versions of overlayfs available to the Linux kernel in production in various distros. Versions 22 and lower have a module called 'overlayfs' while newer versions (23 and higher) have a module called 'overlay' -- note the lack of the 'fs' in the newer version. Psd will automatically detect the overlayfs available to your kernel if it is configured to use one of them.

Since version 6.05 of psd, users wanting to take advantage of this mode MUST have sudo rights (without password prompt) to `/usr/bin/psd-overlay-helper` or global sudo rights. The following line in `/etc/sudoers` will supply your user with these rights. Add it using `/usr/bin/visudo` as root:

```
foo ALL=NOPASSWD: /usr/bin/psd-overlay-helper

```

See the example in the PREVIEW MODE section above which shows a system using overlayfs to illustrate the memory savings that can be achieved. Note the "overlayfs size" report compared to the total "profile size" report for each profile. Be aware that these numbers will change depending on how much data is written to the profile, but in common use cases the overlayfs size will always be less than the profile size.

### Overlayfs needs more memory to accommodate my profile/profiles in /run/user/xxxx. How can I allocate more?

The standard way of controlling the size of /run/user is the RuntimeDirectorySize directive in logind.conf (see the man page for logind.conf for more). By default, 10% of physical memory is used but one can increase it safely. Remember that tmpfs only uses what is actually used; the number specified here is just a maximum allowed.

### My system crashed and did not sync back. What do I do?

Odds are the "last good" backup of your browser profiles is just fine still sitting happily on your filesystem. Upon restarting `psd` (on a reboot for example), a check is preformed to see if the symlink to the tmpfs copy of your profile is invalid. If it is invalid, *psd* will snapshot the "last good" backup before it rotates it back into place. This is more for a sanity check that *psd* did no harm and that any data loss was a function of something else.

**Note:** Users can disable the snapshot/backup feature entirely by uncommenting and setting the USE_BACKUPS variable to 'no' in `$XDG_CONFIG_HOME/psd/psd.conf` if desired.

### Where can I find this snapshot?

It depends on the browser. You will find the snapshot in the same directory as the browser profile and it will contain a date-time-stamp that corresponds to the time at which the recovery took place. For example, chromium will be `~/.config/chromium-backup-crashrecovery-20130912_153310` -- of course, the date_time suffix will be different for you.

### How can I restore the snapshot?

*   Stop `psd`.
*   Confirm that there is no symlink to the tmpfs browser profile directory. If there is, *psd* did not stop correctly for other reasons.
*   Move the "bad" copy of the profile to a backup (do not blindly delete anything).
*   Copy the snapshot directory to the name that browser expects.

Example using Chromium:

```
mv ~/.config/chromium ~/.config/chromium-bad
cp -a ~/.config/chromium-backup-crashrecovery-20130912_153310 ~/.config/chromium

```

At this point you can launch chromium which will use the backup snapshot you just copied into place. If all is well, close the browser and restart psd. You may safely delete `~/.config/chromium-backup-crashrecovery-20130912_153310` at this point.

### Can psd delete the snapshots automatically?

Yes, run psd with the "clean" switch to delete snapshots.

## Поддержка

Пишите в [тему на форуме (англ.)](https://bbs.archlinux.org/viewtopic.php?pid=1026974) для комментариев и прочих обсуждений.

## psd в других дистрибутивах

*psd* представляет из себя обычный bash-скрипт и должен работать на любом дистрибутиве Linux. Многие дистрибутивы предоставляют официальные и пользовательские пакеты для установки psd. На [официальном сайте](https://github.com/graysky2/profile-sync-daemon#installation-from-distro-packages) доступен список пакетов и инструкции по установке.

## Смотрите также

*   [http://www.webupd8.org/2013/02/keep-your-browser-profiles-in-tmpfs-ram.html](http://www.webupd8.org/2013/02/keep-your-browser-profiles-in-tmpfs-ram.html)
*   [http://bernaerts.dyndns.org/linux/250-ubuntu-tweaks-ssd](http://bernaerts.dyndns.org/linux/250-ubuntu-tweaks-ssd)