Related articles

*   [Systemd/Tаймеры](/index.php/Systemd/T%D0%B0%D0%B9%D0%BC%D0%B5%D1%80%D1%8B "Systemd/Tаймеры")

Из [Википедии](https://ru.wikipedia.org/wiki/Cron):

***cron** - классический демон-планировщик задач в UNIX-подобных операционных системах, использующийся для периодического выполнения заданий в определённое время. Регулярные действия описываются инструкциями, помещенными в файлы crontab и в специальные директории.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Активация и автозапуск](#Активация_и_автозапуск)
    *   [2.2 Обработка ошибок в заданиях](#Обработка_ошибок_в_заданиях)
        *   [2.2.1 Пример с msmtp](#Пример_с_msmtp)
        *   [2.2.2 Пример с esmtp](#Пример_с_esmtp)
        *   [2.2.3 Пример с opensmtpd](#Пример_с_opensmtpd)
        *   [2.2.4 Длительные задания cron](#Длительные_задания_cron)
*   [3 Формат crontab](#Формат_crontab)
*   [4 Базовые команды](#Базовые_команды)
*   [5 Примеры](#Примеры)
*   [6 Default editor](#Default_editor)
*   [7 run-parts issue](#run-parts_issue)
*   [8 Running X.org server-based applications](#Running_X.org_server-based_applications)
*   [9 Asynchronous job processing](#Asynchronous_job_processing)
    *   [9.1 Cronie](#Cronie)
    *   [9.2 Dcron](#Dcron)
    *   [9.3 Cronwhip](#Cronwhip)
    *   [9.4 Anacron](#Anacron)
    *   [9.5 Fcron](#Fcron)
*   [10 Ensuring exclusivity](#Ensuring_exclusivity)
*   [11 cronie](#cronie_2)
*   [12 Dcron](#Dcron_2)
*   [13 See also](#See_also)

## Установка

Существует множество реализаций cron, но ни одна из них не устанавливается по умолчанию, т.к. система использует вместо него [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). См. [руководство по cron](http://www.gentoo.org/doc/en/cron-guide.xml) для Gentoo, в котором представлены сравнения.

Доступные пакеты:

*   [cronie](https://www.archlinux.org/packages/?name=cronie)
*   [fcron](https://www.archlinux.org/packages/?name=fcron)
*   [bcron](https://aur.archlinux.org/packages/bcron/)
*   [dcron](https://aur.archlinux.org/packages/dcron/)
*   [vixie-cron](https://aur.archlinux.org/packages/vixie-cron/)
*   [scron-git](https://aur.archlinux.org/packages/scron-git/)

## Настройка

### Активация и автозапуск

После установки демон не будет включен по умолчанию. Установленный пакет устанавливает службу, которая может контролироваться [systemctl](/index.php/Systemctl "Systemctl"). Например, для *cronie* это `cronie.service`.

Текущие активные задания расположены в папках вроде `/etc/cron.daily/` и запуск службы cron активирует их все.

**Note:** *cronie* предоставляет **ежечасную** задачу `0anacron` , которая осуществляют [отложенный запуск других задач](#Asynchronous_job_processing), например, если компьютер был выключен во время срабатывания задачи по расписанию.

### Обработка ошибок в заданиях

cron регистрирует стандартный вывод из *stdout* и *stderr* и пытается отправить его на электронную почту пользователя используя команду `sendmail`. В cronie такие сообщения на электронную почту отключены, если отсутствует файл `/usr/bin/sendmail`. Для того, чтобы электронные письма направлялись пользователю, в системе должен быть запущен smtp-демон, например [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd). Также вы можете установить пакет, который предоставляет команду sendmail и настроить его на отсылку почту удаленному адресату. Ну и наконец, вы можете вести лог при помощи команды `-m` и скрипта.

#### Пример с msmtp

Установите пакет [msmtp-mta](https://www.archlinux.org/packages/?name=msmtp-mta), который создаст символическую ссылку с `/usr/bin/sendmail` на `/usr/bin/msmtp`. Перезапустите `cronie`, чтобы убедиться, что служба обнаружила новую команду `sendmail`. Теперь вам нужно как-то конвертировать для `msmtp` ваше имя пользователя в адрес электронной почты.

Затем либо добавьте строку `MAILTO` в файл crontab, например, так:

```
MAILTO=your@email.com

```

**либо** создайте файл `/etc/msmtprc` и напишите в него строку:

```
aliases /etc/aliases

```

Создайте файл `/etc/aliases`:

```
your_username: your@email.com
# Optional:
default: your@email.com

```

Затем [измените конфигурацию](/index.php/Systemd#Editing_provided_units "Systemd") демона *cronie* заменив команду `ExecStart` на:

```
ExecStart=/usr/bin/crond -n -m '/usr/bin/msmtp -t'

```

#### Пример с esmtp

Установите [esmtp](https://www.archlinux.org/packages/?name=esmtp) и [procmail](https://www.archlinux.org/packages/?name=procmail).

После установки настройте транспорт почты:

 `/etc/esmtprc` 
```
identity *myself*@myisp.com
       hostname mail.myisp.com:25
       username *"myself"*
       password *"secret"*
       starttls enabled
       default
mda "/usr/bin/procmail -d %T"

```

Для работы в режиме доставки Procmail требует права суперпользователя, но это не проблема, т.к. вы все равно запускаете задания cron от имени root.

Чтобы проверить, что все работает, создайте файл `message.txt` с `"test message"` внутри.

Из той же папки запустите:

```
$ sendmail *user_name* < message.txt 

```

Затем:

```
$ cat /var/spool/mail/*user_name*

```

Вы должны увидеть тестовое сообщение, а также время и дату его отправки.

Поток ошибок всех активных заданий теперь перенаправлен в `/var/spool/mail/*user_name*`.

В связи с ограничениями прав, довольно непросто создавать и отправлять электронные письма пользователю root (например, так: `su -c ""`). В `esmtp` можно настроить пересылку сообщений, адресованных root, обычному пользователю:

 `/etc/esmtprc`  `force_mda="*user-name*"` 
**Note:** Если вышенаписанное не сработает, можете попробовать создать локальную копию `~/.esmtprc` с тем же содержанием.

Выполните следующую команду, чтобы дать необходимые права:

```
$ chmod 710 ~/.esmtprc

```

Затем повторите тест с отправкой `message.txt` точно так же, как описано выше.

#### Пример с opensmtpd

Установите [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd).

Отредактируйте `/etc/smtpd/smtpd.conf`. Следующая конфигурация подходит для локальной доставки почты:

```
listen on localhost
accept for local deliver to mbox

```

Можете начинать тестировать ее. Для начала [запустите](/index.php/Start "Start") `smtpd.service`. Затем:

```
$ echo test | sendmail user

```

*user* может проверить свою почту любым [клиентом](/index.php/Category:Email_clients "Category:Email clients"), способным распознать формат mbox, либо просто посмотреть файл `/var/spool/mail/*user*`. Если все прошло нормально, можете [включить](/index.php/Enable "Enable") opensmtpd.

Этот метод имеет то преимущество, что не нужно отправлять уведомления cron на удаленный сервер, не нужно даже никакого сетевого соединения. С другой стороны, в памяти системы висит еще один демон.

**Note:**

*   На момент написания статьи пакет opensmtpd не создает все необходимые папки в `/var/spool/smtpd`, но демон предупредит об этом, указав все необходимые права и владельцев. Просто создайте нужные папки самостоятельно.
*   Даже несмотря на то, что предложенная конфигурация не принимает удаленные подключения, хорошей практикой является добавить дополнительный слой безопасности, заблокировав порт 25 в [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)") или другом файерволле.

#### Длительные задания cron

Представьте, что в cron загружена следующая программа:

```
#!/bin/sh
echo "I had a recoverable error!"
sleep 1h

```

Что произойдет?

1.  cron запускает скрипт
2.  как только cron видит какой-то вывод, он запускает вашу почтовую систему и создает некоторые заголовки. Он оставляет поток открытым, потому что задание не завершено и может быть больше выходных данных.
3.  почтовая система открывает соединение с postfix и оставляет его открытым, пока ждет окончания тела письма.
4.  postfix закрывает простаивающее соединение раньше, чем проходит один час, и вы получаете ошибку вроде этой:

```
smtpmsg='421 … Error: timeout exceeded' errormsg='the server did not accept the mail'

```

Для того, чтобы решить эту проблему, вам понадобятся команды chronic или sponge из пакета [moreutils](https://www.archlinux.org/packages/?name=moreutils).

С их man-страниц:

	chronic

	chronic запускает команду и организовывает ее стандартные потоки вывода и ошибок так, что отображается только неправильный результат работы программы (выход с ненулевым значением или сбой). Если команда выполнена успешно, любые дополнительные выходные данные будут скрыты.

	sponge

	sponge получает стандартный входной поток и пишет его в специальный файл. В отличие от перенаправления командной строки, sponge аггрегирует весь свой входной поток в выходной файл. Если выходной файл не указан, sponge выводит данные в stdout.

Даже если это не указано явно, chronic буферизирует выходные данные команды перед тем, как открыть stdout (как и sponge)

## Формат crontab

Основной формат для crontab таков:

```
*минута* *час* *день_месяца* *месяц* *день_недели* *команда*

```

*   *минута* - значение от 0 до 59
*   *час* - значение от 0 до 23
*   *день_месяца* - значение от 1 до 31
*   *месяц* - значение от 1 до 12
*   *день_недели* - значение от 0 до 6, где 0 - это воскресенье.

Несколько вызовов могут быть перечислены через запятую, интервал может быть задан через дефис, а звёздочка означает любой символ. Пробелы используются для разделения полей. К примеру, строка

```
*/5 9-16 * 1-5,9-12 1-5 ~/bin/i_love_cron.sh

```

вызовет скрипт `i_love_cron.sh` каждые пять минут с 9 AM до 4:55 PM по будням (уточнить, неделя может начинаться с воскресенья) кроме летних месяцев (июнь, июль, август). Больше примеров и дополнительные настройки могут быть найдены ниже.

## Базовые команды

Crontabs никогда не редактируются напрямую; вместо этого пользователи должны использовать `crontab` утилиту для работы со своими crontabs. Чтобы получить доступ к этой утилите, пользователь должен быть членом группы `users` (смотри команду `gpasswd`).

Чтобы просмотреть свои crontabs, пользователь может воспользоваться коммандой:

```
$ crontab -l

```

Для редактирования своих crontabs:

```
$ crontab -e

```

**Note:** По умолчанию команда `crontab` использует редактор `vi`. Чтобы изменить это, [экспортируйте](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `EDITOR` или `VISUAL`, или укажите редактор напрямую: `EDITOR=vim crontab -e`.

Чтобы удалить свои crontabs:

```
$ crontab -r

```

Если пользователь имеет сохранённые crontab и хочет полностью перезаписать свои старые crontab, он может воспользоваться:

```
$ crontab *saved_crontab_filename*

```

Чтобы перезаписать crontab из командной строки ([Wikipedia:stdin](https://en.wikipedia.org/wiki/stdin "wikipedia:stdin")), используйте

```
$ crontab - 

```

Чтобы отредактировать чьи-либо ещё crontab, вызовите следующую команду из под root:

```
# crontab -u *username* -e

```

Этот же формат (присоединяя `-u *username*` к команде) работает так же для чтения и удаления crontabs.

## Примеры

Запись:

```
01 * * * * /bin/echo Hello, world!

```

выполняет команду `/bin/echo Hello, world!` в первую минуту каждого часа каждого дня (т.е. в 12:01, 1:01, 2:01, etc.).

Аналогично:

```
*/5 * * jan mon-fri /bin/echo Hello, world!

```

выполняет то же действие каждые пять минут по будним дням в течение Января (т.е. в 12:00, 12:05, 12:10, etc.).

Строка (как указано в "man 5 crontab"):

```
*0,*5 9-16 * 1-5,9-12 1-5 /home/user/bin/i_love_cron.sh

```

вызывает скрипт `i_love_cron.sh` в пятиминутные интервалы с 9 AM до 5 PM (не включая 5 PM) каждый будний день каждого месяца, кроме летних.

Periodical settings can also be entered as in this crontab template:

```
# Chronological table of program loadings                                       
# Edit with "crontab" for proper functionality, "man 5 crontab" for formatting
# User: johndoe

# mm  hh  DD  MM  W /path/progam [--option]...  ( W = weekday: 0-6 [Sun=0] )
  21  01  *   *   * /usr/bin/systemctl hibernate
  @weekly           $HOME/.local/bin/trash-empty

```

## Default editor

To use an alternate default editor, define the `EDITOR` environment variable in a shell initialization script as described in [Environment variables](/index.php/Environment_variables "Environment variables").

As a regular user, `su` will need to be used instead of `sudo` for the environment variable to be pulled correctly:

```
$ su -c "crontab -e"

```

To have an alias to this `printf` is required to carry the arbitrary string because `su` launches in a new shell:

```
alias scron="su -c $(printf "%q " "crontab -e")"

```

## run-parts issue

cronie uses `run-parts` to carry out script in `cron.daily`/`cron.weekly`/`cron.monthly`. Be careful that the script name in these won't include a dot (.), e.g. `backup.sh`, since `run-parts` without options will ignore them (see: [run-parts(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/run-parts.8)).

## Running X.org server-based applications

Cron does not run under the X.org server therefore it cannot know the environmental variable necessary to be able to start an X.org server application so they will have to be defined. One can use a program like [xuserrun](https://aur.archlinux.org/packages/xuserrun/) to do it:

```
17 02 * ... /usr/bin/xuserrun /usr/bin/xclock

```

Or then can be defined manually (`echo $DISPLAY` will give the current DISPLAY value):

```
17 02 * ... env DISPLAY=:0 /usr/bin/xclock

```

If done through say SSH, permission will need be given:

```
# xhost +si:localuser:$(whoami)

```

## Asynchronous job processing

If you regularly turn off your computer but do not want to miss jobs, there are some solutions available (easiest to hardest):

### Cronie

[cronie](https://www.archlinux.org/packages/?name=cronie) comes with anacron included. The project homepage reads:

Cronie contains the standard UNIX daemon crond that runs specified programs at scheduled times and related tools. It is based on the original cron and has security and configuration enhancements like the ability to use pam and SELinux.

### Dcron

Vanilla [dcron](https://aur.archlinux.org/packages/dcron/) supports asynchronous job processing. Just put it with @hourly, @daily, @weekly or @monthly with a jobname, like this:

```
@hourly         ID=greatest_ever_job      echo This job is very useful.

```

### Cronwhip

[cronwhip](https://aur.archlinux.org/packages/cronwhip/) is a script to automatically run missed cron jobs; it works with the former default cron implementation, *dcron*. See also the [forum thread](https://bbs.archlinux.org/viewtopic.php?id=57973).

### Anacron

Anacron is a full replacement for *dcron* which processes jobs asynchronously.

It is provided by [cronie](https://www.archlinux.org/packages/?name=cronie). The configuration file is `/etc/anacrontab`. Information on the format can be found in the `anacrontab(5)` [man page](/index.php/Man_page "Man page"). Running `anacron -T` will test `/etc/anacrontab` for validity.

### Fcron

Like *anacron*, [fcron](https://www.archlinux.org/packages/?name=fcron) assumes the computer is not always running and, unlike *anacron*, it can schedule events at intervals shorter than a single day which may be useful for systems which suspend/hibernate regularly (such as a laptop). Like cronwhip, fcron can run jobs that should have been run during the computer's downtime.

When replacing [cronie](https://www.archlinux.org/packages/?name=cronie) with fcron be aware the spool directory is `/var/spool/fcron` and the `fcrontab` command is used instead of *crontab* to edit the user crontabs. These crontabs are stored in a binary format with the text version next to them as *foo*.orig in the spool directory. Any scripts which manually edit user crontabs may need to be adjusted due to this difference in behavior.

A quick scriptlet which may aide in converting traditional user crontabs to fcron format:

```
cd /var/spool/cron && (
 for ctab in *; do
  fcrontab ${ctab} -u ${ctab}
 done
)

```

See also the [forum thread](https://bbs.archlinux.org/viewtopic.php?id=140497).

## Ensuring exclusivity

If you run potentially long-running jobs (e.g., a backup might all of a sudden run for a long time, because of many changes or a particular slow network connection), then `flock` ([util-linux](https://www.archlinux.org/packages/?name=util-linux)) can ensure that the cron job won't start a second time.

```
  5,35 * * * * /usr/bin/flock -n /tmp/lock.backup /root/make-backup.sh

```

## cronie

Long time users of vixie-cron (traditional cron) will be confused by how cronie is set up. Here is the relevant file hierarchy:

```
   /etc
     |----- anacrontab
     |----- cron.d
              | ----- 0hourly
     |----- cron.daily
     |----- cron.deny
     |----- cron.hourly
     |----- cron.monthly
     |----- cron.weekly
     |----- crontab

```

Note that the crontab file is **not** created by default, but jobs added here will be run if you wish to use this file. Cronie provides both cron and anacron functionality. The difference is that cron will run jobs at particular time intervals (down to a granularity of one minute) *if the machine is on at the particular time specified*, while anacron runs jobs (with a minimum daily granularity) without assuming that the machine is turned on all the time. When the machine is on, anacron will check to see if there are any jobs that *should have been run* and will run them accordingly. The `/etc/cron.d` and `/etc/cron.hourly` directories are associated with **cron** functionality, while the `/etc/anacrontab` file and `/etc/cron.daily`, `/etc/cron.weekly`, and `/etc/cron.monthly` directories are associated with **anacron** functionality. The `/etc/cron.deny` file is there so that any user who is not specifically prohibited can create their own cron jobs.

To implement a system-wide cron job, create a crontab-like file for it and place it in the `/etc/cron.d` directory or add the job to /etc/crontab. Any executable (these are almost always shell scripts) in `/etc/cron.hourly` will be run every hour.

Anacron functionality is implemented similarly, however using the `/etc/cron.daily`, `/etc/cron.weekly`, or `/etc/cron.monthly` directories, depending on how frequently you want the job to be run. The anacron job files are also executables; i.e. not in crontab-format. Anacron is triggered at the beginning of every hour by the crontab file `/etc/cron.d/0hourly` which runs the executables in `/etc/cron.hourly` including the file `/etc/cron.hourly/0anacron` - deleting these will prevent anacron running any daily, weekly or monthly tasks.

**Note:** the output of `systemctl status cronie` might show a message such as `crond[<PID>]: (root) CAN'T OPEN (/etc/crontab): No such file or directory`. However, this is not an error as of cronie 1.4.8\. See [this](https://lists.archlinux.org/pipermail/arch-general/2012-February/025178.html) discussion.

## Dcron

The cron daemon parses a configuration file known as `crontab`. Each user on the system can maintain a separate crontab file to schedule commands individually. The root user's crontab is used to schedule system-wide tasks (though users may opt to use `/etc/crontab` or the `/etc/cron.d` directory, depending on which cron implementation they choose).

```
/var/spool/cron/root

```

```
# Run command at a scheduled time
# Edit this 'crontab -e' for error checking, man 1 crontab for acceptable format

# <@freq>                       <tags and command>
@hourly         ID=sys-hourly   /usr/sbin/run-cron /etc/cron.hourly
@daily          ID=sys-daily    /usr/sbin/run-cron /etc/cron.daily
@weekly         ID=sys-weekly   /usr/sbin/run-cron /etc/cron.weekly
@monthly        ID=sys-monthly  /usr/sbin/run-cron /etc/cron.monthly

# mm  hh  DD  MM  W /path/command (or tags) # W = week: 0-6, Sun=0
  21  01  *   *   * /usr/bin/systemctl suspend

```

These lines exemplify one of the formats that crontab entries can have, namely whitespace-separated fields specifying:

1.  @period
2.  ID=jobname (this tag is specific to dcron)
3.  command

The other standard format for crontab entries is:

1.  minute
2.  hour
3.  day
4.  month
5.  day of week
6.  command

The crontab files themselves are usually stored as `/var/spool/cron/username`. For example, root's crontab is found at `/var/spool/cron/root`

See the crontab [man page](/index.php/Man_page "Man page") for further information and configuration examples.

## See also

*   [Gentoo Linux Cron Guide](http://www.gentoo.org/doc/en/cron-guide.xml)