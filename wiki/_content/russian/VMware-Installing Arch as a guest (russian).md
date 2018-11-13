Related articles

*   [VMware](/index.php/VMware "VMware")
*   [Installing VMWare vCLI](/index.php/Installing_VMWare_vCLI "Installing VMWare vCLI")

Эта статья посвящена установке Arch Linux в продукт [VMware](/index.php/VMware "VMware") , такой как [Player (Plus)](http://www.vmware.com/products/player/), [Fusion](http://www.vmware.com/products/fusion/) или [Workstation](http://www.vmware.com/products/workstation/).

## Contents

*   [1 Встроенные драйверы](#Встроенные_драйверы)
*   [2 VMware Tools versus Open-VM-Tools](#VMware_Tools_versus_Open-VM-Tools)
*   [3 Open-VM-Tools](#Open-VM-Tools)
    *   [3.1 Utilities](#Utilities)
    *   [3.2 Modules](#Modules)
    *   [3.3 Установка](#Установка)
        *   [3.3.1 Многопользовательская цель](#Многопользовательская_цель)
        *   [3.3.2 Graphical Target](#Graphical_Target)
    *   [3.4 Resolution update on window resize](#Resolution_update_on_window_resize)
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
    *   [7.1 Sound problems](#Sound_problems)
    *   [7.2 Mouse problems](#Mouse_problems)
    *   [7.3 Boot problems](#Boot_problems)
        *   [7.3.1 Slow boot time](#Slow_boot_time)
        *   [7.3.2 Shutdown/Reboot hangs](#Shutdown/Reboot_hangs)
    *   [7.4 Window resolution autofit problems](#Window_resolution_autofit_problems)
        *   [7.4.1 Potential solution 1](#Potential_solution_1)
        *   [7.4.2 Potential solution 2](#Potential_solution_2)
        *   [7.4.3 Potential solution 3](#Potential_solution_3)
    *   [7.5 Drag and drop, copy/paste](#Drag_and_drop,_copy/paste)
    *   [7.6 Problems when running as a shared VM on Workstation 11](#Problems_when_running_as_a_shared_VM_on_Workstation_11)
    *   [7.7 Shared folder not mounted after system upgrade](#Shared_folder_not_mounted_after_system_upgrade)

## Встроенные драйверы

*   `vmw_balloon` - Драйвер управления физической памятью. Он действует как «воздушный шар», который можно раздувать, чтобы восстановить физические страницы, зарезервировав их в гостевой комнате и аннулируя их на мониторе, освобождая лежащие в основе страницы машины, чтобы они могли быть выделены другим гостям. Он также может быть дефлирован, чтобы позволить гостю использовать больше физической памяти. Выделенная память виртуальной машины может быть повторно использована на хосте, не прерывая гостя.
*   `vmw_pvscsi` - Для VMware's Paravirtual SCSI (PVSCSI) HBA.
*   `vmw_vmci` - Интерфейс связи виртуальной машины. Он обеспечивает высокоскоростную связь между хостом и гостем в виртуальной среде с помощью виртуального устройства VMCI.
*   `vmwgfx` - Для 3D-ускорения. Это драйвер DRM с поддержкой KMS для виртуального оборудования VMware SVGA2.
*   `vmxnet3` - Для виртуального сетевого адаптера VMware's vmxnet3.
*   a fuse-based hgfs implementation has been added to `open-vm-tools` 10.0+ and is supported from kernel version 4.0+.

These drivers are only needed if you are running Arch Linux on a hypervisor like [VMware vSphere Hypervisor](http://www.vmware.com/products/vsphere-hypervisor). Client-server applications can write to the VMCI Sock (vsock) interface to make use of the VMCI virtual device, when communicating between virtual machines.

*   `vsock` - The Virtual Socket Protocol. It is similar to the TCP/IP socket protocol, allowing communication between Virtual Machines and hypervisor or host.
*   `vmw_vsock_vmci_transport` - Implements a VMCI transport for Virtual Sockets.

**Note:** Arch's [Udev](/index.php/Udev "Udev") auto-detects and enables a few of these modules. Additional modules, such as `vmw_balloon`, may need to be added to your [Mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `MODULES` list. For example: ` # cat /etc/mkinitcpio.conf` 
```
...
MODULES="... vmw_balloon vmw_pvscsi vsock vmw_vsock_vmci_transport ..."
```

Обязательно пересобирайте:

```
 # mkinitcpio -p linux

```

Some modules, such as the legacy `vmhgfs` shared folder module, will require additional work to manually `compile` and systemd `enable` in order to function properly.

## VMware Tools versus Open-VM-Tools

In 2007, VMware released large partitions of the [VMware Tools](http://kb.vmware.com/kb/340) under the LGPL as [Open-VM-Tools](http://sourceforge.net/projects/open-vm-tools/). The official Tools are not available [separately](http://packages.vmware.com/tools/esx/latest/repos/index.html) for Arch Linux.

Originally, VMware Tools provided the best drivers for network and storage, combined with the functionality for other features such as time synchronization. However, for quite a while now the drivers for the network/SCSI adapter are part of the Linux kernel, and VMware Tools is only needed for extra features like Unity mode.

Both VMware Tools and Open-VM-Tools require the installation of [xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware).

## Open-VM-Tools

### Utilities

[open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) пакет поставляется со следующими утилитами:

*   `vmtoolsd` - Служба, ответственная за отчет о статусе виртуальной машины.
*   `vmware-checkvm` - Инструмент для проверки, запущена ли программа в гостевой системе.
*   `vmware-toolbox-cmd` - Инструмент для получения информации о виртуальной машине хоста.
*   `vmware-user-suid-wrapper` - Инструмент, позволяющий совместное использование буфера обмена (копирование / вставка) между хостом и гостем.
*   `vmware-vmblock-fuse` - Утилита файловой системы. Включает функции перетаскивания между хостом и гостем через [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (Filesystem in Userspace).
*   `vmware-xferlogs` - Дамп протоколирует / отлаживает информацию в лог-файл виртуальной машины.
*   `vmhgfs-fuse` - Утилита для установки общих папок vmhgfs.

### Modules

The [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) package comes with the following modules:

*   `vmhgfs` - Legacy filesystem driver. Enables legacy sharing implementation between host and guest.
*   `vmxnet` - for the old VMXNET network adapter.

### Установка

[Install](/index.php/Install "Install") the [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools). Если вы хотите использовать общие папки, вам также необходимо установить [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) package.

Open-VM-Tools читает информацию о версии из `/etc/arch-release`, который пуст:

```
# cat /proc/version > /etc/arch-release

```

#### Многопользовательская цель

Если вы загружаетесь в `multi-user.target` затем следуйте приведенным здесь шагам. Если вы загружаетесь в graphical.target, пропустите этот раздел и прочитайте инструкции для `graphical.target`.

[Start](/index.php/Start "Start") `vmtoolsd.service` и при необходимости активировать его при загрузке.

#### Graphical Target

If you are booting into a graphical environment then follow these steps to enable the VMware tools.

Enable the `vmware-vmblock-fuse.service` Systemd service.

If you have installed [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) then you should enable the `dkms.service` Systemd service which automatically recompiles the kernel modules after a kernel update.

Try to install [gtkmm](https://www.archlinux.org/packages/?name=gtkmm) manually if it does not work properly.

### Resolution update on window resize

[Start](https://bbs.archlinux.org/viewtopic.php?pid=1081629#p1081629) `/usr/bin/vmware-user-suid-wrapper` from within X.

## Official VMware Tools

### Modules

*   `vmblock` - Filesystem driver. Enables drag & drop functionality between host and guest ([superseded](https://www.mail-archive.com/open-vm-tools-devel@lists.sourceforge.net/msg00213.html) by the `vmware-vmblock-fuse` utility).
*   `vmci` - High performance communication interface between host and guest.
*   `vmmon` - Virtual Machine Monitor.
*   `vmnet` - Networking driver.
*   `vsock` - VMCI sockets.

**Note:** There is no module for `vmware-vmblock-fuse`, and `vmblock` has been removed from the kernel unless you disable `fuse`. Instead, systemd services need to be `enabled` to allow these functions. See instructions below.

### Installation (from guest)

Install the dependencies: [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) (for building), [net-tools](https://www.archlinux.org/packages/?name=net-tools) (for `ifconfig`, used by the installer) and [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (for kernel headers).

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

Enable `vmware-vmblock-fuse` systemd services:

```
 # abs community/open-vm-tools
 # cp /var/abs/community/open-vm-tools/vmware-* /usr/lib/systemd/system
 # systemctl enable vmware-vmblock-fuse.service

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
.host:/*<shared_folder>* */home/user1/shares* fuse.vmhgfs-fuse defaults 0 0

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
ExecStart=
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

### Drag and drop, copy/paste

The drag-and-drop (copy/paste) feature requires both [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) and [gtkmm](https://www.archlinux.org/packages/?name=gtkmm) packages to be installed in order to work.

`/etc/xdg/autostart/vmware-user.desktop` may try to start *vmware-user-suid-wrapper* properly when you log in, but there is an unspecified relationship between it and *gtkmm* that causes it to silently fail. This is documented in [FS#43159](https://bugs.archlinux.org/task/43159).

### Problems when running as a shared VM on Workstation 11

Workstation 11 has a bug where vmware-hostd crashes if an Arch guest is running as a shared VM and vmtoolsd is running in the guest. A patch to open-vm-tools to work around the bug is [here](https://github.com/vmware/open-vm-tools/issues/31).

### Shared folder not mounted after system upgrade

This is probably only happens to [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools). Since the vmhgfs module belongs to [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) which belongs to AUR repositiory, therefore would not get's updated automatically by the `pacman -Syu` command. Always update the [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) manually before the system upgrade.

If you happened to get in to this situation, you need to remove the automount for shared file system, upgrade and do a `mkinitcpio -p linux`.