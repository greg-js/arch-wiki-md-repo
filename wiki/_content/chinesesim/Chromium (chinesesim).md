相关文章

*   [Chromium Tips and Tweaks (简体中文)](/index.php/Chromium_Tips_and_Tweaks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium Tips and Tweaks (简体中文)")
*   [Browser Plugins (简体中文)](/index.php/Browser_Plugins_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Browser Plugins (简体中文)")
*   [Firefox (简体中文)](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)")
*   [Opera](/index.php/Opera "Opera")

**翻译状态：** 本文是英文页面 [Chromium](/index.php/Chromium "Chromium") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-12-04，点击[这里](https://wiki.archlinux.org/index.php?title=Chromium&diff=0&oldid=496319)可以查看翻译后英文页面的改动。

[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) 是一款来自 "The Chromium Project" 的开源图形网络浏览器，基于 [Blink](https://en.wikipedia.org/wiki/Blink_(web_engine) 渲染引擎。

## Contents

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 设置成默认浏览器](#设置成默认浏览器)
    *   [2.2 Flash播放器](#Flash播放器)
    *   [2.3 Widevine内容解密插件](#Widevine内容解密插件)
    *   [2.4 在Chromium中打开pdf文件](#在Chromium中打开pdf文件)
    *   [2.5 证书管理](#证书管理)
*   [3 提示和技巧](#提示和技巧)
*   [4 疑难解答](#疑难解答)
    *   [4.1 字体](#字体)
    *   [4.2 PDF 插件中的字体问题](#PDF_插件中的字体问题)
    *   [4.3 在浏览器和Flash播放器插件强制使用3D加速功能](#在浏览器和Flash播放器插件强制使用3D加速功能)
    *   [4.4 WebGL](#WebGL)
    *   [4.5 界面混乱](#界面混乱)
*   [5 资源](#资源)

## 安装

稳定版的 Chromium, 可以[安装](/index.php/Pacman "Pacman") 软件包 [chromium](https://www.archlinux.org/packages/?name=chromium)。要使用打印功能，请参考 [Gtk#Printers not shown in the GTK print dialog](/index.php/Gtk#Printers_not_shown_in_the_GTK_print_dialog "Gtk").

其它版本：

*   **Chromium Beta Channel** — 测试版本

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=chromium-beta)</small>

*   **Chromium Dev Channel** — 开发版本

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/)

*   **Chromium snapshot builds** — 未经测试的每日构建版本

	[https://build.chromium.org/](https://build.chromium.org/) || [chromium-snapshot-bin](https://aur.archlinux.org/packages/chromium-snapshot-bin/)

*   **Chromium with [VA-API](/index.php/VA-API "VA-API") support** — 增加了启用 VA-API 的补丁

	[https://chromium-review.googlesource.com/c/chromium/src/+/532294](https://chromium-review.googlesource.com/c/chromium/src/+/532294) || [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/)

[AUR](/index.php/AUR "AUR")中还有包含 Flash Player 和 Widevine [EME](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions "wikipedia:Encrypted Media Extensions")(支持 Netflix)的二进制版的[google-chrome](https://aur.archlinux.org/packages/google-chrome/) 和

*   **Google Chrome Beta Channel** — 测试版本

	[https://www.google.com/chrome](https://www.google.com/chrome) || [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)

*   **Google Chrome Dev Channel** — 开发版本

	[https://www.google.com/chrome](https://www.google.com/chrome) || [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)

**Note:** 从 54 版本开始，本地客户端支持 (NaCl) 功能已经被 [chromium](https://www.archlinux.org/packages/?name=chromium) 移除，打开 NaCl 程序会显示错误: "This plugin is not supported". [google-chrome](https://aur.archlinux.org/packages/google-chrome/) 软件包支持 NaCl.

在[Chromium 与 Chrome 比较](https://code.google.com/p/chromium/wiki/ChromiumBrowserVsGoogleChrome) 可以查看Chromium vs Chrome和版本号的区别。

[List of applications#Blink-based](/index.php/List_of_applications#Blink-based "List of applications") 还列出了基于 Blink 的浏览器.

## 配置

### 设置成默认浏览器

要讲 Chromium 设置成默认浏览器或设置下载文件的打开方式，请参阅 [Default applications](/index.php/Default_applications "Default applications")。

### Flash播放器

使用 Google Chrome 时会自动安装 Flash 播放器。

要在 Chromium 中使用，可以安装软件包 [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash)。

并且要在`chrome://settings/content`中启用Flash。

### Widevine内容解密插件

Widevine 是 Google 的 Encrypted Media Extensions (媒体加密拓建，即EME) 内容解密组件。它用来看 Netflix 这一类的付费的视频内容，并已经内置在Chrome中。

要安装 Chromium 的 Widevine CDM，安装 [chromium-widevine](https://aur.archlinux.org/packages/chromium-widevine/) 软件包。

请启用 `chrome://settings/content/protectedContent` 中的 *Allow sites to play protected content*。

### 在Chromium中打开pdf文件

Chromium 和 Google Chrome 已经内置了 *Chromium PDF Viewer* 插件，所以不需要再安装其它三方插件。如果不要使用 pdf.js, 请先在 `chrome://plugins` 中禁用 *Chromium PDF Viewer*。

### 证书管理

Chromium 使用 [NSS](/index.php/Network_Security_Services "Network Security Services") 管理证书，可以通过`chrome://settings/certificates`.设置。

## 提示和技巧

见主要文章: [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks")。

## 疑难解答

### 字体

**Note:** Chromium does not fully integrate with fontconfig/GTK/Pango/X/etc. due to its sandbox. For more information, see the [Linux Technical FAQ](https://dev.chromium.org/developers/linux-technical-faq).

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