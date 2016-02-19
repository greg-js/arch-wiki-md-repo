Processor manufacturers release stability and security updates to the processor [microcode](https://en.wikipedia.org/wiki/Microcode "wikipedia:Microcode"). While microcode can be updated through the BIOS, the Linux kernel is also able to apply these updates during boot. These updates provide bug fixes that can be critical to the stability of your system. Without these updates, you may experience spurious crashes or unexpected system halts that can be difficult to track down.

Users of CPUs belonging to the Intel Haswell and Broadwell processor families in particular must install these microcode updates to ensure system stability. But all Intel users should install the updates as a matter of course.

## Contents

*   [1 Installation](#Installation)
*   [2 Enabling Intel microcode updates](#Enabling_Intel_microcode_updates)
    *   [2.1 Grub](#Grub)
    *   [2.2 systemd-boot](#systemd-boot)
    *   [2.3 EFI boot stub / EFI handover](#EFI_boot_stub_.2F_EFI_handover)
    *   [2.4 rEFInd](#rEFInd)
    *   [2.5 Syslinux](#Syslinux)
*   [3 Verifying that microcode got updated on boot](#Verifying_that_microcode_got_updated_on_boot)
*   [4 Which CPUs accept microcode updates](#Which_CPUs_accept_microcode_updates)
    *   [4.1 Detecting available microcode update](#Detecting_available_microcode_update)
*   [5 Enabling Intel early microcode loading in custom kernels](#Enabling_Intel_early_microcode_loading_in_custom_kernels)
*   [6 See also](#See_also)

## Installation

For AMD processors the microcode updates are available in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware), which is installed as part of the base system. No further action is needed.

For Intel processors, [install](/index.php/Install "Install") the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package, and continue reading.

## Enabling Intel microcode updates

Microcode must be loaded by the bootloader. Because of the wide variability in users' early-boot configuration, Intel microcode updates may not be triggered automatically by Arch's default configuration. Many AUR kernels have followed the path of the official Arch kernels in this regard.

These updates must be enabled by adding `/boot/intel-ucode.img` as the **first initrd in the bootloader config file**. This is in addition to the normal initrd file. See below for instructions for common bootloaders.

### Grub

*grub-mkconfig* will automatically detect the microcode update and configure grub appropriately. After installing the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package, users are directed to regenerate the grub config to activate loading the microcode update by running:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Alternatively, users that manage their grub config file manually can add `/intel-ucode.img` or `/boot/intel-ucode.img` to `grub.cfg` as follows:

```
[...]
    echo	'Loading initial ramdisk ...'
    initrd	/intel-ucode.img /initramfs-linux.img
[...]

```

Repeat it for each menu entry.

**Warning:** This file will automatically be overwritten by `/usr/bin/grub-mkconfig` during certain updates negating the changes. It is strongly recommended to use the configuration directory in `/etc/grub.d` to manage your grub configuration needs.

### systemd-boot

Use the `initrd` option twice in `/boot/loader/entries/*.conf`:

```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /intel-ucode.img
initrd  /initramfs-linux.img
options ...

```

### EFI boot stub / EFI handover

Append two `initrd=` options:

 `initrd=/intel-ucode.img initrd=/initramfs-linux.img` 

### rEFInd

Edit boot options in `/boot/refind_linux.conf` as per EFI boot stub above, example:

```
"Boot with standard options" "ro root=UUID=(...) quiet initrd=intel-ucode.img initrd=initramfs-linux.img"

```

Users employing manual stanzas in `/boot/refind.conf` to define the kernels should simply add `initrd=/intel-ucode.img` or `/boot/intel-ucode.img` as required to the options line, and not in the main part of the stanza.

### Syslinux

**Note:** There must be no spaces between the `intel-ucode` and `initramfs-linux` initrd files. The period signs also do not signify any shorthand or missing code; the amendment must be made exactly as illustrated below.

Multiple initrd's can be separated by commas in `/boot/syslinux/syslinux.cfg`:

```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    INITRD ../intel-ucode.img,../initramfs-linux.img
    APPEND ...

```

## Verifying that microcode got updated on boot

Use `/usr/bin/dmesg` to see if the microcode has been updated:

```
$ dmesg | grep microcode

```

On Intel systems one should see something similar to the following, indicating that microcode is updated early:

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
[    0.507335] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba

```

It is entirely possible, particularly with newer hardware, that there is no microcode update for the CPU. In that case, the output may look like this:

```
[    0.292893] microcode: CPU0 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292899] microcode: CPU1 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292906] microcode: CPU2 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292912] microcode: CPU3 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292956] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba

```

On AMD systems microcode is updated a bit later in the boot process, so the output would look something like this:

```
[    0.807879] microcode: CPU0: patch_level=0x01000098
[    0.807888] microcode: CPU1: patch_level=0x01000098
[    0.807983] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba
[   16.150642] microcode: CPU0: new patch_level=0x010000c7
[   16.150682] microcode: CPU1: new patch_level=0x010000c7

```

**Note:** The date displayed does not correspond to the version of the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package installed. It does show the last time Intel updated the microcode that corresponds to the specific hardware being updated.

## Which CPUs accept microcode updates

Users may consult either Intel or AMD at the following links to see if a particular model is supported:

*   [AMD's Operating System Research Center](http://www.amd64.org/microcode.html).
*   [Intel's download center](https://downloadcenter.intel.com/download/24661).

### Detecting available microcode update

It is possible to find out if the `intel-ucode.img` contains a microcode image for the running CPU with [iucode-tool](https://aur.archlinux.org/packages/iucode-tool/).

*   Install [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) (changing initrd is not required for detection)
*   Install [iucode-tool](https://aur.archlinux.org/packages/iucode-tool/) from the [AUR](/index.php/AUR "AUR")
*   `# modprobe cpuid`
*   `# bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS -`

	(extract microcode image and search it for your cpuid)

*   If an update is available, it should show up below *selected microcodes*
*   The microcode might already be in your vendor bios and not show up loading in dmesg. Compare to the current microcode running `grep microcode /proc/cpuinfo`

## Enabling Intel early microcode loading in custom kernels

In order for early loading to work in custom kernels, "CPU microcode loading support" needs to be compiled into the kernel, NOT compiled as a module. This will enable the "Early load microcode" prompt which should be set to "Y".

```
CONFIG_MICROCODE=y
CONFIG_MICROCODE_INTEL=y
CONFIG_MICROCODE_INTEL_EARLY=y
CONFIG_MICROCODE_EARLY=y

```

## See also

*   [Updating microcodes](https://flossexperiences.wordpress.com/2013/11/17/updating-microcodes/)
*   [Notes on Intel Microcode updates](http://inertiawar.com/microcode/)
*   [Kernel early microcode](https://www.kernel.org/doc/Documentation/x86/early-microcode.txt)
*   [Erratum found in Haswell/Broadwell](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly)