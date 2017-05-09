QQ 是腾讯公司开发的即时通讯软件，为 ICQ 的仿制品，是中国最流行的 IM 软件。本页面列出了 Linux 下使用 QQ 的各种解决方案。

## Contents

*   [1 基于 WebQQ](#.E5.9F.BA.E4.BA.8E_WebQQ)
    *   [1.1 SmartQQ](#SmartQQ)
    *   [1.2 官方 Adobe Air 客户端](#.E5.AE.98.E6.96.B9_Adobe_Air_.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [1.3 PyWebQQ (python-webqq)](#PyWebQQ_.28python-webqq.29)
    *   [1.4 pidgin-lwqq](#pidgin-lwqq)
    *   [1.5 telepathy/empathy-lwqq](#telepathy.2Fempathy-lwqq)
    *   [1.6 gtkqq](#gtkqq)
    *   [1.7 qtqq](#qtqq)
    *   [1.8 weechat-webqq](#weechat-webqq)
*   [2 独立开发](#.E7.8B.AC.E7.AB.8B.E5.BC.80.E5.8F.91)
    *   [2.1 libqq](#libqq)
*   [3 官方版本](#.E5.AE.98.E6.96.B9.E7.89.88.E6.9C.AC)
*   [4 Wine 模拟](#Wine_.E6.A8.A1.E6.8B.9F)
    *   [4.1 Wine QQ](#Wine_QQ)
    *   [4.2 Wine QQ 轻聊版](#Wine_QQ_.E8.BD.BB.E8.81.8A.E7.89.88)
    *   [4.3 Wine TM](#Wine_TM)
    *   [4.4 CrossOver TM2013](#CrossOver_TM2013)
    *   [4.5 Awesome 下的配置](#Awesome_.E4.B8.8B.E7.9A.84.E9.85.8D.E7.BD.AE)
    *   [4.6 i3 下的配置](#i3_.E4.B8.8B.E7.9A.84.E9.85.8D.E7.BD.AE)
*   [5 参阅](#.E5.8F.82.E9.98.85)

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

## 独立开发

### libqq

[libqq](http://code.google.com/p/libqq-pidgin/)是 Pidgin 下的QQ协议插件，采用2010版协议改写。目前已比较稳定，但开发貌似停滞不前。

AUR：[libqq-svn](https://aur.archlinux.org/packages/libqq-svn/)、[libqq-pidgin-svn](https://aur.archlinux.org/packages/libqq-pidgin-svn/)（貌似一样）

**优点**：基于功能强大的Pidgin，无需安装第三方软件，桌面整合好，节省资源。
**缺点**：仍有稳定性问题。

## 官方版本

**警告:** QQ for Linux 已经无法使用。请勿尝试此方案。

腾讯在 2008 年底发布了 QQ for Linux 1.0 Preview 3，功能如下：

1.  支持和好友传送文件
2.  支持和好友/群发送图片
3.  支持群里截屏并传送截图
4.  聊天设置中，已经可以设定按回车键发送

## Wine 模拟

[Wine (简体中文)](/index.php/Wine_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wine (简体中文)") 是类 UNIX 系统下运行微软 Windows 程序的"兼容层"，可以用它模拟 Windows 环境来运行 QQ/TM。

**警告:** Wine QQ/TM 在平铺式窗口管理器下的样式可能会大规模失控，需要进行额外的配置

### Wine QQ

目前较为成熟的 Wine 模拟方案为[deepinwine-qq](https://aur.archlinux.org/packages/deepinwine-qq/)。

之前比较好的解决方案有 [清风老师](http://phpcj.org/wineqq/) 提供的 Wine QQ 方案等。

**注意:** 如果系统默认不是中文环境可能无法输入中文,解决方法是修改启动文件的`Exec`: `$HOME/.local/share/applications/wine-QQ.desktop`  `Exec=env LC_ALL=zh_CN.UTF-8 wine ".wine/drive_c/Program Files/QQ/Bin/QQ.exe"` 

**注意:** 此方案只需要安装[wine](https://www.archlinux.org/packages/?name=wine)即可，安装其它的Wine库可能造成干扰。第一次启动的时候会自动下载安装`Mono`库。如果安装失败，可以首先删除`$HOME/.wine`并卸载所有Wine相关的包后重启系统，得到一个相对干净的环境再尝试按上面博客的步骤进行安装

### Wine QQ 轻聊版

**注意:** 此方案使用QQ轻聊版6.7，更高版本在当前wine版本需要[额外的调整](http://blog.lilydjwg.me/2015/10/26/run-tencent-qq-lite-with-wine.186640.html)才能安装

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

### Wine TM

对于仍然能用的 TM 版本（TM2009Beta3.4、TM2013preview1），使用[以下方案](http://blog.lilydjwg.me/2013/3/24/run-tencent-messenger-with-wine.38382.html)可以成功：

```
$ winetricks riched20 ie6 mfc42

```

然后运行 winecfg，切换到「函数库」选项卡，在「已有的函数库顶替」中编辑「urlmon.dll」项，设置其使用「内建」版本。

将 ie6 替换成 ie7 亦可。可能需要安装相关字体支持，比如安装 simsun.ttc 字体。

在 Wine 1.7.6 之后，**登录后片刻状态自动变成离开的问题已经修复**。但是此离开状态检测是在 Wine 环境内部的（和全局快捷键一样），也就是如果没有用户操作传递给此 Wine 环境中的任意程序，**即使用户在 Linux 上做其它事情，在指定时间之后 TM 仍然会转变成离开状态**。因此建议在「在线状态」设置中禁用自动将状态切换为「离开」的功能。

已知可以正常使用的功能：

*   基本聊天
*   截图、粘贴剪贴板中的图像
*   文件传输
*   群共享
*   远程协助（作为求助方和协助方均可）

已知问题：

*   GIF 动画显示不正常
*   输入法光标跟随无效。输入法的提示窗口总是位于输入框下方
*   截图仅能截取一个屏幕，在双显示器时会有问题。快捷键仅在 Wine 程序拥有焦点时可以工作
*   偶尔可能会假死或者崩溃（在 CrossOver 版本中非常少见）
*   在 [Awesome](/index.php/Awesome "Awesome") 下（特别是双显示器的扩展屏上时），鼠标拖动窗口上边缘可能导致窗口乱跑
*   安装界面部分文本在点击后、鼠标经过时变为白色
*   托盘右键菜单弹出后，点击 Wine 之外的程序它并不会自动消失

Wine TM2013 的 Wine 环境大小为 227.8MiB，[7z](/index.php/P7zip "P7zip") 压缩后为 67.1MiB。

### CrossOver TM2013

关于 [CrossOver](/index.php/CrossOver "CrossOver") 版本的 TM2013 相关信息参见[此处](http://www.codeweavers.com/support/forums/general/?t=37;msg=151682)。除了更加稳定之外，和自行 Wine 的版本没有明显区别。

### Awesome 下的配置

Wine QQ/TM 在平铺式窗口管理器下可能不太听话。以下是一些 [Awesome (简体中文)](/index.php/Awesome_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Awesome (简体中文)") 配置，其作用为：

*   将所有 TM 的窗口设置为浮动
*   清除不需要的窗口边框、避免菜单弹出时焦点移动到菜单上
*   在使用标签式会话窗口时，增加[使用 Alt+数字来切换标签页](http://blog.lilydjwg.me/2013/11/15/switch-tabs-with-alt-num-in-wined-tm-exe-in-awesome.41729.html)的快捷键（需要安装 [xdotool](/index.php?title=Xdotool&action=edit&redlink=1 "Xdotool (page does not exist)")）
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