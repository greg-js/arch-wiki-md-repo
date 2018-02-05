这是对主文 [Openbox](/index.php/Openbox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Openbox (简体中文)") 的补充. 这篇文章涉及定制 Openbox 的外观. 有帮助的软件例如面板,托盘也有说明.

## Contents

*   [1 主题和外观](#.E4.B8.BB.E9.A2.98.E5.92.8C.E5.A4.96.E8.A7.82)
    *   [1.1 Openbox 主题](#Openbox_.E4.B8.BB.E9.A2.98)
    *   [1.2 X11 鼠标光标](#X11_.E9.BC.A0.E6.A0.87.E5.85.89.E6.A0.87)
    *   [1.3 GTK 主题](#GTK_.E4.B8.BB.E9.A2.98)
    *   [1.4 桌面图标](#.E6.A1.8C.E9.9D.A2.E5.9B.BE.E6.A0.87)
    *   [1.5 桌面壁纸](#.E6.A1.8C.E9.9D.A2.E5.A3.81.E7.BA.B8)
*   [2 推荐的程序软件](#.E6.8E.A8.E8.8D.90.E7.9A.84.E7.A8.8B.E5.BA.8F.E8.BD.AF.E4.BB.B6)
    *   [2.1 登录管理器](#.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.2 混合桌面视图](#.E6.B7.B7.E5.90.88.E6.A1.8C.E9.9D.A2.E8.A7.86.E5.9B.BE)
    *   [2.3 面板,托盘,页调度程序](#.E9.9D.A2.E6.9D.BF.2C.E6.89.98.E7.9B.98.2C.E9.A1.B5.E8.B0.83.E5.BA.A6.E7.A8.8B.E5.BA.8F)
        *   [2.3.1 面板](#.E9.9D.A2.E6.9D.BF)
        *   [2.3.2 托盘](#.E6.89.98.E7.9B.98)
        *   [2.3.3 页调度程序](#.E9.A1.B5.E8.B0.83.E5.BA.A6.E7.A8.8B.E5.BA.8F)
    *   [2.4 文件管理器](#.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.5 应用程序启动器](#.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E5.90.AF.E5.8A.A8.E5.99.A8)
        *   [2.5.1 Dmenu](#Dmenu)
        *   [2.5.2 Gmrun](#Gmrun)
        *   [2.5.3 Bashrun2](#Bashrun2)
        *   [2.5.4 Kupfer](#Kupfer)
        *   [2.5.5 Launchy](#Launchy)
        *   [2.5.6 LXPanel](#LXPanel)
        *   [2.5.7 Gnome-panel](#Gnome-panel)
    *   [2.6 剪贴板管理器](#.E5.89.AA.E8.B4.B4.E6.9D.BF.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.7 音量管理器](#.E9.9F.B3.E9.87.8F.E7.AE.A1.E7.90.86.E5.99.A8)
        *   [2.7.1 Gvolwheel, gvtray](#Gvolwheel.2C_gvtray)
        *   [2.7.2 Obmixer](#Obmixer)
        *   [2.7.3 Volti](#Volti)
        *   [2.7.4 Volumeicon, volwheel](#Volumeicon.2C_volwheel)
    *   [2.8 电池 & CPU](#.E7.94.B5.E6.B1.A0_.26_CPU)
        *   [2.8.1 Trayfreq](#Trayfreq)
    *   [2.9 键盘布局转换器](#.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80.E8.BD.AC.E6.8D.A2.E5.99.A8)
        *   [2.9.1 Fbxkb, xxkb, axkb](#Fbxkb.2C_xxkb.2C_axkb)
        *   [2.9.2 xneur](#xneur)
    *   [2.10 注销对话框](#.E6.B3.A8.E9.94.80.E5.AF.B9.E8.AF.9D.E6.A1.86)

## 主题和外观

除了 Openbox 主题标题外, 其它段落都是为那些把 Openbox 配置为单独的桌面而不和 GNOME, KDE , Xfce 混用的人而写的.

### Openbox 主题

Openbox主题控制了窗口边框的外观 , 包括标题和标题上的按钮. 也决定了程序菜单的外观和屏幕显示(OSD).

额外的主题可以从标准库得到:

```
# pacman -S openbox-themes

```

这个包不是决定性的. 你也可以从其它网站下载,例如:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

下载的主题可以解压到 <tt>~/.themes</tt> 然后用 ObConf 安装或选用.

新建主题非常容易而且有 [丰富的文档](http://openbox.org/wiki/Help:Themes).

想要 GUI 的主题编辑器, 看这里 [ObTheme](http://xyne.archlinux.ca/info/obtheme).

### X11 鼠标光标

参阅 [Cursor themes](/index.php/Cursor_themes "Cursor themes").

### GTK 主题

参阅 [GTK+#Themes](/index.php/GTK%2B#Themes "GTK+").

### 桌面图标

Openbox 不提供在桌面显示图标的工具. Xfdesktop, PcmanFM, [ROX](http://rox.sourceforge.net), [iDesk](/index.php/Idesk "Idesk"), 甚至 Nautilus (和 gnome-settings-daemon) 可以提供这种功能.

ROX 和 PCmanFM 作为轻量级的文件管理器有着额外的优势.

### 桌面壁纸

Openbox 自身不能更改壁纸. 由 [Feh](/index.php/Feh "Feh") 或 [Nitrogen](/index.php/Nitrogen "Nitrogen") 等类似的程序提供. 其它可选的包括 ImageMagick, hsetroot 和 xsetbg. 或者 Pcmanfm 和 Xfdesktop 也可以.

可以禁止 gnome-settings-daemon 加载壁纸:

```
$ gconftool-2 --set /apps/gnome_settings_daemon/plugins/background/active --type bool False

```

在 Gnome 3 中，使用：

```
$ gsettings set org.gnome.desktop.background draw-background false

```

## 推荐的程序软件

**注意:** <u>主要的</u> [Openbox](/index.php/Openbox "Openbox") 是关于安装 Openbox.

这篇 <u>补充的</u> wiki 文章详述在 Openbox 安装后可以具体的程序配置.

Arch's wiki 上有一个 [轻量级软件清单](/index.php/Lightweight_Applications "Lightweight Applications"); 大多数十分适合 Openbox.

### 登录管理器

[SLiM](http://slim.berlios.de/) 轻量图形登录管理器. 为单独运行的 Openbox 配置. 参考 Arch's [SLiM](/index.php/SLiM "SLiM") wiki for instructions.

[Qingy](http://qingy.sourceforge.net/) 轻量,可配置性高的图形登录管理器. 支持登录到一个文本终端或 X 会话. 使用 [DirectFB](http://www.directfb.org). Qingy 不启动 X 会话除非选择的会话使用 X Windows. 看 Arch's wiki 的 [Qingy](/index.php/Qingy "Qingy").

### 混合桌面视图

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr") 是一个混合窗口管理器,能够为 Openbox 和其它窗口管理器渲染阴影,褪色,和窗口透明.注意 xcompmgr 不值得使用因为不再开发了.出现问题也不会被修复.(例如, 出现一个与 tint2 0.9有关的问题:系统托盘图标有崩溃的趋向)

### 面板,托盘,页调度程序

大量的程序为 Openbox 提供了面板/任务栏, 系统托盘, 页调度程序:

#### 面板

| 
```
[Avant window navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")                 

 [BMPanel](http://nsf.110mb.com/bmpanel/)                           

 [Cairo-dock](http://developer.berlios.de/projects/cairo-dock/)     

 [Fbpanel](http://fbpanel.sourceforge.net)                          

 [Fspanel](http://freshmeat.net/projects/fspanel/)

```
 | 
```
   [Gnome-panel](http://live.gnome.org/GnomePanel/)                 

   [LXPanel](http://www.gnomefiles.org/app.php/LXPanel)             

   [Pancake](http://www.failedprojects.de/pancake/)                 

   [PerlPanel](http://freshmeat.net/projects/perlpanel/)            

  [PyPanel](/index.php/PyPanel "PyPanel")

```
 | 
```
     [Screenlets](http://www.screenlets.org/)                       

    [Tint2](/index.php/Tint2 "Tint2")                                               

     [Wbar](http://code.google.com/p/wbar/)                         

     [Xfce4-panel](http://www.xfce.org/projects/xfce4-panel/)       

```
 |

#### 托盘

```
 [Stalonetray](http://stalonetray.sourceforge.net/)                

 [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

```

#### 页调度程序

```
 [IPager](http://useperl.ru/ipager/index.en.html)                  

 [Neap](http://code.google.com/p/neap/)                            

 [Netwmpager](https://aur.archlinux.org/packages.php?ID=17563)      

```

如果不想桌面布局上有页调度程序, 试试 [obsetlayout](https://aur.archlinux.org/packages/obsetlayout/), 一个设置布局的工具版本.

### 文件管理器

两个流行的轻量级文件管理器:

*   [Thunar](/index.php/Thunar "Thunar") Thunar支持插件和自动挂载功能.
*   [ROX](http://rox.sourceforge.net) ROX 提供一组文件/桌面图标.

```
# pacman -S thunar
# pacman -S rox

```

*   [PCManFM](http://pcmanfm.sourceforge.net) 稍微有点不轻量.

```
# pacman -S pcmanfm   #  PcManFM 提供桌面图标.
# pacman -S ntfs-3g   #  允许 PCManFM 挂载 NTFS 设备.

```

更轻量的,考虑 [Gentoo](http://www.obsession.se/gentoo/) 或 [emelFM2.](http://emelfm2.net/). 这两个软件实现了典型的两格布局, 其它的文件管理器有 [xfe](http://sourceforge.net/projects/xfe/) 和 [muCommander.](http://www.mucommander.com/)

也可以用 Gnome 的 Nautilus. 虽然不轻量而且比上述程序要慢, 但是 Nautilus 支持 [virtual file systems,](https://en.wikipedia.org/wiki/Virtual_file_system "wikipedia:Virtual file system") 通过 SSH, FTP, 或 Samba 接入文件夹.这也是优势.

### 应用程序启动器

#### Dmenu

安装设置 [dmenu](/index.php/Dmenu "Dmenu") 在 wiki 中有描述 . 然后把下面的内容加入 `~/.config/openbox/rc.xml` 的 <keyboard> 段来开启用快捷键启动 dmenu :

```
   <keybind key="W-space">
     <action name="Execute">
       <execute>dmenu_run</execute>
     </action>
   </keybind>

```

#### [Gmrun](/index.php/Gmrun "Gmrun")

[gmrun](http://sourceforge.net/projects/gmrun) 提供一个很好的运行对话框, 类似在 Gnome 和 KDE 中的 Alt+F2 功能:

```
# pacman -S gmrun

```

关于 Gmrun 的细节, 看 [here](/index.php/Gmrun "Gmrun"). 把以下内容加入 `~/.config/openbox/rc.xml` 的 <keyboard> 段来开启 Alt+F2 功能 :

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

#### Bashrun2

[bashrun2](http://bashrun.sourceforge.net) 提供了一种不同的, 准系统的方法来运行对话框.在一个小的 xterm 窗口内使用一个特定的 bash 会话. 可以在 [AUR](https://aur.archlinux.org/packages.php?ID=43465) 找到,跟以上一样用 Alt+F2 启动. 想让 bashrun2 更像一个运行对话框, 把以下内容加入 `~/.config/openbox/rc.xml` 的 <applications> 段:

```
   <application name="bashrun2-run-dialog">
     <desktop>all</desktop>
     <decor>no</decor>  # switch to yes if you prefer a bordered window
     <focus>yes</focus>
     <skip_pager>yes</skip_pager>
     <layer>above</layer>
   </application>

```

#### Kupfer

[Kupfer](https://aur.archlinux.org/packages.php?ID=27896) 是用 Python 写的 Quicksilver 的一个启动激发器.

"只要输入程序或文件的名字的前部分就能用它来快速唤起一程序或文档.除了快速启动外它可以做得更多: 有更多的接入对象和不同的插件运行自定义命令"

#### Launchy

[Launchy](http://www.launchy.net/) 是比较不简洁的方法; 它有多种皮肤和提供更多的功能类如计算器, 查看天气等. 最初是窗口, 类似 Gnome Do.

```
# pacman -S launchy

```

用 Ctrl+Space 启动.

#### LXPanel

LXPanel 的运行对话框可以用下面命令执行

```
lxpanelctl run

```

#### Gnome-panel

gnome-panel 的运行对话框:

```
gnome-panel-control --run-dialog

```

### 剪贴板管理器

你或者想安装功能更丰富的剪贴板管理器.

**xfce4-clipman-plugin, parcellite,** 或 **glipper-old** 可以用 pacman 安装. 把剪贴板管理器加入 **`autostart`.**

### 音量管理器

#### Gvolwheel, gvtray

Gvolwheel 是一个通过在系统托盘的图标管理音量的混音管理器. [gvolwheel](https://aur.archlinux.org/packages/gvolwheel/) , AUR 上有.

Gvtray 是系统托盘上的主混音管理器. [gvtray](https://aur.archlinux.org/packages/gvtray/) AUR 上有.

#### Obmixer

Obmixer 是用 C 写的小程序. 它打算作为 Gnome 的音量管理器的轻量级替代. [obmixer](https://aur.archlinux.org/packages.php?ID=31131) AUR 有.

#### Volti

Volti 是在系统托盘/通知区域控制音量的 GTK+ 程序 . [volti](https://aur.archlinux.org/packages.php?ID=33525) AUR 有.

#### Volumeicon, volwheel

Volumeicon 系统托盘上的音量控制. [volumeicon](https://www.archlinux.org/packages/?name=volumeicon) AUR 有.

Volwheel 是通过鼠标滚轮控制音量的托盘图标. [volwheel](https://www.archlinux.org/packages/?name=volwheel) AUR 有.

### 电池 & CPU

#### Trayfreq

[Trayfreq](/index.php/Trayfreq "Trayfreq") 是一个轻量的电池监视器和 CPU 频率定标器.

### 键盘布局转换器

#### Fbxkb, xxkb, axkb

AUR 的键盘指示器和转换器 [fbxkb](https://aur.archlinux.org/packages/fbxkb/)

AUR 的键盘布局转换/指示器 [xxkb](https://www.archlinux.org/packages/?name=xxkb)

#### xneur

X 神经转换器是一个文本分析器.它探测输入的语言，有错误则改正。 [xneur](https://aur.archlinux.org/packages/xneur/) AUR 有.

### 注销对话框

[exitx](https://aur.archlinux.org/packages/exitx/) 和 [exitx-polkit](https://aur.archlinux.org/packages.php?ID=47005) 是分别使用 sudo 和 Policykit 的注销对话框, AUR 上有.

[obshutdown](https://aur.archlinux.org/packages/obshutdown/) 是一个不错的 openbox 关机管理器。

另外，你也可以使用 openbox 的菜单创建一个简单的对话框，也可以绑定快捷键。

一个使用 `exit-menu` 作为 id ，Exit 作为标签的例子:

```
<menu id="exit-menu" label="Exit">
	<item label="Log Out">
		<action name="Execute">
			<command>openbox --exit</command>
		</action>
	</item>
	<item label="Shutdown">
		<action name="Execute">
			<command>systemctl poweroff</command>
		</action>
	</item>
	<item label="Restart">
		<action name="Execute">
		        <command>systemctl reboot</command>
		</action>
	</item>
	<item label="Suspend">
		<action name="Execute">
		        <command>systemctl suspend</command>
		</action>
	</item>
	<item label="Hibernate">
		<action name="Execute">
		        <command>systemctl hibernate</command>
		</action>
	</item>
</menu>

```

以上添加到 menu.xml，然后在你的菜单或者子菜单调用：

```
<menu id="exit-menu"/>

```

如果你想绑定快捷键，只需要把这个键绑定添加到 rc.xml:

```
<keybind key="XF86PowerOff">
  <action name="ShowMenu">
      <menu>exit-menu</menu>
  </action>
</keybind>

```

这会绑定到关机键，如果你需要的话也可把 XF86PowerOff 改成你喜欢的键。