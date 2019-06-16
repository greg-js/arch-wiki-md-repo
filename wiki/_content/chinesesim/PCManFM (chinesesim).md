Related articles

*   [LXDE_(简体中文)](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)")
*   [Openbox_(简体中文)](/index.php/Openbox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Openbox (简体中文)")
*   [File manager functionality_(简体中文)](/index.php/File_manager_functionality_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File manager functionality (简体中文)")
*   [SpaceFM](/index.php/SpaceFM "SpaceFM")
*   [Thunar_(简体中文)](/index.php/Thunar_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Thunar (简体中文)")
*   [GNOME Files](/index.php/GNOME_Files "GNOME Files")
*   [Nemo](/index.php/Nemo "Nemo")

**翻译状态：** 本文是英文页面 [PCManFM](/index.php/PCManFM "PCManFM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-05-06，点击[这里](https://wiki.archlinux.org/index.php?title=PCManFM&diff=0&oldid=570432)可以查看翻译后英文页面的改动。

[PCManFM](https://wiki.lxde.org/en/PCManFM) 是一个开源的文件管理器，并且是 [LXDE](/index.php/LXDE "LXDE")的默认文件管理器。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 桌面管理](#桌面管理)
    *   [2.1 桌面首选项](#桌面首选项)
    *   [2.2 新建图标](#新建图标)
*   [3 守护进程模式](#守护进程模式)
*   [4 开机自启](#开机自启)
*   [5 其他特性和功能](#其他特性和功能)
*   [6 提示与技巧](#提示与技巧)
    *   [6.1 为其他文件生成缩略图](#为其他文件生成缩略图)
    *   [6.2 设置终端模拟器](#设置终端模拟器)
    *   [6.3 集成压缩包管理器](#集成压缩包管理器)
    *   [6.4 “创建新的...”模板](#“创建新的...”模板)
*   [7 故障排除](#故障排除)
    *   [7.1 启动窗口空白](#启动窗口空白)
    *   [7.2 没有 "Applications"](#没有_"Applications")
    *   [7.3 无图标](#无图标)
    *   [7.4 鼠标按钮不能触发 "上一/下一 文件夹" 功能](#鼠标按钮不能触发_"上一/下一_文件夹"_功能)
    *   [7.5 --desktop 参数不生效或使X-server崩溃](#--desktop_参数不生效或使X-server崩溃)
    *   [7.6 终端模拟器的高级配置没有保存](#终端模拟器的高级配置没有保存)
    *   [7.7 记住文件排序设置](#记住文件排序设置)
    *   [7.8 挂载设备时候提醒 "Not authorized"](#挂载设备时候提醒_"Not_authorized")
    *   [7.9 Operation not supported](#Operation_not_supported)

## 安装

有以下版本可供选择[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")：

*   [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)
*   [pcmanfm-gtk3](https://www.archlinux.org/packages/?name=pcmanfm-gtk3)：gtk3版本
*   [pcmanfm-git](https://aur.archlinux.org/packages/pcmanfm-git/)：开发版
*   [pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt)或[pcmanfm-qt-git](https://aur.archlinux.org/packages/pcmanfm-qt-git/)：[Qt](/index.php/Qt "Qt")版本

可选组件：

*   [gvfs](https://www.archlinux.org/packages/?name=gvfs)：提供回收站功能
*   [udisks](/index.php/Udisks "Udisks")：远程文件系统的挂载支持

## 桌面管理

如果要用PCManFM进行桌面管理，比如设置壁纸和桌面图标，使用这个命令：

```
pcmanfm --desktop

```

原生的桌面管理菜单会被PCManFM提供的桌面管理菜单所替换。

如果要还原，只需要在桌面右击，选择 `桌面偏好设置`(`Desktop preferences`)，在 `高级`(`Desktop`)选项卡中选择 `右击时选择窗口管理器提供的菜单`(`Right click shows WM menu`)。或者在命令行中输入：

```
pcmanfm --desktop-off

```

### 桌面首选项

如果你使用的是窗口管理器提供的原生桌面菜单，只要输入下面命令就能进入修改桌面配置：

```
$ pcmanfm --desktop-pref

```

可以考虑把这句命令绑定快捷键或绑定到原生桌面菜单以方便使用。

### 新建图标

文本文档、图片等用户文件可以直接拖放到桌面上。至于应用程序快捷方式，需要把它们的`.desktop`文件**复制**到`~/Desktop`文件夹；不能拖放`.desktop`文件，否则就会是移动而不是复制，这会导致这个应用从应用启动器中消失。如果用命令行就应该是这样：

```
cp /usr/share/applications/<name of application>.desktop ~/Desktop

```

例如，下面的命令为 [lxterminal](https://www.archlinux.org/packages/?name=lxterminal) 创建了一个桌面快捷方式：

```
cp /usr/share/applications/lxterminal.desktop ~/Desktop

```

使用 [XDG user directories](/index.php/XDG_user_directories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "XDG user directories (简体中文)") 程序创建 `$HOME` 目录的用户不需要再做其他配置。

## 守护进程模式

如果你想在后台运行PCManFM ( 比如说要自动挂载移动硬盘等可移动介质)，使用：

```
pcmanfm -d

```

如果自动挂载失败，请参见 [udisks](/index.php/Udisks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udisks (简体中文)").

## 开机自启

PCManFM如何作为[daemon](/index.php/Daemon "Daemon")进程自动启动或为一个独立的[window manager](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)")管理桌面取决于窗口管理器本身。

例如，如果要它为 [Openbox](/index.php/Openbox "Openbox") 管理桌面，要把下面的命令加入到 `~/.config/openbox/autostart` 文件：

```
pcmanfm --desktop &

```

对于特定的窗口管理器，请查看相关的维基文档或者官方主页来了解详情。如果该窗口管理器没有提供 autostart 文件，则可以编辑以下的文件来自动启动 PCManFM：

*   [xinitrc](/index.php/Xinitrc "Xinitrc"): 如果使用的是 [SLiM](/index.php/SLiM "SLiM") [display manager](/index.php/Display_manager "Display manager") 或者 [Startx](/index.php/Startx "Startx") 命令
*   [xprofile](/index.php/Xprofile "Xprofile"): 如果使用的是诸如 [LXDM](/index.php/LXDM "LXDM") 、 [LightDM](/index.php/LightDM "LightDM")之类的 [display manager](/index.php/Display_manager "Display manager")

## 其他特性和功能

新手用户应该意识到，PCManFM只是一个文件管理器，它并不会像 [Xfce](/index.php/Xfce "Xfce") 和 [KDE](/index.php/KDE "KDE") 这种完整的 [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)") 一样提供众多特性和功能。阅读 [file manager functionality](/index.php/File_manager_functionality "File manager functionality") 来了解文件管理器应该做什么的信息。

## 提示与技巧

### 为其他文件生成缩略图

PCManFM 对图片文件可以自动生成缩略图。对于其他文件类型，PCManFM 使用 `/usr/share/thumbnailers` 文件夹里的文件所提供的信息来产生缩略图。提供缩略图生成器(thumbnailers)的软件包通常会在 `/usr/share/thumbnailers` 自动添加 *.thumbnailer* 文件。例如：

*   [libgsf](https://www.archlinux.org/packages/?name=libgsf)：提供OpenDocument文件的thumbnailer
*   [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer)：视频文件的
*   [evince](https://www.archlinux.org/packages/?name=evince)：PDF文件的

**Tip:** 如果你不喜欢 `evince`，可以用 [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) 的 `convert` 命令来生成PDF文件的缩略图，需要在 `/usr/share/thumbnailers` 创建一个 *.thumbnailer* 后缀名的文件，内容如下： `/usr/share/thumbnailers/imagemagick-pdf.thumbnailer` 
```
[Thumbnailer Entry]
TryExec=convert
Exec=convert %i[0] -thumbnail %s %o
MimeType=application/pdf;application/x-pdf;image/pdf;
```

**Note:** *Exec* 里的 *[0]* 是为了让 `convert` 按照 PDF 的第一页生成缩略图。这是 `convert` 接受的参数，和 *.thumbnailer* 文件的语法没有任何关系。

同理，你可以创建其他的 *.thumbnailer* 文件来给某种文件生成缩略图。基本的语法是：`%i` 指需要生成缩略图的文件， `%o` 指生成的缩略图文件，`%s`指缩略图的大小。这三个参数会在传递给缩略图生成器之前被替换成相应的数据。

**Tip:** 如果只有同类型的文件只有一部分生成了缩略图，你可能需要调整可以有缩略图的文件的最大大小，在 *Edit > Preferences > Display* 里调整。

### 设置终端模拟器

在 *Edit > Preferences > Advanced* 里面的 *Tools > Open Current Folder in Terminal*，你可以配置 PCManFM 调用的终端模拟器。

### 集成压缩包管理器

可以在 *Edit > Preferences > Advanced* 中设置集成的压缩包管理器。目前 PCManFM 支持 [file-roller](https://www.archlinux.org/packages/?name=file-roller), [xarchiver](https://www.archlinux.org/packages/?name=xarchiver) (或者 [xarchiver-gtk2](https://www.archlinux.org/packages/?name=xarchiver-gtk2)), [engrampa](https://www.archlinux.org/packages/?name=engrampa), [ark](https://www.archlinux.org/packages/?name=ark) 和 [squeeze-git](https://aur.archlinux.org/packages/squeeze-git/)。

### “创建新的...”模板

模板文件保存在 `~/Templates` ，点击*文件>新建...*可以选择相应的模板。默认的模板是“创建文件夹”和“创建空白文件”。

## 故障排除

### 启动窗口空白

如果你启动应用时，界面一片空白，那么你可以试着卸载 [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) 然后安装 [lxmenu-data](https://www.archlinux.org/packages/?name=lxmenu-data)。此外，设置如下环境变量：

```
export XDG_MENU_PREFIX=lxde-
export XDG_CURRENT_DESKTOP=LXDE

```

### 没有 "Applications"

删掉 `$HOME/.cache/menus` 文件夹里的东西，然后重新运行 PCManFM。

*XDG_MENU_PREFIX* 这个环境变量需要设置好，它的值应该和 `/etc/xdg/menus/` 目录里的文件的文件名的开头部分匹配。可以通过 `.xinitrc` 文件设置这个环境变量，例如：

```
export XDG_MENU_PREFIX="lxde-"

```

参考[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1110903) 以及Linux Mint论坛的[[2]](http://forums.linuxmint.com/viewtopic.php?f=175&t=53986#p501920)（特别推荐）

### 无图标

如果你用的是 [window manager](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)") 而不是 [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")，而文件夹和文件没有图标，你需要指定 GTK+ 图标主题。

例如，你安装了 [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons)，在 `~/.gtkrc-2.0` **或者** `/etc/gtk-2.0/gtkrc` 里添加这一行：

```
gtk-icon-theme-name = "oxygen"

```

**Note:** 重启 PCManFM 才能生效。

设置成还没有安装的图标主题是没用的。用下面这个命令查看安装了的图标主题：

```
$ ls ~/.icons/ /usr/share/icons/

```

如果看着都不爽，那就用这个命令查看所有可以安装的图标主题，选一个来安装：

```
$ pacman -Ss icon-theme

```

**Tip:** 如果想要有个图形界面，安装 [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) 并用它来设置图标主题。

### 鼠标按钮不能触发 "上一/下一 文件夹" 功能

用 [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") 来搞定这个功能。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys)、[xvkbd](https://aur.archlinux.org/packages/xvkbd/)，在 `~/.xbindkeysrc` 里添加以下内容：

 `~/.xbindkeysrc` 
```
# Sample .xbindkeysrc for a G9x mouse.
"/usr/bin/xvkbd -text '\[Alt_L]\[Left]'"
 b:8
"/usr/bin/xvkbd -text '\[Alt_L]\[Right]'"
 b:9
```

按键代码可以通过 [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) 获取。

最后在 `~/.xinitrc` 里添加以下内容来在登录时触发 *xbindkeys*。

```
xbindkeys &

```

### --desktop 参数不生效或使X-server崩溃

确保你有 `~/.config/pcmanfm` 文件夹的所有权和写权限。

通过使用 `--desktop-pref` 参数或者修改 `~/.config/pcmanfm/default/pcmanfm.config` 来设置桌面壁纸来解决问题。

### 终端模拟器的高级配置没有保存

请设置 libfm 配置文件的权限：

```
$ chmod -R 755 ~/.config/libfm
$ chmod 644 ~/.config/libfm/libfm.conf

```

### 记住文件排序设置

在 *View > Sort Files* 里可以设置文件排序，但是如果要让 PCManFM 记住这个设置，需要打开 *Edit > Preferences* 然后再关掉，这样会让当前的sort_type 和 sort_by 的值写入 `~/.config/pcmanfm/LXDE/pcmanfm.conf` 文件。

### 挂载设备时候提醒 "Not authorized"

在 `/etc/polkit-1/rules.d/00-mount-internal.rules` 文件里添加这个 [polkit](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Polkit (简体中文)") 规则：

 `/etc/polkit-1/rules.d/00-mount-internal.rules` 
```
polkit.addRule(function(action, subject) {
    if ((action.id == "org.freedesktop.udisks2.filesystem-mount-system" &&
       subject.local && subject.active && subject.isInGroup("storage")))
       {
          return polkit.Result.YES;
       }
 });
```

并且把你的用户添加到 `storage` 用户组里：

```
# usermod -aG storage *username*

```

### Operation not supported

参见 [会话权限](/index.php/General_troubleshooting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#会话权限 "General troubleshooting (简体中文)").