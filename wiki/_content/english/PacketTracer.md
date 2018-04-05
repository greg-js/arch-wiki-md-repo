[Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer-download/) is a powerful network simulation program that allows students to experiment with network behavior and ask “what if” questions. As an integral part of the Networking Academy comprehensive learning experience, Packet Tracer provides simulation, visualization, authoring, assessment, and collaboration capabilities and facilitates the teaching and learning of complex technology concepts. [Source](https://www.netacad.com/web/about-us/cisco-packet-tracer)

## Contents

*   [1 Disclaimer](#Disclaimer)
*   [2 Installation](#Installation)
    *   [2.1 64-bit systems](#64-bit_systems)
    *   [2.2 Assessment environment check](#Assessment_environment_check)
*   [3 See also](#See_also)

## Disclaimer

Understand if you have permission from Cisco Systems to use this software. If you do not meet eligibility, discontinue your progress and consider alternatives such as [GNS3](/index.php/GNS3 "GNS3").

## Installation

### 64-bit systems

See the [AUR](/index.php/AUR "AUR") article for important usage topics. For now, only download and extract the tarball for [packettracer](https://aur.archlinux.org/packages/packettracer/) from the [AUR](/index.php/AUR "AUR").

You will need to have access to the file `PacketTracer71_64bit_linux.tar.gz` to continue with the installation. For your convenience, the sha1sum of this file is provided below.

```
$ sha1sum PacketTracer71_64bit_linux.tar.gz
bbc776e62725ac714c228e87e239dda4dfd9449c  PacketTracer71_64bit_linux.tar.gz

```

Copy this file to your working directory with the same name and continue the installation normally. The [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") file found in the earlier tarball will require this archive. It is not provided in the tarball itself for ethical and legal reasons. The required file may change in the future, based on the version of PacketTracer available at that time. At the time of writing, the file is named `PacketTracer71_64bit_linux.tar.gz`.

Finally, please read the EULA at `/usr/share/licenses/packettracer/eula.txt` and uninstall if you do not agree. If you agree, the program can be found under most menu systems in the Internet category.

### Assessment environment check

The Cisco Packet Tracer-based Assessment Environment Check is used to confirm that students can start packet tracer activities for assessments such as practice and final exams. It is critical that you have a working version of [Java](/index.php/Java "Java") installed. Perform the check at [this page](http://skills.netacad.net/check/check.html) to confirm whether or not this ability is functional.

```
javaws PT-Assessment-Client.jnlp

```

## See also

*   [GNS3](/index.php/GNS3 "GNS3")
*   [Cisco Packet Tracer - Networking Academy](https://www.netacad.com/web/about-us/cisco-packet-tracer)
*   [Cisco Packet Tracer-based Assessment Environment Check](http://skills.netacad.net/check/check.html)
*   [PacketTracer -- video visualizing the installation process](https://youtu.be/NPJpQrZ1C_s)