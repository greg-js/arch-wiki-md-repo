相关文章

*   [SSH keys (简体中文)](/index.php/SSH_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH keys (简体中文)")
*   [Pam abl](/index.php/Pam_abl "Pam abl")
*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [sshguard](/index.php/Sshguard "Sshguard")
*   [SSHFS (简体中文)](/index.php/SSHFS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSHFS (简体中文)")
*   [Syslog-ng](/index.php/Syslog-ng "Syslog-ng")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")
*   [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP")

**翻译状态：** 本文是英文页面 [Secure Shell](/index.php/Secure_Shell "Secure Shell") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-05-04，点击[这里](https://wiki.archlinux.org/index.php?title=Secure+Shell&diff=0&oldid=518925)可以查看翻译后英文页面的改动。

**Secure Shell** (**SSH**) 是一个允许两台电脑之间通过安全的连接进行数据交换的网络协议。加密保证了数据的保密性和完整性。SSH采用公钥加密技术来验证远程主机，以及(必要时)允许远程主机验证用户。

SSH 通常用于远程访问和执行命令，但是它也支持隧道，转发任意 TCP 端口以及 X11 连接；它还能够用 SFTP 或 SCP 协议来传输文件。

一个 SSH 服务器默认情况下，在 TCP 端口 22 进行监听。一个 SSH 客户端程序通常被用来建立一个远程连接到 **sshd** 守护进程。这两者都被广泛地存在于现代操作系统中，包括 Mac OS X，GNU/Linux，Solaris 和 OpenVMS 等。以专有软件、自由软件以及开源版本的形式和不同的复杂性和完整性存在。

(来源：[维基百科 Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell"))

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 安装OpenSSH](#安装OpenSSH)
    *   [1.2 SSH 客户端](#SSH_客户端)
        *   [1.2.1 配置](#配置)
    *   [1.3 SSH 服务端](#SSH_服务端)
        *   [1.3.1 配置](#配置_2)
        *   [1.3.2 管理 sshd 守护进程](#管理_sshd_守护进程)
        *   [1.3.3 安全防护](#安全防护)
            *   [1.3.3.1 强制公钥验证](#强制公钥验证)
            *   [1.3.3.2 双因素验证与公钥](#双因素验证与公钥)
            *   [1.3.3.3 防止暴力破解](#防止暴力破解)
                *   [1.3.3.3.1 使用 ufw](#使用_ufw)
                *   [1.3.3.3.2 使用 iptables](#使用_iptables)
                *   [1.3.3.3.3 防止暴力破解的工具](#防止暴力破解的工具)
            *   [1.3.3.4 禁用或限制 root 账户登录](#禁用或限制_root_账户登录)
                *   [1.3.3.4.1 禁用 root 登录](#禁用_root_登录)
                *   [1.3.3.4.2 限制 root 登录](#限制_root_登录)
            *   [1.3.3.5 保护 authorized_keys 文件](#保护_authorized_keys_文件)
*   [2 其他 SSH 客户端与服务端](#其他_SSH_客户端与服务端)
    *   [2.1 Dropbear](#Dropbear)
    *   [2.2 Mosh](#Mosh)
*   [3 提示与技巧](#提示与技巧)
    *   [3.1 加密 Socks 通道](#加密_Socks_通道)
        *   [3.1.1 第一步：开始连接](#第一步：开始连接)
        *   [3.1.2 第二步：配置你的浏览器(或其它程序)](#第二步：配置你的浏览器(或其它程序))
    *   [3.2 X11 转发](#X11_转发)
        *   [3.2.1 配置](#配置_3)
        *   [3.2.2 使用方法](#使用方法)
    *   [3.3 转发其他端口](#转发其他端口)
    *   [3.4 跳板机](#跳板机)
    *   [3.5 通过中继反向 SSH 连接](#通过中继反向_SSH_连接)
    *   [3.6 端口复用](#端口复用)
    *   [3.7 加速 SSH](#加速_SSH)
    *   [3.8 用 SSHFS 挂载远程文件系统](#用_SSHFS_挂载远程文件系统)
    *   [3.9 保持在线](#保持在线)
    *   [3.10 利用 systemd 自动重启 SSH 隧道](#利用_systemd_自动重启_SSH_隧道)
    *   [3.11 Autossh - 自动重启 SSH 会话和隧道连接](#Autossh_-_自动重启_SSH_会话和隧道连接)
        *   [3.11.1 利用 systemd 在引导后自动运行 autossh](#利用_systemd_在引导后自动运行_autossh)
    *   [3.12 当 SSH 守护进程出错时的其他选择](#当_SSH_守护进程出错时的其他选择)
*   [4 疑难解答](#疑难解答)
    *   [4.1 自检清单](#自检清单)
    *   [4.2 拒绝连接或者超时问题](#拒绝连接或者超时问题)
        *   [4.2.1 端口转发](#端口转发)
        *   [4.2.2 SSH服务是否开启并且正在监听？](#SSH服务是否开启并且正在监听？)
        *   [4.2.3 是否是防火墙阻止了连接？](#是否是防火墙阻止了连接？)
        *   [4.2.4 你的电脑和目的主机之间是否连接？](#你的电脑和目的主机之间是否连接？)
        *   [4.2.5 你的 ISP 或第三方屏蔽了默认端口？](#你的_ISP_或第三方屏蔽了默认端口？)
            *   [4.2.5.1 诊断](#诊断)
            *   [4.2.5.2 可能的解决方案](#可能的解决方案)
        *   [4.2.6 "Read from socket failed: connection reset by peer" 错误](#"Read_from_socket_failed:_connection_reset_by_peer"_错误)
    *   [4.3 "[your shell]: No such file or directory" / SSH 认证问题](#"[your_shell]:_No_such_file_or_directory"_/_SSH_认证问题)
    *   [4.4 "Terminal unknown" 或 "Error opening terminal" 错误](#"Terminal_unknown"_或_"Error_opening_terminal"_错误)
        *   [4.4.1 TERM hack](#TERM_hack)
    *   [4.5 "Connection closed by x.x.x.x [preauth]" 错误](#"Connection_closed_by_x.x.x.x_[preauth]"_错误)
    *   [4.6 id_dsa 被 OpenSSH 7.0 拒绝](#id_dsa_被_OpenSSH_7.0_拒绝)
    *   [4.7 OpenSSH 7.0 的 "No matching key exchange method found" 错误](#OpenSSH_7.0_的_"No_matching_key_exchange_method_found"_错误)
    *   [4.8 断开 SSH 连接时 tmux/screen 会话被关闭](#断开_SSH_连接时_tmux/screen_会话被关闭)
    *   [4.9 SSH 会话无响应](#SSH_会话无响应)
*   [5 参阅](#参阅)

## OpenSSH

OpenSSH (OpenBSD Secure Shell) 是一套使用 ssh 协议，通过计算机网络，提供加密通讯会话的计算机程序。它被创建为 SSH Communications Security 公司拥有专利的 Secure Shell 软件套装的一个开源替代。OpenSSH 是由 Theo de Raadt 领导的 OpenBSD 项目的一部分。

人们常把 OpenSSH 与相似名字的 OpenSSL 搞混，但是，这两个项目是由不同的团队出于不同的目的开发出来的。相似的名字只是由于相似的目标。

### 安装OpenSSH

从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")中[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [openssh](https://www.archlinux.org/packages/?name=openssh).

### SSH 客户端

连接SSH服务器，运行命令

```
$ ssh -p *port* *user*@*server-address*

```

如果服务器仅允许使用密钥登录，请参考 [SSH Keys](/index.php/SSH_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH keys (简体中文)") 。

#### 配置

客户端可以在配置文件中存储常用选项和常用主机，下列选项都可以应用至全局或应用至特定主机。 例如：

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

某些选项没有命令行参数，但是可以使用 `-o` 在命令行中配置指定选项的参数。 例如 `-oKexAlgorithms=+diffie-hellman-group1-sha1`.

### SSH 服务端

#### 配置

SSH 守护进程的配置文件是`/etc/ssh/ssh**d**_config`。

只允许某些用户访问的话，加入这一行：

```
AllowUsers    *user1 user2*

```

只允许一些组访问：

```
AllowGroups   *group1 group2*

```

你也可以运行以下命令关联文件(如`/etc/issue`文件)到登录欢迎信息：

```
 Banner /etc/issue

```

公钥和私钥在 *sshd* [service 文件](#管理_sshd_守护进程) 安装的时候就自动生成在 `/etc/ssh` 里面了，四个秘钥对分别由四种算法生成： [dsa、rsa、ecdsa 和 ed25519](/index.php/SSH_keys#Choosing_the_authentication_key_type "SSH keys")。要让 sshd 使用一组特定的密钥，请指定以下选项：

```
 HostKey /etc/ssh/ssh_host_rsa_key

```

如果此服务器在公网中，建议运行以下命令以更改sshd服务监听端口：

```
 Port 39901

```

**Tip:**

*   参考 [TCP 和 UDP 端口号列表](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers") 和本地的 `/etc/services` 文件来选择一个未被常用服务占用的端口。把端口从默认的 22 改成别的可以减少由于端口扫描器尝试自动登录造成的登录日志条目，更多信息请参考 [Port knocking](/index.php/Port_knocking "Port knocking")。
*   完全取消密码登录方式可以极大的增强安全性，请查看[#强制公钥验证](#强制公钥验证)。查看[#安全防护](#安全防护)了解更多增强安全性的手段。
*   OpenSSH 可以监听多个端口，只需在配置文件中加入多行`Port *port_number*`即可。

#### 管理 sshd 守护进程

[openssh](https://www.archlinux.org/packages/?name=openssh) 包括了两种 [systemd](/index.php/Systemd "Systemd") 服务:

1.  `sshd.service`,使 SSH 守护进程始终运行，并为每个入站连接创建子进程。[[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh#n16) 适用于有大量 SSH 流量的系统。[[2]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh&id=4cadf5dff444e4b7265f8918652f4e6dff733812#n15)
2.  `sshd.socket` + `sshd@.service`, 为每个连接生成 SSH 守护进程的实例。它意味着让 *systemd* 监听 SSH socket，并且只有在有连接传入时启动守护进程。几乎所有情况下都推荐使用`sshd`。 [[3]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh&id=4cadf5dff444e4b7265f8918652f4e6dff733812#n18)[[4]](http://lists.freedesktop.org/archives/systemd-devel/2011-January/001107.html)[[5]](http://0pointer.de/blog/projects/inetd.html)

[start](/index.php/Start "Start") 并 [enable](/index.php/Enable "Enable") `sshd.service` **或** `sshd.socket` 中的任何一个都可以启动守护进程。

如果选择了 sshd.socket，并且不在默认的 22 端口监听，你需要[编辑](/index.php/Edit "Edit") ststemd 单元文件：

 `# systemctl edit sshd.socket` 
```
[Socket]
ListenStream=
ListenStream=12345

```

**警告:** 使用 `sshd.socket` 会使 `ListenAddress` 设置无效，这将允许来自任何地址的连接。为了达到与 `ListenAddress` 一样设置 IP 的效果， 你必须在 `ListenStream` 中指定端口*和* IP (例如：`ListenStream=192.168.1.100:22`)。你还需要在 `[Socket]` 下面增加 `FreeBind=true`，否则设置 IP 与设置 `ListenAddress` 有着相同的缺陷：如果网络未及时启动，socket 将无法启动。

**提示：** 打开 `sshd.service` 时将为每个连接启动一个 `sshd@.service` 的临时实例（实例名称不同）。因此，`sshd.socket` 和常规 `sshd.service` 都不允许监视日志中的连接尝试。使用 `journalctl -u "sshd@*"` 或 `journalctl /usr/bin/sshd` 可以看到 socket 激活的 SSH 实例的日志。

#### 安全防护

允许通过SSH进行远程登录对管理服务器很有用，但也会对服务器构成安全威胁。SSH 通常是暴力攻击的目标，因此 SSH 访问需要适当限制，以防止第三方访问您的服务器。

下列是有关该主题的优秀指南：

*   [Article by Mozilla Infosec Team](https://wiki.mozilla.org/Security/Guidelines/OpenSSH)
*   [Secure sshd](https://stribika.github.io/2015/01/04/secure-secure-shell.html)

##### 强制公钥验证

如果客户端无法通过公钥进行身份验证，则默认情况下，SSH服务器将使用密码来验证，从而允许恶意用户通过[暴力破解](#防止暴力破解)密码获取访问权限。一种防止此类攻击的有效方法是完全禁用密码登录，并强制使用[SSH keys](/index.php/SSH_keys "SSH keys")。可以在 `sshd_config` 中禁用以下选项：

```
PasswordAuthentication no

```

**警告:** 在将上述选项添加到你的配置之前，请确保所有需要 SSH 访问的帐户都在相应的 `authorized_keys` 文件中设置了公钥验证。请参阅 [SSH keys#Copying the public key to the remote server](/index.php/SSH_keys#Copying_the_public_key_to_the_remote_server "SSH keys") 以获取更多信息。

##### 双因素验证与公钥

SSH 可以设置为采用多种方式进行身份验证，你可以使用 `AuthenticationMethods` 选项来指明在登录时需要哪些身份验证方式。这使你可以用公钥与双因素验证结合来登录。

参阅 [Google Authenticator (简体中文)](/index.php/Google_Authenticator_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Google Authenticator (简体中文)") 来设置 Google Authenticator。

为了使 [PAM (简体中文)](/index.php/PAM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PAM (简体中文)") 与 OpenSSH 协同工作， 编辑下列文件：

 `/etc/ssh/sshd_config` 
```
ChallengeResponseAuthentication yes
AuthenticationMethods publickey keyboard-interactive:pam

```

然后，你可以使用公钥**或** PAM 中设置的用户验证信息两者之一登录。

另外，如果你想登录时同时验证公钥**和** PAM，请使用逗号而不是空格来分隔 AuthenticationMethods：

 `/etc/ssh/sshd_config` 
```
ChallengeResponseAuthentication yes
AuthenticationMethods publickey**,**keyboard-interactive:pam

```

通过要求提供公钥**和** PAM 认证，你可能希望禁用密码登录：

 `/etc/pam.d/sshd` 
```
auth      required  pam_securetty.so     #disable remote root
#Require google authenticator
auth      required  pam_google_authenticator.so
#But not password
#auth      include   system-remote-login
account   include   system-remote-login
password  include   system-remote-login
session   include   system-remote-login

```

##### 防止暴力破解

暴力破解的概念很简单，即某人不断尝试用大量随机产生的用户名和密码对来登录网页或服务器的某个服务（比如 SSH）。

###### 使用 ufw

请参阅 [ufw#Rate limiting with ufw](/index.php/Ufw#Rate_limiting_with_ufw "Ufw").

###### 使用 iptables

如果你已经在用 iptables，可以配置以下规则来保护 SSH 免受暴破。

**注意:** 此示例中 SSH 所用的 TCP 端口已经改为了 42660。

在应用后面的规则之前，我们先新建一条规则链来记录并拒绝过多的连接请求：

```
# iptables -N LOG_AND_DROP

```

第一条规则将应用于预示 TCP 42660 端口有新连接的数据包：

```
# iptables -A INPUT -p tcp -m tcp --dport 42660 -m state --state NEW -m recent --set --name DEFAULT --rsource

```

下一条规则告诉 iptables 查找匹配前一条规则的数据包，这些数据包也来自已添加到监视列表中的主机。

```
# iptables -A INPUT -p tcp -m tcp --dport 42660 -m state --state NEW -m recent --update --seconds 90 --hitcount 4 --name DEFAULT --rsource -j LOG_AND_DROP

```

现在，让 iptables 决定如何处理 TCP 42660 端口的通信中不符合上述规则的数据包。

```
# iptables -A INPUT -p tcp -m tcp --dport 42660 -j ACCEPT

```

我们向 LOG_AND_DROP 表增加如下规则，并使用 -j (jump) 参数将数据包的信息传递给日志记录工具。

```
# iptables -A LOG_AND_DROP -j LOG --log-prefix "iptables deny: " --log-level 7

```

在按照第一条规则进行记录后，所有数据包将被丢弃。

```
# iptables -A LOG_AND_DROP -j DROP

```

###### 防止暴力破解的工具

你可以用类似 [fail2ban](/index.php/Fail2ban "Fail2ban") 或 [sshguard](/index.php/Sshguard "Sshguard") 的自动防暴破的脚本来阻挡攻击者。

*   仅允许来自受信任位置的 SSH 入站连接。
*   使用 [fail2ban](/index.php/Fail2ban "Fail2ban") 或 [sshguard](/index.php/Sshguard "Sshguard") 自动阻止多次密码验证失败的 IP 地址。
*   使用 [pam_shield](https://github.com/jtniehof/pam_shield) 来阻止在一定时间内执行过多登录尝试的 IP 地址。与 [fail2ban](/index.php/Fail2ban "Fail2ban") 或 [sshguard](/index.php/Sshguard "Sshguard")不同，该程序不考虑登录成功或失败。

##### 禁用或限制 root 账户登录

允许 root 账户随意通过 SSH 登录通常是不安全的，有两种方法可以限制 root 账户通过 SSH 登录，从而提高安全性。

###### 禁用 root 登录

Sudo 可以有选择地为需要 root 权限的操作提供相应的权限，且不需要登录 root 账户。这样即可关闭 root 登录，并且可以看做一种防范暴力攻击的安全措施，因为现在攻击者除了要猜测密码外还要猜测帐户名称。

通过编辑 `/etc/ssh/sshd_config` 中的 "Authentication" 一节可以使 SSH 屏蔽 root 用户登录，只要将 `#PermitRootLogin prohibit-password` 改成 `no` 并取消该行注释即可：

 `/etc/ssh/sshd_config` 
```
PermitRootLogin no
...

```

然后 [重启](/index.php/Restart "Restart") SSH 守护进程。

现在你将无法通过 root 账户登录，但仍可以用普通账户登录并使用 [su](/index.php/Su "Su") 或者 [sudo](/index.php/Sudo "Sudo") 来完成系统维护工作。

###### 限制 root 登录

一些自动化的维护任务（比如远程备份整个系统）需要完整的 root 权限。要以安全的方式允许 root 登录而不是禁用它，可以只允许远程登录的 root 用户执行指定的命令，在 `~root/.ssh/authorized_keys` 头部加上指定的密钥即可，例如：

```
command="/usr/lib/rsync/rrsync -ro /" ssh-rsa …

```

这样，任何用户持有该秘钥即可执行引号之间的命令。

为了弥补因 root 用户名称暴露而导致受攻击的可能性增加，可以将以下命令加入 `sshd_config`：

```
PermitRootLogin forced-commands-only

```

该设置不仅会限制 root 用户通过 SSH 执行的命令，还会禁用密码登录方式，强制 root 帐户使用公钥登录。

如果不想限制 root 用户可执行的命令，可以仅关闭密码验证来强制使用公钥验证：

```
PermitRootLogin prohibit-password

```

##### 保护 authorized_keys 文件

你可以阻止其他用户向该文件加入新公钥且通过新的公钥连接。

把 `authorized_keys` 文件的权限全部去掉，只保留读权限：

```
$ chmod 400 ~/.ssh/authorized_keys

```

为防止用户把权限改回来，可以对 `authorized_keys` 文件采取 [set the immutable bit（设为不可变）](/index.php/File_permissions_and_attributes#chattr_and_lsattr "File permissions and attributes") 操作。尽管如此，用户仍然可以重命名 `~/.ssh` 并新建一个 `~/.ssh` 目录和 `authorized_keys` 文件。所以 `~/.ssh` 目录也要设置 immutable bit。

**注意:** 如果你自己需要新增一个公钥，你需要先移除 `authorized_keys` 文件的 immutable bit，并增加写权限，最后按上述步骤重新加密。

## 其他 SSH 客户端与服务端

除了 OpenSSH，还有很多可用的 SSH [客户端](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients "wikipedia:Comparison of SSH clients") 和 [服务端](https://en.wikipedia.org/wiki/Comparison_of_SSH_servers "wikipedia:Comparison of SSH servers")。

### Dropbear

[Dropbear](https://en.wikipedia.org/wiki/Dropbear_(software) 是一个 SSH-2 客户端与服务端。 [dropbear](https://www.archlinux.org/packages/?name=dropbear) 可以从 [官方仓库](/index.php/Official_repositories "Official repositories") 下载。

它的命令行版客户端叫 dbclient。

### Mosh

来自 Mosh [网站](http://mosh.mit.edu/)：

	Remote terminal application that allows roaming, supports intermittent connectivity, and provides intelligent local echo and line editing of user keystrokes. Mosh is a replacement for SSH. It is more robust and responsive, especially over slow connections such as Wi-Fi, cellular, and long-distance.

	翻译：允许“漫游”的远程终端，支持间歇性的连接，并提供对于用户按键的智能本地回馈和行编辑回馈。Mosh 是 SSH 的替代品。它更加强大而快速，特别针对诸如 Wi-Fi，移动网络和超远距离等慢速连接环境。

[安装](/index.php/Install "Install") [mosh](https://www.archlinux.org/packages/?name=mosh) 这个包， 或安装最新版：[mosh-git](https://aur.archlinux.org/packages/mosh-git/)。

Mosh 有一个未写入文档的命令行选项：`--predict=experimental`，它可以产生更有力的本地按键响应。对降低键盘输入视觉上的延迟确认感兴趣的用户可能更喜欢这个预测模式。

**提示：** Mosh 从设计上就不允许你访问会话的历史记录，请考虑安装终端复用工具，如 [tmux](/index.php/Tmux "Tmux") 或 [GNU Screen](/index.php/GNU_Screen "GNU Screen") 。

## 提示与技巧

### 加密 Socks 通道

对于连接到各种不安全的无线网络上的笔记本电脑用户来说,这个是特别有用的！唯一所需要的就是一个一定程度上处于安全的地点的 SSH 服务器，比如在家里或办公室。用动态的 DNS 服务 [DynDNS](http://www.dyndns.org/) 也可能是很有用的，这样你就不必记住你的 IP 了。

#### 第一步：开始连接

你只要执行这一个命令就能开始你的连接：

```
$ ssh -TND 4711 *user*@*host*

```

这里的 `*user*` 是你在 `*host*` 这台 SSH 服务器上的用户名。它会让你输入密码，然后你就能连上了。 `N` 表示不采用交互提示，而 `D` 表示指定监听的本地端口（你可以使用任何你喜欢的数字），`T` 表示禁用伪 tty 分配。

加了 `-v` (verbose) 标志以后的输出可以让你能够验证到底连了哪个端口。

#### 第二步：配置你的浏览器(或其它程序)

如果你没有配置你的浏览器（或其他程序）使用这个新创建的 socks 隧道，上述步骤是无效的。由于当前版本的 SSH 支持 SOCKS4 和 SOCKS5，因此您可以使用其中任何一种。

*   对于 Firefox: *Edit > Preferences > Advanced > Network > Connection > Setting*:
    选中 *Manual proxy configuration* 单选框, 然后在 *SOCKS host* 里输入 `localhost`， 然后在后面那个框中输入你的端口号（本例中为 `4711`）。

Firefox 不会自动通过 socks 隧道发送 DNS 请求，这一潜在的隐私问题可以通过以下步骤来解决：

1.  在 Firefox 地址栏中输入：about:config 。
2.  搜索：network.proxy.socks_remote_dns
3.  将该值设为 true。
4.  重启浏览器。

*   对于 Chromium: 你可以将 SOCKS 设置设置为环境变量或命令行选项。我建议将下列函数之一加入到你的 `.bashrc`：

```
function secure_chromium {
    port=4711
    export SOCKS_SERVER=localhost:$port
    export SOCKS_VERSION=5
    chromium &
    exit
}

```

或者

```
function secure_chromium {
    port=4711
    chromium --proxy-server="socks://localhost:$port" &
    exit
}

```

现在打开终端然后输入：

```
$ secure_chromium

```

享受你的安全隧道吧！

### X11 转发

为了通过 SSH 运行图形程序你必须使用 X11 转发 (forwarding)。这不要求对端安装了完整的 X11，但是至少要装好 *xauth*。*xauth* 是一个用来管理 `Xauthority` 配置的工具，该配置用于服务器与客户端之间的 X11 会话认证([source](http://xmodulo.com/2012/11/how-to-enable-x11-forwarding-using-ssh.html))。

**警告:** X11 转发有着重要的安全问题需要考虑，至少应先阅读 [ssh(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh.1)、[sshd_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5) 和 [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5) 手册页。也可以参考 [这个 StackExchange 帖](https://security.stackexchange.com/questions/14815/security-concerns-with-x11-forwarding)。

#### 配置

在远程主机上：

*   [安装](/index.php/Install "Install") [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) 和 [xorg-xhost](https://www.archlinux.org/packages/?name=xorg-xhost) 这两个包
*   在 `/etc/ssh/ssh**d**_config` 上:
    *   确保 `AllowTcpForwarding` 和 `X11UseLocalhost` 已经设置为 *yes*，并且 `X11DisplayOffset` 设置为 *10* （这些是默认设置，参考 [sshd_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5)）
    *   将 `X11Forwarding` 设置为 *yes*
*   最后 [重启](/index.php/Restart "Restart") [*sshd* 守护进程](#Daemon_management).

在客户端上，通过在命令行设置 `-X` 参数启用 `ForwardX11`，或者在[客户端配置文件](#配置)中将 `ForwardX11` 设置为 *yes*。

**提示：** 如果 GUI 绘制不正常或者有错误提示，你可以启用 `ForwardX11Trusted` 选项（或在命令行中加上 `-Y` 参数），这将使 X11 转发脱离 [X11 SECURITY extension](http://www.x.org/wiki/Development/Documentation/Security/) 的控制，如果你这样做，请确保已经读过本节开头的[警告](#X11_转发)。

#### 使用方法

正常登录远程主机，如果客户端的配置文件中没有启用 *ForwardX11* 那就加上 `-X` 参数：

```
$ ssh -X *user@host*

```

如果在运行图形程序的时候碰到错误，尝试用 *ForwardX11Trusted* 代替 *ForwardX11* ：

```
$ ssh -Y *user@host*

```

现在你应该可以运行服务器上的任何 X 图形程序，任何输出都会重定向至你当前的会话：

```
$ xclock

```

如果碰到 "Cannot open display" 的错误，请尝试用非管理员账户运行下列命令：

```
$ xhost +

```

上述命令将允许任何人转发 X11 应用程序，这个命令可以限制特定的主机类型：

```
$ xhost +hostname

```

其中 hostname 是要转发到的特定主机的名称。更多信息可以查看 [xhost(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xhost.1)。

请注意某些应用程序，它们会检查本地计算机上正在运行的实例。[Firefox](/index.php/Firefox "Firefox") 就是其中之一：你可以关掉本机上的 Firefox 或者使用以下启动参数来启动远程实例：

```
$ firefox --no-remote

```

当你连接时收到 "X11 forwarding request failed on channel 0" 错误（或者服务器上的 `/var/log/errors.log` 文件显示 "Failed to allocate internet-domain X11 display socket" 错误），请确保已经安装 [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth)，如果装完了仍然不起作用，尝试以下方法之一：

*   在*服务器*的 `ssh**d**_config` 中启用 `AddressFamily any` 选项，或者
*   将*服务器*的 `ssh**d**_config` 中的 `AddressFamily` 选项设为 inet。

将其设置为 inet 可能会修复 IPv4 上的 Ubuntu 客户端的问题。

要以其他用户身份运行 SSH 服务器上的 X 应用程序，你需要先用已知用户登录，取出 `xauth list` 中的身份认证行，然后 `xauth add` 它。

**提示：** [这里](http://unix.stackexchange.com/a/12772/29867) 是 [一些](http://unix.stackexchange.com/a/46748/29867) 用来诊断 `X11 Forwarding` 问题有用的 [链接](http://superuser.com/a/805060/185665)。

### 转发其他端口

除了 SSH 内建的对 X11 的支持之外，它也能通过本地转发和远程转发，来为任何的TCP连接建立隧道。

本地转发时，会在本机打开一个端口，连接将被转发到一个远程主机，并给定一个目的地。很多时候，转发目的地和远程主机会相同，因此也提供了一条SSH命令来建立一个安全的VNC连接。本地转发可以通过 `-L` 来设置，后面可以指定一个地址及端口 `<tunnel port>:<destination address>:<destination port>`。

如下：

```
$ ssh -L 1000:mail.google.com:25 192.168.0.100

```

以上指令将会通过 SSH 得到一个在 `192.168.0.100` 的 shell，同时也会创建一个从本机 TCP 1000 端口到 mail.google.com 上的 25 端口的隧道。建立之后，通过 `localhost:1000` 的连接可以直接连接到 Gmail 的 SMTP 端口。对 Google 而言，任何这样的连接都是来自 `192.168.0.100` 的（即使这些连接中没有数据传输），并且，在本机和 192.168.0.100 之间的数据传递是安全的，但 `192.168.0.100` 和 Google 之间是不安全的，除非还采取了别的手段保障数据安全。

同样：

```
$ ssh -L 2000:192.168.0.100:6001 192.168.0.100

```

以上指令会将到 `localhost:2000` 的连接直接转发到远程主机 192.168.0.100 的 6001 端口。对于使用 VNC 服务器（tightvns包的一部分）建立的 VNC 连接来说，以上的例子尽管很有效，但是安全性有待商榷。

远程转发允许任何远程主机通过 SSH 隧道连接到本机，提供了和本地转发相反的功能，突破了防火墙的限制。通过 `-R` 参数，以及 `<tunnel port>:<destination address>:<destination port>` 能够实现远程转发。

如下:

```
$ ssh -R 3000:irc.freenode.net:6667 192.168.0.200

```

将会在 `192.168.0.200` 上得到一个 shell，同时，来自 `192.168.0.200` 的 3000 端口（远程主机的 `localhost:3000`）的数据将会通过隧道转发至本机，然后转发至 irc.freenode.net 上的 6667 端口。因此，在这个例子中，在远程主机上能够使用 IRC 程序，即使端口 6667 被阻止。

本地转发和远程转发都可以提供一个安全的“网关”，允许其他计算机无需运行 SSH 或者 SSH daemon 来使用 SSH 隧道，即在隧道起点提供绑定的地址，作为转发规则。例如 `<tunnel address>:<tunnel port>:<destination address>:<destination port>`。`<tunnel address>` 可以是作为隧道起点的机器上的任何地址，地址 `localhost` 允许来自本地回环的连接，空地址 `*` 允许来自任意网卡的连接。默认情况下，转发仅限于连接至位于隧道“起点”的主机，即 `<tunnel address>` 被设置为 `localhost`。本地转发不需要额外的设置，而远程转发受限于对端的 SSH daemon 设置。更多关于远程转发和本地转发的信息可分别参阅 [sshd_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5) 中的 `GatewayPorts` 选项和 [ssh(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh.1) 中的 `-L address` 选项。

### 跳板机

在某些情况下，你与目标主机之间可能无法直接连接，此时就要用到跳板机。因此，我们尝试将两个或更多 SSH 隧道连接在一起，并假设您的本地密钥已针对链中的每个服务器授权。这可以通过使用SSH代理转发 (`-A`) 和伪终端分配 (`-t`) 来实现，它使用以下语法转发本地密钥：

```
$ ssh -A -t -l user1 bastion1 \
  ssh -A -t -l user2 intermediate2 \
  ssh -A -t -l user3 target

```

一个更简单的方法是使用 `-J` 选项：

```
$ ssh -J user1@bastion1,user2@intermediate2 user3@target

```

`-J` 指令中的多个主机可以用逗号隔开，它们将按照列出的顺序连接。`user...@` 部分不是必需的，但可以使用。定义 `-J` 选项里的不同的主机规格可以使用 ssh 配置文件，因此如果需要，可以在那里设置特定的每个主机选项。

### 通过中继反向 SSH 连接

这个想法是客户端通过一个中继连接到服务器，而服务器使用反向 SSH 隧道连接到同一个中继。例如，当服务器位于 NAT 后面时，这是很有用的，而此处的中继是一个可公开访问的 SSH 服务器，用作用户有权访问的代理服务器。前提是客户端的密钥同时对中继和服务器都已经授权，服务器需要授权中继用于反向 SSH 连接。

以下配置假设 user1 是客户端使用的账户，user2 是中继的，user3 是服务器的。首先服务器要先建立反向隧道：

```
ssh -R 2222:localhost:22 -N user2@relay

```

这可以利用启动脚本、systemd service 或者 [autossh](https://www.archlinux.org/packages/?name=autossh) 来自动完成。

在客户端使用以下命令建立连接：

```
ssh user2@relay ssh user3@localhost -p 2222

```

可以在中继的 `~/.ssh/authorized_keys` 中定义 `command` 字段来建立反向隧道：

```
command="ssh user3@localhost -p 2222" ssh-rsa KEY2 user1@client

```

在这种情况下用下列命令建立连接：

```
ssh user2@relay

```

注意，客户端内 scp 的自动完成功能失效，甚至在某些配置下 scp 本身也无法工作。

### 端口复用

SSH 守护进程通常监听 22 端口，但是许多公共热点会屏蔽非常规 HTTP/S 端口（分别是 80 和 443 端口）的流量，这样就屏蔽了 SSH 连接。最快的解决方法是让 `sshd` 额外监听白名单上的端口：

 `/etc/ssh/sshd_config` 
```
Port 22
Port 443

```

但是443端口很有可能已经被 HTTPS 服务占用，在这种情况下可以使用端口复用工具，比如 [sslh](https://www.archlinux.org/packages/?name=sslh)，它可以监听在一个被复用的端口上并转发相应的数据包给对应的服务。

### 加速 SSH

此处列出一些可以加速全部连接或针对某台主机加速的 [客户端配置](#配置) 选项。要了解这些选项的完整概述，请参阅 [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5)。

*   使用以下参数来使到某一台主机的所有回话 (sessions) 共享同一个连接：
    ```
    ControlMaster auto
    ControlPersist yes
    ControlPath ~/.ssh/sockets/socket-%r@%h:%p

    ```

	其中 `~/.ssh/sockets` 可以是一个其他用户不可写入的任意目录。

*   `ControlPersist` 指定在初始客户端连接关闭后，主服务器在后台等待新客户端的时间。可能的值是：
    *   `no` 指定在最后一个客户端断开后立即关闭连接，
    *   一个用秒数表示的时间，
    *   `yes` 连接不会自动关闭，而是始终处于等待。

*   另一种加速的方法是通过 `Compression yes` 选项或者 `-C` 参数来启用压缩。

**注意:** [ssh(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh.1) 指出：“在调制解调器线路或其他慢速线路上启用压缩是可取的，但在网速快的情况下只会降低速度。”这条提示可能会适得其反，具体取决于你的网络配置。

*   通过使用 `AddressFamily inet` 选项或者 `-4` 参数来跳过 IPv6 查找，可以缩短登录时间。

*   最后，如果你想用 SFTP 或 SCP，[High Performance SSH/SCP](https://www.psc.edu/index.php/hpn-ssh) 可以通过动态提高 SSH 缓冲区大小来显著提高吞吐量。安装 [openssh-hpn-git](https://aur.archlinux.org/packages/openssh-hpn-git/) 这个包来使用打过这一增强补丁的 OpenSSH 版本。

### 用 SSHFS 挂载远程文件系统

请参阅 [SSHFS](/index.php/SSHFS "SSHFS") 来将一个 SSH 可访问的远程文件系统挂载至一个本地目录，然后你就能在挂载好的文件上执行常规操作（复制，重命名，用 vim 编辑等等）。*sshfs* 比 *shfs* 更好，因为后者自 2004 年起就没再更新。

**提示：** 软件包 [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) 可以用于在登录时自动运行 autosshfs。

### 保持在线

默认情况下，如果你的会话空闲了某个时间之后，它会自动登出。为了保持会话，在长时间没有数据传输时客户端可以向服务器发送一个激活信号。与之对应，服务器也可以在一段时间没有收到消息时定期发送一个信号。

*   在 **服务器**，`ClientAliveInterval` 是没有从客户端收到消息后的超时时间，超时后 *sshd* 将会发送一个请求来等待回应。默认是 0，指不会发出请求。比如要求每隔 60 秒向客户端发送响应请求，在你的 [服务器配置](#配置_2) 里设置 `ClientAliveInterval 60` 即可。`ClientAliveCountMax` 和 `TCPKeepAlive` 选项也可以参考一下。
*   在 **客户端**，`ServerAliveInterval` 控制着从客户端发往服务器的响应请求的时间间隔。比如要求服务器每隔 120 秒响应一次，在你的 [客户端配置](#配置) 里加入 `ServerAliveInterval 120` 即可。`ServerAliveCountMax` 和 `TCPKeepAlive` 选项也可以参考一下。

**注意:** 为确保会话保持活动状态，客户端或服务器中只有一个需要发送保持活动请求。如果用户同时控制服务器和客户端，那么合理的选择是使用 `ServerAliveInterval` 选项配置需要保持会话的客户端，并保留其他客户端和服务器的默认配置。

### 利用 systemd 自动重启 SSH 隧道

[systemd](/index.php/Systemd "Systemd") 可以在开机/登录时自动启动 SSH，*还可以* 在 SSH 连接断开时自动重连。这使它成为管理 SSH 隧道的有力工具。

下面的 service 可以使用 [ssh 配置](#配置) 里面的配置在你登录系统的时候自动开启一个 SSH 隧道。如果连接因为某种原因断开，它将会每隔10秒重启一下：

 `~/.config/systemd/user/tunnel.service` 
```
[Unit]
Description=SSH tunnel to myserver

[Service]
Type=simple
Restart=always
RestartSec=10
ExecStart=/usr/bin/ssh -F %h/.ssh/config -N myserver

```

然后 [enable](/index.php/Enable "Enable") 并且 [start](/index.php/Start "Start") 这个 user service。欲知如何防止连接超时，请参阅 [#Keep alive](#Keep_alive)。如果你想在系统引导后就打开这个连接，你需要将这个 unit 重写为 system service。

### Autossh - 自动重启 SSH 会话和隧道连接

当一个 SSH 会话或隧道无法保持连接（比如网络环境差导致客户端断线），可以使用 [autossh](https://www.archlinux.org/packages/?name=autossh) 来自动重启它们。

使用范例：

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" username@example.com

```

结合 [SSHFS](/index.php/SSHFS "SSHFS")：

```
$ sshfs -o reconnect,compression=yes,transform_symlinks,ServerAliveInterval=45,ServerAliveCountMax=2,ssh_command='autossh -M 0' username@example.com: /mnt/example 

```

通过一个由 [Proxy settings](/index.php/Proxy_settings "Proxy settings") 设置好的 SOCKS 代理来连接：

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" -NCD 8080 username@example.com 

```

使用 `-f` 选项以后可以使 autossh 作为后台进程运行，然而以这种方式运行意味着不能交互输入密码。

当你在会话中打出 `exit` 即可结束会话，或者 autossh 收到了 SIGTERM, SIGINT of SIGKILL 信号。

#### 利用 systemd 在引导后自动运行 autossh

如果你想自动启动 autossh，创建一个 systemd unit 文件：

 `/etc/systemd/system/autossh.service` 
```
[Unit]
Description=AutoSSH service for port 2222
After=network.target

[Service]
Environment="AUTOSSH_GATETIME=0"
ExecStart=/usr/bin/autossh -M 0 -NL 2222:localhost:2222 -o TCPKeepAlive=yes foo@bar.com

[Install]
WantedBy=multi-user.target
```

其中 `AUTOSSH_GATETIME=0` 是一个环境变量，它表示 ssh 需要连上多久，autossh 才判定这个连接是成功的。将它设为 0 后 autossh 也会忽略 ssh 的第一次运行失败。这在开机启动 autossh 时可能是有用的。其他环境变量可以在手册页找到。当然，如果需要的话，你可以使这个单元更加复杂（详情请参阅 systemd 文档），显然你可以使用自己的 autossh 选项，但请注意 `-f` 选项意味着 `AUTOSSH_GATETIME=0` 无法在 systemd 中起效。

别忘了 [start](/index.php/Start "Start") 且/或 [enable](/index.php/Enable "Enable") 这个 service。

你可能还会需要关闭 ControlMaster，像这样：

```
ExecStart=/usr/bin/autossh -M 0 -o ControlMaster=no -NL 2222:localhost:2222 -o TCPKeepAlive=yes foo@bar.com

```

**提示：** 同时管理多个 autossh 进程也是很简单的，要保持多个隧道连接，只需要用不同的文件名创建多个 service 文件。

### 当 SSH 守护进程出错时的其他选择

对于仅依赖 SSH 的远程或无头服务器，启动 SSH 守护程序失败（例如系统升级后）可能会阻止管理员访问。[systemd](/index.php/Systemd "Systemd") 通过 `OnFailure` 选项提供了简便的解决方案。

假设服务器运行 `sshd` 并且 [telnet](/index.php/Telnet "Telnet") 是所选的故障安全替代方案。按如下所示创建一个文件。**不要** [enable](/index.php/Enable "Enable") telnet.socket！

 `/etc/systemd/system/sshd.service.d/override.conf` 
```
[Unit]
OnFailure=telnet.socket
```

这样就行了。当 `sshd` 正在运行时，Telnet 是不可用的。如果 `sshd` 无法启动，可以打开一个 telnet 会话进行恢复。

## 疑难解答

### 自检清单

在进一步阅读前，请先仔细检查下面这些常见故障。

1.  配置文件存放目录 `~/.ssh` 及目录下的文件应该只有你的账户才有访问权限（在客户端和服务器上都检查这一条）：
    ```
    $ chmod 700 ~/.ssh
    $ chmod 600 ~/.ssh/*
    $ chown -R $USER ~/.ssh

    ```

2.  检查客户端的公钥（比如 `id_rsa.pub`）在服务器的 `~/.ssh/authorized_keys` 文件里面。
3.  检查有没有在 [服务器配置](#配置_2) 里面设置 `AllowUsers` 或 `AllowGroups` 来限制 SSH 访问。
4.  检查用户是否设置了密码。有时还没有登录过服务器的新用户没有密码。
5.  把 `LogLevel DEBUG` 加到 `/etc/ssh/sshd_config` 文件尾部。
6.  使用 `journalctl -xe` 查看可能的错误信息。
7.  在客户端和服务器上 [重启](/index.php/Restart "Restart") `sshd` 然后注销/重新登录。

### 拒绝连接或者超时问题

#### 端口转发

如果您位于 NAT 模式/路由器之后（除非您位于 VPS 或可公开寻址的主机上），请确保您的路由器可以将传入的 ssh 连接转发到您的计算机。使用 `$ ip addr` 查找服务器的内网 IP 地址，并将您的路由器设置为将 SSH 端口上的 TCP 数据包转发到该 IP。[portforward.com](http://portforward.com) 可以提供帮助。

#### SSH服务是否开启并且正在监听？

```
$ ss -tnlp

```

如果以上的命令没有显示 SSH 端口是打开的，那么说明 SSH 服务没有启动。查看 `/var/log/messages` 来寻找错误信息。

#### 是否是防火墙阻止了连接？

[Iptables](/index.php/Iptables "Iptables") 可能会阻止 `22` 端口的连接。使用 `# iptables -nvL` 来检查可能会在 `INPUT` 链上导致丢包的规则。必要情况下可以用以下命令来解锁端口：
```
# iptables -I INPUT 1 -p tcp --dport 22 -j ACCEPT

```

更多配置防火墙的信息，请参阅 [firewalls](/index.php/Firewalls "Firewalls").

#### 你的电脑和目的主机之间是否连接？

测试你的电脑和目的主机的连接情况：

```
# tcpdump -lnn -i any port ssh and tcp-syn

```

它会显示一些基本信息，然后等待数据交换。现在尝试你的连接。如果没有输出，就可能是你的电脑网络阻塞了。（也许是防火墙问题，也许是 NAT 路由的问题）

#### 你的 ISP 或第三方屏蔽了默认端口？

**注意:** 只有在你**确保**你没有运行任何防火墙，你已经在路由器上配置了 DMZ 主机或已经将端口映射到你的计算机，而这些都没有用的情况下才尝试以下步骤。可以在此找到诊断步骤或可能的解决方案。

某些情况下，你的运营商会屏蔽默认端口（22 端口），无论怎么尝试（尝试开启端口、强化堆栈、防范洪水攻击）都无济于事。要确认确实存在屏蔽，只要创建一个接受任何来源（0.0.0.0）的服务器并远程连接它。

如果你收到与此类似的错误消息：

```
ssh: connect to host www.inet.hr port 22: Connection refused

```

就表示你的 ISP **没有**屏蔽端口，但是服务器没有在该端口上运行 SSH 服务（请参阅 [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity")）。

但是，如果你收到与这条类似的错误消息：

```
ssh: connect to host 111.222.333.444 port 22: Operation timed out 

```

这就表示有人阻止了 22 端口的 TCP 连接，基本上是通过防火墙或第三方干预（如 ISP 阻止和/或拒绝端口 22 上的传入通信），使得端口不可用。如果你的计算机上没有运行任何防火墙，并且在你的路由器和交换机中没有这方面的流量，那么你的 ISP 屏蔽了通讯。

为了再次检查确认，可以在服务器上运行 Wireshark 并让它监听在 22 端口。由于 Wireshark 是一个二层数据包嗅探工具，而 TCP/UDP 工作在第三层及以上（参阅 [IP Network stack](https://en.wikipedia.org/wiki/Internet_protocol_suite "wikipedia:Internet protocol suite")），如果在连接时未收到任何内容，则第三方很可能阻止了该端口上到服务器的流量。

##### 诊断

[安装](/index.php/Install "Install") [tcpdump](https://www.archlinux.org/packages/?name=tcpdump) 或 Wireshark ([wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli))。

用于 tcpdump:

```
# tcpdump -ni *interface* "port 22"

```

用于 Wireshark:

```
$ tshark -f "tcp port 22" -i *interface*

```

其中 `*interface*` 是用于连接 WAN 的网络适配器（用 `ip a` 来查找）。如果在尝试远程连接时没有收到任何数据包，则可以确信你的 ISP 屏蔽了 22 端口上的传入连接。

##### 可能的解决方案

此方案是换一个 ISP 没有屏蔽的端口。编辑 `/etc/ssh/sshd_config` 文件来使用不同的端口。例如，新增这几行：

```
Port 22
Port 1234

```

还要确保文件中的其他“Port”配置行被注释掉。只是注释“Port 22”并加上“Port 1234”不会解决问题，因为那样 sshd 将只监听在 1234 端口上。写入这两行可以在两个端口上运行 SSH 服务器。

[重启](/index.php/Restart "Restart") 服务器上的 `sshd.service` 就基本完成了。你还需要配置客户端来使用与默认端口不同的端口，这个问题有很多种解决方案，在这里我们只介绍两种。

#### "Read from socket failed: connection reset by peer" 错误

使用最近版本的 openssh 连接到较旧的 ssh 服务器时有时会失败，并显示上述错误消息。这可以通过为该主机设置各种 [客户端选项](#配置) 来解决。有关下列选项的更多信息，请参阅 [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5)。

问题可能出在 `ecdsa-sha2-nistp*-cert-v01@openssh` 椭圆曲线算法上。这些算法可以通过在 `HostKeyAlgorithms` 里设置可用算法来排除那些算法。

如果这不起作用，可能是秘钥列表太长了。设置 `Ciphers` 来减少列表长度（少于 80 个字符应该可以）。同样的，也可以尝试缩短 `MACs` 列表。

参阅 openssh bug forum 上的 [讨论](http://www.gossamer-threads.com/lists/openssh/dev/51339)。

### "[your shell]: No such file or directory" / SSH 认证问题

对于这个问题，一个可能的原因是需要 SSH 客户端在 `$SHELL` 中提供绝对路径（例如可以通过 `whereis -b [your shell]` 得到)，即使你的 shell 在 `$PATH` 里的某个路径中。

### "Terminal unknown" 或 "Error opening terminal" 错误

如果你在登录时收到上述错误，这意味着服务器无法识别你的终端。使用 Ncurses 的应用程序（如 nano）可能会失败，并显示“Error opening terminal”。

正确的解决方案是在服务器上安装客户端终端的 terminfo 文件。这会告诉服务器上的控制台程序如何正确地与终端进行交互。你可以使用 `$ infocmp` 获得关于当前 terminfo 的信息，然后找出 [哪个包包括了它们](/index.php/Pacman#Querying_package_databases "Pacman")。

如果你不能正常[安装](/index.php/Install "Install")它，可以把 terminfo 复制到服务器上你的主目录里面：

```
$ ssh myserver mkdir -p  ~/.terminfo/${TERM:0:1}
$ scp /usr/share/terminfo/${TERM:0:1}/$TERM myserver:~/.terminfo/${TERM:0:1}/

```

重新登录、登出服务器后这个问题应该已经解决。

#### TERM hack

**警告:** 这只能作为最后的手段。

你可以在服务器上的环境（例如 `.bash_profile`）中简单地设置 `TERM=xterm` 。这将消除错误并允许 ncurses 应用程序再次运行，但除非你的终端的控制序列与 xterm 完全匹配，否则可能会遇到奇怪的行为和图形界面问题。

### "Connection closed by x.x.x.x [preauth]" 错误

如果你在 sshd 的 log 里看到这条错误，请确保你已经设置了可用的 HostKey

```
HostKey /etc/ssh/ssh_host_rsa_key

```

### id_dsa 被 OpenSSH 7.0 拒绝

出于安全原因，OpenSSH 7.0 弃用了 DSA 公钥。如果你必须启用它们，请[设置](#配置) `PubkeyAcceptedKeyTypes +ssh-dss` 选项（[http://www.openssh.com/legacy.html](http://www.openssh.com/legacy.html) 没有提到这一点）。

### OpenSSH 7.0 的 "No matching key exchange method found" 错误

OpenSSH 7.0 弃用了 diffie-hellman-group1-sha1 密钥算法，因为它很弱并且在所谓 Logjam 攻击的理论范围内（参阅http://www.openssh.com/legacy.html）。如果特定主机需要这个密钥算法，ssh 会产生如下错误消息：

```
Unable to negotiate with 127.0.0.1: no matching key exchange method found.
Their offer: diffie-hellman-group1-sha1

```

这个问题的最佳解决方案是将服务器升级/配置为不使用不推荐的算法。如果做不到这一点，可以配置[客户端选项](#配置) `KexAlgorithms +diffie-hellman-group1-sha1` 强制客户端使用这个算法。

### 断开 SSH 连接时 tmux/screen 会话被关闭

如果进程在会话结束时被终止，那么你可能是用 ssh.socket 激活的，[systemd](https://www.archlinux.org/packages/?name=systemd) 注意到 SSH 会话进程退出，然后杀掉了 tmux/screen 进程。这种情况有两种解决方案。一种是通过使用 `ssh.service` 来代替 `ssh.socket` 来避免使用 socket 激活。另一个是在 `ssh@.service` 的 Service 部分设置 `KillMode=process`。

在常规的 `ssh.service` 里面 `KillMode=process` 这个选项也是有用的，它可以在 service 停止或重启时防止 SSH 会话进程或 [screen](https://www.archlinux.org/packages/?name=screen) 或 [tmux](https://www.archlinux.org/packages/?name=tmux) 进程被 kill 掉。

### SSH 会话无响应

SSH 响应 [流控制命令](https://en.wikipedia.org/wiki/Software_flow_control "wikipedia:Software flow control") 中的 `XON` 和 `XOFF` 命令。 当你按 `Ctrl+s` 时，它会冻结/挂起/停止响应。按 `Ctrl+q` 恢复会话。

## 参阅

*   [Wikipedia:Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell")
*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)
*   [OpenSSH key management, Part 1](http://www.ibm.com/developerworks/library/l-keyc/index.html) and [Part 2](http://www.ibm.com/developerworks/library/l-keyc2) on IBM developerWorks
*   [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)