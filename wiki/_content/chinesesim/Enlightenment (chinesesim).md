相关文章

*   [桌面环境](/index.php/%E6%A1%8C%E9%9D%A2%E7%8E%AF%E5%A2%83 "桌面环境")
*   [显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器")
*   [窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")

## Contents

*   [1 Enlightenment](#Enlightenment)
    *   [1.1 安装](#.E5.AE.89.E8.A3.85)
        *   [1.1.1 从 AUR 安装](#.E4.BB.8E_AUR_.E5.AE.89.E8.A3.85)
    *   [1.2 启动 Enlightenment](#.E5.90.AF.E5.8A.A8_Enlightenment)
        *   [1.2.1 Entrance](#Entrance)
        *   [1.2.2 手动启动 Enlightenment](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8_Enlightenment)
    *   [1.3 配置](#.E9.85.8D.E7.BD.AE)
        *   [1.3.1 网络](#.E7.BD.91.E7.BB.9C)
        *   [1.3.2 Polkit 代理](#Polkit_.E4.BB.A3.E7.90.86)
        *   [1.3.3 集成 GNOME 密钥环](#.E9.9B.86.E6.88.90_GNOME_.E5.AF.86.E9.92.A5.E7.8E.AF)
        *   [1.3.4 系统托盘](#.E7.B3.BB.E7.BB.9F.E6.89.98.E7.9B.98)
        *   [1.3.5 通知](#.E9.80.9A.E7.9F.A5)
    *   [1.4 主题](#.E4.B8.BB.E9.A2.98)
        *   [1.4.1 GTK+](#GTK.2B)
    *   [1.5 模块和小部件](#.E6.A8.A1.E5.9D.97.E5.92.8C.E5.B0.8F.E9.83.A8.E4.BB.B6)
        *   [1.5.1 "外部" 模块](#.22.E5.A4.96.E9.83.A8.22_.E6.A8.A1.E5.9D.97)
    *   [1.6 默认键绑定](#.E9.BB.98.E8.AE.A4.E9.94.AE.E7.BB.91.E5.AE.9A)
    *   [1.7 排错](#.E6.8E.92.E9.94.99)
        *   [1.7.1 合成](#.E5.90.88.E6.88.90)
        *   [1.7.2 字体看不清楚](#.E5.AD.97.E4.BD.93.E7.9C.8B.E4.B8.8D.E6.B8.85.E6.A5.9A)
        *   [1.7.3 背光总是较暗](#.E8.83.8C.E5.85.89.E6.80.BB.E6.98.AF.E8.BE.83.E6.9A.97)
        *   [1.7.4 光标主题不一致](#.E5.85.89.E6.A0.87.E4.B8.BB.E9.A2.98.E4.B8.8D.E4.B8.80.E8.87.B4)
        *   [1.7.5 背景图片](#.E8.83.8C.E6.99.AF.E5.9B.BE.E7.89.87)
*   [2 Enlightenment DR16](#Enlightenment_DR16)
    *   [2.1 安装 E16](#.E5.AE.89.E8.A3.85_E16)
    *   [2.2 基本设置](#.E5.9F.BA.E6.9C.AC.E8.AE.BE.E7.BD.AE)
        *   [2.2.1 启动、重启、停止脚本](#.E5.90.AF.E5.8A.A8.E3.80.81.E9.87.8D.E5.90.AF.E3.80.81.E5.81.9C.E6.AD.A2.E8.84.9A.E6.9C.AC)
        *   [2.2.2 合成器（Compositor）](#.E5.90.88.E6.88.90.E5.99.A8.EF.BC.88Compositor.EF.BC.89)
*   [3 参考资料](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99)
*   [4 配置输入法](#.E9.85.8D.E7.BD.AE.E8.BE.93.E5.85.A5.E6.B3.95)
    *   [4.1 ibus](#ibus)

## Enlightenment

这个软件包提供了 [Enlightenment](https://www.enlightenment.org/) 的[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")及其构建库 EFL（Enlightenment Foundation Libraries）。后者提供了额外的桌面环境特性，如工具包、对象画布和抽象对象。Enlightenment 从 2005 年开始开发，2011 年 2 月发布 1.0 稳定版本。

### 安装

可[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")同名软件包 [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) 。

还可以安装 [terminology](https://www.archlinux.org/packages/?name=terminology)，这是一个基于 EFL 的终端仿真器。

#### 从 AUR 安装

**警告:** 其中某些软件包使用不稳定的开发版代码，请风险自担。

开发版的软件包源码及其依赖的包构建文件可以从 [enlightenment-git](https://aur.archlinux.org/packages/enlightenment-git/) 下载。 以下是基于 EFL 的应用，大部份是开发版本，尚未正式发布：

*   [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) – Ecrire 文本编辑器
*   [edi](https://aur.archlinux.org/packages/edi/) – 基于EFL的集成开发环境(IDE)
*   [elbow-git](https://aur.archlinux.org/packages/elbow-git/) – Elbow 浏览器
*   [eluminance-git](https://aur.archlinux.org/packages/eluminance-git/) – Eluminance 图片浏览器
*   [enjoy-git](https://aur.archlinux.org/packages/enjoy-git/) – [Enjoy](https://trac.enlightenment.org/e/wiki/Enjoy) 音乐播放器
*   [eperiodique](https://aur.archlinux.org/packages/eperiodique/) – [Eperiodique](http://eperiodique.sourceforge.net/) periodic 表格查看器
*   [ephoto](https://aur.archlinux.org/packages/ephoto/) and [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) – [Ephoto](http://smhouston.us/ephoto/)图片查看器
*   [epour](https://aur.archlinux.org/packages/epour/) – 基于EFL的种子(torrent)客户端
*   [epymc-git](https://aur.archlinux.org/packages/epymc-git/) – E Python 多媒体中心
*   [equate-git](https://aur.archlinux.org/packages/equate-git/) – Equate 计算器
*   [eruler-git](https://aur.archlinux.org/packages/eruler-git/) – Eruler 屏幕尺和测量工具
*   [efbb-git](https://aur.archlinux.org/packages/efbb-git/) – Escape from Booty Bay 类似《愤怒的小鸟》的游戏
*   [elemines-git](https://aur.archlinux.org/packages/elemines-git/) – [Elemines](http://elemines.sourceforge.net/) 《扫雷》类型的游戏
*   [espionage-git](https://aur.archlinux.org/packages/espionage-git/) – Espionage D-Bus 监测器
*   [ev-git](https://aur.archlinux.org/packages/ev-git/) – ev 简单图片查看器
*   [rage](https://aur.archlinux.org/packages/rage/) and [rage-git](https://aur.archlinux.org/packages/rage-git/) – Rage 视频播放器

### 启动 Enlightenment

从你惯用的[显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器")选择*Enlightenment* ，或配置好 [xinitrc](/index.php/Xinitrc "Xinitrc") 从控制台启动。

#### Entrance

**警告:** Entrance 为实验性版本，还不被 systemd 完全支持 ，请风险自担。

Enlightenment 提供了一个名为 Entrance 的新显示管理器，由 [entrance-git](https://aur.archlinux.org/packages/entrance-git/) 提供。Entrance 十分精巧，它用 `/etc/entrance.conf` 管理配置。可以通过 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") 启用 `entrance.service` 服务来使用它。

#### 手动启动 Enlightenment

如果选择从控制台手工启动，把下列内容加入 `~/.xinitrc` 文件：

 `~/.xinitrc` 
```
exec enlightenment_start

```

然后就可以输入 `startx` 来启动 Enlightenment。详见 [xinitrc](/index.php/Xinitrc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinitrc (简体中文)")。

### 配置

Enlightenment 提供了一个精巧的配置系统，可以从主菜单中选择“设置”子菜单进入。

#### 网络

**ConnMan**

Enlightenment 首选的网络管理器是 [ConnMan](/index.php/ConnMan "ConnMan") ，包名： [connman](https://www.archlinux.org/packages/?name=connman) 。配置方法参见：[ConnMan](/index.php/ConnMan "ConnMan")。

为实现更多的配置，还可以安装 Econnman （AUR 中的 [econnman](https://aur.archlinux.org/packages/econnman/) 或 [econnman-git](https://aur.archlinux.org/packages/econnman-git/)）及其相关依赖包。

**把 ConnMan 添加到书架**

1.  设置 -> 扩展 -> 模块
2.  系统
3.  连接管理器（Connection Manager）
4.  加载（选中并点击*加载*）
5.  在屏幕底部书架点击右键
6.  进入书架 -> 内容
7.  滚动项目列表找到 *ConnMan*
8.  点击*添加*

**NetworkManager**

你也可以使用 [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 来管理网络连接。参见 [NetworkManager (简体中文)](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NetworkManager (简体中文)")。

注意：这个小程序需要Appindicator支持才能在Enlightenment的[系统托盘](#.E7.B3.BB.E7.BB.9F.E6.89.98.E7.9B.98)中显示。可参考[NetworkManager#Appindicator](/index.php/NetworkManager#Appindicator "NetworkManager").作为使用该程序的一种选择，NetworkManager包含了CLI and TUI两种网络配置界面--参见[NetworkManager#命令行](/index.php/NetworkManager#.E5.91.BD.E4.BB.A4.E8.A1.8C "NetworkManager")。

#### Polkit 代理

Enlightenment 没有提供[图形化的 polkit 认证代理](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81.E7.BB.84.E4.BB.B6 "Polkit (简体中文)")。如果要执行某些需授权的操作（例如安装系统设备上的文件系统），你要安装一个认证代理并且使它自动启动。后者可以导航至***设置面板 > 应用 > 启动应用程序 > 系统***设置项并激活它。AUR 中提供了一个基于 EFL 的认证代理，名为 [polkit-efl-git](https://aur.archlinux.org/packages/polkit-efl-git/)。

#### 集成 GNOME 密钥环

在Enlightenment中可以使用gnome-keyring. 然而你需要做一点小的更改才能让它完全地工作。首先你需要设置Enlightenment去自动启动gnome-keyring，定位到*Settings Panel > Apps > Startup Applications > System* 并激活 *Certificate and Key Storage*、 *GPG Password Agent*、*SSH Key Agent* 以及 "Secret Storage Service"。 然后, 你应该编辑 `~/.pam_environment` 并添加下面的代码:

```
       #Set gnome-keyring as the ssh authentication agent
       SSH_AUTH_SOCK=/run/user/${UID}/keyring/ssh

```

上述代码会覆盖"enlightenment-start"变量的自动启动配置，从"ssh-agent" 切换到gnome-keyring。

更多信息参考[GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")一文。

#### 系统托盘

**注意:** 从 Enlightenment 20 版开始，对 Xembed 的支持已被移除 [[1]](https://twitter.com/_enlightenment_/status/538000507315314688)。这意味着许多“传统的”托盘部件将无法显示在托盘。要使用这些托盘部件，需要另外安装一个独立的系统托盘程序（例如 [stalonetray](https://www.archlinux.org/packages/?name=stalonetray)）

Enlightenment 支持系统托盘，但默认未启用。若要启用系统托盘，请打开 Enlightenment 主菜单，导航至***设置***子菜单，点击***模块***选项，向下滚动至***系统托盘***选项并聚焦，点击***加载***按钮。这样就加载了模块，可将其添加到书架中。在待添加系统托盘的书架上右击，聚焦于***书架***子菜单，点击***内容*** 选项，向下滚动到***系统托盘***并聚焦，然后点击***添加***按钮。

#### 通知

Enlightenment 的“通知”扩展模块提供了一个通知服务器。

*   通知可以按下述定义显示在屏幕任一角落
*   可用的屏幕策略有：主屏幕、当前屏幕、所有屏幕和 Xinerama
*   通知可以按紧急程度过滤（低、普通、紧急，及各种组合形式）
*   可以设置默认通知消隐时间，也可以设置是否强制不自动消隐
*   通知服务器可以设置是否忽略替换 ID 的请求

### 主题

下列更多主题用于定制 Enlightenment 外观：

*   [enlightenment-themes.org](https://www.enlightenment-themes.org/)
*   [relighted.c0n.de](http://relighted.c0n.de/#100) 默认主题的 200 种不同颜色组合
*   [git.enlightenment.org](http://git.enlightenment.org/themes)（用 git 抓取喜欢的主题，运行 'make' 生成 .edj 后缀的主题文件）
*   [packages.bodhilinux.com](http://packages.bodhilinux.com/bodhi/pool/stable/b/) 这里有一堆不错的主题（需从 .deb 包中释放出 .edj 文件，可以用 ArchLinux 的基础组件 bsdtar 释放）。在他们的维基上还提供了一个很不错的分类
*   [[2]](https://web.archive.org/web/20140120083020/http://art.bodhilinux.com/doku.php?id=bodhi_e17_themes_v3)。
*   [exchange.enlightenment.org](https://web.archive.org/web/20161025233126/https://exchange.enlightenment.org/theme) (archived)

你可以在主题设置对话框中安装这些 .edj 文件格式的主题，或者把它们放在 `~/.e/e/themes` 目录中。

**注意:** Enlightenment 未提供完整的主题 API，多年来，甚至在 E17 发布后，很多主题 API 也已改变。未及时更新的主题很可能无法正常工作。

**提示：** 若要使 GTK 和 Qt 应用程序与 Enlightenment 默认主题相匹配，你可以下载一个类似 [E17 GTK 主题](http://gnome-look.org/content/show.php/?content=163472)这样的主题包，放在 `~/.themes/` 中或者安装[gtk-theme-e17gtk-git](https://aur.archlinux.org/packages/gtk-theme-e17gtk-git/)包，并在Enlightenment 的设置中选中它，然后对其做配置。这样可以使所有 GTK2 和 GTK3 应用匹配默认 Enlightenment 主题，然后，你可以配置 Qt 应用程序（或者配置 Qt 的默认设置），让其使用 Gtk+ 主题。这样 Qt 应用程序将模拟当前使用的 GTK 应用程序。这样就可以让绝大部分应用程序都使用 enlightenment 的主题。参阅[Qt 与 GTK 应用程序外观一致化](/index.php/Qt_%E4%B8%8E_GTK_%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E5%A4%96%E8%A7%82%E4%B8%80%E8%87%B4%E5%8C%96 "Qt 与 GTK 应用程序外观一致化")。

#### GTK+

替换 GTK+ 主题的选项在***设置 > 全部 > 外观 > 应用程序主题***。

### 模块和小部件

	模块

	小工具的后端支持代码在Enlightenment中使用的名称。

	小工具

	前端或用户界面，应该有助于Enlightenment的用户完成某项任务。

很多模块提供了可以添加到桌面或面板上的小工具。某些模块(如CPUFreq) 只提供了单个的小工具；而一些模块 (如Composite) 虽然不提供小工具，但提供了额外的功能。 注意某些小工具（如Systray）只能被添加到面板上，而另一些小工具（如Moon）只能在桌面上加载。

#### "外部" 模块

**警告:** 这些第三方模块不被官方开发者支持。它们直接来自 git ，因而随时可能工作异常。请风险自担。

除了这里列举的模块, 更多的模块可以从[e-modules-extra-git](https://aur.archlinux.org/packages/e-modules-extra-git/)找到。

**Scale Windows**

*Scale Windows*模块添加了额外的功能，但需要开启 compositing. 缩放窗口特效（Scale Windows）可以缩小所有打开的窗口并使它们全部进入预览视图。 这项功能与macOS中的"Mission Control"功能相类似. scale pager特效缩放所有桌面并将它们如壁纸一样显示，类似于插件 expo. 这两项功能都可以添加到桌面，或者与快捷键、鼠标以及屏幕边缘绑定起来。

某些用户喜欢将标准的窗口选择快捷键`ALT + Tab`改变为使用缩放窗口特效（Scale Windows）去选择窗口。为了达到上述目的, 你需要依次定位到*Menu> Settings > Settings Panel > Input> Keys*. 在这里你可以设置任何你喜欢的快捷键。

若需要将窗口选择键绑定功能替换为缩放窗口特效（Scale Windows）,滚动做面板直到*ALT*节然后找到并选择`ALT + Tab`. 然后滚动右面版寻找"Scale Windows"并选择*Select Next* 或者*Select Next (All)* 并点击*Apply*保存设置，*Select Next*选项仅能看到当前桌面的窗口，*Select Next (All)*选项可看到所有桌面上的窗口。 可以使用[upstream git](https://git.enlightenment.org/enlightenment/modules/comp-scale.git/)包。

### 默认键绑定

<caption>Some default Enlightenment keybindings</caption>
| Shift + F10 | Maximize Vertically |
| Ctrl + Menu | Show "Clients" (windows) Menu |
| Alt + Escape | Show "Everything Launcher" (apps, windows, etc) |
| Win + Left | Maximize Left |
| Win + Right | Maximize Right |
| Alt + Shift + F10 | Maximize Horizontally |
| Alt + Shift + Left | Flip to the Desktop on the Left |
| Alt + Shift + Right | Flip to the Desktop on the Right |
| Ctrl + Alt + D | Show the desktop |
| Ctrl + Alt + F | Toggle Fullscreen |
| Ctrl + Alt + I | Toggle iconic mode |
| Ctrl + Alt + K | Kill window |
| Ctrl + Alt + L | Lock the desktop |
| Ctrl + Alt + N | Maximize Window |
| Ctrl + Alt + R | Toggle Shade up |
| Ctrl + Alt + W | Window menu |
| Ctrl + Alt + X | Close a window |
| Ctrl + Alt + Down | Lower |
| Ctrl + Alt + Up | Raise |
| Ctrl + Alt + Left | Flip to desktop on left |
| Ctrl + Alt + Right | Flip to desktop on right |
| Ctrl + Alt + Delete | End session dialog |
| Ctrl + Alt + Insert | Launch the default terminal |

### 排错

如果你的Enlightenment出现了一些奇怪的行为, 你可以尝试下面的步骤:

1.  尝试使用默认主题，看这些行为是否会出现；
2.  禁用你安装的所有第三方模块；
3.  备份`~/.e`文档并移除`~/.e`(使用命令`mv ~/.e ~/.e.back`)；

若你确定自己发现了一个BUG，请将它提交到[directly upstream](https://phab.enlightenment.org/maniphest/task/create/)页面。

#### 合成

当需要在无法打开设置窗口的情况下重置设置的时候, 可以通过硬编码（hardcoded）快捷键`Ctrl + Alt + Shift + Home`重置合成器的设置。

#### 字体看不清楚

如果字体太小而无法阅读,首先确定你已经安装了正确的字体包。 安装[ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) 和[ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera) 字体包是一个不错的选择。

你可以在 *Settings > Settings Panel > Look > Scaling*选项中设置缩放。

#### 背光总是较暗

你或许会发现在登出的情况下 Enlightenment 会常规性的将背光调低为30%，却只能在你登录到另一个新的Enlightenment session时才能恢复到100%。当使用Enlightenment和另一个桌面环境时，该问题特别明显；因为当使用该桌面环境时，背光不会自动恢复到正常水平。要修复该问题， 打开 *Settings Panel*，在*Look* 标签下, 勾选 *Composite* 选项。勾选*Don't fade backlight* 前的方框并点击*OK*.

#### 光标主题不一致

可能会发现桌面的光标主题与应用（如[Firefox (简体中文)](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)")）中的光标主题不一样。 这是因为应用使用的是X光标主题，而Enlightenment有自己的光标主题设置。 为了前后一致, 你可以设置 Enlightenment总是使用X光标主题。 为了实现该目标, 打开 Enlightenment的 *Settings Panel* 然后点击 *Input*标签。之后点击 *Mouse* 选项。将其主题从*Enlightenment* 切换到 *X* 然后点击*OK*保存即可。 你应该可以发现光标主题在每一个地方都是一样的。 如果X光标主题并不总是一致的，可参考[光标主题](/index.php/Cursor_themes_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#XDG_.E8.A7.84.E5.88.99 "Cursor themes (简体中文)")

#### 背景图片

你需要将想要设置为背景的图片拷贝到 `~/.e/e/backgrounds/`目录下。

在桌面的任意地方点击鼠标中键（MMB）或右键（RMB）访问“设置”选项，选择`/Desktop/Backgrounds/`

任何新拷贝到`~/.e/e/backgrounds/`文件夹下的图片都会自动更新可供选择的背景列表。 从下拉菜单中选择你想要设置的图片。在全局设置中的 *appropriate*选项卡内，可以调整背景图像的平铺、填充屏幕等。

## Enlightenment DR16

Enlightenment, 开发版 16 第一次发布于2000年,在2009年到达了 1.0版. 初始情况下，DR16表示Enlightenment项目的0.16版。它就是现在Arch源的"Enlightenment16", 直到今天还在开发维护中, 通常由它的维护者 Kim 'kwo' Woelders提供更新。With compositing, shadows and transparencies, E16 kept all of the speed that presided over its foundation by original author Carsten "Rasterman" Haitzler but with up to date refinement.

### 安装 E16

安装[enlightenment16](https://www.archlinux.org/packages/?name=enlightenment16)包.

如需要深入的文档，可以参考`/usr/share/doc/e16/e16.html`. 在[e16(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/e16.1)中的手册，只给了一些启动选项。

### 基本设置

E16的大多数设置文件保存在`~/.e16`目录中，并且是基于文本、可以编辑的。其中也包含了菜单（menus）。

快捷键可以通过手动修改,也可以使用e16keyedit 软件修改；该软件可以在[sourceforge](http://sourceforge.net/projects/enlightenment/)页面找到。注意：默认情况下不会在`~/.e16`目录下创建键盘快捷键绑定文件。如果你想做修改的话，可以通过下面的命令将安装包自带的键盘快捷键绑定文件复制到你的home目录下：

```
$ cp /usr/share/e16/config/bindings.cfg ~/.e16

```

#### 启动、重启、停止脚本

在你的`~/.e16`文件夹中创建 Init, a Start and a Stop 文件夹: 任何在这些文件夹中的 .sh 脚本 将会在启动时(位于Init文件夹)、每次重启时(位于Start文件夹)或者关机时(位于Stop文件夹)被执行; 假如你允许它们通过 MMB / settings / session / <enable scripts> button并 通过`chmod +x **yourscript.sh**`命令赋予它们可执行权限。经典的例子是启动pulseaudio或者你喜欢的网络管理程序。

#### 合成器（Compositor）

阴影、透明等等特效位于 Composite 项下的 MMB 或 RMB / 设置。

## 参考资料

*   [Enlightenment 主页](http://www.enlightenment.org/)
*   [Enlightenment Exchange](http://exchange.enlightenment.org/)
*   [Enlightenment 开发者文档](http://docs.enlightenment.org/)
*   [Bodhi Guide to Enlightenment](http://www.bodhilinux.com/e17guide/e17guideEN/)
*   [E17-Stuff](http://www.e17-stuff.org/)
*   [DR16 下载资源](http://sourceforge.net/projects/enlightenment/)
*   [Enlightenment 用户邮件列表](https://lists.sourceforge.net/lists/listinfo/enlightenment-users)
*   [Enlightenment 开发者邮件列表](https://lists.sourceforge.net/lists/listinfo/enlightenment-devel)
*   [irc://irc.freenode.net#e](irc://irc.freenode.net#e)

## 配置输入法

**注意:** 英文版本节文字已删除。为方便中文用户，本节内容暂予保留

E17 内置了输入法支持的模块，支持的输入法有 iiimf 、scim 和 uim 。使用这些输入法的配置在

```
Settings -> Settings Panel -> Language -> Input Method Settings -> Advanced

```

System 配置中，使用者只需选择即可。使用其他输入法的用户可以在 Personal 配置中添加。

### ibus

ibus 的配置参数为：

```
Input Method Parameters:
 Name              ibus
 Execute Command   /usr/bin/ibus-daemon --xim
 Setup Command     /usr/bin/ibus-setup

```

```
Exported Environment Variables:
 GTK_IM_MODULE     ibus
 QT_IM_MODULE      ibus
 XMODIFIERS        @im=ibus

```