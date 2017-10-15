**翻译状态：** 本文是英文页面 [TigerVNC](/index.php/TigerVNC "TigerVNC") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-10-06，点击[这里](https://wiki.archlinux.org/index.php?title=TigerVNC&diff=0&oldid=337318)可以查看翻译后英文页面的改动。

VNC 服务是一个远程显示守护进程，它向用户提供一些远程功能，包括：

1.  直接控制本地 X 会话；
2.  在一台机器上的后台并行 X 会话，即并不显示在物理显示器上而是虚拟显示器。即使用户断开连接，在服务器上运行的所有程序依旧可以运行。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 运行 VNC 服务](#.E8.BF.90.E8.A1.8C_VNC_.E6.9C.8D.E5.8A.A1)
    *   [2.1 初次设置](#.E5.88.9D.E6.AC.A1.E8.AE.BE.E7.BD.AE)
        *   [2.1.1 创建环境和密码文件](#.E5.88.9B.E5.BB.BA.E7.8E.AF.E5.A2.83.E5.92.8C.E5.AF.86.E7.A0.81.E6.96.87.E4.BB.B6)
        *   [2.1.2 编辑 xstartup 文件](#.E7.BC.96.E8.BE.91_xstartup_.E6.96.87.E4.BB.B6)
        *   [2.1.3 权限](#.E6.9D.83.E9.99.90)
    *   [2.2 启动服务](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1)
*   [3 在物理显示器上（5900端口）运行VNC服务](#.E5.9C.A8.E7.89.A9.E7.90.86.E6.98.BE.E7.A4.BA.E5.99.A8.E4.B8.8A.EF.BC.885900.E7.AB.AF.E5.8F.A3.EF.BC.89.E8.BF.90.E8.A1.8CVNC.E6.9C.8D.E5.8A.A1)
    *   [3.1 使用 TigerVNC 的 x0vncserver （推荐）](#.E4.BD.BF.E7.94.A8_TigerVNC_.E7.9A.84_x0vncserver_.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)
    *   [3.2 使用 x11vnc （推荐）](#.E4.BD.BF.E7.94.A8_x11vnc_.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)
    *   [3.3 使用一个 dirty hack （不推荐）](#.E4.BD.BF.E7.94.A8.E4.B8.80.E4.B8.AA_dirty_hack_.EF.BC.88.E4.B8.8D.E6.8E.A8.E8.8D.90.EF.BC.89)
        *   [3.3.1 基本设置](#.E5.9F.BA.E6.9C.AC.E8.AE.BE.E7.BD.AE)
        *   [3.3.2 给 xorg-server 打补丁](#.E7.BB.99_xorg-server_.E6.89.93.E8.A1.A5.E4.B8.81)
*   [4 连接 VNC 服务](#.E8.BF.9E.E6.8E.A5_VNC_.E6.9C.8D.E5.8A.A1)
    *   [4.1 无密码验证](#.E6.97.A0.E5.AF.86.E7.A0.81.E9.AA.8C.E8.AF.81)
    *   [4.2 图形界面客户端示例](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E5.AE.A2.E6.88.B7.E7.AB.AF.E7.A4.BA.E4.BE.8B)
*   [5 使用 SSH 隧道加密 VNC 服务](#.E4.BD.BF.E7.94.A8_SSH_.E9.9A.A7.E9.81.93.E5.8A.A0.E5.AF.86_VNC_.E6.9C.8D.E5.8A.A1)
    *   [5.1 服务端配置](#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E9.85.8D.E7.BD.AE)
    *   [5.2 客户端配置](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.85.8D.E7.BD.AE)
    *   [5.3 在 Android 设备上通过 SSH 连接 VNC 服务器](#.E5.9C.A8_Android_.E8.AE.BE.E5.A4.87.E4.B8.8A.E9.80.9A.E8.BF.87_SSH_.E8.BF.9E.E6.8E.A5_VNC_.E6.9C.8D.E5.8A.A1.E5.99.A8)
*   [6 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [6.1 在开关机时启动关闭 VNC 服务](#.E5.9C.A8.E5.BC.80.E5.85.B3.E6.9C.BA.E6.97.B6.E5.90.AF.E5.8A.A8.E5.85.B3.E9.97.AD_VNC_.E6.9C.8D.E5.8A.A1)
    *   [6.2 复制远程机器剪贴板内容到本地](#.E5.A4.8D.E5.88.B6.E8.BF.9C.E7.A8.8B.E6.9C.BA.E5.99.A8.E5.89.AA.E8.B4.B4.E6.9D.BF.E5.86.85.E5.AE.B9.E5.88.B0.E6.9C.AC.E5.9C.B0)
    *   [6.3 解决无光标问题](#.E8.A7.A3.E5.86.B3.E6.97.A0.E5.85.89.E6.A0.87.E9.97.AE.E9.A2.98)
    *   [6.4 连接到 OS X（Mac）系统](#.E8.BF.9E.E6.8E.A5.E5.88.B0_OS_X.EF.BC.88Mac.EF.BC.89.E7.B3.BB.E7.BB.9F)
*   [7 中文原内容](#.E4.B8.AD.E6.96.87.E5.8E.9F.E5.86.85.E5.AE.B9)

## 安装

VNC 服务由 [tigervnc](https://www.archlinux.org/packages/?name=tigervnc) 提供，在 [AUR](/index.php/AUR "AUR") 中也有 [tightvnc](https://aur.archlinux.org/packages/tightvnc/)。

## 运行 VNC 服务

### 初次设置

#### 创建环境和密码文件

在首次运行时，VNC服务会创建其初始环境文件和用户密码文件：

 `$ vncserver` 
```
You will require a password to access your desktops.

Password:
Verify:

New 'mars:1 (facade)' desktop is mars:1

Creating default startup script /home/facade/.vnc/xstartup
Starting applications specified in /home/facade/.vnc/xstartup
Log file is /home/facade/.vnc/mars:1.log

```

VNC服务运行的默认端口是 :1 ，它代表服务运行的TCP端口（5900+n = 端口号）。在此例中，它运行在 5900+1=5901 。再次执行VNC服务会创建另一个实例，并运行在下一个更高的空闲端口上，例如 :2 或说 5902。

**注意:** 在物理内存允许的条件下，Linux系统可以拥有任意数量的VNC服务——它们互相并行。

使用 -kill 开关来关闭VNC服务：

```
$ vncserver -kill :1

```

#### 编辑 xstartup 文件

VNC 服务读取 `~/.vnc/xstartup` 文件（功能类似于 [.xinitrc](/index.php/.xinitrc ".xinitrc")）。如果需要图形环境，则用户至少需要定义一个桌面环境来启动。例如：启动xfce4

```
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
exec startxfce4

```

**注意:** 已知 `XKL_XMODMAP_DISABLE` 一行可以用来解决（在虚拟桌面环境的终端下打字时）按键混乱的相关问题

确保该文件有可执行权限：

```
 chmod u+x ~/.vnc/xstartup

```

#### 权限

像对待 `~/.ssh` 一样保护 `~/.vnc` 是很好的做法，虽然并非必须。执行下面的命令来达到该目的：

```
$ chmod 700 ~/.vnc

```

### 启动服务

Vncserver 通过开关（命令行参数）来提供灵活性。下面的例子启动具有特定分辨率、允许多用户同时观看/控制且设置 dpi 为 96 的 VNC 服务。

```
$ vncserver -geometry 1440x900 -alwaysshared -dpi 96 :1

```

**注意:** 不必对 vncserver 使用标准分辨率。可以使用任意奇怪分辨率——例如 1429x882 或者 1900x200——来取代 1440x900。

如需要完整的选项表，向 vncserver 传递 -help 开关。

```
$ vncserver -help

```

## 在物理显示器上（5900端口）运行VNC服务

### 使用 TigerVNC 的 x0vncserver （推荐）

TigerVNC 提供名为 x0vncserver 的二进制文件，它具有和 x11vnc 相类似的功能。例如：

```
x0vncserver -display :0 -passwordfile ~/.vnc/passwd

```

欲获取更多信息，执行

```
man x0vncserver

```

### 使用 x11vnc （推荐）

如果需要远程控制物理显示，使用 [x11vnc](https://www.archlinux.org/packages/?name=x11vnc)。参见 [X11vnc](/index.php/X11vnc "X11vnc") 获取更多信息。

### 使用一个 dirty hack （不推荐）

#### 基本设置

安装 xorg-server 和 tigervnc，并且在 Xorg 的配置中载入“vnc”。 示例： `/etc/X11/xorg.conf.d/10-vnc.conf`:

```
Section "Module"
  Load "vnc"
EndSection

Section "Screen"
  Identifier "Screen0"
  Option "SecurityTypes" "None"
EndSection

```

为了进行密码验证，在执行 vncpasswd 命令后，将“Screen”一节换成下面这样

```
Section "Screen"
  Identifier "Screen0"
  Option "SecurityTypes" "VncAuth"
  Option "UserPasswdVerifier" "VncAuth"
  Option "PasswordFile" "/root/.vnc/passwd"
EndSection

```

#### 给 xorg-server 打补丁

很不幸，在 xorg-server 包中有一个 bug。（2013/11/15）幸好 fedora 对此有一个补丁。

[http://pkgs.fedoraproject.org/cgit/xorg-x11-server.git/plain/0001-include-export-key_is_down-and-friends.patch?h=f19&id=06e94667faa0cd1f9f32cf54e9e447ef50fde635](http://pkgs.fedoraproject.org/cgit/xorg-x11-server.git/plain/0001-include-export-key_is_down-and-friends.patch?h=f19&id=06e94667faa0cd1f9f32cf54e9e447ef50fde635)

执行 abs 命令，放好补丁文件并编辑 PKGBUILD。

PKGBUILD 例子：

```
source = vnc.patch
sha256sums = '1bbbe70236dc70b5e35572f2197d163637100f8c58d0038bdc240df075eb5726'
prepare() {
  cd "${pkgbase}-${pkgver}"
  # patch for vnc module
  patch -Np1 -i ../vnc.patch

```

补丁（为免链接失效）

```
+++ b/include/input.h
@@ -244,12 +244,12 @@  typedef struct _InputAttributes {
 #define KEY_POSTED 2
 #define BUTTON_POSTED 2

-extern void set_key_down(DeviceIntPtr
diff --git a/include/input.h b/include/input.h
index 350daba..2d5e531 100644
--- a/include/input.h
+++ b/include/input.h
@@ -244,12 +244,12 @@  typedef struct _InputAttributes {
 #define KEY_POSTED 2
 #define BUTTON_POSTED 2

-extern void set_key_down(DeviceIntPtr pDev, int key_code, int type);
-extern void set_key_up(DeviceIntPtr pDev, int key_code, int type);
-extern int key_is_down(DeviceIntPtr pDev, int key_code, int type);
-extern void set_button_down(DeviceIntPtr pDev, int button, int type);
-extern void set_button_up(DeviceIntPtr pDev, int button, int type);
-extern int button_is_down(DeviceIntPtr pDev, int button, int type);
+extern _X_EXPORT void set_key_down(DeviceIntPtr pDev, int key_code, int type);
+extern _X_EXPORT void set_key_up(DeviceIntPtr pDev, int key_code, int type);
+extern _X_EXPORT int key_is_down(DeviceIntPtr pDev, int key_code, int type);
+extern _X_EXPORT void set_button_down(DeviceIntPtr pDev, int button, int type);
+extern _X_EXPORT void set_button_up(DeviceIntPtr pDev, int button, int type);
+extern _X_EXPORT int button_is_down(DeviceIntPtr pDev, int button, int type);

extern void InitCoreDevices(void);
extern void InitXTestDevices(void);

```

## 连接 VNC 服务

一个 VNC 服务可允许任意数量的客户端来连接。下面给出一个简单例子，其中 VNC 服务运行在 10.1.10.2 的 5901（:1，使用速记法）端口：

```
$ vncviewer 10.1.10.2:1

```

### 无密码验证

`-passwd` 开关允许我们定义服务器上 `~/.vnc/passwd` 文件的位置。在服务器方面（无论是通过 [SSH](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)") 还是物理接触），用户需要有权访问该文件。在任一情况下，都应将该文件放在客户端文件系统的一个安全位置（例如一个仅给期望用户以读取权限的位置）。

```
$ vncviewer -passwd /path/to/server-passwd-file

```

### 图形界面客户端示例

*   [gtk-vnc](https://www.archlinux.org/packages/?name=gtk-vnc)
*   [kdenetwork-krdc](https://www.archlinux.org/packages/?name=kdenetwork-krdc)
*   [rdesktop](https://www.archlinux.org/packages/?name=rdesktop)
*   [vinagre](https://www.archlinux.org/packages/?name=vinagre)
*   [remmina](https://www.archlinux.org/packages/?name=remmina)
*   [vncviewer-jar](https://www.archlinux.org/packages/?name=vncviewer-jar)

## 使用 SSH 隧道加密 VNC 服务

### 服务端配置

若希望从 LAN 保护之外访问 VNC 服务，你需要考虑明文密码及客户端与服务端之间未加密通信的问题。VNC 服务可以很简单地使用 SSH 隧道进行加密。另外，不要使用此方法对外界打开另一个端口，因为通信会沿用户之前对 WAN 打开的 SSH 端口在隧道中依次进行。在这种情况下，强烈推荐使用 -localhost 开关运行 vncserver。该开关仅允许接收*从本机*发起的连接，并顺理成章地仅允许物理 SSH 连接并认证到机器上的用户。（This switch only allows connections *from the localhost* -- and by analogy only by users physically ssh'ed and authenticated on the box!）

```
$ vncserver -geometry 1440x900 -alwaysshared -dpi 96 -localhost :1

```

### 客户端配置

既然服务器现在只接受本机的连接，使用 -L 开关通过 SSH 连接到该机器来打开隧道。例如：

```
$ ssh 目标机器IP -L 8900/localhost/5901

```

该命令将服务器的 5901 端口转发到客户机的 8900 端口。一旦已通过 SSH 连接，则保持该 xterm 或 shell 窗口开启——它会作为和服务器通信的加密隧道。为了通过 VNC 连接，打开第二个 xterm 并连接到客户机的加密隧道上（而不是远程服务器的 IP 地址）：

```
$ vncviewer localhost::8900

```

以下来自 SSH 的手册页面： *-L [bind_address:] port:host:hostport*

*Specifies that the given port on the local (client) host is to be forwarded to the given host and port on the remote side. This works by allocating a socket to listen to port on the local side, optionally bound to the specified bind_address. Whenever a connection is made to this port, the connection is forwarded over the secure channel, and a connection is made to host port hostport from the remote machine. Port forwardings can also be specified in the configuration file. IPv6 addresses can be specified with an alternative syntax:*

*[bind_address/] port/host/ hostport or by enclosing the address in square brackets.* *Only the superuser can forward privileged ports. By default, the local port is bound in accordance with the GatewayPorts setting. However, an explicit bind_address may be used to bind the connection to a specific address. The bind_address of ``localhost'' indicates that the listening port be bound for local use only, while an empty address or `*' indicates that the port should be available from all interfaces.*

### 在 Android 设备上通过 SSH 连接 VNC 服务器

为了在 Android 设备上通过 SSH 连接到 VNC 服务器，需要具备以下条件：

```
1\. 在要连接的机器上运行 SSH 服务
2\. 在要连接的机器上运行 VNC 服务。（使用上面提到的 -localhost 标志来运行服务）
3\. 在 Android 设备上安装 SSH 客户端。（ConnectBot 是一个常见选择，并在本向导中用作例子。）
4\. 在 Android 设备上安装VNC客户端（androidVNC）

```

考虑为目标使用一些动态 DNC 服务，来解决无固定 IP 地址问题。（原文：Consider some dynamic DNS service for targets that do not have static IP addresses.）

在 ConnectBot 中，键入 IP 并连接到所期望的机器。按选项键，选择端口转发，并增加一个新端口然后保存之：

```
Nickname: vnc
Type: Local
Source port: 5901
Destination: 127.0.0.1:5901
```

在 androidVNC 中：

```
Nickname: nickname
Password: 设置 VNC 服务器时使用的密码
Address: 127.0.0.1 (we are in local after connecting through SSH)
Port: 5901
```

连接即可。

## 提示和技巧

### 在开关机时启动关闭 VNC 服务

在这里寻找这个文件`/usr/lib/systemd/system/vncserver.service`

 `/etc/systemd/system/vncserver@:1.service` 
```
# The vncserver service unit file
#
# 1\. Copy this file to /etc/systemd/system/vncserver@:x.service
#  Note that x is the port number on which the vncserver will run.  The default is 1 which 
#  corresponds to port 5901\.  For a 2nd instance, use x=2 which corresponds to port 5902.
# 2\. Edit User=
#   ("User=foo")
# 3\. Edit  and vncserver parameters appropriately
#   ("/usr/bin/vncserver %i -arg1 -arg2 -argn")
# 4\. Run `systemctl --system daemon-reload`
# 5\. Run `systemctl enable vncserver@:<display>.service`
#
# DO NOT RUN THIS SERVICE if your local area network is untrusted! 
#
# See the wiki page for more on security
# https://wiki.archlinux.org/index.php/Vncserver

[Unit]
Description=Remote desktop service (VNC)
After=syslog.target network.target

[Service]
Type=forking
User=

# Clean any existing files in /tmp/.X11-unix environment
ExecStartPre=-/usr/bin/vncserver -kill %i
ExecStart=/usr/bin/vncserver %i
ExecStop=/usr/bin/vncserver -kill %i

[Install]
WantedBy=multi-user.target

```

### 复制远程机器剪贴板内容到本地

如果从远程机器到本机的复制不工作，如该[参考](https://bbs.archlinux.org/viewtopic.php?id=101243)下面所述，在服务器上执行 autocutsel：

```
$ autocutsel -fork

```

现在，按下 F8 键显示 VNC 弹出菜单，选择 `Clipboard: local -> remote` 选项。

你可以将上述命令放在 `~/.vnc/xstartup` 中，以使其在 VNC 服务启动时自动运行。

### 解决无光标问题

如果使用 `x0vncserver` 时光标无法显示，那么像下面这样启动 vncviewer：

```
$ vncviewer DotWhenNoCursor=1 <server>

```

或者将 `DotWhenNoCursor=1` 写在 tigervnc 的配置文件（默认在 `~/.vnc/default.tigervnc`）中。

### 连接到 OS X（Mac）系统

参见 [https://help.ubuntu.com/community/AppleRemoteDesktop](https://help.ubuntu.com/community/AppleRemoteDesktop) 。已在 Remmina 上测试。

## 中文原内容

VNC 代表 'Virtual Network Computing'（即虚拟网络计算机）.

他是一种远程屏幕显示协议，也是一种使用该协议控制远程计算机的程序。通过它，你可以从任何地方的计算机，不管他们是局域网内的还是因特网上的，你都可以连接到你的桌面上。

你可以通过安装[SSH](/index.php/SSH "SSH")（Secure SHell）支持来提升VNC会话的安全性。

在ArchLinux中，内含有很多种VNC服务器和客户端可用，比如：

*   [Tightvnc](/index.php/Tightvnc "Tightvnc")

*   [X11vnc (简体中文)](/index.php/X11vnc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "X11vnc (简体中文)")

*   其他

你可以通过执行下面的命令来查看所有的VNC程序列表：

```
# pacman -Ss vnc

```