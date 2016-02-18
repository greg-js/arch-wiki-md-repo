**翻译状态：** 本文是英文页面 [KMSCON](/index.php/KMSCON "KMSCON") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-10-07，点击[这里](https://wiki.archlinux.org/index.php?title=KMSCON&diff=0&oldid=272485)可以查看翻译后英文页面的改动。

来自 [project GitHub page](https://github.com/dvdhrm/kmscon) 的介绍：

	*Kmscon 是基于 KMS 的简单终端模拟软件。它试图为 VT 终端的内核实现提供一种用户空间终端实现。*

## Contents

*   [1 特性](#.E7.89.B9.E6.80.A7)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 替换 linux 终端](#.E6.9B.BF.E6.8D.A2_linux_.E7.BB.88.E7.AB.AF)
*   [4 中日韩文字支持](#.E4.B8.AD.E6.97.A5.E9.9F.A9.E6.96.87.E5.AD.97.E6.94.AF.E6.8C.81)
*   [5 问题](#.E9.97.AE.E9.A2.98)

## 特性

Kmscon can function as a drop-in replacement for the in-kernel linux-console. Features include:

*   完整的 vt220 to vt510 实现。
*   完整的国际化支持：
    *   Kmscon 支持打印全部 Unicode 字符，包括中日韩文字。
    *   Kmscon 通过 libxkbcommon 对国际键盘布局提供支持，所以人们可以使用 X 支持的所有键盘布局。
*   硬件渲染加速。
*   Multi-seat capability.

**Note:** In order to be able to log into a kmscon console as root, you have to disable the `pam_securetty` module by removing or commenting out the corresponding line in `/etc/pam.d/login`.

## 安装

虽然名字里带有 DMS，kmscon 并非硬性依赖 DMS。 Kmscon 支持的视频后端如下： fbdev （Linux fbdev 视频后端）， drm2d （Linux DRM 软解后端）， drm3d （Linux DRM 硬解后端）。 只要你的系统安装其中之一就行。

你可以从[官方仓库](/index.php/Official_repositories "Official repositories")安装 [kmscon](https://www.archlinux.org/packages/?name=kmscon) 也可以从 [AUR](/index.php/AUR "AUR") 安装 [kmscon-git](https://aur.archlinux.org/packages/kmscon-git/)。

## 替换 linux 终端

切换到 root，执行：

```
# ln -s /usr/lib/systemd/system/kmsconvt\@.service /etc/systemd/system/autovt\@.service
# systemctl enable kmsconvt\@.service

```

上述操作使 [systemd](https://www.archlinux.org/packages/?name=systemd) 使用 kmscon 而非 agetty 创建每一个虚拟终端（VT）。如果 mkscon 因为什么情况启动失败的话， agetty 会被启动。

## 中日韩文字支持

Kmscon 通过默认的字体引擎 [pango](https://www.archlinux.org/packages/?name=pango) 支持渲染中日韩文字。但是， 必须为 [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 设置全局配置，来将等款字帖映射到合适的中日韩字体上。我们为中文用户提供如下配置模板。此模板可以满足中文字体渲染要求：

 `/etc/fonts/conf.d/99-kmscon.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
<match>
        <test name="family"><string>monospace</string></test>
        <edit name="family" mode="prepend" binding="strong">
                <string>DejaVu Sans Mono</string>
                <string>WenQuanYi Micro Hei Mono</string>
        </edit>
</match>
</fontconfig>

```

你需要安装 [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) 和 [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei)，它们都可以在官方仓库中找到。

## 问题

*   You may want to add `--hwaccel --drm` to ExecStart if you have problems with switching between [Xorg](/index.php/Xorg "Xorg") and kmscon.

```
 ExecStart=/usr/bin/kmscon "--vt=%I" --seats=seat0 --no-switchvt --font-name Terminus --font-size 12 --hwaccel --drm

```

*   As version 7, if you cannot control the audio, add your user to **audio** [group](/index.php/Users_and_groups#Group_management "Users and groups"). Be aware of th [shortcomings](/index.php/Alsa#Installation "Alsa") of this choice.