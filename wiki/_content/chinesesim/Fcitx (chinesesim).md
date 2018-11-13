Related articles

*   [IBus](/index.php/IBus "IBus")
*   [SCIM](/index.php/SCIM "SCIM")
*   [UIM](/index.php/UIM "UIM")

**翻译状态：** 本文是英文页面 [Fcitx](/index.php/Fcitx "Fcitx") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-31，点击[这里](https://wiki.archlinux.org/index.php?title=Fcitx&diff=0&oldid=535074)可以查看翻译后英文页面的改动。

[Fcitx](https://en.wikipedia.org/wiki/Fcitx "wikipedia:Fcitx") (Flexible Input Method Framework) ──即小企鹅输入法，它是一个以 GPL 方式发布的[输入法](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method")平台,可以通过安装引擎支持多种输入法，支持简入繁出，是在 Linux 操作系统中常用的中文输入法。它的优点是，短小精悍、跟程序的兼容性比较好。

## Contents

*   [1 安装](#安装)
    *   [1.1 输入法引擎](#输入法引擎)
        *   [1.1.1 中文](#中文)
        *   [1.1.2 Japanese](#Japanese)
        *   [1.1.3 其它语言](#其它语言)
    *   [1.2 输入法模块](#输入法模块)
    *   [1.3 其它](#其它)
*   [2 使用](#使用)
    *   [2.1 桌面环境](#桌面环境)
    *   [2.2 非桌面环境](#非桌面环境)
    *   [2.3 Xim](#Xim)
*   [3 配置](#配置)
    *   [3.1 配置工具](#配置工具)
    *   [3.2 替换自带的经典界面](#替换自带的经典界面)
    *   [3.3 输入法](#输入法)
    *   [3.4 扩充内置拼音词库](#扩充内置拼音词库)
    *   [3.5 皮肤](#皮肤)
    *   [3.6 云拼音](#云拼音)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 快捷键](#快捷键)
    *   [4.2 Vim](#Vim)
    *   [4.3 剪贴板](#剪贴板)
    *   [4.4 特殊符号](#特殊符号)
    *   [4.5 快速输入](#快速输入)
*   [5 故障排除](#故障排除)
    *   [5.1 停用或修改 *Extra key for trigger input method*](#停用或修改_Extra_key_for_trigger_input_method)
    *   [5.2 首先诊断问题所在](#首先诊断问题所在)
    *   [5.3 Emacs 无法使用输入法](#Emacs_无法使用输入法)
    *   [5.4 Firefox 右键菜单不弹出](#Firefox_右键菜单不弹出)
    *   [5.5 在 GTK2 程序中用 Ctrl + Space 不能调出输入法](#在_GTK2_程序中用_Ctrl_+_Space_不能调出输入法)
    *   [5.6 在 gnome-terminal中 Ctrl + Space 不能调出输入法](#在_gnome-terminal中_Ctrl_+_Space_不能调出输入法)
    *   [5.7 Ctrl + ; 会调出 Fcitx 的剪贴板](#Ctrl_+_;_会调出_Fcitx_的剪贴板)
    *   [5.8 fcitx-sogoupinyin 卡死、联想失败](#fcitx-sogoupinyin_卡死、联想失败)
    *   [5.9 在某些程序下输入法总是被切换到美语键盘](#在某些程序下输入法总是被切换到美语键盘)
    *   [5.10 Gnome On Wayland 用户无法使用 fcitx](#Gnome_On_Wayland_用户无法使用_fcitx)
*   [6 参见](#参见)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")软件包 [fcitx](https://www.archlinux.org/packages/?name=fcitx)。

### 输入法引擎

Fcitx 内置的输入法支持中文 [拼音](https://en.wikipedia.org/wiki/Pinyin "wikipedia:Pinyin") 和基于字符表的输入(例如[五笔](https://en.wikipedia.org/wiki/Wubi_method "wikipedia:Wubi method")). 根据语言的不同，有不同的输入法引擎可以选择。

#### 中文

在 Fcitx 支持的拼音输入法中，内置拼音响应速度最快。Fcitx 同样支持流行的第三方拼音输入法以提供更好的整句输入效果.

*   [fcitx-sunpinyin](https://www.archlinux.org/packages/?name=fcitx-sunpinyin) 在输入速度和输入精度之间有较好的平衡。
*   [fcitx-libpinyin](https://www.archlinux.org/packages/?name=fcitx-libpinyin) 算法比 sunpinyin 先进。
*   [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime), 即著名中文输入法 [Rime IME](/index.php/Rime_IME "Rime IME")的 Fcitx 版本。但它不支持 Fcitx 本身的 [#特殊符号](#特殊符号) 和 [#快速输入](#快速输入) 功能，自定义设置请参见[官方](http://rime.im)，
*   [fcitx-googlepinyin](https://www.archlinux.org/packages/?name=fcitx-googlepinyin), Google 拼音输入法 for Android.
*   [fcitx-sogoupinyin](https://aur.archlinux.org/packages/fcitx-sogoupinyin/), 搜狗输入法for linux—支持全拼、简拼、模糊音、云输入、皮肤、中英混输入。[官方网址](http://pinyin.sogou.com/linux/)
*   [fcitx-cloudpinyin](https://www.archlinux.org/packages/?name=fcitx-cloudpinyin) 可以提供云拼音输入的支持，支持 Fcitx 下的所有拼音输入法，Fcitx-rime 除外。
*   [fcitx-chewing](https://www.archlinux.org/packages/?name=fcitx-chewing) 为 Fcitx 添加 chewing (繁体中文注音) 输入引擎支持。依赖 [libchewing](https://www.archlinux.org/packages/?name=libchewing).
*   [fcitx-table-extra](https://www.archlinux.org/packages/?name=fcitx-table-extra) adds [Cangjie](https://en.wikipedia.org/wiki/Cangjie_input_method "wikipedia:Cangjie input method"), [Zhengma](https://en.wikipedia.org/wiki/Zhengma_method "wikipedia:Zhengma method"), [Boshiamy](https://en.wikipedia.org/wiki/Boshiamy_method "wikipedia:Boshiamy method") support.

#### Japanese

*   [fcitx-mozc](https://www.archlinux.org/packages/?name=fcitx-mozc), 为 Fcitx 添加 mozc (日语) 输入引擎支持，mozc 是 Google 日语输入法的开源版本。
*   [fcitx-kkc](https://www.archlinux.org/packages/?name=fcitx-kkc), a new Japanese Kana Kanji input engine, based on [libkkc](https://www.archlinux.org/packages/?name=libkkc).
*   [fcitx-anthy](https://www.archlinux.org/packages/?name=fcitx-anthy), 为 Fcitx 添加 anthy (日语) 输入引擎支持。

#### 其它语言

*   [fcitx-hangul](https://www.archlinux.org/packages/?name=fcitx-hangul), 为 Fcitx 添加 hangul (韩语) 输入引擎支持。
*   [fcitx-m17n](https://www.archlinux.org/packages/?name=fcitx-m17n), 为 Fcitx 添加 m17n (多国语言码表) 输入引擎支持。
*   [fcitx-unikey](https://www.archlinux.org/packages/?name=fcitx-unikey), 为 Fcitx 添加 unikey (越南语) 输入引擎支持。
*   [fcitx-sayura](https://www.archlinux.org/packages/?name=fcitx-sayura), 为 Fcitx 添加 sayura （僧伽罗语） 输入引擎支持。

### 输入法模块

Fcitx 提供对 Gtk+/Qt 提供了输入法模块，请根据需要安装 [fcitx-gtk2](https://www.archlinux.org/packages/?name=fcitx-gtk2), [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3), [fcitx-qt4](https://www.archlinux.org/packages/?name=fcitx-qt4) 和 [fcitx-qt5](https://www.archlinux.org/packages/?name=fcitx-qt5). 软件包组 [fcitx-im](https://www.archlinux.org/groups/x86_64/fcitx-im/) 包含了全部模块。如果没有安装对应的模块，一般还是可以在大部分程序中使用输入法的。不过很可能出现从无法光标跟随、无法显示预编辑字符串、无法输入甚至程序卡死等情况。

某些程序不使用 Gtk+/Qt 的输入法模块，这些程序包括:

*   所有不使用 Gtk+/Qt的程序，如使用 Tk, motif, 甚至 xlib 的程序
*   Emacs,Opera,OpenOffice,LibreOffice,Skype,Wine,Java,Xterm,urxvt,WPS

### 其它

*   [fcitx-ui-light](https://www.archlinux.org/packages/?name=fcitx-ui-light), Fcitx 的轻量 UI.
*   [fcitx-table-extra](https://www.archlinux.org/packages/?name=fcitx-table-extra) Fcitx 的一些额外码表支持，包括仓颉 3, 仓颉 5, 粤拼, 速成, 五笔, 郑码等等
*   [fcitx-table-other](https://www.archlinux.org/packages/?name=fcitx-table-other), Fcitx 的一些更奇怪的码表支持，包括 Latex, Emoji, 以及一大堆不明字符等等。

您还可以在 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 找到更多以上软件包的 Git 版以及其它。

## 使用

### 桌面环境

如果您用 XDG 兼容的桌面环境，比如 [KDE](/index.php/KDE "KDE"), [GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce"), [LXDE](/index.php/LXDE "LXDE"), 那么当您安装好 Fcitx 并重新登录后，Fcitx 应该会自动启动。如果没有的话，可以打开控制台并运行`fcitx`。为检验 Fcitx 是否正常运行, 打开一个程序，比如 leafpad, 按 CTRL+Space 激活 Fcitx 并试着输入几个字。

如果 Fcitx 没有随桌面环境自动启动，或者您想修改下 Fcitx 启动参数，请用桌面环境提供的自动启动工具配置，或者直接编辑用户目录`~/.config/autostart/` 下的 `fcitx-autostart.desktop` 文件以确认自动启动是否被禁用。如果用户目录下的文件并不存在，您可以复制自动启动文件 `/etc/xdg/autostart/fcitx-autostart.desktop` 到用户目录：

```
cp /etc/xdg/autostart/fcitx-autostart.desktop ~/.config/autostart/

```

如果您使用的桌面环境并不自动支持 XDG 自动启动, 请在您使用的启动脚本里面添加 `fcitx` 以实现自动启动。

当 iBus 等其它输入法程序同时启动且开启了 Xim 支持时, 可能会害 Fcitx 启动不了，请确保已禁用了其它输入法程序的自动启动。

### 非桌面环境

将下面内容加入桌面的启动脚本，以注册输入法模块并支持 xim 程序。

 `~/.pam_environment` 
```
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx

```

重新登录后让环境变量生效。

如果 *fcitx* 没有自动启动，请将 `fcitx &` 加入 `~/.xinitrc`。

*   请不要在 `.bashrc` 设置这些环境变量。`bashrc`只应用于交互性 bash 会话的初始化，并不应用于非交互性脚本或 X 会话的初始化。
*   如果 Qt 使用 fcitx 有问题，请执行 qtconfig (qtconfig-qt4)，在输入法配置中将 fcitx 设置为 "Default Input Method"。

### Xim

您还可以在 Gtk+/Qt 程序中用 xim, 为此您要将上面设置的变量改成如下的值：

```
GTK_IM_MODULE=xim
QT_IM_MODULE=xim

```

**警告:** 使用 xim, 很可能会遇到一些包括不能输入, 没有光标跟随, 重启输入法时应用程序卡死在内的无法由 Fcitx 解决的问题，且官方不支持解决。

重新登录后让环境变量生效。

**Note:** Gtk2 从 2.24.20 开始，使用 `/usr/lib/gtk-2.0/2.10.0/immodules.cache` 作为缓存文件。如果设置了 `GTK_IM_MODULE_FILE` 环境变量或在安装后修改了配置，请清掉环境变量并使用 `/usr/bin/gtk-query-immodules-2.0 --update-cache` 更新缓存。

## 配置

### 配置工具

Fcitx 提供了若干图形界面的配置程序：KDE 中的 [kcm-fcitx](https://www.archlinux.org/packages/?name=kcm-fcitx), 基于 GTK+3 的 [fcitx-configtool](https://www.archlinux.org/packages/?name=fcitx-configtool)。

安装完配置工具[fcitx-configtool](https://www.archlinux.org/packages/?name=fcitx-configtool)之后打开配置工具的方法是用终端运行fcitx-config-gtk3，打开这个配置工具之后还要添加中文输入法。对于新安装的英文系统，要取消只显示当前语言的输入法（Only Show Current Language），才能看到和添加中文输入法(Pinyin, Libpinyin等)。

如果要手工编辑 fcitx 的配置文件，请确保系统中并没有在运行 fcitx ，否则手工编辑的配置内容可能丢失。

### 替换自带的经典界面

Fcitx 支持使用 kimpanel 协议的界面，以提供更好的桌面整合体验.

*   Gnome-Shell: 安装 [gnome-shell-extension-kimpanel-git](https://aur.archlinux.org/packages/gnome-shell-extension-kimpanel-git/), 它提供了类似 ibus-gjs 的用户体验，其候选框界面将会采用 Gnome-Shell 的主题风格, 同时在状态栏中增加 Fcitx 的输入法状态图标。
*   KDE: [kimtoy](https://www.archlinux.org/packages/?name=kimtoy) 可以使用搜狗输入法和 Fcitx 本身的皮肤。

### 输入法

您可以在配置界面工具中添加／移除启用的输入法。列表第一项将作为「未激活」状态使用，请遵从界面上的提示将列表中的此项设为键盘布局输入法，比如「(键盘 - 英文)」，列表第二项则是默认输入法，其它项则为可切换到的输入法。

**警告:** 请必须将键盘布局输入法设为列表中第一项, 否则可能会无法禁用中文输入。

### 扩充内置拼音词库

用户配置拼音词库在 `~/.config/fcitx/pinyin`, 其中 `pybase.mb` 为拼音单字库，`pyphrase.mb` 为拼音词库。如果这两文件并不存在，直接将您下载的词库放置到 `/usr/share/fcitx/pinyin`. 重启 Fcitx 即可。

### 皮肤

下载皮肤并解压缩到下面任一目录，如果没有可以新建目录：

```
/usr/share/fcitx/skin   ##全局设置
~/.config/fcitx/skin    #特定用户设置

```

### 云拼音

安装后重启 Fcitx 即可，所选的云拼音输入结果会自动添加到当前输入法的词库中。提醒：建议在fcitx设置里面将“云拼音来源”由Google改为“百度”，Google国内访问不是很顺畅。

启用云拼音后，从云拼音获得的候选词会默认添加到候选词列表中的第二个，显示位置可以通过云拼音的设置配置。如果云拼音的结果和本地输入法给出的结果一致，云拼音后选项会和本地产生的候选项自动合并，不会产生重复的候选项。

若安装fcitx-cloudpinyin后，在配置程序里却没有看见云拼音，记得勾上“高级”复选框。这时云拼音会显示出来，再勾上云拼音。

**注意:** 不推荐将云拼音候选词设为第一个候选词，因为当网络情况不好，没有及时返回云拼音结果，那么云拼音结果将默认降到第二候选词的位置，于是这个过程可能会涉及到默认候选词的改变。

## 提示与技巧

### 快捷键

部分常用默认快捷键：

*   Ctrl + Space 激活输入法
*   左Shift 临时切换到英文
*   Ctrl + Shift 输入法间切换
*   -/= 向前/向后翻页
*   Shift + Space 全角、半角切换

**注意:** 您可以在配置界面的全局配置中修改这些快捷键。

### Vim

如果您经常在 Vim 下使用 Fcitx, 可以安装 [vim-fcitx](https://aur.archlinux.org/packages/vim-fcitx/) 插件，或者在 `~/.vimrc` 添加如下代码。以退出插入模式时，自动关闭 Fcitx, 反之则反：

```
"##### auto fcitx  ###########
let g:input_toggle = 1
function! Fcitx2en()
   let s:input_status = system("fcitx-remote")
   if s:input_status == 2
      let g:input_toggle = 1
      let l:a = system("fcitx-remote -c")
   endif
endfunction

function! Fcitx2zh()
   let s:input_status = system("fcitx-remote")
   if s:input_status != 2 && g:input_toggle == 1
      let l:a = system("fcitx-remote -o")
      let g:input_toggle = 0
   endif
endfunction

set ttimeoutlen=150
"退出插入模式
autocmd InsertLeave * call Fcitx2en()
"进入插入模式
autocmd InsertEnter * call Fcitx2zh()
"##### auto fcitx end ######

```

**注意:** 由于要调用外部程序，这将明显拖慢会反复进出插入模式的映射。建议改写相关映射，用带 Python 支持的 Vim 加以配合 fcitx.vim 亦可改善效率。

### 剪贴板

[Fcitx 自带剪贴板](https://www.csslayer.info/wordpress/fcitx-dev/fcitx-clipboard/)，其快捷键为 `Ctrl + ;`, 小小功能拯救世界。

### 特殊符号

创建 `~/.config/fcitx/data/pySym.mb`, 文件内容示范如下：

```
 #第一个字符为“#”的行是注释
 #格式：编码 符号
 #编码只能为小写字母，经拼音解析后最长为10(如py为2，pinyin也为2)
 #数学符号
 sxfh ＋
 sxfh －
 sxfh ＜
 sxfh ＝
 sxfh ＞
 sxfh ±
 sxfh ×
 sxfh ÷
 sxfh ∈
 sxfh ∏
 sxfh ∑
 sxfh ∕
 sxfh √
 sxfh ∝

```

直接输入某编码，可以匹配出对应的特殊符号。

**注意:** 编码只能用二十六个小写字母表示；以 v 开头，无效。

### 快速输入

确保在 `~/.config/fcitx/config` 里把 `SemiColonAction` 修改为 `QuickPhrase`.

创建 `~/.config/fcitx/data/QuickPhrase.mb`, 文件内容示范如下：

```
 #第一个字符为“#”的行是注释
 #格式：编码 符号
 #数学符号

 dianhua 123456789
 youbian 123456
 dizhi 中华人民共和国北京市长安街一号
 aowu ┗<(=｀O′=)>┛ 
 mobai ｍ<(＿　＿)>ｍ 
 baobao <(=′▽')爻 (`▽｀=)> 
 baobao <(=*′д｀)爻(′д｀*=)> 
 qiangbi ▄︻┻┳═一…… ☆<(=￣□￣=!)>
 xiaoku 😂
 canyue 🌖
 xuehua ❄

```

按 `;` 并输入编码，可实现快速输入，自然也能用来当 [颜文字库](http://blog.felixc.at/2012/05/kitty-for-fcitx-quickphrase/)和[emoji表情库](https://github.com/levinit/fcitx-emoji)。

**注意:** 编码除了不得有空格，不得以 `;` 开头之外，没有其它限制。

## 故障排除

### 停用或修改 *Extra key for trigger input method*

设置位于 *全局配置* 标签，默认是 *SHIFT*, 也就是说两边的 shift 键都会修改输入法。这个设置可能在输入大写字母的时候引起误触，而且可能会在安装后恢复成默认值。要确保进行的修改没有被覆盖，请设置配置文件为只读：`# chattr +i ~/.config/fcitx/config`.

### 首先诊断问题所在

当你遇到任何 fcitx 有关的问题，比如 ctrl+space 在有的程序中不能工作，首先应该用 `fcitx-diagnose` 命令诊断问题的原因。 `fcitx-diagnose` 会列出所有 fcitx 正常运行所需的前提条件，从输出结果中通常可以找到问题的原因。 在网上（比如在 irc 或者论坛里）询问别人关于 fcitx 配置的问题时，也请首先提供你的 `fcitx-diagnose` 输出结果（比如贴到 pastebin 服务），这将加速别人帮你找到问题所在。

### Emacs 无法使用输入法

当 `LC_CTYPE` 为英文时, 在 Emacs 上可能无法使用输入法。若遇到此情况，请在启动 Emacs 时将 `LC_CTYPE` 设为 `zh_CN.UTF-8`. 终端下并不会遇到此现象，因为输入法会交给终端程序处理。

Emacs 默认 fontset 会使用 "-*-*-*-r-normal--14-*-*-*-*-*-*-*" 字体 (terminus, 75dpi 等等，可以通过 `xlsfonts` 命令查看)，如果您并没有匹配的字体，无法呼出 Fcitx.

### Firefox 右键菜单不弹出

[Firefox](/index.php/Firefox "Firefox") 升级到 13 后可能与 xim 发生冲突，解决办法是确定安装了 [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3) 并且把环境配置文件中的

```
 export GTK_IM_MODULE=xim

```

换成

```
 export GTK_IM_MODULE=fcitx

```

### 在 GTK2 程序中用 `Ctrl + Space` 不能调出输入法

当 `locale` 为英文时，在 GTK+2 程序中有可能无法正常使用 Fcitx，例如 [Chromium (简体中文)](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)") 或 [Firefox (简体中文)](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)") 等。请确认 [fcitx-gtk2](https://www.archlinux.org/packages/?name=fcitx-gtk2) 已安装且已设置 `GTK_IM_MODULE`。

### 在 gnome-terminal中 `Ctrl + Space` 不能调出输入法

使用 GDM 3.16 启动 GNOME，可能在某些程序中无法使用 `Ctrl + Space` 调出输入法。解决方法是修改GSettings配置

```
gsettings set \
  org.gnome.settings-daemon.plugins.xsettings overrides \
  "{'Gtk/IMModule':<'fcitx'>}"

```

### `Ctrl + ;` 会调出 Fcitx 的剪贴板

严格的说，这不是 BUG, Fcitx 的 `Ctrl + ;` 会覆盖很多用户自己的快捷键，特别是 Emacs 用户。有必要时，可以在配置界面中禁用剪贴板插件，或更改其激活快捷键。

### fcitx-sogoupinyin 卡死、联想失败

如果您遇到下列的问题：

*   输入类似「安装」、「暗影」等 "a" 开头的词语，出现卡死的情况。
*   输入并不以拼音 "a" 开头的词语时，却出现「阿拉伯」、「阿里巴巴」等以 "a" 开头的错误联想词语等。

可以通过删除 `~/.config/fcitx/sogou` 下的所有内容的方式解决。

**注意:** 此操作会清空用户词库。

### 在某些程序下输入法总是被切换到美语键盘

比如在 XMind 下，当 Enter 出新结点时，输入法就会被切换到美语键盘，不得不按 Ctrl-Space 以重新切回中文输入法。

启动 Fcitx 的 Config, 在 Global Config 选项卡下的「Share State Among Window」选项里选中「PerProgram」或「All」即可解决。

### Gnome On Wayland 用户无法使用 fcitx

由于 wayland 无法读取 `~/.xprofile` 中的环境变量，所以请在`/etc/environment`中加入：

```
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx

```

或在登录时选择 **运行于 Xorg 的 Gnome** 。

## 参见

*   [Fcitx GitHub](https://github.com/fcitx/fcitx/)
*   [Fcitx Google Code](https://code.google.com/p/fcitx/)
*   [Fcitx Wiki](http://fcitx-im.org/)
*   [Fcitx Themes](http://kde-look.org/index.php?xcontentmode=88)
*   [猫颜文字 For Fcitx QuickPhrase](http://blog.felixc.at/2012/05/kitty-for-fcitx-quickphrase/)
*   [emoji常用表情-fcitx-emoji](https://github.com/levinit/fcitx-emoji)
*   [史前大坑 Fcitx 官方 Artwork 团队出品：Fcitx 输入法皮肤制作全教程](https://forum.suse.org.cn/viewtopic.php?f=16&t=731)
*   [rime 朙(ming)月拼音擴充詞庫](https://bintray.com/rime-aca/dictionaries/luna_pinyin.dict/view/general)
*   [Fcitx not work in terminal, nautilus, gedit](https://bugzilla.gnome.org/show_bug.cgi?id=747825#c6)