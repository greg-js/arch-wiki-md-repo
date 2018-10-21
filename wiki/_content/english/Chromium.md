Related articles

*   [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks")
*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox](/index.php/Firefox "Firefox")
*   [Opera](/index.php/Opera "Opera")

[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) is an open-source graphical web browser based on the [Blink](https://en.wikipedia.org/wiki/Blink_(web_engine) rendering engine. It is the basis for the proprietary Google Chrome browser.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default applications](#Default_applications)
    *   [2.2 Flash Player plugin](#Flash_Player_plugin)
    *   [2.3 Widevine Content Decryption Module plugin](#Widevine_Content_Decryption_Module_plugin)
    *   [2.4 PDF viewer plugin](#PDF_viewer_plugin)
    *   [2.5 Certificates](#Certificates)
    *   [2.6 Hardware video acceleration](#Hardware_video_acceleration)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Fonts](#Fonts)
        *   [4.1.1 Font rendering issues in PDF plugin](#Font_rendering_issues_in_PDF_plugin)
        *   [4.1.2 Font rendering issues of UTF characters](#Font_rendering_issues_of_UTF_characters)
        *   [4.1.3 Tab font size is too large](#Tab_font_size_is_too_large)
    *   [4.2 Force GPU acceleration](#Force_GPU_acceleration)
    *   [4.3 WebGL](#WebGL)
    *   [4.4 Zoomed-in GUI](#Zoomed-in_GUI)
    *   [4.5 Password prompt on every start with GNOME Keyring](#Password_prompt_on_every_start_with_GNOME_Keyring)
    *   [4.6 Chromecasts in the network are not discovered](#Chromecasts_in_the_network_are_not_discovered)
    *   [4.7 Losing cookies and passwords when switching between desktop environments](#Losing_cookies_and_passwords_when_switching_between_desktop_environments)
    *   [4.8 Hang on startup when Google Sync enabled](#Hang_on_startup_when_Google_Sync_enabled)
*   [5 See also](#See_also)

## Installation

The open-source project, **Chromium**, can be [installed](/index.php/Install "Install") with the [chromium](https://www.archlinux.org/packages/?name=chromium) package.

Other alternatives include:

*   **Chromium Dev Channel** — the development version

	[https://chromereleases.googleblog.com/](https://chromereleases.googleblog.com/) || [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/)

*   **Chromium snapshot builds** — the untested nightly version

	[https://build.chromium.org/](https://build.chromium.org/) || [chromium-snapshot-bin](https://aur.archlinux.org/packages/chromium-snapshot-bin/)

*   **Chromium with VA-API support** — see [#Hardware video acceleration](#Hardware_video_acceleration)

	[https://chromium-review.googlesource.com/c/chromium/src/+/532294](https://chromium-review.googlesource.com/c/chromium/src/+/532294) || [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/)

The derived browser, **Google Chrome**, which automatically installs Flash Player and Widevine [EME](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions "wikipedia:Encrypted Media Extensions") (for e.g. Netflix), can be [installed](/index.php/Install "Install") with the [google-chrome](https://aur.archlinux.org/packages/google-chrome/) package.

Other alternatives include:

*   **Google Chrome Beta Channel** — the beta version

	[https://www.google.com/chrome/browser/beta.html](https://www.google.com/chrome/browser/beta.html) || [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)

*   **Google Chrome Dev Channel** — the development version

	[https://www.google.com/chrome/](https://www.google.com/chrome/) || [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)

**Note:** Support for native client (NaCl) has been dropped in [chromium](https://www.archlinux.org/packages/?name=chromium) version 54, see [FS#51511](https://bugs.archlinux.org/task/51511). Opening NaCl applications will display this error message: "This plugin is not supported". The [google-chrome](https://aur.archlinux.org/packages/google-chrome/) package supports NaCl.

See these [two](https://chromium.googlesource.com/chromium/src/+/master/docs/chromium_browser_vs_google_chrome.md) [articles](https://www.howtogeek.com/202825/what%E2%80%99s-the-difference-between-chromium-and-chrome/) for an explanation of the differences between Chromium and Chrome.

On top of the different Chromium build channels, a number of forks exist with more or less special features; see [List of applications#Blink-based](/index.php/List_of_applications#Blink-based "List of applications").

## Configuration

### Default applications

To set Chromium as the default browser and to change which applications Chromium launches when opening downloaded files, see [default applications](/index.php/Default_applications "Default applications").

### Flash Player plugin

Flash Player is automatically installed when using Google Chrome.

To install it for Chromium, [install](/index.php/Install "Install") the [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash) package.

Make sure Flash is allowed to run in `chrome://settings/content/flash`.

### Widevine Content Decryption Module plugin

Widevine is Google's Encrypted Media Extensions (EME) Content Decryption Module (CDM). It is used to watch premium video content such as Netflix. It is automatically installed when using Google Chrome.

To install it for Chromium, [install](/index.php/Install "Install") the [chromium-widevine](https://aur.archlinux.org/packages/chromium-widevine/) package. Make sure *Allow sites to play protected content* is checked in `chrome://settings/content/protectedContent`.

### PDF viewer plugin

Chromium and Google Chrome are bundled with the *Chromium PDF Viewer* plugin. If you don't want to use this plugin, check *Open PDFs using a different application* in `chrome://settings/content/pdfDocuments`.

### Certificates

Chromium uses [Network Security Services](/index.php/Network_Security_Services "Network Security Services") for certificate management. Certificates can be managed in `chrome://settings/certificates`.

### Hardware video acceleration

**Note:** You might need to [#Force GPU acceleration](#Force_GPU_acceleration) and see [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") first.

Accelerated video decoding via VA-API is available using [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/) and can be enabled either by:

*   enabling `chrome://flags/#enable-accelerated-video` and `chrome://flags/#enable-accelerated-mjpeg-decode` flags;
*   specifying `--enable-accelerated-video` and `--enable-accelerated-mjpeg-decode` on the command line or adding them to [persistent configuration](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks").

Additionally `--disable-gpu-driver-bug-workarounds` has been tested and confirmed to remove video freezes (especially when watching in fullscreen).

## Tips and tricks

See the main article: [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks").

## Troubleshooting

### Fonts

**Note:** Chromium does not fully integrate with fontconfig/GTK/Pango/X/etc. due to its sandbox. For more information, see the [Linux Technical FAQ](https://dev.chromium.org/developers/linux-technical-faq).

#### Font rendering issues in PDF plugin

To fix the font rendering in some PDFs one has to install the [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) package, otherwise the substituted font causes text to run into other text. This was [reported on the chromium bug tracker](https://code.google.com/p/chromium/issues/detail?id=369991) by an Arch user.

#### Font rendering issues of UTF characters

UTF characters may render as boxes (e.g. simplified Chinese characters). Installing [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) will allow for the characters to be rendered as expected.

#### Tab font size is too large

Chromium will use the GTK settings as described in [GTK+#Configuration](/index.php/GTK%2B#Configuration "GTK+"). When configured, Chromium will use the `gtk-font-name` setting for tabs (which may mismatch window font size). To override these settings, use `--force-device-scale-factor=1.0`.

### Force GPU acceleration

**Warning:** Disabling the rendering blacklist may cause unstable behavior, including crashes of the host. See the bug reports in `chrome://gpu` for details.

To force GPU acceleration, *enable* the flags: `--ignore-gpu-blacklist`, `--enable-gpu-rasterization`, `--enable-zero-copy` in `chrome://flags` or [append](/index.php/Append "Append") to the [persistent configuration](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks"). Additionally the flag `--disable-gpu-driver-bug-workarounds` may need to be passed to prevent GPU workaround from being used. Flags in `chrome://gpu` should state "Hardware accelerated" when configured and available.

For *Native GpuMemoryBuffers* the flag `--enable-native-gpu-memory-buffers` needs to be pass or some optimizations (like the zero-copy rasterizer) will use software rendering. The flag isn't available under `chrome://flags` and must be passed as a [persistent flag](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks") or directly from the command line.

### WebGL

There is the possibility that your graphics card has been blacklisted by Chromium. See [#Force GPU acceleration](#Force_GPU_acceleration).

If you are using Chromium with [Bumblebee](/index.php/Bumblebee "Bumblebee"), WebGL might crash due to GPU sandboxing. In this case, you can disable GPU sandboxing with `optirun chromium --disable-gpu-sandbox`.

Visit `chrome://gpu/` for debugging information about WebGL support.

Chromium can save incorrect data about your GPU in your user profile (e.g. if you use switch between an Nvidia card using Optimus and Intel, it will show the Nvidia card in `chrome://gpu` even when you're not using it or primusrun/optirun). Running using a different user directory, e.g, `chromium --user-data-dir=$(mktemp -d)` may solve this issue. For a persistent solution you can reset the GPU information by deleting `~/.config/chromium/Local\ State`.

### Zoomed-in GUI

Chromium's graphical interface will sometimes automatically scale for [HiDPI](/index.php/HiDPI "HiDPI") displays. To disable this, use `--force-device-scale-factor=1`.

### Password prompt on every start with GNOME Keyring

See [GNOME/Keyring#Passwords are not remembered](/index.php/GNOME/Keyring#Passwords_are_not_remembered "GNOME/Keyring").

### Chromecasts in the network are not discovered

You will need to enable the Media Router Component Extension in `chrome://flags/#load-media-router-component-extension`.

### Losing cookies and passwords when switching between desktop environments

If you see the message `Failed to decrypt token for service AccountId-*` in the terminal when you start Chromium, it might try to use the wrong password storage backend. This might happen when you switch between Desktop Environments.

See [Chromium/Tips and tricks#Force a password store](/index.php/Chromium/Tips_and_tricks#Force_a_password_store "Chromium/Tips and tricks").

### Hang on startup when Google Sync enabled

Try launching Chrome with `--password-store=basic` or another appropriate password store.

See [Chromium/Tips and tricks#Force a password store](/index.php/Chromium/Tips_and_tricks#Force_a_password_store "Chromium/Tips and tricks").

## See also

*   [Chromium homepage](https://www.chromium.org/)
*   [Google Chrome release notes](https://googlechromereleases.blogspot.com)
*   [Chrome web store](https://chrome.google.com/webstore/category/home)
*   [Differences between Chromium and Google Chrome](https://en.wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "wikipedia:Chromium (web browser)")
*   [List of Chromium command-line switches](http://peter.sh/experiments/chromium-command-line-switches/)