The HP Zbook Studio G3 is a workstation replacement laptop.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Using hybrid graphics](#Using_hybrid_graphics)
    *   [1.2 Disabling Hybrid graphics](#Disabling_Hybrid_graphics)
    *   [1.3 Font size during installation](#Font_size_during_installation)
    *   [1.4 Dual boot with windows](#Dual_boot_with_windows)
*   [2 Configuration](#Configuration)
    *   [2.1 X config](#X_config)
    *   [2.2 HiDPI configuration](#HiDPI_configuration)
    *   [2.3 Touchpad configuration](#Touchpad_configuration)
    *   [2.4 Mute button LED indicator](#Mute_button_LED_indicator)

## Installation

Installation is generally pretty straight forward, however, there are some things to consider. Follow the general instructions of the [installation|guide](/index.php/Installation_guide "Installation guide")

### Using hybrid graphics

Due to a kernel issue, use of nouveau or bbswitch may result in lockups. To prevent this, add `acpi_osi=! acpi_osi="Windows 2009"` to your kernel command line ([source](https://github.com/Bumblebee-Project/Bumblebee/issues/764#issuecomment-234494238), [Kernel bug 156341](https://bugzilla.kernel.org/show_bug.cgi?id=156341)).

### Disabling Hybrid graphics

If you do not mind greatly reducing your battery life and would like to use the NVIDIA graphics by default, you can change Hybrid graphisc in the firmware setup.

In the BIOS settings, (which you enter by pressing Escape during boot) change the graphics mode from Auto/Hybrid to discrete.

### Font size during installation

Due to the high screen resolution if this machine, you may want to change the font of your terminal during installation:

```
# setfont sun12x22

```

### Dual boot with windows

This laptop usually comes pre-loaded with windows 7. Although the laptop boots in [UEFI](/index.php/UEFI "UEFI") mode, it appears as though the Windows bootloader is present in the MBR of the hard drive (there is no EFI system partition). It may be wise to install Arch with an MBR bootloader if you wish to preserve the [windows installation](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## Configuration

### X config

Install the [NVIDIA](/index.php/NVIDIA "NVIDIA") driver. If you are using the system in discrete graphics mode, you may need to run nvidia-xconfig as root to be able to run [X](/index.php/X "X").

### HiDPI configuration

If you are using a desktop environments such as gnome or KDE, they should have their own [management tools](/index.php/HiDPI#Desktop_environments "HiDPI"). If you are using more power-user type window managers such as [i3](/index.php/I3 "I3"), you may need to add the following line in your .xinitrc file

 `~/.xinitrc` 
```
xrdb -merge ~/.Xresources
xrandr --output eDP-1 --dpi 288
exec i3
```

The name of the output device depends on the graphics adapter and driver. Use [xrandr](/index.php/Xrandr "Xrandr") to find out the actual name.

### Touchpad configuration

The touchpad may be "hijacked" by the `i2c_hid` device driver. Although the touchpad is working, its configuration is fixed to two buttons, two-finger natural scrolling and no tapping; Any changes with `xinput` or other tools will have no effect.

To prevent this you have to [blacklist](/index.php/Blacklist "Blacklist") `i2c_hid` by adding the following lines to a `*.conf` file in `/etc/modprobe.d` ([source](https://bbs.archlinux.org/viewtopic.php?pid=1602689#p1602689)):

 `/etc/modprobe.d/touchpad.conf` 
```
blacklist i2c_hid
install i2c_hid /bin/false
```

After a reboot (unloading `i2c_hid`, if possible, may be sufficient) the touchpad should be fully configurable [libinput device](/index.php/Libinput#Configuration "Libinput").

### Mute button LED indicator

To fix the mute button LED, create a file

 `/etc/modprobe.d/alsa-base.conf`  `options snd-hda-intel model=mute-led-gpio`