[Help](//www.mediawiki.org/wiki/Special:MyLanguage/Help:Categories)

# Category:Getting and installing Arch

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This category contains articles about Arch Linux releases, and downloading and installing Arch Linux.

The installation media and their [GnuPG](/index.php/GnuPG "GnuPG") signatures can be acquired from the [Download](https://archlinux.org/download/) page. The single ISO image supports both 32bit and 64bit systems.

## Verify signature

It is recommended to verify the image signature before use, especially when downloading from an _HTTP mirror_, as these are run by volunteers who could [serve malicious images](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

On a system with [GnuPG](/index.php/GnuPG "GnuPG") installed, do this by downloading the _PGP signature_ (under _Checksums_) to the ISO directory, and verifying it with `gpg --verify archlinux-<version>-dual.iso.sig`. If the public key is not found, [import](/index.php/GnuPG#Import_key "GnuPG") it with `gpg --recv-keys _key-id_`.

Alternatively, run `pacman-key -v archlinux-<version>-dual.iso.sig` from an existing Arch Linux installation.

## Installation methods

The table below offers an overview of the common ways to boot the installation media. As the installation process retrieves packages from a remote repository, these methods require an internet connection; see [Offline installation of packages](/index.php/Offline_installation_of_packages "Offline installation of packages") and [Archiso#Installation without Internet access](/index.php/Archiso#Installation_without_Internet_access "Archiso") when none is available.

<table class="wikitable">

<tbody>

<tr>

<th>Method</th>

<th>Articles</th>

<th>Conditions</th>

</tr>

<tr>

<td>Write the image on flash media or optical disc, then boot from it.</td>

<td>

*   [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media")
*   [Optical disc drive#Burning](/index.php/Optical_disc_drive#Burning "Optical disc drive")

</td>

<td>

*   Installation on one, or a few machines at most
*   Obtain a directly bootable system

</td>

</tr>

<tr>

<td>Mount the image on a server machine and have clients boot it over the network.</td>

<td>

*   [PXE](/index.php/PXE "PXE")
*   [Diskless system](/index.php/Diskless_system "Diskless system")

</td>

<td>

*   Client-server model
*   Wired (1Gbit+) network connection

</td>

</tr>

<tr>

<td>Mount the image in a running Linux system and install Arch from a chroot environment.</td>

<td>

*   [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux")
*   [Install from SSH](/index.php/Install_from_SSH "Install from SSH")

</td>

<td>

*   Replace an existing system with reduced downtime
*   Install on the local machine, or a remote one via [VNC](/index.php/VNC "VNC") or [SSH](/index.php/SSH "SSH")

</td>

</tr>

<tr>

<td>Set up a virtual machine and install Arch as a guest system.</td>

<td>

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

</td>

<td>

*   Operating system compatible with virtualization software
*   Obtain an isolated system for learning, testing or debugging

</td>

</tr>

</tbody>

</table>

## See also

*   [README.transfer](https://projects.archlinux.org/archiso.git/tree/docs/README.transfer)
*   [README.altbootmethods](https://projects.archlinux.org/archiso.git/tree/docs/README.altbootmethods)

## Pages in category "Getting and installing Arch"

The following 28 pages are in this category, out of 28 total.

### A

*   [Arch Linux AMIs for Amazon Web Services](/index.php/Arch_Linux_AMIs_for_Amazon_Web_Services "Arch Linux AMIs for Amazon Web Services")
*   [Archboot](/index.php/Archboot "Archboot")
*   [Archboot (Русский)](/index.php/Archboot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archboot (Русский)")
*   [Archiso](/index.php/Archiso "Archiso")

### B

*   [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")

### D

*   [Diskless system](/index.php/Diskless_system "Diskless system")
*   [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system")
*   [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows")
*   [Dual boot with Windows/SafeBoot](/index.php/Dual_boot_with_Windows/SafeBoot "Dual boot with Windows/SafeBoot")
*   [Dynamic Disks](/index.php/Dynamic_Disks "Dynamic Disks")

### G

*   [General recommendations](/index.php/General_recommendations "General recommendations")

### I

*   [Install bundled 32-bit system in 64-bit system](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system")
*   [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux")
*   [Install from SSH](/index.php/Install_from_SSH "Install from SSH")
*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")
*   [Installing Arch Linux on ZFS](/index.php/Installing_Arch_Linux_on_ZFS "Installing Arch Linux on ZFS")
*   [Installing with Fake RAID](/index.php/Installing_with_Fake_RAID "Installing with Fake RAID")
*   [ISCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot")

### M

*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

### O

*   [Offline installation of packages](/index.php/Offline_installation_of_packages "Offline installation of packages")

### P

*   [PXE](/index.php/PXE "PXE")

### R

*   [Remastering the Install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO")

### S

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")

### T

*   [TalkingArch](/index.php/TalkingArch "TalkingArch")

### U

*   [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media")

### V

*   [Virtual Private Server](/index.php/Virtual_Private_Server "Virtual Private Server")
*   [VMware/Installing Arch as a guest](/index.php/VMware/Installing_Arch_as_a_guest "VMware/Installing Arch as a guest")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Category:Getting_and_installing_Arch&oldid=404112](https://wiki.archlinux.org/index.php?title=Category:Getting_and_installing_Arch&oldid=404112)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [About Arch](/index.php/Category:About_Arch "Category:About Arch")