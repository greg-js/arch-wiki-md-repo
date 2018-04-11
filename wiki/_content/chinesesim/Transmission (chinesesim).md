**翻译状态：** 本文是英文页面 [Transmission](/index.php/Transmission "Transmission") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-04-09，点击[这里](https://wiki.archlinux.org/index.php?title=Transmission&diff=0&oldid=507716)可以查看翻译后英文页面的改动。

[Transmission](http://www.transmissionbt.com/) 是一个轻量级、跨平台的 BitTorrent 客户端。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 图形界面的配置](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E7.9A.84.E9.85.8D.E7.BD.AE)
*   [3 Transmission 守护程序和命令行](#Transmission_.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F.E5.92.8C.E5.91.BD.E4.BB.A4.E8.A1.8C)
    *   [3.1 守护程序的启动与停止](#.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F.E7.9A.84.E5.90.AF.E5.8A.A8.E4.B8.8E.E5.81.9C.E6.AD.A2)
    *   [3.2 减少多余的日志](#.E5.87.8F.E5.B0.91.E5.A4.9A.E4.BD.99.E7.9A.84.E6.97.A5.E5.BF.97)
    *   [3.3 仅当连接到网络时运行](#.E4.BB.85.E5.BD.93.E8.BF.9E.E6.8E.A5.E5.88.B0.E7.BD.91.E7.BB.9C.E6.97.B6.E8.BF.90.E8.A1.8C)
        *   [3.3.1 Netctl](#Netctl)
        *   [3.3.2 Wicd](#Wicd)
    *   [3.4 选择一个用户](#.E9.80.89.E6.8B.A9.E4.B8.80.E4.B8.AA.E7.94.A8.E6.88.B7)
    *   [3.5 配置守护程序](#.E9.85.8D.E7.BD.AE.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F)
        *   [3.5.1 Host 白名单](#Host_.E7.99.BD.E5.90.8D.E5.8D.95)
        *   [3.5.2 监视目录](#.E7.9B.91.E8.A7.86.E7.9B.AE.E5.BD.95)
        *   [3.5.3 启用 IPv6](#.E5.90.AF.E7.94.A8_IPv6)
        *   [3.5.4 CLI 使用示范](#CLI_.E4.BD.BF.E7.94.A8.E7.A4.BA.E8.8C.83)
*   [4 Web 界面](#Web_.E7.95.8C.E9.9D.A2)
    *   [4.1 GUI 方式](#GUI_.E6.96.B9.E5.BC.8F)
    *   [4.2 CLI 方式](#CLI_.E6.96.B9.E5.BC.8F)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [5.1 无法使用网络连接至守护程序](#.E6.97.A0.E6.B3.95.E4.BD.BF.E7.94.A8.E7.BD.91.E7.BB.9C.E8.BF.9E.E6.8E.A5.E8.87.B3.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F)
    *   [5.2 无法显示 Web 界面](#.E6.97.A0.E6.B3.95.E6.98.BE.E7.A4.BA_Web_.E7.95.8C.E9.9D.A2)
*   [6 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 安装

有多种可选的软件包：

*   [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) - 包括命令行工具、守护程序和 [#Web 界面](#Web_.E7.95.8C.E9.9D.A2)。
*   [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk) - GTK+ 3 图形界面.
*   [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt) - Qt5 图形界面.
*   [tremc-git](https://aur.archlinux.org/packages/tremc-git/) - 用于守护程序的 Curses 界面。

**注意:** GTK+ 客户端无法连接至守护程序，想用守护程序的用户可以考虑带图形界面的 Qt 包，或是带 Curses 界面的 tremc 包。

## 图形界面的配置

两种带 GUI 的版本 *transmission-gtk* 和 *transmission-qt* 都可以在没有后端守护程序的情况下独立运行。

GUI 版本都被配置为开箱即用，但用户可能仍需要更改一些设置。GUI 配置文件的默认路径是 `~/.config/transmission`。

在 Transmission 的网站上，有一份各种选项如何配置的教程： [https://github.com/transmission/transmission/wiki/Editing-Configuration-Files](https://github.com/transmission/transmission/wiki/Editing-Configuration-Files).

## Transmission 守护程序和命令行

*transmission-cli* 支持的命令包括：

	*transmission-daemon*: 启动守护程序。

	*transmission-remote*: 调用本地或远程守护程序的 [命令行界面](https://en.wikipedia.org/wiki/Command-line_interface "wikipedia:Command-line interface")，后面跟着希望守护程序运行的命令。

	*transmission-show*: 返回指定种子文件的信息。

	*transmission-create*: 创建一个新的种子文件。

	*transmission-edit*: 新增、删除或替换一个 tracker 服务器的 announce URL。

	*transmission-cli*: ([已弃用](https://github.com/transmission/transmission/commit/950387ab5a443629598f93c057f41150707866ab)) 启动一个非守护程序的本地 *transmission* 实例，用于手动下载一个种子。

	*tremc*: (需要 [tremc-git](https://aur.archlinux.org/packages/tremc-git/)) 为本地或远程守护程序启动一个 [curses](https://en.wikipedia.org/wiki/curses_(programming_library) 界面。

### 守护程序的启动与停止

就像 [#选择一个用户](#.E9.80.89.E6.8B.A9.E4.B8.80.E4.B8.AA.E7.94.A8.E6.88.B7) 里面的说明那样，transmission 的守护程序可以按以下方式运行：

*   作为 *transmission* 用户运行，只要 [用 systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") start/enable `transmission.service` 服务即可。

	你可以按照 [#选择一个用户](#.E9.80.89.E6.8B.A9.E4.B8.80.E4.B8.AA.E7.94.A8.E6.88.B7) 里的说明更改默认用户。

*   用你自己的账户，只要在账户下运行： `$ transmission-daemon` 守护程序可以这样来停止： `$ killall transmission-daemon` 

启动守护程序将会创建一个初始的 *transmission* 配置文件。详情参阅 [#配置守护程序](#.E9.85.8D.E7.BD.AE.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F)。

另一种停止 transmission 的方法是使用 *transmission-remote* 命令：

```
$ transmission-remote --exit

```

### 减少多余的日志

运行 transmission-daemon 可能会产生许多不需要的日志条目。只要用一个小脚本包装一下再启动就可以过滤日志输出。以下示例可以提供一些启发：

 `transwrap.sh` 
```
#!/bin/zsh
killall transmission-daemon 2> /dev/null
transmission-daemon --foreground --log-info 2>&1 | while read line; do
	echo $line |
		grep -v "announcer.c:\|platform.c:\|announce done (tr-dht.c:" |
		grep -v "Saved.*variant.c:" |
		while read line; do
			echo $line | grep -q "Queued for verification (verify.c:" &&
				notify-send --app-name="Transmission Started" "${line#* * }"
			echo $line | grep -q "changed from .Incomplete. to .Complete." &&
				notify-send --app-name="Transmission Complete" "${line#* * }"
			echo $line | systemd-cat --identifier="TransWrap" --priority=5
		done 2>&1 > /dev/null
	done&disown

```

### 仅当连接到网络时运行

#### Netctl

你可能只想在连接某些网络时运行 transmission。下面的脚本会先检查连接是否在授权的网络列表中，是的话再继续启动 transmission-daemon。

 `/etc/netctl/hooks/90-transmission.sh` 
```
#!/bin/bash

# The SSIDs for which we enable this.
declare -A ssids=(
    ["network_1"]=y
    ["network_2"]=y
)

if [[ ${ssids[$SSID]} ]]; then
    case $ACTION in
        CONNECT|REESTABLISHED)
            # Need to wait, otherwise doesn't seem to bind to 9091.
            sleep 30
            systemctl start transmission
            ;;
        *)
            systemctl stop transmission
            ;;
    esac
fi

```

#### Wicd

在文件夹 `/etc/wicd/scripts/postconnect` 里创建一个 [启动脚本](#.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F.E7.9A.84.E5.90.AF.E5.8A.A8.E4.B8.8E.E5.81.9C.E6.AD.A2)，并且在文件夹 `/etc/wicd/scripts/predisconnect` 里创建一个 [停止脚本](#.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F.E7.9A.84.E5.90.AF.E5.8A.A8.E4.B8.8E.E5.81.9C.E6.AD.A2)。记得给它们运行权限，例如：

 `/etc/wicd/scripts/postconnect/transmission` 
```
#!/bin/bash

systemctl start transmission
```
 `/etc/wicd/scripts/predisconnect/transmission` 
```
#!/bin/bash

systemctl stop transmission
```

### 选择一个用户

选择你想如何运行 `transmission`：

*   作为独立用户运行，默认用户是 `transmission`（推荐，因为安全性更高）。

默认情况下，*transmission* 会创建名为 `transmission` 的用户和组（它的主目录的文件位于 `/var/lib/transmission/`），并且用这个“账户”运行。这是一种安全措施，因为这样 *transmission* 及其下载的文件将无法访问 `/var/lib/transmission/` 目录之外的文件。配置、操作和访问下载的文件需要使用 “root” 权限完成（比如用 [sudo](/index.php/Sudo "Sudo")）。

*   在你自己的账户下运行。

设置这种方式需要 [重写](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BF.AE.E6.94.B9.E7.8E.B0.E5.AD.98.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6 "Systemd (简体中文)") 已提供的服务文件并在其中指定你的用户名：

 `/etc/systemd/system/transmission.service.d/username.conf` 
```
[Service]
User=*your_username*
```

### 配置守护程序

[启动守护程序](#.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F.E7.9A.84.E5.90.AF.E5.8A.A8.E4.B8.8E.E5.81.9C.E6.AD.A2) 来创建缺省的配置文件。

*   如果用 `transmission` 这个用户来运行 Transmission，配置文件会存放在 `/var/lib/transmission/.config/transmission-daemon/settings.json`。

*   如果用你自己的账户运行 Transmission，配置文件会存放在 `~/.config/transmission-daemon/settings.json`。

使用一个 Transmission 客户端或者用自带的 web 界面（在支持的浏览器中用 [http://localhost:9091](http://localhost:9091) 来访问）可以自定义守护程序。

在 Transmission 的网站上，有一份各种选项如何配置的教程：[https://github.com/transmission/transmission/wiki/Editing-Configuration-Files](https://github.com/transmission/transmission/wiki/Editing-Configuration-Files)

**注意:** 如果你想用一个文本编辑器手动编辑配置文件，请先 [停止守护程序](#.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F.E7.9A.84.E5.90.AF.E5.8A.A8.E4.B8.8E.E5.81.9C.E6.AD.A2)；否则当它停止时将会覆盖配置文件。

**注意:** 另一种方式是，可以用 SIGHUP 信号指示守护程序重新加载其配置，运行 `kill -s SIGHUP `pidof transmission-daemon`` 即可。

一个给那些用 `transmission` 账户运行的用户的建议是，用适当的权限创建一个共享的下载目录，这样就能同时允许 `transmission` 账户和其他账户访问下载文件，也能相应地更新配置文件。例如：

```
# mkdir /mnt/data/torrents
# chown -R facade:transmission /mnt/data/torrents
# chmod -R 775 /mnt/data/torrents

```

现在 `/mnt/data/torrents` 目录可供系统账户 `facade` 和 `transmission` 用户所属的 `transmission` 组访问。非常不鼓励使这个目录可读写（即不要将目录 *chmod* 到 *777*），而是应该将个别用户/组的部分权限授予部分目录。

**注意:** 如果 `/mnt/data/torrents` 位于一个可移除的设备上，比如这是一个 `/etc/fstab` 条目且带有 `nofail` 选项，那么 Transmission 会报告说没有找到文件。要解决这个问题，可以在 `/etc/systemd/system/transmission.service.d/transmission.conf` 文件的 `[Unit]` 一节中加入 `RequiresMountsFor=/mnt/data/torrents`。

另一种方法是把你的账户加入 `transmission` 用户组 (`#usermod -a -G transmission yourusername`)，然后修改 `/var/lib/transmission` 和 `/var/lib/transmission/Downloads` 目录的权限设置，以允许 `transmission` 组成员对这两个目录的 `rwx` 访问权。

#### Host 白名单

如果你想用远程主机的主机名来访问位于该主机上的 Transmission 守护程序，你需要把主机名加入 `settings.json` 文件中的 `rpc-host-whitelist` 字段中。 否则你会在连接主机时收到一条 "421 Misdirected Request" 错误。

如果你用该服务器的 IP 地址来访问守护程序，这一步可以省略。

#### 监视目录

如果你想 *自动添加某个文件夹中的 .torrent 文件*，但是配置文件中的 `watch-dir` 和 `watch-dir-enabled` 选项都不起作用，可以带 `-c /path/to/watch/dir` 参数启动 transmission 守护程序。

如果你在用 systemd，按照 [systemd (简体中文)#修改现存单元文件](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BF.AE.E6.94.B9.E7.8E.B0.E5.AD.98.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6 "Systemd (简体中文)") 里面的描述编辑 `transmission.service` 单元文件。

#### 启用 IPv6

默认情况下，守护程序仅监听 IPv4 连接。要同时监听 IPv6 连接，安装 [transmission-cli-ipv6](https://aur.archlinux.org/packages/transmission-cli-ipv6/) (或者 [transmission-cli-git](https://aur.archlinux.org/packages/transmission-cli-git/)，或者等 Transmission 3.0 发布)，然后把 `settings.json` 里的 `rpc-bind-address` 选项改为 `"::"`。

#### CLI 使用示范

如果你想删除所有已完成的种子，可以用下面的命令（用你自己的用户名和密码）：

```
# transmission-remote -n 'username:password' -l | grep 100% | awk '{print $1}'| paste -d, -s | xargs -i transmission-remote -t {} -r

```

## Web 界面

### GUI 方式

当 Transmission 安装完毕后就可以轻易架起 web 界面。你只需要单击 **edit** 菜单，选择 **preferences**。单击 **Remote** 选项卡并启用 **Allow remote access**。

此处你可以修改默认的监听端口 9091。

单击 **Use authentication** 并填写用户名和密码就可以启用身份认证。

要提高安全性，可以启用 **Only allow these IP addresses** 限制来自任意 IP 的访问。

现在你可以单击 **Open web client** （用你的默认浏览器打开）或手动访问 `http://*TARGET_IP_ADDRESS*:*PORT*` 来启动 web 界面。

如果没有修改监听端口，默认是 9091。在这种情况下访问链接是 `[http://localhost:9091](http://localhost:9091)`。

**注意:** 记住，必须安装 [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli)。

### CLI 方式

设置 web 界面甚至不需要借助图形界面，因为守护程序提供了类似的选项。你无需指定任何参数即可访问 web 界面，可参阅 [#守护程序的启动与停止](#.E5.AE.88.E6.8A.A4.E7.A8.8B.E5.BA.8F.E7.9A.84.E5.90.AF.E5.8A.A8.E4.B8.8E.E5.81.9C.E6.AD.A2)。

不过，你仍然可以指定在前一节中看到的所有选项：

 `$ transmission-daemon --auth --username arch --password linux --port 9091 --allowed "127.0.0.1"` 

等同于

 `$ transmission-daemon -t -u arch -v linux -p 9091 -a "127.0.0.1"` 

## 故障排除

#### 无法使用网络连接至守护程序

在 `network.service` 初始化后守护程序就会开始运行。但是，如果启用了 `dhcpcd` 服务而不是特定设备的服务（比如 `dhcpcd@enp1s0.service`），可能 Transmission 会因为启动过早而无法绑定到相应的网络接口。于是 web 界面无法访问。一种可能的解决方案是在 systemd 单元的 [配置文件](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BF.AE.E6.94.B9.E7.8E.B0.E5.AD.98.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6 "Systemd (简体中文)") 里增加 `Requires` 行。

 `/etc/systemd/system/transmission.service.d/fixdep.conf` 
```
[Unit]
Requires=network.target
```

#### 无法显示 Web 界面

```
404: Not Found

Couldn't find Transmission's web interface files!

Users: to tell Transmission where to look, set the TRANSMISSION_WEB_HOME environment variable to the folder where the web interface's index.html is located.

Package Builders: to set a custom default at compile time, #define PACKAGE_DATA_DIR in libtransmission/platform.c or tweak tr_getClutchDir () by hand.
```

即使你用图形界面，也需要安装 [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) 来支持 web 界面。

## 更多信息

*   [Transmission 维基](https://trac.transmissionbt.com/wiki)
*   [HeadlessUsage](https://trac.transmissionbt.com/wiki/HeadlessUsage/General)