**Если вы хотите организовать официальное зеркало, посетите [эту страницу](https://wiki.archlinux.org/index.php/DeveloperWiki:NewMirrors).**

**Замечание:** 95% пользователей не нуждаются в зеркале. Большинство пакетов из репозитория вы никогда не используете. Инструкция может понадобиться человеку, управляющему большим количеством машин с Arch Linux. Возможно, [Network Shared Pacman Cache](/index.php/Network_Shared_Pacman_Cache "Network Shared Pacman Cache") окажется для вас более полезным. Вы также можете воспользоваться [pkgd](http://xyne.archlinux.ca/info/pkgd) для создания общедоступного кэша в локальной сети без необходимости управления центральным кэшем.

**Замечание:** Синхронизация с rsync.archlinux.org доступна только для официальных зеркал. Если вы хотите создать официальное зеркало, напишите об этом в почтовой рассылке.

Для создания полного зеркала для личных целей используйте **rsync://distro.ibiblio.org/distros/archlinux/**

Эта статья описывает принцип создания зеркала всех пакетов и iso-образов на локальной машине, переодического обновления зеркала с помощью cron, публикацию зеркала с помощью vsftpd и настройки pacman для использования локального зеркала.

## Contents

*   [1 Размер зеркала](#.D0.A0.D0.B0.D0.B7.D0.BC.D0.B5.D1.80_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
*   [2 Предварительные действия](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B2.D0.B0.D1.80.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D0.B8.D1.8F)
*   [3 Создание директории локального зеркала](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B8_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
*   [4 Скрипт синхронизации](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.D1.81.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8)
*   [5 Запуск задания cron](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B7.D0.B0.D0.B4.D0.B0.D0.BD.D0.B8.D1.8F_cron)
    *   [5.1 Редактирование задания cron](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B4.D0.B0.D0.BD.D0.B8.D1.8F_cron)
*   [6 Настройка pacman для использования локального зеркала](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_pacman_.D0.B4.D0.BB.D1.8F_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
    *   [6.1 Единственный компьютер](#.D0.95.D0.B4.D0.B8.D0.BD.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_.D0.BA.D0.BE.D0.BC.D0.BF.D1.8C.D1.8E.D1.82.D0.B5.D1.80)
    *   [6.2 Несколько компьютеров](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BA.D0.BE.D0.BC.D0.BF.D1.8C.D1.8E.D1.82.D0.B5.D1.80.D0.BE.D0.B2)
        *   [6.2.1 Настройка FTP-сервера](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_FTP-.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
        *   [6.2.2 Доступ pacman к зеркалу](#.D0.94.D0.BE.D1.81.D1.82.D1.83.D0.BF_pacman_.D0.BA_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D1.83)
*   [7 Первая синхронизация](#.D0.9F.D0.B5.D1.80.D0.B2.D0.B0.D1.8F_.D1.81.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)

## Размер зеркала

Чтобы прикинуть необходимое свободное пространство для организации локального зеркала взгляните на следующие цифры:

*   archive - 14GB (заморожено)
*   core + extra + community - 20GB на июль 2010
*   testing + community-testing - от нескольких мегабайт до нескольких гигабайт
*   временные репозитории (например, gnome-unstable, kde-unstable, xorg18 и т.п.) - до 1GB
*   iso - 11GB на июль 2010
*   other - 5.3GB на июль 2010
*   sources - 6.8GB на июль 2010

Большинство зеркал синхронизируют все директории (включая временные репозитории), кроме "archive", "other" и "sources", таким образом необходимо примерно 35GB для организации зеркала Arch Linux.

## Предварительные действия

Для начала обновите систему и установите необходимые инструменты:

```
pacman -Syu
pacman -S rsync vsftpd

```

Затем создайте нового пользователя (без привилегии входа в систему), который будет использоваться для операций синхронизации и обслуживания файлов на FTP-сервере. В нашем примере имя пользователя - "mirror", но вы можете использовать другое имя. **Не** используйте root или любой другой аккаунт, который используется для входа в систему. Из соображений безопасности мы используем пользователя с наименьшими возможными привилегиями.

```
useradd -m -s /bin/false mirror

```

Настраиваем зеркало.

## Создание директории локального зеркала

Для скриптов, логов и пакетов будем использовать <tt>/home/mirror</tt> - домашний каталог нашего непривилегированного пользователя.

Необходимо создать несколько директорий в /home/mirror:

```
cd /home/mirror
sudo -u mirror mkdir {scripts,files,logs}

```

## Скрипт синхронизации

Далее создадим скрипт синхронизации, <tt>scripts/mirrorsync.sh</tt>, используя любимый текстовый редактор.

```
#!/bin/bash
#
# The script to sync a local mirror of the Arch Linux repositories and ISOs
#
# Copyright (C) 2007 Woody Gilk <woody@archlinux.org>
# Modifications by Dale Blount <dale@archlinux.org>
# and Roman Kyrylych <roman@archlinux.org>
# and Vadim Gamov <nickleiten@gmail.com>
# Licensed under the GNU GPL (version 2)

# Filesystem locations for the sync operations
SYNC_HOME="/home/mirror"
SYNC_LOGS="$SYNC_HOME/logs"
SYNC_FILES="$SYNC_HOME/files"
SYNC_LOCK="$SYNC_HOME/mirrorsync.lck"

# Select which repositories to sync
# Valid options are: core, extra, testing, community, iso
# Leave empty to sync a complete mirror
# SYNC_REPO=(core extra testing community iso)
SYNC_REPO=()

# Set the rsync server to use
# Only official public mirrors are allowed to use rsync.archlinux.org
# SYNC_SERVER=rsync.archlinux.org::ftp
SYNC_SERVER=distro.ibiblio.org::archlinux

# Set the format of the log file name
# This example will output something like this: sync_20070201-8.log
LOG_FILE="pkgsync_$(date +%Y%m%d-%H).log"

#Watchdog part (time in seconds of uninterruptable work of script)
#        Needed for low-speed and/or unstable links to prevent
#       rsync hunging up.
#        New instance of script checks for timeout, if it occurs
#       it'll kill previous instance, in elsecase it'll exit without
#       any work.
WD_TIMEOUT=10800 

# Do not edit the following lines, they protect the sync from running more than
# one instance at a time
if [ ! -d $SYNC_HOME ]; then
  echo "$SYNC_HOME does not exist, please create it, then run this script again."
  exit 1
fi

if [ -f $SYNC_LOCK ];then
    OPID=`head -n1 $SYNC_LOCK`;
    TIMEOUT=`head -n2 $SYNC_LOCK|tail -n1`;
    NOW=`date +%s`;
    if [ "$NOW" -ge "$TIMEOUT" ];then
       kill -9 $OPID;
    fi
    MYNAME=`basename $0`;
    TESTPID=`ps -p $OPID|grep $OPID|grep $MYNAME`;
    if [ "$TESTPID" != "" ];then
        echo "exit";
        exit 1;
    else
        rm $SYNC_LOCK;
    fi
fi
echo $$ > "$SYNC_LOCK"
echo `expr \`date +%s\` + $WD_TIMEOUT` >> "$SYNC_LOCK"
# End of non-editable lines

# Create the log file and insert a timestamp
touch "$SYNC_LOGS/$LOG_FILE"
echo "=============================================" | tee -a "$SYNC_LOGS/$LOG_FILE"
echo ">> Starting sync on $(date --rfc-3339=seconds)" | tee -a "$SYNC_LOGS/$LOG_FILE"
echo ">> ---" | tee -a "$SYNC_LOGS/$LOG_FILE"

if [ -z $SYNC_REPO ]; then
  # Sync a complete mirror
  rsync -rtlvH --delete-after --delay-updates --safe-links --max-delete=1000 $SYNC_SERVER "$SYNC_FILES" | tee -a "$SYNC_LOGS/$LOG_FILE"
  # Create $repo.lastsync file with timestamp like "2007-05-02 03:41:08+03:00"
  # which may be useful for users to know when the mirror was last updated
  date --rfc-3339=seconds > "$SYNC_FILES/$repo.lastsync"
else
  # Sync each of the repositories set in $SYNC_REPO
  for repo in ${SYNC_REPO[@]}; do
    repo=$(echo $repo | tr [:upper:] [:lower:])
    echo ">> Syncing $repo to $SYNC_FILES/$repo" | tee -a "$SYNC_LOGS/$LOG_FILE"

    # If you only want to mirror i686 packages, you can add
    # " --exclude=os/x86_64" after "--delete-after"
    # 
    # If you only want to mirror x86_64 packages, use "--exclude=os/i686"
    # If you want both i686 and x86_64, leave the following line as it is
    #
    rsync -rtlvH --delete-after --delay-updates --max-delete=1000 $SYNC_SERVER/$repo "$SYNC_FILES" | tee -a "$SYNC_LOGS/$LOG_FILE"

    # Create $repo.lastsync file with timestamp like "2007-05-02 03:41:08+03:00"
    # which may be useful for users to know when the repository was last updated
    date --rfc-3339=seconds > "$SYNC_FILES/$repo.lastsync"

    # Sleep 5 seconds after each repository to avoid too many concurrent connections
    # to rsync server if the TCP connection does not close in a timely manner
    sleep 5 
  done
fi

# Insert another timestamp and close the log file
echo ">> ---" | tee -a "$SYNC_LOGS/$LOG_FILE"
echo ">> Finished sync on $(date --rfc-3339=seconds)" | tee -a "$SYNC_LOGS/$LOG_FILE"
echo "=============================================" | tee -a "$SYNC_LOGS/$LOG_FILE"
echo "" | tee -a "$SYNC_LOGS/$LOG_FILE"

# Remove the lock file and exit
rm -f "$SYNC_LOCK"
exit 0

```

Не пугайтесь, просто скопируйте скрипт. Сделаем его исполняемым.

```
chmod +x scripts/mirrorsync.sh

```

Готово, теперь у вас есть скрипт, который, при необходимости, можно легко отредактировать. Возможно, вы не желаете его запускать вручную, в этом случае можно настроить cron для автоматического запуска.

Небольшое замечание перед следующим шагом: директория с логами может со временем вырасти в размерах. Проверяйте ее периодически, подчищая мусор. Рекомендуется настроить [LogRotate](/index.php?title=LogRotate&action=edit&redlink=1 "LogRotate (page does not exist)") для этого, либо написать собственный скрипт.

## Запуск задания cron

Убедитесь в наличии необходимых утилит cron:

```
pacman -S dcron

```

Будем запускать нашу задачу с помощью <tt>crontab</tt> (для дополнительной информации обратитесь к мануалу по crontab). Этот метод предпочтителен с точки зрения безопасности, не требует создания <tt>/etc/cron.*</tt> файлов, а также гибко контролируем во время работы.

Создайте <tt>scripts/mirror.cron</tt> со следующим содержимым:

```
0 3 * * * /home/mirror/scripts/mirrorsync.sh

```

Далее необходимо активировать crontab:

```
crontab -u mirror scripts/mirror.cron

```

Убедитесь, что crontab подхватил наше задание:

```
crontab -u mirror -l

```

Должны увидеть содержимое <tt>scripts/mirror.cron</tt>. Если этого не произошло, вернитесь к предыдущей команде и проверьте, все ли сделано правильно.

Данная задача будет запускать наш скрипт синхронизации каждую ночь в 3 часа. Разумеется, вы можете изменить этот параметр по своему усмотрению, для информации по синтаксису crontab обратитесь к [http://www.adminschoice.com/docs/crontab.htm](http://www.adminschoice.com/docs/crontab.htm).

### Редактирование задания cron

Если появится необходимость в редактировании <tt>mirror.cron</tt>, используйте следующую команду:

```
crontab -u mirror -e

```

Если редактируете файл вручную, используйте следующую команду для обновления crontab:

```
crontab -u mirror scripts/mirror.cron

```

Приступим к настройке pacman для использования локального зеркала.

## Настройка pacman для использования локального зеркала

Следуйте данным шагам, если предполагается пользование зеркалом только единственным локальным компьютером.

### Единственный компьютер

**Замечание:** Не совсем гуманно создавать локальное зеркало для единственной машины. Вы отнимаете часть пропускного канала сервера синхронизации, который бы мог быть задействован для более важных операций. Подумайте над этим.

Для этого типа настройки нет необходимости в vsftpd, т.к. доступ осуществляется напрямую к файлам: file:// url, а не ftp:// url.

Добавьте следующую строку в начало файла списка серверов <tt>/etc/pacman.d/mirrorlist</tt>:

```
Server = file:///home/mirror/files/$repo/os/i686

```

Не забудьте заменить <tt>i686</tt> на <tt>x86_64</tt>, если используете 64-битную версию Arch Linux.

### Несколько компьютеров

Для доступа сетевых компьютеров к зеркалу используется FTP. Вы также можете использовать FTP для синхронизации локального компьютера (детали этого читайте дальше).

#### Настройка FTP-сервера

Для начала сконфигурируем vsftpd. Приведите <tt>/etc/vsftpd.conf</tt> к следующему виду:

```
# vsftpd config file /etc/vsftpd.conf
#
# Setup for a secure anonymous FTP server
#
# Listen (non-xinetd) mode
listen=YES
# Use tcp_wrappers to control connections
tcp_wrappers=YES
# Use localtimes instead of GMT for files
use_localtime=YES
# Hide the true user/group ID of files
hide_ids=YES
# 
# Enable anonymous access (pacman requires this)
anonymous_enable=YES
# Use this user for anonymous logins
ftp_username=mirror
# Chroot directory for anonymous user
anon_root=/home/mirror/files/archlinux
# Don't require a password for anonymous access (pacman requires this)
no_anon_password=YES
#
# User to run vsftpd as (same as ftp_username)
nopriv_user=mirror
# Enable recursive "ls" listing
ls_recurse_enable=YES
#
# Forcefully destroy sessions after X seconds of inactivity 
# (It is highly recommended to not set this above 300)
idle_session_timeout=120
# Forcefully stop sending data after X seconds of inactivity during a transfer
# (It is highly recommended to not set this higher than idle_session_timeout)
data_connection_timeout=30

```

Итог - очень защищенный FTP-сервер, адаптированный под наши нужды. Обратите внимание, что сервер **не** требует пароля, поэтому не предназначен для работы в публичной сети (хотя, дело ваше). *Описание возможности работы pacman с FTP-сервером, защищенным паролем выходит за рамки этого документа.*

Если предполагается соединение с этим компьютером извне, необходимо добавить следующую строку в <tt>/etc/hosts.allow</tt>:

```
vsftpd : ALL : ALL

```

Учтите, что таким образом вы разрешаете **всем** доступ к зеркалу. Если вы хотите контролировать доступ, но не знаете как, загляните на [linux.about.com](http://linux.about.com/od/commands/l/blcmdl5_hostsal.htm).

Запустим vsftpd:

```
sudo /etc/rc.d/vsftpd start

```

Если vsftpd не запустился, ищите ошибки в <tt>/etc/vsftpd.conf</tt>.

#### Доступ pacman к зеркалу

Отредактируйте файл <tt>/etc/pacman.d/mirrorlist</tt> для использования нашего зеркала. Добавьте следующую строку в начало файла:

```
Server = [ftp://192.168.1.21/$repo/os/i686](ftp://192.168.1.21/$repo/os/i686)

```

Обратите внимание, что <tt>192.168.1.21</tt> - IP-адрес нашей тестовой машины. Ваш адрес, естественно, может быть другим (его можно узнать при помощи <tt>ifconfig -a</tt> или <tt>ifconfig eth0</tt>).

Если хотите использовать это зеркало на локальной машине, используйте следующую строку:

```
Server = [ftp://localhost/$repo/os/i686](ftp://localhost/$repo/os/i686)

```

Сетевые машины должны использовать IP-адрес для доступа к репозиторию. Также следует отметить, что машина, обслуживающая зеркало, должна иметь статический IP-адрес.

## Первая синхронизация

Испробуем? Выполните следующую команду для начала синхронизации:

```
sudo -u mirror ./scripts/mirrorsync.sh

```

Процесс синхронизации будет выводиться в консоль, а также в лог-файлы. Для просмотра можете использовать что-то вроде:

```
tail -f logs/pkgsync_20070203-9.log

```

В зависимости от скорости вашего интернета процесс затянется на несколько часов/дней. При последующих синхронизациях будут загружаться только новые пакеты, поэтому это будет намного быстрее.

Дождитесь окончания первой синхронизации, затем выполните <tt>pacman -Syy</tt>, чтобы убедиться, что новые зеркала синхронизировались должным образом. Вот, собственно, и все!