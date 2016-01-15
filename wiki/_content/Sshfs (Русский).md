# Sshfs (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

Вы можете использовать sshfs для монтирования удаленной системы - доступной через [SSH](/index.php/SSH_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH (Русский)") - в локальную папку так, что сможете совершать любые операции над примонтированными файлами с помощью любого инструмента (копирование, переименовывание, редактирование с помощью vim и др.). Использование sshfs вместо shfs рекомендуется в большинстве случаев, так как ни одна новая версия shfs не была выпущена с 2004 года.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Монтирование](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [1.2 Размонтирование](#.D0.A0.D0.B0.D0.B7.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [2 Изменение корневого каталога](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.B0)
*   [3 Вспомогательные программы](#.D0.92.D1.81.D0.BF.D0.BE.D0.BC.D0.BE.D0.B3.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)
*   [4 Автоматическое монтирование](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [4.1 По запросу](#.D0.9F.D0.BE_.D0.B7.D0.B0.D0.BF.D1.80.D0.BE.D1.81.D1.83)
    *   [4.2 При загрузке](#.D0.9F.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
    *   [4.3 Безопасный доступ пользователей](#.D0.91.D0.B5.D0.B7.D0.BE.D0.BF.D0.B0.D1.81.D0.BD.D1.8B.D0.B9_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
*   [5 Параметры](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Контрольный список](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D1.81.D0.BF.D0.B8.D1.81.D0.BE.D0.BA)
    *   [6.2 Connection reset by peer](#Connection_reset_by_peer)
    *   [6.3 Remote host has disconnected](#Remote_host_has_disconnected)
    *   [6.4 Freezing apps (e.g. Nautilus, Gedit)](#Freezing_apps_.28e.g._Nautilus.2C_Gedit.29)
    *   [6.5 Shutdown hangs when sshfs is mounted](#Shutdown_hangs_when_sshfs_is_mounted)
*   [7 See also](#See_also)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [sshfs](https://www.archlinux.org/packages/?name=sshfs) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

### Монтирование

**Совет:** Можно использовать [Google Authenticator](/index.php/Google_Authenticator_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Google Authenticator (Русский)") c sshfs для дополнительной безопасности.

Перед монтированием, убедитесь, что права целевой директории позволяют получать к ней надлежащий доступ. Для монтирования удаленной директории, выполните:

```
$ sshfs _USERNAME@HOSTNAME_OR_IP:/REMOTE_PATH LOCAL_MOUNT_POINT SSH_OPTIONS_

```

Например:

```
$ sshfs sessy@mycomputer:/remote/path /local/path -C -p 9876 -o allow_other

```

Где `-p 9876` является номером порта, `-C` - использование сжатия и `-o allow_other` дает разрешение обычным пользователям доступ к чтению/записи.

**Обратите внимание:** Пользователи также могут задать нестандартный порт в host-by-host конфигурации в `~/.ssh/config`, чтобы избежать параметра -p. Для получения дополнительной информации см. [Secure Shell (Русский)#Сохранение данных о подключении в конфигурационном файле ssh](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D0.BE_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B8_.D0.B2_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D0.BE.D0.BC_.D1.84.D0.B0.D0.B9.D0.BB.D0.B5_ssh "Secure Shell (Русский)")

SSH запросит пароль, если необходимо. Если вы не хотите постоянно вводить пароль, прочитайте: [как использовать ключ аутентификации RSA с SSH](http://linuxmafia.com/~karsten/Linux/FAQs/sshrsakey.html) или [SSH Keys](/index.php/SSH_keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH keys (Русский)").

**Совет:** Чтобы быстро смонтировать удаленную директорию, сделать нужные файловые манипуляции и отмонтировать ее, добавьте в скрипт следующее:

```
sshfs USERNAME@HOSTNAME_OR_IP:/REMOTE_PATH LOCAL_MOUNT_POINT SSH_OPTIONS
mc LOCAL_MOUNT_POINT
fusermount -u LOCAL_MOUNT_POINT

```

Скрипт смонтирует удаленный каталог, запустит MC и отмонтирует при выходе.

### Размонтирование

Чтобы отмонтировать удаленную систему:

```
$ fusermount -u _LOCAL_MOUNT_POINT_

```

Например:

```
$ fusermount -u /mnt/sessy

```

## Изменение корневого каталога

Вы можете привязать (определенного) пользователя к определенной директории путем редактирования `/etc/ssh/sshd_config`:

 `/etc/ssh/sshd_config` 

```
.....
Match User someuser 
       ChrootDirectory /chroot/%u
       ForceCommand internal-sftp #ограничить пользователя только в sftp
       AllowTcpForwarding no
       X11Forwarding no
.....
```

**Обратите внимание:** Вы должны запускать команду chroot c правами суперпользователя, иначе вы не сможете подключиться. Обратитесь к страницам man для получения дополнительной информации по `Match, ChrootDirectory` и `ForceCommand`.

## Вспомогательные программы

Если вам часто приходится монтировать файловые системы sshfs, то вас может заинтересовать sshfs помощник, такой как [sftpman](/index.php/Sftpman "Sftpman").

Доступ к нему можно получить при помощи интерфейса командной строки или GTK-интерфейса. Монтирование/размонтирование выполняется одной/одним командой/кликом.

## Автоматическое монтирование

Автоматическое монтирование происходит при загрузке или по запросу (для получения доступа к директории). В обоих случаях настройка будет происходить в `/etc/[fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")`.

**Обратите внимание:** Запомните, что автоматическое монтирование выполняется с правами суперпользователя, поэтому вы не можете использовать `.ssh/config` вашего пользователя.

Чтобы разрешить суперпользователю использовать ключ SSH обычного пользователя, нужно указать полный путь в опции `IdentityFile`.

**Самое главное** - используйте хотя бы раз каждую примонтированную файловую систему sshfs **в режиме суперпользователя**, таким образом сигнатуры хоста будут добавлены в файл `.ssh/known_hosts`.

### По запросу

С помощью systemd возможно монтирование по запросу используя `/etc/fstab`.

Например:

```
user@host:/remote/folder /mount/point  fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,IdentityFile=/home/user/.ssh/id_rsa,allow_other,reconnect 0 0

```

Главные опции здесь - _noauto,x-systemd.automount,_netdev_.

*   _noauto_ - монтирование не будет происходит при загрузке.
*   _x-systemd.automount_ - делает магию связанную с запросом.
*   __netdev_ - показывает, что это сетевое устройство, а не блочное (без этой опции может появится ошибка "No such device")

**Совет:**

Существует еще 2 способа для создания такого типа монтирования. Они не требуют редактировать `/etc/fstab`, чтобы создать новую точку монтирования. Вместо этого, обычные пользователи могут создавать точки монтирования, просто пытаясь получить к ним доступ (что-то вроде этого `ls ~/mnt/ssh/[user@]yourremotehost[:port]`):

*   [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/)<sup><small>AUR</small></sup> - использует AutoFS. Пользователям нужно включить ее при помощи `autosshfs-user`.
*   [afuse](https://aur.archlinux.org/packages/afuse/)<sup><small>AUR</small></sup> - универсальный пользовательский автомонтировщик для файловых систем FUSE. Он также прекрасно работает и с sshfs. Не требуется никаких активаций со стороны пользователя. Пример: `afuse -o mount_template='sshfs -o ServerAliveInterval=10 -o reconnect %r:/ %m' -o unmount_template='fusermount -u -z %m' ~/mnt/ssh`

### При загрузке

Пример того, как использовать sshfs для монтировании удаленной файловой системы при помощи `/etc/[fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")`

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs  defaults,_netdev  0  0

```

Для примера возьмите линию из _fstab_

```
llib@192.168.1.200:/home/llib/FAH  /media/FAH2  fuse.sshfs  defaults,_netdev  0  0

```

Выше приведенная строка будет работать только в том случае, если вы используете SSH ключ. Смотрите [SSH keys](/index.php/SSH_keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH keys (Русский)")

Если вы не единственный пользователь, использующий sshfs:

```
user@domain.org:/home/user  /media/user   fuse.sshfs    defaults,allow_other,_netdev    0  0

```

Очень важно убедится в том, что параметр монтирования __netdev_ установлен, чтобы быть уверенным в доступности сети перед монтированием.

### Безопасный доступ пользователей

Когда используется автомонтирование через `/etc/[fstab](/index.php/Fstab "Fstab")`, файловая система будет монтироваться от суперпользователя. По умолчанию, это приводит к нежелательным результатам, если вы хотите получать доступ как обычный пользователь и ограничить доступ другим пользователям.

Пример конфигурации:

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs noauto,x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/USERNAME/.ssh/id_rsa,allow_other,default_permissions,uid=USER_ID_N,gid=USER_GID_N 0 0

```

Описание опций:

*   _allow_other_ - позволяет другим пользователям отличным от монтирующего (т.е. суперпользователь) получать доступ к монтируемуму.
*   _default_permissions_ - позволяет ядру проверять права, т.е. использовать актуальные права на удаленной файловой системе. А также запрещает доступ всем, кроме объявленных в _allow_other_.
*   _uid_, _gid_ - устанавливает владельца файлов в соответствии с переданными значениями; _uid_ - это числовой идентификатор пользователя, _gid_ - числовой идентификатор группы пользователя.

## Параметры

sshfs может автоматически конвертировать ваш и удаленный идентификатор пользователя.

Добавьте параметр _idmap_ с значением _user_, чтобы переводить идентификатор подключаемого пользователя:

```
# sshfs -o idmap=user sessy@mycomputer:/home/sessy /mnt/sessy -C -p 9876

```

Это действие сопоставит идентификатор удаленного пользователя "sessy" с идентификатором локального пользователя, который запускает этот процесс ("суперпользователь" в примере выше) и идентификатор группы пользователя останется неизменным. Если вам требуется более точный контроль над переводом идентификатора пользователя и его группы, то посмотрите на параметры _idmap=file_, _uidfile_ и _gidfile_.

## Решение проблем

### Контрольный список

Для начала, прочитайте следующую страницу вики [SSH Checklist](https://wiki.archlinux.org/index.php/Secure_Shell#Checklist). Проблемы, которые следует проверить:

1\. Получает ли ваш логин SSH дополнительную информацию от сервера, например, такую как файл `/etc/issue`? Это может быть причиной некорректной работы SSHFS. Вас следует временно деактивировать данный файл:

```
$ mv /etc/issue /etc/issue.orig

```

2\. Имейте в виду, что большинство статей по устранению неполадок связанных с SSH, найденных в интернете, **не** связаны с Systemd. Часто определения в `/etc/fstab` ошибочно начинаются с `_sshfs#_user@host:/mnt/server/folder ... fuse ...` вместо того, чтобы использовать следующий синтаксис `user@host:/mnt/server/folder ... fuse._sshfs_ ... _x-systemd_, ...`.

3\. Убедитесь, что владелец исходной папки и ее содержимого на сервере владеет соответственный пользователь:

```
$ chown -R USER_S: /mnt/servers/folder

```

4\. Серверный пользовательский идентификатор может отличаться от соответствующего клиентского. Очевидно, что имена пользователей будут одинаковыми. Вам просто нужно позаботиться о клиентском идентификаторе. SSHFS будет преобразовывать идентификатор пользователя посредством следующего параметра:

```
uid=_USER_C_ID_,gid=_GROUP_C_ID_

```

5\. Проверьте, чтобы клиент имел права на целевую точку монтирования (каталог). Данная директория должна иметь такой же идентификатор, как в настройках монтирования SSHFS.

```
$ chown -R USER_C: /mnt/client/folder

```

6\. Проверьте, что точка монтирования (папка) пуста. По умолчанию вы не можете монтировать каталоги SSHFS в непустые директории.

7\. Если вы хотите автоматически монтировать объекты SSH используя публичный ключ аутентификации (без пароля) через `/etc/fstab`, то используйте следующую линию как пример;

```
_USER_S_@_SERVER_:/mnt/on/server      /nmt/on/client        fuse.sshfs      x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/_USER_C_/.ssh/id_rsa,allow_other,default_permissions,uid=_USER_C_ID_,gid=_GROUP_C_ID_,umask=0   0 0

```

и учитывая следующий пример настроек...

*   SERVER = Имя сервера (serv)
*   USER_S = Имя пользователя сервера (pete)
*   USER_C = Имя пользователя клиента (pete)
*   USER_S_ID = Идентификатор пользователя сервера (1004)
*   USER_C_ID = Идентификатор пользователя клиента (1000)
*   GROUP_C_ID = Идентификатор группы пользователя клиента (100)

Вы можете получить идентификатор пользователя и группы посредством следующей команды:

```
$ id ИМЯПОЛЬЗОВАТЕЛЯ

```

Вот конечная строка для монтирования SSHFS в `/etc/fstab`:

```
pete@serv:/mnt/on/server      /nmt/on/client        fuse.sshfs      x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/pete/.ssh/id_rsa,allow_other,default_permissions,uid=1004,gid=1000,umask=0   0 0

```

8\. Если вам известны еще проблемы для этого контрольного списка, то, пожалуйста, добавьте их выше.

### Connection reset by peer

*   If you are trying to access the remote system with a hostname, try using its IP address, as it can be a domain name solving issue. Make sure you edit `/etc/hosts` with the server details.
*   If you are using non-default key names and are passing it as `-i .ssh/my_key`, this will not work. You have to use `-o IdentityFile=/home/user/.ssh/my_key`, with the full path to the key.
*   If your /root/.ssh/config is a symlink, you will be getting this error as well. See [this serverfault topic](http://serverfault.com/questions/507748/bad-owner-or-permissions-on-root-ssh-config)
*   Adding the option '`sshfs_debug`' (as in '`sshfs -o sshfs_debug user@server ...`') can help in resolving the issue.
*   If that doesn't reveal anything useful, you might also try adding the option '`debug`'
*   If you are trying to sshfs into a router running DD-WRT or the like, there is a solution [here](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT). (note that the -osftp_server=/opt/libexec/sftp-server option can be used to the sshfs command in stead of patching dropbear)
*   Old Forum thread: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613)
*   Make sure your user can log into the server (especially when using AllowUsers)
*   Make sure `Subsystem sftp /usr/lib/ssh/sftp-server` is enabled in `/etc/ssh/sshd_config`.

**Note:** When providing more than one option for sshfs, they must be comma separated. Like so: '`sshfs -o sshfs_debug,IdentityFile=</path/to/key> user@server ...`')

### Remote host has disconnected

If you receive this message directly after attempting to use _sshfs_:

*   First make sure that the **remote** machine has _sftp_ installed! It will not work, if not.

**Tip:** If your remote server is running OpenWRT: `opkg install openssh-sftp-server` will do the trick

*   Then, try checking the path of the `Subsystem` listed in `/etc/ssh/sshd_config` on the remote machine to see, if it is valid. You can check the path to it with `find / -name sftp-server`.

For Arch Linux the default value in `/etc/ssh/sshd_config` is `Subsystem sftp /usr/lib/ssh/sftp-server`.

### Freezing apps (e.g. Nautilus, Gedit)

**Note:** This prevents the recently used file list from being populated and may lead to possible write errors.

If you experience freezing/hanging (stopped responding) applications, you may need to disable write-access to the `~/recently-used.xbel` file.

```
# chattr +i /home/USERNAME/.local/share/recently-used.xbel

```

See the following [bug report](https://bugs.archlinux.org/task/40260) for more details and/or solutions.

### Shutdown hangs when sshfs is mounted

Systemd may hang on shutdown if an sshfs mount was mounted manually and not unmounted before shutdown. To solve this problem, create this file (as root):

 `/etc/systemd/system/killsshfs.service` 

```
[Unit]
After=network.target

[Service]
RemainAfterExit=yes
ExecStart=-/bin/true
ExecStop=-/usr/bin/pkill sshfs

[Install]
WantedBy=multi-user.target

```

Then enable the service: `systemctl enable killsshfs.service`

## See also

*   [sftpman](/index.php/Sftpman "Sftpman") - sshfs helper tool
*   [SSH](/index.php/SSH "SSH")
*   [How to mount chrooted SSH filesystem](http://wiki.gilug.org/index.php/How_to_mount_SFTP_accesses), with special care with owners and permissions questions.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sshfs_(Русский)&oldid=415151](https://wiki.archlinux.org/index.php?title=Sshfs_(Русский)&oldid=415151)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Secure Shell (Русский)](/index.php/Category:Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Secure Shell (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")