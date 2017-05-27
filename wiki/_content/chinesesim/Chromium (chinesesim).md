**翻译状态：** 本文是英文页面 [Chromium](/index.php/Chromium "Chromium") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-02，点击[这里](https://wiki.archlinux.org/index.php?title=Chromium&diff=0&oldid=447735)可以查看翻译后英文页面的改动。

[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) 是一款来自 "The Chromium Project" 的开源图形网络浏览器，基于 [WebKit](https://en.wikipedia.org/wiki/WebKit "wikipedia:WebKit")渲染引擎。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 设置成默认浏览器](#.E8.AE.BE.E7.BD.AE.E6.88.90.E9.BB.98.E8.AE.A4.E6.B5.8F.E8.A7.88.E5.99.A8)
    *   [2.2 Flash播放器](#Flash.E6.92.AD.E6.94.BE.E5.99.A8)
    *   [2.3 Widevine Content Decryption Module plugin](#Widevine_Content_Decryption_Module_plugin)
    *   [2.4 在Chromium中打开pdf文件](#.E5.9C.A8Chromium.E4.B8.AD.E6.89.93.E5.BC.80pdf.E6.96.87.E4.BB.B6)
    *   [2.5 证书管理](#.E8.AF.81.E4.B9.A6.E7.AE.A1.E7.90.86)
*   [3 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [3.1 字体](#.E5.AD.97.E4.BD.93)
    *   [3.2 卡顿](#.E5.8D.A1.E9.A1.BF)
    *   [3.3 PDF 插件中的字体问题](#PDF_.E6.8F.92.E4.BB.B6.E4.B8.AD.E7.9A.84.E5.AD.97.E4.BD.93.E9.97.AE.E9.A2.98)
    *   [3.4 在浏览器和Flash播放器插件强制使用3D加速功能](#.E5.9C.A8.E6.B5.8F.E8.A7.88.E5.99.A8.E5.92.8CFlash.E6.92.AD.E6.94.BE.E5.99.A8.E6.8F.92.E4.BB.B6.E5.BC.BA.E5.88.B6.E4.BD.BF.E7.94.A83D.E5.8A.A0.E9.80.9F.E5.8A.9F.E8.83.BD)
    *   [3.5 WebGL](#WebGL)
    *   [3.6 界面混乱](#.E7.95.8C.E9.9D.A2.E6.B7.B7.E4.B9.B1)
*   [4 资源](#.E8.B5.84.E6.BA.90)

## 安装

稳定版的 Chromium, 可以[安装](/index.php/Pacman "Pacman") 软件包 [chromium](https://www.archlinux.org/packages/?name=chromium)。

其它版本：

*   **Chromium Beta Channel** — 测试版本

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=chromium-beta)</small>

*   **Chromium Dev Channel** — 开发版本

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/)

*   **Chromium snapshot builds** — 未经测试的每日构建版本

	[https://build.chromium.org/](https://build.chromium.org/) || [chromium-snapshot-bin](https://aur.archlinux.org/packages/chromium-snapshot-bin/)

*   **Chromium with [VA-API](/index.php/VA-API "VA-API") support** — 增加了启用 VA-API 的补丁

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/)

[AUR](/index.php/AUR "AUR")中还有包含 Flash Player 和 Widevine [EME](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions "wikipedia:Encrypted Media Extensions")(支持 Netflix)的二进制版的[google-chrome](https://aur.archlinux.org/packages/google-chrome/) 和

*   **Google Chrome Beta Channel** — 测试版本

	[https://www.google.com/chrome](https://www.google.com/chrome) || [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)

*   **Google Chrome Dev Channel** — 开发版本

	[https://www.google.com/chrome](https://www.google.com/chrome) || [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)

**Note:** Google Chrome 停止了 32 位支持，仅支持 64 位安装。

在[Chromium 与 Chrome 比较](https://code.google.com/p/chromium/wiki/ChromiumBrowserVsGoogleChrome) 可以查看Chromium vs Chrome和版本号的区别。

[List of applications#Blink-based](/index.php/List_of_applications#Blink-based "List of applications") 还列出了基于 Blink 的浏览器.

## 配置

### 设置成默认浏览器

要讲 Chromium 设置成默认浏览器或设置下载文件的打开方式，请参阅 [Default applications](/index.php/Default_applications "Default applications")。

### Flash播放器

**注意:** Chromium 不再支持 Netscape plugin API (NPAPI)，[flashplugin](https://www.archlinux.org/packages/?name=flashplugin) 已经无法工作。

可以使用 Google Chrome (新Pepper API)提供的 Flash.

*Pepper Flash* 是使用了新的 Pepper plugin API 的 Flash Player 插件。要在 Chromium 中使用，可以从包[pepper-flash](https://aur.archlinux.org/packages/pepper-flash/)来安装。

添加以下内容 (请将版本号替换为当前最新版本) 到`~/.config/chrome-dev-flags.conf`.

```
--ppapi-flash-path=/usr/lib/PepperFlash/libpepflashplayer.so --ppapi-flash-version=25.0.0.171

```

并且要在`chrome://settings/content`中启用Flash。

### Widevine Content Decryption Module plugin

Widevine is Google's Encrypted Media Extensions (EME) Content Decryption Module (CDM). It is used to watch premium video content such as Netflix. It comes bundled with Chrome.

To install the Widevine CDM for Chromium, install the [chromium-widevine](https://aur.archlinux.org/packages/chromium-widevine/) package.

Make sure the plugin is enabled in `chrome://plugins`.

### 在Chromium中打开pdf文件

Chromium 和 Google Chrome 已经内置了 *Chromium PDF Viewer* 插件，所以不需要再安装其它三方插件。如果不plugin, so installing a third-party plugin is not required.要使用 pdf.js, 请先在 `chrome://plugins` 中禁用 *Chromium PDF Viewer* ，然后参考 [Browser plugins#PDF.js](/index.php/Browser_plugins#PDF.js "Browser plugins") 进行设置。

### 证书管理

Chromium 使用 [NSS](/index.php/Nss "Nss") 管理证书，可以通过`Settings` → `Show advanced settings...` → `Manage Certificates...` 设置。

## 疑难解答

### 字体

**Note:** Chromium does not fully integrate with fontconfig/GTK/Pango/X/etc. due to its sandbox. For more information, see the [Linux Technical FAQ](https://dev.chromium.org/developers/linux-technical-faq).

### 卡顿

chrome 及 chromium 在中文环境下使用可能会极其卡顿，原因在于Google Chrome UI 的缺省字体继承自 Gnome 桌面设置（而不是 chrome://settings/）, 地址栏弹出框的缺省字体也是继承自 Gnome 桌面设置。字体名称的标准名称和本地化名称不相同导致了 Skia 缓存无法命中。Skia 缓存无法命中导致 fontconfig 频繁被调用， 而该调用非常消耗 CPU 时间，导致chrome卡顿。因此不要使用文泉驿这样拥有本地化名称的字体，推荐使用Noto Sans CJK系列字体。

AdBlock Plus 最近系列版本占用明显增大，也可能导致卡顿，建议换用ublock origin来减少占用，对于一些低配置电脑效果明显。

### PDF 插件中的字体问题

安装软件包 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 可以解决一些 PDF 的字体显示问题，不然的话替代字体会显示成其他的文字。[reported on the chromium bug 报告](https://code.google.com/p/chromium/issues/detail?id=369991).

### 在浏览器和Flash播放器插件强制使用3D加速功能

**警告:** 禁用渲染列表可能会导致包括主机崩溃在内的不稳定的行为。你可以在这里看到Bug报告`chrome://gpu`.

首先，确认你已经安装了所有已经在 [VDPAU](/index.php/VDPAU "VDPAU") 中列出的包。然后，在 `chrome://flags` 中将 "Override software rendering list" 设置为 *enable*。你可以在 `chrome://gpu` 中检查设置是否起效。这也可能会减少 [radeon](/index.php/Radeon "Radeon") 驱动的画面撕裂问题。

### WebGL

有时 Chromium 会在某些显卡配置中禁用 WebGL，可以通过URL中输入`about:flags`，然后启用 WebGL. 通过命令行 `--enable-webgl` 选项也能启用它。

有可能 Chromium 把你的显卡列入了黑名单，如果是这样，可以通过`--ignore-gpu-blacklist`选项禁用黑名单。或者在`about:flags` 中启用 *Override software rendering list*.

### 界面混乱

Chromium 的图形界面可能在高分屏上显示异常，可以使用 `--force-device-scale-factor=1` 选项禁用按设备 DPI 缩放。

## 资源

*   [Chromium 主页](http://www.chromium.org/Home)
*   [Differences from Google Chrome](https://en.wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "wikipedia:Chromium (web browser)")
*   [Announcements and release notes for the Google Chrome browser](http://googlechromereleases.blogspot.com/)