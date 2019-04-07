Related articles

*   [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks")
*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox](/index.php/Firefox "Firefox")
*   [Opera](/index.php/Opera "Opera")

[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) is an open-source graphical web browser based on the [Blink](https://en.wikipedia.org/wiki/Blink_(web_engine) rendering engine. It is the basis for the proprietary Google Chrome browser.

Google Chrome has following notable built-in features over Chromium:

*   [Flash player](https://en.wikipedia.org/wiki/Flash_player "wikipedia:Flash player"), also available via [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash).
*   Widevine [EME](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions "wikipedia:Encrypted Media Extensions") for e.g. Netflix, also available via [chromium-widevine](https://aur.archlinux.org/packages/chromium-widevine/).
*   [Native client](https://en.wikipedia.org/wiki/Native_client "wikipedia:Native client") (NaCl). Support for native client (NaCl) has been dropped from Chromium packages since version 54, see [FS#51511](https://bugs.archlinux.org/task/51511).

See these [two](https://chromium.googlesource.com/chromium/src/+/master/docs/chromium_browser_vs_google_chrome.md) [articles](https://www.howtogeek.com/202825/what%E2%80%99s-the-difference-between-chromium-and-chrome/) for an explanation of the differences between Chromium and Chrome.

See [List of applications/Internet#Blink-based](/index.php/List_of_applications/Internet#Blink-based "List of applications/Internet") for other browsers based on Chromium.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default applications](#Default_applications)
    *   [2.2 Certificates](#Certificates)
    *   [2.3 Widevine Content Decryption Module plugin](#Widevine_Content_Decryption_Module_plugin)
    *   [2.4 Force GPU acceleration](#Force_GPU_acceleration)
    *   [2.5 Hardware video acceleration](#Hardware_video_acceleration)
    *   [2.6 Flash Player plugin](#Flash_Player_plugin)
    *   [2.7 PDF viewer plugin](#PDF_viewer_plugin)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Fonts](#Fonts)
        *   [4.1.1 Font rendering issues in PDF plugin](#Font_rendering_issues_in_PDF_plugin)
        *   [4.1.2 Font rendering issues of UTF characters](#Font_rendering_issues_of_UTF_characters)
        *   [4.1.3 Tab font size is too large](#Tab_font_size_is_too_large)
    *   [4.2 WebGL](#WebGL)
    *   [4.3 Incorrect HiDPI rendering](#Incorrect_HiDPI_rendering)
    *   [4.4 Password prompt on every start with GNOME Keyring](#Password_prompt_on_every_start_with_GNOME_Keyring)
    *   [4.5 Chromecasts in the network are not discovered](#Chromecasts_in_the_network_are_not_discovered)
    *   [4.6 Losing cookies and passwords when switching between desktop environments](#Losing_cookies_and_passwords_when_switching_between_desktop_environments)
    *   [4.7 Hang on startup when Google Sync enabled](#Hang_on_startup_when_Google_Sync_enabled)
*   [5 See also](#See_also)

## Installation

There are several packages available to [install](/index.php/Install "Install") Chromium with:

*   [chromium](https://www.archlinux.org/packages/?name=chromium) – stable release.
*   [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/) – development release.
*   [chromium-snapshot-bin](https://aur.archlinux.org/packages/chromium-snapshot-bin/) – nightly build.
*   [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/) – patched stable release with [VA-API](#Hardware_video_acceleration).
*   [chromium-vaapi-bin](https://aur.archlinux.org/packages/chromium-vaapi-bin/) – patched stable release with [VA-API](#Hardware_video_acceleration), pre-compiled.

Google Chrome packages:

*   [google-chrome](https://aur.archlinux.org/packages/google-chrome/) – stable release.
*   [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/) – beta release.
*   [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/) – development release.

## Configuration

### Default applications

To set Chromium as the default browser and to change which applications Chromium launches when opening downloaded files, see [default applications](/index.php/Default_applications "Default applications").

### Certificates

Chromium uses [Network Security Services](/index.php/Network_Security_Services "Network Security Services") for certificate management. Certificates can be managed in `chrome://settings/certificates`.

### Widevine Content Decryption Module plugin

Widevine is Google's Encrypted Media Extensions (EME) Content Decryption Module (CDM). It is used to watch premium video content such as Netflix. It is automatically installed when using Google Chrome.

To install it for Chromium, [install](/index.php/Install "Install") the [chromium-widevine](https://aur.archlinux.org/packages/chromium-widevine/) package. Make sure *Allow sites to play protected content* is checked in `chrome://settings/content/protectedContent`.

### Force GPU acceleration

**Warning:** Disabling the rendering blacklist may cause unstable behavior, including crashes of the host. See the bug reports in `chrome://gpu` for details.

By default Chromium on Linux doesn't use any GPU acceleration. To force GPU acceleration, [append](/index.php/Append "Append") the following flags to [persistent configuration](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks"):

 `~/.config/chromium-flags.conf` 
```
--ignore-gpu-blacklist
--enable-gpu-rasterization
--enable-native-gpu-memory-buffers
--enable-zero-copy

```

Additionally the flag `--disable-gpu-driver-bug-workarounds` may need to be passed to prevent GPU workaround from being used. Flags in `chrome://gpu` should state "Hardware accelerated" when configured and available.

### Hardware video acceleration

Accelerated video decoding using [VA-API](/index.php/VA-API "VA-API") can be used with community made patches [[1]](https://bugs.chromium.org/p/chromium/issues/detail?id=463440#c65), packages are available in [AUR](/index.php/AUR "AUR") as [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/) or [chromium-vaapi-bin](https://aur.archlinux.org/packages/chromium-vaapi-bin/).

Be sure to install correct VA-API driver for your video card and verify VA-API has been enabled and working correctly, see [Hardware video acceleration#Verifying VA-API](/index.php/Hardware_video_acceleration#Verifying_VA-API "Hardware video acceleration").

To enable video acceleration, [append](/index.php/Append "Append") the following flags to [persistent configuration](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks"):

 `~/.config/chromium-flags.conf` 
```
--enable-accelerated-mjpeg-decode
--enable-accelerated-video

```

**Note:** Additionally [#Force GPU acceleration](#Force_GPU_acceleration) and set `--disable-gpu-driver-bug-workarounds` to remove video freezes (especially when watching in fullscreen).

### Flash Player plugin

Flash Player is automatically installed when using Google Chrome.

To install it for Chromium, [install](/index.php/Install "Install") the [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash) package.

Make sure Flash is allowed to run in `chrome://settings/content/flash`.

### PDF viewer plugin

Chromium and Google Chrome are bundled with the *Chromium PDF Viewer* plugin. If you don't want to use this plugin, check *Open PDFs using a different application* in `chrome://settings/content/pdfDocuments`.

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

### WebGL

There is the possibility that your graphics card has been blacklisted by Chromium. See [#Force GPU acceleration](#Force_GPU_acceleration).

If you are using Chromium with [Bumblebee](/index.php/Bumblebee "Bumblebee"), WebGL might crash due to GPU sandboxing. In this case, you can disable GPU sandboxing with `optirun chromium --disable-gpu-sandbox`.

Visit `chrome://gpu/` for debugging information about WebGL support.

Chromium can save incorrect data about your GPU in your user profile (e.g. if you use switch between an Nvidia card using Optimus and Intel, it will show the Nvidia card in `chrome://gpu` even when you're not using it or primusrun/optirun). Running using a different user directory, e.g, `chromium --user-data-dir=$(mktemp -d)` may solve this issue. For a persistent solution you can reset the GPU information by deleting `~/.config/chromium/Local\ State`.

### Incorrect HiDPI rendering

Chromium will automatically scale for a [HiDPI](/index.php/HiDPI "HiDPI") display, however this may cause an incorrect renderend GUI.

The flag `--force-device-scale-factor=1` may be used to overrule the automatic scaling factor.

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