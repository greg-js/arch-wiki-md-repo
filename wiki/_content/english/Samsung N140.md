This article provides information about installing and setting up Arch Linux on the Samsung N140\. It is also relevant for the Samsung N130 which is identical except for the omission of Bluetooth and stereo speakers (and possibly a different battery capacity). There are versions of the N130 which include a 3G cellular modem, available from Vodafone and China Mobile. The [Samsung NC10](/index.php/Samsung_NC10 "Samsung NC10") is similar but not identical to the N140, so you may or may not find useful information on that page.

## Contents

*   [1 Installation](#Installation)
*   [2 Configure your installation](#Configure_your_installation)
    *   [2.1 Ethernet](#Ethernet)
    *   [2.2 Wifi](#Wifi)
        *   [2.2.1 Atheros AR9285](#Atheros_AR9285)
        *   [2.2.2 Realtek RTL8192E](#Realtek_RTL8192E)
    *   [2.3 Cellular 3G Modem](#Cellular_3G_Modem)
    *   [2.4 Graphics Adapter](#Graphics_Adapter)
        *   [2.4.1 Kernel Mode Setting](#Kernel_Mode_Setting)
            *   [2.4.1.1 Method A](#Method_A)
            *   [2.4.1.2 Method B](#Method_B)
        *   [2.4.2 Backlight Brightness](#Backlight_Brightness)
        *   [2.4.3 External VGA](#External_VGA)
    *   [2.5 Audio](#Audio)
    *   [2.6 Suspend and hibernate](#Suspend_and_hibernate)
        *   [2.6.1 Hibernate](#Hibernate)
    *   [2.7 Fn keys](#Fn_keys)
        *   [2.7.1 Binding Fn keys in Openbox](#Binding_Fn_keys_in_Openbox)
    *   [2.8 Saving Power](#Saving_Power)

## Installation

Do the standard Arch installation procedure from the ARCH CD ISO using an external USB CDROM drive. Alternatively boot the Arch installer from a USB flash drive. The standard Arch kernel is recommended.

## Configure your installation

### Ethernet

RTL8101e/8102e fast ethernet. Works out of the box.

### Wifi

The supplied wifi device is either an Atheros AR9285 (PCI ID = 168c:002b) (European markets) or a Realtek RTL8192E (US and UK markets).

#### Atheros AR9285

```
02:00.0 Network controller [0280]: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) [168c:002b] (rev 01)

```

The kernel module for this device is "ath9k". Kernels 2.6.32 release candidates and later seem to work fine.

#### Realtek RTL8192E

```
02:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8192E/RTL8192SE Wireless LAN Controller (rev 01)

```

Confirmed working out of the box on the current release (2014.07.03), with 3.15.3 Kernel.

### Cellular 3G Modem

_Specifications required_

### Graphics Adapter

The video controller is an Intel chipset that works with the xf86-video-intel driver.

```
00:02.0 VGA compatible controller [0300]: Intel Corporation Mobile 945GME Express Integrated Graphics Controller [8086:27ae] (rev 03)
00:02.1 Display controller [0380]: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller [8086:27a6] (rev 03)

```

#### Kernel Mode Setting

See also [Intel#KMS .28Kernel Mode Setting.29](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel").

[KMS](/index.php/KMS "KMS") works providing real consoles at the native LCD resolution, 1024x600. There is a known problem with 2.6.32 kernels (later release candidates up to at least release 2.6.32.8), which results in screen flickering and blackouts about 5 minutes after resuming from suspend-to-RAM or suspend-to-disk.

**Note:**

*   If you encounter screen flickering or blackouts with KMS enabled, try setting **i915.powersave=0** as a kernel boot option
*   Since version 2.10.0 of `xf86-video-intel`, support for UMS has been removed from the intel driver. This means that KMS is a requirement now

##### Method A

If you are using a kernel with no inital ramdisk and you can simply add the required options to the GRUB kernel line:

```
# (3) Arch Linux N130
title  Arch Linux Custom N130 Kernel
root   (hd0,YOURROOT-1)
kernel /boot/vmlinuz26-N130 root=/dev/sdaYOURROOT resume=/dev/sdaYOURSWAP ro quiet **i915.powersave=0 i915.modeset=1**

```

##### Method B

If you are using an initial ramdisk (either the standard kernel or the custom kernel method B above) then do the following:

Edit `/etc/modprobe.d/modprobe.conf`:

```
options i915 powersave=0 
options i915 modeset=1

```

Edit `/etc/mkinitcpio.conf`:

```
MODULES="intel_agp i915"
FILES="/etc/modprobe.d/modprobe.conf"

```

Put keymap early in `/etc/mkinitcpio.conf` HOOKS. Regenerate the init ramdisk for the kernel(s) you are running:

```
$ mkinitcpio -p linux

```

Remove any vga= or video= from grub `/boot/grub/menu.lst` kernel line, and reboot.

#### Backlight Brightness

Brightness function keys confirmed working out of the box on current release (2014.07.03) with 3.15.3 kernel.

#### External VGA

External VGA works out of the box with xrandr / krandrtray. Tested at 1920x1080 resolution.

### Audio

The audio device is an Intel HD.

```
00:1b.0 Audio device [0403]: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller [8086:27d8] (rev 02)

```

### Suspend and hibernate

Suspend and hibernate work out of the box with `systemd-logind`. See below for setting up resuming from [hibernation](https://wiki.archlinux.org/index.php/Samsung_N140#Hibernate).

Edit `/etc/systemd/logind.conf` to change default key handling.

```
/etc/systemd/logind.conf
---------------------------------------
HandlePowerKey=poweroff
HandleSuspendKey=suspend
HandleHibernateKey=hibernate
HandleLidSwitch=suspend

```

Don't forget to restart the service after making changes

```
# systemctl restart systemd-logind.service

```

You can call the functions from the command line with `systemctl _function_`

Alternatively using a power manager, for example `xfce4-power-manager`, you can control key handling from a GUI.

If you are a KDE4 user you can take advantage of powerdevil (included in kdemod-core/kdemod-kdebase-workspace since release 4.2) to manipulate the screen brightness, cpu scaling and hibernate. Suspend from KDE works too, but if you are using handler.sh to suspend on the button/lid and button/sleep acpi events, then KDE only needs to lock the screen. Note that cpu scaling requires acpi-cpufreq module to be loaded at boot.

#### Hibernate

Hibernate works out of the box with `systemd`, but you need to have a SWAP file/partition.

You will need to add `resume=swap_partition` to your kernel parameters. Example below for GRUB.

```
/etc/default/grub
---------------------------------------------
GRUB_CMDLINE_LINUX_DEFAULT="resume=/dev/sda1"

```

Run `grub-mkconfig -o /boot/grub/grub.cfg`

If you use an initramfs (default for Arch), you need to add the `resume` hook into the configuration of [mkinitcpio](https://wiki.archlinux.org/index.php/Mkinitcpio)

```
/etc/mkinitcpio.conf
---------------------------------------------------------------
# resume must be placed after block and lvm2, but before filesystems
HOOKS="... block lvm2 resume filesystems ..."

```

Then, rebuild the initrd image

```
# mkinitcpio -p linux

```

### Fn keys

#### Binding Fn keys in Openbox

In [Openbox](/index.php/Openbox "Openbox") one can use the internal keybind setup instead of xbindkeys. Example of rc.xml (In this instance, volume Fn Keys):

```
   <keybind key="XF86AudioRaiseVolume">
     <action name="Execute">
       <command>amixer set Master 5%+ unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioLowerVolume">
     <action name="Execute">
       <command>amixer set Master 5%- unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioMute">
     <action name="Execute">
       <command>amixer set Master toggle</command>
     </action>
   </keybind>

```

### Saving Power

Read [Laptop#Power management](/index.php/Laptop#Power_management "Laptop").

The Samsung N130/N140 contains a 1.6 GHz Intel Atom ULV (ultra low voltage) N270 processor, designed for low power consumption. The power consumption of the netbook (not just the processor) can be as low as 6W on idle with HDD spun down, although a typical figure under normal usage would be considerably higher.

Obviously the battery life depends on battery capacity as well as power consumption. The supplied battery varies in different markets. This list is a guideline only. Do not rely on this information before purchase -- check with YOUR vendor and update this wiki if it is incorrect:

```
Voltage 11.1V

```

```
N130             = 4000mAh [44Wh] (most markets), 5200mAh [57Wh] (Sweden)
N130 (Vodafone)  = ? [?] (Spain)
N130 (CMCC)      = ? [?] (China)
N140             = 5200mAh [57Wh] (US, Germany, France, Sweden), 5900mAh [65Wh] (UK)
Extended battery = 7800mAh [86Wh]

```

Install [powertop](https://www.archlinux.org/packages/?name=powertop) which is a [very useful tool](/index.php/Powertop "Powertop") for measuring and tuning power consumption.

Enable CPU frequency scaling (P-states) by loading the driver module `acpi-cpufreq`. This is most conveniently done dropping a namesake file in `/etc/modules-load.d`:

 `/etc/modules-load.d/acpi-cpufreq.conf` 

```
acpi-cpufreq

```

Select the CPU frequency governor by adding the following lines to a systemd tmpfile:

 `/etc/tmpfiles.d/local.conf` 

```
 w /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor - - - - ondemand
 w /sys/devices/system/cpu/cpu1/cpufreq/scaling_governor - - - - ondemand

```

**Note:** Contrary to the advice in many places `hdparm -B 255 /dev/sda` does NOT necessarily turn off advanced power management. What happens depends on the disk model. With the Samsung HM160HI disk 255 results in very frequent spindowns