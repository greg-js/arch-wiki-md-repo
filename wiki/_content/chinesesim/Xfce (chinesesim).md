相关文章

*   [桌面环境](/index.php/Desktop_Environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop Environment (简体中文)")
*   [显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Xfwm](/index.php/Xfwm "Xfwm")
*   [Thunar](/index.php/Thunar "Thunar")
*   [LXDE](/index.php/LXDE "LXDE")
*   [GNOME](/index.php/GNOME "GNOME")

**翻译状态：** 本文是英文页面 [Xfce](/index.php/Xfce "Xfce") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-07-16，点击[这里](https://wiki.archlinux.org/index.php?title=Xfce&diff=0&oldid=468608)可以查看翻译后英文页面的改动。

[Xfce](http://www.xfce.org) 是一个基于 GTK+2 的轻量级模块化的 [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")。为了提供完整的用户体验，它包含窗口管理器、文件管理器、桌面和面板。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 启动Xfce](#启动Xfce)
*   [3 配置](#配置)
    *   [3.1 菜单](#菜单)
        *   [3.1.1 Whisker 菜单](#Whisker_菜单)
        *   [3.1.2 编辑菜单](#编辑菜单)
    *   [3.2 桌面](#桌面)
        *   [3.2.1 图标文字的透明背景](#图标文字的透明背景)
        *   [3.2.2 从右键菜单中剔除 Thunar 选项](#从右键菜单中剔除_Thunar_选项)
        *   [3.2.3 多显示器连续壁纸](#多显示器连续壁纸)
        *   [3.2.4 关闭窗口的快捷键](#关闭窗口的快捷键)
    *   [3.3 会话](#会话)
        *   [3.3.1 自启动程序](#自启动程序)
            *   [3.3.1.1 延迟应用程序启动](#延迟应用程序启动)
        *   [3.3.2 锁定屏幕](#锁定屏幕)
            *   [3.3.2.1 面板的锁定按钮](#面板的锁定按钮)
        *   [3.3.3 禁用保存的会话](#禁用保存的会话)
        *   [3.3.4 默认窗口管理器](#默认窗口管理器)
    *   [3.4 更换主题](#更换主题)
    *   [3.5 声音](#声音)
        *   [3.5.1 声音主题](#声音主题)
        *   [3.5.2 键盘音量键](#键盘音量键)
            *   [3.5.2.1 快捷键](#快捷键)
    *   [3.6 键盘快捷键](#键盘快捷键)
    *   [3.7 Polkit 验证代理](#Polkit_验证代理)
    *   [3.8 Display blanking](#Display_blanking)
*   [4 提示和小技巧](#提示和小技巧)
    *   [4.1 从 thunar 和 xfdesktop 隐藏分区](#从_thunar_和_xfdesktop_隐藏分区)
    *   [4.2 屏幕截图](#屏幕截图)
    *   [4.3 禁用终端 F1 和 F11 快捷方式](#禁用终端_F1_和_F11_快捷方式)
        *   [4.3.1 终端的颜色主题和调色板](#终端的颜色主题和调色板)
        *   [4.3.2 修改默认颜色主题](#修改默认颜色主题)
    *   [4.4 终端之 Tango 主题](#终端之_Tango_主题)
    *   [4.5 终端下用鼠标中键打开 URL](#终端下用鼠标中键打开_URL)
    *   [4.6 颜色管理](#颜色管理)
    *   [4.7 多显示器](#多显示器)
    *   [4.8 SSH 代理](#SSH_代理)
    *   [4.9 滚动时不获得焦点](#滚动时不获得焦点)
    *   [4.10 修改窗口管理器 modifier](#修改窗口管理器_modifier)
    *   [4.11 设置触摸板两指单击为鼠标中键](#设置触摸板两指单击为鼠标中键)
    *   [4.12 限制亮度划块的最小亮度](#限制亮度划块的最小亮度)
*   [5 常见问题与解答](#常见问题与解答)
    *   [5.1 动作按钮没有图标](#动作按钮没有图标)
    *   [5.2 桌面图标顺序被打乱](#桌面图标顺序被打乱)
    *   [5.3 GTK 主题在多显示器下不正常](#GTK_主题在多显示器下不正常)
    *   [5.4 右键菜单没有图标](#右键菜单没有图标)
    *   [5.5 NVIDIA 和 xfce4-sensors-plugin](#NVIDIA_和_xfce4-sensors-plugin)
    *   [5.6 面板小程序挤在左边](#面板小程序挤在左边)
    *   [5.7 首选应用程序没有效果](#首选应用程序没有效果)
    *   [5.8 恢复默认设置](#恢复默认设置)
    *   [5.9 会话失败](#会话失败)
    *   [5.10 标题栏字体使 xfce4-title 崩溃](#标题栏字体使_xfce4-title_崩溃)
    *   [5.11 笔记本盖设置没有效果](#笔记本盖设置没有效果)
    *   [5.12 电源管理插件显示剩余时间和百分比](#电源管理插件显示剩余时间和百分比)
*   [6 相关文章](#相关文章)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) 包组。如果需要的话，还可以安装 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 包组。此包组提供了一些额外的插件和一些有用的工具，如 [mousepad](https://www.archlinux.org/packages/?name=mousepad) 编辑器。 Xfce 默认使用 [Xfwm](/index.php/Xfwm "Xfwm") 作为窗口管理器。

## 启动Xfce

从[显示管理器](/index.php/Display_manager "Display manager")中选择*Xfce Session*，或者添加 `exec startxfce4` 到 [Xinitrc](/index.php/Xinitrc "Xinitrc") 中。

**注意:** 不要直接调用 `xfce4-session`可执行文件，`startxfce4` 是正确的命令，它会在恰当的时间调用前述可执行文件。

## 配置

Xfce 把配置的选项保存到 [Xfconf](http://docs.xfce.org/xfce/xfconf/start)。有几个方式来修改这些选项：

*   在主菜单中，选择 [设置](http://docs.xfce.org/xfce/xfce4-settings/start)和要自定义的类别。类别是通常位于 `/usr/bin/xfce4-*` 和 `/usr/bin/xfdesktop-settings` 中的程序。
*   `xfce4-settings-editors` 可以查看和修改所有设置。此处修改的选项会立即生效。使用`xfconf-query`从命令行更改设置；[文档中](http://docs.xfce.org/xfce/xfconf/xfconf-query)有更多的细节。
*   设置保存在 XML 文件中。此文件位于 `~/.config/xfce4/xfconf/xfce-perchannel-xml/`，可以手动修改。但是，此处的修改不会立即生效。

### 菜单

#### Whisker 菜单

[xfce4-whiskermenu-plugin](https://www.archlinux.org/packages/?name=xfce4-whiskermenu-plugin)（包含在 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 中）是一个可选应用启动器。它可以显示收藏夹列表，通过类别按钮浏览所有已安装的应用程序，并支持模糊搜索。安装完成后，就可以替换掉面板1的第一个项目“应用程序菜单”了（在“设置/面板/项目"选择添加”Whisker 菜单“）。

#### 编辑菜单

许多图形工具可以用来实现此项需求：

*   **XAME** — 使用Gambas编写，用于Xfce编辑菜单项的图形工具，在其他环境中没有效果。（已停止开发）

	[http://www.redsquirrel87.com/XAME.php](http://www.redsquirrel87.com/XAME.php) || [xame](https://aur.archlinux.org/packages/xame/)

*   **MenuLibre** — 一个高级的菜单编辑器，提供了一个纯粹、易用的界面。

	[https://launchpad.net/menulibre](https://launchpad.net/menulibre) || [menulibre](https://aur.archlinux.org/packages/menulibre/)

*   **Alacarte** — GNOME的菜单编辑器。

	[http://www.gnome.org/](http://www.gnome.org/) || [alacarte](https://www.archlinux.org/packages/?name=alacarte)

当然，也可以手动创建 `~/.config/menus/xfce-applications.menu`。下面给出一个示例的配置：

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

你可以通过编辑 `.desktop` 本身来改变Xfce的菜单。隐藏项，可以参见 [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries")。你可以通过改变 `Categories=` 桌面项的行，来编辑应用程序类别。参见 [Desktop entries#File example](/index.php/Desktop_entries#File_example "Desktop entries")。

### 桌面

#### 图标文字的透明背景

默认桌面图标的文字是白色背景，可以创建或者修改 `~/.gtkrc-2.0` 来得到不一样的效果：

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

#### 从右键菜单中剔除 Thunar 选项

使用如下的命令：

```
$ xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0

```

#### 多显示器连续壁纸

打开 `xfce4-settings-editor` 创建如下的属性：

```
Property: /backdrop/screen0/xinerama-stretch
Type: Boolean
Value: TRUE|1|Enabled

```

#### 关闭窗口的快捷键

Xfce没有关闭窗口的快捷键，当程序假死时，我们可能需要这样的快捷键。

使用 [xorg-xkill](https://www.archlinux.org/packages/?name=xorg-xkill)，`xkill` 可以交互关闭窗口。对于当下的激活窗口，使用包 [xdotool](https://www.archlinux.org/packages/?name=xdotool)：

```
$ xdotool getwindowfocus windowkill

```

也可以：

```
$ sh -c "xkill -id $(xprop -root -notype | sed -n '/^_NET_ACTIVE_WINDOW/ s/^.*# *\|\,.*$//g p')"

```

添加快捷键，使用 **设置 > 键盘** 或者使用应用程序，如 [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys)。

### 会话

#### 自启动程序

可以在 **程序 > 设置 > 设置管理器 > 会话和自启动** 中点击**应用程序自启动**，设置与Xfce一起启动的自启动程序。 此处列出了所有自启动的程序。点击 **添加** 按钮后可以添加自定义的自启动任务，需指定可执行文件的路径。

当然，也可以将要执行的命令（包括设置环境变量）加入 [xinitrc](/index.php/Xinitrc "Xinitrc")。如果使用 [显示管理器](/index.php/Display_manager "Display manager")，则加入 [xprofile](/index.php/Xprofile "Xprofile") 。

##### 延迟应用程序启动

延迟某个应用程序启动有时可能很有用。在**应用程序自启动**中指定类似 `sleep 3 && command` 的命令不会起作用。作为一个解决办法，可以使用如下命令：

```
sh -c "sleep 3 && command"

```

#### 锁定屏幕

要通过 *xflock4* 脚本锁定 Xfce4 会话，可以从下面软件列表中选择安装一个：[xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver), [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver), [slock](https://www.archlinux.org/packages/?name=slock) 和 [xlockmore](https://www.archlinux.org/packages/?name=xlockmore)。

或者，可以设置锁定命令：

```
$ xfconf-query -c xfce4-session -p /general/LockCommand -s "light-locker-command -l" --create -t string

```

更新命令可以使用：

```
$ xfconf-query -c xfce4-session -p /general/LockCommand -s "light-locker-command -l"

```

[List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security") 包含一个全面的屏幕锁定程序列表。

**提示：** [light-locker](https://www.archlinux.org/packages/?name=light-locker) 是和 [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) 相整合的。安装 light-locker 后,电源管理设定中会出现*安全*标签页。现有的*系统休眠时锁定屏幕*选项会集成到*安全*标签页中。

##### 面板的锁定按钮

活动按钮面板的锁定按钮直接执行 `/usr/bin/xflock4`，就忽略了上面的 `/general/LockCommand` 设置和[这里](https://bbs.archlinux.org/viewtopic.php?id=189484)阐述的设置别名的方法。

使用 [light-locker](https://www.archlinux.org/packages/?name=light-locker) 有两种方法：

*   编辑 `/usr/bin/xflock4` 来直接执行 `light-locker-command -l`。这不应该被用于多用户系统，而且更新软件包的时候不能被覆写。
*   用自定义启动器替换活动按钮提供的锁定按钮. 在活动按钮设置里移除锁定按钮，再向面板中添加一个启动器，把 *Command* 设置为 `light-locker-command -l`，还可以把图标设置成 `system-lock-screen`。

#### 禁用保存的会话

可以通过下面命令禁用某个用户已保存的会话：

```
$ xfconf-query -t bool -c xfce4-session -p /general/SaveOnExit -s false

```

然后进入 *应用程序* -> *设置* -> *会话和启动* -> *会话* 并点击 *清除已保存的会话* 按钮。

**提示：** 如果上面命令无法持久生效，可以用下面命令：`xfconf-query -c xfce4-session -p /general/SaveOnExit -n -t bool -s false`

Xfce [kiosk 模式](https://wiki.xfce.org/howto/kiosk_mode) 可以用来彻底禁用对话的保存。要禁用对话，创建或者编辑 `/etc/xdg/xfce4/kiosk/kioskrc` 并加入如下内容：

```
[xfce4-session]
SaveSession=NONE

```

如果kiosk模式不起作用，用户可以给会话目录设置只读权限：

```
$ rm ~/.cache/sessions/* && chmod 500 ~/.cache/sessions

```

此操作会防止Xfce保存所有的会话，即使任何别的设置允许保存会话。

#### 默认窗口管理器

**注意:** 要使更改生效，需要清除保存的会话，并确保在首次注销时禁用会话保存。 一旦选择的窗口管理器正在运行，可以再次启用会话保存。

窗口管理器的设定保存在：

*   /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml - 系统设置
*   ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml - 用户设置

单个用户的默认窗口管理器可以用*xfconf-query*命令设置：

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -sa **wm_name**

```

如果要使用命令行选项启动窗口管理器，请使用以下命令：:

```
$ xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -t string -s **wm_name** -s **--wm-option**

```

如需更多命令行选项，只需向命令中添加更多 `-t string` 和 `-s **--wm-option**` 参数。

如需更改整个系统的默认窗口管理器，手动编辑上面指定的文件，将*xfwm4*更改为首选窗口管理器，并添加更多 `<value type="string" value="**--wm-option**"/>` 选项（如果需要）。

要更改窗口管理器，还可以设置 `**wm_name** --replace` 自启动，或者在终端中运行 `**wm_name** --replace &`并确保在注销时保存会话。请注意该方法并没有真正地更改默认窗口管理器，而只是每次开机时将其替换掉。如果你使用自动启动工具，应该禁用保存的会话，因为这可能导致新的窗口管理器在默认窗口管理器之后启动两次。

### 更换主题

在 [xfce-look.org](http://www.xfce-look.org) 上有不少 XFCE 的主题。 *Xfwm* 的主题保存在 `/usr/share/themes/xfce4`, 在 *设置 > 窗口管理器* 中可以更改主题。 而[GTK+](/index.php/GTK%2B "GTK+") 主题在 *设置 > 外观* 设置。

如果想要使所有的应用能有一个统一的外观, 参见 [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") 获得更多的信息。

另参见 [Cursor themes](/index.php/Cursor_themes "Cursor themes"), [Icons](/index.php/Icons "Icons"), 和 [Font configuration](/index.php/Font_configuration "Font configuration")。

### 声音

#### 声音主题

XFCE4支持 [freedesktop system sounds](https://www.freedesktop.org/wiki/Specifications/sound-theme-spec/)， 但需要配置。

启用声音主题：

1.  安装 [libcanberra](https://www.archlinux.org/packages/?name=libcanberra) 和 [libcanberra-pulse](https://www.archlinux.org/packages/?name=libcanberra-pulse) 以提供 [PulseAudio](/index.php/PulseAudio "PulseAudio") 支持。
2.  "canberra-gtk-module" 应该在 GTK_MODULES 环境变量 （需要重新登陆）；
3.  在 设置管理器 → 外观 → 设置 选项卡 勾选 "启用事件声音" ；
4.  在 设置编辑器（Settings Editor） 设置 "xsettings/Net/SoundThemeName" 为一个在 `/usr/share/sounds/` 下的声音主题；
5.  在混声器里（比如pavucontrol）打开系统声音（System Sounds）。

[sound-theme-freedesktop](https://www.archlinux.org/packages/?name=sound-theme-freedesktop) 提供兼容的声音主题，但是不好用。推荐 [sound-theme-smooth](https://aur.archlinux.org/packages/sound-theme-smooth/) （上面的 SoundThemeName 设置为 "Smooth"）。

#### 键盘音量键

[xfce4-pulseaudio-plugin](https://www.archlinux.org/packages/?name=xfce4-pulseaudio-plugin) 提供了一个面板小程序，它支持键盘音量控制和音量提示。或者，可以用不提供面板图标的 [xfce4-volumed-pulse](https://aur.archlinux.org/packages/xfce4-volumed-pulse/)，它还提供键绑定和通知控制。当同时使用 [pasystray](https://www.archlinux.org/packages/?name=pasystray) 进行更细微的控制时会很方便。

还可以用 [xfce4-mixer](https://git.xfce.org/apps/xfce4-mixer/)，它同样提供面板小程序和键盘快捷键，并支持Alsa。然而，请注意，它是基于已在1.0中放弃的GStreamer 0.10的功能。

[List of applications#Volume managers](/index.php/List_of_applications#Volume_managers "List of applications") 下有和特定桌面无关的选项替代。

##### 快捷键

如不使用控制音量键的小程序或守护程序，则可以使用Xfce的键盘设置手动将音量控制命令映射到音量键。对于您正在使用的音响系统，请参阅以下链接到相应命令的部分。

*   ALSA: [Advanced Linux Sound Architecture#Keyboard volume control](/index.php/Advanced_Linux_Sound_Architecture#Keyboard_volume_control "Advanced Linux Sound Architecture").
*   PulseAudio: [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio")
*   OSS: [OSS#Using multimedia keys with OSS](/index.php/OSS#Using_multimedia_keys_with_OSS "OSS").

### 键盘快捷键

键盘快捷键在两个地方设置： *设置 > 窗口管理器 > 键盘* 和 *设置 > 键盘 > 快捷键*。

### Polkit 验证代理

在安装 [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session) 时，会同时安装 [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome)，并随系统自动启动;无需用户干预。更多信息请参见 [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit")。

Xfce 可用的第三方 Polkit 身份认证代理，参见 [xfce-polkit-git](https://aur.archlinux.org/packages/xfce-polkit-git/) 和 [xfce-polkit](https://aur.archlinux.org/packages/xfce-polkit/)。

### Display blanking

**Note:** There are some issues associated with blanking and resuming from blanking in some configurations. See [[1]](https://bbs.archlinux.org/viewtopic.php?id=194313&p=2)[[2]](https://bugzilla.xfce.org/show_bug.cgi?id=11107).

Some programs that are commonly used with Xfce will control monitor blanking and [DPMS](/index.php/DPMS "DPMS") (monitor powersaving) settings. They are discussed below.

	Xfce Power Manager

Xfce Power Manager will control blanking and DPMS settings. These settings can be configured by running *xfce4-power-manager-settings* and clicking the *Display* tab. Note that unticking the *Handle display power management* option means that the Power Manager will disable DPMS - it does not mean that the Power Manager will relinquish control of DPMS. Also note that it will not disable screen blanking. To disable both blanking and DPMS, right click on the power manager system tray icon or left click on the panel applet and make sure that the option labelled *Presentation mode* is ticked.

	XScreenSaver

See [XScreenSaver#DPMS and blanking settings](/index.php/XScreenSaver#DPMS_and_blanking_settings "XScreenSaver"). Note that if XScreenSaver is running alongside Xfce Power Manager, it may not be entirely clear which application is in control of blanking and DPMS as both applications are competing for control of the same settings. Therefore, in a situation where it is important that the monitor not be blanked (when watching a film for instance), it is advisable to disable blanking and DPMS through both applications.

	xset

If neither of the above applications are running, then blanking and DPMS settings can be controlled using the *xset* command, see [DPMS#Modifying DPMS and screensaver settings using xset](/index.php/DPMS#Modifying_DPMS_and_screensaver_settings_using_xset "DPMS").

## 提示和小技巧

### 从 thunar 和 xfdesktop 隐藏分区

如果你的系统分区在桌面和 Thunar 中被显示成了已加载分区，可以安装 [gvfs](https://www.archlinux.org/packages/?name=gvfs) 试试。在 [Udisks#Hide selected partitions](/index.php/Udisks#Hide_selected_partitions "Udisks") 参见更多的选项。

### 屏幕截图

Xfce 有自己的截图工具 [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter)。它是 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 包组的一部分。

到 *应用程序 > 设置 > 键盘*, *应用程序快捷方式*. 添加 `xfce4-screenshooter -f` (或 `-w` 为活动窗口)命令用 `Print` 键截屏。 其他可选参数参见 screenshooter 的 man 手册。

此外，也可用其他独立的截图程序如 [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot")。

### 禁用终端 F1 和 F11 快捷方式

XFCE 终端下 F1 和 F11 分别被绑定给了帮助和全屏，给一些程序造成了冲突。要禁用这些快捷方式，创建或修改下面的配置文件然后注销重新登录。F10 可以在设置里更改。

 `~/.config/xfce4/terminal/accels.scm` 
```
(gtk_accel_path "<Actions>/terminal-window/fullscreen" "")
(gtk_accel_path "<Actions>/terminal-window/contents" "")

```

#### 终端的颜色主题和调色板

可以在首选项的外观标签下修改终端主题颜色和调色板。这些色彩可用于多大数控制台程序如[Emacs](/index.php/Emacs "Emacs")，[Vi](/index.php/Vi "Vi") 等。 它们的设置单独存储在每个用户的 `~/.config/xfce4/terminal/terminalrc` 文件中。 还有更多主题可供选择。论坛下 [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818) 有数百的更多终端配色方案。

#### 修改默认颜色主题

XFCE 的 `extra/terminal` 包使用了较暗的颜色使得文字在默认的黑色背景下很难阅读并会使人感到不适，请把以下文字写入到 terminalrc 文件中来使用一个较明亮的颜色主题, 它会在一直在较暗的终端背景下可见。

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

### 终端之 Tango 主题

用你喜欢的编辑器打开 `~/.config/xfce4/terminal/terminalrc` 加入：

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

### 终端下用鼠标中键打开 URL

升级到 0.8 后鼠标中键的默认行为改成了粘贴到光标。 要改回元行为，修改 `${XDG_CONFIG_HOME}/xfce4/terminal/terminalrc`（默认 `XDG_CONFIG_HOME=${HOME}/.config`）

 `${XDG_CONFIG_HOME}/xfce4/terminal/terminalrc` 
```
[Configuration]
MiscMiddleClickOpensUri=TRUE
```

### 颜色管理

Xfce 本身没有颜色管理的功能支持。 [[4]](https://bugzilla.xfce.org/show_bug.cgi?id=8559) 查看 [ICC profiles](/index.php/ICC_profiles "ICC profiles") 寻找替代。

### 多显示器

[xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) 的 4.11.4 之后 Xfce 开始支持多显示器。可以在 *应用程序* -> *设置* -> *显示* 下配置。更多信息请看 Xfce 文档 [display](http://docs.xfce.org/xfce/xfce4-settings/display)。

### SSH 代理

默认 Xfce 4.10 会在会话启动时试着按顺序打开 gpg-agent 或 ssh-agent。要禁用的话，运行如下命令：

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/enabled -n -t bool -s false

```

若 gpg-agent 安装了也要启动 ssh-agent 的话运行：

```
xfconf-query -c xfce4-session -p /startup/ssh-agent/type -n -t string -s ssh-agent

```

要使用 [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")，在*设置*里的*会话和启动*的*高级*页选中*桌面启动时启动 GNOME 服务*。这还会禁止 gpg-agent 和 ssh-agent 的启动。

参见：[http://docs.xfce.org/xfce/xfce4-session/advanced](http://docs.xfce.org/xfce/xfce4-session/advanced)

### 滚动时不获得焦点

在 *设置 > 窗口管理器微调 > 辅助功能* 下取消 *按下任意鼠标按钮时提升窗口*。

### 修改窗口管理器 modifier

默认的 modifier 是 `Alt`。可以用 *xfconf-query*更改。比如说下面的命令会将其改为 `Super`：

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Super"

```

严格地说，并不支持多 modifier。可是实际可以用 `><` 把多个键分隔起来。比如下面的命令会把 modifier 改为 `Ctrl+Alt`：

```
$ xfconf-query -c xfwm4 -p /general/easy_click -n -t string -s "Ctrl><Alt"

```

### 设置触摸板两指单击为鼠标中键

如果你想让触摸板两指单击识别为鼠标中键，创建或更改如下文件：

 `~/.config/xfce4/xfconf/xfce-perchannel-xml/pointers.xml` 
```
<channel name="pointers" version="1.0">
  <property name="SynPS2_Synaptics_TouchPad" type="empty">
    <property name="Properties" type="empty">
      <property name="Synaptics_Tap_Action" type="array">
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="0"/>
        <value type="int" value="1"/>
        <value type="int" value="2"/>
        <value type="int" value="3"/>
      </property>
    </property>
  </property>
</channel>

```

数组中的2就是鼠标中键。

### 限制亮度划块的最小亮度

在一些显示器下亮度等级设为0后背光会完全关掉。`xfce4-power-manager 1.3.2` 有一个新的隐藏选项可以调节最小亮度。用 xfconf4 添加一个名为 `brightness-slider-min-level` 的整数键，将其改为合适的最小亮度值。

## 常见问题与解答

### 动作按钮没有图标

当使用的图标主题不全或所含图标名称不正确时会发生这种情况，换一个有对应图标的主题即可解决，见 [Icons#Xfce icons](/index.php/Icons#Xfce_icons "Icons")。

然后就可以在 *应用程序 -> 设置 -> 外观 -> 图标* 处更换主题。

或者你也可以使用当前图标主题中的图标。首先需要知道当前的图标主题名，运行命令：

```
$ xfconf-query -c xsettings -p /Net/IconThemeName

```

设置如下的变量：

```
$ icontheme=/usr/share/icons/*主题名*

```

然后创建从其他主题到现有主题特定图标的链接（下列命令假设你安装了 [elementary-xfce-icons](https://aur.archlinux.org/packages/elementary-xfce-icons/) 主题）。

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

注销重新登录后应该就能起作用了。

### 桌面图标顺序被打乱

在一些情况下（比如打开面板设置对话框时）桌面图标的顺序会被改变。这是因为其顺序是由在 `~/.config/xfce4/desktop/` 下的文件所决定的，而每次改变桌面（添加删除图标或改变位置）就会生成一个新文件，导致了可能的冲突。

要解决这个问题，打开那个目录然后只留下一个正确的配置文件。可以通过其内容来判别到底是哪个文件。里面行数定义为 `row 0`，列数定义为 `col 0`。因而如下的文件内容：

```
[Firefox]
row=3
col=0

```

意为火狐在最左边第四行。

### GTK 主题在多显示器下不正常

一些配置工具会损坏 displays.xml 从而导致 *应用程序 > 设置 > 外观* 无法工作。要解决问题，删除 `~/.config/xfce4/xfconf/xfce-perchannel-xml/displays.xml` 然后重新设置。

### 右键菜单没有图标

**注意:** GConf 已被不建议使用，但这个方法还有效。

有时一些程序，包括用 [Qt](/index.php/Qt "Qt") 写的程序的右键菜单没有图标。这个问题只发生在 Xfce 下。运行如下命令:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### NVIDIA 和 xfce4-sensors-plugin

要探测 NVIDIA gpu 的温度，需要安装 [libxnvctrl](https://www.archlinux.org/packages/?name=libxnvctrl) 并且用 [ABS](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)") 重新编译 [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) 软件包。或者改安装 [xfce4-sensors-plugin-nvidia](https://aur.archlinux.org/packages/xfce4-sensors-plugin-nvidia/)。

### 面板小程序挤在左边

添加一个分割符并选中”扩展”属性。 [[5]](https://forums.linuxmint.com/viewtopic.php?f=110&t=155602})

### 首选应用程序没有效果

大多数程序依赖 [xdg-open](/index.php/Xdg-open "Xdg-open") 来用首选应用程序打开想要的文件和 URL。

要让 xdg-open 和 xdg-settings 与 Xfce 桌面环境检测和整合，需要 [安装](/index.php?title=Install_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Install (简体中文) (page does not exist)") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) 包。

如果不这么做的话，在 exo-preferred-applications 设置的首选应用程序就没有效果。 安装后 *xdg-open* 会检测到你正在运行 Xfce，从而把调用全转交给 *exo-open*。它会正常地使用你的首选应用程序设置。

要确认 xdg-open 是否正常工作，询问 *xdg-settings* 默认浏览器的返回结果：

```
# xdg-settings get default-web-browser

```

如果输出的是：

```
xdg-settings: unknown desktop environment

```

这说明 xdg-open 没有检测出你的桌面环境。原因很可能在没有安装 [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) 包。

### 恢复默认设置

如果出于某些愿意需要恢复默认设置，重命名 `~/.config/xfce4-session/` 和 `~/.config/xfce4/`

```
$ mv ~/.config/xfce4-session/ ~/.config/xfce4-session-bak
$ mv ~/.config/xfce4/ ~/.config/xfce4-bak

```

重新登录后就会起效果。若登录时出现 `Unable to load a failsafe session`，见 [#会话失败](#会话失败)一节。

### 会话失败

包括以下症状：

*   鼠标变成了叉号甚至没有鼠标
*   没有标题栏，无法关闭窗口
*   (`xfwm4-settings`) 不起动，报 `These settings cannot work with your current window manager (unknown)`
*   [显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)") 报错，例如 `No window manager registered on screen 0`。
*   `Unable to load a failsafe session`

```
Unable to load a failsafe session.
Unable to determine failsafe session name.  Possible causes: xfconfd isn't running (D-Bus setup problem); environment variable $XDG_CONFIG_DIRS is set incorrectly (must include "/etc"), or xfce4-session is installed incorrectly. 

```

重启可能会解决问题，但原因在于错误的会话。删除会话目录：

```
$ rm -r ~/.cache/sessions/

```

还有就是保证 `$HOME` 的对应目录是被启动 `xfce4` 的用户所拥有的。见 [Chown](/index.php/Chown "Chown")。

### 标题栏字体使 xfce4-title 崩溃

[安装](/index.php/Install "Install") [ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid) 和 [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)。参见 [FS#44382](https://bugs.archlinux.org/task/44382)。

### 笔记本盖设置没有效果

你可能会发现 Xfce4 电源管理器的合盖设置没有效果，不论什么设置合盖后总是挂起。这是因为默认 logind 而非电源管理器接管了合盖的事件。要更改该行为，运行命令：

```
$ xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/logind-handle-lid-switch -s false

```

**注意:** 有些情况下当你更改合盖动作和挂起时锁定的设置时 `logind-handle-lid-switch` 设置会又变成 true，详见 [[6]](https://bugzilla.xfce.org/show_bug.cgi?id=12756#c2)。你需要再手动把它设成 `logind-handle-lid-switch` false。

### 电源管理插件显示剩余时间和百分比

版本 1.5.1 引进了新的显示一个标签的隐藏功能。xfconf4 整数选项 `show-panel-label`可以设置不同的标签类型：0（无标签），1（百分比），2（剩余时间）或 3（两方）。

参见：[1.5.1 release notes](https://mail.xfce.org/pipermail/xfce-announce/2015-June/000424.html)

## 相关文章

*   [Xfce - About](http://www.xfce.org/about/)
*   [http://docs.xfce.org/](http://docs.xfce.org/) - 完整的文档
*   [Xfce-Look](http://www.xfce-look.org/) - 主题，壁纸等
*   [Xfce Wikia](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) - 如何用目录编辑器编辑自动生成的目录
*   [Xfce Wiki](http://wiki.xfce.org)