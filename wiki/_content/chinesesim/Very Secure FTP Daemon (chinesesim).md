**翻译状态：** 本文是英文页面 [Very Secure FTP Daemon](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-19，点击[这里](https://wiki.archlinux.org/index.php?title=Very+Secure+FTP+Daemon&diff=0&oldid=536323)可以查看翻译后英文页面的改动。

[vsftpd](https://security.appspot.com/vsftpd.html) (“Very Secure FTP Daemon“) 是一个为 UNIX 类系统开发的轻量，稳定和安全的 FTP 服务器端。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 允许上传](#允许上传)
    *   [2.2 本地用户登录](#本地用户登录)
    *   [2.3 匿名用户登录](#匿名用户登录)
    *   [2.4 Chroot 限制](#Chroot_限制)
    *   [2.5 限制用户登录](#限制用户登录)
    *   [2.6 限制连接数](#限制连接数)
    *   [2.7 使用 xinetd](#使用_xinetd)
    *   [2.8 使用 SSL/TLS 来保护 FTP](#使用_SSL/TLS_来保护_FTP)
    *   [2.9 在被动模式下解析主机名](#在被动模式下解析主机名)
    *   [2.10 端口配置](#端口配置)
    *   [2.11 配置 iptables](#配置_iptables)
*   [3 小技巧](#小技巧)
    *   [3.1 虚拟用户的 PAM 认证](#虚拟用户的_PAM_认证)
        *   [3.1.1 为虚拟用户创建私有目录](#为虚拟用户创建私有目录)
*   [4 问题解决](#问题解决)
    *   [4.1 vsftpd: Error 500 with kernel 4.18+](#vsftpd:_Error_500_with_kernel_4.18+)
    *   [4.2 vsftpd: refusing to run with writable root inside chroot()](#vsftpd:_refusing_to_run_with_writable_root_inside_chroot())
    *   [4.3 FileZilla Client: GnuTLS error -8 -15 -110 when connecting via SSL](#FileZilla_Client:_GnuTLS_error_-8_-15_-110_when_connecting_via_SSL)
    *   [4.4 vsftpd.service fails to run on boot](#vsftpd.service_fails_to_run_on_boot)
    *   [4.5 Passive mode replies with the local IP address to a remote connection](#Passive_mode_replies_with_the_local_IP_address_to_a_remote_connection)
    *   [4.6 ipv6 only fails with: 500 OOPS: run two copies of vsftpd for IPv4 and IPv6](#ipv6_only_fails_with:_500_OOPS:_run_two_copies_of_vsftpd_for_IPv4_and_IPv6)
    *   [4.7 vsftpd 连接在使用 nis 的机器上失败: yp_bind_client_create_v2: RPC: Unable to send](#vsftpd_连接在使用_nis_的机器上失败:_yp_bind_client_create_v2:_RPC:_Unable_to_send)
*   [5 更多资源](#更多资源)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [vsftpd](https://www.archlinux.org/packages/?name=vsftpd) 然后 [启动/启用](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)") `vsftpd.service` 守护程序。

使用 [xinetd](https://en.wikipedia.org/wiki/xinetd "wikipedia:xinetd") 监视和控制 vsftpd 连接，请参见 [#使用 xinetd](#使用_xinetd)。

## 配置

vsftpd 的大多数配置都可以通过编辑 `/etc/vsftpd.conf` 文件实现。 该文件本身自带大量注释说明，所以这一章节只就一些重要的配置予以说明。有关所有可用选项和文档，请参阅 [vsftpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vsftpd.conf.5) 手册页。默认情况下，由 `/srv/ftp` 提供文件。

允许的连接 `/etc/hosts.allow`：

```
# 允许所有连接
vsftpd: ALL
# IP 地址范围
vsftpd: 10.0.0.0/255.255.255.0

```

### 允许上传

需要将 `/etc/vsftpd.conf` 中的 `write_enable` 值设为 YES，以便允许修改文件系统（如上传）：

```
write_enable=YES

```

### 本地用户登录

需要修改 `/etc/vsftpd.conf` 中的如下值，以便允许 `/etc/passwd` 中的用户登录:

```
local_enable=YES

```

### 匿名用户登录

以下行控制匿名用户是否可以登录。默认情况下，匿名登录只能从 `/srv/ftp` 下载：

 `/etc/vsftpd.conf` 
```
...
# 允许匿名 FTP？ （当心 - 默认情况下允许除非您将其注释）。
anonymous_enable=YES
...
# 取消注释以允许匿名 FTP 用户上传文件。
# 只有上述全局写入被激活，才会有效果。
# 另外，你显然需要创建 FTP 用户有写权限的目录。
# anon_upload_enable=YES
#
# 如果您希望匿名 FTP 用户能够创建新目录，请取消注释。
# anon_mkdir_write_enable=YES
...
```

您也可以添加以下选项（详见 [vsftpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vsftpd.conf.5)）：

 `/etc/vsftpd.conf` 
```
# 匿名登录不需要密码
no_anon_password=YES

# 匿名客户端的最大传输速率（以 Bytes/秒 为单位）
anon_max_rate=30000

# 用于匿名登录的目录
anon_root=/example/directory/
```

### Chroot 限制

为了阻止用户离开家目录，可以设置 chroot 环境。要启用此功能，请在 `/etc/vsftpd.conf` 中添加以下行：

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list

```

`chroot_list_file` 定义了被 chroot 限制的用户列表。

对于更严格的环境，请指定以下行：

```
chroot_local_user=YES

```

这将默认为所有用户启用 chroot 环境。 在这种情况下，`chroot_list_file` 定义了**不受** chroot 限制的用户列表。

### 限制用户登录

可以通过在 `/etc/vsftpd.conf` 中添加以下两行来阻止特定用户登录FTP服务器：

```
userlist_enable=YES
userlist_file=/etc/vsftpd.user_list

```

`userlist_file` 文件列出**不允许**登录的用户。

如果您只想允许特定的用户登录，请添加以下行：

```
userlist_deny=NO

```

此时 `userlist_file` 文件指定**允许**登录的用户。

### 限制连接数

可以通过在 `/etc/vsftpd.conf` 中添加如下信息来限制本地用户的数据传输速率：

```
local_max_rate=1000000 # 最大数据传输速率（单位: Bytes/秒）
max_clients=50 # 可以同时连接的最大客户端数
max_per_ip=2 # 每个 IP 允许的最大连接数

```

### 使用 xinetd

Xinetd 提供增强的监控和控制连接功能。对于基本的可以工作的 vsftpd-server 是不必要的

安装 vsftpd 将会添加必要的服务文件 `/etc/xinetd.d/vsftpd`，默认情况下，服务被禁用。

启用ftp服务：

```
service ftp
{
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/sbin/vsftpd
        log_on_success  += HOST DURATION
        log_on_failure  += HOST
        disable                 = no
}

```

如果您将 vsftpd 守护程序设置为以独立模式运行，而不是启动 vsftpd 守护程序和 [启用](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)") `xinetd.service`，请在 `/etc/vsftpd.conf` 中进行以下更改：

```
listen=NO

```

否则连接将失败：

```
500 OOPS: could not bind listening IPv4 socket

```

### 使用 SSL/TLS 来保护 FTP

首先，您需要一个 *X.509 SSL/TLS* 证书才能使用TLS。如果您没有，可以轻松生成如下的自签名证书：

```
# cd /etc/ssl/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -keyout vsftpd.pem -out vsftpd.pem
# chmod 600 vsftpd.pem

```

你会被问到关于你公司的问题，等等。由于你的证书不是一个可信任的，所填的内容并不重要，它只会被用于加密。要使用可信证书，您可以从 [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt") 这样的证书颁发机构获得证书。

然后，编辑配置文件：

 `/etc/vsftpd.conf` 
```
ssl_enable=YES

# 如果你接受匿名连接你可能要启用这个设置
# allow_anon_ssl=NO

# 默认情况下所有非匿名登录被迫使用 SSL 发送和接收密码和数据，设置为 NO，以允许不安全的连接
force_local_logins_ssl=NO
force_local_data_ssl=NO

# 选择你想要的
force_local_logins_ssl=YES

# TLS v1 协议连接是首选，默认情况下启用此模式，而禁用 SSL v2 和 v3 时，以下设置是默认设置，不需要更改，除非您特别需要 SSL
# ssl_tlsv1=YES
# ssl_sslv2=NO
# ssl_sslv3=NO
# 提供您的证书和私钥注释的路径，它们可以包含在同一个文件中或不同的文件中
rsa_cert_file=/etc/ssl/certs/vsftpd.pem
rsa_private_key_file=/etc/ssl/certs/vsftpd.pem

# 此设置默认设置为 YES，并要求所有数据连接都显示会话重用，这证明他们知道控制通道的秘密。这种方式更安全，但不受许多 FTP 客户端的支持，为了更好的兼容性而设置为 NO
require_ssl_reuse=NO
```

### 在被动模式下解析主机名

要覆盖 vsftpd 在被动模式下通过服务器的主机名发布的 IP 地址，并在启动时解析 DNS，在 `/etc/vsftpd.conf` 中增加以下两行：

```
pasv_addr_resolve=YES
pasv_address=*yourdomain.org*

```

**注意:**

*   对于动态DNS，定期更新 *pasv_address* 并重新启动服务器是不必要的，因为它有时可以被读取。
*   您可能无法通过 LAN 以被动模式连接，在这种情况下，请尝试使用主动模式而不是LAN客户端。

### 端口配置

可能需要调整默认FTP侦听端口和被动模式数据端口：

*   对于暴露于 Web 的 FTP 服务器，为了减少服务器受到攻击的可能性，可以将侦听端口改为除标准端口 21 以外的端口。
*   要限制被动模式将打开的端口，可以提供一个范围。

这些端口配置更改可以使用以下几行完成：

 `/etc/vsftpd.conf` 
```
listen_port=2211
pasv_min_port=5000
pasv_max_port=5003
```

### 配置 iptables

通常，运行FTP守护进程的服务器受 [iptables](/index.php?title=Iptables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%EF%BC%89&action=edit&redlink=1 "Iptables (简体中文） (page does not exist)") 防火墙的保护。要允许访问FTP服务器，需要打开相应的端口，如：

```
# iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 21 -j ACCEPT

```

本文不会提供有关如何设置iptables的任何说明，但这里是一个例子：[Simple stateful firewall](/index.php/Simple_stateful_firewall_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Simple stateful firewall (简体中文)")。

有一些内核模块需要在这里引用的 iptables 正确的处理 FTP 连接。 其中特别是 *nf_conntrack_ftp*。这是需要的，因为 FTP 使用给定的 *listen_port*（默认为21） 仅用于命令，所有的数据传输都是通过不同的端口完成的。这些端口由 FTP 守护程序为每个会话随机选择（也取决于是使用主动还是被动模式）。要告诉 iptables 应该接受端口上的数据包，需要 *nf_conntrack_ftp*。要在启动时自动加载，请在 `/etc/modules-load.d` 中创建新文件，例如：

```
# echo nf_conntrack_ftp > /etc/modules-load.d/nf_conntrack_ftp.conf

```

如果内核 >= 4.7，您需要通过 *sysctl* 设置 *net.netfilter.nf_conntrack_helper = 1*，如：

```
# echo net.netfilter.nf_conntrack_helper=1 > /etc/sysctl.d/70-conntrack.conf

```

或使用

```
# iptables -A PREROUTING -t raw -p tcp --dport 21 -j CT --helper ftp

```

## 小技巧

### 虚拟用户的 PAM 认证

由于 [PAM (简体中文)](/index.php/PAM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PAM (简体中文)") 不再提供 `pam_userdb.so` 另一个简单的方法是使用 [libpam_pwdfile](https://aur.archlinux.org/packages/libpam_pwdfile/)。对于具有许多用户的环境，另一个选项可能是 [pam_mysql](https://aur.archlinux.org/packages/pam_mysql/) 。但是，本节仅限于解释如何通过 `pam_pwdfile.so` 配置 chroot 环境和身份验证。

在此示例中，我们创建目录 `vsftpd`：

```
# mkdir /etc/vsftpd

```

创建和存储用户名和密码的一个选择是使用 Apache 的生成器 htpasswd：

```
# htpasswd -c /etc/vsftpd/.passwd

```

上述命令的一个问题是 vsftpd 可能无法读取生成的 MD5 散列密码。如果使用 -d 开关运行相同的命令，则使用 crypt() 加密，vsftpd 的密码变得可读，但其缺点是安全性较低，密码限制为8个字符。 Openssl 可用于使用算法1生成基于 MD5 的 BSD 密码：

```
# openssl passwd -1

```

无论那个解决方案 `/etc/vsftpd/.passwd` 应该如下所示：

```
username1:hashed_password1
username2:hashed_password2
...

```

接下来，您需要使用 `pam_pwdfile.so` 和生成的 `/etc/vsftpd/.passwd` 文件创建 PAM 服务。在本例中，我们为 *vsftpd* 创建了一个 PAM 策略，其中包含以下内容：

 `/etc/pam.d/vsftpd` 
```
auth required pam_pwdfile.so pwdfile /etc/vsftpd/.passwd
account required pam_permit.so
```

现在是为虚拟用户创建一个 home 的时候了。在示例中，决定用 `/srv/ftp` 为虚拟用户托管数据，这也反映了 Arch 的默认目录结构。首先创建 virtual 用户并使 `/srv/ftp` 成为它的 home：

```
# useradd -d /srv/ftp virtual

```

让 virtual 成为所有者

```
# chown virtual:virtual /srv/ftp

```

一个基本的没有私人文件夹配置的 /etc/vsftpd，默认的虚拟用户的 home 文件夹:

```
# 指向正确的 PAM 服务文件
pam_service_name=vsftpd
write_enable=YES
hide_ids=YES
listen=YES
connect_from_port_20=YES
anonymous_enable=NO
local_enable=YES
dirmessage_enable=YES
xferlog_enable=YES
chroot_local_user=YES
guest_enable=YES
guest_username=virtual
virtual_use_local_privs=YES

```

您自己的设置可能不需要一些参数。如果您希望 chroot 环境可写，您将需要将以下内容添加到配置文件中：

```
allow_writeable_chroot = YES

```

否则 vsftpd 的默认安全设置会抱怨，如果它检测到 chroot 是可写的。

[Start](/index.php/Start "Start") `vsftpd.service`。

您现在应该可以使用存储在 `/etc/vsftpd/.passwd` 中的任何用户和密码从FTP客户端登录。

#### 为虚拟用户创建私有目录

首先创建用户文件夹

```
# mkdir /srv/ftp/user1
# mkdir /srv/ftp/user2
# chown virtual:virtual /srv/ftp/user?/

```

随后, 在 `/etc/vsftpd.conf` 增加如下行:

```
local_root=/srv/ftp/$USER
user_sub_token=$USER

```

## 问题解决

### vsftpd: Error 500 with kernel 4.18+

[seccomp](https://en.wikipedia.org/wiki/seccomp "wikipedia:seccomp") 在 vsftpd 中默认激活，这导致某些内核版本出现兼容性问题。这已经修复了，你可以在 [RedHat Bugzilla＃845980](https://bugzilla.redhat.com/show_bug.cgi?id=845980) 中看到，但在较新的内核中仍然可能导致问题。

如果在列出目录时遇到故障，将其添加到 `/etc/vsftpd.conf`：

```
seccomp_sandbox=NO

```

### vsftpd: refusing to run with writable root inside chroot()

从 vsftpd 2.3.5 开始，用户被锁定的 chroot 目录不可写。这是为了防止安全漏洞。

允许上传的安全方法是保持 chroot 启用，并配置您的 FTP 目录。

```
local_root=/srv/ftp/user

```

```
# mkdir -p /srv/ftp/user/upload
#
# chmod 550 /srv/ftp/user
# chmod 750 /srv/ftp/user/upload

```

如果你必须这么做：

您可以将其放入您的 `/etc/vsftpd.conf` 以解决此安全性增强（自vsftpd 3.0.0；来自 [Fixing 500 OOPS: vsftpd: refusing to run with writable root inside chroot ()](http://www.benscobie.com/fixing-500-oops-vsftpd-refusing-to-run-with-writable-root-inside-chroot/))：

```
allow_writeable_chroot=YES

```

或者：

安装 [vsftpd-ext](https://aur.archlinux.org/packages/vsftpd-ext/)  并在 conf 文件中设置

```
allow_writable_chroot=YES

```

### FileZilla Client: GnuTLS error -8 -15 -110 when connecting via SSL

vsftpd 尝试在 SSL 会话中显示纯文本错误消息。为了进行调试，暂时禁用加密，您将看到正确的错误消息。[[1]](http://ramblings.linkerror.com/?p=45) [[2]](https://serverfault.com/questions/772494/vsftpd-list-causes-gnutls-error-15)

### vsftpd.service fails to run on boot

如果您启用了 `vsftpd.service`，并且无法在启动时运行，请确保它已在服务文件中设置为在 `network.target` 之后加载：

 `/usr/lib/systemd/system/vsftpd.service` 
```
[Unit]
Description=vsftpd daemon
After=network.target
```

### Passive mode replies with the local IP address to a remote connection

如果 vsftpd 将本地地址返回给远程连接，如：

```
227 Entering Passive Mode (192,168,0,19,192,27).

```

It may be that the FTP server is behind a NAT router and while some devices monitor FTP connections and dynamically replace the IP address specification for packets containing the PASV response, some do not. 可能是 FTP 服务器位于 NAT 路由器后面，而有些设备会监视 FTP 连接并动态替换包含 PASV 响应的数据包的 IP 地址规范，但有些设备却不会。

使用以下命令在 vsftpd 配置中指示外部IP地址：

```
 pasv_address=*externalIPaddress*

```

或者可选地：

```
pasv_addr_resolve=YES
pasv_address=*my.domain.name*

```

如果在更改后无法进行内部连接，则可能需要运行 2 个 vsftpd，一个用于内部连接，一个用于外部连接。

**提示：** 要找出 NAT 路由器是否拦截 PASV 响应并用外部 IP 替换内部 IP，可以在 TLS 模式下检查客户端的服务器响应。加密的数据包不能被路由器识别并且未被修改。

### ipv6 only fails with: 500 OOPS: run two copies of vsftpd for IPv4 and IPv6

你很有可能已经注释了这一行

```
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
#listen=YES
#
# This directive enables listening on IPv6 sockets. To listen on IPv4 and IPv6
# sockets, you must run two copies of vsftpd with two configuration files.
# Make sure, that one of the listen options is commented !!
listen_ipv6=YES

```

而不是设置

```
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
listen=NO

```

### vsftpd 连接在使用 nis 的机器上失败: yp_bind_client_create_v2: RPC: Unable to send

as mentioned on the vsftpd faq page, "...built-in sandboxing uses network isolation on Linux. This may be interfering with any module that needs to use the network to perform operations or lookups" 正如在 vsftpd fap 页面上提到的那样，“...内置沙盒使用 linux 上的网络隔离可能会干扰任何需要使用网络执行操作或查找的模块”

将这个未公开的行添加到你的 `/etc/vsftpd.conf`

```
isolate_network=NO

```

## 更多资源

*   [vsftpd official homepage](http://vsftpd.beasts.org/)
*   [vsftpd.conf man page](http://vsftpd.beasts.org/vsftpd_conf.html)
*   [vsftpd FAQ](https://security.appspot.com/vsftpd/FAQ.txt)