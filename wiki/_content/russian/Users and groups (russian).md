Пользователи и группы пользователей используются на GNU/Linux для управления доступом — то есть, для управления доступом к системным файлам, каталогам и периферии. Linux предлагает относительно простые и грубые механизмы контроля доступа по умолчанию. Для более продвинутых вариантов, см. [ACL](/index.php/ACL "ACL") и [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Обзор](#Обзор)
*   [2 Права и собственность](#Права_и_собственность)
*   [3 Управление пользователями](#Управление_пользователями)
*   [4 Управление группами](#Управление_группами)
*   [5 Группы](#Группы)
    *   [5.1 Пользовательские группы](#Пользовательские_группы)
    *   [5.2 Системные группы](#Системные_группы)
    *   [5.3 Pre-systemd groups](#Pre-systemd_groups)

## Обзор

*Пользователь* это любой кто использует компьютер. Имена пользователей могут быть любыми, например Mary или Bill, или псевдонимы вместо реальных имен, например Dragonlady или Pirate. Единственное что важно — это то что у компьютера есть имя для каждого созданного аккаунта, и то, что это имя, с помощью которого человек получает доступ к компьютеру. Некоторые службы и программы также запускаются с ограниченными или полными правами.

Управление аккаунтами пользователей используется в целях безопасности, ограничивая доступ несколькими способами.

Любой человек может иметь один и более аккаунт, поэтому каждому аккаунту должно соответствовать уникальное имя. Также есть несколько зарезервированных имен, которые нельзя использовать, например "root", "hal", и "adm".

Пользователи могут быть объединены в группы, и в зависимости от того в каких группах состоят пользователи их привилегии будут различаться.

**Примечание:** Новичкам стоит использовать эти инструменты аккуратно и воздержаться от изменения уже созданных аккаунтов, кроме своего.

## Права и собственность

From [In UNIX Everything is a File](http://ph7spot.com/musings/in-unix-everything-is-a-file):

	*ОС семейства UNIX созданы следуя нескольким единым идеям и концептам, которые отразились в их дизайне, интерфейсе, культуре и эволюции. Одна из важнейших таких идей: "все - это файл"*

	*Этот ключевой принцип состоит в предоставлении единой парадигмы для доступа к широкому кругу устройств ввода/вывода: документы, директории, жесткие диски, CD-диски, модемы, клавиатуры, принтеры, мониторы, терминалы и даже некоторые межпроцессовые взаимодействия и сетевые соединения. Фокус в том, чтобы предоставить простые абстракции для всех этих ресурсов, каждую из которых отцы UNIX назвали "файлом". Так как доступ к любому "файлу" можно получить через один и тот же интерфейс(API, не путать с GUI), вы можете использовать один и тот же набор базовых команд для чтения/записи диска, клавиатуры, документа или сетевого устройства.*

```
[Extending UNIX File Abstraction for General-Purpose Networking](http://www.intel-research.net/Publications/Pittsburgh/101220041324_277.pdf):

```

	*A fundamental and very powerful, consistent abstraction provided in UNIX and compatible operating systems is the file abstraction. Many OS services and device interfaces are implemented to provide a file or file system metaphor to applications. This enables new uses for, and greatly increases the power of, existing applications — simple tools designed with specific uses in mind can, with UNIX file abstractions, be used in novel ways. A simple tool, such as cat, designed to read one or more files and output the contents to standard output, can be used to read from I/O devices through special device files, typically found under the `/dev` directory. On many systems, audio recording and playback can be done simply with the commands, "`cat /dev/audio > myfile`" and "`cat myfile > /dev/audio`," respectively.*

Каждый файл в системе GNU/Linux принадлежит определённому пользователю и группе. Также следует отметить, что существует три типа доступа к файлу: чтение, запись, и выполнение. Различные типы доступа могут быть применены к пользователю и группе, владеющими файлом, а так же всем остальным (не являющимся владельцами файла). Владельцев файлов, а также права доступа можно определить с помощью команды `ls`:

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

 `$ stat -c %U /media/sf_Shared/`  `root` 

Группа:

 `$ stat -c %G /media/sf_Shared/`  `vboxsf` 

Права доступа:

 `$ stat -c %A /media/sf_Shared/`  `drwxrwx---` 

Права доступа отображаются в виде трёх групп символов, представляющих права доступа пользователя, владеющего файлом, владеющей группы, и всех остальных соответственно. Например, символы `-rw-r--r--` означают, что владелец файла имеет право на чтение и запись, но не выполнение (`rw-`), в то время как пользователи, относящиеся к владеющей группе, и все остальные пользователи имеют лишь право на чтение (`r--` и `r--`). Между тем, символы `drwxrwx---` указывают на то, что владелец файла и прочие пользователи, относящиеся к владеющей группе, все имеют право на чтение, запись, и выполнение (`rwx` и `rwx`), тогда как остальные пользователи вообще не имеют никаких прав доступа к файлу (`---`). Первый символ означает тип файла: «d» — каталог, «-» — файл, «l» — ссылка.

Узнать список файлов, которыми владеет тот или иной пользователь и группа, можно с помощью команды `find`:

```
# find / -group [group]

```

```
# find / -user [user]

```

Пользователь и группа могут быть изменены с помощью команды `chown` (change owner). Права доступа к файлу могут быть изменены с помощью команды `chmod` (change mode).

See [chown(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chown.1), [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1), and [Linux file permissions](http://www.tuxfiles.org/linuxhelp/filepermissions.html) for additional detail.

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

## Группы

### Пользовательские группы

Некоторые пользователи должны состоять в некоторых из следующих групп, чтобы получить доступ к периферийным устройствам и упростить администрирование системы:

| Группа | Затронутые файлы | Цель |
| adm | Группа администрирования, аналогичная `wheel`. |
| ftp | `/srv/ftp/` | Доступ к файлам, обслуживаемым [FTP](https://en.wikipedia.org/wiki/FTP "wikipedia:FTP") серверами. |
| games | `/var/games` | Доступ к некоторым игровым программам. |
| http | `/srv/http/` | Доступ к файлам, обслуживаемым [HTTP](https://en.wikipedia.org/wiki/HTTP "wikipedia:HTTP") серверами. |
| log | Доступ к лог-файлам в `/var/log/`, созданным [syslog-ng](/index.php/Syslog-ng "Syslog-ng"). |
| rfkill | `/dev/rfkill` | Право управления состоянием питания беспроводных устройств (используется rfkill). |
| sys | Право администрирования принтеров в [CUPS](/index.php/CUPS "CUPS"). |
| systemd-journal | `/var/log/journal/*` | Может использоваться для обеспечения доступа (только для чтения) к журналам systemd, в качестве альтернативы `adm` and `wheel` [[1]](https://cgit.freedesktop.org/systemd/systemd/tree/README?id=fdbbf0eeda929451e2aaf34937a72f03a225e315#n190). В противном случае отображаются только сообщения, созданные пользователем. |
| users | Стандартная группа пользователей. |
| uucp | `/dev/ttyS[0-9]+`, `/dev/tts/[0-9]+`, `/dev/ttyUSB[0-9]+`, `/dev/ttyACM[0-9]+`, `/dev/rfcomm[0-9]+` | RS-232 последовательные порты и подключенные к ним устройства. |
| wheel | Группа администрирования, обычно используемая для предоставления доступа к [sudo](/index.php/Sudo "Sudo") и [su](/index.php/Su "Su") (Не использует его по умолчанию, настраивается в `/etc/pam.d/su` и `/etc/pam.d/su-l`). Он также может использоваться для получения полного доступа на чтение к [journal](/index.php/Systemd#Journal "Systemd") файлам. |

### Системные группы

Следующие группы используются для системных целей, назначение пользователям требуется только для специальных целей:

| Группа | Затронутые файлы | Цель |
| dbus | Используется внутри [dbus](https://www.archlinux.org/packages/?name=dbus) |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | Смотрите [Core utilities#locate](/index.php/Core_utilities#locate "Core utilities"). |
| lp | `/dev/lp[0-9]*`, `/dev/parport[0-9]*`, `/etc/cups`, `/var/log/cups`, `/var/cache/cups`, `/var/spool/cups` | Доступ к устройствам параллельного порта (принтеры и другие) и доступ (только для чтения) к файлам [CUPS](/index.php/CUPS "CUPS"). Если вы запустите устройство параллельного порта без принтера, см. [FS#50009](https://bugs.archlinux.org/task/50009) возможные. |
| mail | `/usr/bin/mail` |
| nobody | Непривилегированная группа. |
| proc | `/proc/*pid*/` | Группа, уполномоченная изучать информацию о процессах, в противном случае запрещена опцией монтирования [proc filesystem](https://www.kernel.org/doc/Documentation/filesystems/proc.txt). Группа должна быть явно задана с помощью опции монтирования. |
| smmsp | [sendmail](/index.php/Sendmail "Sendmail") группа. |
| tty | `/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx` |
| utmp | `/run/utmp`, `/var/log/btmp`, `/var/log/wtmp` |

### Pre-systemd groups

Перед переходом arch на [systemd](/index.php/Systemd "Systemd"), пользователи должны были быть добавлены вручную в эти группы, чтобы иметь возможность доступа к соответствующим устройствам. This way has been deprecated in favour of [udev](/index.php/Udev "Udev") marking the devices with a `uaccess` [tag](https://github.com/systemd/systemd/blob/master/src/login/70-uaccess.rules) and *logind* assigning the permissions to users dynamically via [ACLs](/index.php/ACL "ACL") according to which session is currently active. Обратите внимание: сеанс не должен быть разбит, чтобы это сработало (см. [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")).

Есть некоторые исключения, которые требуют добавления пользователя в некоторые из этих групп: например, если вы хотите разрешить пользователям доступ к устройству, даже когда они не вошли в систему. Однако обратите внимание, что добавление пользователей в группы может добавить некоторые функциональные возможности(например, группа `audio` нарушит быстрое переключение пользователей и позволяет приложениям блокировать смешение программного обеспечения).

| Группы | Затронутые файлы | Цель |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | Прямой доступ к звуковому оборудованию для всех сеансов. По-прежнему требуется, чтобы [ALSA](/index.php/ALSA "ALSA") и [OSS](/index.php/OSS "OSS") работали в удаленных сеансах, см.[ALSA#User privileges](/index.php/ALSA#User_privileges "ALSA"). |
| disk | `/dev/sd[a-z][1-9]` | Доступ к блочным устройствам, не затронутым другими группами, такими как `optical`, `floppy`, и `storage`. |
| floppy | `/dev/fd[0-9]` | Доступ к флоппи-дискам. |
| input | `/dev/input/event[0-9]*`, `/dev/input/mouse[0-9]*` | Доступ к устройствам ввода. Введено в systemd 215 [[2]](http://lists.freedesktop.org/archives/systemd-commits/2014-June/006343.html). |
| kvm | `/dev/kvm` | Доступ к виртуальным машинам с использованием [KVM](/index.php/KVM "KVM"). |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | Доступ к оптическим устройствам, таким как CD- и DVD-приводы. |
| scanner | `/var/lock/sane` | Доступ к оборудованию сканера. |
| storage | Доступ к съемным дискам, таким как жесткие диски USB, флеш-накопители, MP3-плееры; Позволяет пользователю монтировать запоминающие устройства. |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | Доступ к устройствам захвата видео, аппаратное ускорение 2D / 3D, framebuffer ([X](/index.php/X "X") можно использовать *без* поддержки этой группы). |