The HP Zbook Studio G3 is a workstation replacement laptop.

## Contents

*   [1 Status](#Status)
*   [2 Installation](#Installation)
    *   [2.1 Using hybrid graphics](#Using_hybrid_graphics)
    *   [2.2 Disabling Hybrid graphics](#Disabling_Hybrid_graphics)
    *   [2.3 Font size during installation](#Font_size_during_installation)
    *   [2.4 Dual boot with windows](#Dual_boot_with_windows)
*   [3 Configuration](#Configuration)
    *   [3.1 X config](#X_config)
    *   [3.2 HiDPI configuration](#HiDPI_configuration)

## Status

This laptop is currently very difficult to get working with Arch. Despite the progress described below, it sometimes stops working, and it is unclear exactly why. At this moment I would NOT reccommend buying this laptop unless you want a challenge.

## Installation

Installation is generally pretty straight forward, however, there are some things to consider. Follow the general instructions of the [[guide](https://wiki.archlinux.org/index.php/Installation_guide%7Cinstallation)]

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

Install the [nvidia](/index.php/NVIDIA "NVIDIA") driver. If you are using the system in discrete graphics mode, you may need to run nvidia-xconfig as root to be able to run [X](/index.php/X "X").

### HiDPI configuration

If you are using a desktop environments such as gnome or KDE, they should have their own [management tools](/index.php/HiDPI#Desktop_environments "HiDPI"). If you are using more power-user type window managers such as [i3](/index.php/I3 "I3"), you may need to add the following line in your .xinitrc file

 `~/.xinitrc` 
```
xrdb -merge ~/.Xresources
xrandr --output eDP-1 --dpi 220
exec i3
```