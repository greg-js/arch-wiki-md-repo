Пользователи и группы пользователей используются на GNU/Linux для управления доступом — то есть, для управления доступом к системным файлам, каталогам и переферии. Linux предлагает относительно простые и грубые механизмы контроля доступа по умолчанию. Для более продвинутых вариантов, см. [ACL](/index.php/ACL "ACL") и [LDAP Authentication](/index.php/LDAP_Authentication "LDAP Authentication")

## Contents

*   [1 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
*   [2 Права и собственность](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B0_.D0.B8_.D1.81.D0.BE.D0.B1.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
*   [3 Управление пользователями](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F.D0.BC.D0.B8)
*   [4 Управление группами](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B0.D0.BC.D0.B8)
*   [5 Groups](#Groups)

## Обзор

*Пользователь* это любой кто использует компьютер. Имена пользователей могут быть любыми, например Mary или Bill, или псевдонимы вместо реальных имен, например Dragonlady или Pirate. Единственное что важно — это то что у компьютера есть имя для каждого созданного аккаунта, и то, что это имя, с помощью которого человек получает доступ к компьютеру. Некоторые службы и программы также запускаются с ограниченными или полными правами.

Управление аккаунтами пользователей используется в целях безопасности, ограничивая доступ несколькими способами.

Любой человек может иметь один и более аккаунт, поэтому каждому аккаунту должно соответствовать уникальное имя. Также есть несколько зарезервированных имен, которые нельзя использовать, например "root", "hal", и "adm".

Пользователи могут быть объединены в группы, и в зависимости от того в каких группах состоят пользователи их привилегии будут различаться.

**Примечание:** Новичкам стоит использовать эти инструменты аккуратно и воздержаться от изменения уже созданных аккаунтов, кроме своего.

## Права и собственность

From [In UNIX Everything is a File](http://ph7spot.com/musings/in-unix-everything-is-a-file):

	*ОС семейства UNIX созданы следуя нескольким единым идеям и концептам, которые отразились в их дизайне, интерфейсе, культуре и эволюции. Одна из важнейших таких идей: "все - это файл"*

	*Этот ключевой принцип состоит в предоставлении единой парадигмы для доступа к широкому кругу устройств ввода/вывода: документы, директории, жесткие диски, CD-диски, модемы, клавиотуры, принтеры, мониторы, терминалы и даже некоторые межпроцессовые взаимодействия и сетевые соединения. Фокус в том, чтобы предоставить простые абстракции для всех этих ресурсов, каждую из которых отцы UNIX назвали "файлом". Так как доступ к любому "файлу" можно получить через один и тот же интерфейс(API, не путать с GUI), вы можете использовать один и тот же набор базовых команд для чтения/записи диска, клавиатуры документа или сетевого устройства.*

```
[Extending UNIX File Abstraction for General-Purpose Networking](http://www.intel-research.net/Publications/Pittsburgh/101220041324_277.pdf):

```

	*A fundamental and very powerful, consistent abstraction provided in UNIX and compatible operating systems is the file abstraction. Many OS services and device interfaces are implemented to provide a file or file system metaphor to applications. This enables new uses for, and greatly increases the power of, existing applications — simple tools designed with specific uses in mind can, with UNIX file abstractions, be used in novel ways. A simple tool, such as cat, designed to read one or more files and output the contents to standard output, can be used to read from I/O devices through special device files, typically found under the `/dev` directory. On many systems, audio recording and playback can be done simply with the commands, "`cat /dev/audio > myfile`" and "`cat myfile > /dev/audio`," respectively.*

Каждый файл в системе GNU/Linux принадлежит определённому пользователю и группе. Также следует отметить, что существует три типа доступа к файлу: чтение, запись, и выполнение. Различные типы доступа могут быть применены к пользователю и группе, владеющими файлом, а так же всем остальным (не являющимся владельцами файла). Владельнцев файлов, а также права доступа можно определить с помощью команды `ls`:

 `$ ls -l /boot/` 
```
total 13740
drwxr-xr-x 2 root root    4096 Jan 12 00:33 grub
-rw-r--r-- 1 root root 8570335 Jan 12 00:33 initramfs-linux-fallback.img
-rw-r--r-- 1 root root 1821573 Jan 12 00:31 initramfs-linux.img
-rw-r--r-- 1 root root 1457315 Jan  8 08:19 System.map26
-rw-r--r-- 1 root root 2209920 Jan  8 08:19 vmlinuz-linux
```

Первая колонка отображает права доступа к файлу (например, файл `initramfs-linux.img` имеет права доступа `-rw-r--r--`). Третья и четвёртая колонки отображают пользователя и группу, владеющих файлом, соответственно. В этом примере, всеми файлами владеет пользователь *root*, а так же одноимённая группа: *root*.

 `$ ls /media/ -l` 
```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared
```

В этом примере, каталог `sf_Shared` принадлежит пользователю *root* и группе *vboxsf*. Также можно определить владельцев и права доступа используя команду `stat`:

Пользователь:

 `$ stat -c %U /media/sf_Shared/`  `root` 

Группа:

 `$ stat -c %G /media/sf_Shared/`  `vboxsf` 

Права доступа:

 `$ stat -c %A /media/sf_Shared/`  `drwxrwx---` 

Права доступа отображаются в виде трёх групп символов, представляющих права доступа пользователя, владеющего файлом, владеющей группы, и всех остальных соответственно. Например, символы `-rw-r--r--` означают, что владелец файла имеет право на чтение и запись, но не выполнение (`rw-`), в то время как пользователи, относящиеся к владеющей группе, и все остальные пользователи имеют лишь право на чтение (`r--` и `r--`). Между тем, символы `drwxrwx---` указывают на то, что владелец файла и прочие пользователи, относящиеся к владеющей группе, все имеют право на чтение, запись, и выполнение (`rwx` и `rwx`), тогда как остальные пользователи вообще не имеют никаких прав доступа к файлу (`---`). Первый символ означает тип файла: «d» — каталог, «-» — файл, «l» — ссылка.

Узнать список файлов, которыми владеет тот или иной пользователь и группа, можно с помощью команды `find`:

```
# find / -group [group]

```

```
# find / -user [user]

```

Пользователь и группа могут быть изменены с помощью команды `chown` (change owner). Права доступа к файлу могут быть изменены с помощью команды `chmod` (change mode).

See [man chown](http://linux.die.net/man/1/chown), [man chmod](http://linux.die.net/man/1/chmod), and [Linux file permissions](http://www.tuxfiles.org/linuxhelp/filepermissions.html) for additional detail.

## Управление пользователями

Информация о пользователях находится в файле `/etc/passwd`. Чтобы узнать список всех пользователей в системе:

```
$ cat /etc/passwd

```

На каждый аккаунт приходится по одной строке, имеющей следующий формат:

```
account:password:UID:GID:GECOS:directory:shell

```

где:

*   `account` — имя пользователя
*   `password` — пароль пользователя
*   `UID` — идентификационный номер пользователя
*   `GID` — идентификационный номер основной группы пользователя
*   `GECOS` — необязательное поле, используемое для указания дополнительной информации о пользователе (напирмер, полное имя пользователя)
*   `directory` — домашний каталог (`$HOME`) пользователя
*   `shell` — командный интерпретатор пользователя (обычно `/bin/sh`)

**Примечание:** Arch Linux использует *затенённые* пароли. Файл `passwd` доступен для чтения всем, поэтому хранить в нём пароли небезопасно. С целью сохранить секретность, в поле `password` находится символ `x`, указываюший на то, что пароль сохранён в файле с ограниченным доступом `/etc/shadow`.

Посмотреть список пользователей, вошедших в систему, можно с помощью команды `who`.

Чтобы добавить нового пользователя, следует использовать команды `useradd`:

```
# useradd -m -g [основная группа] -G [дополнительные группы] -s [командный интерпретатор] [имя пользователя]

```

*   **`-m`** — создаёт домашний каталог пользователя, вида `/home/[имя пользователя]`; в пределах которого, пользователь, не имеющий прав доступа root, может создавать и удалять файлы, устанавливать программы, и т. д.
*   **`-g`** — определяет имя или номер основной группы пользователя; группа должна существовать; номер группы должен относится к уже существующей группе; если параметр не указан, пользователю будет присвоена группа в соответствии с переменной `USERGROUPS_ENAB`, находящейся в `/etc/login.defs`.
*   **`-G`** — определяет список дополнительных групп, в которые входит пользователь; каждая группа отделяется от другой запятой без пробелов; по умолчанию пользователь принадлежит только основной группе.
*   **`-s`** — определяет командную оболочку пользователя; сценарии запуска Arch Linux используют Bash; после завершения запуска системы, командная оболочка будет той, что указана в данном параметре; при выборе отличного от Bash интерпретатора, убедитесь, что он установлен в систему.

Стандартный пример - добавление нового пользователя *archie*, с выбором баша в качестве оболочки и включением его в группы *wheel* и *audio*:

```
# useradd -m -g users -G wheel,audio -s /bin/bash archie

```

Для более продвинутых примеров, наберите:

```
$ man useradd

```

Для того, чтобы ввести полную информацию о пользователе (ФИО, и пр.), наберите:

```
# chfn [имя пользователя] option specifies that the user's home directory and mail spool should also be deleted

```

(при таком использовании `chfn` запускается в интерактивном режиме).

Для указания пароля пользователя, наберите:

```
# passwd [имя пользователя]

```

Также доступна интерактивная утилита для добавления пользователей:

```
# adduser

```

`adduser` запрашивает различную информацию о пользователе, и составляет команду для `useradd`. Также включает в себя действия, выполняемые `chfn` и `passwd`.

Удаление пользователей выполняется командой `userdel`.

```
# userdel -r [имя пользователя]

```

Опция `-r` также удаляет домашнюю директорию и почту пользователя.

## Управление группами

`/etc/group` - файл, хранящий информацию о группах пользователей.

Чтобы отобразить группы, в которые включен пользователь, можно использовать команду `groups`:

```
$ groups [имя пользователя]

```

Если имя пользователя не указано, команда отобразит группы текущего пользователя.

Используя команду `id` можно получить дополнительную информацию, такую как ID пользователя и его групп (UID и GID):

```
$ id [имя пользователя]

```

Отобразить список всех групп:

```
$ cat /etc/group

```

Добавить новую группу командой `groupadd`:

```
# groupadd [имя группы]

```

Добавить пользователя в группу, команда `gpasswd`:

```
# gpasswd -a [имя пользователя] [имя группы]

```

Удалить группу:

```
# groupdel [имя группы]

```

Убрать пользователя из группы:

```
# gpasswd -d [имя пользователя] [имя группы]

```

Пользователю необходимо перезайти в систему, чтобы изменения вступили в силу.

## Groups

Workstation/desktop users often add their non-root user to the following groups to allow access to peripherals and other hardware and facilitate system administration:

*   audio
*   floppy
*   lp
*   network
*   optical
*   power
*   storage
*   video
*   wheel

<caption>A list of groups and their function (sorted alphabetically)</caption>
| Group | Affected files | Purpose |
| adm | `/var/log/*` | Read access to log files. |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | Access to sound hardware. |
| avahi |
| bin | `/usr/bin/*` | Right to modify binaries only by root, but right to read or executed by anyone. (Please modify this for better understanding...) |
| camera | Access to [Digital Cameras](/index.php/Digital_Cameras "Digital Cameras"). |
| clamav | `/var/lib/clamav/*`, `/var/log/clamav/*` | Used by [Clam AntiVirus](/index.php/Clam_AntiVirus "Clam AntiVirus"). |
| daemon |
| dbus | `/var/run/dbus/*` |
| disk | `/dev/sda[1-9]`, `/dev/sdb[1-9]` | Access to block devices not affected by other groups such as optical, floppy, and storage. |
| floppy | `/dev/fd[0-9]` | Access to floppy drives. |
| ftp | `/srv/ftp` |
| games | `/var/games` | Access to some game software. |
| gdm |
| hal | `/var/run/hald`, `/var/cache/hald` |
| http |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | Right to use `updatedb` command. |
| log | `/var/log/*` | Access to log files in `/var/log`, |
| lp | `/etc/cups`, `/var/log/cups`, `/var/cache/cups`, `/var/spool/cups` | Access to printer hardware; enables the user to manage print jobs. |
| mem |
| mail | `/usr/bin/mail` |
| network | Right to change network settings such as when using [NetworkManager](/index.php/NetworkManager "NetworkManager"). |
| networkmanager | Requirement for your user to connect wirelessly with [NetworkManager](/index.php/NetworkManager "NetworkManager"). This group is not included with Arch by default so it must be added manually. |
| nobody | Unprivileged group. |
| ntp |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | Access to optical devices such as CD and DVD drives. |
| policykit |
| power | Right to use [suspend](/index.php/Pm-utils "Pm-utils") utilities and power management controls. |
| rfkill |
| root | `/*` | Complete system administration and control (root, admin). |
| scanner | `/var/lock/sane` | Access to scanner hardware. |
| smmsp | `sendmail` group |
| storage | Access to removable drives such as USB hard drives, flash/jump drives, MP3 players; enables the user to mount storage devices through [HAL](/index.php/HAL "HAL") and [D-Bus](/index.php/D-Bus "D-Bus"). |
| stb-admin |
| sys | Right to admin printers in [CUPS](/index.php/CUPS "CUPS"). |
| thinkpad | `/dev/misc/nvram` | Used by ThinkPad users for access to tools such as [tpb](/index.php/Tpb "Tpb"). |
| tty | `/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx` | Eg. to acces /dev/ACMx |
| users | Standard users group. |
| uucp | `/dev/ttyS[0-9]`, `/dev/tts/[0-9]` | Serial and USB devices such as modems, handhelds, RS-232/serial ports. |
| vboxusers | `/dev/vboxdrv` | Right to use [VirtualBox](/index.php/VirtualBox "VirtualBox") software. |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | Access to video capture devices, DRI/3D hardware acceleration ([X](/index.php/Xorg "Xorg") can be used *without* belonging to this group). |
| vmware | Right to use [VMware](/index.php/VMware "VMware") software. |
| wheel | Right to use [sudo](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)") (setup with `visudo`), also affected by PAM. |