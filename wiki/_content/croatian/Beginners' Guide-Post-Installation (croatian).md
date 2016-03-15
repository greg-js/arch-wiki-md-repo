**Tip:** Ovo je dio višestraničnog vodiča za početnike. **[Klikni ovdje](/index.php/Beginners%27_Guide_(Hrvatski) "Beginners' Guide (Hrvatski)")** ako želiš čitati vodič u cijelosti.

## Contents

*   [1 Nakon instalacije](#Nakon_instalacije)
    *   [1.1 Nadogradnja](#Nadogradnja)
        *   [1.1.1 Configure the network (if necessary)](#Configure_the_network_.28if_necessary.29)
            *   [1.1.1.1 Wired LAN](#Wired_LAN)
            *   [1.1.1.2 Wireless LAN](#Wireless_LAN)
            *   [1.1.1.3 Proxy Server](#Proxy_Server)
            *   [1.1.1.4 Analog Modem, ISDN, and DSL (PPPoE)](#Analog_Modem.2C_ISDN.2C_and_DSL_.28PPPoE.29)
        *   [1.1.2 Update, Sync, and Upgrade the system with pacman](#Update.2C_Sync.2C_and_Upgrade_the_system_with_pacman)
            *   [1.1.2.1 /etc/pacman.conf](#.2Fetc.2Fpacman.conf)
            *   [1.1.2.2 Package Repositories](#Package_Repositories)
            *   [1.1.2.3 AUR](#AUR)
        *   [1.1.3 /etc/pacman.d/mirrorlist](#.2Fetc.2Fpacman.d.2Fmirrorlist)
        *   [1.1.4 rankmirrors](#rankmirrors)
            *   [1.1.4.1 Mirrorcheck for up-to-date packages](#Mirrorcheck_for_up-to-date_packages)
        *   [1.1.5 Get familiar with pacman](#Get_familiar_with_pacman)
        *   [1.1.6 Update the System](#Update_the_System)
            *   [1.1.6.1 Ignoring Packages](#Ignoring_Packages)
            *   [1.1.6.2 The Arch rolling release model](#The_Arch_rolling_release_model)
    *   [1.2 Adding a User](#Adding_a_User)
        *   [1.2.1 Deleting the user account](#Deleting_the_user_account)
*   [2 Extras](#Extras)
    *   [2.1 Create DVD and CDROM symlinks](#Create_DVD_and_CDROM_symlinks)
    *   [2.2 Sudo](#Sudo)
    *   [2.3 Sound](#Sound)
    *   [2.4 **G**raphical **U**ser **I**nterface](#Graphical_User_Interface)
        *   [2.4.1 Install X](#Install_X)
        *   [2.4.2 Install video driver](#Install_video_driver)
            *   [2.4.2.1 NVIDIA Graphics Cards](#NVIDIA_Graphics_Cards)
            *   [2.4.2.2 ATI Graphics Cards](#ATI_Graphics_Cards)
        *   [2.4.3 Install input drivers](#Install_input_drivers)
        *   [2.4.4 Configure X (Optional)](#Configure_X_.28Optional.29)
            *   [2.4.4.1 Non-US keyboard](#Non-US_keyboard)
        *   [2.4.5 Testing X](#Testing_X)
            *   [2.4.5.1 Message bus](#Message_bus)
            *   [2.4.5.2 Start X](#Start_X)
            *   [2.4.5.3 In case of errors](#In_case_of_errors)
            *   [2.4.5.4 Need Help?](#Need_Help.3F)
        *   [2.4.6 Install Fonts](#Install_Fonts)
        *   [2.4.7 Choose and install a graphical interface](#Choose_and_install_a_graphical_interface)
        *   [2.4.8 Methods for starting your Graphical Environment](#Methods_for_starting_your_Graphical_Environment)
            *   [2.4.8.1 Manually](#Manually)
            *   [2.4.8.2 Automatically](#Automatically)

## Nakon instalacije

**Čestitamo! Dobrodošli u svoj novi sustav Arch Linux!**

Ova sekcija će prolaziti kroz razne obavezne procedore nakon instalacije poput nadogradnje novog sustava i dodavanje regularnog korisnika ne-administratora.

### Nadogradnja

Your new Arch Linux base system is now a functional GNU/Linux environment ready for customization. From here, you may build this elegant set of tools into whatever you wish or require for your purposes.

Login with the root account. We will configure pacman and update the system as root.

**Note:** Virtual consoles 1-6 are available. You may switch between them with <ALT>+F1...F6

#### Configure the network (if necessary)

If you properly configured your system, you should have a working network. Try to `ping example.com` to verify:

 `$ ping -c 3 example.com ` 
```
PING example.com (192.0.43.10) 56(84) bytes of data.
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=1 ttl=248 time=25.6 ms
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=2 ttl=248 time=22.9 ms
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=3 ttl=248 time=23.6 ms

--- example.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 22.912/24.062/25.632/1.156 ms
```

If you have successfully established a network connection, continue with **[Update, Sync, and Upgrade the system with pacman](#Update.2C_Sync.2C_and_Upgrade_the_system_with_pacman)**.

If, after trying to ping www.google.com, an "unknown host" error is received, you may conclude that your network is not properly configured. You may choose to double-check the following files for integrity and proper settings:

`/etc/rc.conf` - Specifically, check your HOSTNAME and NETWORKING section for typos and errors.

`/etc/hosts` - Double-check for format, typos, and errors.

`/etc/resolv.conf` - If you are using a static IP. If you are using DHCP, this file will be dynamically created and destroyed by default.

**Tip:** Advanced instructions for configuring the network can be found in the [Network](/index.php/Network "Network") article.

##### Wired LAN

Check your Ethernet with

 `$ ip addr` 

All interfaces will be listed. You should see an entry for eth0, or perhaps eth1\. These examples will use eth0.

**Static IP**

If required, you can set a new static IP with:

 `# ip addr add <ip>/<netmask> dev <interface>` 

and the default gateway with

 `# ip route add default via <ip>` 

Verify that `/etc/resolv.conf` contains your DNS server and add it if it is missing. Check your network again with `ping -c 3 www.google.com`. If everything is working now, adjust `/etc/rc.conf` as described above for static IP.

**DHCP**

If you have a DHCP server/router in your network try:

 `# dhcpcd eth0` 

If this is working, adjust `/etc/rc.conf` as described above, for dynamic IP.

##### Wireless LAN

Please see [Wireless Quickstart For the Live Environment](/index.php/Beginners%27_Guide/Installation#Setup_wireless_in_the_live_environment_.28optional.29 "Beginners' Guide/Installation") for details on connecting to a wireless network. Although you are no longer running off the installation media, the commands are the same as long as you installed all related wireless packages during package selection. Remember, your wireless device may need firmware in order to operate. For troubleshooting, check the detailed [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") page.

##### Proxy Server

If you are behind a proxy server, edit `/etc/wgetrc` and set http_proxy and ftp_proxy in it.

##### Analog Modem, ISDN, and DSL (PPPoE)

See [Internet Access](/index.php/Internet_Access "Internet Access") for detailed instructions.

#### Update, Sync, and Upgrade the system with [pacman](/index.php/Pacman "Pacman")

Now we will update the system using [pacman](/index.php/Pacman "Pacman"). [Pacman](/index.php/Pacman "Pacman") is the **pac**kage **man**ager of Arch Linux. It manages your entire package system and handles installation, removal, package downgrade (through cache), custom compiled package handling, automatic dependency resolution, remote and local searches and much more. Pacman will now be used to download software packages from remote repositories and install them onto your system.

**Note:** If you installed via a Netinstall, many, if not all, of your packages will already be up to date. However, it is still advisable to run through this update process.

##### /etc/pacman.conf

pacman will attempt to read `/etc/pacman.conf` each time it is invoked. This configuration file is divided into sections, or repositories. Each section defines a package [repository](/index.php/Official_repositories "Official repositories") that pacman can use when searching for packages. The exception to this is the `options` section, which defines global options.

**Note:** The defaults should work, so modifying at this point may be unnecessary, but verification is always recommended. Further info available in the [Mirrors](/index.php/Mirrors "Mirrors") article.
 `# nano /etc/pacman.conf` 

Repositories are described below; enable all desired repositories by removing the # in front of the 'Include =' and '[repository]' lines.

**Note:** When choosing repos, be sure to uncomment both the repository header lines in [brackets] as well as the 'Include =' lines. Failure to do so will result in the selected repository being omitted! This is a very common error.

##### Package Repositories

A [software repository](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository") is a storage location from which software packages may be retrieved and installed on a computer. Arch Linux [package maintainers](/index.php/Package_Maintainer "Package Maintainer") (developers and [Trusted Users](/index.php/Trusted_Users "Trusted Users")) maintain a number of official repositories containing software packages for essential and popular software, readily accessible via [pacman](/index.php/Pacman "Pacman"). This article outlines those officially-supported repositories. See [Official repositories](/index.php/Official_repositories "Official repositories") for more information including details about the purpose of each repository.

Most people will want to use [core], [extra] and [community]. If you want to run 32-bit applications on Arch x86_64, enable the [multilib] repository by adding the lines below to `/etc/pacman.conf`:

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

##### AUR

The **[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")** (AUR) also contains the **unsupported** branch, which cannot be accessed directly by pacman. **AUR** [unsupported] does not contain binary packages. Rather, it provides more than thirty-one thousand PKGBUILD scripts for building packages from source, that may be unavailable through the other repos. When an AUR unsupported package acquires enough popular votes, it may be moved to the AUR [community] binary repo, if a trusted user (TU) is willing to adopt and maintain it there.

*   TU maintained
*   All PKGBUILD bash build scripts
*   **Not** pacman accessible by default

**Note:** There are a number of pacman wrappers (**[AUR helpers](/index.php/AUR_helpers "AUR helpers")**) available to help you seamlessly access AUR.

#### /etc/pacman.d/mirrorlist

Defines pacman repository mirrors and priorities.

**Note:** If your installation medium is old, your mirrorlist might be outdated, which might lead to problems when updating archlinux with pacman (see here for the [bug report](https://bugs.archlinux.org/task/22510)). Therefore it is a good idea to get the latest version of the mirrorlist from [the pacman mirror list generator page](https://www.archlinux.org/mirrorlist/). Copy the freshly generated list to `/etc/pacman.d/mirrorlist` before you continue.

Open `/etc/pacman.d/mirrorlist` in an editor and uncomment (remove the '#' in front) a server close to you. Then issue a complete package refresh:

 `# pacman -Syy` 

Passing two `--refresh` or `-y` flags forces pacman to refresh all package lists even if they are considered to be up to date. Issuing `pacman -Syy` *whenever a mirror is changed*, is good practice and will avoid possible headaches.

#### rankmirrors

Alternatively, you can use `rankmirrors`. `rankmirrors` is a bash script which will attempt to detect uncommented mirrors specified in `/etc/pacman.d/mirrorlist` which are closest to the installation machine based on latency. Faster mirrors will dramatically improve pacman performance, and the overall Arch Linux experience. This script may be run periodically, especially if the chosen mirrors provide inconsistent throughput and/or updates. Note that `rankmirrors` does not test for throughput. Tools such as `wget` or `rsync` may be used to effectively test for mirror throughput after a new `/etc/pacman.d/mirrorlist` has been generated.

Issue the following command to completely refresh package database, upgrade and install `curl`:

 `# pacman -Syyu curl` 

*   *If you get an error at this step, use the command `nano /etc/pacman.d/mirrorlist` and uncomment a server that suits you.*

`cd` to the `/etc/pacman.d/` directory:

 `# cd /etc/pacman.d` 

Backup the existing `/etc/pacman.d/mirrorlist`:

 `# cp mirrorlist mirrorlist.backup` 

Edit mirrorlist.backup and uncomment all mirrors on the same continent or within geographical proximity to test with rankmirrors.

 `# nano mirrorlist.backup` 

Run the script against the mirrorlist.backup with the -n switch and redirect output to a new /etc/pacman.d/mirrorlist file:

 `# rankmirrors -n 6 mirrorlist.backup > mirrorlist` 
**Note:** **-n 6**: will rank the 6 closest mirrors

Force pacman to refresh all package lists with the new mirrorlist in place:

 `# pacman -Syy` 

##### Mirrorcheck for up-to-date packages

Since `rankmirrors` does not take into account how up-to-date a mirror's package list is, it is important to note that one or more of the mirrors it selects as fastest may still be out-of-date. [ArchLinux MirrorStatus](https://www.archlinux.org/mirrors/status/) reports various aspects about the mirrors such as network problems with mirrors, data collection problems, the last time mirrors have been synced, etc. One may wish to manually inspect `/etc/pacman.d/mirrorlist`, ensuring that the file contains only up-to-date mirrors if having the latest package versions is a priority.

Alternatively, the [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) can automatically rank mirrors close to your location by how up-to-date they are.

**Tip:** For a script that automates the process of getting and installing a `mirrorlist` file from the Pacman Mirrorlist Generator, see [Mirrors](/index.php/Mirrors#Script_to_automate_use_of_Pacman_Mirrorlist_Generator "Mirrors").

#### Get familiar with pacman

pacman is the Arch user's best friend. It is highly recommended to study and learn how to use the pacman(8) tool. Try:

 `$ man pacman` 

For more information, have a look at the [pacman](/index.php/Pacman "Pacman") wiki entry at your own leisure, or check out the [pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") entry for a comparison to other popular package managers.

#### Update the System

You are now ready to upgrade your entire system. Before you do, read through the [news](https://www.archlinux.org/news/) (and optionally the [announce mailing list](https://archlinux.org/pipermail/arch-announce/)). Often the developers will provide important information about required configurations and modifications for known issues. Consulting these pages before any upgrade is good practice.

Sync, refresh, and upgrade your entire new system with:

 `# pacman -Syu` 

or:

 `# pacman --sync --refresh --sysupgrade` 

pacman will now download a fresh copy of the master package list from the server(s) defined in `/etc/pacman.conf` and perform all available upgrades. You may be prompted to upgrade pacman itself at this point. If so, say yes, and then reissue the `pacman -Syu` command when finished.

Reboot if a kernel upgrade has occurred.

**Note:** Occasionally, configuration changes may take place requiring user action during an update; read pacman's output for any pertinent information. See [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") for more details.

Pacman output is saved in `/var/log/pacman.log`.

See [Package Management FAQ](/index.php/FAQ#Package_Management "FAQ") for answers to frequently asked questions regarding updating and managing your packages.

##### Ignoring Packages

After executing the command `pacman -Syu`, the entire system will be updated. It is possible to prevent a package from being upgraded. A typical scenario would be a package for which an upgrade may prove problematic for the system. In this case, there are two options; indicate the package(s) to skip in the pacman command line using the --ignore switch (`pacman -S --help` for details) or permanently indicate the package(s) to skip in the `/etc/pacman.conf` file in the IgnorePkg array. For more information, please see the [pacman](/index.php/Pacman "Pacman") wiki entry.

Please note that the power user is expected to keep the system up to date with pacman -Syu, rather than selectively upgrading packages. You may diverge from this typical usage as you wish; just be warned that there is a greater chance that things will not work as intended and that it could break your system. The majority of complaints happen when selective upgrading, unusual compilation or improper software installation is performed. Use of **IgnorePkg** in `/etc/pacman.conf` is therefore discouraged, and should only be used sparingly, if you know what you are doing.

##### The Arch rolling release model

Keep in mind that Arch is a **rolling release** distribution. This means there is never a reason to reinstall or perform elaborate system rebuilds to upgrade to the newest version. Simply issuing `pacman -Syu` periodically keeps your entire system up-to-date and on the bleeding edge. At the end of this upgrade, your system is completely current. Remember to **reboot** if a kernel upgrade has occurred.

### Adding a User

**Note:** Before adding your users, consider hardening your system by switching from md5 password hashes to sha512 password hashes (see: [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes")).

Linux is a multi-user environment. You should not do your everyday work using the root account: it is more than poor practice, it is dangerous. Use root for administrative tasks only and instead add a normal user account using the `adduser` program:

 `# adduser` 

You will be asked to enter some information in an interactive way. In the following example we are creating the user *archie*:

```
Login name for new user []: **archie**

User ID ('UID') [ defaults to next available ]:

Initial group [ users ]:

Additional groups (comma separated) []: **audio,lp,optical,storage,video,wheel,games,power,scanner**

Home directory [ /home/archie ]:

Shell [ /bin/bash ]:

Expiry date (YYYY-MM-DD) []:

```

As showed in the example, you are advised to enter values only for the *Login name* and the *Additional groups*, and leave empty all the other fields.

The list of *Additional groups* in the example is a typical choice for a desktop system, hence it is recommended especially for beginners:

*   **audio** - for tasks involving sound card and related software
*   **lp** - for managing printing tasks
*   **optical** - for managing tasks pertaining to the optical drive(s)
*   **storage** - for managing storage devices
*   **video** - for video tasks and hardware acceleration
*   **wheel** - for using sudo
*   **games** - needed for write permission for games in the games group
*   **power** - used with power options (e.g. shutdown with power button)
*   **scanner** - for using a scanner

Now you will be presented with a preview of your new account, and the ability to cancel or continue operations: after pressing `ENTER` the account will be created, and you will be prompted to enter additional, optional informations for the new user (e.g. the full name). After that, you will be asked to enter the password for your account.

Your new non-root user has finally been created, complete with a home directory and a login password.

See [Users and groups](/index.php/Users_and_groups "Users and groups") for further information. If you want to change the name of your user or any existing user, consult the [Change username](/index.php/Change_username "Change username") page. You may also check the man pages for `usermod(8)` and `gpasswd(8)`.

#### Deleting the user account

In the event of error, or if you wish to delete this user account in favor of a different name or for any other reason, use `/usr/sbin/userdel`:

 `# userdel -r [username]` 

The `-r` option will remove the user's home directory and its content, along with the the user's mail spool.

## Extras

You should now have a completely functional Arch system which will act as a suitable base for you to build upon based on your needs. However, most people are interested in a desktop system, complete with sound and graphics. This part of the guide will provide a brief overview of the procedure to acquire these extras.

### Create DVD and CDROM symlinks

Many desktop applications will expect the presence of CDROM and DVD symlinks to the `/dev/sr0` device node. Four useful symlinks may be created as so:

 `# for i in cdrom cdrw dvd dvdrw; do ln -s /dev/sr0 /dev/$i; done` 

To make the symlinks persistently created after each boot, add the above command to `/etc/rc.local`.

Alternatively, you may wish to add the commands sequentially for readability:

```
#!/bin/bash
#
# /etc/rc.local: Local multi-user startup script.
#
# create optical drive symlinks
ln -s /dev/sr0 /dev/cdrom
ln -s /dev/sr0 /dev/cdrw
ln -s /dev/sr0 /dev/dvd
ln -s /dev/sr0 /dev/dvdrw

```

### Sudo

Install Sudo:

 `# pacman -S sudo` 

To add a user as a sudo user (a "sudoer"), the visudo command must be run as root.

By default, the visudo command uses the editor [vi](/index.php/Vi "Vi"). If you do not know how to use vi, you may set the EDITOR environment variable to the editor of your choice, such as in this example with the editor "nano":

```
# EDITOR=nano visudo

```

**Note:** Please note that you are setting the variable and starting visudo on the same line at the same time. This will not work properly as two separated commands.

If you are comfortable using vi, issue the visudo command without the EDITOR=nano variable:

 `# visudo` 

This will open the file `/etc/sudoers` in a special session of vi. visudo copies the file to be edited to a temporary file, edits it with an editor, (vi by default), and subsequently runs a sanity check. If it passes, the temporary file overwrites the original with the correct permissions.

**Warning:** Do not edit `/etc/sudoers` directly with an editor; errors in syntax can cause annoyances (like rendering the root account unusable). You **must** use the *visudo* command to edit `/etc/sudoers`.

In the previous section we added your user to the "wheel" group. To give users in the wheel group full root privileges when they precede a command with "sudo", uncomment the following line:

```
%wheel	ALL=(ALL) ALL

```

Now you can give any user access to the sudo command by simply adding them to the wheel group.

For more information, such as sudoer <TAB> completion, see [Sudo](/index.php/Sudo "Sudo").

### Sound

If you want sound, proceed to [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") for instructions. Alternatively, proceed to the [next section](#Graphical_User_Interface) first, and set up sound later.

**Note:** ALSA usually works out-of-the-box, it just needs to be unmuted.

The [Advanced Linux Sound Architecture](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture") (ALSA) is included with the kernel and it is recommended to try it first. However, if it does not work or you are not satisfied with the quality, the [Open Sound System](https://en.wikipedia.org/wiki/Open_Sound_System "wikipedia:Open Sound System") is a viable alternative. OSSv4 has been released under a free license and is generally considered a significant improvement over the older OSSv3 which was replaced by ALSA. Instructions can be found in the [OSS article](/index.php/OSS "OSS").

If you have advanced audio requirements, take a look at [Sound](/index.php/Sound "Sound") for an overview of various articles.

### **G**raphical **U**ser **I**nterface

#### Install X

The [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (commonly **X11**, or **X**) is a networking and display protocol which provides windowing on bitmap displays. It provides the standard toolkit and protocol to build graphical user interfaces (GUIs).

**Note:** If you are installing Arch as a Virtualbox guest, you need a different way to complete X installation. See [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest"), then jump to the configuration part below.

Now we will install the base **[Xorg](/index.php/Xorg "Xorg")** packages using pacman.

Install the base packages:

 `# pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils` 

Install [mesa](https://en.wikipedia.org/wiki/Mesa_3D_(OpenGL) for 3D support:

 `# pacman -S mesa` 

The 3D utilities glxgears and [glxinfo](http://dri.freedesktop.org/wiki/glxinfo) are included in the **mesa-demos** package. Install if needed:

 `# pacman -S mesa-demos` 

#### Install video driver

Next, you should install a driver for your graphics card.

You will need knowledge of which video chipset your machine has. If you do not know, use the `/usr/sbin/lspci` program:

 `$ lspci` 
**Note:** The **vesa** driver is the most generic, and should work with almost any modern video chipset. If you cannot find a suitable driver for your video chipset, vesa *should* work with any video card, but it offers only unaccelerated 2D performance.

For a complete list of all **open-source** video drivers, search the package database:

```
$ pacman -Ss xf86-video | less

```

**Note:** Proprietary drivers for NVIDIA and ATI are covered in the next sections. If you plan on doing heavy 3D processing such as gaming, consider using these.

Use pacman to install the appropriate video driver for your video card/onboard video. Example for the Savage driver:

 `# pacman -S xf86-video-savage` 
**Tip:** For some Intel graphics cards, configuration may be necessary to get proper 2D or 3D performance, see [Intel](/index.php/Intel "Intel") for more information.

##### NVIDIA Graphics Cards

NVIDIA users have three options for drivers (in addition to the vesa driver):

*   The open-source nouveau driver, which offers fast 2d acceleration and experimental 3d support which is good enough for basic compositing (note: does not fully support powersaving yet). [Feature Matrix.](http://nouveau.freedesktop.org/wiki/FeatureMatrix)
*   The open-source (but obfuscated) nv driver, which is very slow and only has 2d support.
*   The proprietary nvidia drivers, which offer good 3d performance and powersaving. Even if you plan on using the proprietary drivers, it is recommended to start with nouveau and then switch to the binary driver after you have X set up and working. Nouveau often works out-of-the-box, while nvidia will require configuration and likely some troubleshooting. See [NVIDIA](/index.php/NVIDIA "NVIDIA") for more information.

The open-source nouveau driver should be good enough for most users and is recommended:

 `# pacman -S xf86-video-nouveau` 

For experimental 3D support:

 `# pacman -S nouveau-dri` 
**Tip:** For advanced instructions, see [Nouveau](/index.php/Nouveau "Nouveau").

##### ATI Graphics Cards

ATI owners have two options for drivers (in addition to the vesa driver):

*   The open source **radeon** driver provided by the **xf86-video-ati** package. See the [radeon feature matrix](http://wiki.x.org/wiki/RadeonFeature) for details.
*   The proprietary **fglrx** driver provided by the [catalyst](https://aur.archlinux.org/packages.php?O=0&K=catalyst&do_Search=Go) package located in the [AUR](/index.php/AUR "AUR"). It supports only newer devices (HD2xxx and newer). It was once a package offered by Arch in the **extra** repository, but as of March 2009, official support has been dropped because of dissatisfaction with the quality and speed of development of the proprietary driver. See [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") for more information.

The open-source driver is the recommended choice. Install the **radeon** ATI Driver:

 `# pacman -S xf86-video-ati` 
**Tip:** For advanced instructions, see [ATI](/index.php/ATI "ATI").

#### Install input drivers

Udev should be capable of detecting your hardware without problems and evdev (**xf86-input-evdev**) is the modern, hotplugging input driver for almost all devices so in most cases, installing input drivers is not needed. At this point, evdev has already been installed as a dependency of Xorg.

If evdev does not support your device, install the needed driver from the xorg-input-drivers group.

For a complete list of available input drivers, invoke a pacman search:

```
# pacman -Ss xf86-input | less

```

**Note:** You only need xf86-input-keyboard or xf86-input-mouse if you plan on disabling hotplugging, otherwise, evdev will act as the input driver.

Laptop users (or users with a touchscreen) will also need the synaptics package to allow X to configure the touchpad/touchscreen:

 `# pacman -S xf86-input-synaptics` 
**Tip:** For instructions on fine tuning or troubleshooting touchpad settings, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") article.

#### Configure X (Optional)

**Warning:** Proprietary drivers usually require a reboot after installation along with configuration. See [NVIDIA](/index.php/NVIDIA "NVIDIA") or [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") for details.

X Server features auto-configuration and therefore can function without an `xorg.conf`. If you still wish to manually configure X Server, please see the [Xorg](/index.php/Xorg "Xorg") wiki page.

##### Non-US keyboard

If you do not use a standard US keyboard, you need to set the keyboard layout in `/etc/X11/xorg.conf.d/10-evdev.conf`:

```
Section "InputClass"
    Identifier "evdev keyboard catchall"
    MatchIsKeyboard "on"
    MatchDevicePath "/dev/input/event*"
    Driver "evdev"
    **Option "XkbLayout" "be"**
EndSection

```

If, for example, you wish to use a variant of the US keyboard, add the following into the same section from the previous example:

```
Option "XkbLayout" "us"
Option "XkbVariant" "dvorak"

```

**Note:** The **XkbLayout** key may differ from the keymap code you used with the km or loadkeys command. A list of many keyboard layouts and variants can be found in `/usr/share/X11/xkb/rules/base.lst` (see text after line beginning with `! layout`). For instance the layout: **gb** corresponds to "English (UK)".

#### Testing X

This section will explain how to start a very basic graphical environment in order to test **X**. This uses the simple default **X** window manager, twm.

Install the default test environment:

 `# pacman -S xorg-twm xorg-xclock xterm` 

The default X environment is rather bare. [This section below](#Choose_and_install_a_graphical_interface) will deal with installing a desktop environment or window manager of your choice to supplement X.

If you installed Xorg before creating your regular user, there will be an empty `.xinitrc` file in your $HOME that you need to either delete or edit in order to start a graphical environment. Simply deleting it will cause **X** to run with the default environment (twm, xclock, xterm).

 `$ rm ~/.xinitrc` 

##### Message bus

**Note:** [dbus](/index.php/Dbus "Dbus") is likely required for many of your applications to work properly, if you know you do not need it, skip this section.

Install [dbus](/index.php/Dbus "Dbus"):

 `# pacman -S dbus` 

Start the dbus daemon:

 `# rc.d start dbus` 

Add dbus to your DAEMONS array so it starts automatically on boot:

 `/etc/rc.conf`  `DAEMONS=(... **dbus** ...)` 

##### Start X

**Note:** The Ctrl-Alt-Backspace shortcut traditionally used to kill X has been deprecated and will not work to exit out of this test. You can enable Ctrl-Alt-Backspace by editing `xorg.conf`, as described [here](/index.php/Xorg#Ctrl-Alt-Backspace_doesn.27t_work "Xorg").

Finally, start Xorg:

 `$ startx` 

or:

 `$ xinit -- /usr/bin/X -nolisten tcp` 

A few movable windows should show up, and your mouse should work. Once you are satisfied that **X** installation was a success, you may exit out of **X** by issuing the `exit` command into the prompts until you return to the console.

If the screen goes black, you may still attempt to switch to a different virtual console (CTRL-Alt-F2, for example), and login blindly as root, followed by <Enter>, followed by root's password followed by <Enter>.

You can attempt to kill the **X** server with `/usr/bin/pkill` (note the capital letter **X**):

 `# pkill X` 

If **pkill** does not work, reboot blindly with:

 `# reboot` 

##### In case of errors

If a problem occurs, look for errors in `/var/log/Xorg.0.log`. Be on the lookout for any lines beginning with `(EE)` which represent errors, and also `(WW)` which are warnings that could indicate other issues.

 `$ grep EE /var/log/Xorg.0.log` 

Errors may also be searched for in the console output of the virtual console from which **X** was started.

See the [Xorg](/index.php/Xorg "Xorg") article for detailed instructions and troubleshooting.

##### Need Help?

If you are still having trouble after consulting the [Xorg](/index.php/Xorg "Xorg") article and need assistance via the Arch forums, be sure to install and use **wgetpaste**:

 `# pacman -S wgetpaste` 

Use **wgetpaste** and provide links for the following files when asking for help in your forum post:

*   ~/.xinitrc
*   /etc/X11/xorg.conf
*   /var/log/Xorg.0.log
*   /var/log/Xorg.0.log.old

Use it like so:

 `$ wgetpaste </path/to/file>` 

Post the corresponding links given within your forum post. Be sure to provide appropriate hardware and driver information as well.

**Note:** It is very important to provide detail when troubleshooting X. Please provide all pertinent information as detailed above when asking for assistance on the Arch forums.

#### Install Fonts

At this point, you may wish to save time by installing visually pleasing, true type fonts, before installing a desktop environment/window manager. DejaVu is a set of high quality, general-purpose fonts.

Install with:

 `# pacman -S ttf-dejavu` 

*   Refer to [Font configuration](/index.php/Font_configuration "Font configuration") for how to configure font rendering and [Fonts](/index.php/Fonts "Fonts") for font suggestions and installation instructions.
*   Steps to install Microsoft fonts are detailed in the [MS Fonts](/index.php/MS_Fonts "MS Fonts") article.

#### Choose and install a graphical interface

The X Window System provides the basic framework for building a graphical user interface (GUI).

**Note:** Choosing your DE or WM is a very subjective and personal decision. Choose the best environment for *your* needs.

	Window Manager (WM) 

	Controls the placement and appearance of application windows in conjunction with the X Window System. **See [Window managers](/index.php/Window_manager#Window_managers "Window manager") for more information.**

	Desktop Environment (DE)

	Works atop and in conjunction with X, to provide a completely functional and dynamic GUI. A DE typically provides a window manager, icons, applets, windows, toolbars, folders, wallpapers, a suite of applications and abilities like drag and drop. **See [Desktop environments](/index.php/Desktop_environment#Desktop_environments "Desktop environment") for more information.**

**Note:** You can build your own DE by using a WM and the applications of your choice.

After installing a graphical interface, you may wish to continue with [General recommendations](/index.php/General_recommendations "General recommendations") for post-installation instructions.

#### Methods for starting your Graphical Environment

##### Manually

You might prefer to start X manually from your terminal rather than booting straight into the desktop. For DE-specific commands, please see the wiki page corrosponding to your DE for more information. For more generic **X** commands, please see the [section on the Xorg page](/index.php/Xorg#Methods_for_starting_your_Graphical_Environment "Xorg").

##### Automatically

You might prefer to have the desktop start automatically during boot instead of starting X manually. See [Display manager](/index.php/Display_manager "Display manager") for instructions on using a login manager or [Start X at Boot](/index.php/Start_X_at_Boot "Start X at Boot") for two lightweight methods that do not rely on a display manager.

**[Vodič za početnike](/index.php/Beginners%27_Guide_(Hrvatski) "Beginners' Guide (Hrvatski)")**

* * *

[Predgovor](/index.php/Beginners%27_Guide/Preface_(Hrvatski) "Beginners' Guide/Preface (Hrvatski)") >> [Priprema](/index.php/Beginners%27_Guide/Preparation_(Hrvatski) "Beginners' Guide/Preparation (Hrvatski)") >> [Instalacija](/index.php/Beginners%27_Guide/Installation_(Hrvatski) "Beginners' Guide/Installation (Hrvatski)") >> **Nakon instalacije** >> [Bilješke](/index.php/Beginners%27_Guide/Extra_(Hrvatski) "Beginners' Guide/Extra (Hrvatski)")