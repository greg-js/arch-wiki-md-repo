**翻译状态：** 本文是英文页面 [Chromium](/index.php/Chromium "Chromium") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-03-22，点击[这里](https://wiki.archlinux.org/index.php?title=Chromium&diff=0&oldid=362695)可以查看翻译后英文页面的改动。

[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) 是一款来自Google的开源图形网络浏览器，基于 [WebKit](https://en.wikipedia.org/wiki/WebKit "wikipedia:WebKit")渲染引擎。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 设置成默认浏览器](#.E8.AE.BE.E7.BD.AE.E6.88.90.E9.BB.98.E8.AE.A4.E6.B5.8F.E8.A7.88.E5.99.A8)
    *   [2.2 文件关联](#.E6.96.87.E4.BB.B6.E5.85.B3.E8.81.94)
    *   [2.3 Flash播放器](#Flash.E6.92.AD.E6.94.BE.E5.99.A8)
    *   [2.4 在Chromium中打开pdf文件](#.E5.9C.A8Chromium.E4.B8.AD.E6.89.93.E5.BC.80pdf.E6.96.87.E4.BB.B6)
        *   [2.4.1 libpdf](#libpdf)
        *   [2.4.2 PDF.js](#PDF.js)
    *   [2.5 证书管理](#.E8.AF.81.E4.B9.A6.E7.AE.A1.E7.90.86)
*   [3 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [3.1 杂音](#.E6.9D.82.E9.9F.B3)
    *   [3.2 卡顿](#.E5.8D.A1.E9.A1.BF)
    *   [3.3 PDF 插件中的字体问题](#PDF_.E6.8F.92.E4.BB.B6.E4.B8.AD.E7.9A.84.E5.AD.97.E4.BD.93.E9.97.AE.E9.A2.98)
    *   [3.4 在浏览器和Flash播放器插件强制使用3D加速功能](#.E5.9C.A8.E6.B5.8F.E8.A7.88.E5.99.A8.E5.92.8CFlash.E6.92.AD.E6.94.BE.E5.99.A8.E6.8F.92.E4.BB.B6.E5.BC.BA.E5.88.B6.E4.BD.BF.E7.94.A83D.E5.8A.A0.E9.80.9F.E5.8A.9F.E8.83.BD)
    *   [3.5 代理设置](#.E4.BB.A3.E7.90.86.E8.AE.BE.E7.BD.AE)
    *   [3.6 WebGL](#WebGL)
    *   [3.7 Google Play 与 Flash](#Google_Play_.E4.B8.8E_Flash)
    *   [3.8 当语言被设置为英语时，亚洲字符不能正确的被显示的问题](#.E5.BD.93.E8.AF.AD.E8.A8.80.E8.A2.AB.E8.AE.BE.E7.BD.AE.E4.B8.BA.E8.8B.B1.E8.AF.AD.E6.97.B6.EF.BC.8C.E4.BA.9A.E6.B4.B2.E5.AD.97.E7.AC.A6.E4.B8.8D.E8.83.BD.E6.AD.A3.E7.A1.AE.E7.9A.84.E8.A2.AB.E6.98.BE.E7.A4.BA.E7.9A.84.E9.97.AE.E9.A2.98)
*   [4 资源](#.E8.B5.84.E6.BA.90)

## 安装

稳定版的 Chromium 位于 [官方源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 可以直接[安装](/index.php/Pacman "Pacman") [chromium](https://www.archlinux.org/packages/?name=chromium)。

[AUR](/index.php/Arch_User_Repository "Arch User Repository")中可以找到

*   [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/) - 开发版本
*   [chromium-browser-bin](https://aur.archlinux.org/packages/chromium-browser-bin/) - 二进制版本

**注意:** 完整的编译 [Chromium-dev](https://aur.archlinux.org/packages/Chromium-dev/) 至少要花费编译Linux内核一样长的时间。

[AUR](/index.php/AUR "AUR")中还有包含 Flash Player 的二进制版的[google-chrome](https://aur.archlinux.org/packages/google-chrome/) 和

*   [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)
*   [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)

在[Chromium 与 Chrome 比较](https://code.google.com/p/chromium/wiki/ChromiumBrowserVsGoogleChrome) 可以查看Chromium vs Chrome和版本号的区别。

## 配置

### 设置成默认浏览器

默认浏览器通过[xdg-open](/index.php/Xdg-open "Xdg-open")设置，详情请参阅[xdg-open#Set the default browser](/index.php/Xdg-open#Set_the_default_browser "Xdg-open") 和 [Default applications](/index.php/Default_applications "Default applications")。

更多信息请阅读 [Xdg-open](/index.php/Xdg-open "Xdg-open")。

### 文件关联

Chromium 依赖[xdg-open](/index.php/Xdg-open "Xdg-open")打开文件和链接,详情参阅[xdg-open#Configuration](/index.php/Xdg-open#Configuration "Xdg-open")和[默认程序](/index.php/Default_applications "Default applications").

### Flash播放器

**注意:** Chromium 不再支持 Netscape plugin API (NPAPI)，[flashplugin](https://www.archlinux.org/packages/?name=flashplugin) 已经无法工作。

可以使用 Google Chrome (新Pepper API)提供的 Flash.

可以通过[AUR](/index.php/AUR "AUR")中提供的软件包进行安装:

*   [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/) - 稳定版本
*   [chromium-pepper-flash-dev](https://aur.archlinux.org/packages/chromium-pepper-flash-dev/) - 开发版本

请在`chrome://plugins`中启用 `/usr/lib/PepperFlash/libpepflashplayer.so`.

### 在Chromium中打开pdf文件

有多种方法可以实现：

#### libpdf

libpdf是谷歌自己的 pdf 查看工具，从 Chromium V37 中开始包含。

#### PDF.js

请参考 [Browser plugins#PDF.js](/index.php/Browser_plugins#PDF.js "Browser plugins")

### 证书管理

Chromium 使用 [NSS](/index.php/Nss "Nss") 管理证书，可以通过`Settings` → `Show advanced settings...` → `Manage Certificates...` 设置。

## 疑难解答

### 杂音

如果在使用 HDMI 的时候出现杂音，可以试下增大声音缓存的大小：

```
$ chromium --audio-buffer-size=2048

```

### 卡顿

chrome 及 chromium 在中文环境下使用可能会极其卡顿，原因在于Google Chrome UI 的缺省字体继承自 Gnome 桌面设置（而不是 chrome://settings/）, 地址栏弹出框的缺省字体也是继承自 Gnome 桌面设置。字体名称的标准名称和本地化名称不相同导致了 Skia 缓存无法命中。Skia 缓存无法命中导致 fontconfig 频繁被调用， 而该调用非常消耗 CPU 时间，导致chrome卡顿。因此不要使用文泉驿这样拥有本地化名称的字体，推荐使用Noto Sans CJK系列字体。

AdBlock Plus 最近系列版本占用明显增大，也可能导致卡顿，建议换用ublock origin来减少占用，对于一些低配置电脑效果明显。

### PDF 插件中的字体问题

安装软件包 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 可以解决一些 PDF 的字体显示问题，不然的话替代字体会显示成其他的文字。[reported on the chromium bug 报告](https://code.google.com/p/chromium/issues/detail?id=369991).

### 在浏览器和Flash播放器插件强制使用3D加速功能

**警告:** 禁用渲染列表可能会导致包括主机崩溃在内的不稳定的行为。你可以在这里看到Bug报告`chrome://gpu`.

首先，确认你已经安装了所有已经在 [VDPAU](/index.php/VDPAU "VDPAU") 中列出的包。然后，在 `chrome://flags` 中将 "Override software rendering list" 设置为 *enable*。你可以在 `chrome://gpu` 中检查设置是否起效。这也可能会减少 [radeon](/index.php/Radeon "Radeon") 驱动的画面撕裂问题。

### 代理设置

许多情况下代理设置无法正常工作，尤其是在 KDE 界面中。解决方法是使用Chromium的命令行选项例如`--proxy-pac-url` 和 `--proxy-server`进行代理设置。

### WebGL

有时 Chromium 会在某些显卡配置中禁用 WebGL，可以通过URL中输入`about:flags`，然后启用 WebGL. 通过命令行 `--enable-webgl` 选项也能启用它。

有可能 Chromium 把你的显卡列入了黑名单，如果是这样，可以通过`--ignore-gpu-blacklist`选项禁用黑名单。或者在`about:flags` 中启用 *Override software rendering list*.

### Google Play 与 Flash

Flash 中的 DRM 内容需要 HAL 才能够正常播放。 通过 Google Play Movies 可以很快体现出这一点. 如果有人尝试在没有HAL的情况下播放一个 Google Play 上的电影，那么他就会见到一个类似于 YouTube 的播放界面，但是视频却并不会被播放。查看 [Flash DRM content](/index.php/Flash_DRM_content "Flash DRM content") 以获取更多信息。

### 当语言被设置为英语时，亚洲字符不能正确的被显示的问题

这是一个已知的存在于 Chromium v42版本之前的问题。 [[1]](https://code.google.com/p/chromium/issues/detail?id=7160) 为了解决这个问题, 请分别安装字体: [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai)， [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) 和 [ttf-unfonts-core](https://aur.archlinux.org/packages/ttf-unfonts-core/)。 [[2]](http://superuser.com/questions/192704/why-cant-my-chromium-display-japanese-characters)

## 资源

*   [Chromium 主页](http://www.chromium.org/Home)
*   [Differences from Google Chrome](https://en.wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "wikipedia:Chromium (web browser)")
*   [Announcements and release notes for the Google Chrome browser](http://googlechromereleases.blogspot.com/)