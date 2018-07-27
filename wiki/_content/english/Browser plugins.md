Related articles

*   [Browser extensions](/index.php/Browser_extensions "Browser extensions")
*   [Opera](/index.php/Opera "Opera")
*   [Firefox](/index.php/Firefox "Firefox")
*   [Chromium](/index.php/Chromium "Chromium")

There are two types of browser plugins, based on the plugin API they use:

*   Netscape plugin API ([NPAPI](https://en.wikipedia.org/wiki/NPAPI "wikipedia:NPAPI")): these plugins work in most smaller browsers ([Firefox supports only the Flash Player plugin](/index.php/Firefox#Plugins "Firefox"), Chromium and Opera do **not** support these plugins).
*   Pepper plugin API (**PPAPI**): these plugins work in [Chromium](/index.php/Chromium "Chromium") (and Chrome), [Opera](/index.php/Opera "Opera") and [Vivaldi](/index.php/Vivaldi "Vivaldi").

Most plugins on this page are NPAPI-only, unless noted otherwise.

## Contents

*   [1 Flash players](#Flash_players)
    *   [1.1 Adobe Flash Player](#Adobe_Flash_Player)
        *   [1.1.1 Installation](#Installation)
        *   [1.1.2 Upgrade](#Upgrade)
        *   [1.1.3 Configuration](#Configuration)
        *   [1.1.4 Multiple monitor full-screen fix](#Multiple_monitor_full-screen_fix)
        *   [1.1.5 Playing DRM-protected content](#Playing_DRM-protected_content)
    *   [1.2 Shumway](#Shumway)
    *   [1.3 Gnash](#Gnash)
    *   [1.4 Lightspark](#Lightspark)
*   [2 PDF viewer](#PDF_viewer)
    *   [2.1 PDF.js](#PDF.js)
    *   [2.2 External PDF viewers](#External_PDF_viewers)
*   [3 UnionPay Online Pay](#UnionPay_Online_Pay)
*   [4 Citrix](#Citrix)
*   [5 Java (IcedTea)](#Java_.28IcedTea.29)
*   [6 Pipelight](#Pipelight)
*   [7 Multimedia playback](#Multimedia_playback)
*   [8 Google Hangouts](#Google_Hangouts)
*   [9 MozPlugger](#MozPlugger)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Flash Player: no sound](#Flash_Player:_no_sound)
    *   [10.2 Flash Player: blocking sound for other applications or delayed playback](#Flash_Player:_blocking_sound_for_other_applications_or_delayed_playback)
    *   [10.3 Flash Player: performance](#Flash_Player:_performance)
    *   [10.4 Flash Player: black bars in full screen playback on multi-headed setups](#Flash_Player:_black_bars_in_full_screen_playback_on_multi-headed_setups)
    *   [10.5 Firefox: old Flash Player version shown after upgrade](#Firefox:_old_Flash_Player_version_shown_after_upgrade)
    *   [10.6 Firefox: plugins are installed but not working](#Firefox:_plugins_are_installed_but_not_working)

## Flash players

### Adobe Flash Player

#### Installation

The package you will need to install depends on the browser you use.

*   The NPAPI version can be [installed](/index.php/Install "Install") with the [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) package.
*   The PPAPI version can be [installed](/index.php/Install "Install") with the [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash) package.

**Note:**

*   Some Flash apps may require the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) package in order to properly render text.
*   The [freshplayerplugin](https://aur.archlinux.org/packages/freshplayerplugin/) package provides an *experimental* adapter to use [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash) with NPAPI based browsers like Firefox. It can be configured (e.g. for enabling HW-acceleration) by copying `/usr/share/freshplayerplugin/freshwrapper.conf.example` to `~/.config/freshwrapper.conf`.

#### Upgrade

If you are using [Firefox](/index.php/Firefox "Firefox"), please make sure to follow [this instruction first](/index.php/Firefox#Firefox_detects_the_wrong_version_of_my_plugin "Firefox").

#### Configuration

To change the preferences (privacy settings, resource usage, etc.) of Flash Player, right click on any embedded Flash content (for instance [adobe's flash home](https://helpx.adobe.com/flash-player.html)) and choose *Settings* from the menu.

You can also use the Flash settings file `/etc/adobe/mms.cfg`. Gentoo has an extensively commented [example mms.cfg](http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/www-plugins/adobe-flash/files/mms.cfg).

To enable video decoding with [hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"), add/uncomment the following line:

```
EnableLinuxHWVideoDecode = 1

```

It might also be required to add/uncomment the following line:

```
OverrideGPUValidation = 1

```

#### Multiple monitor full-screen fix

When using a multiple monitor setup, or swapping between virtual desktops, it is possible to lose focus on a fullscreen flash window. In such a case, the adobe flash-plugin will automatically exit full-screen mode. This may not be to your liking.

Unfortunately, this behavior is hard coded into the binary. In order to change this behavior it is necessary to alter the binary.

Fixing this issue only works for the NPAPI plugin and this issue can be fixed via 2 ways.

*   Using the [flashplugin-focusfix](https://aur.archlinux.org/packages/flashplugin-focusfix/).

*   [Patching manually](http://www.webupd8.org/2012/10/ubuntu-multi-monitor-tweaks-full-screen.html):

	After the package has been installed, backup `libflashplayer.so`:

	 `# cp /usr/lib/mozilla/plugins/libflashplayer.so /usr/lib/mozilla/plugins/libflashplayer.so.backup` 

	Then, you will need to alter that file using a hex editor like [ghex](https://www.archlinux.org/packages/?name=ghex). You must open it with root privileges obviously.

	 `# ghex /usr/lib/mozilla/plugins/libflashplayer.so` 

	Using the hex editor find the string `_NET_ACTIVE_WINDOW`. In ghex the readable string is on the right hand side of the window, and the hex is on the left, you are trying to locate the readable string. It should be easy to find using a search function.

	Upon finding `_NET_ACTIVE_WINDOW` rewrite the line, but **do not** change the length of the line, for example `_NET_ACTIVE_WINDOW` becomes `_XET_ACTIVE_WINDOW`.

	Save the binary, and restart any processes using the plugin (as this will crash any instance of the plugin in use.)

#### Playing DRM-protected content

See [Flash DRM content](/index.php/Flash_DRM_content "Flash DRM content").

### Shumway

[Shumway](http://mozilla.github.io/shumway/) is a [discontinued](https://github.com/mozilla/shumway/issues/2420) HTML5 technology experiment that explores building a faithful and efficient renderer for the SWF file format without native code assistance. The plugin may be installed directly from [Mozilla's github.io site](http://mozilla.github.io/shumway/).

### Gnash

[Gnash](https://en.wikipedia.org/wiki/Gnash_(software) is a free (libre) alternative to Adobe Flash Player. It is available both as a standalone player for desktop computers and embedded devices, as well as a browser plugin, and supports the SWF format up to version 7 (with versions 8 and 9 under development) and about 80% of ActionScript 2.0.

There is a packages available: [gnash-git](https://aur.archlinux.org/packages/gnash-git/).

### Lightspark

[Lightspark](http://lightspark.github.com/) is another attempt to provide a free alternative to Adobe Flash aimed at supporting newer Flash formats. Lightspark has the ability to fall back on Gnash for old content, which enables users to install both and enjoy wider coverage. Although it is still very much in development, it supports some [popular sites](https://github.com/lightspark/lightspark/wiki/Site-Support).

Lightspark can be [installed](/index.php/Install "Install") with the [lightspark-git](https://aur.archlinux.org/packages/lightspark-git/) package.

## PDF viewer

### PDF.js

[PDF.js](https://github.com/mozilla/pdf.js) is a PDF renderer created by Mozilla and built using HTML5 technologies.

It is included in [Firefox](/index.php/Firefox "Firefox").

For [Chromium](/index.php/Chromium "Chromium") and Google Chrome it is available as extension in the [Chrome Web Store](https://chrome.google.com/webstore/detail/pdf-viewer/oemmndcbldboiebfnladdacbdfmadadm).

### External PDF viewers

To use an external PDF viewer you need [#MozPlugger](#MozPlugger).

If you want to use MozPlugger with Evince, for example, you have to find the lines containing `pdf` in the `/etc/mozpluggerrc` file and modify the corresponding line after `GV()` as below:

```
repeat noisy swallow(evince) fill: evince "$file"

```

(replace `evince` with something else if it is not your viewer of choice).

When using Firefox, you may need to change 2 values in `about:config`:

*   Change `pdfjs.disabled`'s value to *true*;
*   Change `plugin.disable_full_page_plugin_for_types`'s value to an empty value.

Restart and it should work like a charm!

## UnionPay Online Pay

**Note:** This plugin is NPAPI-only and thus does **not work** in Chromium, Opera and Firefox.

[Install](/index.php/Install "Install") [upeditor](https://aur.archlinux.org/packages/upeditor/) package for the "security plugin" used by UnionPay Online Pay (银联在线支付).

## Citrix

See [Citrix](/index.php/Citrix "Citrix").

## Java (IcedTea)

**Note:** Both Java plugins are NPAPI-only and thus do **not work** in Chromium, Opera and Firefox.

To enable [Java](/index.php/Java "Java") support in your browser, you have two options: the open-source [OpenJDK](https://en.wikipedia.org/wiki/OpenJDK "wikipedia:OpenJDK") (recommended) or Oracle's proprietary version. For details about why OpenJDK is recommended see [[1]](https://mailman.archlinux.org/pipermail/arch-general/2011-August/021671.html).

To use OpenJDK, you have to install the [IcedTea](http://icedtea.classpath.org/wiki/Main_Page) browser plugin, [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web).

If you want to use Oracle's JRE, install the [jre](https://aur.archlinux.org/packages/jre/) package.

## Pipelight

See [Pipelight](/index.php/Pipelight "Pipelight").

## Multimedia playback

Many browsers support the [GStreamer](/index.php/GStreamer "GStreamer") framework to play multimedia inside HTML5 `<audio>` and `<video>` elements. Check the optional dependencies of the browser package (or of the web engine, e.g. [webkit2gtk](https://www.archlinux.org/packages/?name=webkit2gtk) or [qt5-webkit](https://www.archlinux.org/packages/?name=qt5-webkit)) to see if GStreamer is supported. See [GStreamer#Installation](/index.php/GStreamer#Installation "GStreamer") for the description of each plugin.

For media formats that are not natively supported by your browser (e.g. most browsers don't play `.mkv` files), the following plugins are available:

*   **Rosa Media Player Plugin** — Qt-based NPAPI plugin that uses MPlayer as backend.

	[https://abf.rosalinux.ru/uxteam/ROSA_Media_Player](https://abf.rosalinux.ru/uxteam/ROSA_Media_Player) || [rosa-media-player-plugin](https://aur.archlinux.org/packages/rosa-media-player-plugin/)

*   **VLC Plugin** — NPAPI plugin that uses VLC as backend.

	[https://code.videolan.org/videolan/npapi-vlc](https://code.videolan.org/videolan/npapi-vlc) || [npapi-vlc](https://aur.archlinux.org/packages/npapi-vlc/)

## Google Hangouts

**Note:** This plugin is not required when using Chromium or Firefox

Hangouts plugin can be installed with the [google-talkplugin](https://aur.archlinux.org/packages/google-talkplugin/) package. Hangouts is a messenger by Google, that allows you to make video call between 15 people simultaneously, or share your screen with others.

## MozPlugger

MozPlugger can be installed with the [mozplugger](https://aur.archlinux.org/packages/mozplugger/) package.

[MozPlugger](http://mozplugger.mozdev.org/) is a Mozilla plugin which can show many types of multimedia inside your browser. To accomplish this, it uses external programs such as MPlayer, xine, Evince, OpenOffice, TiMidity, etc. To modify or add applications to be used by MozPlugger just modify the `/etc/mozpluggerrc` file.

For example, MozPlugger uses OpenOffice by default to open `doc` files. To change it to use LibreOffice instead, look for the OpenOffice section:

 `/etc/mozpluggerrc` 
```
...
### OpenOffice
define([OO],[swallow(VCLSalFrame) fill: ooffice2.0 -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: soffice -nologo $1 "$file"])
...

```

and add LibreOffice at the beginning of the list:

 `/etc/mozpluggerrc` 
```
...
### LibreOffice/OpenOffice
define([OO],[swallow(VCLSalFrame) fill: libreoffice --nologo --norestore --view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice2.0 -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: soffice -nologo $1 "$file"])
...

```

**Note:** Be sure to also choose LibreOffice as your preferred application to open `doc` files.

As another simple example, if you want to open `cpp` files with your favorite text editor (we will use Kate) to get syntax highlighting, just add a new section to your `mozpluggerrc` file:

 `/etc/mozpluggerrc` 
```
text/x-c++:cpp:C++ Source File
text/x-c++:hpp:C++ Header File
    repeat noisy swallow(kate) fill: kate -b "$file"

```

To change the default of MPlayer so that [mpv](/index.php/Mpv "Mpv") is used instead, change the appropriate lines such that:

 `/etc/mozpluggerrc` 
```
...
### MPlayer

#define(MP_CMD,[mplayer -really-quiet -nojoystick -nofs -zoom -vo xv,x11 -ao esd,alsa,oss,arts,null -osdlevel 0 $1 </dev/null])
define(MP_CMD,[mpv -really-quiet $1 </dev/null])

#define(MP_EMBED,[embed noisy ignore_errors: MP_CMD(-xy $width -wid $window $1)])
define(MP_EMBED,[embed noisy ignore_errors: MP_CMD(--autofit=$width -wid $window $1)])

#define(MP_NOEMBED,[noembed noisy ignore_errors maxaspect swallow(MPlayer): MP_CMD($1)])
define(MP_NOEMBED,[noembed noisy ignore_errors maxaspect swallow(mpv): MP_CMD($1)])

...

#define(MP_AUDIO,[mplayer -quiet -nojoystick $1 </dev/null])
define(MP_AUDIO,[mpv -really-quiet $1 </dev/null])

#define(MP_AUDIO_STREAM,[controls stream noisy ignore_errors: mplayer -quiet -nojoystick $1 "$file" </dev/null])
define(MP_AUDIO_STREAM,[controls stream noisy ignore_errors: mpv -really-quiet $1 "$file" </dev/null])
...
```

For a more complete list of MozPlugger options see [mozplugger(7)](https://www.freebsd.org/cgi/man.cgi?query=mozplugger).

## Troubleshooting

### Flash Player: no sound

Flash Player outputs its sound only through the default [ALSA](/index.php/ALSA "ALSA") device, which is number **0**. If you have multiple sound devices (a very common example is having a sound card and HDMI output in the video card), then your preferred device may have a different number.

For a list of available devices with their respective numbers, run:

 `$ aplay -l` 
```
 **** List of PLAYBACK Hardware Devices ****
 card 0: Generic [HD-Audio Generic], device 3: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: DX [Xonar DX], device 0: Multichannel [Multichannel]
   Subdevices: 0/1
   Subdevice #0: subdevice #0
 card 1: DX [Xonar DX], device 1: Digital [Digital]
   Subdevices: 1/1
   Subdevice #0: subdevice #0

```

In this case, the HDMI output is `card 0` and the sound card is `card 1`. To make your sound card the default for ALSA, create the file `.asoundrc` in your home directory, with the following content:

 `~/.asoundrc` 
```
pcm.!default {
    type hw
    card 1
}

ctl.!default {
    type hw
    card 1
}

```

### Flash Player: blocking sound for other applications or delayed playback

If sound is delayed within Flash videos or Flash stops sound from any other application, then make sure you do not have `snd_pcm_oss` module loaded:

```
$ lsmod | grep snd_pcm_oss

```

You can unload it:

```
# rmmod snd_pcm_oss

```

and restart the browser to see if it helps.

### Flash Player: performance

Adobe's Flash plugin has some serious performance issues, especially when CPU frequency scaling is used. There seems to be a policy not to use the whole CPU workload, so the frequency scaling governor does not clock the CPU any higher. To work around this issue, see [CPU frequency scaling#Switching threshold](/index.php/CPU_frequency_scaling#Switching_threshold "CPU frequency scaling")

### Flash Player: black bars in full screen playback on multi-headed setups

The Flash plugin has a known bug where the full screen mode does not really work when you have a multi-monitor setup. Apparently, it incorrectly determines the full screen resolution, so the full screen Flash Player fills the correct monitor but gets scaled as if the monitor had the resolution of the total display area.

To fix this, you can use the "hack" described [here](http://al.robotfuzz.com/content/workaround-fullscreen-flash-linux-multiheaded-desktops). Simply download the source from the link given on the page, and follow the instructions in the README.

**Note:** While the author mentions using NVDIA's TwinView, the hack should work for any multi-monitor setup.

### Firefox: old Flash Player version shown after upgrade

Solution for Firefox: delete file "pluginreg.dat" in user's profile directory.

*   Close firefox
*   Go to `/home/*<username>*/.mozilla/firefox/*<profile_folder>*/`
*   Delete file "pluginreg.dat"

Firefox will automatically rebuild this file once it is started again. Make sure to substitute *<username>* and *<profile_folder>* with the appropriate information.

### Firefox: plugins are installed but not working

A common problem is that the plugin path is unset. This typically occurs on a new install, when the user has not re-logged in before running Firefox after the installation. Test if the path is unset:

```
$ printenv MOZ_PLUGIN_PATH

```

If unset, then either re-login, or source `/etc/profile.d/mozilla-common.sh` and start Firefox from the same shell:

```
$ source /etc/profile.d/mozilla-common.sh && firefox

```