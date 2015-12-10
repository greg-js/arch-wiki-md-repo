# ASUS Zenbook UX32A

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This page contains infos and tips for installing and configuring Arch Linux on the Asus Zenbook UX32A.

## Contents

*   [1 Installation](#Installation)
*   [2 Compatibility](#Compatibility)
*   [3 Function Keys](#Function_Keys)
    *   [3.1 i3 configuration](#i3_configuration)

## Installation

The installation should work with no problems, wifi should work out of the box. The UX32A ships in two versions, either with 500 GB HDD + 24 GB SSD or with 128 GB HDD and 128 GB SSD. Since 24 GB is more then enough for a full Arch Linux installation, it is recommended to install at least the non-home partitions onto the SSD.

**Warning:** This could lead to problems if Windows stays installed on the same machine

## Compatibility

Most things work withouth problems, to controll the backlights you have to follow the instructions here: [ASUS Zenbook Prime UX31A#Keyboard backlight](/index.php/ASUS_Zenbook_Prime_UX31A#Keyboard_backlight "ASUS Zenbook Prime UX31A").

## Function Keys

The following function keys work:

*   Standby (FN+F1)
*   Screen brightness (FN+F5/F6)
*   Turn Screen on/off (FN+F7)

The other keys are recognised and yield the specific signal, with the exception of the Presentation Mode (FN+F8), which only yields 'p' and the wifi button, which isn't recognised at all.

### i3 configuration

For the i3 window manager you can use the following in your configuration to make some of the keys work:

 `~/.i3/config` 

```

bindsym XF86AudioLowerVolume exec amixer -q set Master 5-
bindsym XF86AudioRaiseVolume exec amixer -q set Master 5+
bindsym XF86AudioMute exec $(amixer get Master | grep off > /dev/null && amixer -q set Master unmute) || amixer -q set Master mute

bindsym XF86TouchpadToggle exec $(xinput list-props 12 | grep 'Device Enabled.*1$'  > /dev null && xinput set-prop 12 134 0) || xinput set-prop 12 134 1

bindsym XF86KdbBrightnessDown exec asus-kdb-backlight off
bindsym XF86KdbBrightnessUp exec asus-kdb-backlight on

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Zenbook_UX32A&oldid=376475](https://wiki.archlinux.org/index.php?title=ASUS_Zenbook_UX32A&oldid=376475)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")