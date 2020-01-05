Processor manufacturers release stability and security updates to the processor [microcode](https://en.wikipedia.org/wiki/Microcode "wikipedia:Microcode"). These updates provide bug fixes that can be critical to the stability of your system. Without them, you may experience spurious crashes or unexpected system halts that can be difficult to track down.

All users with an AMD or Intel CPU should install the microcode updates to ensure system stability.

Microcode updates are usually shipped with the motherboard's firmware and applied during firmware initialization. Since OEMs might not release firmware updates in a timely fashion and old systems do not get new firmware updates at all, the ability to apply CPU microcode updates during boot was added to the Linux kernel. [The Linux microcode loader](https://www.kernel.org/doc/Documentation/x86/microcode.txt) supports three loading methods:

1.  **Early loading** updates the microcode very early during boot, before the initramfs stage, so it is the preferred method. This is mandatory for CPUs with severe hardware bugs, like the Intel Haswell and Broadwell processor families.
2.  **Late loading** updates the microcode after booting which could be too late since the CPU might have already tried to use a bugged instruction set. Even if already using early loading, late loading can still be used to apply a newer microcode update without needing to reboot.
3.  **Built-in microcode** can be compiled into the kernel that is then applied by the early loader.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Early loading](#Early_loading)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 Enabling early microcode loading in custom kernels](#Enabling_early_microcode_loading_in_custom_kernels)
        *   [1.2.2 GRUB](#GRUB)
        *   [1.2.3 systemd-boot](#systemd-boot)
        *   [1.2.4 EFISTUB](#EFISTUB)
        *   [1.2.5 rEFInd](#rEFInd)
        *   [1.2.6 Syslinux](#Syslinux)
        *   [1.2.7 LILO](#LILO)
*   [2 Late loading](#Late_loading)
    *   [2.1 Enabling late microcode updates](#Enabling_late_microcode_updates)
    *   [2.2 Disabling late microcode updates](#Disabling_late_microcode_updates)
*   [3 Verifying that microcode got updated on boot](#Verifying_that_microcode_got_updated_on_boot)
*   [4 Which CPUs accept microcode updates](#Which_CPUs_accept_microcode_updates)
    *   [4.1 Detecting available microcode update](#Detecting_available_microcode_update)
*   [5 See also](#See_also)

## Early loading

Microcode must be loaded by the [boot loader](/index.php/Boot_loader "Boot loader"). Because of the wide variability in users' early-boot configuration, microcode updates may not be triggered automatically by Arch's default configuration. Many AUR kernels have followed the path of the official Arch [kernels](/index.php/Kernels "Kernels") in this regard.

These updates must be enabled by adding `/boot/amd-ucode.img` or `/boot/intel-ucode.img` as the **first initrd in the bootloader config file**. This is in addition to the normal initrd file. See below for instructions for common bootloaders.

**Note:** In the following sections replace `*cpu_manufacturer*` with your CPU manufacturer, i.e. `amd` or `intel`.

**Tip:** For [Arch Linux on a removable drive](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key") add both microcode files as `initrd` to the boot loader configuration. Their order does not matter as long as they both are specified before the real initramfs image.

### Installation

For AMD processors, [install](/index.php/Install "Install") the [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) package.

For Intel processors, [install](/index.php/Install "Install") the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package.

If your Arch installation is [on a removable drive](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key") that needs to have microcode for both manufacturer processors, install both packages.

### Configuration

#### Enabling early microcode loading in custom kernels

In order for early loading to work in custom kernels, "CPU microcode loading support" needs to be compiled into the kernel, **not** compiled as a module. This will enable the "Early load microcode" prompt which should be set to `Y`.

```
CONFIG_BLK_DEV_INITRD=Y
CONFIG_MICROCODE=y
CONFIG_MICROCODE_INTEL=Y
CONFIG_MICROCODE_AMD=y

```

#### GRUB

*grub-mkconfig* will automatically detect the microcode update and configure [GRUB](/index.php/GRUB "GRUB") appropriately. After installing the microcode package, regenerate the GRUB config to activate loading the microcode update by running:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:** *grub-mkconfig* does not add the microcode images to the fallback initramfs boot entry. See [FS#60999](https://bugs.archlinux.org/task/60999).

Alternatively, users that manage their GRUB config file manually can add `/boot/*cpu_manufacturer*-ucode.img` (or `/*cpu_manufacturer*-ucode.img` if `/boot` is a separate partition) as follows:

 `/boot/grub/grub.cfg` 
```
...
echo 'Loading initial ramdisk'
initrd	**/boot/*cpu_manufacturer*-ucode.img** /boot/initramfs-linux.img
...

```

Repeat it for each menu entry.

#### systemd-boot

Use the `initrd` option to load the microcode, before the initial ramdisk, as follows:

 `/boot/loader/entries/*entry*.conf` 
```
title   Arch Linux
linux   /vmlinuz-linux
**initrd  /*cpu_manufacturer*-ucode.img**
initrd  /initramfs-linux.img
...

```

The latest microcode `*cpu_manufacturer*-ucode.img` must be available at boot time in your [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP). The ESP must be mounted as `/boot` in order to have the microcode updated every time [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) or [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) is updated. Otherwise, copy `/boot/*cpu_manufacturer*-ucode.img` to your ESP at every update of the microcode package.

For [kernels that have been generated as a single file](/index.php/Systemd-boot#Preparing_kernels_for_/EFI/Linux "Systemd-boot") containing all initrd, cmdline and kernel, first generate the initrd to integrate by creating a new one as follows:

```
cat /boot/*cpu_manufacturer*-ucode.img /boot/initramfs-linux.img > my_new_initrd
objcopy ... --add-section .initrd=my_new_initrd
```

#### EFISTUB

Append two `initrd=` options:

```
**initrd=/*cpu_manufacturer*-ucode.img** initrd=/initramfs-linux.img

```

#### rEFInd

Edit boot options in `/boot/refind_linux.conf` and add `initrd=/boot/*cpu_manufacturer*-ucode.img` (or `initrd=/*cpu_manufacturer*-ucode.img` if `/boot` is a separate partition) as the first initramfs. For example:

```
"Boot using default options"     "root=PARTUUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* rw add_efi_memmap **initrd=/boot/*cpu_manufacturer*-ucode.img** initrd=/boot/initramfs-%v.img"

```

Users employing [manual stanzas](/index.php/REFInd#Manual_boot_stanzas "REFInd") in `*esp*/EFI/refind/refind.conf` to define the kernels should simply add `initrd=/boot/*cpu_manufacturer*-ucode.img` (or `/*cpu_manufacturer*-ucode.img` if `/boot` is a separate partition) as required to the options line, and not in the main part of the stanza. E.g.:

```
options  "root=PARTUUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* rw add_efi_memmap **initrd=/boot/*cpu_manufacturer*-ucode.img**"

```

#### Syslinux

**Note:** There must be no spaces between the `*cpu_manufacturer*-ucode.img` and `initramfs-linux.img` initrd files. The `INITRD` line must be exactly as illustrated below.

Multiple initrd's can be separated by commas in `/boot/syslinux/syslinux.cfg`:

```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    INITRD **../*cpu_manufacturer*-ucode.img**,../initramfs-linux.img
...

```

#### LILO

[LILO](/index.php/LILO "LILO") and potentially other old bootloaders do not support multiple initrd images. In that case, `*cpu_manufacturer*-ucode.img` and `initramfs-linux.img` will have to be merged into one image.

**Warning:** The merged image must be recreated after each kernel update!

**Note:** The order is important. The original image `initramfs-linux.img` must be placed **after** `*cpu_manufacturer*-ucode.img` in the resulting image.

To merge both images into one image named `initramfs-merged.img`, the following command can be used:

```
# cat /boot/*cpu_manufacturer*-ucode.img /boot/initramfs-linux.img > /boot/initramfs-merged.img

```

Now, edit `/etc/lilo.conf` to load the new image.

```
...
initrd=/boot/initramfs-merged.img
...

```

And run `lilo` as root:

```
# lilo

```

## Late loading

Late loading of microcode updates happens after the system has booted. It uses files in `/usr/lib/firmware/amd-ucode/` and `/usr/lib/firmware/intel-ucode/`.

For AMD processors the microcode update files are provided by [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

For Intel processors no package provides the microcode update files ([FS#59841](https://bugs.archlinux.org/task/59841)). To use late loading you need to manually extract `intel-ucode/` from Intel's provided archive.

### Enabling late microcode updates

Unlike early loading, late loading of microcode updates on Arch Linux are enabled by default using `/usr/lib/tmpfiles.d/linux-firmware.conf`. After boot the file gets parsed by [systemd-tmpfiles-setup.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles-setup.service.8) and CPU microcode gets updated.

To manually reload the microcode, e.g. after updating the microcode files in `/usr/lib/firmware/amd-ucode/` or `/usr/lib/firmware/intel-ucode/`, run:

```
# echo 1 > /sys/devices/system/cpu/microcode/reload

```

This allows to apply newer microcode updates without rebooting the system. For [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) you can automate it with a [pacman hook](/index.php/Pacman_hook "Pacman hook"), e.g.:

 `/etc/pacman.d/hooks/microcode_reload.hook` 
```
[Trigger]
Operation = Upgrade
Type = File
Target = usr/lib/firmware/amd-ucode/*

[Action]
Description = Applying CPU microcode updates...
When = PostTransaction
Depends = sh
Exec = /bin/sh -c 'echo 1 > /sys/devices/system/cpu/microcode/reload'
```

### Disabling late microcode updates

For AMD systems the CPU microcode will get updated even if [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) is not installed since the files in `/usr/lib/firmware/amd-ucode/` are provided by the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package ([FS#59840](https://bugs.archlinux.org/task/59840)).

For [virtual machines](/index.php/Virtual_machine "Virtual machine") and [containers](https://en.wikipedia.org/wiki/Container_(virtualization) ([FS#46591](https://bugs.archlinux.org/task/46591)) it is not possible to update the CPU microcode, so you may want to disable microcode updates. To do so, you must override the [tmpfile](/index.php/Tmpfile "Tmpfile") `/usr/lib/tmpfiles.d/linux-firmware.conf` that is provided by [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware). It can be done by creating a file with the same filename in `/etc/tmpfiles.d/`:

```
# ln -s /dev/null /etc/tmpfiles.d/linux-firmware.conf

```

## Verifying that microcode got updated on boot

Use *dmesg* to see if the microcode has been updated:

```
$ dmesg | grep microcode

```

On Intel systems one should see something similar to the following on every boot, indicating that microcode is updated very early on:

```
[    0.000000] CPU0 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.221951] CPU1 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.242064] CPU2 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.262349] CPU3 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.507267] microcode: CPU0 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507272] microcode: CPU1 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507276] microcode: CPU2 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507281] microcode: CPU3 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507286] microcode: CPU4 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507292] microcode: CPU5 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507296] microcode: CPU6 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507300] microcode: CPU7 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507335] microcode: Microcode Update Driver: v2.2.

```

**Note:** The date displayed does not correspond to the version of the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package installed. It does show the last time Intel updated the microcode that corresponds to the specific hardware being updated.

It is entirely possible, particularly with newer hardware, that there is no microcode update for the CPU. In that case, the output may look like this:

```
[    0.292893] microcode: CPU0 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292899] microcode: CPU1 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292906] microcode: CPU2 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292912] microcode: CPU3 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292956] microcode: Microcode Update Driver: v2.2.

```

On AMD systems using early loading the output would look something like this:

```
[    2.119089] microcode: microcode updated early to new patch_level=0x0700010f
[    2.119157] microcode: CPU0: patch_level=0x0700010f
[    2.119171] microcode: CPU1: patch_level=0x0700010f
[    2.119183] microcode: CPU2: patch_level=0x0700010f
[    2.119189] microcode: CPU3: patch_level=0x0700010f
[    2.119269] microcode: Microcode Update Driver: v2.2.

```

On AMD systems using late loading the output will show the version of the old microcode before reloading the microcode and the new one once it is reloaded. It would look something like this:

```
[    2.112919] microcode: CPU0: patch_level=0x0700010b
[    2.112931] microcode: CPU1: patch_level=0x0700010b
[    2.112940] microcode: CPU2: patch_level=0x0700010b
[    2.112951] microcode: CPU3: patch_level=0x0700010b
[    2.113043] microcode: Microcode Update Driver: v2.2.
[    6.429109] microcode: CPU2: new patch_level=0x0700010f
[    6.430416] microcode: CPU0: new patch_level=0x0700010f
[    6.431722] microcode: CPU1: new patch_level=0x0700010f
[    6.433029] microcode: CPU3: new patch_level=0x0700010f
[    6.433073] x86/CPU: CPU features have changed after loading microcode, but might not take effect.

```

## Which CPUs accept microcode updates

Users may consult either Intel or AMD at the following links to see if a particular model is supported:

*   [AMD's Operating System Research Center](http://www.amd64.org/microcode.html).
*   [Intel's download center](https://downloadcenter.intel.com/SearchResult.aspx?lang=eng&keyword=processor%20microcode%20data%20file).

### Detecting available microcode update

It is possible to find out if the `intel-ucode.img` contains a microcode image for the running CPU with [iucode-tool](https://www.archlinux.org/packages/?name=iucode-tool).

1.  [Install](/index.php/Install "Install") [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) (changing initrd is not required for detection)
2.  [Install](/index.php/Install "Install") [iucode-tool](https://www.archlinux.org/packages/?name=iucode-tool)
3.  `# modprobe cpuid` 
4.  Extract microcode image and search it for your cpuid:
     `# bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS -` 
5.  If an update is available, it should show up below *selected microcodes*
6.  The microcode might already be in your vendor bios and not show up loading in dmesg. Compare to the current microcode running `grep microcode /proc/cpuinfo`

## See also

*   [Updating microcodes – Experiences in the community](https://flossexperiences.wordpress.com/2013/11/17/updating-microcodes/)
*   [Notes on Intel Microcode updates – Ben Hawkes](http://inertiawar.com/microcode/)
*   [Kernel microcode loader – kernel documentation](https://www.kernel.org/doc/Documentation/x86/microcode.txt)
*   [Erratum found in Haswell/Broadwell – AnandTech](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly)
*   [iucode-tool GitLab project](https://gitlab.com/iucode-tool/iucode-tool)