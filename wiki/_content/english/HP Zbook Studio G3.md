The HP Zbook Studio G3 is a workstation replacement laptop.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Disabling the nouveau driver](#Disabling_the_nouveau_driver)
    *   [1.2 Dual boot with windows](#Dual_boot_with_windows)
*   [2 Configuration](#Configuration)
    *   [2.1 HiDPI configuration](#HiDPI_configuration)

## Installation

Installation is quite straight forward. However, you may need to disable the nouveau driver. After this, follow the general instructions of the [[guide](https://wiki.archlinux.org/index.php/Installation_guide%7Cinstallation)]

Due to the high screen resolution if this machine, you may want to change the font of your terminal during installation:

```
# setfont sun12x22

```

### Disabling the nouveau driver

If you experience problems with loading/unloading kernel modules, and, characteristically lspci never completes, you may need to disable the nouveau driver. The Nouveau driver for the NVIDIA Quatro 1000M graphics card is loaded by default, but it does not always work. Therefore, before installation, you need to blacklist the kernel at boot. Edit the [kernel boot parameters](/index.php/Kernel_modules#Using_kernel_command_line "Kernel modules") to disable this module from being loaded (this can be done in the GRUB menu by pressing 'e'):

```
# modprobe.blacklist=nouveau

```

After installation, you may want to blacklist it permanently:

 `/etc/modprobe.d/nonouveau.conf` 
```
#Do not load the nouveau driver
blacklist nouveau
```

### Dual boot with windows

This laptop usually comes pre-loaded with windows 7. Although the laptop boots in [UEFI](/index.php/UEFI "UEFI") mode, it appears as though the Windows bootloader is present in the MBR of the hard drive (there is no EFI system partition). It may be wise to install Arch with an MBR bootloader if you wish to preserve the [windows installation](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## Configuration

### HiDPI configuration

If you are using a desktop environments such as gnome or KDE, they should have their own [management tools](/index.php/HiDPI#Desktop_environments "HiDPI"). If you are using more power-user type window managers such as [i3](/index.php/I3 "I3"), you may need to add the following line in your .xinitrc file

 `~/.xinitrc` 
```
xrdb -merge ~/.Xresources
xrandr --output eDP-1 --dpi 220
exec i3
```