**Archiso** is a small set of bash scripts capable of building fully functional Arch Linux live CD/DVD/USB images. It is the same tool used to generate the official images, but since it is a very generic tool, it can be used to generate anything from rescue systems, install disks, to special interest live CD/DVD/USB systems, and who knows what else. Simply put, if it involves Arch on a shiny coaster, it can do it. The heart and soul of Archiso is *mkarchiso*. All of its options are documented in its usage output, so its direct usage will not be covered here. Instead, this wiki article will act as a guide for rolling your own live media in no time!

## Contents

*   [1 Setup](#Setup)
*   [2 Configure the live medium](#Configure_the_live_medium)
    *   [2.1 Installing packages](#Installing_packages)
        *   [2.1.1 Custom local repository](#Custom_local_repository)
        *   [2.1.2 Avoid installation of packages belonging to base group](#Avoid_installation_of_packages_belonging_to_base_group)
        *   [2.1.3 Installing packages from multilib](#Installing_packages_from_multilib)
    *   [2.2 Adding files to image](#Adding_files_to_image)
    *   [2.3 Boot Loader](#Boot_Loader)
    *   [2.4 Login manager](#Login_manager)
    *   [2.5 Changing Automatic Login](#Changing_Automatic_Login)
*   [3 Build the ISO](#Build_the_ISO)
    *   [3.1 Rebuild the ISO](#Rebuild_the_ISO)
*   [4 Using the ISO](#Using_the_ISO)
    *   [4.1 CD](#CD)
    *   [4.2 USB](#USB)
    *   [4.3 GRUB](#GRUB)
    *   [4.4 grub4dos](#grub4dos)
*   [5 Installation without Internet access](#Installation_without_Internet_access)
    *   [5.1 Install the archiso to the new root](#Install_the_archiso_to_the_new_root)
    *   [5.2 Chroot and configure the base system](#Chroot_and_configure_the_base_system)
        *   [5.2.1 Restore the configuration of journald](#Restore_the_configuration_of_journald)
        *   [5.2.2 Remove special udev rule](#Remove_special_udev_rule)
        *   [5.2.3 Disable and remove the services created by archiso](#Disable_and_remove_the_services_created_by_archiso)
        *   [5.2.4 Remove special scripts of the Live environment](#Remove_special_scripts_of_the_Live_environment)
        *   [5.2.5 Configure the system](#Configure_the_system)
*   [6 See also](#See_also)
    *   [6.1 Documentation and tutorials](#Documentation_and_tutorials)
    *   [6.2 Example customization template](#Example_customization_template)

## Setup

**Note:**

*   To use Archiso you must be running on a x86_64 platform. [[1]](https://projects.archlinux.org/archiso.git/tree/docs/README.build#n67)
*   It is recommended to act as root in all the following steps. If not, it is very likely to have problems with false permissions later.

Before you begin, [install](/index.php/Install "Install") the [archiso](https://www.archlinux.org/packages/?name=archiso) or [archiso-git](https://aur.archlinux.org/packages/archiso-git/) package.

Archiso comes with two "profiles": *releng* and *baseline*.

*   If you wish to create a fully customised live version of Arch Linux, pre-installed with all your favourite programs and configurations, use *releng*.
*   If you just want to create the most basic live medium, with no pre-installed packages and a minimalistic configuration, use *baseline*.

Now, copy the profile of your choice to a directory where you can make adjustments and build it (we will use `~/archlive`). Execute the following, replacing `**profile**` with either `releng` or `baseline`.

```
# cp -r /usr/share/archiso/configs/**profile**/* ~/archlive

```

*   If you are using the `releng` profile to make a fully customised image, then you can proceed onto [#Configure the live medium](#Configure_the_live_medium).
*   If you are using the `baseline` profile to create a bare image, then you will not be needing to do any customisations and can proceed onto [#Build the ISO](#Build_the_ISO).

## Configure the live medium

This section details configuring the image you will be creating, allowing you to define the packages and configurations you want your live image to contain.

Inside the `~/archlive` directory there are a number of files and directories; we are only concerned with a few of these, mainly:

*   `packages.*` - this is where you list, line by line, the packages you want to have installed, and
*   the `airootfs` directory - this directory acts as an overlay and it is where you make all the customisations.

Generally, every administrative task that you would normally do after a fresh install except for package installation can be scripted into `~/archlive/airootfs/root/customize_airootfs.sh`. It has to be written from the perspective of the new environment, so `/` in the script means the root of the live-iso which is created.

### Installing packages

You will want to create a list of packages you want installed on your live CD system. A file full of package names, one-per-line, is the format for this. This is *great* for special interest live CDs, just specify packages you want in packages.both and bake the image. The `packages.i686` and `packages.x86_64` files allow you to install software on just 32-bit or 64-bit, respectively.

**Note:** If you want to use a [window manager](/index.php/Window_manager "Window manager") in the Live CD then you must add the necessary and correct [video drivers](/index.php/Video_drivers "Video drivers"), or the WM may freeze on loading.

#### Custom local repository

You can also [create a custom local repository](/index.php/Custom_local_repository "Custom local repository") for the purpose of preparing custom packages or packages from [AUR](/index.php/AUR "AUR")/[ABS](/index.php/ABS "ABS"). When doing so with packages for both architectures, you should follow a certain directory order to not run into problems.

For instance:

*   `~/customrepo`
    *   `~/customrepo/x86_64`
        *   `~/customrepo/x86_64/foo-x86_64.pkg.tar.xz`
        *   `~/customrepo/x86_64/customrepo.db.tar.gz`
        *   `~/customrepo/x86_64/customrepo.db` (symlink created by `repo-add`)
    *   `~/customrepo/i686`
        *   `~/customrepo/i686/foo-i686.pkg.tar.xz`
        *   `~/customrepo/i686/customrepo.db.tar.gz`
        *   `~/customrepo/i686/customrepo.db` (symlink created by `repo-add`)

You can then add your repository by putting the following into `~/archlive/pacman.conf`, above the other repository entries (for top priority):

```
# custom repository
[customrepo]
SigLevel = Optional TrustAll
Server = file:///home/**user**/customrepo/$arch

```

So, the build scripts just look for the appropriate packages.

If this is not the case you will be running into error messages similar to this:

```
error: failed to prepare transaction (package architecture is not valid)
:: package foo-i686 does not have a valid architecture

```

#### Avoid installation of packages belonging to base group

By default, `/usr/bin/mkarchiso`, a script which is used by `~/archlive/build.sh`, calls one of the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) named `pacstrap` without the `-i` flag, which causes [Pacman](/index.php/Pacman "Pacman") to not wait for user input during the installation process.

When blacklisting base group packages by adding them to the `IgnorePkg` line in `~/archlive/pacman.conf`, [Pacman](/index.php/Pacman "Pacman") asks if they still should be installed, which means they will when user input is bypassed. To get rid of these packages there are several options:

*   **Dirty**: Add the `-i` flag to each line calling `pacstrap` in `/usr/bin/mkarchiso`.

*   **Clean**: Create a copy of `/usr/bin/mkarchiso` in which you add the flag and adapt `~/archlive/build.sh` so that it calls the modified version of the mkarchiso script.

*   **Advanced**: Create a function for `~/archlive/build.sh` which explicitly removes the packages after the base installation. This would leave you the comfort of not having to type enter so much during the installation process.

#### Installing packages from multilib

To install packages from the [multilib](/index.php/Multilib "Multilib") repository you have to create two pacman configuration files: one for x86_64 and one for i686\. Copy `pacman.conf` to `pacmanx86_64.conf` and `pacmani686.conf`. Uncomment the following lines to enable *multilib* in `pacmanx86_64.conf`:

 `pacmanx86_64.conf` 
```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
```

Then edit `build.sh` with an editor. Replace the following lines:

 `build.sh` 
```
run_once make_pacman_conf

# Do all stuff for each airootfs
for arch in i686 x86_64; do
    run_once make_basefs
    run_once make_packages
done

run_once make_packages_efi

for arch in i686 x86_64; do
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

```

with:

 `build.sh` 
```
cp -v releng/pacmanx86_64.conf releng/pacman.conf
run_once make_pacman_conf

# Do all stuff for each airootfs
for arch in x86_64; do
    run_once make_basefs
    run_once make_packages
    run_once make_packages_efi
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

echo make_pacman_conf i686
cp -v releng/pacmani686.conf releng/pacman.conf
cp -v releng/pacmani686.conf ${work_dir}/pacman.conf

for arch in i686; do
    run_once make_basefs
    run_once make_packages
    run_once make_packages_efi
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

```

In this way packages for x86_64 and i686 will be installed with their own pacman configuration file.

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
ExecStart=-/sbin/agetty --autologin **isouser** --noclear %I 38400 linux

```

Or remove it altogether to disable auto login.

## Build the ISO

Now you are ready to turn your files into the .iso which you can then burn to CD or USB:

First create the `out/` directory,

```
# mkdir ~/archlive/out/

```

then inside `~/archlive`, execute:

```
# ./build.sh -v

```

The script will now download and install the packages you specified to `work/*/airootfs`, create the kernel and init images, apply your customizations and finally build the iso into `out/`.

### Rebuild the ISO

Rebuilding the iso after modifications is not officially supported. However, it is easily possible by applying two steps. First you have to remove lock files in the work directory:

```
# rm -v work/build.make_*

```

Furthermore it is required to edit the script `airootfs/root/customize_airootfs.sh`, and add an id command in the beginning of the `useradd` line as shown here. Otherwise the rebuild stops at this point because the user that is to be added already exists [[2]](https://bugs.archlinux.org/task/41865).

```
! id arch && useradd -m -p "" -g users -G "adm,audio,floppy,log,network,rfkill,scanner,storage,optical,power,wheel" -s /usr/bin/zsh arch

```

Also remove persistent data such as created users or symlinks such as `/etc/sudoers`.

## Using the ISO

### CD

Just burn the iso to a CD. You can follow [Optical disc drive#Burning](/index.php/Optical_disc_drive#Burning "Optical disc drive") as you wish.

### USB

See [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media").

### GRUB

See [Multiboot USB drive#Arch Linux](/index.php/Multiboot_USB_drive#Arch_Linux "Multiboot USB drive").

### grub4dos

Grub4dos is a utility that can be used to create multiboot USBs, able to boot multiple linux distros from the same USB stick.

To boot the generated system on a USB with grub4dos already installed, loop mount the ISO and copy the entire `/arch` directory to the **root of the USB**. Then edit the `menu.lst` file from the grub4dos (it must be on the USB root) and add these lines:

```
title Archlinux x86_64
kernel /arch/boot/x86_64/vmlinuz archisolabel=<your usb label>
initrd /arch/boot/x86_64/archiso.img

```

Change the `x86_64` part as necessary and put your **real** usb label there.

## Installation without Internet access

If you wish to install the archiso (e.g. [the official monthly release](https://www.archlinux.org/download/)) as it is without an Internet connection, or, if you do not want to download the packages you want again:

First, follow the [Installation guide](/index.php/Installation_guide "Installation guide"), skipping the [Installation guide#Connect to the Internet](/index.php/Installation_guide#Connect_to_the_Internet "Installation guide") section, until the [Installation guide#Install the base packages](/index.php/Installation_guide#Install_the_base_packages "Installation guide") step.

### Install the archiso to the new root

Instead of installing the packages with `pacstrap` (which would try to download from the remote repositories), copy *everything* in the live environment to the new root:

```
# time cp -ax / /mnt

```

**Note:** The option (`-x`) excludes some special directories, as they should not be copied to the new root.

Then, copy the kernel image to the new root, in order to keep the integrity of the new system:

```
# cp -vaT /run/archiso/bootmnt/arch/boot/$(uname -m)/vmlinuz /mnt/boot/vmlinuz-linux

```

After that, generate a fstab as described in [Installation guide#Fstab](/index.php/Installation_guide#Fstab "Installation guide").

### Chroot and configure the base system

Next, chroot into your newly installed system:

```
# arch-chroot /mnt /bin/bash

```

**Note:** Before performing the other [Installation guide#Configure the system](/index.php/Installation_guide#Configure_the_system "Installation guide") steps (e.g. locale, keymap, etc.), it is necessary to get rid of the trace of the Live environment (in other words, the customization of archiso which does not fit a non-Live environment).

#### Restore the configuration of journald

[This customization of archiso](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/root/customize_airootfs.sh#n19) will lead to storing the system journal in RAM, it means that the journal will not be available after reboot:

```
# sed -i 's/Storage=volatile/#Storage=auto/' /etc/systemd/journald.conf

```

#### Remove special udev rule

[This rule of udev](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) starts the dhcpcd automatically if there are any wired network interfaces.

```
# rm /etc/udev/rules.d/81-dhcpcd.rules

```

#### Disable and remove the services created by archiso

Some service files are created for the Live environment, please disable the services and remove the file as they are unnecessary for the new system:

```
# systemctl disable pacman-init.service choose-mirror.service
# rm -r /etc/systemd/system/{choose-mirror.service,pacman-init.service,etc-pacman.d-gnupg.mount,getty@tty1.service.d}
# rm /etc/systemd/scripts/choose-mirror

```

#### Remove special scripts of the Live environment

There are some scripts installed in the live system by archiso scripts, which are unnecessary for the new system:

```
# rm /etc/systemd/system/getty@tty1.service.d/autologin.conf
# rm /root/{.automated_script.sh,.zlogin}
# rm /etc/mkinitcpio-archiso.conf
# rm -r /etc/initcpio

```

#### Configure the system

Now you can follow the skipped steps of the [Installation guide#Configure the system](/index.php/Installation_guide#Configure_the_system "Installation guide") section (setting a locale, timezone, hostname, etc.) and finish the installation by creating an initial ramdisk as described in [Installation guide#Initramfs](/index.php/Installation_guide#Initramfs "Installation guide").

## See also

### Documentation and tutorials

*   [Archiso project page](https://projects.archlinux.org/archiso.git)
*   [Official documentation](https://projects.archlinux.org/archiso.git/tree/docs)

### Example customization template

*   [A live DJ distribution powered by ArchLinux and built with Archiso](http://didjix.blogspot.com/)