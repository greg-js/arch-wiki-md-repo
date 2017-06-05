**翻译状态：** 本文是英文页面 [CPU_Frequency_Scaling](/index.php/CPU_Frequency_Scaling "CPU Frequency Scaling") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-04-04，点击[这里](https://wiki.archlinux.org/index.php?title=CPU_Frequency_Scaling&diff=0&oldid=247933)可以查看翻译后英文页面的改动。

本文涵盖了在Lenovo T420笔记本上安装和配置Arch Linux的信息。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 硬件](#.E7.A1.AC.E4.BB.B6)
    *   [2.1 指纹扫描器](#.E6.8C.87.E7.BA.B9.E6.89.AB.E6.8F.8F.E5.99.A8)
    *   [2.2 部分多媒体按键](#.E9.83.A8.E5.88.86.E5.A4.9A.E5.AA.92.E4.BD.93.E6.8C.89.E9.94.AE)
    *   [2.3 未测试](#.E6.9C.AA.E6.B5.8B.E8.AF.95)
*   [3 笔记本设置](#.E7.AC.94.E8.AE.B0.E6.9C.AC.E8.AE.BE.E7.BD.AE)
    *   [3.1 ACPI](#ACPI)
    *   [3.2 Tp_smapi](#Tp_smapi)
    *   [3.3 CPU频率调整](#CPU.E9.A2.91.E7.8E.87.E8.B0.83.E6.95.B4)
    *   [3.4 风扇](#.E9.A3.8E.E6.89.87)
    *   [3.5 Laptop Mode Tools](#Laptop_Mode_Tools)
    *   [3.6 触摸板](#.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [3.7 NVIDIA Optimus](#NVIDIA_Optimus)
    *   [3.8 可选内核引导参数](#.E5.8F.AF.E9.80.89.E5.86.85.E6.A0.B8.E5.BC.95.E5.AF.BC.E5.8F.82.E6.95.B0)
*   [4 故障解决](#.E6.95.85.E9.9A.9C.E8.A7.A3.E5.86.B3)
    *   [4.1 多媒体键](#.E5.A4.9A.E5.AA.92.E4.BD.93.E9.94.AE)
    *   [4.2 重新绑定前进/后退键](#.E9.87.8D.E6.96.B0.E7.BB.91.E5.AE.9A.E5.89.8D.E8.BF.9B.2F.E5.90.8E.E9.80.80.E9.94.AE)
    *   [4.3 打开/关闭触摸板](#.E6.89.93.E5.BC.80.2F.E5.85.B3.E9.97.AD.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [4.4 音量提升/降低键无法改变音量](#.E9.9F.B3.E9.87.8F.E6.8F.90.E5.8D.87.2F.E9.99.8D.E4.BD.8E.E9.94.AE.E6.97.A0.E6.B3.95.E6.94.B9.E5.8F.98.E9.9F.B3.E9.87.8F)
    *   [4.5 使用电池时关机](#.E4.BD.BF.E7.94.A8.E7.94.B5.E6.B1.A0.E6.97.B6.E5.85.B3.E6.9C.BA)
    *   [4.6 重启时挂起](#.E9.87.8D.E5.90.AF.E6.97.B6.E6.8C.82.E8.B5.B7)
    *   [4.7 无背景灯控制](#.E6.97.A0.E8.83.8C.E6.99.AF.E7.81.AF.E6.8E.A7.E5.88.B6)
*   [5 参考文献](#.E5.8F.82.E8.80.83.E6.96.87.E7.8C.AE)

## 安装

此型号笔记本支持[UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")，也支持传统BIOS。

使用最新的[Archiso](https://www.archlinux.org/download/)没有遇到安装问题。

其余安装过程请参考[official install guide](/index.php/Installation_guide "Installation guide")。

## 硬件

除了以下硬件外，其余硬件安装完成即可使用：

### 指纹扫描器

指纹扫描器可以在fprint和PAM配合下完美工作（建议同时安装fingerprint-gui）。

查看 [Fprint#Setup_fingerprint-gui](/index.php/Fprint#Setup_fingerprint-gui "Fprint")以获得更多细节。

### 部分多媒体按键

*   查看 [下文](/index.php/Lenovo_ThinkPad_T420#.E5.A4.9A.E5.AA.92.E4.BD.93.E6.8C.89.E9.94.AE "Lenovo ThinkPad T420")

### 未测试

*   火线

## 笔记本设置

### ACPI

[ACPI](/index.php/ACPI_modules "ACPI modules") 支持完善。没有明显问题。

### Tp_smapi

不幸的是，[tp_smapi](/index.php/Tp_smapi "Tp smapi")在Thinkpad T420上只被部分支持。很多特性从0.41开始才能工作。例如，硬盘驱动器保护机制[HDAPS](/index.php/HDAPS "HDAPS")现在工作得非常好。请阅读链接的wiki入口。

一些特性，如设置电池开始充电阈值仍然不工作。为了控制电池充电阈值，请安装Perl脚本[tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat)，它位于[AUR](/index.php/Arch_User_Repository "Arch User Repository").

通过以下命令加载内核模块`acpi_call`：

```
modprobe acpi_call

```

通过命令手工设置阈值

```
perl /usr/lib/perl5/vendor_perl/tpacpi-bat -v startChargeThreshold 0 40
perl /usr/lib/perl5/vendor_perl/tpacpi-bat -v stopChargeThreshold 0 80

```

这个示例中40和80表示满电量的百分比。请调整为你需要的值。你也可能想编写一个简单的`set-battery.service`并且启用它以便在启动系统时自动执行。虽然这些值应该是永久有效的，但实际上它们会在电池被移除时重置。

```
[Unit]
Description=Set battery capacity

[Service]
Type=oneshot
ExecStart=/usr/bin/perl /usr/lib/perl5/vendor_perl/tpacpi-bat -v stopChargeThreshold 0 80
ExecStart=/usr/bin/perl /usr/lib/perl5/vendor_perl/tpacpi-bat -v startChargeThreshold 0 40

[Install]
WantedBy=multi-user.target

```

另外，如果你装了Windows作为双引导，你仍然可以通过联想电源管理器来控制电池阈值。它会直接与电池控制器通讯来达到目标。

如果使用systemd，你可能想在systemd-modules-load.service加载失败时屏蔽tp_smapi，因为新型号的ThinkPad都能够通过ACPI控制一切（逻辑混乱，没理解原作者什么意思）。

### CPU频率调整

[CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")在这个机型的所有可能处理器上都能正常运作。

### 风扇

thinkpad_acpi需要配置才能让用户空间程序正确控制风扇转速。

 `/etc/modprobe.d/thinkpad_acpi.conf`  `options thinkpad_acpi fan_control=1` 

[thinkfan](https://aur.archlinux.org/packages.php?ID=24359)配置文件需要知道如何控制风扇转速。用以下配置替换默认的传感器配置：

 `/etc/thinkfan.conf`  `sensor /sys/devices/virtual/thermal/thermal_zone0/temp` 

你可以通过在[rc.conf](/index.php/Rc.conf "Rc.conf")文件中添加或删除`DAEMONS`数组中的项来启动它。它最终看起来将类似于：

```
DAEMONS=(...@thinkfan...)

```

或者，如果你使用systemd，请使用：

```
# systemctl enable thinkfan.service

```

### Laptop Mode Tools

使用[Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")时未发现任何问题。

可能的Bug[#使用电池时关机](#.E4.BD.BF.E7.94.A8.E7.94.B5.E6.B1.A0.E6.97.B6.E5.85.B3.E6.9C.BA)

[AUR](/index.php/Arch_User_Repository "Arch User Repository")中的[tlp](https://www.archlinux.org/packages/?name=tlp)是另一个可选的可替换Laptop Mode Tools的工具。

### 触摸板

触摸板和小红帽能直接工作，但触摸板实在太过灵敏而不便使用，因为它被当作是鼠标对待。为了修复这个问题，[安装](/index.php/Pacman "Pacman")[xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)包并把以下两个文件加入你的`/etc/X11/xorg.conf.d/`目录中：

 `50-thinkpad-trackpoint.conf` 
```
 Section "InputClass"
        Identifier      "ThinkPad TrackPoint"
        MatchProduct    "TPPS/2 IBM TrackPoint"
        MatchDevicePath "/dev/input/event*"
        Option          "EmulateWheel"          "true"
        Option          "EmulateWheelButton"    "2"
        Option          "XAxisMapping"          "6 7"
        Option          "YAxisMapping"          "4 5"
 EndSection

```
 `50-twofingerscroll.conf` 
```
 Section "InputClass"
        Identifier      "two finger scrolling"
        Driver          "synaptics"
        MatchProduct    "SynPS/2 Synaptics TouchPad"
        MatchDevicePath "/dev/input/event*"
        Option          "VertTwoFingerScroll"   "on"
        Option          "HorizTwoFingerScroll"  "on"
        Option          "EmulateTwoFingerMinW"  "8"
        Option          "EmulateTwoFingerMinZ"  "40"
        Option          "TapButton1"            "1"
 EndSection

```

请按自己需要调整。阅读[Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")以获取更多信息。

要调整小红帽的速度/灵敏度，请在`/etc/rc.local`中添加如下配置：

 `/etc/rc.local` 
```
TPDEV=/sys/devices/platform/i8042/serio1
echo -n 180 > $TPDEV/speed
echo -n 200 > $TPDEV/sensitivity

```

可取值范围是1-255。

### NVIDIA Optimus

[Bumblebee](/index.php/Bumblebee "Bumblebee")在具有NVIDIA Optimus的型号上工作正常。

### 可选内核引导参数

使用如下内核引导参数可以[[1]](http://www.phoronix.com/scan.php?page=article&item=intel_i915_power&num=1%7C减少电池消耗):

```
i915.i915_enable_rc6=1
i915.i915_enable_fbc=1
i915.lvds_downclock=1 
i915.semaphores=1

```

**注意:** 当前的3.6.x内核中， 可能存在一个未知原因的电源效率衰退问题。它在3.7内核版本中还没有被修复。（预计修复版本是3.8——译者注）

## 故障解决

### 多媒体键

开箱即可使用的多媒体键：

*   无线网络开/关
*   背景灯光设置
*   键盘灯
*   静音

开箱不可直接使用的媒体键：

*   [音量键](#.E9.9F.B3.E9.87.8F.E6.8F.90.E5.8D.87.2F.E9.99.8D.E4.BD.8E.E9.94.AE.E6.97.A0.E6.B3.95.E6.94.B9.E5.8F.98.E9.9F.B3.E9.87.8F) （在[GNOME](/index.php/GNOME "GNOME")中开箱即可使用）
*   麦克风静音（很可能需要自定义内核补丁）

你必须找到变通方案并且自己绑定剩下的键。

### 重新绑定前进/后退键

前进/后退键（方向键旁边的键）可以容易地重新映射为PageDown/PageUp。

[安装](/index.php/Pacman "Pacman") xmodmap及其软件包[xorg-server-utils](https://www.archlinux.org/packages/?name=xorg-server-utils)

新建一个`~/.Xmodmap` 文件，内容为：

```
keysym XF86Back = Page_Up
keysym XF86Forward = Page_Down

```

把此行添加到你的`~/.xinitrc`文件中使它工作：

```
xmodmap ~/.Xmodmap

```

你也可以重新映射上一首(`Fn+方向左`)和下一首(`Fn+方向右`)为Home/End：

```
keysym XF86AudioNext = End
keysym XF86AudioPrev = Home

```

**注意:** 为使修改生效你必须重新登录。

**注意:** 至少在[KDE](/index.php/KDE "KDE")下这些键本来是开箱可用的。

### 打开/关闭触摸板

一些情况下(`Fn+F8`)键无法正常打开或关闭触摸板。有一个简单的键盘绑定需要添加到你的`~/.xbindkeysrc`文件中以使快速切换触摸板键能够工作。为使它工作，运行`xbindkeysrc`。这将会绑定 `Fn+F8`到'切换触摸板开/关'功能。（在i3wm 和 xfce4中通过测试，这些情况下`Fn+F8`原本都不工作）

```
# 切换触摸板开/关
"synclient TouchpadOff=`synclient -l | grep -ce TouchpadOff.*0`"
   m:0x0 + c:199
   XF86TouchpadToggle

```

### 音量提升/降低键无法改变音量

又一个`~/.xbindkeysrc`中的快速键绑定以改变音量（在一些环境中本来不工作）。运行`xbindkeys`使设置生效。截取自[Xbindkeys](/index.php/Xbindkeys "Xbindkeys")：

```
#提升音量
"amixer set Master playback 1+"
   m:0x0 + c:123
   XF86AudioRaiseVolume

```

```
#降低音量
"amixer set Master playback 1-"
   m:0x0 + c:122
   XF86AudioLowerVolume

```

为了生静音按钮工作，我把它与Alsa接口绑定：

```
# Toggle mute
"amixer set Master toggle"
   m:0x0 + c:121
   XF86AudioMute

```

### 使用电池时关机

有用户汇报T420在使用电池时关机变为重启。有一些办法能够尝试修复这个问题，以下展示了三种。

一种办法是禁用模块`ehci_hcd`。查看[Kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")以获得更多信息。

或者是禁用Laptop Mode Tools 把`!laptop-mode`添加到`DAEMONS`数组，它位于文件`/etc/rc.conf`：

```
DAEMONS=(...!laptop-mode...)

```

[这篇论坛帖子](https://bbs.archlinux.org/viewtopic.php?pid=1106437#p1106437)详细描述了其他能让你电脑正常关机的方法。关闭`laptop-mode`守护进程会使电池持续时间受损，所以当移动使用中又需要正常关机时帖子里的方法会更方便。

**注意:** 在笔者的机器上只要在关机时把禁用的蓝牙/无线/WWAN启用，就可以完全避免重启。TLP能够更方便地实现这个功能

### 重启时挂起

这是一个很多笔记本上都存在的问题，可以通过[禁用](/index.php/Kernel_modules#Blacklisting "Kernel modules")`e1000e`内核模块修复。

### 无背景灯控制

有一个用户报告亮度控制（fn+home, fn+end）在一些桌面环境中不工作。可以通过添加如下内核参数修复此问题：

```
acpi_backlight=vendor acpi_osi=Linux

```

## 参考文献

*   [Lenovo ThinkPad T420s](/index.php/Lenovo_ThinkPad_T420s "Lenovo ThinkPad T420s")
*   [ThinkPad T420i上的Arch Linux](http://sysphere.org/~anrxc/j/articles/thinkpad-t420/index.html)