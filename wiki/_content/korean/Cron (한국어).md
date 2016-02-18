출처 [Wikipedia](https://en.wikipedia.org/wiki/Cron):

***cron**은 유닉스 계열 운영 체제의 시간 기반 작업 스케줄러이다. cron을 사용하면 사용자는 명령어나 쉘 스크립트와 같은 작업을 특정 시간이나 날짜에 주기적으로 실행할 수 있도록 일정을 짤 수 있다. 시스템 관리나 작업을 자동화하기 위해 보통 사용된다.[...]*

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 설정](#.EC.84.A4.EC.A0.95)
    *   [2.1 사용자와 자동 시작](#.EC.82.AC.EC.9A.A9.EC.9E.90.EC.99.80_.EC.9E.90.EB.8F.99_.EC.8B.9C.EC.9E.91)
    *   [2.2 Handling errors of jobs](#Handling_errors_of_jobs)
        *   [2.2.1 Example with msmtp](#Example_with_msmtp)
        *   [2.2.2 Example with esmtp](#Example_with_esmtp)
        *   [2.2.3 Example with opensmtpd](#Example_with_opensmtpd)
        *   [2.2.4 Long cron job](#Long_cron_job)
*   [3 Crontab format](#Crontab_format)
*   [4 Basic commands](#Basic_commands)
*   [5 Examples](#Examples)
*   [6 Default editor](#Default_editor)
*   [7 More information](#More_information)
*   [8 run-parts issue](#run-parts_issue)
*   [9 Running Xorg server based applications](#Running_Xorg_server_based_applications)
*   [10 Asynchronous job processing](#Asynchronous_job_processing)
    *   [10.1 Dcron](#Dcron)
    *   [10.2 Cronwhip](#Cronwhip)
    *   [10.3 Anacron](#Anacron)
    *   [10.4 Fcron](#Fcron)
*   [11 Ensuring exclusivity](#Ensuring_exclusivity)
*   [12 See Also](#See_Also)

## 설치

[cronie](https://www.archlinux.org/packages/?name=cronie) is installed by default as part of the **base** group. Other cron implementations exist if preferred, Gentoo's [Cron Guide](http://www.gentoo.org/doc/en/cron-guide.xml) offers comparisons. For example, [fcron](https://www.archlinux.org/packages/?name=fcron), [bcron](https://aur.archlinux.org/packages/bcron/) or [vixie-cron](https://aur.archlinux.org/packages/vixie-cron/) are other alternatives. [dcron](https://aur.archlinux.org/packages/dcron/) used to be the default cron implementation in Arch Linux until May 2011.

## 설정

### 사용자와 자동 시작

cron should be working upon login on a new system to run root scripts. This can be check by looking at the log in `/var/log/`. In order to use crontab application (editor for job entries), users must be members of a designated group `users` or `root`, of which all users should already be members. To ensure cron starts on boot, enable `cronie.service` or `dcron.service` with `systemctl enable <service_name>` depending on which cron implementation you use.

### Handling errors of jobs

cron registers the output from **stdout** and **stderr** and attempts to send it as email to the user's spools via the `sendmail` command. Cronie disables mail output if `/usr/bin/sendmail` is not found. To log these messages use the `-m` option and write a script or install a rudimentary SMTP subsystem.

1.  [Edit](/index.php/Systemd#Editing_provided_unit_files "Systemd") the `cronie.service` unit.
2.  Install [esmtp](https://www.archlinux.org/packages/?name=esmtp), [msmtp](https://www.archlinux.org/packages/?name=msmtp), [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd) or write a custom script.

#### Example with msmtp

Here are two ways to obtain emails from cronie with msmtp:

1.  Install the [msmtp-mta](https://www.archlinux.org/packages/?name=msmtp-mta) package which effectively creates a symbolic link from `/usr/bin/sendmail` to `/usr/bin/msmtp`. You must then provide a way for msmtp to convert your username into an email address.
    *   Either add a `MAILTO` line to your crontab, like so: `MAILTO=your@email.com` — OR —
    *   add this line to `/etc/msmtprc`: `aliases /etc/aliases` and create `/etc/aliases`:
        ```
        your_username: your@email.com
        # Optional:
        default: your@email.com
        ```

2.  [Edit](/index.php/Systemd#Editing_provided_unit_files "Systemd") the `cronie.service` unit. For example, create `/etc/sytemd/system/cronie.service.d/msmtp.conf`:
    ```
    [Service]
    ExecStart=
    ExecStart=/usr/bin/crond -n -m '/usr/bin/msmtp -t'
    ```
    Note: the empty `ExecStart=` cancels any previous `ExecStart` commands.

#### Example with esmtp

```
# pacman -S esmtp procmail

```

After installation configure the routing:

 `/etc/esmtprc` 
```
identity *myself*@myisp.com
       hostname mail.myisp.com:25
       username *"myself"*
       password *"secret"*
       starttls enabled
       default
mda "/usr/bin/procmail -d %T"

```

Procmail needs root privileges to work in delivery mode but it is not an issue if you are running the cronjobs as root anyway.

To test that everything works correctly, create a file `message.txt` with `"test message"` in it.

From the same directory run:

```
$ sendmail *user_name* < message.txt 

```

then:

```
$ cat /var/spool/mail/*user_name*

```

You should now see the test message and the time and date it was sent.

The error output of all jobs will now be redirected to `/var/spool/mail/*user_name*`.

Due to the privileged issue, it is hard to create and send emails to root (e.g. `su -c ""`). You can ask `esmtp` to forward all root's email to an ordinary user with:

 `/etc/esmtprc`  `force_mda="*user-name*"` 
**Note:** If the above test didn't work, you may try creating a local configuration in `~/.esmtprc` with the same content.

Run the following command to make sure it has the correct permission:

```
$ chmod 710 ~/.esmtprc

```
Then repeat the test with `message.txt` exactly as before.

#### Example with opensmtpd

```
# pacman -S opensmtpd

```

Edit `/etc/smtpd/smtpd.conf`. The following configuration allows for local delivery:

```
listen on localhost
accept for local deliver to mbox

```

You can proceed to test it:

```
# systemctl start smtpd
$ echo test | sendmail user

```

*user* can check his/her mail in with any [reader](/index.php/Category:Email_clients "Category:Email clients") able to handle mbox format, or just have a look at the file `/var/spool/mail/*user*`. If everything goes as expected, you can enable opensmtpd for future boots:

```
# systemctl enable smtpd

```

This approach has the advantage of not sending local cron notifications to a remote server. Not even network connection is needed. On the downside, you need a new daemon running.

**Note:** At the moment of writing the Arch opensmtpd package does not create all needed directories under `/var/spool/smtpd`, but the daemon will warn about that specifying the required ownerships and permissions. Just create them as suggested.

**Note:** Even though the suggested configuration does not accept remote connections, it's a healthy precaution to add an additional layer of security blocking port 25 with [iptables](/index.php/Iptables "Iptables") or similar.

#### Long cron job

Suppose this program is invoked by cron :

```
#!/bin/sh
echo "I had a recoverable error!"
sleep 1h

```

What happens is this:

1.  cron runs the script
2.  as soon as cron sees some output, it runs your MTA, and provides it with the headers. It leaves the pipe open, because the job hasn't finished and there might be more output.
3.  the MTA opens the connection to postfix and leaves that connection open while it waits for the rest of the body.
4.  postfix closes the idle connection after less than an hour and you get an error like this :

```
smtpmsg='421 … Error: timeout exceeded' errormsg='the server did not accept the mail'

```

To solve this problem you can use the command chronic or sponge from [moreutils](https://www.archlinux.org/packages/?name=moreutils). From their respective man page:

	chronic

	chronic runs a command, and arranges for its standard out and standard error to only be displayed if the command fails (exits nonzero or crashes). If the command succeeds, any extraneous output will be hidden.

	sponge

	sponge reads standard input and writes it out to the specified file. Unlike a shell redirect, sponge soaks up all its input before opening the output file… If no output file is specified, sponge outputs to stdout.

Even if it's not said chronic buffer the command output before opening its standard output (like sponge does).

## Crontab format

The basic format for a crontab is:

```
<minute> <hour> <day_of_month> <month> <day_of_week> <command>

```

*   *minute* values can be from 0 to 59.
*   *hour* values can be from 0 to 23.
*   *day_of_month* values can be from 1 to 31.
*   *month* values can be from 1 to 12.
*   *day_of_week* values can be from 0 to 6, with 0 denoting Sunday.

Multiple times may be specified with a comma, a range can be given with a hyphen, and the asterisk symbol is a wildcard character. Spaces are used to separate fields. For example, the line:

```
*0,*5 9-16 * 1-5,9-12 1-5 ~/bin/i_love_cron.sh

```

Will execute the script `i_love_cron.sh` at five minute intervals from 9 AM to 4:55 PM on weekdays except during the summer months (June, July, and August). More examples and advanced configuration techniques can be found below.

## Basic commands

Crontabs should never be edited directly; instead, users should use the `crontab` program to work with their crontabs. To be granted access to this command, user must be a member of the users group (see the `gpasswd` command).

To view their crontabs, users should issue the command:

```
$ crontab -l

```

To edit their crontabs, they may use:

```
$ crontab -e

```

To remove their crontabs, they should use:

```
$ crontab -r

```

If a user has a saved crontab and would like to completely overwrite their old crontab, he or she should use:

```
$ crontab *saved_crontab_filename*

```

To overwrite a crontab from the command line ([Wikipedia:stdin](https://en.wikipedia.org/wiki/stdin "wikipedia:stdin")), use

```
$ crontab - 

```

To edit somebody else's crontab, issue the following command as root:

```
# crontab -u *username* -e

```

This same format (appending `-u *username*` to a command) works for listing and deleting crontabs as well.

## Examples

The entry:

```
01 * * * * /bin/echo Hello, world!

```

runs the command `/bin/echo Hello, world!` on the first minute of every hour of every day of every month (i.e. at 12:01, 1:01, 2:01, etc.)

Similarly,

```
*/5 * * jan mon-fri /bin/echo Hello, world!

```

runs the same job every five minutes on weekdays during the month of January (i.e. at 12:00, 12:05, 12:10, etc.)

As noted in the *Crontab Format* section, the line:

```
*0,*5 9-16 * 1-5,9-12 1-5 /home/user/bin/i_love_cron.sh

```

Will execute the script `i_love_cron.sh` at five minute intervals from 9 AM to 5 PM (excluding 5 PM itself) every weekday (Mon-Fri) of every month except during the summer (June, July, and August).

## Default editor

To use an alternate default editor, define the EDITOR envar it in a shell initialization script ([vim-default-editor](https://aur.archlinux.org/packages/vim-default-editor/) is available in the AUR for vim users). For example:

 `/etc/profile.d/nano-default-editor` 
```
#!/bin/sh

export EDITOR=/usr/bin/nano
```

As a regular user, `su` will need to be used instead of `sudo` for the envar to be pulled correctly:

```
su -c "crontab -e"

```

To have an alias to this `printf` is required to carry the arbitrary string because `su` launches in a new shell:

```
alias scron="su -c $(printf "%q " "crontab -e")"

```

## More information

The cron daemon parses a configuration file known as `crontab`. Each user on the system can maintain a separate crontab file to schedule commands individually. The root user's crontab is used to schedule system-wide tasks (though users may opt to use `/etc/crontab` or the `/etc/cron.d` directory, depending on which cron implementation they choose).

There are slight differences between the crontab formats of the different cron daemons. The default root crontab for dcron looks like this:

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

## run-parts issue

cronie uses `run-parts` to carry out script in `cron.daily`/`cron.weekly`/`cron.monthly`. Be careful that the script name in these won't include a dot (.), e.g. `backup.sh`, since `run-parts` without options will ignore them (see: `man run-parts`).

## Running Xorg server based applications

If you find that you can't run X apps from cron jobs then use this prefix:

```
export DISPLAY=:0.0 ;

```

This sets the `DISPLAY` variable to the first display, which is usually right unless you run multiple X servers on your machine.

If it still doesn't work, then you need to use `xhost` to give your user control over X:

```
# xhost +si:localuser:$(whoami)

```

## Asynchronous job processing

If you regularly turn off your computer but do not want to miss jobs, there are some solutions available (easiest to hardest):

### Dcron

Vanilla dcron supports asynchronous job processing. Just put it with @hourly, @daily, @weekly or @monthly with a jobname, like this:

```
@hourly         ID=greatest_ever_job      echo This job is very useful.

```

### Cronwhip

([AUR](https://aur.archlinux.org/packages.php?ID=21079), [forum thread](https://bbs.archlinux.org/viewtopic.php?id=57973)): Script to automatically run missed cron jobs; works with the former default cron implementation, dcron.

### Anacron

([AUR](https://aur.archlinux.org/packages.php?ID=5196)): Full replacement for dcron, processes jobs asynchronously.

### Fcron

([Community](https://www.archlinux.org/packages/community/i686/fcron/), [forum thread](https://bbs.archlinux.org/viewtopic.php?id=140497)): Like anacron, fcron assumes the computer is not always running and, unlike anacron, it can schedule events at intervals shorter than a single day. Like cronwhip, it can run jobs that should have been run during the computer's downtime.

## Ensuring exclusivity

If you run potentially long-running jobs (e.g., a backup might all of a sudden run for a long time, because of many changes or a particular slow network connection), then [lockrun](https://aur.archlinux.org/packages/lockrun/) can ensure that the cron job won't start a second time.

```
  5,35 * * * * /usr/bin/lockrun -n /tmp/lock.backup /root/make-backup.sh

```

## See Also

*   [젠투 리눅스 Cron 설명서](https://wiki.gentoo.org/wiki/Cron)
*   [CronTab Usage Tutorial](http://gotux.net/arch-linux/crontab-usage/)