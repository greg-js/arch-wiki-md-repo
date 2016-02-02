# Installing Cell Broadband Engine SDK

The CBE SDK installation only supports the Fedora 9 or RHEL linux distributions. I managed to install it on my Arch Linux system with the help of [a post in the gentoo forum](http://forums.gentoo.org/viewtopic-t-685982.html), and doing some trial/error.

## Contents

*   [1 Required Packages](#Required_Packages)
*   [2 Installation](#Installation)
    *   [2.1 Get ISOs and build the SDK](#Get_ISOs_and_build_the_SDK)
*   [3 Running the Simulator](#Running_the_Simulator)
    *   [3.1 Other...](#Other...)

## Required Packages

All of the following required packages are provided by the pacman databases and the versions should be recent enough.

Core repository:

*   gcc 4.x
*   glibc
*   perl 5.x
*   freeglut
*   gawk
*   bison
*   flex

Extra repository:

*   rpmextract
*   tcl
*   tk

To make sure all of these are installed:

```
# pacman -S gcc glibc perl freeglut gawk bison flex rpmextract tcl tk

```

## Installation

### Get ISOs and build the SDK

You will have to download the two 3.1 SDK ISOs (Developer, Extra) for Fedora 9 manually from [IBMs website](https://www14.software.ibm.com/webapp/iwm/web/reg/download.do?source=cellsdk&S_PKG=fedora&S_TACT=105AGX16&S_CMP=LP&lang=en_US&cp=UTF-8), which requires free registration. Place them in a build folder for the [cellsdk](https://aur.archlinux.org/packages/cellsdk/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cellsdk)]</sup> AUR package. Now the SDK is ready to be build, but you will have to do it as root because the PKGBUILD uses mount of loop-devices to extract packages from the ISOs. Build the SDK by running:

```
sudo makepkg --asroot

```

Now a cellsdk-3.1-1-x86_64.pkg.tar.gz should be ready for installation! Just run

```
sudo pacman -A cellsdk-3.1-1-x86_64.pkg.tar.gz

```

and now the SDK is installed and ready for use.

## Running the Simulator

Go to /opt/ibm/systemsim-cell/ directory and type sudo ./systemsim -g You can run without root by changing the owner and group.

```
sudo chown -R /opt/ibm/systemsim-cell
sudo chgrp -R /opt/ibm/systemsim-cell 

```

```
cd /opt/ibm/systemsim-cell/bin/s
./systemsim -g

```

### Other...

Since the PKGBUILD does not run the official install script there is bound to be something not setup completely correct... Place a comment on the [cellsdk](https://aur.archlinux.org/packages/cellsdk/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cellsdk)]</sup> AUR page.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Installing_Cell_Broadband_Engine_SDK&oldid=392269](https://wiki.archlinux.org/index.php?title=Installing_Cell_Broadband_Engine_SDK&oldid=392269)"