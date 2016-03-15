В этом документе излагается один из способов распространения пакетов Arch linux по сети. Лучший способ это создание [локального хранилища с ABS и gensync](/index.php?title=%D0%9B%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B3%D0%BE_%D1%85%D1%80%D0%B0%D0%BD%D0%B8%D0%BB%D0%B8%D1%89%D0%B0_%D1%81_ABS_%D0%B8_gensync&action=edit&redlink=1 "Локального хранилища с ABS и gensync (page does not exist)"), доступного по всей локальной сети с использованием NFS или FTP. Этот документ может быть отредактирован, чтобы описать процесс подробно. Пока, подлинник HOWTO оставлен целым ниже:

Дабы распространить все загружаемые вами пакеты, в вашу локальную сеть, сохранить все параметры сети, пропускную способность, дисковое пространство и время сделайте "pacman -Sy" команда для синхронизации с вашим локальным хранилищем. "pacman -S pkgname" команда для загрузки и установки пакета с локального хранилища, если пакета не существует, он загрузится с сервера указанного в списке /etc/pacman.conf и сохранится на локальном хранилище. "alsync" команда для синхронизации и обновления локального хранилища с ftp.archlinux.org

Настройки для моей сети serverip=192.168.14.3 network=192.168.14.0/255.255.255.0 Теперь займёмся вашими:

## Contents

*   [1 Настройка локального сервера](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [1.1 Настройте hosts.allow и hosts.deny](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.82.D0.B5_hosts.allow_.D0.B8_hosts.deny)
*   [2 Для ваших клиентов](#.D0.94.D0.BB.D1.8F_.D0.B2.D0.B0.D1.88.D0.B8.D1.85_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.BE.D0.B2)
*   [3 Синхронизация вашего локального хранилища с archlinux.org](#.D0.A1.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D0.B2.D0.B0.D1.88.D0.B5.D0.B3.D0.BE_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D1.85.D1.80.D0.B0.D0.BD.D0.B8.D0.BB.D0.B8.D1.89.D0.B0_.D1.81_archlinux.org)

## Настройка локального сервера

На вашем сервере создайте nfs(протокол сетевого доступа к файловым системам) доступ с возможностью чтения и записи для любого компьютера вашей сети.

Если ваш локальный сервер под управлением Arch Linux, сделайте следущее:

```
 pacman -S rpcbind
 pacman -S nfs-utils

```

отредактируйте /etc/exports добавьте строку

```
 /var/cache/pacman/pkg
 192.168.14.0/255.255.255.0 (rw,no_root_squash,sync)

```

добавте rpcbind, nfs-common и nfs-server в секцию DAEMONS в /etc/rc.conf

запустите сервисы:

```
 # /etc/rc.d/rpcbind start
 # /etc/rc.d/nfs-common start
 # /etc/rc.d/nfs-server start

```

проверьте что nfsshare и "exportfs" запущены на локальном сервере.

### Настройте hosts.allow и hosts.deny

Всё работает очень просто:

hosts.deny ALL: ALL: DENY

hosts.allow ALL: 192.168.14.

Пояснение:

hosts.deny deny описывает все несуществующие соединения в hosts.allow. hosts.allow allow описывает соединение с с локальной сетью 192.168.14.0/255.255.255.0

## Для ваших клиентов

*   переименуйте /var/cache/pacman/pkg в /var/cache/pacman/pkgorg
*   создайте новый /var/cache/pacman/pkg и смонтируйте там nfs
*   запустите "mount -o rw,nolock 192.168.14.3:/var/cache/pacman/pkg /var/cache/pacman/pkg"
*   если команда монтирования не сработала, добавьте опцию "nfsvers=3"

или если вы хотите, чтобы всё автоматически монтировалось после перезагрузки, добавьте эту строчку в /etc/fstab

```
 192.168.14.3:/var/cache/pacman/pkg /var/cache/pacman/pkg    nfs    rw,nolock

```

*   если монтирование не работает, снова попробуйте добавить эту опцию nfsvers=3 в запись fstab.
*   запустите "mount -a"
*   запустите "df" чтобы проверить монтирование
*   переместите все ваши уже выбранные пакеты из

```
 /var/cache/pacman/pkgorg в /var/cache/pacman/pkg

```

*   отредактируйте /etc/pacman.conf и добавьте все эти строки:

```
 {current}
 Server = file:///var/cache/pacman/pkg

```

**и затем**

```
 {extra}
 Server = file:///var/cache/pacman/pkg

```

Я пропустил последние 3 шага, поскольку у меня уже всё настроено и работает, так как я хочу.

## Синхронизация вашего локального хранилища с archlinux.org

Используйте *"alsync" для соединения, входа в систему, и корректирования вашей базы данных пакетов на локальном nfs сервере.

```
 pacman -S openssl
 pacman -S wget

```

*   создайте фаил /bin/alsync и добавьте эти строки

```
 cd /var/cache/pacman/pkg
 wget -N [ftp://ftp.archlinux.org/current/](ftp://ftp.archlinux.org/current/)**.db.**
 wget -N [ftp://ftp.archlinux.org/extra/](ftp://ftp.archlinux.org/extra/)**.db.**

```

*   chmod 777 /bin/alsync

скопируйте этот файл вашим клиентам

*   чтоб запустить с правами root на первом клиенте

```
 alsync
 pacman -Sy
 pacman -S new-pkgname

```

*   перейдите к следующему клиенту и запустите

```
 pacman -Sy
 pacman -S new-pkgname

```