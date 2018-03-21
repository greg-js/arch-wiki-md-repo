相关文章

*   [KMS](/index.php/KMS "KMS")
*   [fbterm](/index.php/Fbterm "Fbterm")
*   [systemd](/index.php/Systemd "Systemd")

**翻译状态：** 本文是英文页面 [KMSCON](/index.php/KMSCON "KMSCON") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-04-26，点击[这里](https://wiki.archlinux.org/index.php?title=KMSCON&diff=0&oldid=464375)可以查看翻译后英文页面的改动。

来自 [project GitHub page](https://github.com/dvdhrm/kmscon) 的介绍：

	*Kmscon 是基于 KMS 的简单终端模拟软件。它试图为 VT 终端的内核实现提供一种用户空间终端实现。*

## Contents

*   [1 特性](#.E7.89.B9.E6.80.A7)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 中日韩文字支持](#.E4.B8.AD.E6.97.A5.E9.9F.A9.E6.96.87.E5.AD.97.E6.94.AF.E6.8C.81)
*   [4 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)

## 特性

KMSCON 能作为 Linux 内核内置终端的一个完整替代，它具有以下功能：

*   完整的 vt220 to vt510 实现。
*   完整的国际化支持：
    *   Kmscon 支持打印全部 Unicode 字符，包括中日韩文字。
    *   Kmscon 通过 libxkbcommon 对国际键盘布局提供支持，所以人们可以使用 X 支持的所有键盘布局。
*   硬件加速渲染。
*   Multi-seat capability.

**Note:** 要允许 root 用户通过 kmscon 登录，你需要移除或注释 `/etc/pam.d/login` 中的 `pam_securetty` 来停用这个模块。

## 安装

虽然名字里带有 KMS，kmscon 并非硬性依赖 KMS。Kmscon 支持的视频后端如下：fbdev（Linux fbdev 视频后端），drm2d（Linux DRM 软解后端），drm3d（Linux DRM 硬解后端）。请确保你的系统中有其中之一。

你可以从 [AUR](/index.php/AUR "AUR") 安装 [kmscon](https://aur.archlinux.org/packages/kmscon/) 或者 [kmscon-git](https://aur.archlinux.org/packages/kmscon-git/)。

出于保守的策略，你可以继续在 tty1 上使用传统的 getty 而只在其他虚拟终端上运行 kmscon ，或者你可以用 kmscon 替换 getty。

要在 tty1 上启用 kmscon:

```
# systemctl disable getty@tty1.service
# systemctl enable kmsconvt@tty1.service

```

重新启动即可生效。

要在所有的虚拟终端上启用 kmscon :

```
# ln -s /usr/lib/systemd/system/kmsconvt\@.service /etc/systemd/system/autovt\@.service

```

这使 [systemd](https://www.archlinux.org/packages/?name=systemd) 在每个虚拟终端上启动 kmscon 而不是 agetty，同时使 *systemd-logind* 使用 `kmsconvt@.service` 而不是 `getty@.service` 打开新的虚拟终端。不过使用 `getty@.service` 的 systemd 单元不受影响。

如果 *kmscon* 无法启动，它会尝试启动 `getty@.service` ，此外没有虚拟终端可用时这个单元不会启动。

**Warning:** 如果你在所有的终端替换了 getty ，请在重新启动之前确认 *kmscon* 可用 ！不然你只能用 Live CD 一类的介质恢复系统了。

## 中日韩文字支持

Kmscon 通过默认的字体引擎 [pango](https://www.archlinux.org/packages/?name=pango) 支持渲染中日韩文字。但是， 必须为 [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 设置全局配置，来将等宽字体映射到合适的中日韩字体上。我们为中文用户提供如下配置模板。此模板可以满足中文字体渲染要求：

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

## 疑难解答

*   如果你在切换 [Xorg](/index.php/Xorg "Xorg") 和 kmscon 时遇到问题，试着吧 `hwaccel` 添加到 `/etc/kmscon/kmscon.conf` 中。

这个文件和目录不在包内，因此你需要手动创建它们，或者你可以 [编辑 systemd 服务文件](/index.php/Systemd#Editing_provided_units "Systemd")。

```
 ExecStart=/usr/bin/kmscon "--vt=%I" --seats=seat0 --no-switchvt --font-name Terminus --font-size 12 --hwaccel --drm 

```

*   在版本 7 中，如果你不能控制声音，把你的用户添加到 **audio** [组](/index.php/Group "Group") 中。不过要注意这么做的缺点。（ [shortcomings](/index.php/Alsa#Installation "Alsa") ）