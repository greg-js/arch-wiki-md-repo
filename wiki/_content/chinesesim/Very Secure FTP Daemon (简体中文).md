**vsftpd** (Very Secure FTP Daemon) 是一个为UNIX类系统开发的轻量,稳定和安全的FTP服务器端.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 允许上传](#.E5.85.81.E8.AE.B8.E4.B8.8A.E4.BC.A0)
    *   [2.2 本地用户登录](#.E6.9C.AC.E5.9C.B0.E7.94.A8.E6.88.B7.E7.99.BB.E5.BD.95)
    *   [2.3 匿名用户登录](#.E5.8C.BF.E5.90.8D.E7.94.A8.E6.88.B7.E7.99.BB.E5.BD.95)
    *   [2.4 Chroot限制](#Chroot.E9.99.90.E5.88.B6)
    *   [2.5 限制用户登录](#.E9.99.90.E5.88.B6.E7.94.A8.E6.88.B7.E7.99.BB.E5.BD.95)
    *   [2.6 限制连接数](#.E9.99.90.E5.88.B6.E8.BF.9E.E6.8E.A5.E6.95.B0)
    *   [2.7 使用xinetd](#.E4.BD.BF.E7.94.A8xinetd)
*   [3 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [3.1 虚拟用户的PAM认证](#.E8.99.9A.E6.8B.9F.E7.94.A8.E6.88.B7.E7.9A.84PAM.E8.AE.A4.E8.AF.81)
        *   [3.1.1 为虚拟用户创建私有目录](#.E4.B8.BA.E8.99.9A.E6.8B.9F.E7.94.A8.E6.88.B7.E5.88.9B.E5.BB.BA.E7.A7.81.E6.9C.89.E7.9B.AE.E5.BD.95)
*   [4 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [4.1 vsftpd: refusing to run with writable root inside chroot()](#vsftpd:_refusing_to_run_with_writable_root_inside_chroot.28.29)
*   [5 更多资源](#.E6.9B.B4.E5.A4.9A.E8.B5.84.E6.BA.90)

## 安装

Vsftpd包含在官方软件库中, 可以通过pacman轻松安装

```
# pacman -S vsftpd

```

修改 `/etc/hosts.allow` 可以限制vsftp的允许连接:

```
# 允许所有连接
vsftpd: ALL
# 只允许固定IP范围用户登录
vsftpd: 10.0.0.0/255.255.255.0

```

服务器可以通过如下脚本启动:

```
# systemctl start vsftpd.service

```

让vsftpd随系统自动启动：

```
# systemctl enable vsftpd.service

```

## 配置

vsftpd的大多数配置都可以通过编辑`/etc/vsftpd.conf`文件实现. 这个文件自身有大量注释说明, 所以这一章节只就一些重要的配置予以说明. 如果要了解所有的选顶和文档, 请使用man vsftpd.conf (5).

### 允许上传

必需将`/etc/vsftpd.conf`中的`write_enable`值设为YES, 以便允许修改系统, 比如上传:

```
write_enable=YES

```

### 本地用户登录

可以修改`/etc/vsftpd.conf`中的如下值, 以便允许`/etc/passwd`中的用户登录:

```
local_enable=YES

```

### 匿名用户登录

`/etc/vsftpd.conf`如下行控制着匿名用户登录:

```
anonymous_enable=YES # 允许匿名用户登录
no_anon_password=YES # 匿名用户登录不再需要密码
anon_max_rate=30000  # 每个匿名用户最大下载速度(单位:字节每秒)

```

### Chroot限制

为了阻止用户离开家目录, 可以设置chroot环境. 在`/etc/vsftpd.conf`添加如下行实现:

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list

```

`chroot_list_file` 定义了可通过chroot限制的用户列表.

如果要设置更严格的chroot环境, 可以按如下方式设置:

```
chroot_local_user=YES

```

默认为所有用户启用chroot环境, 此时`chroot_list_file` 定义了不使用chroot的用户列表.

### 限制用户登录

在`/etc/vsftpd.conf`添加如下二行:

```
userlist_enable=YES
userlist_file=/etc/vsftpd.user_list

```

`userlist_file` 列出了不允许登录的用户.

如果你只想要允许特定的用户登录, 添加这一行:

```
userlist_deny=NO

```

此时`userlist_file` 列出的就是允许登录的用户.

### 限制连接数

可以为本地用户设定数据传输数率, 最大客户端数以及每个IP的连接数目, 在`/etc/vsftpd.conf`添加如下行:

```
local_max_rate=1000000 # 最大数据传输速率(单位:字节每秒)
max_clients=50         # 同时在线的最大客户端数目
max_per_ip=2           # 每个IP允许的连接数

```

### 使用xinetd

如果要启用xinetd引导vsftpd,创建`/etc/xinetd.d/vsftpd`文件, 并加入如下内容:

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

并启用`/etc/vsftpd.conf`中的如下选顶:

```
pam_service_name=ftp

```

最后, 把xinetd加入`/etc/rc.conf`守护程序列表, 此时不再需要再添加vsftpd,因为它将由xinetd调用:

如果连接服务器时获得如下错误信息:

```
500 OOPS: cap_set_proc

```

你需要在`/etc/rc.conf`的 MODULES= 一行添加*capability*

升级到2.1.0版本后, 连接服务器时可能会出现如下错误:

```
500 OOPS: could not bind listening IPv4 socket

```

在先前的版本中, 将下述行注释掉就足够了:

```
# Use this to use vsftpd in standalone mode, otherwise it runs through (x)inetd
# listen=YES

```

但在新版本以及未来的版本中, 必须显示的指定守护程序启动方式:

```
# Use this to use vsftpd in standalone mode, otherwise it runs through (x)inetd
listen=NO

```

## 小技巧

### 虚拟用户的PAM认证

使用虚拟用户的最大好处是不需要在系统中创建太多的真实用户, 将整个环境限制在某个固定容器中可以提供更高的安全性.

一个虚拟用户数据库可以通过如下的简单文本开始创建:

```
user1
password1
user2
password2

```

它包含了想启用的所有虚拟用户. 将其保存为logins.txt; 这个文件名并没有什么特别的含义. 下一步需要伯克利数据工具, 它被包含在arch的核心系统中. 执行如下命令生成数据库:

```
# db_load -T -t hash -f logins.txt /etc/vsftpd_login.db

```

强列建议把`vsftpd_login.db`文件赋予更严格的权限:

```
# chmod 600 /etc/vsftpd_login.db

```

**警告:** 在明文中列出密码是不安全的. 不要忘记删除临时文件, `rm logins.txt`.

令PAM使用vsftpd_login.db数据库.在`/etc/pam.d/`中创建文件ftp,并加入如下内容:

```
auth required pam_userdb.so db=/etc/vsftpd_login crypt=hash 
account required pam_userdb.so db=/etc/vsftpd_login crypt=hash

```

**注意:** /etc/vsftpd_login不包启.db后缀名

现在要为虚拟用户创建家目录,在这个例子中即为`/srv/ftp`. 首先创建一个真实用户virtual, 并将`/srv/ftp`设为它的家目录:

```
# useradd -d /srv/ftp virtual
# chown virtual:virtual /srv/ftp

```

修改/etc/vsftpd.conf, 并加入如下行. 它将所有的虚拟用户都映射为virtual, 并将之都限制在`/srv/ftp`中:

```
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
guest_enable=YES
guest_username=virtual
virtual_use_local_privs=YES

```

如果通过xinetd方法启动vsftpd服务.现在将只允许数据库中列出的用户登录.

#### 为虚拟用户创建私有目录

首先创建文件夹,并把所有者设为virtual用户

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

### vsftpd: refusing to run with writable root inside chroot()

为了避免一个安全漏洞，从 vsftpd 2.3.5 开始，chroot 目录必须不可写。使用命令：

```
# chmod a-w /home/user

```

对于虚拟用户，使用命令：

```
# chmod a-w /srv/ftp/user1

```

## 更多资源

*   [vsftpd official homepage](http://vsftpd.beasts.org/)
*   [vsftpd.conf man page](http://vsftpd.beasts.org/vsftpd_conf.html)