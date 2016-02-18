[rTorrent](http://libtorrent.rakshasa.no/) 是一个非常简洁、优秀、非常轻量的BT客户端. 它使用了 [ncurses](https://en.wikipedia.org/wiki/ncurses 的低端系统上作为远程的 BT 客户端是非常理想的。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 性能优化](#.E6.80.A7.E8.83.BD.E4.BC.98.E5.8C.96)
    *   [2.2 创建和管理文件](#.E5.88.9B.E5.BB.BA.E5.92.8C.E7.AE.A1.E7.90.86.E6.96.87.E4.BB.B6)
    *   [2.3 端口配置](#.E7.AB.AF.E5.8F.A3.E9.85.8D.E7.BD.AE)
    *   [2.4 附加设置](#.E9.99.84.E5.8A.A0.E8.AE.BE.E7.BD.AE)
*   [3 管理](#.E7.AE.A1.E7.90.86)
    *   [3.1 Redundant mapping](#Redundant_mapping)
*   [4 通过Screen使用rTorrent](#.E9.80.9A.E8.BF.87Screen.E4.BD.BF.E7.94.A8rTorrent)
    *   [4.1 On a remote machine](#On_a_remote_machine)
    *   [4.2 Screen后台运行rTorrent](#Screen.E5.90.8E.E5.8F.B0.E8.BF.90.E8.A1.8CrTorrent)
*   [5 其他提示](#.E5.85.B6.E4.BB.96.E6.8F.90.E7.A4.BA)
    *   [5.1 Send Text Message Upon Torrent Completion Using GMail](#Send_Text_Message_Upon_Torrent_Completion_Using_GMail)
*   [6 See Also](#See_Also)

## 安装

从 [官方源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") [安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") [rtorrent](https://www.archlinux.org/packages/?name=rtorrent) 包。

你也可以从 [AUR](/index.php/Arch_User_Repository "Arch User Repository") 中安装 [rtorrent-git](https://aur.archlinux.org/packages/rtorrent-git/) 或 [rtorrent-extended](https://aur.archlinux.org/packages/rtorrent-extended/)。

## 配置

**注意:** 查看关于此部分的 rTorrent Wiki 文章获取更多信息： [Common Tasks in rTorrent for Dummies](http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks)

在运行 rTorrent 前,首先要创建默认配置文件，该文件可以从 `/usr/share/doc/rtorrent/rtorrent.rc` 上找到，并将其另存为 `.rtorrent.rc` 放到你的主目录中.

```
$ cp /usr/share/doc/rtorrent/rtorrent.rc ~/.rtorrent.rc

```

保存后, 使用你喜爱的文本编辑器打开它并进行有必要的改动. 可以简单地去掉那些你需要使用的选项的注释， 如需更详细的资料,请访问[rTorrent Common Tasks](http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks)

### 性能优化

**注意:** 查看关于此部分的 rTorrent wiki 文章获得更多信息： [性能优化](http://libtorrent.rakshasa.no/wiki/RTorrentPerformanceTuning)

下面这些配置的值主要取决于你的系统和网络速度. 要寻找最佳配置，请访问下面网站并按照指示操作: [优化 BitTorrent 下载速度](http://torrentfreak.com/optimize-your-BitTorrent-download-speed)

```
# 每个种子所允许的最大最小连接数
#min_peers = 40
max_peers = 52

# 同上，针对的是已经完成的种子 （-1 表示和下载中的种子一致）
#min_peers_seed = 10
max_peers_seed = 52

# 每个种子的最大同时上传数
max_uploads = 8

# 全局的上传与下载速度限制（以 KB 为单位），“0”表示无限制
download_rate = 200
upload_rate = 28

```

`check_hash` 选项将在下载完成或 rTorrent 重新启动时对文件进行 Hash 校验。这将确保你获得/做种的文件没有错误：

```
check_hash = yes

```

### 创建和管理文件

`directory` 选项将决定你的 torrent 数据被保存在哪. 如果你想改变默认保存目录，请务必输入正确的绝对路径; rtorrent 有一个奇怪的 Bug，一些时候它不考虑相对路径(如 ~/torrents):

```
directory = /home/[user]/torrents/

```

`session` 选项将允许 rTorrent 保存你的 torrents 的进度. 一定要创建一个会话目录 `.session` (普通用户运行:`$ mkdir ~/.session`):

```
session = /home/[user]/.session/

```

`schedule` 选项将使 rTorrent 监视一个特定目录中的 .torrent 文件。使用这一选项时一定要小心，这将移动 .torrent 文件到你的会话目录下，并将之重命名为其 Hash 值。 当你看到了一个你想要下载的种子文件，你可以使用你的浏览器将这一种子文件保存到这一监视目录下， rTorrent 将会自动的开始下载这一种子文件的内容。必须确保要监视的目录已经被创建(以普通用户身份执行: mkdir ~/watch):

```
# 监听目录中的新的种子文件，并停止那些已经被删除部分的种子
#schedule = watch_directory,5,5,load_start=./watch/*.torrent
#schedule = untied_directory,5,5,stop_untied=
schedule = watch_directory,5,5,load_start=/home/[user]/watch/*.torrent
schedule = untied_directory,5,5,stop_untied=
schedule = tied_directory,5,5,start_tied=

```

下面的 `schedule` 选项将使 rTorrent 在磁盘空间不足时停止。 这对于[Seedbox](http://en.wikipedia.org/wiki/Seedbox)这种磁盘空间非常有限的设备来说是很有用的。按照你的喜好来改变下面的数值：

```
# 当磁盘空间不足时停止下载
schedule = low_diskspace,5,60,close_low_diskspace=100M

```

### 端口配置

`port_range` 选项将指定选用哪一个端口去侦听。建议使用高于 49152 的端口。虽然 rTorrent 允许使用多个的端口，还是建议使用单个的端口。

```
port_range = 49164-49164

```

Additionally, make sure port forwarding is enabled for the proper port(s) (see: [Port Forward Guides](http://portforward.com/english/routers/port_forwarding/routerindex.htm)).

### 附加设置

`encryption` 选项使能加密功能。 使用加密功能十分重要not only for yourself, but also for your peers in the torrent swarm. 人们也许需要对它们的网络提供商模糊其带宽使用。即使你不需要这些保护，开启加密也不会对你有所负作用。详细信息请见： [Bittorrent Protocol Encryption](http://en.wikipedia.org/wiki/BitTorrent_protocol_encryption)

```
# 加密选项，设为0（默认情况）或下面的任何一个：
# allow_incoming, try_outgoing, require, require_RC4, enable_retry, prefer_plaintext
#
# 如下例中的值将允许将接入连接加密，开始时以非加密方式作为连接的输出方式，
# 如行不通则以加密方式进行重试，在加密握手后，优先选择将纯文本以 RC4 加密
#
# encryption = allow_incoming,enable_retry,prefer_plaintext
encryption = allow_incoming,try_outgoing,enable_retry

```

下面的选项用以加入 DHT 支持。如果你使用了 public trackers，你可能希望使能 DHT 以获得更多的连接。如果你仅仅使用了私有的连接，**请不要使能 DHT**，因为这将降低你的速度，并可能造成一些隐密的危险。一些私有连接甚至会就使用 DHT 而向你发出警告。

```
# 使能对 trackerless torrents 或当所有的 tracker 都停止情况下的 DHT 支持。
# 可以被设置为 "disable" （完全禁止 DHT），“off“（不启动 DHT）， "auto"（按需要启
# 动或停止 DHT）或者 "on" (即时开启 DHT)。
# 默认设置为 "off"。要使 DHT 工作，会话目录必须被定义。
#
# dht = auto

# UDP 使用 UHT的端口 
# 
# dht_port = 6881

# 使能 peer 的交换 (对那些没有被标记为私有的 torrent)
#
# peer_exchange = yes

```

**Note:** See the rTorrent wiki article on this subject for more information: [Using DHT](http://libtorrent.rakshasa.no/wiki/RTorrentUsingDHT)

## 管理

| Cmd | Action |
| Ctrl-q | Quit application |
| Left | Returns to the previous screen |
| Right | Goes to the next screen |
| Backspace | Adds the specified *.torrent |

rTorrent依靠用户输入的专有的快捷键.可在官方网站上查看完整的: [rTorrent用户指南](http://libtorrent.rakshasa.no/wiki/RTorrentUserGuide)

**注意:** 快速敲击 `Ctrl-q` 两次会使得 rTorrent 关闭，而不会等待向连接的 tracker 发送停止声明。

这里是一些最基础的快速参考：

*   Control-q : closes rTorrent, done twice makes the program shutdown without waiting to send stopping information to the trackers.
*   Left arrow : returns to the previous screen.
*   Right arrow : goes to the next screen.
*   a|s|d : increase global upload throttle about 1|5|50 KB/s
*   A|S|D : increase global download throttle about 1|5|50 KB/s
*   z|x|c : decrease global upload throttle about 1|5|50 KB/s
*   Z|X|C : decrease global download throttle about 1|5|50 KB/s
*   Control-S : starts download
*   Control-D : stops an active download, removes a stopped download.
*   + or - : changes the download priority of selected torrent.
*   Backspace : adds the specified .torrent. After pressing this button write full path or URL of .torrent file. You can use Tab and other tricks from bash.

### Redundant mapping

`Ctrl-s` is often used for terminal control to stop screen output while `Ctrl-q` is used to start it. These mappings may interfere with rTorrent. Check to see if these terminal options are bound to a mapping:

 `$ stty -a` 
```
...
swtch = <undef>; start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V;
...

```

To remove the mappings, change the terminal characteristics to undefine the aforementioned special characters (i.e. `stop` and `start`):

```
# stty stop undef
# stty start undef

```

To remove these mappings automatically at startup you may add the two preceding commands to your `~/.bashrc` file.

## 通过Screen使用rTorrent

Screen 是允许CLI应用程序在后台运行并支持X运行的一个程序.

安装:

```
pacman -S screen

```

然后复制screenrc到你的用户主目录:

```
cp /etc/screenrc ~/.screenrc

```

要总是通过Screen来运行rTorrent,在.screenrc文件中添加以下内容:

```
screen -t rtorrent rtorrent 

```

要运行screen和rTorrent, 只要简单的在终端运行*screen*就可以了. Control-a followed by d will detach screen, and running *screen -r* will open screen again.

### On a remote machine

Most setups of rTorrent on a remote machine involve using Screen. Supposing you have a detached Screen session with rtorrent on the remote machine (and the option to [SSH](/index.php/SSH "SSH") into it), you can gain access to it using:

 `/usr/bin/ssh -t -p <ssh port on remote machine> <user>@<remote machine> screen -RD` 

If you want immediate access on startup, you will need to [upload a key](http://bloggerdigest.blogspot.com/2006/11/ssh-auto-login-or-passwordless-login.html) from your machine to remote host (so you will not be prompted for a password) and setup a terminal to run the command above. An inittab example using [rungetty](https://aur.archlinux.org/packages/rungetty/) on virtual console 4:

 `sam:45:respawn:/sbin/rungetty tty4 -u <local user> -- /usr/bin/ssh -t -p <ssh port on remote machine> <remote user>@<remote machine> screen -RD` 

### Screen后台运行rTorrent

I use this on my home server to run rtorrent w/ screen as a daemon. With the username *rtorrent* Just create an *rtorrent* file in your */etc/rc.d/* and add the following code.

```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

case "$1" in
  start)
    stat_busy "Starting rtorrent"
    su rtorrent -c 'screen -d -m rtorrent' &> /dev/null
    if [ $? -gt 0 ]; then
      stat_fail
    else
      add_daemon rtorrent
      stat_done
    fi
    ;;
  stop)
    stat_busy "Stopping rtorrent"
    killall -w -s 2 /usr/bin/rtorrent &> /dev/null
    if [ $? -gt 0 ]; then
      stat_fail
    else
      rm_daemon rtorrent
      stat_done
    fi
    ;;
  restart)
    $0 stop
    sleep 1
    $0 start
    ;;
  *)
    echo "usage: $0 {start|stop|restart}"
esac
exit 0

```

On a remote computer I use the following script to connect to the server's daemon process:

```
ssh -t rtorrent@192.168.1.10 'screen -r'

```

## 其他提示

*   To use rTorrent with a tracker that uses https, do the following as root:

```
cd /etc/ssl/certs
wget --no-check-certificate https://www.geotrust.com/resources/root_certificates/certificates/Equifax_Secure_Global_eBusiness_CA-1.cer
mv Equifax_Secure_Global_eBusiness_CA-1.cer Equifax_Secure_Global_eBusiness_CA-1.pem
c_rehash

```

And from now on run rTorrent with:

```
rtorrent -o http_capath=/etc/ssl/certs

```

Be sure to change .screenrc to reflect this change if you use screen:

```
screen -t rtorrent rtorrent -o http_capath=/etc/ssl/certs

```

*   To create .torrent files, I recommend [mktorrent](https://aur.archlinux.org/packages.php?do_Details=1&ID=10635&O=0&L=0&C=0&K=mktorrent&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd) for commandline interface or [RubyTorrent](http://benclarke.ca/rubytorrent/) for GUI.

### Send Text Message Upon Torrent Completion Using GMail

Cell phone providers allow you to "email" your phone:

```
Verizon: 10digitphonenumber@vtext.com
Former AT&T customers: 10digitphonenumber@mmode.com
Sprint: 10digitphonenumber@messaging.sprintpcs.com
T-Mobile: 10digitphonenumber@tmomail.net
Nextel: 10digitphonenumber@messaging.nextel.com
Cingular: 10digitphonenumber@cingularme.com
Virgin Mobile: 10digitphonenumber@vmobl.com
Alltel: 10digitphonenumber@alltelmessage.com OR
10digitphonenumber@message.alltel.com
CellularOne: 10digitphonenumber@mobile.celloneusa.com
Omnipoint: 10digitphonenumber@omnipointpcs.com
Qwest: 10digitphonenumber@qwestmp.com

```

If you have Verizon, your cell phone's "email" is 5551234567@vtext.com

*   Install **Heirloom's mailx** program:

```
pacman -S mailx-heirloom

```

*   Clear the /etc/nail.rc file and enter:

```
set smtp=smtp.gmail.com:587
set smtp-use-starttls
set ssl-verify=ignore
set ssl-auth=login
set smtp-auth-user=USERNAME@gmail.com
set smtp-auth-password=PASSWORD

```

Now to send the text, we must pipe a message to the mailx program.

*   Make a bash script (/path/to/mail.sh):

```
echo "Torrent Done" | mailx 5551234567@vtext.com

```

*   And finally, add the important ~/.rtorrent.rc line:

```
on_finished = move_complete,"execute=/path/to/mail.sh"

```

**Note:** The "move complete" won't affect anything. I couldn't get it to work without it.

## See Also

[Screen Tips](/index.php/Screen_Tips "Screen Tips")

A Detailed Intro to Bittorrent including definition of terms [terms](http://www.dessent.net/btfaq/#terms)