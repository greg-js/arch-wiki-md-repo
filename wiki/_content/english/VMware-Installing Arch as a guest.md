Related articles

*   [VMware](/index.php/VMware "VMware")
*   [Installing VMWare vCLI](/index.php/Installing_VMWare_vCLI "Installing VMWare vCLI")

This article is about installing Arch Linux in a [VMware](/index.php/VMware "VMware") product, such as [Player (Plus)](http://www.vmware.com/products/player/), [Fusion](http://www.vmware.com/products/fusion/) or [Workstation](http://www.vmware.com/products/workstation/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
        *   [6.5.2 Paravirtual Network Adapter](#Paravirtual_Network_Adapter)
        *   [6.5.3 Virtual Machine Settings](#Virtual_Machine_Settings)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Network slow on guest](#Network_slow_on_guest)
    *   [7.2 File share problems with legacy vmhgfs module and newer kernels](#File_share_problems_with_legacy_vmhgfs_module_and_newer_kernels)
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
        *   [7.6.5 Potential solution 5](#Potential_solution_5)
    *   [7.7 Drag and drop, copy/paste](#Drag_and_drop,_copy/paste)
    *   [7.8 Problems when running as a shared VM on Workstation 11](#Problems_when_running_as_a_shared_VM_on_Workstation_11)
    *   [7.9 Shared folder not mounted after system upgrade](#Shared_folder_not_mounted_after_system_upgrade)

## In-kernel drivers

**Note:** Arch's [Udev](/index.php/Udev "Udev") auto-detects and enables some of these modules. If any of them is not auto-detected (check by running `lsmod | grep *modulename*` ) and if it is required, the module can be added to [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `MODULES` array. For example: `/etc/mkinitcpio.conf` 
```
...
MODULES=(... vmw_balloon vmw_pvscsi vsock vmw_vsock_vmci_transport ...)
```

Make sure to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

*   `vmw_balloon` - The physical memory management driver. It acts like a "balloon" that can be inflated to reclaim physical pages by reserving them in the guest and invalidating them in the monitor, freeing up the underlying machine pages so they can be allocated to other guests. It can also be deflated to allow the guest to use more physical memory. Deallocated Virtual Machine memory can be reused in the host without terminating the guest.
*   `vmw_pvscsi` - For VMware's Paravirtual SCSI (PVSCSI) HBA.
*   `vmw_vmci` - The Virtual Machine Communication Interface. It enables high-speed communication between host and guest in a virtual environment via the VMCI virtual device.
*   `vmwgfx` - For 3D acceleration. This is a KMS enabled DRM driver for the VMware SVGA2 virtual hardware.
*   `vmxnet3` - For VMware's vmxnet3 virtual ethernet NIC.
*   a fuse-based hgfs implementation has been added to `open-vm-tools` 10.0+ and is supported from kernel version 4.0+.

The following drivers are only needed if you are running Arch Linux on a hypervisor like [VMware vSphere Hypervisor](http://www.vmware.com/products/vsphere-hypervisor). Client-server applications can write to the VMCI Sock (vsock) interface to make use of the VMCI virtual device, when communicating between virtual machines.

*   `vsock` - The Virtual Socket Protocol. It is similar to the TCP/IP socket protocol, allowing communication between Virtual Machines and hypervisor or host.
*   `vmw_vsock_vmci_transport` - Implements a VMCI transport for Virtual Sockets.

Some modules, such as the legacy `vmhgfs` shared folder module, will require additional work to manually `compile` and systemd `enable` in order to function properly.

## VMware Tools versus Open-VM-Tools

In 2007, VMware released large partitions of the [VMware Tools](http://kb.vmware.com/kb/340) under the LGPL as [Open-VM-Tools](http://sourceforge.net/projects/open-vm-tools/). The official Tools are not available [separately](http://packages.vmware.com/tools/esx/latest/repos/index.html) for Arch Linux.

Originally, VMware Tools provided the best drivers for network and storage, combined with the functionality for other features such as time synchronization. However, now the drivers for the network/SCSI adapter are part of the Linux kernel.

The official VMware Tools also had the advantage of being able to use the Unity mode feature, but as of VMWare Workstation 12, Unity mode for Linux guests has been removed due to lack of use and developer difficulties in maintaining the feature. See [this thread](https://communities.vmware.com/thread/518735).

## Open-VM-Tools

### Utilities

The [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) package comes with the following utilities:

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

[Install](/index.php/Install "Install") [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools). If the legacy `vmhgfs` shared folder module is desired, the [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) package must be installed (the new `vmhgfs-fuse` driver is included in [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools)). [Start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") `vmtoolsd.service` and `vmware-vmblock-fuse.service`.

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

The following build failures can safely be ignored:

*   VMNEXT 3 virtual network card
*   "Warning: This script could not find mkinitrd or update-initramfs and cannot remake the initrd file!"
*   Fuse components not found on the system.

Enable `vmware-vmblock-fuse` systemd services (make sure the dependencies are manually installed, or that the `-s` flag) used. The `open-vm-tools` source code should be checked out using the [Arch Build System](/index.php/Arch_Build_System "Arch Build System").

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

Additionally, to auto start `vmware-tools` on boot, create a new file `/etc/systemd/system/vmwaretools.service`:

 `/etc/systemd/system/vmwaretools.service` 
```
[Unit]
Description=VMWare Tools daemon

[Service]
ExecStart=/etc/init.d/vmware-tools start
ExecStop=/etc/init.d/vmware-tools stop
PIDFile=/var/lock/subsys/vmware
TimeoutSec=0
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

And enable the new systemd service:

```
 # systemctl enable vmwaretools.service  

```

**Tip:** There is also a [project](https://github.com/rasa/vmware-tools-patches) in GitHub trying to automate these steps.

## Xorg configuration

**Note:** To use Xorg in a Virtual Machine, a minimum of 32MB VGA memory is needed.

Install the dependencies: [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse), [xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware), and [mesa](https://www.archlinux.org/packages/?name=mesa).

These packages should be all that are required to get started with booting into a `graphical target`: . `/etc/xdg/autostart/vmware-user.desktop` will get started which will set up most of what is needed to work with the Virtual Machine.

However, if booting into `multi-user.target` or using an uncommon setup (e.g. multiple monitors), then `vmtoolsd.service` needs to be [enabled](/index.php/Enable "Enable"). In addition to this, edit:

 `/etc/X11/Xwrapper.config`  `needs_root_rights=yes` 

to give permission for loading drivers.

## Tips and tricks

### Shared Folders with `vmhgfs-fuse` utility

**Note:** This functionality is only available with `open-vm-tools` v.10.x and kernel 4.x onwards and with VMware Workstation and Fusion.

Share a folder by selecting *Edit virtual machine settings > Options > Shared Folders > Always enabled*, and creating a new share.

The shared folders should be visible with:

```
$ vmware-hgfsclient

```

Now the folder can be mounted:

```
# mkdir <shared folders root directory>
# vmhgfs-fuse -o allow_other -o auto_unmount .host:/*<shared_folder>* *<shared folders root directory>*

```

If the error message `fusermount: option allow_other only allowed if 'user_allow_other' is set in /etc/fuse.conf` is displayed, uncomment the following line in `/etc/fuse.conf`:

```
user_allow_other

```

Other `vmhgfs-fuse` mount options can be viewed by using the `-h` input flag:

```
# vmhgfs-fuse -h

```

##### fstab

Add a rule for each share:

 `/etc/fstab` 
```
.host:/*<shared_folder>* *<shared folders root directory>* fuse.vmhgfs-fuse nofail,allow_other 0 0

```

Create and mount the Shared Folders:

```
# mkdir *<shared folders root directory>*
# mount *<shared folders root directory>*

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

Ensure the `*<shared folders root directory>*` folder exists on the system. If this folder does not exist then it must be created, as the systemd service depends on it:

```
# mkdir -p *<shared folders root directory>*

```

[Enable](/index.php/Enable "Enable") the `<shared folders root directory>-<shared_folder>.service` mount target.

If all shared folders should be mounted automatically then omit *<shared_folder>*.

### Legacy Shared Folders with vmhgfs module

**Note:** This functionality is only available in VMware Workstation and Fusion

Share a folder by selecting *Edit virtual machine settings > Options > Shared Folders > Always enabled*, and creating a new share.

Ensure the `vmhgfs` driver is loaded:

```
# modprobe vmhgfs

```

The shared folders should be viewable with:

```
$ vmware-hgfsclient

```

Now the folder can be mounted:

```
# mkdir /home/user1/shares
# mount -n -t vmhgfs .host:/*<shared_folder>* /home/user1/shares

```

#### Enable at boot

Edit `mkinitcpio.conf` thusly:

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(... vmhgfs)
...
```

and then [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

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

For shared folders to work the `vmhgfs` driver must be loaded. Create the following `.service`s:

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

Ensure the `*<shared folders root directory>*` folder exists on the system. If this folder does not exist then it must be created, as the systemd scripts depend on it:

```
# mkdir -p *<shared folders root directory>*

```

[Enable](/index.php/Enable "Enable") the `mnt-hgfs.automount` mount target.

If all shared folders should be mounted automatically then omit *<shared_folder>*.

#### Prune mlocate DB

When using [mlocate](/index.php/Mlocate "Mlocate"), it is pointless to index the shared directories in the `locate DB`. Therefore, add the directories to `PRUNEPATHS` in `/etc/updatedb`.

### 3D Acceleration

If not selected at guest creation time, 3D Acceleration can be enabled in: *Edit virtual machine settings > Hardware > Display > Accelerate 3D graphics*.

**Note:** Xorg can be very slow with 3D Acceleration enabled. It some cases, llvmpipe software rendering is much faster.

#### OpenGL and GLSL support

It is possible to update OpenGL and GLSL with new kernel modules, overriding Arch-controlled versions.

Currently, OpenGL 3.3 and GLSL 3.30 can be supported. See [https://bbs.archlinux.org/viewtopic.php?id=202713](https://bbs.archlinux.org/viewtopic.php?id=202713) for more details.

### Time synchronization

Configuring time synchronization in a Virtual Machine is important; fluctuations are bound to occur more easily in a guest VM. This is mostly due to the CPU being shared by more than one guest.

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

To improve the performance of your virtual machine, try the following tips:

#### Paravirtual SCSI adapter

[VMware Paravirtual SCSI (PVSCSI) adapters](http://kb.vmware.com/kb/1010398) are high-performance storage adapters for VMware ESXi that can result in greater throughput and lower CPU utilization. PVSCSI adapters are best suited for environments, where hardware or applications drive a very high amount of I/O throughput.

The SCSI adapter type `VMware Paravirtual` is available in the Virtual Machine settings.

If these settings are not in the virtual machine's configuration, the paravirtual SCSI adapter can still be enabled. Ensure that the paravirtual SCSI adapter is included in the kernel image by modifying the `mkinitcpio.conf`:

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(... vmw_pvscsi)
...
```

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

Shut down the virtual machine and change the SCSI adapter: set the `.vmx` to the following:

```
scsi0.virtualDev = "pvscsi"

```

#### Paravirtual Network Adapter

VMware offers [multiple network adapters](http://kb.vmware.com/kb/1001805) for the guest OS. The default adapter used is usually the `e1000` adapter, which emulates an Intel 82545EM Gigabit Ethernet NIC. This Intel adapter is generally compatible with the built-in drivers across most operating systems, including Arch.

For [more performance and additional features](http://rickardnobel.se/vmxnet3-vs-e1000e-and-e1000-part-1/) (such as multiqueue support), the VMware native `vmxnet3` network adapter can be used.

Arch has the `vmxnet3` kernel module available with a default install. Once enabled in [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") (or if it is auto-detected; check by running `lsmod | grep vmxnet3` to see if it is loaded), shut down and change the network adapter type in the *.vmx* file to the following:

```
ethernet0.virtualDev = "vmxnet3"

```

After changing network adapters, the network and [dhcpcd](/index.php/Dhcpcd "Dhcpcd") settings will need to be updated to use the new adapter name and MAC address.

```
# dhcpcd *new_interface_name*
# systemctl enable dhcpcd@*new_interface_name*.service

```

The new interface name can be obtained by running `ip link`.

#### Virtual Machine Settings

These settings could help improve the responsiveness of the virtual machine by reducing disk I/O, at the expense of using more host memory. [Vmware's KB1008885](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1008885) provides the following optimizations:

```
mainMem.useNamedFile = "FALSE"
MemTrimRate = "0"
prefvmx.useRecommendedLockedMemSize = "TRUE"
MemAllowAutoScaleDown = "FALSE"
sched.mem.pshare.enable = "FALSE"

```

*   **mainMem.useNamedFile**: This will only work for Windows hosts and this parameter can be used if high disk activity is experienced upon shutting down the virtual machine. This will prevent VMware from creating a *.vmem* file. Use *mainmem.backing = "swap"* on Linux hosts instead.
*   **MemTrimRate**: This setting prevents that memory which was released by the guest is released on the host also.
*   **prefvmx.useRecommendedLockedMemSize**: Unfortunately there does not seem to exist a proper explanation for this setting; it seems to prevent the host system from swapping parts of the guest memory.
*   **MemAllowAutoScaleDown**: Prevents VMware from adjusting the memory size of the virtual machine if it cannot allocate enough memory.
*   **sched.mem.pshare.enable**: If several virtual machines are running simultaneously, VMware will try to locate identical pages and share these between the virtual machines. This can be very I/O intensive.

The following settings can also be set in the configuration dialog of VMware Workstation(*Edit -> Preferences... -> Memory/Priority*).

```
prefvmx.minVmMemPct = "100"
mainMem.partialLazySave = "FALSE"
mainMem.partialLazyRestore = "FALSE"

```

*   **prefvmx.minVmMemPct**: Sets amount of RAM in percent which should be reserved by the virtual machine on the host system. If this is set to a lower value it is possible to assign the virtual machine more memory than is available in the host system. Be careful though, as in this case it will most likely lead to excessive hard drive usage. If enough RAM is on the host system, this value should be left at 100.
*   **mainMem.partialLazySave** and **mainMem.partialLazyRestore**: These two parameters will prevent the virtual machine from creating partial snapshots for suspends. When these parameters are used, virtual machine suspension will take slightly longer, but there should be less hard disk activity from VMware trying to store this information.

## Troubleshooting

### Network slow on guest

Arch Linux, as well as other Linux guests, may have slow network speeds while using NAT. To resolve this, switch the network type to **Bridged mode** in the guest settings on the host, changing the configuration file for the network on the guest where necessary. For more information on configuration, see [Network configuration](/index.php/Network_configuration "Network configuration"). If on a Windows host and it is not connecting properly despite correct guest configuration, open the **Virtual Network Editor** on the host as **Administrator** and press the **Restore defaults** button at the bottom left.

### File share problems with legacy vmhgfs module and newer kernels

As the [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) package is no longer being updated, newer kernels are not patched correctly using it to be compatible with a host-guest file share. The [Github repository](https://github.com/davispuh/open-vm-tools-dkms) has some patch files that can be manually applied to restore functionality.

It is also recommended that the AUR comment section be checked for this package.

### Sound problems

If unacceptably loud or annoying sounds occur, then it may be related to the [PC speaker](/index.php/PC_speaker "PC speaker"). The issue may be resolved by disabling the PC speaker within the guest image:

```
 # echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf

```

### Mouse problems

The following problems may occur with the mouse:

*   The automatic grab/ungrab feature does not automatically grab input when the cursor enters the window
*   Missing buttons
*   Input lag
*   Clicks are not registered in some applications
*   Mouse cursor jumps when entering/leaving virtual machine
*   Mouse position jumps to where it left the guest VM

These may be fixed by [uninstalling](/index.php/Uninstall "Uninstall") the [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse) package. [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse) and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) should be sufficient for handling mouse and keyboard inputs.

Adding settings to the `.vmx` configuration file may help ([Mouse position jumps to where it left the guest VM](https://forums.mageia.org/en/viewtopic.php?f=7&t=7977)):

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx` 
```
mouse.vusb.enable = "TRUE"
mouse.vusb.useBasicMouse = "FALSE"
```

VMware also attempts to automatically optimize the mouse for gaming. If problems are experienced, disabling the optimization is recommended: *Edit > Preferences > Input > Optimize mouse for games: Never*

Alternatively, attempting to [disable](http://www.spinics.net/lists/xorg/msg53932.html) the `catchall` event in `60-libinput.conf` may be required:

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

The following errors may be displayed if VMWare's memory hot-add feature is enabled:

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

"Autofit" means that when the VMWare window's size is adjusted in the host, ArchLinux in the guest should automatically follow and readjust its resolution to fit the new size of the host window.

#### Potential solution 1

Ensure autofit is enabled. For VMware Workstation the setting can be found in: *View -> Autosize -> Autofit Guest*

#### Potential solution 2

For some reason, autofit requires the packages **gtkmm** and **gtk2**, so ensure they are installed. If X windows is not installed or a non–GTK-based desktop environment (such as KDE) is being used, the might have to be installed independently.

#### Potential solution 3

The relevant modules may have to be added to mkinitcpio.conf:

 `/etc/mkinitcpio.conf`  `MODULES=(vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx)` 

Do not forget to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

#### Potential solution 4

[Enable](/index.php/Enable "Enable") `vmtoolsd.service`.

If this doesn't work, ensure the `vmtoolsd.service` is [restarted](/index.php/Restart "Restart").

#### Potential solution 5

If [GNOME](/index.php/GNOME "GNOME") is running on [Wayland](/index.php/Wayland "Wayland"), [install](/index.php/Install "Install") [xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware) ([FS#57473](https://bugs.archlinux.org/task/57473)).

See [[1]](https://github.com/vmware/open-vm-tools/issues/22#issuecomment-362705505).

### Drag and drop, copy/paste

**Tip:** There is an unspecified relationship between these features and *gtkmm3* that causes them to silently fail. This is documented in [FS#43159](https://bugs.archlinux.org/task/43159).

The drag-and-drop (copy/paste) feature requires both [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) and [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3) packages to be installed.

Make the command `vmware-user` run after [X11](/index.php/X11 "X11") by either:

*   Ensuring `etc/xdg/autostart/vmware-user.desktop` exists, and if not, running:

```
# cp /etc/vmware-tools/vmware-user.desktop /etc/xdg/autostart/vmware-user.desktop

```

OR

*   Add `vmware-user` to [Xinitrc](/index.php/Xinitrc "Xinitrc").

### Problems when running as a shared VM on Workstation 11

Workstation 11 has a bug where vmware-hostd crashes if an Arch guest is running as a shared VM and vmtoolsd is running in the guest. A patch to open-vm-tools to work around the bug is [here](https://github.com/vmware/open-vm-tools/issues/31).

### Shared folder not mounted after system upgrade

Most likely, this should only happen to [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools). Since the `vmhgfs` module belongs to [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/), the legacy filesystem driver would not be upgraded by using the command `pacman -Syu`. Therefore, [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) should be manually upgraded before the official repositories.

If a shared folder is not mounted after a system upgrade, then remove the shared filesystem automount, upgrade [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/), run `pacman -Syu`, and finally [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs"). Don't forget to restore the filesystem automount.