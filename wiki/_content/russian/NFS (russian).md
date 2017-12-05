Related articles

*   [NFS/Troubleshooting](/index.php/NFS/Troubleshooting "NFS/Troubleshooting")

Взято с [Wikipedia](https://en.wikipedia.org/wiki/Network_File_System "wikipedia:Network File System"):

	*Сетевая файловая система (NFS) - это протокол распределенной файловой системы, первоначально разработанный Sun Microsystems в 1984 году, позволяющий пользователю на клиентском компьютере получать доступ к файлам по сети таким же образом, как и к доступу к локальному хранилищу.*

**Примечание:**

*   NFS не зашифрован. При работе с конфиденциальными данными чтобы шифровать протокол NFS нужно использовать туннель, например [Kerberos](/index.php/Kerberos "Kerberos") или [tinc](/index.php/Tinc "Tinc").
*   В отличие от [Samba](/index.php/Samba "Samba"), NFS по умолчанию не имеет аутентификации пользователя, доступ к клиенту ограничен по их IP-адресам / [hostname](/index.php/Hostname "Hostname").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.1 Сервер](#.D0.A1.D0.B5.D1.80.D0.B2.D0.B5.D1.80)
        *   [2.1.1 Запуск сервера](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
        *   [2.1.2 Разное](#.D0.A0.D0.B0.D0.B7.D0.BD.D0.BE.D0.B5)
            *   [2.1.2.1 Дополнительная конфигурация](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
            *   [2.1.2.2 Ограничение NFS для интерфейсов/IP](#.D0.9E.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_NFS_.D0.B4.D0.BB.D1.8F_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.BE.D0.B2.2FIP)
            *   [2.1.2.3 Убедиться что NFSv4 idmapping полностью включена](#.D0.A3.D0.B1.D0.B5.D0.B4.D0.B8.D1.82.D1.8C.D1.81.D1.8F_.D1.87.D1.82.D0.BE_NFSv4_idmapping_.D0.BF.D0.BE.D0.BB.D0.BD.D0.BE.D1.81.D1.82.D1.8C.D1.8E_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B0)
            *   [2.1.2.4 Статические порты для NFSv3](#.D0.A1.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BF.D0.BE.D1.80.D1.82.D1.8B_.D0.B4.D0.BB.D1.8F_NFSv3)
            *   [2.1.2.5 Совместимость NFSv2](#.D0.A1.D0.BE.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.B8.D0.BC.D0.BE.D1.81.D1.82.D1.8C_NFSv2)
            *   [2.1.2.6 Конфигурация брандмауэра](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.B1.D1.80.D0.B0.D0.BD.D0.B4.D0.BC.D0.B0.D1.83.D1.8D.D1.80.D0.B0)
    *   [2.2 Клиент](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82)
        *   [2.2.1 Ручная установка](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
        *   [2.2.2 Монтирование с использованием /etc/fstab](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_.2Fetc.2Ffstab)
        *   [2.2.3 Монтирование с использованием /etc/fstab и systemd](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_.2Fetc.2Ffstab_.D0.B8_systemd)
        *   [2.2.4 Монтирование с использованием autofs](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_autofs)
*   [3 Подсказки и трюки](#.D0.9F.D0.BE.D0.B4.D1.81.D0.BA.D0.B0.D0.B7.D0.BA.D0.B8_.D0.B8_.D1.82.D1.80.D1.8E.D0.BA.D0.B8)
    *   [3.1 Настройка производительности](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
    *   [3.2 Автоматизация общих ресурсов с помощью systemd-networkd](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D0.BE.D0.B1.D1.89.D0.B8.D1.85_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D0.BE.D0.B2_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_systemd-networkd)
    *   [3.3 Автоматическое управление монтированием](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC)
        *   [3.3.1 Cron](#Cron)
        *   [3.3.2 systemd/Timers](#systemd.2FTimers)
        *   [3.3.3 Монтирование при запуске через systemd](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_systemd)
        *   [3.3.4 Диспетчер NetworkManager](#.D0.94.D0.B8.D1.81.D0.BF.D0.B5.D1.82.D1.87.D0.B5.D1.80_NetworkManager)
        *   [3.3.5 Монтирование NFS и networkmanager](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_NFS_.D0.B8_networkmanager)
*   [4 Устранение неполадок](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
    *   [4.1 Из старого wiki (нужно проверить)](#.D0.98.D0.B7_.D1.81.D1.82.D0.B0.D1.80.D0.BE.D0.B3.D0.BE_wiki_.28.D0.BD.D1.83.D0.B6.D0.BD.D0.BE_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.B8.D1.82.D1.8C.29)
    *   [4.2 soft или hard монтирование](#soft_.D0.B8.D0.BB.D0.B8_hard_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)

## Установка

Для установки сервера и клиента достаточно установить пакет [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

Настоятельно рекомендуется на всех узлах (клиентских и серверных) использовать системы синхронизации времени [time sync daemon](/index.php/Time#Time_synchronization "Time"). Без точной синхронизации системного времени, в процессе функционирования NFS возможно возникновение дополнительных нежелательных задержек.

**Примечание:** Пакет [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) для архитектуры ARM, начиная с версии 1.3.2-4 (а возможно и с более ранних версий) имеет некоторые отличия в функционировании от версий для архитектур x86_64 или i686\. Более детальную информацию о монтировании клиентских узлов можно найти на странице обсуждения dicsussion

## Конфигурация

### Сервер

Серверу NFS нужен список экспорта (общие каталоги), которые определены в `/etc/exports`. Шары NFS, определенные в `/etc/exports`, относятся к так называемому корню NFS. Хорошей практикой безопасности является определение корня NFS в дискретном дереве каталогов в корневой файловой системе сервера, который будет ограничивать пользователей этой точкой монтирования. Bind mounts are used to link the share mount point to the actual directory elsewhere on the filesystem.

Рассмотрим следующий пример, в котором:

1.  Корень NFS `/srv/nfs`.
2.  Экспорт `/srv/nfs/music` через привязку к фактической цели `/mnt/music`.

```
# mkdir -p /srv/nfs/music /mnt/music
# mount --bind /mnt/music /srv/nfs/music

```

Чтобы монтирование выполнялось автоматически, добавьте строчки в `fstab`:

 `/etc/fstab` 
```
/mnt/music /srv/nfs/music  none   bind   0   0

```

**Примечание:** The permissions on the server filesystem is what NFS will honor so ensure that connecting users have the desired access.

**Примечание:** [ZFS](/index.php/ZFS "ZFS") filesystems require special handling of bindmounts, see [ZFS#Bind mount](/index.php/ZFS#Bind_mount "ZFS").

Добавьте каталоги для совместного использования и ограничьте их диапазоном адресов CIDR или имя хоста клиентских машин, которым будет разрешено устанавливать их в `/etc/exports`:

 `/etc/exports` 
```
/srv/nfs       192.168.1.0/24(rw,fsid=root,crossmnt)
/srv/nfs/music 192.168.1.0/24(rw) # чтение и запись для всех с диапазоном IP 192.168.1.*

```
 `/etc/exports` 
```
/srv/nfs *(ro,sync) # Только чтение для всех access to anyone
/srv/nfs/music 192.168.0.2(rw,sync) # Чтение и запись для клиента с IP 192.168.0.2
/srv/nfs/music 192.168.1.1/24(rw,sync) # Чтение и запись для всех клиентов с 192.168.1.1 по 192.168.1.255

```

Если вы хотите сделать ваш разделённый NFS каталог открытым и с правом записи, вы можете использовать опцию all_squash в комбинации с опциями anonuid и anongid.

Например, чтобы установить права для пользователя 'nobody' в группе 'nobody', вы можете сделать следующее:

```
; Доступ на чтение и запись для клиента на 192.168.0.100, с доступом rw для пользователя 99 с gid 99
/files 192.168.0.100(rw,sync,all_squash,anonuid=99,anongid=99))

```

Это также означает, что если вы хотите разрешить доступ к указанной директории, nobody.nobody должен быть владельцем разделённой директории:

```
# chown -R nobody.nobody /files

```

Следует отметить, что изменение `/etc/exports` во время работы сервера потребует повторного экспорта, чтобы изменения вступили в силу выполните:

```
# exportfs -rav

```

Для получения дополнительной информации обо всех доступных опциях см. [exports(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/exports.5).

**Совет:** [ip2cidr](http://ip2cidr.com/) - это инструмент для преобразования диапазонов IP-адресов в корректно структурированную спецификацию CDIR.

**Примечание:** Если целевой экспорт является файловой системой tmpfs, требуется опция `fsid=1`.

#### Запуск сервера

[Start](/index.php/Start "Start") и [enable](/index.php/Enable "Enable") `nfs-server.service`.

#### Разное

##### Дополнительная конфигурация

Расширенные параметры конфигурации могут быть установлены в `/etc/nfs.conf`. Пользователям, настраивающим простую конфигурацию, может не понадобиться редактировать этот файл.

##### Ограничение NFS для интерфейсов/IP

По умолчанию запуск `nfs-server.service` будет прослушивать подключения на всех сетевых интерфейсах, независимо от `/etc/exports`. Это можно изменить, указав, какие IP-адреса и / или имена хостов должны прослушиваться.

 `/etc/nfs.conf` 
```
[nfsd]
host=192.168.1.123
# Кроме того, вы можете использовать имя хоста.
# host=myhostname
```

Изменения будут применены при повторном запуске службы.

```
# systemctl restart nfs-server.service

```

##### Убедиться что NFSv4 idmapping полностью включена

Несмотря на то, что idmapd может работать, он может быть не полностью включен. Убедитесь, что `/sys/module/nfsd/parameters/nfs4_disable_idmapping` возвращает `N` когда не запушен:

Установите в качестве [module option](/index.php/Kernel_modules#Setting_module_options "Kernel modules"), чтобы сделать изменение постоянными, пример:

 `/etc/modprobe.d/nfsd.conf` 
```
options nfsd nfs4_disable_idmapping=0

```

##### Статические порты для NFSv3

Пользователям, нуждающимся в поддержке клиентов NFSv3, может потребоваться использование статических портов. По умолчанию для операций NFSv3 `rpc.statd` и `lockd` используются случайные эфемерные порты; чтобы разрешить операции NFSv3 через статические порты брандмауэра. Измените `/etc/sysconfig/nfs`, чтобы установить `STATDARGS`:

 `/etc/sysconfig/nfs`  `STATDARGS="-p 32765 -o 32766 -T 32803"` 

Для нормальной работы `rpc.mountd` должен обращаться к `/etc/services` и привязываться к одному и тому же статическому порту 20048; однако, если для определения `/etc/sysconfig/nfs` должно быть определено значение `RPCMOUNTDARGS`:

 `/etc/sysconfig/nfs`  `RPCMOUNTDARGS="-p 20048"` 

После внесения этих изменений необходимо перезапустить несколько служб; первый записывает параметры конфигурации в `/run/sysconfig/nfs-utils` (см. `/usr/lib/systemd/scripts/nfs-utils_env.sh`), второй перезапускает `rpc.statd` с новыми портами, последний перезагружает `lockd` (модуль ядра) с новыми портами.[Перезапустите](/index.php/Restart "Restart") эти службы: `nfs-config`, `rpcbind`, `rpc-statd` и `nfs-server`.

После перезапуска на сервере для проверки статических портов используйте `rpcinfo -p`. Использование `rpcinfo -p <server IP>` от клиента должно выявлять те же самые статические порты.

##### Совместимость NFSv2

Для пользователей которые используют клиенты NFSv2 (например, U-Boot), нужно установить `RPCNFSDARGS="-V 2"` в `/etc/sysconfig/nfs`.

##### Конфигурация брандмауэра

Чтобы разрешить доступ через брандмауэр, необходимо использовать tcp и udp-порты 111, 2049 и 20048 при использовании конфигурации по умолчанию; используйте `rpcinfo -p`, чтобы проверить точные порты, используемые на сервере. Чтобы настроить это для [iptables](/index.php/Iptables "Iptables"), выполните следующие команды:

```
# iptables -A INPUT -p tcp -m tcp --dport 111 -j ACCEPT
# iptables -A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT
# iptables -A INPUT -p tcp -m tcp --dport 20048 -j ACCEPT
# iptables -A INPUT -p udp -m udp --dport 111 -j ACCEPT
# iptables -A INPUT -p udp -m udp --dport 2049 -j ACCEPT
# iptables -A INPUT -p udp -m udp --dport 20048 -j ACCEPT

```

Чтобы загрузить эту конфигурацию при каждом запуске системы, отредактируйте `/etc/iptables/iptables.rules`:

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 111 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 20048 -j ACCEPT
-A INPUT -p udp -m udp --dport 111 -j ACCEPT
-A INPUT -p udp -m udp --dport 2049 -j ACCEPT
-A INPUT -p udp -m udp --dport 20048 -j ACCEPT

```

Предыдущие команды можно сохранить, выполнив следующие действия:

```
# iptables-save > /etc/iptables/iptables.rules

```

**Note:** Эта команда будет «отменять» текущую действующую конфигурацию запуска iptables на текущую выбранную

Если вы используете NFSv3 и перечисленные выше статические порты для `rpc.statd` и `lockd`, их также необходимо добавить в конфигурацию:

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 32765 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 32803 -j ACCEPT
-A INPUT -p udp -m udp --dport 32765 -j ACCEPT
-A INPUT -p udp -m udp --dport 32803 -j ACCEPT

```

При использовании только для V4 необходимо открыть только порт tcp 2049\. Поэтому нужна только одна строка.

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT

```

Чтобы применить изменения, [Restart](/index.php/Restart "Restart") `iptables.service`.

### Клиент

Пользователи, намеревающиеся использовать NFS4 с [Kerberos](/index.php/Kerberos "Kerberos"), также должны [start](/index.php/Start "Start") и [enable](/index.php/Enable "Enable") `nfs-client.target`, который запускает `rpc-gssd.service`. Однако из-за ошибки [FS#50663](https://bugs.archlinux.org/task/50663) в glibc `rpc-gssd.service` в настоящее время не запускается. Добавление флага "-f" (foreground) в службе является обходным путем:

 `# systemctl edit rpc-gssd.service` 
```
[Unit]
Requires=network-online.target
After=network-online.target

[Service]
Type=simple
ExecStart=
ExecStart=/usr/sbin/rpc.gssd -f
```

#### Ручная установка

Для NFSv3 используйте эту команду для отображения экспортированных файловых систем сервера:

```
# mount server:/ /mountpoint/on/client

```

Затем отключите сервер NFS для экспорта сервера:

```
# mount -t nfs -o vers=4 servername:/music /mountpoint/on/client

```

Если монтирование не выполняется, попробуйте включить root экспорта сервера (требуется для Debian/RHEL/SLES, для некоторых дистрибутивов требуется `-t nfs4` вместо `-t nfs`):

```
# mount -t nfs -o vers=4 servername:/srv/nfs/music /mountpoint/on/client

```

**Примечание:** Имя сервера должно быть допустимым именем хоста (а не только IP-адресом). В противном случае установка удаленного ресурса будет зависать.

#### Монтирование с использованием /etc/fstab

Использование [fstab](/index.php/Fstab "Fstab") полезно для сервера, который всегда включен и общие ресурсы NFS доступны всякий раз, когда клиент загружается. Измените файл `/etc/fstab` и добавьте соответствующую строку, отражающую настройку. Опять же, root экспорта NFS сервера опущен.

 `/etc/fstab` 
```
servername:/music   /mountpoint/on/client   nfs   rsize=8192,wsize=8192,timeo=14,_netdev	0 0

```

**Примечание:** Консультируйтесь [nfs(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/nfs.5) и [mount(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) для получения дополнительных параметров монтирования.

Некоторые дополнительные варианты монтирования, которые необходимо учитывать, включают:

	rsize и wsize

	значение `rsize` - это количество байтов, используемых при чтении с сервера. Значение `wsize` - это количество байтов, используемых при записи на сервер. Значение по умолчанию для обоих равно 1024, но использование более высоких значений, таких как 8192, может повысить пропускную способность. Это не универсально. Рекомендуется выполнить проверку после внесения этого изменения, см. [#Performance tuning](#Performance_tuning).

	timeo

	значение `timeo` - это время, в десятые доли секунды, для ожидания перед повторной отправкой передачи после таймаута RPC. После первого таймаута значение тайм-аута удваивается для каждой повторной попытки в течение максимум 60 секунд или до тех пор, пока не произойдет большой тайм-аут. Если вы подключаетесь к медленному серверу или по сети с занятостью, более высокая производительность может быть достигнута за счет увеличения этого значения таймаута.

	_netdev

	Опция `_netdev` сообщает системе ждать, пока сеть не поднимется, прежде чем пытаться установить общий ресурс. systemd предполагает это для NFS, но в любом случае это хорошая практика использовать его для всех типов сетевых файловых систем

**Примечание:** Установка шестого поля (`fs_passno`) на ненулевое значение может привести к неожиданному поведению, например. зависанию, когда systemd automount ждет подключения, которое никогда не произойдет.

#### Монтирование с использованием /etc/fstab и systemd

Другим методом является использование службы systemd `automount`. Это лучший вариант, чем `_netdev`, поскольку он быстро подключает сетевое устройство, когда соединение сломано и восстановлено. Кроме того, он решает проблему с помощью autofs, см. Пример ниже:

 `/etc/fstab`  `servername:/home   */mountpoint/on/client*  nfs  noauto,x-systemd.automount,x-systemd.device-timeout=10,timeo=14,x-systemd.idle-timeout=1min 0 0` 

Возможно, придется перезагрузить клиент, чтобы система systemd знала об изменениях в fstab. Кроме того, попробуйте [reloading](/index.php/Systemd#Using_units "Systemd") systemd и перезапустите `*mountpoint-on-client*.automount`, чтобы перезагрузить конфигурацию `/etc/fstab`.

**Tip:**

*   Параметр `noauto` не будет монтировать общий ресурс NFS до его обращения: используйте `auto`, чтобы он был доступен немедленно.
    Если у вас возникли проблемы с сбоем подключения из-за недоступности сети, [enable](/index.php/Enable "Enable") `NetworkManager-wait-online.service`. Это гарантирует, что `network.target` будет иметь все доступные ссылки до того, как они будут активны.
*   Параметр mount `users` позволит пользователям монтировать, но имейте в виду, что он подразумевает дополнительные опции, например, `noexec`.
*   Параметр `x-systemd.idle-timeout=1min` автоматически отключит общий ресурс NFS через 1 минуту неиспользования. Хорошо для ноутбуков, которые могут внезапно отключиться от сети.
*   Если выключение/перезагрузка выполняется слишком долго из-за NFS, [enable](/index.php/Enable "Enable") `NetworkManager-wait-online.service`, чтобы гарантировать, что NetworkManager не будет удален до того, как тома NFS будут размонтированы. Вы также можете попытаться добавить параметр `x-systemd.requires=network.target`, если выключение занимает слишком много времени.

**Примечание:** Пользователи, пытающиеся авторизовать общий ресурс NFS через systemd, который монтируется на сервере, могут быть заморожены при обработке больших объемов данных.

#### Монтирование с использованием autofs

Использование [autofs](/index.php/Autofs "Autofs") полезно, когда несколько компьютеров хотят подключиться через NFS; они могут быть как клиентами, так и серверами. Причина, по которой этот метод предпочтительнее предыдущего, заключается в том, что если сервер выключен, клиент не будет выдавать ошибки о том, что не может найти NFS-акции. Подробнее см. [autofs#NFS network mounts](/index.php/Autofs#NFS_network_mounts "Autofs").

## Подсказки и трюки

### Настройка производительности

Чтобы получить максимальную отдачу от NFS, необходимо настроить параметры монтирования `rsize` и `wsize` в соответствии с требованиями сетевой конфигурации.

В последних ядрах Linux (> 2.6.18) размер операций ввода-вывода, разрешенных сервером NFS (размер максимального размера по умолчанию), варьируется в зависимости от размера ОЗУ с максимальным размером 1M (1048576 байтов), максимальным размером блока сервер будет использоваться, даже если клиентам nfs требуется больше `rsize` и `wsize`. См. [Https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/5.8_Technical_Notes/Known_Issues-kernel.html](Https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/5.8_Technical_Notes/Known_Issues-kernel.html). Можно изменить размер максимального размера по умолчанию, разрешенный сервером, путем записи в `/proc/fs/nfsd/max_block_size` перед запуском *nfsd*. Например, следующая команда восстанавливает предыдущий iosize по умолчанию 32k:

```
# echo 32767 > /proc/fs/nfsd/max_block_size

```

Чтобы сделать изменение постоянным, создайте файл [systemd-tmpfile](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/nfsd-block-size.conf`  `w /proc/fs/nfsd/max_block_size - - - - 32768` 

### Автоматизация общих ресурсов с помощью systemd-networkd

Пользователи, использующие systemd-networkd, могут заметить, что nfs mounts fstab не монтируются при загрузке; появляются следующая ошибка:

```
mount[311]: mount.nfs4: Network is unreachable

```

Простое решение; force systemd ожидать, сеть будет полностью настроена с помощью [enabling](/index.php/Enabling "Enabling") `systemd-networkd-wait-online.service`. Теоретически это замедляет процесс загрузки, поскольку меньшее количество служб выполняется параллельно.

### Автоматическое управление монтированием

Этот трюк полезен для ноутбуков, которым требуются nfs-акции в беспроводной локальной сети. Если хост nfs становится недоступным, общий ресурс nfs будет размонтирован, чтобы надежно предотвратить зависание системы при использовании опции жесткого монтирования. См. [Https://bbs.archlinux.org/viewtopic.php?pid=1260240#p1260240](Https://bbs.archlinux.org/viewtopic.php?pid=1260240#p1260240).

Убедитесь, что точки монтирования NFS правильно указаны в `/etc/fstab`:

```
lithium:/mnt/data           /mnt/data	        nfs noauto,noatime,rsize=32768,wsize=32768 0 0
lithium:/var/cache/pacman   /var/cache/pacman	nfs noauto,noatime,rsize=32768,wsize=32768 0 0

```

**Примечание:** Для этого необходимо использовать имена хостов в `/etc/fstab`, а не IP-адреса.

Параметр mount `noauto` указывает systemd монтировать не автоматически общие ресурсы при загрузке. systemd в противном случае попытается установить общие ресурсы nfs, которые могут или не могут существовать в сети, что приведет к тому, что процесс загрузки закроется с пустым экраном.

Чтобы подключить общие ресурсы NFS с пользователями, не являющимися root, необходимо добавить параметр `user`.

Создайте сценарий `auto_share`, который будет использоваться *cron* или *systemd/Timers* для использования ICMP-пинга, чтобы проверить, доступен ли хост NFS:

 `/usr/local/bin/auto_share` 
```
#!/bin/bash

function net_umount {
  umount -l -f $1 &>/dev/null
}

function net_mount {
  mountpoint -q $1 || mount $1
}

NET_MOUNTS=$(sed -e '/^.*#/d' -e '/^.*:/!d' -e 's/\t/ /g' /etc/fstab | tr -s " ")$'
'b

printf %s "$NET_MOUNTS" | while IFS= read -r line
do
  SERVER=$(echo $line | cut -f1 -d":")
  MOUNT_POINT=$(echo $line | cut -f2 -d" ")

  # Check if server already tested
  if [[ "${server_ok[@]}" =~ "${SERVER}" ]]; then
    # The server is up, make sure the share are mounted
    net_mount $MOUNT_POINT
  elif [[ "${server_notok[@]}" =~ "${SERVER}" ]]; then
    # The server could not be reached, unmount the share
    net_umount $MOUNT_POINT
  else
    # Check if the server is reachable
    ping -c 1 "${SERVER}" &>/dev/null

    if [ $? -ne 0 ]; then
      server_notok[${#Unix[@]}]=$SERVER
      # The server could not be reached, unmount the share
      net_umount $MOUNT_POINT
    else
      server_ok[${#Unix[@]}]=$SERVER
      # The server is up, make sure the share are mounted
      net_mount $MOUNT_POINT
    fi
  fi
done

```

**Примечание:** Если вы хотите протестировать, используя TCP-запрос вместо ICMP-пинга (по умолчанию это tcp-порт 2049 в NFS4), то замените строку:
```
 # Check if the server is reachable
 ping -c 1 "${SERVER}" &>/dev/null

```

with:

```
 # Check if the server is reachable
 timeout 1 bash -c ": < /dev/tcp/${SERVER}/2049"

```
в сценарии `auto_share` выше.

```
# chmod +x /usr/local/bin/auto_share

```

Создайте запись cron или таймер systemd/Timers, чтобы проверять каждую минуту, что сервер доступен.

#### Cron

 `# crontab -e` 
```
* * * * * /usr/local/bin/auto_share

```

#### systemd/Timers

 `# /etc/systemd/system/auto_share.timer` 
```
[Unit]
Description=Check the network mounts

[Timer]
OnCalendar=*-*-* *:*:00

[Install]
WantedBy=timer.target

```
 `# /etc/systemd/system/auto_share.service` 
```
[Unit]
Description=Check the network mounts

[Service]
Type=simple
ExecStart=/usr/local/bin/auto_share

```

```
# systemctl enable auto_share.timer

```

#### Монтирование при запуске через systemd

Системный файл systemd также можно использовать для монтирования общих ресурсов NFS при запуске. Файл устройства не требуется, если NetworkManager установлен и настроен в клиентской системе. См. [#NetworkManager dispatcher](#NetworkManager_dispatcher).

 `/etc/systemd/system/auto_share.service` 
```
[Unit]
Description=NFS automount
After=syslog.target network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/local/bin/auto_share

[Install]
WantedBy=multi-user.target

```

Теперь [enable](/index.php/Enable "Enable") `auto_share.service`.

#### Диспетчер NetworkManager

В дополнение к описанному выше методу [NetworkManager](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") также можно настроить на запуск сценария при изменении статуса сети: [Enable](/index.php/Enable "Enable") и [start](/index.php/Start "Start") `NetworkManager-dispatcher.service`.

Самый простой способ для монтирования общих ресурсов при изменении статуса сети - просто привязать скрипт `auto_share`:

```
# ln -s /usr/local/bin/auto_share /etc/NetworkManager/dispatcher.d/30-nfs.sh

```

Однако в этом конкретном случае размонтирование произойдет только после того, как сетевое соединение уже отключено, что является нечистым и может привести к таким эффектам, как замораживание апплетов KDE Plasma.

Следующий сценарий безопасно отключает общие ресурсы NFS до отключения соответствующего сетевого подключения, прослушивая события `pre-down` и `vpn-pre-down`:

**Примечание:** Этот сценарий игнорирует mounts с параметром noauto.
 `/etc/NetworkManager/dispatcher.d/30-nfs.sh` 
```
#!/bin/bash

# Find the connection UUID with "nmcli con show" in terminal.
# All NetworkManager connection types are supported: wireless, VPN, wired...
WANTED_CON_UUID="CHANGE-ME-NOW-9c7eff15-010a-4b1c-a786-9b4efa218ba9"

if [[ "$CONNECTION_UUID" == "$WANTED_CON_UUID" ]]; then

    # Script parameter $1: NetworkManager connection name, not used
    # Script parameter $2: dispatched event

    case "$2" in
        "up")
            mount -a -t nfs4,nfs 
            ;;
        "pre-down");&
        "vpn-pre-down")
            umount -l -a -t nfs4,nfs >/dev/null
            ;;
    esac
fi

```

Сделайте скрипт исполняемым с помощью [chmod](/index.php/Chmod "Chmod") и создайте символическую ссылку внутри `/etc/NetworkManager/dispatcher.d/pre-down`, чтобы поймать события `pre-down`:

```
# ln -s /etc/NetworkManager/dispatcher.d/30-nfs.sh /etc/NetworkManager/dispatcher.d/pre-down.d/30-nfs.sh

```

Вышеупомянутый скрипт может быть изменен для монтирования разных разделов (даже отличных от NFS) для разных подключений.

См. Также: [NetworkManager#Use dispatcher to handle mounting of CIFS shares](/index.php/NetworkManager#Use_dispatcher_to_handle_mounting_of_CIFS_shares "NetworkManager").

#### Монтирование NFS и networkmanager

Автоматическое монтирование nfs при появлении сети и автоматическое её отмонтирование при её отсутствии. Для этого создадим файл /etc/NetworkManager/dispatcher.d/01ifupdown, в него запишем:

```
#!/bin/bash
      if [ `nm-tool|grep State|cut -f2 -d' '` == "connected" ]; then
              mount -t nfs %server%:%server_dir% %local_dir%
      else
              umount %local_dir%
      fi

```

Где %server% - ip адрес сервера nfs, %server_dir% - директория на сервере, которую требуется подмонтировать и %local_dir% - директория куда оно будет монтироваться.

## Устранение неполадок

Существует специальная статья [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting").

*   См. Также [Avahi](/index.php/Avahi "Avahi"), реализация Zeroconf, которая позволяет автоматически открывать общие ресурсы NFS.
*   HOWTO: [Diskless network boot NFS root](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")
*   [NFS Performance Management](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.prftungd/doc/prftungd/nfs_perf.htm)
*   [Microsoft Services for Unix NFS Client info](http://blogs.msdn.com/sfu/archive/2008/04/14/all-well-almost-about-client-for-nfs-configuration-and-performance.aspx)
*   [NFS on Snow Leopard](https://blogs.oracle.com/jag/entry/nfs_on_snow_leopard) (Dead Link => [Archive.org Mirror](https://web.archive.org/web/20151212160906/https://blogs.oracle.com/jag/entry/nfs_on_snow_leopard))

### Из старого wiki (нужно проверить)

/etc/hosts.allow

Чтобы разрешить доступ по сети к nfs серверу для IP 192.168.0.101, вам надо добавить следующие строчки в /etc/hosts.allow:

```
nfsd: 192.168.0.101/255.255.255.255
rpcbind: 192.168.0.101/255.255.255.255
mountd: 192.168.0.101/255.255.255.255

```

Что разрешить доступ всем из подсети 192.168.0.*, необходмио добавить:

```
nfsd: 192.168.0.0/255.255.255.0
rpcbind: 192.168.0.0/255.255.255.0
mountd: 192.168.0.0/255.255.255.0

```

Чтобы все машины могли иметь доступ, напишите в файл /etc/hosts.allow следующие строчки:

```
nfsd: ALL
rpcbind: ALL
mountd:ALL

```

Подробнее про настройку файла /etc/hosts.allow, смотрите, например, [http://www.die.net/doc/linux/man/man5/hosts.allow.5.html](http://www.die.net/doc/linux/man/man5/hosts.allow.5.html)

### soft или hard монтирование

Настройка клиента

nfs клиент может обрабатывать сбои сервера в работе. Есть две опции монтирования: hard и soft.

soft:

Если запрос на получение файла не выполнен, NFS клиент сообщит об ошибке процессу, который пытается получить доступ к файлу. Некоторые программы умеют это обрабатывать, большая же часть - нет. Разработчики nfs не рекомендуют использовать эту опцию; это прямой путь к повреждённым данным и потере информации.

hard:

Программа, осуществляющая доступ к файлу повиснет при смерти сервера. Процесс не может быть прерван или убит (только "sure kill"), пока вы не укажете опцию intr. Когда NFS сервер вернётся к работе, программа продолжит работу с того места, где остановилась. Разработчики NFS рекомендуют использование опций hard,intr со всеми монтируемые NFS файловые системы.

Смотрите man mount для подробной информации об опциях монтирования.