[VirtualBox](https://www.virtualbox.org) is a [hypervisor](https://en.wikipedia.org/wiki/Hypervisor "wikipedia:Hypervisor") used to run operating systems in a special environment, called a virtual machine, on top of the existing operating system. VirtualBox is in constant development and new features are implemented continuously. It comes with a [Qt](/index.php/Qt "Qt") GUI interface, as well as headless and [SDL](https://en.wikipedia.org/wiki/Simple_DirectMedia_Layer "wikipedia:Simple DirectMedia Layer") command-line tools for managing and running virtual machines.

In order to integrate functions of the host system to the guests, including shared folders and clipboard, video acceleration and a seamless window integration mode, *guest additions* are provided for some guest operating systems.

## Contents

*   [1 Installation steps for Arch Linux hosts](#Installation_steps_for_Arch_Linux_hosts)
    *   [1.1 Install the core packages](#Install_the_core_packages)
    *   [1.2 Install the VirtualBox kernel modules](#Install_the_VirtualBox_kernel_modules)
        *   [1.2.1 Hosts running a custom kernel](#Hosts_running_a_custom_kernel)
            *   [1.2.1.1 DKMS Install](#DKMS_Install)
    *   [1.3 Load the VirtualBox kernel modules](#Load_the_VirtualBox_kernel_modules)
    *   [1.4 Add usernames to the vboxusers group](#Add_usernames_to_the_vboxusers_group)
    *   [1.5 Guest additions disc](#Guest_additions_disc)
    *   [1.6 Extension pack](#Extension_pack)
    *   [1.7 Use the right front-end](#Use_the_right_front-end)
*   [2 Installation steps for Arch Linux guests](#Installation_steps_for_Arch_Linux_guests)
    *   [2.1 Installation in EFI mode](#Installation_in_EFI_mode)
    *   [2.2 Install the Guest Additions](#Install_the_Guest_Additions)
    *   [2.3 Load the Virtualbox kernel modules](#Load_the_Virtualbox_kernel_modules_2)
    *   [2.4 Launch the VirtualBox guest services](#Launch_the_VirtualBox_guest_services)
    *   [2.5 Hardware acceleration](#Hardware_acceleration)
    *   [2.6 Enable shared folders](#Enable_shared_folders)
        *   [2.6.1 Manual mounting](#Manual_mounting)
        *   [2.6.2 Automounting](#Automounting)
        *   [2.6.3 Mount at boot](#Mount_at_boot)
*   [3 Import/export VirtualBox virtual machines from/to other hypervisors](#Import.2Fexport_VirtualBox_virtual_machines_from.2Fto_other_hypervisors)
    *   [3.1 Remove additions](#Remove_additions)
    *   [3.2 Use the right virtual disk format](#Use_the_right_virtual_disk_format)
        *   [3.2.1 Automatic tools](#Automatic_tools)
        *   [3.2.2 Manual conversion](#Manual_conversion)
    *   [3.3 Create the VM configuration for your hypervisor](#Create_the_VM_configuration_for_your_hypervisor)
*   [4 Virtual disks management](#Virtual_disks_management)
    *   [4.1 Formats supported by VirtualBox](#Formats_supported_by_VirtualBox)
    *   [4.2 Disk image format conversion](#Disk_image_format_conversion)
        *   [4.2.1 VMDK to VDI and VDI to VMDK](#VMDK_to_VDI_and_VDI_to_VMDK)
        *   [4.2.2 VHD to VDI and VDI to VHD](#VHD_to_VDI_and_VDI_to_VHD)
        *   [4.2.3 QCOW2 to VDI and VDI to QCOW2](#QCOW2_to_VDI_and_VDI_to_QCOW2)
    *   [4.3 Mount virtual disks](#Mount_virtual_disks)
        *   [4.3.1 VDI](#VDI)
    *   [4.4 Compact virtual disks](#Compact_virtual_disks)
    *   [4.5 Increase virtual disks](#Increase_virtual_disks)
        *   [4.5.1 General procedure](#General_procedure)
        *   [4.5.2 Increase size for VDI disks](#Increase_size_for_VDI_disks)
    *   [4.6 Replace a virtual disk manually from the .vbox file](#Replace_a_virtual_disk_manually_from_the_.vbox_file)
        *   [4.6.1 Transfer between Linux host and other OS](#Transfer_between_Linux_host_and_other_OS)
    *   [4.7 Clone a virtual disk and assigning a new UUID to it](#Clone_a_virtual_disk_and_assigning_a_new_UUID_to_it)
*   [5 Advanced configuration](#Advanced_configuration)
    *   [5.1 Virtual machine launch management](#Virtual_machine_launch_management)
        *   [5.1.1 Starting virtual machines with a service](#Starting_virtual_machines_with_a_service)
        *   [5.1.2 Starting virtual machines with a keyboard shortcut](#Starting_virtual_machines_with_a_keyboard_shortcut)
    *   [5.2 Use specific device in the virtual machine](#Use_specific_device_in_the_virtual_machine)
        *   [5.2.1 Using USB webcam / microphone](#Using_USB_webcam_.2F_microphone)
        *   [5.2.2 Detecting web-cams and other USB devices](#Detecting_web-cams_and_other_USB_devices)
    *   [5.3 Access a guest server](#Access_a_guest_server)
    *   [5.4 D3D acceleration in Windows guests](#D3D_acceleration_in_Windows_guests)
    *   [5.5 VirtualBox on a USB key](#VirtualBox_on_a_USB_key)
    *   [5.6 Run a native Arch Linux installation inside VirtualBox](#Run_a_native_Arch_Linux_installation_inside_VirtualBox)
        *   [5.6.1 Make sure you have a persistent naming scheme](#Make_sure_you_have_a_persistent_naming_scheme)
        *   [5.6.2 Make sure your mkinitcpio image is correct](#Make_sure_your_mkinitcpio_image_is_correct)
        *   [5.6.3 Create a VM configuration to boot from the physical drive](#Create_a_VM_configuration_to_boot_from_the_physical_drive)
            *   [5.6.3.1 Create a raw disk .vmdk image](#Create_a_raw_disk_.vmdk_image)
            *   [5.6.3.2 Create the VM configuration file](#Create_the_VM_configuration_file)
    *   [5.7 Install a native Arch Linux system from VirtualBox](#Install_a_native_Arch_Linux_system_from_VirtualBox)
    *   [5.8 Move a native Windows installation to a virtual machine](#Move_a_native_Windows_installation_to_a_virtual_machine)
        *   [5.8.1 Tasks on Windows](#Tasks_on_Windows)
        *   [5.8.2 Using Disk2vhd to clone Windows partition](#Using_Disk2vhd_to_clone_Windows_partition)
        *   [5.8.3 Tasks on GNU/Linux](#Tasks_on_GNU.2FLinux)
        *   [5.8.4 Fix MBR and Microsoft bootloader](#Fix_MBR_and_Microsoft_bootloader)
        *   [5.8.5 Known limitations](#Known_limitations)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 VERR_ACCESS_DENIED](#VERR_ACCESS_DENIED)
    *   [6.2 pacstrap script fails](#pacstrap_script_fails)
    *   [6.3 Keyboard and mouse are blocked in my virtual machine](#Keyboard_and_mouse_are_blocked_in_my_virtual_machine)
    *   [6.4 Cannot send CTRL+ALT+Fn key to my virtual machine](#Cannot_send_CTRL.2BALT.2BFn_key_to_my_virtual_machine)
    *   [6.5 Fix ISO images problems](#Fix_ISO_images_problems)
    *   [6.6 VirtualBox GUI does not match my GTK Theme](#VirtualBox_GUI_does_not_match_my_GTK_Theme)
    *   [6.7 OpenBSD unusable when virtualisation instructions unavailable](#OpenBSD_unusable_when_virtualisation_instructions_unavailable)
    *   [6.8 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [6.9 USB subsystem is not working on the host or guest](#USB_subsystem_is_not_working_on_the_host_or_guest)
    *   [6.10 Failed to create the host-only network interface](#Failed_to_create_the_host-only_network_interface)
    *   [6.11 WinXP: Bit-depth cannot be greater than 16](#WinXP:_Bit-depth_cannot_be_greater_than_16)
    *   [6.12 Use serial port in guest OS](#Use_serial_port_in_guest_OS)
    *   [6.13 Windows 8.x Error Code 0x000000C4](#Windows_8.x_Error_Code_0x000000C4)
    *   [6.14 Windows 8, 8.1 or 10 fails to install, boot or has error "ERR_DISK_FULL"](#Windows_8.2C_8.1_or_10_fails_to_install.2C_boot_or_has_error_.22ERR_DISK_FULL.22)
    *   [6.15 Linux guests have slow/distorted audio](#Linux_guests_have_slow.2Fdistorted_audio)
    *   [6.16 Guest freezes after starting Xorg](#Guest_freezes_after_starting_Xorg)
    *   [6.17 "NS_ERROR_FAILURE" and missing menu items](#.22NS_ERROR_FAILURE.22_and_missing_menu_items)
    *   [6.18 USB modem](#USB_modem)
    *   [6.19 "The specified path does not exist. Check the path and then try again." error in Windows guests](#.22The_specified_path_does_not_exist._Check_the_path_and_then_try_again..22_error_in_Windows_guests)
    *   [6.20 No 64-bit OS client options](#No_64-bit_OS_client_options)
    *   [6.21 Host OS freezes on Virtual Machine start](#Host_OS_freezes_on_Virtual_Machine_start)
    *   [6.22 The virtual machine has terminated unexpectedly during startup with exit code 1 (0x1)](#The_virtual_machine_has_terminated_unexpectedly_during_startup_with_exit_code_1_.280x1.29)
    *   [6.23 Analog microphone not working in guest](#Analog_microphone_not_working_in_guest)
*   [7 See also](#See_also)

## Installation steps for Arch Linux hosts

In order to launch VirtualBox virtual machines on your Arch Linux box, follow these installation steps.

### Install the core packages

[install](/index.php/Install "Install") the [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) package. [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) will also be installed as a required dependency. To compile the virtualbox modules provided by `virtualbox-host-dkms`, it will also be necessary to install the appropriate headers package(s) for your installed kernel(s)[[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html):

*   [linux](https://www.archlinux.org/packages/?name=linux) kernel: [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)
*   [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel: [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers)
*   [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) kernel: [linux-zen-headers](https://www.archlinux.org/packages/?name=linux-zen-headers)
*   [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) kernel: [linux-grsec-headers](https://www.archlinux.org/packages/?name=linux-grsec-headers)

You can also install the [qt4](https://www.archlinux.org/packages/?name=qt4) optional dependency in order to use the graphical interface which is based on [Qt](/index.php/Qt "Qt"). This is not required if you intend to use VirtualBox in command-line only. [See below to learn the differences](#Use_the_right_front-end).

### Install the VirtualBox kernel modules

Next, to fully virtualize your guest installation, VirtualBox provides the following [kernel modules](/index.php/Kernel_modules "Kernel modules"): `vboxdrv`, `vboxnetadp`, `vboxnetflt`, and `vboxpci`. These must be added to your host kernel.

The binary compatibility of kernel modules depends on the API of the kernel against which they have been compiled. The problem with the Linux kernel is that these interfaces might not be the same from one kernel version to another. In order to avoid compatibility problems and subtle bugs, each time the Linux kernel is upgraded, it is advised to recompile the kernel modules against the Linux kernel version that has just been installed. This is what Arch Linux packagers actually do with the VirtualBox kernel modules packages: each time a new Arch Linux kernel is released, the Virtualbox modules are upgraded accordingly.

#### Hosts running a custom kernel

If you use or intend to use a self-compiled kernel from sources, you have to know that VirtualBox does not require any virtualization modules (e.g. virtuo, kvm,...). The VirtualBox kernel modules provide all the necessary for VirtualBox to work properly. You can thus disable in your kernel *.config* file these virtualization modules if you do not use other hypervisors like Xen, KVM or QEMU.

##### DKMS Install

**Tip:** [DKMS](/index.php/DKMS "DKMS") can automatically generate the modules of the current running kernel by running the following command: `# dkms autoinstall` 

As the [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) package requires compilation, make sure you have the kernel headers corresponding to your custom kernel version to prevent this error from happening: `Your kernel headers for kernel *your custom kernel version* cannot be found at /usr/lib/modules/*your custom kernel version*/build or /usr/lib/modules/*your custom kernel version*/source`

Once [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) is installed, simply generate the kernel modules for the custom kernel by running the following command:

```
# dkms install vboxhost/*virtualbox-host-source version* -k *your custom kernel version*/*your architecture*

```

**Tip:** Use this all-in-one command instead, if you do not want to adapt the above command: `# dkms install vboxhost/$(pacman -Q virtualbox|awk '{print $2}'|sed 's/\-.\+//') -k $(uname -rm|sed 's/\ /\//')` 

To automatically recompile the VirtualBox kernel modules when their sources get upgraded (i.e. when the [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) package has been upgraded), enable the `dkms` service.

### Load the VirtualBox kernel modules

Since version 5.0.16, [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) and [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) use **systemd-modules-load** service to load their modules at boot time.

**Note:** If you don't want the VirtualBox modules to be loaded at boot time, you have to use the classic systemd logic to mask modules by putting an empty files (or symlink to `/dev/null`) in `/etc/modules-load.d`

Among the [kernel modules](/index.php/Kernel_modules "Kernel modules") VirtualBox uses, there is a mandatory module named `vboxdrv`, which must be loaded before any virtual machines can run.

To load the module manually:

```
# modprobe vboxdrv

```

The following modules are optional but are recommended if you do not want to be bothered in some advanced configurations (precised here after): `vboxnetadp`, `vboxnetflt` and `vboxpci`.

*   `vboxnetadp` and `vboxnetflt` are both needed when you intend to use the [bridged](https://www.virtualbox.org/manual/ch06.html#network_bridged) or [host-only networking](https://www.virtualbox.org/manual/ch06.html#network_hostonly) feature. More precisely, `vboxnetadp` is needed to create the host interface in the VirtualBox global preferences, and `vboxnetflt` is needed to launch a virtual machine using that network interface.

*   `vboxpci` is needed when your virtual machine needs to pass through a PCI device on your host.

**Note:** If the VirtualBox kernel modules were loaded in the kernel while you updated the modules, you need to reload them manually to use the new updated version. To do it, run `vboxreload` as root.

Finally, if you use the aforementioned "Host-only" or "bridge networking" feature, make sure [net-tools](https://www.archlinux.org/packages/?name=net-tools) is installed. VirtualBox actually uses `ifconfig` and `route` to assign the IP and route to the host interface configured with `VBoxManage hostonlyif` or via the GUI in *Settings > Network > Host-only Networks > Edit host-only network (space) > Adapter*.

### Add usernames to the vboxusers group

To use the USB ports of your host machine in your virtual machines, add to the `vboxusers` [group](/index.php/Group "Group") the usernames that will be authorized to use this feature. The new group does not automatically apply to existing sessions; the user has to log out and log in again, or start a new environment with the `newgrp` command or with `sudo -u $USER -s`. To add the current user to the `vboxusers` group, type:

```
# gpasswd -a $USER vboxusers

```

### Guest additions disc

It is also recommended to install the [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) package on the host running VirtualBox. This package will act as a disc image that can be used to install the guest additions onto guest systems other than Arch Linux. The *.iso* file will be located at `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso`, and may have to be mounted manually inside the virtual machine. Once mounted, you can run the guest additions installer inside the guest.

### Extension pack

Since VirtualBox 4.0, non-GPL components have been split from the rest of the application. Despite being released under a non-free license and **being only available for personal use**, you might be interested in installing the Oracle Extension Pack which provides [additional features](https://www.virtualbox.org/manual/ch01.html#intro-installing). To avoid manual manipulation, the [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) package is available, and a prebuilt version can be found in the [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories") repository.

If you prefer to use the traditional and manual way: download the extension manually and install it via the GUI (*File > Preferences > Extensions*) or via `VBoxManage extpack install <.vbox-extpack>`, make sure you have a toolkit (like [Polkit](/index.php/Polkit "Polkit"), gksu, etc.) to grant privileged access to VirtualBox. The installation of this extension [requires root access](https://www.virtualbox.org/ticket/8473).

### Use the right front-end

Now, you are ready to use VirtualBox. Congratulations!

Multiple front-ends are available to you of which two are available by default:

*   If you want to use VirtualBox in command-line only (only launch and change settings of existing virtual machines), you can use the `VBoxSDL` command. VBoxSDL does only provide a simple window that contains only the *pure* virtual machine, without menus or other controls.
*   If you want to use VirtualBox in command-line without any GUI running (e.g. on a server) to create, launch and configure virtual machines, use the `VBoxHeadless` which produces no visible output on the host at all, but instead only delivers VRDP data (note: VRDP is only enabled if the extension pack is installed).

If you installed the [qt4](https://www.archlinux.org/packages/?name=qt4) optional dependency, you can run `VirtualBox` and have a nice-looking GUI interface with menus usable via the mouse.

Finally, you can use [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox") to administrate your virtual machines via a web interface.

Refer to the [VirtualBox manual](https://www.virtualbox.org/manual) to learn how to create virtual machines.

**Warning:** If you intend to store virtual disk images on a [Btrfs](/index.php/Btrfs "Btrfs") file system, before creating any images, you should consider disabling [Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs") for the destination directory of these images.

## Installation steps for Arch Linux guests

Boot the Arch installation media through one of the virtual machine's virtual drives. Then, complete the installation of a basic Arch system as explained in the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") or the [Installation guide](/index.php/Installation_guide "Installation guide").

#### Installation in EFI mode

If you want to install Arch Linux in EFI mode inside VirtualBox, in the settings of the virtual machine, choose *System* item from the panel on the left and *Motherboard* tab from the right panel, and check the checkbox *Enable EFI (special OSes only)*. After selecting the kernel from the Arch Linux installation media's menu, the media will hang for a minute or two and will continue to boot the kernel normally afterwards. Be patient.

Once the system and the boot loader are installed, VirtualBox will first attempt to run `/EFI/BOOT/BOOTX64.EFI` from the ESP. If that first option fails, VirtualBox will then try the EFI shell script `startup.nsh` from the root of the ESP. This means that in order to boot the system you have the following options:

*   [Launch the bootloader manually](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") from the EFI shell every time;
*   Move the bootloader to the default `/EFI/BOOT/BOOTX64.EFI` path;
*   Create the `startup.nsh` script at the ESP root containing the path to the boot loader application, e.g. `\EFI\grub\grubx64.efi`.

Do not bother with the VirtualBox Boot Manager (accessible with `F2` at boot): EFI entries added to it manually at boot or with [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) will persist after a reboot [but are lost when the VM is shut down](https://www.virtualbox.org/ticket/11177).

See also [UEFI Virtualbox installation boot problems](https://bbs.archlinux.org/viewtopic.php?id=158003).

### Install the Guest Additions

VirtualBox [Guest Additions](https://www.virtualbox.org/manual/ch04.html) provides drivers and applications that optimize the guest operating system including improved image resolution and better control of the mouse. Within the installed guest system, if using a graphical environment, install [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils). Otherwise install [virtualbox-guest-utils-nox](https://www.archlinux.org/packages/?name=virtualbox-guest-utils-nox) for VirtualBox Guest utilities without X support.

Both packages will install [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) as a dependency. To compile the virtualbox modules provided by `virtualbox-guest-dkms`, it will also be necessary to install the appropriate headers package(s) for your installed kernel(s)[[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html):

*   [linux](https://www.archlinux.org/packages/?name=linux) kernel: [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)
*   [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel: [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers)
*   [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) kernel: [linux-zen-headers](https://www.archlinux.org/packages/?name=linux-zen-headers)
*   [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) kernel: [linux-grsec-headers](https://www.archlinux.org/packages/?name=linux-grsec-headers)

**Note:**

*   You can alternatively install the Guest Additions with the ISO from the [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) package, provided you installed this on the host system. To do this, go to the device menu click Insert Guest Additions CD Image.
*   To recompile the vbox kernel modules, run `rcvboxdrv` as root.

### Load the Virtualbox kernel modules

To load the modules automatically, [enable](/index.php/Enable "Enable") the `vboxservice` service which loads the modules and synchronizes the guest's system time with the host.

To load the modules manually, type:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

To load the VirtualBox module at boot time, refer to [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules") and create a `*.conf` file (e.g. `virtualbox.conf`) in `/etc/modules-load.d/` with these lines:

 `/etc/modules-load.d/virtualbox.conf` 
```
vboxguest
vboxsf
vboxvideo
```

Note that depending on your choice of paravirtualization in VirtualBox, you may need to [edit the unit](/index.php/Systemd#Editing_provided_units "Systemd") with the following property to get it to load: `ConditionVirtualization=*paravirtualization*`

Run `systemd-detect-virt` in the console to determine your paravirtualization.

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

As a shortcut, the `VBoxClient-all` bash script enables all of these features. You should set `VBoxClient` to be automatically loaded as your [desktop environment](/index.php/Desktop_environment "Desktop environment") or [window manager](/index.php/Window_manager "Window manager") starts. In practice,

*   if you are using a [desktop environment](/index.php/Desktop_environment "Desktop environment"), you just need to check a box or add the `/usr/sbin/VBoxClient-all` to the autostart section in your [desktop environment](/index.php/Desktop_environment "Desktop environment") settings (the DE will typically set a flag to a *.desktop* file in `~/.config/autostart`, see [the Autostart section](/index.php/Autostart#Desktop_entries "Autostart") for more details);
*   if you do not have any [desktop environment](/index.php/Desktop_environment "Desktop environment"), add the following line to the top of `~/.xinitrc` above any `exec` options. See [Xinitrc](/index.php/Xinitrc "Xinitrc") for detail.

 `~/.xinitrc`  `/usr/bin/VBoxClient-all` 

VirtualBox can also synchronize the time between the host and the guest. To do this, run `VBoxService` as root. To set this to run automatically on boot, simply [enable](/index.php/Enable "Enable") the `vboxservice` service.

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
*   your username must be in this group, use this command `gpasswd -a $USER vboxsf` to add your username and use `newgrp` to apply the changes immediately;

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

## Import/export VirtualBox virtual machines from/to other hypervisors

If you plan to use your virtual machine on another hypervisor or want to import in VirtualBox a virtual machine created with another hypervisor, you might be interested in reading the following steps.

### Remove additions

Guest additions are available in most hypervisor solutions: VirtualBox comes with the Guest Additions, VMware with the VMware Tools, Parallels with the Parallels Tools, etc. These additional components are designed to be installed inside a virtual machine after the guest operating system has been installed. They consist of device drivers and system applications that optimize the guest operating system for better performance and usability [by providing these features](https://www.virtualbox.org/manual/ch04.html).

If you have installed the additions to your virtual machine, please uninstall them first. Your guest, especially if it is using an OS from the Windows family, might behave weirdly, crash or even might not boot at all if you are still using the specific drivers in another hypervisor.

### Use the right virtual disk format

This step will depend on the ability to convert the virtual disk image directly or not.

#### Automatic tools

Some companies provide tools which offer the ability to create virtual machines from a Windows or GNU/Linux operating system located either in a virtual machine or even in a native installation. With such a product, you do not need to apply this and the following steps and can stop reading here.

*   *[Parallels Transporter](http://www.parallels.com/products/transporter)* which is non free, is a product from Parallels Inc. This solution basically consists in an piece of software called *agent* that will be installed in the guest you want to import/convert. Then, Parallels Transporter, <u>which only works on OS X</u>, will create a virtual machine from that *agent* which is contacted either by USB or Ethernet network.
*   *[VMware vCenter Converter](https://www.vmware.com/products/converter/)* which is free upon registration on the VMware webiste, works nearly the same way as Parallels Transporter, but the piece of software that will gather the data to create the virtual machine only works on a Windows platform.

#### Manual conversion

First, familiarize yourself with the [#Formats supported by VirtualBox](#Formats_supported_by_VirtualBox) and [those supported by third-party hypervisors](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines").

*   Importing or exporting a virtual machine from/to a VMware solution is not a problem at all if you use the VMDK or OVF disk format, otherwise converting [#VMDK to VDI and VDI to VMDK](#VMDK_to_VDI_and_VDI_to_VMDK) is possible and the aforementioned VMware vCenter Converter tool is available.

*   Importing or exporting from/to QEMU is not a problem neither: some QEMU formats are supported directly by VirtualBox and conversion between [#QCOW2 to VDI and VDI to QCOW2](#QCOW2_to_VDI_and_VDI_to_QCOW2) is still available if needed.

*   Importing or exporting from/to Parallels hypervisor is the hardest way: Parallels does only support its own HDD format (even the standard and portable OVF format is not supported!).

*   To export your virtual machine to Parallels, you will need to use the Parallels Transporter tool described above.
*   To import your virtual machine to VirtualBox, you will need to use the VMware vCenter Converter described above to convert the VM to the VMware format first. Then, apply the solution to migrate from VMware.

### Create the VM configuration for your hypervisor

Each hypervisor have their own virtual machine configuration file: `.vbox` for VirtualBox, `.vmx` for VMware, a `config.pvs` file located in the virtual machine bundle (`.pvm` file), etc. You will have thus to recreate a new virtual machine in your new destination hypervisor and specify its hardware configuration as close as possible as your initial virtual machine.

Pay a close attention to the firmware interface (BIOS or UEFI) used to install the guest operating system. While an option is available to choose between these 2 interfaces on VirtualBox and on Parallels solutions, on VMware, you will have to add manually the following line to your *.vmx* file.

 `ArchLinux_vm.vmx`  `firmware = "efi"` 

Finally, ask your hypervisor to use the existing virtual disk you have converted and launch the virtual machine.

**Tip:**

*   On VirtualBox, if you do not want to browse the whole GUI to find the right location to add your new virtual drive device, you can [#Replace a virtual disk manually from the .vbox file](#Replace_a_virtual_disk_manually_from_the_.vbox_file), or use the `VBoxManage storageattach` described in [#Increase virtual disks](#Increase_virtual_disks) or in the [VirtualBox manual page](https://www.virtualbox.org/manual/ch08.html#vboxmanage-storageattach).
*   Similarly, in VMware products, you can replace the location of the current virtual disk location by adapting the *.vmdk* file location in your *.vmx* configuration file.

## Virtual disks management

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

Alternately you can use [qemu](https://www.archlinux.org/packages/?name=qemu)'s kernel module that can do this [[attrib](http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/)]:

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

## Advanced configuration

### Virtual machine launch management

#### Starting virtual machines with a service

Find hereafter the implementation details of a systemd service that will be used to consider a virtual machine as a service.

 `/etc/systemd/system/vboxvmservice@.service` 
```
[Unit]
Description=VBox Virtual Machine %i Service
Requires=systemd-modules-load.service
After=systemd-modules-load.service

[Service]
User=*username*
Group=vboxusers
ExecStart=/usr/bin/VBoxHeadless -s %i
ExecStop=/usr/bin/VBoxManage controlvm %i savestate

[Install]
WantedBy=multi-user.target
```

**Note:** Replace `*username*` with a user that is a member of the `vboxusers` group. Make sure the user chosen is the same user that will create/import virtual machines, otherwise the user will not see the VM appliances.

**Note:** If you have multiple virtual machines managed by Systemd and they are not stopping properly, try to add `RemainAfterExit=true` and `KillMode=none` at the end of `[Service]` section.

To enable the service that will launch the virtual machine at next boot, use:

```
# systemctl enable vboxvmservice@*your_virtual_machine_name*

```

To start the service that will launch directly the virtual machine, use:

```
# systemctl start vboxvmservice@*your_virtual_machine_name*

```

VirtualBox 4.2 introduces [a new way](http://lifeofageekadmin.com/how-to-set-your-virtualbox-vm-to-automatically-startup/) for UNIX-like systems to have virtual machines started automatically, other than using a systemd service.

#### Starting virtual machines with a keyboard shortcut

It can be useful to start virtual machines directly with a keyboard shortcut instead of using the VirtualBox interface (GUI or CLI). For that, you can simply define key bindings in `.xbindkeysrc`. Please refer to [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") for more details.

Example, using the `Fn` key of a laptop with an unused battery key (`F3` on the computer used in this example):

```
"VBoxManage startvm 'Windows 7'"
m:0x0 + c:244
XF86Battery

```

**Note:** If you have a space in the name of your virtual machine, then enclose it with single apostrophes like made in the example just above.

### Use specific device in the virtual machine

#### Using USB webcam / microphone

**Note:** You will need to have VirtualBox extension pack installed before following the steps below. See [#Extension pack](#Extension_pack) for details.

1.  Make sure the virtual machine is not running and your webcam / microphone is not being used.
2.  Bring up the main VirtualBox window and go to settings for Arch machine. Go to USB section.
3.  Make sure "Enable USB Controller" is selected. Also make sure that "Enable USB 2.0 (EHCI) Controller" is selected too.
4.  Click the "Add filter from device" button (the cable with the '+' icon).
5.  Select your USB webcam/microphone device from the list.
6.  Now click OK and start your VM.

**Note:** If your Microphone does not show up in the "Add filter from device" menu, try the USB 3.0 and 1.1 options instead (In Step 3).

#### Detecting web-cams and other USB devices

**Note:** This will not do much if you are running a *NIX OS inside of your VM, as most do not have autodetection features.

If the device that you are looking for does not show up on any of the menus in the section above and you have tried all three USB controller options, boot up your VM three seperate times. Once using the USB 1.1 controller, Once using the USB 2.0 controller, etc. Leave the VM running for at least 5 minutes after startup. Sometimes Windows will autodetect the device for you. Be sure you filter any devices that are not a keyboard or a mouse so they do not start up at boot. This insures that Windows will detect the device at start-up.

### Access a guest server

To access [Apache server](https://en.wikipedia.org/wiki/Apache_HTTP_Server "wikipedia:Apache HTTP Server") on a Virtual Machine from the host machine **only**, simply execute the following lines on the host:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/HostPort" *8888*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/GuestPort" *80*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/Protocol" TCP

```

Where 8888 is the port the host should listen on and 80 is the port the VM will send Apache's signal on.

To use a port lower than 1024 on the host machine, changes need to be made to the firewall on that host machine. This can also be set up to work with SSH or any other services by changing "Apache" to the corresponding service and ports.

**Note:** `pcnet` refers to the network card of the VM. If you use an Intel card in your VM settings, change `pcnet` to `e1000`.

To communicate between the VirtualBox guest and host using ssh, the server port must be forwarded under Settings > Network. When connecting from the client/host, connect to the IP address of the client/host machine, as opposed to the connection of the other machine. This is because the connection will be made over a virtual adapter.

### D3D acceleration in Windows guests

Recent versions of Virtualbox have support for accelerating OpenGL inside guests. This can be enabled with a simple checkbox in the machine's settings, right below where video ram is set, and installing the Virtualbox guest additions. However, most Windows games use Direct3D (part of DirectX), not OpenGL, and are thus not helped by this method. However, it is possible to gain accelerated Direct3D in your Windows guests by borrowing the d3d libraries from Wine, which translate d3d calls into OpenGL, which is then accelerated. These libraries are now part of Virtualbox guest additions software.

After enabling OpenGL acceleration as described above, reboot the guest into safe mode (press F8 before the Windows screen appears but after the Virtualbox screen disappears), and install Virtualbox guest additions, during install enable checkbox "Direct3D support". Reboot back to normal mode and you should have accelerated Direct3D.

**Note:** This hack may or may not work for some games depending on what hardware checks they make and what parts of D3D they use.

**Note:** This was tested on Windows XP, 7 and 8.1\. If method does not work on your Windows version please add data here.

### VirtualBox on a USB key

When using VirtualBox on a USB key, for example to start an installed machine with an ISO image, you will manually have to create VDMKs from the existing drives. However, once the new VMDKs are saved and you move on to another machine, you may experience problems launching an appropriate machine again. To get rid of this issue, you can use the following script to launch VirtualBox. This script will clean up and unregister old VMDK files and it will create new, proper VMDKs for you:

```
#!/bin/bash

# Erase old VMDK entries
rm ~/.VirtualBox/*.vmdk

# Clean up VBox-Registry
sed -i '/sd/d' ~/.VirtualBox/VirtualBox.xml

# Remove old harddisks from existing machines
find ~/.VirtualBox/Machines -name \*.xml | while read file; do
  line=`grep -e "type\=\"HardDisk\"" -n $file | cut -d ':' -f 1`
  if [ -n "$line" ]; then
    sed -i ${line}d $file
    sed -i ${line}d $file
    sed -i ${line}d $file
  fi
  sed -i "/rg/d" $file
done

# Delete prev-files created by VirtualBox
find  ~/.VirtualBox/Machines -name \*-prev -exec rm '{}' \;

# Recreate VMDKs
ls -l /dev/disk/by-uuid | cut -d ' ' -f 9,11 | while read ln; do
  if [ -n "$ln" ]; then
    uuid=`echo "$ln" | cut -d ' ' -f 1`
    device=`echo "$ln" | cut -d ' ' -f 2 | cut -d '/' -f 3 | cut -b 1-3`

    # determine whether drive is mounted already
    checkstr1=`mount | grep $uuid`
    checkstr2=`mount | grep $device`
    checkstr3=`ls ~/.VirtualBox/*.vmdk | grep $device`
    if [[ -z "$checkstr1" && -z "$checkstr2" && -z "$checkstr3" ]]; then
      VBoxManage internalcommands createrawvmdk -filename ~/.VirtualBox/$device.vmdk -rawdisk /dev/$device -register
    fi
  fi
done

# Start VirtualBox
VirtualBox

```

Note that your user has to be added to the "disk" group to create VMDKs out of existing drives.

### Run a native Arch Linux installation inside VirtualBox

If you have a dual boot system between Arch Linux and another operating system, it can become rapidly tedious to switch back and forth if you need to work in both. Also, by using virtual machines, you just have a tiny fragment of your computer power, which can cause issues when working on projects requiring performance.

This guide will let you reuse, in a virtual machine, your native Arch Linux installation when you are running your second operating system. This way, you keep the ability to run each operating system natively, but have the option to run your Arch Linux installation inside a virtual machine.

#### Make sure you have a persistent naming scheme

Depending on your hard drive setup, device files representing your hard drives may appear differently when you will run your Arch Linux installation natively or in virtual machine. This problem occurs when using [FakeRAID](/index.php/RAID#Implementation "RAID") for example. The fake RAID device will be mapped in `/dev/mapper/` when you run your GNU/Linux distribution natively, while the devices are still accessible separately. However, in your virtual machine, it can appear without any mapping in `/dev/sdaX` for example, because the drivers controlling the fake RAID in your host operating system (e.g. Windows) are abstracting the fake RAID device.

To circumvent this problem, we will need to use an addressing scheme that is persistent to both systems. This can be achieved using [UUIDs](/index.php/Fstab#UUIDs "Fstab") in your `/etc/fstab` file. Make sure your [fstab](/index.php/Fstab "Fstab") file is using UUIDs, otherwise fix this issue. Read [fstab](/index.php/Fstab "Fstab") and [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

`/etc/fstab` is not the only location where UUIDs are used. Bootloaders and boot managers make use of them too. Now, make sure these are really using UUIDs.

	[GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")

If you are still using the old [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), maybe is it [time to upgrade](/index.php/GRUB_Legacy#Upgrading_to_GRUB2 "GRUB Legacy"), since this package is now dropped from the official Arch Linux repositories. If you want to keep it, edit `/boot/grub/menu.lst` and replace the `root=/dev/sdXX` statement in your Arch Linux boot entry by the Linux UUID mapping in `/dev/disk/by-uuid/` corresponding to your root partition.

```
title  Arch Linux
root
kernel /vmlinuz-linux root=*/dev/disk/by-uuid/0a3407de-014b-458b-b5c1-848e92a327a3* ro vga=773
initrd /initramfs-linux-vbox.img

```

Repeat the process here, for the fallback entry.

	[GRUB](/index.php/GRUB "GRUB")

If you are running the most recent version of [GRUB](/index.php/GRUB "GRUB"); you have nothing to do. Yet another reason to upgrade to GRUB 2.

**Warning:**

*   Make sure your host partition is only accessible in read only from your Arch Linux virtual machine, this will avoid risk of corruptions if you were to corrupt that host partition by writing on it due to lack of attention.
*   You should NEVER allow VirtualBox to boot from the entry of your second operating system, which, as a reminder, is used as the host for this virtual machine! Take thus a special care especially if your default boot loader/boot manager entry is your other operating system. Give a more important timeout or put it below in the order of preferences.

#### Make sure your mkinitcpio image is correct

Make sure your [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") configuration uses the [HOOK](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") `block`:

 `/etc/mkinitcpio.conf` 
```
[...]
HOOKS="base udev autodetect modconf *block* filesystems keyboard fsck"
[...]
```

If it is not present, add it and [regenerate your initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio"):

```
# mkinitcpio -p linux

```

#### Create a VM configuration to boot from the physical drive

##### Create a raw disk .vmdk image

Now, we need to create a new virtual machine which will use a [RAW disk](https://www.virtualbox.org/manual/ch09.html#rawdisk) as virtual drive, for that we will use a ~ 1Kio VMDK file which will be mapped to a physical disk. Unfortunately, VirtualBox does not have this option in the GUI, so we will have to use the console and use an internal command of `VBoxManage`.

Boot the host which will use the Arch Linux virtual machine. The command will need to be adapted according to the host you have.

	On a GNU/Linux host

There is 3 ways to achieve this: login as root, changing the access right of the device with `chmod`, adding your user to the `disk` group. The latter way is the more elegant, let us proceed that way:

```
# gpasswd -a *your_user* disk

```

Apply the new group settings with:

```
$ newgrp

```

Now, you can use the command:

```
$ VBoxManage internalcommands createrawvmdk -filename */path/to/file.vmdk* -rawdisk */dev/sdb* -register 

```

Adapt the above command to your need, especially the path and filename of the VMDK location and the raw disk location to map which contain your Arch Linux installation.

	On a Windows host

Open a command prompt must be run as administrator.
**Tip:** On Windows, open your start menu/start screen, type `cmd`, and type `Ctrl+Shift+Enter`, this is a shortcut to execute the selected program with admin rights.
On Windows, as the disk filename convention is different from UNIX, use this command to determine what drives you have in your Windows system and their location: `# wmic diskdrive get name,size,model` 
```
Model                               Name                Size
WDC WD40EZRX-00SPEB0 ATA Device     \\.\PHYSICALDRIVE1  4000783933440
KINGSTON SVP100S296G ATA Device     \\.\PHYSICALDRIVE0  96024821760
Hitachi HDT721010SLA360 ATA Device  \\.\PHYSICALDRIVE2  1000202273280
Innostor Ext. HDD USB Device        \\.\PHYSICALDRIVE3  1000202273280
```

In this example, as the Windows convention is `\\.\PhysicalDriveX` where X is a number from 0, `\\.\PHYSICALDRIVE1` could be analogous to `/dev/sdb` from the Linux disk terminology.

To use the `VBoxManage` command on Windows, you can either, change the current directory to your VirtualBox installation folder first with `cd C:\Program Files\Oracle\VirtualBox\`

```
# .\VBoxManage.exe internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

or use the absolute path name:

```
# "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

	On another OS host

There are other limitations regarding the aforementioned command when used in other operating systems like OS X, please thus [read carefully the manual page](https://www.virtualbox.org/manual/ch09.html#rawdisk), if you are concerned.

##### Create the VM configuration file

**Note:**

*   To make use of the VBoxManage command on Windows, you need to change the current directory to your VirtualBox installation folder first: cd C:\Program Files\Oracle\VirtualBox\.
*   Windows makes use of backslashes instead of slashes, please replace all slashes / occurrences by backslashes \ in the commands that follow when you will use them.

After, we need to create a new machine (replace the *VM_name* to your convenience) and register it with VirtualBox.

```
$ VBoxManage createvm -name *VM_name* -register

```

Then, the newly raw disk needs to be attached to the machine. This will depend if your computer or actually the root of your native Arch Linux installation is on an IDE or a SATA controller.

If you need an IDE controller:

```
$ VBoxManage storagectl *VM_name* --name "IDE Controller" --add ide
$ VBoxManage storageattach *VM_name* --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

otherwise:

```
$ VBoxManage storagectl *VM_name* --name "SATA Controller" --add sata
$ VBoxManage storageattach *VM_name* --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

While you continue using the CLI, it is recommended to use the VirtualBox GUI, to personalise the virtual machine configuration. Indeed, you must specify its hardware configuration as close as possible as your native machine: turning on the 3D acceleration, increasing video memory, setting the network interface, etc.

Finally, you may want to seamlessly integrate your Arch Linux with your host operating system and allow copy pasting between both OSes. Please refer to [#Install the Guest Additions](#Install_the_Guest_Additions) for that, since this Arch Linux virtual machine is basically an Arch Linux guest.

**Warning:** For [Xorg](/index.php/Xorg "Xorg") to work in natively and in the virtual machine, since obviously it will be using different drivers, it is best if there is no `/etc/X11/xorg.conf`, so Xorg will pick up everything it needs on the fly. However, if you really do need your own Xorg configuration, maybe is it worth to set your default systemd target to `multi-user.target` with `systemctl isolate graphical.target` as root (more details at [Systemd#Targets table](/index.php/Systemd#Targets_table "Systemd") and [Systemd#Change current target](/index.php/Systemd#Change_current_target "Systemd")). In that way, the graphical interface is disabled (i.e. Xorg is not launched) and after you logged in, you can `startx`} manually with a custom `xorg.conf`.

### Install a native Arch Linux system from VirtualBox

In some cases it may be useful to install a native Arch Linux system while running another operating system: one way to accomplish this is to perform the installation through VirtualBox on a [raw disk](http://www.virtualbox.org/manual/ch09.html#rawdisk). If the existing operating system is Linux based, you may want to consider following [Install from Existing Linux](/index.php/Install_from_Existing_Linux "Install from Existing Linux") instead.

This scenario is very similar to [#Run a native Arch Linux installation inside VirtualBox](#Run_a_native_Arch_Linux_installation_inside_VirtualBox), but will follow those steps in a different order: start by [#Create a raw disk .vmdk image](#Create_a_raw_disk_.vmdk_image), then [#Create the VM configuration file](#Create_the_VM_configuration_file).

Now, you should have a working VM configuration whose virtual VMDK disk is tied to a real disk. The installation process is exactly the same as the steps described in [#Installation steps for Arch Linux guests](#Installation_steps_for_Arch_Linux_guests), but [#Make sure you have a persistent naming scheme](#Make_sure_you_have_a_persistent_naming_scheme) and [#Make sure your mkinitcpio image is correct](#Make_sure_your_mkinitcpio_image_is_correct).

**Warning:**

*   For BIOS systems and MBR disks, do not install a bootloader inside your virtual machine, this will not work since the MBR is not linked to the MBR of your real machine and your virtual disk is only mapped to a real partition without the MBR.
*   For UEFI systems without [CSM](https://en.wikipedia.org/wiki/Compatibility_Support_Module#CSM "wikipedia:Compatibility Support Module") and GPT disks, the installation will not work at all since:

*   the [ESP](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition") partition is not mapped to your virtual disk and Arch Linux requires to have the Linux kernel on it to boot as an EFI application (see [EFISTUB](/index.php/EFISTUB "EFISTUB") for details);
*   and the efivars, if you are installing Arch Linux using the EFI mode brought by VirtualBox, are not the one of your real system: the bootmanager entries will hence not be registered.

*   This is why, it is recommended to create your partitions in a native installation first, otherwize the partitions will not be taken into consideration in your MBR/GPT partition table.

After completing the installation, boot your computer natively with an GNU/Linux installation media (whether it be Arch Linux or not), [chroot](/index.php/Beginner%27s_Guide#Chroot_and_configure_the_base_system "Beginner's Guide") into your installed Arch Linux installation and [#Install and configure a bootloader](/index.php/Beginner%27s_Guide#Install_and_configure_a_bootloader "Beginner's Guide").

### Move a native Windows installation to a virtual machine

If you want to migrate an existing native Windows installation to a virtual machine which will be used with VirtualBox on GNU/Linux, this use case is for you. This section only covers native Windows installation using the MSDOS/Intel partition scheme. Your Windows installation must reside on the first MBR partition for this operation to success. Operation for other partitions are available but have been untested (see [#Known limitations](#Known_limitations) for details).

**Warning:** If you are using an OEM version of Windows, this process is unauthorized by the end user license license. Indeed, the OEM license typically states the Windows install is tied with the hardware together. Transferring a Windows install to a virtual machine removes this link. Make thus sure you have a full Windows install or a volume license model before continuing. If you have a full Windows license but the latter is not coming in volume, nor as a special license for several PCs, this means you will have to remove the native installation after the transfer operation has been achieved.

A couple of tasks are required to be done inside your native Windows installation first, then on your GNU/Linux host.

#### Tasks on Windows

The first three following points comes from [this outdated VirtualBox wiki page](https://www.virtualbox.org/wiki/Migrate_Windows#HAL), but are updated here.

*   Remove IDE/ATA controllers checks (Windows XP only): Windows memorize the IDE/ATA drive controllers it has been installed on and will not boot if it detects these have changed. The solution proposed by Microsoft is to reuse the same controller or use one of the same serial, which is impossible to achieve since we are using a Virtual Machine. [MergeIDE](https://www.virtualbox.org/wiki/Migrate_Windows#HardDiskSupport), a German tool, developped upon another other solution proposed by Microsoft can be used. That solution basically consists in taking all IDE/ATA controller drivers supported by Windows XP from the initial driver archive (the location is hard coded, or specify it as the first argument to the `.bat` script), installing them and registering them with the regedit database.

*   Use the right type of Hardware Abstraction Layer (old 32 bits Windows versions): Microsoft ships 3 default versions: `Hal.dll` (Standard PC), `Halacpi.dll` (ACPI HAL) and `Halaacpi.dll` (ACPI HAL with IO APIC). Your Windows install could come installed with the first or the second version. In that way, please [disable the *Enable IO/APIC* VirtualBox extended feature](https://www.virtualbox.org/manual/ch08.html#idp56927888).

*   Disable any AGP device driver (only outdated Windows versions): If you have the files `agp440.sys` or `intelppm.sys` inside the `C:\Windows\SYSTEM32\drivers\` directory, remove it. As VirtualBox uses a PCI virtual graphic card, this can cause problems when this AGP driver is used.

*   Create a Windows recovery disk: In the following steps, if things turn bad, you will need to repair your Windows installation. Make sure you have an install media at hand, or create one with *Create a recovery disk* from Vista SP1, *Create a system repair disc* on Windows 7 or *Create a recovery drive* on Windows 8.x).

#### Using Disk2vhd to clone Windows partition

Boot into Windows, clean up the installation (with [CCleaner](http://www.piriform.com/ccleaner) for example), use [disk2vhd](https://technet.microsoft.com/en-us/library/ee656415.aspx) tool to create a VHD image. Include a reserved system partition (if present) and the actual Windows partition (usually disk C:). The size of Disk2vhd-created image will be the sum of the actual files on the partition (used space), not the size of a whole partition. If all goes well, the image should just boot in a VM and you won't have to go through the hassle with MBR and Windows bootloader, as in the case of cloning an entire partition.

#### Tasks on GNU/Linux

**Tip:** Skip the partition-related parts if you created VHD image with [Disk2vhd](#Using_Disk2vhd_to_clone_Windows_partition).

*   Reduce the native Windows partition size to the size Windows actually needs with `ntfsresize` available from [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). The size you will specify will be the same size of the VDI that will be created in the next step. If this size is too low, you may break your Windows install and the latter might not boot at all.

	Use the `--no-action` option first to run a test:

	 `# ntfsresize --no-action --size *52Gi* */dev/sda1*` 

	If only the previous test succeeded, execute this command again, but this time without the aforementioned test flag.

*   Install VirtualBox on your GNU/Linux host (see [#Installation steps for Arch Linux hosts](#Installation_steps_for_Arch_Linux_hosts) if your host is Arch Linux).

*   Create the Windows disk image from the beginning of the drive to the end of the first partition where is located your Windows installation. Copying from the beginning of the disk is necessary because the MBR space at the beginning of the drive needs to be on the virtual drive along with the Windows partition. In this example two following partitions `sda2` and `sda3`will be later removed from the partition table and the MBR bootloader will be updated.

	 `# sectnum=$(( $(cat /sys/block/''sda/sda1''/start) + $(cat /sys/block/''sda/sda1''/size) ))` 

	Using `cat /sys/block/*sda/sda1*/size` will output the number of total sectors of the first partition of the disk `sda`. Adapt where necessary.

	 `# dd if=''/dev/sda'' bs=512 count=$sectnum | VBoxManage convertfromraw stdin ''windows.vdi'' $(( $sectnum * 512 ))` 

	We need to display the size in byte, `$(( $sectnum * 512 ))` will convert the sector numbers to bytes.

*   Since you created your disk image as root, set the right ownership to the virtual disk image: `# chown *your_user*:*your_group* windows.vdi` 

*   Create your virtual machine configuration file and use the virtual disk created previously as the main virtual hard disk.

*   Try to boot your Windows VM, it may just work. First though remove and repair disks from the boot process as it may interfere (and likely will) booting into safe-mode.

*   Attempt to boot your Windows virtual machine in safe mode (press the F8 key before the Windows logo shows up)... if running into boot issues, read [#Fix MBR and Microsoft bootloader](#Fix_MBR_and_Microsoft_bootloader). In safe-mode, drivers will be installed likely by the Windows plug-and-play detection mechanism [view](http://i.imgur.com/hh1RrSp.png). Additionally, install the VirtualBox Guest Additions via the menu *Devices* > *Insert Guest Additions CD image...*. If a new disk dialog does not appear, navigate to the CD drive and start the installer manually.

*   You should finally have a working Windows virtual machine. Do not forget to read the [#Known limitations](#Known_limitations).

*   Performance tip: according to [VirtualBox manual](http://www.virtualbox.org/manual/ch05.html#harddiskcontrollers), SATA controller has a better performance than IDE. If you can't boot Windows off virtual SATA controller right away, it is probably due to the lack of SATA drivers. Attach virtual disk to IDE controller, create an empty SATA controller and boot the VM - Windows should automatically install SATA drivers for the controller. You can then shutdown VM, detach virtual disk from IDE controller and attach it to SATA controller instead.

#### Fix MBR and Microsoft bootloader

If your Windows virtual machine refuses to boot, you may need to apply the following modifications to your virtual machine.

*   Boot a GNU/Live live distribution inside your virtual machine before Windows starts up.

*   Remove other partitions entries from the virtual disk MBR. Indeed, since we copied the MBR and only the Windows partition, the entries of the other partitions are still present in the MBR, but the partitions are not available anymore. Use `fdisk` to achieve this for example.

```
fdisk ''/dev/sda''
Command (m for help): a
Partition number (''1-3'', default ''3''): ''1''
```

*   Write the updated partition table to the disk (this will recreate the MBR) using the `m` command inside `fdisk`.

*   Use [testdisk](https://www.archlinux.org/packages/?name=testdisk) (see [here](http://www.cgsecurity.org/index.html?testdisk.html) for details) to add a generic MBR:

	 `# testdisk > *Disk /dev/sda...'* > [Proceed] >  [Intel] Intel/PC partition > [MBR Code] Write TestDisk MBR to first sector > Write a new copy of MBR code to first sector? (Y/n) > Y > Write a new copy of MBR code, confirm? (Y/N) > A new copy of MBR code has been written. You have to reboot for the change to take effect. > [OK]` 

*   With the new MBR and updated partition table, your Windows virtual machine should be able to boot. If you are still encountering issues, boot your Windows recovery disk from on of the previous step, and inside your Windows RE environment, execute the commands [described here](http://support.microsoft.com/kb/927392).

#### Known limitations

*   Your virtual machine can sometimes hang and overrun your RAM, this can be caused by conflicting drivers still installed inside your Windows virtual machine. Good luck to find them!
*   Additional software expecting a given driver beneath may either not be disabled/uninstalled or needs to be uninstalled first as the drivers that are no longer available.
*   Your Windows installation must reside on the first partition for the above process to work. If this requirement is not met, the process might be achieved too, but this had not been tested. This will require either copying the MBR and editing in hexadecimal see [VirtualBox: booting cloned disk](http://superuser.com/questions/237782/virtualbox-booting-cloned-disk/253417#253417) or will require to fix the partition table [manually](http://gparted.org/h2-fix-msdos-pt.php) or by repairing Windows with the recovery disk you created in a previous step. Let us consider our Windows installation on the second partition; we will copy the MBR, then the second partition where to the disk image. `VBoxManage convertfromraw` needs the total number of bytes that will be written: calculated thanks to the size of the MBR (the start of the first partition) plus the size of the second (Windows) partition. `{ dd if=/dev/sda bs=512 count=$(cat /sys/block/sda/sda1/start) ; dd if=/dev/sda2 bs=512 count=$(cat /sys/block/sda/sda2/size) ; } | VBoxManage convertfromraw stdin windows.vdi $(( ($(cat /sys/block/sda/sda1/start) + $(cat /sys/block/sda/sda2/size)) * 512 ))`.

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

Add your user to the `uucp` group.

```
# gpasswd -a $USER uucp 

```

and log out and log in again.

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

There are several workarounds:

1.  Disable UAC from Control Panel -> Action Center -> "Change User Account Control settings" from left side pane -> set slider to "Never notify" -> OK and reboot
2.  Copy the file from the shared folder to the guest and run from there
3.  Control Panel -> Network and Internet -> Internet Options -> Security -> Trusted Sites -> Sites -> Add "VBOXSVR" as a website
4.  Start -> type "gpedit.msc" and press Enter -> Computer Configuration -> Administrative Templates -> Windows Components -> Internet Explorer -> Internet Control Panel -> Security Page -> Size to Zone Assignment List -> Add "VBOXSVR" to "2" and reboot

### No 64-bit OS client options

When launching a VM client, and no 64-bit options are available, make sure your CPU virtualization capabilities (usually named `VT-x`) are enabled in the BIOS.

### Host OS freezes on Virtual Machine start

Possible causes/solutions :

*   SMAP

This is a known incompatiblity with SMAP enabled kernels affecting (mostly) Intel Broadwell chipsets. The matter is currently being investigated, with a wide variety of WIP vboxhost module patches out in the wild that are meant to solve the issue. At the moment of writing though, the only 100% guaranteed solution to this problem is disabling SMAP support in your kernel by appending the "nosmap" option to your kernel boot command line.

*   Hardware Virtualisation

Disabling hardware virtualisation (VT-x/AMD-V) may solve the problem.

*   Various Kernel bugs
    *   Fuse mounted partitions (like ntfs) [[7]](https://bbs.archlinux.org/viewtopic.php?id=185841), [[8]](https://bugzilla.kernel.org/show_bug.cgi?id=82951#c12)

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

## See also

*   [VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html)
*   [Wikipedia:VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox")