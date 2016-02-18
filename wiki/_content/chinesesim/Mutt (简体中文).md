## Contents

*   [1 简介](#.E7.AE.80.E4.BB.8B)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 IMAP](#IMAP)
    *   [3.1 内置IMAP](#.E5.86.85.E7.BD.AEIMAP)
    *   [3.2 OfflineIMAP](#OfflineIMAP)
*   [4 POP3](#POP3)
    *   [4.1 内置POP3](#.E5.86.85.E7.BD.AEPOP3)
    *   [4.2 getmail](#getmail)
*   [5 Procmail](#Procmail)
*   [6 SMTP](#SMTP)
    *   [6.1 发送邮件](#.E5.8F.91.E9.80.81.E9.82.AE.E4.BB.B6)
*   [7 其他](#.E5.85.B6.E4.BB.96)
    *   [7.1 邮件签名](#.E9.82.AE.E4.BB.B6.E7.AD.BE.E5.90.8D)
    *   [7.2 用Firefox查看URL链接](#.E7.94.A8Firefox.E6.9F.A5.E7.9C.8BURL.E9.93.BE.E6.8E.A5)
    *   [7.3 Mutt 和 Vim](#Mutt_.E5.92.8C_Vim)
    *   [7.4 一行命令发送邮件](#.E4.B8.80.E8.A1.8C.E5.91.BD.E4.BB.A4.E5.8F.91.E9.80.81.E9.82.AE.E4.BB.B6)
    *   [7.5 附件的中文文件名显示乱码](#.E9.99.84.E4.BB.B6.E7.9A.84.E4.B8.AD.E6.96.87.E6.96.87.E4.BB.B6.E5.90.8D.E6.98.BE.E7.A4.BA.E4.B9.B1.E7.A0.81)
    *   [7.6 编码问题](#.E7.BC.96.E7.A0.81.E9.97.AE.E9.A2.98)

## 简介

Mutt是一个基于ncurse的Email客戶端。

本文使用：

*   offlineimap 下载IMAP协议的邮件(Mutt内置的IMAP协议无法下载)
*   [getmail](http://pyropus.ca/software/getmail/) 下载POP3协议的邮件
*   procmail 过滤邮件
*   msmtp 发送邮件

## 安装

通过下列命令进行安装。

 `# pacman -S mutt offlineimap getmail procmail msmtp` 

修改配置文件

 `~/.muttrc` 
```
set mbox_type=Maildir
set folder=$HOME/.mail
set spoolfile=~/.mail/
set header_cache=~/.mail/.hcache
```

spoolfile里要有cur，new和tmp三个文件夹。

 `$ mkdir -p ~/.mail/{cur,new,tmp} ` 

这是一个最精简的配置文件，能让你访问你的Maildir，并在收件箱（INBOX）中检查新Email。

spoolfile告诉Mutt从本地哪个目录来得到新Email。这里我们改到用户目录下。你还可以添加更多的Spoolfiles，例如邮件列表所在的目录。

## IMAP

### 内置IMAP

运行下列命令，如果有+IMAP则说明Mutt已经编译进了内置IMAP支持。Arch源里的Mutt默认开启。

 `$ mutt -v` 

### OfflineIMAP

首先要启用Community软件库，并通过一个简单的命令 `pacman -S offlineimap` 来安装 OfflineIMAP。 现在你要按自己的需要来设置好它。创建一个文件`~/.offlineimaprc` 并用你喜爱的编辑器来编辑它。下面是一个配置文件的例子。可按自己的需要来编辑它。

```
[general]
accounts = myaccount # change to whatever you want
ui = Curses.Blinkenlights # Gives you a nice blinky output on the console so you know what's happening.
# ui = Noninteractive.Quiet # If uncommented, this would show nothing at all. Great for cronjobs or background-processes

[Account myaccount]
localrepository = mylocal # Profile-Name for the local Mails for a given Account
remoterepository = myremote # Profile-Name for the remote Mails for a given Account
autorefresh = 5 # fetches your mails every 5 Minutes

[Repository mylocal]
type = Maildir # Way of storing Mails locally. Only Maildir is currently supported
localfolders = ~/Mail # Place where the synced Mails should be

[Repository myremote]
type = IMAP # Type of remote Mailbox. Only IMAP is supported right now.
remotehost = imap.myhost.com # Where to connect
ssl = yes # Whether to use SSL or not
# remoteport = 993 # Would specify a port if uncommented. That way, it just tries to use a default-port
remoteuser = myremoteusername # Login-Name
remotepass = myremotepassword # Login-Password. -- ACHTUNG! Of course, this is not too safe. Make sure that the file is readable only by you. Even better: use some of the suggestions in the OfflineIMAP-Manual to make it safer.
```

这是让你能运行起来的最小设置了。更多高级的特性，请参看OfflineIMAP的主页，再回头看一看[annotated offlineimaprc](http://software.complete.org/offlineimap/browser/offlineimap.conf).

现在就快准备好运行OfflineIMAP了。创建一个已经在offlineimaprc中定义好的目录，就f像这样： `mkdir ~/Mail`。然后运行`offlineimap`。你的Email就会同步到本地电脑上了。如果出了什么错，就仔细查看一下错误消息。通常OfflineIMAP对于问题的提示在文字上是比较详尽的。

## POP3

### 内置POP3

### getmail

编辑`~/.getmail/getmailrc`

下面是一个使用Gmail的例子。

 `~/.getmail/getmailrc` 
```
[retriever]
type = SimplePOP3SSLRetriever
server = pop.gmail.com
username = username@gmail.com
port = 995
password = password

[destination]
type = Maildir
path = ~/mail/
```

你可以参考更多配置文件`/usr/share/doc/getmail-4.20.0/getmailrc-example`

现在可以运行getmail了。如果它正常工作，可以为getmail创建一个计划任务[Cron](/index.php/Cron "Cron")，让它每隔一段时间就运行一次。 此设置可以每隔三十分钟，运行一次`getmail` 。

```
$ crontab -e
$ */30 * * * * /usr/bin/getmail
```

## Procmail

[Procmail](http://www.procmail.org/)是一个強大的邮件分捡工具。

修改getmail设置

 `getmailrc` 
```
[destination]
type = MDA_external
path = /usr/bin/procmail
```

配置procmail，下面将对来自happy-kangaroos 邮件列表，以及来自亲朋好友的所有Email作一个排序，每个人都有各自的Maildir。

 `.procmailrc` 
```
MAILDIR=$HOME/mail
DEFAULT=$MAILDIR/inbox/
LOGFILE=$MAILDIR/log

:0:
* ^To: happy-kangaroos@nicehost.com
happy-kangaroos/

:0:
* ^From: loveydovey@iheartyou.net
lovey-dovey/
```

保存`.procmailrc`后，运行getmail，看看它是否在适当的目录中对你的邮件成功排序了。

## SMTP

无论你是用 POP 还是 IMAP 来接收Email，都可能要用SMTP来发送邮件。

### 发送邮件

[Msmtp](http://msmtp.sourceforge.net/)是一个很简单易用的SMTP客戶端。它在`[extra]`软件库中。

```
 pacman -S msmtp

```

用编辑器打开 `~/.msmtprc` 。下面是一个使用Gmail帐戶的 `.msmtprc` 配置例子:

```
account default
host smtp.gmail.com
port 587
protocol smtp
auth on
from username@gmail.com
user username@gmail.com
password mypassword
tls on
tls_starttls on

```

仅用戶本人才能有此文件的读写权限：

 `chmod 600 ~/.msmtprc` 

用 1.4.11 版的 msmtp 时，必然要涉及到设定 TLS 。 [msmtp, TLS, and ArchLinux](http://mychael.gotdns.com/blog/2007/04/18/msmtp-tls-and-archlinux/) 对于如何配置 msmtp 的认证作出了指导。

现在 mutt 一定已经为使用msmtp作好了配置工作。建一个目录： `~/.mutt/`，并打开了 `~/.mutt/muttrc` 。下面的配置文件会让你开始查看和发送Email。

```
set realname='Disgruntled Kangaroo'

set sendmail="/usr/bin/msmtp"

set edit_headers=yes
set folder=~/mail
set mbox=+mbox
set spoolfile=+inbox
set record=+sent
set postponed=+drafts
set mbox_type=Maildir

mailboxes +inbox +lovey-dovey +happy-kangaroos
```

现在，启动 mutt。你会在 `~/mail/inbox` 看到所有的邮件。按下 `m`键来撰写邮件， (它会使用 `EDITOR` 环境变量中定义好的编辑器。如果这个变量还沒有被设定，那么可键入 `export EDITOR=/path/to/yourfavorite/editor` 。想要测试一下，可以给自己发一封邮件。写好信后，在你的编辑器中保存它。再返回到Mutt中，它会显示出这封邮件的消息。按 `y` 来发送它。如果都正常，那么就恭喜了！你能用Mutt了！不过呢，要实现Mutt真正強大的能力，还要作一些进一步的定制才行啊。

一份关于使用与定制Mutt的指南：

*   [My first mutt](http://mutt.blackfish.org.uk/) (由Bruno Postle维护)

[xterminus](/index.php/User:Xterminus "User:Xterminus") 是mutt社区中相当活跃的人。可以从 [Code and Configs Page](http://xtermin.us/code/#muttstuff) 找到他的个人配置文件。如果你有什么特別的问题，请随意在 [the irc channel](/index.php/ArchChannel "ArchChannel") 上提问。

## 其他

### 邮件签名

在你的家目录（$HOME）中创建一个 `.signature` 文件。你的签名会在附在邮件的后面。

### 用Firefox查看URL链接

你可以在$HOME创建一个 `./mutt` 目录，如果沒有的话。 再创建一个名为 macros 的文件。 加入下面的內容：

```
 macro pager \cb <pipe-entry>'urlview'<enter> 'Follow links with urlview'

```

然后安装 urlview ：

```
pacman -S urlview

```

在$HOME创建一个 .urlview 文件，并加入下面的內容：

```
REGEXP (((http|https|ftp|gopher)|mailto)[.:][^ >"\t]*|www\.[-a-z0-9.]+)[^ .,;\t>">\):]
COMMAND firefox %s 

```

当用Mutt阅读邮件时，点击 ctrl+b ，将会列出邮件中所有的超级链接 urls 。用箭头按键上下翻动它们，然后在要访问的链接上点击 enter 。Firefox 将启动，并访问那个站点了。

### Mutt 和 Vim

要将文本的宽度限制在 72 个字符， 可编辑你的 .vimrc 文件，并加入：

```
au BufRead /tmp/mutt-* set tw=72

```

这样，Vim 只有在你使用 Mutt 的时候，都会有上面的行为了。

要设置另外一个临时文件目录，如 ~/.tmp，可在你的 .muttrc 文件中加上一行，如下所示：

```
set tmpdir="~/.tmp"

```

要重新格式化一个调整过的文本，可参看 Vim 的帮助文件：

```
:h 10.7

```

### 一行命令发送邮件

便于命令行使用，或者和cron组合完成自动发送邮件，或者自动发送文件进行备份。

```
mutt -s "this is a great subject" myfriend@gmail.com -a attach.tar.gz < /path/to/content

```

### 附件的中文文件名显示乱码

解决中文附件名为乱码的问题

```
set rfc2047_parameters=yes

```

### 编码问题

如果中文Email有编码问题的话，可能是因为用GBK比用GB2312好。你可以用`iconv`来自动得兑换编码。先修改`mailcap`文件：

```
text/plain; iconv -f gbk -t utf-8 %s; test=echo "%{charset}" | grep -ic "gb2312"; copiousoutput;

```

然后修改配置文件：

 `.muttrc`  `auto_view text/plain` 

也可以把`mailcap`的HTML部分修改以下，用`$(echo %{charset} | sed s/gb2312/gbk/I)`来代替`%{charset}`，比如说：

```
text/html; w3m -dump -I $(echo %{charset} | sed s/gb2312/gbk/I) %s; nametemplate=%s.html; copiousoutput

```