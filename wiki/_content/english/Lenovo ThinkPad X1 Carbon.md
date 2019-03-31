Related articles

*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")
*   [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)")

Lenovo ThinkPad X1 Carbon (X1C). There is also a touch version. Comes without optical drive. Has UEFI BIOS with BIOS-legacy fallback mode.

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Booting](#Booting)
    *   [1.1 Legacy-BIOS](#Legacy-BIOS)
    *   [1.2 UEFI](#UEFI)
    *   [1.3 Hanging on "HWP enabled" message](#Hanging_on_"HWP_enabled"_message)
*   [2 Hardware](#Hardware)
    *   [2.1 Audio](#Audio)
        *   [2.1.1 Xbindkeys](#Xbindkeys)
    *   [2.2 Network](#Network)
    *   [2.3 Touchscreen](#Touchscreen)
    *   [2.4 Video](#Video)
        *   [2.4.1 Brightness control](#Brightness_control)
            *   [2.4.1.1 Xbindkeys](#Xbindkeys_2)
            *   [2.4.1.2 ACPI](#ACPI)
        *   [2.4.2 Wrong EDID for external display](#Wrong_EDID_for_external_display)
    *   [2.5 KMS](#KMS)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Fingerprint Reader](#Fingerprint_Reader)
    *   [2.8 WWAN (Mobile broadband)](#WWAN_(Mobile_broadband))
    *   [2.9 GPS](#GPS)
    *   [2.10 Keyboard backlight](#Keyboard_backlight)
    *   [2.11 Bluetooth](#Bluetooth)
    *   [2.12 Mouse/Touchpad](#Mouse/Touchpad)
    *   [2.13 Docking](#Docking)

## Booting

### Legacy-BIOS

This procedure is far less involved than UEFI and works perfectly.

Boot into your BIOS and change the boot mode to Legacy. Then simply follow the normal [installation guide](/index.php/Installation_guide "Installation guide").

### UEFI

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

### Hanging on "HWP enabled" message

This is due to a [bug](https://bugzilla.kernel.org/show_bug.cgi?id=110941) introduced in Linux 4.4\. To work around it, add `intel_pstate=no_hwp` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## Hardware

Almost everything works out of the box.

### Audio

Sound works out of the box.

#### Xbindkeys

For alternative window managers (Fluxbox, etc..), try installing [xbindkeys](/index.php/Xbindkeys "Xbindkeys") and adding the following to `~/.xbindkeysrc`:

```
"amixer -c 0 set Master 1dB-"
  XF86AudioLowerVolume
"amixer -c 0 set Master 1dB+"
  XF86AudioRaiseVolume

```

### Network

Wired networking works out of the box with the Ethernet to USB adapter. Wireless works out of the box using the `iwlwifi` module.

 `$ lspci`  `output: Network controller: Intel Corporation Centrino Advanced-N 6205 [Taylor Peak] (rev 96)` 

### Touchscreen

Works out of the box. To enable multi-touch, install [Touchegg](/index.php/Touchegg "Touchegg").

### Video

The video card installed is Intel HD Graphics 4000\. See [intel](/index.php/Intel "Intel") for more info.

#### Brightness control

Default brightness adjustment keys work but need to be pressed multiple times to increase/decrease the screen brightness. Use either the [#Xbindkeys_2](#Xbindkeys_2) or [#ACPI](#ACPI) methods to fix this.

Some desktop environments may lack granularity while changing brightness. This is due to the DE (e.g. gnome-settings-daemon) along with the internal graphics module changing the brightness when brightness adjustment keys are pressed causing multiple steps per press. To work around this add the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `video.brightness_switch_enabled=0`.

##### Xbindkeys

Install [xbindkeys](/index.php/Xbindkeys "Xbindkeys") and append the following to `~/.xbindkeysrc`:

```
"xbacklight -dec 5"
  XF86MonBrightnessDown
"xbacklight -inc 5"
  XF86MonBrightnessUp

```

##### ACPI

Writing custom ACPI handlers for the brightness adjustment keys seems to have no effect. In order to use them properly you need to add the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `acpi_osi="!Windows 2012"`. See also [Backlight#ACPI](/index.php/Backlight#ACPI "Backlight"). Note that the ACPI backlight is [disabled by default](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=fbc9fe1b4f222a7c575e3bd8e9defe59c6190a04) on Windows 8 hardware with a native backlight. Consider using the [#Xbindkeys](#Xbindkeys) approach instead.

#### Wrong EDID for external display

With certain connectors (e.g. MiniDP to VGA), there is a bug getting EDID for the external screen while booting:

```
[ 93.736330] [drm:intel_dp_i2c_aux_ch] *ERROR* too many retries, giving up

```

This does not occur if the external screen is connected after booting.

The correct mode can be added per [xrandr#Adding undetected resolutions](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr"):

```
xrandr --newmode 1920x1200_60 154 1920 1968 2000 2080 1200 1203 1209 1235 -hsync +vsync
xrandr --addmode DP1 1920x1200_60
xrandr --output DP1 --mode 1920x1200_60
```

### KMS

Enable [KMS](/index.php/KMS "KMS") using the `i915` module and by enabling VT in BIOS.

### Webcam

Works out of the box. Tested with guvcview

### Fingerprint Reader

Works out of the box with [Fprint](/index.php/Fprint "Fprint").

For a GUI [fingerprint-gui](https://aur.archlinux.org/packages/fingerprint-gui/) from the [AUR](/index.php/AUR "AUR") is already patched to work with the X1's newer fingerprint reader. To get the gui's dropdown to recognize your device, you will have to add your user to the `plugdev` group:

```
$ gpasswd -a <username> plugdev

```

See [fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui") for more information about config

* * *

`lsusb` *output: 147e:2020 Upek TouchChip Fingerprint Coprocessor (WBF advanced mode)*

### WWAN (Mobile broadband)

This model includes a [Ericsson H5321gw](https://www.thinkwiki.org/wiki/Ericsson_H5321_gw_Mobile_Broadband_Module) adapter that can be used as a mobile broadband adapter and GPS.

The SIM-card must be inserted in the back of the laptop.

Add text to the following file and reboot

 `/etc/modprobe.d/avoid-mbib.conf`  `options cdc_ncm prefer_mbim=N` 

Tested OK with [NetworkManager](/index.php/NetworkManager "NetworkManager") with [modemmanager](https://www.archlinux.org/packages/?name=modemmanager) installed

* * *

`lsusb` *output: 0bdb:1926 Ericsson Business Mobile Networks BV*

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

Or use e.g. [foxtrotgps](https://aur.archlinux.org/packages/foxtrotgps/) in [AUR](/index.php/AUR "AUR").

See [this link](https://www.thinkwiki.org/wiki/Ericsson_H5321_gw_Mobile_Broadband_Module) for more info.

* * *

`lsusb` *output: 0bdb:1926 Ericsson Business Mobile Networks BV*

### Keyboard backlight

Works out of the box. Use FN+Space

### Bluetooth

First try to set up [Bluetooth](/index.php/Bluetooth "Bluetooth") normally. If you get kernel error messages:

```
kernel: bluetooth hci0: Direct firmware load for brcm/BCM20702A1-0a5c-21e6.hcd failed with error -2
kernel: Bluetooth: hci0: BCM: Patch brcm/BCM20702A1-0a5c-21e6.hcd not found 

```

You need to manually install the proprietary firmware. The slackware wiki describes one way to do this: [http://www.slackwiki.com/Btfirmware-nonfree](http://www.slackwiki.com/Btfirmware-nonfree).

### Mouse/Touchpad

Works out of the box. See [TrackPoint](/index.php/TrackPoint "TrackPoint") for additional details.

### Docking

This model has no docking port.

Video for USB 3 Docking Stations currently is [not supported](http://www.displaylink.org/forum/showthread.php?t=1748), so you must use a [USB Port Replicator with Digital Video (USB 2.0)](https://www.thinkwiki.org/wiki/USB_Port_Replicator_with_Digital_Video)

This supports:

*   USB-devices connected to dock
*   Audio
*   Microphone
*   Ethernet
*   Video (see [DisplayLink](/index.php/DisplayLink "DisplayLink"))