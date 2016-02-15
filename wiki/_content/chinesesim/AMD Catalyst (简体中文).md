**翻译状态：** 本文是英文页面 [AMD_Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-11-05，点击[这里](https://wiki.archlinux.org/index.php?title=AMD_Catalyst&diff=0&oldid=406475)可以查看翻译后英文页面的改动。

AMD的显卡驱动有两种：一是官方私有驱动(catalyst，译为催化剂)，二是开源驱动(xf86-video-ati).本文主要介绍私有驱动。

AMD曾经将“catalyst”驱动命名为“fglrx” (**F**ire**GL** and **R**adeon **X**). 现在虽然名为“catalyst”,但内核模块名称依然为“fglrx.ko”. 因此,下文中任何提及fglrx 都是指“内核模块”,而不是指软件包.

**官方仓库不再提供Catalyst。** Catalyst [曾被移出Arch官方支持](https://www.archlinux.org/news/ati-catalyst-support-dropped/)，原因是对质量与开发速度的不满。该项目于2013年4月被再次丢弃,截止现在还没有进一步的消息.

与开源驱动相比, Catalyst 在2D,3D渲染和电源管理上更胜一筹,但缺乏高效的多显支持.支持设备为 [ATI/AMD Radeon](https://en.wikipedia.org/wiki/Radeon "wikipedia:Radeon")显卡，芯片组 R600 及以上(Radeon HD 2xxx或者更新). _model_名称 (如X1900, HD4850) 与 _chip_名称 (分别是R580, RV770)间的对照请参见Xorg [decoder ring](http://www.x.org/wiki/RadeonFeature/#index5h2)或者[这个表格](https://en.wikipedia.org/wiki/Comparison_of_AMD_graphics_processing_units "wikipedia:Comparison of AMD graphics processing units").

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 安装Catalyst](#.E5.AE.89.E8.A3.85Catalyst)
        *   [1.1.1 从非官方软件库](#.E4.BB.8E.E9.9D.9E.E5.AE.98.E6.96.B9.E8.BD.AF.E4.BB.B6.E5.BA.93)
        *   [1.1.2 通过AUR安装](#.E9.80.9A.E8.BF.87AUR.E5.AE.89.E8.A3.85)
    *   [1.2 配置驱动](#.E9.85.8D.E7.BD.AE.E9.A9.B1.E5.8A.A8)
        *   [1.2.1 配置X](#.E9.85.8D.E7.BD.AEX)
        *   [1.2.2 启动时加载模块](#.E5.90.AF.E5.8A.A8.E6.97.B6.E5.8A.A0.E8.BD.BD.E6.A8.A1.E5.9D.97)
        *   [1.2.3 禁用KMS](#.E7.A6.81.E7.94.A8KMS)
        *   [1.2.4 检查安装是否成功](#.E6.A3.80.E6.9F.A5.E5.AE.89.E8.A3.85.E6.98.AF.E5.90.A6.E6.88.90.E5.8A.9F)
    *   [1.3 自己编译内核](#.E8.87.AA.E5.B7.B1.E7.BC.96.E8.AF.91.E5.86.85.E6.A0.B8)
    *   [1.4 PowerXpress support](#PowerXpress_support)
        *   [1.4.1 同时运行两个X server(一个使用Intel驱动, 一个使用 fglrx)](#.E5.90.8C.E6.97.B6.E8.BF.90.E8.A1.8C.E4.B8.A4.E4.B8.AAX_server.28.E4.B8.80.E4.B8.AA.E4.BD.BF.E7.94.A8Intel.E9.A9.B1.E5.8A.A8.2C_.E4.B8.80.E4.B8.AA.E4.BD.BF.E7.94.A8_fglrx.29)
        *   [1.4.2 多显示器的PowerXpress笔记本运行于AMD模式时(pxp_switch_catalyst amd)的问题](#.E5.A4.9A.E6.98.BE.E7.A4.BA.E5.99.A8.E7.9A.84PowerXpress.E7.AC.94.E8.AE.B0.E6.9C.AC.E8.BF.90.E8.A1.8C.E4.BA.8EAMD.E6.A8.A1.E5.BC.8F.E6.97.B6.28pxp_switch_catalyst_amd.29.E7.9A.84.E9.97.AE.E9.A2.98)
*   [2 Xorg软件库](#Xorg.E8.BD.AF.E4.BB.B6.E5.BA.93)
    *   [2.1 xorg117](#xorg117)
    *   [2.2 xorg116](#xorg116)
    *   [2.3 xorg115](#xorg115)
    *   [2.4 xorg114](#xorg114)
    *   [2.5 xorg113](#xorg113)
    *   [2.6 xorg112](#xorg112)
*   [3 工具](#.E5.B7.A5.E5.85.B7)
    *   [3.1 Catalyst-hook](#Catalyst-hook)
    *   [3.2 Catalyst-generator](#Catalyst-generator)
    *   [3.3 OpenCL / OpenGL 开发](#OpenCL_.2F_OpenGL_.E5.BC.80.E5.8F.91)
        *   [3.3.1 amdapp-aparapi](#amdapp-aparapi)
        *   [3.3.2 amdapp-sdk (以前的amdstream)](#amdapp-sdk_.28.E4.BB.A5.E5.89.8D.E7.9A.84amdstream.29)
        *   [3.3.3 amdapp-codexl](#amdapp-codexl)
*   [4 功能](#.E5.8A.9F.E8.83.BD)
    *   [4.1 Tear Free Rendering](#Tear_Free_Rendering)
    *   [4.2 视频加速](#.E8.A7.86.E9.A2.91.E5.8A.A0.E9.80.9F)
    *   [4.3 显卡/显存频率, 温度, 风扇转速, 超频工具](#.E6.98.BE.E5.8D.A1.2F.E6.98.BE.E5.AD.98.E9.A2.91.E7.8E.87.2C_.E6.B8.A9.E5.BA.A6.2C_.E9.A3.8E.E6.89.87.E8.BD.AC.E9.80.9F.2C_.E8.B6.85.E9.A2.91.E5.B7.A5.E5.85.B7)
    *   [4.4 双屏显示](#.E5.8F.8C.E5.B1.8F.E6.98.BE.E7.A4.BA)
        *   [4.4.1 介绍](#.E4.BB.8B.E7.BB.8D)
        *   [4.4.2 ATI Catalyst Control Center](#ATI_Catalyst_Control_Center)
        *   [4.4.3 安装](#.E5.AE.89.E8.A3.85_2)
        *   [4.4.4 设置](#.E8.AE.BE.E7.BD.AE)
*   [5 卸载](#.E5.8D.B8.E8.BD.BD)
*   [6 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [6.1 运行 atieventsd.service 失败](#.E8.BF.90.E8.A1.8C_atieventsd.service_.E5.A4.B1.E8.B4.A5)
    *   [6.2 无法打开 fglrx_dri.so](#.E6.97.A0.E6.B3.95.E6.89.93.E5.BC.80_fglrx_dri.so)
    *   [6.3 启动 GDM 失败](#.E5.90.AF.E5.8A.A8_GDM_.E5.A4.B1.E8.B4.A5)
    *   [6.4 在Wine上3D应用冻结](#.E5.9C.A8Wine.E4.B8.8A3D.E5.BA.94.E7.94.A8.E5.86.BB.E7.BB.93)
    *   [6.5 视频颜色不正常](#.E8.A7.86.E9.A2.91.E9.A2.9C.E8.89.B2.E4.B8.8D.E6.AD.A3.E5.B8.B8)
    *   [6.6 KWin 与混成](#KWin_.E4.B8.8E.E6.B7.B7.E6.88.90)
    *   [6.7 重启或启动x后，黑屏并且一直不退出](#.E9.87.8D.E5.90.AF.E6.88.96.E5.90.AF.E5.8A.A8x.E5.90.8E.EF.BC.8C.E9.BB.91.E5.B1.8F.E5.B9.B6.E4.B8.94.E4.B8.80.E7.9B.B4.E4.B8.8D.E9.80.80.E5.87.BA)
        *   [6.7.1 错误的ACPI硬件调用](#.E9.94.99.E8.AF.AF.E7.9A.84ACPI.E7.A1.AC.E4.BB.B6.E8.B0.83.E7.94.A8)
    *   [6.8 注销后KDM消失](#.E6.B3.A8.E9.94.80.E5.90.8EKDM.E6.B6.88.E5.A4.B1)
    *   [6.9 直接渲染无效](#.E7.9B.B4.E6.8E.A5.E6.B8.B2.E6.9F.93.E6.97.A0.E6.95.88)
    *   [6.10 休眠问题](#.E4.BC.91.E7.9C.A0.E9.97.AE.E9.A2.98)
        *   [6.10.1 视频播放不能从休眠状态中恢复](#.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE.E4.B8.8D.E8.83.BD.E4.BB.8E.E4.BC.91.E7.9C.A0.E7.8A.B6.E6.80.81.E4.B8.AD.E6.81.A2.E5.A4.8D)
    *   [6.11 系统冻结或硬件锁死](#.E7.B3.BB.E7.BB.9F.E5.86.BB.E7.BB.93.E6.88.96.E7.A1.AC.E4.BB.B6.E9.94.81.E6.AD.BB)
    *   [6.12 硬件冲突](#.E7.A1.AC.E4.BB.B6.E5.86.B2.E7.AA.81)
    *   [6.13 播放视频时系统短时间死机](#.E6.92.AD.E6.94.BE.E8.A7.86.E9.A2.91.E6.97.B6.E7.B3.BB.E7.BB.9F.E7.9F.AD.E6.97.B6.E9.97.B4.E6.AD.BB.E6.9C.BA)
    *   [6.14 "aticonfig: No supported adaptaters detected"](#.22aticonfig:_No_supported_adaptaters_detected.22)
    *   [6.15 让chromium支持WebGL](#.E8.AE.A9chromium.E6.94.AF.E6.8C.81WebGL)
    *   [6.16 用Adobe的flashplugin观看flash，画面迟滞或冻结](#.E7.94.A8Adobe.E7.9A.84flashplugin.E8.A7.82.E7.9C.8Bflash.EF.BC.8C.E7.94.BB.E9.9D.A2.E8.BF.9F.E6.BB.9E.E6.88.96.E5.86.BB.E7.BB.93)
    *   [6.17 GNOME3中移动窗口延迟/很慢](#GNOME3.E4.B8.AD.E7.A7.BB.E5.8A.A8.E7.AA.97.E5.8F.A3.E5.BB.B6.E8.BF.9F.2F.E5.BE.88.E6.85.A2)
    *   [6.18 在1920x1080分辨率下不能全屏(欠扫描,屏幕周围有黑边)](#.E5.9C.A81920x1080.E5.88.86.E8.BE.A8.E7.8E.87.E4.B8.8B.E4.B8.8D.E8.83.BD.E5.85.A8.E5.B1.8F.28.E6.AC.A0.E6.89.AB.E6.8F.8F.2C.E5.B1.8F.E5.B9.95.E5.91.A8.E5.9B.B4.E6.9C.89.E9.BB.91.E8.BE.B9.29)
    *   [6.19 双屏设置: 关于加速,OpenGL,合成,效能的一般问题](#.E5.8F.8C.E5.B1.8F.E8.AE.BE.E7.BD.AE:_.E5.85.B3.E4.BA.8E.E5.8A.A0.E9.80.9F.2COpenGL.2C.E5.90.88.E6.88.90.2C.E6.95.88.E8.83.BD.E7.9A.84.E4.B8.80.E8.88.AC.E9.97.AE.E9.A2.98)
    *   [6.20 禁用VariBright功能](#.E7.A6.81.E7.94.A8VariBright.E5.8A.9F.E8.83.BD)
    *   [6.21 Hybrid/PowerXpress: 关掉独立GPU](#Hybrid.2FPowerXpress:_.E5.85.B3.E6.8E.89.E7.8B.AC.E7.AB.8BGPU)
    *   [6.22 从X会话切换到TTY黑屏/低分辨率TTY](#.E4.BB.8EX.E4.BC.9A.E8.AF.9D.E5.88.87.E6.8D.A2.E5.88.B0TTY.E9.BB.91.E5.B1.8F.2F.E4.BD.8E.E5.88.86.E8.BE.A8.E7.8E.87TTY)
    *   [6.23 从X会话切换到TTY黑屏,背光并没有关闭](#.E4.BB.8EX.E4.BC.9A.E8.AF.9D.E5.88.87.E6.8D.A2.E5.88.B0TTY.E9.BB.91.E5.B1.8F.2C.E8.83.8C.E5.85.89.E5.B9.B6.E6.B2.A1.E6.9C.89.E5.85.B3.E9.97.AD)
    *   [6.24 切换TTY后切换回X会话时,只有一个带鼠标的黑屏](#.E5.88.87.E6.8D.A2TTY.E5.90.8E.E5.88.87.E6.8D.A2.E5.9B.9EX.E4.BC.9A.E8.AF.9D.E6.97.B6.2C.E5.8F.AA.E6.9C.89.E4.B8.80.E4.B8.AA.E5.B8.A6.E9.BC.A0.E6.A0.87.E7.9A.84.E9.BB.91.E5.B1.8F)
    *   [6.25 30 FPS / Tear-Free / V-Sync bug](#30_FPS_.2F_Tear-Free_.2F_V-Sync_bug)
    *   [6.26 背光调节不起效](#.E8.83.8C.E5.85.89.E8.B0.83.E8.8A.82.E4.B8.8D.E8.B5.B7.E6.95.88)
    *   [6.27 使用 plasma 时 Chromium 出现毛刺(glitching)](#.E4.BD.BF.E7.94.A8_plasma_.E6.97.B6_Chromium_.E5.87.BA.E7.8E.B0.E6.AF.9B.E5.88.BA.28glitching.29)
*   [7 参见](#.E5.8F.82.E8.A7.81)

## 安装

共有三种途径安装Catalyst。第一种是用[Vi0L0](https://aur.archlinux.org/account/Vi0l0/)(Arch非官方Catalyst维护人员)维护的软件库.此库包涵了所有可用的软件包.第二种方式就是通过AUR，Vi0L0提供的PKGBUILDs跟他用于构建他仓库的PKGBUILDs完全一样。最后你还可以直接通过AMD官方下载Catalyst.

自Catalyst 12.4, AMD已将针对Radeon HD 5xxx 和 Radeon HD 2xxx, 3xxx and 4xxx 显卡驱动分开开发，因此在你选择何种安装方式之前，应查看你的显卡型号。Radeon HD 2xxx, 3xxx and 4xxx 显卡用 **legacy**驱动，Radeon HD 5xxx（以及更新的）用普通Catalyst。但无论你需要哪种驱动,都应安装Catalyst utilities。

**注意:** 你会发现,每种安装方式都会进行的一个相同的操作,无论你采用哪种安装方式,你都应了解一些通用的安装说明。

### 安装Catalyst

#### 从非官方软件库

如果你不喜欢通过[AUR](/index.php/AUR "AUR")来安装,则使用此方法。此软件库由我们的[Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")维护。所有的包都经过签名，所以安全方面无需担心。下文提及的很多其他与AMD显卡有关的包也是由Vi0L0维护。

Vi0L0有三个不同的Catalyst软件库:

*   [catalyst](/index.php/Unofficial_user_repositories#catalyst "Unofficial user repositories"):Radeon HD 5xxx及更新的显卡使用的普通Catalyst驱动。包含了最新的 (稳定版或者beta版) Catalyst.
*   _catalyst-stable_:Radeon HD 5xxx及更新的显卡使用的普通Catalyst驱动。包含了最新的稳定版 Catalyst.
*   [catalyst-hd234k](/index.php/Unofficial_user_repositories#catalyst-hd234k "Unofficial user repositories"):Radeon HD 2xxx, 3xxx and 4xxx显卡使用的legacy Catalyst驱动.

要启用上述软件库的话,参见[Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")中所述方法. 记得在`pacman.conf`中的**其他软件库之前**添加相应软件库.

**注意:** _catalyst_和_catalyst-stable_软件库的URL相同.若要启用_catalyst-stable_,步骤与启用_catalyst_相同,并在`pacman.conf`中将`[catalyst]`替换成`[catalyst-stable]`.如果你需要某个旧版本,这儿也有并且URL也相同,比如_catalyst-stable-13.4_.

**警告:**

*   legacy Catalyst不支持Xorg Server 1.17\. 要使用此驱动的话，参见 [#Xorg repositories](#Xorg_repositories) 来回滚到 Xorg Server 1.16.

**小贴士:** 有时 catalyst.wirephire.com 因为超出带宽上限而不能提供下载(曾发生过这个问题),或者你到这个服务器的连接很慢.这时,你可以尝试另外的镜像服务器: [[1]](http://mirror.rts-informatique.fr/archlinux-catalyst/) (rtsinformatique 提供,法国) 和 [[2]](http://mirror.hactar.bz/Vi0L0/) (goll 提供,德国). 不过,这些服务器不保证随时可用.需要的话就反注释掉,多准备一个替代品以防镜像临时不可用也是好习惯.

Repository mirroring can be easily achieved using `rsync://mirror.rts-informatique.fr::archlinux-catalyst`.

完成后更新pacman数据库并[安装](/index.php/Pacman "Pacman")这些软件包(更多信息参见[#工具](#.E5.B7.A5.E5.85.B7)):

*   _catalyst-hook_
*   _catalyst-utils_
*   _catalyst-libgl_
*   _opencl-catalyst_ - 可选,OpenCL支持
*   _lib32-catalyst-utils_ - 可选,64-bit系统上32-bit的OpenGL支持
*   _lib32-catalyst-libgl_ - 可选,64-bit系统上32-bit的OpenGL支持
*   _lib32-opencl-catalyst_ - 可选,64-bit系统上32-bit的OpenCL支持

如果你是一台Intel/AMD双显卡笔记本,参考下这个:

*   _catalyst-hook_
*   _catalyst-utils-pxp_
*   _lib32-catalyst-utils-pxp_ - 可选,64-bit系统上32-bit的OpenGL支持

**注意:** 如果pacman询问是否移除**libgl**,尽管回答"是".

**警告:** 软件包catalyst已从Vi0L0的仓库移除,catalyst-hook取而代之.

#### 通过AUR安装

还可以通过[AUR](/index.php/AUR "AUR")安装。如果你需为你的电脑进行定制安装，则用此方法。此方法极为繁琐，因为它需要的工作量最大，而且每次内核更新后你得手动更新Catalyst。

**警告:** 若通过AUR安装 Catalyst, 每次内核更新你都得重新编译Catalyst,否则X将不能启动。

在 Vi0L0's 软件库中提到的一切软件包[AUR](/index.php/AUR "AUR")中也可用::

*   [Catalyst](https://aur.archlinux.org/packages/Catalyst/)
*   [Catalyst-generator](https://aur.archlinux.org/packages/Catalyst-generator/)
*   [Catalyst-hook](https://aur.archlinux.org/packages/Catalyst-hook/)
*   [Catalyst-utils](https://aur.archlinux.org/packages/Catalyst-utils/)
*   [Lib32-catalyst-utils](https://aur.archlinux.org/packages/Lib32-catalyst-utils/)

AUR还提供些独家软件包。它含有被称为 _Catalyst-total_的包和一些beta阶段的软件:

*   [Catalyst-total](https://aur.archlinux.org/packages/Catalyst-total/)
*   [Catalyst-total-pxp](https://aur.archlinux.org/packages/Catalyst-total-pxp/)
*   [Catalyst-total-hd234k](https://aur.archlinux.org/packages/Catalyst-total-hd234k/)
*   [Catalyst-test](https://aur.archlinux.org/packages/Catalyst-test/)

[catalyst-total](https://aur.archlinux.org/packages/catalyst-total/)包能让AUR用户更为方便。它能构建驱动、内核工具、32位内核工具和[catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/)(参见[#工具](#.E5.B7.A5.E5.85.B7)).

[catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/)让Catalyst对powerXpress提供实验性支持。

### 配置驱动

安装完毕后，要配置 X，让其使用Catalyst。要确保fglrx模块在启动阶段加载，而且要禁用[kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting").

#### 配置X

你需要创建 `xorg.conf` 文件来配置X. Catalyst提供了`aticonfig`工具来创建和（或）修改此文件。 通过访问`/etc/ati/amdpcsdb`文件它几乎能配置显卡的各项参数。了解完整的配置选项`aticonfig`可运行:

```
# aticonfig --help | less

```

**警告:** 在将各项配置参数提交到`/etc/X11/xorg.conf`之前使用`--output`选项，`/etc/X11/xorg.conf.d`中的所有内容都会被覆盖。(Use the `--output` option before committing to `/etc/X11/` as an `xorg.conf` file will override anything in `/etc/X11/xorg.conf.d/`)

**注意:** 如果坚持使用`xorg.conf.d`下的新配置文件：为了让`Device`部分与`/etc/X11/xorg.conf.d/20-radeon.conf`相匹配，则使用`# aticonfig [...] --output`.但这有一个缺点，很多依赖xorg.conf的`aticonfig`选项都无法使用。

现在来配置 Catalyst. 若只有一个显示器，运行:

```
# aticonfig --initial

```

**注意:** 如果对PowerXpress有疑问,安装 [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/).

注意，若你使用双显示器则使用下面的命令。 此命令会成两个配置文件，第二个显示器的配置文件在第一个前面

```
# aticonfig --initial=dual-head --screen-layout=above

```

**注意:** 了解与设置双显有关的更多信息可查看[#双屏显示](#.E5.8F.8C.E5.B1.8F.E6.98.BE.E7.A4.BA)

你可与[Sample Xorg.conf](/index.php/Xorg#Sample_configurations "Xorg")上的任何一个示例文件进行对照。

虽然目前的版本的Xorg启动时能自动探测大多数选项，但不同Xorg版本的默认参数可能会有所不同，最好明确指定一些参数.

给一个示例配置 (注意) **仅供参考**. 标`#`必须有,标`##`很可能会用到:

 `/etc/X11/xorg.conf` 

```
Section "ServerLayout"
        Identifier     "Arch"
        Screen      0  "Screen0" 0 0          # 0's are necessary.
EndSection
Section "Module"
        Load [...]
        [...]
EndSection
Section "Monitor"
        Identifier   "Monitor0"
        ...
EndSection
Section "Device"
        Identifier  "Card0"
        Driver      "fglrx"                         # Essential.
        BusID       "PCI:1:0:0"                     # Recommended if autodetect fails.
        Option      "OpenGLOverlay" "0"             ##
        Option      "XAANoOffscreenPixmaps" "false" ##
EndSection
Section "Screen"
        Identifier "Screen0"
        Device     "Card0"
        Monitor    "Monitor0"
        DefaultDepth    24
        SubSection "Display"
                Viewport   0 0
                Depth     24                        # Should not change from '24'
                Modes "1280x1024" "2048x1536"       ## 1st value=default resolution, 2nd=maximum.
                Virtual 1664 1200                   ## (x+64, y) to workaround potential OGL rect. artifacts/
        EndSubSection                               ## fixed in Catalyst 9.8
EndSection
Section "DRI"
        Mode 0666                                   # May help enable direct rendering.
EndSection
```

**注意:** 一旦升级Catalyst就要通过后面的方法删除`amdpcsdb`文件: 关闭X，删除`/etc/ati/amdpcsdb`，启动X然后运行`amdcccle` -否则`amdcccle`将会显示错误的Catalyst版本号

_更多信息参考[这里](https://bbs.archlinux.org/viewtopic.php?id=57084)._

#### 启动时加载模块

禁用`radeon`以防其自动加载. 在`/etc/modprobe.d/modprobe.conf`里禁用_radeon_,同时保证它不被`/etc/modules-load.d/`里的文件加载. 详见[kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

接下来,使模块`fglrx`自动加载. 添加`fglrx`到`/etc/modules-load.d/`下已有的模块文件的新一行,或者创建一个新的模块文件并添加`fglrx`.

#### 禁用KMS

**注意:** 使用`catalyst-utils-pxp`或者`catalyst-total-pxp`的用户不要这样做,因为intel驱动需要KMS.

禁用KMS很重要.由于Catalyst根本不使用[KMS](/index.php/KMS "KMS")，得将其禁用。否则，当系统切换至TTY或在桌面环境下关机时，系统可能会冻结。

添加 `nomodeset` 到你的 [内核参数](/index.php/Kernel_parameters "Kernel parameters").

#### 检查安装是否成功

重启电脑并登录, 运行下列命令可查看`fglrx`是否正确运行:

```
$ lsmod | grep fglrx

```

若有输出, 则证明安装成功。可以尝试用 `$ startx` 或者显示管理器来启动X (参见 [Xorg#Running](/index.php/Xorg#Running "Xorg")).

下面的命令可以输出你的显卡型号信息:

```
$ fglrxinfo

```

运行以下命令检查直接渲染模式是否启用:

```
$ glxinfo | grep direct

```

若显示`"direct rendering: yes"`，恭喜你，到位了! 若无`$ glxinfo`命令，安装[mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) package。

**注意:** 对于`glxgears`,你也可以使用:

```
$ fgl_glxgears

```

来测试fglrx.

**警告:** 最近几版Xorg，库函数路径变了，因此即使安装`libGL.so`也不一定能正确人加载。请检查GL是否工作，可阅读"故障排除"段落

### 自己编译内核

在手动编译的内核上,你必须构建你自己的`catalyst-$kernel`包.

**注意:** 如果你讨厌打包或毫无经验，可先阅读[ABS](/index.php/ABS "ABS")。

1.  从[Catalyst](/index.php/AUR "AUR")上获取`PKGBUILD` 和 `catalyst.install`文件。
2.  编辑PKGBUILD. 两个地方需要修改:
    1.  将`pkgname=catalyst` 修改为 `pkgname=catalyst-$kernel_name`,`$kernel_name`可以随意取(如：custom, mm)。
    2.  将`linux`的依赖修改为`$kernel_name`。
3.  构建并安装软件包;运行`makepkg -i` 和 `makepkg`，接着运行 `# pacman -U pkgname.pkg.tar.gz`

**注意:**

*   如果在安装有多内核的系统上，你必须为所有内核安装 [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) 包。这不会引起冲突.

*   [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/)能为你自动构建`catalyst-{kernver}`，因此这些步骤根本就可省略。 请参考[工具 部分](#.E5.B7.A5.E5.85.B7).

### PowerXpress support

PowerXpress technology 允许支持dual-graphic功能(以前叫做AMD Hybrid CrossFire technology)的笔记本电脑从集成显卡(IGP) 切换到独立显卡，以增加电池寿命或者实现更好的3D渲染效能。

为了在archlinux上用上这个功能，你j将需要:

*   从 [AUR](/index.php/AUR "AUR") 获取并编译 [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/) 这个软件包，或者
*   从 [catalyst] 软件仓库安装 **catalyst-utils-pxp** 软件包 (如果需要，还有 lib32-catalyst-utils-pxp)。

对于intel集成显卡的切换，你还需要安装 [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl) 软件包和intel的驱动：[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 。

**注意:** **对最新的13.1版本的Catalyst(不是Catalyst legacy) ChrisXY 能够兼容最新的 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) (版本 1.13.1), [mesa](https://www.archlinux.org/packages/?name=mesa) 9.0.1 和 [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.20.18**.

对于所有版本低于13.1的Catalyst（和任何版本的Catalyst legacy)，和新的intel驱动存在一些兼容问题。**最近的[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)开发版本是2.20.2-2**，所以你可能必须从Arch软件仓库中的最新版本降级（尽管我们推荐你试验性地使用最新的驱动，因为有可能它在你这里没有问题）

[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.20.2-2 只兼容 xorg-server 1.12 并且特它是 **xorg112 repository**的一部分. 如果你想使用它，你必须降级xorg-server。具体信息见 [#Xorg repositories](#Xorg_repositories).

现在你可以用下面这些命令切换集成显卡和独立显卡：

```
# aticonfig --px-igpu    #for integrated GPU
# aticonfig --px-dgpu    #for discrete GPU
```

Just remember that fglrx needs `/etc/X11/xorg.conf` configured for AMD's card with `fglrx` inside. 要记着对含有 `fglrx` 模块的AMD显卡，fglrx需要 `/etc/X11/xorg.conf` 这个文件

你也可以用`pxp_switch_catalyst` 这个切换脚本完成一些其他有用的操作：

*   Switching `xorg.conf` - it will rename `xorg.conf` into `xorg.conf.cat` (if there is fglrx inside) or `xorg.conf.oth` (if there is intel inside) and then it will create a symlink to `xorg.conf`, depending on what you chose.
*   Running `aticonfig --px-Xgpu`.
*   Running `switchlibGL`.
*   Adding/removing `fglrx` into/from `/etc/modules-load.d/catalyst.conf`.

Usage:

```
# pxp_switch_catalyst amd
# pxp_switch_catalyst intel
```

如果你试图在装有intel驱动的设备上运行X图形界面时遇到问题，你可以尝试强制开启"UXA" acceleration: 在`xorg.conf`中写`Option "AccelMethod" "uxa"`,就象这样：

 `/etc/X11/xorg.conf` 

```
Section "Device"
        Identifier  "Intel Graphics"
        Driver      "intel"
        #Option      "AccelMethod"  "sna"
        **Option      "AccelMethod"  "uxa"**
        #Option      "AccelMethod"  "xaa"
EndSection
```

#### 同时运行两个X server(一个使用Intel驱动, 一个使用 fglrx)

因为fglrx容易崩溃（考虑到PowerXpress），主要X server使用Intel驱动，另一个使用需要3D加速的fglrx驱动是个不错的选择。但是在开启第二个X server的时候，简单地从集成显卡 `aticonfig` 或者 `amdcccle`切换到独立显卡将引发一系列不正常的bugs。

为了同时运行两个X server（每个用不同的驱动），你首先需要设置出一个可以和Catalyst一起正常工作的X图形环境，然后把它的 `xorg.conf`移动到一个临时的地方（比如`/etc/X11/xorg.conf.fglrx`）。下次X图形环境启动时，它将默认使用intel驱动来代替fglrx。

在开启第二个使用fglrx的X server，只需要在运行X之前，把`xorg.conf` 移回合适的地方(`/etc/X11/xorg.conf`)。这个方法甚至允许你在两个运行的X sessions之间来回切换。当你不需要使用fglrx时，再把 `xorg.conf` 移动到其他地方。

这种方法唯一的坏处是不能使用intel驱动的3D加速。但它的2D却能完全发挥作用。除此之外，它还能给我们一个非常稳定的桌面环境。

#### 多显示器的PowerXpress笔记本运行于AMD模式时(pxp_switch_catalyst amd)的问题

当PowerXpress笔记本工作于AMD-only模式时(比如设置全部渲染工作交给独显),你有可能会遇到显示器伪影/重复的情况.这是一个已知的问题,发生于7xxxM系列显卡.

当旋转或者缩放一个显示器时现象会消失,所以你可以使用xrandr来解决这个问题:

 `xrandr --output HDMI1 --left-of LVDS1 --primary --scale 1x1 --output LVDS1 --scale 1.0001x1.0001` 

## Xorg软件库

Catalyst由于其缓慢的更新而被人大为诟病。因升级Xorg而造成两者不兼容是稀松平常的事。也就意味着Catalyst用户要么自己编译Xorg的包要么使用一个只包含Xorg包的回溯软件库，该库中不提供更新版Xorg以确保兼容性。 Vi0L0提供好几个这样的库.

要启用上述软件库的话,参见[Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")中所述方法. 记得在`pacman.conf`中的**其他软件库之前(甚至在你的catalyst仓库前,如果你有的话)**添加相应软件库(使用和[catalyst](/index.php/Unofficial_user_repositories#catalyst "Unofficial user repositories")库相同的PGP密匙).

### xorg117

Catalyst 不支持 xorg-server 1.18

```
[xorg117]
Server = http://catalyst.wirephire.com/repo/xorg117/$arch
## Mirrors, if the primary server does not work or is too slow:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg117/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg117/$arch

```

### xorg116

Catalyst < 15.7 不支持 xorg-server 1.17

```
[xorg116]
Server = http://catalyst.wirephire.com/repo/xorg116/$arch
## 如果上面那个不行或者太慢的话就换这些镜像站:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg116/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg116/$arch

```

### xorg115

Catalyst < 14.9 不支持 xorg-server 1.16

```
[xorg115]
Server = http://catalyst.wirephire.com/repo/xorg115/$arch
## 如果上面那个不行或者太慢的话就换这些镜像站:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg115/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg115/$arch

```

### xorg114

Catalyst < 14.1 不支持 xorg-server 1.15.

```
[xorg114]
Server = http://catalyst.wirephire.com/repo/xorg114/$arch
## 如果上面那个不行或者太慢的话就换这些镜像站:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg114/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg114/$arch

```

### xorg113

Catalyst < 13.6 不支持 xorg-server 1.14.

```
[xorg113]
Server = http://catalyst.wirephire.com/repo/xorg113/$arch
## 如果上面那个不行或者太慢的话就换这些镜像站:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg113/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg113/$arch

```

### xorg112

Catalyst < 12.10 和 Catalyst Legacy 不支持 xorg-server 1.13.

```
[xorg112]
Server = http://catalyst.wirephire.com/repo/xorg112/$arch
## 如果上面那个不行或者太慢的话就换这些镜像站:
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/xorg112/$arch
#Server = http://mirror.hactar.bz/Vi0L0/xorg112/$arch

```

## 工具

### Catalyst-hook

[Catalyst-hook](https://aur.archlinux.org/packages/Catalyst-hook/) 是一个 [systemd](/index.php/Systemd "Systemd") 服务,它在系统关机或重启后重新构建`fglrx`模块(如果需要的话,比如内核升级后).

使用之前请保证 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 组和 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) 包(对应你的内核)已经安装.

只需激活`catalyst-hook.service`服务即可:

```
# systemctl enable catalyst-hook
# systemctl start catalyst-hook

```

你也可以用这个软件包来手动构建`fglrx`模块. 在内核更新后运行 `catalyst_build_module` 脚本即可:

```
# catalyst_build_module all

```

**一些技术细节:**

The `catalyst-hook.service` is stopping the systemd "river" and is forcing systemd to wait until catalyst-hook finishes its job.

`catalyst-hook.service` 调用 `catalyst_build_module check` 来检查是否有必要重构建fglrx.

`check` 检查`fglrx`模块是否存在:

*   不存在,将构建它;

*   存在,它将比较两个参数来确定是否有必要重构建`fglrx`.

这里的参数是 `/usr/lib/modules/<kernel_version>/build/Module.symvers` 的md5值. (因为我(这里指Vi0L0)发现每一个版本的这个文件都不一样). 第一个参数是现有的 `Module.symvers` 文件md5.第二个参数是`fglrx`模块构建时 `Module.symvers` 文件的md5\. 这个参数被`catalyst_build_module`脚本编译到`fglrx`模块.

如果参数不同,将编译新的`fglrx`模块.

check 检查整个 `/usr/lib/modules/` 目录 ,为安装的所有内核编译fglrx模块(如果需要的话). 如果没有必要构建或重构建,进程将很快结束.

### Catalyst-generator

[catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/)包能构建并安装`fglrx`模块，该模块与pacman兼容的`catalyst-${kernver}`相适应。与[#Catalyst-hook](#Catalyst-hook)的区别是必须手动使用此命令，而Catalyst-hook则不需。

通过[makepkg](/index.php/Makepkg "Makepkg")，它能构建`catalyst-${kernver}`二进制包并用[pacman](/index.php/Pacman "Pacman")安装。`${kernver}` 是软件包的目标内核版本 (例如 catalyst-2.6.35-ARCH 适用于 2.6.35-ARCH 内核).

非特权用户使用`catalyst_build_module`来构建并安装`catalyst-{kernver}`包。安装时会提示输入root密码。

简单说一下如何使用此包:

1.  root用户: 使用`catalyst_build_module remove`。此举会删除无用的`catalyst-{kernver}`包。
2.  非特权用户: 使用`catalyst_build_module ${kernver}`, `${kernver}`是指升级过后的内核版本。也可通过`catalyst_build_module all`为所有安装的内核构建`catalyst-{kernver}`。
3.  若要删除`catalyst-generator`, 在使用`catalyst_build_module remove_all`命令删除catalyst-generator之前最好切换到root用户，**这会删除所有`catalyst-{kernver}`包.**

当删除`Catalyst-generator`时，`Catalyst-generator`不能自动删除那些`catalyst-{kernver}`包，这是因为pacman不允许有一个以上的实例同时运行。若在使用`# pacman -R catalyst-generator`前忘记运行`# catalyst_build_module remove_all`，catalyst-generator将会询问删除catalyst-generator自身后要删除哪个`catalyst-{kernver}`包。

Catalyst-generator 是最安全的,最符合KISS原则的,因为:

1.  你可以使用非特权用户来构建包;
2.  它在 fakeroot 环境构建包;
3.  它不乱丢文件,[pacman](/index.php/Pacman "Pacman")知道文件们在哪;
4.  你需要做的只是,记得去使用它

**注意:** 在构建 `catalyst-{kernver}` 时，若看到下列警告，乃正常情况，不必莫名惊诧:

```
**WARNING:** Package contains reference to $srcdir

```

```
**WARNING:** '.pkg' is not a valid archive extension

```

### OpenCL / OpenGL 开发

这几年AMD一直在为OpenCL and OpenGL的开发做一套工具集。

现在AMD在**"Heterogeneous Computing"**的旗帜下提供了更多的工具集，幸运的是它们也在Linux下可用。

在AUR和 [catalyst] 软件仓库，你可以找到这些代表了AMD最重要工作的工具软件包：

*   [amdapp-aparapi](https://aur.archlinux.org/packages/amdapp-aparapi/)
*   [amdapp-sdk](https://aur.archlinux.org/packages/amdapp-sdk/)
*   [amdapp-codexl](https://aur.archlinux.org/packages/amdapp-codexl/)

APP 这个缩写代表 Accelerated Parallel Processing（加速并行处理）。

#### amdapp-aparapi

AMD的Aparapi是一个用java实现的API，用于并行地表达图像数据，它同时也是一个能把java字节码翻译成能被OpenCL识别的运行时组件。所以它能够被很多种图形处理器（GPU）执行。如果Aparapi在GPU上不能执行，那将在java的线程池中执行。

更多关于Aparapi的信息：[here](http://developer.amd.com/tools/heterogeneous-computing/aparapi/)。

#### amdapp-sdk (以前的amdstream)

AMD APP 软件开发工具套件，是一个由AMD制作地一套完整的开发平台。它让你能够快速和容易地使用AMD APP技术，使得你的程序得到加速。这个SDK提供了代码实例，技术文档和其他资料，让您可以在你的C\C++程序中使用 OpenCL, Bolt, or C++ AMP等技术实现计算加速。

从2.8版本开始，amdapp-sdk 提供了 aparapiUtil 和 aparapi 的代码实例。有一个包已经加入到了[catalyst]软件仓库。它依赖于[amdapp-aparapi](https://aur.archlinux.org/packages/amdapp-aparapi/)。AUR中的软件包让你选择需不需要aparapi's additions。

2.8 版本没有提供探查功能（ Profiler functionality），它已经被移到CodeXL中了。

关于 AMD APP SDK 的更多信息： [here](http://developer.amd.com/tools/heterogeneous-computing/amd-accelerated-parallel-processing-app-sdk/)。

#### amdapp-codexl

CodeXL 是一个带有静态OpenCl内核分析器的OpenCL and OpenGL调试器和探查器。它具有GUI界面，是在著名的[gdebugger](https://aur.archlinux.org/packages/gdebugger/) 基础上完成的。它只支持 x86_64 系统。

关于CodeXL的更多信息： [这里](http://developer.amd.com/tools/heterogeneous-computing/codexl/)。

## 功能

### Tear Free Rendering

在**Catalyst 11.1**中，很可能是添加了三重缓存和v-sync，_Tear Free Desktop_减少了2D，3D视频应用的屏幕撕裂毛病。但这需要额外的GPU处理。

要启用'Tear Free Desktop'，运行`amdcccle`，然后设置`Display Options` → `Tear Free`。

或以root身份运行:

```
# aticonfig --set-pcs-u32=DDX,EnableTearFreeDesktop,1

```

若禁用，使用`amdcccle`或以root身份运行:

```
# aticonfig --del-pcs-key=DDX,EnableTearFreeDesktop

```

### 视频加速

**[Video Acceleration API](https://en.wikipedia.org/wiki/Video_Acceleration_API "wikipedia:Video Acceleration API") (VA API)**是为基于Linux/UNIX操作系统提供利用GPU加速视频处理的一个开源函数库和应用程序接口规范。启用视频加速后，通过各种入口(VLD, IDCT, Motion Compensation, deblocking)它能加速常用编码标准（MPEG-2, MPEG-4 ASP/H.263, MPEG-4 AVC/H.264, and VC-1/WMV3)视频文件的解码过程（俗称硬解）。

VA-API在[xvba-video](https://aur.archlinux.org/packages/xvba-video/)上有一个私有后端（2009年10月）, 它允许使用VA-API的程序通过[XvBA (X-Video Bitstream Acceleration API designed by AMD)](https://en.wikipedia.org/wiki/XvBA "wikipedia:XvBA")函数库来充分利用拥有uvd2（第二代通用视频解码单元）芯片组的视频加速功能.

**注意:** 使用 `catalyst-test` 或者 `catalyst-total` 时不需要安装 [xvba-video](https://aur.archlinux.org/packages/xvba-video/) , 因为有已经创建好的符号链接代替.

xvba-video和支持XvBA的软件仍还在开发，**但在大多数情况下它都能很好的工作**. 通过AUR构建(或通过Vi0L0的仓库直接安装)专有[xvba-video](https://aur.archlinux.org/packages/xvba-video/)包，若这个版本对你来说有问题,用[libva-xvba-driver](https://aur.archlinux.org/packages/libva-xvba-driver/)取代; 并安装[mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) and [libva](https://www.archlinux.org/packages/?name=libva)。然后将视频播放器的视频输出设置为vaapi:gl:

```
$ mplayer -vo vaapi:gl movie.avi

```

此选项可添加到mplayer的配置文件，参考[MPlayer](/index.php/MPlayer "MPlayer")。

针对 **smplayer**:

```
Options → Preferences → General → Video (tab) → Output driver: User Defined : vaapi:gl
Options → Preferences → General → Video (tab) → Double buffering **on**
Options → Preferences → General → General → Screenshots → Turn screenshots **off**
Options → Preferences → Performance → Threads for decoding: **1** (to turn off -lavdopts parameter)

```

**注意:** 如果启用了Tear Free Desktop，则按下列步骤:

```
Options -> Preferences -> General -> Video (tab) -> Output driver: vaapi

```

若视频输出中没有**vaapi:gl**选项 - 可使用:

```
**vaapi**, **vaapi:gl2** or 简单的 **xv(0 - AMD Radeon [AVIVO Video](https://en.wikipedia.org/wiki/Avivo "wikipedia:Avivo"))**.

```

针对 **VLC**:

```
Tools → Preferences → Input & Codecs → Use GPU accelerated decoding

```

它有助于在**amdcccle**中启用v-sync:

```
3D → More Settings → Wait for vertical refresh = Always On

```

**注意:** 若使用**Compiz/KWin**，消除**画面抖动**的唯一方法就是切换至**全屏**并且 **关闭Redirected Fullscreen**。 使用**compiz**，需在ccsm的General Options中设置**Redirected Direct Rendering**。若此举无效，则将其关闭。**KWin**默认关闭此功能，若出现画面抖动则通过`System Settings` → `Desktop Effects` → `Advanced`.

将"Suspend desktop effects for fullscreen windows"开启或关闭。}}

### 显卡/显存频率, 温度, 风扇转速, 超频工具

`$ aticonfig --od-getclocks`可以获知当前显卡/显存频率。

`$ aticonfig --pplib-cmd "get fanspeed 0"`可以获知风扇转速（显卡）；

`$ aticonfig --odgt`可以获知显卡温度。

`$ aticonfig --pplib-cmd "set fanspeed 0 50"`可以设置风扇转速，其中查询索引50代表速度百分比。

若超频或与之相反，则使用图形工具反而相对容易些，如需要qt的**ATi Overclocking Utility**。你可以从[这儿](http://kde-apps.org/content/show.php/ATI+Overclock?content=47796)找到(不过它可能过时了).

更复杂的[amdoverdrivectrl](https://aur.archlinux.org/packages/amdoverdrivectrl/)也能达到此目的，它的主页是[here](http://sourceforge.net/projects/amdovdrvctrl)。可通过[AUR](https://aur.archlinux.org/packages.php?ID=45298)或Vi0L0's非官方软件库构建安装包。

### 双屏显示

#### 介绍

**警告:** 由于安装方式的不同，并且每种安装方式需要与其相对应进行配置，因此设置双屏显示并没有特定的方法,你必须根据你自己的需要采用相应的步骤。当然可以多尝试几种方法。**所以,在修改之前,请务必将你现在能正常使用的`/etc/X11/xorg.conf`备份,以便遇到问题时可以从命令行恢复.**

*   本节讲述如何配置"BIG Desktop"效果。主要是不同尺寸的屏幕如何通过两个不同的输出接口（DVI + HDMI）共享一个显卡。

*   Xinerama解决办法有些不便，尤其是不能与XrandR兼容。因为XrandR对于我们所讲的来说是必须的，所以不使用Xinerama。

*   双头显示能让你有两个不同的会话（一个屏幕一个）。你可以随心所欲地干任何事情，但不能将窗口从一个屏幕移动到另一个屏幕。若只有一个屏幕，你得在Xorg会话里为Server Layout section的每个会话定义鼠标，具体方法查看：

[ATI Documentation](http://support.amd.com/us/kbarticles/Pages/1105-HowCanIConfigureMultip.aspx)

#### ATI Catalyst Control Center

ATI的图形工具非常有用，我们将尽可能地使用它。运行下面命令可启用它:

```
$ {kdesu/gksu} amdcccle

```

**警告:** **千万不要**直接使用sudo。 Sudo虽能给予管理员权限，却使用用户账户的信息（如环境变量）。GNOME下使用_gksu_，KDE下使用_kdesu_。

#### 安装

开始之前，确保你的硬件接插正确，电源开启，而且你得你的硬件属性（2D还是3D屏，屏幕尺寸，刷新率等）。通常情况下，在启动阶段两个显示器都会被识别却不需正确区分先后顺序，而是依赖热插拔功能。尤其在不使用(`/etc/X11/xorg.conf`)配置时。

首先要让你的桌面环境和X认识你的显示器。为此，要为你两个显示器生成基本的Xorg配置文件:

```
# aticonfig --initial --desktop-setup=horizontal --overlay-on=1

```

或

```
# aticonfig --initial=dual-head --screen-layout=left

```

{{注意|`overlay`非常重要，因为它能让两个显示器拥有1种（多种）像素。

**提示:** 运行`aticonfig --help`了解所有可用的命令。

现在可编辑基本的Xorg配置文件（如：添加分辨率）。分辨率一定要正确，尤其是使用不同尺寸的显示器。分辨率在"Screen" section:

```
 SubSection "Display"
    Depth     24
    Modes     "X-resolution screen 1xY-resolution screen 1" "Xresolution screen 2xY-resolution screen 2"
 EndSubSection

```

这以后就不需手动编辑`xorg.conf`，而ATI的图形化工具。重启X，确保正确支持两个显示器和识别屏幕分辨率（两个屏幕相互独立而不是完全一样。

#### 设置

现在只需以root身份启动ATI控制中心，在显示菜单设置你需要的选项(下拉菜单中的小箭头)。设置好后重启X就大功造成（你和我都可松口气了，这段翻译有点难度，呵呵）!

重启X之前,不要忘了核实`xorg.conf`。主要是核实"Display"下的"Screen"节, 在"Virtual"行里，两个显示器的分辨率应该一样。"Server Layout"节则是剩下的参数。

## 卸载

你可能会因为catalyst不工作或者是想试试开源驱动而要卸载掉catalyst:移除 `catalyst` 和 `catalyst-utils` 包. 当然你也应该移除 [catalyst-generator](https://aur.archlinux.org/packages/catalyst-generator/), [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/) 和 [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) 包(如果你安装了的话).

**警告:**

*   你也许需要使用 `# pacman -Rdd` 来移除 [catalyst-utils](https://aur.archlinux.org/packages/catalyst-utils/) (和/或 [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)) 因为它(们)包含了 _gl_ 相关文件,许多包会依赖他们. 这些依赖关系将在安装[xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)时被满足.
*   你也许会需要移除 `/etc/profile.d/ati-flgrx.sh` 和 `/etc/profile.d/lib32-catalyst` (如果他们存在), 否则 `r600_dri.so` 将会载入失败,你将得不到3D支持.

**注意:** 你应该从 `/etc/pacman.conf` 移除非官方仓库,然后运行 `# pacman -Syu`, 因为那些仓库包含过时的Xorg包(为了兼容`catalyst`),而 [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) 包需要来自[官方仓库](/index.php/Official_repositories "Official repositories")的最新的Xorg包.

按如下步骤:

*   如果你有 `/etc/modprobe.d/blacklist-radeon.conf` ,删除文件或者注释掉文件中的`blacklist radeon`.
*   如果你在 `/etc/modules-load.d` 下有配置文件要在启动时载入 `fglrx` 模块, 删除掉或者注释掉 `fglrx` 那一行.
*   记住删除/备份 `/etc/X11/xorg.conf`.
*   如果安装了 [catalyst-hook](https://aur.archlinux.org/packages/catalyst-hook/) 包,记得关掉它的systemd服务的自启动.
*   如果你在 [内核参数](/index.php/Kernel_parameters "Kernel parameters") 中指定了`nomodeset`而现在你打算使用KMS,那么删除`nomodeset`.

*   安装另一个驱动之前记得**重启** .

## 故障排除

若能启动到命令行，问题很可能出在`/etc/X11/xorg.conf`

可阅读`/var/log/Xorg.0.log`或通过下列命令查找线索:

```
$ grep '(EE)' /var/log/Xorg.0.log
$ grep '(WW)' /var/log/Xorg.0.log

```

若看不懂显示的是什么东东,请先搜索论坛,没有结果的话,可将其提交到[thread specific to ATI/AMD](https://bbs.archlinux.org/viewtopic.php?pid=1166052#p1166052/)，注意要提交两者显示的信息。

### 运行 atieventsd.service 失败

从 [官方仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 安装 [acpid](https://www.archlinux.org/packages/?name=acpid). 启用并运行acpid[守护进程](/index.php/Daemon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Daemon (简体中文)").

如果还不行, 编辑 `/usr/lib/systemd/system/atieventsd.service` ,把 `acpid.socket` 改成 `acpid.service`.

### 无法打开 fglrx_dri.so

创建从 `/usr/lib/xorg/modules/dri/fglrx_dri.so` 到 `/usr/X11R6/lib64/modules/dri/fglrx_dri.so` 或其它需要路径的链接：

```
# mkdir -p /usr/X11R6/lib64/modules/dri
# ln -s /usr/lib/xorg/modules/dri/fglrx_dri.so /usr/X11R6/lib64/modules/dri/fglrx_dri.so

```

### 启动 GDM 失败

降级 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 或者试试其它 [显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)") 比如 [LightDM](/index.php/LightDM "LightDM").

### 在Wine上3D应用冻结

若在Wine上3D应用挂起，禁用TLS。使用`aticonfig`或编辑`/etc/X11/xorg.conf`。使用`aticonfig`:

```
# aticonfig --tls=off

```

或以root身份打开`/etc/X11/xorg.conf`，在_Device_段添加`Option "UseFastTLS" "off"`。

只需来个二选一，然后重启X让其生效。

### 视频颜色不正常

仍然使用`vaapi:gl`来防止画面抖动，但这样不会有视频加速:

*   不使用`-vo vaapi`运行**mplayer**。

*   若是**smplayer**，在Options → Preferences → Advanced → Options for MPlayer → Options:中删除`-vo vaapi`。

此后还可以启动**smplayer**的截屏功能。

### KWin 与混成

根据你的显卡，在OpenGL和XRender渲染方式中选择一种更快的。 在某些情况下，XRender还可以解决一些人为的错误(比如调整命令行大小)。

### 重启或启动x后，黑屏并且一直不退出

检查在启动加载器的内核参数行是否添加了`nomodeset`(参考 [#禁用KMS](#.E7.A6.81.E7.94.A8KMS))。 你如果在使用legacy驱动 (`catalyst-hd234k`) 黑屏的话, 尝试降级 xorg-server 到 1.12 (使用 [#xorg112](#xorg112) 库).

#### 错误的ACPI硬件调用

出现此种错误很可能是fglrx模块与系统的ACPI硬件调用配合不够默契而自身禁用，屏幕也就不会有输出。

果真那样，运行:

```
$ aticonfig --acpi-services=off

```

### 注销后KDM消失

若使用Catalyst，当注销后你会获取tty1这个控制台而不是KDM的欢迎界面。每次注销后你必须让kdm重启X服务器. 将标题为`[X-:*-Core]`段里下面行前的注释删掉:

 `/usr/share/config/kdm/kdmrc`  `TerminateServer=True` 

当前注销KDE后KDM就会出现。

### 直接渲染无效

**警告:** 在安装或升级catalyst后却没重启系统，也有可能出现此种错误，因为系统需要加载fglrx.ko模块来让驱动正常工作。

若直接渲染有问题，运行:

```
$ LIBGL_DEBUG=verbose glxinfo > /dev/null

```

从此命令输出的第一行至末尾都与直接渲染无效有关，且非常详细。

常见错误提示和解决办法:

```
libGL error: XF86DRIQueryDirectRenderingCapable returned false

```

*   Ensure that you are loading the correct agp modules for your AGP chipset before you load the `fglrx` kernel module. To determine which agp modules you will need, run `# hwdetect --show-agp`. Then open your `/etc/modules-load.d/fglrx.conf` and add the agp module on a line **before** the `fglrx` line.
*   若使用AGP的芯片组，确保加载fglrx模块之前加载正确的agp模块。要确定哪些agp模块，运行`hwdetect --show-agp`,然后打开`/etc/modules-load.d`下的`fglrx.conf`，将agp模块添加到fglrx行**之前**。

```
libGL error: failed to open DRM: Operation not permitted
libGL error: reverting to (slow) indirect rendering

```

```
libGL: OpenDriver: trying /usr/lib/xorg/modules/dri//fglrx_dri.so
libGL error: dlopen /usr/lib/xorg/modules/dri//fglrx_dri.so failed
(/usr/lib/xorg/modules/dri//fglrx_dri.so: cannot open shared object file: No such file or directory)
libGL error: unable to find driver: fglrx_dri.so

```

*   某些软件未正确安装。在错误提示中，若路径为`/usr/X11R6/lib/modules/dri/fglrx_dri.so`,彻底注销，然后重新登录。若使用图形化的登录管理器(gdm, kdm, xdm)，确保每次登录时`/etc/profile`都会被读取。将`source /etc/profile`添加到`~/.xsession`或`~/.xinitrc`通过都达到以上目的（不同的登录管理器修改的文件不一样）。

*   若路径为`/usr/lib/xorg/modules/dri/fglrx_dri.so`,试着重装[catalyst](https://aur.archlinux.org/packages/catalyst/)包。

若错误信息为:

```
fglrx: libGL version undetermined - OpenGL module is using glapi fallback

```

可能是因为系统装了多个版本的`libGL.so`.下面的命令应该得到这样的回显:

 `$ locate libGL.s` 

```

/usr/lib/libGL.so
/usr/lib/libGL.so.1
/usr/lib/libGL.so.1.2
```

系统应只有3个libGL.so文件，若不止(例如`/usr/X11R6/lib/libGL.so.1.2`)，则将其删除。

若使用X11R7且系统中有下列文件，系统并不会给出任何错误提示，一定要将他们删除:

```
/usr/X11R6/lib/libGL.so.1.2
/usr/X11R6/lib/libGL.so.1

```

### 休眠问题

#### 视频播放不能从休眠状态中恢复

若启动了framebuffer，Catalyst不能从挂机状态中恢复。在[内核参数](/index.php/Kernel_parameters "Kernel parameters")中添加 `vga=0` 可禁用framebuffer。

其他加载器，参考[#禁用KMS](#.E7.A6.81.E7.94.A8KMS)。

### 系统冻结或硬件锁死

*   过去，`radeonfb`的framebuffer驱动很容易导致这个问题。若内核编译时启用对radeonfb的支持，应换内核看是否能解决此问题。

*   若退出桌面环境（关机、挂机和切换到tty等）时系统冻结，很可能忘记禁用KMS。(参见 [#禁用KMS](#.E7.A6.81.E7.94.A8KMS))

### 硬件冲突

当和某些版本的nForce3芯片组一起使用时，Radeon不能3D加速。目前虽还未找到具体原因，但有资料表明： indicate that it may be possible to get acceleration with this combination of hardware by booting with the drivers from 先用nVIDIA驱动启动到Windows然后再重启系统就可能获得3D加速。在root控制台使用下列命令可识别此问题(会得到与下列相似(使用基于nForce3系统)的输出:)：

 `$ dmesg | grep agp` 

```
     agpgart: Detected AGP bridge 0
     agpgart: Setting up Nforce3 AGP.
     agpgart: aperture base > 4G

```

或者还有下面的命令得到如下的回显:

 `$ tail -n 100 /var/log/Xorg.0.log | grep agp`  ` (EE) fglrx(0): [agp] unable to acquire AGP, error "xf86_ENODEV"` 

则就有问题。

有些资料说在某些情形下降级主板的BIOS可能有助于解决问题，但注意此方法并不是在各种情况下都适用，而且**方法不对则很可能让显卡报废。**

参考[这个错误报告](http://bugzilla.kernel.org/show_bug.cgi?id=6350)。

### 播放视频时系统短时间死机

使用Catalyst可导致此问题。

当用mplayer，若不定时出现几秒到几分钟的死机。查看日志，若有与下面相似的信息：

 `/var/log/messages.log` 

```
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<f8bc628c>] ? ip_firegl_ioctl+0x1c/0x30 [fglrx]
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium [<c0197038>] ? vfs_ioctl+0x78/0x90
Nov 28 18:31:56 pandemonium [<c01970b7>] ? do_vfs_ioctl+0x67/0x2f0
Nov 28 18:31:56 pandemonium [<c01973a6>] ? sys_ioctl+0x66/0x70
Nov 28 18:31:56 pandemonium [<c0103ef3>] ? sysenter_do_call+0x12/0x33
Nov 28 18:31:56 pandemonium [<c01c64a6>] ? proc_get_sb+0xc6/0x160
Nov 28 18:31:56 pandemonium =======================
```

给内核参数添加`nopat`和/或`nomodeset`到[内核参数](/index.php/Kernel_parameters "Kernel parameters")应该能行

### "aticonfig: No supported adaptaters detected"

若得到：

 `# aticonfig --initial` 

```
aticonfig: No supported adapters detected

```

可以在`etc/X11/xorg.conf`中设置device,或者复制以前的能工作的 `/etc/ati/control` 文件 (推荐 - 这也能解决水印的问题),这可能让Catalyst正常工作.

从AMD下载先前版本的fglrx,使用`--extract driver`参数运行. 文件将提取到`driver/common/etc/ati/control`. 用它覆盖原来的control文件后重启X. 你可以试试不同版本的.

设置型号的方法:在`/etc/X11/xorg.conf`将device段设置为:

 `/etc/X11/xorg.conf` 

```
Section "Device"
        Identifier "ATI radeon ********"
        Driver     "fglrx"
EndSection

```

此处`****`为设备型号(6870 for the HD 6870的显卡为6870，APU E-350为6310，通过网络是很容易查到的).

Xorg启动后很可能使用`amdcccle`而不是`aticonfig`。这里会有一个"AMD不支持硬件"水印。

用下面脚本可将此水印删除:

```
#!/bin/sh
DRIVER=/usr/lib/xorg/modules/drivers/fglrx_drv.so
for x in $(objdump -d $DRIVER|awk '/call/&&/EnableLogo/{print "\\x"$2"\\x"$3"\\x"$4"\\x"$5"\\x"$6}'); do
 sed -i "s/$x/\x90\x90\x90\x90\x90/g" $DRIVER
done

```

然后重启。

### 让chromium支持WebGL

在Google的Chromium/Chrome浏览器里，Linux的Catalyst驱动被列入了黑名单。参见 [Chromium#WebGL](/index.php/Chromium#WebGL "Chromium") .

### 用Adobe的flashplugin观看flash，画面迟滞或冻结

编辑:

 `/etc/adobe/mms.cfg` 

```
#EnableLinuxHWVideoDecode=1
OverrideGPUValidation=true
```

如果你使用KDE,请确保 系统设置->工作空间外观与行为->桌面效果->高级 里,"为全屏窗口挂起桌面特效" 没有勾选.

### GNOME3中移动窗口延迟/很慢

你可以试试这么做,有报告称大多数情况下此方法有效。

将下面行添加到`~/.profile`或`/etc/profile`:

```
export CLUTTER_VBLANK=none

```

重启X或操作系统。

### 在1920x1080分辨率下不能全屏(欠扫描,屏幕周围有黑边)

这经常会在使用HDMI连接显示器/电视时发生.

这似乎是AMD/ATI为适应所有HDTV的一项新功能,可以在amdccle中调整.

使用amdcccle(图形界面)你可以选择要修改的显示输出,将欠扫描设置成0% (aticonfig默认15%欠扫描). (至少)版本14.10有时也会出现显示调整的下面没有欠扫描的滑块的情况.(It is possible as well that the underscan slider won't show under the display's adjustments, as sometimes in (at least) version 14.10.)

这不是永久的配置,重启X,重启系统,挂起后唤醒甚至切换tty之后都会失效.

要使这成为永久配置的话,你需要以root身份在console下使用aticonfig来调整欠扫描设置,或者手动编辑 `/etc/ati/amdpcsdb` (也是以root身份)

**用aticonfig的方法:**

```
# aticonfig --set-pcs-u32=MCIL,DigitalHDTVDefaultUnderscan,0

```

改变设置后重启.

新版本的话(比如12.11), 要是ccc总不能保存过扫描设置,你可以试试:

```
# aticonfig --set-pcs-u32=MCIL,TVEnableOverscan,0

```

**手动编辑/etc/ati/amdpcsdb的方法:**

在 `[AMDPCSROOT/SYSTEM/MCIL]` 之下的任意位置添加

```
# DigitalHDTVDefaultUnderscan=V0

```

新版本的话(比如12.11), 要是ccc总不能保存过扫描设置,你可以试试: 在 `[AMDPCSROOT/SYSTEM/MCIL]` 之下找到这一行

```
# TVEnableOverscan=V1

```

然后把它变成

```
# TVEnableOverscan=V0

```

改变设置后重启.

**Note:** 也许你会发现,无论你怎么干,登录/注销/重启后, `/etc/ati/amdpcsdb` 总是被覆写/还原, 于是你的修改就不见了 _(:з」∠)_.(You might find that the file /etc/ati/amdpcsdb will be overwritten and revert no matter what you do as user or as root even with log in/log out/reboot, ergo the modification will not stick.)

所以你得在fglrx没运行的时候改它.

可以试着重启进入什么不需要运行fglrx的"安全模式"什么的,或者是直接进console模式

**应对措施:** 要是因某些原因你不想动ATI的配置文件,你可以设置面板的位置与分辨率来规避问题 以普通用户运行:

```
# aticonfig --set-dispattrib=DISPLAYTYPE,positionX:0
# aticonfig --set-dispattrib=DISPLAYTYPE,positionY:0
# aticonfig --set-dispattrib=DISPLAYTYPE,sizeX:1920
# aticonfig --set-dispattrib=DISPLAYTYPE,sizeY:1080

```

`DISPLAYTYPE`代表你想改的显示器,比如"dfp9". 用如下命令获得你的 `DISPLAYTYPE` :

```
# xrandr --current

```

如果没启用RandR的话,你可以用这个:

```
# aticonfig --query-monitor

```

也许需要用显示开关或 DISPLAY 变量来设置适当的显示/屏幕(比如 :0.1).

这将告诉你目前哪一个显示正连接着或断开着,以及它的详情

这个应对措施不是永久配置,不过是个让面板及上边内容看起来合适的方便快捷的方法

**Note:** 新版驱动不应再使用`aticonfig --set-pcs-val=MCIL,DigitalHDTVDefaultUnderscan,0`, ATI声明过这已被弃用并即将被移除.

用 `aticonfig --help | grep set-pcs-val` 来阅读ATI的说明.

### 双屏设置: 关于加速,OpenGL,合成,效能的一般问题

试着禁用 xinerama 和 xrandr12\. 如下:

输入:

```
# aticonfig --initial
# aticonfig --set-pcs-str="DDX,EnableRandR12,FALSE"

```

然后重启系统. 在 `/etc/X11/xorg.conf` 中检查 xinerama 是不是被禁用了, 如果没有,禁用它,然后重启系统.( In /etc/X11/xorg.conf check that xinerama is disabled, if it's not disable it and reboot your system. )

接下来运行`amdcccle`,如下: amdcccle→显示管理→多屏幕显示→以display(s) 2多屏显示桌面(amdcccle->display manager->multi-display->multidisplay desktop with display(s) 2\. ).

再次重启,再按你的想法设置显示.

### 禁用VariBright功能

[Vari-Bright](http://support.hp.com/vn-en/document/c02848104) 动态调整显示面板用电量以节能. 输入以下命令以禁用 VariBright:

```
# aticonfig --set-pcs-u32=MCIL,PP_UserVariBrightEnable,0

```

### Hybrid/PowerXpress: 关掉独立GPU

当你使用 [catalyst-total-pxp](https://aur.archlinux.org/packages/catalyst-total-pxp/) 或 catalyst-utils-pxp 时,你也许会发现切换到集成GPU时,独立GPU仍在工作,又耗电又使得系统温度很高.

对于集显是intel的话你可以通过 `vgaswitcheroo` 来关掉独立GPU. 不过很不幸有些时候不行...

然后这时你可以试试 [acpi_call](https://www.archlinux.org/packages/?name=acpi_call). MrDeepPurple准备好了脚本来完成这个任务.脚本在启动和恢复系统的时候通过systemd服务调用. 这是他的脚本:

```
#!/bin/sh
libglx=$(/usr/lib/fglrx/switchlibglx query)
modprobe acpi_call
if [ "$libglx" = "intel" ]; then
    echo '\_SB.PCI0.PEG0.PEGP._OFF' > /proc/acpi/call
fi

```

### 从X会话切换到TTY黑屏/低分辨率TTY

接受这个"功能"吧，这出现在catalys 13.2 beta，解决方法是使用`vga=`内核选项，比如`vga=792`。 使用

```
$ hwinfo --framebuffer

```

来得到支持的分辨率列表 选择最适合你的分辨率,粘贴到启动引导器的内核行,比如 `vga=0x03d4`

### 从X会话切换到TTY黑屏,背光并没有关闭

使用 [uvesafb](/index.php/Uvesafb "Uvesafb") 作为 framebuffer 驱动. 而且, `uvesafb` 可以为 TTY 设置任意分辨率.

### 切换TTY后切换回X会话时,只有一个带鼠标的黑屏

如果你遇到了这个bug的话,试着添加

```
Option      "XAANoOffscreenPixmaps" "true"

```

到你的 xorg.conf 的 'Device' 部分.

同时, 确认已安装有 [polkit 认证代理](/index.php/Polkit#Authentication_agents "Polkit") 并正在运行, 因为这种情况可能会在某程序想要请求密码但没有认证代理来显示密码对话框时出现.

### 30 FPS / Tear-Free / V-Sync bug

这个Bug发生于Catalyst 13.6 beta, 到现在(13.9)还没修复.

激活 "Tear Free"(防撕裂) 功能之后,所有新启动的OpenGL程序都出现延迟,常表现为只有30 FPS,复合桌面环境也是.("After enabling "Tear Free" functionality every freshly started OpenGL application is lagging, often generates only 30 FPS, it also touches composited desktop.")

M132找到一个解决方法.在 "AMD Catalyst Control Center" (amdcccle) 里完成这些操作:

```
1\. 开启 Tear-Free, 这将设置 3D V-Sync 为"总是开启".
2\. 设置 3D V-Sync 为"总是关闭".
3\. 确认 Tear-Free 仍为"开启".
4\. 重启X/重登录.

```

这在KDE 4.11.x下有效.M132的建议: "试着关闭 "Detect refresh rate" ,并为复合插件("Composite plugin")指定显示器刷新率."

### 背光调节不起效

如果你的背光调节有问题, 你可以试试:

```
# aticonfig --set-pcs-u32=MCIL,PP_PhmUseDummyBackEnd,1

```

一些用户报告说这导致FPS降低.要恢复默认的话:

```
# aticonfig --set-pcs-u32=MCIL,PP_PhmUseDummyBackEnd,0

```

[更多信息见此](http://ati.cchtml.com/show_bug.cgi?id=711)

### 使用 plasma 时 Chromium 出现毛刺(glitching)

添加 --disable-gpu 参数来启动 chromium, 比如,对 /usr/share/applications/chromium.desktop, 改成这样:

```
# cat /usr/share/applications/chromium.desktop | grep -i exec
Exec=chromium %U --disable-gpu

```

## 参见

*   [Unofficial Wiki for the ATI Linux Driver](http://wiki.cchtml.com/index.php/Main_Page)
*   [Unofficial ATI Linux Driver Bugzilla](http://ati.cchtml.com/query.cgi)