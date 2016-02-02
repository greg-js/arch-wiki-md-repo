# PacketTracer

Cisco Packet Tracer is a powerful network simulation program that allows students to experiment with network behavior and ask “what if” questions. As an integral part of the Networking Academy comprehensive learning experience, Packet Tracer provides simulation, visualization, authoring, assessment, and collaboration capabilities and facilitates the teaching and learning of complex technology concepts. [Source](https://www.netacad.com/web/about-us/cisco-packet-tracer)

## Contents

*   [1 Disclaimer](#Disclaimer)
*   [2 Installation](#Installation)
    *   [2.1 32-bit systems](#32-bit_systems)
    *   [2.2 64-bit systems](#64-bit_systems)
    *   [2.3 Assessment environment check](#Assessment_environment_check)
    *   [2.4 Video supplements](#Video_supplements)
*   [3 See also](#See_also)

## Disclaimer

Understand if you have permission from Cisco Systems to use this software. If you do not meet eligibility, discontinue your progress and consider alternatives such as [Gns3](/index.php/Gns3 "Gns3").

## Installation

### 32-bit systems

See the [AUR](/index.php/AUR "AUR") article for important usage topics. For now, only download and extract the tarball for [packettracer](https://aur.archlinux.org/packages/packettracer/) from the [AUR](/index.php/AUR "AUR")

You will need to have access to the file `Cisco Packet Tracer 6.0.1 for Linux (with tutorials)` to continue with the installation. For your convenience, the sha1sum and md5sum of this file is provided below.

```
$ sha1sum Cisco\ Packet\ Tracer\ 6.0.1\ for\ Linux\ \(with\ tutorials\)
81f74633115fab6bd1cb699f203a5a5375830c30  Cisco Packet Tracer 6.0.1 for Linux (with tutorials)
$ md5sum Cisco\ Packet\ Tracer\ 6.0.1\ for\ Linux\ \(with\ tutorials\)
6d623bc0761cbb6e3cdccb3c0e0ec70b  Cisco Packet Tracer 6.0.1 for Linux (with tutorials)

```

Copy this file to your working directory, maintaining the name. The [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") file found in the earlier tarball will require this archive. It is not provided in the tarball itself for ethical and legal reasons. This file requirement may change in the future, based on the version of packet tracer available at that time. At the time of writing, the proper file name is `Cisco Packet Tracer 6.0.1 for Linux (with tutorials)`.

After you have copied the file to the working directory (the directory you extracted the tarball to), you may now continue installation normally.

Finally, please read the EULA at `/usr/share/licenses/packettracer/eula.txt` and uninstall if you do not agree. If you agree, the program can be found under most menu systems in the Internet category.

### 64-bit systems

See the [AUR](/index.php/AUR "AUR") article for important usage topics. For now, only download and extract the tarball for [packettracer](https://aur.archlinux.org/packages/packettracer/) from the [AUR](/index.php/AUR "AUR")

You will need to enable the [Multilib](/index.php/Multilib "Multilib") repository to continue. Ensure to update the package list and upgrade with `pacman -Syu`

[Install](/index.php/Install "Install") [lib32-openssl](https://www.archlinux.org/packages/?name=lib32-openssl), [lib32-qt4](https://www.archlinux.org/packages/?name=lib32-qt4), [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng), and [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) from the [official repositories](/index.php/Official_repositories "Official repositories"). Answer yes if you are asked to remove gcc-libs.

You will need to have access to the file `Cisco Packet Tracer 6.0.1 for Linux (with tutorials)` to continue with the installation. For your convenience, the sha1sum and md5sum of this file is provided below.

```
$ sha1sum Cisco\ Packet\ Tracer\ 6.0.1\ for\ Linux\ \(with\ tutorials\)
81f74633115fab6bd1cb699f203a5a5375830c30  Cisco Packet Tracer 6.0.1 for Linux (with tutorials)
$ md5sum Cisco\ Packet\ Tracer\ 6.0.1\ for\ Linux\ \(with\ tutorials\)
6d623bc0761cbb6e3cdccb3c0e0ec70b  Cisco Packet Tracer 6.0.1 for Linux (with tutorials)

```

Copy this file to your working directory, maintaining the name. The [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") file found in the earlier tarball will require this archive. It is not provided in the tarball itself for ethical and legal reasons. This file requirement may change in the future, based on the version of packet tracer available at that time. At the time of writing, the proper file name is `Cisco Packet Tracer 6.0.1 for Linux (with tutorials)`.

After you have copied the file to the working directory (the directory you extracted the tarball to), you may now continue installation normally.

Finally, please read the EULA at `/usr/share/licenses/packettracer/eula.txt` and uninstall if you do not agree. If you agree, the program can be found under most menu systems in the Internet category.

### Assessment environment check

_This applies to both 32-bit and 64-bit systems._

The Cisco Packet Tracer-based Assessment Environment Check is used to confirm that students can start packet tracer activities for assessments such as practice and final exams. It is critical that you have a working version of [Java](/index.php/Java "Java") installed. Perform the check at [this page](http://skills.netacad.net/check/check.html) to confirm whether or not this ability is functional.

### Video supplements

You may use these videos as supplements to the installation to either ease or visualize the installation process.

[PacketTracer -- Archlinux 32-bit](http://youtu.be/XBPLOxuXvAw)

[PacketTracer -- Archlinux 64-bit](http://youtu.be/NPJpQrZ1C_s)

## See also

*   [Gns3](/index.php/Gns3 "Gns3")
*   [Cisco Packet Tracer - Networking Academy](https://www.netacad.com/web/about-us/cisco-packet-tracer)
*   [Cisco Packet Tracer-based Assessment Environment Check](http://skills.netacad.net/check/check.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PacketTracer&oldid=412152](https://wiki.archlinux.org/index.php?title=PacketTracer&oldid=412152)"