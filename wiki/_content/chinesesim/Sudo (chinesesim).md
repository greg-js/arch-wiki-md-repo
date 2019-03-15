相关文章

*   [Users and Groups (简体中文)](/index.php/Users_and_Groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and Groups (简体中文)")
*   [su](/index.php/Su "Su")

**翻译状态：** 本文是英文页面 [Sudo](/index.php/Sudo "Sudo") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-15，点击[这里](https://wiki.archlinux.org/index.php?title=Sudo&diff=0&oldid=559971)可以查看翻译后英文页面的改动。

[Sudo](https://www.sudo.ws/sudo/)(substitute user do) 使得系统管理员可以授权特定用户或用户组作为 root 或他用户执行某些（或所有）命令，同时还能够对命令及其参数提供审核跟踪。

用户可以选择用 [su](/index.php/Su "Su") 切换到 root 用户运行命令，但是这种方式会启动一个 root shell 并允许用户运行之后的所有的命令。而 sudo 可以针对单个命令、仅在需要时授予临时权限，减少因为执行错误命令损坏系统的可能性。sudo 也能以其他用户身份执行命令并且记录用户执行的命令，以及失败的权限申请。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 使用](#使用)
*   [3 配置](#配置)
    *   [3.1 查看当前设置](#查看当前设置)
    *   [3.2 使用 visudo](#使用_visudo)
    *   [3.3 设置示例](#设置示例)
    *   [3.4 sudoers文件默认权限](#sudoers文件默认权限)
    *   [3.5 密码过期时间](#密码过期时间)
*   [4 使用技巧](#使用技巧)
    *   [4.1 bash 自动补全支持](#bash_自动补全支持)
    *   [4.2 跨终端sudo](#跨终端sudo)
    *   [4.3 环境变量](#环境变量)
    *   [4.4 传递命令别名](#传递命令别名)
    *   [4.5 使用root密码](#使用root密码)
    *   [4.6 禁止root登陆](#禁止root登陆)
        *   [4.6.1 kdesu](#kdesu)
    *   [4.7 让 sudo 使用 /etc/sudoers.d 中的文件](#让_sudo_使用_/etc/sudoers.d_中的文件)
    *   [4.8 编辑文件](#编辑文件)
*   [5 疑难解答](#疑难解答)
    *   [5.1 SSH TTY 问题](#SSH_TTY_问题)
    *   [5.2 权限 Umask](#权限_Umask)
    *   [5.3 默认 skeleton 文件](#默认_skeleton_文件)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")软件包 [sudo](https://www.archlinux.org/packages/?name=sudo)。

## 使用

在配置之前，普通用户还无法使用sudo。所以请认真阅读配置部分。

普通用户只需在命令前加上`sudo`，即可使用 root 特权执行命令：

```
$ sudo *cmd*

```

参见：[sudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudo.8) 。

## 配置

有关配置和密码过期等问题的更多信息，请阅读 [man sudoers](http://www.sudo.ws/man/1.8.13/sudoers.man.html)。

### 查看当前设置

命令 `sudo -ll` 可以显示当前的 sudo 配置; 命令 `sudo -lU *user*` 可以查看某个特定用户的设置。

### 使用 visudo

sudo的配置文件是`/etc/sudoers`。`visudo`会锁住`sudoers`文件，保存修改到临时文件，然后检查文件格式，确保正确后才会覆盖`sudoers`文件。必须保证`sudoers`格式正确，否则sudo将无法运行。

**警告:** `/etc/sudoers`格式错误会导致sudo不可用。**必须**使用`visudo`编辑该文件防止出错。

`visudo`调用的默认编辑器是`vi`。官方仓库里的 sudo 编译时开启了`--with-env-editor`，会采用环境变量 `VISUAL` 和 `EDITOR`的设置。如果设置了`VISUAL` 就不会使用`EDITOR`。

如果要临时使用其他编辑器，在该命令前加上`EDITOR`环境变量即可。例如，要使用 `nano`，用root运行以下命令：

```
# EDITOR=nano visudo

```

要永久设置编辑器，请查看 [定义本地环境变量](/index.php/Environment_variables#Defining_variables "Environment variables").

系统级的设置可以把编辑器设置到 `/etc/sudoers`。以 `nano` 为例，使用`visudo`打开该文件，加入以下内容：

```
# Defaults specification
# Reset environment by default
Defaults      env_reset
# Set default EDITOR to vim, and do not allow visudo to use EDITOR/VISUAL.
Defaults      editor=/usr/bin/nano, !env_editor

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
Defaults:USER_NAME      !authenticate

```

**警告:** 任何以您的用户名运行的程序都可以无需密码就执行 sudo。

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

**提示：** 如果timestamp_timeout设置为0，sudo总是询问密码。

## 使用技巧

### bash 自动补全支持

详情参见：[bash (简体中文)#自动命令补全](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#自动命令补全 "Bash (简体中文)")。

### 跨终端sudo

**警告:** 此举使得所有进程都使用同一个sudo任务。

如果不想每次启动新终端都重新输入密码，在配置文件中禁止**tty_tickets**即可：

```
Defaults !tty_tickets

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
Defaults !env_reset

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

**Tip:** 要在禁用 root 账号后使用交互 root 身份确认，请使用 `sudo -i`.

#### kdesu

KDE下常用 kdesu 以 root 权限执行图形程序。默认情况下，即使root账户被禁用，kdesu仍会尝试使用su切换root。需要配置kdesu以使用sudo，创建/编辑`~/.config/kdesurc`，加入：

```
[super-user-command]
super-user-command=sudo

```

或者使用下面命令：

```
$ kwriteconfig5 --file kdesurc --group super-user-command --key super-user-command sudo

```

### 让 sudo 使用 /etc/sudoers.d 中的文件

*sudo* 可以解析 `/etc/sudoers.d/` 目录中的文件，这样就不需要编辑单一的 `/etc/sudoers` 文件，可以单独修改一个设置然后放入此目录。目录中配置的格式和 `/etc/sudoers`一样, 优点包括：

*   不需要编辑 {ic|sudoers.pacnew}} 文件;
*   如果新配置有问题，可以删除这个文件而不用编辑 `/etc/sudoers`.

`/etc/sudoers.d/` 目录中的文件是按字母顺序加载的，`.` 或 `~` 开头的文件会被跳过。文件名应该以双字母开头，例如 `01_foo`，请注意配置文件的顺序以避免相互覆盖。

+

**Warning:** The files in `/etc/sudoers.d/` are just as fragile as `/etc/sudoers` itself: any improperly formatted file will prevent `sudo` from working. Hence, for the same reason it is strongly advised to use `visudo`

### 编辑文件

`sudo -e` 或 `sudoedit` 可以实现用其它用户编辑文件，但是文件编辑器本身还是以当前用户运行。

这样可以不已 root 用户运行程序，但是保存时具有 root 权限，详情参考 [sudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudo.8#e).

可以用 [meld](https://www.archlinux.org/packages/?name=meld) 管理 [pacnew](/index.php/Pacman/Pacnew_and_Pacsave "Pacman/Pacnew and Pacsave") 文件:

```
$ SUDO_EDITOR=meld sudo -e /etc/*file*{,.pacnew*}*

```

## 疑难解答

### SSH TTY 问题

远程执行命令时，SSH默认不会分配tty。没有tty，sudo就无法在获取密码时关闭回显。使用`-tt`选项强制SSH分配tty。

另一方面，sudoers中的`Defaults`选项`requiretty`要求只有拥有tty的用户才能使用sudo。可以通过`visudo`编辑配置文件，禁用这个选项：

```
# Disable "ssh hostname sudo <cmd>", because it will show the password in clear text. 
# You have to run "ssh -t hostname sudo <cmd>".
#
# Defaults    requiretty

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