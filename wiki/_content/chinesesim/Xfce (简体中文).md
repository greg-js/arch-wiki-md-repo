**翻译状态：** 本文是英文页面 [Xfce](/index.php/Xfce "Xfce") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-07-10，点击[这里](https://wiki.archlinux.org/index.php?title=Xfce&diff=0&oldid=242786)可以查看翻译后英文页面的改动。

[Xfce](http://www.xfce.org) 是一个轻量级模块化的 [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)") 现基于 GTK+ 2。为了提供完整的用户体验，它包含窗口管理器、文件管理器、桌面和面板。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动Xfce](#.E5.90.AF.E5.8A.A8Xfce)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 菜单](#.E8.8F.9C.E5.8D.95)
        *   [3.1.1 Whisker menu](#Whisker_menu)
        *   [3.1.2 编辑项](#.E7.BC.96.E8.BE.91.E9.A1.B9)
    *   [3.2 桌面](#.E6.A1.8C.E9.9D.A2)
        *   [3.2.1 图标文字的背景透明](#.E5.9B.BE.E6.A0.87.E6.96.87.E5.AD.97.E7.9A.84.E8.83.8C.E6.99.AF.E9.80.8F.E6.98.8E)
        *   [3.2.2 从右击菜单中剔除Thunar选项](#.E4.BB.8E.E5.8F.B3.E5.87.BB.E8.8F.9C.E5.8D.95.E4.B8.AD.E5.89.94.E9.99.A4Thunar.E9.80.89.E9.A1.B9)
        *   [3.2.3 杀死窗口的快捷键](#.E6.9D.80.E6.AD.BB.E7.AA.97.E5.8F.A3.E7.9A.84.E5.BF.AB.E6.8D.B7.E9.94.AE)
    *   [3.3 会话](#.E4.BC.9A.E8.AF.9D)
        *   [3.3.1 自启动程序](#.E8.87.AA.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)
            *   [3.3.1.1 延迟自启动应用程序](#.E5.BB.B6.E8.BF.9F.E8.87.AA.E5.90.AF.E5.8A.A8.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
        *   [3.3.2 锁定屏幕](#.E9.94.81.E5.AE.9A.E5.B1.8F.E5.B9.95)
        *   [3.3.3 切换用户](#.E5.88.87.E6.8D.A2.E7.94.A8.E6.88.B7)
        *   [3.3.4 禁用会话](#.E7.A6.81.E7.94.A8.E4.BC.9A.E8.AF.9D)
        *   [3.3.5 默认窗口管理器](#.E9.BB.98.E8.AE.A4.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [3.4 更换主题](#.E6.9B.B4.E6.8D.A2.E4.B8.BB.E9.A2.98)
    *   [3.5 声音](#.E5.A3.B0.E9.9F.B3)
        *   [3.5.1 使用OSS驱动如何让xfce4-mixer来控制音量](#.E4.BD.BF.E7.94.A8OSS.E9.A9.B1.E5.8A.A8.E5.A6.82.E4.BD.95.E8.AE.A9xfce4-mixer.E6.9D.A5.E6.8E.A7.E5.88.B6.E9.9F.B3.E9.87.8F)
        *   [3.5.2 使用快捷键改变音量](#.E4.BD.BF.E7.94.A8.E5.BF.AB.E6.8D.B7.E9.94.AE.E6.94.B9.E5.8F.98.E9.9F.B3.E9.87.8F)
            *   [3.5.2.1 ALSA](#ALSA)
            *   [3.5.2.2 OSS](#OSS)
            *   [3.5.2.3 Xfce4-volumed](#Xfce4-volumed)
            *   [3.5.2.4 Volumeicon](#Volumeicon)
        *   [3.5.3 加入启动音效](#.E5.8A.A0.E5.85.A5.E5.90.AF.E5.8A.A8.E9.9F.B3.E6.95.88)
    *   [3.6 键盘快捷键](#.E9.94.AE.E7.9B.98.E5.BF.AB.E6.8D.B7.E9.94.AE)
    *   [3.7 Polkit 身法认证代理](#Polkit_.E8.BA.AB.E6.B3.95.E8.AE.A4.E8.AF.81.E4.BB.A3.E7.90.86)
*   [4 提示和小技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [4.1 从 thunar 和 xfdesktop 隐藏分区](#.E4.BB.8E_thunar_.E5.92.8C_xfdesktop_.E9.9A.90.E8.97.8F.E5.88.86.E5.8C.BA)
    *   [4.2 屏幕截图](#.E5.B1.8F.E5.B9.95.E6.88.AA.E5.9B.BE)
    *   [4.3 禁用终端 F1 和 F11 快捷方式](#.E7.A6.81.E7.94.A8.E7.BB.88.E7.AB.AF_F1_.E5.92.8C_F11_.E5.BF.AB.E6.8D.B7.E6.96.B9.E5.BC.8F)
        *   [4.3.1 终端的颜色主题和调色板](#.E7.BB.88.E7.AB.AF.E7.9A.84.E9.A2.9C.E8.89.B2.E4.B8.BB.E9.A2.98.E5.92.8C.E8.B0.83.E8.89.B2.E6.9D.BF)
        *   [4.3.2 更改默认颜色主题](#.E6.9B.B4.E6.94.B9.E9.BB.98.E8.AE.A4.E9.A2.9C.E8.89.B2.E4.B8.BB.E9.A2.98)
        *   [4.3.3 修改默认颜色主题](#.E4.BF.AE.E6.94.B9.E9.BB.98.E8.AE.A4.E9.A2.9C.E8.89.B2.E4.B8.BB.E9.A2.98)
    *   [4.4 终端之Tango主题](#.E7.BB.88.E7.AB.AF.E4.B9.8BTango.E4.B8.BB.E9.A2.98)
    *   [4.5 颜色管理](#.E9.A2.9C.E8.89.B2.E7.AE.A1.E7.90.86)
    *   [4.6 多显示器](#.E5.A4.9A.E6.98.BE.E7.A4.BA.E5.99.A8)
    *   [4.7 SSH 代理](#SSH_.E4.BB.A3.E7.90.86)
    *   [4.8 Scroll a background window without shifting focus on it](#Scroll_a_background_window_without_shifting_focus_on_it)
    *   [4.9 修改鼠标按键](#.E4.BF.AE.E6.94.B9.E9.BC.A0.E6.A0.87.E6.8C.89.E9.94.AE)
*   [5 常见问题与解答](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98.E4.B8.8E.E8.A7.A3.E7.AD.94)
    *   [5.1 Xfce4-xkb-plugin settings issue](#Xfce4-xkb-plugin_settings_issue)
    *   [5.2 Thunar 不显示缩略图](#Thunar_.E4.B8.8D.E6.98.BE.E7.A4.BA.E7.BC.A9.E7.95.A5.E5.9B.BE)
    *   [5.3 Locales 设置被GDM忽略](#Locales_.E8.AE.BE.E7.BD.AE.E8.A2.ABGDM.E5.BF.BD.E7.95.A5)
    *   [5.4 恢复默认设置](#.E6.81.A2.E5.A4.8D.E9.BB.98.E8.AE.A4.E8.AE.BE.E7.BD.AE)
    *   [5.5 NVIDIA 和 xfce4-sensors-plugin](#NVIDIA_.E5.92.8C_xfce4-sensors-plugin)
    *   [5.6 会话错误](#.E4.BC.9A.E8.AF.9D.E9.94.99.E8.AF.AF)
    *   [5.7 升级Xfce 4.10以后window buttons不能自动扩展长度](#.E5.8D.87.E7.BA.A7Xfce_4.10.E4.BB.A5.E5.90.8Ewindow_buttons.E4.B8.8D.E8.83.BD.E8.87.AA.E5.8A.A8.E6.89.A9.E5.B1.95.E9.95.BF.E5.BA.A6)
    *   [5.8 Preferred Applications preferences have no effect](#Preferred_Applications_preferences_have_no_effect)
    *   [5.9 Action Buttons in the panel are missing icons](#Action_Buttons_in_the_panel_are_missing_icons)
    *   [5.10 修改挂载参数](#.E4.BF.AE.E6.94.B9.E6.8C.82.E8.BD.BD.E5.8F.82.E6.95.B0)
*   [6 相关文章](#.E7.9B.B8.E5.85.B3.E6.96.87.E7.AB.A0)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) 包组。如果需要的话，还可以安装 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 包组。此包组提供了一些额外的插件和一些有用的工具，如 [mousepad](https://www.archlinux.org/packages/?name=mousepad) 编辑器。

## 启动Xfce

从显示管理器（[display manager](/index.php/Display_manager "Display manager")）选择_Xfce Session_，或者添加 `exec startxfce4` 到 [Xinitrc](/index.php/Xinitrc "Xinitrc")中。

**注意:** 不要直接启动 `xfce4-session`，因为它已经被 `startxfce4` 运行了。

## 配置

Xfce把配置的选项保存到[Xfconf](http://docs.xfce.org/xfce/xfconf/start)。有几个方式来修改这些选项：

*   在主菜单中，选择[Settings](http://docs.xfce.org/xfce/xfce4-settings/start)，选择想要修改的选项。选项实际上是位于`/usr/bin/xfce4-*`和`/usr/bin/xfdesktop-settings`中的程序。
*   `xfce4-settings-editors`能看到和修改所有的设置。此处修改的选项会立即生效。使用`xfconf-query`来通过命令行设置；[文档中](http://docs.xfce.org/xfce/xfconf/xfconf-query)有更多的细节。
*   设置保存在XML文件中。此文件位于`~/.config/xfce4/xfconf/xfce-perchannel-xml/`，也可以手动修改文件。但是，此处的修改不会立即生效。

### 菜单

#### Whisker menu

[xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) 是一个可选应用启动器。它可以显示所有的已安装应用中最喜欢和经常被使用的应用。

#### 编辑项

有一些工具可以用来实现此项需求

*   **XAME** — 使用Gambas编写，用于Xfce编辑菜单项的图形工具，在其他环境中没有效果。

	[http://www.redsquirrel87.com/XAME.html](http://www.redsquirrel87.com/XAME.html) || [xame](https://aur.archlinux.org/packages/xame/)

*   **MenuLibre** — 一个高级的菜单编辑器，提供了一个纯粹，易用的界面。

	[https://launchpad.net/menulibre](https://launchpad.net/menulibre) || [menulibre](https://aur.archlinux.org/packages/menulibre/)

*   **Alacarte** — GNOME的菜单编辑器。

	[http://www.gnome.org/](http://www.gnome.org/) || [alacarte](https://www.archlinux.org/packages/?name=alacarte)

当然，也可以手动创建 `~/.config/menus/xfce-applications.menu` 。下面给出一个示例的配置：

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
  "[http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd](http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd)">

```

```
<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

```

```
    <Exclude>
        <Filename>xfce4-run.desktop</Filename>
        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>
        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

```

```
    <Layout>
        <Merge type="all"/>
        <Separator/>
        <Menuname>Settings</Menuname>
        <Separator/>
        <Filename>xfce4-session-logout.desktop</Filename>
    </Layout>
</Menu>

```

`<MergeFile>` 标签包含了默认的Xfce菜单。

`<Exclude>` 标签剔除了你不想在菜单中出现的应用程序。尽管此处我们只剔除了一些Xfce的默认快捷方式，但是你也可以剔除 `firefox.desktop` 或其他任何的应用程序。

`<Layout>` 标签定义了菜单的布局。应用程序可以被放在文件夹中，或任何我们想要的组织方式。在 [Xfce wiki](http://wiki.xfce.org/howto/customize-menu) 有更多的详细信息。

你可以通过编辑 `.desktop` 本身来改变Xfce的菜单。隐藏项，可以参见 [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries")。你可以改变 `Categories=` 桌面项的行，以编辑应用程序的标签（category）。参见 [Desktop entries#File example](/index.php/Desktop_entries#File_example "Desktop entries")。

### 桌面

#### 图标文字的背景透明

默认桌面图标的文字是白色背景，可以创建或者修改 `~/.gtkrc-2.0`来得到不一样的效果：

```
style "xfdesktop-icon-view" {
    XfdesktopIconView::label-alpha = 10
    base[NORMAL] = "#000000"
    base[SELECTED] = "#71B9FF"
    base[ACTIVE] = "#71B9FF"
    fg[NORMAL] = "#fcfcfc"
    fg[SELECTED] = "#ffffff"
    fg[ACTIVE] = "#ffffff"
}
widget_class "*XfdesktopIconView*" style "xfdesktop-icon-view"

```

#### 从右击菜单中剔除Thunar选项

使用如下的命令：

```
$ xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0

```

#### 杀死窗口的快捷键

Xfce没有杀死窗口的快捷键，当程序假死时，我们可能需要这样的快捷键。

通过包 [xorg-xkill](https://www.archlinux.org/packages/?name=xorg-xkill)，使用 `xkill` 来交互时的杀掉一个窗口。对于当下的激活窗口，使用包 [xdotool](https://www.archlinux.org/packages/?name=xdotool)：

```
$ xdotool getwindowfocus windowkill

```

也可以：

```
$ xkill -id "$(xprop -root -notype | sed -n '/^_NET_ACTIVE_WINDOW/ s/^.*# *\|\,.*$//g p')"

```

添加快捷键，使用 **设置 > 键盘** 或者使用应用程序，如 [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys)。

### 会话

#### 自启动程序

可以在 **程序 > 设置 > 设置管理器 > 会话和自启动** 中，设置与Xfce一起启动的自启动程序。 此处列出了所有自启动的程序。点击 **添加** 按钮后可以添加自定义的自启动任务。

当然，也可以选择命令行脚本来启动你需要的程序。包括给GUI运行时设置必须的变量。

*   复制文件 `/etc/xdg/xfce4/xinitrc` 到 `~/.config/xfce4/`
*   编辑此文件。 比如，你可以添加一些如下的命令行到文件中：

```
source $HOME/.bashrc
# start rxvt-unicode server
urxvtd -q -o -f

```

##### 延迟自启动应用程序

有时候，延迟某个应用程序的自启动是很有用的。特别是如 `sleep 3 && command` 这样的命令在自启动中是不起作用的。与之相对，你需要使用如下的语法来替代：

```
sh -c "sleep 3 && command"

```

#### 锁定屏幕

**Tip:** The [light-locker](https://www.archlinux.org/packages/?name=light-locker) 对话锁定集成在 [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) 包中。 如果安装了亮度控制, '安全’标签页会加入到电源管理设定中。已经有的'到系统休眠时锁定屏幕'的选项会集成到'安全'标签页中。

锁定Xfce4对话（通过`xflock4`），如下包中至少需要安装一个：[xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock) 和 [xlockmore](https://www.archlinux.org/packages/?name=xlockmore)。You may also make a local copy of _xflock4_, for example `/usr/local/bin/xflock4`, which specifies another screen locker of choice.

为了改变屏保，或通过 Whisker Menu (**Properties > Behavior > Lock Screen**)这样的程序改变。可以在[List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security") 看到其他的选项。

#### 切换用户

**注意:** 想要不用GDM而能切换用户, 需要安装一个DM:

*   For LXDM - [LXDM#Simultaneous users and switching users](/index.php/LXDM#Simultaneous_users_and_switching_users "LXDM").
*   For LightDM - [LightDM (简体中文)#Xfce4 下多用户切换](/index.php/LightDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Xfce4_.E4.B8.8B.E5.A4.9A.E7.94.A8.E6.88.B7.E5.88.87.E6.8D.A2 "LightDM (简体中文)").

只要 [Display manager](/index.php/Display_manager "Display manager") 有切换用户的功能，Xfce4都是可以支持的，比如 [LightDM](/index.php/LightDM "LightDM") 和 [GDM](/index.php/GDM "GDM") 。关于你所使用的DM的信息，需要参看其wiki页面。当你已经安装并配置好你的DM之后，你就可以通过'actions buttons'菜单项来切换用户。

#### 禁用会话

Xfce kiosk 模式可以用来彻底禁用对话的保存。为了禁用对话，创建或者编辑 `/etc/xdg/xfce4/kiosk/kioskrc` 并加入如下的行：

```
[xfce4-session]
SaveSession=NONE

```

如果kiosk模式不能工作，用户可以给对话目录设置 r/o 权限：

```
$ rm ~/.cache/sessions/* && chmod 500 ~/.cache/sessions

```

此操作会防止Xfce保存所有的会话，除了设置和配置。

#### 默认窗口管理器

**注意:** 为了使你做的更改能起作用，在设置后你必须清楚以保存的会话，并确保初次登出时没有勾选保存会话。当更改奇效后，可以再开启保存会话

窗口管理器的全局设定保存在 `/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml`。单独用户的配置，可以通过执行下面的命令获得：

```
$ cp /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

这些文件中，窗口管理器的配置只有在 **Client0_Command**下面的才会起作用。此行必须把 `<value type="string" value="xfwm4"/>` 改为 `<value type="string" value="window_manager_executable"/>` 

也可以运行命令 `window_manager --replace`， 用你的窗口管理器的名字来替代其中的 **window_manger**，比如 `metacity`。

如果使能了保存会话，在你登出时还在运行的窗口，在你下次登入是会自动打开运行。

**注意:** 如果你使用了自启动列表来启动你的窗口管理器，那么建议你禁用保存会话。如果保存会话没有使能，窗口管理器可以会在登入时启动两次。

如果你不想用保存会话，你也可以添加把需要的窗口管理器启动添加到Xfce的自启动列表。可以在主菜单中 _Settings Manager > Session and Startup > Application Autostart_然后点击 _Add_。在 _Command_ 输入正确的命令启动需要的窗口管理器，然后可以起添加名字和描述。点击 _Ok_ ，然后登出再登入，就能生效。（原谅这个翻译，我并不使用中文的Xfce界面，所以并不知道这些设置对应的翻译是怎么样的，请求别人翻译）

### 更换主题

在 [xfce-look.org](http://www.xfce-look.org) 上有不少XFCE的主题。 _Xfwm_ 的主题保存在 `/usr/share/themes/xfce4`, 在 _Settings > Window Manager_中可以更改主题。 而[GTK+](/index.php/GTK%2B "GTK+") 主题在 _Settings > Appearance_。

如果想要使所有的应用能有一个统一的外观, 参见 [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications")获得更多的信息。

相关主题在 [Cursor themes](/index.php/Cursor_themes "Cursor themes"), [Icons](/index.php/Icons "Icons"), 和 [Font configuration](/index.php/Font_configuration "Font configuration") 中。

### 声音

[xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) 是 Xfce 组开发的用户混音程序和面板插件，是 xfce4 组的一部分，所以应该已经安装。它使用 [gstreamer](https://www.archlinux.org/packages/?name=gstreamer) 作为控制音量的后端，所以必须安装 xfce4-mixer 列出的可选依赖关系，否则点击时会出现如下错误：

```
 GStreamer was unable to detect any sound devices. Some sound system specific GStreamer packages may be missing. It may also be a permissions problem.

```

需要的插件由硬件觉得，大部分用户需要 [安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 软件包 [gstreamer0.10-base-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-base-plugins). 如果面板已经启动，安装后需要重新登陆，或删除再加入。如果不能工作，可能还需要其他插件如[gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) 或 [gstreamer0.10-bad-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-bad-plugins).

更多关于默认声卡的设置请阅读 [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture")。此外还可以使用 [PulseAudio](/index.php/PulseAudio "PulseAudio") 和 [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

#### 使用OSS驱动如何让xfce4-mixer来控制音量

新版的xfce4-mixer使用了gstreamer作为后端，这样就不用直接与驱动交流，更加统一。与驱动打交道的工作交给了gstreamer。因此如果你xfce4-mixer无法正常工作，就需要配置好gstreamer。首先当然你得安装xfce4-mixer。

```
 pacman -S xfce4-mixer gstreamer0.10-base-plugins

```

你需要至少安装gstreamer0.10-good-plugins,考虑安装gstreamer0.10-bad-plugins

```
 pacman -S gstreamer0.10-good-plugins gstreamer0.10-bad-plugins

```

然后删除面板上的mixer插件，然后重新添加一次，或者先登出然后再登录一次，对gstreamer做更改后必须这样做才能让操作生效。

也能够下载PKGBUILD 或者其他你需要的ABS[here](https://projects.archlinux.org/svntogit/packages.git/tree/gstreamer0.10-good/repos), 修改 PKGBUILD, 添加参数 --enable-oss.

```
 ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
   **--enable-oss \**
   --disable-static --enable-experimental \
   --disable-schemas-install \
   --disable-hal \
   --with-package-name="GStreamer Good Plugins (Archlinux)" \
   --with-package-origin="[https://www.archlinux.org/](https://www.archlinux.org/)"

```

然后开始安装：

```
 makepkg -i

```

如果仍然失败，就到论坛发贴求助，或者到OSS官方论坛查看[[1]](http://www.4front-tech.com/forum/)

#### 使用快捷键改变音量

使用xbindkeys也可以达到相同的效果。

```
Settings --> Keyboard

```

单击"Application Shortcuts" 选项卡中 "Add" 按钮. 输入命令即可添加快捷键了。

##### ALSA

升高音量：

```
amixer set Master 5%+

```

降低音量：

```
amixer set Master 5%-

```

静音：

```
amixer set Master toggle

```

你如果使用的是标准的XF86Audio 快捷键，在在终端输入以下内容：

```
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioRaiseVolume -n -t string -s "amixer set Master 5%+ unmute"
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioLowerVolume -n -t string -s "amixer set Master 5%- unmute"
xfconf-query -c xfce4-keyboard-shortcuts -p /commands/custom/XF86AudioMute -n -t string -s "amixer set Master toggle"

```

若 `amixer set Master toggle` 不工作，尝试使用调节PCM直接调节音量(`amixer set PCM toggle`) 。

这个频段必须使用 "mute" 参数工作。要检查计算机是否支持mute，运行 `alsamixer` 在终端查看Master条上是否有两个 M (MM) 。 若没有显示，则你的电脑可能不支持 mute 参数。假如你不得不切换使用 PCM 改变音量，那必须确保你的 xfce-mixer 也要调节 PCM 通道，而不是普通的 Master 通道。

##### OSS

使用脚本文件: [[http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Using_multimedia_keys_with_OSS](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Using_multimedia_keys_with_OSS) ]

如果你使用ossvol (推荐): 升高音量：

```
ossvol -i 1

```

降低音量：

```
ossvol -d 1

```

静音/取消静音：

```
ossvol -t

```

如果使用 pulseaudio 时 xfce4-volumed 无法静音，请尝试：

```
xfconf-query -c xfce4-mixer -p /active-card -s `xfconf-query -c xfce4-mixer -p /sound-card`

```

##### Xfce4-volumed

来自[AUR](/index.php/AUR "AUR") 的 [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/) daemon 能自动识别键盘的多媒体按键并映射到 Xfce-mixer。并能通过OSD通知音量变化的情况。Xfce4-volumed 不需要任何设置即可开始工作。

假如你使用pulseaudio 和 xfce4-volumed 取消静音不能正常使用，可以按照上面的 pulseaudio 部分修改 pactl 命令的键盘命令。

##### Volumeicon

[volumeicon](https://www.archlinux.org/packages/?name=volumeicon) is an alternative to xfce4-volumed in the community repo also handling keybindings and notifications through [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd).

#### 加入启动音效

Arch中并没有内置启动音效的设置页面, 但是您可以通过把下面的字段加入程序自启动设置来实现:

```
aplay /boot/startupsound.wav

```

音频文件的来源和名称可以随意指定, 但是在命名时请尽量简明并保证文件的小巧，把音频文件放入`/boot`目录即可。

### 键盘快捷键

键盘快捷键在两个地方定义： _Settings > Window Manager > Keyboard_ 和 _Settings > Keyboard > Shortcuts_。

### Polkit 身法认证代理

在安装 [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session) 时，会一起安装 [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) 代理，并会随系统自动启动;并不主要用户的干预。更多信息，参见 [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit")。

Xfce可用的第三方的 Polkit 身法认证代理，参见 [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/)。

## 提示和小技巧

### 从 thunar 和 xfdesktop 隐藏分区

参见 [Udisks#Hide selected partitions](/index.php/Udisks#Hide_selected_partitions "Udisks").

### 屏幕截图

Xfce 有自己的截图工具, [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter).它是 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 包组的一部分.

到 _应用程序 > 设置 > 键盘_, _应用程序快捷方式_. 添加 `xfce4-screenshooter -f` (或 `-w` 为活动窗口)命令用 `Print` 打印键截屏. 其他可选参数参见 screenshooter 的 man 手册

此外，也可用其他独立的截图程式如 [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot")

### 禁用终端 F1 和 F11 快捷方式

The xfce terminal binds F1 and F11 to help and fullscreen, respectively, which can make using programs like htop difficult. To disable those shortcuts, create or edit its configuration file, then log out and log back in. F10 can disabled in the Preferences menu.

 `~/.config/xfce4/terminal/accels.scm` 

```
(gtk_accel_path "<Actions>/terminal-window/fullscreen" "")
(gtk_accel_path "<Actions>/terminal-window/contents" "")

```

#### 终端的颜色主题和调色板

可以在首选项的外观标签下修改中断主题颜色和调色板. 这些色彩可用于多大数控制台程序如[Emacs](/index.php/Emacs "Emacs"), [Vi](/index.php/Vi "Vi")等. 它们的设置单独存储在每个用户的`~/.config/xfce4/terminal/terminalrc`文件. 还有更多主题可供选择. [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818) 查找更多终端配色方案

#### 更改默认颜色主题

XFCE 的 `extra/terminal` 包带有暗色调色板. To change this, append the following in your terminalrc file for a lighter color theme, that is always visible in darker Terminal backgrounds.

```
~/.config/xfce4/terminal/terminalrc

```

```
ColorPalette5=#38d0fcaaf3a9
ColorPalette4=#e013a0a1612f
ColorPalette2=#d456a81b7b42
ColorPalette6=#ffff7062ffff
ColorPalette3=#7ffff7bd7fff
ColorPalette13=#82108210ffff

```

#### 修改默认颜色主题

XFCE的`extra/terminal`包使用了较暗的颜色使得文字在默认的黑色背景下很难阅读并会使人感到不适，请把以下文字写入到terminalrc文件中来使用一个较明亮的颜色主题, 它会在一直在较暗的终端背景下可见.

```
~/.config/xfce4/terminal/terminalrc

```

```
ColorPalette5=#38d0fcaaf3a9
ColorPalette4=#e013a0a1612f
ColorPalette2=#d456a81b7b42
ColorPalette6=#ffff7062ffff
ColorPalette3=#7ffff7bd7fff
ColorPalette13=#82108210ffff

```

### 终端之Tango主题

用你喜欢的编辑器打开`~/.config/xfce4/terminal/terminalrc`加入：

```
ColorForeground=White
ColorBackground=#323232323232
ColorPalette1=#2e2e34343636
ColorPalette2=#cccc00000000
ColorPalette3=#4e4e9a9a0606
ColorPalette4=#c4c4a0a00000
ColorPalette5=#34346565a4a4
ColorPalette6=#757550507b7b
ColorPalette7=#060698989a9a
ColorPalette8=#d3d3d7d7cfcf
ColorPalette9=#555557575353
ColorPalette10=#efef29292929
ColorPalette11=#8a8ae2e23434
ColorPalette12=#fcfce9e94f4f
ColorPalette13=#72729f9fcfcf
ColorPalette14=#adad7f7fa8a8
ColorPalette15=#3434e2e2e2e2
ColorPalette16=#eeeeeeeeecec

```

### 颜色管理

Xfce has no native support for colour management. [[2]](https://bugzilla.xfce.org/show_bug.cgi?id=8559) See [ICC profiles](/index.php/ICC_profiles "ICC profiles") for alternatives.

### 多显示器

As of [xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) version 4.11.4, Xfce has support for multiple monitors. Settings can be configured in the _Applications_ -> _Settings_ -> _Display_ dialog. For more information, see the [display](http://docs.xfce.org/xfce/xfce4-settings/display) article from the Xfce documentation.

### SSH 代理

By default Xfce 4.10 will try to load gpg-agent or ssh-agent in that order during session initialization. To disable this, create an xfconf key using the following command:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

To force using ssh-agent even if gpg-agent is installed, run the following instead:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

To use [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), simply tick the checkbox _Launch GNOME services on startup_ in the _Advanced_ tab of _Session Manager_ in Xfce's settings. This will also disable gpg-agent and ssh-agent.

Source: [http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### Scroll a background window without shifting focus on it

Go to _Main Menu > Settings > Window Manager Tweaks > Accessibility_ tab. Uncheck _Raise windows when any mouse button is pressed_.

### 修改鼠标按键

By default, the mouse button modifier in Xfce is set to `Alt`. This can be changed with _xfconf-query_. For instance, the following command will set the `Super` key as the mouse button modifier:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Super"

```

Strictly speaking, using multiple modifiers is not supported. However, as a workaround, multiple modifiers can be specified if the key names are separated with `><`. For instance, to set `Ctrl+Alt` as the mouse button modifier, you can use the following command:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Ctrl><Alt"

```

## 常见问题与解答

### Xfce4-xkb-plugin settings issue

There is a bug in version _0.5.4.1-1_ which causes xkb-plugin to _lose keyboard, layout switching and compose key_ settings. As a workaround you may enable _Use system defaults_ option in keyboard settings. To do so run

```
xfce4-keyboard-settings

```

Go to _Layout_ tab and set the _Use system defaults_ flag, then reconfigure xkb-plugin.

### Thunar 不显示缩略图

Thunar 已经支持 **Tumbler** 选项，只要安装Tumbler:

```
pacman -S tumbler

```

更详细内容请参考 [Thunar Wiki](/index.php/Thunar_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Thunar_Thumbnailers "Thunar (简体中文)").

### Locales 设置被GDM忽略

成为超级用户添加locales到 /var/lib/AccountsService/users/$USER:

```
su -c "nano /var/lib/AccountsService/users/$USER"

```

用你自己的locales代替 hu_HU.UTF-8 :

```
[User]
Language=hu_HU.UTF-8
XSession=xfce

```

也可以利用sed程序。 注意在 .UTF-8前面加 "/":

```
su -c "sed -i 's/Language=.*/Language=hu_HU\.UTF-8/' /var/lib/AccountsService/users/$USER"

```

重启GDM。

### 恢复默认设置

若你折腾到想还原xfce4的默认设置,重命名 `~/.config/xfce4-session/` 和 `~/.config/xfce4/`就可以了XD

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

注销后生效。

### NVIDIA 和 xfce4-sensors-plugin

要探测NVIDIA的gpu温度需要安装 [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) 并且重新编译 [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) 软件包。

### 会话错误

如果窗口管理器不能正常运行（鼠标是一个X形，或者不能关闭窗口），不能正常还原，这时候说明会话出错。 删除掉session及其`.cache` 文件夹。

```
# rm -r ~/.cache/sessions/

```

在重启计算机之后会话应该就还原正常了。（只重启Xfce亦可）

### 升级Xfce 4.10以后window buttons不能自动扩展长度

这种情况导致类似windows布局的panel始终和通知区域来回移动，不能定位在右下方。 原因是新版的Window Buttons panel plugin不能自动适应面板长度。

为了回到之前的效果，可以在Window Buttons之后添加一个分隔符，属性选中"_扩展_"。

### Preferred Applications preferences have no effect

If you have set your preferred applications with _exo-preferred-applications_, but they do not seem to be taken into consideration, see [Xfce#xdg-open_integration_.28Preferred_Applications.29](/index.php/Xfce#xdg-open_integration_.28Preferred_Applications.29 "Xfce")

### Action Buttons in the panel are missing icons

This happens if icons for some actions (Suspend, Hibernate) are missing from the icon theme, or at least do not have the expected names. First, find out the currently used icon theme in the Settings Manager (→Appearance→Icons). Match this with a subdirectory of `/usr/share/icons`. For example, if the icon theme is GNOME, make a note of the directory name `/usr/share/icons/gnome`.

```
icontheme=/usr/share/icons/gnome

```

Make sure that the [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) is installed as this contains the needed icons. Now create symbolic links from the current icon theme into the `hicolor` icon theme.

```
ln -s /usr/share/icons/hicolor/16x16/actions/xfpm-suspend.png   ${icontheme}/16x16/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/16x16/actions/xfpm-hibernate.png ${icontheme}/16x16/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/22x22/actions/xfpm-suspend.png   ${icontheme}/22x22/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/22x22/actions/xfpm-hibernate.png ${icontheme}/22x22/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/24x24/actions/xfpm-suspend.png   ${icontheme}/24x24/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/24x24/actions/xfpm-hibernate.png ${icontheme}/24x24/actions/system-hibernate.png
ln -s /usr/share/icons/hicolor/48x48/actions/xfpm-suspend.png   ${icontheme}/48x48/actions/system-suspend.png
ln -s /usr/share/icons/hicolor/48x48/actions/xfpm-hibernate.png ${icontheme}/48x48/actions/system-hibernate.png

```

Log out and in again, and you should see icons for all actions.

### 修改挂载参数

比较常见的问题是自动挂载USB设备后，其中FAT文件系统的编码总是探测失败，ñ, ß, etc. 默认用utf8的iocharset编码能够有效解决这个问题，添加以下内容至`/etc/xdg/xfce4/mount.rc`：

```
[vfat]
uid=<auto>
shortname=winnt
**utf8=true**
# FreeBSD specific option
longnames=true
flush=true

```

当你使用utf-8时，文件系统小心的探测文件中的内容。

还有一个比较推荐添加的 **flush**参数 ，以免数据频繁更新导致拖慢thunar的复制进程。Adding _async_ instead will speed up write ops, but make sure to use _Eject_ option in Thunar to unmount the stick. Globally, mount options for storage devices present at boot can be set in [fstab](/index.php/Fstab "Fstab"), and for other devices in [udev](/index.php/Udev "Udev") rules.

## 相关文章

*   [http://docs.xfce.org/](http://docs.xfce.org/) - The complete documentation.
*   [Xfce-Look](http://www.xfce-look.org/) - Themes, wallpapers, and more.
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) - How to edit the auto generated menu with the menu editor
*   [Xfce Wiki](http://wiki.xfce.org)