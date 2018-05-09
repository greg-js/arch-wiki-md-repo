相关文章

*   [Display Manager (简体中文)](/index.php/Display_Manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display Manager (简体中文)")

摘自 [XDM 手册页](http://www.xfree86.org/current/xdm.1.html):

	*Xdm 能为本地和远程服务器提供一系列图形显示功能。xdm的设计满足图形显示的基本要求并遵循开放组织标准(XDMCPX Display Manager Control Protocol)，即X显示管理协议。Xdm提供的功能与init, getty等以文本登录为主的程序相似:提供登录会话，获取用户名和密码，并将授权给予登录用户并提供工作会话。*

XDM 提供了一个简单而又直观的图形登录界面。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 定义会话](#.E5.AE.9A.E4.B9.89.E4.BC.9A.E8.AF.9D)
    *   [2.2 主题](#.E4.B8.BB.E9.A2.98)
        *   [2.2.1 壁纸](#.E5.A3.81.E7.BA.B8)
        *   [2.2.2 字体](#.E5.AD.97.E4.BD.93)
        *   [2.2.3 登录对话框位置](#.E7.99.BB.E5.BD.95.E5.AF.B9.E8.AF.9D.E6.A1.86.E4.BD.8D.E7.BD.AE)
        *   [2.2.4 删除徽标](#.E5.88.A0.E9.99.A4.E5.BE.BD.E6.A0.87)
    *   [2.3 多 X 会话和登录](#.E5.A4.9A_X_.E4.BC.9A.E8.AF.9D.E5.92.8C.E7.99.BB.E5.BD.95)
    *   [2.4 无密码登录](#.E6.97.A0.E5.AF.86.E7.A0.81.E7.99.BB.E5.BD.95)

## 安装

安装软件包 [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) 然后 [启用](/index.php/Enable "Enable") `xdm.service` 服务。

要使用 Arch Linux XDM 主题，可以安装软件包 [xdm-archlinux](https://www.archlinux.org/packages/?name=xdm-archlinux)，然后**不启用** `xdm.service`，而是启用 `xdm-archlinux.service`。

## 配置

### 定义会话

和 [GDM]] 或 [LightDM](/index.php/LightDM "LightDM") 等大部分 [显示管理器](/index.php/Display_manager "Display manager") 不同，XDM 不会从 `/usr/share/xsessions` 目录中的 .desktop 文件读取会话。XDM 没有会话菜单。XDM 会执行账号主目录下的 `.xsession` 文件。

例如要启动 xface，`~/.xsession` 应该是：

```
startxfce4

```

请确保 `.xsession` 文件可执行：

```
$ chmod 700 ~/.xsession

```

### 主题

详情请参考 xdm 手册，默认的配置文件位于 `/etc/X11/xdm/Xresources`,[xdm-archlinux](https://www.archlinux.org/packages/?name=xdm-archlinux) 主题的配置文件位于 `/etc/X11/xdm/archlinux/Xresources`。

#### 壁纸

可以使用 [qiv](https://www.archlinux.org/packages/?name=qiv) 设置 XDM 的壁纸:

*   安装 [qiv](https://www.archlinux.org/packages/?name=qiv)
*   创建一个文件夹用于存放图片。 (例如 `/root/backgrounds` 或者 `/usr/local/share/backgrounds`)
*   把图片放进文件夹

*   编辑 `/etc/X11/xdm/Xsetup_0`. 将 `xconsole` 修改为：

```
 /usr/bin/qiv -zr /root/backgrounds/*

```

#### 字体

编辑 `/etc/X11/xdm/Xresources`. 添加/替换 下面字段:

```
 xlogin**greetFont:  -adobe-helvetica-bold-o-normal--20-**-**-**-**-**-iso8859-1
 xlogin**font:       -adobe-helvetica-medium-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin**promptFont: -adobe-helvetica-bold-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin**failFont:   -adobe-helvetica-bold-r-normal--14-**-**-**-**-**-iso8859-1

```

#### 登录对话框位置

```
 xlogin*frameWidth: 1
 xlogin*innerFramesWidth: 1
 xlogin*logoPadding: 0
 xlogin*geometry:    300x175-0-0

```

#### 删除徽标

注释掉以下字段:

```
 #xlogin*logoFileName: /usr/X11R6/lib/X11/xdm/pixmaps/xorg.xpm
 #xlogin*logoFileName: /usr/X11R6/lib/X11/xdm/pixmaps/xorg-bw.xpm

```

### 多 X 会话和登录

启用 [XDMCP](/index.php/XDMCP "XDMCP") 后，可以在同一个机器上运行多个 X 会话：

```
# X -query ip_xdmcp_server :2

```

这将启动第二个会话，在窗口中需要 [xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr)

```
# Xephyr -query this_machine_ip :2

```

### 无密码登录

要启用 XDM 无密码登录，将下面内容加入 `/etc/X11/xdm/Xresources`:

```
xlogin*allowNullPasswd: true

```