## Contents

*   [1 Configuration Tips](#Configuration_Tips)
    *   [1.1 更好的视频性能](#.E6.9B.B4.E5.A5.BD.E7.9A.84.E8.A7.86.E9.A2.91.E6.80.A7.E8.83.BD)
    *   [1.2 添加或编辑 GDM 会话](#.E6.B7.BB.E5.8A.A0.E6.88.96.E7.BC.96.E8.BE.91_GDM_.E4.BC.9A.E8.AF.9D)
    *   [1.3 调整/etc/hosts](#.E8.B0.83.E6.95.B4.2Fetc.2Fhosts)
*   [2 Misc Tips](#Misc_Tips)
    *   [2.1 锁定屏幕](#.E9.94.81.E5.AE.9A.E5.B1.8F.E5.B9.95)
    *   [2.2 在登录时解锁gnome密匙环](#.E5.9C.A8.E7.99.BB.E5.BD.95.E6.97.B6.E8.A7.A3.E9.94.81gnome.E5.AF.86.E5.8C.99.E7.8E.AF)
    *   [2.3 GNOME Files Tips](#GNOME_Files_Tips)
        *   [2.3.1 改变浏览模式 (Spatial View)](#.E6.94.B9.E5.8F.98.E6.B5.8F.E8.A7.88.E6.A8.A1.E5.BC.8F_.28Spatial_View.29)
    *   [2.4 加速面板的自动隐藏](#.E5.8A.A0.E9.80.9F.E9.9D.A2.E6.9D.BF.E7.9A.84.E8.87.AA.E5.8A.A8.E9.9A.90.E8.97.8F)
    *   [2.5 GNOME Menu Tips](#GNOME_Menu_Tips)
        *   [2.5.1 加速菜单出现速度](#.E5.8A.A0.E9.80.9F.E8.8F.9C.E5.8D.95.E5.87.BA.E7.8E.B0.E9.80.9F.E5.BA.A6)
        *   [2.5.2 编辑菜单](#.E7.BC.96.E8.BE.91.E8.8F.9C.E5.8D.95)
            *   [2.5.2.1 用户菜单](#.E7.94.A8.E6.88.B7.E8.8F.9C.E5.8D.95)
            *   [2.5.2.2 用户组菜单, 系统菜单](#.E7.94.A8.E6.88.B7.E7.BB.84.E8.8F.9C.E5.8D.95.2C_.E7.B3.BB.E7.BB.9F.E8.8F.9C.E5.8D.95)
        *   [2.5.3 Custom Icon](#Custom_Icon)
*   [3 有用的附加功能](#.E6.9C.89.E7.94.A8.E7.9A.84.E9.99.84.E5.8A.A0.E5.8A.9F.E8.83.BD)
    *   [3.1 FAM](#FAM)
    *   [3.2 GNOME系统监视器](#GNOME.E7.B3.BB.E7.BB.9F.E7.9B.91.E8.A7.86.E5.99.A8)
    *   [3.3 在GNOME Files中烧录CD](#.E5.9C.A8GNOME_Files.E4.B8.AD.E7.83.A7.E5.BD.95CD)
    *   [3.4 GNOME系统工具](#GNOME.E7.B3.BB.E7.BB.9F.E5.B7.A5.E5.85.B7)
    *   [3.5 Gdesklets:桌面小部件](#Gdesklets:.E6.A1.8C.E9.9D.A2.E5.B0.8F.E9.83.A8.E4.BB.B6)
*   [4 其他应用程序](#.E5.85.B6.E4.BB.96.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [4.1 gnome-terminal](#gnome-terminal)
    *   [4.2 gedit](#gedit)
    *   [4.3 eog](#eog)
    *   [4.4 file-roller](#file-roller)
    *   [4.5 gcalctool](#gcalctool)
    *   [4.6 rhythmbox](#rhythmbox)
    *   [4.7 sound-juicer](#sound-juicer)
    *   [4.8 totem](#totem)
    *   [4.9 gimp](#gimp)
    *   [4.10 gftp](#gftp)
    *   [4.11 abiword](#abiword)
    *   [4.12 gnumeric](#gnumeric)
    *   [4.13 Leave message feature in gnome screensaver](#Leave_message_feature_in_gnome_screensaver)
    *   [4.14 DevilsPie](#DevilsPie)
*   [5 See also](#See_also)

## Configuration Tips

### 更好的视频性能

Some users report that, if they move the player window while playing a video file, a blue border appears around the video while it is moving. If you experience this, go to Desktop->Preferences->Multimedia Systems Selector, and under video change the "Default Sink" to "XWindows (No Xv)". When you click test, the blue border should be gone and on the whole, video should perform better.

注意: 这已经不适合于 Gnome 2.20 或以后的版本。([Evanlec](/index.php/User:Evanlec "User:Evanlec"))

### 添加或编辑 GDM 会话

GDM 的会话配置文件存放在 /etc/X11/sessions 文件夹下，以_.desktop_为后缀。你可以新建一个会话配置文件或编辑现有的会话配置文件，**下面以添加一个名叫mysession的新会话为例**。 复制一个已存在的 *.desktop 文件来新建会话：

```
cd /etc/X11/sessions
cp gnome.desktop mysession.desktop

```

使用编辑器打开这个新的配置文件

```
nano mysession.desktop

```

现在，你可以使用 GDM 来登录这个新的会话了。

### 调整/etc/hosts

如果你的 gnome 程序运行缓慢，可能是你没有正确设定/etc/hosts文件。一个正确的/etc/hosts文件应该包含以下内容：

```
127.0.0.1       localhost.localdomain     localhost      YOURHOSTNAME

```

注意到最后面的 _YOURHOSTNAME_ 吗？你需要在这添加上你的主机名，主机名可以通过运行 /bin/hostname 命令查看。

更多的信息可以查看： [Configuring_network](/index.php/Configuring_network "Configuring network")

## Misc Tips

### 锁定屏幕

安装 xscreensaver

```
pacman -S xscreensaver

```

1.  进入 桌面 -> 配置 -> 屏幕保护
2.  启用一个或多个屏幕保护
3.  即刻开始锁定屏幕，直到输入用户密码才能解除锁定。

**或者**可以安装 gnome-screensaver

```
pacman -S gnome-screensaver

```

### 在登录时解锁gnome密匙环

在 /etc/pam.d/gdm 最后加入如下几行:

```
auth            optional        pam_gnome_keyring.so
session         optional        pam_gnome_keyring.so  auto_start

```

在 /etc/pam.d/gnome-screensaver 中加入:

```
auth        optional     pam_gnome_keyring.so

```

在 /etc/pam.d/passwd 中加入:

```
password        optional        pam_gnome_keyring.so

```

[http://live.gnome.org/GnomeKeyring/Pam](http://live.gnome.org/GnomeKeyring/Pam)

**更简单的方法：** 安装 seahorse 这个包，一个很好的GUI程序，可以方便的设置登录时解锁gnome密匙环，安装后点击"系统 -> 附件 -> 授权 "打开。

### GNOME Files Tips

如何快速的定位到位置栏？ 只需要按：

```
control + L

```

#### 改变浏览模式 (Spatial View)

1.  确保已经安装了gconf-editor（配置编辑器），打开它
2.  定位到 _apps/nautilus/preferences_
3.  在 _always_use_browser_ 值后面打勾

**或者：**

1.  点击 _Files_ 的 _编辑_ >> _首选项_
2.  定位到 _行为_ 标签
3.  在 _总是在浏览器窗口中打开_ 前打勾

### 加速面板的自动隐藏

如果你使用面板功能里的 _自动隐藏_ 功能，但发现需要太长的时间来出现/消失，可以试试这个：

1.  打开 gconf-editor（配置编辑器）
2.  定位到 _/apps/panel/global_
3.  设置 _panel_hide_delay_ 和 _panel_show_delay_ 到一个合适的数值，数值越低速度越快，数值的单位为毫秒。

### GNOME Menu Tips

#### 加速菜单出现速度

可以使用下面的命令来移除GNOME菜单的延时：

```
echo "gtk-menu-popup-delay = 0" >> ~/.gtkrc-2.0

```

或者添加值 _gtk-menu-popup-delay = 0_ 到 _~/.gtkrc-2.0_ 文件下

#### 编辑菜单

大多数 Gnome 用户总是抱怨菜单问题。 如编辑菜单的形式和权限，或多用户使用各自的菜单。

##### 用户菜单

(提示: 这个可能已经过时。从gnome 2.14 开始已经拥有自己的菜单编辑器（部分功能，确实只有部分功能，所以在 gnome 自带全功能的菜单编辑器之前，这种方式还是有效的。）

作为一名用户，应该在桌面建立程序的快捷方式。一旦成功创建并测试成功，启动 GNOME Files 文件管理器并在地址栏输入 `applications:///` 。创建你自己的菜单组，把你所创建的程序快捷键放在这里。如此，你将在主菜单上看到你所想要的菜单组及新的程序快捷键。

或者安装 Alacarte，它能够方便的通过图形界面的方式创建，变更和移除菜单:

```
pacman -S alacarte

```

##### 用户组菜单, 系统菜单

你会发现gnome 菜单都是如 'appname.desktop' 的形式存在于 /usr/share/gnome/share/applications下。

*   编辑其中的一个直到适合你的新程序为止，然后保存。
*   使之能让所有用户使用
    你需要让文件的权限变为 644 (管理员: rw 组: r 其他: r), 所以所有的用户都可以使用。
*   使之能让一个组或者单个用户使用
    你需要设置文件不同的权限; 例如只让一个组或者单个用户使用。

这是一个 Scite 菜单的样例:

```
[Desktop Entry]
Encoding=UTF-8
Name=SciTE
Comment=SciTE editor
Type=Application
Exec=/usr/bin/scite
Icon=/usr/share/pixmaps/scite_48x48.png
Terminal=false
Categories=GNOME;Application;Development;
StartupNotify=true

```

提示: gnome 菜单下的文件夹:

当你在 applications:/// 下创建一个文件夹，并且希望改变它的图标 - 右击，选择 “编辑启动器” 并更换图标。如果你右击并选择“属性”然后改变图标的话，不会在菜单中显示新的图标。

#### Custom Icon

This is a quick guide on changing the gnome "foot" icon of your main menu to the icon of your choice.

*   Open the configuration editor in gnome (it should be in System Tools of your main menu) or run `gconf-editor`
*   In the configuration editor go to apps > panel > objects > find the object for your menu (an easy way to spot the correct object is that it will have "Main Menu" in the tool tip section).
*   Set the path to your icon in the "Custom_Icon" field.
*   Check "Use_Custom_Icon" a little ways down.
*   To see the change without having to restart X, open a terminal window and type:

```
killall gnome-panel

```

## 有用的附加功能

### FAM

FAM allows gnome to do such useful things as automatically update the menu when new applications are installed, and refresh GNOME Files when a directory it is viewing is changed.

See the [FAM Wiki](/index.php/FAM "FAM") for instructions on how to install it.

### GNOME系统监视器

安装后会出现一个 _系统监视器_ 程序，用于显示处理器/内存/交换分区和所有正在运行的应用程序等信息。它并不会在默认安装桌面时安装，所以必须单独安装来使用它：

```
pacman -Sy gnome-system-monitor

```

### 在GNOME Files中烧录CD

```
pacman -Sy nautilus-cd-burner

```

### GNOME系统工具

这将增加了若干个菜单项到 _系统_ => _系统管理_ 下，有 _用户管理_，_日期和时间_，_网络_，_服务_，_共享文件夹_。更多的可以查看： [Gnome documentation](http://www.gnome.org/projects/gst/).

```
pacman -Sy gnome-system-tools

```

需要注意 pacman 安装完成时返回的信息。要使用这些功能，需要将你的用户加入到 _stb-admin_ 组中：

```
gpasswd -a USER_NAME stb-admin

```

启动stbd

```
/etc/rc.d/stbd start

```

### Gdesklets:桌面小部件

可以添加时钟，日历，天气预报等到你的桌面上

```
pacman -S gdesklets

```

你能从这里找到更多的小部件 [gdesklets.org](http://www.gdesklets.de/?q=desklet/browse)。 To install them, download the files. Next, in the Gnome menu, open Applications->Accessories->gDesklets. When the gDesklets Shell appears, drag the new gdesklet file onto the shell. If you want gdesklets to load when you log in, click on the Gnome menu under System->Preferences->Sessions. Choose "Startup Programs", click "add", and type in the data. The command should be /usr/bin/gdesklets. You can always find such a path by typing "whereis gdesklets".

## 其他应用程序

这些都是一些很好的应用程序，可以使用下面的命令全部安装：

```
pacman -Sy gnome-extra

```

这是一个组，如果里面包含了你不需要的包，可以很容易的选择不下载。

### gnome-terminal

GNOME默认的终端程序，你应该在你第一次登录GNOEM前安装，除非你更喜欢使用 [xterm](/index.php/Xterm "Xterm")。

### gedit

具有语法突出显示模式的多功能文本编辑器。

### eog

Eye-of-Gnome，一个轻量级、快速和小巧的图像浏览器，可以调整照片大小和旋转照片。

### file-roller

归档管理器，支持许多格式。需要安装 _unrar_，_unzip_，_p7zip_ 来分别支持rar，zip和7z格式。

```
pacman -Sy unrar unzip p7zip

```

### gcalctool

一个功能强大的计算器。

### rhythmbox

一个类似于iTunes的音乐播放器。

### sound-juicer

CD Ripper, integrates with rhythmbox.

_To enable default mp3 profiles in preferences menu:_

```
pacman -S gstreamer0.10-lame gstreamer0.10-taglib

```

Note: This should not be necessary anymore, since these packages now are included in gstreamer0.10-ugly-plugins and gstreamer0.10-good-plugins.

_If you're having other problems with SoundJuicer , click [here](/index.php/User:Munk3h "User:Munk3h")_

### totem

一个使用gstreamer后端或xine后端的电影播放器。

### gimp

被称为linux上的Photoshop，并且还是开源的。

### gftp

一个支持多线程FTP客户端。

### abiword

一个小巧、快速和兼容 .doc 文档的文字编辑器。

### gnumeric

一个类似于excel的电子表格编辑器。

### Leave message feature in gnome screensaver

This is a cool feature provided by gnome-screensaver 2.20, somebody can leave a message for you when you are not at your desk. Please install notification-daemon to make this work.

### DevilsPie

A very useful application that can be run as a daemon within gnome. It manipulates windows allowing you to start programs on a desired desktop or in a size of your choice among many other things. Brings a whole new level of control into the metacity engine. There's a pretty good HOWTO on their [homepage](http://live.gnome.org/DevilsPie),

## See also

*   [GNOME_(简体中文)](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")