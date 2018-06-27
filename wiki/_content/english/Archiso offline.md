[se:Archiso utan internet](/index.php?title=Se:Archiso_utan_internet&action=edit&redlink=1 "Se:Archiso utan internet (page does not exist)")

Related articles

*   [Archiso](/index.php/Archiso "Archiso")

**Archiso offline** is a addon to the traditional [archiso](https://www.archlinux.org/packages/?name=archiso) package. This addon simply creates a CD/DVD much like most other Linux distributions have, a self-contained CD/DVD with all the packages needed to install a base Arch Linux system as well as offer AUR packaging (optional).

## Contents

*   [1 Setup](#Setup)
    *   [1.1 Installing packages](#Installing_packages)
*   [2 Build the ISO](#Build_the_ISO)
*   [3 See also](#See_also)
    *   [3.1 Documentation and tutorials](#Documentation_and_tutorials)
    *   [3.2 Example build script](#Example_build_script)

## Setup

[install](/index.php/Install "Install") [archiso-offline-releng](https://aur.archlinux.org/packages/archiso-offline-releng/), this will install [archiso](https://www.archlinux.org/packages/?name=archiso) (or use [archiso-git](https://aur.archlinux.org/packages/archiso-git/) if installed) since it's a heavy dependency for this package.

The installation steps after installing this package is mostly identical with [Archiso](/index.php/Archiso "Archiso"). However, by default Archiso comes with two "profiles": *releng* and *baseline*. This package adds a additional "profile" called **offline_releng** which replaces all of the online-required steps in a installation process with locally hosted packages.

It does so by sourcing the `packages.x86_64` into `pacman --noconfirm -w --cachedir ...` and placing the files in a *HTTP-like* structure under `/srv/http`. The full list of packages sourced by default are `base base-devel` and any packages listed in `packages.x86_64`.

Additional packages can be added as described in [Archiso#Configure_the_live_medium](/index.php/Archiso#Configure_the_live_medium "Archiso")

### Installing packages

Follow the same procedure as described in [Archiso#Installing_packages](/index.php/Archiso#Installing_packages "Archiso"), the only difference being `packages.aur` which is a additional feature in the build process enabling the possibility to include [AUR Packages](https://aur.archlinux.org) into the offline medium.

**Note:** If AUR packages are found by the build process, a build-user will be automatically created with `"%wheel ALL=(ALL) NO"` sudoers permission. It's a known issue and a long term bad solution. Make sure your sudoers file looks correct after building your offline ISO for now.

## Build the ISO

Again, assuming you've followed the [Archiso](/index.php/Archiso "Archiso") documentation, more specifically the [Archiso#Build_the_ISO](/index.php/Archiso#Build_the_ISO "Archiso") steps, you should have a ISO under:

```
# ~/archlive/out/

```

## See also

### Documentation and tutorials

*   [Archiso project page](https://projects.archlinux.org/archiso.git)
*   [Official Archiso documentation](https://projects.archlinux.org/archiso.git/tree/docs)

### Example build script

*   [A Arch Linux Offline build script with custom script execution on live boot](https://github.com/Torxed/Scripts/blob/master/bash/build_offline)