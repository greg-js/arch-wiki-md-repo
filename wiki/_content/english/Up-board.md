The [up-board](http://up-board.org) is a Intel based SOC.

## Contents

*   [1 Installation](#Installation)
*   [2 GPIO](#GPIO)
*   [3 Sound](#Sound)
    *   [3.1 Compilation](#Compilation)
        *   [3.1.1 Manual](#Manual)
        *   [3.1.2 Arch Build System](#Arch_Build_System)

## Installation

The up-board features a [UEFI](/index.php/UEFI "UEFI") only setup (no BIOS emulation). The standard UEFI installation process may be followed. [systemd-boot](/index.php/Systemd-boot "Systemd-boot") works well as a simple bootloader.

**Note:** The installation disk for the up-board is `/dev/mmcblk0`. [GPT](/index.php/GPT "GPT") is the recommended partition type.

## GPIO

The GPIO pins on the UP board are routed through a CPLD that requires a custom driver. This driver has not yet been added to the mainline kernel, but there are patches available that add the functionality. The AUR package [linux-up](https://aur.archlinux.org/packages/linux-up/) provides the mainline kernel with the driver patched in and enabled.

## Sound

As of August 2016, the mainline kernel does not support sound through HDMI for cherry trail based devices like the up-board. There are plans on adding support to the mainline kernel as noted [here](https://bugzilla.kernel.org/show_bug.cgi?id=113971#c6), but in the mean time if you wish to have sound you will need to manually patch your kernel. There is currently no AUR package including these patches.

### Compilation

Without any optimizations, compilation on the up-board takes around 5-6 hours. Setting your `MAKEFLAGS` beforehand will drastically improve the compilation time. If you're using the ABS the [makepkg](/index.php/Makepkg "Makepkg") page has information on how to set the variable in there.

#### Manual

*   Download a copy of the patched kernel from [here](https://github.com/plbossart/sound/archive/byt-cht-hdmi-v4.7.tar.gz) and the latest kernel sources from [http://www.kernel.org](http://www.kernel.org).

*   Once you've extracted the archive, you will need to remove the inline reference in one of the header files. You can do this with sed like so:

```
$ sed -i 's/inline//g' sound-byt-cht-hdmi-v4.7/sound/hdmi_audio/intel_mid_hdmi_audio.h

```

*   Next you'll need to create a patch for the 2 folders that have been changed, `sound/` and `drivers/gpu/drm/i915`:

```
$ diff -ENwbur {linux-4.7.2,sound-byt-cht-hdmi-v4.7}/drivers/gpu/drm/i915 >> cherry.patch
$ diff -ENwbur {linux-4.7.2,sound-byt-cht-hdmi-v4.7}/sound >> cherry.patch

```

*   Once the patch has been created you can move it into the kernel sources directory and run:

```
$ patch -p1 < cherry.patch

```

*   Lastly, you'll need to make sure that `CONFIG_SUPPORT_HDMI=y` option is in the `.config`.

#### Arch Build System

If you wish to build the kernel using the ABS, follow the steps provided in [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). Remember to add the patch to the prepare function and run *updpkgsums* to update the checksum for the changed config file.