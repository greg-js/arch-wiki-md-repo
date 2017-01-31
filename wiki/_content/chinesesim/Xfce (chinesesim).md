**翻译状态：** 本文是英文页面 [Xfce](/index.php/Xfce "Xfce") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-10，点击[这里](https://wiki.archlinux.org/index.php?title=Xfce&diff=0&oldid=439589)可以查看翻译后英文页面的改动。

[Xfce](http://www.xfce.org) 是一个基于 GTK+2 的轻量级模块化的 [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")。为了提供完整的用户体验，它包含窗口管理器、文件管理器、桌面和面板。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动Xfce](#.E5.90.AF.E5.8A.A8Xfce)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 菜单](#.E8.8F.9C.E5.8D.95)
        *   [3.1.1 Whisker 菜单](#Whisker_.E8.8F.9C.E5.8D.95)
        *   [3.1.2 编辑菜单](#.E7.BC.96.E8.BE.91.E8.8F.9C.E5.8D.95)
    *   [3.2 桌面](#.E6.A1.8C.E9.9D.A2)
        *   [3.2.1 图标文字的背景透明](#.E5.9B.BE.E6.A0.87.E6.96.87.E5.AD.97.E7.9A.84.E8.83.8C.E6.99.AF.E9.80.8F.E6.98.8E)
        *   [3.2.2 从右击菜单中剔除Thunar选项](#.E4.BB.8E.E5.8F.B3.E5.87.BB.E8.8F.9C.E5.8D.95.E4.B8.AD.E5.89.94.E9.99.A4Thunar.E9.80.89.E9.A1.B9)
        *   [3.2.3 杀死窗口的快捷键](#.E6.9D.80.E6.AD.BB.E7.AA.97.E5.8F.A3.E7.9A.84.E5.BF.AB.E6.8D.B7.E9.94.AE)
    *   [3.3 会话](#.E4.BC.9A.E8.AF.9D)
        *   [3.3.1 自启动程序](#.E8.87.AA.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)
            *   [3.3.1.1 延迟自启动应用程序](#.E5.BB.B6.E8.BF.9F.E8.87.AA.E5.90.AF.E5.8A.A8.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
        *   [3.3.2 锁定屏幕](#.E9.94.81.E5.AE.9A.E5.B1.8F.E5.B9.95)
        *   [3.3.3 切换用户](#.E5.88.87.E6.8D.A2.E7.94.A8.E6.88.B7)
        *   [3.3.4 禁用保存的会话](#.E7.A6.81.E7.94.A8.E4.BF.9D.E5.AD.98.E7.9A.84.E4.BC.9A.E8.AF.9D)
        *   [3.3.5 默认窗口管理器](#.E9.BB.98.E8.AE.A4.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [3.4 更换主题](#.E6.9B.B4.E6.8D.A2.E4.B8.BB.E9.A2.98)
    *   [3.5 声音](#.E5.A3.B0.E9.9F.B3)
        *   [3.5.1 Xfce4 mixer](#Xfce4_mixer)
            *   [3.5.1.1 Change default sound card in Xfce4 mixer](#Change_default_sound_card_in_Xfce4_mixer)
        *   [3.5.2 xfce4-alsa-plugin](#xfce4-alsa-plugin)
        *   [3.5.3 Keyboard volume buttons](#Keyboard_volume_buttons)
            *   [3.5.3.1 Shortcuts](#Shortcuts)
    *   [3.6 键盘快捷键](#.E9.94.AE.E7.9B.98.E5.BF.AB.E6.8D.B7.E9.94.AE)
    *   [3.7 Polkit 身法认证代理](#Polkit_.E8.BA.AB.E6.B3.95.E8.AE.A4.E8.AF.81.E4.BB.A3.E7.90.86)
    *   [3.8 Display blanking](#Display_blanking)
*   [4 提示和小技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [4.1 从 thunar 和 xfdesktop 隐藏分区](#.E4.BB.8E_thunar_.E5.92.8C_xfdesktop_.E9.9A.90.E8.97.8F.E5.88.86.E5.8C.BA)
    *   [4.2 屏幕截图](#.E5.B1.8F.E5.B9.95.E6.88.AA.E5.9B.BE)
    *   [4.3 禁用终端 F1 和 F11 快捷方式](#.E7.A6.81.E7.94.A8.E7.BB.88.E7.AB.AF_F1_.E5.92.8C_F11_.E5.BF.AB.E6.8D.B7.E6.96.B9.E5.BC.8F)
        *   [4.3.1 终端的颜色主题和调色板](#.E7.BB.88.E7.AB.AF.E7.9A.84.E9.A2.9C.E8.89.B2.E4.B8.BB.E9.A2.98.E5.92.8C.E8.B0.83.E8.89.B2.E6.9D.BF)
        *   [4.3.2 修改默认颜色主题](#.E4.BF.AE.E6.94.B9.E9.BB.98.E8.AE.A4.E9.A2.9C.E8.89.B2.E4.B8.BB.E9.A2.98)
    *   [4.4 终端之Tango主题](#.E7.BB.88.E7.AB.AF.E4.B9.8BTango.E4.B8.BB.E9.A2.98)
    *   [4.5 颜色管理](#.E9.A2.9C.E8.89.B2.E7.AE.A1.E7.90.86)
    *   [4.6 多显示器](#.E5.A4.9A.E6.98.BE.E7.A4.BA.E5.99.A8)
    *   [4.7 SSH 代理](#SSH_.E4.BB.A3.E7.90.86)
    *   [4.8 Scroll a background window without shifting focus on it](#Scroll_a_background_window_without_shifting_focus_on_it)
    *   [4.9 修改鼠标按键](#.E4.BF.AE.E6.94.B9.E9.BC.A0.E6.A0.87.E6.8C.89.E9.94.AE)
*   [5 常见问题与解答](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98.E4.B8.8E.E8.A7.A3.E7.AD.94)
    *   [5.1 Action buttons are missing icons](#Action_buttons_are_missing_icons)
    *   [5.2 Desktop icons rearrange themselves](#Desktop_icons_rearrange_themselves)
    *   [5.3 GTK themes not working with multiple monitors](#GTK_themes_not_working_with_multiple_monitors)
    *   [5.4 Xfce4-xkb-plugin settings issue](#Xfce4-xkb-plugin_settings_issue)
    *   [5.5 Icons do not appear in right-click menus](#Icons_do_not_appear_in_right-click_menus)
    *   [5.6 Keyboard settings are not saved in xkb-plugin](#Keyboard_settings_are_not_saved_in_xkb-plugin)
    *   [5.7 NVIDIA 和 xfce4-sensors-plugin](#NVIDIA_.E5.92.8C_xfce4-sensors-plugin)
    *   [5.8 Panel applets keep being aligned on the left](#Panel_applets_keep_being_aligned_on_the_left)
    *   [5.9 Preferred Applications preferences have no effect](#Preferred_Applications_preferences_have_no_effect)
    *   [5.10 Restore default settings](#Restore_default_settings)
    *   [5.11 Session failure](#Session_failure)
    *   [5.12 Fonts in window title crashing xfce4-title](#Fonts_in_window_title_crashing_xfce4-title)
    *   [5.13 Laptop lid settings ignored](#Laptop_lid_settings_ignored)
    *   [5.14 Rendering issues with Adwaita theme](#Rendering_issues_with_Adwaita_theme)
*   [6 相关文章](#.E7.9B.B8.E5.85.B3.E6.96.87.E7.AB.A0)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) 包组。如果需要的话，还可以安装 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 包组。此包组提供了一些额外的插件和一些有用的工具，如 [mousepad](https://www.archlinux.org/packages/?name=mousepad) 编辑器。 Xfce 默认使用 [Xfwm](/index.php/Xfwm "Xfwm") 作为窗口管理器。

## 启动Xfce

从显示管理器（[display manager](/index.php/Display_manager "Display manager")）选择*Xfce Session*，或者添加 `exec startxfce4` 到 [Xinitrc](/index.php/Xinitrc "Xinitrc")中。

**注意:** 不要直接启动 `xfce4-session`，因为它已经被 `startxfce4` 运行了。

## 配置

Xfce把配置的选项保存到[Xfconf](http://docs.xfce.org/xfce/xfconf/start)。有几个方式来修改这些选项：

*   在主菜单中，选择[Settings](http://docs.xfce.org/xfce/xfce4-settings/start)，选择想要修改的选项。选项实际上是位于`/usr/bin/xfce4-*`和`/usr/bin/xfdesktop-settings`中的程序。
*   `xfce4-settings-editors`能看到和修改所有的设置。此处修改的选项会立即生效。使用`xfconf-query`来通过命令行设置；[文档中](http://docs.xfce.org/xfce/xfconf/xfconf-query)有更多的细节。
*   设置保存在XML文件中。此文件位于`~/.config/xfce4/xfconf/xfce-perchannel-xml/`，也可以手动修改文件。但是，此处的修改不会立即生效。

### 菜单

#### Whisker 菜单

[xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin) 是一个可选应用启动器。它可以显示所有的已安装应用中最喜欢和经常被使用的应用。支持应用分类和模糊查询。

#### 编辑菜单

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

<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

    <Exclude>
        <Filename>xfce4-run.desktop</Filename>
        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>
        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

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

当然，也可以将要执行的命令（包括变量）加入 [xinitrc](/index.php/Xinitrc "Xinitrc")。如果使用 [[Display manager|显示管理器「」，则加入 [xprofile](/index.php/Xprofile "Xprofile")

##### 延迟自启动应用程序

有时候，延迟某个应用程序的自启动是很有用的。特别是如 `sleep 3 && command` 这样的命令在自启动中是不起作用的。与之相对，你需要使用如下的语法来替代：

```
sh -c "sleep 3 && command"

```

#### 锁定屏幕

要通过 *xflock4* 脚本锁定 Xfce4 会话，可以从下面软件列表中选择安装一个：[xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock) 和 [xlockmore](https://www.archlinux.org/packages/?name=xlockmore)。

或者可以选择使用下面命令设置屏保：

```
$ xfconf-query -c xfce4-session -p /general/LockCommand -s "light-locker-command -l" --create -t string

```

要更新命令是，可以使用：

```
$ xfconf-query -c xfce4-session -p /general/LockCommand -s "light-locker-command -l"

```

[List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security") 包含了屏幕锁定程序列表。

**Tip:** The [light-locker](https://www.archlinux.org/packages/?name=light-locker) 会话锁定集成在 [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) 中。安装后,'安全’标签页会显示在电源管理设定中。已经有的'系统休眠时锁定屏幕'选项会集成到'安全'标签页中。

**Note:** 可以手动修改 *xflock4* 脚本，参考帖子：[[1]](https://bbs.archlinux.org/viewtopic.php?id=189484). 为了避免修改被更新覆盖，可以将 *xflock4* 复制到 `/usr/local/bin`，这里的修改会覆盖 `/usr/bin` 下的默认版本。

#### 切换用户

只要 [Display manager](/index.php/Display_manager "Display manager") 有切换用户的功能，Xfce4都是可以支持的，比如 [LightDM](/index.php/LightDM "LightDM") 和 [GDM](/index.php/GDM "GDM") 。关于你所使用的DM的信息，需要参看其wiki页面。当你已经安装并配置好你的DM之后，你就可以通过'actions buttons'菜单项来切换用户。

想要不用GDM而能切换用户, 需要安装一个DM:

*   For LXDM - [LXDM#Simultaneous users and switching users](/index.php/LXDM#Simultaneous_users_and_switching_users "LXDM").
*   For LightDM - [LightDM (简体中文)#Xfce4 下多用户切换](/index.php/LightDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Xfce4_.E4.B8.8B.E5.A4.9A.E7.94.A8.E6.88.B7.E5.88.87.E6.8D.A2 "LightDM (简体中文)").

#### 禁用保存的会话

可以通过下面命令禁用某个用户的会话：

```
$ xfconf-query -t bool -c xfce4-session -p /general/SaveOnExit -s false

```

然后进入 *Applications* -> *Settings* -> *Session and Startup* -> *Sessions* 并点击 *Clear saved sessions* 按钮.

**Tip:** 如果上面命令无法持久生效，可以用下面命令：`xfconf-query -c xfce4-session -p /general/SaveOnExit -n -t bool -s false`

Xfce [kiosk](https://wiki.xfce.org/howto/kiosk_mode) 模式可以用来彻底禁用对话的保存。为了禁用对话，创建或者编辑 `/etc/xdg/xfce4/kiosk/kioskrc` 并加入如下的行：

```
[xfce4-session]
SaveSession=NONE

```

如果kiosk模式不能工作，用户可以给对话目录设置只读权限：

```
$ rm ~/.cache/sessions/* && chmod 500 ~/.cache/sessions

```

此操作会防止Xfce保存所有的会话，除了设置和配置。

#### 默认窗口管理器

**注意:** 为了应用更改，在设置后必须清除已经保存的会话，并确保初次登出时没有勾选保存会话。更改生效后，可以再开启保存会话

窗口管理器的设定保存在

*   /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml - 系统设置
*   ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml - 用户设置

单个用户的默认窗口管理器可以用下面命令修改：

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -sa **wm_name**

```

下面命令增加参数:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -t string -s **wm_name** -s **--wm-option**

```

要修改整个系统的默认窗口管理器，需要手动编辑配置文件，将 *xfwm4* 修改为需要的管理器。可以使用 `<value type="string" value="**--wm-option**"/>` 增加额外的参数。

### 更换主题

在 [xfce-look.org](http://www.xfce-look.org) 上有不少XFCE的主题。 *Xfwm* 的主题保存在 `/usr/share/themes/xfce4`, 在 *Settings > Window Manager*中可以更改主题。 而[GTK+](/index.php/GTK%2B "GTK+") 主题在 *Settings > Appearance*。

如果想要使所有的应用能有一个统一的外观, 参见 [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications")获得更多的信息。

相关主题在 [Cursor themes](/index.php/Cursor_themes "Cursor themes"), [Icons](/index.php/Icons "Icons"), 和 [Font configuration](/index.php/Font_configuration "Font configuration") 中。

### 声音

#### Xfce4 mixer

**Note:** Xfce4 和 and Xfce4 volumed 因为无法移植到 GStreamer 1.0, 上游已经不再维护。详情参考：4.12 [新闻](http://www.xfce.org/about/news/?post=1425081600).

[xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) 是 Xfce 组开发的用户混音程序和面板插件，xfce4 软件组的一部分，所以应该已经安装。要支持 [PulseAudio](/index.php/PulseAudio "PulseAudio") 和 [OSS](/index.php/OSS "OSS")，需要安装 [gstreamer0.10-good-plugins](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins/)。

可能需要变更默认声卡才能正常使用 Xfce4 mixer 详情请参考 [Advanced Linux Sound Architecture#Set the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture")，修改后需要重新登录。此外还可以使用 [PulseAudio](/index.php/PulseAudio "PulseAudio") 和 [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) 或 [OSS](/index.php/OSS "OSS"). 参考[OSS#Applications that use GStreamer](/index.php/OSS#Applications_that_use_GStreamer "OSS").

##### Change default sound card in Xfce4 mixer

In some cases (when using [PulseAudio](/index.php/PulseAudio "PulseAudio") or [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/) for instance) it might be necessary to change the default sound card in Xfce4 Mixer in order for volume control to work as expected. [[2]](http://grumbel.blogspot.co.uk/2011/10/fixing-volume-control-in-xfce4.html)

To change the default sound card, open *xfce4-settings-editor* and navigate to **xfce4-mixer** and check the entries under **sound-cards**. Locate the correct entry for the card you are using and then replace the values of **sound-card** and **active-card** with the entry. If you are using PulseAudio then the entry will likely be similar to the following: **PlaybackInternalAudioAnalogStereoPulseAudioMixer**. Then logout for the changes to take effect.

#### xfce4-alsa-plugin

If you do not use PulseAudio, you can install [xfce4-alsa-plugin](https://aur.archlinux.org/packages/xfce4-alsa-plugin/). It provides a simple panel plugin with the ability to control ALSA volume, though it does not support keyboard volume buttons.

#### Keyboard volume buttons

If the [xfce4-mixer](https://www.archlinux.org/packages/?name=xfce4-mixer) package is version `4.10.0-3` or greater, then the mixer panel applet provides the ability to control the volume using the keyboard. However, volume notifications will not be shown. Alternatively, [xfce4-volumed](https://aur.archlinux.org/packages/xfce4-volumed/) maps volume keys to Xfce4 mixer, and displays notifications through Xfce4-notifyd. If you are using PulseAudio and you do not wish to use Xfce4 Mixer at all, install [xfce4-pulseaudio-plugin](https://www.archlinux.org/packages/?name=xfce4-pulseaudio-plugin). This provides a panel applet which has support for keyboard volume control and volume notifications.

For non desktop environment specific alternatives, see [List of applications#Volume managers](/index.php/List_of_applications#Volume_managers "List of applications").

##### Shortcuts

If you are not using an applet or daemon that controls the volume keys, you can map volume control commands to your volume keys manually using Xfce's keyboard settings. For the sound system you are using, see the sections linked to below for the appropriate commands.

*   ALSA: see [Advanced Linux Sound Architecture#Keyboard volume control](/index.php/Advanced_Linux_Sound_Architecture#Keyboard_volume_control "Advanced Linux Sound Architecture").
*   PulseAudio: see [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio")
*   OSS: see [OSS#Using multimedia keys with OSS](/index.php/OSS#Using_multimedia_keys_with_OSS "OSS").

### 键盘快捷键

键盘快捷键在两个地方定义： *Settings > Window Manager > Keyboard* 和 *Settings > Keyboard > Shortcuts*。

### Polkit 身法认证代理

在安装 [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session) 时，会一起安装 [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) 代理，并会随系统自动启动;并不主要用户的干预。更多信息，参见 [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit")。

Xfce可用的第三方的 Polkit 身法认证代理，参见 [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/)。

### Display blanking

**Note:** There are some issues associated with blanking and resuming from blanking in some configurations. See [[3]](https://bbs.archlinux.org/viewtopic.php?id=194313&p=2)[[4]](https://bugzilla.xfce.org/show_bug.cgi?id=11107).

Some programs that are commonly used with Xfce will control monitor blanking and [DPMS](/index.php/DPMS "DPMS") (monitor powersaving) settings. They are discussed below.

	Xfce Power Manager

Xfce Power Manager will control blanking and DPMS settings. These settings can be configured by running *xfce4-power-manager-settings* and clicking the *Display* tab. Note that unticking the *Handle display power management* option means that the Power Manager will disable DPMS - it does not mean that the Power Manager will relinquish control of DPMS. Also note that it will not disable screen blanking. To disable both blanking and DPMS, right click on the power manager system tray icon or left click on the panel applet and make sure that the option labelled *Presentation mode* is ticked.

	xset

If neither of the above applications are running, then blanking and DPMS settings can be controlled using the *xset* command, see [DPMS#Modifying DPMS and screensaver settings using xset](/index.php/DPMS#Modifying_DPMS_and_screensaver_settings_using_xset "DPMS").

## 提示和小技巧

### 从 thunar 和 xfdesktop 隐藏分区

参见 [Udisks#Hide selected partitions](/index.php/Udisks#Hide_selected_partitions "Udisks").

### 屏幕截图

Xfce 有自己的截图工具, [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter).它是 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 包组的一部分.

到 *应用程序 > 设置 > 键盘*, *应用程序快捷方式*. 添加 `xfce4-screenshooter -f` (或 `-w` 为活动窗口)命令用 `Print` 打印键截屏. 其他可选参数参见 screenshooter 的 man 手册

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

Xfce has no native support for colour management. [[5]](https://bugzilla.xfce.org/show_bug.cgi?id=8559) See [ICC profiles](/index.php/ICC_profiles "ICC profiles") for alternatives.

### 多显示器

As of [xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) version 4.11.4, Xfce has support for multiple monitors. Settings can be configured in the *Applications* -> *Settings* -> *Display* dialog. For more information, see the [display](http://docs.xfce.org/xfce/xfce4-settings/display) article from the Xfce documentation.

### SSH 代理

By default Xfce 4.10 will try to load gpg-agent or ssh-agent in that order during session initialization. To disable this, create an xfconf key using the following command:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

To force using ssh-agent even if gpg-agent is installed, run the following instead:

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

To use [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), simply tick the checkbox *Launch GNOME services on startup* in the *Advanced* tab of *Session Manager* in Xfce's settings. This will also disable gpg-agent and ssh-agent.

Source: [http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### Scroll a background window without shifting focus on it

Go to *Main Menu > Settings > Window Manager Tweaks > Accessibility* tab. Uncheck *Raise windows when any mouse button is pressed*.

### 修改鼠标按键

By default, the mouse button modifier in Xfce is set to `Alt`. This can be changed with *xfconf-query*. For instance, the following command will set the `Super` key as the mouse button modifier:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Super"

```

Strictly speaking, using multiple modifiers is not supported. However, as a workaround, multiple modifiers can be specified if the key names are separated with `><`. For instance, to set `Ctrl+Alt` as the mouse button modifier, you can use the following command:

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Ctrl><Alt"

```

## 常见问题与解答

### Action buttons are missing icons

This happens if icons for some actions (Suspend, Hibernate) are missing from the icon theme, or do not have the expected names. To fix this, install an icon theme which has the necessary icons already added; see [Icons#Xfce icons](/index.php/Icons#Xfce_icons "Icons").

Then, you can switch to that icon theme using Applications -> Settings -> Appearance -> Icons.

Alternatively you can use the required icons provided by the icon theme you installed in your current icon theme. To do so, you first need to find out what the currently used icon theme is called. You can do so by using the command below:

```
$ xfconf-query -c xsettings -p /Net/IconThemeName

```

Then set the following variable:

```
$ icontheme=/usr/share/icons/*theme-name*

```

where *theme-name* is the name of the current icon theme.

Then create symbolic links from the current icon theme into the icon theme providing the icons (this example assumes the icons are being provided by the [elementary-xfce-icons](https://aur.archlinux.org/packages/elementary-xfce-icons/) theme.)

```
ln -s /usr/share/icons/elementary-xfce/apps/16/system-suspend.svg           ${icontheme}/16x16/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/16/system-suspend-hibernate.svg ${icontheme}/16x16/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/22/system-suspend.svg           ${icontheme}/22x22/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/22/system-suspend-hibernate.svg ${icontheme}/22x22/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/24/system-suspend.svg           ${icontheme}/24x24/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/24/system-suspend-hibernate.svg ${icontheme}/24x24/actions/system-hibernate.svg
ln -s /usr/share/icons/elementary-xfce/apps/48/system-suspend.svg           ${icontheme}/48x48/actions/system-suspend.svg
ln -s /usr/share/icons/elementary-xfce/apps/48/system-suspend-hibernate.svg ${icontheme}/48x48/actions/system-hibernate.svg

```

Log out and in again, and you should see icons for all actions.

### Desktop icons rearrange themselves

At certain events (such as opening the panel settings dialog) icons on the desktop rearrange themselves. This is because icon positions are determined by files in the `~/.config/xfce4/desktop/` directory. Each time a change is made to the desktop (icons are added or removed or change position) a new file is generated in this directory and these files can conflict.

To solve the problem, navigate to the directory and delete all the files other than the one which correctly defines the icon positions. You can determine which file defines the correct icon positions by opening it and examining the locations of the icons. The topmost row is defined as `row 0` and the leftmost column is defined by `col 0`. Therefore an entry of:

```
[Firefox]
row=3
col=0

```

means that the Firefox icon will be located on the 4th row of the leftmost column.

### GTK themes not working with multiple monitors

Some configuration tools may corrupt displays.xml, which results in GTK themes under *Applications Menu > Settings > Appearance* ceasing to work. To fix the issue, delete `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` and reconfigure your screens.

### Xfce4-xkb-plugin settings issue

There is a bug in version *0.5.4.1-1* which causes xkb-plugin to *lose keyboard, layout switching and compose key* settings. As a workaround you may enable *Use system defaults* option in keyboard settings. To do so run

```
xfce4-keyboard-settings

```

Go to *Layout* tab and set the *Use system defaults* flag, then reconfigure xkb-plugin.

### Icons do not appear in right-click menus

**Note:** Despite the deprecation of GConf, this method does still work.

Users may find that icons do not appear when right-clicking options within some applications, including those made with [Qt](/index.php/Qt "Qt"). This problem only appears to happen within Xfce. Run these two commands:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### Keyboard settings are not saved in xkb-plugin

There is a bug in [xfce4-xkb-plugin](https://www.archlinux.org/packages/?name=xfce4-xkb-plugin) *0.5.4.1-1* which causes it to lose keyboard, layout switching and compose key settings. [[6]](https://bugzilla.xfce.org/show_bug.cgi?id=10226) As a workaround, enable *Use system defaults* in `xfce4-keyboard-settings`, then reconfigure *xfce4-xkb-plugin*.

### NVIDIA 和 xfce4-sensors-plugin

要探测NVIDIA的gpu温度需要安装 [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) 并且用 [ABS](/index.php/ABS "ABS") 重新编译 [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) 软件包。You also have the option of using [xfce4-sensors-plugin-nvidia](https://aur.archlinux.org/packages/xfce4-sensors-plugin-nvidia/) which replaces [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin).

### Panel applets keep being aligned on the left

Add a separator someplace before the right end and set its "expand" property. [[7]](https://forums.linuxmint.com/viewtopic.php?f=110&t=155602})

### Preferred Applications preferences have no effect

Most applications rely on [xdg-open](/index.php/Xdg-open "Xdg-open") for opening a preferred application for a given file or URL.

In order for xdg-open and xdg-settings to detect and integrate with the Xfce desktop environment correctly, you need to [install](/index.php/Install "Install") the [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

If you do not do that, your preferred applications preferences (set by exo-preferred-applications) will not be obeyed. Installing the package and allowing *xdg-open* to detect that you are running Xfce makes it forward all calls to *exo-open* instead, which correctly uses all your preferred applications preferences.

To make sure xdg-open integration is working correctly, ask *xdg-settings* for the default web browser and see what the result is:

```
# xdg-settings get default-web-browser

```

If it replies with:

```
xdg-settings: unknown desktop environment

```

it means that it has failed to detect Xfce as your desktop environment, which is likely due to a missing [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) package.

### Restore default settings

If for any reason you need to revert back: to the default settings, rename `~/.config/xfce4-session/` and `~/.config/xfce4/`

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

Relogin for changes to take effect. If you get `Unable to load a failsafe session` upon login, see the [#Session failure](#Session_failure) section.

### Session failure

Symptoms include:

*   The mouse is an X and/or does not appear at all;
*   Window decorations have disappeared and windows cannot be closed;
*   (`xfwm4-settings`) will not start, reporting `These settings cannot work with your current window manager (unknown)`;
*   Errors reported by a [display manager](/index.php/Display_manager "Display manager") such as `No window manager registered on screen 0`.
*   Unable to load a failsafe session:

```
Unable to load a failsafe session.
Unable to determine failsafe session name.  Possible causes: xfconfd isn't running (D-Bus setup problem); environment variable $XDG_CONFIG_DIRS is set incorrectly (must include "/etc"), or xfce4-session is installed incorrectly. 

```

Restarting xfce or rebooting your system may solve the problem, but a corrupt session is the likely cause. Delete the session folder:

```
$ rm -r ~/.cache/sessions/

```

Also make sure that the relevant folders in `$HOME` are owned by the user starting `xfce4`. See [Chown](/index.php/Chown "Chown").

### Fonts in window title crashing xfce4-title

[Install](/index.php/Install "Install") [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid) and [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu). See also [FS#44382](https://bugs.archlinux.org/task/44382).

### Laptop lid settings ignored

You may find that the lid close settings in Xfce4 Power Manager are ignored, meaning that the laptop will always suspend on lid close, no matter what settings are chosen in the power manager. This is because the power manager is not set to handle lid close events by default. Instead, logind handles the lid close event. To change this behavior so that the the power manager handles lid close events, execute the following command:

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-lid-switch -s false

```

Note that each time the laptop lid settings are changed in the power manager, this setting will be reset.

### Rendering issues with Adwaita theme

Since the upgrade of gnome-themes-standard from 3.18.0-1 version to 3.20.0-1 the Adwaita theme exhibits several issues when being used in Xfce, like a frame around the notification area and dark background of the tooltip in eclipse.

A ugly solution is to downgrade the [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) to the old 3.18.0-1 meanwhile. The package can be downloaded at:

```
$ wget https://archive.archlinux.org/repos/2016/04/08/extra/os/$(uname -m)/gnome-themes-standard-3.18.0-1-$(uname -m).pkg.tar.xz

```

and installed via pacman's `-U` option.

## 相关文章

*   [http://docs.xfce.org/](http://docs.xfce.org/) - The complete documentation.
*   [Xfce-Look](http://www.xfce-look.org/) - Themes, wallpapers, and more.
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) - How to edit the auto generated menu with the menu editor
*   [Xfce Wiki](http://wiki.xfce.org)