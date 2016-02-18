**翻译状态：** 本文是英文页面 [Chromium](/index.php/Chromium "Chromium") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-03-10，点击[这里](https://wiki.archlinux.org/index.php?title=Chromium&diff=0&oldid=362695)可以查看翻译后英文页面的改动。

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
    *   [3.4 Force 3D acceleration in Flash Player and the browser](#Force_3D_acceleration_in_Flash_Player_and_the_browser)
    *   [3.5 代理设置](#.E4.BB.A3.E7.90.86.E8.AE.BE.E7.BD.AE)
    *   [3.6 WebGL](#WebGL)
    *   [3.7 Google Play and Flash](#Google_Play_and_Flash)
    *   [3.8 Force 3D acceleration in Pepper Flash Player and i.g. the browser with radeon driver](#Force_3D_acceleration_in_Pepper_Flash_Player_and_i.g._the_browser_with_radeon_driver)
    *   [3.9 Asian characters not displayed with language set to English](#Asian_characters_not_displayed_with_language_set_to_English)
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

默认浏览器通过[xdg-open](/index.php/Xdg-open "Xdg-open")设置，详情请参阅[xdg-open#set the default browser](/index.php/Xdg-open#set_the_default_browser "Xdg-open") 和 [Default applications](/index.php/Default_applications "Default applications")。

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

chrome 及 chromium 在中文环境下使用可能会极其卡顿，原因在于Google Chrome UI 的缺省字体继承自 Gnome 桌面设置（而不是 chrome://settings/）, 地址栏弹出框的缺省字体也是继承自 Gnome 桌面设置。字体名称的标准名称和本地化名称不相同导致了 Skia 缓存无法命中。Skia 缓存无法命中导致 fontconfig 频繁被调用， 而该调用非常消耗 CPU 时间，导致chrome卡顿。 所以解决方法就是不要使用文泉驿系列字体，使用非中文名字的字体。

### PDF 插件中的字体问题

安装软件包 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 可以解决一些 PDF 的字体显示问题，不然的话替代字体会显示成其他的文字。[reported on the chromium bug 报告](https://code.google.com/p/chromium/issues/detail?id=369991).

### Force 3D acceleration in Flash Player and the browser

**Warning:** Disabling the rendering list may cause unstable behaviour, including crashes of the host. See the bug reports in `chrome://gpu`.

First, make sure you have all the required packages as explained in [VDPAU](/index.php/VDPAU "VDPAU"). Then, to force 3D rendering *enable* the flag "Override software rendering list" in `chrome://flags`. Check if it is working in `chrome://gpu`. This may also alleviate tearing issues with the [radeon](/index.php/Radeon "Radeon") driver.

### 代理设置

许多情况下代理设置无法正常工作，尤其是在 KDE 界面中。解决方法是使用Chromium的命令行选项例如`--proxy-pac-url` 和 `--proxy-server`进行代理设置。

### WebGL

有时 Chromium 会在某些显卡配置中禁用 WebGL，可以通过URL中输入`about:flags`，然后启用 WebGL. 通过命令行 `--enable-webgl` 选项也能启用它。

有可能 Chromium 把你的显卡列入了黑名单，如果是这样，可以通过`--ignore-gpu-blacklist`选项禁用黑名单。或者在`about:flags` 中启用 *Override software rendering list*.

### Google Play and Flash

DRM content on Flash still requires HAL to play. This is readily apparent with Google Play Movies. If one attempts to play a Google Play movie without HAL, they will receive a YouTube-like screen, but the video will not play. See [Flash DRM content](/index.php/Flash_DRM_content "Flash DRM content") for more information.

### Force 3D acceleration in Pepper Flash Player and i.g. the browser with radeon driver

First, make sure you have all the required packages as explained in [VDPAU](/index.php/VDPAU "VDPAU"). Then, to force 3D rendering *enable* the flag "Override software rendering list" in `chrome://flags`. Check if it is working in `chrome://gpu`.

### Asian characters not displayed with language set to English

This is a known issue with all Chromium versions up to v42\. [[1]](https://code.google.com/p/chromium/issues/detail?id=7160) As a workaround, install fonts separately: [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai), [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) and [ttf-unfonts-core](https://aur.archlinux.org/packages/ttf-unfonts-core/). [[2]](http://superuser.com/questions/192704/why-cant-my-chromium-display-japanese-characters)

## 资源

*   [Chromium 主页](http://www.chromium.org/Home)
*   [Differences from Google Chrome](https://en.wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "wikipedia:Chromium (web browser)")
*   [Announcements and release notes for the Google Chrome browser](http://googlechromereleases.blogspot.com/)