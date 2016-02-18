This page documents configuration and troubleshooting specific to the Acer Aspire One.

Some of this information is from the [Arch Forum](https://bbs.archlinux.org/viewtopic.php?id=51796). You can also find a lot of helpful information from the [AspireOneUser Forum](http://www.aspireoneuser.com/forum/viewforum.php?f=5&sid=29c7eef18d2d6477d7f9db91195fb31a) and [Install Ubuntu Hardy Heron (8.04.1) on the Acer Aspire One](https://help.ubuntu.com/community/AspireOne).

General netbook installation hints can be found also in the [Asus EEE PC Wiki article](/index.php/Installing_Arch_Linux_on_the_Asus_EEE_PC "Installing Arch Linux on the Asus EEE PC")

Also see the pages on the [Acer Aspire One model AOD250-1613 (Android + XP version)](/index.php/Acer_AOD250-1613 "Acer AOD250-1613") and the [Acer Aspire One model AO722-BZ454](/index.php/Acer_AO722-BZ454 "Acer AO722-BZ454").

## Contents

*   [1 Before you begin](#Before_you_begin)
    *   [1.1 A list of choices to be made during installation](#A_list_of_choices_to_be_made_during_installation)
    *   [1.2 Choosing your installation medium](#Choosing_your_installation_medium)
    *   [1.3 Choosing an Installation Image](#Choosing_an_Installation_Image)
    *   [1.4 Preparation prior to installing Arch Linux](#Preparation_prior_to_installing_Arch_Linux)
*   [2 Recommended partition schemes](#Recommended_partition_schemes)
    *   [2.1 File-systems](#File-systems)
    *   [2.2 Choosing maximum lifetime, or data integrity](#Choosing_maximum_lifetime.2C_or_data_integrity)
    *   [2.3 Mounting Options](#Mounting_Options)
*   [3 Hardware](#Hardware)
    *   [3.1 lspci](#lspci)
    *   [3.2 Module setup](#Module_setup)
        *   [3.2.1 Module configuration](#Module_configuration)
            *   [3.2.1.1 Modules to blacklist](#Modules_to_blacklist)
            *   [3.2.1.2 Modules to load](#Modules_to_load)
        *   [3.2.2 Tweaks](#Tweaks)
    *   [3.3 Network](#Network)
        *   [3.3.1 WLAN](#WLAN)
            *   [3.3.1.1 ath5k](#ath5k)
            *   [3.3.1.2 Testing](#Testing)
            *   [3.3.1.3 ath9k and acer_wmi](#ath9k_and_acer_wmi)
        *   [3.3.2 LAN](#LAN)
            *   [3.3.2.1 Aspire One D250/D255e LAN](#Aspire_One_D250.2FD255e_LAN)
    *   [3.4 Audio](#Audio)
        *   [3.4.1 With linux (alsa as modules)](#With_linux_.28alsa_as_modules.29)
        *   [3.4.2 With linux-one and linux-one-dev (alsa built into the kernel)](#With_linux-one_and_linux-one-dev_.28alsa_built_into_the_kernel.29)
        *   [3.4.3 Audio test](#Audio_test)
        *   [3.4.4 Pulseaudio troubleshooting](#Pulseaudio_troubleshooting)
    *   [3.5 Video](#Video)
        *   [3.5.1 External VGA port](#External_VGA_port)
        *   [3.5.2 Setting DPI](#Setting_DPI)
        *   [3.5.3 Setting a proper framebuffer](#Setting_a_proper_framebuffer)
            *   [3.5.3.1 Kernel mode setting (KMS)](#Kernel_mode_setting_.28KMS.29)
            *   [3.5.3.2 uvesafb](#uvesafb)
            *   [3.5.3.3 Using intelfb without an initrd](#Using_intelfb_without_an_initrd)
    *   [3.6 Webcam](#Webcam)
    *   [3.7 Card Reader](#Card_Reader)
    *   [3.8 Additional function keys](#Additional_function_keys)
    *   [3.9 Touchpad](#Touchpad)
        *   [3.9.1 Two-Finger scrolling](#Two-Finger_scrolling)
*   [4 Power management](#Power_management)
    *   [4.1 Enabling CPU frequency scaling](#Enabling_CPU_frequency_scaling)
    *   [4.2 Suspend on lid, shutdown on power button](#Suspend_on_lid.2C_shutdown_on_power_button)
*   [5 Example configurations](#Example_configurations)
    *   [5.1 /etc/rc.local](#.2Fetc.2Frc.local)
*   [6 Customized kernel](#Customized_kernel)
*   [7 Tuning tips](#Tuning_tips)
    *   [7.1 SD Storage Expansion](#SD_Storage_Expansion)
        *   [7.1.1 Labeling Partitions](#Labeling_Partitions)
        *   [7.1.2 Mount expansion as /home](#Mount_expansion_as_.2Fhome)
            *   [7.1.2.1 Method 1: fstab entry](#Method_1:_fstab_entry)
            *   [7.1.2.2 Method 2: rc.local entry](#Method_2:_rc.local_entry)
    *   [7.2 Regulating the CPU fan](#Regulating_the_CPU_fan)
        *   [7.2.1 acerhdf](#acerhdf)
    *   [7.3 Using the Super key for middle-clicking](#Using_the_Super_key_for_middle-clicking)
        *   [7.3.1 Using FVWM 2](#Using_FVWM_2)
        *   [7.3.2 Using xte](#Using_xte)
        *   [7.3.3 Using xbindkeys](#Using_xbindkeys)
    *   [7.4 SSD specific tweaks](#SSD_specific_tweaks)
    *   [7.5 Updating the BIOS](#Updating_the_BIOS)
        *   [7.5.1 Using FreeDOS](#Using_FreeDOS)
            *   [7.5.1.1 AOD150](#AOD150)
        *   [7.5.2 Using Flashrom](#Using_Flashrom)
        *   [7.5.3 Instructions by Acer for AOA110 and AOA150](#Instructions_by_Acer_for_AOA110_and_AOA150)
    *   [7.6 Polishing the boot process](#Polishing_the_boot_process)
    *   [7.7 Compiling for the Atom processor](#Compiling_for_the_Atom_processor)
*   [8 See also](#See_also)

## Before you begin

### A list of choices to be made during installation

*   Installation medium: CD-ROM or USB **(usb is recommended)**
*   Which filesystems to choose:
    *   If you want a journaled filesystem for the SSD or HDD or not **(ext4 is recommended)**
    *   If you want a journaled filesystem for the SD-card or not **(highly recommended, for instance xfs or ext4)**
*   If you want a swap partition or not **(not recommended, but meh)**
    *   A swap partition may wear the disk somewhat, but it makes hibernation possible
    *   Regular "sleep" is still possible without a swap partition
*   Which kernel to use: linux or kernel-netbook **(kernel-netbook is recommended)**
*   Which modules and daemons you want loaded at boot in rc.conf
*   If you want to configure the machine for maximum performance or battery life
*   If you want to configure X for using 3D graphics or not
*   If you wish to boot straight into a graphics mode or not ("KMS")
*   General configuration

There are also all sorts of tweaks along the way, that you may choose to apply.

### Choosing your installation medium

The Acer Aspire One does not come with an optical drive.

This means you will need to install Arch Linux through one of the alternative methods:

*   [USB stick](/index.php/Install_from_USB_stick "Install from USB stick") **(recommended)**
*   External USB CD-ROM drive **(weird, but possible)**

### Choosing an Installation Image

You may wish to use a [pre-release images](https://releng.archlinux.org/isos), rather than the official Arch Linux images. The 2010.05 image may not contain the necessary drivers for the Atheros Ethernet or Broadcom Wireless found on certain Aspire One PCs, such as the D255e.

### Preparation prior to installing Arch Linux

*   Press `F12` at BIOS POST or change boot order with `F2` to select your installation method. (On some systems, `F12` might not be enabled by default, and you must hit `F2` to enter the BIOS and enable it).
*   To boot off the USB stick, choose USB HDD as the boot device.
*   It is recommended to permanently add a SD(HC) card into the left SD card reader to [extend storage space](#SD_Storage_Expansion).
*   Before running `/arch/setup` mount your SD card to be visible to the installer.

## Recommended partition schemes

*   `/dev/sda1` all 8GB on the SSD for `/`, formatted as ext4
*   `/dev/mmcblk0p1` all space on the extensional left side SD(HC) card for `/home`
    *   the SD card needs a journaling file system, like ext4 or xfs
*   No swap at all, unless you want hibernation. Having swap wears the disk somewhat more.

### File-systems

There is a limit in how many times you can write to any disk, SSD or a regular HDD. For SSD, you can write about 2 GB a day and it should last for about 3 years. Regular usage is probably less than this, hence it should last several more years. All disks will wear out eventually, so backup often. This goes for both SSD and HDDs.

In general, having data on a disk should be considered as safe as written notes on a wet paper napkin.

Solid state drives are made of flash memory, they are fast at reading but slow at writing data.

Journaled filesystem writes in a journal what it is modifying in the filesystem, so you will get more writes into the SSD, that will take your write count up as a bit of overhead for each write you will do, but will give you filesystem consistency if something as gone wrong. Same thing goes for the HDD-version.

You can choose a journaled filesystem (like ext4 or xfs) or a non journaled one (like ext2). The choice mainly depends on how important it is to you that all files are okay if you suddenly turn off the computer, compared to slightly less wear and tear over the years, and slightly more speed on disk operations.

The choice depends on your demands. Some people had trouble using ext2 with the SD-card (the filesystem was corrupted) and switched to XFS instead, with great success.

In general, ext4 is a good choice for disks and XFS works well for SD-cards that stay in the slot.

XFS over ext2/ext4 also have the added benefit of not having to wait for disk-checks every Nth boot, which can be a huge annoyance if you are about to hold a presentation.

### Choosing maximum lifetime, or data integrity

For a longer life for your disk, take care to:

*   Not use a journaling file system
*   Not use a swap partition (unless you want to be able to hibernate)
*   Edit your new installation fstab to mount the partitions as "noatime", which will mean better performance and longer life by not writing file access times. "relatime" is an alternative solution. See [this LWN article](http://lwn.net/Articles/244829/) for more information.
*   Not log errors or messages

If, on the other hand, data integrity is more important, use EXT4, XFS or another journaled filesystem instead.

A swap partition may be preferable if you use a browser, or other memory intensive application, that easily makes the system run out of memory. This will use the disk somewhat more, but may prevent crashes. Check the system status with an application like [htop](https://www.archlinux.org/packages/?name=htop). If you find out you need one, it's easy to create a large file and use that as a swap partition.

### Mounting Options

There are some tweaks you can employ in order to get somewhat better performance from your file systems:

*   EXT4:

```
 defaults,noatime

```

*   XFS:

```
 defaults,noatime

```

*   EXT3:

```
 defaults,noatime,errors=remount-ro,commit=15

```

*   EXT2:

```
 defaults,noatime,errors=remount-ro

```

These are to be added to your filesystem mount tab file located under `/etc/fstab`. As example a mount line for the root directory:

```
 /dev/sda1              /             ext4      defaults,noatime    0    1

```

It's also possible to add the "discard" mount option.

Another tweak is to mount each log directory into a memory filesystem (stores everything only into RAM) so you can skip more write counts out of our SSD but suitable also for HDD. These log files will be then deleted each time the system is rebooted.

For that you have to add to the same `/etc/fstab` the follow lines:

```
 none                   /var/log      tmpfs     size=10M   0      0
 none                   /tmp          tmpfs     size=100M  0      0
 none                   /var/tmp      tmpfs     size=20M   0      0

```

**Warning:** The temporary folders listed above will delete all files in those folders after each reboot. You may omit the last three lines, but have increased write access to the SSD.

**Warning:** It has been reported that the stock kernel is causing partition table corruption on the SD card when you resume from a suspend. Corrupted `/home`. Someone on the forum suggested that you need a kernel with `CONFIG_MMC_UNSAFE_RESUME` set to prevent this from happening. This solution did not work for some people, while using XFS instead of ext2 for `/home` worked just fine.

## Hardware

Aspire One common hardware:

*   Intel Atom N270 1.6 GHz cpu, SMP capable (hyperthreading like PIV), up to SSE3 extensions, no EM64T!
*   Intel 945GME chipset
*   Intel 950 GMA onboard graphics adapter
*   8.9 or 10.1 inch Acer Crystal Brite 1024×600 display
*   Realtek High Definition Audio ALC260
*   Battery: 11.V 41,2Wh/2200mAh or 45Wh/2400mAh Lithium-Ionen-Akku / 3 cell, with a 6 cell model planned
*   SD(hc) Card Reader left side: RICOH R5C8xx
*   Multi Card Reader right side Seite: JMicron JMB385 Flash Media Controller
*   Webcam: Acer Crystal Eye Webcam (Suyin Optronics)
*   Wlan: Atheros AR5007EG (Chipset 2425)
*   LAN: Realtek RTL8102E
*   Touchpad: Synaptics
*   Weight: 960 gr.
*   Size: 24,9 x 17 x 2,9 cm
*   One memory expansion slot ( So-DIMM DDRII 400/533/667MHz up to 1GB) under the keyboard hard to access see [memory upgrade](http://www.aspireoneuser.com/forum/viewtopic.php?f=4&t=17); max. 1,5GB

Version A110L

*   One 512MB memory stick onboard soldered
*   8 GB solid state drive (SSD)

Version A150L

*   One 1024MB memory stick onboard soldered
*   120 GB hard disk drive (HDD)

Version D255e

*   LAN: Atheros Communication AR8132 fast ethernet
*   Wireless: Network controller [0280]: Broadcom Corporation BCM4313 802.11b/g LP-PHY [14e4:4727] (rev 01)Subsystem: Broadcom Corporation Device [14e4:0510]

### lspci

```
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev 03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
00:1b.0 Audio device: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 2 (rev 02)
00:1c.2 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 3 (rev 02)
00:1c.3 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 4 (rev 02)
00:1d.0 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #3 (rev 02)
00:1d.3 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #4 (rev 02)
00:1d.7 USB Controller: Intel Corporation 82801G (ICH7 Family) USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA IDE Controller (rev 02)
00:1f.3 SMBus: Intel Corporation 82801G (ICH7 Family) SMBus Controller (rev 02)
02:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101E PCI Express Fast Ethernet controller (rev 02)
03:00.0 Ethernet controller: Atheros Communications, Inc. AR5006EG 802.11 b/g Wireless PCI Express Adapter (rev 01)

```

### Module setup

Ethernet, wireless networking and sound will work with the linux, kernel-netbook, linux-one and linux-one-dev kernels.

#### Module configuration

Now you have to select the modules you need to get the hardware working. Please refer to [kernel modules](/index.php/Kernel_modules "Kernel modules") for more information.

##### Modules to blacklist

*   **memstick** - Makes full load on one core- fixed as of kernel 2.6.29.
*   **snd_pcsp** - PC Speaker will be your sound card and `snd_hda_intel` will not work. Also amazingly annoying if put to use.

##### Modules to load

*   **acpi_cpufreq** - CPU scaling
*   **ath5k** or **ath9k** - The wireless device
*   **pciehp** - The SD card readers' hotplug functionality
*   **r8169** - The ethernet NIC
*   **uvcvideo** - The webcam device

#### Tweaks

Put `zramswap` in the DAEMONS array in /etc/rc.conf to use the zram module that may improve performance. This requires [zramswap](https://aur.archlinux.org/packages/zramswap/) and a recent kernel.

### Network

#### WLAN

AA1 wireless device is a rather new Atheros wireless chip not supported by Linux kernel until version 2.6.27\. Before that an external module was required to be compiled and installed named madwifi.

Now you need to reset the wireless driver upon suspend/resume so you need to create a rule for pm-utils to reload the module. This is done by creating a new file under /etc/pm/config.d/ named modules with:

```
 echo "SUSPEND_MODULES=\"ath5k\"" > /etc/pm/config.d/modules

```

##### ath5k

If you have problems with `ath5k`, you can get the latest version by following the instructions on this site: [http://wireless.kernel.org/en/users/Download](http://wireless.kernel.org/en/users/Download)

Essentially, you install the latest wireless drivers into an `updates/` directory, thus leaving the stock drivers intact for possible reverting.

In some cases, using the ath5k driver can lead to sporadic connection drops after a certain amount of data is transferred. In this case it may help to disable hwcrypt:

```
# ip link set eth0 up
# rmmod -r ath5k
# modprobe ath5k nohwcrypt=1
# ip link set eth0 down

```

If this solves the problem, make the solution permanent by adding the following to `/etc/modprobe.d/ath5k.conf`

```
options ath5k nohwcrypt=1

```

##### Testing

This is one way to test if the wireless card is working:

Use iw dev to find the name of your wireless device:

```
iw dev

```

The output may be something like this:

```
phy#0
        Interface wlp3s0
        wdev 0x1
        addr 00:22:68:aa:bb:cc
        type managed
        channel 11 (2462 MHz), width: 20 MHz (no HT), center1: 2462 MHz

```

From the output, you can see that the name of the wireless interface device is wlp3s0\. Remember this device name!

Now scan the wireless network for access points:

```
# iw wlp3s0 scan | grep SSID

```

If you can see a list of SSID's, then you know your wireless device is working and ready to connect to one of the networks. You may prefer a user friendly tool like nm-applet (included in the [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) package) for typing in passwords and confirming that a connection has been made. Once the connection is set up, nm-applet is not needed, only the NetworkManager service.

##### ath9k and acer_wmi

Some people have reported conflicts between the ath9k and acer_wmi drivers, resulting in the wireless card not functioning. Blacklisting acer_wmi seems to resolve the issue.

#### LAN

*   Use module r8169 for eth0 support with kernel version >=2.6.26.
*   If you have problems with r8169 (unlikely), try r8101.

##### Aspire One D250/D255e LAN

With Archlinux 2010.05 the installation did not work on Aspire One D250/D255\. The modules were not available for either the Atheros LAN card or the Broadcom Wireless. To get the LAN working, try installing a newer developer image of [Arch.](https://releng.archlinux.org/isos/)

### Audio

Typical Intel HD Audio, works out-of-the-box, see [ALSA](/index.php/ALSA "ALSA").

**Note:** If the following steps do not help you to get your internal microphone working, follow the guidelines in this forum thread: [https://bbs.archlinux.org/viewtopic.php?pid=991291](https://bbs.archlinux.org/viewtopic.php?pid=991291).

#### With linux (alsa as modules)

Add one of these as a line in `/etc/modprobe.d/sound.conf`:

*   options snd-hda-intel model=acer-aspire
    *   **Recommended**. Everything works.
*   options snd-hda-intel model=acer
    *   Everything works, except the internal microphone and turning off the loudspeaker when a headset is plugged in. For some people the internal microphone may work.
*   options snd-hda-intel model=auto
    *   Both internal and external microphone does not work

#### With linux-one and linux-one-dev (alsa built into the kernel)

MIDI does not work with linux-one(-dev)!

Add one of these as a kernel option in `/boot/grub/menu.lst`:

*   snd-hda-intel.model=acer-aspire
    *   **Recommended**. Everything works.
*   snd-hda-intel.model=acer
    *   Everything works, except the internal microphone and turning off the loudspeaker when a headset is plugged in. For some people the internal microphone may work.
*   snd-hda-intel.model=auto
    *   Both internal and external microphone does not work

#### Audio test

`aplay /usr/share/sounds/alsa/Front_Center.wav`

#### Pulseaudio troubleshooting

*   [No mic input on Acer Aspire One](/index.php/PulseAudio/Troubleshooting#No_microphone_input_on_Acer_Aspire_One "PulseAudio/Troubleshooting")

### Video

Typical Intel chipset. Works with the xf86-video-intel driver.

You will need to install packages:

*   xorg
*   xf86-video-intel
*   xf86-input-synaptics

For Acer Spire One model D270 xf86-video-intel does not work. Install xf86-video-fbdev instead [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1232202#p1232202).

The Acer Aspire One model A0751h uses the [Poulsbo](/index.php/Poulsbo "Poulsbo") chipset, which is, as of October 2009, incompletely supported in Linux. Instead of using the xf86-video-intel driver, an unofficial repository and driver may be used. This is not an officially-supported driver, and it may or may not work for you. See [this thread in the forums](https://bbs.archlinux.org/viewtopic.php?id=78719) for current status.

Alternatively, using the instructions above and in the [Uvesafb](/index.php/Uvesafb "Uvesafb") article to set up the console framebuffer, and then installing and configuring the xf86-video-fbdev driver, will provide the full resolution -- backlight brightness control is impossible with this method, however.

For the original Linpus Xorg.conf (if you use this you may want to remove the ServerFlags section - the two entries in it disable the Ctrl-Alt-Backspace and Ctrl-Alt-F* hotkeys) please see [Example configurations](#Example_configurations).

#### External VGA port

The external VGA port works without further modifications if the externel screen is connected at boot time. If the screen is added later, the VGA port has to be enabled by `xrandr`. See also section [Additional function keys](#Additional_function_keys) for automating this.

#### Setting DPI

Very large fonts may appear in some applications (for example the menu line in Firefox). Setting the DisplaySize in the Monitor section in combination with the NoDDC option in `xorg.conf` may help:

```
Section "Device"
   ...
   Option    "NoDDC"
   ...
EndSection
...
Section "Monitor"
   ...
   DisplaySize 271 159 # Sets the correct DPI (96 x 96)
   ...
EndSection

```

When using an external screen, the NoDDC option has the effect, that XRandR may no longer be able to determine and use the maximum resolution of the screen. If you have such problems, delete the above lines from `xorg.conf`. Instead add the following to your `~/.xserverrc`:

```
#!/bin/bash
exec /usr/bin/X -dpi 100

```

You may also try 75dpi if you can live with small fonts.

You can also try to add the following to your `~/.Xdefaults`:

```
*dpi: 75

```

#### Setting a proper framebuffer

There are three options for setting the frame buffer (kernel mode setting, uvesafb, and intelfb). The most modern, thus recommended one is kernel mode setting (KMS). This is also the easiest to implement.

##### Kernel mode setting (KMS)

Follow the instructions here: [Intel#Kernel mode setting (KMS)](/index.php/Intel#Kernel_mode_setting_.28KMS.29 "Intel")

##### uvesafb

This will enable a 1024x600 framebuffer with 32bit color. Read [Uvesafb](/index.php/Uvesafb "Uvesafb") for details.

**Warning:** Before you begin, be aware that suspend will most probably not work with Uvesafb. When resuming you will end up with a blank screen.

##### Using intelfb without an initrd

Another option is to use the intelfb framebuffer. This is an option if you are using the linux-one-dev kernel, or any other kernel where intelfb is compiled in the kernel rather than as a module. It is also a good option if you do not want to use an initrd image on boot (hence using the new grub package below.)

First off install `grub2-915resolution` from AUR. (This may mean you need to modify the new /boot/grub/grub.cfg, see the wiki page for help)

To /boot/grub/grub.cfg add the 915 initialisation like so:

```
menuentry "kernel26-one-dev" {
set root=(hd0,1)
**insmod 915resolution
915resolution 5c 1024 600**
linux /vmlinuz-one-dev root=/dev/sda2 ro **video=intelfb vga=604**
}

```

**Note:** This method means you have to change to the new version of grub, which uses a new configuration format, and hence will not work with your old menu.lst

### Webcam

Works on the fly with the kernel26 (>=2.6.22) from core using the UVC kernel module (uvcvideo). Make sure that your user belongs to the "video" group.

Test the webcam:

*   Load the kernel module as root

```
modprobe uvcvideo

```

*   Install and run wxcam as a regular user

```
wxcam

```

*   To stop using the webcam related kernel modules (which saves some battery power)

```
echo uvcvideo videodev v4l1_compat video | xargs rmmod

```

**Tip:** Install and run [Powertop](/index.php/Powertop "Powertop") as root if you are interested in saving even more power.

### Card Reader

**Note:** For some people, this is not needed with the most recent BIOS v3309

To enable hotplugging for the card readers, add the following to `/etc/modprobe.d/pciehp.conf`:

```
options pciehp pciehp_force=1

```

Then add `pciehp` to the modules array in `/etc/rc.conf`:

```
MODULES=( ... pciehp ... )

```

As outlined in [this](https://bbs.archlinux.org/viewtopic.php?pid=879536#p879536) post, you might also need to add the following to your kernel command line (in `/boot/grub/menu.lst`):

```
pcie_ports=native

```

If this don't work, you can force a PCI rescan with this command (successfully tested on Acer Aspire One A110L/ZG5), solution source: [(SOLVED) *jmicron* SD card is recognised only if inserted on boot](https://bbs.archlinux.org/viewtopic.php?id=160309):

```
# echo 1 > /sys/bus/pci/rescan

```

As an alternative, which may possibly also enable powersaving for the card readers, get the [jmb38x_d3e.sh](http://petaramesh.org/public/arc/projects/AcerOne_Ubuntu/jmb38x_d3e.sh) script from the original Linpus install and install it in `/usr/local/sbin`. Remember to give executable rights. Note that this script uses [bc](https://www.archlinux.org/packages/?name=bc) which you may need to install.

Then add the following line to `/etc/rc.local`:

```
/usr/local/sbin/jmb38x_d3e.sh &>/var/log/jmb38x_d3e.log &

```

You may skip the log output if do not want this. You do not need the `pciehp` module in `/etc/rc.conf` if you use this script.

### Additional function keys

See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

### Touchpad

#### Two-Finger scrolling

To enable two-finger scrolling, paste the following in your .xinitrc and restart X:

```
 xinput set-int-prop "Synaptics Mouse" "Synaptics Two-Finger Pressure" 32 10
 xinput set-int-prop "Synaptics Mouse" "Synaptics Two-Finger Width" 32 6
 xinput set-int-prop "Synaptics Mouse" "Two-Finger Scrolling" 8 1
 xinput set-int-prop "Synaptics Mouse" "Synaptics Two-Finger Scrolling" 8 1 1
 xinput set-int-prop "Synaptics Mouse" "Synaptics Jumpy Cursor Threshold" 32 150

```

Note: you might need to change "Synaptics Mouse" to the name your touchpad was assigned.

## Power management

### Enabling CPU frequency scaling

See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

### Suspend on lid, shutdown on power button

Some people needed to install the kernel named "linux-one" in order to make this work properly. On the D250 (and possibly others), if the bios has not been updated to the latest (see elsewhere on this page for how to update the bios), then the 'lid' event is broken in the sense that it always reports 'closed' and it will continue to send lid events once triggered (thus blocking out power button events). In short, if you have problems with getting acpi events to work, update your bios.

See [acpid](/index.php/Acpid "Acpid") for more information.

## Example configurations

### /etc/rc.local

Read this first, for how to enable /etc/rc.local: [http://superuser.com/questions/278396/systemd-does-not-run-etc-rc-local](http://superuser.com/questions/278396/systemd-does-not-run-etc-rc-local)

Preferably, there should be a package that provided this, in a proper systemd-like way.

Please update this page if you find a better method.

```
 #!/bin/bash
 #
 # /etc/rc.local: Local multi-user startup script.
 #
 # Change writeback-time (as suggested by powertop)
 echo 1500 > /proc/sys/vm/dirty_writeback_centisecs
 # Enable laptop mode
 echo 5 > /proc/sys/vm/laptop_mode
 # Make the right SD-slot visible, as suggested by the Debian wiki
 setpci -d 197b:2381 AE=47
 # Set up the wifi-key
 /usr/bin/setkeycodes e055 159
 /usr/bin/setkeycodes e056 158
 # Set up the function keys
 /usr/bin/setkeycodes e025 130
 /usr/bin/setkeycodes e026 131
 /usr/bin/setkeycodes e027 132
 /usr/bin/setkeycodes e029 122
 /usr/bin/setkeycodes e071 134
 /usr/bin/setkeycodes e072 135

```

## Customized kernel

It is common to use customized kernels in these machines to avoid the extra load of modules Arch's stock kernel brings. These are ok for the wide general hardware but in this case you have a very specific set of hardware so that you can build a predefined kernel hardware support.

The [kernel-netbook](https://aur.archlinux.org/packages.php?ID=34625) package in the AUR provides a custom kernel supporting most netbooks with Intel Atom N270/N280/N450/N550 processors.

There is also a A110L specific kernel package [linux-one](https://aur.archlinux.org/packages/linux-one/) on AUR with all necessary modules compiled in kernel. Refer to the [Forum](https://bbs.archlinux.org/viewtopic.php?id=51796) for help on this. There may also be binaries of the latest version on the Forum but since these are user submitted packages you should *always* pick the sources and PKGBUILD, inspect them and build them yourself.

There is also [linux-one-dev](https://aur.archlinux.org/packages.php?ID=51296).

The config for this kernel is derived from the original Linpus Kernel config. The main differences from stock arch kernel:

*   The kernel differs from the stock arch kernel so it can only load Aspire One specific hardware and should not be used in any other hardware;
*   Faster boot time;
*   Reduced package size (although the hardware supported by this kernel will be limited to what it has compiled);
*   Tweaks for better performance on Atom processors;
*   Some tweaks/workarounds to get hardware work flawlessly (MMC/SD cards for example)

On [T.Mondary's site](http://thibm.free.fr) you can also find a precompiled kernel for AAO, in distribution-independent format, but suitable for ArchLinux. This minimal kernel comes with wifi led patches, a coretemp patch, acerhdf and a proper framebuffer with KMS. It can now use ext2 or ext4 (mounting ext4 without a journal is supported since 2.6.29) for the root filesystem, and does not require an initrd.

## Tuning tips

### SD Storage Expansion

#### Labeling Partitions

For using both card readers at a time you have to specify which is the one to use as storage expansion and the one to be used a removable storage by setting a label into the filesystem.

Plug only the expansion SD card into the left card reader and make the desired filesystem with one of the following:

*   XFS:

```
mkfs.xfs /dev/mmcblk0p1

```

*   EXT3

```
mkfs.ext3 /dev/mmcblk0p1

```

*   EXT2

```
mkfs.ext2 /dev/mmcblk0p1

```

Then give the filesystem a label:

*   XFS:

```
xfs_admin -L "SD_HOME" /dev/mmcblk0p1

```

*   EXT3/EXT2:

```
e2label /dev/mmcblk0p1 "SD_HOME"

```

#### Mount expansion as /home

Now that you have an SD card with a defined label, you can mount the SD card at boot. There are two methods for this: either by creating a mount option in `/etc/fstab`, or by adding a mount command to `/etc/rc.local`. The ordinary and recommended method for mounting disk at boot time is through `/etc/fstab`, but as this appears to lead to problems with the SD card reader in the AAO, a second method is listed below to try in case of errors.

##### Method 1: fstab entry

Define a mount option in `/etc/fstab`as defined in [Mounting Options](#Mounting_Options). Do not forget to change the folder which it is to be mounted on, it should be `/home`.

If you already have something in your `/home` folder you need to save a backup in order to upon mounting the SD expansion you have the same files as before so you can try this:

 `$ tar -cfg /home.tar /home` 

Now you can mount the device and put the backup there. Remember to put the line in fstab first and back up `/home` first!

**Warning:** Back up `/home` first. Always think twice before pressing return after `rm`.

```
$  rm -rf /home/*
$  mount /home
$  tar -xvf /home.tar -C /home/
$  rm /home.tar
```

##### Method 2: rc.local entry

For making rc.local work with systemd, see: [http://superuser.com/questions/278396/systemd-does-not-run-etc-rc-local](http://superuser.com/questions/278396/systemd-does-not-run-etc-rc-local)

Mounting `/home` on your SD card through fstab occasionally appears to lead to a problem described in [this](https://bbs.archlinux.org/viewtopic.php?pid=913240#p913240) forum thread, where the SD card gives a "FILESYSTEM CHECK FAILED" error during init on alternating boot-ups. This appears to have to do with the slower nature of SD-cards, and the system trying to mount the card before it is fully initialised.

An alternative method for mounting the SD card is adding `( sleep 4; mount /dev/mmcblk0p1 -t xfs -o defaults,noatime /home )&` to `/etc/rc.local`, and removing the entry of your SD card from `/etc/fstab`.

This command mounts the SD card with a 4 second delay, assuming you partitioned the card with the xfs filesystem. The ampersand after the command backgrounds the process, allowing the system to continue booting while the card mounts.

Find your SD card's UUID by issuing `$ ls -l /dev/disk/by-uuid/` or `# blkid` 

### Regulating the CPU fan

Letting the BIOS regulate the cpu fan results in a noisy monster of a netbook. You can override the default fan settings by using either `acerhdf` (recommended method) or `acerfand` (**not** recommended) based on two scripts.

#### acerhdf

The acerhdf kernel module regulates the fan in a performant and secure way.

From kernel 2.6.31 on the acerhdf module is provided inside the kernel tree. Therefore it comes precompiled with the linux, linux-one and linux-one-dev packages. If you use a kernel version <= 2.6.30 there is a package in AUR called [acerhdf](https://aur.archlinux.org/packages/acerhdf/), which you will have to build and install.

Up to acerhdf version 0.5.18:

```
 options acerhdf verbose=0 fanon=67 fanoff=62 interval=10 kernelmode=1

```

Since version 0.5.19:

```
 options acerhdf verbose=0 fanon=67000 fanoff=62000 interval=10 kernelmode=1

```

Or, to make the fan be more active and cool the AAO more, but make more noise:

Up to acerhdf version 0.5.18:

```
 options acerhdf verbose=0 fanon=62 fanoff=52 interval=10 kernelmode=1

```

Since version 0.5.19:

```
 options acerhdf verbose=0 fanon=62000 fanoff=52000 interval=10 kernelmode=1

```

Make sure you do not use the configuration for >=0.5.19 on <=0.5.18, as the computer will go warm.

The module option "kernelmode=1" automatically activates acerhdf's function.

### Using the Super key for middle-clicking

When browsing the web, a third mouse button is a great help for opening links in tabs. Unfortunately, there is no third mouse button on the Acer Aspire One.

However, one can configure one of the keys on the keyboard for acting like a third mouse button instead. (The Super key is the one with a picture of a little house, or on models that do not have a little house, the key between the fn and alt).

#### Using FVWM 2

Add these two lines to your .fvwm/.fvwm2rc (or just add the second line to your favorite startup function):

```
AddToFunc StartFunction
+ I Key Super_L A N FakeClick depth 0 press 2 wait 200 release 2

```

#### Using xte

1.  Install xautomation, which includes xte
2.  Set up your windowmanager to execute this command at the press of the Super key:

```
xte "mouseclick 2"

```

#### Using xbindkeys

Add this line to your **~/.xbindkeysrc.scm**:

```
 (xbindkey '("Super_L") "xte 'mouseclick 2 &'")

```

### SSD specific tweaks

See [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives").

### Updating the BIOS

#### Using FreeDOS

This method needs to be tested and finetuned. Note that not all USB-disks are possible to boot from.

*   Install [unetbootin](http://unetbootin.sourceforge.net/)
*   Use unetbootin to put FreeDOS on an USB stick
*   Download the latest BIOS from the Acer webpage (latest is 3310)
*   Unzip the BIOS-files to the USB stick
*   Reboot and configure the BIOS to boot from the USB stick before the SSD/HDD
*   Start the BIOS update utility (3310.BAT)
*   Reboot
*   Configure the BIOS to start from the SSD/HDD first again
*   Done

##### AOD150

The bios upgrades on the acer aspire site for the AOD150 line all want you to run it on windows. Here is how the author avoided it (The author does not understand this subject; she just guessed. Again, you are messing with your BIOS and this is not an officially condoned method, so there is a risk you will brick your netbook. You have been warned.):

*   Install [unetbootin](http://unetbootin.sourceforge.net/)
*   Use unetbootin to put FreeDOS on an USB stick
*   **Here is where it changes**
    *   Download the latest BIOS from the Acer webpage, for the AOA150 (latest is 3310). Note that this is the incorrect BIOS for your AOD150 model. From this zip file, you will be using everything except the actual BIOS image.
    *   Download the latest BIOS from the Acer webpage, for the AOD150 (latest is 1.09). Note that this is the correct BIOS, but requires windows to use, so you are only going to use the BIOS image from this file.
    *   Unzip the AOA150 zip file to a scratch directory. You may, for instance, get four files: a .bat file, a .fd file, flashit.exe, and a readme.txt. Copy everything but the .fd file onto your usb drive.
    *   Unzip the AOD150 zip file to a scratch directory. It should result in an exe file (KAV10109.exe) and a readme.txt. Now you have to get the .fd file from the .exe.
    *   Run the exe file using wine. It will extract some files, and then show an error from InsydeFlash complaining that it cannot load the drivers. *Do not* click 'Okay' yet.
    *   Alt-tab to a terminal, and cd into your wine installation's windows temp directory. Mine is $HOME/.wine/drive_c/windows/temp
    *   There should be directory there with the contents of what the exe file extracted. Mine is 7zSe6a.tmp/. If you cannot find it, you can run 'find . -iname InsydeFlash.exe', and whatever directory that file is in is what you want.
    *   Inside that directory should be a file with a .fd extension. Copy this file to your usb drive, alongside the .bat and .exe file you copied before.
    *   You can click 'Okay' and close your wine session now. This will clean up the temp directory, which is why you left it open.
    *   Now cd into your usb drive and edit the .bat file in a text editor of your choice. In it should be a line that calls flashit with one of the arguments being the .fd file for the AOA150\. Mine is '3310.fd'. Delete this, and replace it with the name of the file you just copied from the AOD150's installation. The contents of the batch file should now look something like:

```
flashit KAV10.fd /mc /all /dc

```

*   *   **You have now finished prepping your usb drive**
*   Reboot and configure the BIOS to boot from the USB stick before the SSD/HDD
*   Start the BIOS update utility (3310.BAT)
*   Reboot
*   Configure the BIOS to start from the SSD/HDD first again
*   Done
*   Note that when the author upgraded her BIOS, resuming from a suspend stopped working (blank screen, no keyboard response). To fix that, she removed the mtrr-related parameters from her kernel command-line in /boot/grub/menu.lst (enable_mtrr_cleanup mtrr_spare_reg_nr=1), which she had added before to fix some register quirks for the intel graphics card.

#### Using Flashrom

Flashrom can be used to flash the BIOS directly from Linux. It does not currently seem to support AA1, but it might be worth watching the flashrom-svn package in AUR. See also: [http://www.coreboot.org/Flashrom](http://www.coreboot.org/Flashrom)

#### Instructions by Acer for AOA110 and AOA150

This [routine](http://netbooks-us.custhelp.com/app/answers/detail/a_id/133/~/update-bios-on-aoa110-or-aoa150/) requires nothing more than that a couple of files are copied to a flash drive, and is confirmed to work on AOA110\. In case the link does not work here is an exact quote:

```
Updating the BIOS will require a USB flash drive to store the BIOS information on during the update. To perform the update to the BIOS:
  1\. Go here, click on the BIOS tab and download and extract the latest BIOS for the netbook.
  2\. The files required will be in the Dos_Flash subdirectory.
  3\. Rename the BIOS file from 3310.fd to zg5ia32.fd.
  4\. Copy zg5ia32.fd and Flashit.exe to USB flash drive
  5\. Ensure that the AC adapter is plugged in.
  6\. Insert the USB flash drive into a USB port.
  7\. Press and Hold down the Fn and the Esc keys together and press the power button.
  8\. When the unit's power light comes on wait a few seconds and release the Fn and Esc keys.
  9\. After the keys have been released the power light will start to blink.
 10\. During the BIOS update process the display will be blank.
 11\. Let the unit run and after approximately 1 to 7 minutes, the unit should reboot and the BIOS will be updated.

If the unit fails to reboot, or the BIOS was not updated sucessfully, try the steps again. If the problem persists, the netbook may need service.

Note: These instructions are only for the Acer Aspire One AOA110 and the AOA150 netbook series and should not be performed on any other model Acer Aspire One.

```

### Polishing the boot process

If you use Splashy for the boot graphics and LXDM for the X display manager, you will have a nice, polished and Arch-like boot.

*   [Splashy](/index.php/Splashy "Splashy") shows nice graphics instead of the text that scrolls by when you boot
*   [LXDM](/index.php/LXDM "LXDM") is a lightweight and nice version of xdm/gdm/kdm (logon manager / display manager)
*   [SLiM](/index.php/SLiM "SLiM") is also a possibility

### Compiling for the Atom processor

In /etc/makepkg.conf, set `-march=atom` and `-mtune=atom`

## See also

*   [AspireOneUser.com](http://aspireoneuser.com)
*   [Arch Forum](https://bbs.archlinux.org/viewtopic.php?id=51796)
*   [Install Ubuntu Hardy Heron (8.04.1) on Acer Aspire One](https://help.ubuntu.com/community/AspireOne)
*   [Installing Debian on Acer Aspire One](http://wiki.debian.org/DebianAcerOne)
*   [Gentoo on Acer Aspire One](http://en.gentoo-wiki.com/wiki/Acer_Aspire_One)
*   [AspireOneUser Forum](http://www.aspireoneuser.com/forum/viewforum.php?f=5&sid=29c7eef18d2d6477d7f9db91195fb31a)
*   [Moblin on Acer Aspire One](http://moblin.org/search/node/acer%20aspire%20one)
*   [Macles Blog](http://macles.blogspot.com)
*   [Slackware on Acer Aspire One](http://www.thev.net/cgi-bin/awki.cgi/_Acer_Aspire_One_?stamp=1222950371)
*   [Acer ftp-Server with Sources](http://ftp.twaren.net/Linux/Linpus/Aspire_One_Linpus_Linux)
*   [ArchOne ArchLinux live usb designed for AAO](http://arcierisinasce.wordpress.com/archone/)
*   [My new, old notebook](http://iki.fi/dt/minilaptop.html)