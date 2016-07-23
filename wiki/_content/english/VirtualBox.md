[VirtualBox](https://www.virtualbox.org) is a [hypervisor](https://en.wikipedia.org/wiki/Hypervisor "wikipedia:Hypervisor") used to run operating systems in a special environment, called a virtual machine, on top of the existing operating system. VirtualBox is in constant development and new features are implemented continuously. It comes with a [Qt](/index.php/Qt "Qt") GUI interface, as well as headless and [SDL](https://en.wikipedia.org/wiki/Simple_DirectMedia_Layer "wikipedia:Simple DirectMedia Layer") command-line tools for managing and running virtual machines.

In order to integrate functions of the host system to the guests, including shared folders and clipboard, video acceleration and a seamless window integration mode, *guest additions* are provided for some guest operating systems.

## Contents

*   [1 Installation steps for Arch Linux hosts](#Installation_steps_for_Arch_Linux_hosts)
    *   [1.1 Install the core packages](#Install_the_core_packages)
    *   [1.2 Sign modules](#Sign_modules)
    *   [1.3 Load the VirtualBox kernel modules](#Load_the_VirtualBox_kernel_modules)
    *   [1.4 Accessing host USB devices in guest](#Accessing_host_USB_devices_in_guest)
    *   [1.5 Guest additions disc](#Guest_additions_disc)
    *   [1.6 Extension pack](#Extension_pack)
    *   [1.7 Use the right front-end](#Use_the_right_front-end)
*   [2 Installation steps for Arch Linux guests](#Installation_steps_for_Arch_Linux_guests)
    *   [2.1 Installation in EFI mode](#Installation_in_EFI_mode)
    *   [2.2 Install the Guest Additions](#Install_the_Guest_Additions)
    *   [2.3 Set optimal framebuffer resolution](#Set_optimal_framebuffer_resolution)
    *   [2.4 Load the Virtualbox kernel modules](#Load_the_Virtualbox_kernel_modules_2)
    *   [2.5 Launch the VirtualBox guest services](#Launch_the_VirtualBox_guest_services)
    *   [2.6 Hardware acceleration](#Hardware_acceleration)
    *   [2.7 Enable shared folders](#Enable_shared_folders)
        *   [2.7.1 Manual mounting](#Manual_mounting)
        *   [2.7.2 Automounting](#Automounting)
        *   [2.7.3 Mount at boot](#Mount_at_boot)
*   [3 Virtual disks management](#Virtual_disks_management)
    *   [3.1 Formats supported by VirtualBox](#Formats_supported_by_VirtualBox)
    *   [3.2 Disk image format conversion](#Disk_image_format_conversion)
        *   [3.2.1 VMDK to VDI and VDI to VMDK](#VMDK_to_VDI_and_VDI_to_VMDK)
        *   [3.2.2 VHD to VDI and VDI to VHD](#VHD_to_VDI_and_VDI_to_VHD)
        *   [3.2.3 QCOW2 to VDI and VDI to QCOW2](#QCOW2_to_VDI_and_VDI_to_QCOW2)
    *   [3.3 Mount virtual disks](#Mount_virtual_disks)
        *   [3.3.1 VDI](#VDI)
    *   [3.4 Compact virtual disks](#Compact_virtual_disks)
    *   [3.5 Increase virtual disks](#Increase_virtual_disks)
        *   [3.5.1 General procedure](#General_procedure)
        *   [3.5.2 Increase size for VDI disks](#Increase_size_for_VDI_disks)
    *   [3.6 Replace a virtual disk manually from the .vbox file](#Replace_a_virtual_disk_manually_from_the_.vbox_file)
        *   [3.6.1 Transfer between Linux host and other OS](#Transfer_between_Linux_host_and_other_OS)
    *   [3.7 Clone a virtual disk and assigning a new UUID to it](#Clone_a_virtual_disk_and_assigning_a_new_UUID_to_it)
*   [4 Tips and tricks](#Tips_and_tricks)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 VERR_ACCESS_DENIED](#VERR_ACCESS_DENIED)
    *   [5.2 pacstrap script fails](#pacstrap_script_fails)
    *   [5.3 Keyboard and mouse are blocked in my virtual machine](#Keyboard_and_mouse_are_blocked_in_my_virtual_machine)
    *   [5.4 Cannot send CTRL+ALT+Fn key to my virtual machine](#Cannot_send_CTRL.2BALT.2BFn_key_to_my_virtual_machine)
    *   [5.5 Fix ISO images problems](#Fix_ISO_images_problems)
    *   [5.6 VirtualBox GUI does not match my GTK Theme](#VirtualBox_GUI_does_not_match_my_GTK_Theme)
    *   [5.7 OpenBSD unusable when virtualisation instructions unavailable](#OpenBSD_unusable_when_virtualisation_instructions_unavailable)
    *   [5.8 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [5.9 USB subsystem is not working on the host or guest](#USB_subsystem_is_not_working_on_the_host_or_guest)
    *   [5.10 Failed to create the host-only network interface](#Failed_to_create_the_host-only_network_interface)
    *   [5.11 WinXP: Bit-depth cannot be greater than 16](#WinXP:_Bit-depth_cannot_be_greater_than_16)
    *   [5.12 Use serial port in guest OS](#Use_serial_port_in_guest_OS)
    *   [5.13 Windows 8.x Error Code 0x000000C4](#Windows_8.x_Error_Code_0x000000C4)
    *   [5.14 Windows 8, 8.1 or 10 fails to install, boot or has error "ERR_DISK_FULL"](#Windows_8.2C_8.1_or_10_fails_to_install.2C_boot_or_has_error_.22ERR_DISK_FULL.22)
    *   [5.15 Linux guests have slow/distorted audio](#Linux_guests_have_slow.2Fdistorted_audio)
    *   [5.16 Guest freezes after starting Xorg](#Guest_freezes_after_starting_Xorg)
    *   [5.17 "NS_ERROR_FAILURE" and missing menu items](#.22NS_ERROR_FAILURE.22_and_missing_menu_items)
    *   [5.18 USB modem](#USB_modem)
    *   [5.19 "The specified path does not exist. Check the path and then try again." error in Windows guests](#.22The_specified_path_does_not_exist._Check_the_path_and_then_try_again..22_error_in_Windows_guests)
    *   [5.20 No 64-bit OS client options](#No_64-bit_OS_client_options)
    *   [5.21 Host OS freezes on Virtual Machine start](#Host_OS_freezes_on_Virtual_Machine_start)
    *   [5.22 The virtual machine has terminated unexpectedly during startup with exit code 1 (0x1)](#The_virtual_machine_has_terminated_unexpectedly_during_startup_with_exit_code_1_.280x1.29)
    *   [5.23 Analog microphone not working in guest](#Analog_microphone_not_working_in_guest)
    *   [5.24 Fullscreen mode shows blank guest screen](#Fullscreen_mode_shows_blank_guest_screen)
    *   [5.25 Failed to insert module](#Failed_to_insert_module)
*   [6 See also](#See_also)

## Installation steps for Arch Linux hosts

In order to launch VirtualBox virtual machines on your Arch Linux box, follow these installation steps.

### Install the core packages

[Install](/index.php/Install "Install") the [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) package. You will need to choose a package to provide host modules:

*   for [linux](https://www.archlinux.org/packages/?name=linux) kernel choose [virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch)
*   for other kernels choose [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms)

To compile the virtualbox modules provided by [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms), it will also be necessary to install the appropriate headers package(s) for your installed kernel(s) (e.g. [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) for [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)). [[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) When either VirtualBox or the kernel is updated, the kernel modules will be automatically recompiled thanks to the [DKMS](/index.php/DKMS "DKMS") Pacman hook.

You can also install the [qt5-x11extras](https://www.archlinux.org/packages/?name=qt5-x11extras) optional dependency in order to use the graphical interface which is based on [Qt](/index.php/Qt "Qt"). This is not required if you intend to use VirtualBox in command-line only. [See below to learn the differences](#Use_the_right_front-end).

### Sign modules

When using a custom kernel with `CONFIG_MODULE_SIG_FORCE` option enabled, you must sign your modules with a key generated during kernel compilation.

Navigate to your kernel tree folder and execute the following command:

```
# for module in `ls /lib/modules/$(uname -r)/kernel/misc/{vboxdrv.ko,vboxnetadp.ko,vboxnetflt.ko,vboxpci.ko}` ; do ./scripts/sign-file sha1 certs/signing_key.pem certs/signing_key.x509 $module ; done

```

**Note:** Hashing algorithm does not have to match the one configured, but it must be built into the kernel.

### Load the VirtualBox kernel modules

Since version 5.0.16, [virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch) and [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) use `systemd-modules-load.service` to load all four VirtualBox modules at boot time.

**Note:** If you don't want the VirtualBox modules to be loaded at boot time, you have to mask the default `/usr/lib/modules-load.d/virtualbox-host-modules-arch.conf` (or `-dkms.conf`) by creating an empty file (or symlink to `/dev/null`) with the same name in `/etc/modules-load.d`.

Among the [kernel modules](/index.php/Kernel_modules "Kernel modules") VirtualBox uses, there is a mandatory module named `vboxdrv`, which must be loaded before any virtual machines can run.

To load the module manually, run:

```
# modprobe vboxdrv

```

The following modules are optional but are recommended if you do not want to be bothered in some advanced configurations (precised here after): `vboxnetadp`, `vboxnetflt` and `vboxpci`.

*   `vboxnetadp` and `vboxnetflt` are both needed when you intend to use the [bridged](https://www.virtualbox.org/manual/ch06.html#network_bridged) or [host-only networking](https://www.virtualbox.org/manual/ch06.html#network_hostonly) feature. More precisely, `vboxnetadp` is needed to create the host interface in the VirtualBox global preferences, and `vboxnetflt` is needed to launch a virtual machine using that network interface.

*   `vboxpci` is needed when your virtual machine needs to pass through a PCI device on your host.

**Note:** If the VirtualBox kernel modules were loaded in the kernel while you updated the modules, you need to reload them manually to use the new updated version. To do it, run `vboxreload` as root.

Finally, if you use the aforementioned "Host-only" or "bridge networking" feature, make sure [net-tools](https://www.archlinux.org/packages/?name=net-tools) is installed. VirtualBox actually uses `ifconfig` and `route` to assign the IP and route to the host interface configured with `VBoxManage hostonlyif` or via the GUI in *Settings > Network > Host-only Networks > Edit host-only network (space) > Adapter*.

### Accessing host USB devices in guest

To use the USB ports of your host machine in your virtual machines, add users that will be authorized to use this feature to the `vboxusers` [group](/index.php/Group "Group").

### Guest additions disc

It is also recommended to install the [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) package on the host running VirtualBox. This package will act as a disc image that can be used to install the guest additions onto guest systems other than Arch Linux. The *.iso* file will be located at `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso`, and may have to be mounted manually inside the virtual machine. Once mounted, you can run the guest additions installer inside the guest.

### Extension pack

The Oracle Extension Pack which provides [additional features](https://www.virtualbox.org/manual/ch01.html#intro-installing), is released under a non-free license and **only available for personal use**. To install it, the [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) package is available, and a prebuilt version can be found in the [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories") repository.

If you prefer to use the traditional and manual way: download the extension manually and install it via the GUI (*File > Preferences > Extensions*) or via `VBoxManage extpack install <.vbox-extpack>`, make sure you have a toolkit (like [Polkit](/index.php/Polkit "Polkit"), gksu, etc.) to grant privileged access to VirtualBox. The installation of this extension [requires root access](https://www.virtualbox.org/ticket/8473).

### Use the right front-end

Now, you are ready to use VirtualBox. Congratulations!

Multiple front-ends are available to you of which two are available by default:

*   If you want to use VirtualBox in command-line only (only launch and change settings of existing virtual machines), you can use the `VBoxSDL` command. VBoxSDL does only provide a simple window that contains only the *pure* virtual machine, without menus or other controls.
*   If you want to use VirtualBox in command-line without any GUI running (e.g. on a server) to create, launch and configure virtual machines, use the `VBoxHeadless` which produces no visible output on the host at all, but instead only delivers VRDP data (note: VRDP is only enabled if the extension pack is installed).

If you installed the [qt5-x11extras](https://www.archlinux.org/packages/?name=qt5-x11extras) optional dependency, you can run `VirtualBox` and have a nice-looking GUI interface with menus usable via the mouse.

Finally, you can use [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox") to administrate your virtual machines via a web interface.

Refer to the [VirtualBox manual](https://www.virtualbox.org/manual) to learn how to create virtual machines.

**Warning:** If you intend to store virtual disk images on a [Btrfs](/index.php/Btrfs "Btrfs") file system, before creating any images, you should consider disabling [Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs") for the destination directory of these images.

## Installation steps for Arch Linux guests

Boot the Arch installation media through one of the virtual machine's virtual drives. Then, complete the installation of a basic Arch system as explained in the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") or the [Installation guide](/index.php/Installation_guide "Installation guide").

#### Installation in EFI mode

If you want to install Arch Linux in EFI mode inside VirtualBox, in the settings of the virtual machine, choose *System* item from the panel on the left and *Motherboard* tab from the right panel, and check the checkbox *Enable EFI (special OSes only)*. After selecting the kernel from the Arch Linux installation media's menu, the media will hang for a minute or two and will continue to boot the kernel normally afterwards. Be patient.

Once the system and the boot loader are installed, VirtualBox will first attempt to run `/EFI/BOOT/BOOTX64.EFI` from the [ESP](/index.php/ESP "ESP"). If that first option fails, VirtualBox will then try the EFI shell script `startup.nsh` from the root of the ESP. This means that in order to boot the system you have the following options:

*   [Launch the bootloader manually](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") from the EFI shell every time;
*   Move the bootloader to the default `/EFI/BOOT/BOOTX64.EFI` path;
*   Create the `startup.nsh` script at the ESP root containing the path to the boot loader application, e.g. `\EFI\grub\grubx64.efi`.

Do not bother with the VirtualBox Boot Manager (accessible with `F2` at boot): EFI entries added to it manually at boot or with [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) will persist after a reboot [but are lost when the VM is shut down](https://www.virtualbox.org/ticket/11177).

See also [UEFI Virtualbox installation boot problems](https://bbs.archlinux.org/viewtopic.php?id=158003).

### Install the Guest Additions

VirtualBox [Guest Additions](https://www.virtualbox.org/manual/ch04.html) provides drivers and applications that optimize the guest operating system including improved image resolution and better control of the mouse. Within the installed guest system, install:

*   [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) for VirtualBox Guest utilities with X support
*   [virtualbox-guest-utils-nox](https://www.archlinux.org/packages/?name=virtualbox-guest-utils-nox) for VirtualBox Guest utilities without X support

Both packages will make you choose a package to provide guest modules:

*   for [linux](https://www.archlinux.org/packages/?name=linux) kernel choose [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch)
*   for other kernels choose [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms)

To compile the virtualbox modules provided by [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms), it will also be necessary to install the appropriate headers package(s) for your installed kernel(s) (e.g. [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) for [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)). [[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) When either VirtualBox or the kernel is updated, the kernel modules will be automatically recompiled thanks to the [DKMS](/index.php/DKMS "DKMS") Pacman hook.

**Note:**

*   You can alternatively install the Guest Additions with the ISO from the [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) package, provided you installed this on the host system. To do this, go to the device menu click Insert Guest Additions CD Image.
*   To recompile the vbox kernel modules, run `rcvboxdrv` as root.

The guest additions running on your guest, and the VirtualBox application running on your host must have matching versions, otherwise the guest additions (like shared clipboard) may stop working. If you upgrade your guest (e.g. `pacman -Syu`), make sure your VirtualBox application on this host is also the latest version. "Check for updates" in the VirtualBox GUI is sometimes not sufficient; check the virtualbox.org website.

### Set optimal framebuffer resolution

Typically after installing Guest Additions, a fullscreen Arch guest running X will be set to the optimal resolution for your display; however, the virtual console's framebuffer will be set to a standard, often smaller, resolution detected from VirtualBox's custom VESA driver.

To use the virtual consoles at optimal resolution, Arch needs to recognize that resolution as valid, which in turn requires VirtualBox to pass this information along to the guest OS.

First, check if your desired resolution is not already recognized by running the command:

```
hwinfo --framebuffer

```

If the optimal resolution does not show up, then you will need to run the `VBoxManage` tool on the host machine and add "extra resolutions" to your virtual machine (on a Windows host, go to the VirtualBox installation directory to find `VBoxManage.exe`). For example:

```
VBoxManage setextradata "Arch Linux" "CustomVideoMode1" "1360x768x24"

```

The parameters "Arch Linux" and "1360x768x24" in the example above should be replaced with your VM name and the desired framebuffer resolution. Incidentally, this command allows for defining up to 16 extra resolutions ("CustomVideoMode1" through "CustomVideoMode16").

Afterwards, restart the virtual machine and run `hwinfo --framebuffer` once more to verify that the new resolutions have been recognized by your guest system (which does not guarantee they will all work, depending on your hardware limitations).

Finally, add a `video=*resolution*` kernel parameter ([https://wiki.archlinux.org/index.php/Kernel_parameters](https://wiki.archlinux.org/index.php/Kernel_parameters)) to set the framebuffer to the new resolution, for example `video=1360x768`.

If you use GRUB as your bootloader, you can edit `/etc/default/grub` to include this kernel parameter in the `GRUB_CMDLINE_LINUX_DEFAULT` list, like so:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet video=1360x768"

```

The GRUB menu itself may also be easily set to optimal resolution, by editing the `GRUB_GFXMODE` option on the same configuration file:

```
GRUB_GFXMODE="1360x768x24"

```

On a standard Arch setup, you would then run `grub-mkconfig -o /boot/grub/grub.cfg` to commit these changes to the bootloader.

After these steps, the framebuffer resolution should be optimized for the GRUB menu and all virtual consoles.

**Note:** The GRUB settings `GRUB_GFXPAYLOAD_LINUX` and `vga` will not fix the framebuffer, since they are overriden by virtue of Kernel Mode Setting, which is mandatory for using X under VirtualBox and only allows for setting the framebuffer resolution by setting the kernel parameter described above.

### Load the Virtualbox kernel modules

To load the modules automatically, [enable](/index.php/Enable "Enable") the `vboxservice` service which loads the modules and synchronizes the guest's system time with the host.

To load the modules manually, type:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

Since version 5.0.16, [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch) and [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) use **systemd-modules-load** service to load their modules at boot time.

**Note:** If you don't want the VirtualBox modules to be loaded at boot time, you have to mask the default `/usr/lib/modules-load.d/virtualbox-guest-modules-arch.conf` (or `-dkms.conf`) by creating an empty file (or symlink to `/dev/null`) with the same name in `/etc/modules-load.d`.

### Launch the VirtualBox guest services

After the rather big installation step dealing with VirtualBox kernel modules, now you need to start the guest services. The guest services are actually just a binary executable called `VBoxClient` which will interact with your X Window System. `VBoxClient` manages the following features:

*   shared clipboard and drag and drop between the host and the guest;
*   seamless window mode;
*   the guest display is automatically resized according to the size of the guest window;
*   checking the VirtualBox host version

All of these features can be enabled independently with their dedicated flags:

```
$ VBoxClient --clipboard --draganddrop --seamless --display --checkhostversion

```

As a shortcut, the `VBoxClient-all` bash script enables all of these features.

[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) installs `/etc/xdg/autostart/vboxclient.desktop` that launches `VBoxClient-all` on logon. If your [desktop environment](/index.php/Desktop_environment "Desktop environment") or [window manager](/index.php/Window_manager "Window manager") does not support this scheme, you will need to set up autostarting yourself, see [Autostarting#Graphical](/index.php/Autostarting#Graphical "Autostarting") for more details.

VirtualBox can also synchronize the time between the host and the guest, to do this, [start/enable](/index.php/Start/enable "Start/enable") the `vboxservice.service`.

Now, you should have a working Arch Linux guest. Note that features like clipboard sharing are disabled by default in VirtualBox, and you will need to turn them on in the per-VM settings if you actually want to use them (e.g. *Settings > General > Advanced > Shared Clipboard*).

### Hardware acceleration

Hardware acceleration can be activated from the VirtualBox options on the host computer. Note the [GDM](/index.php/GDM "GDM") display manager 3.16+ is known to [break](https://bugzilla.gnome.org/show_bug.cgi?id=749390) hardware acceleration support. So if you get issues with hardware acceleration, try out another display manager (lightdm seems to work fine).[[3]](https://bbs.archlinux.org/viewtopic.php?id=200025) [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1607593#p1607593)

If you want to share folders between your host and your Arch Linux guest, read on.

### Enable shared folders

Shared folders are managed on the host, in the settings of the Virtual Machine accessible via the GUI of VirtualBox, in the *Shared Folders* tab. There, *Folder Path*, the name of the mount point identified by *Folder name*, and options like *Read-only*, *Auto-mount* and *Make permanent* can be specified. These parameters can be defined with the `VBoxManage` command line utility. See [there for more details](https://www.virtualbox.org/manual/ch04.html#sharedfolders).

No matter which method you will use to mount your folder, all methods require some steps first.

To avoid this issue `/sbin/mount.vboxsf: mounting failed with the error: No such device`, make sure the `vboxsf` kernel module is properly loaded. It should be, since we enabled all guest kernel modules previously.

Two additional steps are needed in order for the mount point to be accessible from users other than root:

*   the [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) package created a group `vboxsf` (done in a previous step);
*   your username must be in `vboxsf` [group](/index.php/Group "Group").

#### Manual mounting

Use the following command to mount your folder in your Arch Linux guest:

```
# mount -t vboxsf *shared_folder_name* *mount_point_on_guest_system*

```

The vboxsf filesystem offers other options which can be displayed with this command:

```
# mount.vboxsf

```

For example if the user was not in the *vboxsf* group, we could have used this command to give access our mountpoint to him:

```
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt/

```

Where *uid* and *gid* are values corresponding to the users we want to give access to. These values are obtained from the `id` command run against this user.

#### Automounting

In order for the automounting feature to work you must have checked the auto-mount checkbox in the GUI or used the optional `--automount` argument with the command `VBoxManage sharedfolder`.

The shared folder should now appear in `/media/sf_*shared_folder_name*`. If users in `media` cannot access the shared folders, check that `media` has permissions 755 or has group ownership `vboxsf` if using permission 750\. This is currently not the default if media is created by installing the `virtualbox-guest-utils`.

You can use symlinks if you want to have a more convenient access and avoid to browse in that directory, e.g.:

```
$ ln -s /media/sf_*shared_folder_name* ~/*my_documents*

```

#### Mount at boot

You can mount your directory with [fstab](/index.php/Fstab "Fstab"). However, to prevent startup problems with systemd, `comment=systemd.automount` should be added to `/etc/fstab`. This way, the shared folders are mounted only when those mount points are accessed and not during startup. This can avoid some problems, especially if the guest additions are not loaded yet when systemd read fstab and mount the partitions.

```
*sharedFolderName*  */path/to/mntPtOnGuestMachine*  vboxsf  uid=*user*,gid=*group*,rw,dmode=700,fmode=600,comment=systemd.automount  0  0

```

*   `*sharedFolderName*`: the value from the VirtualMachine's *Settings > SharedFolders > Edit > FolderName* menu. This value can be different from the name of the real folder name on the host machine. To see the VirtualMachine's *Settings* go to the host OS VirtualBox application, select the corresponding virtual machine and click on *Settings*.
*   `*/path/to/mntPtOnGuestMachine*`: if not existing, this directory should be created manually (for example by using [mkdir](/index.php/Core_utilities#mkdir "Core utilities"))
*   `dmode`/`fmode` are directory/file permissions for directories/files inside `*/path/to/mntPtOnGuestMachine*`.}}

As of 2012-08-02, mount.vboxsf does not support the *nofail* option:

```
*desktop*  */media/desktop*  vboxsf  uid=*user*,gid=*group*,rw,dmode=700,fmode=600,nofail  0  0

```

## Virtual disks management

See also [VirtualBox/Tips and tricks#Import/export VirtualBox virtual machines from/to other hypervisors](/index.php/VirtualBox/Tips_and_tricks#Import.2Fexport_VirtualBox_virtual_machines_from.2Fto_other_hypervisors "VirtualBox/Tips and tricks").

### Formats supported by VirtualBox

VirtualBox supports the following virtual disk formats:

*   VDI: The Virtual Disk Image is the VirtualBox own open container used by default when you create a virtual machine with VirtualBox.

*   VMDK: The Virtual Machine Disk has been initially developed by VMware for their products. The specification was initially closed source, but it became now an open format which is fully supported by VirtualBox. This format offers the ability to be split into several 2GB files. This feature is specially useful if you want to store the virtual machine on machines which do not support very large files. Other formats, excluding the HDD format from Parallels, do not provide such an equivalent feature.

*   VHD: The Virtual Hard Disk is the format used by Microsoft in Windows Virtual PC and Hyper-V. If you intend to use any of these Microsoft products, you will have to choose this format.

**Tip:** Since Windows 7, this format can be mounted directly without any additional application.

*   VHDX (read only): This is the eXtended version of the Virtual Hard Disk format developed by Microsoft, which has been released on 2012-09-04 with Hyper-V 3.0 coming with Windows Server 2012\. This new version of the disk format does offer enhanced performance (better block alignment), larger blocks size, and journal support which brings power failure resiliency. VirtualBox [should support this format in read only](https://www.virtualbox.org/manual/ch15.html#idp63002176).

*   Version 2 of the HDD: The HDD format is developed by Parallels Inc and used in their hypervisor solutions like Parallels Desktop for Mac. Newer versions of this format (i.e. 3 and 4) are not supported due to the lack of documentation for this proprietary format.
    **Note:** There is currently a controversy regarding the support of the version 2 of the format. While the official VirtualBox manual [only reports the second version of the HDD file format as supported](https://www.virtualbox.org/manual/ch05.html#vdidetails), Wikipedia's contributors are [reporting the first version may work too](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines"). Help is welcome if you can perform some tests with the first version of the HDD format.

*   QED: The QEMU Enhanced Disk format is an old file format for QEMU, another free and open source hypervisor. This format was designed from 2010 in a way to provide a superior alternative to QCOW2 and others. This format features a fully asynchronous I/O path, strong data integrity, backing files, and sparse files. QED format is supported only for compatibility with virtual machines created with old versions of QEMU.

*   QCOW: The QEMU Copy On Write format is the current format for QEMU. The QCOW format does support zlib-based transparent compression and encryption (the latter has flaw and is not recommended). QCOW is available in two versions: QCOW and QCOW2\. The latter tends to supersede the first one. QCOW is [currently fully supported by VirtualBox](https://www.virtualbox.org/manual/ch15.html#idp63002176). QCOW2 comes in two revisions: QCOW2 0.10 and QCOW2 1.1 (which is the default when you create a virtual disk with QEMU). VirtualBox does not support this QCOW2 format (both revisions have been tried).

*   OVF: The Open Virtualization Format is an open format which has been designed for interoperability and distributions of virtual machines between different hypervisors. VirtualBox supports all revisions of this format via the [VBoxManage import/export feature](https://www.virtualbox.org/manual/ch08.html#idp55423424) but with [known limitations](https://www.virtualbox.org/manual/ch14.html#KnownProblems).

*   RAW: This is the mode when the virtual disk is exposed directly to the disk without being contained in a specific file format container. VirtualBox supports this feature in several ways: converting RAW disk [to a specific format](https://www.virtualbox.org/manual/ch08.html#idp59139136), or by [cloning a disk to RAW](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi), or by using directly a VMDK file [which points to a physical disk or a simple file](https://www.virtualbox.org/manual/ch09.html#idp57804112).

### Disk image format conversion

#### VMDK to VDI and VDI to VMDK

VirtualBox can handle back and forth conversion between VDI and VMDK by itself with [VBoxManage clonehd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi).

VMDK to VDI:

```
$ VBoxManage clonehd *source.vmdk* *destination.vdi* --format VDI

```

VDI to VMDK:

```
$ VBoxManage clonehd *source.vdi* *destination.vmdk* --format VMDK

```

#### VHD to VDI and VDI to VHD

VirtualBox can handle conversion back and forth this format with [VBoxManage clonehd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) too.

VHD to VDI:

```
$ VBoxManage clonehd *source.vhd* *destination.vdi* --format VDI

```

VDI to VHD:

```
$ VBoxManage clonehd *source.vdi* *destination.vhd* --format VHD

```

#### QCOW2 to VDI and VDI to QCOW2

[VBoxManage clonehd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) cannot handle the QEMU format conversion; we will thus rely on another tool. The `qemu-img` command from [qemu](https://www.archlinux.org/packages/?name=qemu) can be used to convert images back and forth from VDI to QCOW2\.
**Note:** `qemu-img` can handle a bunch of other formats too. According to the `qemu-img --help`, here are the supported formats this tool supports: "*vvfat vpc vmdk vhdx vdi ssh sheepdog sheepdog sheepdog raw host_cdrom host_floppy host_device file qed qcow2 qcow parallels nbd nbd nbd iscsi dmg tftp ftps ftp https http cow cloop bochs blkverify blkdebug'".*

QCOW2 to VDI:

```
$ qemu-img convert -pO vdi *source.qcow2* *destination.vdi*

```

VDI to QCOW2:

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2*

```

As QCOW2 comes in two revisions (see [#Formats supported by VirtualBox](#Formats_supported_by_VirtualBox), use the flag `-o compat=` to specify the revision.

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2* -o compat=0.10

```

or

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2* -o compat=1.1

```

**Tip:** The `-p` parameter is used to get the progression of the conversion task.

### Mount virtual disks

#### VDI

Mounting vdi images only works with fixed size images (a.k.a. static images); dynamic (dynamically size allocating) images are not easily mountable.

The offset of the partition (within the vdi) is needed, then add the value of `offData` to `32256` (e.g. 69632 + 32256 = 101888):

```
$ VBoxManage internalcommands dumphdinfo <storage.vdi> | grep "offData"

```

The can now be mounted with:

```
# mount -t ext4 -o rw,noatime,noexec,loop,offset=101888 <storage.vdi> /mntpoint/

```

You can also use [mount.vdi](https://github.com/pld-linux/VirtualBox/blob/master/mount.vdi) script that, which you can use as (install script itself to `/usr/bin/`):

```
# mount -t vdi -o fstype=ext4,rw,noatime,noexec *vdi_file_location* */mnt/*

```

Alternately you can use [qemu](https://www.archlinux.org/packages/?name=qemu)'s kernel module that can do this [attrib](http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/):

```
# modprobe nbd max_part=16
# qemu-nbd -c /dev/nbd0 <storage.vdi>
# mount /dev/nbd0p1 /mnt/dir/
# # to unmount:
# umount /mnt/dir/
# qemu-nbd -d /dev/nbd0

```

If the partition nodes are not propagated try using `partprobe /dev/nbd0`; otherwise, a vdi partition can be mapped directly to a node by: `qemu-nbd -P 1 -c /dev/nbd0 <storage.vdi>`.

### Compact virtual disks

Compacting virtual disks only works with `.vdi` files and basically consists in the following steps.

Boot your virtual machine and remove all bloat manually or by using cleaning tools like [bleachbit](https://www.archlinux.org/packages/?name=bleachbit) which is [available for Windows systems too](http://bleachbit.sourceforge.net/download/windows).

Wiping free space with zeroes can be achieved with several tools:

*   If you were previously using Bleachbit, check the checkbox *System > Free disk space* in the GUI, or use `bleachbit -c system.free_disk_space` in CLI;
*   On UNIX-based systems, by using `dd` or preferably [dcfldd](https://www.archlinux.org/packages/?name=dcfldd) (see [here](http://superuser.com/a/355322) to learn the differences) :

	 `# dcfldd if=/dev/zero of=*/fillfile* bs=4M` 

	When `fillfile` reaches the limit of the partition, you will get a message like `1280 blocks (5120Mb) written.dcfldd:: No space left on device`. This means that all of the user-space and non-reserved blocks of the partition will be filled with zeros. Using this command as root is important to make sure all free blocks have been overwritten. Indeed, by default, when using partitions with ext filesystem, a specified percentage of filesystem blocks is reserved for the super-user (see the `-m` argument in the `mkfs.ext4` man pages or use `tune2fs -l` to see how much space is reserved for root applications).

	When the aforementioned process has completed, you can remove the file `*fillfile*` you created.

*   On Windows, there are two tools available:

*   `sdelete` from the [Sysinternals Suite](http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx), type `sdelete -s -z *c:*`, where you need to reexecute the command for each drive you have in your virtual machine;
*   or, if you love scripts, there is a [PowerShell solution](http://blog.whatsupduck.net/2012/03/powershell-alternative-to-sdelete.html), but which still needs to be repeated for all drives.

	 `PS> ./Write-ZeroesToFreeSpace.ps1 -Root *c:\* -PercentFree 0` 

**Note:** This script must be run in a PowerShell environment with administrator privileges. By default, scripts cannot be run, ensure the execution policy is at least on `RemoteSigned` and not on `Restricted`. This can be checked with `Get-ExecutionPolicy` and the required policy can be set with `Set-ExecutionPolicy RemoteSigned`.

Once the free disk space have been wiped, shut down your virtual machine.

The next time you boot your virtual machine, it is recommended to do a filesystem check.

*   On UNIX-based systems, you can use `fsck` manually;

*   On GNU/Linux systems, and thus on Arch Linux, you can force a disk check at boot [thanks to a kernel boot parameter](/index.php/Fsck#Forcing_the_check "Fsck");

*   On Windows systems, you can use:

*   either `chkdsk *c:* /F` where `*c:*` needs to be replaced by each disk you need to scan and fix errors;
*   or `FsckDskAll` [from here](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx) which is basically the same software as `chkdsk`, but without the need to repeat the command for all drives;

Now, remove the zeros from the `vdi` file with [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi):

```
$ VBoxManage modifyhd *your_disk.vdi* --compact

```

**Note:** If your virtual machine has snapshots, you need to apply the above command on each `.vdi` files you have.

### Increase virtual disks

#### General procedure

If you are running out of space due to the small hard drive size you selected when you created your virtual machine, the solution adviced by the VirtualBox manual is to use [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi). However this command only works for VDI and VHD disks and only for the dynamically allocated variants. If you want to resize a fixed size virtual disk disk too, read on this trick which works either for a Windows or UNIX-like virtual machine.

First, create a new virtual disk next to the one you want to increase:

```
$ VBoxManage createhd -filename *new.vdi* --size *10000*

```

where size is in MiB, in this example 10000MiB ~= 10GiB, and *new.vdi* is name of new hard drive to be created.

Next, the old virtual disk needs to be cloned to the new one which this may take some time:

```
$ VBoxManage clonehd *old.vdi* *new.vdi* --existing

```

**Note:** By default, this command uses the *Standard* (corresponding to dynamic allocated) file format variant and thus will not use the same file format variant as your source virtual disk. If your *old.vdi* has a fixed size and you want to keep this variant, add the parameter `--variant Fixed`.

Detach the old hard drive and attach new one, replace all mandatory italic arguments by your own:

```
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium none
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium *new.vdi* --type hdd

```

To get the storage controller name and the port number, you can use the command `VBoxManage showvminfo *VM_name*`. Among the output you will get such a result (what you are looking for is in italic):

```
[...]
Storage Controller Name (0):            IDE
Storage Controller Type (0):            PIIX4
Storage Controller Instance Number (0): 0
Storage Controller Max Port Count (0):  2
Storage Controller Port Count (0):      2
Storage Controller Bootable (0):        on
Storage Controller Name (1):            SATA
Storage Controller Type (1):            IntelAhci
Storage Controller Instance Number (1): 0
Storage Controller Max Port Count (1):  30
Storage Controller Port Count (1):      1
Storage Controller Bootable (1):        on
IDE (1, 0): Empty
*SATA* (*0*, 0): /home/wget/IT/Virtual_machines/GNU_Linux_distributions/ArchLinux_x64_EFI/Snapshots/{6bb17af7-e8a2-4bbf-baac-fbba05ebd704}.vdi (UUID: 6bb17af7-e8a2-4bbf-baac-fbba05ebd704)
[...]
```

Download [GParted live image](http://gparted.org/download.php) and mount it as a virtual CD/DVD disk file, boot your virtual machine, increase/move your partitions, umount GParted live and reboot.

**Note:** On GPT disks, increasing the size of the disk will result in the backup GPT header not being at the end of the device. GParted will ask to fix this, click on *Fix* both times. On MBR disks, you do not have such a problem as this partition table as no trailer at the end of the disk.

Finally, unregister the virtual disk from VirtualBox and remove the file:

```
$ VBoxManage closemedium disk *old.vdi*
$ rm *old.vdi*

```

#### Increase size for VDI disks

If your disk is a vdi one, simply run:

```
$ VBoxManage modifyhd *your_virtual_disk.vdi* --resize *the_new_size*

```

Then jump back to the Gparted step, to increase the size of the partition on the virtual disk.

### Replace a virtual disk manually from the .vbox file

If you think that editing a simple *XML* file is more convenient than playing with the GUI or with `VBoxManage` and you want to replace (or add) a virtual disk to your virtual machine, in the *.vbox* configuration file corresponding to your virtual machine, simply replace the GUID, the file location and the format to your needs:

 `ArchLinux_vm.vbox`  `<HardDisk uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*" location="*ArchLinux_vm.vdi*" format="*VDI*" type="Normal"/>` 

then in the `<AttachedDevice>` sub-tag of `<StorageController>`, replace the GUID by the new one.

 `ArchLinux_vm.vbox` 
```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*"/>
</AttachedDevice>
```

**Note:** If you do not know the GUID of the drive you want to add, you can use the `VBoxManage showhdinfo *file*`. If you previously used `VBoxManage clonehd` to copy/convert your virtual disk, this command should have outputted the GUID just after the copy/conversion completed. Using a random GUID does not work, as each [UUID is stored inside each disk image](http://www.virtualbox.org/manual/ch05.html#cloningvdis).

#### Transfer between Linux host and other OS

The information about path to harddisks and the snapshots is stored between `<HardDisks> .... </HardDisks>` tags in the file with the *.vbox* extension. You can edit them manually or use this script where you will need change only the path or use defaults, assumed that *.vbox* is in the same directory with a virtual harddisk and the snapshots folder. It will print out new configuration to stdout.

```
#!/bin/bash
NewPath="${PWD}/"
Snapshots="Snapshots/"
Filename="$1"

 awk -v SetPath="$NewPath" -v SnapPath="$Snapshots" '{if(index($0,"<HardDisk uuid=") != 0){A=$3;split(A,B,"=");
L=B[2];
 gsub(/\"/,"",L);
  sub(/^.*\//,"",L);
  sub(/^.*\\/,"",L);
 if(index($3,"{") != 0){SnapS=SnapPath}else{SnapS=""};
  print $1" "$2" location="\"SetPath SnapS L"\" "$4" "$5}
else print $0}' "$Filename"
```

**Note:**

*   If you will prepare virtual machine for use in Windows host then in the path name end you should use backslash \ instead of / .
*   The script detects snapshots by looking for `{` in the file name.
*   To make it run on a new host you will need to add it first to the register by clicking on **Machine -> Add...** or use hotkeys Ctrl+A and then browse to *.vbox* file that contains configuration or use command line `VBoxManage registervm *filename*.vbox`

### Clone a virtual disk and assigning a new UUID to it

UUIDs are widely used by VirtualBox. Each virtual machines and each virtual disk of a virtual machine must have a different UUID. When you launch a virtual machine in VirtualBox, the latter will keep track of all UUID of your virtual machine instance. See the [VBoxManage list](http://www.virtualbox.org/manual/ch08.html#vboxmanage-list) to list the items registered with VirtualBox.

If you cloned a virtual disk manually by copying the virtual disk file, you will need to assign a new UUID to the cloned virtual drive if you want to use the disk in the same virtual machine or even in another (if that one has already been opened, and thus registered, with VirtualBox).

You can use this command to assign a new UUID to your virtual disk:

```
$ VBoxManage internalcommands sethduuid */path/to/disk.vdi*

```

**Tip:** In the future, to avoid copying the virtual disk and assigning a new UUID to your file manually, use [VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) instead.

**Note:** The commands above supports [all virtual disk formats supported by VirtualBox](#Formats_supported_by_VirtualBox).

## Tips and tricks

For advanced configuration, see [VirtualBox/Tips and tricks](/index.php/VirtualBox/Tips_and_tricks "VirtualBox/Tips and tricks").

## Troubleshooting

### VERR_ACCESS_DENIED

To access the raw vmdk image on a windows host, run the VirtualBox GUI as administrator.

### pacstrap script fails

If you used *pacstrap* in the [#Installation steps for Arch Linux guests](#Installation_steps_for_Arch_Linux_guests) to also [#Install the Guest Additions](#Install_the_Guest_Additions) **before** performing a first boot into the new guest, you will need to `umount -l /mnt/dev` as root before using *pacstrap* again; a failure to do this will render it unusable.

### Keyboard and mouse are blocked in my virtual machine

This means your virtual machine has captured the input of your keyboard and your mouse. Simply press the right `Ctrl` key and your input should control your host again.

To control transparently your virtual machine with your mouse going back and forth your host, without having to press any key, and thus have a seamless integration, install the guest additions inside the guest. Read from the [#Install the Guest Additions](#Install_the_Guest_Additions) step if you guest is Arch Linux, otherwise read the official VirtualBox help.

### Cannot send CTRL+ALT+Fn key to my virtual machine

Your guest operating system is a GNU/Linux distribution and you want to open a new TTY shell by hitting `Ctrl+Alt+F2` or exit your current X session with `Ctrl+Alt+Backspace`. If you type these keyboard shortcuts without any adaptation, the guest will not receive any input and the host (if it is a GNU/Linux distribution too) will intercept these shortcut keys. To send `Ctrl+Alt+F2` to the guest for example, simply hit your *Host Key* (usually the right `Ctrl` key) and press `F2` simultaneously.

### Fix ISO images problems

While VirtualBox can mount ISO images without problem, there are some image formats which cannot reliably be converted to ISO. For instance, ccd2iso ignores .ccd and .sub files, which can give disk images with broken files.

In this case, you will either have to use [CDEmu](/index.php/CDEmu "CDEmu") for Linux inside VirtualBox or any other utility used to mount disk images.

### VirtualBox GUI does not match my GTK Theme

See [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications") for information about theming Qt based applications like Virtualbox.

### OpenBSD unusable when virtualisation instructions unavailable

While OpenBSD is reported to work fine on other hypervisors without virtualisation instructions (VT-x AMD-V) enabled, an OpenBSD virtual machine running on VirtualBox without these instructions will be unusable, manifesting with a bunch of segmentation faults. Starting VirtualBox with the *-norawr0* argument [may solve the problem](https://www.virtualbox.org/ticket/3947). You can do it like this:

```
$ VBoxSDL -norawr0 -vm *name_of_OpenBSD_VM*

```

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

This can occur if a VM is exited ungracefully. The solution to unlock the VM is trivial:

```
$ VBoxManage controlvm *virtual_machine_name* poweroff

```

### USB subsystem is not working on the host or guest

Your user must be in the `vboxusers` group, and you need to install the [extension pack](#Extension_pack) if you want USB 2 support. Then you will be able to enable USB 2 in the VM settings and add one or several filters for the devices you want to access from the guest OS.

If `VBoxManage list usbhost` does not show any USB devices even if run as root, make sure that there is no old udev rules (from VirtualBox 4.x) in */etc/udev/rules.d/*. VirtualBox 5.0 installs udev rules to */usr/lib/udev/rules.d/*. You can use command like `pacman -Qo /usr/lib/udev/rules.d/60-vboxdrv.rules` to determine if the udev rule file is outdated.

Sometimes, on old Linux hosts, the USB subsystem is not auto-detected resulting in an error `Could not load the Host USB Proxy service: VERR_NOT_FOUND` or in a not visible USB drive on the host, [even when the user is in the **vboxusers** group](https://bbs.archlinux.org/viewtopic.php?id=121377). This problem is due to the fact that VirtualBox switched from *usbfs* to *sysfs* in version 3.0.8\. If the host does not understand this change, you can revert to the old behaviour by defining the following environment variable in any file that is sourced by your shell (e.g. your `~/.bashrc` if you are using *bash*):

 `~/.bashrc`  `VBOX_USB=usbfs` 

Then make sure, the environment has been made aware of this change (reconnect, source the file manually, launch a new shell instance or reboot).

Also make sure that your user is a member of the `storage` group.

### Failed to create the host-only network interface

Make sure all required kernel modules are loaded. See [#Load the VirtualBox kernel modules](#Load_the_VirtualBox_kernel_modules).

### WinXP: Bit-depth cannot be greater than 16

If you are running at 16-bit color depth, then the icons may appear fuzzy/choppy. However, upon attempting to change the color depth to a higher level, the system may restrict you to a lower resolution or simply not enable you to change the depth at all. To fix this, run `regedit` in Windows and add the following key to the Windows XP VM's registry:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

Then update the color depth in the "desktop properties" window. If nothing happens, force the screen to redraw through some method (i.e. `Host+f` to redraw/enter full screen).

### Use serial port in guest OS

Check you permission for the serial port:

```
$ /bin/ls -l /dev/ttyS*
crw-rw---- 1 root uucp 4, 64 Feb  3 09:12 /dev/ttyS0
crw-rw---- 1 root uucp 4, 65 Feb  3 09:12 /dev/ttyS1
crw-rw---- 1 root uucp 4, 66 Feb  3 09:12 /dev/ttyS2
crw-rw---- 1 root uucp 4, 67 Feb  3 09:12 /dev/ttyS3

```

Add your user to the `uucp` [group](/index.php/Group "Group").

### Windows 8.x Error Code 0x000000C4

If you get this error code while booting, even if you choose OS Type Win 8, try to enable the `CMPXCHG16B` CPU instruction:

```
$ vboxmanage setextradata *virtual_machine_name* VBoxInternal/CPUM/CMPXCHG16B 1

```

### Windows 8, 8.1 or 10 fails to install, boot or has error "ERR_DISK_FULL"

Update the VM's settings by going to *Settings > Storage > Controller:SATA* and check "Use Host I/O Cache".

### Linux guests have slow/distorted audio

The AC97 audio driver within the Linux kernel occasionally guesses the wrong clock settings when running inside Virtual Box, leading to audio that is either too slow or too fast. To fix this, create a file in `/etc/modprobe.d` with the following line:

```
options snd-intel8x0 ac97_clock=48000

```

### Guest freezes after starting Xorg

Faulty or missing drivers may cause the guest to freeze after starting Xorg, see for example [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) and [[6]](https://bbs.archlinux.org/viewtopic.php?id=156079). Try disabling 3D acceleration in *Settings > Display*, and check if all [Xorg](/index.php/Xorg "Xorg") drivers are installed.

### "NS_ERROR_FAILURE" and missing menu items

If you encounter this message when first time starting the virtual machine:

```
Failed to open a session for the virtual machine debian.
Could not open the medium '/home/.../VirtualBox VMs/debian/debian.qcow'.
QCow: Reading the L1 table for image '/home/.../VirtualBox VMs/debian/debian.qcow' failed (VERR_EOF).
VD: error VERR_EOF opening image file '/home/.../VirtualBox VMs/debian/debian.qcow' (VERR_EOF).

Result Code: 
NS_ERROR_FAILURE (0x80004005)
Component: 
Medium

```

Exit VirtualBox, delete all files of the new machine and from virtualbox config file remove the last line in `MachineRegistry` menu (or the offending machine you are creating):

 `~/.config/VirtualBox/VirtualBox.xml` 
```
...
<MachineRegistry>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/debian/debian.vbox"/>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/ubuntu/ubuntu.vbox"/>
  ~~<MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/lastvmcausingproblems/lastvmcausingproblems.qcow"/>~~
</MachineRegistry>
...
```

This happens sometimes when selecting *QCOW*/*QCOW2*/*QED* disk format when creating a new virutal disk.

### USB modem

If you have a USB modem which is being used by the guest OS, killing the guest OS can cause the modem to become unusable by the host system. Killing and restarting `VBoxSVC` should fix this problem.

### "The specified path does not exist. Check the path and then try again." error in Windows guests

This error message often appears when running an .exe file which requires administrator priviliges from a shared folder in windows guests. See [the bug report](https://www.virtualbox.org/ticket/5732) for details.

There are two workarounds:

1.  Disable UAC from Control Panel -> Action Center -> "Change User Account Control settings" from left side pane -> set slider to "Never notify" -> OK and reboot
2.  Copy the file from the shared folder to the guest and run from there

Other threads on the internet suggest to add VBOXSVR to the list of trusted sites, but this doesn't work with Windows 7 or newer.

### No 64-bit OS client options

When launching a VM client, and no 64-bit options are available, make sure your CPU virtualization capabilities (usually named `VT-x`) are enabled in the BIOS.

If you're using a Windows host, you may need to disable Hyper-V, as it prevents VirtualBox from using VT-x. [[7]](https://www.virtualbox.org/ticket/12350)

### Host OS freezes on Virtual Machine start

Possible causes/solutions :

*   SMAP

This is a known incompatiblity with SMAP enabled kernels affecting (mostly) Intel Broadwell chipsets. The matter is currently being investigated, with a wide variety of WIP vboxhost module patches out in the wild that are meant to solve the issue. At the moment of writing though, the only 100% guaranteed solution to this problem is disabling SMAP support in your kernel by appending the "nosmap" option to your kernel boot command line.

*   Hardware Virtualisation

Disabling hardware virtualisation (VT-x/AMD-V) may solve the problem.

*   Various Kernel bugs
    *   Fuse mounted partitions (like ntfs) [[8]](https://bbs.archlinux.org/viewtopic.php?id=185841), [[9]](https://bugzilla.kernel.org/show_bug.cgi?id=82951#c12)

Generally, such issues are observed after upgrading VirtualBox or linux kernel. Downgrading them to the previous versions of theirs might solve the problem.

### The virtual machine has terminated unexpectedly during startup with exit code 1 (0x1)

When trying to launch a virtual machine, an error message like the following appears:

```
The virtual machine has terminated unexpectedly during startup with exit code 1 (0x1)
NS_ERROR_FAILURE 0x80004005
Component: MachineWrap
Interface: IMachine
```

This may occur after upgrading the [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) or [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules) package. Try reloading the `vboxdrv` module:

```
# modprobe -r vboxdrv
# modprobe vboxdrv

```

### Analog microphone not working in guest

If the audio input from an analog microphone is working correctly on the host, but no sound seems to get through to the guest, despite the microphone device apparently being detected normally, installing a [sound server](/index.php/Sound_system#Sound_servers "Sound system") such as [PulseAudio](/index.php/PulseAudio "PulseAudio") on the host might fix the problem.

### Fullscreen mode shows blank guest screen

On some window managers ([i3](/index.php/I3 "I3")), VirtualBox has issues with fullscreen mode properly due to the overlay bar. To workaround this issue, disable "Show in Full-screen/Seamless" option in "Guest Settings --> User Interface --> Mini ToolBar". See [the upstream bug report](https://www.virtualbox.org/ticket/14323) for more information.

### Failed to insert module

If you encounter problem when loading modules as follow:

```
Failed to insert 'vboxdrv': Required key not available

```

Make sure you signed your modules or disable `CONFIG_MODULE_SIG_FORCE` in your kernel config.

## See also

*   [VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html)
*   [Wikipedia:VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox")