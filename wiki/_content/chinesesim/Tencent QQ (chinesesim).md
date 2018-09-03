QQ 是腾讯公司开发的即时通讯软件，为 ICQ 的仿制品，是中国最流行的 IM 软件。本页面列出了 Linux 下使用 QQ 的各种解决方案。

## Contents

*   [1 使用虚拟机](#.E4.BD.BF.E7.94.A8.E8.99.9A.E6.8B.9F.E6.9C.BA)
*   [2 基于 WebQQ](#.E5.9F.BA.E4.BA.8E_WebQQ)
    *   [2.1 SmartQQ](#SmartQQ)
    *   [2.2 官方 Adobe Air 客户端](#.E5.AE.98.E6.96.B9_Adobe_Air_.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.3 PyWebQQ (python-webqq)](#PyWebQQ_.28python-webqq.29)
    *   [2.4 pidgin-lwqq](#pidgin-lwqq)
    *   [2.5 telepathy/empathy-lwqq](#telepathy.2Fempathy-lwqq)
    *   [2.6 gtkqq](#gtkqq)
    *   [2.7 qtqq](#qtqq)
    *   [2.8 weechat-webqq](#weechat-webqq)
    *   [2.9 SmartIM](#SmartIM)
*   [3 独立开发](#.E7.8B.AC.E7.AB.8B.E5.BC.80.E5.8F.91)
    *   [3.1 libqq](#libqq)
*   [4 官方版本](#.E5.AE.98.E6.96.B9.E7.89.88.E6.9C.AC)
*   [5 Wine 模拟](#Wine_.E6.A8.A1.E6.8B.9F)
    *   [5.1 Wine QQ](#Wine_QQ)
    *   [5.2 Wine QQ 轻聊版](#Wine_QQ_.E8.BD.BB.E8.81.8A.E7.89.88)
    *   [5.3 Wine TIM](#Wine_TIM)
        *   [5.3.1 安装前的准备](#.E5.AE.89.E8.A3.85.E5.89.8D.E7.9A.84.E5.87.86.E5.A4.87)
        *   [5.3.2 安装及配置](#.E5.AE.89.E8.A3.85.E5.8F.8A.E9.85.8D.E7.BD.AE)
        *   [5.3.3 相关问题解决](#.E7.9B.B8.E5.85.B3.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [5.4 CrossOver TM2013](#CrossOver_TM2013)
    *   [5.5 Awesome 下的配置](#Awesome_.E4.B8.8B.E7.9A.84.E9.85.8D.E7.BD.AE)
    *   [5.6 i3 下的配置](#i3_.E4.B8.8B.E7.9A.84.E9.85.8D.E7.BD.AE)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 使用虚拟机

简单方便，不用解决各种依赖、字体等问题。这里建议使用 VirtualBox。

1\. 安装[virtualbox](https://www.archlinux.org/packages/?name=virtualbox)，可参看[VirtualBox (简体中文)](/index.php/VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VirtualBox (简体中文)") 。 2\. 下载[Microsoft 提供的正版虚拟机专用系统](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/)(选择 VirtualBox 格式的下载）。

3\. 从虚拟机导入系统（根据使用需求设置虚拟机要使用的 CPU 和内存配置）；

4\. 在虚拟机中的 Windows 系统中安装腾讯 QQ。

技巧：VirtualBox 的**无缝模式**（默认按键 CTRL + L)开启后，虚拟机系统中开启的窗口就如同在宿主机中的原生窗口一样，使用体验大大提升。

## 基于 WebQQ

**警告:** 腾讯将关闭旧版的 WebQQ，并用SmartQQ取而代之, 届时恐怕所有依赖 WebQQ 协议的客户端都将不可用。

### SmartQQ

[SmartQQ](http://w.qq.com/) 是腾讯推出的网页端 QQ，它高度模仿微信风格，功能欠完善，高度依赖网络环境，而且需要通过手机客户端扫描二维码登录。

将 Google Chrome 的把网站做为应用程序与其桌面提醒功能整合，也可以打造一个实用的 QQ 软件：

1.  安装并运行 [Chromium (简体中文)](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)")或者[火狐浏览器firefox](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)")，并打开 [SmartQQ](http://w.qq.com/)，需要手机QQ客户端扫描二维码登陆，功能少。

### 官方 Adobe Air 客户端

**警告:** Adobe Air 的 Linux 版本似乎已经停止开发，且从 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 编译安装时会用到大量 lib32 库，会与 64位 Arch Linux 原有的库发生冲突，不推荐使用

腾讯官方提供的 WebQQ 客户端，基于 Adobe Air 平台。

在 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 安装 [webqq](https://aur.archlinux.org/packages/webqq/) 即可。

### PyWebQQ (python-webqq)

**注意:** 据用户报告，访问速度非常差，不推荐使用

[PyWebQQ（python-webqq）](http://code.google.com/p/python-webqq/)是用 python-webkit 包装而成的 WebQQ 桌面版，均可以访问 Smart QQ 或 WebQQ。由于使用单独的浏览器内核，可以避免长期挂机拖慢浏览器。并且提供了简单的桌面整合，能最小化到托盘，支持消息提醒。

在 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 安装 [python-webqq-svn](https://aur.archlinux.org/packages/python-webqq-svn/) 即可。

### pidgin-lwqq

**警告:** 该作者已经停止对其更新，见（[github页面](https://github.com/xiehuc/pidgin-lwqq) ）。

[pidgin-lwqq](https://github.com/xiehuc/pidgin-lwqq) 是一个 [Pidgin (简体中文)](/index.php/Pidgin_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pidgin (简体中文)") 插件，实现了 WebQQ 协议支持。目前该项目已经停止更新。

### telepathy/empathy-lwqq

telepathy的插件[telepathy-lwqq-git](https://aur.archlinux.org/packages/telepathy-lwqq-git/)，[empathy](https://www.archlinux.org/packages/?name=empathy)（基于telepahty框架）也支持。

### gtkqq

**警告:** 据用户报告，该程序缺失维护长达两年，已不可用

[gtkqq](https://github.com/kernelhcy/gtkqq)是基于 WebQQ 协议的QQ客户端，基于GTK+开发。界面简洁清爽，功能比较完善。但目前还出于开发阶段，易崩溃。

在 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 安装 [gtkqq-git](https://aur.archlinux.org/packages/gtkqq-git/) 即可。

### qtqq

**警告:** 程序无法获取好友列表，暂不可用，作者未回应

用 [qt (简体中文)](/index.php/Qt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Qt (简体中文)") 开发的 qq 客户端，基于 webqq3.0 协议。

在 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 安装 [qtqq-git](https://aur.archlinux.org/packages/qtqq-git/) 即可。

### weechat-webqq

**注意:** 也可选择其它支持IRC协议的聊天客户端

在 [WeeChat](/index.php/WeeChat "WeeChat") 可使用的 QQ 插件脚本，使用 perl语言开发的 [Mojo-Webqq](https://github.com/sjdy521/Mojo-Webqq)库，基于 smartqq 协议 。 源码脚本可访问 [weechat-webqq](https://github.com/wxg4net/weechat-webqq) 获取

### SmartIM

SmartIM 是一个用java写的，包含简单的IM API封装的小程序，支持SmartQQ、微信。不过遗憾的是仍然需要扫描二维码。

不支持图片，视频，表情和语音，不过支持依赖第三方服务器的文件传输。

使用方法：只需将jar包下载下来，然后安装java-openjdk之后，就可以在终端通过“java -jar”的方式直接运行了。

Github 地址： [Jamling/SmartIM](https://github.com/Jamling/SmartIM)。

## 独立开发

### libqq

[libqq](http://code.google.com/p/libqq-pidgin/)是 Pidgin 下的QQ协议插件，采用2010版协议改写。目前已比较稳定，但开发貌似停滞不前。

AUR：[libqq-svn](https://aur.archlinux.org/packages/libqq-svn/)、[libqq-pidgin-svn](https://aur.archlinux.org/packages/libqq-pidgin-svn/)（貌似一样）

**优点**：基于功能强大的Pidgin，无需安装第三方软件，桌面整合好，节省资源。
**缺点**：仍有稳定性问题。

## 官方版本

**警告:** QQ for Linux 已经无法使用。请勿尝试此方案。

腾讯在 2008 年底发布了 QQ for Linux 1.0 Preview 3

## Wine 模拟

[Wine (简体中文)](/index.php/Wine_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wine (简体中文)") 是类 UNIX 系统下运行微软 Windows 程序的"兼容层"，可以用它模拟 Windows 环境来运行 QQ/TM。

**警告:** Wine QQ/TM 在平铺式窗口管理器下的样式可能会大规模失控，需要进行额外的配置

### Wine QQ

目前较为成熟的 Wine 模拟方案为[deepin-qq-im](https://aur.archlinux.org/packages/deepin-qq-im/)，也可以从 [ArchLinux CN 源](https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror/) 安装 deepin-qq-im。

**警告:** 受 wine 上游的一个[Bug](https://bugs.winehq.org/show_bug.cgi?id=45199) 影响，官方仓库中提供的[wine](https://www.archlinux.org/packages/?name=wine)自3.8开始无法运行许多程序，包括 QQ 和 TIM。截止3.15-1版本此问题仍未修复。您可以将[wine](https://www.archlinux.org/packages/?name=wine)[降级](/index.php/Downgrading_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Downgrading packages (简体中文)")到3.7来绕过这个问题。也可以按照[FS#58833](https://bugs.archlinux.org/task/58833)二楼的方法，使用[ABS](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")修改编译参数之后重新编译安装[wine](https://www.archlinux.org/packages/?name=wine)。

之前比较好的解决方案有 [清风老师](http://phpcj.org/wineqq/) 提供的 Wine QQ 方案等。

**注意:**

*   如果系统默认不是中文环境可能无法输入中文,解决方法是修改启动文件的`Exec`:

 `$HOME/.local/share/applications/wine-QQ.desktop`  `Exec=env LC_ALL=zh_CN.UTF-8 wine ".wine/drive_c/Program Files/QQ/Bin/QQ.exe"` 

*   此方案只需要安装[wine](https://www.archlinux.org/packages/?name=wine)即可，安装其它的 Wine 库可能造成干扰。第一次启动的时候会自动下载安装`Mono`库。如果安装失败，可以首先删除`$HOME/.wine`并卸载所有 Wine 相关的包后重启系统，得到一个相对干净的环境再尝试按上面博客的步骤进行安装。

*   安装成功之后要取消勾选 QQ 的自动更新，以免自动更新导致不可用。

### Wine QQ 轻聊版

**注意:** 此方案使用QQ轻聊版6.7，更高版本在当前wine版本需要[额外的调整](https://blog.lilydjwg.me/2015/10/26/run-tencent-qq-lite-with-wine.186640.html)才能安装

安装[winetricks](https://www.archlinux.org/packages/?name=winetricks)、[wine](https://www.archlinux.org/packages/?name=wine)。创建 qqlight.verb 如下，

```
w_metadata qqlight apps \
 title="QQ Light" \
 publisher="Tencent" \
 year="2015" \
 media="download" \
 file1="QQ6.7Light.exe" \
 installed_exe1="$W_PROGRAMS_X86_WIN/Tencent/QQ/Bin/QQ.exe" \
 homepage="[http://www.qq.com](http://www.qq.com)" \
 unattended="no"

load_qqlight()
{
    w_download [http://dldir1.qq.com/qqfile/qq/QQ6.7Light/13466/QQ6.7Light.exe](http://dldir1.qq.com/qqfile/qq/QQ6.7Light/13466/QQ6.7Light.exe) e1e1ff2bf6461c08047d0a01927a43c5a0746bdf

    if w_workaround_wine_bug 29636 "Installing native riched20 to work around crash bug"
    then
        w_call riched20
    fi

    if w_workaround_wine_bug 34566 "Installing native ctf to work around crash"
    then
        w_call msctf
    fi

    # Make sure chinese fonts are available
    w_call fakechinese

    # uses mfc42u.dll
    w_call mfc42

    cd "$W_CACHE/$W_PACKAGE"
    w_try "$WINE" "$file1"

    # fix crash after login
    mkdir -p ~/.local/share/wineprefixes/qqlight/drive_c/users/$LOGNAME/Application\ Data/Tencent/QQ/Misc/com.tencent.wireless/SDK
    chmod 000 ~/.local/share/wineprefixes/qqlight/drive_c/users/$LOGNAME/Application\ Data/Tencent/QQ/Misc/com.tencent.wireless/SDK

    w_declare_exe "$W_PROGRAMS_X86_WIN\\Tencent\\QQ\\Bin" QQ.exe
}

```

运行 winetricks 安装，

```
$ winetricks qqlight.verb

```

安装完成后通过 wineconsole 启动，

```
$ wineconsole .wine/drive_c/run-qqlight.bat

```

### Wine TIM

[TIM](http://im.qq.com/download/)是腾讯推出的主打办公协同的QQ版本。

**警告:** 受 wine 上游的一个[Bug](https://bugs.winehq.org/show_bug.cgi?id=45199) 影响，官方仓库中提供的[wine](https://www.archlinux.org/packages/?name=wine)自3.8开始无法运行许多程序，包括 QQ 和 TIM。截止3.15-1版本此问题仍未修复。您可以将[wine](https://www.archlinux.org/packages/?name=wine)[降级](/index.php/Downgrading_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Downgrading packages (简体中文)")到3.7来绕过这个问题。也可以按照[FS#58833](https://bugs.archlinux.org/task/58833)二楼的方法，使用[ABS](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")修改编译参数之后重新编译安装[wine](https://www.archlinux.org/packages/?name=wine)。

同时，在 AUR 中，仍有已经稳定成熟的模拟方案：[deepin-wine-tim](https://aur.archlinux.org/packages/deepin-wine-tim/)。当然，你也可以选择按下文的方法手动安装配置。

#### 安装前的准备

**提示：** 如果使用crossover内建的TIM可忽略该准备步骤。

可参考[Wine (简体中文)](/index.php/Wine_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wine (简体中文)")

*   安装[wine](https://www.archlinux.org/packages/?name=wine)、[wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) 和 [wine-mono](https://www.archlinux.org/packages/?name=wine-mono)

```
$ pacman -S wine wine_gecko wine-mono winetricks

```

*   使用内建函数库

打开winecfg，在函数库一项中的“新增函数库顶替”中选择添加riched20，也可也执行以下命令添加：

```
$ winetricks riched20

```

*   中文字体显示

可以提供windows字体[Font configuration#Applications without fontconfig support](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration")或使用linux的字体，方法如下：

**警告:** 经测试，使用文泉驿和思源黑体，均出现部分位置文字内容无法显示的情况（但影响很小）

**提示：** 默认显示dpi为96,可能使文字显示毛躁不清，可在winecfg的“显示”选项卡中将dpi适当调高（例如缩放125%则为120，缩放150%则为144）。

新建一个reg文件，例如名为wine-fonts.reg，写入如下内容：

```
REGEDIT4
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\FontLink\SystemLink]
"Lucida Sans Unicode"="wqy-microhei.ttc"
"Microsoft Sans Serif"="wqy-microhei.ttc"
"Microsoft YaHei"="wqy-microhei.ttc"
"MS Sans Serif"="wqy-microhei.ttc"
"Tahoma"="wqy-microhei.ttc" 
"Tahoma Bold"="wqy-microhei.ttc"
"SimSun"="wqy-microhei.ttc"
"Arial"="wqy-microhei.ttc"
"Arial Black"="wqy-microhei.ttc"
"宋体"="wqy-microhei.ttc"
"新細明體"="wqy-microhei.ttc"

```

保存后运行：

```
 $ wine regedit

```

打开regedit图形界面，点击注册表-导入注册表文件，然后选择wine-fonts.reg即可。

#### 安装及配置

*   安装tim

使用wine安装tim。可以使用右键菜单中的“运行程”序运行tim的exe文件进行安装，也可以使用命令行：

```
 $ wine tim.exe

```

*   增加启动菜单项

安装的tim可能没有在程序列表中生成图标。自行添加图标，新建一个名为tim.desktop的文件，写入以下内容：

```
 [Desktop Entry]
 Encoding=UTF-8
 Version=1
 Name=TIM
 Comment=Tencent TIM
 Exec=wine '~/.wine/drive_c/Program Files/Tencent/TIM/Bin/TIM.exe'
 Icon=~/.wine/drive_c/Program Files/Tencent/TIM/TIMUninst.ico
 Terminal=false
 Type=Application
 Categories=Network;

```

其中comment是程序介绍，Exec是执行命令，Icon是要显示的图表，可以根据实际情况进行修改。（自带的ico图表不太清晰，可下载[该图标文件](https://sqimg.qq.com/qq_product_operations/eim/site/img/share.png)更换） 将tim.desktop移动到~/.local/share/applications或/usr/share/applications文件夹下即可。

**注意:** desktop entry 有时无法使用，需要将里面的相对路径改成绝对路径。

#### 相关问题解决

*   文件被占用

打开进程管理器，杀死 TIM.exe 进程即可。 原因是退出tim后，某些相关进程仍然在后台运行。也可以使用如下脚本来启动 TIM，它会首先查找已有的 TIM.exe 进程，杀死该进程后启动新的 TIM：

 `start-tim.sh` 
```
#!/bin/sh
# script to start TIM
# kill TIM before start TIM
for pid in `pgrep TIM.exe`; do
	if [ -n ${pid} ]; then
		kill ${pid}
	fi
done
# start TIM
wine '~/.wine/drive_c/Program Files/Tencent/TIM/Bin/TIM.exe'

```

然后将上文中的 tim.desktop 中的 `Exec` 的值改为 `start-tim.sh` 即可．

*   xfce4(xfwm4)下无法输入表情

打开设置管理器-窗口管理器微调-焦点，取消勾选激活焦点防窃取和遵照标准的ICCCM焦点提示即可。 原因是表情窗口获取焦点时会发生不兼容现象。

*   wine-3.8与wine-3.9版本出现无法加载gdi32.dll错误

Archlinux打包的wine-3.8与wine-3.9.1版本会出现无法加载gdi32.dll的错误，可以使用命令“sudo pacman -U /var/cache/pacman/pkg/wine-3.7-1-x86_64.pkg.tar.xz”将wine降级到之前的3.7版本解决。为了避免被升级到新3.9版本，可以编辑"/etc/pacman.conf"文档，去掉"IgnorePkg"一行前面的"#"号，并在该行"="号后面添加"wine"；在后续更新中该问题得到解决后，记得去掉wine，以便更新之。

### CrossOver TM2013

关于 [CrossOver](/index.php/CrossOver "CrossOver") 版本的 TM2013 相关信息参见[此处](http://www.codeweavers.com/support/forums/general/?t=37;msg=151682)。除了更加稳定之外，和自行 Wine 的版本没有明显区别。

### Awesome 下的配置

Wine QQ/TM 在平铺式窗口管理器下可能不太听话。以下是一些 [Awesome (简体中文)](/index.php/Awesome_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Awesome (简体中文)") 配置，其作用为：

*   将所有 TM 的窗口设置为浮动
*   清除不需要的窗口边框、避免菜单弹出时焦点移动到菜单上
*   在使用标签式会话窗口时，增加[使用 Alt+数字来切换标签页](https://blog.lilydjwg.me/2013/11/15/switch-tabs-with-alt-num-in-wined-tm-exe-in-awesome.41729.html)的快捷键（需要安装 [xdotool](/index.php?title=Xdotool&action=edit&redlink=1 "Xdotool (page does not exist)")）
*   自动关闭弹出的新闻窗口

```
function myfocus_filter(c)
  if awful.client.focus.filter(c) then
    -- This works with tooltips and some popup-menus
    if c.class == 'Wine' and c.above == true then
      return nil
    elseif c.class == 'Wine'
      and c.type == 'dialog'
      and c.skip_taskbar == true
      and c.size_hints.max_width and c.size_hints.max_width < 160
      then
      -- for popup item menus of Photoshop CS5
      return nil
    else
      return c
    end
  end
end

awful.rules.rules = {
  -- All clients will match this rule.
  {
    rule = { },
    properties = {
      -- 这里使用我们自己的函数
      focus = myfocus_filter,
      -- 以下是默认的部分
      border_width = beautiful.border_width,
      border_color = beautiful.border_normal,
      keys = clientkeys,
      buttons = clientbuttons,
    }
  }, {
    rule_any = { 
      instance = {'TM.exe', 'QQ.exe'},
    },
    properties = {
      -- This, together with myfocus_filter, make the popup menus flicker taskbars less
      -- Non-focusable menus may cause TM2013preview1 to not highlight menu
      -- items on hover and crash.
      focusable = true,
      floating = true,
      -- 去掉边框
      border_width = 0,
    }
  }, {
    -- 其它规则
  }
}

alt_switch_keys = awful.util.table.join(
    -- it's easier for a vimer to manage this than figuring out a nice way to loop and concat
    awful.key({'Mod1'}, 1, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+1') end),
    awful.key({'Mod1'}, 2, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+2') end),
    awful.key({'Mod1'}, 3, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+3') end),
    awful.key({'Mod1'}, 4, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+4') end),
    awful.key({'Mod1'}, 5, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+5') end),
    awful.key({'Mod1'}, 6, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+6') end),
    awful.key({'Mod1'}, 7, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+7') end),
    awful.key({'Mod1'}, 8, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+8') end),
    awful.key({'Mod1'}, 9, function(c) awful.util.spawn('xdotool key --window ' .. c.window .. ' ctrl+9') end)
)
function bind_alt_switch_tab_keys(client)
    client:keys(awful.util.table.join(client:keys(), alt_switch_keys))
end -- }}}

client.connect_signal("manage", function (c, startup)
  -- 其它配置

  if c.instance == 'TM.exe' then
    -- 添加 Alt+n 支持
    bind_alt_switch_tab_keys(c)
    -- 关闭各类新闻通知小窗口
    if c.name and c.name:match('^腾讯') and c.above then
      c:kill()
    end
  end

  -- 其它配置
end)

```

[一个完整的 Awesome 配置](https://github.com/lilydjwg/myawesomerc)。

### i3 下的配置

原生配置下，启动 `qq2012` 时会自动最大化，且边框不美观，可在 [i3 (简体中文)](/index.php/I3_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "I3 (简体中文)") 的 `config` 设置如下两条规则以改善：

```
for_window [instance="QQ.exe"] floating enable
for_window [instance="QQ.exe"] border none

```

## 参阅

*   [openSUSE wiki 的 QQ 条目](https://zh.opensuse.org/SDB:QQ)
*   [Web 端的 QQ 群空间](http://qun.qzone.qq.com/) 当所使用 QQ 客户端不支持群空间时，可以此用该服务代替。
*   [IM QQ-QQ 手机版](http://im.qq.com/mobileqq/) 移动端也未尝不也是一种代替方案。
*   [hillwoodroc/winetricks-zh](https://github.com/hillwoodroc/winetricks-zh) hillwoodroc/winetricks-zh
*   [Wine QQ “杂交版”](http://tieba.baidu.com/p/4814636033) huixingjihua@tieba 制作的Wine QQ国际版 2012