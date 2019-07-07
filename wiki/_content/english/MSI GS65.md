| **Device** | **Status** | **Modules** |
| Intel GPU | Working | modesetting |
| Nvidia GPU | Working | nvidia (not nouveau) |
| Ethernet | Working | alx |
| Wireless | Working | iwlwifi |
| Audio | Working | snd_hda_intel |
| Webcam | Working | uvcvideo |
| Bluetooth | Working | btusb |
| USB | Working |
| Thunderbolt | Working | thunderbolt |
| Power management | Partially Working |
| Keyboard | Partially Working |
| Touchpad | Partially Working | libinput |

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 BIOS](#BIOS)
        *   [1.1.1 2.20.1271](#2.20.1271)
        *   [1.1.2 E16Q2IMS.110](#E16Q2IMS.110)
    *   [1.2 Video](#Video)
        *   [1.2.1 Backlight](#Backlight)
        *   [1.2.2 Drivers](#Drivers)
        *   [1.2.3 Multihead](#Multihead)
    *   [1.3 Webcam](#Webcam)
    *   [1.4 Power Management](#Power_Management)
    *   [1.5 Keyboard](#Keyboard)
        *   [1.5.1 Lights](#Lights)
        *   [1.5.2 Button Mapping](#Button_Mapping)
            *   [1.5.2.1 Airplane Mode Key Combination](#Airplane_Mode_Key_Combination)
            *   [1.5.2.2 Unmapped Buttons](#Unmapped_Buttons)
        *   [1.5.3 Non-US Keyboards' Backslash/Pipe 102nd Key](#Non-US_Keyboards'_Backslash/Pipe_102nd_Key)
    *   [1.6 Touchpad](#Touchpad)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Webcam is not detected](#Webcam_is_not_detected)
*   [3 Tips and Tricks](#Tips_and_Tricks)
    *   [3.1 Microphone noise reduction](#Microphone_noise_reduction)
*   [4 Known Issues](#Known_Issues)
    *   [4.1 Lockup Issue (lspci and poweroff hang)](#Lockup_Issue_(lspci_and_poweroff_hang))
    *   [4.2 Cheese Hangs While Opening Camera](#Cheese_Hangs_While_Opening_Camera)
    *   [4.3 Wifi is hardblocked (airplane mode) after waking up from suspend](#Wifi_is_hardblocked_(airplane_mode)_after_waking_up_from_suspend)
    *   [4.4 System freeze](#System_freeze)
    *   [4.5 Display outputs don't work after suspend](#Display_outputs_don't_work_after_suspend)
*   [5 More Information](#More_Information)
    *   [5.1 MS-16Q2](#MS-16Q2)
        *   [5.1.1 Microarchitecture, Processor and Platform](#Microarchitecture,_Processor_and_Platform)
        *   [5.1.2 PCI Devices](#PCI_Devices)
        *   [5.1.3 USB Devices](#USB_Devices)
        *   [5.1.4 Input Devices](#Input_Devices)

## Configuration

### BIOS

#### 2.20.1271

At bootup, the BIOS settings page is entered via the delete key, the quick boot select window can be activated via the F11 key, PXE scanning can be activated via the F12 key

In the BIOS setings, the model name can be seen in the Main tab, [Secure Boot](/index.php/Secure_Boot "Secure Boot") can be disabled from the Security tab and boot mode can optionally be switched from [UEFI](/index.php/UEFI "UEFI") to legacy. Advanced BIOS options can be accessed by going to the 'Advanced' tab and holding down l-alt, then pressing r-ctrl, r-shift, then F2.

There is no known option to disable the discrete intel GPU, there may be one present after unlocking the advanced options.

#### E16Q2IMS.110

This BIOS version introduces many ACPI problems (if BIOS is changed from [UEFI](/index.php/UEFI "UEFI") to legacy), including a flood of "No handler or method for GPE [00->6E]" at boot, which can be solved through kernel parameters:

*   `acpi=off` allows to boot but most things won't work, including the keyboard and touchpad.
*   `pci=nomsi` or `acpi=off acpi=force` allows to boot and have working keyboard and touchpad, but the NVidia card won't work ; neither will the USB3 ports.
*   `pcie_aspm=off` will allow most things to work: keyboard, touchpad, USB 3 devices, NVidia card.

### Video

#### Backlight

[Backlight](/index.php/Backlight "Backlight") works out of the box

 `# ls /sys/class/backlight/` 
```
intel_backlight

```

#### Drivers

[PRIME](/index.php/PRIME "PRIME") functionality works by using only [nvidia](https://www.archlinux.org/packages/?name=nvidia) and will work without the intel video driver, instead using modsetting.

The [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) driver does not work well in PRIME configuration (see [#Known Issues](#Known_Issues)}).

#### Multihead

[Multihead](/index.php/Multihead "Multihead") support works with intel-virtual-output tool, following the 'port wired to Nvidia' instructions at [Bumblebee](https://github.com/Bumblebee-Project/Bumblebee/wiki/Multi-monitor-setup) and using this post at [Stack Exchange](https://superuser.com/questions/1082617/bumblebee-with-hdmi-on-nvidia-make-usable-both-with-without-connected-monitor).

Thunderbolt port is wired to Intel GPU thus allowing for external monitor to be used with nvidia gpu off.

### Webcam

The webcam is device 003 on bus 001\. See [Webcam setup](/index.php/Webcam_setup "Webcam setup") for more details.

 `# lsusb -vs 001:003` 
```
Bus 001 Device 003: ID 5986:211c Acer, Inc 
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.01
  bDeviceClass          239 Miscellaneous Device
  bDeviceSubClass         2 
  bDeviceProtocol         1 Interface Association
  bMaxPacketSize0        64
  idVendor           0x5986 Acer, Inc
  idProduct          0x211c 
  bcdDevice            3.01
  iManufacturer           1 SunplusIT Inc
  iProduct                2 HD Webcam
  iSerial                 0 
  bNumConfigurations      1
...

```

### Power Management

Battery indicator works out of the box.

Sleep and wake also work with the proper configuration (see [Power management](/index.php/Power_management "Power management")).

An issue when sleeping is that the networking will be disabled when waking and set to airplane mode. This issue does not affect hibernation.

### Keyboard

#### Lights

 `# lsusb -vs 001:002` 
```
Bus 001 Device 002: ID 1038:1122 SteelSeries ApS 
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass            0 
  bDeviceSubClass         0 
  bDeviceProtocol         0 
  bMaxPacketSize0        64
  idVendor           0x1038 SteelSeries ApS
  idProduct          0x1122 
  bcdDevice            2.29
  iManufacturer           1 SteelSeries
  iProduct                2 SteelSeries KLC
  iSerial                 0 
  bNumConfigurations      1

```

The Steel Series lights on the keyboard cannot be configured with [msi-keyboard-git](https://aur.archlinux.org/packages/msi-keyboard-git/) or [msiklm-git](https://aur.archlinux.org/packages/msiklm-git/), because those tools only work with region-based RGB lighting. For this laptop model, the tool [msi-perkeyrgb](https://aur.archlinux.org/packages/msi-perkeyrgb/) provides partial control.

 `$ msi-perkeyrgb -m gs65 --list-preset` 
```
Available presets for GS65:
	- aqua
	- chakra
	- default
	- disco
	- drain
	- freeway
	- plain
	- rainbow-split
	- roulette

```
 `$ msi-perkeyrgb -m gs65 -p aqua` 

If keyboard lights remain off, be sure you've rebooted after installing msi-perkeyrgb to refresh udev and that the brightness is turned to maximum with Fn+PgUp, then try the command again.

#### Button Mapping

##### Airplane Mode Key Combination

The airplane mode key combination (FN + F10) is disabled by default. Adding the following kernel parameters activates airplane mode key combination:

`acpi_osi=! acpi_osi="Windows 2009"`

##### Unmapped Buttons

The following buttons don't have any function or keycodes.

*   FN + F7
*   FN + Home

#### Non-US Keyboards' Backslash/Pipe 102nd Key

**Warning:** As of Feb 2019, systemd 241.7 reverted this change; this workaround is no longer required.

Systemd v240 addressed an issue for US keyboards which broke the mapping for the 102nd key on non-US keyboards. This is the key on the right of the space bar. For a UK keyboard it is the backslash/pipe key and you can correct the scancode to keycode mapping with `# setkeycodes 56 86` . To make this permanent, save the command to an executable shell script with a #!/bin/sh shebang, then create and enable the following systemd unit file:

```
[Unit]
Description=Remap backslash key
[Service]
Type=oneshot
ExecStart=/path/to/shell/script
[Install]
WantedBy=multi-user.target

```

### Touchpad

Single tap and double finger scrolling work. Multi gestures do not work out the box though, they are detected with [libinput-gestures](https://aur.archlinux.org/packages/libinput-gestures/).

## Troubleshooting

### Webcam is not detected

If `/dev/video0` is unavailable and `lsusb` does not list the webcam, make sure that hard webcam switch is activated. The switch is indicated on the F6 key and can be toggled with `FN + F6`.

## Tips and Tricks

### Microphone noise reduction

GS65 has the twin microphone, which is very cool to have for noise reduction and echo cancellation, as well as background sounds suppression via beamforming technique. To get the best of it add this line to `/etc/pulse/default.pa`:

```
load-module module-echo-cancel use_master_format=1 aec_method=webrtc aec_args="beamforming=1 mic_geometry=-0.025,0,0,0.025,0,0"
set-default-source alsa_input.pci-0000_00_1f.3.analog-stereo.echo-cancel

```

Also, it could be useful to add `analog_gain_control=0` to `aec_args` to disable automatic gain control.

## Known Issues

### Lockup Issue (lspci and poweroff hang)

**Symptoms**:

*   lspci hangs
*   poweroff hangs

**Applies to**: Arch boot ISO and systems with nouveau or without nvidia driver installed. See [NVIDIA Optimus#Lockup issue (lspci hangs)](/index.php/NVIDIA_Optimus#Lockup_issue_(lspci_hangs) "NVIDIA Optimus").

**Solutions**:

*   **Arch ISO:** Add `modprobe.blacklist=nouveau` to the kernel parameters ([https://superuser.com/a/1301487](https://superuser.com/a/1301487)).
*   **System without nouveau**: Install [nvidia](https://www.archlinux.org/packages/?name=nvidia).

### Cheese Hangs While Opening Camera

The issue can be fixed by installing [vlc](https://www.archlinux.org/packages/?name=vlc) and running:

```
$ vlc v4l:// :v4l-vdev="/dev/video0"

```

Following this, cheese should work correctly.

### Wifi is hardblocked (airplane mode) after waking up from suspend

Waking from suspend will have wifi in airplane mode. [[1]](https://askubuntu.com/questions/1043547/wifi-hard-blocked-after-suspend-in-ubuntu-on-gs65)

 `# rfkill list` 
```
1: phy0: Wireless LAN
	Soft blocked: no
	Hard blocked: yes

```

Wifi can be reactivated by either using the [airplane mode key combination](#Airplane_Mode_Key_Combination) twice or by hibernating and rebooting.

A way to mitigate this is by setting systemd to hibernate instead of suspending.

 `/etc/systemd/logind.conf` 
```
HandleSuspendKey=hibernate
HandleLidSwitch=hibernate

```

### System freeze

From time to time the graphical interface will freeze and the keyboard will be unresponsive, though audio keeps running. It tends to happen when CPU temperature is high and CPUs are throttling.

There is no known solution for this.

It is not clear what causes this issue:

 `$ journalctl -r --boot -1 ` 
```
Jul 22 20:27:40 almsi kernel: nvidia-modeset: ERROR: GPU:0: Failed to allocate memory for the display color lookup table.

```

### Display outputs don't work after suspend

If the laptop is suspended with another monitor connected, then on wake all display outputs do not recognise when an external display is connected to any port. This persists across reboots. Worryingly it also persists if you reboot into Windows.

One workaround is to boot into Windows, suspend the laptop, then wake it. Connected displays will then be recognised when rebooting into Windows or Arch.

## More Information

### MS-16Q2

#### Microarchitecture, Processor and Platform

 `uname -mpi` 
```
x86_64 unknown unknown

```

#### PCI Devices

 `lspci` 
```
00:00.0 Host bridge: Intel Corporation Device 3ec4 (rev 07)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Device 3e9b
00:12.0 Signal processing controller: Intel Corporation Device a379 (rev 10)
00:14.0 USB controller: Intel Corporation Device a36d (rev 10)
00:14.2 RAM memory: Intel Corporation Device a36f (rev 10)
00:14.3 Network controller: Intel Corporation Device a370 (rev 10)
00:16.0 Communication controller: Intel Corporation Device a360 (rev 10)
00:1b.0 PCI bridge: Intel Corporation Device a340 (rev f0)
00:1d.0 PCI bridge: Intel Corporation Device a330 (rev f0)
00:1d.4 PCI bridge: Intel Corporation Device a334 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Device a30d (rev 10)
00:1f.3 Audio device: Intel Corporation Device a348 (rev 10)
00:1f.4 SMBus: Intel Corporation Device a323 (rev 10)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Device a324 (rev 10)
01:00.0 VGA compatible controller: NVIDIA Corporation GP104M [GeForce GTX 1070 Mobile] (rev a1)
3b:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a808
3c:00.0 Ethernet controller: Qualcomm Atheros Killer E2500 Gigabit Ethernet Controller (rev 10)

```

#### USB Devices

 `lsusb` 
```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 002: ID 1038:1122 SteelSeries ApS 
Bus 001 Device 003: ID 8087:0aaa Intel Corp. 
Bus 001 Device 005: ID 5986:211c Acer, Inc
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

#### Input Devices

 `ls -lah /dev/input/by-id` 
```
total 0
drwxr-xr-x 2 root root  80 Oct 27 11:24 .
drwxr-xr-x 4 root root 480 Oct 27 11:24 ..
lrwxrwxrwx 1 root root   9 Oct 27 09:14 usb-SteelSeries_SteelSeries_KLC-event-if01 -> ../event5
lrwxrwxrwx 1 root root  10 Oct 27 11:24 usb-SunplusIT_Inc_HD_Webcam-event-if00 -> ../event10

```