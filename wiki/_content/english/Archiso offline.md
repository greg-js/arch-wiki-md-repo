Related articles

*   [Archiso](/index.php/Archiso "Archiso")

**Archiso Offline** is a addon to the traditional [archiso](https://www.archlinux.org/packages/?name=archiso) package. Enabling users to build a offline installation ISO based on the official ISO. Much like most other Linux distributions have as their default option, Arch users can create similar ISO builds with this package.

A additional feature of Archiso Offline is AUR packages are possible to include in the ISO build process.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Setup](#Setup)
    *   [1.1 Installing packages](#Installing_packages)
*   [2 Build the ISO](#Build_the_ISO)
    *   [2.1 Example build process](#Example_build_process)
*   [3 See also](#See_also)
    *   [3.1 Documentation and tutorials](#Documentation_and_tutorials)
    *   [3.2 Example build script](#Example_build_script)
    *   [3.3 Known shortcommings](#Known_shortcommings)

## Setup

[install](/index.php/Install "Install") [archiso-offline-releng](https://aur.archlinux.org/packages/archiso-offline-releng/), this will also install [archiso](https://www.archlinux.org/packages/?name=archiso) *(or use [archiso-git](https://aur.archlinux.org/packages/archiso-git/) if installed)*.

The setup steps after installing this package is mostly identical with [Archiso](/index.php/Archiso "Archiso").
However, by default Archiso comes with two "profiles": *releng* and *baseline*, Archiso Offline adds one additional profile called *offline_releng*.

The *offline_releng* profile replaces all of the online-dependent steps in a normal [installation process](/index.php/Installation_guide "Installation guide") with locally hosted packages within the ISO. So instead of trying to fetch packages online, packages are sourced from the ISO directly.

The build process enables this by by sourcing the `packages.x86_64` and running `pacman --noconfirm -w --cachedir ... <packages>` and placing the files in a *HTTP-like* structure under `/srv/http`. Then pointing the ISO `pacman.conf` to that structure.
AUR packages are also sourced, but cached a little bit differently. But AUR packages are sourced from `packages.aur`.
The full list of packages sourced by default are `base base-devel` and any packages listed in `packages.x86_64` from the official *releng* config.

Additional packages can be added as described in [Archiso#Configure the live medium](/index.php/Archiso#Configure_the_live_medium "Archiso")

### Installing packages

Follow the same procedure as described in [Archiso#Installing packages](/index.php/Archiso#Installing_packages "Archiso"), the only difference being `packages.aur` which is a additional feature in the build process, enabling the possibility to include [AUR Packages](https://aur.archlinux.org) into the offline medium.

**Note:** If AUR packages are found by the build process, a build-user will be automatically created with `"%wheel ALL=(ALL) NO"` sudoers permission. It's a known issue and a long term bad solution. Make sure your sudoers file looks correct after building your offline ISO for now.

## Build the ISO

Again, assuming you've followed the [Archiso](/index.php/Archiso "Archiso") documentation, more specifically the [Archiso#Build the ISO](/index.php/Archiso#Build_the_ISO "Archiso") steps, you should have a ISO under:

```
# ~/archlive/out/

```

### Example build process

Example of **installation steps**:

```
# mkdir -p /tmp/archiso-offline
# cd /tmp/archiso-offline
# wget [https://aur.archlinux.org/cgit/aur.git/snapshot/archiso-offline-releng.tar.gz](https://aur.archlinux.org/cgit/aur.git/snapshot/archiso-offline-releng.tar.gz)
# tar xvzf archiso-offline-releng
# cd archiso-offline-releng
# makepkg -s
# sudo pacman -U *.xz

```

The actual **build process**:

```
# mkdir -p /tmp/iso_build_dir
# cp -r /usr/share/archiso/configs/offline_releng/* /tmp/iso_build_dir/
# cd /tmp/iso_build_dir
# echo "python" >> packages.x86_64
# echo "lighttpd2-git" >> packages.aur
# echo "systemctl enable lighttpd2" >> ./airootfs/root/customize_airootfs.sh
# rm -rf work*
# ./build.sh -v
# file out/*.iso

```

And that should be it. This example installs [python](https://www.archlinux.org/packages/?name=python) to the live ISO environment as well as [lighttpd2-git](https://aur.archlinux.org/packages/lighttpd2-git/). It also enables auto-start of **lighttpd2** once the ISO boots.

## See also

### Documentation and tutorials

*   [Archiso project page](https://projects.archlinux.org/archiso.git)
*   [Official Archiso documentation](https://projects.archlinux.org/archiso.git/tree/docs)

### Example build script

*   [Four types of build scripts for Archiso Offline.](https://github.com/Torxed/Scripts/tree/master/bash/build-scripts/isos)

### Known shortcommings

A few things and issues are known in this project.
The first being that some packages might want to be hosted locally, but not installed locally in the ISO environment. As of today there is no good solution for this, so all packages declared in `packages.{x86_64, aur`} are both installed - and hosted in the ISO environment.

Another big issue is the AUR build-user. There is no clear way to solve this, but there are better solutions than the one in place today. Especially the use of `sudoers`.