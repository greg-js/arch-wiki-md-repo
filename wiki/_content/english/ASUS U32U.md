This page is aimed to collect the recipes needed after a fresh install of archlinux on a laptop from the Asus U32U serie.

**Note:** You may not need those tricks if you are using a desktop environment such as [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [Xfce](/index.php/Xfce "Xfce"),...

## Contents

*   [1 Bootloader](#Bootloader)
    *   [1.1 System Recovery](#System_Recovery)
*   [2 Sound issue](#Sound_issue)
*   [3 Microphone](#Microphone)

## Bootloader

To show the boot menu press `Esc` during startup.

### System Recovery

In order to restore to Factory Default Settings you'll have to press `F10` at startup **AND** Recovery from the grub.

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