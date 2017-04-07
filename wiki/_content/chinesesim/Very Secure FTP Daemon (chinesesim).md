**vsftpd** (Very Secure FTP Daemon) 是一个为UNIX类系统开发的轻量,稳定和安全的FTP服务器端.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 允许上传](#.E5.85.81.E8.AE.B8.E4.B8.8A.E4.BC.A0)
    *   [2.2 本地用户登录](#.E6.9C.AC.E5.9C.B0.E7.94.A8.E6.88.B7.E7.99.BB.E5.BD.95)
    *   [2.3 匿名用户登录](#.E5.8C.BF.E5.90.8D.E7.94.A8.E6.88.B7.E7.99.BB.E5.BD.95)
    *   [2.4 Chroot 限制](#Chroot_.E9.99.90.E5.88.B6)
    *   [2.5 限制用户登录](#.E9.99.90.E5.88.B6.E7.94.A8.E6.88.B7.E7.99.BB.E5.BD.95)
    *   [2.6 限制连接数](#.E9.99.90.E5.88.B6.E8.BF.9E.E6.8E.A5.E6.95.B0)
    *   [2.7 使用 xinetd](#.E4.BD.BF.E7.94.A8_xinetd)
    *   [2.8 使用 SSL 使 FTP 安全](#.E4.BD.BF.E7.94.A8_SSL_.E4.BD.BF_FTP_.E5.AE.89.E5.85.A8)
    *   [2.9 动态 DNS](#.E5.8A.A8.E6.80.81_DNS)
    *   [2.10 Port configurations](#Port_configurations)
    *   [2.11 Configuring iptables](#Configuring_iptables)
*   [3 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [3.1 虚拟用户的PAM认证](#.E8.99.9A.E6.8B.9F.E7.94.A8.E6.88.B7.E7.9A.84PAM.E8.AE.A4.E8.AF.81)
        *   [3.1.1 为虚拟用户创建私有目录](#.E4.B8.BA.E8.99.9A.E6.8B.9F.E7.94.A8.E6.88.B7.E5.88.9B.E5.BB.BA.E7.A7.81.E6.9C.89.E7.9B.AE.E5.BD.95)
*   [4 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [4.1 vsftpd: no connection (Error 500) with recent kernels (3.5 and newer) and .service](#vsftpd:_no_connection_.28Error_500.29_with_recent_kernels_.283.5_and_newer.29_and_.service)
    *   [4.2 vsftpd: refusing to run with writable root inside chroot()](#vsftpd:_refusing_to_run_with_writable_root_inside_chroot.28.29)
    *   [4.3 FileZilla Client: GnuTLS error -8 -15 -110 when connecting via SSL](#FileZilla_Client:_GnuTLS_error_-8_-15_-110_when_connecting_via_SSL)
    *   [4.4 vsftpd.service fails to run on boot](#vsftpd.service_fails_to_run_on_boot)
    *   [4.5 ipv6 only fails with: 500 OOPS: run two copies of vsftpd for IPv4 and IPv6](#ipv6_only_fails_with:_500_OOPS:_run_two_copies_of_vsftpd_for_IPv4_and_IPv6)
*   [5 更多资源](#.E6.9B.B4.E5.A4.9A.E8.B5.84.E6.BA.90)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [vsftpd](https://www.archlinux.org/packages/?name=vsftpd).

[启动/启用](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") `vsftpd.service` 守护程序。

有关通过 xinetd 使用 vsftpd 的过程，请参阅 [#使用 xinetd](#.E4.BD.BF.E7.94.A8_xinetd)。

## 配置

vsftpd 的大多数配置都可以通过编辑 `/etc/vsftpd.conf` 文件实现。 该文件本身自带大量注释说明，所以这一章节只就一些重要的配置予以说明。 有关所有可用选项和文档，请参阅 vsftpd.conf(5) 或 [在线查看](https://security.appspot.com/vsftpd/vsftpd_conf.html) 手册页。默认情况下，由 `/srv/ftp` 提供文件。

允许的连接 `/etc/hosts.allow`：

```
# 允许所有连接
vsftpd: ALL
# IP地址范围
vsftpd: 10.0.0.0/255.255.255.0

```

### 允许上传

需要将 `/etc/vsftpd.conf` 中的 `write_enable` 值设为YES，以便允许修改文件系统（如上传）:

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
# 允许匿名FTP？ （当心 - 默认情况下允许除非您将其注释）。
anonymous_enable=YES
...
# 取消注释以允许匿名FTP用户上传文件。
# 只有上述全局写入被激活，才会有效果。
# 另外，你显然需要创建FTP用户有写权限的目录。
# anon_upload_enable=YES
#
# 如果您希望匿名FTP用户能够创建新目录，请取消注释。
# anon_mkdir_write_enable=YES
...
```

您也可以添加以下选项（详见 `man vsftpd.conf`）：

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

Xinetd提供增强的监控和控制连接功能。It is not necessary though for a basic good working vsftpd-server.

安装 vsftpd 将会添加必要的服务文件 `/etc/xinetd.d/vsftpd`， 默认情况下，服务被禁用。

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

如果您将vsftpd守护程序设置为以独立模式运行，而不是启动 vsftpd 守护程序和 [enable](/index.php/Enable "Enable") `xinetd.service`，请在 `/etc/vsftpd.conf` 中进行以下更改：

```
listen=NO

```

否则连接将失败：

```
500 OOPS: could not bind listening IPv4 socket

```

### 使用 SSL 使 FTP 安全

生成一个SSL证书，如这样：

```
# cd /etc/ssl/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -keyout /etc/ssl/certs/vsftpd.pem -out /etc/ssl/certs/vsftpd.pem
# chmod 600 /etc/ssl/certs/vsftpd.pem

```

您将被询问有关您公司等的许多问题，如果您的证书是不需要信任的，那么您填写的内容并不重要。但是您将使用这些内容加密！如果您计划在使用此功能方面取得信任，则可以从 CA 如 thawte,verisign 获得一个。

编辑您的配置 `/etc/vsftpd.conf`

```
#这个很重要
ssl_enable=YES

#选择你想要的
# 如果你接受 anon-connections 你可能要启用这个
# allow_anon_ssl=NO

#选择你想要的
# 我猜这是一个性能上的问题
# force_local_data_ssl=NO

#选择你想要的
force_local_logins_ssl=YES

#你至少应该启用这个如果你启用 ssl...
ssl_tlsv1=YES
#选择你想要的
ssl_sslv2=YES
#选择你想要的
ssl_sslv3=YES
#给出您当前生成的 *.pem 文件的正确路径
rsa_cert_file=/etc/ssl/certs/vsftpd.pem
# *.pem 文件包含密钥和证书
rsa_private_key_file=/etc/ssl/certs/vsftpd.pem

```

### 动态 DNS

确保在 `/etc/vsftpd.conf` 中放入以下两行：

```
pasv_addr_resolve=YES
pasv_address=yourdomain.noip.info

```

定期更新 pasv_address 并重新启动服务器的脚本是**不必要**的，因为它可以在别处被找到！

**注意:** 您将无法通过 LAN 连接到被动模式。尝试在局域网 PC 的 FTP 客户端上的活动模式。

### Port configurations

Especially for private FTP servers that are exposed to the web it's recommended to change the listening port to something other than the standard port 21\. This can be done using the following lines in `/etc/vsftpd.conf`:

```
listen_port=2211

```

Furthermore a custom passive port range can be given by:

```
pasv_min_port=49152
pasv_max_port=65534

```

### Configuring iptables

Often the server running the FTP daemon is protected by an [iptables](/index.php/Iptables "Iptables") firewall. To allow access to the FTP server the corresponding port needs to be opened using something like

```
# iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 21 -j ACCEPT

```

This article won't provide any instruction on how to set up iptables but here is an example: [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall").

There are some kernel modules needed for proper FTP connection handling by iptables that should be referenced here. Among those especially *nf_conntrack_ftp*. It is needed as FTP uses the given *listen_port* (21 by default) for commands only; all the data transfer is done over different ports. These ports are chosen by the FTP daemon at random and for each session (also depending on whether active or passive mode is used). To tell iptables that packets on ports should be accepted, *nf_conntrack_ftp* is required. To load it automatically on boot create a new file in `/etc/modules-load.d` e.g.:

```
# echo nf_conntrack_ftp > /etc/modules-load.d/nf_conntrack_ftp.conf

```

If the kernel >= 4.7 you either need to set *net.netfilter.nf_conntrack_helper=1* via *sysctl* e.g.

```
# echo net.netfilter.nf_conntrack_helper=1 > /etc/sysctl.d/70-conntrack.conf

```

or use

```
# iptables -A PREROUTING -t raw -p tcp --dport 21 -j CT --helper ftp

```

## 小技巧

### 虚拟用户的PAM认证

Since [PAM](/index.php/PAM "PAM") no longer provides `pam_userdb.so` another easy method is to use [libpam_pwdfile](https://aur.archlinux.org/packages/libpam_pwdfile/). For environments with many users another option could be [pam_mysql](https://aur.archlinux.org/packages/pam_mysql/). This section is however limited to explain how to configure a chroot environment and authentication by `pam_pwdfile.so`.

In this example we create the directory `vsftpd`:

```
# mkdir /etc/vsftpd

```

One option to create and store user names and passwords is to use the Apache generator htpasswd:

```
# htpasswd -c /etc/vsftpd/.passwd

```

A problem with the above command is that vsftpd might not be able to read the generated MD5 hashed password. If running the same command with the -d switch, crypt() encryption, password become readable by vsftpd, but the downside of this is less security and a password limited to 8 characters. Openssl could be used to produce a MD5 based BSD password with algorithm 1:

```
# openssl passwd -1

```

Whatever solution the produced `/etc/vsftpd/.passwd` should look like this:

```
username1:hashed_password1
username2:hashed_password2
...

```

Next you need to create a PAM service using `pam_pwdfile.so` and the generated `/etc/vsftpd/.passwd` file. In this example we create a PAM policy for *vsftpd* with the following content:

 `/etc/pam.d/vsftpd` 
```
auth required pam_pwdfile.so pwdfile /etc/vsftpd/.passwd
account required pam_permit.so
```

Now it is time to create a home for the virtual users. In the example `/srv/ftp` is decided to host data for virtual users, which also reflects the default directory structure of Arch. First create the general user virtual and make `/srv/ftp` its home:

```
# useradd -d /srv/ftp virtual

```

Make virtual the owner:

```
# chown virtual:virtual /srv/ftp

```

A basic `/etc/vsftpd.conf` with no private folders configured, which will default to the home folder of the virtual user:

```
# pointing to the correct PAM service file
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

Some parameters might not be necessary for your own setup. If you want the chroot environment to be writable you will need to add the following to the configuration file:

```
allow_writeable_chroot=YES

```

Otherwise vsftpd because of default security settings will complain if it detects that chroot is writable.

[Start](/index.php/Start "Start") `vsftpd.service`.

You should now be able to login from a ftp-client with any of the users and passwords stored in `/etc/vsftpd/.passwd`.

#### 为虚拟用户创建私有目录

首先创建用户文件夹

```
# mkdir /srv/ftp/user1
# mkdir /srv/ftp/user2
# chown virtual:virtual /srv/ftp/user?/

```

随后, 在`/etc/vsftpd.conf`增加如下行:

```
local_root=/srv/ftp/$USER
user_sub_token=$USER

```

## 问题解决

### vsftpd: no connection (Error 500) with recent kernels (3.5 and newer) and .service

add this to your /etc/vsftpd.conf

```
seccomp_sandbox=NO

```

### vsftpd: refusing to run with writable root inside chroot()

As of vsftpd 2.3.5, the chroot directory that users are locked to must not be writable. This is in order to prevent a security vulnerabilty.

The safe way to allow upload is to keep chroot enabled, and configure your FTP directories.

```
local_root=/srv/ftp/user

```

```
# mkdir -p /srv/ftp/user/upload
#
# chmod 550 /srv/ftp/user
# chmod 750 /srv/ftp/user/upload

```

If you must:

You can put this into your `/etc/vsftpd.conf` to workaround this security enhancement (since vsftpd 3.0.0; from [Fixing 500 OOPS: vsftpd: refusing to run with writable root inside chroot ()](http://www.benscobie.com/fixing-500-oops-vsftpd-refusing-to-run-with-writable-root-inside-chroot/)):

```
allow_writeable_chroot=YES

```

or alternative:

Install [vsftpd-ext](https://aur.archlinux.org/packages/vsftpd-ext/) and set in the conf file allow_writable_root=YES

### FileZilla Client: GnuTLS error -8 -15 -110 when connecting via SSL

vsftpd tries to display plain-text error messages in the SSL session. In order to debug this, temporarily disable encryption and you will see the correct error message.[[1]](http://ramblings.linkerror.com/?p=45) [[2]](https://serverfault.com/questions/772494/vsftpd-list-causes-gnutls-error-15)

### vsftpd.service fails to run on boot

If you have enabled the vsftpd service and it fails to run on boot, make sure it is set to load after network.target in the service file:

 `/usr/lib/systemd/system/vsftpd.service` 
```
[Unit]
Description=vsftpd daemon
After=network.target
```

### ipv6 only fails with: 500 OOPS: run two copies of vsftpd for IPv4 and IPv6

you most likely have commented out the line

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

instead of setting

```
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
listen=NO

```

## 更多资源

*   [vsftpd official homepage](http://vsftpd.beasts.org/)
*   [vsftpd.conf man page](http://vsftpd.beasts.org/vsftpd_conf.html)