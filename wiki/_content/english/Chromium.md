[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) is an open-source graphical web browser from "The Chromium Project", based on the [Blink](https://en.wikipedia.org/wiki/Blink_(layout_engine) rendering engine.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default applications](#Default_applications)
    *   [2.2 Flash Player plugin](#Flash_Player_plugin)
    *   [2.3 Widevine Content Decryption Module plugin](#Widevine_Content_Decryption_Module_plugin)
    *   [2.4 PDF viewer plugin](#PDF_viewer_plugin)
        *   [2.4.1 PDF.js](#PDF.js)
    *   [2.5 Certificates](#Certificates)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Constant freezes under KDE](#Constant_freezes_under_KDE)
    *   [4.2 Fonts](#Fonts)
        *   [4.2.1 Font rendering issues in PDF plugin](#Font_rendering_issues_in_PDF_plugin)
    *   [4.3 Force 3D acceleration](#Force_3D_acceleration)
    *   [4.4 WebGL](#WebGL)
    *   [4.5 Distorted GUI](#Distorted_GUI)
*   [5 See also](#See_also)

## Installation

The open-source project, **Chromium**, can be [installed](/index.php/Install "Install") with the [chromium](https://www.archlinux.org/packages/?name=chromium) package.

Other alternatives include:

*   **Chromium Beta Channel** — the beta version

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=chromium-beta)</small>

*   **Chromium Dev Channel** — the development version

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/)

*   **Chromium snapshot builds** — the untested nightly version

	[https://build.chromium.org/](https://build.chromium.org/) || [chromium-snapshot-bin](https://aur.archlinux.org/packages/chromium-snapshot-bin/)

*   **Chromium with [VA-API](/index.php/VA-API "VA-API") support** — with a patch to enable VA-API

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/)

The derived browser, **Google Chrome**, bundled with Flash Player and Widevine [EME](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions "wikipedia:Encrypted Media Extensions") (for e.g. Netflix), can be [installed](/index.php/Install "Install") with the [google-chrome](https://aur.archlinux.org/packages/google-chrome/) package.

Other alternatives include:

*   **Google Chrome Beta Channel** — the beta version

	[https://www.google.com/chrome](https://www.google.com/chrome) || [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)

*   **Google Chrome Dev Channel** — the development version

	[https://www.google.com/chrome](https://www.google.com/chrome) || [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)

**Note:** Google Chrome dropped 32 bits support, and only supports 64 bits installation

See these [two](https://chromium.googlesource.com/chromium/src/+/master/docs/chromium_browser_vs_google_chrome.md) [articles](http://news.softpedia.com/news/Google-Chrome-vs-Chromium-Understanding-Stable-Beta-Dev-Releases-and-Version-No-140060.shtml) for an explanation of the differences between Stable/Beta/Dev, as well as Chromium vs. Chrome and an explanation of the version numbering.

On top of the different Chromium build channels, a number of forks exist with more or less special features; see [List of applications#Blink-based](/index.php/List_of_applications#Blink-based "List of applications").

## Configuration

### Default applications

To set Chromium as the default browser and to change which applications Chromium launches when opening downloaded files, see [default applications](/index.php/Default_applications "Default applications").

### Flash Player plugin

**Note:** Chromium no longer supports the Netscape plugin API (NPAPI), so [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) from the repositories cannot be used.

*Pepper Flash* is the Flash Player plugin, using the new Pepper plugin API. It is co-developed by Google and Adobe, and distributed bundled with Google Chrome.

To install Pepper Flash for Chromium, install the [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/) package. If you want the development version, install the [chromium-pepper-flash-dev](https://aur.archlinux.org/packages/chromium-pepper-flash-dev/) package instead.

Make sure the plugin is enabled in `chrome://plugins` and restart chromium via its menu.

### Widevine Content Decryption Module plugin

Widevine is Google's Encrypted Media Extensions (EME) Content Decryption Module (CDM). It is used to watch premium video content such as Netflix. It comes bundled with Chrome.

To install the Widevine CDM for Chromium, install the [chromium-widevine](https://aur.archlinux.org/packages/chromium-widevine/) package.

Make sure the plugin is enabled in `chrome://plugins`.

### PDF viewer plugin

Chromium and Google Chrome are bundled with the *Chromium PDF Viewer* plugin, so installing a third-party plugin is not required.

If you prefer another implementation, disable the *Chromium PDF Viewer* plugin in `chrome://plugins`, and install one of the following alternatives:

#### PDF.js

See the main article: [Browser plugins#PDF.js](/index.php/Browser_plugins#PDF.js "Browser plugins")

### Certificates

Chromium uses [NSS](/index.php/Network_Security_Services "Network Security Services") for certificate management. Certificates can be managed in `Settings` → `Show advanced settings...` → `Manage Certificates...`.

## Tips and tricks

See the main article: [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks").

## Troubleshooting

### Constant freezes under KDE

[Uninstall](/index.php/Uninstall "Uninstall") [libcanberra-pulse](https://www.archlinux.org/packages/?name=libcanberra-pulse). See: [BBS#1228558](https://bbs.archlinux.org/viewtopic.php?pid=1228558).

### Fonts

**Note:** Chromium does not fully integrate with fontconfig/GTK/Pango/X/etc. due to its sandbox. For more information, see the [Linux Technical FAQ](https://dev.chromium.org/developers/linux-technical-faq).

#### Font rendering issues in PDF plugin

To fix the font rendering in some PDFs one has to install the [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) package, otherwise the substituted font causes text to run into other text. This was [reported on the chromium bug tracker](https://code.google.com/p/chromium/issues/detail?id=369991) by an Arch user.

### Force 3D acceleration

**Warning:** Disabling the rendering list may cause unstable behaviour, including crashes of the host. See the bug reports in `chrome://gpu`.

First follow [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). Then, to force 3D rendering, *enable* the flag "Override software rendering list" in `chrome://flags`. Check if it is working in `chrome://gpu`. This may also alleviate tearing issues with the [radeon](/index.php/Radeon "Radeon") driver.

### WebGL

**Warning:** [Catalyst](/index.php/Catalyst "Catalyst") does not support the `GL_ARB_robustness` extension. When using this driver, it is possible that a malicious site could use WebGL to perform a DoS attack on your graphic card.

Chromium will sometimes disable WebGL with certain graphics card configurations. To remedy this, enter `chrome://flags` into the URL bar and *disable* the *Disable WebGL* flag. Alternatively, pass the command-line flag `--enable-webgl` to Chromium in the terminal.

There is also the possibility that your graphics card has been blacklisted by Chromium. See [#Force 3D acceleration](#Force_3D_acceleration).

If you are using Chromium with [Bumblebee](/index.php/Bumblebee "Bumblebee"), WebGL might crash due to GPU sandboxing. In this case, you can disable GPU sandboxing with `optirun chromium --disable-gpu-sandbox`.

If none of the above solves your problem, you may be able to visit `chrome://gpu/` for additional debugging info.

### Distorted GUI

Chromium's graphical interface may look unsightly, distorted and zoomed in on high-DPI displays. To disable any attempts to scale display according to device DPI, use `--force-device-scale-factor=1`.

## See also

*   [Chromium homepage](https://www.chromium.org/)
*   [Google Chrome release notes](https://googlechromereleases.blogspot.com)
*   [Chrome web store](https://chrome.google.com/webstore/category/home)
*   [Differences between Chromium and Google Chrome](https://en.wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "wikipedia:Chromium (web browser)")
*   [List of Chromium command-line switches](http://peter.sh/experiments/chromium-command-line-switches/)