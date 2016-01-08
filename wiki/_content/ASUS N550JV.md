# ASUS N550JV

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Intel</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>xf86-video-intel</td>

</tr>

<tr>

<td>Nvidia</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>nouveau _or_ nvidia</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>r8169</td>

</tr>

<tr>

<td>Wireless</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>ath9k</td>

</tr>

<tr>

<td>Audio</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>xf86-input-synaptics</td>

</tr>

<tr>

<td>Camera</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>linux-uvc</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>rtsx_usb</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>btusb</td>

</tr>

</tbody>

</table>

[ASUS N550JV](http://www.asus.com/Notebooks_Ultrabooks/N550JV/specifications/) - this article covers hardware specific configuration. All topics covered can be performed after an installation of Arch Linux has been finished and the machine rebooted into it.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Video](#Video)
        *   [1.1.1 Install](#Install)
        *   [1.1.2 Brightness](#Brightness)
    *   [1.2 Audio](#Audio)
    *   [1.3 Keyboard](#Keyboard)
        *   [1.3.1 Brightness](#Brightness_2)
        *   [1.3.2 Incorrectly mapped buttons](#Incorrectly_mapped_buttons)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Audio](#Audio_2)
        *   [2.1.1 Dual boot](#Dual_boot)
        *   [2.1.2 Bug](#Bug)
        *   [2.1.3 Sound pops twice during shutdown and sleep](#Sound_pops_twice_during_shutdown_and_sleep)
    *   [2.2 Power](#Power)
        *   [2.2.1 Messages during console login](#Messages_during_console_login)
        *   [2.2.2 RF Kill Switch](#RF_Kill_Switch)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Touchpad switch](#Touchpad_switch)
    *   [3.2 Special keys for window managers](#Special_keys_for_window_managers)

## Configuration

### Video

#### Install

Install [bumblebee along with Nvidia and Intel drivers](/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNVIDIA "Bumblebee"). Add the kernel parameter `rcutree.rcu_idle_gp_delay=1` to your bootloader configuration, so that _optirun_ will not fail to start.

#### Brightness

`FN+F5` and `FN+F6` will not produce any output (will not work) untill you use the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `acpi_osi=` to your bootloader. It's indeed followed by a blank space.

### Audio

Install [PulseAudio](/index.php/PulseAudio "PulseAudio").

After installation, reboot the laptop to ensure all modules are loaded. Check if the fallback device is correctly set to _Build-in Audio Analog Stereo_ with [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol). See [PulseAudio/Troubleshooting#Fallback device is not respected](/index.php/PulseAudio/Troubleshooting#Fallback_device_is_not_respected "PulseAudio/Troubleshooting") for more information. Also check for muted devices:

```
$ alsamixer -c PCH

```

**Note:** [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) provides `alsamixer` and `amixer` shell programs.

### Keyboard

#### Brightness

In some cases, `FN+F3` and `FN+F4` might not work out of box with some [desktop environments](/index.php/Desktop_environments "Desktop environments"), so install [asus-kbd-backlight](https://aur.archlinux.org/packages/asus-kbd-backlight/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"). Load the module to control hotkeys:

```
# modprobe asus-nb-wmi

```

and [start and enable](/index.php/Enable "Enable") the `asus-kbd-backlight.service`.

Now you can take control over the keyboard backlight:

```
$ asus-kbd-backlight up
$ asus-kbd-backlight down
$ asus-kbd-backlight max
$ asus-kbd-backlight off
$ asus-kbd-backlight night
$ asus-kbd-backlight 2
$ asus-kbd-backlight show

```

#### Incorrectly mapped buttons

`Media` and `FN+F7` buttons are not mapped correctly. It is not necessary to remap `FN+F7` shortcut, because it works without any additional configuration.

Install [xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap), which provides app `xmodmap`. Generate a xmodmap config file if you haven't done it already:

```
$ xmodmap -pke > ~/.Xmodmap

```

Then open it and locate keycode 234:

 `~/.Xmodmap` 

```
...
keycode 233 = XF86MonBrightnessUp NoSymbol XF86MonBrightnessUp
**keycode 234 = XF86AudioMedia NoSymbol XF86AudioMedia**
keycode 235 = XF86Display NoSymbol XF86Display
...

```

Now move `XF86AudioMedia NoSymbol XF86AudioMedia` text on the empty keycode 248 and leave keycode 234 empty:

 `~/.Xmodmap` 

```
...
**keycode 234 =** 
...
...
...
keycode 247 =
**keycode 248 = XF86AudioMedia NoSymbol XF86AudioMedia**
keycode 249 =
...

```

Optionally, for `FN+F7` give some value on keycode 253.

 `~/.Xmodmap` 

```
...
keycode 252 =
**keycode 253 = XF86Launch0 NoSymbol XF86Launch0**
keycode 254 =
...

```

The next step is apply changes:

```
$ xmodmap ~/.Xmodmap

```

Test with `xev` or try to bind something on media button. `FN+F7` should be controlled by hardware and switch display without any additional configuration. Also, if you are satisfied, put the command above to [Xinitrc](/index.php/Xinitrc "Xinitrc").

 `~/.xinitrc` 

```
{ sleep 10; xmodmap ~/.Xmodmap; } &

```

## Troubleshooting

### Audio

##### Dual boot

If you boot your laptop right after Windows to Linux, sound might only work through headphones jack, but not through speakers and subwoofer. The quick fix is to suspend your laptop and resume it back.

##### Bug

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** The bug might not be a bug for everyone (means just me). Can anyone let me know in the talk page whether they have it as well or not? (Discuss in [Talk:ASUS N550JV#](https://wiki.archlinux.org/index.php/Talk:ASUS_N550JV))

The internal speakers seems not to play any sound until volume is being increased significantly. This also occurs on Windows operation system as well as on Linux.

#### Sound pops twice during shutdown and sleep

Create new file:

 `/etc/systemd/system/beep-disable.service` 

```
[Unit]
Description=Unloads audio module to prevent beep on shutdown
DefaultDependencies=no

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'rmmod snd_hda_intel'

[Install]
WantedBy=shutdown.target suspend.target

```

and one more:

 `/etc/systemd/system/beep-disable-wakeup.service` 

```
[Unit]
Description=Load sound module back on system resume
After=suspend.target
Wants=local-system-resume.service
Before=local-system-resume.service

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'modprobe snd_hda_intel'

[Install]
WantedBy=suspend.target

```

Then [enable](/index.php/Enable "Enable") `beep-disable.service` and `beep-disable-wakeup.service` as root.

### Power

#### Messages during console login

After booting up, when Linux asks you to enter your login and password, some messages might appear similar to these:

```
Nouveau E[    PBUS][0000:01:00.0] MIMO write of 0x00000002 FAULT at 0x4188ac [ IBUS]
Nouveau E[    DRM] Pointer to TMDS table invalid
Nouveau E[    DRM] Pointer to flat panel table invalid

```

The quick fix is to press Enter several times so you will see `Login:` again. Use graphical login manager instead of command line.

**Note:** After installing correct drivers, this message should not appear anymore.

#### RF Kill Switch

You might get this message during boot, but the number after rfkill (e.g. rfkill**2**) could be different:

```
Failed to start Load/Save RF Kill Switch Status of rfkill2

```

The first thing you should try is to install [rfkill](https://www.archlinux.org/packages/?name=rfkill). If the messages remains - just ignore it.

## Tips and tricks

### Touchpad switch

The touchpad can be toggled using a `xinput` [script](/index.php/Touchpad_Synaptics#Software_toggle "Touchpad Synaptics").

### Special keys for window managers

If you prefer using a [Window manager](/index.php/Window_manager "Window manager") rather than a [Desktop environment](/index.php/Desktop_environment "Desktop environment"), most settings will not work out of the box, so you might need to manually bind every single `FN` button combination. How to bind, see [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg").

<table class="wikitable"><caption>FN buttons output</caption>

<tbody>

<tr>

<th>Buttons</th>

<th>Output</th>

</tr>

<tr>

<td>Media Button</td>

<td>XF86AudioMedia (xmodmap)</td>

</tr>

<tr>

<td>FN + F1</td>

<td>XF86Sleep</td>

</tr>

<tr>

<td>FN + F2</td>

<td>XF86WLAN</td>

</tr>

<tr>

<td>FN + F3</td>

<td>XF86KbdBrightnessDown</td>

</tr>

<tr>

<td>FN + F4</td>

<td>XF86KbdBrightnessUp</td>

</tr>

<tr>

<td>FN + F5</td>

<td>XF86MonBrightnessDown</td>

</tr>

<tr>

<td>FN + F6</td>

<td>XF86MonBrightnessUp</td>

</tr>

<tr>

<td>FN + F7</td>

<td>XF86Launch0 (xmodmap)</td>

</tr>

<tr>

<td>FN + F8</td>

<td>XF86Display</td>

</tr>

<tr>

<td>FN + F9</td>

<td>XF86TouchpadToggle</td>

</tr>

<tr>

<td>FN + F10</td>

<td>XF86AudioMute</td>

</tr>

<tr>

<td>FN + F11</td>

<td>XF86AudioLowerVolume</td>

</tr>

<tr>

<td>FN + F12</td>

<td>XF86AudioRaiseVolume</td>

</tr>

<tr>

<td>FN + C</td>

<td>XF86Launch1</td>

</tr>

<tr>

<td>FN + V</td>

<td>XF86WebCam</td>

</tr>

<tr>

<td>FN + Space</td>

<td>XF86Launch6</td>

</tr>

<tr>

<td>FN + NumEnter</td>

<td>XF86Calculator</td>

</tr>

<tr>

<td>FN + Left</td>

<td>XF86AudioPrev</td>

</tr>

<tr>

<td>FN + Right</td>

<td>XF86AudioNext</td>

</tr>

<tr>

<td>FN + Up</td>

<td>XF86AudioStop</td>

</tr>

<tr>

<td>FN + Down</td>

<td>XF86AudioPlay</td>

</tr>

<tr>

<td>FN + Delete</td>

<td>Insert</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_N550JV&oldid=414647](https://wiki.archlinux.org/index.php?title=ASUS_N550JV&oldid=414647)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")