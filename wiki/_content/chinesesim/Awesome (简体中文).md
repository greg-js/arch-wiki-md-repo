**翻译状态：** 本文是英文页面 [Awesome](/index.php/Awesome "Awesome") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-8-12，点击[这里](https://wiki.archlinux.org/index.php?title=Awesome&diff=0&oldid=329002)可以查看翻译后英文页面的改动。

来自[awesome](https://en.wikipedia.org/wiki/awesome_(window_manager) "wikipedia:awesome (window manager)")网站：

*[Awesome](http://awesome.naquadah.org/) 是 XWindows 下可高度定制的新一代窗口管理器。运行快捷、扩展性强，遵循GPLv2发布。*

*Awesome主要面向高级用户、开发者和那些希望完美控制自己电脑的图形界面的人。*

本文主要内容为安装、使用、配置和自定义 awesome 窗口管理器。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用Awesome](#.E4.BD.BF.E7.94.A8Awesome)
    *   [2.1 不使用登陆管理器](#.E4.B8.8D.E4.BD.BF.E7.94.A8.E7.99.BB.E9.99.86.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.2 使用登陆管理器](#.E4.BD.BF.E7.94.A8.E7.99.BB.E9.99.86.E7.AE.A1.E7.90.86.E5.99.A8)
        *   [2.2.1 GDM, LightDM 以及其他使用 /usr/share/xsessions/ 的管理器](#GDM.2C_LightDM_.E4.BB.A5.E5.8F.8A.E5.85.B6.E4.BB.96.E4.BD.BF.E7.94.A8_.2Fusr.2Fshare.2Fxsessions.2F_.E7.9A.84.E7.AE.A1.E7.90.86.E5.99.A8)
        *   [2.2.2 KDM](#KDM)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 创建配置文件](#.E5.88.9B.E5.BB.BA.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [3.2 更多的配置资源](#.E6.9B.B4.E5.A4.9A.E7.9A.84.E9.85.8D.E7.BD.AE.E8.B5.84.E6.BA.90)
    *   [3.3 调试 rc.lua](#.E8.B0.83.E8.AF.95_rc.lua)
        *   [3.3.1 使用 Xephyr](#.E4.BD.BF.E7.94.A8_Xephyr)
        *   [3.3.2 使用 awmtt](#.E4.BD.BF.E7.94.A8_awmtt)
    *   [3.4 改变键盘布局](#.E6.94.B9.E5.8F.98.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
*   [4 主题](#.E4.B8.BB.E9.A2.98)
    *   [4.1 设置墙纸](#.E8.AE.BE.E7.BD.AE.E5.A2.99.E7.BA.B8)
        *   [4.1.1 version >= 3.5](#version_.3E.3D_3.5)
        *   [4.1.2 随机墙纸](#.E9.9A.8F.E6.9C.BA.E5.A2.99.E7.BA.B8)
*   [5 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [5.1 使用awesome作为GNOME的窗口管理器](#.E4.BD.BF.E7.94.A8awesome.E4.BD.9C.E4.B8.BAGNOME.E7.9A.84.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [5.2 像compiz那样的平铺桌面效果](#.E5.83.8Fcompiz.E9.82.A3.E6.A0.B7.E7.9A.84.E5.B9.B3.E9.93.BA.E6.A1.8C.E9.9D.A2.E6.95.88.E6.9E.9C)
    *   [5.3 在awesome 3中显示/隐藏wibox](#.E5.9C.A8awesome_3.E4.B8.AD.E6.98.BE.E7.A4.BA.2F.E9.9A.90.E8.97.8Fwibox)
    *   [5.4 截图](#.E6.88.AA.E5.9B.BE)
    *   [5.5 动态标签](#.E5.8A.A8.E6.80.81.E6.A0.87.E7.AD.BE)
    *   [5.6 Space Invaders](#Space_Invaders)
    *   [5.7 Naughty弹窗提醒](#Naughty.E5.BC.B9.E7.AA.97.E6.8F.90.E9.86.92)
    *   [5.8 弹出菜单项](#.E5.BC.B9.E5.87.BA.E8.8F.9C.E5.8D.95.E9.A1.B9)
    *   [5.9 Awesome的更多插件](#Awesome.E7.9A.84.E6.9B.B4.E5.A4.9A.E6.8F.92.E4.BB.B6)
    *   [5.10 Transparency](#Transparency)
        *   [5.10.1 ImageMagick](#ImageMagick)
    *   [5.11 自动运行程序](#.E8.87.AA.E5.8A.A8.E8.BF.90.E8.A1.8C.E7.A8.8B.E5.BA.8F)
    *   [5.12 使用 awesome-client 给文本插件传递信息](#.E4.BD.BF.E7.94.A8_awesome-client_.E7.BB.99.E6.96.87.E6.9C.AC.E6.8F.92.E4.BB.B6.E4.BC.A0.E9.80.92.E4.BF.A1.E6.81.AF)
    *   [5.13 使用其他任务栏](#.E4.BD.BF.E7.94.A8.E5.85.B6.E4.BB.96.E4.BB.BB.E5.8A.A1.E6.A0.8F)
    *   [5.14 Fix Java (GUI appears gray only)](#Fix_Java_.28GUI_appears_gray_only.29)
    *   [5.15 Prevent Nautilus from displaying the desktop (Gnome3)](#Prevent_Nautilus_from_displaying_the_desktop_.28Gnome3.29)
    *   [5.16 Transitioning away from Gnome3](#Transitioning_away_from_Gnome3)
    *   [5.17 Prevent the mouse scroll wheel from changing tags](#Prevent_the_mouse_scroll_wheel_from_changing_tags)
    *   [5.18 菜单栏中的应用程序目录](#.E8.8F.9C.E5.8D.95.E6.A0.8F.E4.B8.AD.E7.9A.84.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E7.9B.AE.E5.BD.95)
    *   [5.19 应用菜单](#.E5.BA.94.E7.94.A8.E8.8F.9C.E5.8D.95)
    *   [5.20 标题栏](#.E6.A0.87.E9.A2.98.E6.A0.8F)
    *   [5.21 Start xor jump](#Start_xor_jump)
    *   [5.22 Battery notification](#Battery_notification)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Mouse Cursor Missing](#Mouse_Cursor_Missing)
    *   [6.2 Grey Java GUIs](#Grey_Java_GUIs)
    *   [6.3 LibreOffice](#LibreOffice)
    *   [6.4 Mod4 key](#Mod4_key)
        *   [6.4.1 Mod4 key vs. IBM ThinkPad users](#Mod4_key_vs._IBM_ThinkPad_users)
    *   [6.5 Eclipse: cannot resize/move main window](#Eclipse:_cannot_resize.2Fmove_main_window)
    *   [6.6 YouTube: fullscreen appears in background](#YouTube:_fullscreen_appears_in_background)
    *   [6.7 Starting console clients on specific tags](#Starting_console_clients_on_specific_tags)
    *   [6.8 Redirecting console output to a file](#Redirecting_console_output_to_a_file)
*   [7 External Links](#External_Links)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")位于[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")的软件包 [awesome](https://www.archlinux.org/packages/?name=awesome)。

如果你对不稳定的预览版本有兴趣，可以从 [AUR](/index.php/AUR "AUR") 安装 [awesome-git](https://aur.archlinux.org/packages/awesome-git/)。但是请注意，这是一个不稳定的开发版，配置文件会有语法差异。

## 使用Awesome

### 不使用登陆管理器

不使用登录管理器来运行 awesome，只要添加 **`exec awesome`**到你的启动脚本（比如 ~/.xinitrc）。 详情参阅[xinitrc](/index.php/Xinitrc "Xinitrc")

你也可以甚至不用登陆直接使用预置用户启动Awesome，请参考[Start X at login](/index.php/Start_X_at_login "Start X at login")

### 使用登陆管理器

要想用登陆管理器启动awesome，看[这里](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)").

#### GDM, LightDM 以及其他使用 /usr/share/xsessions/ 的管理器

Awesome 会自动地为这些登陆管理器安装一份配置文件，不需要做其他的事就能在登陆时选择启动Awesome。

#### KDM

以root身份创建:

 `/usr/share/apps/kdm/sessions/awesome.desktop` 
```
[Desktop Entry]
Name=Awesome
Comment=Tiling Window Manager
Type=Application
Exec=/usr/bin/awesome
TryExec=/usr/bin/awesome
```

## 配置

Awesome默认的配置已经很不错了，不过你迟早会想要做一些修改的。配置文件是一个lua脚本：`~/.config/awesome/rc.lua`.

### 创建配置文件

创建配置文件所在的文件夹

```
 $ mkdir -p ~/.config/awesome/

```

Awesome会自动使用~/.config/awesome/rc.lua里的所有配置。这个文件并不会自动创建，所以我们先要从模板复制一个过来：

```
$ cp /etc/xdg/awesome/rc.lua ~/.config/awesome

```

配置文件的语法会随着Awesome的版本升级而变化，所以当你升级了之后遇到问题时，重复上面的步骤，或者你得手动修改配置文件。

要获得关于配置Awesome的更多信息，请看[Awesome wiki的配置部分](http://awesome.naquadah.org/wiki/Awesome_3_configuration)

### 更多的配置资源

**注意:** Awesome配置文件语法有时会变化，所以你可能得动手修改下载的配置文件。

一些不错的rc.lua的例子可以在下面这些站点找到：

*   [http://git.sysphere.org/awesome-configs/tree/](http://git.sysphere.org/awesome-configs/tree/) - Adrian C 的 Awesome 3.4 配置文件。 (anrxc)
*   [http://pastebin.com/f6e4b064e](http://pastebin.com/f6e4b064e) - Darthlukan 的 Awesome 3.4 配置文件.
*   [http://www.calmar.ws/dotfiles/dotfiledir/dot_awesomerc.lua](http://www.calmar.ws/dotfiles/dotfiledir/dot_awesomerc.lua)
*   [http://oxmoz.no-ip.org/awesome/rc.lua](http://oxmoz.no-ip.org/awesome/rc.lua)
*   [http://www.ugolnik.info/downloads/awesome/rc.lua](http://www.ugolnik.info/downloads/awesome/rc.lua) (screen) - 带有小型标题栏和状态栏的Awesome3配置文件。
*   [http://github.com/wolgri/wolgri.config/tree/master/.config/awesome/rc.lua](http://github.com/wolgri/wolgri.config/tree/master/.config/awesome/rc.lua)
*   [http://github.com/bash/dotfiles/blob/master/.config/awesome/rc.lua](http://github.com/bash/dotfiles/blob/master/.config/awesome/rc.lua)
*   [http://github.com/nblock/config/blob/master/.config/awesome/rc.lua](http://github.com/nblock/config/blob/master/.config/awesome/rc.lua)
*   [https://github.com/setkeh/Awesome-3.5](https://github.com/setkeh/Awesome-3.5) - [Setkeh](/index.php/User:Setkeh "User:Setkeh") 的 Awesome 3.5 配置文件.
*   [http://awesome.naquadah.org/wiki/User_Configuration_Files](http://awesome.naquadah.org/wiki/User_Configuration_Files) - Collection of user configurations on the awesome homepage.

### 调试 rc.lua

#### 使用 Xephyr

用这种方式可以在不破坏现有桌面的情况下对rc.lua进行测试。首先把 rc.lua 复制到一个新文件rc.lua.new，接着进行修改。然后在Xephyr中运行新的rc.lua (Xephyr允许你在XWindow中植入一个新的XWindow - ([screenshot](http://www.dante4d.cz/pub/screenie/2009-08-01-025216_1920x1200_scrot.png))。 你可以这样测试你的新rc.lua

```
$ Xephyr -ac -br -noreset -screen 1152x720 :1 &
$ DISPLAY=:1.0 awesome -c ~/.config/awesome/rc.lua.new

```

这种方式的巨大优势在于如果你弄坏了rc.lua.new，你不至于把现有的Awesome桌面弄得一团糟（并且很可能还会把XWindow弄崩溃了，没保存的工作全部丢失………）。一旦你觉得新的配置文件不错，就用rc.lua.new代替rc.lua，然后重启Awesome。

#### 使用 awmtt

[awmtt](https://aur.archlinux.org/packages/awmtt/) (Awesome WM Testing Tool) 是一个基于 Xephyr 的易于使用的脚本。默认情况下，它会测试 `~/.config/awesome/rc.lua.test` 。如果该文件不存在，它会测试当前使用的 rc.lua 。也可以指定要测试的配置文件所在路径：

```
$ awmtt start -C ~/.config/awesome/rc.lua.new

```

当测试完成后，使用以下命令关闭窗口:

```
$ awmtt stop

```

或者通过以下命令立即查看变化:

```
$ awmtt restart

```

### 改变键盘布局

如果需要使用不同的键盘布局 [qwerty -> dvorak] 有两种方法。

*   第一种就是按照 Awesome Wiki [这里](http://awesome.naquadah.org/wiki/Change_keyboard_maps#Display.2Fchange_keyboard_map) 所说的更改 Awesome 的配置
*   第二种就是在 [xorg settings](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg") 改变键盘布局

## 主题

[Beautiful](http://awesome.naquadah.org/wiki/Beautiful)可以让你动态地改变背景图片和颜色主题，而不需要改变 `rc.lua`。

默认的主题文件在 `/usr/share/awesome/themes/default`。把它复制到 `~/.config/awesome/themes/default` 然后修改一下 `rc.lua` 中的 `theme_path`。

```
beautiful.init(awful.util.getdir("config") .. "/themes/default/theme.lua")

```

更多细节参考 [这里](http://awesome.naquadah.org/wiki/Beautiful)

一些样例 [themes](http://awesome.naquadah.org/wiki/Beautiful_themes)

### 设置墙纸

Beautiful 可以设置墙纸，所以你就不用在 `.xinitrc` 或者 `.xsession` 中自己设置了。这允许你给每个主题配一个墙纸。

#### version >= 3.5

3.5 版本的 Awesome 不再提供 awsetbg 命令，但有了一个名为 gears 的模块。你可以在 `theme.lua` 通过以下代码设置你的墙纸。

```
theme.wallpaper = "~/.config/awesome/themes/awesome-wallpaper.png" 

```

为了加载你的墙纸，请确保你的 `rc.lua` 含有以下代码:

```
beautiful.init("~/.config/awesome/themes/default/theme.lua")
for s = 1, screen.count() do
	gears.wallpaper.maximized(beautiful.wallpaper, s, true)
end

```

#### 随机墙纸

请把以下代码加入你的 `rc.lua`(for awesome >= 3.5):

```
-- configuration - edit to your liking
wp_index = 1
wp_timeout  = 10
wp_path = "/path/to/wallpapers/"
wp_files = { "01.jpg", "02.jpg", "03.jpg" }

-- setup the timer
wp_timer = timer { timeout = wp_timeout }
wp_timer:connect_signal("timeout", function()

  -- set wallpaper to current index for all screens
  for s = 1, screen.count() do
    gears.wallpaper.maximized(wp_path .. wp_files[wp_index], s, true)
  end

  -- stop the timer (we don't need multiple instances running at the same time)
  wp_timer:stop()

  -- get next random index
  wp_index = math.random( 1, #wp_files)

  --restart the timer
  wp_timer.timeout = wp_timeout
  wp_timer:start()
end)

-- initial start when rc.lua is first run
wp_timer:start()
```

如果想从指定目录中自动抓取图片，把以下代码加入你的 `rc.lua`(for awesome >= 3.5 ):

```
-- {{{ Function definitions

-- scan directory, and optionally filter outputs
function scandir(directory, filter)
    local i, t, popen = 0, {}, io.popen
    if not filter then
        filter = function(s) return true end
    end
    print(filter)
    for filename in popen('ls -a "'..directory..'"'):lines() do
        if filter(filename) then
            i = i + 1
            t[i] = filename
        end
    end
    return t
end

-- }}}

-- configuration - edit to your liking
wp_index = 1
wp_timeout  = 10
wp_path = "/path/to/wallpapers/"
wp_filter = function(s) return string.match(s,"%.png$") or string.match(s,"%.jpg$") end
wp_files = scandir(wp_path, wp_filter)

-- setup the timer
wp_timer = timer { timeout = wp_timeout }
wp_timer:connect_signal("timeout", function()

  -- set wallpaper to current index for all screens
  for s = 1, screen.count() do
    gears.wallpaper.maximized(wp_path .. wp_files[wp_index], s, true)
  end

  -- stop the timer (we don't need multiple instances running at the same time)
  wp_timer:stop()

  -- get next random index
  wp_index = math.random( 1, #wp_files)

  --restart the timer
  wp_timer.timeout = wp_timeout
  wp_timer:start()
end)

-- initial start when rc.lua is first run
wp_timer:start()
```

想要随机切换墙纸，只需要注释掉 `wallpaper_cmd` 那一行, 然后把以下代码添加到你的 `.xinitrc` 中(for awesome <= 3.4 ):

```
while true;
do
  awsetbg -r <path/to/the/directory/of/your/wallpapers>
  sleep 15m
done &

```

## 小技巧

如果你有自己的小技巧想与大家分享，请随意添加。

### 使用awesome作为GNOME的窗口管理器

GNOME有“开包即用”的优势，你可以在使用GNOME的同时改用awesome作为窗口管理器。如果你在用GNOME 3的话，你可以安装[awesome-gnome](https://aur.archlinux.org/packages/awesome-gnome/)包，然后在用GDM登陆的时候选择"Awesome GNOME"。更多详细内容请参考[awesome wiki](http://awesome.naquadah.org/wiki/Quickly_Setting_up_Awesome_with_Gnome)。

### 像compiz那样的平铺桌面效果

Revelation可以显示所有你开启的客户端；左键点击客户端会跳到该客户端所在的第一个标签并聚焦于该客户端。按下回车键会跳到当前聚焦的客户端，按下ESc键退出。更多内容请参考[[1]](http://awesome.naquadah.org/wiki/Revelation)。

### 在awesome 3中显示/隐藏wibox

要使用Modkey-b来在当前屏幕上隐藏/显示默认的状态栏 (Awesome 2.3中的默认行为)，把下面代码加入rc.lua里的globalkeys变量:

```
awful.key({ modkey }, "b", function ()
    mywibox[mouse.screen].visible = not mywibox[mouse.screen].visible
end),

```

### 截图

在awesome中想要通过PrtScn按键来截图就必须借助其他截图工具. Arch软件仓库中,Scrot是个很简单就可以实现这些功能的截图工具.

只需要输入:

```
# pacman -S scrot

```

如果optional dependencies中可选的包觉得有用,也可以安装.

下一步,就是需要获得PrtScr按键的按键名, 如果不确定是什么,一般就是 "Print"了.

终端里面输入命令:

```
# xev

```

然后按键盘上的PrtScr按键, 将会输出类似下面的结果:

```
 KeyPress event ....
     root 0x25c, subw 0x0, ...
     state 0x0, keycode 107 (keysym 0xff61, **Print**), same_screen YES,
     ....

```

我们判断没错,键名就是 "Print".

接下来继续配置awesome!

在配置文件中的全局数组(任意地方)中输入并保存:

Lua 代码:

```
 awful.key({ }, "Print", function () awful.util.spawn("scrot -e 'mv $f ~/screenshots/ 2>/dev/null'") end),

```

这里的 ~/screenshots/ 可以改成你截图想要保存的地方.

### 动态标签

[Eminent](http://awesome.naquadah.org/wiki/Eminent)是一个小型的lua库，扩展了awful并提供了简单快速的wmii一样的动态标签功能。跟shifty不同, eminent无意提供全面详尽的标签系统，而是试图让动态标签越简单越好。实际上除了导入eminent库，你不用在rc.lua里改任何东西，eminent会把所有的事情帮你搞定。

[Shifty](http://awesome.naquadah.org/wiki/Shifty)是实现了动态标签的一个Awesome 3的扩展。它也实现了一个配置系统来让你设置几个变量和键位绑定就完全掌控你的桌面！

### Space Invaders

[Space Invaders](http://awesome.naquadah.org/wiki/Space_Invaders)是一个用来展现Awesome Lua API无限能力的演示。

请注意它从3.4-rc1版以后就没有被包括进Awesome包里了。

### Naughty弹窗提醒

请查看[Awesome维基上的naughty页面](http://awesome.naquadah.org/wiki/Naughty).

### 弹出菜单项

这是一份 awesome3 的默认简单菜单项, 看起来要自定义也十分容易. 然而,如果你在用awesome的 2.x 版本, 那么请看*[awful.menu](http://awesome.naquadah.org/wiki/Awful.menu)*.

如果你想要配置 freedesktop.org 的菜单项,就到 *[awesome-freedesktop](https://github.com/terceiro/awesome-freedesktop)* .

一个 awesome3 的菜单配置示例:

```
myawesomemenu = {
   { "lock", "xscreensaver-command -activate" },
   { "manual", terminal .. " -e man awesome" },
   { "edit config", editor_cmd .. " " .. awful.util.getdir("config") .. "/rc.lua" },
   { "restart", awesome.restart },
   { "quit", awesome.quit }
}

mycommons = {
   { "pidgin", "pidgin" },
   { "OpenOffice", "soffice-dev" },
   { "Graphic", "gimp" }
}

mymainmenu = awful.menu.new({ items = { 
                                        { "terminal", terminal },
                                        { "icecat", "icecat" },
                                        { "Editor", "gvim" },
                                        { "File Manager", "pcmanfm" },
                                        { "VirtualBox", "VirtualBox" },
                                        { "Common App", mycommons, beautiful.awesome_icon },
                                        { "awesome", myawesomemenu, beautiful.awesome_icon }
                                       }
                             })
```

### Awesome的更多插件

*Awesome中的插件是一些你可以加入插件栏 (状态栏和标题栏) 的东西，它们提供了关于你的系统的各种信息，并让你很方便地直接在窗口管理器上就看到这些信息。这些插件很简易而且有很强的灵活性。* -- 来自 [Awesome Wiki: Widgets](http://awesome.naquadah.org/wiki/Widgets_in_awesome)。

有一个被广泛使用的插件库叫**Wicked** (只与**3.4版以前**的Awesome兼容)，它提供了更多插件，比如MPD插件，CPU使用情况，内存使用情况等。要更详细的了解参见 [Wicked](http://awesome.naquadah.org/wiki/Wicked)。

Awesome 3.4中用来代替Wicked的有**[Vicious](http://awesome.naquadah.org/wiki/Vicious)**，**[Obvious](http://awesome.naquadah.org/wiki/Obvious)** 和 **[Bashets](http://awesome.naquadah.org/wiki/Bashets)**。如果你选择使用vicious，你也应该看看 [vicious的文档](http://git.sysphere.org/vicious/tree/README)。

### Transparency

Awesome has support for true transparency through xcompmgr. Note that you'll probably want the git version of xcompmgr, which is [available in AUR](https://aur.archlinux.org/packages.php?ID=16554).

Add this to your ~/.xinitrc:

```
xcompmgr &

```

See *man xcompmgr* or [xcompmgr](/index.php/Xcompmgr "Xcompmgr") for more options.

In awesome 3.4, window transparency can be set dynamically using signals. For example, your rc.lua could contain the following:

```
client.add_signal("focus", function(c)
                              c.border_color = beautiful.border_focus
                              c.opacity = 1
                           end)
client.add_signal("unfocus", function(c)
                                c.border_color = beautiful.border_normal
                                c.opacity = 0.7
                             end)

```

**If you got error messages about add_signal, using connect_signal insteaded.**

Note that if you are using conky, you must set it to create its own window instead of using the desktop. To do so, edit ~/.conkyrc to contain:

```
own_window yes
own_window_transparent yes
own_window_type desktop

```

Otherwise strange behavior may be observed, such as all windows becoming fully transparent. Note also that since conky will be creating a transparent window on your desktop, any actions defined in awesome's rc.lua for the desktop will not work where conky is.

As of Awesome 3.1, there is built-in pseudo-transparency for wiboxes. To enable it, append 2 hexadecimal digits to the colors in your theme file (~/.config/awesome/themes/default, which is usually a copy of /usr/share/awesome/themes/default), like shown here:

```
bg_normal = #000000AA

```

where "AA" is the transparency value.

To change transparency for the actual selected window by pressing Modkey + PageUp/PageDown you can also use tansset-df available through the community package repository and the following modification to your rc.lua:

```
globalkeys = awful.util.table.join(
    -- your keybindings
    [...]
    awful.key({ modkey }, "Next", function (c)
        awful.util.spawn("transset-df --actual --inc 0.1")
    end),
    awful.key({ modkey }, "Prior", function (c)
        awful.util.spawn("transset-df --actual --dec 0.1")
    end),
    -- Your other key bindings
    [...]
)

```

#### ImageMagick

如果你用ImageMagick的*display*命令来设置你的墙纸，可能会遇到xcompmgr效果不好的问题。请注意awsetbg可能会用*display*如果它没有其他选项。安装habak，feh，hsetroot或者其他的包应该会解决这个问题。 (*grep -A 1 wpsetters /usr/bin/awsetbg* 来看你有哪些选项)

### 自动运行程序

*参见 [Awesome维基上的自动运行](https://awesome.naquadah.org/wiki/Autostart).*

Awesome不会运行那些被Freedesktop如GNOME或KDE设置为自动运行的程序。不过Awesome提供了一些运行程序的函数 (除了Lua标准库里的函数 `os.execute`)。要运行跟GNOME或KDE里一样自动运行的程序，你可以从 [AUR](/index.php/AUR "AUR") 安装 [dex-git](https://aur.archlinux.org/packages/dex-git/)，然后在你的rc.lua里加入:

```
os.execute"dex -a -e Awesome"

```

如果你只想列出一些程序来在让Awesome启动时运行，你可以创建一个你需要启动命令的列表然后循环启动:

```
do
  local cmds = 
  { 
    "swiftfox",
    "mutt",
    "consonance",
    "linux-fetion",
    "weechat-curses",
    --and so on...
  }

  for _,i in pairs(cmds) do
    awful.util.spawn(i)
  end
end

```

(你也可以调用 `os.execute` 加上命令名，在结尾加上 '`&`'，但最好还是调用 spawn 函数来运行)

如要程序仅在当前没有运行情况下运行，你可以只在 `pgrep` 找不到跟它一样名字的进程的时候运行它。

```
function run_once(prg)
  awful.util.spawn_with_shell("pgrep -u $USER -x " .. prg .. " || (" .. prg .. ")")
end

```

所以，举个例子，要在当前 `parcellite` 没有运行的情况下运行 `parcellite`:

```
run_once("parcellite")

```

### 使用 awesome-client 给文本插件传递信息

只需要创建一个新的插件，就可以很容易的传递信息。

```
 mywidget = widget({ type = "textbox", name = "mywidget" })
 mywidget.text = "initial text"

```

使用 awesome-client 从外部更新“initial text":

```

 echo -e 'mywidget.text = "new text"' | awesome-client

```

不要忘记把插件增加到 wibox.

### 使用其他任务栏

如果你喜欢 awesome 既轻量又强大的功能,但又不喜欢默认那个任务栏的外观, 你可以安装其他的.比如 xfce4-panel:

```
sudo pacman -S xfce4-panel

```

当然,你可能有更好的选择.然后要把它添加到配置文件 rc.lua 的自动启动部分(该如何写请看wiki吧).你可以注释掉配置文件中给每个桌面创建 wiboxes 的那部分(开头是"mywibox[s] = awful.wibox({ position = "top", screen = s })"),因为已经不需要了. 检查配置文件没有错误之后就可以执行命令生效:

```
awesome -k rc.lua

```

另外你还需要改变"modkey+R"的快捷键绑定, 比如用Xfrun4, bashrun等,来替代awesome自带的启动器. 请看这个[Openbox](/index.php/Openbox_Themes_and_Apps#Application_launchers "Openbox Themes and Apps")文章中的启动器部分作为参考. 别忘了添加

```
      properties = { floating = true } },
    { rule = { instance = "$yourapplicationlauncher" },

```

到你 rc.lua 配置文件中

### Fix Java (GUI appears gray only)

Guide taken from [[2]](https://bbs.archlinux.org/viewtopic.php?pid=450870).

1.  Install [wmname](https://www.archlinux.org/packages/?name=wmname) from community
2.  Run the following command or add it to your `.xinitrc`: `wmname LG3D` 

**Note:**

If you use a non-reparenting window manager and Java 6, you should uncomment the corresponding line in `/etc/profile.d/openjdk6.sh`

If you use a non-reparenting window manager and Java 7, you should uncomment the corresponding line in `/etc/profile.d/jre.sh`

**Note:**

As of Java 1.7 and Awesome 3.5 (as installed by the awesome-git package) the fixes described above may cause undesirable behaviour related to menus not receiving proper focus. Awesome is now, apparently, a reparenting window manager as of [this commit](http://git.naquadah.org/?p=awesome.git;a=commit;h=102063dbbdfb0bc9f43268d98f7dcb5269547395).

If you are experiencing problems having applied the 'wmname' and '_JAVA_AWT_WM_NONREPARENTING' fixes against a recent Java and Awesome, try removing both fixes.

### Prevent Nautilus from displaying the desktop (Gnome3)

Run dconf-editor. Navigate to org->gnome->desktop->background and uncheck "draw-background" as well as "show-desktop-icons" for good measure. That's it!

Another option is moving /usr/bin/nautilus to a new location and replacing it with a script that runs 'nautilus --no-desktop' passing any arguments it receives along.

```
#!/bin/sh
/usr/bin/nautilus-real --no-desktop $@

```

### Transitioning away from Gnome3

Run 'gnome-session-properties' and remove programs that you won't be needing anymore (e.g Bluetooth Manager, Login Sounds, etc).

If you'd like to get rid of GDM, make sure that your rc.conf DAEMONS list includes "dbus" (and "cupsd" if you have a printer). It's advisable to get a different login manager (like [SLiM](/index.php/SLiM "SLiM")), but you can do things manually if you wish. That entails setting up your [.xinitrc properly](/index.php/Udev "Udev") and installing something like devmon ([AUR](https://aur.archlinux.org/packages.php?ID=45842)).

If you wan't to keep a few convenient systray applets and your GTK theme, append this to your rc.lua;

```
function start_daemon(dae)
	daeCheck = os.execute("ps -eF | grep -v grep | grep -w " .. dae)
	if (daeCheck ~= 0) then
		os.execute(dae .. " &")
	end
end

procs = {"gnome-settings-daemon", "nm-applet", "kupfer", "gnome-sound-applet", "gnome-power-manager"}
for k = 1, #procs do
	start_daemon(procs[k])
end

```

### Prevent the mouse scroll wheel from changing tags

In your rc.lua, change the Mouse Bindings section to the following;

```
-- {{{ Mouse bindings
root.buttons(awful.util.table.join(
    awful.button({ }, 3, function () mymainmenu:toggle() end)))
-- }}}

```

### 菜单栏中的应用程序目录

[community] 中的 Awesome 软件包含有 [menubar](http://awesome.naquadah.org/wiki/Menubar/3.5) （默认情况下，按下 modkey+p 会在屏幕上方打开一个类似于 dmenu 的应用程序菜单）。但是，它仅搜索位于 `/usr/share/applications` 及 `/usr/local/share/applications` 目录下的 .desktop 文件 （后者很可能在大多数 Arch 用户的系统中都不存在）。为了改变这一情况，可以把下面这行代码加入到你的 `rc.lua` （最好能把它加到 "Menubar configuration" 那一部分中）

```
app_folders = { "/usr/share/applications/", "~/.local/share/applications/" }

```

**注意:** 每次 Awesime 启动都会重新读取 `.desktop` 文件，因此文件过多会拖慢 Awesome 的启动速度。如果你更喜欢使用其他方式来运行程序，可以通过在 `rc.lua` 移除 `local menubar = require("menubar")` 及其它涉及到 `menubar` 的变量来禁用菜单栏。

### 应用菜单

如果想要在点击Awesome图标，或者在桌面空白处右键点击时，看到较传统模式的应用菜单，可以参照[Xdg-menu#Awesome](/index.php/Xdg-menu#Awesome "Xdg-menu")的说明。但应用菜单不会在安装或卸载程序时进行更新。所以，确保运行类似如下的命令，更新应用菜单：

```
 xdg_menu --format awesome --root-menu /etc/xdg/menus/arch-applications.menu >~/.config/awesome/archmenu.lua

```

### 标题栏

你可以很容易地在配置文件中把 `titlebars_enabled` 设置为 true 来启用标题栏。如果想要切换标题栏的显示与否，可以把以下代码加入配置文件，然后通过按 `modkey + Ctrl + t` 来切换。

```
awful.key({ modkey, "Control" }, "t",
   function (c)
       -- toggle titlebar
       awful.titlebar.toggle(c)
   end)

```

如果想默认情况下隐藏标题栏，仅需要在配置文件中标题栏创建后加入以下代码

```
awful.titlebar.hide(c)

```

### Start xor jump

There is an extension called *Run or raise*, which makes it possible to configure a key to start a program if no instance exists, else jump to it. This is very useful for some programs: browsers, irc clients, music players, etc. The instructions are very well laid out at [http://awesome.naquadah.org/wiki/Run_or_raise](http://awesome.naquadah.org/wiki/Run_or_raise), the modular approach is advisable.

### Battery notification

If you want to add a simple battery notification you can add following lines to your rc.lua. These lines originate from a [blogpost](http://bpdp.blogspot.be/2013/06/battery-warning-notification-for.html). Note that you need naughty for the notifications (installed by default in version 3.5).

 `rc.lua` 
```

-- battery warning
local function trim(s)
  return s:find'^%s*$' and '' or s:match'^%s*(.*%S)'
end

local function bat_notification()
  local f_capacity = assert(io.open("/sys/class/power_supply/BAT0/capacity", "r"))
  local f_status = assert(io.open("/sys/class/power_supply/BAT0/status", "r"))
  local bat_capacity = tonumber(f_capacity:read("*all"))
  local bat_status = trim(f_status:read("*all"))

  if (bat_capacity <= 10 and bat_status == "Discharging") then
    naughty.notify({ title      = "Battery Warning"
      , text       = "Battery low! " .. bat_capacity .."%" .. " left!"
      , fg="#ffffff"
      , bg="#C91C1C"
      , timeout    = 15
      , position   = "bottom_right"
    })
  end
end

battimer = timer({timeout = 60})
battimer:connect_signal("timeout", bat_notification)
battimer:start()

-- end here for battery warning

```

## Troubleshooting

### Mouse Cursor Missing

If you are able to login into awesome, the mouse cursor vanishes while mouse actions are still working, you can try this:

```
gsettings set org.gnome.settings-daemon.plugins.cursor active false

```

### Grey Java GUIs

Some Java Applications may render just grey, empty windows. This is related to nonreparenting.

A fix might be uncommenting the last line in /etc/profile.d/jre.sh or set this manually.

```
export _JAVA_AWT_WM_NONREPARENTING=1

```

other Methods could be found here: [http://awesome.naquadah.org/wiki/Problems_with_Java](http://awesome.naquadah.org/wiki/Problems_with_Java)

### LibreOffice

If you encounter UI problems with libreoffice install libreoffice-gnome.

### Mod4 key

The Mod4 is by default the **Win key**. If it's not mapped by default, for some reason, you can check the keycode of your Mod4 key with

```
$ xev

```

It should be 115 for the left one. Then add this to your ~/.xinitrc

```
xmodmap -e "keycode 115 = Super_L" -e "add mod4 = Super_L"
exec awesome

```

The problem in this case is that some xorg installations recognize keycode 115, but incorrectly as the 'Select' key. The above command explictly remaps keycode 115 to the correct 'Super_L' key.

#### Mod4 key vs. IBM ThinkPad users

IBM ThinkPads do not come equipped with a Window key (although Lenovo have changed this tradition on their ThinkPads). As of writing, the Alt key is not used in command combinations by the default rc.lua (refer to the Awesome wiki for a table of commands), which allows it be used as a replacement for the Super/Mod4/Win key. To do this, edit your rc.lua and replace:

```
modkey = "Mod4"

```

by:

```
modkey = "Mod1"

```

Note: Awesome does a have a few commands that make use of Mod4 plus a single letter. Changing Mod4 to Mod1/Alt could cause overlaps for some key combinations. The small amount of instances where this happens can be changed in the rc.lua file.

If you do not like to change the awesome standards, you might like to remap a key. For instance the caps lock key is rather useless (for me) adding the following contents to ~/.Xmodmap

```
clear lock 
add mod4 = Caps_Lock

```

and [(re)load](/index.php/Xmodmap#Custom_table "Xmodmap") the file. This will change the caps lock key into the mod4 key and works nicely with the standard awesome settings. In addition, if needed, it provides the mod4 key to other X-programs as well.

Not confirmed, but if recent updates of xorg related packages break mentioned remapping the second line can be replaced by (tested on a DasKeyboard with no left Super key):

```
keysym Caps_Lock = Super_L Caps_Lock

```

### Eclipse: cannot resize/move main window

If you get stuck and cannot move or resize the main window (using mod4 + left/right mouse button) edit the workbench.xml and set fullscreen/maximized to false (if set) and reduce the width and height to numbers smaller than your single screen desktop area.

**Note:** workbench.xml can be found in: <eclipse_workspace>/.metadata/.plugins/org.eclipse.ui.workbench/ and the line to edit is <window height="xx" maximized="true" width="xx" x="xx" y="xx">.

### YouTube: fullscreen appears in background

[[3]](https://bbs.archlinux.org/viewtopic.php?pid=1085494#p1085494) If YouTube videos appear underneath your web browser when in fullscreen mode, add this to your rc.lua

```
   { rule = { instance = "plugin-container" },
     properties = { floating = true } },

```

With Chromium add

```
   { rule = { instance = "exe" },
     properties = { floating = true } },

```

### Starting console clients on specific tags

It does not work when the console application is invoked from a GTK terminal (e.g. LXTerminal). [URxvt](/index.php/URxvt "URxvt") is known to work.

### Redirecting console output to a file

Some GUI application are very verbose when launched from a terminal. As a consequence, when started from Awesome, they output everything to the TTY from where Awesome was started, which tend to get messy. To remove the garbage output, you have to redirect it. However, the `awful.util.spawn` function does not handle pipes and redirections very well as stated in [the official FAQ](http://awesome.naquadah.org/wiki/FAQ#How_to_execute_a_shell_command.3F).

As example, let's redirect [Luakit](/index.php/Luakit "Luakit") output to a temporary file:

```
awful.key({ modkey, }, "w", function () awful.util.spawn_with_shell("luakit 2>>/tmp/luakit.log") end),

```

## External Links

*   [http://awesome.naquadah.org/wiki/FAQ](http://awesome.naquadah.org/wiki/FAQ) - FAQ
*   [http://www.lua.org/pil/](http://www.lua.org/pil/) - Programming in Lua (first edition)
*   [http://awesome.naquadah.org/](http://awesome.naquadah.org/) - The official awesome website
*   [http://awesome.naquadah.org/wiki/Main_Page](http://awesome.naquadah.org/wiki/Main_Page) - the awesome wiki
*   [http://www.penguinsightings.org/desktop/awesome/](http://www.penguinsightings.org/desktop/awesome/) - A review
*   [http://compsoc.tardis.ed.ac.uk/wiki/AwesomeWM_guide](http://compsoc.tardis.ed.ac.uk/wiki/AwesomeWM_guide) - Awesome guide
*   [https://bbs.archlinux.org/viewtopic.php?id=88926](https://bbs.archlinux.org/viewtopic.php?id=88926) - share your awesome!