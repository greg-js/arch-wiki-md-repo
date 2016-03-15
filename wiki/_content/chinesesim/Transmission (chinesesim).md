**翻译状态：** 本文是英文页面 [Transmission](/index.php/Transmission "Transmission") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-03-18，点击[这里](https://wiki.archlinux.org/index.php?title=Transmission&diff=0&oldid=250764)可以查看翻译后英文页面的改动。

[Transmission](http://www.transmissionbt.com/) 是一个轻量级、跨平台的 BitTorrent 客户端。是许多 Linux 发行版默认的 BitTorrent 客户端。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 作为守护进程运行](#.E4.BD.9C.E4.B8.BA.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E8.BF.90.E8.A1.8C)
        *   [2.1.1 更改守护进程用户](#.E6.9B.B4.E6.94.B9.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E7.94.A8.E6.88.B7)
*   [3 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 安装

[官方仓库](/index.php/Official_repositories "Official repositories")中有几个可选的:

	[transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli)

	包括命令行工具、守护进程和 web 客户端.

	[transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk)

	GTK+ 图形界面.

	[transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt)

	Qt 图形界面.

## 配置

对于 [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk) 和 [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt)，配置文件的默认路径是 `~/.config/transmission`。

对于 [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli)，默认路径是 `~/.config/transmission-daemon`。

### 作为守护进程运行

首先安装 [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli)。 然后启动 *transmission* [守护进程](/index.php/Daemon "Daemon").

在浏览器中访问 [http://127.0.0.1:9091](http://127.0.0.1:9091) 以查看 web 客户端。

你可以根据自己的喜好编辑主要的配置文件 `~/.config/transmission-daemon/settings.json` 。在编辑之前**你必须先停止守护进程**， 否则你的修改 **不会被保存**. 默认情况下，守护进程会以 *transmission* 的用户身份运行，其 home 目录是 `/var/lib/transmission/`。也就是说，默认的配置文件是 `/var/lib/transmission/.config/transmission-daemon/settings.json`.

**Note:** 如果你找不到 `~/.config/transmission-daemon` 目录, 运行一次 `transmission-daemon` 来创建它

如果你更改了下载目录, 请确保 *transmission* 用户对新的下载目录有读写权限。

#### 更改守护进程用户

如果你使用 systemd，你必须同时在 service 文件 (`/usr/lib/systemd/system/transmission.service`) 和临时文件 (`/usr/lib/tmpfiles.d/transmission.conf`) 中修改用户。 把它们复制到 `/etc` 目录下的相应位置：

```
# cp /usr/lib/systemd/system/transmission.service /etc/systemd/system/
# cp /usr/lib/tmpfiles.d/transmission.conf /etc/tmpfiles.d/

```

创建一个新组，比如叫做，`transmission`:

```
# groupadd transmission

```

把你选择的用户加到这个新的 `[组]`，比如 `transmission` 中：

```
# gpasswd -a [用户] [组]

```

然后把 service 文件和临时文件中的 `User=` 设置为你选择的用户，就像下面这样：

 `/etc/tmpfiles.d/transmission.conf`  `d /run/transmission - [用户] [组] -` 

然后运行 `systemd-tmpfiles --create transmission.conf` 并重启 transmission 服务.

编辑之后，你需要重新加载 service 文件:

```
# systemctl daemon-reload

```

别忘了把 '/run/transmission' 目录的权限设置为 **777** 。

如果想让 Transmission 守护进程以自己的组运行，你必须给下载目录分配写入权限。要做到这一点，你需要运行：

```
# chgrp transmission /path/to/download
# chmod g+w /path/to/download

```

## 更多信息

*   [Transmission 维基](https://trac.transmissionbt.com/wiki)
*   [HeadlessUsage](https://trac.transmissionbt.com/wiki/HeadlessUsage/General)