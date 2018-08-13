Ссылки по теме

*   [USB накопители](/index.php/USB_%D0%BD%D0%B0%D0%BA%D0%BE%D0%BF%D0%B8%D1%82%D0%B5%D0%BB%D0%B8 "USB накопители")

[MTP](https://en.wikipedia.org/wiki/MTP "wikipedia:MTP"), или *Media Transfer Protocol*, класс USB устройств, использующихся большинством мобильных телефонов (все Windows Phone 7/8/10, большинство современных Android устройств) и медиаплееров (например, Creative Zen).

**Состояние перевода:** На этой странице представлен перевод статьи [MTP](/index.php/MTP "MTP"). Дата последней синхронизации: 21 ноября 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=MTP&diff=0&oldid=490585).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Функциональность](#.D0.A4.D1.83.D0.BD.D0.BA.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [1.2 Интеграция с файловыми менеджерами](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D0.BC.D0.B8_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0.D0.BC.D0.B8)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [3 Использование медиаплееров](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.B4.D0.B8.D0.B0.D0.BF.D0.BB.D0.B5.D0.B5.D1.80.D0.BE.D0.B2)
*   [4 mtpfs](#mtpfs)
*   [5 jmtpfs](#jmtpfs)
*   [6 go-mtpfs](#go-mtpfs)
*   [7 simple-mtpfs](#simple-mtpfs)
*   [8 Устранение неполадок gvfs-mtp](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_gvfs-mtp)
*   [9 Устранение неполадок kio-mtp](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_kio-mtp)

## Установка

### Функциональность

Поддержка MTP в Linux осуществляется [установкой](/index.php?title=%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%BE%D0%B9&action=edit&redlink=1 "Установкой (page does not exist)") пакета [libmtp](https://www.archlinux.org/packages/?name=libmtp). Он может быть установлен отдельно и использоваться для доступа к устройствам. Тем не менее, доступно большое число пакетов, которые используют его как зависимость и добавляют удобные (например, файловый менеджер) функциональные возможности и совместимость с конкретными типами устройств, что включает в себя и ускорение передачи данных.

Каждый из этих пакетов реализует [файловую систему в пользовательском пространстве](https://en.wikipedia.org/wiki/FUSE_(%D0%BC%D0%BE%D0%B4%D1%83%D0%BB%D1%8C_%D1%8F%D0%B4%D1%80%D0%B0) "wikipedia:FUSE (модуль ядра)"):

*   [mtpfs](https://www.archlinux.org/packages/?name=mtpfs)
*   [jmtpfs](https://aur.archlinux.org/packages/jmtpfs/) - подтверждена совместимость с устройствами новее Android 4+
*   [go-mtpfs-git](https://aur.archlinux.org/packages/go-mtpfs-git/) - подтверждена совместимость с устройствами новее Android 3+
*   [simple-mtpfs](https://aur.archlinux.org/packages/simple-mtpfs/)
*   [android-file-transfer](https://www.archlinux.org/packages/?name=android-file-transfer) - MTP клиент с аскетичным UI

Их общая цель заключена в расширении функционала и увеличении производительности `libmtp`. Так как существует множество различных USB устройств, возможно, вы захотите проверить, какой из них лучше подходит для вас.

**Важно:** `libmtp` не очень хорошо поддерживает новые устройства на Android - часто случаются зависания передачи данных и проблемы с удаленным просмотром файловой системы. Низкая производительность ожидается для всех устройств. Более того, если ваш кабель USB имеет повреждения, программы, использующие libmtp, могут завершаться с ошибкой или зависать до тех пор, пока вы не отсоедините свое устройство. Для подключения устройств рекомендуется использовать USB Mass Storage (если есть такая возможность), или воспользоваться [ADB](/index.php/ADB "ADB") (например, [adbfs-rootless-git](https://aur.archlinux.org/packages/adbfs-rootless-git/)) для передачи файлов. Он показывает высокую производительность на большинстве устройств и поддерживает дополнительные Android-специфичные функции (такие как установка APKs, управление пакетами на устройстве, резервное копирование данных или доступ к командной оболочке устройства).

**Совет:** После установки пакетов, связанных с MTP, рекомендуется перезагрузить компьютер.

### Интеграция с файловыми менеджерами

Чтобы просматривать содержимое накопителя вашего Android устройства через MTP в файловом менеджере, установите соответствующий плагин:

*   Для файловых менеджеров, которые используют [GVFS](/index.php/GVFS "GVFS") ([GNOME Files](/index.php/GNOME_Files "GNOME Files"), Xfce's [Thunar](/index.php/Thunar "Thunar")), установите [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) для поддержки MTP и [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) для поддержки PTP.
*   Для файловых менеджеров, которые используют KIO (KDE's Dolphin), установите [kio-mtp](https://www.archlinux.org/packages/?name=kio-mtp) (поддержка PTP уже включена в него).

Также существует альтернатива плагинам: минималистичный MTP клиент [android-file-transfer](https://www.archlinux.org/packages/?name=android-file-transfer).

После установки необходимых пакетов, ваше устройство должно отобразиться в файловом менеджере автоматически, и вы сможете получать доступ к файлам по URL наподобие такого: `mtp://[usb:002,013]/`.

**Примечание:** Если у вас более новое Android устройство, которое не поддерживает UMS (USB-накопитель) и вы считаете что [mtpfs](https://www.archlinux.org/packages/?name=mtpfs) очень медленный или работает некорректно, то вы можете установить [jmtpfs](https://aur.archlinux.org/packages/jmtpfs/) из AUR.

## Использование

**Примечание:** Не забудьте разблокировать ваш телефон (лок-скрин) перед подключением, потому что иначе вы увидите сообщения об ошибке.

После установки у вас есть несколько доступных MTP инструментов. При подключении вашего MTP-устройства используйте:

```
# mtp-detect

```

чтобы узнать, обнаружено ли ваше устройство MTP. Если вы получаете ошибки о разрешении, помните, что вам нужно быть в группе uucp для доступа к системе USB в целом.

Чтобы подключиться к вашему устройству MTP, используйте:

```
# mtp-connect

```

Если соединение выполнено успешно, для доступа к данным на устройстве существует несколько вариантов переключения в сочетании с `mtp-connect`.

Есть также несколько автономных команд, которые вы можете использовать для доступа к вашему устройству MTP, например,
**Warning:** Некоторые команды могут быть вредны для вашего устройства MTP!!!!!

```
 mtp-albumart        mtp-emptyfolders    mtp-getplaylist     mtp-reset           mtp-trexist
 mtp-albums          mtp-files           mtp-hotplug         mtp-sendfile
 mtp-connect         mtp-folders         mtp-newfolder       mtp-sendtr
 mtp-delfile         mtp-format          mtp-newplaylist     mtp-thumb
 mtp-detect          mtp-getfile         mtp-playlists       mtp-tracks

```

Если вы видите сообщение типа:

```
Device 0 (VID=XXXX and PID=XXXX) is UNKNOWN.
Please report this VID/PID and the device model to the libmtp development team

```

Вы должны проверить, было ли уже ваше устройство в этом списке: [Список поддерживаемых устройств[[1]](http://sourceforge.net/p/libmtp/code/ci/HEAD/tree/src/music-players.h)] Если это не так, сообщите об этом команде разработчиков. Если это так, ваш libmtp может быть немного устаревшим. Чтобы libmtp нормально функционировал в данном случае, вы можете добавить свое устройство в:

```
/usr/lib/udev/rules.d/69-libmtp.rules

```

## Использование медиаплееров

Использование медиаплееровВы также можете использовать свое устройство MTP в музыкальных проигрывателях, таких как Amarok. Для этого вам, возможно, придется отредактировать /usr/lib/udev/rules.d/51-android.rules (устройство MTP, используемое в следующем примере, представляет собой Galaxy Nexus): Для этого выполните:

```
$ lsusb

```

и найдите свое устройство, это будет что-то вроде:

```
Bus 003 Device 011: ID 04e8:6860 Samsung Electronics Co., Ltd GT-I9100 Phone [Galaxy S II], GT-P7500 [Galaxy Tab 10.1]

```

в этом случае запись будет:

```
SUBSYSTEM=="usb", ATTR{idVendor}=="04e8", ATTR{idProduct}=="6860", MODE="0666", OWNER="[имя пользователя]"

```

Затем перезагрузите правила udev:

```
# udevadm control --reload

```

**Note:** После установки MTP вам может потребоваться перезагрузка, чтобы ваше устройство распознавалось

## mtpfs

**Warning:** Возможно, что это не сработает, и вам может потребоваться [gphoto2](/index.php/Digital_Cameras#libgphoto2 "Digital Cameras") или файловый менеджер с поддержкой gvfs, такой как [PCManFM](/index.php/PCManFM "PCManFM") или [Thunar](/index.php/Thunar "Thunar").

Mtpfs - файловая система FUSE, которая поддерживает чтение и запись с любого устройства MTP. В основном это позволяет подключить ваше устройство к внешнему диску.

Mtpfs можно установить с пакетом [mtpfs](https://www.archlinux.org/packages/?name=mtpfs), доступным из [official repositories](/index.php/Official_repositories "Official repositories").

*   Сначала отредактируйте `/etc/fuse.conf` и раскомментируйте следующую строку:

```
user_allow_other

```

*   Для примонтирования устройства:

```
$ mtpfs -o allow_other /mnt/YOURMOUNTPOINT

```

*   Для размонтирования устройства:

```
$ fusermount -u /mnt/YOURMOUNTPOINT

```

*   Для размонтирования устройства от root:

```
# umount /mnt/YOURMOUNTPOINT

```

Кроме того, вы можете поместить их в свой файл ~/.bashrc:

```
alias android-connect="mtpfs -o allow_other /media/YOURMOUNTPOINT"
alias android-disconnect="fusermount -u /media/YOURMOUNTPOINT"

```

Или, с sudo:

```
alias android-disconnect="sudo umount -u /media/YOURMOUNTPOINT"

```

**Note:** Если вы не хотите запрашивать пароль при использовании sudo, обратитесь к [USB storage devices](/index.php/USB_storage_devices "USB storage devices")

## jmtpfs

[jmtpfs](http://research.jacquette.com/jmtpfs-exchanging-files-between-android-devices-and-linux/) - файловая система FUSE и libmtp для доступа к устройствам MTP (Media Transfer Protocol). Он был специально разработан для обмена файлами между системами Linux и новыми устройствами Android, поддерживающими MTP, но не USB Mass Storage. jmtpfs доступен как [jmtpfs](https://aur.archlinux.org/packages/jmtpfs/) в [AUR](/index.php/AUR "AUR").

Используйте эти команды для монтирования устройства:

```
$ jmtpfs ~/mtp

```

И данную команду для его размонтирования:

```
$ fusermount -u ~/mtp

```

## go-mtpfs

**Note:** Go-mtpfs gives a better performance while writing files to some devices than mtpfs/jmtpfs. Try it if you have slow speeds.

**Note:** Mounting with Go-mtpfs fails if external SD Card is present. If you have also external SD Card please remove it and then try mounting again.

If the above instructions do not show any positive results one should try [go-mtpfs-git](https://aur.archlinux.org/packages/go-mtpfs-git/) from the [AUR](/index.php/AUR "AUR"). The following has been tested on a Samsung Galaxy Nexus GSM, Asus/Google Nexus 7 (2012 1st gen model), Samsung Galaxy S 3 mini and Google Nexus 4\. (This is the only mtp software which worked for me on Nexus 4\. Settings are usb debugging enabled, connected as media device.)

If you want do it simpler, install [go](https://www.archlinux.org/packages/?name=go), [libmtp](https://www.archlinux.org/packages/?name=libmtp) and [git](https://www.archlinux.org/packages/?name=git) from the [official repositories](/index.php/Official_repositories "Official repositories"). After that install [go-mtpfs-git](https://aur.archlinux.org/packages/go-mtpfs-git/) from the [AUR](/index.php/AUR "AUR").

As in the section above install [android-udev](https://www.archlinux.org/packages/?name=android-udev) which will provide you with "/usr/lib/udev/rules.d/51-android.rules" edit it to apply to your idVendor and idProduct, which you can see after running mtp-detect. To the end of the line add with a comma OWNER="yourusername". Save the file.

*   Add yourself to the "fuse" group:

```
gpasswd -a [user] fuse

```

*   If the group "fuse" does not exist create it with:

```
groupadd fuse

```

Logout or reboot to apply these changes.

*   To create a mount point called "Android" issue the following commands:

```
mkdir Android

```

*   To mount your phone use:

```
go-mtpfs Android

```

*   To unmount your phone:

```
fusermount -u Android

```

You can create a .bashrc alias as in the example above for easier use.

## simple-mtpfs

Это еще одна файловая система FUSE для устройств MTP. Вы можете найти это более надежным, чем [mtpfs](https://www.archlinux.org/packages/?name=mtpfs). [simple-mtpfs](https://aur.archlinux.org/packages/simple-mtpfs/) доступен в AUR или может быть построен из источника. Не запускайте следующие команды с правами root!

Чтобы указать запуск MTP-устройств

```
$ simple-mtpfs --list-devices

```

Для монтирования устройств MTP (в этом примере устройства 0) выполните

```
$ simple-mtpfs /path/to/your/mount/point

```

Для отмнонтирования

```
$ fusermount -u /path/to/your/mount/point

```

## Устранение неполадок gvfs-mtp

Если вы установили пакет [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp), и ваше устройство не отображается в файловом менеджере, вам может потребоваться написать правило udev для автоматической установки устройства.

Подключите ваше устройство и получите идентификатор поставщика и идентификатор продукта, соответственно:

```
$ lsusb
Bus 001 Device 007: ID 0421:0661 Nokia Mobile Phones Lumia 920
(...)

```

Два числа после ID *vendorId*:*productID*

Затем сделайте правило udev, то есть выполните

```
# nano /usr/lib/udev/rules.d/51-android.rules

```

и введите это правило:

```
ATTR{idVendor}=="ВАШ VENDOR УСТРОЙСТВА ЗДЕСЬ", ATTR{idProduct}=="ВАШ ID УСТРОЙСТВА ЗДЕСЬ", SYMLINK+="libmtp",  MODE="660", ENV{ID_MTP_DEVICE}="1"

```

Перезагрузите правила udev.

```
# udevadm control --reload

```

И перезагрузите систему. Теперь файловые менеджеры (например, Thunar) должны иметь возможность авторизовать MTP-устройство. [[2]](https://bbs.archlinux.org/viewtopic.php?id=180719)

## Устранение неполадок kio-mtp

Если вы не можете использовать действие «Открыть с помощью диспетчера файлов», вы можете обойти эту проблему, отредактировав файл **/usr/share/apps/solid/actions/solid_mtp.desktop**

Замените строку

```
Exec=kioclient exec mtp:udi=%i/

```

На

```
Exec=dolphin "mtp:/"

```