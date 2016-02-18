**Konsileto:** Ĉi tiu gvido estas parto de plurpaĝa artikolo por la gvido de komencantoj. **[Alklaku ĉi tie](/index.php/Beginners%27_Guide_(Esperanto) "Beginners' Guide (Esperanto)")** se vi volas legi la gvidon unupaĝe.

Ĉi tiu dokumento gvidos vin inter la procezo de instalado de [Arch Linux](/index.php?title=Arch_Linux_(Esperanto)&action=edit&redlink=1 "Arch Linux (Esperanto) (page does not exist)") per la [skriptoj de instalado de Arch](https://github.com/falconindy/arch-install-scripts). Antaŭ ol instalado, bonvole legu la [oftajn demandojn](/index.php?title=FAQ_(Esperanto)&action=edit&redlink=1 "FAQ (Esperanto) (page does not exist)").

La komunume prizorgata [Arch-vikio](/index.php/Main_Page_(Esperanto) "Main Page (Esperanto)") estas utila risurco kaj estu rigardata por problemoj unue. La [IRC](https://en.wikipedia.org/wiki/eo:IRC "wikipedia:eo:IRC")-kanalo ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) kaj la [forumoj](https://bbs.archlinux.org/) ankaŭ disponeblas se la respondo ne troveblas aliloke. Aldone, kontolu la paĝojn de `man` por ĉiuj komandoj, kiujn vi ne konas: tio invokeblas kutime per `man *komando*`.

## Contents

*   [1 Pretigo](#Pretigo)
    *   [1.1 Burn or write the latest installation medium](#Burn_or_write_the_latest_installation_medium)
        *   [1.1.1 Installing over the network](#Installing_over_the_network)
        *   [1.1.2 Installing on a virtual machine](#Installing_on_a_virtual_machine)
    *   [1.2 Boot the installation medium](#Boot_the_installation_medium)
        *   [1.2.1 Testing if you are booted into UEFI mode](#Testing_if_you_are_booted_into_UEFI_mode)
        *   [1.2.2 Troubleshooting boot problems](#Troubleshooting_boot_problems)

## Pretigo

**Noto:** Se vi volas instali Arch el ekzistanta GNU/Linux-distribuaĵo, bonvole legu [ĉi tiun artikolon](/index.php?title=Install_from_Existing_Linux_(Esperanto)&action=edit&redlink=1 "Install from Existing Linux (Esperanto) (page does not exist)"). Tio utilas specife se vi planas instali Arch per [VNC](/index.php/VNC "VNC") aŭ [SSH](/index.php/SSH "SSH") fore.

### Burn or write the latest installation medium

This guide pertains to the current release (2012.11.01), which can be obtained from the [Download](https://archlinux.org/download/) page.

*   Burn the ISO image on a CD or DVD with your preferred software.

**Note:** The quality of optical drives and the discs themselves varies greatly. Generally, using a slow burn speed is recommended for reliable burns. If you are experiencing unexpected behaviour from the disc, try burning at the lowest speed supported by your burner.

*   Or you can write the ISO image on a USB stick. For detailed instructions, see [USB Installation Media](/index.php/USB_Installation_Media "USB Installation Media").

#### Installing over the network

Instead of writing the boot media to a disc or USB stick, you may alternatively boot the .iso image over the network. This works well when you already have a server set up. Please see [this article](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") for more information, and then continue to [Boot the installation medium](#Boot_the_installation_medium).

#### Installing on a virtual machine

Installing on a [virtual machine](https://en.wikipedia.org/wiki/Virtual_machine "wikipedia:Virtual machine") is a good way to become familiar with Arch Linux and its installation procedure without leaving your current operating system and repartitioning the storage drive. It will also let you keep this Beginners' Guide open in your browser throughout the installation. Some users may find it beneficial to have an independent Arch Linux system on a virtual drive, for testing purposes.

Examples of virtualization software are [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

The exact procedure for preparing a virtual machine depends on the software, but will generally follow these steps:

1.  Create the virtual disk image that will host the operating system.
2.  Properly configure the virtual machine parameters.
3.  Boot the downloaded ISO image with a virtual CD drive.
4.  Continue with [Boot the installation medium](#Boot_the_installation_medium).

The following articles may be helpful:

*   [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Installing Arch Linux in VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

### Boot the installation medium

First, you may have to change the boot order in your computer's BIOS. To do this, you have to press a key (usually `Delete`, `F1`, `F2`, `F11` or `F12`) during the POST (Power On Self-Test) phase. Then, select "Boot Arch Linux" from the menu and press `Enter` in order to begin with the installation.

**Note:** The memory requirement for a basic install is 64 MB of RAM.

**Note:** Users seeking to perform the Arch Linux installation remotely via an [SSH](/index.php/SSH "SSH") connection are encouraged to make a few tweaks at this point to enable SSH connections directly to the live CD environment. If interested, see the [Install from SSH](/index.php/Install_from_SSH "Install from SSH") article.

##### Testing if you are booted into UEFI mode

In case you have a [UEFI](/index.php/UEFI "UEFI") motherboard and UEFI Boot mode is enabled (and is preferred over BIOS/Legacy mode), the CD/USB will automatically launch Arch Linux kernel (EFISTUB via Gummiboot Boot Manager). To check whether you have booted into UEFI mode, load the `efivars` kernel module (before chrooting) and then check whether there are files in `/sys/firmware/efi/vars/`:

```
# modprobe efivars       # before chrooting
# ls -1 /sys/firmware/efi/vars/

```

**Note:** The kernel module `efivars` detects and populates the UEFI Runtime Variables at `/sys/firmware/efi/vars`. This module is **not** loaded automatically during the boot process, and until this module is loaded, and the kernel booted in UEFI mode, **without** `noefi` parameter, no files will exist in `/sys/firmware/efi/vars`. These variables are later modified by `efibootmgr` to add bootloader entry to UEFI boot menu. In BIOS mode, modprobe will not give any error about efivars module. The correct way to detect UEFI boot is to check for files in `/sys/firmware/efi/vars` .

##### Troubleshooting boot problems

*   If you're using an Intel video chipset and the screen goes blank during the boot process, the problem is likely an issue with Kernel Mode Setting ([KMS](/index.php/KMS "KMS")). A possible workaround may be achieved by rebooting and pressing `Tab` over the entry that you're trying to boot (i686 or x86_64). At the end of the string type `nomodeset` and press `Enter`. Alternatively, try `video=SVIDEO-1:d` which, if it works, will not disable kernel mode setting. See the [Intel](/index.php/Intel "Intel") article for more information.

*   If the screen does *not* go blank and the boot process gets stuck while trying to load the kernel, press `Tab` while hovering over the menu entry, type `acpi=off` at the end of the string and press `Enter`.

**[Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")**

* * *

[Preparation](/index.php/Beginners%27_guide/Preparation "Beginners' guide/Preparation") >> [Installation](/index.php/Beginners%27_guide/Installation "Beginners' guide/Installation")