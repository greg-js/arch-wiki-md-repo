Есть два типа плагинов для браузеров, в зависимости от API, на котором они основаны:

*   Netscape plugin API (NPAPI): эти плагины работают в [Firefox](/index.php/Firefox "Firefox"), [Opera](/index.php/Opera "Opera") и большинстве других браузеров (**не** в [Chromium](/index.php/Chromium "Chromium")).
*   Pepper plugin API (PPAPI): эти плагины работают только в [Chromium](/index.php/Chromium "Chromium") и Chrome.

Most plugins on this page are NPAPI-only, unless noted otherwise.

## Contents

*   [1 Flash Player](#Flash_Player)
    *   [1.1 Shumway](#Shumway)
    *   [1.2 Gnash](#Gnash)
    *   [1.3 Lightspark](#Lightspark)
    *   [1.4 Adobe Flash Player](#Adobe_Flash_Player)
        *   [1.4.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
        *   [1.4.2 Configuration](#Configuration)
        *   [1.4.3 Disable the "Press ESC to exit full screen mode" message](#Disable_the_.22Press_ESC_to_exit_full_screen_mode.22_message)
        *   [1.4.4 Multiple monitor full-screen fix](#Multiple_monitor_full-screen_fix)
        *   [1.4.5 Fullscreen fix for GNOME 3](#Fullscreen_fix_for_GNOME_3)
            *   [1.4.5.1 Firefox](#Firefox)
            *   [1.4.5.2 Chrome / Chromium](#Chrome_.2F_Chromium)
            *   [1.4.5.3 Epiphany / GNOME Web](#Epiphany_.2F_GNOME_Web)
    *   [1.5 Video players workarounds](#Video_players_workarounds)
        *   [1.5.1 Open-with Firefox extension](#Open-with_Firefox_extension)
*   [2 PDF viewer](#PDF_viewer)
    *   [2.1 PDF.js](#PDF.js)
    *   [2.2 External PDF viewers](#External_PDF_viewers)
    *   [2.3 Adobe Reader](#Adobe_Reader)
        *   [2.3.1 32-bit](#32-bit)
        *   [2.3.2 64-bit](#64-bit)
*   [3 Citrix](#Citrix)
*   [4 Java (IcedTea)](#Java_.28IcedTea.29)
*   [5 Pipelight](#Pipelight)
*   [6 Multimedia playback](#Multimedia_playback)
    *   [6.1 Other plugins](#Other_plugins)
*   [7 Other](#Other)
    *   [7.1 MozPlugger](#MozPlugger)
    *   [7.2 kpartsplugin](#kpartsplugin)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Flash Player: no sound](#Flash_Player:_no_sound)
    *   [8.2 Flash Player: blocking sound for other applications or delayed playback](#Flash_Player:_blocking_sound_for_other_applications_or_delayed_playback)
    *   [8.3 Flash Player: performance](#Flash_Player:_performance)
    *   [8.4 Flash Player: low webcam resolution](#Flash_Player:_low_webcam_resolution)
    *   [8.5 Flash Player: black bars in full screen playback on multi-headed setups](#Flash_Player:_black_bars_in_full_screen_playback_on_multi-headed_setups)
    *   [8.6 Flash Player: blue tint on videos with NVIDIA](#Flash_Player:_blue_tint_on_videos_with_NVIDIA)
    *   [8.7 Flash Player: leaking overlay with NVIDIA](#Flash_Player:_leaking_overlay_with_NVIDIA)
    *   [8.8 Flash Player: videos not working on older systems](#Flash_Player:_videos_not_working_on_older_systems)
    *   [8.9 Plugins are installed but not working](#Plugins_are_installed_but_not_working)
    *   [8.10 Gecko Media Player will not play Apple trailers](#Gecko_Media_Player_will_not_play_Apple_trailers)

## Flash Player

### Shumway

[Shumway](http://mozilla.github.io/shumway/) is an HTML5 technology experiment that explores building a faithful and efficient renderer for the SWF file format without native code assistance. As of 2013-01-01, the plugin may be installed directly from [Mozilla's github.io site](http://mozilla.github.io/shumway/). According to the [Shumway wiki](https://github.com/mozilla/shumway/wiki), "Integration with Firefox is a possibility if the experiment proves successful."

Shumway is also embedded in Firefox Nightly/Aurora builds.

### Gnash

See also [Wikipedia:Gnash](https://en.wikipedia.org/wiki/Gnash "wikipedia:Gnash").

[GNU Gnash](http://www.gnu.org/software/gnash/) is a free (libre) alternative to Adobe Flash Player. It is available both as a standalone player for desktop computers and embedded devices, as well as a browser plugin, and supports the SWF format up to version 7 (with versions 8 and 9 under development) and about 80% of ActionScript 2.0.

There are multiple packages available: [gnash](https://aur.archlinux.org/packages/gnash/), [gnash-kde4](https://aur.archlinux.org/packages/gnash-kde4/), [gnash-git](https://aur.archlinux.org/packages/gnash-git/).

**Note:** If you find that Gnash does not work properly right out of the box, then you may also need to [install](/index.php/Pacman "Pacman") [gstreamer0.10-ffmpeg](https://aur.archlinux.org/packages/gstreamer0.10-ffmpeg/) from the [official repositories](/index.php/Official_repositories "Official repositories").

### Lightspark

[Lightspark](http://lightspark.github.com/) is another attempt to provide a free alternative to Adobe Flash aimed at supporting newer Flash formats. Lightspark has the ability to fall back on Gnash for old content, which enables users to install both and enjoy wider coverage. Although it is still very much in development, it supports some [popular sites](https://github.com/lightspark/lightspark/wiki/Site-Support).

Lightspark can be [установлен](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") with the package [lightspark](https://aur.archlinux.org/packages/lightspark/) or [lightspark-git](https://aur.archlinux.org/packages/lightspark-git/).

### Adobe Flash Player

#### Установка

Пакет, который нужно установить зависит от браузера, которым вы пользуетесь.

*   Версию NPAPI можно [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") с помощью пакета [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) из официальных репозиториев. Этот плагин больше [не поддерживается Adobe](https://blogs.adobe.com/flashplayer/2012/02/adobe-and-google-partnering-for-flash-player-on-linux.html) и остановился на версии 11.2; однако Adobe будет предоставлять обносления безопасности в течение 5 лет (т.е. до 2017).

*   Версия PPAPI распространяется вместе с Google Chrome. Если вы используете Chromium или какой-либо другой браузер, использующий интерфейс PPAPI, то смотрите [Chromium#Flash Player plugin](/index.php/Chromium#Flash_Player_plugin "Chromium") для дополнительной информации.

**Примечание:** Некоторым Flash приложениям требуется [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") для того, чтобы правильно отображать текст.

#### Configuration

To change the preferences (privacy settings, resource usage, etc.) of Flash Player, right click on any embedded Flash content and choose *Settings* from the menu, or go to the [Adobe website](http://helpx.adobe.com/flash-player/kb/find-version-flash-player.html). There, a Flash animation will give you access to your local settings.

You can also use the Flash settings file `/etc/adobe/mms.cfg`.

**Warning:** Flash hardware acceleration could be still unstable. See [[1]](https://forums.adobe.com/thread/911321)

To enable [VDPAU](/index.php/VDPAU "VDPAU"), uncomment the following line:

```
EnableLinuxHWVideoDecode=1

```

A more detailed example configuration:

 `/etc/adobe/mms.cfg` 
```
AVHardwareDisable = 0
FullScreenDisable = 0
LocalFileReadDisable = 1
FileDownloadDisable = 1
FileUploadDisable = 1
LocalStorageLimit = 1
ThirdPartyStorage = 1
AssetCacheSize = 10
AutoUpdateDisable = 1
LegacyDomainMatching = 0
LocalFileLegacyAction = 0
AllowUserLocalTrust = 0
# DisableSockets = 1 
OverrideGPUValidation = 1
DisableDeviceFontEnumeration = 1 #Prevent sites to identify you by snooping the installed fonts
```

You can also refer to the [mms.cfg from Gentoo](http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/www-plugins/adobe-flash/files/mms.cfg), which is extensively commented.

#### Disable the "Press ESC to exit full screen mode" message

**Note:** This only works for the NPAPI plugin.

For a way to disable this message see [this ubuntuforums.org post](http://ubuntuforums.org/showthread.php?t=1839293).

Backup `libflashplayer.so`:

```
# cp /usr/lib/mozilla/plugins/libflashplayer.so /usr/lib/mozilla/plugins/libflashplayer.so.backup 

```

Make a copy of it in your home directory:

```
# cp /usr/lib/mozilla/plugins/libflashplayer.so ~/

```

Install [wine](https://www.archlinux.org/packages/?name=wine) from the official repositories.

Download `Flash Fullscreen Patcher.zip` from [this page](http://forum.videohelp.com/threads/304807-How-to-remove-annoying-Press-Esc-to-message-in-Flash-Video), extract and execute with `wine`:

```
$ wget [https://www.dropbox.com/s/ssrlsnx1csdyc8p/Flash%20Fullscreen%20Patcher%20v3.00%20%2B%20Source.zip](https://www.dropbox.com/s/ssrlsnx1csdyc8p/Flash%20Fullscreen%20Patcher%20v3.00%20%2B%20Source.zip)
$ unzip Flash\ Fullscreen\ Patcher\ v3.00\ +\ Source.zip Flash\ Fullscreen\ Patcher.exe
$ wine Flash\ Fullscreen\ Patcher.exe

```

Patch `libflashplayer.so` (the one from your home directory) using the GUI. Copy the patched Flash Player back to the plugins directory:

```
# cp ~/libflashplayer.so /usr/lib/mozilla/plugins/

```

#### Multiple monitor full-screen fix

**Note:**

*   This only works for the NPAPI plugin.
*   There is also a package [flashplugin-focusfix](https://aur.archlinux.org/packages/flashplugin-focusfix/) in the [AUR](/index.php/AUR "AUR") that includes this fix.

	*sourced from this post on [webupd8](http://www.webupd8.org/2012/10/ubuntu-multi-monitor-tweaks-full-screen.html)*

When using a multiple monitor setup, or swapping between virtual desktops, it is possible to lose focus on a fullscreen flash window. In such a case, the adobe flash-plugin will automatically exit full-screen mode. This may not be to your liking.

Unfortunately, this behavior is hard coded into the binary. In order to change this behavior it is necessary to alter the binary.

First you will need a hex editor, such as [ghex](https://www.archlinux.org/packages/?name=ghex).

Then, you will need to alter the adobe flash-plugin binary, which is commonly located at `/lib/mozilla/plugins/libflashplayer.so`. It is prudent of course to first backup the file, in case you want to revert the behavior or make a mistake while editing.

```
# cp /usr/lib/mozilla/plugins/libflashplayer.so /usr/lib/mozilla/plugins/libflashplayer.so.backup 

```

Then open the binary in the hex editor with **root privileges**:

```
# ghex /usr/lib/mozilla/plugins/libflashplayer.so

```

Using the hex editor find the string `_NET_ACTIVE_WINDOW`. In ghex the readable string is on the right hand side of the window, and the hex is on the left, you are trying to locate the readable string. It should be easy to find using a search function.

Upon finding `_NET_ACTIVE_WINDOW` rewrite the line, but **do not** change the length of the line, for example `_NET_ACTIVE_WINDOW` becomes `_XET_ACTIVE_WINDOW`.

Save the binary, and restart any processes using the plugin (as this will crash any instance of the plugin in use.)

#### Fullscreen fix for GNOME 3

If you have problems with Flash's fullscreen-mode (video freezes but audio keeps playing), then it is probably because the fullscreen flash window is displayed *behind* the browser window. This is a [known upstream bug in mutter](https://bugzilla.gnome.org/show_bug.cgi?id=722743). You can easily fix this by using [devilspie](https://en.wikipedia.org/wiki/Devil%27s_Pie_(software) "wikipedia:Devil's Pie (software)"):

Install [devilspie](https://www.archlinux.org/packages/?name=devilspie) from the official repositories.

Create the `~/.devilspie` directory:

```
# mkdir ~/.devilspie

```

Now you have to create a config file for each browser you use (see below)

Finally, add devilspie to your list of startup items by adding the following file to `~/.config/autostart`

 `~/.config/autostart/devilspie.desktop` 
```
[Desktop Entry]
Name=devilspie
Exec=devilspie
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
```

##### Firefox

 `~/.devilspie/flash-fullscreen-firefox.ds` 
```
(if
(is (application_name) "plugin-container")
(begin
(focus)
)
)
```

##### Chrome / Chromium

 `~/.devilspie/flash-fullscreen-chrome.ds` 
```
(if
(is (application_name) "exe")
(begin
(focus)
)
)
```

##### Epiphany / GNOME Web

 `~/.devilspie/flash-fullscreen-epiphany.ds` 
```
(if
(is (application_name) "WebKitPluginProcess")
(begin
(focus)
)
)
```

### Video players workarounds

#### Open-with Firefox extension

1.  Install [Open-with](https://addons.mozilla.org/en-US/firefox/addon/open-with/) add-on.
2.  Open `about:openwith`, select *Add...*
3.  In the dialog select a video streaming capable player (e.g. [/usr/bin/mpv](/index.php/Mpv "Mpv")).
4.  (Optional step) Add needed arguments to the player (e.g. you may want `--force-window --ytdl` for *mpv*)
5.  (Optional step) Choose how to display the dialogs using the left panel.
6.  Right click on links or visit pages containing videos. If the site is supported, the player will open as expected.

The same procedure can be used to associate video downloaders such as *youtube-dl*.

## PDF viewer

### PDF.js

[PDF.js](https://mozillalabs.com/en-US/pdfjs/) is a PDF renderer created by Mozilla and built using HTML5 technologies.

For [Firefox](/index.php/Firefox "Firefox") it is available as a [plugin](https://addons.mozilla.org/en-US/firefox/addon/pdfjs/), which is included in [Firefox](/index.php/Firefox "Firefox") since version 19.

For [Chromium](/index.php/Chromium "Chromium") and Google Chrome there is an experimental extension in the [Chrome web store](https://chrome.google.com/webstore/detail/pdf-viewer/oemmndcbldboiebfnladdacbdfmadadm) or alternatively it can be built from the source of [Pdf.js](https://github.com/mozilla/pdf.js).

### External PDF viewers

To use an external PDF viewer you need [#MozPlugger](#MozPlugger) or [#kpartsplugin](#kpartsplugin).

If you want to use MozPlugger with Evince, for example, you have to find the lines containing `pdf` in the `/etc/mozpluggerrc` file and modify the corresponding line after `GV()` as below:

```
repeat noisy swallow(evince) fill: evince "$file"

```

(replace `evince` with something else if it is not your viewer of choice).

If this is not enough, you may need to change 2 values in `about:config`:

*   Change `pdfjs.disabled`'s value to *true*;
*   Change `plugin.disable_full_page_plugin_for_types`'s value to an empty value.

Restart and it should work like a charm!

### Adobe Reader

Due to licensing restrictions, Adobe Reader cannot be distributed from any of the official Arch Linux repositories. There are versions available in the [AUR](/index.php/AUR "AUR"). Please note that no matter how many votes it receives, Adobe Reader will never be included in the [official repositories](/index.php/Official_repositories "Official repositories").

Also, there are [localizations](https://aur.archlinux.org/packages.php?O=0&K=acroread-&do_Search=Go) available in many languages.

#### 32-bit

Adobe Acrobat Reader is only available as a 32-bit binary. It can be installed with the [acroread](https://aur.archlinux.org/packages/acroread/) package, available in the [AUR](/index.php/AUR "AUR").

This package installs the Acrobat Reader application as well as the Firefox plugin. Note that hardware-assisted rendering is unavailable under Linux (at least using a Geforce 8600GTS with driver version 185.18.14).

#### 64-bit

There is yet to be an official 64-bit version of Adobe Reader.

To use it in a 64-bit environment, you can:

*   Follow [this guide](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64") originally posted in the forums. It involves creating a chrooted environment that could be reused for other 32-bit only applications.

*   Install [acroread](https://aur.archlinux.org/packages/acroread/) (with all its 32-bit dependencies) from [AUR](/index.php/AUR "AUR"). Be advised that the [Firefox](/index.php/Firefox "Firefox") plugin cannot be used *directly* with this binary -- it will not load in the 64-bit browser. To load it install the [nspluginwrapper](https://www.archlinux.org/packages/?name=nspluginwrapper) package from the official [[multilib]](/index.php/Multilib "Multilib") repository and run:

```
$ nspluginwrapper -v -a -i

```

as a normal user. This checks the plugin directory and links the plugins as needed.

## Citrix

See [Citrix](/index.php/Citrix "Citrix").

## Java (IcedTea)

**Note:** Java [does not work on Chromium](https://www.java.com/en/download/faq/chrome.xml), since they've disabled all NPAPI pluggins. Install another browser to use any Java plugin.

To enable [Java](/index.php/Java "Java") support in your browser, you have two options: the open-source [OpenJDK](https://en.wikipedia.org/wiki/OpenJDK "wikipedia:OpenJDK") (recommended) or Oracle's proprietary version. For details about why OpenJDK is recommended see [this](https://mailman.archlinux.org/pipermail/arch-general/2011-August/021671.html).

To use OpenJDK, you have to install the [IcedTea](http://icedtea.classpath.org/wiki/Main_Page) browser plugin, [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web).

If you want to use Oracle's JRE, install the [jre](https://aur.archlinux.org/packages/jre/) (or [jre6](https://aur.archlinux.org/packages/jre6/)) package, available in the [AUR](/index.php/AUR "AUR").

See [Java#OpenJDK](/index.php/Java#OpenJDK "Java") for additional details and references.

**Note:** If you experience any problems with the Java plugin (e.g. it is not recognized by the browser), you can try this [solution](/index.php/Flash#Plugins_are_installed_but_not_working "Flash").

## Pipelight

See [Pipelight](/index.php/Pipelight "Pipelight").

## Multimedia playback

Many browsers support the [GStreamer](/index.php/GStreamer "GStreamer") framework to play multimedia inside HTML5 `<audio>` and `<video>` elements. Check the optional dependencies of the browser package (or [webkitgtk](https://aur.archlinux.org/packages/webkitgtk/)/[webkitgtk2](https://aur.archlinux.org/packages/webkitgtk2/) if using a webkit-based browser) to see which version of GStreamer is supported: this can be either `gst-*` for the current version, or `gstreamer0.10-*` for the legacy version. See [GStreamer#Installation](/index.php/GStreamer#Installation "GStreamer") for the description of each plugin.

### Other plugins

*   **Gecko Media Player** — Mozilla browser plugin to handle media on websites, using MPlayer.

	[https://sites.google.com/site/kdekorte2/gecko-mediaplayer](https://sites.google.com/site/kdekorte2/gecko-mediaplayer) || [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer)

*   **Totem Plugin** — Browser plugin based on the [Totem](https://en.wikipedia.org/wiki/Totem_(software) media player for [GNOME](/index.php/GNOME "GNOME") which uses [GStreamer](/index.php/GStreamer "GStreamer").

	[http://projects.gnome.org/totem/](http://projects.gnome.org/totem/) || [totem](https://www.archlinux.org/packages/?name=totem)

*   **Rosa Media Player Plugin** — Qt-based browser plugin also based on MPlayer.

	[https://abf.rosalinux.ru/uxteam/ROSA_Media_Player](https://abf.rosalinux.ru/uxteam/ROSA_Media_Player) || [rosa-media-player-plugin](https://aur.archlinux.org/packages/rosa-media-player-plugin/)

*   **VLC Plugin** — NPAPI-based plugin that uses VLC technologies.

	[http://git.videolan.org/?p=npapi-vlc.git;a=summary](http://git.videolan.org/?p=npapi-vlc.git;a=summary) || [npapi-vlc-git](https://aur.archlinux.org/packages/npapi-vlc-git/)

## Other

### MozPlugger

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

For a more complete list of MozPlugger options see [this page](http://www.linuxmanpages.com/man7/mozplugger.7.php).

### kpartsplugin

[The KParts plugin](http://www.unix-ag.uni-kl.de/~fischer/kpartsplugin/) is a plugin that uses KDE's KPart technology to embed different file viewers in the browser, such as Okular (for PDF), Ark (for different archives), Calligra Words (for ODF), etc. It cannot use applications that are not based on the KPart technology.

The KParts plugin can be installed with the package [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin), available in the official repositories.

## Troubleshooting

### Flash Player: no sound

Flash Player outputs its sound only through the default [ALSA](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") device, which is number **0**. If you have multiple sound devices (a very common example is having a sound card and HDMI output in the video card), then your preferred device may have a different number.

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

### Flash Player: low webcam resolution

If your webcam has low resolution in Flash (the image looks very pixelated) you can try starting your browser with this:

```
$ LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so [broswer]

```

### Flash Player: black bars in full screen playback on multi-headed setups

The Flash plugin has a known bug where the full screen mode does not really work when you have a multi-monitor setup. Apparently, it incorrectly determines the full screen resolution, so the full screen Flash Player fills the correct monitor but gets scaled as if the monitor had the resolution of the total display area.

To fix this, you can use the "hack" described [here](http://al.robotfuzz.com/content/workaround-fullscreen-flash-linux-multiheaded-desktops). Simply download the source from the link given on the page, and follow the instructions in the README.

**Совет:** The hack is available in the [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") and can be installed with the [fullscreenhack](https://aur.archlinux.org/packages/fullscreenhack/) package

**Примечание:** While the author mentions using NVDIA's TwinView, the hack should work for any multi-monitor setup

### Flash Player: blue tint on videos with NVIDIA

An issue with [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) versions 11.2.202.228-1 and 11.2.202.233-1 causes it to send the U/V panes in the incorrect order resulting in a blue tint on certain videos. Version 0.5 of [libvdpau](https://www.archlinux.org/packages/?name=libvdpau) includes a workaround to fix this, see the [official announcement](http://lists.x.org/archives/xorg-announce/2012-September/002066.html).

### Flash Player: leaking overlay with NVIDIA

This bug is due to the incorrect color key being used by the [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) version 11.2.202.228-1 (see [this post](http://www.nvnews.net/vbulletin/showpost.php?p=2514210&postcount=102) on the NVIDIA forums) and causes the Flash content to "leak" into other pages or solid black backgrounds. To avoid this issue simply export `VDPAU_NVIDIA_NO_OVERLAY=1` within either your shell profile (e.g. `~/.bash_profile` or `~/.zprofile`) or `~/.xinitrc`

### Flash Player: videos not working on older systems

If you have Adobe Flash installed on an older system and you start playing a video which simply turns black with nothing happening, it is most likely that your CPU does not support SSE2\. You can simply check this by looking at your CPU flags with this command:

```
$ grep sse2 /proc/cpuinfo

```

If no results are returned, then you need to install an older version of Flash (for example 10.3, or 11.1). Older versions possibly will have vulnerabilities. You should then consider sandboxing Firefox using [sandfox](https://aur.archlinux.org/packages/sandfox/). See the [sandfox homepage](https://igurublog.wordpress.com/downloads/script-sandfox/) for usage information.

Older versions of Flash are available here: [https://www.adobe.com/products/flashplayer/distribution3.html](https://www.adobe.com/products/flashplayer/distribution3.html) You need to copy `libflashplayer.so` to the folder `/usr/lib/mozilla/plugins/`

Older [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) packages can be downloaded from the [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") e.g. [flashplugin-10](https://aur.archlinux.org/packages/flashplugin-10/).

The most recent package without SSE2 is `flashplugin-11.1.102.63-1-i686.pkg.tar.xz`. If you use the packaged version, you have to add `IgnorePkg = flashplugin` to `/etc/pacman.conf`.

### Plugins are installed but not working

A common problem is that the plugin path is unset. This typically occurs on a new install, when the user has not re-logged in before running Firefox after the installation. Test if the path is unset:

```
echo $MOZ_PLUGIN_PATH

```

If unset, then either re-login, or source `/etc/profile.d/mozilla-common.sh` and start Firefox from the same shell:

```
source /etc/profile.d/mozilla-common.sh && firefox

```

### Gecko Media Player will not play Apple trailers

If Apple Trailers appear to start to play and then fail, try setting the user agent for your browser to:

```
QuickTime/7.6.2 (qtver=7.6.2;os=Windows NT 5.1Service Pack 3)

```