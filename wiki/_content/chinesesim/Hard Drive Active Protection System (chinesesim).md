**翻译状态：** 本文是英文页面 [Hard_Drive_Active_Protection_System](/index.php/Hard_Drive_Active_Protection_System "Hard Drive Active Protection System") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-09，点击[这里](https://wiki.archlinux.org/index.php?title=Hard_Drive_Active_Protection_System&diff=0&oldid=390293)可以查看翻译后英文页面的改动。

HDAPS意为"硬盘主动防护系统",它在硬盘受到突然冲击时(比如你的笔记本掉落或撞击到桌子上时)保护硬盘,其工作原理是在发生意外冲击时停放磁头,这样磁头就不会撞击到盘片上,也许这会避免一个灾难性的硬盘损伤.

**Note:** [固态硬盘](/index.php/Solid_State_Drives_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Solid State Drives (简体中文)")不需要HDAPS,因为其不包含高速旋转的机械部件.

## Contents

*   [1 震动检测](#.E9.9C.87.E5.8A.A8.E6.A3.80.E6.B5.8B)
    *   [1.1 tp_smapi](#tp_smapi)
    *   [1.2 模块参数invert](#.E6.A8.A1.E5.9D.97.E5.8F.82.E6.95.B0invert)
*   [2 保护](#.E4.BF.9D.E6.8A.A4)
    *   [2.1 hdapsd](#hdapsd)
*   [3 图形界面工具](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E5.B7.A5.E5.85.B7)
*   [4 参见](#.E5.8F.82.E8.A7.81)

## 震动检测

硬件需要支持震动检测。一般来说，实现此功能的是笔记本主板上的一个加速度计。除了硬件，还需要有驱动程序将硬件检测到的内容告诉操作系统。这个部分描述实现此功能的驱动程序。

### tp_smapi

[tp_smapi](/index.php/Tp_smapi "Tp smapi") 是一套适用于ThinkPad的驱动程序集。如果你有一台支持此功能的ThinkPad，就算你没打算使用HDAPS也强烈推荐使用tp_smapi。除了很多有用的功能外，tp_smapi还会把加速计输出为操纵杆设备`/dev/input/js#` (注意! 这可能会干扰到系统的其他操纵杆设备).

从community库中安装[tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi).重启后会启动大部分的驱动，设备信息位于`/sys/devices/platform/smapi`.

内核有自己的 HDAPS 驱动，之前需要手动装载模块 tp_smapi 模块，现在[tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) 软件包会将`hdaps.ko` 安装到 [/lib/modules/$(uname -r)/updates](http://www.mail-archive.com/arch-dev-public@archlinux.org/msg01995.html)，替换掉内置模块。这样只需加入`hdaps`模块就好了。

**Note:** 参见 [这个bug报告](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=628829), 某些ThinkPad使用了tp_smapi不支持的固件,并且看起来在不久的将来tp_smapi也不会支持这些固件. 这些系列存在此问题: Edge, SL, L, X1xxe. 项目页面表示 x121e 主要功能应该没问题，但是用户报告无法工作，所以这些设备目前的支持都有问题。

### 模块参数invert

某些ThinkPads需要添加invert模块参数来正确处理X和Y旋转轴. 如果需要的话,在`/etc/modprobe.d/modprobe.conf`中添加:

```
options hdaps invert=1

```

例如 ThinkPad T410,可以添加`invert=1` .invert可以取如下值:

*   invert=1 反转X和Y轴;
*   invert=2 反转X轴 (如果已经倒置两轴则此参数值无效)
*   invert=4 交换X和Y (在反转之前)

参数值可以相加. 例如, invert=5 交换两轴后反转两轴. 最大的参数值是7.如果你不清楚该怎么办的话,可以使用[hdaps-gl](https://aur.archlinux.org/packages/?K=hdaps-gl)或者其它图形界面工具 (见下). 另外, 你可以从 [这张表](http://www.thinkwiki.org/wiki/Tp_smapi#Model-specific_status)里的"HDAPS axis orientation"项中得出你需要的参数值.

除了修改后重新载入 `hdaps` 模块之外, 还可以通过直接写 `/sys/devices/platform/hdaps/invert` 来修改 `invert` 值。

## 保护

现在,你的硬件已经能将受到冲击的信息报告给操作系统,我们需要让操作系统在收到此信息后保护硬盘.这个部分描述的是在收到信息后保护硬盘的软件.

### hdapsd

hdapsd可以接收HDAPS传感器的信息并判断是否受到冲击,如果是的话通知内核停放磁头.

设置hdaps时你应该检查硬盘的[SMART](/index.php/SMART "SMART")信息中的"Load cycle count". 如果检测太过于敏感的话,磁头将会不停地进行停放操作,load cycle count将会上升很快.

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85 "Pacman (简体中文)")[hdapsd](https://www.archlinux.org/packages/?name=hdapsd)后,通过`hdapsd.service`来[启动](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") hdapsd的守护进程.

你可以在hdaps的unit file里调整参数(详见[systemd的文章](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BF.AE.E6.94.B9.E7.8E.B0.E5.AD.98.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6 "Systemd (简体中文)")). 比如以下面的文件覆盖默认的service文件将调整hdaps的灵敏度与记录:

 `/etc/systemd/system/hdapsd.service.d/sensitivity.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/hdapsd --sensitivity=40 -blp

```

然后重载配置.

## 图形界面工具

这里有一些显示hdapsd状态的软件,通过它们你很容易知道发生了些什么.你可以选择不安装它们.

**HDAPS monitor** — KDE4 plasmoid对于HDAPS.

	[https://store.kde.org/content/show.php/?content=103481](https://store.kde.org/content/show.php/?content=103481) || [kdeplasma-applets-hdaps-monitor](https://aur.archlinux.org/packages/kdeplasma-applets-hdaps-monitor/)

**xfce4-hdaps** — Xfce4面板小程序.

	[http://michael.orlitzky.com/code/xfce4-hdaps.xhtml](http://michael.orlitzky.com/code/xfce4-hdaps.xhtml) || [xfce4-hdaps](https://aur.archlinux.org/packages/xfce4-hdaps/)

**HDAPSicon** — （之前的thinkhdaps）是一个独立的GTK小程序.运行时会在通知区显示图标.

	[https://github.com/thpani/thinkhdaps](https://github.com/thpani/thinkhdaps) || [hdapsicon-git](https://aur.archlinux.org/packages/hdapsicon-git/)

**hdaps-gl** — 一个简单的OpenGL程序 ,它以3D动画的形式显示您的ThinkPad的状态,和联想的Windows下的软件很像.

	[https://github.com/evgeni/hdapsd](https://github.com/evgeni/hdapsd) || [hdaps-gl](https://aur.archlinux.org/packages/hdaps-gl/)

## 参见

*   [How to protect the harddisk through APS at ThinkWiki](http://www.thinkwiki.org/wiki/How_to_protect_the_harddisk_through_APS)
*   [HDAPS at ThinkWiki](http://www.thinkwiki.org/wiki/HDAPS)