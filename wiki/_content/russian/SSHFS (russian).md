Ссылки по теме

*   [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")
*   [Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")
*   [Secure Shell (Русский)](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)")
*   [sftpman](/index.php/Sftpman "Sftpman")

[SSHFS](https://github.com/libfuse/sshfs) - клиент файловой системы на основе FUSE для монтирования каталогов через [SSH](/index.php/SSH_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH (Русский)").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Монтирование](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [1.2 Размонтирование](#.D0.A0.D0.B0.D0.B7.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [2 Опции](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8)
*   [3 Изменение корневого каталога](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.B0)
*   [4 Автомонтирование](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [4.1 По запросу](#.D0.9F.D0.BE_.D0.B7.D0.B0.D0.BF.D1.80.D0.BE.D1.81.D1.83)
    *   [4.2 При загрузке](#.D0.9F.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
    *   [4.3 Безопасный доступ пользователей](#.D0.91.D0.B5.D0.B7.D0.BE.D0.BF.D0.B0.D1.81.D0.BD.D1.8B.D0.B9_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Контрольный список](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D1.81.D0.BF.D0.B8.D1.81.D0.BE.D0.BA)
    *   [5.2 Сброс соединения пиром](#.D0.A1.D0.B1.D1.80.D0.BE.D1.81_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D0.B8.D1.80.D0.BE.D0.BC)
    *   [5.3 Удаленный хост отключен](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_.D1.85.D0.BE.D1.81.D1.82_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD)
    *   [5.4 Зависание приложений (например, Gnome Files, Gedit)](#.D0.97.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.28.D0.BD.D0.B0.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80.2C_Gnome_Files.2C_Gedit.29)
    *   [5.5 Проблемы с монтированием fstab](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_fstab)
    *   [5.6 Не работает Git в примонтированной директории](#.D0.9D.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_Git_.D0.B2_.D0.BF.D1.80.D0.B8.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D0.BE.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B8)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [sshfs](https://www.archlinux.org/packages/?name=sshfs)

**Совет:** Если часто приходится монтировать файловые системы sshfs, то вас могут заинтересовать помощники sshfs, такие как [qsshfs](https://aur.archlinux.org/packages/qsshfs/), [sftpman](/index.php/Sftpman "Sftpman"), [sshmnt](https://aur.archlinux.org/packages/sshmnt/) или [fmount.py](https://github.com/lahwaacz/Scripts/blob/master/fmount.py).

### Монтирование

Для того, чтобы примонтировать каталог, используя SSH, пользователь должен иметь доступ к нему. Монтирование удаленной директории:

```
$ sshfs *[user@]host:[dir] mountpoint [options]*

```

Например:

```
$ sshfs myuser@mycomputer:/remote/path /local/path -C -p 9876

```

Где `-p 9876` является номером порта, `-C` - использование сжатия. Для дополнительных опций смотрите раздел [#Опции](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8).

Если не указан путь, то по умолчанию он указывает на удаленную домашнюю директорию пользователя. Имя пользователя по умолчанию и опции могут быть заданы в `~/.ssh/config`. Смотрите [Secure Shell#Client usage](/index.php/Secure_Shell#Client_usage "Secure Shell").

SSH запросит пароль, если необходимо. Если вы не хотите постоянно вводить пароль, прочитайте: [как использовать ключ аутентификации RSA с SSH](http://linuxmafia.com/~karsten/Linux/FAQs/sshrsakey.html) или [SSH Keys](/index.php/SSH_keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH keys (Русский)").

**Совет:** Можно использовать [Google Authenticator](/index.php/Google_Authenticator_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Google Authenticator (Русский)") c sshfs для дополнительной безопасности.

### Размонтирование

Чтобы размонтировать удаленную систему:

```
$ fusermount -u *local_mount_point*

```

Например:

```
$ fusermount -u /mnt/sessy

```

## Опции

*sshfs* может автоматически конвертировать ваш и удаленный идентификатор пользователя. Используйте параметр `idmap=user`, чтобы перевести UID подключаемого пользователя к удаленному пользователю `myuser` (GID остается нетронутым):

```
$ sshfs myuser@mycomputer:/remote/path /local/path -o idmap=user

```

Если вам требуется более точный контроль над переводом идентификаторов между локальным и удаленным пользователем, то обратите внимание на опции *idmap=file*, *uidfile* и *gidfile*.

## Изменение корневого каталога

Вы можете привязать определенного пользователя к конкретной директории на удаленной системе. Это может быть выполнено путем редактирования `/etc/ssh/sshd_config`:

 `/etc/ssh/sshd_config` 
```
.....
Match User "someuser"
       ChrootDirectory "/chroot/%u"
       ForceCommand internal-sftp
       AllowTcpForwarding no
       X11Forwarding no
.....
```

**Примечание:** Владельцем chroot директории **должен** быть суперпользователь, иначе вы не сможете подключиться.

Смотрите [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot"). Также обратите внимание в [sshd_config(5)](http://man7.org/linux/man-pages/man5/sshd_config.5.html) на `Match`, `ChrootDirectory` и `ForceCommand`.

## Автомонтирование

Автоматическое монтирование происходит при загрузке или по запросу (для получения доступа к каталогу). В любом случае настройка будет происходить в `/etc/[fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")`.

**Примечание:** Запомните, что автоматическое монтирование выполняется с правами суперпользователя, поэтому вы не можете использовать `.ssh/config` обычного пользователя.

Чтобы разрешить суперпользователю использовать ключ SSH обычного пользователя, нужно указать полный путь в опции `IdentityFile`.

**Самое главное** - используйте хотя бы раз каждую примонтированную файловую систему sshfs **в режиме суперпользователя**, таким образом подписи хоста будут добавлены в файл `/root/.ssh/known_hosts`.

### По запросу

Посредством systemd можно монтировать по запросу, используя `/etc/fstab`.

Например:

```
user@host:/remote/folder /mount/point  fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,IdentityFile=/home/user/.ssh/id_rsa,allow_other,reconnect 0 0

```

Главные опции - *noauto,x-systemd.automount,_netdev*.

*   *noauto* - монтирование не будет происходит при загрузке.
*   *x-systemd.automount* - делает магию, связанную с запросом.
*   *_netdev* - показывает, что это сетевое устройство, а не блочное (без этой опции может появится ошибка "No such device")

**Примечание:** После редактирования `/etc/fstab`, (пере)запустите соответствующий сервис: `systemctl daemon-reload && systemctl restart <цель>`; можно найти `<цель>`, используя `systemctl list-unit-files --type automount`

**Совет:**

Существует еще 2 способа для создания такого типа монтирования. Они не требуют редактирования `/etc/fstab` для создания новой точки монтирования. Вместо этого, обычные пользователи смогут создавать точки монтирования, просто пытаясь получить к ним доступ (например, `ls ~/mnt/ssh/[user@]yourremotehost[:port]`):

*   [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) - использует AutoFS. Пользователям нужно включить ее при помощи `autosshfs-user`.
*   [afuse](https://aur.archlinux.org/packages/afuse/) - универсальный пользовательский автомонтировщик для файловых систем FUSE. Он также прекрасно работает и с sshfs. Не требуется никаких активаций со стороны пользователя. Пример: `afuse -o mount_template='sshfs -o ServerAliveInterval=10 -o reconnect %r:/ %m' -o unmount_template='fusermount -u -z %m' ~/mnt/ssh`

### При загрузке

Пример того, как использовать sshfs для монтировании удаленной файловой системы при помощи `/etc/[fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")`

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs  defaults,_netdev  0  0

```

Для примера возьмите линию из *fstab*

```
llib@192.168.1.200:/home/llib/FAH  /media/FAH2  fuse.sshfs  defaults,_netdev  0  0

```

Выше приведенная строка будет работать только в том случае, если вы используете SSH ключ. Смотрите [SSH keys](/index.php/SSH_keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH keys (Русский)")

Если вы не единственный пользователь, использующий sshfs:

```
user@domain.org:/home/user  /media/user   fuse.sshfs    defaults,allow_other,_netdev    0  0

```

Очень важно убедится в том, что параметр *_netdev* установлен, чтобы быть уверенным в доступности сети перед монтированием.

### Безопасный доступ пользователей

Когда используется автомонтирование через `/etc/[fstab](/index.php/Fstab "Fstab")`, файловая система будет монтироваться от суперпользователя. По умолчанию, это приводит к нежелательным результатам, если вы хотите получать доступ как обычный пользователь и ограничить доступ другим пользователям.

Пример конфигурации:

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs noauto,x-systemd.automount,_netdev,user,idmap=user,follow_symlinks,identityfile=/home/USERNAME/.ssh/id_rsa,allow_other,default_permissions,uid=USER_ID_N,gid=USER_GID_N 0 0

```

Описание опций:

*   *allow_other* - позволяет другим пользователям, отличным от монтирующего (то есть обычным пользователям), получать доступ к тому, что монтируется.
*   *default_permissions* - позволяет ядру проверять права, иначе говоря использовать актуальные права на удаленной файловой системе. А также запрещает доступ всем, кроме объявленных в *allow_other*.
*   *uid*, *gid* - устанавливает владельца файлов в соответствии с переданными значениями; *uid* - это числовой идентификатор пользователя, *gid* - числовой идентификатор группы пользователя.

## Решение проблем

### Контрольный список

Для начала, прочитайте следующую страницу вики [Secure Shell (Русский)#Проверка](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0 "Secure Shell (Русский)"). Пункты, которые следует проверить:

1\. Получает ли ваш логин SSH дополнительную информацию от сервера, например, файл `/etc/issue`? Это может запутать SSHFS. Вам следует временно отключить серверный файл `/etc/issue`:

```
$ mv /etc/issue /etc/issue.orig

```

2\. Имейте в виду, что большинство статей по устранению неполадок, связанных с SSH, **не** связаны с Systemd. Часто определения в `/etc/fstab` ошибочно начинаются с `*sshfs#*user@host:/mnt/server/folder ... fuse ...` вместо того, чтобы использовать следующий синтаксис `user@host:/mnt/server/folder ... fuse.*sshfs* ... *x-systemd*, ...`.

3\. Убедитесь в том, что владелец исходной папки и ее содержимого на сервере владеет соответствующий пользователь:

```
$ chown -R USER_S: /mnt/servers/folder

```

4\. Серверный идентификатор пользователя может отличаться от соответствующего клиентского. Очевидно, что имена пользователей будут одинаковыми. Вам просто нужно позаботиться о клиентском идентификаторе. SSHFS будет преобразовывать идентификатор пользователя посредством следующего параметра:

```
uid=*USER_C_ID*,gid=*GROUP_C_ID*

```

5\. Проверьте, чтобы клиент имел права на целевую точку монтирования (каталог). Данная директория должна иметь такой же идентификатор, как в настройках монтирования SSHFS.

```
$ chown -R USER_C: /mnt/client/folder

```

6\. Проверьте, что точка монтирования (папка) пуста. По умолчанию, вы не можете монтировать каталоги SSHFS в непустые директории.

7\. Если вы хотите автоматически монтировать объекты SSH, используя публичный ключ аутентификации (без пароля), через `/etc/fstab`, то используйте следующую строчку, как пример:

```
*USER_S*@*SERVER*:/mnt/on/server      /nmt/on/client        fuse.sshfs      x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/*USER_C*/.ssh/id_rsa,allow_other,default_permissions,uid=*USER_C_ID*,gid=*GROUP_C_ID*,umask=0   0 0

```

и, учитывая следующий пример настроек...

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

### Сброс соединения пиром

*   Если вы пытаетесь получить доступ к удаленной машине, используя имя хоста, то попробуйте использовать ее адрес или доменной имя, смотря, что исправит проблему. Убедитесь в том, что вы изменили `/etc/hosts` в соответствии со свойствами сервера.
*   Если вы используете нестандартные имена ключей и передаете их как `-i .ssh/my_key`, то это не будет работать. Вам следует использовать `-o IdentityFile=/home/user/.ssh/my_key` с указанием полного пути к ключу.
*   Если ваш файл `/root/.ssh/config` является символической ссылкой, то вы получите сообщение об ошибке. Смотрите [эту тему](http://serverfault.com/questions/507748/bad-owner-or-permissions-on-root-ssh-config)
*   Добавление опции '`sshfs_debug`' (как в '`sshfs -o sshfs_debug user@server ...`') может помочь в решении проблемы.
*   Если это не помогло выявить ничего полезного, то вы можете также попробовать добавить опцию '`debug`'
*   Если вы пытаетесь использовать sshfs в роутере, работающем на DD-WRT или чем-то подобном, то решение проблемы [здесь](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT). (обратите внимание, что опция osftp_server=/opt/libexec/sftp-server может быть использована в командах SSH вместо патча dropbear)
*   Старая тема на форуме: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613).
*   Убедитесь, что ваш пользователь можешь зайти на сервер (особенно при использовании AllowUsers).
*   Убедитесь в том, что `Subsystem sftp /usr/lib/ssh/sftp-server` включен в `/etc/ssh/sshd_config`.

**Примечание:** Когда вы посылаете больше одного аргумента в sshfs, они должны разделяться запятыми. Например: '`sshfs -o sshfs_debug,IdentityFile=</path/to/key> user@server ...`')

### Удаленный хост отключен

Если это сообщение появляется непосредственно после попытки использовать *sshfs*:

*   Сначала убедитесь, что на удаленном компьютере установлен *sftp*! Ничего не будет работать, пока пакет не будет установлен.
*   Затем попробуйте проверить корректность пути к `Subsystem sftp`, указанного в `/etc/ssh/sshd_config` на удаленной машине.

### Зависание приложений (например, Gnome Files, Gedit)

**Важно:** Этот способ предотвращает от загрязнения список последних использованных файлов и может привести к возможным ошибкам записи.

Если у вас зависают (не отвечают) приложения, вам, возможно, придется отключить защиту от записи файлу `~/recently-used.xbel`.

```
# chattr +i /home/USERNAME/.local/share/recently-used.xbel

```

Смотрите следующий [отчет об ошибке](https://bugs.archlinux.org/task/40260) для более подробной информации и/или решения.

### Проблемы с монтированием fstab

Для получения подробной отладочной информации, добавьте следующее в параметры монтирования:

```
ssh_command=ssh\040-vv,sshfs_debug,debug

```

**Note:** `\040` - пробел, используемый fstab для разделения полей.

Чтобы видеть отладочную информацию, запустив при этом `mount -av`, удалите следующее:

```
noauto,x-systemd.automount

```

### Не работает Git в примонтированной директории

Выполняя некоторые операции в репозитории Git, примонтированном через SSHFS, вы можете получить следующую ошибку:

```
fatal: cannot update the ref 'HEAD': unable to append to '.git/logs/HEAD': Invalid argument

```

Ее можно исправить, добавив флаг `-o writeback_cache=no` в команду монтирования

Это было введено в sshfs 3.2 и, по-видимому, является фичей, а не багом. Для получения дополнительной информации смотрите [FS#55242](https://bugs.archlinux.org/task/55242) и [sshfs#82](https://github.com/libfuse/sshfs/issues/82).

## Смотрите также

*   [sftpman](/index.php/Sftpman "Sftpman") - помощник sshfs
*   [SSH](/index.php/SSH "SSH")
*   [Как монтировать файловую систему SSH, находящуюся в chroot-среде](http://wiki.gilug.org/index.php/How_to_mount_SFTP_accesses), с специальными владельцами и вопросами доступа.