相关文章

*   [SSH keys](/index.php/SSH_keys "SSH keys")
*   [Pam abl](/index.php/Pam_abl "Pam abl")
*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [sshguard](/index.php/Sshguard "Sshguard")
*   [Sshfs](/index.php/Sshfs "Sshfs")
*   [Syslog-ng](/index.php/Syslog-ng "Syslog-ng")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")

**Secure Shell** (**SSH**) 是一个允许两台电脑之间通过安全的连接进行数据交换的网络协议。加密保证了数据的保密性和完整性。SSH采用公钥加密技术来验证远程主机，以及(必要时)允许远程主机验证用户。

SSH 通常用于远程访问和执行命令，但是它也支持隧道，转发任意 TCP 端口以及 X11 连接；它还能够用 SFTP 或 SCP 协议来传输文件。

一个 SSH 服务器默认情况下，在 TCP 端口 22 进行监听。一个 SSH 客户端程序通常被用来建立一个远程连接到 **sshd** 守护进程。这两者都被广泛地存在于现代操作系统中，包括 Mac OS X，GNU/Linux，Solaris 和 OpenVMS 等。以专利的，自由软件的以及开源版本的形式和不同的复杂性和完整性存在。

(来源：[维基百科 Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell"))

## Contents

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 安装OpenSSH](#.E5.AE.89.E8.A3.85OpenSSH)
    *   [1.2 SSH客户端](#SSH.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [1.2.1 配置 SSH](#.E9.85.8D.E7.BD.AE_SSH)
    *   [1.3 SSH服务端](#SSH.E6.9C.8D.E5.8A.A1.E7.AB.AF)
        *   [1.3.1 配置 SSH守护进程](#.E9.85.8D.E7.BD.AE_SSH.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
        *   [1.3.2 管理 sshd 守护进程](#.E7.AE.A1.E7.90.86_sshd_.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
*   [2 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [2.1 加密Socks通道](#.E5.8A.A0.E5.AF.86Socks.E9.80.9A.E9.81.93)
        *   [2.1.1 第一步：开始连接](#.E7.AC.AC.E4.B8.80.E6.AD.A5.EF.BC.9A.E5.BC.80.E5.A7.8B.E8.BF.9E.E6.8E.A5)
        *   [2.1.2 第二步：配置你的浏览器(或其它程序)](#.E7.AC.AC.E4.BA.8C.E6.AD.A5.EF.BC.9A.E9.85.8D.E7.BD.AE.E4.BD.A0.E7.9A.84.E6.B5.8F.E8.A7.88.E5.99.A8.28.E6.88.96.E5.85.B6.E5.AE.83.E7.A8.8B.E5.BA.8F.29)
    *   [2.2 X11 转发](#X11_.E8.BD.AC.E5.8F.91)
    *   [2.3 转发其他端口](#.E8.BD.AC.E5.8F.91.E5.85.B6.E4.BB.96.E7.AB.AF.E5.8F.A3)
    *   [2.4 加速SSH](#.E5.8A.A0.E9.80.9FSSH)
        *   [2.4.1 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [2.5 用SSHFS挂载远程文件系统](#.E7.94.A8SSHFS.E6.8C.82.E8.BD.BD.E8.BF.9C.E7.A8.8B.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [2.6 保持在线](#.E4.BF.9D.E6.8C.81.E5.9C.A8.E7.BA.BF)
    *   [2.7 在配置文件中保存连接信息](#.E5.9C.A8.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E4.B8.AD.E4.BF.9D.E5.AD.98.E8.BF.9E.E6.8E.A5.E4.BF.A1.E6.81.AF)
    *   [2.8 更改ssh主机prompt](#.E6.9B.B4.E6.94.B9ssh.E4.B8.BB.E6.9C.BAprompt)
    *   [2.9 当sshd服务器宕机时自动登出所有客户端](#.E5.BD.93sshd.E6.9C.8D.E5.8A.A1.E5.99.A8.E5.AE.95.E6.9C.BA.E6.97.B6.E8.87.AA.E5.8A.A8.E7.99.BB.E5.87.BA.E6.89.80.E6.9C.89.E5.AE.A2.E6.88.B7.E7.AB.AF)
*   [3 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3_2)
    *   [3.1 拒绝连接或者超时问题](#.E6.8B.92.E7.BB.9D.E8.BF.9E.E6.8E.A5.E6.88.96.E8.80.85.E8.B6.85.E6.97.B6.E9.97.AE.E9.A2.98)
        *   [3.1.1 SSH服务是否开启并且正在监听吗？](#SSH.E6.9C.8D.E5.8A.A1.E6.98.AF.E5.90.A6.E5.BC.80.E5.90.AF.E5.B9.B6.E4.B8.94.E6.AD.A3.E5.9C.A8.E7.9B.91.E5.90.AC.E5.90.97.EF.BC.9F)
        *   [3.1.2 是否是防火墙阻止了连接？](#.E6.98.AF.E5.90.A6.E6.98.AF.E9.98.B2.E7.81.AB.E5.A2.99.E9.98.BB.E6.AD.A2.E4.BA.86.E8.BF.9E.E6.8E.A5.EF.BC.9F)
        *   [3.1.3 你的电脑和目的主机之间是否连接？](#.E4.BD.A0.E7.9A.84.E7.94.B5.E8.84.91.E5.92.8C.E7.9B.AE.E7.9A.84.E4.B8.BB.E6.9C.BA.E4.B9.8B.E9.97.B4.E6.98.AF.E5.90.A6.E8.BF.9E.E6.8E.A5.EF.BC.9F)
        *   [3.1.4 Read from socket failed: Connection reset by peer](#Read_from_socket_failed:_Connection_reset_by_peer)
    *   [3.2 "[your shell]: No such file or directory" / ssh认证问题](#.22.5Byour_shell.5D:_No_such_file_or_directory.22_.2F_ssh.E8.AE.A4.E8.AF.81.E9.97.AE.E9.A2.98)
*   [4 See Also](#See_Also)

## OpenSSH

OpenSSH (OpenBSD Secure Shell) 是一套使用ssh协议，通过计算机网络，提供加密通讯会话的计算机程序。它被创建为 SSH Communications Security 公司拥有专利的 Secure Shell 软件套装的一个开源替代。OpenSSH是由Theo de Raadt领导的OpenBSD项目的一部分。

人们常把 OpenSSH 与相似名字的 OpenSSL 搞混，但是，这两个项目是由不同的团队出于不同的目的开发出来的。相似的名字只是由于相似的目标。

### 安装OpenSSH

从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")中[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [openssh](https://www.archlinux.org/packages/?name=openssh).

### SSH客户端

连接SSH服务器，运行命令

```
 $ssh -p port user@server-address

```

如果服务器仅允许使用密钥登录，请参考 [SSH Keys](/index.php/SSH_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH keys (简体中文)") 。

#### 配置 SSH

SSH客户端的配置文件是`/etc/ssh/```ssh```_config` 或 `~/.ssh/config`.

现在已经不需要额外设置 `Protocol 2`, 默认的协议已经是 `Protocol 2` 了 ([http://www.openssh.org/txt/release-5.4](http://www.openssh.org/txt/release-5.4)) 。

 `~/.ssh/config` 
```
# global options
User *user*

# host-specific options
Host myserver
    HostName *server-address*
    Port     *port*
```

进行了如上的配置后，以下命令是等效的

```
$ ssh -p *port* *user*@*server-address*
$ ssh myserver

```

查看 [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5) 获取更多信息。

某些选项没有命令行参数，但是可以使用 `-o` 在命令行中配置指定选项的参数。 例如 `-o```KexAlgorithms```=+```diffie-hellman-group1-sha1````.

### SSH服务端

#### 配置 SSH守护进程

**提示：**

*   更多安全配置请参考 [SSH Keys](/index.php/SSH_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH keys (简体中文)")

SSH 守护进程的配置文件是`/etc/ssh/```sshd```_config`。

只允许某些用户访问的话，加入这一行：

```
AllowUsers    user1 user2

```

只允许一些组访问：

```
AllowGroups   group1 group2

```

要禁止通过SSH进行root用户登录，加入以下行：

```
PermitRootLogin no

```

运行以下命令以更改sshd服务监听端口：

```
 Port 39901

```

**提示：**

*   可以考虑把默认的端口从22改成更高的端口(参考 [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity")).尽管ssh的运行端口可以被像nmap这样的端口扫描器侦测到，但改变它可以减少由于自动验证的尝试造成的登录日志条目。有关端口号列表请参考`/etc//services`或[list of TCP and UDP port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers")
*   完全取消密码登录方式可以极大的增强安全性，(参考 [SSH Keys](/index.php/SSH_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH keys (简体中文)")).

你也可以取消BANNER选项的注释，然后编辑`/etc/issue`加入友好的欢迎信息内容。

你也可以运行以下命令关联文件(如`/etc/issue`文件)到登录欢迎信息：

```
 Banner /etc/issue

```

ssh主机秘钥将由sshd服务文件自动配置。如果你想要自定义秘钥，运行以下命令以自定义秘钥：

```
 HostKey /etc/ssh/ssh_host_rsa_key

```

#### 管理 sshd 守护进程

你可以使用下面的命令启动sshd：

```
# systemctl start sshd

```

你可以使用下面的命令开机启动sshd:

```
# systemctl enable sshd.service

```

**警告:** Systemd 是一个异步启动的进程。如果你绑定 SSH 守护进程到某个特定的 IP 地址 `ListenAddress 192.168.1.100`，它可能会在引导时启动失败，因为默认的 sshd.service 单元文件没有对网络接口启动的依赖。当绑定到一个 IP 地址时，你需要添加 `After=network.target` 到自定义的 sshd.service 单元文件中。参见 [Systemd#Replacing provided unit files](/index.php/Systemd#Replacing_provided_unit_files "Systemd").

或者你可以启用SSH Daemon socket，这样当第一次传入连接时启动守护进程:

```
# systemctl enable sshd.socket

```

如果你使用非默认端口22，你必须在文件(/lib/systemd/system/sshd.socket)中设置"ListenStream"为相应的端口。

[openssh](https://www.archlinux.org/packages/?name=openssh) comes with two kinds of [systemd](/index.php/Systemd "Systemd") service files:

1.  `sshd.service`, which will keep the SSH daemon permanently active and fork for each incoming connection.[[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh#n16) It is especially suitable for systems with a large amount of SSH traffic.[[2]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh&id=4cadf5dff444e4b7265f8918652f4e6dff733812#n15)
2.  `sshd.socket` + `sshd@.service`, which spawn on-demand instances of the SSH daemon per connection. Using it implies that *systemd* listens on the SSH socket and will only start the daemon process for an incoming connection. It is the recommended way to run `sshd` in almost all cases.[[3]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh&id=4cadf5dff444e4b7265f8918652f4e6dff733812#n18)[[4]](http://lists.freedesktop.org/archives/systemd-devel/2011-January/001107.html)[[5]](http://0pointer.de/blog/projects/inetd.html)

You can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") either `sshd.service` **or** `sshd.socket` to begin using the daemon.

If using the socket service, you will need to [edit](/index.php/Edit "Edit") the unit file if you want it to listen on a port other than the default 22:

 `# systemctl edit sshd.socket` 
```
[Socket]
ListenStream=
ListenStream=12345

```

**Warning:** Using `sshd.socket` negates the `ListenAddress` setting, so it will allow connections over any address. To achieve the effect of setting `ListenAddress`, you must specify the port *and* IP for `ListenStream` (e.g. `ListenStream=192.168.1.100:22`). You must also add `FreeBind=true` under `[Socket]` or else setting the IP address will have the same drawback as setting `ListenAddress`: the socket will fail to start if the network is not up in time.

**Tip:** When using socket activation neither `sshd.socket` nor the daemon's regular `sshd.service` allow to monitor connection attempts in the log, but executing `# journalctl /usr/bin/sshd` does.

## 提示与技巧

### 加密Socks通道

对于连接到各种不安全的无线网络上的笔记本电脑用户来说,这个是特别有用的！唯一所需要的就是一个一定程度上处于安全的地点的SSH服务器，比如在家里或办公室。用动态的DNS服务[DynDNS](http://www.dyndns.org/)也可能是很有用的，这样你就不必记住你的IP了。

#### 第一步：开始连接

你只要在你喜欢的终端中执行这一个命令就能开始你的连接：

```
$ ssh -ND 4711 user@host

```

这里的“user”是你在“host”这台SSH服务器上运行的用户名。它会让你输入密码，然后你就能连上了。“N”表示不采用交互提示，而“D”表示指定监听的本地端口（你可以使用任何你喜欢的数字）

一个办法可以让这个过程更简单，那就是在~/.bashrc中加入这样一行：

```
alias sshtunnel="ssh -ND 4711 -v user@host"

```

加入冗长的“-v”标志更好，因为这样你可以验证是真的是从那个端口连接的。现在你只要执行命令“sshtunnel”就可以。 ：）

#### 第二步：配置你的浏览器(或其它程序)

如果你不配置你的web浏览器以便使用新创建的socks通道的话，上面的一步完全没用！

*   对于Firefox: *Edit -> Preferences -> Advanced -> Network -> Connection -> Setting*:

	检查"Manual proxy configuration" radio button？, 并且在"SOCKS host" 文本段输入"localhost" , 然后在接下来的一个文本框中输入你的端口数（上面我们用的是4711）。

	确定你选择使用SOCKS4。这个程序对不会对SOCKS5起作用.

	享受你的安全通道吧！

### X11 转发

为了通过SSH运行图形程序你必须使用X11 Forwarding。一个选项就是需要设置服务器和客户端的配置文件(这里所说的“客户端”指运行你的X11服务器的电脑，而你的X应用程序运行在“服务器”上）。

在服务器上安装xorg-xauth：

```
# pacman -S xorg-xauth

```

*   在**服务器**上，编辑`ssh**d**_config`启用**AllowTcpForwarding**选项。
*   在**服务器**上，编辑`ssh**d**_config`启用**X11Forwarding**选项。
*   在**服务器**上，编辑`ssh**d**_config`将**X11DisplayOffset**选项设为10。
*   在**服务器**上，编辑`ssh**d**_config`启用**X11UseLocalhost**选项。

同时：

*   在**客户端**上，编辑`ssh_config`启用**ForwardX11**选项。

当GUI大量绘制时，请启用**ForwardX11Trusted**。

为了使用X11 forwarding，首先通过SSH登陆到你的服务器：

```
$ ssh -X -p port user@server-address

```

如果你在运行图形应用程序时收到了一些错误，请尝试可信的X11 forwarding：

```
$ ssh -Y -p port user@server-address

```

你现在可以在远程服务器上启用任何的X程序，输出将会被转发到你的本地会话中：

```
$ xclock

```

如果你遇到了“Cannot open display”错误，请尝试使用非root账户执行下述命令：

```
$ xhost +

```

上述命令将会允许任何用户转发X11应用程序。为了限制只能转发到特定主机：

```
$ xhost +hostname

```

上述命令中的hostname是你想要转发到的主机名。使用“man xhost”获取更多信息。

值得注意的是，一些应用程序会检查本地正在运行的实例。Firefox就是一个例子。你可以关闭正在执行的Firefox，或者使用下述启动参数来在本地启动一个远程实例：

```
$ firefox -no-remote

```

### 转发其他端口

除了SSH内建的对X11的支持之外，它也能通过本地转发和远程转发，来为任何的TCP连接建立隧道。

本地转发时，会在本机打开一个端口，连接将被转发到一个远程主机，并给定一个目的地。很多时候，转发目的地和远程主机会相同，因此也提供了一条SSH命令来建立一个安全的VNC连接。本地转发可以通过`-L`来设置，后面可以指定一个地址及端口`<tunnel port>:<destination address>:<destination port>`。 如下：

```
$ ssh -L 1000:mail.google.com:25 192.168.0.100

```

以上指令将会通过SSH得到一个在192.168.0.100的shell，同时也会创建一个从本机1000端口到mai.google.com上的25端口的隧道。建立之后，localhost:1000会通过192.168.0.100连接到Gmail的SMTP端口。任何从192.168.0.100到mail.google.com:25的连接（即使不必要）都会以这样的方式建立，并且，在本机和192.168.0.100之间的数据传递都是安全的，除非你采取了别的手段。 同样：

```
$ ssh -L 2000:192.168.0.100:6001 192.168.0.100
$ ssh -L 2000:localhost:6001 192.168.0.100

```

以上指令会将到localhost:2000的连接直接转发到远程主机192.168.0.100的6001端口。对于使用VNC服务器（tightvns包的一部分）建立的VNC连接来说，以上的例子尽管很有效，但是安全性有待商榷。

远程转发允许任何远程主机通过SSH隧道连接到本机，提供了和本地转发相反的功能，突破了防火墙的限制。通过`-R`参数，以及`<tunnel port>:<destination address>:<destination>`能够实现远程转发。

如下:

```
$ ssh -R 3000:irc.freenode.net:6667 192.168.0.200

```

将会在192.168.0.200上得到一个shell，同时也会创建一个从192.168.0.200上的3000端口到irc.freenode.net上的6667端口的隧道。建立之后，192.168.0.200:3000会通过本机连接到freenode的IRC端口。到192.168.0.200的3000端口的连接将会通过隧道发送到本机然后转发到irc.freenode.net的6667端口。因此，在这个例子中，在远程主机上IRC程序能够被使用，即使端口6667被阻止。

本地转发`-L`和远程转发`-R`都可以提供一个安全的"网关"，允许其他计算机无需使用SSH或者SSH daemon来使用ssh隧道。例如 `<tunnel address>:<tunnel port>:<destination address>:<destination port>`. `<tunnel address>`可以是作为网关的机器上的任何地址，例如 `localhost`(仅允许本地访问)，`192.168.0.100`(仅允许通过192.168.0.100访问)， `*`(允许所有地址访问)。 `<tunnel address>`若留空则默认设置为`localhost`，本地转发`-L`不需要额外的设置，而远程转发`-R`需要配置SSH daemon设置，请参阅`sshd_config(5)`中的`GatewayPorts`。

### 加速SSH

为了加速连续的到同一台主机的连接，你可以在远程主机的`/etc/ssh/ssh_config`中增加以下内容：

```
ControlMaster auto
ControlPath ~/.ssh/socket-%r@%h:%p

```

改变SSH的计算来减少cpu使用能够提高速度。关于这一点，最好的选择是arcfour和blowfish-cbc。

```
**除非你清楚你在做什么，否则不要做; arcfour有大量众所周知的缺点**。 通过增加参数`"c"`:
$ ssh -c arcfour,blowfish-cbc user@server-address

```

为了持续地使用这个，可以在`/etc/ssh/ssh_config`中增加以下内容：

```
Ciphers arcfour,blowfish-cbc

```

其他能够加速的选项是`"C"`参数，同样，以下将是长久的解决方案：

```
Compression yes

```

登陆时间可以通过`"4"`来减少，它是通过IPv6旁路进行寻路。同上：

```
AddressFamily inet

```

或者在`~/.bashrc`中增加以下内容也能够达到长久的效果（前提是你使用bash）：

```
alias ssh='ssh -C4c arcfour,blowfish-cbc'

```

#### 问题解决

确定你的“DISPLAY”变量在远程主机上能被解析：

```
$ ssh -X user@server-address
server $ echo $DISPLAY
localhost:10.0
server $ telnet localhost 6010
localhost/6010: lookup failure: Temporary failure in name resolution   

```

这个问题能通过添加localhost到 `/etc/hosts`来解决。

### 用SSHFS挂载远程文件系统

安装sshfs

```
# pacman -S sshfs

```

将你想要允许挂载SSH文件夹的用户添加到fuse组里

```
# gpasswd -a USER fuse

```

加载fuse模块(比如说在/etc/rc.conf中)

And then然后，在登录后，你就可以试着挂用sshfs载远程文件夹了:

```
# mkdir ~/remote_folder
# sshfs USER@remote_server:/tmp ~/remote_folder

```

上面的命令将把远程服务器上的/tmp文件夹挂载到本地的~/remote_folder目录下。复制任何文件到这个目录将使文件通过SCP通过网络传输。 Same concerns direct file editing, creating or removing.

当我们完成在远程文件夹下的工作，我们可以这样来卸载它：

```
# fusermount -u ~/remote_folder

```

如果我们需要经常在这个文件夹下，让它通过/etc/fstab挂载是一个明智的选择。这个办法可以让它在启动的时候挂载或者通过手动挂载（如果是noauto选项的话），而不需要每次都去挂载它。下面是一个简单的样本：

```
sshfs#USER@remote_server:/tmp /full/path/to/directory fuse    defaults,auto    0 0

```

### 保持在线

如果你的会话空闲，它会自动登出。为了保持会话， 可以把以下内容增加到客户端的`~/.ssh/config`或者`/etc/ssh/ssh_config`。

```
ServerAliveInterval 120

```

这将会使得客户端每120秒发送一个“alive”的信号到服务器。

反过来，为了保持到达本地的会话，你可以设置：

```
ClientAliveInterval 120

```

(或者其他任何大于0的数字)在服务器的`/etc/ssh/sshd_config`。

### 在配置文件中保存连接信息

通常当你想登录到一台远程主机的时候，你至少需要输入主机名和IP地址。为了减少这个重复劳动，你可以使用本地的`$HOME/.ssh/config` 或者全局的`/etc/ssh/ssh_config`：

 `$HOME/.ssh/config` 
```
Host myserver
    HostName 123.123.123.123
    Port 12345
    User bob
Host other_server
    HostName test.something.org
    User alice
    CheckHostIP no
    Cipher blowfish

```

现在你能用指定的名称来简单地连接到远程主机：

```
$ ssh myserver

```

如果需要查看完整选项，可以查看你的系统上的ssh_config文档， 或者它的官方网站[ssh_config documentation](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh_config)。

### 更改ssh主机prompt

区别你的电脑和远程主机是很有必要的，特别是它们的prompt相同时。只要把一下内容插入到你的bashrc文件即可达到这个效果。

 `$HOME/.bashrc` 
```
if [ -n "$SSH_CLIENT" ]; then
        PS1='\[\e[0;33m\]\u@\h:\wSSH$\[\e[m\] '
else
        PS1='\[\e[0;32m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[1;32m\]\$\[\    e[m\] '
fi
```

可以访问[Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt")了解更多关于PS1变量定制的更多信息。

### 当sshd服务器宕机时自动登出所有客户端

为了在sshd服务器宕机（比如重启或关机）时自动登出所有客户端，需要在sshd服务器的/etc/rc.local.shutdown 增加以下内容：

```
who | cut -d " " -f1 | uniq | xargs pkill -KILL -u

```

这防止了ssh客户端在超时之后挂起，最终得到这样的结果：

```
Write failed: Broken pipe

```

## 问题解决

### 拒绝连接或者超时问题

#### SSH服务是否开启并且正在监听吗？

```
$ ssh -tnlp

```

如果以上的命令没有显示SSH端口是打开的，那么说明SSH服务没有启动。查看`/var/log/messages`来寻找错误信息。

#### 是否是防火墙阻止了连接？

更新你的防火墙规则来排除干扰：

```
# rc.d stop iptables

```

或者：

```
# iptables -P INPUT ACCEPT
# iptables -P OUTPUT ACCEPT
# iptables -F INPUT
# iptables -F OUTPUT

```

#### 你的电脑和目的主机之间是否连接？

测试你的电脑和目的主机的连接情况：

```
# tcpdump -lnn -i any port ssh and tcp-syn

```

它会显示一些基本信息，然后等待数据交换。现在尝试你的连接。如果没有输出，就可能是你的电脑网络阻塞了。（也许是防火墙问题，也许是NAT路由的问题，祝你好运！）

#### Read from socket failed: Connection reset by peer

最近版本的openssh有时候会因为以上信息崩溃，据说是elliptic curve 加密的bug。在这种情况下，请编辑这个文件：

```
~/.ssh/config

```

如果不存在，就创建它，然后加入以下内容：

```
HostKeyAlgorithms ssh-rsa-cert-v01@openssh.com,ssh-dss-cert-v01@openssh.com,ssh-rsa-cert-v00@openssh.com,ssh-dss-cert-v00@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss

```

在openssh5.9中，以上的修复工作不会奏效。不过，还可以这样做：

```
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc 
MACs hmac-md5,hmac-sha1,hmac-ripemd160

```

可以访问[discussion](http://www.gossamer-threads.com/lists/openssh/dev/51339)来查看openssh的bug问题.

### "[your shell]: No such file or directory" / ssh认证问题

对于这个问题，一个可能的原因是需要SSH客户端在`$SHELL`中提供绝对路径（例如可以通过`whereis -b [your shell]`得到)，即使你的shell在`$PATH`中。另一个原因也可能是，用户不是*network*组的成员。

## See Also

*   [SSH keys](/index.php/SSH_keys "SSH keys")
*   [pam_abl](/index.php/Pam_abl "Pam abl")
*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [sshguard](/index.php/Sshguard "Sshguard")
*   [SSHFS](/index.php/SSHFS "SSHFS")
*   [A Cure for the Common SSH Login Attack](http://www.soloport.com/iptables.html)
*   [使用SSH密钥](/index.php/%E4%BD%BF%E7%94%A8SSH%E5%AF%86%E9%92%A5 "使用SSH密钥")
*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)
*   [OpenSSH key management, Part 1](http://www.ibm.com/developerworks/library/l-keyc/index.html) and [Part 2](http://www.ibm.com/developerworks/library/l-keyc2) on IBM developerWorks