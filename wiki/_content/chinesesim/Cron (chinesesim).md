相关文章

*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")

摘自 [Wikipedia](https://en.wikipedia.org/wiki/Cron "wikipedia:Cron"):

	*cron* 是一个在 Unix 及类似操作系统上执行计划任务的程序。用户可以在指定的时间段周期性地运行命令或 shell 脚本，通常用于系统的自动化维护或者管理。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 激活及开机启动](#.E6.BF.80.E6.B4.BB.E5.8F.8A.E5.BC.80.E6.9C.BA.E5.90.AF.E5.8A.A8)
    *   [3.1 处理任务中的错误](#.E5.A4.84.E7.90.86.E4.BB.BB.E5.8A.A1.E4.B8.AD.E7.9A.84.E9.94.99.E8.AF.AF)
        *   [3.1.1 使用 ssmtp](#.E4.BD.BF.E7.94.A8_ssmtp)
        *   [3.1.2 Example with msmtp](#Example_with_msmtp)
        *   [3.1.3 Example with esmtp](#Example_with_esmtp)
        *   [3.1.4 Example with opensmtpd](#Example_with_opensmtpd)
        *   [3.1.5 Long cron job](#Long_cron_job)
*   [4 Crontab 格式](#Crontab_.E6.A0.BC.E5.BC.8F)
*   [5 基本命令](#.E5.9F.BA.E6.9C.AC.E5.91.BD.E4.BB.A4)
*   [6 范例](#.E8.8C.83.E4.BE.8B)
*   [7 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)
*   [8 run-parts issue](#run-parts_issue)
*   [9 运行 X 程序](#.E8.BF.90.E8.A1.8C_X_.E7.A8.8B.E5.BA.8F)
*   [10 Asynchronous job processing](#Asynchronous_job_processing)
    *   [10.1 Dcron](#Dcron)
    *   [10.2 Cronwhip](#Cronwhip)
    *   [10.3 Anacron](#Anacron)
    *   [10.4 Fcron](#Fcron)
*   [11 参见](#.E5.8F.82.E8.A7.81)

## 安装

cron 有多个实现程序，但是基础系统默认使用 [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")，都没用安装，用户可以选择其一进行安装。[Gentoo Linux Cron 指南](http://www.gentoo.org/doc/en/cron-guide.xml) 提供了一个这些实现之间的比较。软件包:

*   [cronie](https://www.archlinux.org/packages/?name=cronie)
*   [fcron](https://www.archlinux.org/packages/?name=fcron)
*   [dcron](https://aur.archlinux.org/packages/dcron/)
*   [vixie-cron](https://aur.archlinux.org/packages/vixie-cron/)
*   [scron-git](https://aur.archlinux.org/packages/scron-git/)

## 配置

## 激活及开机启动

安装后，默认的守护进程不会启动。安装的软件包都提供了可以用 [systemctl](/index.php/Systemd#Using_units "Systemd") 控制的服务文件。例如 *cronie* 使用 `cronie.service`.

`/etc/cron.daily/` 目录包含当前的任务，启动 cron 服务时会触发所有当天任务。

**Note:** *cronie* 提供了 `0anacron`任务，每小时执行一次，可以执行其它因为未开机而延迟的任务。

### 处理任务中的错误

cron 会记录 *stdout* 和 *stderr* 的输出并尝试通过 `sendmail` 命令发送邮件给用户。如果 Cronie 未找到 `/usr/bin/sendmail`，则会禁用邮件通知。要发送邮件到用户的 spool，需要在系统上运行 smtp 进程，例如 [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd)。也可以安装提供 sendmail 命令的软件包，然后配置成通过外部邮件服务器发送邮件。或者使用 `-m` 选项将错误记录到日志并通过定制的脚本进行处理。

**Tip:** 通过 [Postfix#Local mail](/index.php/Postfix#Local_mail "Postfix") 可以发送邮件到本地系统。

1.  [编辑](/index.php/Edit "Edit") `cronie.service` 服务。
2.  安装 [esmtp](https://www.archlinux.org/packages/?name=esmtp), [msmtp](/index.php/Msmtp "Msmtp"), [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd), [ssmtp](/index.php/SSMTP "SSMTP") 或编写自定义脚本。

#### 使用 ssmtp

ssmtp 是一个仅包含发送功能的 sendmail 模拟器，可以从本地计算机向 smtp 服务器发送邮件。尽管目前已经没用活跃维护者，这个程序依然是发送邮件的最简单方式。没用需要运行的后台进程，最简单的配置只需要一个包含三行内容的配置文件(发送服务提供商支持未认证转发的时候)。ssmtp 无法收取邮件、展开扩展或管理队列。

安装 [ssmtp](https://www.archlinux.org/packages/?name=ssmtp)，安装时会创建 `/usr/bin/sendmail` 链接，指向 `/usr/bin/ssmtp`. 安装后编辑 `/etc/ssmtp/ssmtp.conf` 配置文件。详情请参考 [ssmtp](/index.php/SSMTP "SSMTP")，到 `/usr/bin/sendmail` 的软链接可以确保 [S-nail](/index.php/S-nail "S-nail") 等提供 `/usr/bin/mail` 的程序可以无需修改直接使用。

安装配置完成后重启 `cronie` 以重新确认 `/usr/bin/sendmail` 已经被安装。

#### Example with msmtp

Install [msmtp-mta](https://www.archlinux.org/packages/?name=msmtp-mta), which creates a symbolic link from `/usr/bin/sendmail` to `/usr/bin/msmtp`. Restart `cronie` to make sure it detects the new `sendmail` command. You must then provide a way for `msmtp` to convert your username into an email address.

Then either add `MAILTO` line to your crontab, like so:

```
MAILTO=your@email.com

```

**or** create `/etc/msmtprc` and append this line:

```
aliases /etc/aliases

```

and create `/etc/aliases`:

```
your_username: your@email.com
# Optional:
default: your@email.com

```

Then [modify the configuration](/index.php/Systemd#Editing_provided_units "Systemd") of *cronie* daemon by replacing the `ExecStart` command with:

```
ExecStart=/usr/bin/crond -n -m '/usr/bin/msmtp -t'

```

#### Example with esmtp

Install [esmtp](https://www.archlinux.org/packages/?name=esmtp) and [procmail](https://www.archlinux.org/packages/?name=procmail).

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

Install [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd).

Edit `/etc/smtpd/smtpd.conf`. The following configuration allows for local delivery:

```
listen on localhost
accept for local deliver to mbox

```

You can proceed to test it. First [start](/index.php/Start "Start") `smtpd.service`. Then do:

```
$ echo test | sendmail user

```

*user* can check his/her mail in with any [reader](/index.php/Category:Email_clients "Category:Email clients") able to handle mbox format, or just have a look at the file `/var/spool/mail/*user*`. If everything goes as expected, you can [enable](/index.php/Enable "Enable") opensmtpd for future boots.

This approach has the advantage of not sending local cron notifications to a remote server. On the downside, you need a new daemon running.

**Note:**

*   At the moment of writing the Arch opensmtpd package does not create all needed directories under `/var/spool/smtpd`, but the daemon will warn about that specifying the required ownerships and permissions. Just create them as suggested.
*   Even though the suggested configuration does not accept remote connections, it's a healthy precaution to add an additional layer of security blocking port 25 with [iptables](/index.php/Iptables "Iptables") or similar.

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

Chronic too buffers the command output before opening its standard output.

## Crontab 格式

crontab 的基本格式是：

```
<分钟> <小时> <日> <月份> <星期> <命令>

```

*   *分钟* 值从 0 到 59.
*   *小时* 值从 0 到 23.
*   *日* 值从 1 到 31.
*   *月* 值从 1 到 12.
*   *星期* 值从 0 到 6, 0 代表星期日.

多个时间可以用逗号隔开，范围可以用连字符给出，星号可以作为通配符。空格用来分开字段。例如，下面一行：

```
*0,*5 9-16 * 1-5,9-12 1-5 /home/user/bin/i_love_cron.sh

```

会在夏天(六、七、八月)之外的每周周一到周五的上午9点到下午4点之间每5分钟执行一次 `i_love_cron.sh`。更多范例和高级配置方法见下文。

## 基本命令

Crontabs 不应该直接编辑；用户应该使用 *crontab* 程序来处理他们的 crontabs。为了能够访问这个命令，用户必须添加到 users 用户组 (见 gpasswd 命令).

要查看 crontabs，用户应该运行下面的命令：

```
$ crontab -l

```

要编辑 crontabs，可以使用：

```
$ crontab -e

```

要移除 crontabs, 可以使用：

```
$ crontab -d

```

如果用户有一个保存好的 crontab 想要用它完全覆盖旧的 crontab，可以使用：

```
$ crontab *saved_crontab_filename*

```

想从命令行([Wikipedia:stdin](https://en.wikipedia.org/wiki/stdin "wikipedia:stdin"))覆盖一个 crontab，使用：

```
$ crontab - 

```

想编辑别的用户的 crontab, 使用root运行下面的命令:

```
# crontab -u *username* -e

```

同一个格式 (追加 "-u *username*" 到命令后) 也可以用来列出或删除 crontabs。

如果想使用 nano 而不是 vi 作为 crontab 编辑器，添加下面的变量到 `/etc/bash.bashrc`:

```
export EDITOR="/usr/bin/nano"

```

然后重启终端

## 范例

下面的条目:

```
01 * * * * /bin/echo Hello, world!

```

将会在每个月的每一天的每一个小时的第一分钟（例如，在12：01，1：01，2：01等）执行命令 `/bin/echo Hello, world!`

类似地,

```
*/5 * * jan mon-fri /bin/echo Hello, world!

```

将会在一月的每个工作日每五分钟（例如，在12：00，12：05，12：10等）执行一次相同的命令。

As noted in the *Crontab Format* section, the line:

```
*0,*5 9-16 * 1-5,9-12 1-5 /home/user/bin/i_love_cron.sh

```

Will execute the script `i_love_cron.sh` at five minute intervals from 9 AM to 5 PM (excluding 5 PM itself) every weekday (Mon-Fri) of every month except during the summer (June, July, and August).

## 更多信息

The cron daemon parses a configuration file known as *crontab*. Each user on the system can maintain a separate crontab file to schedule commands individually. The root user's crontab is used to schedule system-wide tasks (though users may opt to use `/etc/crontab` or the `/etc/cron.d` directory, depending on which cron implementation they choose).

There are slight differences between the crontab formats of the different cron daemons. The default root crontab for dcron looks like this:

```
/var/spool/cron/root

```

```
# root crontab
# DO NOT EDIT THIS FILE MANUALLY! USE crontab -e INSTEAD

# man 1 crontab for acceptable formats:
#    <minute> <hour> <day> <month> <dow> <tags and command>
#    <@freq> <tags and command>

# SYSTEM DAILY/WEEKLY/... FOLDERS
@hourly         ID=sys-hourly   /usr/sbin/run-cron /etc/cron.hourly
@daily          ID=sys-daily    /usr/sbin/run-cron /etc/cron.daily
@weekly         ID=sys-weekly   /usr/sbin/run-cron /etc/cron.weekly
@monthly        ID=sys-monthly  /usr/sbin/run-cron /etc/cron.monthly

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

cronie使用run-parts来执行在cron.hourly/cron.daily/cron.weekly/cron.monthly里的脚本。 请注意这些文件夹里的脚本名字中不应该含有'.'，因为不含有任何参数的run-parts将会忽略他们。例如backup.sh这个脚本是不会被执行的，请将其改名为backup或者其他不含有'.'的名字以定时执行该脚本。 要获取更详细的信息请 man run-parts

## 运行 X 程序

If you find that you cannot run X apps from cron jobs then put this before the command:

```
export DISPLAY=:0.0 ;

```

That sets the DISPLAY variable to the first display; which is usually right unless you like to run multiple xservers on your machine.

If it still does not work then you need to use xhost to give your user control over X11:

```
# xhost +si:localuser:$(whoami)

```

I put it in my gnome `Startup Applications' like this:

```
bash -c "xhost +si:localuser:$(whoami)"

```

## Asynchronous job processing

If you regularly turn off your computer but do not want to miss jobs, there are some solutions available (easiest to hardest):

### Dcron

Vanilla dcron supports asynchronous job processing. Just put it with @hourly, @daily, @weekly or @monthly with a jobname, like this:

```
@hourly         ID=greatest_ever_job      echo This job is very useful.

```

### Cronwhip

([AUR](https://aur.archlinux.org/packages.php?ID=21079), [forum thread](https://bbs.archlinux.org/viewtopic.php?id=57973)): Script to automatically run missed cron jobs; works with the default cron implementation, dcron.

### Anacron

([AUR](https://aur.archlinux.org/packages.php?ID=5196)): Full replacement for dcron, processes jobs asynchronously.

### Fcron

([Community](https://www.archlinux.org/packages/community/i686/fcron/), [forum thread](https://bbs.archlinux.org/viewtopic.php?id=140497)): Like anacron, fcron assumes the computer is not always running and, unlike anacron, it can schedule events at intervals shorter than a single day. Like cronwhip, it can run jobs that should have been run during the computer's downtime.

## 参见

*   [Gentoo Linux Cron 指南](http://www.gentoo.org/doc/en/cron-guide.xml)