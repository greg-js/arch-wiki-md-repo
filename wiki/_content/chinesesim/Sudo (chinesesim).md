**翻译状态：** 本文是英文页面 [Sudo](/index.php/Sudo "Sudo") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-01-31，点击[这里](https://wiki.archlinux.org/index.php?title=Sudo&diff=0&oldid=358889)可以查看翻译后英文页面的改动。

[sudo](http://www.gratisoft.us/sudo/)(substitute user do) 使得系统管理员可以授权特定用户或用户组作为 root 或他用户执行某些（或所有）命令，同时还能够对命令及其参数提供审核跟踪。

## Contents

*   [1 合理性](#.E5.90.88.E7.90.86.E6.80.A7)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 查看当前设置](#.E6.9F.A5.E7.9C.8B.E5.BD.93.E5.89.8D.E8.AE.BE.E7.BD.AE)
    *   [4.2 使用 visudo](#.E4.BD.BF.E7.94.A8_visudo)
    *   [4.3 设置示例](#.E8.AE.BE.E7.BD.AE.E7.A4.BA.E4.BE.8B)
    *   [4.4 sudoers文件默认权限](#sudoers.E6.96.87.E4.BB.B6.E9.BB.98.E8.AE.A4.E6.9D.83.E9.99.90)
    *   [4.5 密码过期时间](#.E5.AF.86.E7.A0.81.E8.BF.87.E6.9C.9F.E6.97.B6.E9.97.B4)
*   [5 使用技巧](#.E4.BD.BF.E7.94.A8.E6.8A.80.E5.B7.A7)
    *   [5.1 sudoers 范例](#sudoers_.E8.8C.83.E4.BE.8B)
    *   [5.2 bash 自动补全支持](#bash_.E8.87.AA.E5.8A.A8.E8.A1.A5.E5.85.A8.E6.94.AF.E6.8C.81)
    *   [5.3 跨终端sudo](#.E8.B7.A8.E7.BB.88.E7.AB.AFsudo)
    *   [5.4 环境变量](#.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F)
    *   [5.5 传递命令别名](#.E4.BC.A0.E9.80.92.E5.91.BD.E4.BB.A4.E5.88.AB.E5.90.8D)
    *   [5.6 扯淡](#.E6.89.AF.E6.B7.A1)
    *   [5.7 使用root密码](#.E4.BD.BF.E7.94.A8root.E5.AF.86.E7.A0.81)
    *   [5.8 禁止root登陆](#.E7.A6.81.E6.AD.A2root.E7.99.BB.E9.99.86)
        *   [5.8.1 gksu](#gksu)
        *   [5.8.2 kdesu](#kdesu)
    *   [5.9 让 sudo 使用 /etc/sudoers.d 中的文件](#.E8.AE.A9_sudo_.E4.BD.BF.E7.94.A8_.2Fetc.2Fsudoers.d_.E4.B8.AD.E7.9A.84.E6.96.87.E4.BB.B6)
*   [6 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [6.1 SSH TTY 问题](#SSH_TTY_.E9.97.AE.E9.A2.98)
    *   [6.2 显示用户权限](#.E6.98.BE.E7.A4.BA.E7.94.A8.E6.88.B7.E6.9D.83.E9.99.90)
    *   [6.3 权限 Umask](#.E6.9D.83.E9.99.90_Umask)
    *   [6.4 默认 skeleton 文件](#.E9.BB.98.E8.AE.A4_skeleton_.E6.96.87.E4.BB.B6)

## 合理性

用户也可以通过[su](/index.php/Su "Su")切换到root用户运行命令。然而与su的启动一个root shell允许用户运行之后的所有的命令不同，sudo可以针对单个命令授予临时权限。sudo仅在需要时授予用户权限，减少了用户因为错误执行命令损坏系统的可能性。sudo也可以用来以其他用户身份执行命令。此外，sudo可以记录用户执行的命令，以及失败的特权获取。

## 安装

从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")中[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")软件包 [sudo](https://www.archlinux.org/packages/?name=sudo)。在配置之前，普通用户还无法使用sudo。所以请认真阅读配置部分。

## 使用

普通用户只需在命令前加上`sudo`，即可使用root（或其他用户）特权执行命令：

```
$ sudo pacman -Syu

```

参见：[sudo 手册](http://www.gratisoft.us/sudo/man/sudo.html)。

## 配置

### 查看当前设置

命令 `sudo -ll` 可以显示当前的 sudo 配置。

### 使用 visudo

sudo的配置文件是`/etc/sudoers`。`visudo`会锁住`sudoers`文件，保存修改到临时文件，然后检查文件格式，确保正确后才会覆盖`sudoers`文件。必须保证`sudoers`格式正确，否则sudo将无法运行。

**警告:** `/etc/sudoers`格式错误会导致sudo不可用。**必须**使用`visudo`编辑该文件防止出错。

`visudo`调用的默认编辑器是`vi`。官方仓库里的 sudo 编译时开启了`--with-env-editor`，会采用环境变量 `VISUAL` 和 `EDITOR`的设置。如果设置了`VISUAL` 就不会使用`EDITOR`。

如果要临时使用其他编辑器，在该命令前加上`EDITOR`环境变量即可。例如，要使用 `nano`，用root运行以下命令：

```
# EDITOR=nano visudo

```

要永久设置编辑器，请查看 [定义本地环境变量](/index.php/Environment_variables#Defining_variables_locally "Environment variables").

系统级的设置可以把编辑器设置到 `/etc/sudoers`。以 `nano` 为例，使用`visudo`打开该文件，加入以下内容：

```
# Defaults specification
# Reset environment by default
Defaults      env_reset
# Set default EDITOR to vim, and do not allow visudo to use EDITOR/VISUAL.
Defaults      editor=/usr/bin/nano, !env_editor

```

### 设置示例

要为某个用户可以执行所有命令，在配置文件中加入：

```
用户名   ALL=(ALL) ALL

```

如果只想允许以某个主机名登录用户执行命令：

```
用户名   主机名=(ALL) ALL

```

允许wheel[用户组](/index.php/Groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Groups (简体中文)")成员无密码使用sudo：

```
%wheel      ALL=(ALL) NOPASSWD: ALL

```

要不询问某个用户的密码:

```
Defaults:USER_NAME      !authenticate

```

只为用户启用部分命令的执行权限：

```
用户名 主机名=/sbin/halt,/sbin/poweroff,/sbin/reboot,/usr/bin/pacman -Syu

```

**注意:** 最后的设置会覆盖前面的设置，所以限定多的配置应该放到配置文件的后面。

只为某个主机名登录用户启用部分命令的执行权限，不用输入密码：

```
USER_NAME HOST_NAME= NOPASSWD: /usr/bin/halt,/usr/bin/poweroff,/usr/bin/reboot,/usr/bin/pacman -Syu

```

更详细的`sudoers`范例，参见[本页](http://www.gratisoft.us/sudo/sample.sudoers)。此外，更多信息参见：[sudoers 手册](http://www.gratisoft.us/sudo/man/sudoers.html)。

### sudoers文件默认权限

sudoers文件的属主和属组ID必须都是0，文件权限位是0440（-r--r-----）。如果你不小心改变了默认权限，应当立即恢复它们：

```
# chown -c root:root /etc/sudoers
# chmod -c 0440 /etc/sudoers

```

### 密码过期时间

用户可以修改sudo记录密码的时间。使用`visudo`命令将如下内容加入`/etc/sudoers`：

```
Defaults:用户名 timestamp_timeout=20

```

对该用户，sudo将记录密码20分钟。时间值也可以是小数。

**小贴士:** 如果timestamp_timeout设置为0，sudo总是询问密码。

## 使用技巧

### sudoers 范例

该配置针对使用终端复用器（screen、tmux或者ratpoison）：

```
/etc/sudoers

```

```
Cmnd_Alias WHEELER = /usr/sbin/lsof, /bin/nice, /bin/ps, /usr/bin/top, /usr/local/bin/nano, /usr/sbin/ss, /usr/bin/locate, /usr/bin/find, /usr/bin/rsync
Cmnd_Alias PROCESSES = /bin/nice, /bin/kill, /usr/bin/nice, /usr/bin/ionice, /usr/bin/top, /usr/bin/kill, /usr/bin/killall, /usr/bin/ps, /usr/bin/pkill
Cmnd_Alias EDITS = /usr/bin/vim, /usr/bin/nano, /usr/bin/cat, /usr/bin/vi
Cmnd_Alias ARCHLINUX = /usr/sbin/gparted, /usr/bin/pacman

root ALL = (ALL) ALL
yourusename ALL = (ALL) ALL, NOPASSWD: WHEELER, NOPASSWD: PROCESSES, NOPASSWD: ARCHLINUX, NOPASSWD: EDITS

Defaults !requiretty, !tty_tickets, !umask
Defaults visiblepw, path_info, insults, lecture=always
Defaults loglinelen = 0, logfile =/var/log/sudo.log, log_year, log_host, syslog=auth
Defaults mailto=webmaster@foobar.com, mail_badpass, mail_no_user, mail_no_perms
Defaults passwd_tries = 8, passwd_timeout = 1
Defaults env_reset, always_set_home, set_home, set_logname
Defaults !env_editor, editor="/usr/bin/vim:/usr/bin/vi:/usr/bin/nano"
Defaults timestamp_timeout=360
Defaults passprompt="Sudo invoked by [%u] on [%H] - Cmd run as %U - Password for user %p:"

```

### bash 自动补全支持

详情参见：[bash#Auto-completion](/index.php/Bash#Auto-completion "Bash")。

### 跨终端sudo

**警告:** 此举使得所有进程都使用同一个sudo任务。

如果不想每次启动新终端都重新输入密码，在配置文件中禁止**tty_tickets**即可：

```
Defaults !tty_tickets

```

### 环境变量

当前用户的环境变量不会应用到sudo启动的程序，除非使用`-E`选项：

```
$ sudo -E pacman -Syu

```

如果经常需要这样做，可以在`~/.bashrc`（或其他shell配置文件）中加入命令别名：

```
alias sudo="sudo -E"

```

在`/etc/sudoers`中添加以下内容作用相同：

```
Defaults !env_reset

```

可以把需要传递环境变量的命令设置到`env_keep`：

```
Defaults env_keep += "ftp_proxy http_proxy https_proxy no_proxy"

```

### 传递命令别名

当前用户的命令别名不会应用到sudo。如果需要这样，只需在`~/.bashrc`或者`/etc/bash.bashrc`中加入：

```
alias sudo='sudo '

```

### 扯淡

用户输入密码不正确时，sudo会提示“Sorry, try again.”。在配置文件的“Defaults”部分加入以下内容，会得到更有趣的错误提示：

```
#Defaults specification
Defaults insults

```

输入`sudo -K`清空密码缓存，然后测试。

### 使用root密码

默认sudo询问用户密码。添加`targetpw` 或 `rootpw`到配置文件的“Defaults”部分，可以让sudo询问root密码：

```
Defaults targetpw

```

可以限定特定的组使用 root 密码：

```
Defaults:%wheel targetpw
%wheel ALL=(ALL) ALL

```

### 禁止root登陆

**警告:** ArchLinux用户最好不要禁用root用户，出问题就麻烦大了。

有了sudo，用户也许希望禁止使用root登陆。没有了root用户，黑客就不知道管理员账户的名字了。

**警告:** 务必在禁用root**之前**配置好其他用户的权限！

使用`passwd`命令锁住root用户：

```
# passwd -l root

```

下列命令解锁root用户：

```
$ sudo passwd -u root

```

或者，编辑`/etc/shadow`文件，将root的加密口令列替换为“!”：

```
root:!:12345::::::

```

要再次启用sudo，重新设置其密码即可：

```
$ sudo passwd root

```

#### gksu

要设置 *gksu* 使用 sudo 而不是 root:

```
$ gconftool-2 --set --type boolean /apps/gksu/sudo-mode true

```

#### kdesu

KDE下常用kdesu以root权限执行GUI程序。默认情况下，即使root账户被禁用，kdesu仍会尝试使用su切换root。需要配置kdesu以使用sudo，创建/编辑`/usr/share/config/kdesurc`加入：

```
[super-user-command]
super-user-command=sudo

```

### 让 sudo 使用 /etc/sudoers.d 中的文件

*sudo* 可以解析 `/etc/sudoers.d/` 目录中的文件，这样就不需要编辑单一的 `/etc/sudoers` 文件，可以单独修改一个设置然后放入此目录。目录中配置的格式和 `/etc/sudoers`一样, 优点包括：

*   不需要编辑 {ic|sudoers.pacnew}} 文件;
*   如果新配置有问题，可以删除这个文件而不用编辑 `/etc/sudoers`.

## 疑难解答

### SSH TTY 问题

远程执行命令时，SSH默认不会分配tty。没有tty，sudo就无法在获取密码时关闭回显。使用`-tt`选项强制SSH分配tty（使用两次`-tt`）。

另一方面，sudoers中的`Defaults`选项`requiretty`要求只有拥有tty的用户才能使用sudo。可以通过`visudo`编辑配置文件，禁用这个选项：

```
# Disable "ssh hostname sudo <cmd>", because it will show the password in clear text. 
# You have to run "ssh -t hostname sudo <cmd>".
#
# Defaults    requiretty

```

### 显示用户权限

通过下列命令查看用户权限：

```
 sudo -lU 用户名

```

仅查看自己的权限：

```
 sudo -l

```

输出：

```
Matching Defaults entries for yourusename on this host:
    loglinelen=0, logfile=/var/log/sudo.log, log_year, syslog=auth, mailto=sqpt.webmaster@gmail.com, mail_badpass, mail_no_user, mail_no_perms, env_reset, always_set_home, tty_tickets, lecture=always, pwfeedback, rootpw, set_home

User yourusename may run the following commands on this host:
    (ALL) ALL, 
    (ALL) NOPASSWD: /usr/sbin/lsof, /bin/nice, /usr/sbin/ss, /usr/bin/su, /usr/bin/locate, /usr/bin/find, /usr/bin/rsync, /usr/bin/strace, 
    (ALL) /bin/nice, /bin/kill, /usr/bin/nice, /usr/bin/ionice, /usr/bin/top, /usr/bin/kill, /usr/bin/killall, /usr/bin/ps, /usr/bin/pkill, 
    (ALL) /usr/sbin/gparted, /usr/bin/pacman
    (ALL) /usr/local/bin/synergyc, /usr/local/bin/synergys, 
    (ALL) /usr/bin/vim, /usr/bin/nano, /usr/bin/cat
    (root) NOPASSWD: /usr/local/bin/synergyc

```

### 权限 Umask

Sudo 会统一用户的 [umask](/index.php/Umask "Umask") 值和它自己的 umask (默认是 0022)。这会阻止 sudo 创建比该用户的 umask 允许的打开权限更多的文件。这默认是合理的，因为没有使用自定义 umask。但是这可能导致用sudo运行一个命令和root运行一个命令建立的文件权限不同。如果这导致了问题，sudo 提供了一个方法来修复 umask，即使想要的 umask 比用户指定的 umask 权限还要多。添加下面内容 (使用 `visudo`) 会覆盖 sudo 的默认行为：

```
Defaults umask = 0022
Defaults umask_override

```

这会将 sudo 的 umask 设置为 root 的默认 umask (0022)，覆盖掉默认行为，无论用户的umask设置成什么都会使用这里设定的值。

### 默认 skeleton 文件

[此页面](http://www.sudo.ws/sudo/sudoers.man.html#x5355444f455253204f5054494f4e53) 列出了所有可用配置。