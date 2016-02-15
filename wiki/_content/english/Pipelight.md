Pipelight is a special browser plugin which allows one to use Windows-only plugins inside Linux browsers. The main focus of the project is on Silverlight and its features, such as watching DRM protected videos. It works by creating a bridge between a Windows application, which handles the Windows-only plugin (e.g. Silverlight), and a native Linux browser plugin. The Windows application is run using a patched version of Wine, therefore requiring Pipelight users to move to this version. Pipelight can be used in browsers that support NPAPI plugins, such as Firefox. It does **not** work with Chromium.

**Tip:**

*   If you are here because you want to watch **Netflix** or **Amazon Instant Videos**, you do not need to install Silverlight/Pipelight. It is easier to install [google-chrome](https://aur.archlinux.org/packages/google-chrome/), which includes the Widevine content decryption plugin which satisfies Netflix's DRM requirements. This should move to other browsers e.g. Firefox (who have agreed to implement the HTML5 code) in due course.
*   If you are here because you want to watch **BlinkBox** (UK) you need to install [google-chrome](https://aur.archlinux.org/packages/google-chrome/) (Requires: version 42+) and use the [User-Agent Switcher for Chrome](https://chrome.google.com/webstore/detail/user-agent-switcher-for-c/djflhoibgkdhkhhcedjiklpkjnoahfmg) extension with a Mac UA string 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/42.0.2311.90 Safari/537.36'. Windows UA strings will result in WP209 playback errors due to HDCP.

**Note:** Pipelight playback of **BlinkBox** content (which used to work fine with the Silverlight 5.0 plugin) now appears broken.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing from the AUR](#Installing_from_the_AUR)
    *   [1.2 Installing from the unofficial pipelight repositories](#Installing_from_the_unofficial_pipelight_repositories)
*   [2 Managing plugins](#Managing_plugins)
    *   [2.1 Plug-in(s) not visible in Mozilla Firefox](#Plug-in.28s.29_not_visible_in_Mozilla_Firefox)
*   [3 User Agent](#User_Agent)
*   [4 Verification](#Verification)
*   [5 GPU Acceleration in Silverlight](#GPU_Acceleration_in_Silverlight)
    *   [5.1 Default behavior](#Default_behavior)
    *   [5.2 Force hardware acceleration](#Force_hardware_acceleration)
    *   [5.3 Disable graphics card verification](#Disable_graphics_card_verification)
*   [6 Custom variables](#Custom_variables)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Pipelight stopped working after upgrade of chromium (version 35+)](#Pipelight_stopped_working_after_upgrade_of_chromium_.28version_35.2B.29)
    *   [7.2 Silverlight plug-in error with Firefox and apparmor](#Silverlight_plug-in_error_with_Firefox_and_apparmor)
    *   [7.3 Videos playing very fast and no sound / bad sound quality](#Videos_playing_very_fast_and_no_sound_.2F_bad_sound_quality)
    *   [7.4 GNOME 3/Firefox fullscreen issues](#GNOME_3.2FFirefox_fullscreen_issues)
    *   [7.5 Pipelight renders all Chinese characters as squares](#Pipelight_renders_all_Chinese_characters_as_squares)
    *   [7.6 No sound when using PulseAudio](#No_sound_when_using_PulseAudio)
*   [8 Tips](#Tips)
    *   [8.1 Test 1080p video playback](#Test_1080p_video_playback)
*   [9 See also](#See_also)

## Installation

**Warning:** NPAPI support has been dropped from Chrome/Chromium. Pipelight only works on a browser (e.g. FireFox) with enabled NPAPI support.

Pipelight is not presently available in the [official repositories](/index.php/Official_repositories "Official repositories"), and can be either installed from the [AUR](/index.php/AUR "AUR") or the unofficial [[pipelight]](/index.php/Unofficial_user_repositories#pipelight "Unofficial user repositories") repository, maintained by the Pipelight developers.

### Installing from the AUR

Pipelight is available in the [AUR](/index.php/AUR "AUR") as the [pipelight](https://aur.archlinux.org/packages/pipelight/) package.

### Installing from the unofficial pipelight repositories

Pre-built Pipelight packages for Arch Linux can be obtained from the unofficial [pipelight](/index.php/Unofficial_user_repositories#pipelight "Unofficial user repositories") repository, which is maintained by the Pipelight developers. Since these packages are pre-built, it does not require the time expensive task of compiling wine from sources. If you are running a 64-bit system, you will need to enable the [Multilib](/index.php/Multilib "Multilib") repository first.

## Managing plugins

Pipelight can be used to manage browser plugins including Silverlight, Adobe Flash Player/Shockwave Player.

Update the plugins:

```
# pipelight-plugin --update

```

To list all available plugins:

```
$ pipelight-plugin --help

```

Enable the plugin globally:

```
# pipelight-plugin --enable _plugin_

```

or locally:

```
$ pipelight-plugin --enable _plugin_

```

### Plug-in(s) not visible in Mozilla Firefox

If upon starting [Firefox](/index.php/Firefox "Firefox") the enabled plugin doesn't appear under `about:plugins`, try running the following command before starting Mozilla Firefox:

```
# pipelight-plugin --create-mozilla-plugins

```

## User Agent

Since some sites (e.g. Netflix) refuse to stream to a Linux browser, the user agent may have to be [changed](https://answers.launchpad.net/pipelight/+faq/2351).

## Verification

There is a test page available [here](http://bubblemark.com/sl3/TestPage.html). Alternatively, detected plugins can be listed in `about:plugins`.

## GPU Acceleration in Silverlight

### Default behavior

Silverlight applets may include an option called `enableGPUAcceleration` which controls whether or not [hardware acceleration](http://en.wikipedia.org/wiki/Hardware_acceleration) should be used (i.e. use the graphics card for video playback). This option is under the control of specific website's administrator, but this option can also be forced from the client's side (see below). By default, GPU acceleration is only enabled on verified systems cards **and** pages that require it. Herein, system verification is executed through the bash script `/usr/share/pipelight/hw-accel-default` that checks the graphics card vendor. Note that this script depends on the `glxinfo` utility, which is part of [mesa-demos](https://www.archlinux.org/packages/?q=mesa-demos). Make sure this package is installed if you want to Pipelight's graphics verification method.

### Force hardware acceleration

To take control of the `enableGPUAcceleration` option yourself and enable hardware acceleration by default, perform the following steps:

```
# nano /usr/share/pipelight/configs/pipelight-silverlight5.1

```

Change the following line:

```
# overwriteArg      = enableGPUAcceleration=true

```

to:

```
overwriteArg      = enableGPUAcceleration=true

```

### Disable graphics card verification

Pipelight has been tested on graphics cards from several vendors. The known-to-work card are whitelisted and are the only cards that Pipelight enables hardware acceleration on by default. This behavior can be circumvented by disabling the hardware verification procedure. However, it is recommended to check the output of the verfication procedure first. Make sure you have [mesa-demos](https://www.archlinux.org/packages/?q=mesa-demos) installed and run:

```
/usr/share/pipelight/hw-accel-default
echo $?

```

If this returns `0`, your card is identified as a whitelisted card, otherwise it is not. In that case, you might try to disable verification. First copy Pipelight's default Silverlight configuration file to your home directory (see above), then change:

```
silverlightGraphicDriverCheck  = /usr/share/pipelight/hw-accel-default

```

to:

```
silverlightGraphicDriverCheck = /bin/true

```

## Custom variables

The selection of custom variables found in Wine-Silverlight and Pipelight are as following:

*   [wine-silverlight](https://aur.archlinux.org/packages/wine-silverlight/)

1.  `customprefix`
    *   Installs Wine to `/opt` instead of `/usr` (to not conflict with [wine](https://www.archlinux.org/packages/?name=wine)).
2.  `_prefix`
    *   Allows setting a custom location.

*   [pipelight](https://aur.archlinux.org/packages/pipelight/)

1.  `_prefix`
    *   Allows setting a custom location. Default is `/usr`.
2.  `_wine`
    *   Location of Wine-Silverlight.

For example, to install Wine-Silverlight in `/opt`:

*   **wine-silverlight:** set `customprefix=1`.
*   **pipelight**: set `_wine=/opt/wine-silverlight`.

**Warning:** Failure to do this in the PKGBUILD will result in the files having to be modified manually.

## Troubleshooting

### Pipelight stopped working after upgrade of chromium (version 35+)

NPAPI support has now been dropped from chromium. If you want to recompile in NPAPI support yourself, patches from Michael Müller are attached to this bug [[1]](https://bugs.archlinux.org/task/40676?string=chromium&project=1&search_name=&only_watched=1&type%5B0%5D=&sev%5B0%5D=&pri%5B0%5D=&due%5B0%5D=&reported%5B0%5D=&cat%5B0%5D=&status%5B0%5D=open&percent%5B0%5D=&opened=&dev=&closed=&duedatefrom=&duedateto=&changedfrom=&changedto=&openedfrom=&openedto=&closedfrom=&closedto=) The patches are originally from: [[2]](https://bugs.launchpad.net/ubuntu/+source/chromium-browser/+bug/1307989)

### Silverlight plug-in error with Firefox and apparmor

If you are running [AppArmor](/index.php/AppArmor "AppArmor") and Firefox, you may see an error when loading Silverlight plug-in. You will need to modify or create an apparmor profile.

### Videos playing very fast and no sound / bad sound quality

**Note:** This solution is taken from [this](https://answers.launchpad.net/pipelight/+question/236240) page at the Pipelight's LaunchPad page and editted to reflect changes in newer version of Pipelight.

One of the causes of bad sound quality or laggy playback might be the use of [PulseAudio](/index.php/PulseAudio "PulseAudio"). Since Pipelight uses wine to handle the audio playback, changing the audio output module there can solve some problems. A good alternative to [PulseAudio](/index.php/PulseAudio "PulseAudio") is [alsa](/index.php/Alsa "Alsa") and can be enabled as follows.

First download, install and run the winetricks plugin.

```
$ wget -O ~/.wine-pipelight/winetricks [http://winetricks.org/winetricks](http://winetricks.org/winetricks)
$ chmod +x ~/.wine-pipelight/winetricks
$ WINEPREFIX=~/.wine-pipelight WINE=/opt/wine-compholio/bin/wine WINEARCH=win32 ~/.wine-pipelight/winetricks

```

Choose: "Select the default wineprefix" -> "Change Wine settings" -> "sound=alsa"

Then test whether this solves your problem (restart your browser and open a Silverlight video). If not, change the audio output device in wine to analog. Run the wine configuration utility:

```
WINEPREFIX=~/.wine-pipelight WINE=/opt/wine-compholio/bin/wine WINEARCH=win32 /opt/wine-compholio/bin/winecfg

```

Open the _Audio_ tab and change the **Output device** to `Out: HDA Intel - ALC1200 Analog`

**Note:** The actual device name may vary from system to system.

This may solve video lagging issues if PulseAudio was causing it. ALSA audio might still go through PulseAudio though, if you have pulseaudio-alsa installed. This is not a problem by itself, but you may have to restart PulseAudio. This is done by runnning:

```
$ pulseaudio -k

```

### GNOME 3/Firefox fullscreen issues

In GNOME 3, fullscreen pipelight windows do not focus properly in firefox. This can be fixed using [devilspie](https://en.wikipedia.org/wiki/Devil%27s_Pie_(software) "wikipedia:Devil's Pie (software)"):

First, install [devilspie](https://www.archlinux.org/packages/?name=devilspie) from the official repositories,

Create the `~/.devilspie` directory:

```
$ mkdir ~/.devilspie

```

Next, create the following file:

 `~/.devilspie/pipelight-fullscreen-firefox.ds` 

```
(if
    (and
        (is (window_class) "Wine")
        (or
            (is (application_name) "Adobe Flash Player")
            (is (application_name) "Microsoft Silverlight")
        )
    )
    (begin
        (focus)
    )
)
```

Finally we need to make devilspie autostart. This can be accomplished by creating the following file:

 `~/.config/autostart/devilspie.desktop` 

```
[Desktop Entry]
Name=devilspie
Exec=devilspie
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
```

### Pipelight renders all Chinese characters as squares

Silverlight will only use ”Microsoft Yahei” font to render Chinese characters, you need to install this font (probably from other Windows OSes) to support Chinese character rendering

Other known issues and solutions are often listed in the [Pipelight FAQ](https://answers.launchpad.net/pipelight/+faqs).

### No sound when using PulseAudio

If you are using PulseAudio you may get no sound from Silverlight applications. To allow wine to use PulseAudio you have to install [libpulse](https://www.archlinux.org/packages/?name=libpulse) and [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa). On 64-bit systems use [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins). You can configure the used audio device using `WINEPREFIX="/home/username/.wine-pipelight" winecfg`

## Tips

### Test 1080p video playback

To verify your Pipelight installation and check its performance on high definition videos, you can use [this](http://www.iis.net/media/experiencesmoothstreaming1080p) video for testing purposes.

## See also

*   [Launchpad FAQ](https://answers.launchpad.net/pipelight/+faqs)
*   [Official website](http://fds-team.de/cms/articles/2013-08/pipelight-using-silverlight-in-linux-browsers.html)
*   [Launchpad](https://launchpad.net/pipelight/)