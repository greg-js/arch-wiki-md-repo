Related articles

*   [LXDE_(简体中文)](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)")
*   [Openbox_(简体中文)](/index.php/Openbox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Openbox (简体中文)")
*   [File manager functionality_(简体中文)](/index.php/File_manager_functionality_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File manager functionality (简体中文)")
*   [SpaceFM](/index.php/SpaceFM "SpaceFM")
*   [Thunar_(简体中文)](/index.php/Thunar_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Thunar (简体中文)")
*   [GNOME Files](/index.php/GNOME_Files "GNOME Files")
*   [Nemo](/index.php/Nemo "Nemo")

**翻译状态：** 本文是英文页面 [PCManFM](/index.php/PCManFM "PCManFM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-07，点击[这里](https://wiki.archlinux.org/index.php?title=PCManFM&diff=0&oldid=495212)可以查看翻译后英文页面的改动。

[PCManFM](https://wiki.lxde.org/en/PCManFM) 是一个开源的文件管理器，并且是 [LXDE](/index.php/LXDE "LXDE")的默认文件管理器。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 桌面管理](#.E6.A1.8C.E9.9D.A2.E7.AE.A1.E7.90.86)
    *   [2.1 桌面首选项](#.E6.A1.8C.E9.9D.A2.E9.A6.96.E9.80.89.E9.A1.B9)
    *   [2.2 新建图标](#.E6.96.B0.E5.BB.BA.E5.9B.BE.E6.A0.87)
*   [3 守护进程模式](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E6.A8.A1.E5.BC.8F)
*   [4 开机自启](#.E5.BC.80.E6.9C.BA.E8.87.AA.E5.90.AF)
*   [5 额外特色与功能](#.E9.A2.9D.E5.A4.96.E7.89.B9.E8.89.B2.E4.B8.8E.E5.8A.9F.E8.83.BD)
*   [6 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [6.1 为其他文件生成缩略图](#.E4.B8.BA.E5.85.B6.E4.BB.96.E6.96.87.E4.BB.B6.E7.94.9F.E6.88.90.E7.BC.A9.E7.95.A5.E5.9B.BE)
    *   [6.2 设置终端模拟器](#.E8.AE.BE.E7.BD.AE.E7.BB.88.E7.AB.AF.E6.A8.A1.E6.8B.9F.E5.99.A8)
    *   [6.3 集成归档管理器](#.E9.9B.86.E6.88.90.E5.BD.92.E6.A1.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [6.4 创建模板](#.E5.88.9B.E5.BB.BA.E6.A8.A1.E6.9D.BF)
*   [7 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [7.1 启动窗口空白](#.E5.90.AF.E5.8A.A8.E7.AA.97.E5.8F.A3.E7.A9.BA.E7.99.BD)
    *   [7.2 无 "Applications"](#.E6.97.A0_.22Applications.22)
    *   [7.3 无图标](#.E6.97.A0.E5.9B.BE.E6.A0.87)
    *   [7.4 无 "上一/下一 文件夹"](#.E6.97.A0_.22.E4.B8.8A.E4.B8.80.2F.E4.B8.8B.E4.B8.80_.E6.96.87.E4.BB.B6.E5.A4.B9.22)
    *   [7.5 --desktop parameter not working or crashing X-server](#--desktop_parameter_not_working_or_crashing_X-server)
    *   [7.6 终端模拟器的高级配置无法保存](#.E7.BB.88.E7.AB.AF.E6.A8.A1.E6.8B.9F.E5.99.A8.E7.9A.84.E9.AB.98.E7.BA.A7.E9.85.8D.E7.BD.AE.E6.97.A0.E6.B3.95.E4.BF.9D.E5.AD.98)
    *   [7.7 Make PCManFM remember your preferred Sort Files settings](#Make_PCManFM_remember_your_preferred_Sort_Files_settings)
    *   [7.8 挂载驱动时候提醒"Not authorized"](#.E6.8C.82.E8.BD.BD.E9.A9.B1.E5.8A.A8.E6.97.B6.E5.80.99.E6.8F.90.E9.86.92.22Not_authorized.22)
    *   [7.9 Operation not supported](#Operation_not_supported)

## 安装

从仓库中选择 [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) [安装](/index.php/%E5%AE%89%E8%A3%85 "安装")，如果想安装gtk3版本，选择 [pcmanfm-gtk3](https://www.archlinux.org/packages/?name=pcmanfm-gtk3)；如果想安装开发版，选择 [pcmanfm-git](https://aur.archlinux.org/packages/pcmanfm-git/)。 推荐安装[gvfs](https://www.archlinux.org/packages/?name=gvfs)以提供回收站功能；推荐安装 [udisks](/index.php/Udisks "Udisks") 实现远程文件系统的挂载支持。

如果你想安装[Qt](/index.php/Qt "Qt")版本，可以选择 [pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt) 或 [pcmanfm-qt-git](https://aur.archlinux.org/packages/pcmanfm-qt-git/).

## 桌面管理

使用如下命令，能够使用PCManFM进行桌面管理，比设置壁纸，桌面图标等：

```
pcmanfm --desktop

```

原生的桌面管理菜单会被PCManFM提供的桌面管理菜单所替换。但是，只需要在桌面右击，选择 `桌面偏好设置`，在 `高级`选项卡中选择 `右击时选择窗口管理器提供的菜单`，即可还原。或者在命令行中输入：

```
pcmanfm --desktop-off

```

即可关闭

### 桌面首选项

如果你使用的是原生的桌面管理器，只要输入下面命令就能进入修改桌面配置

```
$ pcmanfm --desktop-pref

```

可以考虑把这句命令添加快捷键等方式，以方便使用。

### 新建图标

User content such as text files, documents, images and so forth can be dragged and dropped directly onto the desktop. To create shortcuts for applications it will be necessary to copy their `.desktop` files to the `~/Desktop` directory itself. Do not drag and drop the files there as they will be moved completely. The syntax of the command to do so is:

```
cp /usr/share/applications/<name of application>.desktop ~/Desktop

```

For example - where installed - to create a desktop shortcut for [lxterminal](https://www.archlinux.org/packages/?name=lxterminal), the following command would be used:

```
cp /usr/share/applications/lxterminal.desktop ~/Desktop

```

For those who used the [XDG user directories](/index.php/XDG_user_directories "XDG user directories") program to create their `$HOME` directories no further configuration will be required.

## 守护进程模式

如果你想在后台运行PCManFM ( 比如说要自动挂载移动硬盘等可移动介质)，使用：

```
pcmanfm -d

```

如果自动挂载失败，请参见 [udisks](/index.php/Udisks "Udisks").

## 开机自启

How PCManFM may be autostarted as a [daemon](/index.php/Daemon "Daemon") process or to manage the desktop for a standalone [window manager](/index.php/Window_manager "Window manager") will depend on the window manager itself. For example, to enable management of the desktop for [Openbox](/index.php/Openbox "Openbox"), the following command would be added to the `~/.config/openbox/autostart` file:

```
pcmanfm --desktop &

```

Review the relevant wiki article and/or official home page for a particular installed or intended window manager. Should a window manager not provide an autostart file, PCManFM may be alternatively autostarted by editing one or both of the following files:

*   [xinitrc](/index.php/Xinitrc "Xinitrc"): When using the [SLiM](/index.php/SLiM "SLiM") [display manager](/index.php/Display_manager "Display manager") or [Startx](/index.php/Startx "Startx") command
*   [xprofile](/index.php/Xprofile "Xprofile"): When using a display manager such as [LXDM](/index.php/LXDM "LXDM") or [LightDM](/index.php/LightDM "LightDM")

## 额外特色与功能

Less experienced users should be aware that a file manager alone - especially when installed in a standalone [Window manager](/index.php/Window_manager "Window manager") such as [Openbox](/index.php/Openbox "Openbox") - will not provide the features and functionality users of full desktop environments such as [Xfce](/index.php/Xfce "Xfce") and [KDE](/index.php/KDE "KDE") will be accustomed to. Review the [file manager functionality](/index.php/File_manager_functionality "File manager functionality") article for further information.

## 提示与技巧

### 为其他文件生成缩略图

PCManFM supports image thumbnails out of the box. However, in order to view thumbnails of other file types, PCManFM uses the information provided in the files located at `/usr/share/thumbnailers`. The packages which provide a thumbnailer usually add the corresponding *.thumbnail* file at `/usr/share/thumbnailers`. For example, in order to get thumbnails for OpenDocument files, you may install [libgsf](https://www.archlinux.org/packages/?name=libgsf) from the official repositories. For video files' thumbnails, the package [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer) is required. For PDF files, you may install [evince](https://www.archlinux.org/packages/?name=evince) from the official repositories, which provides `evince-thumbnailer` and the corresponding file at `/usr/share/thumbnailers`. However, if you prefer not to install `evince`, you can also replicate the functionality of `evince-thumbnailer` using [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)'s `convert` command. This is accomplished by creating a new file with the *.thumbnailer* extension (e.g.: `imagemagick-pdf.thumbnailer`) at `/usr/share/thumbnailers` with the following content:

```
  [Thumbnailer Entry]
  TryExec=convert
  Exec=convert %i[0] -thumbnail %s %o
  MimeType=application/pdf;application/x-pdf;image/pdf;

```

**Note:** The *[0]* next to the input file is specified so that `convert` only generates a thumbnail of the first page. This is a `convert`-specific syntax and has nothing to do with the syntax of the thumbnailers' files.

Following this example, you can specify custom thumbnailers by creating your own *.thumbnail* files. Keep in mind that `%i` refers to the input file (the file which will have its thumbnail made), `%o` to the output file (the thumbnail image) and `%s` to the size of the thumbnail. These parameters will be automatically substituted with the corresponding data and passed to the thumbnailer program by PCManFM.

**Tip:** If you only get thumbnails of certain files and not of all the files of the same type try increasing the maximum file size of the files that get a thumbnail at *Edit > Preferences > Display*.

### 设置终端模拟器

You can configure what terminal emulator PCManFM should use for *Tools > Open Current Folder in Terminal* under *Edit > Preferences > Advanced* e.g. `bash -c 'pantheon-terminal --working-directory "$PWD"'`.

### 集成归档管理器

可以在*编辑 > 偏好设置 > 高级* 中设置集成的归档管理器。目前 PCManFM 支持 [file-roller](https://www.archlinux.org/packages/?name=file-roller), [xarchiver](https://www.archlinux.org/packages/?name=xarchiver) (或者 [xarchiver-gtk2](https://www.archlinux.org/packages/?name=xarchiver-gtk2)), [engrampa](https://www.archlinux.org/packages/?name=engrampa), [ark](https://www.archlinux.org/packages/?name=ark) 和 [squeeze-git](https://aur.archlinux.org/packages/squeeze-git/)。

### 创建模板

模板文件保存在 `~/Templates` ，点击*文件>新建...*可以选择相应的模板

## 故障排除

### 启动窗口空白

如果你启动应用时，界面一片空白，那么你可以试着卸载 [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) 然后安装 [lxmenu-data](https://www.archlinux.org/packages/?name=lxmenu-data)。此外，设置如下环境变量：

```
export XDG_MENU_PREFIX=lxde-
export XDG_CURRENT_DESKTOP=LXDE

```

### 无 "Applications"

You can try this method: Delete all files in the `$HOME/.cache/menus` directory, and run PCManFM again.

PCManFM requires the environment variable *XDG_MENU_PREFIX* to be set. The value of the variable should match the beginning of a file present in the `/etc/xdg/menus/` directory. E.g. you can set the value in your `.xinitrc` file with the line:

```
export XDG_MENU_PREFIX="lxde-"

```

See these threads for more informations: [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1110903), and especially this post from the Linux Mint forums: [[2]](http://forums.linuxmint.com/viewtopic.php?f=175&t=53986#p501920)

### 无图标

If you are using a [window manager](/index.php/Window_manager "Window manager") instead of a [desktop environment](/index.php/Desktop_environment "Desktop environment") and you have no icons for folders and files, specify a GTK+ icon theme.

If you have e.g. [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons) installed, edit `~/.gtkrc-2.0` **or** `/etc/gtk-2.0/gtkrc` and add the following line:

```
gtk-icon-theme-name = "oxygen"

```

**Note:** All instances of PCManFM have to be restarted for changes to apply!

Else, use an different one (*gnome*, *hicolor*, and *locolor* do not work). To list all installed icon themes:

```
$ ls ~/.icons/ /usr/share/icons/

```

If none of them is suitable, install one. To list all installable icon packages:

```
$ pacman -Ss icon-theme

```

**Tip:** For an alternative GUI solution, install [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) and apply an icon theme from there.

### 无 "上一/下一 文件夹"

A method to fix this is with [Xbindkeys](/index.php/Xbindkeys "Xbindkeys").

Install [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys), [xvkbd](https://aur.archlinux.org/packages/xvkbd/) and edit `~/.xbindkeysrc` to contain the following:

```
# Sample .xbindkeysrc for a G9x mouse.
"/usr/bin/xvkbd -text '\[Alt_L]\[Left]'"
 b:8
"/usr/bin/xvkbd -text '\[Alt_L]\[Right]'"
 b:9

```

Actual button codes can be obtained with package [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev).

Add:

```
xbindkeys &

```

to your `~/.xinitrc` to execute xbindkeys on log-in.

### --desktop parameter not working or crashing X-server

Make sure you have ownership and write permissions on `~/.config/pcmanfm`.

Setting the wallpaper either by using the `--desktop-pref` parameter or editing `~/.config/pcmanfm/default/pcmanfm.config` solves the problem.

### 终端模拟器的高级配置无法保存

Make sure you have rights on libfm configuration file:

```
$ chmod -R 755 ~/.config/libfm
$ chmod 644 ~/.config/libfm/libfm.conf

```

### Make PCManFM remember your preferred Sort Files settings

You can use *View > Sort Files* to change the order in which PCManFM lists the files, but PCManFM won't remember that the next time you start it. To make it remember, go to *Edit > Preferences* and close. That will write your current sort_type and sort_by values into `~/.config/pcmanfm/LXDE/pcmanfm.conf`.

### 挂载驱动时候提醒"Not authorized"

Make this [polkit](/index.php/Polkit "Polkit") rule in `/etc/polkit-1/rules.d/00-mount-internal.rules`:

```
polkit.addRule(function(action, subject) {
   if ((action.id == "org.freedesktop.udisks2.filesystem-mount-system" &&
      subject.local && subject.active && subject.isInGroup("storage")))
      {
         return polkit.Result.YES;
      }
});

```

And add your user to storage group:

```
# usermod -aG storage username

```

### Operation not supported

See the General troubleshooting article on [Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").