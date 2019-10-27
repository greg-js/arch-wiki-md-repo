QQ 是腾讯公司开发的即时通讯软件，为 ICQ 的仿制品，是中国最流行的 IM 软件。本页面列出了 Linux 下使用 QQ 的各种解决方案。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 虚拟机](#虚拟机)
*   [2 Wine](#Wine)
    *   [2.1 Deepin QQ/TIM](#Deepin_QQ/TIM)
    *   [2.2 Crossover](#Crossover)
    *   [2.3 AppImage](#AppImage)
    *   [2.4 清风老师的 Wine QQ 方案](#清风老师的_Wine_QQ_方案)
    *   [2.5 手动 Wine 方案](#手动_Wine_方案)
        *   [2.5.1 QQ 轻聊版](#QQ_轻聊版)
        *   [2.5.2 TIM](#TIM)
*   [3 官网版本](#官网版本)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 HiDPI 支持](#HiDPI_支持)
    *   [4.2 平铺式窗口管理器下的配置](#平铺式窗口管理器下的配置)
        *   [4.2.1 Awesome](#Awesome)
        *   [4.2.2 i3](#i3)
*   [5 疑难解答](#疑难解答)
    *   [5.1 字体配置](#字体配置)
    *   [5.2 文件被占用](#文件被占用)
    *   [5.3 xfce4(xfwm4)下无法输入表情](#xfce4(xfwm4)下无法输入表情)
    *   [5.4 在非中文 locale 下无法输入中文](#在非中文_locale_下无法输入中文)
*   [6 参阅](#参阅)

## 虚拟机

您可以在虚拟机中运行一个完整的 Windows 系统，并在此中运行 QQ。相比于其他的方案，这种方案出错的几率是最小的，缺点是占用的资源较多。

一般使用 [VirtualBox](/index.php/VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VirtualBox (简体中文)") 即可满足需求，也可以参考 [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors") 选择其它的虚拟机程序。

**提示：**

*   根据[许可条款](https://www.microsoft.com/en-us/Useterms/OEM/Windows/10Mobile/UseTerms_OEM_Windows_10Mobile_ChineseSimplified.htm)，在每个虚拟设备上运行 Windows 都需要单独的授权。但您可以选择使用[微软提供的虚拟机专用系统](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/)(免费使用）。
*   如果您使用 VirtualBox，建议您开启**[无缝模式](https://www.virtualbox.org/manual/ch04.html#seamlesswindows)**，这个功能能让您在宿主机的桌面下无缝操作虚拟机中的窗口。

## Wine

[Wine](/index.php/Wine_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wine (简体中文)") 是类 UNIX 系统下运行微软 Windows 程序的"兼容层"，可以用它模拟 Windows 环境来运行 QQ/TIM。

**警告:** Wine QQ/TIM 在平铺式窗口管理器下的样式可能会大规模失控，需要进行[额外的配置](#平铺式窗口管理器下的配置)。

### Deepin QQ/TIM

Deepin QQ/TIM 是 wine 中相对成熟的方案。几乎开箱即用，bug 较少。

您可以安装[deepin-qq-im](https://aur.archlinux.org/packages/deepin-qq-im/)或[deepin-wine-tim](https://aur.archlinux.org/packages/deepin-wine-tim/)，也可以从 [ArchLinux CN 源](https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror/) 安装deepin.com.qq.office或者deepin.com.qq.im。

如果是Arch系KDE/Plasma桌面，请[按照这个教程](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#程序自启动/ "KDE (简体中文)")，先安装gnome-settings-daemon，然后将/usr/lib/gsd-xsettings设置为自动启动

### Crossover

可以使用 [CrossOver](/index.php/CrossOver "CrossOver") 运行 QQ、TM2013 和 TIM。更多详情可以参阅[CrossOver的兼容性列表](https://www.codeweavers.com/compatibility)。

### AppImage

AppImage 是一种把应用打包成单一文件的格式。您可以在[[1]](https://github.com/askme765cs/Wine-QQ-TIM)下载到封装好的 Wine QQ/TIM。只需要赋予可执行权限即可使用。由于 AppImage 格式附带了程序所需要的依赖，所以这种方式受系统中其他组件版本的影响最小。

**注意:** 由于 AppImage 不使用系统的 Wine，所以对 Wine 的调整可能无效，例如[#HiDPI 支持](#HiDPI_支持)。

### 清风老师的 Wine QQ 方案

您也可以使用[清风老师](http://phpcj.org/wineqq/) 提供的 Wine QQ 方案。

**注意:** 安装成功之后要取消勾选 QQ 的自动更新，以免自动更新导致不可用。

### 手动 Wine 方案

#### QQ 轻聊版

**注意:** 此方案使用QQ轻聊版6.7，更高版本在当前wine版本需要[额外的调整](https://blog.lilydjwg.me/2015/10/26/run-tencent-qq-lite-with-wine.186640.html)才能安装。

安装[winetricks](https://www.archlinux.org/packages/?name=winetricks)、[wine](https://www.archlinux.org/packages/?name=wine)。创建 qqlight.verb 如下：

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

运行 winetricks 安装：

```
$ winetricks qqlight.verb

```

安装完成后通过 wineconsole 启动：

```
$ wineconsole .wine/drive_c/run-qqlight.bat

```

#### TIM

1.  安装[wine](https://www.archlinux.org/packages/?name=wine)、[wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) 和 [wine-mono](https://www.archlinux.org/packages/?name=wine-mono)。
2.  执行`winetricks riched20`，也可使用 `winecfg` 设置函数库顶替。
3.  中文字体显示见[#字体配置](#字体配置)。
4.  安装 TIM。

**提示：** 安装的tim可能没有在程序列表中生成图标。若要自行添加图标，新建一个名为tim.desktop的文件，写入以下内容： `tim.desktop` 
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
将 `tim.desktop` 移动到`~/.local/share/applications`或`/usr/share/applications`文件夹下即可。

## 官网版本

1.  在2019年10月24日这个特殊的日子，Linux QQ全新回归，从心出发·趣无止境
2.  下载安装请查看官网

## 提示与技巧

### HiDPI 支持

在 HiDPI 显示器上，QQ/TIM 的界面可能会过小。在较新版本的 QQ/TIM 中已经加入了对 HiDPI 的支持。只需手动调整 Wine 的 DPI 即可。

执行 `winecfg`，在打开的窗口中切换到**显示**选项卡并调整 DPI。

**注意:** 如果您使用的不是默认的 Wine 容器（例如使用了deepin QQ/TIM），那么需要在执行 `winecfg` 时指定`WINEPREFIX` 变量。例如`env WINEPREFIX=$HOME/.deepinwine/Deepin-QQ winecfg` 或是 `env WINEPREFIX=$HOME/.deepinwine/Deepin-TIM winecfg`。

### 平铺式窗口管理器下的配置

#### Awesome

Wine QQ/TM 在平铺式窗口管理器下可能不太听话。以下是一些 [Awesome](/index.php/Awesome_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Awesome (简体中文)") 配置，其作用为：

*   将所有 TM 的窗口设置为浮动
*   清除不需要的窗口边框、避免菜单弹出时焦点移动到菜单上
*   在使用标签式会话窗口时，增加[使用 Alt+数字来切换标签页](https://blog.lilydjwg.me/2013/11/15/switch-tabs-with-alt-num-in-wined-tm-exe-in-awesome.41729.html)的快捷键（需要安装 [xdotool](/index.php/Xdotool "Xdotool")）
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

#### i3

原生配置下，启动 `qq2012` 时会自动最大化，且边框不美观，可在 [i3](/index.php/I3 "I3") 的 `config` 设置如下两条规则以改善：

```
for_window [instance="QQ.exe"] floating enable
for_window [instance="QQ.exe"] border none

```

## 疑难解答

### 字体配置

如果中文的显示遇到问题，可以尝试先执行`winetricks fakechinese`。

另请参阅 [Wine#Fonts](/index.php/Wine#Fonts "Wine") 和 [Font configuration#Applications without fontconfig support](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration")。

### 文件被占用

杀死 QQ 或 TIM 的进程即可。 在退出 QQ/TIM 之后，某些相关进程仍然在后台运行。也可以使用如下脚本来启动 QQ/TIM，它会首先查找已有的进程，杀死该进程后启动新的 QQ/TIM。

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

上面的例子适用于 TIM，稍作修改之后即可应用于 QQ。

### xfce4(xfwm4)下无法输入表情

打开设置管理器-窗口管理器微调-焦点，取消勾选激活焦点防窃取和遵照标准的ICCCM焦点提示即可。

原因是表情窗口获取焦点时会发生不兼容现象。

### 在非中文 locale 下无法输入中文

修改 `.desktop` 文件的 `Exec`，这个文件一般位于 `/usr/share/applications/` 或者 `~/.local/share/applications/`。

在 `Exec` 行中加入 `env LC_ALL=zh_CN.UTF-8`。 例如，原来的 `Exec` 为：

```
Exec=".wine/drive_c/Program Files/QQ/Bin/QQ.exe"

```

则应改为：

```
Exec=env LC_ALL=zh_CN.UTF-8 wine ".wine/drive_c/Program Files/QQ/Bin/QQ.exe"

```

## 参阅

*   [openSUSE wiki 的 QQ 条目](https://zh.opensuse.org/SDB:QQ)
*   [Web 端的 QQ 群空间](http://qun.qzone.qq.com/) 当所使用 QQ 客户端不支持群空间时，可以此用该服务代替。
*   [IM QQ-QQ 手机版](http://im.qq.com/mobileqq/) 移动端也未尝不也是一种代替方案。
*   [hillwoodroc/winetricks-zh](https://github.com/hillwoodroc/winetricks-zh) hillwoodroc/winetricks-zh
*   [Wine QQ “杂交版”](http://tieba.baidu.com/p/4814636033) huixingjihua@tieba 制作的Wine QQ国际版 2012