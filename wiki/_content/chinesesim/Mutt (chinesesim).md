Mutt是一个基于文本的邮件客户端，因其强大的功能而闻名。 Mutt虽然已诞生二十多年了，但仍然是大量用户的首选邮件客户端。

Mutt主要侧重于作为邮件用户代理（MUA），最初是为了查看邮件而编写的。 与其他邮件应用程序相比，稍后实现的功能（检索，发送和过滤邮件）比较简单，因此用户可能希望使用外部应用程序来扩展Mutt的功能。

尽管如此，Arch Linux [mutt](https://www.archlinux.org/packages/?name=mutt)软件包编译支持IMAP，POP3和SMTP协议，从而消除了外部应用程序的必要性。

本文内容包括使用本地IMAP发送和检索邮件，设置如何使用[OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP")或[getmail](/index.php/Getmail "Getmail")（POP3协议）来检索邮件，使用[procmail](/index.php/Procmail "Procmail")通过POP3协议过滤邮件，使用[msmtp](/index.php/Msmtp "Msmtp")发送邮件。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 NeoMutt](#NeoMutt)
*   [2 配置](#配置)
*   [3 IMAP](#IMAP)
    *   [3.1 内置IMAP](#内置IMAP)
    *   [3.2 OfflineIMAP](#OfflineIMAP)
*   [4 POP3](#POP3)
    *   [4.1 内置POP3](#内置POP3)
    *   [4.2 getmail](#getmail)
*   [5 Procmail](#Procmail)
*   [6 SMTP](#SMTP)
    *   [6.1 发送邮件](#发送邮件)
*   [7 其他](#其他)
    *   [7.1 邮件签名](#邮件签名)
    *   [7.2 用Firefox查看URL链接](#用Firefox查看URL链接)
    *   [7.3 Mutt 和 Vim](#Mutt_和_Vim)
    *   [7.4 一行命令发送邮件](#一行命令发送邮件)
    *   [7.5 附件的中文文件名显示乱码](#附件的中文文件名显示乱码)
    *   [7.6 编码问题](#编码问题)

## 安装

安装 [mutt](https://www.archlinux.org/packages/?name=mutt) 包，或者考虑使用 [#NeoMutt](#NeoMutt) 包代替。

可以考虑为IMAP程序安装外部帮助程序，例如 [isync](/index.php/Isync "Isync")，[OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") 或者 [msmtp](/index.php/Msmtp "Msmtp")。

如果使用 POP3，安装 [getmail](https://www.archlinux.org/packages/?name=getmail)， [fetchmail](https://aur.archlinux.org/packages/fetchmail/) 或者 [fdm](https://www.archlinux.org/packages/?name=fdm) 和 [procmail](https://www.archlinux.org/packages/?name=procmail)。

**注意:**

*   如果仅仅使用明文登录认证方式，[libsasl](https://www.archlinux.org/packages/?name=libsasl) 包可以满足要求。
*   如果使用 CRAM-MD5, GSSAPI 或者 DIGEST-MD5, 安装 [cyrus-sasl-gssapi](https://www.archlinux.org/packages/?name=cyrus-sasl-gssapi) 包。
*   如果使用 Gmail 作为 SMTP 服务器, 需要安装 [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl) 包。

### NeoMutt

[NeoMutt](http://www.neomutt.org/) 项目旨在汇集 Mutt 的所有补丁。它增加了很多[功能](http://www.neomutt.org/feature.html)。许多旧的 Mutt 补丁已经被更新，整理和记录。

AUR 中有许多不同的 mutt 包，每个都提供了不同的补丁，NeoMutt 计划在未来通过适当的编译选项来替代它们。现在，可以在AUR中通过 [neomutt](https://www.archlinux.org/packages/?name=neomutt) 和 [neomutt-git](https://aur.archlinux.org/packages/neomutt-git/) 找到NeoMutt。

## 配置

本章节包含 [#IMAP](#IMAP), [#POP3](#POP3), [#Maildir](#Maildir) 和 [#SMTP](#SMTP) 的配置。

Mutt 默认识别两个位置的配置文件： `~/.muttrc` 和 `~/.mutt/muttrc`。 任何一个配置文件都可以工作。 如果决定将初始化文件放在其他地方，使用

```
 `$ mutt -F /path/to/.muttrc`。

```

You should also know some prerequisite for Mutt configuration. Its syntax is very close to the Bourne Shell. For example, you can get the content of another config file:

```
source /path/to/other/config/file

```

Mutt 配置的语法非常接近Bourne Shell。 例如，可以获取另一个配置文件的内容：

```
source /path/to/other/config/file

```

可以使用变量并将 shell 命令的结果赋值给变量。

```
set editor=`echo \$EDITOR`

```

`$` 符号被转义，这样在传递给 shell 之前它不会被 Mutt 替换。 还要注意使用反引号，因为 bash 语法 `$（...）` 不起作用。 Mutt 有很多预定义的变量，但是也可以自己定义变量。用户变量 **必须以 "my" 开头**！

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
COMMAND firefox %s 

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
text/plain; iconv -f gbk -t utf-8 %s; test=echo "%{charset}" | grep -ic "gb2312"; copiousoutput;

```

然后修改配置文件：

 `.muttrc`  `auto_view text/plain` 

也可以把`mailcap`的HTML部分修改以下，用`$(echo %{charset} | sed s/gb2312/gbk/I)`来代替`%{charset}`，比如说：

```
text/html; w3m -dump -I $(echo %{charset} | sed s/gb2312/gbk/I) %s; nametemplate=%s.html; copiousoutput

```