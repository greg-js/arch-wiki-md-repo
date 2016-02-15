## Contents

*   [1 Things you should know](#Things_you_should_know)
*   [2 Foreword](#Foreword)
*   [3 Video](#Video)
*   [4 Input devices](#Input_devices)
*   [5 Networking](#Networking)

## Things you should know

1.  Touchpad is buggy - after a while driver loses contact with it and all fancy options become disabled

## Foreword

To install linux on this shiny pile of great hardware you need to use “noapic” or “acpi=noirq” kernel parameters. After you install distro you need to load modules in proper order or kernel will freeze. Ron Kuris reported lucky module order in kernel bugzilla - i2c_core nvidia snd_hda_codec cpufreq_conservative ohci_hcd snd_hda_intel ndiswrapper. I installed Arch64 and modified module preloading parameter in /etc/mkinitcpio.conf:

```
   MODULES="i2c_core bcm43xx nvidia cpufreq_conservative cpufreq_powersave cpufreq_ondemand ohci_hcd fuse usbhid powernow-k8 snd_hda_intel pata_amd ata_generic sata_nv"

```

... and rebuild initramfs (mkinitcpio -p linux)

System should work now.

## Video

This lappy has GeForceGo 7200 adapter and glossy widescreen LCD. You’ll need nvidia proprietary driver. To make use of LCD’s native resolution you need to place correct mode in /etc/X11/xorg.conf:

```
   Section "Screen"
   Identifier "Screen 1"
   Device "nVidia"
   Monitor "LCD"
   DefaultDepth 24

```

```
   Subsection "Display"
   Depth 24
   Modes "1280x800"
   ViewPort 0 0
   EndSubsection
   EndSection

```

## Input devices

To use sensor keys and remote control you need to set keyboard model in /etc/X11/xorg.conf

```
   Option "XkbModel" "hpzt11xx"

```

Add this command to some startup script, /etc/rc.local in Arch Linux:

```
   setkeycodes e008 221 e00e 226 e00c 213

```

And finally add these commands to startup of your windowmanager or desktop environment. I put them to ~/.xinitrc

```
   xmodmap -e "keycode 197 = XF86Pictures"
   xmodmap -e "keycode 237 = XF86Video"
   xmodmap -e "keycode 118 = XF86Music"

```

TODO: Add Fn+fx keys Remote control mimics keyboard, no additional software needed. Range is about 4 meters.

Touchpad is generic Synaptic. On/off switch on it is hardware, kernel seems not to like the way it works - after a while driver loses contact with device and touchpad loses all fancy features like 3rd button emulation and scrollbar.

## Networking

bcm43xx is unstable. NDISWrapper is buggy. bcm43xx developers swear bcm4311 (used in this lappy) is stable in 2.6.22, yet to test... Ethernet: works flawlessly with forcedeth module. Modem: Don’t know anything about it, i don’t think i will ever use it.

On A similar dv6000, ndiswrapper works flawlessly with the bcm4311 chipset.