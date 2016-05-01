**翻译状态：** 本文是英文页面 [Users_and_Groups](/index.php/Users_and_Groups "Users and Groups") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-12-14，点击[这里](https://wiki.archlinux.org/index.php?title=Users_and_Groups&diff=0&oldid=410430)可以查看翻译后英文页面的改动。

GNU/Linux 通过用户和用户组实现[访问控制](https://en.wikipedia.org/wiki/access_control#Computer_security "wikipedia:access control") —— 包括对文件访问、设备使用的控制。Linux 默认的访问控制机制相对简单直接，不过还有一些更加高级的机制，包括 [ACL](/index.php/ACL "ACL") 和 [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication").

## Contents

*   [1 概览](#.E6.A6.82.E8.A7.88)
*   [2 权限与属主](#.E6.9D.83.E9.99.90.E4.B8.8E.E5.B1.9E.E4.B8.BB)
*   [3 用户管理](#.E7.94.A8.E6.88.B7.E7.AE.A1.E7.90.86)
    *   [3.1 添加登录用户](#.E6.B7.BB.E5.8A.A0.E7.99.BB.E5.BD.95.E7.94.A8.E6.88.B7)
    *   [3.2 添加系统用户](#.E6.B7.BB.E5.8A.A0.E7.B3.BB.E7.BB.9F.E7.94.A8.E6.88.B7)
    *   [3.3 其它用户管理示例](#.E5.85.B6.E5.AE.83.E7.94.A8.E6.88.B7.E7.AE.A1.E7.90.86.E7.A4.BA.E4.BE.8B)
    *   [3.4 用户名修改经验](#.E7.94.A8.E6.88.B7.E5.90.8D.E4.BF.AE.E6.94.B9.E7.BB.8F.E9.AA.8C)
    *   [3.5 用户信息存储](#.E7.94.A8.E6.88.B7.E4.BF.A1.E6.81.AF.E5.AD.98.E5.82.A8)
*   [4 用户组管理](#.E7.94.A8.E6.88.B7.E7.BB.84.E7.AE.A1.E7.90.86)
*   [5 文件列表](#.E6.96.87.E4.BB.B6.E5.88.97.E8.A1.A8)
*   [6 群组列表](#.E7.BE.A4.E7.BB.84.E5.88.97.E8.A1.A8)
    *   [6.1 用户组](#.E7.94.A8.E6.88.B7.E7.BB.84)
    *   [6.2 系统组](#.E7.B3.BB.E7.BB.9F.E7.BB.84)
    *   [6.3 程序专用组](#.E7.A8.8B.E5.BA.8F.E4.B8.93.E7.94.A8.E7.BB.84)
    *   [6.4 不再使用的组](#.E4.B8.8D.E5.86.8D.E4.BD.BF.E7.94.A8.E7.9A.84.E7.BB.84)
    *   [6.5 systemd 之前的群组](#systemd_.E4.B9.8B.E5.89.8D.E7.9A.84.E7.BE.A4.E7.BB.84)

## 概览

*用户*一般指使用计算机的人。在本文语境中，该词指用来识别用户的用户名称，既可以是 Mary 或 Bill 这样的真名，也可以是 Dragonlady, Pirate 这样的昵称。关键是，计算机给每个账户分配了特定的名称，而用户则使用这些名称访问计算机。除了人之外，一些系统服务也以有部分限制，又享有部分特权的用户账户身份运行。

由于安全需要，「用户管理」应运而生，以加以明确限制各个用户账户的权限。超级用户 root 于计算机里拥有至高无上的管理权限，所以一般只作管理用。非特权用户则可以用 [su](/index.php/Su "Su") 或 [sudo](/index.php/Sudo "Sudo") 程序以临时获得特权。

个体可以拥有多账户，只不过彼此名称当然不同。但有一些用户名称已事先被系统占用，比如 "root".

此外，任意用户可能从属某个「用户组」。此外用户也能够新加入某些已经存在的用户组，以获取该组所拥有的特权。

**注意:** 新手请务必谨慎地使用这方面的工具，并且要避免对除自己以外的其他**已存在**用户发生误操作。

## 权限与属主

摘自 [In UNIX Everything is a File （UNIX 中一切皆文件）](http://ph7spot.com/musings/in-unix-everything-is-a-file)：

	集众多灵感及理念之大成，UNIX 操作系统打造出了它的设计、接口、文化甚至革新。重中之重，有一句道理：「一切皆文件」可谓 UNIX 的真谛之一。

	根据这一设计原则，必须要有统一的模型，用以管理对大量 I/O 资源的访问：文档、目录、磁盘、CD-ROM、调制解调器、键盘、打印机、显示器和终端等等，甚至也包括了进程、网络之间的通信。而解决之策，就是为所有这些资源提成一个抽象层，UNIX 之父们称之为「文件」。所有文件都通过一致的 API 以提供访问，因此光只用同一套简单的命令，就可以读写磁盘、键盘、文档以及网络设备。

摘自 [Extending UNIX File Abstraction for General-Purpose Networking （针对常规的网络应用，扩展出 UNIX 文件抽象层）](http://www.intel-research.net/Publications/Pittsburgh/101220041324_277.pdf)：

	UNIX 及兼容系统提供了一个即基本又强悍的抽象层——文件。很多系统服务和设备的应用程序接口，一开始都被设计为文件或文件系统之类的东西。这赋予程序全新的姿态——通过文件抽象层，我们就可以以全新的方式使用众多现成的、且用途单一的小工具。例如 cat 工具，原本只用来读取文件，再将其内容发送到标准输出，但现在它也可以直接访问特殊设备文件（通常在 `/dev` 目录中），加以读取 I/O 设备。在很多系统上，音频记录和播放也可以通过一令执行：分别是 `cat /dev/audio > myfile` 以及 `cat myfile > /dev/audio`.

GNU/Linux 系统中的每一个文件都从属一个用户（属主）和一个用户组（属组）。另外，还有三种类型的访问权限：读（read）、写（write）、运行（execute）。我们可以针对文件的属主、属组、而设置相应的访问权限。再次，我们可以通过 [ls](/index.php/Core_utilities#ls "Core utilities") 命令的长列表格式以查询文件属主、属组和权限：

 `$ ls /boot/ -l` 
```
total 18492
drwxr-xr-x 3 root root    12288 Aug 21 03:27 grub
-rw-r--r-- 1 root root 12487150 Aug 29 18:24 initramfs-linux-fallback.img
-rw-r--r-- 1 root root  2990626 Aug 29 18:23 initramfs-linux.img
-rw-r--r-- 1 root root  3440576 Aug 26 15:17 vmlinuz-linux 

```

第一列是文件访问权限（例如，文件`initramfs-linux.img`的权限为`-rw-r--r--`），第三列和第四列分别是属主和属组（本例中所有文件属主都是*root*用户，属组都是*root*组）。

 `$ ls -l /media/` 
```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared
```

上述例子中，`sf_Shared`目录由*root*用户和*vboxsf*组所有。使用`stat`命令也可以查看文件所有权和权限：

属主：

 `$ stat -c %U /media/sf_Shared/`  `root` 

属组：

 `$ stat -c %G /media/sf_Shared/`  `vboxsf` 

访问权限：

 `$ stat -c %A /media/sf_Shared/`  `drwxrwx---` 

访问权限由三组字符组成，分别代表属主、属组、其他人的权限。例如，`-rw-r--r--`表示属组有读写权限、但无运行权限（`rw-`），属组用户和其他用户只有读取权限（`r--`）。又如，`drwxrwx---`表示文件属主和属组用户有读、写、执行权限（`rwx`），而禁止其他用户任何访问（`---`）。第一个字符”d“代表文件类型（目录）。

通过`find`命令查找属于某个用户或某个组的文件：

```
# find / -group "用户组"
# find / -user "用户"

```

文件的属主、属组可以通过`chown`命令更改。文件的权限可以通过`chmod`命令修改。

详情参见：[man chown](http://linux.die.net/man/1/chown)、[man chmod](http://linux.die.net/man/1/chmod)、[Linux 文件权限](http://www.linux.com/learn/tutorials/309527-understanding-linux-file-permissions)。

## 用户管理

使用`who`命令，可以查看目前已登陆的用户。

使用`useradd`命令添加用户：

```
# useradd -m -g "初始组" -G "附加组" -s "登陆shell" "用户"

```

*   **`-m`**：创建用户主目录`/home/[用户名]`；在自己的主目录内，即使不是root用户也可以读写文件、安装程序等等。
*   **`-g`**：设置用户初始组的名称或数字ID；该组必须是存在的；如果没有设置该选项，`useradd`会根据`/etc/login.defs`文件中的USERGROUPS_ENAB环境变量进行设置。默认(`USERGROUPS_ENAB yes`) 会用和用户名相同的名字创建群组，`GID` 等于 `UID`.
*   **`-G`**：用户要加入的附加组列表；使用逗号分隔多个组，不要添加空格；如果不设置，用户仅仅加入初始组。
*   **`-s`**：用户默认登录shell的路径；启动过程结束后，默认启动的登录shell在此处设定；请确保使用的shell已经安装，默认是 [Bash](/index.php/Bash "Bash")。

**警告:** 为了登录，登录 shell 必须位于 `/etc/shells` 中, 否则 `pam_shell` 模块会阻止登录请求。不要使用 `/usr/bin/bash` 替代 `/bin/bash`, 除非这个路径已经在 `/etc/shells`中正确配置.

*   有时候需要禁止某些用户执行登录动作，例如用来执行系统服务的用户。将shell设置成 `/usr/bin/nologin` 就可以禁止用户登录。(`nologin(8)`).

### 添加登录用户

以典型的桌面系统为例，要添加一个名为*archie*的用户，并使用[bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)")作为登录shell：

```
# useradd -m -G wheel -s /bin/bash archie

```

此命令会自动创建 `archie` 群组，并成为 `archie` 的默认登录群组。建议每一个用户都设置自己的默认群组，因为[umask](/index.php/Umask "Umask") 默认值是 `002`, 所以同一个默认群组的用户会有创建文件的写权限。参阅 [User Private Groups](https://security.ias.edu/how-and-why-user-private-groups-unix)。

要赋予一个群组某个目录的写权限，可以在父目录中设置：

```
# chmod g+s *our_shared_directory*

```

有关`useradd`的高级用法，参见man页：

```
$ man useradd

```

通过下列命令设置用户密码，虽然不是必须的，还是强烈建议设置密码

```
# passwd [用户名]

```

### 添加系统用户

为进程、守护进程分配不同的系统用户可以更安全的管控目录及文件的访问。下面命令创建一个不创建 `home` 目录的非登录用户(可以加入 `-U` 参数创建一个和用户名相同的群组):

```
# useradd -r -s /usr/bin/nologin *username*

```

### 其它用户管理示例

更改用户登录名：

```
# usermod -l *newname* *oldname*

```

更改用户主目录：

```
# usermod -dm /my/new/home *username*

```

`-m` 选项会自动创建新目录并移动内容。

将用户加入 (`*群组*`，用逗号分隔:

```
# usermod -aG *群组* *username*

```

{{警告|如果不使用 `-a` 选项，用户会离开没有列在`*群组*`的其它群组。

*gpasswd* 也能实现同样的修改，但是一次只能加入一个组：

```
# gpasswd --add *username* *group*

```

通过下列命令设置*GECOS*字段（用户信息，例如用户全名）：

```
# chfn [用户名]

```

（这样将会以交互式模式启动`chfn`）

此外，可以设置 GECOS comment：

```
# usermod -c "Comment" *username*

```

使用`userdel`命令删除用户：

```
# userdel -r [用户名]

```

`-r`选项表示一并删除用户主目录和邮件。

### 用户名修改经验

**警告:** 确保你不是使用你要修改的用户名登录，同时按下(`Ctrl`+`Alt`+`F1`)打开一个新的终端，使用root用户登录，或用其他用户登录后使用su命令登录为root用户。

操作得当的话，在Arch（或其他Linux发行版）中更改用户名是安全的，并且很简单。你可以更改用户所属的组。按照以下步骤进行，可以保留受影响用户的UID和GID，而不会搞乱你已经设置好的文件权限。还有一种方法是手动编辑 `/etc/passwd` 文件。

*   如果要使用[sudo](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)")，请更新文件`/etc/sudoers`把新的用户（以root登录使用visudo命令）添加进去。
*   如果修改了`~/.bashrc`的PATH环境变量，并把新的用户添加进去。
*   同样的，记得更改配置文件`/etc/rc.local`或者任何配置文件里用到的，放在旧的用户主目录里的脚本或者挂载点。
*   我不得不重复[Firefox拼写校正](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.8B.BC.E5.86.99.E6.A3.80.E6.9F.A5.E5.AD.97.E5.85.B8 "Firefox (简体中文)")里的步骤，否则更改用户名后拼写校正就不再起作用了。
*   更改用户名后，我不得不重新安装Thunderbird扩展（[Enigmail](http://enigmail.mozdev.org/home/index.php)）。
*   系统（桌面快捷方式，脚本等）里使用了旧的用户主目录的地方，都需要进行修改。要在脚本中避免这样的问题，可以使用`~`或`$HOME`变量来表示主目录。

### 用户信息存储

本地用户信息储存在`/etc/passwd`文件中。要查看系统上所有用户账户：

```
$ cat /etc/passwd

```

一行代表一个用户，格式如下，每行分七个部分，用英文冒号“:”分开：

```
account:password:UID:GID:GECOS:directory:shell

```

此处：

*   `account`：用户名，不能为空，而且要符合标准的*NIX命名规则。
*   `password`：加密的密码，可以使用一个小写的"x"（不带括号）表示密码保存在`/etc/shadow`文件里。
*   `UID` `GID`：每个用户和组有一个对应的UID和GID（用户ID和组ID）。Arch里面，第一个非root用户的默认UID是1000，后续创建的用户UID也应大于1000，特定用户的GID应该属于指定的首要组，组的ID数值列在`/etc/group`文件里。
*   `GECOS`：可选的注释字段，通常记录用户全名
*   `directory`：用于登录命令设置`$HOME`环境变量。某些服务的用户主目录设置为"/"是安全的，但不建议普通用户设置为此目录。
*   `shell`：是用户默认登录的shell，通常是[Bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)")，还可选择其他的命令解释器，默认是"/bin/bash"（不带括号），如果你用的是别的shell，在这里设置其路径，此部分是可选的，可留空。

**注意:** Arch Linux 使用*影子*密码。`passwd`文件对所有人可读，在里面存储密码（无论是否加密过）是很不安全的。在`password`字段，通常使用一个占位字符（`x`）代替。加密过的密码储存在`/etc/shadow`文件，该文件对普通用户限制访问。

示例：

```
jack:x:1001:100:Jack Smith,some comment here,,:/home/jack:/bin/bash

```

示例分解说明：用户登录名为jack，密码保存在`/etc/shadow`，UID为1001，首要组的ID是100 (users组)，全名Jack Smith并加了一些注释，主目录是`/home/jack`，使用Bash作为默认shell。

## 用户组管理

`/etc/group`文件储存了系统中用户组的信息，详情参见：`man group`。

使用`groups`命令查看用户所在组的名称：

```
$ groups [用户名]

```

若省略用户名，默认显示当前用户所在组。

`id`命令提供额外的信息，包括用户UID以及相关用户组GID：

```
$ id [用户名]

```

查看所有组：

```
$ cat /etc/group

```

使用`groupadd`创建新的组：

```
# groupadd [组名]

```

使用`gpasswd`将用户添加到组：

```
# gpasswd -a [用户名] [组名]

```

更改用户所属的组名，不变更`GID`：

```
# groupmod -n newname oldname

```

删除用户组：

```
# groupdel [组名]

```

将用户从组中移除：

```
# gpasswd -d [用户名] [组名]

```

如果用户已登录，必须重新登录使更改生效。

## 文件列表

**警告:** 不要手动编辑这些文件。有些工具可以更好的处理锁定、避免数据库错误。

| 文件 | 作用 |
| `/etc/shadow` | 保存用户安全信息 |
| `/etc/passwd` | 用户账户信息 |
| `/etc/gshadow` | 保存组账号的安全信息 |
| `/etc/group` | 定义用户所属的组 |
| `/etc/sudoers` | 可以运行 sudo 的用户 |
| `/home/*` | 主目录 |

## 群组列表

### 用户组

| 组 | 影响文件 | 作用 |
| games | `/var/games` | 访问一些游戏。 |
| rfkill | **不再使用!** 控制无线设备的电源 (可能被 [rfkill](https://www.archlinux.org/packages/?name=rfkill) 使用). |
| users | 标准用户组. |
| uucp | `/dev/ttyS[0-9]`, `/dev/tts/[0-9]` | 串口和 USB 设备，例如猫、手柄 RS-232/串口。 |
| wheel | 管理组，通常用于　sudo　和 su 命令权限。systemd 会允许非　root 的 wheel 组用户启动服务。[[1]](http://cgit.freedesktop.org/systemd/systemd/tree/TODO#n79) |

### 系统组

下列组系统使用，一般不被 Arch 用户使用：

| 组 | 影响文件 | 作用 |
| avahi |
| bin | `/usr/bin/*` | 以只读权限访问 `/usr/bin/` 中的二进制文件. |
| clamav | `/var/lib/clamav/*`, `/var/log/clamav/*` | [Clam AntiVirus](/index.php/Clam_AntiVirus "Clam AntiVirus") 使用. |
| daemon |
| dbus | `/var/run/dbus/*` |
| ftp | `/srv/ftp` | [FTP](https://en.wikipedia.org/wiki/FTP "wikipedia:FTP") 服务器，例如 [Proftpd](/index.php/Proftpd "Proftpd") |
| gdm | X 认证目录 (ServAuthDir) | [GDM](/index.php/GDM "GDM") 组. |
| hal | `/var/run/hald`, `/var/cache/hald` |
| http |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| mail | `/usr/bin/mail` |
| mem |
| mpd | `/var/lib/mpd/*`, `/var/log/mpd/*`, `/var/run/mpd/*`, 可选的音乐目录 | [MPD](/index.php/MPD "MPD") 组. |
| nobody | 无权限的组。 |
| ntp | `/var/lib/ntp/*` | [NTPd](/index.php/NTPd "NTPd") 组. |
| policykit | [PolicyKit](/index.php/PolicyKit "PolicyKit") 组. |
| root | `/*` | 完全的系统管理和控制 (root, admin) |
| smmsp | [sendmail](https://en.wikipedia.org/wiki/sendmail "wikipedia:sendmail") 组. |
| systemd-journal | `/var/log/journal/*` | 访问完整系统日志，不在此组中的用户仅能访问自己生成的信息。 |
| tty | `/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx` | 访问 `/dev/ACMx` |
| vboxsf | 虚拟系统的共享目录 | [VirtualBox](/index.php/VirtualBox "VirtualBox")使用. |

### 程序专用组

如下组中的成员可以执行特定程序：

| 组 | 影响文件 | 作用 |
| adbusers | `/dev/`中的设备节点 | 访问 [Android](/index.php/Android "Android") 调试桥。 |
| cdemu | `/dev/vhba_ctl` | 使用 [CDemu](/index.php/CDemu "CDemu") 模拟驱动. |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | 使用 [updatedb](https://en.wikipedia.org/wiki/updatedb "wikipedia:updatedb") 命令。 |
| networkmanager | 通过 [NetworkManager](/index.php/NetworkManager "NetworkManager") 连接无线网的权限。这个组在默认的Arch设置里没有，需要手动添加 |
| thinkpad | `/dev/misc/nvram` | ThinkPad 用户访问 [tpb](/index.php/Tpb "Tpb") 等工具。 |
| vboxusers | `/dev/vboxdrv` | 使用Virtualbox软件 |
| vmware | 使用 [VMware](/index.php/VMware "VMware") 软件。 |

### 不再使用的组

| 群组 | 目的 |
| log | `/var/log/*` | 访问 `/var/log` 中的日志. |
| ssh | 默认不创建，不是标准组。 |
| stb-admin | **不再使用!** 曾经用来控制 [system-tools-backends](http://system-tools-backends.freedesktop.org/) 的访问。 |
| kvm | 用户空间软件可以访问 `/dev/kvm` 接口 | 使用 [KVM](/index.php/KVM "KVM") 的硬件虚拟化。 |

### systemd 之前的群组

如下组是 systemd 之前使用，目前已经没有任何作用，使用后还可能对功能有影响:

| 组 | 作用 |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | 直接访问声音硬件([ALSA](/index.php/ALSA "ALSA") 和 [OSS](/index.php/OSS "OSS")). |
| camera | 访问 [Digital Cameras](/index.php/Digital_Cameras "Digital Cameras"). |
| disk | `/dev/sda[1-9]`, `/dev/sdb[1-9]` | 直接访问不受 *optical*, *floppy* 和 *storage* 组控制的块设备. 除非有特殊需要, 否则不建议将一般用户添加至该组. |
| floppy | `/dev/fd[0-9]` | 访问软盘驱动器。 |
| lp | `/etc/cups`, `/var/log/cups`, `/var/cache/cups`, `/var/spool/cups` | 访问打印设备，管理打印任务。 |
| network | 改变网络设置的权限，比如使用 [NetworkManager](/index.php/NetworkManager "NetworkManager") 的权限. |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | 访问光学设备，比如CD，DVD。 |
| power | 使用 [Pm-utils](/index.php/Pm-utils "Pm-utils") (挂起、休眠...) 和电源管理控制。 |
| scanner | `/var/lock/sane` | 访问扫描仪硬件。 |
| storage | 访问可移动储存器，例如 USB 硬盘、flash 存储器、MP3 播放器等；用户可以通过 [D-Bus](/index.php/D-Bus "D-Bus") 挂载设备。 |
| sys | 管理 [CUPS](/index.php/CUPS "CUPS") 中的打印机. |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | 访问视频捕获和硬件加速设备。例如framebuffer ([X](/index.php/Xorg "Xorg") 不属于这个组也能使用). |