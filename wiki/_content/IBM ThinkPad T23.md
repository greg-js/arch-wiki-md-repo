# IBM ThinkPad T23

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Video Card](#Video_Card)
        *   [1.1.1 Easy Installation](#Easy_Installation)
        *   [1.1.2 Advanced Installation](#Advanced_Installation)
            *   [1.1.2.1 Configuration](#Configuration_2)
            *   [1.1.2.2 Troubleshooting](#Troubleshooting)
    *   [1.2 Power Management](#Power_Management)
        *   [1.2.1 Suspend and Hibernate](#Suspend_and_Hibernate)
        *   [1.2.2 Sleepmode](#Sleepmode)
        *   [1.2.3 Laptop Mode Tools](#Laptop_Mode_Tools)
        *   [1.2.4 CPU frequency scaling](#CPU_frequency_scaling)
        *   [1.2.5 Tp_smapi](#Tp_smapi)
    *   [1.3 Hotkeys](#Hotkeys)
        *   [1.3.1 tpb](#tpb)
        *   [1.3.2 NumLock](#NumLock)
*   [2 See also](#See_also)

## Configuration

### Video Card

#### Easy Installation

Make sure [Xorg](/index.php/Xorg "Xorg") is installed, and then [install](/index.php/Install "Install") [xf86-video-savage](https://www.archlinux.org/packages/?name=xf86-video-savage) from the [official repositories](/index.php/Official_repositories "Official repositories").

Then, edit your [xorg.conf](/index.php/Xorg.conf "Xorg.conf") to reflect the following contents:

```
# xorg.conf -'man xorg.conf'
# see also 'man savage' for more detailed options
```

```
  ...
  Section "Device"
    Identifier "gfxcard"
    Driver "savage"
  EndSection

  Section "Screen"
    Identifier             "Screen0"  #Collapse Monitor and Device section to Screen section
    Device                 "gfxcard"
    Monitor                "Monitor0"
    DefaultDepth            16 
  EndSection
  ...
```

	→ See also: [Xorg](/index.php/Xorg "Xorg")

#### Advanced Installation

Thanks to Conor Behan for [this post](https://bbs.archlinux.org/viewtopic.php?id=137666) and [User:mulesryan](https://wiki.archlinux.org/index.php/User:Mulesryan) for figuring out this chipset.

The savage driver supports two types of hardware acceleration: XAA and EXA. Unfortunately, you can use DRI for SuperSavage **only if** you are using XAA. Since you want hardware 3D (for instance, opengl/d3d in wine) then this is probably important.

This means you must run [xorg-server](/index.php?title=Xorg-server&action=edit&redlink=1 "Xorg-server (page does not exist)") < 1.13, because starting in 1.13 XAA was removed.

| Video Card | Xorg Driver | Mesa DRI Driver | Packages needed for DRI |
| **S3 SuperSavage IX** | [xf86-video-savage](https://www.archlinux.org/packages/?name=xf86-video-savage) | [savage-dri](https://www.archlinux.org/packages/?name=savage-dri) | [xf86-video-savage](https://www.archlinux.org/packages/?name=xf86-video-savage) (<2.3.6-2) [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) (<1.13), [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) (<2.7.3-2), [xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev) (<0.4.3-2), [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa) (<2.3.2-2) |

##### Configuration

 `xorg.conf` 

```
 ...
 Section "Extensions"
        Option "Composite" "Enable"
        Option "RENDER" "Enable"
 EndSection

 Section "Device"
        Identifier "gfxcard"
        Driver "savage"
        Option "hwcursor" "1"
        Option "DPMS" "on"
        Option "backingstore"
        Option "BusType" "AGP"
        Option "AGPMode" "4"
        Option "AGPSize" "16" 
        Option "AccelMethod" "XAA" 
        Option "DRI" "true"
        Option "BCIforXv" "true"
        Option "AGPforXv" "true"
 EndSection

 Section "DRI"
    Mode 0666
 EndSection
 ...
```

If you've set up everything correctly, you should see this in /var/log/Xorg.0.log:

```
[ 63286.129] (II) SAVAGE(0): [DRI] installation complete
...
[ 63286.132] (II) SAVAGE(0): Direct rendering enabled
..
[ 63286.233] (II) AIGLX: enabled GLX_SGI_make_current_read
[ 63286.233] (II) AIGLX: Loaded and initialized savage
[ 63286.233] (II) GLX: Initialized DRI GL provider for screen 0

```

##### Troubleshooting

```
[  2864.984] (EE) AIGLX: reverting to software rendering
[  2865.028] (II) AIGLX: Loaded and initialized swrast
[  2865.028] (II) GLX: Initialized DRISWRAST GL provider for screen 0

```

Are you using the versions of the packages specified? Are you using XAA acceleration? Did you compile with the configure flags specified?

### Power Management

#### Suspend and Hibernate

Works flawlessly. See [Suspend to Disk](/index.php/Suspend_to_Disk "Suspend to Disk"). Also known to work with [Pm-utils](/index.php/Pm-utils "Pm-utils").

#### Sleepmode

An easy way is to use "suspend to swap" by appending

```
resume=/dev/sd_x_ 

```

to the kernel line in `/boot/grub/menu.lst`

[Sleepmode](https://wiki.archlinux.org/index.php/Sleepmode)

#### Laptop Mode Tools

Works flawlessly. See [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools").

#### CPU frequency scaling

Works as described in [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

#### Tp_smapi

See [Tp_smapi](/index.php/Tp_smapi "Tp smapi")

### Hotkeys

They work better after loading the thinkpad_acpi module, to assign the generated keycodes to their supposed functions.

#### tpb

Install [tpb](https://aur.archlinux.org/packages/tpb/), available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

tpb (for **T**hink**p**ad **B**uttons) adds an on-screen volume bar for the volume buttons, **THINKPAD** button assignment, on-screen messages for **Thinklight**, (on and off) and more.

#### NumLock

If not already working, this key may be configured by adding:

```
keycode 77 = Num_Lock 

```

to `~/.xmodmap`.

## See also

*   [Thinkwiki](http://www.thinkwiki.org/wiki/Category:T23)

Retrieved from "[https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_T23&oldid=412098](https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_T23&oldid=412098)"