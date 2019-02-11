**翻译状态：** 本文是英文页面 [Conky](/index.php/Conky "Conky") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-01-23，点击[这里](https://wiki.archlinux.org/index.php?title=Conky&diff=0&oldid={{{3}}})可以查看翻译后英文页面的改动。

Related articles

*   [Conky/Tips_and_tricks](/index.php/Conky/Tips_and_tricks "Conky/Tips and tricks")
*   [Lm_sensors](/index.php/Lm_sensors "Lm sensors")
*   [Hddtemp](/index.php/Hddtemp "Hddtemp")

Conky 是一个用于X窗口系统的系统监视软件。它可以运行在 GNU/Linux 和 FreeBSD 上，是一个基于GPL协议的免费软件。Conky 可以监控许多系统变量，包括 CPU，内存，交换分区，磁盘空间，温度，top，上传，下载，系统消息，以及更多。它具有很高的可配置性，但配置有一些难于理解。Conky是torsmo的一个分支。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 双屏幕](#双屏幕)
    *   [2.2 配置文件语法更改](#配置文件语法更改)
*   [3 字体](#字体)
    *   [3.1 符号字体](#符号字体)
*   [4 自启动](#自启动)
*   [5 故障排除](#故障排除)
    *   [5.1 Conky启动并且在屏幕上不显示任何内容](#Conky启动并且在屏幕上不显示任何内容)
    *   [5.2 透明度](#透明度)
        *   [5.2.1 伪透明](#伪透明)
        *   [5.2.2 启用真实透明](#启用真实透明)
        *   [5.2.3 半透明](#半透明)
    *   [5.3 不最小化显示桌面](#不最小化显示桌面)
    *   [5.4 在GNOME Shell集成](#在GNOME_Shell集成)
    *   [5.5 UTF-8 多字节字符固定滚动修复](#UTF-8_多字节字符固定滚动修复)
    *   [5.6 避免闪烁](#避免闪烁)
*   [6 你还可以看](#你还可以看)

## 安装

*   [官方软件库](/index.php/Official_repositories "Official repositories")中已经包含了[conky](https://www.archlinux.org/packages/?name=conky)，您可以通过[pacman](/index.php/Pacman "Pacman")来安装它。

除了 [官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库") 上的 [conky](https://www.archlinux.org/packages/?name=conky) 软件包, 在 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 上还有很多关于conky的软件包。

*   Conky基本包，没有X11依赖 [conky-cli](https://aur.archlinux.org/packages/conky-cli/)
*   Nvidia支持： [conky-nvidia](https://aur.archlinux.org/packages/conky-nvidia/)
*   Lua支持： [conky-lua](https://aur.archlinux.org/packages/conky-lua/)
*   Nvidia和Lua支持： [conky-lua-nv](https://aur.archlinux.org/packages/conky-lua-nv/)

一些在conky变量上的建设需要安装额外的应用才能被使用，例如温度控制的 [Hddtemp](/index.php/Hddtemp "Hddtemp") 和音乐控制的 [mpd](/index.php/Mpd "Mpd")

你可以编辑`~/.conkyrc`文件来定制您的conky或是使用[homeproject-screenshot](http://conky.sourceforge.net/screenshots.html)等其他网站上的范例

附加应用:

*   **Conky Manager** — Conky小部件的主题管理器. 它提供开启、关闭选项, 浏览和编辑已经安装的Conky主题.

	[http://www.teejeetech.in/p/conky-manager.html](http://www.teejeetech.in/p/conky-manager.html) || [conky-manager](https://www.archlinux.org/packages/?name=conky-manager)

## 配置

*   当您在编辑配置文件时,点击保存命令可立即看到conky界面的变化.您也没有必要重新登录您的X环境.所以您可以尽情尝试每一个设置，保存配置文件并查看conky界面的变化,然后修改不合适的地方.

*   或者，您可以使用默认配置:

```
$ conky -C > ~/.config/conky/conky.conf

```

当然最好还是使用位于当前用户下`~/.conkyrc`的配置文件. 就像其他的应用一样, conky会先查看当前用户下的`.conkyrc`文件.如果检测失败,那么它将使用位于`/etc/conky`的默认配置文件.

如果您保存配置文件在本地,比如在保存在您的home目录中,您将不能查看任何的日志文件除非您更改一些配置. One of the nice features of conky is to pipe to your desktop some `/var/log/` files to read all kinds of log messages.这些文件只能在`root`身份下查看,然后您需要通过`sudo`来启动conky.用`root`身份来启动conky是不推荐的,所以您需要进行以下设置:

```
$ usermod -aG log username

```

将 `username` 加入 `log group`. 现在 `username` can read log files, and you will be able to redirect log messages with conky on your desktop.

*   如果conky并没有显现应有的效果 -- 比如 minimum_size -- 您需查看是否是因清空了 `/etc/conky/conky.conf`中的内容，或是因注释相关字段所造成。

### 双屏幕

当你使用双屏幕配置时, 你需要进行一些设置来将 *conky* 放置到你想让它呆在桌面的某个位置.

通过调整`gap_x`, 假设你设置的是1680x1050像素的分辨率，你希望窗口位于左侧显示器的中间顶部，你应使用 :

```
alignment = 'top_left',
gap_X = 840,

```

`alignment` 的作用是显而易见的， `gap_X`是从屏幕左边框开始的距离（以像素为单位）。.

`xinerama_head`是一个可替换的选项，下面将在第二个屏幕的右上角放置“conky”窗口:

```
alignment = 'top_right',
xinerama_head = 2,

```

### 配置文件语法更改

从conky 1.10以来，配置文件都是用新的lua语法编写的，比如：

```
 conky.config = {
   -- Comments start with a double dash
   bool_value = true,
   string_value = 'foo',
   int_value = 42,
 }
 conky.text = [[
 $variable
 ${evaluated variable}
 ]]

```

下面的一些示例可能仍然使用旧语法，例如：

```
 bool_value yes
 string_value 'foo'
 int_value 42

```

通过Lua脚本可以从旧语法转换为新的Lua语法。 [here](https://github.com/brndnmtthws/conky/blob/master/extras/convert.lua).

## 字体

要用conky显示unicode格式图片和emoji，你需要支持此功能的[font](/index.php/Fonts#Emoji_and_symbols "Fonts") 然后将conky配置为需显示的unicode字体. 例如:

```
 ${font Symbola:size=48}☺${font} 

```

### 符号字体

符号字体常用于更复杂的conky配置，其中一些流行的配置包括；

*   [ttf-pizzadude-bullets](https://aur.archlinux.org/packages/ttf-pizzadude-bullets/) - PizzaDude Bullet's font
*   [otf-font-awesome-5-free](https://aur.archlinux.org/packages/otf-font-awesome-5-free/) - Font awesome icon from from [http://fontawesome.com/](http://fontawesome.com/)
*   [ttf-weather-icons](https://aur.archlinux.org/packages/ttf-weather-icons/) - Erik flowers weather icon font with 222 glyphs

## 自启动

Conky可以通过几种不同的方式自启动, 一如 "[Autostarting](/index.php/Autostarting "Autostarting")"所述. 请选择最适合您的窗口管理器/桌面环境的方式.

Conky有一种配置，使它在后台分支运行。这可能对于某些自动启动设置有效。

In `conky.conf`:

```
conky.config = {
    background = true,
}

```

如果你使用图形桌面环境，并希望通过`conky.desktop` 自启动，请使用以下命令：

 `~/.config/autostart/conky.desktop` 
```
[Desktop Entry]
Type=Application
Name=conky
Exec=conky --daemonize --pause=5
StartupNotify=false
Terminal=false
```

`pause=5`参数在“conky”启动时会延时5秒钟，以确保桌面有时间加载并启动。

## 故障排除

这些是人们在conky发现的问题和他们的解决方案。

### Conky启动并且在屏幕上不显示任何内容

首先检查配置文件文本变量中的语法错误。然后再次检查你的用户是否有权运行配置文件中的每个命令，以及是否安装了所有需要的包。

### 透明度

Conky支持两种不同类型的透明度。需要安装并运行[composite manager](/index.php/Composite_manager "Composite manager"). 如果启用了真实透明，但是没有运行复合管理器，那么conky将不会优先透明，但是为字体、图像和背景启用了透明度。

#### 伪透明

默认情况下，在Conky中启用了伪透明。伪透明通过复制背景图像，并使用相关部分作为conky的背景达成效果。一些窗口管理器将背景墙纸设置为根窗口之上的一个级别，这可能导致conky具有灰色背景。要解决此问题，需要手动将其设置为*feh*。 In `~/.xinitrc`:

```
 sleep 1 && feh --bg-center ~/background.png &

```

#### 启用真实透明

要实现真正的透明性，必须运行一个[composite manager](/index.php/Composite_manager "Composite manager") 并在conky.config内的`.conkyrc`中添加以下行：

```
 conky.config = {
    own_window = true,
    own_window_transparent = true,
    own_window_argb_visual = true,
    own_window_type = desktop,
 }

```

如果窗口类型“桌面”不起作用，请尝试将其更改为 `normal`.如果仍然不起作用，请尝试其他选项，例如: `dock`, `panel`, 或者 `override` 替代.

**Note:** [Xfce](/index.php/Xfce "Xfce")需要混合启用，请参见 [[1]](https://forum.xfce.org/viewtopic.php?pid=25939).

#### 半透明

要在真实透明模式下实现半透明，必须在conky配置文件中使用以下设置:

```
 conky.config = {
    own_window = true,
    own_window_transparent = false,
    own_window_argb_visual = true,
    own_window_argb_value = 90,
    own_window_type = desktop,
 }

```

为了降低conky窗口的透明度，其中一种方式是可以将`own_window_argb_value` 的值增至 255.

### 不最小化显示桌面

**Using Compiz:** 如果 'Show Desktop' 选项或键绑定与所有其他窗口一起和condy最小化, 启动compiz配置设置管理器，转到“General Options”并取消选中“Hide Skip Taskbar Windows”选项。.

如果不使用compiz，请尝试编辑 `conky.conf` 并添加/更改如下:

```
own_window_type = 'override',

```

或者

```
own_window_type = 'desktop',

```

请参阅“conky”帮助文档了解具体差异。但是，后一个选项允许您使用调整大小键绑定（例如OpenBox）将窗口捕捉到“conky”的边界，而第一个选项则没有。

### 在GNOME Shell集成

有人在[GNOME](/index.php/GNOME "GNOME")内的*conky*经历了错误.

在 `conky.conf`添加:

```
own_window = true,
own_window_type = 'desktop',

```

### UTF-8 多字节字符固定滚动修复

“conky”（1.9.0）的当前版本存在一个[bug](https://github.com/brndnmtthws/conky/issues/129) 其中滚动文本按字节而不是按字符递增，从而导致包含多字节字符的文本在滚动时消失并重新出现。在 AUR: [conky-utfscroll](https://aur.archlinux.org/packages/conky-utfscroll/)中可以找到修复此错误的补丁包。

### 避免闪烁

*Conky*需要X服务内的双重缓冲扩展名*(DBE)* 支持来避免闪烁，因为没有它，窗口就无法足够快速的更新窗口. 可以通过 在 `/etc/X11/xorg.conf` 里的 [Xorg](/index.php/Xorg "Xorg")通过在`"Module"`中添加`Load "dbe"` 选项来启动. `xorg.conf` 文件已经被包含特定配置文件的`/etc/X11/xorg.conf.d` 所替代(1.8.x 版本以上)。只要 *DBE* 存在于`/usr/lib/xorg/modules`它就会被自动加载. 加载模块列表可以使用 `grep LoadModule /var/log/Xorg.0.log`查看.

要启用双重缓冲，请将`double_buffer`选项加入`conky.conf`:

```
 conky.config = {
     double_buffer = true,
 }

```

## 你还可以看

*   [官方网站](https://github.com/brndnmtthws/conky)
*   [官方配置的Conky变量](http://conky.sourceforge.net/config_settings.html)
*   [官方Conky对象](http://conky.sourceforge.net/variables.html)
*   [Arch论坛中的Conky配置](https://bbs.archlinux.org/viewtopic.php?id=39906)
*   [Conky](http://freecode.com/projects/conky/) on [Freecode](https://en.wikipedia.org/wiki/Freecode "wikipedia:Freecode")
*   [#conky](irc://chat.freenode.org/conky) IRC chat channel on [freenode](https://en.wikipedia.org/wiki/Freenode "wikipedia:Freenode")
*   [常见问题](http://novel.evilcoder.org/wiki/index.php?title=ConkyFAQ&oldid=12463)