# Sony vaio VGN-SA/SB

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

SONY VAIO SA/SB ( S series ) **Model No. VPCSA**/VPCSB****

*   First edition of this article: kernel 3.3.5

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Wired/Wireless](#Wired.2FWireless)
    *   [1.2 Hybrid Graphics](#Hybrid_Graphics)
        *   [1.2.1 Disable discrete graphics on boot with a systemd unit](#Disable_discrete_graphics_on_boot_with_a_systemd_unit)
        *   [1.2.2 ATI disabled on boot. Get long battery life.](#ATI_disabled_on_boot._Get_long_battery_life.)
        *   [1.2.3 Use both at any time. Switchable.](#Use_both_at_any_time._Switchable.)
        *   [1.2.4 New functions. Set variety.](#New_functions._Set_variety.)
    *   [1.3 Touchpad](#Touchpad)
    *   [1.4 Optical(Secondary Channel)](#Optical.28Secondary_Channel.29)
    *   [1.5 HDD/SSD(Primary Channel)](#HDD.2FSSD.28Primary_Channel.29)
*   [2 Power Management](#Power_Management)
    *   [2.1 Sandy/Ivy bridge issue](#Sandy.2FIvy_bridge_issue)
    *   [2.2 CPU](#CPU)

## Hardware

### Wired/Wireless

Some udev errors are shown at boot like this:

```
[   16.369825] Bad LUN (0:2)

[   16.392657] Bad target number (1:0)

[   16.405941] Bad target number (2:0)

[   16.419294] Bad target number (3:0)

[   16.469295] Bad target number (4:0)

[   16.522611] Bad target number (5:0)

[   16.575913] Bad target number (6:0)

[   16.629228] Bad target number (7:0)

```

However, nothing to effect in use. If you want to solve these messages, realtek official drivers may be required.

### Hybrid Graphics

**"STAMINA-SPEED" switch is designed as a software switch. This DIP switch is located on one of the individual circuit from mainboard, separately.** For easy to understand it, just imagine such as a wireless switch on laptop computers. Therefore, there is nothing to do; feel free to control this switch. Follows are only suggestions within ATI models, your style to go.

#### Disable discrete graphics on boot with a systemd unit

You can use systemd to automatically disable your discrete graphics card on boot. You need to make a script file and a service file. You won't need to do what's in section 2.2.2 if you do this

1) First, make a script file in `/usr/lib/systemd/scripts` an example name would be `ati_off`.

```
#!/bin/bash
echo OFF > /sys/kernel/debug/vgaswitcheroo/switch

```

2) Next, make a service file (e.g. atioff.service) in `/usr/lib/systemd/system`.

```
[Unit]
Description=Turn off the discrete graphics card on boot

[Service]
Type=oneshot
ExecStart=/bin/bash /usr/lib/systemd/scripts/ati_off
RemainAfterExit=no

[Install]
Wantedby=multi-user.target

```

Now [enable](/index.php/Enable "Enable") `atioff.service`.

#### ATI disabled on boot. Get long battery life.

If you want to get more long battery life first, take this method is recommended.

1) mounting debugfs

```
# mount -t debugfs debugfs /sys/kernel/debug

```

or /etc/fstab

```
debugfs /sys/kernel/debug debugfs 0 0

```

2) disable ATI using "vga_switcheroo"

Radeon module should be loaded.

```
# modprobe radeon

```

Power OFF ATI.

```
# echo OFF > /sys/kernel/debug/vgaswitcheroo/switch

```

Check status correct or not.

```
cat /sys/kernel/debug/vgaswitcheroo/switch

```

Result;

```
0:IGD:+:Pwr:0000:00:02.0

1:DIS: :Off:0000:01:00.0

```

#### Use both at any time. Switchable.

If you want to use both intel and ati, commands are avaiable.

1) mounting debugfs

2) using "vga_switcheroo" Radeon module should be loaded.

Enable ATI

```
# echo DDIS > /sys/kernel/debug/vgaswitcheroo/switch

```

Enable intel

```
# echo DIGD > /sys/kernel/debug/vgaswitcheroo/switch

```

Power ON/OFF

```
# echo OFF > /sys/kernel/debug/vgaswitcheroo/switch
# echo ON > /sys/kernel/debug/vgaswitcheroo/switch

```

Check current status

```
cat /sys/kernel/debug/vgaswitcheroo/switch

```

#### New functions. Set variety.

For more control completely, there is a way to use various functions which you like, e.g. setkeycode.

Please note: Unfortunately BIOS on this machine has no option in order to select which cards you want to use definitly.

### Touchpad

ALPS touchpad is recognized as Im/PS2 Wheel Mouse with scrolling on the right edge. It is hard to be recognized as ALPS currently. A fix that allows for multitouch has been provided here: [http://nwoki.wordpress.com/2012/10/02/multitouch-fix-for-alps-touchpad/](http://nwoki.wordpress.com/2012/10/02/multitouch-fix-for-alps-touchpad/)

### Optical(Secondary Channel)

The button to open this optical drive on the top of keybaord is available by default, power management timer is also good to work (see 3.Power Management > 3.5 Chipset, Optical, USB and more). When it remove/replacement, you can easy to turn only 2 screws or disable from BIOS.

### HDD/SSD(Primary Channel)

You can easy to access in order to remove/replacement. Just open back pannel in front of this machine, then you could see battery on the right, memory module slot on the top-left, and 2.5 inch drive space (9mm height) on this bottom.

Please note: Press release bar at the bottom of battery, remove it first.

## Power Management

You can get battery life into 4-5 hours (HDDs), 6-7 hours and more (SSDs), even if "ondemand" governor. You never have to give up a performance working with built-in battery only.

### Sandy/Ivy bridge issue

Sandy/Ivy bridge platforms have to add special options on your [kernel line](/index.php/Kernel_line "Kernel line") for intel video power management. These options would be deprecated for near the future.

pcie_aspm=force i915.i915_enable_rc6=1 i915.i915_enable_fbc=1 i915.lvds_downclock=1

Please note: Options should be selected by your using style, to know what effects are expected on every option. In fact, some electric reports show less or no evaluate battery life than ever before.

### CPU

Cpufrequtils is useful to set governors. To change voltage manually, cpupower provides better solution currently.

Please note: If you try to use Gnome 3 with cpupower, confliction with cpufrequtils may arouse. To avoid this, pacman "-Sddf" option is also unfunctional. Please refer to bug report.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sony_vaio_VGN-SA/SB&oldid=349251](https://wiki.archlinux.org/index.php?title=Sony_vaio_VGN-SA/SB&oldid=349251)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Sony](/index.php/Category:Sony "Category:Sony")