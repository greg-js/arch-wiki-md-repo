Описывает процесс установки и конфигурирования AutoFS, пакета для автоматического монтирования съёмных носителей и сетевых ресурсов.

## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Конфигурирование](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.1 Съёмные носители](#.D0.A1.D1.8A.D1.91.D0.BC.D0.BD.D1.8B.D0.B5_.D0.BD.D0.BE.D1.81.D0.B8.D1.82.D0.B5.D0.BB.D0.B8)
    *   [3.2 Монтирование NFS](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_NFS)
    *   [3.3 Samba](#Samba)
    *   [3.4 FTP и SSH (через Fuse)](#FTP_.D0.B8_SSH_.28.D1.87.D0.B5.D1.80.D0.B5.D0.B7_Fuse.29)
        *   [3.4.1 Удалённые FTP](#.D0.A3.D0.B4.D0.B0.D0.BB.D1.91.D0.BD.D0.BD.D1.8B.D0.B5_FTP)
        *   [3.4.2 Удалённые SSH](#.D0.A3.D0.B4.D0.B0.D0.BB.D1.91.D0.BD.D0.BD.D1.8B.D0.B5_SSH)
*   [4 Запуск AutoFS](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_AutoFS)
*   [5 Решение проблем и советы](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC_.D0.B8_.D1.81.D0.BE.D0.B2.D0.B5.D1.82.D1.8B)
    *   [5.1 Опциональные параметры](#.D0.9E.D0.BF.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B)
    *   [5.2 Распознавание нескольких устройств](#.D0.A0.D0.B0.D1.81.D0.BF.D0.BE.D0.B7.D0.BD.D0.B0.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.B8.D1.85_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
    *   [5.3 Права доступа AutoFS](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B0_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0_AutoFS)
*   [6 Ссылки на внешние источники](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8_.D0.BD.D0.B0_.D0.B2.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D0.B8.D1.81.D1.82.D0.BE.D1.87.D0.BD.D0.B8.D0.BA.D0.B8)
*   [7 Альтернативы для AutoFS](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D1.8B_.D0.B4.D0.BB.D1.8F_AutoFS)

## Введение

Этот документ описывают процедуру установки AutoFS, пакета который даёт возможность автоматического монтирования съёмных носителей и сетевых ресурсов при вставке или получении доступа к ним.

## Установка

*   Установите пакет AutoFS:

```
# pacman -S autofs

```

**Обратите внимание:** Вам больше не нужно загружать модуль `autofs4`.

## Конфигурирование

AutoFS использует для конфигурирования шаблоны, расположенные в `/etc/autofs`. Основной шаблон называется `auto.master`, он может указывать на один или несколько других шаблонов для конкретных типов носителей.

*   Откройте `/etc/autofs/auto.master` своим любимым редактором. Вы увидите что-то подобное:

 `/etc/autofs/auto.master`  `#/media /etc/autofs/auto.media` 

Первое значение в каждой строке определяет базовый каталог, в который носители будут монтироваться, второе значение - шаблон который будет использован. По умолчанию базовая директория /var/autofs, но вы можете изменить путь на любое другое значение по вашему желанию. Например:

```
/media/misc     /etc/autofs/auto.misc     --timeout=5
/media/net      /etc/autofs/auto.net      --timeout=60

```

Дополнительный параметр `timeout` устанавливает количество секунд после которых устройство будет размонтировано. Параметр `ghost` означает что сконфигурированные ресурсы будут отображаться всегда, а не только тогда, когда они вставлены и доступны. Это полезно тогда, когда вы не хотите запоминать или угадывать имена съёмных носителей и сетевых ресурсов.

Конечные каталоги должны существовать в системе и быть пусты, поскольку их содержимое будет заменено с динамически загружаемого носителя. Однако это не критично, если вы случайно монтировали носитель в непустую директорию, просто измените путь в auto.master и перезапустите AutoFS чтобы вернуть исходное содержимое.

**Обратите внимание:** Убедитесь в наличии пустой строки в конце файла шаблона (нажмите ENTER после последнего слова). Если нет корректной EOF-строки, демон AutoFS не будет загружен правильно.

*   Откройте файл `/etc/nsswitch.conf` и добавьте запись для автоматического монтирования:

```
automount: files

```

### Съёмные носители

*   Откройте `/etc/autofs/auto.misc` и добавьте, удалите или измените всевозможные устройства. Например:

```
#kernel   -ro                                        ftp.kernel.org:/pub/linux
#boot     -fstype=ext2                               :/dev/hda1
usbstick  -fstype=auto,async,nodev,nosuid,umask=000  :/dev/sdb1
cdrom     -fstype=iso9660,ro                         :/dev/cdrom
#floppy   -fstype=auto                               :/dev/fd0

```

Если у вас комбинированный CD/DVD-привод вы можете изменить тип в строке cdrom на "-fstype=auto" для авто-определения типа носителя.

### Монтирование NFS

AutoFS предоставляет новый способ автоматического обнаружения и монтирования NFS-ресурсов на удалённых серверах (шаблон конфигурирования сетевых ресурсов `/etc/autofs/auto.net` был удалён в autofs5). Чтобы включить автоматическое обнаружение и монтирование сетевых ресурсов со всех доступных серверов без необходимости дополнительного конфигурирования, вам необходимо добавить следующее в файл `/etc/autofs/auto.master`:

```
/net -hosts --timeout=60

```

Каждое имя хоста должно быть разрешено, например, любой IP-адрес в `/etc/hosts` или заданный через DNS.

К примеру, есть удалённый сервер _fileserver_ с ресурсом NFS, который называется _/home/share_, вы можете получить доступ к ресурсу просто набрав:

```
# cd /net/fileserver/home/share

```

**Обратите внимание:** _ghosting_, i.e. automatically creating directory placeholders before mounting shares is enabled by default, although AutoFS installation notes claim to remove that option from `/etc/conf.d/autofs` in order to start the AutoFS daemon.

The `-hosts` option uses a similar mechanism as the _showmount_ command to detect remote shares. You can see the exported shares by typing:

```
# showmount <servername> -e 

```

Замените _<servername>_ на имя ващего собственного сервера.

### Samba

Сборка пакета в Arch не содержит каких-либо samba или cifs шаблонов/скриптов (23.07.2009), но следующее должно работать для отдельных ресурсов:

добавьте следующее в `/etc/autofs/auto.master`

```
/media/[my_server] /etc/autofs/auto.[my_server]

```

а затем создайте файл `/etc/autofs/auto.[my_server]`

```
[my_share] -fstype=cifs,[other_options] ://[my_server_ip]/[my_share]

```

### FTP и SSH (через Fuse)

Доступ к удалённым FTP- и SSH-серверам может быть легко получен с AutoFS, используя Fuse, часть виртуальной файловой системы.

#### Удалённые FTP

Во-первых, установите пакет curlftpfs из репозитория Community:

```
# pacman -S curlftpfs

```

Загрузите модуль Fuse:

```
# modprobe fuse

```

Добавьте fuse массив _modules_ в `/etc/rc.conf` для загрузки его при каждом запуске компьютера.

Далее, добавьте новую запись для FTP-серверов в `/etc/autofs/auto.master`:

```
/media/ftp        /etc/autofs/auto.ftp    --timeout=60,ghost

```

Создайте файл `/etc/autofs/auto.ftp` и добавьте сервер в формате `[ftp://myuser:mypassword@host:port/path](ftp://myuser:mypassword@host:port/path)`:

```
servername -fstype=curl,allow_other    :ftp\://myuser\:mypassword\@remoteserver

```

**Обратите внимание:** Ваши пароли может видеть каждый, кто запустит _df_ (только для примонтированных серверов) или откроет файл `/etc/autofs/auto.ftp`.

Если Вы хотите немного больше безопасности, можете создать файл `~root/.netrc` и указать пароли там. Пароли по-прежнему написаны в текстовом формате, но Вы можете задать права 600, и команда _df_ их не покажет (неважно, примонтирован сервер, или нет). Этот способ также менее чувствителен к специальным символам (которых иначе необходимо избегать) в паролях. Придерживайтесь такого формата:

```
machine remoteserver  
login myuser
password mypassword

```

Строчка в `/etc/autofs/auto.ftp` выглядит как эта, без имени пользователя и пароля:

```
servername -fstype=curl,allow_other    :ftp\://remoteserver

```

Создайте файл `/sbin/mount.curl` с кодом:

```
#! /bin/sh
curlftpfs $1 $2 -o $4,disable_eprt

```

Создайте файл `/sbin/umount.curl` с кодом:

```
#! /bin/sh
fusermount -u $1

```

Установите права для обоих файлов:

```
# chmod 755 /sbin/mount.curl
# chmod 755 /sbin/umount.curl

```

После перезапуска Ваш новый FTP-сервер должен быть доступен через `/media/ftp/servername`

#### Удалённые SSH

Здесь основные инструкции по доступу к удалённой файловой системе через SSH с помощью AutoFS.

**Обратите внимание:** Приведённый пример не использует ssh-passphrase для упрощения установки, просим учесть, что это может оказаться угрозой безопасности в случае использования его в Вашей системе.

Установите пакет sshfs из репозитория Extra

```
# pacman -S sshfs

```

Загрузите модуль Fuse:

```
# modprobe fuse

```

Добавьте fuse в секцию _modules_ в `/etc/rc.conf`, чтобы загружать его при каждом запуске системы.

Установите OpenSSH:

```
# pacman -S openssh

```

Сгенерируйте ключ SSH:

```
# ssh-keygen -t dsa

```

Когда генератор запросит фразу-пароль, просто нажмите enter. Использование ключей SSH без фразы-пароля, однако запуск AutoFS без фразы-пароля приводит к некоторым дополнительным трудностям, которые (пока) не были освещены в этой статье.

Далее, скопируйте общественный ключ на удалённый SSH сервер:

```
# ssh-copy-id -i ~/.ssh/id_dsa.pub username@remotehost

```

Скопируйте личный ключ в домашнюю директорию пользователя root, чтобы AutoFS могла его найти:

```
# sudo cp ~/.ssh/id_dsa /root/.ssh/id_dsa

```

Вышеприведённое работает, если AutoFS запускается с правами root и по умолчанию не имеет доступа в домашнюю директорию пользователя, содержащую личный ключ.

Войти на удалённый сервер без ввода пароля можно так:

```
# ssh username@remotehost

```

Создайте новый вход для сервера SSH в `/etc/autofs/auto.master`:

```
/media/ssh		/etc/autofs/auto.ssh	--timeout=60,ghost

```

Создайте файл `/etc/autofs/auto.ssh` и добавьте SSH:

```
servername     -fstype=fuse,rw,nodev,nonempty,allow_other,max_read=65536 :sshfs\#username@host\:/

```

После перезапуска Ваш сервер SSH должен быть доступен через `/media/ssh/servername`

## Запуск AutoFS

*   Когда настройка закончена, запустите демон AutoFS с правами суперпользователя:

```
# /etc/rc.d/autofs start

```

Чтобы запускать демон при запуске системы, Вы можете добавить `autofs` в секцию DAEMONS в /etc/rc.conf, и `autofs4` в секцию modules в том же файле.

Если Вы изменяете шаблон auto.master при работающей AutoFS, Вам придётся перезапустить демон, чтобы получить эффект от изменений:

```
# /etc/rc.d/autofs restart

```

Теперь утройства будут автоматически монтироваться при каждом доступе, они будут оставаться подключенными в течении всего времени доступа.

## Решение проблем и советы

Эта секция содержит несколько решений самых распространённых проблем с AutoFS.

### Опциональные параметры

Вы можете установить параметры, такие как `timeout`, на общесистемном уровне для всех медиаустройств AutoFS в `/etc/conf.d/autofs`:

*   Откройте файл `/etc/conf.d/autofs` и отредактируйте строку daemonoptions:

```
daemonoptions='--timeout=5'

```

*   Чтобы сделать возможным ведение логов (по умолчанию его нет), добавьте `--verbose` в строку daemonoptions в `/etc/conf.d/autofs`, например:

```
daemonoptions='--verbose --timeout=5'

```

После перезапуска autofs, подробный вывод виден в /var/log/daemon.log

### Распознавание нескольких устройств

Если Вы используете несколько устройств USB и хотите легко отсоединять их, Вы можете использовать AutoFS чтобы определять точки монтирования и udev чтобы давать имена Вашим устройствам USB. Посмотрите [Map Custom Device Entries with udev](/index.php/Map_Custom_Device_Entries_with_udev "Map Custom Device Entries with udev") для инструкций по настройке правил udev.

### Права доступа AutoFS

Если AutoFS не работает правильно, убедитесь в том, что права доступа для файлов шаблонов установлены правильно, иначе AutoFS не будет запускаться. Это может случиться, если Вы сделали резервную копию способом, который не сохраняет права. Вот как должны быть установлены права доступа для файлов конфигурации:

*   0644 - /etc/autofs/auto.master
*   0644 - /etc/autofs/auto.media
*   0644 - /etc/autofs/auto.misc
*   0644 - /etc/conf.d/autofs

В общем, скрипты (такие как previous auto.net) должны иметь установленный бит исполнения (chown a+x filename), а списки монтируемых устройств не должны.

Если Вы получаете ошибки в `/var/log/daemon.log`, подобные этим, значит у Вас проблемы с правами доступа:

```
May  7 19:44:16 peterix automount[15218]: lookup(program): lookup for petr failed
May  7 19:44:16 peterix automount[15218]: failed to mount /media/cifs/petr

```

## Ссылки на внешние источники

*   Оригинальная информация на этой странице основана на теме: [https://bbs.archlinux.org/viewtopic.php?t=7630](https://bbs.archlinux.org/viewtopic.php?t=7630), с дополнительной информацией, найденной здесь: [http://libranet.com/support/2.8/0381](http://libranet.com/support/2.8/0381)
*   Информация об использовании FTP и SFTP с AutoFS основана на этой статье из Gentoo Wiki: [http://en.gentoo-wiki.com/wiki/Mounting_SFTP_and_FTP_shares](http://en.gentoo-wiki.com/wiki/Mounting_SFTP_and_FTP_shares)
*   Больше информации о SSH можно найти на страницах [SSH](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)") и [SSH Keys](/index.php/SSH_Keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH Keys (Русский)") этого wiki.

## Альтернативы для AutoFS

*   [Thunar Volume Manager](/index.php/Thunar_Volume_Manager "Thunar Volume Manager") - система автомонтирования для пользователей Thunar file manager.
*   Pcmanfm-fuse - лёгкий менеджер файлов со встроенной поддержкой для поддержки удалённых расшар: [https://aur.archlinux.org/packages.php?ID=22992](https://aur.archlinux.org/packages.php?ID=22992)