## NFS

Для использования NFS в Arch Linux требуются установленные пакеты portmap и nfs-utils, бОльшая часть функциональности NFS уже содержится в ядре. Как подозревал FUBAR, идентификатор пользователя robert различается на двух машинах: uid=1000 на Arch и uid=1001 на Xandros. В NFS, я обошел это вставляя 'no_root_squash' в директивы экспорта /etc/exports, например:

```
/        hostname_DT(rw,no_root_squash,subtree_check)
/home    hostname_DT(rw,no_root_squash,subtree_check)
/mnt/sda5    hostname_DT(rw,no_root_squash,subtree_check)
/mnt/sda7    hostname_DT(rw,no_root_squash,subtree_check)

```

Используя NFS, также необходимо добавить строки в /etc/hosts.allow для некоторых демонов и программ, используемых NFS, специфичных адреса допущенные к использованию этих сервисов, например, для portmap:

```
portmap: 192.168.0.5, 192.168.0.7            # здесь должны использоваться IP адреса!

```

и тоже самое для nsfd, nfslock, lockd, rquotad, mountd, statd, mount, umount. На Xandros, эти два имеют различные имена: rpc.nsfd и rpc.mountd.

## FISH

Использовать FISH очень просто. Не требуется монтировать удаленные файловые системы, единственный момент, который требуется - чтобы на файл-сервере был запущен сервис sshd. То есть на Арче необходимо установить openssh и прописать сервис sshd в строку DAEMONS файла /etc/rc.conf. Необходимо остановить файервол для установления соединения, но после того, как соединение установлено, файервол можно перезапустить.

Также необходимо добавить строчку в /etc/hosts.allow с адресами машин, которым можно использовать sshd, т.е.:

```
sshd: 192.168.0.5, 192.168.0.7      (или  sshd: ALL )

```

и закомментировать строку "ALL: ALL: DENY" в Арчевом /etc/hosts.deny.

После этих действий, все, что необходимо сделать - ввести 'fish://root@сервер/' в адресную строку Konqueror'а для обыкновенного пользователя с запросом рутового пароля.

Недостаток FISH в периодических запросах пароля, но я предполагаю этого можно избежать, используя ключи SSH.

## SHFS

SHFS устанавливается и настраивается только на клиентской машине. Единственное требование к серверу - это установленный и работающий sshd. Если Вы на клиентском Арче, установите shfs (pacman -S shfs) и убедитесь, что на сервере отключен файервол и запущен sshd.

После установки создаём точку монтирования:

```
# mkdir -p /mnt/shfs

```

Установите suid bit на /usr/bin/shfsmount и /usr/bin/shfsumount если вы хотите позволить всем пользователям монтировать/размонтировать удалённые разделы используя shfs. Можете сделать это через Konqueror или командами

```
# chmod u+s /usr/bin/shfsmount
# chmod u+s /usr/bin/shfsumount

```

Права получатся такие: -rwsr-xr-x root root.

Монтируем удалённую файловую систему:

```
# shfsmount root@сервер:/ /mnt/shfs -o uid=пользователь

```

(или # mount -t shfs root@remote_hostname:/ /mnt/shfs -o uid=пользователь)

Использование опции -o uid=robert нужно из-за возможного несоответствия uid'ов пользователей на разных компьютерах.

В приглашение 'root@remote_hostname's password:' введите рутовый пароль. Теперь вы имеете доступ к удаленной файловой системе в качестве пользователя robert в директории /mnt/shfs, даже после рестарта файервола на удаленном сервере.

Как в случае с использованием FISH, для SHFS необходимо добавление адресов компьютеров, использующих sshd, т.е.:

```
sshd: 192.168.0.5, 192.168.0.7      #(или  sshd: ALL )

```

и закомментировать или удалить строку "ALL: ALL: DENY" в файле /etc/hosts.deny

Автор статьи не имеет достаточного опыта в предоставлении удаленного доступа к файлам и просит профессионалов в этой области дополнить статью.

note by cheer: вынесено с ветки форума [https://bbs.archlinux.org/viewtopic.php?id=26926](https://bbs.archlinux.org/viewtopic.php?id=26926)