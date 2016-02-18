Tento článek pojednává o provozování VirtualBoxu v Archu, možná vás bude zajímat [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")

[VirtualBox](http://www.virtualbox.org) je emulátor virtuálního PC jako [vmware](/index.php/Vmware "Vmware"). Obsahuje plno vlastností integrovaných ve vmware, stejně jako své vlastní. Je v neustálém vývoji a nové vlastnosti postupně přibývají. Verze 2.2 například přinesla podporu 3D OpenGL akcelerace pro hostované Linux a Solaris systémy. Má přehledné grafické uživatelské rozhraní (Qt a/nebo SDL) a je možné jej obsluhovat přes příkazovou řádku. VirtualBox umožňuje běh iTunes jako v sučasnosti v podstatě jedinou možnost, jak synchronizovat iPod Touch nebo iPhone s verzí 3.0 nebo vyšší.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Spuštění VirtualBoxu](#Spu.C5.A1t.C4.9Bn.C3.AD_VirtualBoxu)
*   [3 Nastavení](#Nastaven.C3.AD)
    *   [3.1 Nastavení sítě](#Nastaven.C3.AD_s.C3.ADt.C4.9B)
        *   [3.1.1 NAT](#NAT)
        *   [3.1.2 Síťový most](#S.C3.AD.C5.A5ov.C3.BD_most)
    *   [3.2 Přídavky pro hosta](#P.C5.99.C3.ADdavky_pro_hosta)
        *   [3.2.1 Host s Arch Linuxem](#Host_s_Arch_Linuxem)
        *   [3.2.2 Windows guests](#Windows_guests)
    *   [3.3 Keyboard and mouse between the host and the guest](#Keyboard_and_mouse_between_the_host_and_the_guest)
    *   [3.4 Using full resolution of the host system in the guest](#Using_full_resolution_of_the_host_system_in_the_guest)
    *   [3.5 Sharing folders between the host and the guest](#Sharing_folders_between_the_host_and_the_guest)
    *   [3.6 Getting audio to work in the guest machine](#Getting_audio_to_work_in_the_guest_machine)
    *   [3.7 Setting up the RAM and video memory for the guest](#Setting_up_the_RAM_and_video_memory_for_the_guest)
    *   [3.8 Setting up CD-ROM for the guest](#Setting_up_CD-ROM_for_the_guest)
    *   [3.9 Enabling D3D acceleration in Windows guests](#Enabling_D3D_acceleration_in_Windows_guests)
*   [4 Virtualized OS setup](#Virtualized_OS_setup)
    *   [4.1 Test a liveCD/DVD](#Test_a_liveCD.2FDVD)
*   [5 Maintenance](#Maintenance)
    *   [5.1 Rebuild the vboxdrv module](#Rebuild_the_vboxdrv_module)
    *   [5.2 Compact a disk image](#Compact_a_disk_image)
    *   [5.3 Increase the size of a virtual hard drive for a Windows guest](#Increase_the_size_of_a_virtual_hard_drive_for_a_Windows_guest)
    *   [5.4 Windows Xp and Nokia phones](#Windows_Xp_and_Nokia_phones)
*   [6 Migrating from another VM](#Migrating_from_another_VM)
    *   [6.1 Converting from QEMU images](#Converting_from_QEMU_images)
    *   [6.2 Converting from VMware images](#Converting_from_VMware_images)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Getting Web-cams and other USB devices to detect](#Getting_Web-cams_and_other_USB_devices_to_detect)
    *   [7.2 Sending a CTRL+ALT+F1 to the Guest](#Sending_a_CTRL.2BALT.2BF1_to_the_Guest)
    *   [7.3 Starting VMs at system boot on headless servers](#Starting_VMs_at_system_boot_on_headless_servers)
    *   [7.4 Guest managament daemon](#Guest_managament_daemon)
    *   [7.5 Accessing server on VM from host](#Accessing_server_on_VM_from_host)
    *   [7.6 DAEMON Tools](#DAEMON_Tools)
    *   [7.7 Using VirtualBox on a USB key](#Using_VirtualBox_on_a_USB_key)
    *   [7.8 phpVirtualBox](#phpVirtualBox)
*   [8 External links](#External_links)

## Instalace

	[virtualbox](https://www.archlinux.org/packages/?name=virtualbox)

	Obsahuje základní balík licencovaný podle GPL, k nalezení je v community repositáři.

	[virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/)

	Tento podle PUEL licencovaný rozšiřující balík je dostupný zdarma pro soukromé použití jednotlivcem. Je možné jej stáhnout z [AUR](/index.php/AUR "AUR"). Obsahuje RPD server, podporuje USB 2.0 a PXE bootování na Intel síťových kartách.

Instalace základního balíčku:

```
# pacman -S virtualbox

```

Volitelně je možné nainstalovat [qt4](https://www.archlinux.org/packages/?name=qt4) pro možnost využívat GUI:

```
# pacman -S qt4

```

## Spuštění VirtualBoxu

Přiřazení uživatele do **vboxusers' skupiny:**

```
# gpasswd -a USERNAME vboxusers

```

Sestavení potřebných modulů:

```
# /etc/rc.d/vboxdrv setup

```

Nakonec je záhodno editovat `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` a pří)idat *vboxrv* do sekce MODULES, aby se modul ovladače načetl při příštím spuštění:

```
MODULES=(... *vboxdrv*)

```

Pro načtení modulu ručně na vyžádádání:

```
# modprobe vboxdrv

```

Spuštění Virtualboxu:

```
$ VirtualBox

```

## Nastavení

### Nastavení sítě

Virtuální počítače ve Virtualboxu mohou být do sítě připojeny různými metodami; zejména pomocí [#NAT](#NAT) a [#Síťový most](#S.C3.AD.C5.A5ov.C3.BD_most). Právě [#NAT](#NAT) je nejjednodušší možností a je výchozí pro nově vytvořené virtuální stroje.

[Manuál VirtualBoxu](http://www.virtualbox.org/manual/UserManual.html) popisuje možnosti síťování. Ty jsou právě tam přesně popsány a jsou platné pro většinu operačních systémů.

#### NAT

Nastacení ve Virtualboxu:

*   ve volbě "Nastavení" virtuálního počítače
*   zvolit panel *Síť* z možností nalevo
*   jako *Připojena k* zvolte možnost *NAT*

Virtualbox obsahuje DHCP server a umožňuje tak nastavit podřízené systémy pomocí DHCP. IP adresa v NATu první síťového adaptéru je 10.0.2.0, 10.0.3.0 pro další a tak dále.

#### Síťový most

Síťový most je možné nastavit několika způsoby; jedná se o jednoduché nastavení za cenu omezených možností kontroly. Další možnosti jsou uvedené v [Pokročilé nastavení sítě Virtualbox](/index.php?title=Pokro%C4%8Dil%C3%A9_nastaven%C3%AD_s%C3%ADt%C4%9B_Virtualbox&action=edit&redlink=1 "Pokročilé nastavení sítě Virtualbox (page does not exist)"). V novějších verzích je možné propojit síťovým mostem rozhraní mezi hostem a hostitelským bezdrátovým rozhraním bez využití klihoven a nástrojů třetích stran.

Před dalším pokračováním je nutné načíst potřebné moduly:

```
# modprobe vboxnetflt

```

Ve Virtualboxu:

*   v nabídce *Nastavení* virtuálního počítače
*   zvolte *Síť* z levého menu
*   u *Připojena k* zvolte *Síťový most*
*   v *Název* vyberte síťové rozhraní připojení k síti, které má být využito pro připojení virtuálního počítače

Spusťte virtuální počítač a nastavte jej jako obvykle; za pomocí DHCp nebo staticky.

### Přídavky pro hosta

Přídavky pro hosta umožňují sdílení složek, zlepšují podporu akcelerace grafického rozhraní a zpřístupňují obou-směrnou schránku mezi hostem a hostitelem. Integrace myši je další funkcionalitou, která odstraňuje nutnost přepínat myš mezi hostem a hostitelem.

#### Host s Arch Linuxem

Více v [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest")

#### Windows guests

After installing Windows (XP etc.) on your virtual machine, simply select *Devices → Install Guest Additions...*

This will mount the iso image and windows should then automatically launch the guest additions installer. Follow the instructions to the end.

### Keyboard and mouse between the host and the guest

*   To capture the keyboard and mouse, click the mouse inside the virtual machine display.
*   To uncapture, press right `Ctrl`.

To get seamless mouse integration between host and guest, install the [#Guest Additions](#Guest_Additions) inside the guest.

When generating the guests' `xorg.conf` with `X -configure`, the InputDevice section may feature the `mouse` driver. After installing the Guest Additions, replace `mouse` with `vboxmouse` and then restart X or reboot the guest.

Alternatively, add the following to the guest's `xorg.conf`:

```
Section "InputDevice"
   Identifier   "Mouse0"
   Driver       "vboxmouse"
   Option       "Protocol" "auto"
   Option       "Device" "/dev/input/mice"
   Option       "ZAxisMapping" "4 5 6 7"
EndSection

Section         "ServerLayout"
   Identifier   "X.org Configured"
   Screen     0 "Screen0" 0 0
   InputDevice  "Mouse0" "CorePointer"
   InputDevice  "Keyboard0" "CoreKeyboard"
EndSection

```

### Using full resolution of the host system in the guest

Set the resolution of your guest in the grub boot script `/boot/grub/menu.lst`, i.e. add the correct vga code to the kernel command line. For a resolution of 1280x1024, this would e.g. look like

```
# kernel /vmlinuz26 root=/dev/disk/by-uuid/7bdc5dee-8fb0-4260-bc43-60ac6e4e4a54 ro vga=795

```

Add the resolution to `/etc/X11/xorg.conf`, e.g.

```
Section "Screen"
...
	SubSection "Display"
		Viewport   0 0
		Depth     24
		Modes "1280x1024" "1024x768"
	EndSubSection
...
EndSection

```

If you experience problems with your resolution dropping back to second lower resolution in the 'Modes' setting, simply omit the second resolution. Example

```
               Modes "1280x1024"

```

### Sharing folders between the host and the guest

In the settings of the virtual machine go to shared folders tab and add the folders you want to share.

*   NOTE: You need to install Guest Additions in order to use this feature.

```
In a Linux host, *Devices → Install Guest Additions*
Yes (when asked to download the CD image)
Mount (when asked to register and mount)

```

In a Linux host, create one or more folders for sharing files, then set the shared folders via the virtualbox menu (guest window).

In a Windows guest, starting with VirtualBox 1.5.0, shared folders are browseable and are therefore visible in Windows Explorer. Open Windows Explorer and look for it under *My Networking Places → Entire Network → VirtualBox Shared Folders*.

Launch the windows explorer (run explorer command) to browse the network places -> expand with the (+) sign : entire network → VirtualBox shared folders → **\\Vboxsvr** → then you can now expand all your configured shared folders here, and set up shortcuts for linux folders in the guest filesystem. You can alternatively use the "Add network place wizard", and browse to "VBoxsvr".

Alternatively, on the Windows command line, you can also use the following:

```
net use x: \\VBOXSVR\sharename

```

While `VBOXSVR` is a fixed name, replace `x:` with the drive letter that you want to use for the share, and sharename with the share name specified with VBoxManage.

In a Windows guest, to improve loading and saving files (e.g. MS Office) by VirtualBox Shared Folders edit *c:\windows\system32\drivers\etc\hosts* as below:

```
127.0.0.1 localhost vboxsvr

```

In a Linux guest, use the following command:

```
# mount -t vboxsf [-o OPTIONS] sharename mountpoint
  (Notes: sharename is optional or same as selected in the VirtualBox-Dialog , mountpoint of the shared directory in the hosts filesystem)

```

	Automatically mounting a shared folder is possible through the linux-guest /etc/fstab file. You may also specify the uid=#,gid=# (where # is replaced by the actual numerical uid and gid) to mount the share with normal user permissions instead of root permissions. (this can be helpful to mount parts of your host ~/home for use in your linux-guest. To do this add an entry in the following format to the linux-guest /etc/fstab:

```
sharename mountpoint vboxsf uid=#,gid=# 0 0

```

Replace `sharename` with the share name specified with VBoxManage, and mountpoint with the path where you want the share to be mounted (e.g. /mnt/share). The usual mount rules apply, that is, create this directory first if it does not exist yet.

Beyond the standard options supplied by the mount command, the following are available:

```
iocharset=CHARSET

```

to set the character set used for I/O operations (utf8 by default) and

```
convertcp=CHARSET

```

to specify the character set used for the shared folder name (utf8 by default).

### Getting audio to work in the guest machine

In the machine settings, go to the audio tab and select the correct driver according to your sound system (ALSA, OSS or PulseAudio).

### Setting up the RAM and video memory for the guest

You can change the default values by going to *Settings → General*.

### Setting up CD-ROM for the guest

You can change the default values by going to *Settings → CD/DVD-ROM*.

Check mount CD/DVD drive and select one of the following options.

### Enabling D3D acceleration in Windows guests

Recent versions of Virtualbox have support for accelerating OpenGL inside guests. This can be enabled with a simple checkbox in the machine's settings, right below where video ram is set, and installing the Virtualbox guest additions. However, most Windows games use Direct3D (part of DirectX), not OpenGL, and are thus not helped by this method. However, it is possible to gain accelerated Direct3D in your Windows guests by borrowing the d3d libraries from Wine, which translate d3d calls into OpenGL, which is then accelerated.

After enabling OpenGL acceleration as described above, go to [http://www.nongnu.org/wined3d/](http://www.nongnu.org/wined3d/) in your Windows guest and grab the "Latest version (Installer):". Reboot the guest into safe mode (press F8 before the Windows screen appears but after the Virtualbox screen disappears), and install wined3d, accepting the defaults during the install. (You may check the box for DirectX 10 support if you like, dont touch anything else.) Reboot back to normal mode and you should have accelerated Direct3D.

**Note:** This hack may or may not work for some games depending on what hardware checks they make and what parts of D3D they use.

**Note:** This has only been tried on Windows XP and Windows 7 RC guests AFAIK, and does not work on the Windows 7 guest. If you have experience with this on a different windows version, please add that data here.

## Virtualized OS setup

Virtualbox needs to be setup to virtualize another operating system.

### Test a liveCD/DVD

Click the 'New' button to create a new virtual environment. Name it appropriately and select Operating System type and version. Select base memory size (note: most operating systems will need at least 512MB to function properly). Create a new hard disk image (a hard disk image is a file that will contain the operating system's filesystem and files).

When the new image has been created, click 'Settings', then CD/DVD-ROM, check 'Mount CD/DVD Drive' then select an ISO image.

## Maintenance

### Rebuild the vboxdrv module

Note that any time your kernel version changes (due to an upgrade, recompile, etc.) you must also rebuild the VirtualBox kernel modules.

Ensure that *kernel26-headers* is still installed, and run the following command:

```
# /etc/rc.d/vboxdrv setup

```

This will build the VirtualBox kernel modules for the *currently running kernel*; if you have just upgraded your kernel package, reboot before trying to rebuild your kernel modules.

After rebuilding the module, do not forget to load it with

```
# modprobe vboxdrv

```

*vboxdrv* and *vboxnetflt* should be in the MODULES=() section of your /etc/rc.conf

If you are using an old virtualbox_bin package built from AUR, run:

```
# vbox_build_module

```

If you need to rebuild the Virtual Box Additions in a guest installation of Arch Linux, use this command:

```
# /etc/rc.d/rc.vboxadd setup

```

### Compact a disk image

See [How to compact a VirtualBox virtual disk image (VDI)](http://my.opera.com/locksley90/blog/2008/06/01/how-to-compact-a-virtualbox-virtual-disk-image-vdi)

### Increase the size of a virtual hard drive for a Windows guest

WARNING: ONLY TESTED WITH XP GUEST!

If you find that you are running out of space due to the small hard drive size you selected when created your VM, you can take the following steps:

Create a new vdi in ~/.VirtualBox/HardDisks by running:

```
# cd ~/.VirtualBox/HardDisks
# VBoxManage createhd -filename new.vdi --size 10000 --remember

```

where size is in mb, in this example 10000MB ~= 10GB, and new.vdi is name of new hard drive to be created.

Next the old vdi needs to be cloned to the new vdi, this may take some time so wait while it occurs:

```
# VBoxManage clonehd old.vdi new.vdi --existing

```

Detach old harddrive and attach new hard drive, replace VMName with whatever you called your VM:

```
# VBoxManage modifyvm VMName --hda none
# VBoxManage modifyvm VMName --hda new.vdi

```

Boot the VM, run Partition Wizard 5 to resize the partition on the fly, and reboot.

Remove old vdi from VirtualBox and delete

```
# VBoxManage closemedium disk old.vdi
# rm old.vdi

```

### Windows Xp and Nokia phones

To get working Windows XP and Nokia phones with Pc Suite mode, Virtualbox needs two simple steps:

**1.** Add a rule to udev with `/etc/udev/rules.d/40-permissions.rules`:

```
LABEL="usb_serial_start"
ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", \
GROUP="usbfs", MODE="0660", GROUP="dialout"
LABEL="usb_serial_end"

```

**2.** Create the group usbfs and add its user to it

```
$ sudo groupadd usbfs
$ sudo usermod -a -G usbfs $USER

```

After a logout, connect a Nokia phone with PC Suite mode and start Windows XP to test new rule.

## Migrating from another VM

The `qemu-img` program can be used to convert images from one format to another, or add compression or encryption to an image.

```
  # pacman -S qemu

```

### Converting from QEMU images

To convert a QEMU image for use with VirtualBox, first convert it to *raw* format, then use VirtualBox's conversion utility to convert and compact it in its native format.

```
  $ qemu-img convert -O raw test.qcow2 test.raw
  $ VBoxManage modifyvdi /full/path/to/test.vdi compact
or 
  $ qemu-img convert -O raw test.qcow2 test.raw
    (of course you must have installed qemu package for that)
  $ VBoxManage convertfromraw /full/path/to/test.raw /full/path/to/test.vdi
  $ VBoxManage modifyvdi      /full/path/to/test.vdi compact

```

### Converting from VMware images

Do

```
  $ VBoxManage clonehd source.vmdk target.vdi --format VDI

```

This may not be needed anymore with recent virtualbox versions (to be confirmed)

## Tips and tricks

### Getting Web-cams and other USB devices to detect

Make sure you filter any devices that are not a keyboard or a mouse so they don't start up at boot and this insures that Windows will detect the device at start-up.

### Sending a CTRL+ALT+F1 to the Guest

If your guest O/S is a Linux distro, and you want to open a new tty text shell or exit X via typing `Ctrl`+`Alt`+`F1`, you can easily send this command to the guest O/S simply by hitting your 'Host Key' (usually the `Ctrl` in the Right side of your keyboard) + `F1` or `F2`, etc.

### Starting VMs at system boot on headless servers

Add this line to /etc/rc.local

```
exec /bin/su -c 'VBoxManage startvm --type headless <*UUID|NAME*>' *PREFERED_USER* >/dev/null 2>&1

```

Where <UUID|NAME> is the guest identifier, and PREFERRED_USER is the user profile that contains the VM definitions and .vdi files.

To determine the available VMs for a user:

```
su -c 'VBoxManage list vms' PREFERED_USER

```

To save the state of a running VM:

```
su -c 'VBoxManage controlvm <UUID|NAME> savestate' PREFERED_USER

```

### Guest managament daemon

Below is a [daemon](/index.php/Daemon "Daemon") for automating guest administration. Guests will be initialized on start, and state-saved on stop.

The configuration file:

 `/etc/conf.d/vbox_service` 
```
# Guests to manage:
#VB_GUESTS=('OpenBSD' 'Slackware' 'Windows XP')
#
# Disable a guest by prepending a bang:
#VB_GUESTS=('OpenBSD' 'Slackware' !'Windows XP')
#
# Default value matches none:
VB_GUESTS=()

# User to run Virtual Box as:
VB_USER='vbox'

```

The script:

 `/etc/rc.d/vbox_service` 
```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

unset VB_GUESTS
unset VB_USER
[[ -r /etc/conf.d/vbox_service ]] && . /etc/conf.d/vbox_service
[[ ${VB_GUESTS[@]} ]] || VB_GUESTS=()
[[ ${VB_USER[@]} ]]   || VB_USER='vbox'

match() {
 [[ $REPLY =~ $1 ]] && m=("${BASH_REMATCH[@]}")
}

vm_raw() {
 local argv=''
 printf -v argv ' %q ' "$@"
 su -c "/usr/bin/VBoxManage $argv" -s /bin/sh "$VB_USER"
}

vm_ls() {
 local -A out=''
 local -i ret=1

 local m=()
 while read -r; do
   match '^"(.+)" \{(.+)\}$'
   out[${m[1]}]=${m[2]}
 done < <(vm_raw list vms)

 local i=''
 for i in "${VB_GUESTS[@]##!*}"; do
   if [[ ${out[$i]} ]]; then
     printf ' %q ' "${out[$i]}"
     ret=0
   fi
 done

 return $ret
}

vm_envinit() {
 local m=()
 while read -r; do
   match '^(.+)="?([^"]+)'
   env[$1:${m[1]}]=${m[2]}
 done < <(vm_raw showvminfo --machinereadable "$1")
}

start() {
 if [[ ${env[$1:VMState]} != 'running' ]]; then
   vm_raw startvm --type headless "$1"
 fi
}

stop() {
 if [[ ${env[$1:VMState]} == 'running' ]]; then
   vm_raw controlvm "$1" savestate
 fi
}

restart() {
 stop "$1"
 sleep 3
 start "$1"
}

usage() {
 printf '%s
' "usage: $0 <start|stop|restart> [name|uuid]..." >&2
}

if [[ ! $1 =~ ^(start|stop|restart)$ ]]; then
  usage
  exit 2
fi
cmd=$1
shift || eval set -- "$(vm_ls)"

stat_busy "${cmd^}ing VMs:"
trap 'stat_die' ERR
set -Ee

declare -A env=''

for i; do
  [[ $i ]]
  vm_envinit  "$i"
  stat_append "${env[$i:name]}, "
  $cmd        "${env[$i:UUID]}" &>/dev/null
done

stat_done

```

### Accessing server on VM from host

To access apache on a VM from the Host machine ONLY, simply execute the following lines on the Host:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/HostPort" 8888
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/GuestPort" 80
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/Protocol" TCP

```

Where 8888 is the port the host should listen on and 80 is the port the VM will send Apache's signal on. To use a port lower than 1024 on the host machine changes need to be made to the firewall on the host machine. This can also be set up to work with SSH, etc.. by changing "Apache" to whatever service and using different ports.

Note: "pcnet" refers to the network card of the VM. If you use an Intel card in your VM settings change "pcnet" to "e1000"

*   from [[1]](http://mydebian.blogdns.org/?p=111)

It might also be necessary to allow connections from the outside to the server in your VM. E.g. if the guest OS is Arch, you may want to add the line

```
httpd: ALL

```

to your /etc/hosts.allow file.

### DAEMON Tools

While VirtualBox can mount ISO images without a problem, there are some image formats which cannot reliably be converted to ISO. For instance, ccd2iso ignores .ccd and .sub files, which can give disk images with broken files. cdemu, fuseiso, and MagicISO will do the same. In this case there is no choice but to use Daemon Tools inside VirtualBox.

Recent Daemon Tools versions won't install, so use this old one: [[2]](http://www.disc-tools.com/download/daemon347+hashcalc)

### Using VirtualBox on a USB key

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

### phpVirtualBox

An open source, AJAX implementation of the VirtualBox user interface written in PHP. As a modern web interface, it allows you to access and control remote VirtualBox instances. Much of its verbage and some of its code is based on the (inactive) vboxweb project. It allows the administrator to remotely, graphically, administer their virtual machines without having to log in to their headless VirtualBox servers.

This requires the PUEL edition for VirtualBox.

An installation guide is available here: [http://code.google.com/p/phpvirtualbox/wiki/Installation](http://code.google.com/p/phpvirtualbox/wiki/Installation)

Arch Linux users should uncomment these 2 extensions in */etc/php/php.ini*

```
extension=json.so
extension=soap.so

```

See also [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")

## External links

*   [VirtualBox User Manual](http://www.virtualbox.org/manual/UserManual.html)