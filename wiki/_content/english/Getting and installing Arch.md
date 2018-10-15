The installation media and their [GnuPG](/index.php/GnuPG "GnuPG") signatures can be acquired from the [Download](https://archlinux.org/download/) page.

## Verify signature

It is recommended to verify the image signature before use, especially when downloading from an *HTTP mirror*, where downloads are generally prone to be intercepted to [serve malicious images](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

On a system with [GnuPG](/index.php/GnuPG "GnuPG") installed, do this by downloading the *PGP signature* (under *Checksums*) to the ISO directory, and [verifying](/index.php/GnuPG#Verify_a_signature "GnuPG") it with `gpg --keyserver pgp.mit.edu --keyserver-options auto-key-retrieve --verify archlinux-<version>-x86_64.iso.sig`.

Alternatively, run `pacman-key -v archlinux-<version>-x86_64.iso.sig` from an existing Arch Linux installation as root.

**Note:**

*   The signature itself could be manipulated if it is downloaded from a mirror site, instead of from [archlinux.org](https://archlinux.org/download/) as above. In this case, ensure that the public key, which is used to decode the signature, is signed by another, trustworthy key. The `gpg` command will output the fingerprint of the public key.
*   Another method to verify the authenticity of the signature is to ensure that the public key's fingerprint is identical to the key fingerprint of the [Arch Linux developer](https://www.archlinux.org/people/developers/) who signed the ISO-file. See [Wikipedia:Public-key_cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography") for more information on the public-key process to authenticate keys.

## Installation methods

The table below offers an overview of the common ways to boot the installation media. As the installation process retrieves packages from a remote repository, these methods require an internet connection; see [Offline installation of packages](/index.php/Offline_installation_of_packages "Offline installation of packages") and [Installation without internet access](/index.php/Installation_without_internet_access "Installation without internet access") when none is available.

**Note:**

*   Pointing the current boot device to a drive containing the Arch installation media is typically achieved by pressing a key during the [POST](https://en.wikipedia.org/wiki/Power-on_self_test "w:Power-on self test") phase, as indicated on the splash screen. Refer to your motherboard's manual for details.
*   When the Arch menu appears, select *Boot Arch Linux* and press `Enter` to enter the installation environment.
*   See [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) for a list of [boot parameters](/index.php/Kernel_parameters#Configuration "Kernel parameters"), and [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) for a list of included packages.

| Method | Articles | Conditions |
| Write the image on flash media or optical disc, then boot from it. | 

*   [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media")
*   [Optical disc drive#Burning](/index.php/Optical_disc_drive#Burning "Optical disc drive")

 | 

*   Installation on one, or a few machines at most
*   Obtain a directly bootable system

 |
| Mount the image on a server machine and have clients boot it over the network. | 

*   [PXE](/index.php/PXE "PXE")
*   [Diskless system](/index.php/Diskless_system "Diskless system")

 | 

*   Client-server model
*   Wired (1Gbit+) network connection

 |
| Mount the image in a running Linux system and install Arch from a chroot environment. | 

*   [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux")
*   [Install from SSH](/index.php/Install_from_SSH "Install from SSH")

 | 

*   Replace an existing system with reduced downtime
*   Install on the local machine, or a remote one via [VNC](/index.php/VNC "VNC") or [SSH](/index.php/SSH "SSH")

 |
| Set up a virtual machine and install Arch as a guest system. | 

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

 | 

*   Operating system compatible with virtualization software
*   Obtain an isolated system for learning, testing or debugging

 |
| Install Arch next to a Windows installation. | 

*   [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows")

 | 

*   Machine shared with Windows users
*   Allow to easily factory-reset a Windows-preinstalled device

 |

## See also

*   [README.transfer](https://projects.archlinux.org/archiso.git/tree/docs/README.transfer)
*   [README.altbootmethods](https://projects.archlinux.org/archiso.git/tree/docs/README.altbootmethods)