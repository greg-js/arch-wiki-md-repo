Related articles

*   [Security](/index.php/Security "Security")
*   [pam_mount](/index.php/Pam_mount "Pam mount")
*   [pam_usb](/index.php/Pam_usb "Pam usb")
*   [pam_abl](/index.php/Pam_abl "Pam abl")
*   [pam_oath](/index.php/Pam_oath "Pam oath")

**翻译状态：** 本文是英文页面 [PAM](/index.php/PAM "PAM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-14，点击[这里](https://wiki.archlinux.org/index.php?title=PAM&diff=0&oldid=436909)可以查看翻译后英文页面的改动。

Linux PAM( Pluggable Authentication Modules ) 提供了一个框架，用于进行系统级的用户认证。如下描述引用自 [[1]](http://www.linux-pam.org/whatispam.html):

	PAM provides a way to develop programs that are independent of authentication scheme. These programs need "authentication modules" to be attached to them at run-time in order to work. Which authentication module is to be attached is dependent upon the local system setup and is at the discretion of the local system administrator. （ PAM 可以使程序开发与认证方式细节分离，而是在程序运行时调用“认证”模型完成工作。认证模型可以由本地系统管理员通过配置进行选择）

本文描述在 Arch Linux 下为本地和远端用户配置 PAM 权限的方式方法。具体的细节配置方法将在专门的文章内展开。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 安全性参数](#.E5.AE.89.E5.85.A8.E6.80.A7.E5.8F.82.E6.95.B0)
    *   [2.2 PAM 基础配置](#PAM_.E5.9F.BA.E7.A1.80.E9.85.8D.E7.BD.AE)
        *   [2.2.1 示例](#.E7.A4.BA.E4.BE.8B)
*   [3 配置方法](#.E9.85.8D.E7.BD.AE.E6.96.B9.E6.B3.95)
    *   [3.1 安全性参数配置](#.E5.AE.89.E5.85.A8.E6.80.A7.E5.8F.82.E6.95.B0.E9.85.8D.E7.BD.AE)
    *   [3.2 PAM stack and module configuration](#PAM_stack_and_module_configuration)
*   [4 更多 PAM 包](#.E6.9B.B4.E5.A4.9A_PAM_.E5.8C.85)
*   [5 相关资源](#.E7.9B.B8.E5.85.B3.E8.B5.84.E6.BA.90)

## 安装

[pam](https://www.archlinux.org/packages/?name=pam) 包是基础安装包，默认已经安装在系统。PAM 模块被放置于 `/usr/lib/security` 目录

软件源中另外还包括其它一些可选的 PAM 包，详见 [#配置方法](#.E9.85.8D.E7.BD.AE.E6.96.B9.E6.B3.95)

## 配置

`/etc` 目录有多个子目录与 PAM 相关，使用命令 `pacman -Ql pam | grep /etc` 查看默认创建的配置文件。这些配置与 [#安全性参数](#.E5.AE.89.E5.85.A8.E6.80.A7.E5.8F.82.E6.95.B0)或 [#PAM 基础配置](#PAM_.E5.9F.BA.E7.A1.80.E9.85.8D.E7.BD.AE) 有关。

### 安全性参数

`/etc/security` 包含了对认证方法参数的系统级配置，安装后的文件与软件开发方默认配置一致。

注意 Arch Linux 没有对这些文件进行定制。例如 `/etc/security/pwquality.conf` 配置可用于系统级别默认的密码认证方式，但需要手动将 `pam_pwquality.so` 模块加入到 [#PAM 基础配置](#PAM_.E5.9F.BA.E7.A1.80.E9.85.8D.E7.BD.AE) 内。

详见 [#安全性参数配置](#.E5.AE.89.E5.85.A8.E6.80.A7.E5.8F.82.E6.95.B0.E9.85.8D.E7.BD.AE)。

### PAM 基础配置

`/etc/pam.d/` 目录专门用于存放 PAM 配置，用于为具体的应用程序设置独立的认证方式。配置文件由以下安装包提供：

*   [pambase](https://www.archlinux.org/packages/?name=pambase) 安装包，提供了 Arch Linux 中为应用程序使用的 PAM 基础配置文件
*   其它基础安装包。例如 [util-linux](https://www.archlinux.org/packages/?name=util-linux) 添加了为 *login* 及其它一些应用的认证配置， [shadow](https://www.archlinux.org/packages/?name=shadow) 安装包为 Archlinux 提供默认的用户数据库认证方式（参见[Users and groups](/index.php/Users_and_groups "Users and groups")）

不同的安装包的配置文件都被放在该目录，在运行时被不同的应用程序加载。例如，在用户登录时，*login*程序将加载 `system-local-login` 策略，具体过程如下：

 `/etc/pam.d/`  `login -> system-local-login -> system-login -> system-auth` 

不同的应用程序，可能使用不同的配置文件。例如，[openssh](https://www.archlinux.org/packages/?name=openssh) 安装其 `sshd` PAM 策略，如下所示：

 `/etc/pam.d/`  `sshd -> system-remote-login -> system-login -> system-auth` 

配置文件的选择与应用程序有关。一种特定的认证方式可能仅用到 `sshd`，远程登录用到 `system-remote-login`，对这两者的修改不用影响到本地登录（local logins）。而对 `system-login` 或 `system-auth` 的修改将同时对 local 和 remote 的登录产生影响。

如 `sshd` 的例子，任何 **pam-aware** 的应用程序需要将它的认证策略安装到 `/etc/pam.d` 目录下，以更集成和使用 PAM 提供的功能。否则应用程序将使用默认配置 `/etc/pam.d/other`。

**Tip:** PAM 是在运行过程中被动态链接使用的，例如 `$ ldd /usr/bin/login |grep pam` 
```
libpam.so.0 => /usr/lib/libpam.so.0 (0x000003d8c32d6000)
libpam_misc.so.0 => /usr/lib/libpam_misc.so.0 (0x000003d8c30d2000)
```
*login* 程序是 pam-aware 的，因此 **必需** 指定一个认证策略。

PAM 手册 *pam(8)* 和 *pam.d(5)* 描述了配置文件的标准规范。手册分四部分：账户，认证，密码和会话管理，同时还包括了配置项的可选内容。

此外，文档 `/usr/share/doc/Linux-PAM/index.html` 包含多种指导文档，包括了每种标准模块的 man 手册。

**Warning:** 对 PAM 配置的修改会影响用户认证。不正确的修改可能导致**所有用户都无法登录**错误。已经登录用户还可以继续操作，因此习惯上对 PAM 作操作时使用一个用户修改，另一个账号在另一个终端来测试认证情况

#### 示例

下所的两个小例子用于**反面示例**:

首先是下面两行配置：

 `/etc/pam.d/system-auth` 
```
auth      required  pam_unix.so     try_first_pass nullok
auth      optional  pam_permit.so
```

[pam_unix(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pam_unix.8) 说明如下：“本认证 （ `pam_unix.so` ）用于检查用户密码作为认证。默认情况不允许密码为空的用户进入”。而 `pam_permit.so` 允许密码为空的情况。如果将 `rerquired` 和 `optional` 交换位置，则两种情况都将允许无密码登录。

第二种情况恰好相反，默认情况下创建如下的文件：

```
# touch /etc/nologin

```

将导致只有 root 用户可以登录（Arch Linux 默认允许 root 用户登录）。要让普通用户可以登录，则需要删除该文件。

参考 [#PAM stack and module configuration](#PAM_stack_and_module_configuration)来对具体使用进行配置。

## 配置方法

本节简要说明如何修改 PAM 配置，如何添加新的 PAM 模块。具体的模块 man 手册与模块名一致（去掉 `.so` 后缀）

### 安全性参数配置

下面的章节描述如何修改 PAM 默认参数配置：

*   [Security#Enforcing strong passwords using pam_cracklib](/index.php/Security#Enforcing_strong_passwords_using_pam_cracklib "Security")

	展示如何使用 `pam_crackib.so` 强制密码认证

*   [Security#Lockout user after three failed login attempts](/index.php/Security#Lockout_user_after_three_failed_login_attempts "Security")

	展示如何使用 `pam_tally.so` 限制登录

*   [Security#Allow only certain users](/index.php/Security#Allow_only_certain_users "Security")

	展示使用 `pam_wheel.so` 限制用户登录

*   [Realtime process management#Configuring PAM](/index.php/Realtime_process_management#Configuring_PAM "Realtime process management") and [Security#Limit amount of processes](/index.php/Security#Limit_amount_of_processes "Security")

	描述如何使用 `pam_limits.so` 来配置系统进程

### PAM stack and module configuration

下面的章节说明对于具体的模块，如何修改 [#PAM 基础配置](#PAM_.E5.9F.BA.E7.A1.80.E9.85.8D.E7.BD.AE)

[Official repositories](/index.php/Official_repositories "Official repositories") PAM 模块:

*   [pam_mount](/index.php/Pam_mount "Pam mount")

	`pam_mount.so` 在用户登录时自动挂载加密目录

*   [ECryptfs#Auto-mounting](/index.php/ECryptfs#Auto-mounting "ECryptfs")

	`pam_ecryptfs.so` 自动挂载加密目录

*   [Dm-crypt/Mounting at login#PAM configuration](/index.php/Dm-crypt/Mounting_at_login#PAM_configuration "Dm-crypt/Mounting at login")

	`pam_exec.so` 在用户登录时执行自定义脚本

*   [Active Directory Integration#Configuring PAM](/index.php/Active_Directory_Integration#Configuring_PAM "Active Directory Integration")

	使用 `pam_winbind.so` 和 `pam_krb5.so` 通过 Active Directory (LDAP, Kerberos 服务) 进行用户认证

*   [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication") with its [LDAP authentication#NSS and PAM](/index.php/LDAP_authentication#NSS_and_PAM "LDAP authentication") section

	`pam_ldap.so` 介绍集成 LDAP 主对端认证过程

*   [Yubikey#Two-factor authentication with SSH](/index.php/Yubikey#Two-factor_authentication_with_SSH "Yubikey")

	`pam_yubico.so` 通过私有的 Yubikey 进行认证

*   [pam_oath](/index.php/Pam_oath "Pam oath")

	`pam_oath.so` 软件方式的 two-factor 认证

来自于 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 的 PAM 模块:

*   [pam_usb](/index.php/Pam_usb "Pam usb")

	`pam_usb.so` 通过 USB 设备进行认证

*   [SSH keys#pam_ssh](/index.php/SSH_keys#pam_ssh "SSH keys")

	`pam_ssh.so` 认证远端用户

*   [pam_abl](/index.php/Pam_abl "Pam abl")

	`pam_abl.so` 限制通过 ssh 的暴力攻击

*   [EncFS](/index.php/EncFS#.2Fetc.2Fpam.d.2F "EncFS")

	`pam_encfs.so` 实现自动挂载加密目录

*   [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator")

	`pam_google_authenticator.so` two-factor 认证

*   [Very Secure FTP Daemon#PAM with virtual users](/index.php/Very_Secure_FTP_Daemon#PAM_with_virtual_users "Very Secure FTP Daemon")

	`pam_pwdfile.so` 认证非本地用户的 FTP 登录和 chroot 限制

## 更多 PAM 包

除了上面提到的安装包，[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 包括更多的 PAM 模块和工具。

PAM 相关的通用工具有：

*   **[libx32_pam](https://github.com/ArchLinux-x32/libx32-pam)** — Arch Linux PAM x32 ABI library

	[http://linux-pam.org/](http://linux-pam.org/) || [libx32-pam](https://aur.archlinux.org/packages/libx32-pam/)

*   **[Pamtester](http://linux.die.net/man/1/pamtester)** — PAM 测试工具集

	[http://pamtester.sourceforge.net/](http://pamtester.sourceforge.net/) || [pamtester](https://aur.archlinux.org/packages/pamtester/)

Note the AUR features a keyword tag for [PAM](https://aur.archlinux.org/packages/?O=0&SeB=k&K=pam&outdated=off&SB=p&SO=d&PP=50&do_Search=Go), but not all available packages are updated to include it. Hence, searching the [package description](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=pam&outdated=off&SB=p&SO=d&PP=50&do_Search=Go) may be necessary.

## 相关资源

*   [linux-pam.org](http://www.linux-pam.org/) - The project homepage
*   [Understanding and configuring PAM](https://www.ibm.com/developerworks/linux/library/l-pam/index.html) - An introductory article