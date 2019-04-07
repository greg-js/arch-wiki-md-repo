Related articles

*   [Remastering the Install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO")
*   [Archiso as pxe server](/index.php/Archiso_as_pxe_server "Archiso as pxe server")
*   [Archboot](/index.php/Archboot "Archboot")
*   [Offline installation](/index.php/Offline_installation "Offline installation")

**Archiso** is a small set of bash scripts capable of building fully functional Arch Linux live CD/DVD/USB images. It is the same tool used to generate the official images, but since it is a very generic tool, it can be used to generate anything from rescue systems, install disks, to special interest live CD/DVD/USB systems, and who knows what else. Simply put, if it involves Arch on a shiny coaster, it can do it. The heart and soul of Archiso is *mkarchiso*. All of its options are documented in its usage output, so its direct usage will not be covered here. Instead, this wiki article will act as a guide for rolling your own live media in no time!

If you require a technical run-down of requirements and build steps only, have a look at the [official project documentation](https://git.archlinux.org/archiso.git/tree/docs) too.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Setup](#Setup)
*   [2 Configure the live medium](#Configure_the_live_medium)
    *   [2.1 Installing packages](#Installing_packages)
        *   [2.1.1 Custom local repository](#Custom_local_repository)
        *   [2.1.2 Preventing installation of packages belonging to base group](#Preventing_installation_of_packages_belonging_to_base_group)
        *   [2.1.3 Installing packages from multilib](#Installing_packages_from_multilib)
    *   [2.2 Adding files to image](#Adding_files_to_image)
    *   [2.3 Boot Loader](#Boot_Loader)
        *   [2.3.1 UEFI Secure Boot](#UEFI_Secure_Boot)
    *   [2.4 Login manager](#Login_manager)
    *   [2.5 Changing Automatic Login](#Changing_Automatic_Login)
*   [3 Build the ISO](#Build_the_ISO)
    *   [3.1 Rebuild the ISO](#Rebuild_the_ISO)
*   [4 Using the ISO](#Using_the_ISO)
*   [5 See also](#See_also)
    *   [5.1 Documentation and tutorials](#Documentation_and_tutorials)
    *   [5.2 Example customization template](#Example_customization_template)
    *   [5.3 Creating a offline installation ISO](#Creating_a_offline_installation_ISO)
    *   [5.4 Find a previous version of an ISO image](#Find_a_previous_version_of_an_ISO_image)

## Setup

**Note:** It is recommended to act as root in all the following steps. If not, it is very likely to have problems with false permissions later.

Before you begin, [install](/index.php/Install "Install") the [archiso](https://www.archlinux.org/packages/?name=archiso) or [archiso-git](https://aur.archlinux.org/packages/archiso-git/) package.

Archiso comes with two "profiles": *releng* and *baseline*.

*   If you wish to create a fully customized live version of Arch Linux, pre-installed with all your favorite programs and configurations, use *releng*.
*   If you just want to create the most basic live medium, with no pre-installed packages and a minimalistic configuration, use *baseline*.

Now, copy the profile of your choice to a directory (*archlive* in the example below) where you can make adjustments and build it. Execute the following, replacing `**profile**` with either `releng` or `baseline`.

```
# cp -r /usr/share/archiso/configs/**profile**/ *archlive*

```

*   If you are using the `releng` profile to make a fully customized image, then you can proceed onto [#Configure the live medium](#Configure_the_live_medium).
*   If you are using the `baseline` profile to create a bare image, then you will not be needing to do any customization and can proceed onto [#Build the ISO](#Build_the_ISO).

## Configure the live medium

This section details configuring the image you will be creating, allowing you to define the packages and configurations you want your live image to contain.

Inside the `*archlive*` directory created in [#Setup](#Setup) there are a number of files and directories; we are only concerned with a few of these, mainly:

*   `packages.x86_64` - this is where you list, line by line, the packages you want to have installed, and
*   the `airootfs` directory - this directory acts as an overlay and it is where you make all the customizations.

Generally, every administrative task that you would normally do after a fresh install except for package installation can be scripted into `*archlive*/airootfs/root/customize_airootfs.sh`. It has to be written from the perspective of the new environment, so `/` in the script means the root of the live-iso which is to be created.

### Installing packages

Edit the lists of packages in `packages.x86_64` to indicate which packages are to be installed on the live medium.

**Note:** If you want to use a [window manager](/index.php/Window_manager "Window manager") in the Live CD then you must add the necessary and correct [video drivers](/index.php/Video_drivers "Video drivers"), or the WM may freeze on loading.

#### Custom local repository

For the purpose of preparing custom packages or packages from [AUR](/index.php/AUR "AUR")/[ABS](/index.php/ABS "ABS"), you could also [create a custom local repository](/index.php/Custom_local_repository "Custom local repository"). You can then add your repository by putting the following into `~/archlive/pacman.conf`, above the other repository entries (for top priority):

 `~/archlive/pacman.conf` 
```
...
# custom repository
[customrepo]
SigLevel = Optional TrustAll
Server = file:///home/**user**/customrepo/$arch
...
```

#### Preventing installation of packages belonging to base group

By default, `/usr/bin/mkarchiso`, a script which is used by `~/archlive/build.sh`, calls one of the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) named `pacstrap` without the `-i` flag, which causes [Pacman](/index.php/Pacman "Pacman") to not wait for user input during the installation process.

When blacklisting base group packages by adding them to the `IgnorePkg` line in `~/archlive/pacman.conf`, [Pacman](/index.php/Pacman "Pacman") asks if they still should be installed, which means they will when user input is bypassed. To get rid of these packages there are several options:

*   **Dirty**: Add the `-i` flag to each line calling `pacstrap` in `/usr/bin/mkarchiso`.

*   **Clean**: Create a copy of `/usr/bin/mkarchiso` in which you add the flag and adapt `~/archlive/build.sh` so that it calls the modified version of the mkarchiso script.

*   **Advanced**: Create a function for `~/archlive/build.sh` which explicitly removes the packages after the base installation. This would leave you the comfort of not having to type enter so much during the installation process.

#### Installing packages from multilib

To install packages from the [multilib](/index.php/Multilib "Multilib") repository simply uncomment the repository in `~/archlive/pacman.conf`:

 `pacman.conf` 
```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
```

### Adding files to image

**Note:** You must be root to do this, do not change the ownership of any of the files you copy over, **everything** within the airootfs directory must be root owned. Proper ownerships will be sorted out shortly.

The airootfs directory acts as an overlay, think of it as root directory '/' on your current system, so any files you place within this directory will be copied over on boot-up.

So if you have a set of iptables scripts on your current system you want to be used on you live image, copy them over as such:

```
# cp -r /etc/iptables ~/archlive/airootfs/etc

```

Placing files in the users home directory is a little different. Do not place them within `airootfs/home`, but instead create a skel directory within `airootfs/` and place them there. We will then add the relevant commands to the `customize_airootfs.sh` which we are going to use to copy them over on boot and sort out the permissions.

First, create the skel directory:

```
# mkdir ~/archlive/airootfs/etc/skel

```

Now copy the 'home' files to the skel directory, e.g for `.bashrc`:

```
# cp ~/.bashrc ~/archlive/airootfs/etc/skel/

```

When `~/archlive/airootfs/root/customize_airootfs.sh` is executed and a new user is created, the files from the skel directory will automatically be copied over to the new home folder, permissions set right.

Similarly, some care is required for special configuration files that reside somewhere down the hierarchy. As an example the `/etc/X11/xinit/xinitrc` configuration file resides on a path that might be overwritten by installing a package. To place the configuration file one should put the custom `xinitrc` in `~/archlive/airootfs/etc/skel/` and then modify `customize_airootfs.sh` to move it appropriately.

### Boot Loader

The default file should work fine, so you should not need to touch it.

Due to the modular nature of isolinux, you are able to use lots of addons since all *.c32 files are copied and available to you. Take a look at the [official syslinux site](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) and the [archiso git repo](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). Using said addons, it is possible to make visually attractive and complex menus. See [here](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

#### UEFI Secure Boot

If you want to make your Archiso bootable on a UEFI Secure Boot enabled environment, you must use a signed bootloader. You can follow the instructions on [Secure Boot#Booting an install media](/index.php/Secure_Boot#Booting_an_install_media "Secure Boot").

### Login manager

Starting X at boot is done by enabling your login manager's [systemd](/index.php/Systemd "Systemd") service. If you know which .service file needs a softlink: Great. If not, you can easily find out in case you are using the same program on the system you build your iso on. Just use:

```
$ ls -l /etc/systemd/system/display-manager.service

```

Now create the same softlink in `~/archlive/airootfs/etc/systemd/system`. For LXDM:

```
# ln -s /usr/lib/systemd/system/lxdm.service ~/archlive/airootfs/etc/systemd/system/display-manager.service

```

This will enable LXDM at system start on your live system.

Alternatively you can just enable the service in `airootfs/root/customize_airootfs.sh` along with other services that are enabled there.

If you want the graphical environment to actually start automatically during boot make sure to edit `airootfs/root/customize_airootfs.sh` and replace

```
systemctl set-default multi-user.target

```

with

```
systemctl set-default graphical.target

```

### Changing Automatic Login

The configuration for getty's automatic login is located under `airootfs/etc/systemd/system/getty@tty1.service.d/autologin.conf`.

You can modify this file to change the auto login user:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --autologin **isouser** --noclear %I 38400 linux

```

Or remove it altogether to disable auto login.

## Build the ISO

Now you are ready to turn your files into the .iso which you can then burn to CD or USB.

Inside `~/archlive`, execute:

```
# ./build.sh -v

```

The script will now download and install the packages you specified to `work/*/airootfs`, create the kernel and init images, apply your customizations and finally build the iso into `out/`.

### Rebuild the ISO

Rebuilding the iso after modifications is not officially supported. However, it is easily possible by applying two steps. First you have to remove lock files in the work directory:

```
# rm -v work/build.make_*

```

If you have edited `airootfs/root/customize_airootfs.sh` to create an unprivileged user, the rebuild will fail when creating it because the user will already exist ([FS#41865](https://bugs.archlinux.org/task/41865)). To avoid this issue, you need to check if the user exists before running `useradd`, e.g. by running `id`:

```
! id arch && useradd -m -p "" -g users -G "adm,audio,floppy,log,network,rfkill,scanner,storage,optical,power,wheel" -s /usr/bin/zsh arch

```

Also remove persistent data such as created users or symlinks such as `/etc/sudoers`.

Rebuilds can be sped up slightly by editing the pacstrap script (located at /bin/pacstrap) and changing the following at line 361:

Before:

```
if ! pacman -r "$newroot" -Sy "${pacman_args[@]}"; then

```

After:

```
if ! pacman -r "$newroot" -Sy --needed "${pacman_args[@]}"; then

```

This increases the speed of the initial bootstrap, since it does not have to download and install any of the base packages that are already installed.

## Using the ISO

See the [Installation guide](/index.php/Installation_guide "Installation guide") article for various options.

## See also

### Documentation and tutorials

*   [Archiso project page](https://projects.archlinux.org/archiso.git)
*   [Official documentation](https://projects.archlinux.org/archiso.git/tree/docs)

### Example customization template

*   [A live DJ distribution powered by ArchLinux and built with Archiso](http://easy.open.and.free.fr/didjix/)

### Creating a offline installation ISO

*   [Archiso offline](/index.php/Archiso_offline "Archiso offline")

### Find a previous version of an ISO image

*   [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive")