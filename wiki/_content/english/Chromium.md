[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) is an open-source graphical web browser from "The Chromium Project", based on the [Blink](https://en.wikipedia.org/wiki/Blink_(web_engine) rendering engine.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default applications](#Default_applications)
    *   [2.2 Flash Player plugin](#Flash_Player_plugin)
    *   [2.3 Widevine Content Decryption Module plugin](#Widevine_Content_Decryption_Module_plugin)
    *   [2.4 PDF viewer plugin](#PDF_viewer_plugin)
    *   [2.5 Certificates](#Certificates)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Constant freezes under KDE](#Constant_freezes_under_KDE)
    *   [4.2 Fonts](#Fonts)
        *   [4.2.1 Font rendering issues in PDF plugin](#Font_rendering_issues_in_PDF_plugin)
    *   [4.3 Force 3D acceleration](#Force_3D_acceleration)
    *   [4.4 WebGL](#WebGL)
    *   [4.5 Distorted GUI](#Distorted_GUI)
    *   [4.6 Disable keyring password prompt](#Disable_keyring_password_prompt)
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

*   **Chromium with GTK+ 3** — built with gtk3 instead of gtk2

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || [chromium-gtk3](https://aur.archlinux.org/packages/chromium-gtk3/)

The derived browser, **Google Chrome**, bundled with Widevine [EME](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions "wikipedia:Encrypted Media Extensions") (for e.g. Netflix), can be [installed](/index.php/Install "Install") with the [google-chrome](https://aur.archlinux.org/packages/google-chrome/) package.

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

*Pepper Flash* is the Flash Player plugin, using the new Pepper plugin API. To install it for Chromium, [install](/index.php/Install "Install") it the [pepper-flash](https://aur.archlinux.org/packages/pepper-flash/) package.

For Chrome < 57, make sure the plugin is enabled in `chrome://plugins` and restart Chromium via its menu.

Make sure Flash is allowed to run in `chrome://settings/content`.

### Widevine Content Decryption Module plugin

Widevine is Google's Encrypted Media Extensions (EME) Content Decryption Module (CDM). It is used to watch premium video content such as Netflix. It comes bundled with Chrome.

To install the Widevine CDM for Chromium, install the [chromium-widevine](https://aur.archlinux.org/packages/chromium-widevine/) package.

For Chrome < 57, make sure the plugin is enabled in `chrome://plugins`.

For Chrome >= 57, make sure *Allow sites to play protected content* is checked in `chrome://settings/content`.

### PDF viewer plugin

Chromium and Google Chrome are bundled with the *Chromium PDF Viewer* plugin, so installing a third-party plugin is not required.

If you prefer another implementation, check *Open PDF files in the default PDF viewer application* at the bottom of `chrome://settings/content`, and install one of the alternatives from [Browser plugins#PDF viewer](/index.php/Browser_plugins#PDF_viewer "Browser plugins").

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

**Warning:** Disabling the rendering blacklist may cause unstable behaviour, including crashes of the host. See the bug reports in `chrome://gpu`.

First follow [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). Then, to force 3D rendering, *enable* the flags: "Override software rendering list", "GPU rasterization", "Zero-copy rasterizer" in `chrome://flags`. Check if it is working in `chrome://gpu`. This may also alleviate tearing issues with the [radeon](/index.php/Radeon "Radeon") driver.

If "Native GpuMemoryBuffers" under `chrome://gpu` mentions software rendering, you additionally need to pass the `--enable-native-gpu-memory-buffers` flag, or some optimizations (like the zero-copy rasterizer) won't do anything. This flag isn't available under `chrome://flags` - it must be passed in either the chromium-flags.conf file (as noted in [Chromium/Tips_and_tricks#Making_flags_persistent](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks")) or directly on the command line.

### WebGL

**Warning:** [Catalyst](/index.php/Catalyst "Catalyst") does not support the `GL_ARB_robustness` extension. When using this driver, it is possible that a malicious site could use WebGL to perform a DoS attack on your graphic card.

There is the possibility that your graphics card has been blacklisted by Chromium. See [#Force 3D acceleration](#Force_3D_acceleration).

If you are using Chromium with [Bumblebee](/index.php/Bumblebee "Bumblebee"), WebGL might crash due to GPU sandboxing. In this case, you can disable GPU sandboxing with `optirun chromium --disable-gpu-sandbox`.

Visit `chrome://gpu/` for debugging information about WebGL support.

Chromium can save incorrect data about your GPU in your user profile (e.g. if you use switch between an Nvidia card using Optimus and Intel, it will show the Nvidia card in `chrome://gpu` even when you're not using it or primusrun/optirun). Running using a different user directory, e.g, `chromium --user-data-dir=$(mktemp -d)` may solve this issue. For a persistent solution you can reset the GPU information by deleting `~/.config/chromium/Local\ State`.

### Distorted GUI

Chromium's graphical interface may look unsightly, distorted and zoomed in on high-DPI displays. To disable any attempts to scale display according to device DPI, use `--force-device-scale-factor=1`.

### Disable keyring password prompt

See [GNOME/Keyring#Passwords are not remembered](/index.php/GNOME/Keyring#Passwords_are_not_remembered "GNOME/Keyring"). You may also need to edit the Chromium command line to append `--password-store=gnome`.

## See also

*   [Chromium homepage](https://www.chromium.org/)
*   [Google Chrome release notes](https://googlechromereleases.blogspot.com)
*   [Chrome web store](https://chrome.google.com/webstore/category/home)
*   [Differences between Chromium and Google Chrome](https://en.wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "wikipedia:Chromium (web browser)")
*   [List of Chromium command-line switches](http://peter.sh/experiments/chromium-command-line-switches/)