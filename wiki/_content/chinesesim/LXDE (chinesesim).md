摘自 [LXDE.org | LXDE官方主页](http://lxde.org/):

	*The "Lightweight X11 Desktop Environment" is an extremely fast-performing and energy-saving desktop environment. Maintained by an international community of developers, it comes with a beautiful interface, multi-language support, standard keyboard short cuts and additional features like tabbed file browsing. LXDE uses less CPU and less RAM than other environments. It is especially designed for cloud computers with low hardware specifications, such as, netbooks, mobile devices (e.g. MIDs) or older computers.*

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 运行 LXDE](#.E8.BF.90.E8.A1.8C_LXDE)
    *   [2.1 显示管理器](#.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.2 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C)
*   [3 小提示](#.E5.B0.8F.E6.8F.90.E7.A4.BA)
    *   [3.1 自动挂载](#.E8.87.AA.E5.8A.A8.E6.8C.82.E8.BD.BD)
    *   [3.2 更换GTK主题 ，开启阴影和透明效果](#.E6.9B.B4.E6.8D.A2GTK.E4.B8.BB.E9.A2.98_.EF.BC.8C.E5.BC.80.E5.90.AF.E9.98.B4.E5.BD.B1.E5.92.8C.E9.80.8F.E6.98.8E.E6.95.88.E6.9E.9C)
    *   [3.3 更换鼠标指针主题](#.E6.9B.B4.E6.8D.A2.E9.BC.A0.E6.A0.87.E6.8C.87.E9.92.88.E4.B8.BB.E9.A2.98)
    *   [3.4 更换窗口管理器](#.E6.9B.B4.E6.8D.A2.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
*   [4 相关资源](#.E7.9B.B8.E5.85.B3.E8.B5.84.E6.BA.90)

## 安装

LXDE是模块化的，所以LXDE至少需要安装一个窗口管理器才能运行，譬如 [lxde-common](https://www.archlinux.org/packages/?name=lxde-common) 和 [openbox](https://www.archlinux.org/packages/?name=openbox) (或者其他的窗口管理器）。 这个[lxde](https://www.archlinux.org/groups/x86_64/lxde/) 页面包含了所有的LXDE组件。

你可以安装LXDE软件包组:

```
# pacman -S lxde

```

LXDE 是模块化的. 你可以从下面的列表中挑选你需要的包，最少要安装 [lxde-common](https://www.archlinux.org/packages/?name=lxde-common), [lxsession](https://www.archlinux.org/packages/?name=lxsession), [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) 和一个窗口管理器。

LXDE在arch中已经有一个软件包组，可以这样安装LXDE桌面环境：

```
# pacman -S lxde

```

这样就会下载Lxde软件包组中的软件包：

*   [gpicview](https://www.archlinux.org/packages/?name=gpicview): 轻量级图片查看工具
*   [libfm](https://www.archlinux.org/packages/?name=libfm): 一个文件管理器库 (lxshortcut: 一个编辑修改应用程序快捷键的工具。)
*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance): 配置 GTK＋的主题、图表主题以及应用程序使用的字体
*   [lxappearance-obconf](https://www.archlinux.org/packages/?name=lxappearance-obconf): 一个用于配置Openbox的LXAppearance插件。
*   [lxde-common](https://www.archlinux.org/packages/?name=lxde-common): 一个LXDE的默认配置
*   [lxde-icon-theme](https://www.archlinux.org/packages/?name=lxde-icon-theme): LXDE图标主题
*   [lxdm](https://www.archlinux.org/packages/?name=lxdm): 一个轻量级的显示管理器
*   [lxinput](https://www.archlinux.org/packages/?name=lxinput): 一个配置键盘和鼠标的小程序
*   [lxlauncher](https://www.archlinux.org/packages/?name=lxlauncher): 主要用于上网本的程序运行器
*   [lxmenu-data](https://www.archlinux.org/packages/?name=lxmenu-data): 用于适应 freedesktop.org 菜单文件。
*   [lxmusic](https://www.archlinux.org/packages/?name=lxmusic): 轻量级XMMS2客户端
*   [lxpanel](https://www.archlinux.org/packages/?name=lxpanel): LXDE 桌面面板
*   [lxrandr](https://www.archlinux.org/packages/?name=lxrandr): 屏幕管理器
*   [lxsession](https://www.archlinux.org/packages/?name=lxsession): X11标准兼容的会话管理器，支持关闭、重启和休眠
*   [lxtask](https://www.archlinux.org/packages/?name=lxtask): 轻量级任务管理器
*   [lxterminal](https://www.archlinux.org/packages/?name=lxterminal): 轻量级终端模拟器
*   [menu-cache](https://www.archlinux.org/packages/?name=menu-cache): 一个创建菜单的守护进程
*   [openbox](https://www.archlinux.org/packages/?name=openbox): LXDE 默认目前使用的一个轻量级的、基本兼容并且高度可配置的窗口管理器）。
*   [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm): LXDE 默认使用的轻量级文件管理程序，提供了桌面整合。which also provides desktop integration

安装完成后, 复制3个文件到`~/.config/openbox`:

也可以运行以下命令

```
mkdir -p ~/.config/openbox
cp /etc/xdg/openbox/{menu.xml,rc.xml,autostart} ~/.config/openbox

```

同时还需要安装[Gamin](/index.php/Gamin "Gamin")(一个文件和目录监视工具),它会按照程序的需要运行，不需要像[FAM](/index.php/FAM "FAM")一样使用守护进程。如果已经安装了FAM，删除它，停止服务，并安装gamin:

```
# pacman -S gamin

```

当然了，您或许也会对这些软件包感兴趣：[leafpad](https://www.archlinux.org/packages/?name=leafpad)（一款小巧的编辑器），[obconf](https://www.archlinux.org/packages/?name=obconf)（Openbox的窗口设定工具），[epdfview](https://www.archlinux.org/packages/?name=epdfview)（pdf阅读工具） [gamin](/index.php/Gamin "Gamin")

安装它们：

```
# pacman -S leafpad obconf epdfview

```

## 运行 LXDE

有很多种方式可以启动LXDE。

### 显示管理器

如果你用一个像[GDM](/index.php/GDM "GDM"), [KDM](/index.php/KDM "KDM"), 或者 [SLiM](/index.php/SLiM "SLiM")的 [显示管理器](/index.php/Display_manager "Display manager") 启动LXDE. 请参考display manager的页面.

介绍[LXDM](/index.php/LXDM "LXDM"),一个LXDE项目中的据试验性的显示管理器被放在 [这里了](/index.php/LXDE#LXDM "LXDE").

如果你不使用显示管理器的话，添加

```
export DESKTOP_SESSION=LXDE

```

到你的 ~/.bash_profile 在别的任何xdg-open之前

### 命令行

从命令行启用到桌面，有多种方式可选

如果使用 "startx"，你需要在你的`~/.xinitrc`文件最后添加

```
exec startlxde

```

如果你想开机自动运行“startx”，可以看看页面[Starting X at boot](/index.php/Start_X_at_Boot#Starting_X_as_preferred_user_without_logging_in "Start X at Boot")

对于其它任务，你可能需要保证"dbus"以守护进程运行

详情可查看 [xinitrc](/index.php/Xinitrc "Xinitrc")，如保持会话等

## 小提示

### 自动挂载

[PCManFM#Volume_handling](/index.php/PCManFM#Volume_handling "PCManFM")

### 更换GTK主题 ，开启阴影和透明效果

如果您对您现在的GTK主题不太满意，您可以通过Lxappearance来改换。LXDE支持部分Gnome的GTK主题，您可以从GnomeLook这样的网站下载，然后通过Lxappearance来安装。您个人的主题一般放在您用户目录下的.themes文件夹中。 如果非常不幸，您的Lxappearance似乎不能拿来安装主题，那么，您可以试着安装 gtk-theme-switch2来安装GTK主题：

```
# pacman -S gtk-theme-switch2

```

这是一个极简易的小程序，并且您只能从终端输入switch2来启动它：

```
# switch2

```

安装，选择好您的GTK主题后，别忘了点选“Apply”，以使其生效。 至于开启阴影效果，您可以通过安装xcompmgr来实现：

```
# pacman -S xcompmgr

```

xcompmgr是命令行的工具，没有图形化的界面来供您设置，因此，您只能从终端里设置并开启。有许多人认为，这样设置最适合：

```
# xcompmgr -Ss -n -Cc -fF -I-10 -O-10 -D1 -t-3 -l-4 -r4 &

```

您可以在/etc/xdg/lxsession/LXDE/autostart中将其设置为自启动的，比如：

```
@xcompmgr -Ss -n -Cc -fF -I-10 -O-10 -D1 -t-3 -l-4 -r4 &

```

这样，您每次开机就会自动开启阴影效果了。 如果您希望您的窗口有透明的效果，您可以安装transset-df来实现：

```
# pacman -S transset-df

```

安装完后，您可以在终端下键入transset-df，回车后，鼠标指针会变成十字形，然后在您希望得到透明效果的程序界面上，单击鼠标左键，您就能得到透明效果了。 当然，您也可以采用Keybind（键绑定）的方式来开启透明效果。有人给出了这样的方案，即用您喜欢的编辑器打开您用户目录下的.config/openbox/lxde-rc.xml文件，在该配置文件的Titlebar那一行下面添上：

```
<mousebind button="Up" action="Click">
<action name="Execute">
<execute>transset-df -p -x 1.0 --inc 0.1 </execute>
</action>
</mousebind>
<mousebind button="Down" action="Click">
<action name="Execute">
<execute>transset-df -p -m 0.1 --dec 0.1</execute>
</action>
</mousebind>

```

完成后，保存退出。这样，当您将鼠标悬停到某个程序界面的标题栏时，您就可以用鼠标滚轮来开启并调控透明效果了。

### 更换鼠标指针主题

目前，LXDE还没有提供一个程序来直接调整鼠标指针主题，因此，您只能通过对X Cursor的配置来调整。参见[X11 Cursors](/index.php/X11_Cursors "X11 Cursors")。

### 更换窗口管理器

根据个人喜好，你可以很容易的更换LXDE默认的窗口管理器，比如fvwm, icewm, dwm,awesome等等

你窗口管理器的设置保存在下面这个文件中：

	/etc/xdg/lxsession/LXDE/default

比如说,你的/etc/xdg/lxsession/LXDE/default可能是这个样子的:

```
smproxy
openbox
lxpanel

```

smproxy 是一个由xorg提供的程序. 他可以为那些不支持X11 R6会话管理机制的程序提供会话管理支持

所以强烈要求你保留此行。

openbox是当前的窗口管理器，你可以用你自己喜欢的来替代之。

## 相关资源

*   [LXDE项目](http://lxde.sourceforge.net)
*   [最新组件](https://sourceforge.net/project/showfiles.php?group_id=180858)
*   [PCMan文件管理器](https://sourceforge.net/project/showfiles.php?group_id=156956)