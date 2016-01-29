# ASUS U32U

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:ASUS U32U#](https://wiki.archlinux.org/index.php/Talk:ASUS_U32U))

This page is aimed to collect the recipes needed after a fresh install of archlinux on a laptop from the Asus U32U serie.

**Note:** You may not need those tricks if you are using a desktop environment such as [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [Xfce](/index.php/Xfce "Xfce"),...

## Contents

*   [1 Bootloader](#Bootloader)
    *   [1.1 System Recovery](#System_Recovery)
*   [2 RF-kill issue](#RF-kill_issue)
*   [3 Sound issue](#Sound_issue)
*   [4 Microphone](#Microphone)
*   [5 Video](#Video)
*   [6 Touchpad](#Touchpad)
    *   [6.1 Multitouch](#Multitouch)
*   [7 LEDs](#LEDs)
*   [8 Special Keys](#Special_Keys)
*   [9 LID](#LID)
*   [10 SD Card Reader](#SD_Card_Reader)

## Bootloader

To show the boot menu press `Esc` during startup.

### System Recovery

In order to restore to Factory Default Settings you'll have to press `F10` at startup **AND** Recovery from the grub.

## RF-kill issue

In order to get rid of the RF-kill issue after a fresh install you should add `options asus_nb_wmi wapf=1` to `/etc/modprobe.d/asus_nb_wmi.conf`

This is not needed as of kernel release 3.19.2

## Sound issue

To get sound working you should create a user specific file `~/.asoundrc` or a system-wide file `/etc/asound.conf` with the folowing content:

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

A good configuration for the sound could be as follow:

```

Master: 100
Headphone: 100
Speaker 100
PCM: 100
Mic: 34
Mic Boost: 51
S/PDIF: M
S/PDIF D: 0
Auto-Mut: Enabled
Internal: 22
Internal: 51

```

## Microphone

A good configuration for the microphone could be as follow:

```

Mic Boost: 51
Capture: 47
Digital: 81
Internal Mic Boost: 51

```

## Video

| Brand | Type | Driver | [Multilib](/index.php/Multilib "Multilib") Package
(for 32-bit applications on Arch x86_64) |  Documentation  |
| ** AMD/ATI ** |  Open source  | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [ATI](/index.php/ATI "ATI") |
| Proprietary | [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/catalyst-dkms)]</sup> | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)<sup><small>AUR</small></sup> | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |

## Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

### Multitouch

It seems that [touchegg](https://aur.archlinux.org/packages/touchegg/)<sup><small>AUR</small></sup> can be used

## LEDs

Out of the box the wifi led does not work. Other leds seem to work.

All LEDs work on a fresh install as of release 3.19.2

## Special Keys

`Fn + F1` (**Suspends**) works out of the box

`Fn + F2` (**Toggle Wi-Fi**) works out of the box

`Fn + F5` (**Dim brightness**) works out of the box

`Fn + F6` (**Increase brightness**) works out of the box

`Fn + F7` (**Turn screen off**) works out of the box

`Fn + F8` (**Toggle multi monitor setup**) works out of the box

`Fn + F10` (**Mute**) works out of the box

`Fn + F11` (**Decrease Volume**) works out of the box

`Fn + F12` (**Increase Volume**) works out of the box

When using VLC player with Gnome, the four media keys work out of the box.

`Fn + Down` (**Play/Pause**)

`Fn + Up` (**Stop**)

`Fn + Left` (**Previous Track**)

`Fn + Right` (**Next Track**)

## LID

Closing Lid seems to suspend computer (to be confirmed, otherwise install [acpi](/index.php/Acpi "Acpi"))

## SD Card Reader

Works out of the box

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_U32U&oldid=399198](https://wiki.archlinux.org/index.php?title=ASUS_U32U&oldid=399198)"