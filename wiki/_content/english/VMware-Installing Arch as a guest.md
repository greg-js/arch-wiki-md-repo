Related articles

*   [VMware](/index.php/VMware "VMware")
*   [Installing VMWare vCLI](/index.php/Installing_VMWare_vCLI "Installing VMWare vCLI")

This article is about installing Arch Linux in a [VMware](/index.php/VMware "VMware") product, such as [Player (Plus)](http://www.vmware.com/products/player/), [Fusion](http://www.vmware.com/products/fusion/) or [Workstation](http://www.vmware.com/products/workstation/).

## Contents

*   [1 In-kernel drivers](#In-kernel_drivers)
*   [2 VMware Tools versus Open-VM-Tools](#VMware_Tools_versus_Open-VM-Tools)
*   [3 Open-VM-Tools](#Open-VM-Tools)
    *   [3.1 Utilities](#Utilities)
    *   [3.2 Modules](#Modules)
    *   [3.3 Installation](#Installation)
*   [4 Official VMware Tools](#Official_VMware_Tools)
    *   [4.1 Modules](#Modules_2)
    *   [4.2 Installation (from guest)](#Installation_(from_guest))
*   [5 Xorg configuration](#Xorg_configuration)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Shared Folders with vmhgfs-fuse utility](#Shared_Folders_with_vmhgfs-fuse_utility)
        *   [6.1.1 fstab](#fstab)
        *   [6.1.2 Systemd](#Systemd)
    *   [6.2 Legacy Shared Folders with vmhgfs module](#Legacy_Shared_Folders_with_vmhgfs_module)
        *   [6.2.1 Enable at boot](#Enable_at_boot)
            *   [6.2.1.1 fstab](#fstab_2)
            *   [6.2.1.2 Systemd](#Systemd_2)
        *   [6.2.2 Prune mlocate DB](#Prune_mlocate_DB)
    *   [6.3 3D Acceleration](#3D_Acceleration)
        *   [6.3.1 OpenGL and GLSL support](#OpenGL_and_GLSL_support)
    *   [6.4 Time synchronization](#Time_synchronization)
        *   [6.4.1 Host machine as time source](#Host_machine_as_time_source)
        *   [6.4.2 External server as time source](#External_server_as_time_source)
    *   [6.5 Performance Tips](#Performance_Tips)
        *   [6.5.1 Paravirtual SCSI adapter](#Paravirtual_SCSI_adapter)
        *   [6.5.2 Paravirtual Network Adapater](#Paravirtual_Network_Adapater)
        *   [6.5.3 Virtual Machine Settings](#Virtual_Machine_Settings)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Network slow on guest](#Network_slow_on_guest)
    *   [7.2 File share problems with newer kernels](#File_share_problems_with_newer_kernels)
    *   [7.3 Sound problems](#Sound_problems)
    *   [7.4 Mouse problems](#Mouse_problems)
    *   [7.5 Boot problems](#Boot_problems)
        *   [7.5.1 Slow boot time](#Slow_boot_time)
        *   [7.5.2 Shutdown/Reboot hangs](#Shutdown/Reboot_hangs)
    *   [7.6 Window resolution autofit problems](#Window_resolution_autofit_problems)
        *   [7.6.1 Potential solution 1](#Potential_solution_1)
        *   [7.6.2 Potential solution 2](#Potential_solution_2)
        *   [7.6.3 Potential solution 3](#Potential_solution_3)
        *   [7.6.4 Potential solution 4](#Potential_solution_4)
    *   [7.7 Drag and drop, copy/paste](#Drag_and_drop,_copy/paste)
    *   [7.8 Problems when running as a shared VM on Workstation 11](#Problems_when_running_as_a_shared_VM_on_Workstation_11)
    *   [7.9 Shared folder not mounted after system upgrade](#Shared_folder_not_mounted_after_system_upgrade)

## In-kernel drivers

*   `vmw_balloon` - The physical memory management driver. It acts like a "balloon" that can be inflated to reclaim physical pages by reserving them in the guest and invalidating them in the monitor, freeing up the underlying machine pages so they can be allocated to other guests. It can also be deflated to allow the guest to use more physical memory. Deallocated Virtual Machine memory can be reused in the host without terminating the guest.
*   `vmw_pvscsi` - For VMware's Paravirtual SCSI (PVSCSI) HBA.
*   `vmw_vmci` - The Virtual Machine Communication Interface. It enables high-speed communication between host and guest in a virtual environment via the VMCI virtual device.
*   `vmwgfx` - For 3D acceleration. This is a KMS enabled DRM driver for the VMware SVGA2 virtual hardware.
*   `vmxnet3` - For VMware's vmxnet3 virtual ethernet NIC.
*   a fuse-based hgfs implementation has been added to `open-vm-tools` 10.0+ and is supported from kernel version 4.0+.

These drivers are only needed if you are running Arch Linux on a hypervisor like [VMware vSphere Hypervisor](http://www.vmware.com/products/vsphere-hypervisor). Client-server applications can write to the VMCI Sock (vsock) interface to make use of the VMCI virtual device, when communicating between virtual machines.

*   `vsock` - The Virtual Socket Protocol. It is similar to the TCP/IP socket protocol, allowing communication between Virtual Machines and hypervisor or host.
*   `vmw_vsock_vmci_transport` - Implements a VMCI transport for Virtual Sockets.

**Note:** Arch's [Udev](/index.php/Udev "Udev") auto-detects and enables a few of these modules. Additional modules, such as `vmw_balloon`, may need to be added to your [Mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `MODULES` list. For example: ` # cat /etc/mkinitcpio.conf` 
```
...
MODULES="... vmw_balloon vmw_pvscsi vsock vmw_vsock_vmci_transport ..."
```

Make sure to rebuild with:

```
 # mkinitcpio -p linux

```

Some modules, such as the legacy `vmhgfs` shared folder module, will require additional work to manually `compile` and systemd `enable` in order to function properly.

## VMware Tools versus Open-VM-Tools

In 2007, VMware released large partitions of the [VMware Tools](http://kb.vmware.com/kb/340) under the LGPL as [Open-VM-Tools](http://sourceforge.net/projects/open-vm-tools/). The official Tools are not available [separately](http://packages.vmware.com/tools/esx/latest/repos/index.html) for Arch Linux.

Originally, VMware Tools provided the best drivers for network and storage, combined with the functionality for other features such as time synchronization. However, for quite a while now the drivers for the network/SCSI adapter are part of the Linux kernel.

The official VMware Tools used to have the advantage of being able to use the Unity mode feature, but as of VMWare Workstation 12, Unity mode for Linux guests has been removed due to lack of use and developer difficulties in maintaining the feature. See the answer in [this thread](https://communities.vmware.com/thread/518735).

## Open-VM-Tools

### Utilities

The [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) package comes namely with the following utilities:

*   `vmtoolsd` - Service responsible for the Virtual Machine status report.
*   `vmware-checkvm` - Tool to check whether a program is running in the guest.
*   `vmware-toolbox-cmd` - Tool to obtain Virtual Machine information of the host.
*   `vmware-user` - Tool to enable clipboard sharing (copy/paste) between host and guest.
*   `vmware-vmblock-fuse` - Filesystem utility. Enables drag & drop functionality between host and guest through [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (Filesystem in Userspace).
*   `vmware-xferlogs` - Dumps logging/debugging information to the Virtual Machine logfile.
*   `vmhgfs-fuse` - Utility for mounting vmhgfs shared folders.

### Modules

*   `vmhgfs` - Legacy filesystem driver. Enables legacy sharing implementation between host and guest.
*   `vmxnet` - for the old VMXNET network adapter.

### Installation

[Install](/index.php/Install "Install") the [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools). If you want to use shared folders you also need to install the [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) package. [Start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") `vmtoolsd.service` and `vmware-vmblock-fuse.service`.

Try to install [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3) manually if it does not work properly. To enable copy and paste between host and guest [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3) is required.

## Official VMware Tools

### Modules

*   `vmblock` - Filesystem driver. Enables drag & drop functionality between host and guest ([superseded](https://www.mail-archive.com/open-vm-tools-devel@lists.sourceforge.net/msg00213.html) by the `vmware-vmblock-fuse` utility).
*   `vmci` - High performance communication interface between host and guest.
*   `vmmon` - Virtual Machine Monitor.
*   `vmnet` - Networking driver.
*   `vsock` - VMCI sockets.

**Note:** There is no module for `vmware-vmblock-fuse`, and `vmblock` has been removed from the kernel unless you disable `fuse`. Instead, systemd services need to be `enabled` to allow these functions. See instructions below.

### Installation (from guest)

Install the dependencies: [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) (for building), [net-tools](https://www.archlinux.org/packages/?name=net-tools) (for `ifconfig`, used by the installer) and [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (for kernel headers). A make dependency for checking out `open-vm-tools` is [asp](https://www.archlinux.org/packages/?name=asp).

Then, create bogus init directories for the installer:

```
# for x in {0..6}; do mkdir -p /etc/init.d/rc${x}.d; done

```

The installer can then be mounted:

```
# mount /dev/cdrom /mnt

```

Extracted (e.g. to `/root`):

```
# tar xf /mnt/VMwareTools*.tar.gz -C /root

```

And started:

```
# perl /root/vmware-tools-distrib/vmware-install.pl

```

You can safely ignore the following build failures:

*   VMNEXT 3 virtual network card
*   "Warning: This script could not find mkinitrd or update-initramfs and cannot remake the initrd file!"
*   Fuse components not found on the system.

Enable `vmware-vmblock-fuse` systemd services (make sure you install the dependencies manually or use the `-s` flag):

```
 $ asp checkout open-vm-tools
 $ cd open-vm-tools/repos/community-x86_64/
 $ makepkg -s --asdeps
 # cp vm* /usr/lib/systemd/system
 # systemctl enable vmware-vmblock-fuse
 # systemctl enable vmtoolsd

```

Reboot the Virtual Machine:

```
# systemctl reboot

```

Log in and start the VMware Tools:

```
# /etc/init.d/rc6.d/K99vmware-tools start

```

**Tip:** There is also a [project](https://github.com/rasa/vmware-tools-patches) in GitHub trying to automate all this.

## Xorg configuration

**Note:** To use Xorg in a Virtual Machine, a minimum of 32MB VGA memory is needed.

Install the dependencies: [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse), [xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware), and [mesa](https://www.archlinux.org/packages/?name=mesa).

If booting into a `graphical target` you are almost done. `/etc/xdg/autostart/vmware-user.desktop` will get started which will setup most of the things needed to work with the Virtual Machine.

However, if booting into `multi-user.target` or using an uncommon setup (e.g. multiple monitors), then `vmtoolsd.service` needs to be [enabled](/index.php/Enable "Enable"). In addition to this, edit:

 `/etc/X11/Xwrapper.config`  `needs_root_rights=yes` 

to give permission for loading drivers.

## Tips and tricks

### Shared Folders with `vmhgfs-fuse` utility

**Note:** This functionality is only available with `open-vm-tools` v.10.x and kernel 4.x onwards and with VMware Workstation and Fusion.

Share a folder by selecting *Edit virtual machine settings > Options > Shared Folders > Always enabled*, and creating a new share.

You should be able to see the shared folders with:

```
$ vmware-hgfsclient

```

Now you can mount the folder:

```
# mkdir <shared folders root directory>
# vmhgfs-fuse -o allow_other -o auto_unmount .host:/*<shared_folder>* *<shared folders root directory>*

```

Other `vmhgfs-fuse` mount options can be viewed by using the `-h` input flag:

```
# vmhgfs-fuse -h

```

##### fstab

Add a rule for each share:

 `/etc/fstab` 
```
.host:/*<shared_folder>* */home/user1/shares* fuse.vmhgfs-fuse nofail 0 0

```

Create and mount the Shared Folders:

```
# mkdir /home/user1/shares
# mount /home/user1/shares

```

##### Systemd

Create the following `.service`:

 `/etc/systemd/system/*<shared folders root directory>*-*<shared_folder>*.service` 
```
[Unit]
Description=Load VMware shared folders
Requires=vmware-vmblock-fuse.service
After=vmware-vmblock-fuse.service
ConditionPathExists=.host:/*<shared_folder>*
ConditionVirtualization=vmware

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/vmhgfs-fuse -o allow_other -o auto_unmount .host:/*<shared_folder>* *<shared folders root directory>*

[Install]
WantedBy=multi-user.target
```

Make sure the `*<shared folders root directory>*` folder exists on your system. If this folder does not exist then you have to create it as the systemd service depends on it:

```
# mkdir -p *<shared folders root directory>*

```

[Enable](/index.php/Enable "Enable") the `<shared folders root directory>-<shared_folder>.service` mount target.

If you want to mount all shared folders automatically then omit *<shared_folder>*.

### Legacy Shared Folders with vmhgfs module

**Note:** This functionality is only available in VMware Workstation and Fusion

Share a folder by selecting *Edit virtual machine settings > Options > Shared Folders > Always enabled*, and creating a new share.

Make sure the `vmhgfs` driver is loaded:

```
# modprobe vmhgfs

```

You should be able to see the shared folders with:

```
$ vmware-hgfsclient

```

Now you can mount the folder:

```
# mkdir /home/user1/shares
# mount -n -t vmhgfs .host:/*<shared_folder>* /home/user1/shares

```

#### Enable at boot

Edit your `mkinitcpio.conf` like this:

 ` # cat /etc/mkinitcpio.conf` 
```
...
MODULES="... vmhgfs"
...
```

and then update your ramdisk:

```
# mkinitcpio -p linux

```

##### fstab

Add a rule for each share:

 `/etc/fstab` 
```
.host:/*<shared_folder>* */home/user1/shares* vmhgfs defaults 0 0

```

Create and mount the Shared Folders:

```
# mkdir /home/user1/shares
# mount /home/user1/shares

```

##### Systemd

For shared folders to be working you need to have loaded the `vmhgfs` driver. Simply create the following `.service`s:

 `/etc/systemd/system/*<shared folders root directory>*-*<shared_folder>*.mount` 
```
[Unit]
Description=Load VMware shared folders
ConditionPathExists=.host:/*<shared_folder>*
ConditionVirtualization=vmware

[Mount]
What=.host:/*<shared_folder>*
Where=*<shared folders root directory>*/*<shared_folder>*
Type=vmhgfs
Options=defaults,noatime

[Install]
WantedBy=multi-user.target
```
 `/etc/systemd/system/*<shared folders root directory>*-*<shared_folder>*.automount` 
```
[Unit]
Description=Load VMware shared folders
ConditionPathExists=.host:/*<shared_folder>*
ConditionVirtualization=vmware

[Automount]
Where=*<shared folders root directory>*/*<shared_folder>*

[Install]
WantedBy=multi-user.target
```

Make sure the `*<shared folders root directory>*` folder exists on your system. If this folder does not exist then you have to create it as the systemd scripts depend on it:

```
# mkdir -p *<shared folders root directory>*

```

[Enable](/index.php/Enable "Enable") the `mnt-hgfs.automount` mount target.

If you want to mount all shared folders automatically then omit *<shared_folder>*.

#### Prune mlocate DB

When using [mlocate](/index.php/Mlocate "Mlocate"), it is useless to index the shared directories in the `locate DB`. Therefore, add the directories to `PRUNEPATHS` in `/etc/updatedb`.

### 3D Acceleration

If not selected at guest creation time, 3D Acceleration can be enabled in: *Edit virtual machine settings > Hardware > Display > Accelerate 3D graphics*.

**Note:** Xorg can be very slow with 3D Acceleration enabled. It some cases, llvmpipe software rendering is much faster.

#### OpenGL and GLSL support

It is possible to update OpenGL and GLSL with new kernel modules, overriding Arch-controlled versions.

At the time of this writing, OpenGL 3.3 and GLSL 3.30 can be supported. See [https://bbs.archlinux.org/viewtopic.php?id=202713](https://bbs.archlinux.org/viewtopic.php?id=202713) for more details.

### Time synchronization

Configuring time synchronization in a Virtual Machine is important; fluctuations are bound to occur more easily in a guest, compared to a physical host. This is mostly due to the CPU being shared by more than one guest.

There are 2 options to set up time synchronization: the host or an external source.

#### Host machine as time source

To use the host as a time source, ensure `vmtoolsd.service` is [started](/index.php/Start "Start"). Then enable the time synchronization:

```
# vmware-toolbox-cmd timesync enable

```

To synchronize the guest after suspending the host:

```
# hwclock --hctosys --localtime

```

#### External server as time source

See [NTP](/index.php/NTP "NTP").

### Performance Tips

You can try the followings tips to improve the performance of your virtual machine.

#### Paravirtual SCSI adapter

[VMware Paravirtual SCSI (PVSCSI) adapters](http://kb.vmware.com/kb/1010398) are high-performance storage adapters for VMware ESXi that can result in greater throughput and lower CPU utilization. PVSCSI adapters are best suited for environments, where hardware or applications drive a very high amount of I/O throughput.

The SCSI adapter type `VMware Paravirtual` is available in the Virtual Machine settings.

If you do not have these settings in your virtual machine configuration you can still use the paravirtual SCSI adapter like this: Make sure that the paravirtual SCSI adapter is included in your kernel image. For this you have to modify your `mkinitcpio.conf`

 ` cat /etc/mkinitcpio.conf` 
```
...
MODULES="... vmw_pvscsi"
...
```

Rebuild your ramdisk:

```
# mkinitcpio -p linux

```

Shutdown your virtual machine and change the SCSI adapter your `.vmx` to the following:

```
scsi0.virtualDev = "pvscsi"

```

#### Paravirtual Network Adapater

VMware offers [multiple network adapters](http://kb.vmware.com/kb/1001805) for the guest OS. The default adapter used is usually the `e1000` adapter, which emulates an Intel 82545EM Gigabit Ethernet NIC. This Intel adapter is generally compatible with the built-in drivers across most operating systems, include Arch.

For [much more performance and additional features](http://rickardnobel.se/vmxnet3-vs-e1000e-and-e1000-part-1/) (such as multiqueue support), the VMware native `vmxnet3` network adapter can be used.

Arch has the `vmxnet3` kernel module available with a default install. Once enabled in [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") (or if it is auto-detected, check by running `lsmod | grep vmxnet3` to see if it is loaded), shutdown and change the network adapter type in your *.vmx* file to the following:

```
ethernet0.virtualDev = "vmxnet3"

```

After changing network adapters, you will need to update your network and [dhcpcd](/index.php/Dhcpcd "Dhcpcd") settings to use the new adapter name and mac address.

```
# dhcpcd *new_interface_name*
# systemctl enable dhcpcd@*new_interface_name*.service

```

You can get the new interface name by running `ip link`

#### Virtual Machine Settings

These settings could help improve the responsiveness of your virtual machine by reducing disk I/O at the expense of using more host memory. [Vmware's KB1008885](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1008885) provides the following optimizations:

```
mainMem.useNamedFile = "FALSE"
MemTrimRate = "0"
prefvmx.useRecommendedLockedMemSize = "TRUE"
MemAllowAutoScaleDown = "FALSE"
sched.mem.pshare.enable = "FALSE"

```

*   **mainMem.useNamedFile**: This will only work for Windows hosts and you can use this parameter if you experience high disk activity on shutting down the virtual machine. This will prevent VMware from creating a *.vmem* file. Use *mainmem.backing = "swap"* on Linux hosts instead.
*   **MemTrimRate**: This setting prevents that memory which was released by the guest is released on the host also.
*   **prefvmx.useRecommendedLockedMemSize**: Unfortunately there does not seem to exist a proper explanation for this setting. This setting seems to prevent the host system from swapping parts of the guest memory.
*   **MemAllowAutoScaleDown**: Prevents that VMware adjusts the memory size of the virtual machine in case it cannot allocate enough memory.
*   **sched.mem.pshare.enable**: If several virtual machines are running simultaneously VMware will try to locate identical pages and share these between the virtual machines. This can be very I/O intensive.

The following settings could also be set in the configuration dialog of VMware Workstation(*Edit -> Preferences... -> Memory/Priority*).

```
prefvmx.minVmMemPct = "100"
mainMem.partialLazySave = "FALSE"
mainMem.partialLazyRestore = "FALSE"

```

*   **prefvmx.minVmMemPct**: Sets amount of RAM in percent which should be reserved by the virtual machine on the host system. If you set this to a lower value it is possible to assign the virtual machine more memory than available in the host system. Be careful though in this case as this will most likely lead to excessive hard drive usage. If you have enough RAM then leave this value at 100.
*   **mainMem.partialLazySave** and **mainMem.partialLazyRestore**: These two parameters will prevent the virtual machine from creating partial snapshots for suspends. When you use these parameters and you suspend your virtual machine it will take a little bit longer, but there should be less hard disk activity from VMware trying to store this information.

## Troubleshooting

### Network slow on guest

Arch Linux, as well as other Linux guests, may have slow network speeds while using NAT. To resolve this, switch the network type to **Bridged mode** in the guest settings on the host, changing the configuration file for the network on the guest where necessary. For more information on configuration, see [Network configuration](/index.php/Network_configuration "Network configuration"). If on a Windows host and it is not connecting properly despite correct guest configuration, open the **Virtual Network Editor** on the host as **Administrator** and press the **Restore defaults** button at the bottom left.

### File share problems with newer kernels

As the [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) package is no longer being updated, newer kernels are not patched correctly using it to be compatible with a host-guest file share. The [Github repository](https://github.com/davispuh/open-vm-tools-dkms) has some patch files that can be manually applied to restore functionality.

It is also recommended you check the AUR comment section for this package.

### Sound problems

If unacceptably loud and annoying sounds occur, then it may be related to the [PC speaker](/index.php/PC_speaker "PC speaker"). The issue may be resolved by globally disabling the PC speaker within the guest image:

```
 # echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf

```

### Mouse problems

The following problems may occur with mouse:

*   The automatic grab/ungrab feature will not automatically grab input when cursor enters the window
*   Missing buttons
*   Input lag
*   Clicks are not registered in some applications
*   Mouse cursor jumps when entering/leaving virtual machine
*   Mouse position jumps to where it left the guest VM

You can try to [uninstall](/index.php/Uninstall "Uninstall") the [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse) package. [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse) and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) should be sufficient for handling mouse and keyboard inputs.

You can try to add these settings to your `.vmx` configuration file ([Mouse position jumps to where it left the guest VM](https://forums.mageia.org/en/viewtopic.php?f=7&t=7977)):

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx` 
```
mouse.vusb.enable = "TRUE"
mouse.vusb.useBasicMouse = "FALSE"
```

VMware also attempts to automatically optimize mouse for gaming. If experiencing problems, disabling it is recommended: *Edit > Preferences > Input > Optimize mouse for games: Never*

Alternatively, attempting to [disable](http://www.spinics.net/lists/xorg/msg53932.html) the `catchall` event in `60-libinput.conf` may be needed:

 `/usr/share/X11/xorg.conf.d/60-libinput.conf` 
```
#Section "InputClass"
#        Identifier "libinput pointer catchall"
#        MatchIsPointer "on"
#        MatchDevicePath "/dev/input/event*"
#        Driver "libinput"
#EndSection

```

### Boot problems

#### Slow boot time

You may see the following errors if VMWare's memory hot-add feature is enabled.

*   add_memory failed
*   acpi_memory_enable_device() error

Disable the memory hot-add feature by setting `mem.hotadd = "FALSE"` to the `.vmx`.

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx`  `mem.hotadd = "FALSE"` 

#### Shutdown/Reboot hangs

Adjust the timeout for the vmtoolsd service (defaults to 90 seconds).

 `/etc/systemd/system/vmtoolsd.service.d/timeout.conf` 
```
[Service]
TimeoutStopSec=1
```

### Window resolution autofit problems

Autofit means that when you resize the VMWare window in the host, ArchLinux should automatically follow and readjust its resolution to fit the new size of the host window.

#### Potential solution 1

Make sure you have enabled autofit.

For VMware Worksation you can find the setting in: *View -> Autosize -> Autofit Guest*

#### Potential solution 2

For some reason autofit requires packages **gtkmm** and **gtk2**, so you should check that you have them installed. If you don't have X windows installed or you are using a non GTK-based desktop environment such as KDE, you might have to install them manually.

#### Potential solution 3

You may need to add the modules to mkinitcpio.conf.

 `/etc/mkinitcpio.conf`  `MODULES="vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx"` 

Do not forget to run:

 `# mkinitcpio -p linux` 

#### Potential solution 4

[Enable](/index.php/Enable "Enable") `vmtoolsd.service`.

If this doesn't work, make sure you [restart](/index.php/Restart "Restart") the `vmtoolsd.service`.

### Drag and drop, copy/paste

**Tip:** There is an unspecified relationship between it and *gtkmm3* that causes it to silently fail. This is documented in [FS#43159](https://bugs.archlinux.org/task/43159).

The drag-and-drop (copy/paste) feature requires both [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) and [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3) packages to be installed in order to work.

Make the command `vmware-user` run after [X11](/index.php/X11 "X11") by either:

*   Ensuring `etc/xdg/autostart/vmware-user.desktop` exists, and if not, run:

```
# cp /etc/vmware-tools/vmware-user.desktop /etc/xdg/autostart/vmware-user.desktop

```

OR

*   Add `vmware-user` to [Xinitrc](/index.php/Xinitrc "Xinitrc")

### Problems when running as a shared VM on Workstation 11

Workstation 11 has a bug where vmware-hostd crashes if an Arch guest is running as a shared VM and vmtoolsd is running in the guest. A patch to open-vm-tools to work around the bug is [here](https://github.com/vmware/open-vm-tools/issues/31).

### Shared folder not mounted after system upgrade

Most likely, this should only happen to [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools). Since the `vmhgfs` module belongs to [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/), the legacy filesystem driver would not be upgraded by using the command `pacman -Syu`. Therefor, [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) should be manually upgraded before the official repositories.

If a shared folder is not mounted after a system upgrade, then remove the shared filesystem automount, upgrade [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/), run `pacman -Syu`, and finally execute `mkinitcpio -p linux`. Don't forget to restore the filesystem automount.