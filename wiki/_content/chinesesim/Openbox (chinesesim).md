相关文章

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")

Openbox 是一个轻量级、可高度定制以及支持大量标准的窗口管理器。它的特性在 [官方网站](http://icculus.org/openbox/) 有详细的文档说明。这篇文章是关于在 Arch Linux 下 运行 Openbox。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 升级到 Openbox 3.5](#.E5.8D.87.E7.BA.A7.E5.88.B0_Openbox_3.5)
*   [3 Openbox 作为一个单独的窗口管理器](#Openbox_.E4.BD.9C.E4.B8.BA.E4.B8.80.E4.B8.AA.E5.8D.95.E7.8B.AC.E7.9A.84.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
*   [4 Openbox 作为在桌面环境使用的窗口管理器](#Openbox_.E4.BD.9C.E4.B8.BA.E5.9C.A8.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83.E4.BD.BF.E7.94.A8.E7.9A.84.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [4.1 GNOME 2.24 和 2.26](#GNOME_2.24_.E5.92.8C_2.26)
    *   [4.2 GNOME 2.26 Redux](#GNOME_2.26_Redux)
    *   [4.3 KDE](#KDE)
    *   [4.4 Xfce4](#Xfce4)
*   [5 对于多显示器用户](#.E5.AF.B9.E4.BA.8E.E5.A4.9A.E6.98.BE.E7.A4.BA.E5.99.A8.E7.94.A8.E6.88.B7)
*   [6 首选项](#.E9.A6.96.E9.80.89.E9.A1.B9)
    *   [6.1 手动配置](#.E6.89.8B.E5.8A.A8.E9.85.8D.E7.BD.AE)
    *   [6.2 ObConf](#ObConf)
    *   [6.3 程序定制](#.E7.A8.8B.E5.BA.8F.E5.AE.9A.E5.88.B6)
*   [7 菜单](#.E8.8F.9C.E5.8D.95)
    *   [7.1 手动配置菜单](#.E6.89.8B.E5.8A.A8.E9.85.8D.E7.BD.AE.E8.8F.9C.E5.8D.95)
    *   [7.2 MenuMaker](#MenuMaker)
    *   [7.3 XdgMenu](#XdgMenu)
    *   [7.4 Obmenu](#Obmenu)
        *   [7.4.1 obm-xdg](#obm-xdg)
    *   [7.5 openbox-menu](#openbox-menu)
    *   [7.6 基于 Python 的 xdg 菜单脚本](#.E5.9F.BA.E4.BA.8E_Python_.E7.9A.84_xdg_.E8.8F.9C.E5.8D.95.E8.84.9A.E6.9C.AC)
    *   [7.7 Openbox 菜单生成器](#Openbox_.E8.8F.9C.E5.8D.95.E7.94.9F.E6.88.90.E5.99.A8)
    *   [7.8 Pipe menus](#Pipe_menus)
*   [8 启动程序](#.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)
    *   [8.1 开启自启动](#.E5.BC.80.E5.90.AF.E8.87.AA.E5.90.AF.E5.8A.A8)
    *   [8.2 自启动脚本](#.E8.87.AA.E5.90.AF.E5.8A.A8.E8.84.9A.E6.9C.AC)
    *   [8.3 自启动目录](#.E8.87.AA.E5.90.AF.E5.8A.A8.E7.9B.AE.E5.BD.95)
*   [9 主题和外观](#.E4.B8.BB.E9.A2.98.E5.92.8C.E5.A4.96.E8.A7.82)
    *   [9.1 Openbox 主题](#Openbox_.E4.B8.BB.E9.A2.98)
    *   [9.2 鼠标指针,图标,壁纸](#.E9.BC.A0.E6.A0.87.E6.8C.87.E9.92.88.2C.E5.9B.BE.E6.A0.87.2C.E5.A3.81.E7.BA.B8)
*   [10 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [10.1 Aero snap 特效](#Aero_snap_.E7.89.B9.E6.95.88)
    *   [10.2 文件关联](#.E6.96.87.E4.BB.B6.E5.85.B3.E8.81.94)
    *   [10.3 复制粘贴](#.E5.A4.8D.E5.88.B6.E7.B2.98.E8.B4.B4)
    *   [10.4 窗口透明](#.E7.AA.97.E5.8F.A3.E9.80.8F.E6.98.8E)
    *   [10.5 程序的 Xprop 值](#.E7.A8.8B.E5.BA.8F.E7.9A.84_Xprop_.E5.80.BC)
        *   [10.5.1 Xprop for Firefox](#Xprop_for_Firefox)
    *   [10.6 链接菜单到按键](#.E9.93.BE.E6.8E.A5.E8.8F.9C.E5.8D.95.E5.88.B0.E6.8C.89.E9.94.AE)
    *   [10.7 在背景的 Urxvt](#.E5.9C.A8.E8.83.8C.E6.99.AF.E7.9A.84_Urxvt)
        *   [10.7.1 ToggleShowDesktop 例外](#ToggleShowDesktop_.E4.BE.8B.E5.A4.96)
    *   [10.8 键盘音量控制](#.E9.94.AE.E7.9B.98.E9.9F.B3.E9.87.8F.E6.8E.A7.E5.88.B6)
*   [11 其他资源](#.E5.85.B6.E4.BB.96.E8.B5.84.E6.BA.90)

## 安装

[openbox](https://www.archlinux.org/packages/?name=openbox) 可以从 Arch Linux 的[官方仓库](/index.php/%E5%AE%98%E6%96%B9%E4%BB%93%E5%BA%93 "官方仓库")里[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")得到。

安装完成后, 你应该把默认的配置文件 **`rc.xml`**, **`menu.xml`**, 和 **`autostart`** 和`environment` 复制到 *`~/.config/openbox`* :

```
$ mkdir -p ~/.config/openbox
$ cp /etc/xdg/openbox/{rc.xml,menu.xml,autostart,environment} ~/.config/openbox

```

**注意:** 不要用 root 进行以上操作，应使用普通用户。

这四个文件组成了 Openbox 配置的基础。每一个文件是配置的独立的部分，它们的功能是：

	`rc.xml`

	本文件是配置文件.用于定义键盘快捷键, 主题, 虚拟桌面等。

	`menu.xml`

	本文件定义了在桌面用鼠标击键时显示的菜单。它定义了程序启动器和快捷方式。请看 [#菜单](#.E8.8F.9C.E5.8D.95) 段。

	`autostart`

	本文件在 Openbox 启动时读取。包含了一些需要启动的程序，通常用来定义许多环境变量、启动面板/dock、设置壁纸或者执行其他启动脚本等等。细节请看 [Openbox Wiki](http://openbox.org/wiki/Help:Autostart).

	`environment`

	本文件被 openbox-session 启动时调用。它包含了在 Openbox 上下文中定义的变量。任何你想对 Openbox 本身可见以及从菜单启动的程序需要的变量都放在这里。

## 升级到 Openbox 3.5

如果你从早期版本升级到 Openbox 3.5 或更高版本，注意以下改变：

*   现在有一个新的配置文件叫 `environment`，你应该把它从`/etc/xdg/openbox`复制到`~/.config/openbox`。
*   以前叫 `autostart.sh` 的配置文件现在叫 `autostart`。你应该把你的文件重命名，去掉.sh。
*   `rc.xml` 中一些配置的语法改变了。尽管 Openbox 能够理解旧选项，你还是应该对比一下你的配置文件和 `/etc/xdg/openbox` 看看哪些改变影响你。

## Openbox 作为一个单独的窗口管理器

Openbox 可以作为一个单独的窗口管理器使用. 这样的安装和配置通常比作为桌面环境的一部分要简单. 单独运行 openbox 可以减少系统的 CPU 和 内存负载

让Openbox作为一个单独的窗口管理器运行,把以下内容加入 **`~/.xinitrc`** :

```
exec openbox-session

```

详情请参阅[xinitrc](/index.php/Xinitrc "Xinitrc")。

如果想在命令行下启动 Openbox , 用 xinit :

```
$ xinit /usr/bin/openbox-session

```

如果你以前使用过另外的窗口管理器(类如 Xfwm)而且现在 Openbox 在退出 X 后不能启动,移动 autostart 目录:

```
mv ~/.config/autostart ~/.config/autostart-bak

```

**注意:** Openbox 中的 xdg-autostart 需要 [pyxdg](https://www.archlinux.org/packages/?name=pyxdg)

## Openbox 作为在桌面环境使用的窗口管理器

Openbox 可以作为成熟桌面环境的替代窗口管理器.这种方法 Openbox 的配置依赖于桌面环境.

### GNOME 2.24 和 2.26

创建 `/usr/share/applications/openbox.desktop` 添加以下内容:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=OpenBox
Exec=openbox
NoDisplay=true
# name of loadable control center module
X-GNOME-WMSettingsModule=openbox
# name we put on the WM spec check window
X-GNOME-WMName=OpenBox

```

设置 gconf, 设 **`/desktop/gnome/session/required_components/windowmanager`** 为 **`openbox`:**

```
$ gconftool-2 -s -t string /desktop/gnome/session/required_components/windowmanager openbox

```

最后, 从 GDM 会话选项菜单中选择 **GNOME** 会话.

### GNOME 2.26 Redux

***如果上面的 GNOME 2.24 失败了:***

当尝试用 "Gnome/Openbox" 会话登录-- 而且始终不能登录, 试试以下内容. 这是一种通过始终把 Openbox 作为 Gnome 会话打开而达到目的的方法:

1.  通过 Gnome-only 会话登录 (这时的 WM 应该是 Metacity).
2.  安装 Openbox ,如果以前没装的话.
3.  点击菜单到 *系统 → 首选项 → 启动程序* (在旧版本的 Gnome 可能是 '会话')
4.  打开启动程序, 选择 '+ Add' 加入以下内容. 忽略以 # 开始的注释.
5.  点击 'Add' 数据入口窗口的按钮. 保证已输入内容旁边的选择框已选.
6.  退出 Gnome 会话,重新登录.
7.  现在 Openbox 应该作为窗口管理器运行.

```
Name:    Openbox Windox Manager          # Can be changed
Command: openbox --replace               # Text should not be removed from this line, but possibly added to it
Comment: Replaces metacity with openbox  # Can be changed

```

这样做就创建一个自启动程序,每当 Gnome 的用户会话启动时执行.

### KDE

1.  如果你使用KDM，请选择"KDE/Openbox"登录选项
2.  如果你使用startx，添加 `exec openbox-kde-session` 到 `~/.xinitrc`
3.  在 shell 中输入：

```
$ xinit /usr/bin/openbox-kde-session

```

### Xfce4

登录到普通的 Xfce4 会话，在终端中输入：

```
$ killall xfwm4 ; openbox & exit

```

这样会终止 wfwm4，启动 Openbox，最后会关闭终端。 注销，确定选中了 "Save session for future logins" 选项 在下一次登录后，Xfce4 就会使用 Openbox 作为它的窗口管理器。

使 Openbox 可以从 xfce4-session 中注销, 编辑 `~/.config/openbox/menu.xml` (如果没有,从 `/etc/xdg/openbox` 中复制).

查找以下内容:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

改变为:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

否则, 使用 root-menu 的 "Exit" 选项会导致 Openbox 结束自身的执行, 使你没有窗口管理器.

如果使用鼠标滚轮切换虚拟桌面遇到问题, 编辑 `~/.config/openbox/rc.xml` . 移动 *mouse binds with* 动作 "DesktopPrevious" 和 "DesktopNext" 从上下文 "Desktop" 到 "Root" (你可能需要定义 *Root* 上下文).

当使用 Openbox 的 root-menu 代替 Xfce 的菜单,可以使用以下命令退出 Xfdesktop :

```
$ xfdesktop --quit

```

Xfdesktop 管理壁纸和桌面图标,可以用其它程序代替这些功能,类如 ROX .

(当终止了 Xfdesktop, 上面切换虚拟桌面的问题不会再有.)

## 对于多显示器用户

尽管 Openbox 本身提供了高于一般的多显示器支持，一个叫做 [Openbox Multihead](https://aur.archlinux.org/packages.php?ID=51460) 的分支可以在 AUR 找到，它提供给多显示器用户每个显示器一个桌面。这种模型很少在浮动窗口管理器中找到，但是在 tiling 窗口管理器中很常见。这里解释的很详细： [Xmonad 网站](http://xmonad.org/tour.html#workspace)。还可以参考 [README.MULTIHEAD](https://github.com/BurntSushi/openbox-multihead/blob/multihead/README.MULTIHEAD) 获取更易懂的对于新功能的描述，以及 Openbox Multihead 中的选项设置

当只有一个显示器的时候 Openbox Multihead 会和普通的 Openbox 表现相同。

使用 Openbox Multihead 的一个缺点是它破坏了 EWMH 假设，依旧是用户同时能且只能看到一个桌面。因此现存的 pagers 不会工作的很好。想要修补这个问题，[pager-multihead](https://aur.archlinux.org/packages.php?ID=51536) 可以在 AUR 找到，它和 Openbox Multihead 是兼容的。 [Screenshots](http://imgur.com/a/cnZeq#y04nk).

最后，一个新版本的 [pytyle](https://aur.archlinux.org/packages.php?ID=51626) 也可以在 AUR 找到，和 Openbox Multihead 合作的很好

当只有一个显示器的时候，pytyle3 和 pager-multihead 都可以在没有 Openbox Multihead 的时候工作的很好。

## 首选项

有两种选择来配置 OpenBox 的偏好:

### 手动配置

要手动配置OpenBox,使用文本编辑器编辑 `~/.config/openbox/rc.xml` . 配置文件内含大量的注释, 而且在官方上可以找到更多的 [帮助文档](http://icculus.org/openbox/index.php/Help:Contents).

### ObConf

[ObConf](http://icculus.org/openbox/index.php/ObConf:About) 是一个基于图形界面的Openbox配置工具, 它能设定包括主题、虚拟桌面、窗口属性和桌面边缘的大多数配置.

```
# pacman -S obconf

```

ObConf不能用来设定键盘快捷键和其他一些高级功能。这些修改，您必须手动编辑 `rc.xml` （见上文）

另外一个选择是 [AUR](/index.php/AUR "AUR") 上的 [ObKey](http://code.google.com/p/obkey/).

### 程序定制

Openbox 允许针对每一个程序定制.这样可以对给定的程序设定规则.例如:

*   启动浏览器在一个指定的虚拟桌面.
*   开启没有窗口装饰的终端(窗口色彩)
*   让 bit-torrent 客户端开启在指定的屏幕位置.

针对程序的设定定义在 `~/.config/openbox/rc.xml` .在注释中有指导说明.更多的细节可以在 Openbox 的官网上找到[Help:Applications](http://openbox.org/wiki/Help:Applications)

## 菜单

默认 Openbox 菜单包括很多菜单项供使用,其中有些尚未安装,你可能不需要或根本不想安装.你可能想定制 `menu.xml`,有很多种方法可以定制

### 手动配置菜单

用文本编辑器编辑`~/.config/openbox/menu.xml`. 许多设定不需加以说明,更多的细节在 [帮助文件](http://icculus.org/openbox/index.php/Help:Menus).

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) 用来为各种窗口管理器创建基于XML的菜单，包括Openbox. MenuMaker将搜寻您电脑中的可执行程序，并在搜索结果的基础上建立一个XML菜单. 根据需要，它可以配置除特定程序类型(类如 GNOME,KDE 等)外的程序

```
# pacman -S menumaker    #  Install MenuMaker from the repository

```

安装后, 你可以通过运行以下命令来生成一个完整的菜单文件(`menu.xml`):

```
$ mmaker -v OpenBox3     #  Will not overwrite an existing menu file.
$ mmaker -vf OpenBox3    #  Force option permits overwriting the menu file.
$ mmaker --help          #  See the full set of options for MenuMaker.

```

MenuMaker创建了一个很全面的 `menu.xml`. 你可以手动编辑 menu.xml文件, 或者在安装新的软件时生成一个新的菜单.

### XdgMenu

[XdgMenu](/index.php/XdgMenu "XdgMenu")，一个类似于MenuMaker的工具，但是你可以使用Pipe Menus方式自动产生而不需要刷新:

```
 # pacman -S archlinux-xdg-menu

```

在menu.xml中加入以下代码：

```
 <menu id="apps" label="所有应用" execute="xdg_menu --format openbox3-pipe --root-menu /etc/xdg/menus/arch-applications.menu" />

```

然后在在'root-menu'中加入

```
 <menu id="apps" />

```

或者你可以直接产生全部菜单内容（*将会重写menu.xml，谨慎使用*）:

```
 $ xdg_menu --format openbox3 --root-menu /etc/xdg/menus/arch-applications.menu --fullmenu > .config/openbox/menu.xml

```

参考：[XdgMenu#OpenBox](/index.php/XdgMenu#OpenBox "XdgMenu")

### Obmenu

Obmenu 是一个基于GUI的 openbox 菜单编辑软件.对于不喜欢手动编辑 xml 文件的人来说,obmenu 可能是最好的选择. Obmenu可以从 community 仓库里得到:

```
# pacman -S obmenu

```

安装完毕后, 运行 `obmenu` 就可以增加或者删除指定的软件.

#### obm-xdg

<tt>obm-xdg</tt> 是安装 Obmenu 时附带的一个命令行工具. 它的作用是将已经安装的 GTK/GNOME 程序归类放置到相应子菜单中去

想要使用 obm-xdg, 得先在 `~/.config/openbox/menu.xml` 文件中添加一下代码 :

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

然后添加以下一行到 'root-menu' 项下你想要它出现的位置:

```
<menu id="xdg-menu"/>

```

用 obm-xdg 自身创建 `~/.config/openbox/menu.xml` 添加以下内容:

```
<openbox_menu>
 <menu execute="obm-xdg" id="root-menu" label="apps"/>
</openbox_menu>

```

然后执行 `openbox --reconfigure` 刷新 openbox 菜单. 现在右键菜单里面应该多了一个名字为 **xdg** 的子菜单项.

**注意:** 如果你没有安装 GNOME , 想让 obm-xdg 正常工作, 必须得先安装 **gnome-menus**.

### openbox-menu

Openbox-menu 使用来自 LXDE 项目的 [menu-cache](http://sourceforge.net/projects/lxde/files/menu-cache/) 为 Openbox 创建动态菜单。

项目主页在这儿： [http://mimasgpc.free.fr/openbox-menu_en.html](http://mimasgpc.free.fr/openbox-menu_en.html)

AUR 包在这儿： [[1]](https://aur.archlinux.org/packages.php?ID=31605)

### 基于 Python 的 xdg 菜单脚本

这个脚本属于 Fedora 的 Openbox 包. 你只需要把脚本放在任何一个地方和创建一个菜单项.

这里是一个 submission :[script](http://pastebin.com/f2f827625)

这里是一个 head :[latest script](http://pkgs.fedoraproject.org/gitweb/?p=openbox.git;f=xdg-menu;hb=HEAD)

下载你喜欢的一个(你可能会喜欢 head 版本).把脚本放在任何地方.我用的是 ~/Documents/build/xdg-menu .根据脚本的存放路径更改菜单项.

用文本编辑器打开 `menu.xml`加入以下内容.你也可以更改标签.

```
<menu id="apps-menu" label="xdgmenu" execute="python /home/shiki/Documents/build/xdg-menu"/>

```

保存文件,执行 `openbox --reconfigure`.

### Openbox 菜单生成器

AUR 上有 [obmenugen-bin](https://aur.archlinux.org/packages.php?ID=27300),Openbox 菜单生成器从 *.desktop 文件生成菜单文件.Obmenugen 提供用简单的正则过滤(隐藏)菜单项的文本文件.

```
$ obmenugen               # 创建菜单文件
$ openbox --reconfigure   # 查看你生成的菜单

```

### Pipe menus

与其它窗口管理器类似, Openbox 允许脚本动态生成菜单(menus on-the-fly).类似的例子有系统监视器,媒体播放器管理,还有天气监视器. Pipe menu 脚本可以从 Openbox 官网上找到 [Openbox:Pipemenus](http://openbox.org/wiki/Openbox:Pipemenus).

用户 *Xyne* 创建了一个 pipe menu 的文件浏览器,用户 *brisbin33* 创建了一个 pipe menu 用于扫描和连接无线热点(用 netcfg).相应的功能可以在论坛找到:[file browser](https://bbs.archlinux.org/viewtopic.php?id=77197&p=1),[wifi](https://bbs.archlinux.org/viewtopic.php?id=78290).

用户 *jnguyen* 用 Udisks 创建了一个用来管理可移动设备的 pipe menu.这个论坛的帖子在这:[obdevicemenu](https://bbs.archlinux.org/viewtopic.php?id=114702).

## 启动程序

Openbox 特性支持在启动时运行程序.由 "openbox-session" 命令提供.

### 开启自启动

有两种方法实现自启动:

1.  如果用 startx 或 xinit 登陆到 X 会话, 修改 `~/.xinitrc`. 把 execute 行的 *openbox* 为 **openbox-session**.
2.  如果用 GDM/KDM , 那么选择 *Openbox* 会话它会自动执行自启动脚本.

### 自启动脚本

Openbox 执行一个位于`/etc/xdg/openbox/autostart`的系统级的脚本，然后会执行 `~/.config/openbox/autostart` 的用户自启动脚本。这个用户脚本默认不存在，需要用户自己创建。

全部说明可以从 Openbox 官网上找到:[Help:Autostart](http://openbox.org/wiki/Help:Autostart).

**注意:** 自启动脚本在 OpenBox 3.5 之前叫做 autostart.sh 。尽管现在也可以工作，还是建议升级过的用户手动去掉 .sh 扩展名。

### 自启动目录

Openbox 也会启动在 `/etc/xdg/autostart` 中的所有的 *.desktop 文件 - 这不管是否有用户启动脚本都会执行。例如，`nm-applet`,安装了一个文件到这个位置，如果用户在自启动脚本中放入通常的 `(sleep 3 && /usr/bin/nm-applet --sm-disable) &` 会导致运行两次。有一个关于这个的讨论和管理方法在 [这儿](https://bbs.archlinux.org/viewtopic.php?pid=993738)。

## 主题和外观

这篇添加的文章 **[Openbox Themes and Apps](/index.php/Openbox_Themes_and_Apps "Openbox Themes and Apps")** 有关于改变 Openbox's GUI 的详细信息.

你可能安装了一系列由不同的工具包开发的程序.某个程序的配置设定可能会在一个非期望的位置.

例如,[Geany](http://www.geany.org/)(一个IDE) 双击的设定由 `~/gtkrc2.0` 决定,而不是你所希望的 `~/.config/openbox/rc.xml`.一些 Geany 的可视外观同样由 .gtkrc-2.0 设定.

查阅添加的的 [Openbox Themes and Apps](/index.php/Openbox_Themes_and_Apps#Themes_and_appearance "Openbox Themes and Apps") 获得关于视觉主题的信息.

### Openbox 主题

Openbox主题的外观控制窗口边框,包括标题栏和标题栏按钮.他们还确定出现在应用程序的菜单和屏幕显示(OSD).更多的主题可以用以下命令从标准库得到:

```
# pacman -S openbox-themes

```

这个包并没有包含全部的 openbox 主题，你可以从以下网站获得更多的主题:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

下载的主题可以通过释放到 **~/.themes** 目录来安装或者通过使用ObConf工具来安装.

创建一个新的主题是相当容易的，并且可以从官方找到 [详细说明](http://icculus.org/openbox/index.php/Help:Themes).

### 鼠标指针,图标,壁纸

更多的 GUI 定制信息请看 [Openbox Themes and Apps](/index.php/Openbox_Themes_and_Apps#X11_Mouse_cursors "Openbox Themes and Apps").

## 提示与技巧

### Aero snap 特效

Windows 7 支持一种独特的窗口特性，当窗口移动到屏幕边缘的时候可以 snap 窗口。这种特效可以通过 Openbox 键盘绑定做到，参见[这里](http://ubuntuforums.org/showthread.php?t=1796793)。

### 文件关联

因为 Openbox 和你使用的一些程序不能很好地整合.你的(文件)浏览器可能会遇到一些问题.你的浏览器可能不会知道哪个程序使用哪种类型的文件.

AUR 上一个叫 [gnome-defaults-list](https://aur.archlinux.org/packages.php?ID=23170) 的软件包含了在 Gnome 桌面环境内指定的程序与文件类型清单. 清单安装在 `/etc/gnome/defaults.list.`

用文本编辑器打开这个文件.你可以替换选定的程序.例如, totem <=> vlc 或 eog <=> mirage. 保存文件 `~/.local/share/applications/defaults.list`.

另一种方法是从仓库安装 *perl-file-mimeinfo* 调用 **mimeopen** 类似这样:

```
mimeopen -d /path/to/file

```

会提示用哪个程序来打开 /path/to/file:

```
Please choose a default application for files of type text/plain
       1) notepad  (wine-extension-txt)
       2) Leafpad  (leafpad)
       3) OpenOffice.org Writer  (writer)
       4) gVim  (gvim)
       5) Other...

```

你的回答会变成打开这种类型文件使用的默认程序. Mimeopen 安装在 `/usr/bin/perlbin/vendor/mimetype`.

### 复制粘贴

终端上 **Ctrl+Insert** 是复制,而 **Shift+Insert** 是粘贴.

也可以是 **Ctrl+Shift+C** 复制,而 **mouse middle-click** 是粘贴 (终端里).

其它程序大多使用惯例的键盘快捷键来复制粘贴.

### 窗口透明

程序 transset-df (事实上与 *transset* 一样) 用 pacman -S transset-df 安装.有了 transset-df 你可以开启 window-transparency on-the-fly.

例如把以下内容加入 `~/.config/openbox/rc.xml`, 你就可以用鼠标滚轮在窗口标题栏转动滚轮来调节窗口透明度(在 <mouse> 段):

```
    <context name="Titlebar">
     . . .
     <mousebind button="Up" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --inc  </execute>
       </action>
     </mousebind>
     <mousebind button="Down" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --dec </execute>
       </action>
     </mousebind>
     . . .
   </context>

```

在动作组没有定义额外的动作时这种更改有效.

### 程序的 Xprop 值

如果你经常使用针对程序的设定, 你会发现以下 bash 别名很方便:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

执行 **`xp`** 点击正在运行的已经设置针对程序设定的程序. 结果会只显示 Openbox 需要的信息, 就是 WM_WINDOW_ROLE 和 WM_CLASS (名称和类别) 的值:

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

#### Xprop for Firefox

无论什么原因, Firefox 和相似的程序会忽略程序规则(例如 <desktop>) 除非 `class="Firefox*"` 已使用.这种用法不考虑任何 xprop 报告给程序的 WM_CLASS.

### 链接菜单到按键

有些人想链接 Openbox 菜单 (或其它菜单) 到一个目标.对于想创建一个面板按钮来弹出菜单会非常有用.虽然 Openbox 没有提供这种功能,一个程序名叫**xdotool** 能模拟一个击键动作. Openbox 可以配置绑定这个击键动作到 *ShowMenu* 动作.

包 [xdotool](https://aur.archlinux.org/packages.php?do_Details=1&ID=14789&O=0&L=0&C=0&K=xdotool&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd) 可以从 AUR 上得到.安装好 *xdotool* 后, 把以下内容添加到 **`rc.xml`** 的 <keyboard> 段 :

```
 <keybind key="A-C-q">
   <action name="ShowMenu">
     <menu>root-menu</menu>
   </action>
 </keybind>

```

Restart/reconfigure Openbox. 接下来的命令在你的光标位置弹出菜单.这个命令可以原样执行,或链接到一个目标,或放在脚本里.

```
$ xdotool key ctrl+alt+q

```

当然,改变为你喜欢的键盘快捷键. 这里是一个 **tint2** (一个类似任务栏的面板) 配置文件里的片断,当点击到时钟区时弹出一个菜单.每一个按键组合被设定为打开一个 openbox 的 **`rc.xml`** 配置文件里的菜单. 右击菜单与左击菜单不同:

```
clock_rclick_command = xdotool key --clearmodifiers "ctrl+XF86PowerOff"
clock_lclick_command = xdotool key --clearmodifiers "alt+XF86PowerOff"

```

### 在背景的 Urxvt

在桌面背景中运行一个终端对于 Openbox 来说很容易.你不需要 **devilspie**.

首先要开启透明, 打开 `.Xdefaults` (没有则在家目录建一个).

```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24    #我不使用全屏, 如果想使用全屏不要被这迷惑,看下面.
URxvt*borderLess:true
URxvt*foreground:Black   #前景色.我的壁纸是白色,你或者想把它改为白色.

```

接下来编辑 `.config/openbox/rc.xml` :

```
<application name="URxvt">
  <decor>no</decor>
  <focus>yes</focus>
  <position>
    <x>center</x>
    <y>20</y>
  </position>
  <layer>below</layer>
  <desktop>all</desktop>
  <maximized>true</maximized> #Only if you want a full size terminal.
</application>

```

神奇的地方来自 `<layer>below</layer>` 这行, 这把 urxvt 程序放在其它程序下面. 在这里 Urxvt 会在所有桌面显示,请按需更改.

注意:可以用其它名字代替 <application name="URxvt">, (例如 "URxvt-bg"), 还有当启动 urxvt 时使用 -name 选项. 这种方式, 只有重命名为 URxvf-bg 的 urxvt 终端会根据在 rc.xml 中设定的程序规则进行捕捉和修改.例如: urxvt -name URxvt-bg (大小写敏感)

#### ToggleShowDesktop 例外

当使用 ToggleShowDesktop 命令时上面的方法仍然会最小化 Urxvt .避免这种情况的方法在 [forum post](https://bbs.archlinux.org/viewtopic.php?pid=865844#p865844). 这包括修改 Urxvt's 源代码.

### 键盘音量控制

如果使用 ALSA,你可以使用 amixer 来调节音量. 你可以使用 Openbox 的按键绑定来模仿多媒体键. (或者,你想找出你真正的多媒体按键来作映射.) 例如, 在 rc.xml 的 <keyboard> 段:

```
   <keybind key="W-Up">
     <action name="Execute">
       <command>amixer set Master 5%+</command>
     </action>
   </keybind>

```

这会绑定 Windows 键 + 上箭头 来把 ALSA 主音量提高 5%. 下面是对应的音量下降的绑定:

```
   <keybind key="W-Down">
     <action name="Execute">
       <command>amixer set Master 5%-</command>
     </action>
   </keybind>

```

你也可以使用 XF86Audio 键绑定:

```
   <keybind key="XF86AudioRaiseVolume">
     <action name="Execute">
       <command>amixer set Master 5%+ unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioLowerVolume">
     <action name="Execute">
       <command>amixer set Master 5%- unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioMute">
     <action name="Execute">
       <command>amixer set Master toggle</command>
     </action>
   </keybind>

```

上面的例子在大多数的多媒体键盘上可以工作.这应该可以用相应的多媒体按键来增减你的声音设备的音量或静音.注意在例子中:

*   "Mute" 键如果当前在静音模式则应该取消静音.
*   "Raise" and "Lower" 键如果当前是静音则应该取消静音.

## 其他资源

*   [Openbox Website](http://openbox.org/) – The official website
*   [Planet Openbox](http://planetob.openmonkey.com/) – Openbox news portal
*   [Box-Look.org](http://www.box-look.org/) – A good resource for themes and related artwork
*   [Openbox Hacks and Configs Thread](https://bbs.archlinux.org/viewtopic.php?id=93126) @ Arch Linux Forums
*   [Openbox Screenshots Thread](https://bbs.archlinux.org/viewtopic.php?id=45692) @ Arch Linux Forums