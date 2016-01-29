# Toshiba Satellite S75-A7221

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** WIP (Discuss in [Talk:Toshiba Satellite S75-A7221#](https://wiki.archlinux.org/index.php/Talk:Toshiba_Satellite_S75-A7221))

I recently installed Arch Linux on my new laptop. I'll be adding my experience installing on both BIOS and UEFI modes as well as hardware and the packages to go with it during installation.

## Contents

*   [1 Display](#Display)
*   [2 Networking](#Networking)
    *   [2.1 Wired](#Wired)
    *   [2.2 Wireless](#Wireless)
*   [3 Sound](#Sound)

## Display

This laptop has the Intel HD Graphics 4600 onboard. Install the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) along with [mesa](https://www.archlinux.org/packages/?name=mesa) to get 2D/3D acceleration working. You will also want to enable [multilib](/index.php/Multilib "Multilib") and install [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) to get hardware acceleration working on your 32-bit applications.

When booting, whether installing or post-install, you will need to add `acpi_backlight=vendor` to your kernel options. This will prevent a black screen on boot.

## Networking

### Wired

### Wireless

## Sound

Retrieved from "[https://wiki.archlinux.org/index.php?title=Toshiba_Satellite_S75-A7221&oldid=352857](https://wiki.archlinux.org/index.php?title=Toshiba_Satellite_S75-A7221&oldid=352857)"