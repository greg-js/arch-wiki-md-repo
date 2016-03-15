**翻译状态：** 本文是英文页面 [CDemu](/index.php/CDemu "CDemu") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-02-11，点击[这里](https://wiki.archlinux.org/index.php?title=CDemu&diff=0&oldid=246797)可以查看翻译后英文页面的改动。

[CDemu](http://cdemu.sourceforge.net/) 是一个虚拟光驱，可以挂载.bin/.cue, .nrg, 或 .ccd 等非ISO-9660格式光盘镜像。`mount` 只能挂载包含单一文件系统的 iso。而许多 cd 都带有复杂的信息，比如混合数据和音轨。CDemu 能获得这些CD镜像完整、原始的内容。

CDemu 利用vhba内核模块模拟出一个SCSI CD/DVD设备，由后台运行的cdemud守护进程(<tt>cdemud</tt>)与该模块通信。镜像分析代码被抽象到一个库中(<tt>libmirage</tt>)，需要支持新的镜像格式时，也便于扩充。守护进程响应来自客户端的[dbus](/index.php/Dbus "Dbus")命令。CDemu软件包提供了两种可选的客户端：基于命令行的(<tt>cdemu-client</tt>)和[GNOME](/index.php/GNOME "GNOME")的panel applet——(<tt>gcdemu</tt>).

## 安装

CDemu 可以通过 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库") 中的软件包 [cdemu-client](https://www.archlinux.org/packages/?name=cdemu-client) 获得。

[AUR](/index.php/AUR "AUR") 中包含了多个图形界面：

*   GTK/Gnome [gcdemu](https://aur.archlinux.org/packages/gcdemu/): 提供 GNOME 面板程序。
*   KDE [kde-cdemu-manager](https://aur.archlinux.org/packages/kde-cdemu-manager/): 独立程序，与 Dolphin 的动作菜单交互，可以在镜像文件上右键。
*   Plasma 5 : [kde-cdemu-manager-kf5](https://aur.archlinux.org/packages/kde-cdemu-manager-kf5/) 是 [kde-cdemu-manager](https://aur.archlinux.org/packages/kde-cdemu-manager/) 在KF5框架上的移植。

启动 Systemd 服务:

```
# systemctl enable cdemu-daemon.service

```

## 示例

将单个镜像加载为第一个设备：

```
# cdemu load 0 ~/image.mds

```

将多文件镜像加载为第一个设备：

```
# cdemu load 0 ~/session1.toc ~/session2.toc ~/session3.toc

```

设定字符编码:

```
# cdemu load 0 ~/image.cue --encoding=windows-1250

```

挂载加密镜像:

```
# cdemu load 0 ~/image.daa --password=seeninplain

```

卸载第一个设备:

```
# cdemu unload 0

```

显示设备状态:

```
# cdemu status

```

显示设备挂载信息:

```
# cdemu device-mapping

```

Setting daemon debug mask for the first device:

```
# cdemu daemon-debug-mask 0 0x01

```

Obtaining library debug mask for the first device:

```
# cdemu library-debug-mask 0

```

Disabling DPM emulation on all devices:

```
# cdemu dpm-emulation all 0

```

Enabling transfer rate emulation on first device:

```
# cdemu tr-emulation 0 1

```

Changing device ID of first device:

```
# cdemu device-id 0 "MyVendor" "MyProduct" "1.0.0" "Test device ID"

```

Enumerating supported parsers:

```
# cdemu enum-supported-parsers

```

Enumerating supported fragments:

```
# cdemu enum-supported-fragments

```

Enumerating supported daemon debug masks:

```
# cdemu enum-daemon-debug-masks

```

Enumerating supported library debug masks:

```
# cdemu enum-library-debug-masks

```

Displaying daemon and library version:

```
# cdemu version

```