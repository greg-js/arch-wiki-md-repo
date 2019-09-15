From the [osu! wiki](https://osu.ppy.sh/help/wiki/Welcome):

	a free-to-win rhythm game developed by peppy with four game modes: osu!standard, a circle clicking simulator; osu!taiko, a drumming emulator; osu!catch, a fruit salad catcher; and osu!mania, a key smashing synthesizer.

Currently, the game is being rewritten in C# with better Linux support, but in the meanwhile, a solution with Wine has to be established. This article will provide instructions on setting up osu! and provide various tricks to achieve performance up to par (if not better) than on its main intended platform.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Video drivers](#Video_drivers)
    *   [1.2 Graphics tablet](#Graphics_tablet)
    *   [1.3 Mouse](#Mouse)
    *   [1.4 Installing Wine and other components](#Installing_Wine_and_other_components)
    *   [1.5 Configuring Wine](#Configuring_Wine)
    *   [1.6 Installing the game](#Installing_the_game)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Odd font rendering](#Odd_font_rendering)
    *   [2.2 Sound latency](#Sound_latency)
        *   [2.2.1 Wine latency patches](#Wine_latency_patches)
    *   [2.3 Choppy approach circles](#Choppy_approach_circles)

## Prerequisites

### Video drivers

It is recommended to run the game under [Xorg](/index.php/Xorg "Xorg"). If [Wayland](/index.php/Wayland "Wayland") is used, the game still needs to be ran through XWayland by lack of support from Wine, which may have a performance hit.

Empirically with regards to performance, when using an AMD video card, the open source drivers are preferred. When it comes to Nvidia, the proprietary drivers are preferred. For Intel integrated graphics, the drivers which come with the kernel tend to suffice.

To check if your driver is properly accelerating graphics, consult:

```
glxinfo | grep render

```

**Note:** For further information, see [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") and [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg")

Furthermore, be sure your refresh rate is set to the most optimal setting using a display configuration utility such as [xrandr](/index.php/Xrandr "Xrandr").

### Graphics tablet

**Note:** For further information, refer to the main article [Wacom tablet](/index.php/Wacom_tablet "Wacom tablet"). Touchscreen users may wish to review this page as well.

The most common input pointing device used by more involved players is the graphics tablet.

The [Linux Wacom Project](https://linuxwacom.github.io/) provides excellent support for the majority of tablets, including many non-Wacom tablets. Conveniently, the Arch kernel includes said driver and your tablet should be recognized and work right out of the box. Though, to fine-tune the properties of the tablet such as its area or button configuration, it is desired to [install](/index.php/Install "Install") the X driver [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) which provides the `xsetwacom` utility.

If you are using an obscure tablet which does not enjoy full support, there is a chance it is supported by the [DIGImend project](https://digimend.github.io/).

### Mouse

**Tip:** See [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration") and [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate") to fully configure your mouse

The most important setting is to disable mouse acceleration:

```
xset m 0 0

```

### Installing Wine and other components

A custom Wine package specifically for osu! has been created with specific latency patches, see [#Wine latency patches](#Wine_latency_patches).

[Install](/index.php/Install "Install") the following packages:

[wine-staging](https://www.archlinux.org/packages/?name=wine-staging), [winetricks](https://www.archlinux.org/packages/?name=winetricks), [libpng](https://www.archlinux.org/packages/?name=libpng) and [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng).

If [wine](https://www.archlinux.org/packages/?name=wine) is already installed, you may wish to keep this package instead as wine-staging is not exactly necessary.

### Configuring Wine

**Note:** For the remainder of this article, it is assumed you install osu! in `~/osu-wine/`

Create the prefix and install necessary packages:

```
env WINEPREFIX=~/osu-wine WINEARCH=win32 winetricks -q dotnet462 cjkfonts gdiplus

```

### Installing the game

Download the game and install it using the prefix we made prior:

```
curl -O [https://m1.ppy.sh/r/osu!install.exe](https://m1.ppy.sh/r/osu!install.exe)
env WINEPREFIX=~/osu-wine WINEARCH=win32 wine ./osu\!install.exe

```

The installer tends to install the game under the directory `C:\Users\youruser\Local Settings\Application Data\osu!`. Pay proper attention to the installation directory before the installation takes place.

## Troubleshooting

If above instructions have been followed, the following issues are common problems which may occur.

### Odd font rendering

Use font smoothing:

```
env WINEPREFIX=~/osu-wine WINEARCH=win32 winetricks settings fontsmooth=rgb

```

Refer to [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts") if you are still dissatisfied with the result.

### Sound latency

You can achieve slightly less delay by surpassing Pulse and interfacing directly to ALSA:

```
env WINEPREFIX=~/osu-wine WINEARCH=win32 winetricks sound=alsa

```

A small tweak can also be applied to the registry:

```
cat > dsound.reg << "EOF"
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Wine\DirectSound]
"HelBuflen"="512"
"SndQueueMax"="3"
EOF

env WINEPREFIX=~/osu-wine WINEARCH=win32 wine regedit dsound.reg

```

#### Wine latency patches

Wine can be configured to provide less sound latency. A dedicated member of this game community maintains a dated version of Wine with some applied [patches](https://blog.thepoon.fr/osuLinuxAudioLatency/#inside-winepulsedrv).

You can either:

*   [Install](/index.php/Install "Install") [wine-osu](https://aur.archlinux.org/packages/wine-osu/). This might take some time to compile.
*   Install a binary version of the same version of Wine by [adding in a package repository](https://blog.thepoon.fr/osuLinuxAudioLatency/#arch-linux-users).

### Choppy approach circles

Limit your maximum frame rate in your user config file `osu!.user.cfg` such that it has the highes value your computer can handle stably, e.g.

```
CustomFrameLimit = 1000

```