**翻译状态：** 本文是英文页面 [Fluxbox](/index.php/Fluxbox "Fluxbox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-07-24，点击[这里](https://wiki.archlinux.org/index.php?title=Fluxbox&diff=0&oldid=462899)可以查看翻译后英文页面的改动。

Fluxbox 是一个 X11 下的窗口管理器。它基于 Blackbox（现在停止开发） 0.61.1 的代码构建，现在依然在开发中，并且功能显著增强。Fluxbox 占用资源少，速度快，并且提供切换和分组等有趣的窗口管理工具。配置文件简单易懂，便于编辑，有上百种的美化桌面的“主题”。Archlinux 和 Fluxbox 可以让一台 Pentium 800 和 256M 内存的电脑焕发活力。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动 Fluxbox](#.E5.90.AF.E5.8A.A8_Fluxbox)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 菜单管理](#.E8.8F.9C.E5.8D.95.E7.AE.A1.E7.90.86)
        *   [3.1.1 使用 fluxbox-generate_menu](#.E4.BD.BF.E7.94.A8_fluxbox-generate_menu)
        *   [3.1.2 使用 MenuMaker](#.E4.BD.BF.E7.94.A8_MenuMaker)
        *   [3.1.3 使用 Xdg-menu](#.E4.BD.BF.E7.94.A8_Xdg-menu)
        *   [3.1.4 手动创建/编辑菜单](#.E6.89.8B.E5.8A.A8.E5.88.9B.E5.BB.BA.2F.E7.BC.96.E8.BE.91.E8.8F.9C.E5.8D.95)
    *   [3.2 Init 文件](#Init_.E6.96.87.E4.BB.B6)
    *   [3.3 热键](#.E7.83.AD.E9.94.AE)
        *   [3.3.1 声音](#.E5.A3.B0.E9.9F.B3)
    *   [3.4 工作区](#.E5.B7.A5.E4.BD.9C.E5.8C.BA)
    *   [3.5 切换和分组](#.E5.88.87.E6.8D.A2.E5.92.8C.E5.88.86.E7.BB.84)
    *   [3.6 壁纸](#.E5.A3.81.E7.BA.B8)
        *   [3.6.1 轻松切换多个壁纸](#.E8.BD.BB.E6.9D.BE.E5.88.87.E6.8D.A2.E5.A4.9A.E4.B8.AA.E5.A3.81.E7.BA.B8)
        *   [3.6.2 使用 feh](#.E4.BD.BF.E7.94.A8_feh)
        *   [3.6.3 使用 Nitrogen](#.E4.BD.BF.E7.94.A8_Nitrogen)
    *   [3.7 主题](#.E4.B8.BB.E9.A2.98)
    *   [3.8 Slit](#Slit)
    *   [3.9 自启动程序](#.E8.87.AA.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)
    *   [3.10 其他菜单](#.E5.85.B6.E4.BB.96.E8.8F.9C.E5.8D.95)
    *   [3.11 桌面效果](#.E6.A1.8C.E9.9D.A2.E6.95.88.E6.9E.9C)
    *   [3.12 通知](#.E9.80.9A.E7.9F.A5)
    *   [3.13 没有 xorg.conf 文件后的 Xorg 配置](#.E6.B2.A1.E6.9C.89_xorg.conf_.E6.96.87.E4.BB.B6.E5.90.8E.E7.9A.84_Xorg_.E9.85.8D.E7.BD.AE)
        *   [3.13.1 在 Fluxbox 中设定键盘布局](#.E5.9C.A8_Fluxbox_.E4.B8.AD.E8.AE.BE.E5.AE.9A.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)。

## 启动 Fluxbox

**图形界面登录**

在 [显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器") 的会话菜单中选择 *fluxbox*。

**手动**

编辑 `~/.xinitrc` 并添加如下几行:

```
exec startfluxbox

```

查看 [xinitrc](/index.php/Xinitrc "Xinitrc") 来获取详细信息，例如保存登录会话。

## 配置

系统范围的 Fluxbox 配置文件在 `/usr/share/fluxbox` 中，用户个人配置文件在 `~/.fluxbox` 中，配置文件如下：

*   *init* - 主要的 Fluxbox 资源配置文件。参阅 [编辑init文件](http://fluxbox-wiki.org/category/howtos/en/Editing_the_init_file.html)。
*   *menu* - Fluxbox 菜单配置文件。参阅下文和 [编辑menu文件](http://fluxbox-wiki.org/category/howtos/en/Editing_the_menu.html)。
*   *keys* - Fluxbox 键盘快捷键（热键）配置文件。参阅下文和 [这里](http://fluxbox-wiki.org/category/howtos/en/Keyboard_shortcuts.html)。
*   *startup* - 编辑开机启动程序，参阅下文中关于 .xinitrc 的部分和 [这里](http://fluxbox-wiki.org/category/howtos/en/Editing_the_startup_file.html)。
*   *overlay* - 重载主题元素的配置文件。参阅 [这里](http://fluxbox-wiki.org/category/howtos/en/Style_overlay.html)。
*   *apps* - 记忆具体应用程序窗口配置的文件。参阅 [这里](http://fluxbox-wiki.org/category/howtos/en/Editing_the_apps_file.html)。
*   *windowmenu* - 配置窗口菜单自身的文件。[看这里](http://fluxbox-wiki.org/category/howtos/en/Editing_the_windowmenu.html)。

文件夹中有很多不太重要的配置文件。需要注意的有 init，menu，keys 和 startup。

### 菜单管理

第一次安装 Fluxbox 时系统会在 `~/.fluxbox/menu` 中创建基本的程序菜单，在桌面上右击鼠标可以访问该菜单。和其他轻量窗口管理器一样，Fluxbox 在安装新程序的时候并不自动升级其程序菜单。因此推荐先在系统上安装需要的应用程序，然后再生成或编辑程序菜单。有四种基本方法来添加/编辑项目和增强菜单：

#### 使用 fluxbox-generate_menu

Fluxbox 提供一个内建的命令：

```
$ fluxbox-generate_menu

```

该命令会根据系统中已安装的程序来自动生成 `~/.fluxbox/menu` 文件。但是生成的菜单综合性不如使用 [MenuMaker](#MenuMaker) 生成的菜单。

#### 使用 MenuMaker

[MenuMaker](http://menumaker.sourceforge.net) 是一个为各种各样的窗口管理器创建基于 XML 菜单的有力工具，支持 Fluxbox。MenuMaker 搜索计算机中所有的可执行程序，基于搜索结果创建程序菜单。如果需要的话，可以配置其排除 Legacy X，GNOME, KDE, 和 Xfce 的应用程序。

安装 [menumaker](https://www.archlinux.org/packages/?name=menumaker)，运行以下命令生成一个完整菜单并覆盖默认菜单。

```
$ mmaker -f FluxBox

```

可以在运行命令时加入以下开关来避免将基于命令行的程序—例如 *alsamixer*—加入菜单：`--no-legacy` 和 `--no-debian`。例如：

```
$ mmaker -f --no-legacy --no-debian FluxBox

```

要查看更多 MenuMaker 选项：

```
 mmaker --help

```

#### 使用 Xdg-menu

可以使用 [Xdg-menu](/index.php/Xdg-menu "Xdg-menu") 来生成菜单，参阅 [Xdg-menu#FluxBox](/index.php/Xdg-menu#FluxBox "Xdg-menu") 章节。

#### 手动创建/编辑菜单

使用编辑器编辑 `~/.fluxbox/menu` 文件，一个菜单项目的基本语法类似：

```
[exec] (name) {command} <path to icon>

```

"name" 是想要在菜单项目上显示的文字，"command" 是程序所在的位置。"<path to icon>"是可选的。例如：

```
[exec] (Firefox Browser) {/usr/bin/firefox} <path to firefox icon>

```

创建子菜单的语法如下：

```
[submenu] (Name)
...
...
[end]

```

编辑完成后，保存退出，不需要重启 Fluxbox。更多的信息参阅 [编辑 Fluxbox 菜单](http://fluxbox-wiki.org/category/howtos/en/Editing_the_menu.html)。

### Init 文件

`~/.fluxbox/init` 文件是 Fluxbox 的主要配置资源文件。可以用来改变 Fluxbox，窗口，工具栏，焦点等基本功能。一些选项也可以从Fluxbox配置菜单中找到。详细内容参阅 [编辑 init 文件](http://fluxbox-wiki.org/category/howtos/en/Editing_the_init_file.html)。

### 热键

Fluxbox 提供基本的热键功能。Fluxbox 热键文件位于 `~/.fluxbox/keys`。 Control 键代表 "Control"。 `Mod1` 对应 Alt 键，`Mod4` 对应 Super 键（Super 键不是一个标准按键，经常被映射到 "Win" 键）。当 Fluxbox 安装完成后第一次运行时，Fluxbox 提供一组几乎完成的非常有用的热键。细读精研 `~/.fluxbox/keys` 文件可以增强 Fluxbox 体验。

例子：快捷的方式来控制扬声器音量：

```
Control Mod1 Up :Exec amixer set Master,0 5%+
Control Mod1 Down :Exec amixer set Master,0 5%-

```

#### 声音

参考 [Advanced Linux Sound Architecture#Keyboard volume control](/index.php/Advanced_Linux_Sound_Architecture#Keyboard_volume_control "Advanced Linux Sound Architecture") 和 [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio")。

### 工作区

Fluxbox 默认提供四个工作区。可以通过 Ctrl+F1-F4 快捷键访问，或者在工具栏上的箭头单击左键。也可以通过使用鼠标中键在桌面上单击，在工作区菜单上选择工作区。

### 切换和分组

当桌面上有两个以上窗口时，在一个窗口的上窗口标签单击 ctrl+鼠标左键，然后拖动该窗口到另一个窗口，这两个窗口会以标签页的形式集合在一起，现在执行一个窗口操作将影响到整个窗口“集合”。在标签页上单击 ctrl+鼠标左键，然后拖动到桌面空白位置将还原窗口。

### 壁纸

在 Fluxbox 种设置壁纸一直很复杂，特别是透明度问题。请参阅 Fluxbox wiki 中 [壁纸设置](http://fluxbox-wiki.org/category/howtos/en/Howto_set_the_background.html) 章节。

检查计算机中是否有壁纸设置程序。

```
$ fbsetbg -i

```

如果没有，安装 feh, esetroot 或者 wmsetbg。然后在 `~/.xinitrc` 文件中 "exec" 行之前添加 "fbsetbg" 行。例如：

```
fbsetbg /path/to/my/image.image

```

如果该命令返回如下信息：

```
$ /usr/bin/fbsetbg: line 153: xmessage: command not found

```

那么需要安装 xorg-xmessage 包。

#### 轻松切换多个壁纸

在 Fluxbox 菜单中添加子菜单如下：

```
[submenu] (Backgrounds)
[wallpapers] (~/.fluxbox/backgrounds) {feh --bg-scale}
[wallpapers] (/usr/share/fluxbox/backgrounds) {feh --bg-scale}
[end]

```

将壁纸放到 `~/.fluxbox/backgrounds` 中或者其他指定文件夹，壁纸将以同样的方式在主题中显示。

在没有 'xinerama' 的系统上显示双屏幕壁纸和上述一样，例如：

```
[submenu] (Backgrounds)
[wallpapers] (/path/to/your/backgrounds) {feh --bg-scale --no-xinerama }
[end]

```

#### 使用 feh

安装 [feh](https://www.archlinux.org/packages/?name=feh)。

以下步骤确保 Fluxbox 下次启动时会加载 feh 背景。

**1.** 确保 `.fehbg` 可执行:

```
$ chmod 770 ~/.fehbg

```

**2.** 在 `~/.fluxbox/init` 文件中添加/修改以下行:

```
session.screen0.rootCommand:	~/.fehbg

```

**3.** 在 `~/.fluxbox/startup` 文件中添加/修改以下行:

```
~/.fehbg

```

#### 使用 Nitrogen

也可以使用 [Nitrogen](/index.php/Nitrogen "Nitrogen")。使用以下命令来运行图形壁纸选择软件：

```
$ nitrogen

```

添加包含图片的文件夹，选择图片然后应用。当然可以更改图片选项，例如壁纸居中或者放大。

添加如下行：

```
nitrogen --restore &

```

到 `~/.fluxbox/startup` 文件中确保壁纸在登陆时使用。

如果重启 Fluxbox 后，当前选择主题的壁纸覆盖了 Nitrogen 设置的壁纸。编辑使用的主题的 `theme.cfg` 文件，注释或者删除如下几行来解决这个问题:

```
background:
background.color:
background.colorTo:

```

### 主题

要安装 Fluxbox 主题，将主题文件解压缩到主题文件夹，默认的主题文件夹是

*   全局 - `/usr/share/fluxbox/styles`
*   仅用户 - `~/.fluxbox/styles`

Archlinux [AUR](/index.php/AUR "AUR") 中有一套很漂亮的 Fluxbox 主题—"fluxmod-styles"。从 [这里](https://aur.archlinux.org/packages/fluxmod-styles/) 获得。正确安装后将会在 Fluxbox 菜单中的 Fluxbox -> Styles section 中显示。

想要创建自己的 Fluxbox 主题，请参阅 [fluxbox-style(5)](http://fluxbox.org/help/man-fluxbox-style.php)， [Fluxbox/Style guide](/index.php/Fluxbox/Style_guide "Fluxbox/Style guide") 和 [主题指南](http://tenr.de/howto/style_fluxbox/style_fluxbox.html)。

如果使用

```
$ mmaker -f FluxBox

```

创建菜单，那么安装完主题后将不会看到主题选择菜单。 将下面几行添加到 `~/.fluxbox/menu` 文件中的重启菜单选项后来修正。

```
[submenu] (System Styles) {Choose a style...}
      [stylesdir] (/usr/share/fluxbox/styles)
        [end]
[submenu] (User Styles) {Choose a style...}
      [stylesdir] (~/.fluxbox/styles)
        [end]

```

### Slit

Fluxbox，WindowMaker 和一些轻量的窗口管理器都有 "Slit"，可以是所有程序 "dock" 化。一个 "dock" 化的程序可以锚定在任何工作区上，可以被轻松移动，并且不受任何窗口操作的影响，它基本上是一个小部件，将时钟，系统监视器，天气等 "dock" 化非常有用。参阅 [dockapps.net](http://www.dockapps.net/)。

### 自启动程序

Fluxbox 本身提供了自启动程序的功能。`~/.fluxbox/startup` 文件是一个像启动 Fluxbox 一样自启动应用程序的脚本。`#` 标记是注释。

一个简单的例子：

```
fbsetbg -l # sets the last background set, very useful and recommended.
# In the below commands the ampersand symbol (&) is required on all applications that do not terminate immediately.
# Failure to provide them will cause Fluxbox not to start.
idesk &
xterm &
# exec is for starting Fluxbox itself, do not put an ampersand (&) after this or Fluxbox will exit immediately.
exec /usr/bin/fluxbox
# or if you want to keep a log, uncomment the below command and comment out the above command:
# exec /usr/bin/fluxbox -log ~/.fluxbox/log

```

### 其他菜单

上面的 "菜单管理" 章节讨论了主要菜单。这些菜单在 Fluxbox 行话中称为"根"菜单。Fluxbox 也为用户提供了一些其他的菜单。

*   工作区菜单：在桌面上点击鼠标中键。
*   配置菜单：位于"根"菜单的 "Fluxbox" 部分。
*   窗口菜单：在任何窗口或者最小化窗口的标题栏右击鼠标。可以编辑窗口菜单。参阅 fluxbox-menu man page。
*   工具栏菜单：在工具栏空白部分右击鼠标。也在配置菜单的子菜单中。
*   Slit 菜单：在配置菜单的子菜单中。

### 桌面效果

想要在 Fluxbox 开启桌面效果—透明或者阴影，需要安装 X compositor，例如 [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") 或者 [Compton](/index.php/Compton "Compton")。

### 通知

在 Fluxbox 中开启桌面通知，需要安装通知服务器。参阅 [desktop notifications](/index.php/Desktop_notifications "Desktop notifications")。

### 没有 xorg.conf 文件后的 Xorg 配置

Xorg 不再需要 *xorg.conf* 文件了，以前在 xorg.conf 文件中所做的关于键盘和省电模式的设定可以通过以下方式调整。

#### 在 Fluxbox 中设定键盘布局

将以下行添加到 `~/.fluxbox/startup` 文件中：

```
setxkbmap us -variant intl & # 在 us 键盘中添加特殊字符支持 (类似 éóíáú)

```

可以添加自己的语言代码来代替 'us'，并且移除 'variant' 选项。参阅 *setxkbmap* 手册页来获得更多选项。

在 `~/.fluxbox/menu` 文件中添加以下行来获得菜单中帮助功能:

```
[submenu] (Keyboard)
      [exec] (normal) {setxkbmap us}
      [exec] (international) {setxkbmap us -variant intl}
[end]

```

## 参阅

*   [Fluxbox Homepage](http://fluxbox.org/)
*   [Fluxbox wiki](http://fluxbox-wiki.org/)
*   [Gentoo Wiki about Fluxbox](http://wiki.gentoo.org/wiki/Fluxbox)
*   [Themes for Fluxbox](https://www.box-look.org/browse/cat/139/ord/latest/)
*   [Narada's Fluxbox Guide](https://bbs.archlinux.org/viewtopic.php?id=77729)
*   The Fluxbox man pages: fluxbox, fluxbox-menu, fluxbox-style, fluxbox-keys, fluxbox-apps, fluxbox-remote, fbsetroot, fbsetbg, fbrun, startfluxbox.
*   [Arch Linux Fluxbox screenshots](https://bbs.archlinux.org/viewtopic.php?id=90260)