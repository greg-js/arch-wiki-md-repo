Thunar 是一个快速、轻量级、容易使用的文件管理器。它是 Xfce4 的一部分，但是它能够和不同的窗口管理器一起工作。Thunar 对 [Openbox](/index.php/Openbox "Openbox") 和 [Awesome](/index.php/Awesome "Awesome") 用户非常有吸引力。

## Contents

*   [1 安装](#安装)
*   [2 自动挂载](#自动挂载)
    *   [2.1 Thunar Volume 管理器](#Thunar_Volume_管理器)
        *   [2.1.1 安装](#安装_2)
        *   [2.1.2 配置](#配置)
        *   [2.1.3 提示和技巧](#提示和技巧)
            *   [2.1.3.1 使用 Daemon 模式](#使用_Daemon_模式)
            *   [2.1.3.2 设置图标主题](#设置图标主题)
    *   [2.2 Thunar 存档管理插件](#Thunar_存档管理插件)
        *   [2.2.1 安装](#安装_3)
    *   [2.3 Thunar 媒体标签插件](#Thunar_媒体标签插件)
        *   [2.3.1 安装](#安装_4)
    *   [2.4 Thunar Thumbnailers](#Thunar_Thumbnailers)
        *   [2.4.1 安装](#安装_5)
    *   [2.5 Thunar 共享](#Thunar_共享)
        *   [2.5.1 安装](#安装_6)
        *   [2.5.2 配置](#配置_2)
*   [3 参考资料](#参考资料)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") [官方软件源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 中的 [thunar](https://www.archlinux.org/packages/?name=thunar) 软件包。

如果使用 [Xfce4](/index.php/Xfce_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xfce (简体中文)")，Thunar 应该已被安装。

## 自动挂载

Thunar 使用 [gvfs](/index.php/Gvfs "Gvfs") 进行自动挂载，安装配置方法请阅读[GVFS](/index.php/GVFS "GVFS")。

### Thunar Volume 管理器

Thunar 支持自动挂载，Thunar Volume 管理器扩展了 Thunar 自带的挂载功能，例如，在挂载时自动的运行命令或者自动打开一个 Thunar 窗口。

#### 安装

```
# pacman -S thunar-volman

```

#### 配置

它也能被配置为当相机和音频播放器连接时执行一定的行为。 安装好此插件之后：

1.  启动 Thunar 点击 Edit - Preferences
2.  选择 Advanced 标签，选中 'Enable Volume Management'（未安装时显示：Install the "thunar-volman" package to use the volume management support in Thunar）
3.  点击配置进行适当的改变（看下面的例子）

这里有一个设置的例子，使用 Amarok 播放 CD。

```
Multimedia - Audio CDs: `amarok --cdplay %d`

```

#### 提示和技巧

##### 使用 Daemon 模式

Thunar 可以被运行在 daemon 模式下。这样做有不少好处，例如能够快速启动，Thunar 运行在后台，在必要时仅打开一个窗口（例如，当插入一个 flash 设备）。

自动运行它的一种方式是通过 `.xinitrc` 或者自动启动的脚本（such as [Openbox](/index.php/Openbox "Openbox")'s `autostart`）。使用 Daemon 模式运行只需要简单的添加以下语句到你的启动脚本中或者在终端运行：

```
thunar --daemon &

```

##### 设置图标主题

如果你没有使用 Gnome 或者 Xfce，那么可能缺少与 icons 相关的包或者配置。像 Awesome 和 Xmonad 之类的窗口管理器并不附带 X 设置管理器（XSettings managers），而 Thunar 首先就会去寻找 icon 的设置信息。如果你已经使用了很多 Xfce4 和 Gnome 应用程序，那么 xfce-mcs-manager 可能已经被安装了并且在启动时运行。我们可以在 ~/.gtkrc-2.0 中添加这样的设置：

```
gtk-icon-theme-name = "Tango"

```

当然，安装 gnome-icon-theme 包能够改变 Thunar 默认下所有文件都是白纸图标（paper icon）的情况。

```
# pacman -S gnome-icon-theme

```

### Thunar 存档管理插件

Thunar 存档管理插件是类似于 File Roller，Ark，Xarchiver，它是文件存档管理软件的前端，为打开、解压提供了统一的接口。

#### 安装

```
# pacman -S thunar-archive-plugin

```

### Thunar 媒体标签插件

媒体标签插件会显示媒体文件的详细信息。它支持 ID3（MP3 文件格式的系统）和 Ogg/Vorbis 标签。它也包含重命名器（renamer？），允许编辑媒体标签。

#### 安装

```
# pacman -S thunar-media-tags-plugin

```

### Thunar Thumbnailers

The aim of the Thunar Thumbnailers project is to provide thumbnail generation for media formats that are neglected by other thumbnailers. If you want thumbnails and deal with media formats that are not compatible with other thumbnailers, use this. For a full list of supported formats, see the [project page](http://goodies.xfce.org/projects/thunar-plugins/thunar-thumbnailers/).

#### 安装

```
# pacman -S thunar-thumbnailers

```

### Thunar 共享

Thunar 共享插件允许你快速的通过 Samba 来共享一个文件夹并且无须 root 来进行访问。

#### 安装

在 [AUR](/index.php/AUR "AUR") 中安装 [thunar-shares-plugin](https://aur.archlinux.org/packages.php?ID=24152) 包。

#### 配置

使用 root 用户：

export 以下变量到环境中去用于接下来命令的执行：

```
 # export USERSHARES_DIR="/var/lib/samba/usershares"
 # export USERSHARES_GROUP="sambashare"

```

在 /var/lib/samba 中创建用户共享目录：

```
 # mkdir -p ${USERSHARES_DIR}

```

创建 sambashare 组：

```
 # groupadd ${USERSHARES_GROUP}

```

改变目录和组的所有者：

```
 # chown root:${USERSHARES_GROUP} ${USERSHARES_DIR}

```

改变 usershares 目录的权限，让 sambashare 组中的用户可以读、写、执行文件：

```
 # chmod 01770 ${USERSHARES_DIR}

```

使用你喜欢的文本编辑器（以 root 身份）创建文件 /etc/samba/smb.conf

```
 # joe /etc/samba/smb.conf

```

使用此 smb.conf 配置文件：

```
 #This is the main Samba configuration file. You should read the
 #smb.conf(5) manual page in order to understand the options listed
 #here. Samba has a huge number of configurable options (perhaps too
 #many!) most of which are not shown in this example
 #
 #For a step to step guide on installing, configuring and using samba, 
 # read the Samba-HOWTO-Collection. This may be obtained from:
 #  [http://www.samba.org/samba/docs/Samba-HOWTO-Collection.pdf](http://www.samba.org/samba/docs/Samba-HOWTO-Collection.pdf)
 #
 # Many working examples of smb.conf files can be found in the 
 # Samba-Guide which is generated daily and can be downloaded from: 
 #  [http://www.samba.org/samba/docs/Samba-Guide.pdf](http://www.samba.org/samba/docs/Samba-Guide.pdf)
 #
 # Any line which starts with a ; (semi-colon) or a # (hash) 
 # is a comment and is ignored. In this example we will use a #
 # for commentry and a ; for parts of the config file that you
 # may wish to enable
 #
 # NOTE: Whenever you modify this file you should run the command "testparm"
 # to check that you have not made any basic syntactic errors. 
 #
 [global]
   workgroup = WORKGROUP
   security = share
   server string = My Share
   load printers = yes
   log file = /var/log/samba/%m.log
   max log size = 50
   usershare path = /var/lib/samba/usershares
   usershare max shares = 100
   usershare allow guests = yes
   usershare owner only = yes

  #Windows Internet Name Serving Support Section:

  #WINS Support - Tells the NMBD component of Samba to enable it's WINS Server
 ;   wins support = yes

 # WINS Server - Tells the NMBD components of Samba to be a WINS Client
 #	Note: Samba can be either a WINS Server, or a WINS Client, but NOT both
 ;   wins server = w.x.y.z

 #WINS Proxy - Tells Samba to answer name resolution queries on
 # behalf of a non WINS capable client, for this to work there must be
 # at least one	WINS Server on the network. The default is NO.
 ;   wins proxy = yes

```

保存文件并且添加你的用户到 sambashares 组，替换下面的 "your_username" 为你的用户名：

```
 # usermod -a -G ${USERSHARES_GROUP} your_username

```

重启 Samba：

```
 # /etc/rc.d/samba restart

```

登出再登录。你现在可以在任何文件夹上点击右键属性中进行共享了。

让你的 samba 在系统启动时启动，添加 samba 到 `/etc/rc.conf` 中的 daemons 去。

更多的信息，访问 [Samba](/index.php/Samba "Samba") wiki 页面。

## 参考资料

*   [Thunar](http://thunar.xfce.org/index.html) 项目页面。
*   [Thunar Volume Manager](http://goodies.xfce.org/projects/thunar-plugins/thunar-volman) 项目页面。
*   [Thunar Archive Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin) 项目页面。
*   [Thunar Media Tags Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) 项目页面。
*   [Thunar Thumbnailers](http://goodies.xfce.org/projects/thunar-plugins/thunar-thumbnailers/) 项目页面。
*   [Thunar Shares Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin/) 项目页面。
*   插件：[list](http://goodies.xfce.org/projects/thunar-plugins/start)。