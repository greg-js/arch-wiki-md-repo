[VirtualBox](http://www.virtualbox.org) egy virtuális PC emulátor, mint a [VMVare](http://www.vmware.com). Sok funkciója a VMware-ből ismert, de van néhány saját is. Ez állandó fejlesztésben van és új funkciókat valósítanak meg egész idő alatt. Pl. 2.2-es verzióban bevezetett OpenGL 3D gyorsítás támogatása a Linux és Solaris vendégeknek. Szép GUI felülete (Qt-t és / vagy SDL) vagy parancssori eszköztára van a virtuális gépek kezeléséhez. A felügyelet nélküli működés is támogatott. iTunes futtatása VirtualBox alatt az egyetlen módja (jelenleg), hogy szinkronizáld iPod Touch / iPhone firmware 3.0+.

## Contents

*   [1 Kiadások](#Kiad.C3.A1sok)
    *   [1.1 VirtualBox (OSE)](#VirtualBox_.28OSE.29)
    *   [1.2 VirtualBox (PUEL)](#VirtualBox_.28PUEL.29)
*   [2 Telepítés](#Telep.C3.ADt.C3.A9s)
    *   [2.1 VirtualBox (OSE)](#VirtualBox_.28OSE.29_2)
    *   [2.2 VirtualBox PUEL (virtualbox_bin)](#VirtualBox_PUEL_.28virtualbox_bin.29)
        *   [2.2.1 Szükséges QT lib-ek](#Sz.C3.BCks.C3.A9ges_QT_lib-ek)
    *   [2.3 VirtualBox 2.1 (másik alternatíva)](#VirtualBox_2.1_.28m.C3.A1sik_alternat.C3.ADva.29)
*   [3 Konfigurálás](#Konfigur.C3.A1l.C3.A1s)
    *   [3.1 Billentyű és egér a kiszolgáló és vendég között](#Billenty.C5.B1_.C3.A9s_eg.C3.A9r_a_kiszolg.C3.A1l.C3.B3_.C3.A9s_vend.C3.A9g_k.C3.B6z.C3.B6tt)
    *   [3.2 Getting network in the guest machine to work](#Getting_network_in_the_guest_machine_to_work)
        *   [3.2.1 NAT hálózat használata](#NAT_h.C3.A1l.C3.B3zat_haszn.C3.A1lata)
        *   [3.2.2 Kiszolgálói csatoló hálózat használata (VirtualBox módra)](#Kiszolg.C3.A1l.C3.B3i_csatol.C3.B3_h.C3.A1l.C3.B3zat_haszn.C3.A1lata_.28VirtualBox_m.C3.B3dra.29)
        *   [3.2.3 Kiszolgálói csatoló hálózat használata(Arch módra)](#Kiszolg.C3.A1l.C3.B3i_csatol.C3.B3_h.C3.A1l.C3.B3zat_haszn.C3.A1lata.28Arch_m.C3.B3dra.29)
        *   [3.2.4 Kiszolgálói csatoló hálózat használata (általános)](#Kiszolg.C3.A1l.C3.B3i_csatol.C3.B3_h.C3.A1l.C3.B3zat_haszn.C3.A1lata_.28.C3.A1ltal.C3.A1nos.29)
        *   [3.2.5 Kiszolgálói csatoló hálózat használata vezetéknálküli eszközzele](#Kiszolg.C3.A1l.C3.B3i_csatol.C3.B3_h.C3.A1l.C3.B3zat_haszn.C3.A1lata_vezet.C3.A9kn.C3.A1lk.C3.BCli_eszk.C3.B6zzele)
    *   [3.3 Getting USB to work in the guest machine](#Getting_USB_to_work_in_the_guest_machine)
    *   [3.4 Guest Additions telepítése](#Guest_Additions_telep.C3.ADt.C3.A9se)
    *   [3.5 Megosztott mappák a kiszolgáló és vendég között](#Megosztott_mapp.C3.A1k_a_kiszolg.C3.A1l.C3.B3_.C3.A9s_vend.C3.A9g_k.C3.B6z.C3.B6tt)
    *   [3.6 Getting audio to work in the guest machine](#Getting_audio_to_work_in_the_guest_machine)
    *   [3.7 RAM és Video Memoria beállítása a virtuális PC-hez](#RAM_.C3.A9s_Video_Memoria_be.C3.A1ll.C3.ADt.C3.A1sa_a_virtu.C3.A1lis_PC-hez)
    *   [3.8 CD-ROM beállítása a virtuális PC-hez](#CD-ROM_be.C3.A1ll.C3.ADt.C3.A1sa_a_virtu.C3.A1lis_PC-hez)
    *   [3.9 OpenGL gyorsítás engedélyezése Arch Linux vendégeken](#OpenGL_gyors.C3.ADt.C3.A1s_enged.C3.A9lyez.C3.A9se_Arch_Linux_vend.C3.A9geken)
    *   [3.10 D3D gyorsítás engedélyezése Windows vendégeken](#D3D_gyors.C3.ADt.C3.A1s_enged.C3.A9lyez.C3.A9se_Windows_vend.C3.A9geken)
*   [4 VirtualBox indítása](#VirtualBox_ind.C3.ADt.C3.A1sa)
*   [5 Virtualizált OS beállítása](#Virtualiz.C3.A1lt_OS_be.C3.A1ll.C3.ADt.C3.A1sa)
    *   [5.1 Egy LiveCD/DVD tesztelése](#Egy_LiveCD.2FDVD_tesztel.C3.A9se)
*   [6 Karbantartás](#Karbantart.C3.A1s)
    *   [6.1 A vboxdrv modul újraépítése](#A_vboxdrv_modul_.C3.BAjra.C3.A9p.C3.ADt.C3.A9se)
    *   [6.2 Compact a Disk Image](#Compact_a_Disk_Image)
    *   [6.3 Windows Xp és Nokia telefonok](#Windows_Xp_.C3.A9s_Nokia_telefonok)
*   [7 Migrating From Another VM](#Migrating_From_Another_VM)
    *   [7.1 Converting from QEMU images](#Converting_from_QEMU_images)
    *   [7.2 VMware image-ok konvertálása](#VMware_image-ok_konvert.C3.A1l.C3.A1sa)
*   [8 Tippek és Trükkök](#Tippek_.C3.A9s_Tr.C3.BCkk.C3.B6k)
    *   [8.1 CTRL+ALT+F1 küldése a vendégnek](#CTRL.2BALT.2BF1_k.C3.BCld.C3.A9se_a_vend.C3.A9gnek)
    *   [8.2 Speeding up HDD Access for the Guest](#Speeding_up_HDD_Access_for_the_Guest)
    *   [8.3 VMs indítása rendszerinduláskor Felügyelet-nélküli szerveren](#VMs_ind.C3.ADt.C3.A1sa_rendszerindul.C3.A1skor_Fel.C3.BCgyelet-n.C3.A9lk.C3.BCli_szerveren)
    *   [8.4 Accessing Server on VM from Host](#Accessing_Server_on_VM_from_Host)
*   [9 Arch Linux futtatása vendégként](#Arch_Linux_futtat.C3.A1sa_vend.C3.A9gk.C3.A9nt)
*   [10 Külső hívatkozások](#K.C3.BCls.C5.91_h.C3.ADvatkoz.C3.A1sok)

## Kiadások

VirtualBox két kiadásban áll rendelkezésre : VirtualBox OSE (Open Source Edition - nyílt forrású kiadás) és a VirtualBox PUEL (Personal Use and Evaluation License - személyes használat és kipróbálási licenc)

### VirtualBox (OSE)

VirtualBox (OSE) a VirtualBox nyílt forrású változata, amely megtalálható a közösségi adattárban. Hiányoznak belőle bizonyos funkciók, mint például az USB eszközök támogatása, valamint a beépített RDP szerver.

### VirtualBox (PUEL)

VirtualBox PUEL is a binary-only version (egyéni felhasználásra ingyenes). There are several available from the AUR, but the most popular PKGBUILD was written and is maintained by thotypous. You can download it from the [AUR at this link](https://aur.archlinux.org/packages.php?ID=9753) or directly from the [VirtualBox](http://www.virtualbox.org/wiki/Downloads) website. The PUEL edition offers the following advantages:

*   **Remote Display Protocol (RDP) Server** - a complete RDP server on top of the virtual hardware, allowing users to connect to a virtual machine remotely using any RDP compatible client

*   **USB support** - a virtual USB controller which allows USB 1.1 and USB 2.0 devices to be passed through to virtual machines

*   **USB over RDP** - a combination of the RDP server and USB support, allowing users to make USB devices available to virtual machines running remotely

*   **iSCSI initiator** - a builtin iSCSI initiator making it possible to use iSCSI targets as virtual disks without the guest requiring support for iSCSI

## Telepítés

### VirtualBox (OSE)

VirtualBox (OSE) elérhető a közösségi tárolóból:

```
# pacman -S virtualbox-ose

```

**Note:** This package is not in x86_64 Repositories. See the link to the PKGBUILD by thotypous in the AUR above if you are running Arch x86_64 and want to use VirtualBox.

This will select by default <tt>virtualbox-ose</tt> and <tt>virtualbox-modules</tt> packages. Once installed, a desktop entry can be located in *Applications → System Tools → VirtualBox OSE*

Now, add the desired username to the **vboxusers** group:

```
# gpasswd -a USERNAME vboxusers

```

**Note:** You must logout/login in order for this change to take effect.

Lastly, edit `/etc/rc.conf` as root and add **vboxdrv** to the MODULES array in order to load the VirtualBox drivers at startup. For example:

```
MODULES=(loop **vboxdrv** fuse ...)

```

To load the module manually, run the following in a terminal as root:

```
# modprobe vboxdrv

```

### VirtualBox PUEL (virtualbox_bin)

VirtualBox PUEL is available from the [AUR: virtualbox_bin](https://aur.archlinux.org/packages.php?ID=9753).

Download the tarball from the above page. As a normal user, unpack, change directory, and `makepkg`:

```
# tar -xzf virtualbox_bin.tar.gz
# cd virtualbox_bin
# makepkg

```

This will create a .pkg.tar.gz file in the virtualbox_bin directory. Then, as root:

```
# pacman -U PACKAGE-NAME.pkg.tar.gz

```

This will compile the vboxdrv kernel modules and install VirtualBox in `/opt/VirtualBox`, and add the vboxusers group.

Now, add the desired username to the **vboxusers** group:

```
# gpasswd -a USERNAME vboxusers

```

**Note:** You must logout/login in order for this change to take effect.

Lastly, edit `/etc/rc.conf` as root and add **vboxdrv** to the MODULES array in order to load the VirtualBox drivers at startup. For example:

```
MODULES=(loop **vboxdrv** fuse ...)

```

To load the module manually, run the following in a terminal as root:

```
# modprobe vboxdrv

```

#### Szükséges QT lib-ek

Currently, VirtualBox relies on QT4 for its graphical interface. If you require a GUI, ensure you have QT4 installed:

```
# pacman -S qt

```

### VirtualBox 2.1 (másik alternatíva)

VirtualBox.run install can be done using the All Distributions package from the [Linux section](http://www.virtualbox.org/wiki/Linux_Downloads) of the VirtualBox Website.

Make sure the Qt 4.3.0 and SDL 1.2.7 or higher packages are installed:

```
# pacman -S qt sdl 

```

Download the appropriate architecture file i386/AMD64\. In a terminal window, browse to the download folder and as root run:

```
# sh VirtualBox-2.XXXX-Linux_ARCH.run

```

This will install the package to the /opt/VirtualBox-2.XXX folder.

After installation, a desktop entry can be located in *Applications → System Tools → Sun xVM VirtualBox*

Now, add the desired username to the **vboxusers** group:

```
# gpasswd -a USERNAME vboxusers

```

Lastly, edit `/etc/rc.conf` as root and add **vboxdrv** to the MODULES array in order to load the VirtualBox drivers at startup.

Start the VirtualBox GUI either with the command:

```
# VirtualBox 

```

or using the *Applications* desktop entry. In version 2.1.x, an installation wizard should start and take you through the process of setting up a virtual machine. Otherwise, use the help menu to get started. **Continue reading to see the more advanced options and setups...**

## Konfigurálás

After having installed VirtualBox on our system and added ourselves in the vboxusers group, you can start configuring our system in order to make all the features of VirtualBox available to us. Create a new virtual machine using the wizard provided by the GUI and then click settings in order to edit the virtual machine settings.

### Billentyű és egér a kiszolgáló és vendég között

*   To capture the keyboard and mouse, click the mouse inside the Virtual Machine display.
*   To uncapture, press Ctrl-Alt-Delete.

If [Xorg](/index.php/Xorg "Xorg") freezes mouse and keyboard you will have to disable the [new hot plugging feature of Xorg 1.5](/index.php/Xorg#Input_hotplugging_with_xorg-server_1.5 "Xorg") by adding in `/etc/X11/xorg.conf`:

```
Section "ServerFlags"
       . . .
       Option "AutoAddDevices" "False"
       . . .
EndSection

```

This is needed for Linux guests in a Mac OS X or Windows host. Also needed for Linux hosts (tested with Arch64 host and Arch64 guest).

Also, mouse pointer integration does not work out of the box. To fix it, make sure you have the following sections in your `xorg.conf`:

```
Section "InputDevice"
   Identifier "Mouse0"
   Driver "vboxmouse"
   Option         "Protocol" "auto"
   Option         "Device" "/dev/input/mice"
   Option         "ZAxisMapping" "4 5 6 7"
EndSection

```

```
Section "ServerLayout"
   Identifier     "X.org Configured"
   Screen      0  "Screen0" 0 0
   InputDevice    "Mouse0" "CorePointer"
   InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

```

When generating your `xorg.conf` with `"X -configure"`, you will end up with an InputDevice section that uses the `mouse` driver. After installing the Guest Additions, you should replace `mouse` with `vboxmouse` and then restart X or reboot your VM.

### Getting network in the guest machine to work

First, get network working in the guest machine. Click the network tab. The not attached option means you will have "Network cable unplugged" or similar error in the guest computer.

#### NAT hálózat használata

This is the simplest way to get network. Select NAT network and it should be ready to use. Then, the guest operating system can be automatically configured by using DHCP.

The NAT IP address on the first card is 10.0.2.0, 10.0.3.0 on the second and so on.

Also in VirtualBox 2.2.0+ NAT network DHCP clients will not configure your nameserver (DNS server for windows guests) you will have to manually configure the nameserver(DNS server)

#### Kiszolgálói csatoló hálózat használata (VirtualBox módra)

Since VirtuaBox 2.1.0 it has a native support for host interface networking. Just add **vboxnetflt** to your MODULES section in `[rc.conf](/index.php/Rc.conf "Rc.conf")` and choose *Host Interface Networking* (or *Bridged adapter* in [2.2](http://forums.virtualbox.org/viewtopic.php?f=1&t=16447)) in the virtual machine configuration.

**Note**: DHCP broadcasting does not seem to work properly under this way. Set up your guest networking with static IP assignment.

#### Kiszolgálói csatoló hálózat használata(Arch módra)

You are going to just edit these files and reboot:

*   `/etc/conf.d/bridges`
*   `/etc/rc.conf`
*   `/etc/vbox/interfaces`

Edit: **`/etc/conf.d/bridges`**

```
bridge_br0="eth0 vbox0" # Put any interfaces you need.
BRIDGE_INTERFACES=(br0)

```

**`/etc/rc.conf`**

First add the bridge module to your MODULES line

```
MODULES=( <your other modules> **bridge**)

```

Then, in your NETWORKING section, make the following changes:

```
eth0="eth0 up"
br0="dhcp" # Maybe you have some static configuration; change to fit
INTERFACES=(eth0 br0)

```

**Note** by gpan:

**`/etc/rc.conf`**

First add the vboxdrv (and vboxnetflt in case of 2.1.0 version) module to your MODULES line:

```
MODULES=( <your other modules> vboxdrv vboxnetflt )

```

**Note** by vit:

**`/etc/rc.conf`**

In my case it did not work untill adding vboxnetadp to modules.

Next, you should edit your `/etc/udev/rules.d/60-vboxdrv.rules` and type:

```
KERNEL=="vboxdrv", NAME="vboxdrv", OWNER="root", GROUP="vboxusers", MODE="0660"

```

Save it and exit.

Then open terminal and type:

```
# pacman -S bridge-utils uml_utilities

```

Create a new bridge with this command:

```
# brctl addbr br0

```

**`/etc/vbox/interfaces`**

(You can set up more interfaces if you want. Sky is the limit!):

```
vbox0 your_user br0 # Be sure that your user is in the vboxusers group.

```

Reboot.

**Note:** Remember to set up your virtual machine with proper network configuration.

**Note:** If you have any issue, make sure that you have the bridge-utils package installed and vboxnet daemon loaded.

#### Kiszolgálói csatoló hálózat használata (általános)

This way is a bit harder, but it allows you to see the VirtualMachine as a "real" computer on your local network. You need to get bridge-utils

```
# pacman -S bridge-utils uml_utilities

```

**Note** by Sp1d3rmxn:

	You also need to have the TUN module loaded... in `[rc.conf](/index.php/Rc.conf "Rc.conf")` add `"tun"` (without the quotes) to your MODULES section. For testing this out right now without rebooting you can load the module from the command line by `"modprobe tun"`.

	Then you MUST set these permissions otherwise you will never get VBox to init the interface. The command is `"chmod 666 /dev/net/tun"` (without the quotes).

	Now proceed with the rest as it is written below.

**Note**

	As said by Sp1d3rmxn, set these permissions, but, instead of using the command, set them in `/etc/udev/rules.d/60-vboxdrv.rules`, which will apply them on boot:

```
KERNEL=="vboxdrv", NAME="vboxdrv", OWNER="root", GROUP="vboxusers", MODE="0660"
KERNEL=="tun", OWNER="root", GROUP="vboxusers", MODE="0660"

```

**1.** Create a new bridge with this command:

```
# brctl addbr br0

```

**2.** If you are not using DHCP, run ifconfig and note down the network configuration of your existing network interface (e.g. eth0), which will need to be copied to the bridge.

**Note:** You will need this settings so make sure you do not lose them.

**3.** Switch your physical network adapter to "promiscuous" mode so that it will accept Ethernet frames for MAC addresses other than its own (replace `eth0` with your network interface):

```
# ifconfig eth0 0.0.0.0 promisc 

```

**Note:** You will lose network connectivity on eth0 at this point.

**4.** Add your network adapter to the bridge:

```
# brctl addif br0 eth0

```

**5.** Transfer the network configuration previously used with your physical ethernet adapter to the new bridge. If you are using DHCP, this should work:

```
# dhclient br0

```

**Note** by Sp1d3rmxn:

	Use `"dhcpcd -t 30 -h yourhostname br0 &"` instead of the above

Otherwise, run `"ifconfig br0 x.x.x.x netmask x.x.x.x"` and use the values that you noted down previously.

**6.** To create a permanent host interface called vbox0 (all host interfaces created in this way must be called vbox followed by a number) and add it to the network bridge created above, use the following command:

```
VBoxAddIF vbox0 vboxuser br0

```

Replace `vboxuser` with the name of the user who is supposed to be able to use the new interface.

**Note:** VboxAddIF is located in /opt/VirtualBox-VERSION OF VIRTUALBOX/VBoxAddIF

Alternatively, you can [setup VirtualBox networking](http://mychael.gotdns.com/blog/2007/05/31/virtualbox-bridging/) through your `/etc/rc.conf` to enable a bridged connection.

#### Kiszolgálói csatoló hálózat használata vezetéknálküli eszközzele

Bridging as described above will not work with a wireless device. Using [parprouted](https://aur.archlinux.org/packages.php?ID=16356) however it can be accomplished.

1.  Install parprouted and iproute
2.  `# ln -s /usr/sbin/ip /sbin/ip`
3.  Make sure IP fowarding is enabled: `# sysctl net.ipv4.ip_forward=1`, and/or edit `/etc/sysctl.d/40-ip-forward.conf`.
4.  `# VBoxTunctl -b -u <user>`, to create the tap device
5.  `# ip link set tap0 up; ip addr add 192.168.0.X/24 dev tap0`, needs to be a manually set IP on the same network your wireless device is.
6.  `# parprouted wlan0 tap0`

### Getting USB to work in the guest machine

(csak a PUEL kiadásban elérhető)

**Note:** As of VirtualBox>2.2.4 this is no longer necessary to mount a usb filesystem.

First in order to make USB available for use to the virtual machine you must add this line to your `/etc/fstab`:

```
none /proc/bus/usb usbfs auto,busgid=108,busmode=0775,devgid=108,devmode=0664 0 0

```

Then tell mount to reread `/etc/fstab`:

```
# mount -a

```

`108` is is the id of the group which should be allowed to access USB-devices. Change it to the id of your vboxusers group. You can get the id by running:

```
$ grep vboxusers /etc/group

```

Restart Virtualbox and click the USB tab in the settings of the virtual machine and select which devices are available to your pc on boot. If you wish your virtual machine to use device that you have just plugged in (assuming the virtual machine has booted already), go to the VirtualMachine screen go to *Devices → USB Devices* and select the device you wish to plug in the virtual PC.

**Note** by bjimba:

Recent versions of VirtualBox, as noted above, do not require usbfs, however you will need the HAL daemon running if you do not use usbfs. See the [HAL](/index.php/HAL "HAL") wiki page for details.

### Guest Additions telepítése

The Guest Additions make the shared folders feature available, as well as better video (3D available in version 2.1+) and mouse drivers. You will have mouse integration, thus no need to release the mouse after using it in the guest and one can also enable a bidirectional clipboard.

**Note:** The instructions immediately below are for an Archlinux guest on an Archlinux host.

After you booted the virtual machine, go to menu *Devices → Install Guest Additions...* Once you have clicked it, VirtualBox loads an ISO into the current CD-ROM, so you will not see anything happen yet ;).

You will require gcc and make if you do not already have them so install them typing the following as root:

```
# pacman -S gcc make 

```

If you are running arch in VirtualBox install the kernel headers

```
# pacman -S kernel26-headers

```

Then do the following as root:

```
# mount /media/cdrom

```

for i686 systems (32 bit):

```
# sh /media/cdrom/VBoxLinuxAdditions-x86.run

```

for x86-64 systems (64 bit):

```
# sh /media/cdrom/VBoxLinuxAdditions-amd64.run

```

It will build and install the kernel modules, install the Xorg drivers and create init scripts. It will most probably print out errors about init scripts and run levels and what not. Ignore them. You will find `rc.vboxadd` in /etc/rc.d which will load them on demand. To have the Guest Additions loaded at boot time, just add those to the DAEMONS array in `/etc/rc.conf` eg.:

```
DAEMONS=(syslog-ng network netfs crond alsa **rc.vboxadd**)

```

Another option is to install one of these packages:

```
# pacman -S virtualbox-additions

```

or

```
# pacman -S virtualbox-ose-additions

```

You will then have an ISO to mount as a loop device. Remember to load the loop kernel module before:

```
# modprobe loop
# mount /usr/lib/virtualbox/additions/VBoxGuestAdditions.iso /media/cdrom -o loop

```

Then execute `VBoxLinuxAdditions.run` as before. Before adding `rc.vboxadd` to DAEMONS check `/etc/rc.local` for commands to load the vboxadd daemons put by the installation script.

**Windows vendégek**

After installing Windows (XP etc.) on your virtual machine, simply select *Devices → Install Guest Additions...*

This will mount the iso image and windows should then automatically launch the guest additions installer. Follow the instructions to the end.

### Megosztott mappák a kiszolgáló és vendég között

In the settings of the virtual machine go to shared folders tab and add the folders you want to share.

*   NOTE: You need to install Guest Additions in order to use this feature.

```
In a Linux host, *Devices → Install Guest Additions*
Yes (when asked to download the CD image)
Mount (when asked to register and mount)

```

In a Linux host, create one folder for sharing files.

In a Windows guest, starting with VirtualBox 1.5.0, shared folders are browseable and are therefore visible in Windows Explorer. Open Windows Explorer and look for it under *My Networking Places → Entire Network → VirtualBox Shared Folders*.

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

### RAM és Video Memoria beállítása a virtuális PC-hez

You can change the default values by going to *Settings → General*.

### CD-ROM beállítása a virtuális PC-hez

You can change the default values by going to *Settings → CD/DVD-ROM*.

Check mount CD/DVD drive and select one of the following options.

**Note:** If no CD-ROM drive is detected, make sure the HAL daemon is running. To start it, run the following command as root:

```
# /etc/rc.d/hal start

```

### OpenGL gyorsítás engedélyezése Arch Linux vendégeken

Due to a bug in the VirtualBox guest addition setup scripts (as of VBox 3.1.2), simply ticking the "3D acceleration" checkbox in the virtual machine settings and installing the guest additions won't enable 3D acceleration for OpenGL applications under X for Arch Linux guests (and possibly others). In order to still get OpenGL acceleration, a bit of manual intervention is necessary after installing the guest additions. As root, run:

```
ln -s /usr/lib/VBoxOGL.so /usr/lib/xorg/modules/dri/vboxvideo_dri.so
ln -s /usr/lib/xorg/modules/dri /usr/lib/dri

```

Also make sure the user starting X in the guest is in the **video** group.

### D3D gyorsítás engedélyezése Windows vendégeken

Recent versions of Virtualbox have support for accelerating OpenGL inside guests. This can be enabled with a simple checkbox in the machine's settings, right below where video ram is set, and installing the Virtualbox guest additions. However, most Windows games use Direct3D (part of DirectX), not OpenGL, and are thus not helped by this method. However, it is possible to gain accelerated Direct3D in your Windows guests by borrowing the d3d libraries from Wine, which translate d3d calls into OpenGL, which is then accelerated.

After enabling OpenGL acceleration as described above, go to [http://www.nongnu.org/wined3d/](http://www.nongnu.org/wined3d/) in your Windows guest and grab the "Latest version (Installer):". Reboot the guest into safe mode (press F8 before the Windows screen appears but after the Virtualbox screen disappears), and install wined3d, accepting the defaults during the install. (You may check the box for DirectX 10 support if you like, dont touch anything else.) Reboot back to normal mode and you should have accelerated Direct3D.

**Note:** This hack may or may not work for some games depending on what hardware checks they make and what parts of D3D they use.

**Note:** This has only been tried on Windows XP and Windows 7 RC guests AFAIK, and does not work on the Windows 7 guest. If you have experience with this on a different windows version, please add that data here.

## VirtualBox indítása

To start Virtualbox, run the following command in a terminal:

```
$ VirtualBox

```

Or in KDE menu, select: <System><Sun Virtualbox>

## Virtualizált OS beállítása

Virtualbox needs to be setup to virtualize another operating system.

### Egy LiveCD/DVD tesztelése

Click the 'New' button to create a new virtual environment. Name it appropriately and select Operating System type and version. Select base memory size (note: most operating systems will need at least 512MB to function properly). Create a new hard disk image (a hard disk image is a file that will contain the operating system's filesystem and files).

When the new image has been created, click 'Settings', then CD/DVD-ROM, check 'Mount CD/DVD Drive' then select an ISO image.

## Karbantartás

### A vboxdrv modul újraépítése

Note that any time your kernel version changes (due to upgrade, recompile, etc.) you must also rebuild the VirtualBox kernel.

**Depending of your version :**

* * *

On **version 3.1.2** and possibly later /etc/rc.d/rc.vboxdrv does not exist.

Install *kernel26-headers*. This is difference than the kernel-headers package

As root, run:

```
# KERN_DIR=/usr/src/<your kernel directory> KERN_INCL=/usr/include vbox_build_module

```

* * *

On **virtualbox_bin from AUR** *or* on **versions 2.1 to 3.1.1**, run the following command:

```
# vbox_build_module

```

This binary will be located in one of the following locations: <tt>/sbin</tt>, <tt>/bin</tt>, or <tt>/usr/bin</tt>.

**Note:** If you are using one of the Virtualbox PKGBUILD's from the AUR, you will also need to update your modules via this method. In most cases, users of x86_64 will need to use one of the PKBUILDS of Virtualbox since the official repos only have support for the i686 architecture.

* * *

On **versions before 2.1**, update the kernel module by running the following command:

```
# /etc/rc.d/rc.vboxdrv setup

```

After rebuilding the module, do not forget to load it with

```
# modprobe vboxdrv

```

*vboxdrv* and *vboxnetflt* should be in the MODULES=() section of your /etc/rc.conf

### Compact a Disk Image

See [How to compact a VirtualBox virtual disk image (VDI)](http://my.opera.com/locksley90/blog/2008/06/01/how-to-compact-a-virtualbox-virtual-disk-image-vdi)

### Windows Xp és Nokia telefonok

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

## Migrating From Another VM

The `qemu-img` program can be used to convert images from one format to another, or add compression or encryption to an image.

```
  # pacman -S qemu

```

### Converting from QEMU images

To convert a QEMU image for use with VirtualBox, first convert it to *raw* format, then use VirtualBox's conversion utility to convert and compact it in its native format.

```
  $ qemu-img convert -O raw test.qcow2 test.raw
  $ VBoxManage modifyvdi /full/path/to/test.vdi compact

```

### VMware image-ok konvertálása

Do

```
  $ qemu-img convert image.vmdk image.bin
  $ VBoxManage convertdd image.bin image.vdi

```

This may not be needed anymore with recent virtualbox versions (to be confirmed)

## Tippek és Trükkök

### CTRL+ALT+F1 küldése a vendégnek

If your guest O/S is a Linux distro, and you want to open a new tty text shell or exit X via typing `Ctrl`+`Alt`+`F1`, you can easily send this command to the guest O/S simply by hitting your 'Host Key' (usually the `Ctrl` in the Right side of your keyboard) + `F1` or `F2`, etc.

### Speeding up HDD Access for the Guest

Enabling the SATA(AHCI) controller within Virtualbox can speed up Host disk operations. This is available though Settings>Hard Disks in current versions of Virtual Box.

### VMs indítása rendszerinduláskor Felügyelet-nélküli szerveren

```
exec /bin/su PREFERRED_USER -l -c "/bin/bash --login -c \"VBoxHeadless -startvm {UUID}\" >/dev/null 2>&1"

```

Where PREFERRED_USER is the user profile that contains the VM definitions and .vdi files. This will start the VM with a RDP server running on port 3389. To determine the available VMs for a user:

```
su PREFERRED_USER -c "VBoxManage list vms"

```

To suspend the VM:

```
su PREFERRED_USER -c "VBoxManage controlvm {UUID} savestate"

```

### Accessing Server on VM from Host

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

## Arch Linux futtatása vendégként

To install guest additions with support for Xorg follow these steps:

**Note:** Run these steps as root

```
$ pacman -S xorg

```

**Note:** install entire group (is everything actually required?)

```
$ pacman -S kernel26-headers gcc make
$ mount and install VirtualBox guest additions
$ X -configure
$ change the mouse driver from "mouse" to "vboxmouse" in /root/xorg.conf.new
$ mv /root/xorg.conf.new /etc/X11/xorg.conf
$ add hal to DAEMONS in rc.conf

```

**Note:** It is not required to add rc.vboxadd to DAEMONS because it is added to /etc/rc.local automatically

**Note:** Run these steps while logged into your user account

```
$ add /usr/bin/VBoxClient-all to the top of ~/.xinitrc (even if ~/.xinitrc does not exist)

```

## Külső hívatkozások

*   [VirtualBox Felhasználói Kézikönyv (en)](http://www.virtualbox.org/manual/UserManual.html)