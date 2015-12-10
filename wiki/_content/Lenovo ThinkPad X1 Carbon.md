# Lenovo ThinkPad X1 Carbon

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")

## Contents

*   [1 Model description](#Model_description)
    *   [1.1 Legacy-BIOS](#Legacy-BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Hardware](#Hardware)
    *   [2.1 Audio](#Audio)
        *   [2.1.1 Xbindkeys](#Xbindkeys)
    *   [2.2 Network](#Network)
        *   [2.2.1 Wired](#Wired)
        *   [2.2.2 Wireless](#Wireless)
    *   [2.3 Touchscreen](#Touchscreen)
    *   [2.4 Video](#Video)
        *   [2.4.1 Brightness control](#Brightness_control)
            *   [2.4.1.1 Xbindkeys](#Xbindkeys_2)
        *   [2.4.2 EDID bug](#EDID_bug)
    *   [2.5 KMS](#KMS)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Fingerprint Reader](#Fingerprint_Reader)
    *   [2.8 WWAN (Mobile broadband)](#WWAN_.28Mobile_broadband.29)
    *   [2.9 GPS](#GPS)
    *   [2.10 Keyboard backlight](#Keyboard_backlight)
    *   [2.11 Bluetooth](#Bluetooth)
    *   [2.12 Mouse/Touchpad](#Mouse.2FTouchpad)
*   [3 Other hardware](#Other_hardware)
    *   [3.1 Docking](#Docking)

## Model description

Lenovo ThinkPad X1 Carbon (X1C). There is also a touch version. Comes without optical drive. Has UEFI BIOS with BIOS-legacy fallback mode.

**Tip:** A great resource for thinkpads is [http://www.thinkwiki.org/wiki/ThinkWiki](http://www.thinkwiki.org/wiki/ThinkWiki)

### Legacy-BIOS

This procedure is far less involved than UEFI and works perfectly.

In order to turn off UEFI booting you will need to boot into your BIOS and change the boot mode to Legacy. Afterward, follow the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") for standard installation instructions.

### UEFI

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB").**

**Notes:** unnecessary duplication (Discuss in [Talk:Lenovo ThinkPad X1 Carbon#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_X1_Carbon))

Use [archboot](/index.php/Archboot "Archboot") to install or see [https://bbs.archlinux.org/viewtopic.php?pid=1288500#p1288500](https://bbs.archlinux.org/viewtopic.php?pid=1288500#p1288500)

1\. You follow the guide from here and skip the part about errors and refind: [Create_UEFI_bootable_USB_from_ISO](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface")

2\. Make sure you USB is mounted to /boot/efi and install grub, like so:

```
$ grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --boot-directory=/boot/efi/ --recheck --debug

```

OBS: You can remove the entry from your EFI bootmanger, with efibootmgr by issuing:

```
$ efibootmgr -b XX -B

```

3\. Now you can choose if you wanna hack you grub.cfg or use the custom config in grub.d. Either way generate the grub.cfg:

```
$ grub-mkconfig -o /boot/efi/grub/grub.cfg

```

4\. Make certain appropriate changes have been made to grub.cfg. My working example, which could use cleaning:

 `/etc/grub.d/10_linux` 

```
### BEGIN /etc/grub.d/10_linux ###
menuentry 'Arch Linux test'  {
	load_video
	set gfxpayload=keep
	insmod gzio
	insmod part_gpt
	insmod ext2
	set root='hd0,gpt1'
	if [ x$feature_platform_search_hint = xy ]; then
	  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1  B35D-FE34
	else
	  search --no-floppy --fs-uuid --set=root B35D-FE34
	fi
	echo	'Loading Linux core repo kernel ...'
	linux	/arch/boot/x86_64/vmlinuz root=UUID=B35D-FE34 ro  archisobasedir=arch archisolabel=ARCH_201306
	echo	'Loading initial ramdisk ...'
	initrd	/arch/boot/x86_64/archiso.img
}

### END /etc/grub.d/10_linux ###

```

5\. Move the grub.efi to overwrite the archiso supplied one (which btw works on my desktop. I guess GRUB includes more workarounds for buggy firmware from manufactureres. See this video, if you have time: [http://mjg59.dreamwidth.org/10014.html](http://mjg59.dreamwidth.org/10014.html)

```
$ mv /boot/efi/EFI/arch_grub/grubx64.efi /mnt/efi/EFI/boot/bootx64.efi

```

Success. Somethings are implied, like GPT partitiontable etc.

## Hardware

Almost everything works out of the box.

### Audio

Sound works out of the box.

#### Xbindkeys

For alternative window managers (Fluxbox, etc..), try installing [xbindkeys](/index.php/Xbindkeys "Xbindkeys") and adding the following to ~/.xbindkeysrc

```
"amixer -c 0 set Master 1dB-"
  XF86AudioLowerVolume
"amixer -c 0 set Master 1dB+"
  XF86AudioRaiseVolume

```

### Network

#### Wired

Comes with USB->Ethernet plug. Works out of the box.

#### Wireless

Works out of the box. Uses the following module

*   iwlwifi

* * *

`lspci` _output: Network controller: Intel Corporation Centrino Advanced-N 6205 [Taylor Peak] (rev 96)_

### Touchscreen

Works out of the box. To enable multi-touch, install [Touchegg](/index.php/Touchegg "Touchegg").

### Video

The video card installed is Intel HD Graphics 4000\. See [intel](/index.php/Intel "Intel") for more info.

#### Brightness control

Default brightness adjustment keys work but need to be pressed multiple times to increase/decrease the screen brightness. Writing your own acpi handlers for those buttons seems to have no effect. In order to use it properly you need to append a new kernel parameter and make new grub config. Make sure to escape double quotes. For Grub:

 `/etc/default/grub` 

```
GRUB_CMDLINE_LINUX_DEFAULT="acpi_osi=\"!Windows 2012\""

```

```
sudo grub-mkconfig -o /boot/grub/grub.cfg

```

For Syslinux:

 `/boot/syslinux/syslinux.cfg` 

```
APPEND root=/dev/sda2 rw acpi_osi="!Windows 2012"

```

Read more about why it's necessary at [Backlight#ACPI](/index.php/Backlight#ACPI "Backlight")

Some depending on their desktop environment may lack granularity while changing brightness. This is due to the DE (e.g. gnome-settings-daemon) along with the internal graphics module changing the brightness when brightness adjustment keys are pressed causing multiple steps per press. To work around this one can add the following to their boot parameters:

```
video.brightness_switch_enabled=0

```

##### Xbindkeys

For alternative window managers (Fluxbox, etc..), try installing [xbindkeys](/index.php/Xbindkeys "Xbindkeys") and adding the following to ~/.xbindkeysrc

```
"xbacklight -dec 5"
  XF86MonBrightnessDown
"xbacklight -inc 5"
  XF86MonBrightnessUp

```

#### EDID bug

**Note:** Update: This is due to the use of a mini-DP->VGA-adapter. Tested without bugs with a mini-DP->DP-cable.

There is a bug getting EDID for the external screen when connected at bootup.

I get this error message

```
[ 93.736330] [drm:intel_dp_i2c_aux_ch] *ERROR* too many retries, giving up

```

If external screen is connected after bootup everything works fine.

I had to manually add a modeline and set the preferred resolution with this script.

 `/usr/local/bin/dp-output` 

```
# Monitor setup
EXTERNAL_OUTPUT="DP1"
INTERNAL_OUTPUT="LVDS1"

xrandr |grep $EXTERNAL_OUTPUT | grep " connected " | if [ $? -eq 0 ]; then
        xrandr --newmode 1920x1200_60 154 1920 1968 2000 2080 1200 1203 1209 1235 -hsync +vsync
        xrandr --addmode DP1 1920x1200_60
        xrandr --output $INTERNAL_OUTPUT --off --output $EXTERNAL_OUTPUT --mode 1920x1200_60
fi

```

And add the script to startup at X-session start. Since I use [SLiM](/index.php/SLiM "SLiM") it`s done with this setting in slim.conf

 `/etc/slim.conf`  `sessionstart_cmd dp-output` 

### KMS

Get [KMS](/index.php/KMS "KMS") working by adding i915 to the modules line

 `/etc/mkinitcpio.conf`  `MODULES="i915"` 

```
$ mkinitcpio -p linux

```

You also have to enable VT in BIOS.

### Webcam

Works out of the box. Tested with guvcview

### Fingerprint Reader

Works out of the box with [Fprint](/index.php/Fprint "Fprint").

For a GUI [fingerprint-gui](https://aur.archlinux.org/packages/fingerprint-gui/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") is already patched to work with the X1's newer fingerprint reader. To get the gui's dropdown to recognize your device, you will have to add your user to the `plugdev` group:

```
$ gpasswd -a <username> plugdev

```

See [fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui") for more information about config

* * *

`lsusb` _output: 147e:2020 Upek TouchChip Fingerprint Coprocessor (WBF advanced mode)_

### WWAN (Mobile broadband)

This model includes a [Ericsson H5321gw](http://www.thinkwiki.org/wiki/Ericsson_H5321_gw_Mobile_Broadband_Module) adapter that can be used as a mobile broadband adapter and GPS.

The SIM-card must be inserted in the back of the laptop.

Add text to the following file and reboot

 `/etc/modprobe.d/avoid-mbib.conf`  `options cdc_ncm prefer_mbim=N` 

Tested OK with [NetworkManager](/index.php/NetworkManager "NetworkManager") with [modemmanager](https://www.archlinux.org/packages/?name=modemmanager) installed

* * *

`lsusb` _output: 0bdb:1926 Ericsson Business Mobile Networks BV_

### GPS

Install gpsd from extra and mbm-gpsd-git from AUR. Add this to the following file

 `/etc/udev/rules.d/99-mbm.rules` 

```
ATTRS{idVendor}=="0bdb", ATTRS{idProduct}=="1926", ENV{ID_USB_INTERFACE_NUM}=="09", ENV{MBM_CAPABILITY}="gps_nmea"
ATTRS{idVendor}=="0bdb", ATTRS{idProduct}=="1926", ENV{ID_USB_INTERFACE_NUM}=="03", ENV{MBM_CAPABILITY}="gps_ctrl"

```

Reboot to reload udev rules.

Run `sudo mbm-gpsd`

See if there is GPS-output `cat /dev/gps0`

Run `sudo gpsd -b -N /dev/gps0`

To test it `xgps`

Or use e.g. [foxtrotgps](https://aur.archlinux.org/packages/foxtrotgps/)<sup><small>AUR</small></sup> in [AUR](/index.php/AUR "AUR").

See [this link](http://www.thinkwiki.org/wiki/Ericsson_H5321_gw_Mobile_Broadband_Module) for more info.

* * *

`lsusb` _output: 0bdb:1926 Ericsson Business Mobile Networks BV_

### Keyboard backlight

Works out of the box. Use FN+Space

### Bluetooth

Works out of the box. Test with:

```
$ systemctl start bluetooth
$ bluetoothctl

[bluetooth]# power on

```

### Mouse/Touchpad

Works out of the box. See [TrackPoint](/index.php/TrackPoint "TrackPoint") for details.

## Other hardware

### Docking

This model comes without a docking port.

Since the video for USB 3 Docking Stations currently is not supported[[1]](http://www.displaylink.org/forum/showthread.php?t=1748), I had to go for [USB Port Replicator with Digital Video (USB 2.0)](http://www.thinkwiki.org/wiki/USB_Port_Replicator_with_Digital_Video)

This works:

*   USB-devices connected to dock
*   Audio
*   Microphone
*   Ethernet
*   Video (follow [DisplayLink](/index.php/DisplayLink "DisplayLink") guide)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X1_Carbon&oldid=369886](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X1_Carbon&oldid=369886)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")