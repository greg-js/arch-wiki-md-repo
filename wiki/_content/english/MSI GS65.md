| **Device** | **Status** | **Modules** |
| Intel GPU | Working | modesetting |
| Nvidia GPU | Working | nvidia (not nouveau) |
| Ethernet | Working | alx |
| Wireless | Working with patch | iwlwifi |
| Audio | Working | snd_hda_intel |
| Webcam | Working | uvcvideo |
| Bluetooth | Working | btusb |
| USB | Working |
| Power management | Partially Working |
| Keyboard | Partially Working |
| Touchpad | Partially Working | libinput |

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 BIOS](#BIOS)
        *   [1.1.1 2.20.1271](#2.20.1271)
    *   [1.2 Networking](#Networking)
        *   [1.2.1 Wireless](#Wireless)
    *   [1.3 Video](#Video)
        *   [1.3.1 Backlight](#Backlight)
        *   [1.3.2 Drivers](#Drivers)
        *   [1.3.3 Multihead](#Multihead)
    *   [1.4 Webcam](#Webcam)
    *   [1.5 Power Management](#Power_Management)
    *   [1.6 Keyboard](#Keyboard)
        *   [1.6.1 Lights](#Lights)
        *   [1.6.2 Button Mapping](#Button_Mapping)
            *   [1.6.2.1 Unmapped Buttons](#Unmapped_Buttons)
    *   [1.7 Touchpad](#Touchpad)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Webcam is not detected](#Webcam_is_not_detected)
*   [3 Tips and Tricks](#Tips_and_Tricks)
*   [4 Known Issues](#Known_Issues)
    *   [4.1 Lockup Issue (lspci and poweroff hang)](#Lockup_Issue_.28lspci_and_poweroff_hang.29)
    *   [4.2 Cheese Hangs While Opening Camera](#Cheese_Hangs_While_Opening_Camera)
    *   [4.3 Wifi is hardblocked (airplane mode) after waking up from suspend](#Wifi_is_hardblocked_.28airplane_mode.29_after_waking_up_from_suspend)
    *   [4.4 System freeze](#System_freeze)
*   [5 More Information](#More_Information)
    *   [5.1 MS-16Q2](#MS-16Q2)
        *   [5.1.1 Microarchitecture, Processor and Platform](#Microarchitecture.2C_Processor_and_Platform)
        *   [5.1.2 PCI Devices](#PCI_Devices)
        *   [5.1.3 USB Devices](#USB_Devices)

## Configuration

### BIOS

#### 2.20.1271

At bootup, the BIOS settings page is entered via the delete key, the quick boot select window can be activated via the F11 key, PXE scanning can be activated via the F12 key

In the BIOS setings,he model name can be seen in the Main tab, [Secure Boot](/index.php/Secure_Boot "Secure Boot") can be disabled from the Security tab and boot mode can optionally be switched from [UEFI](/index.php/UEFI "UEFI") to legacy.

There is no option to disable the discrete intel GPU.

### Networking

#### Wireless

Support for the Killer 1550 is not there yet but is coming. [[1]](https://www.spinics.net/lists/linux-wireless/msg172978.html)[[2]](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git/tree/drivers/net/wireless/intel/iwlwifi/pcie/drv.c?id=998ce0330c94eca4b13b8f062b3f0ca9ef9ad6d8#n622)[[3]](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git/commit/?id=a3ef483ec5002b7af5a2ad04cb7a77366cd23b9f)

It should be possible to add support by patching the kernel [[4]](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/drivers/net/wireless/intel/iwlwifi/pcie/drv.c#n799) to add `{IWL_PCI_DEVICE(0xA370, 0x1552, iwl9560_2ac_cfg_soc)},`

Using the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") it is possible to rebuild the kernel using this patch which add the mapping for the wifi on kernel 4.17.11

 `0001-Add-patch-for-MSI-GS65-wifi.patch` 
```
From 740ff066915a8ef636fc7f14fe9c7023bc61e488 Mon Sep 17 00:00:00 2001
From: Sandy Carter <bwrsandman@gmail.com>
Date: Tue, 19 Jun 2018 09:38:08 -0700
Subject: [PATCH] Add patch for MSI GS65 wifi

---
 repos/core-x86_64/0005-Add-wifi-support.patch | 10 ++++++
 repos/core-x86_64/PKGBUILD                    | 34 ++++++++++++++++++-
 2 files changed, 43 insertions(+), 1 deletion(-)
 create mode 100644 repos/core-x86_64/0005-Add-wifi-support.patch

diff --git a/repos/core-x86_64/0005-Add-wifi-support.patch b/repos/core-x86_64/0005-Add-wifi-support.patch
new file mode 100644
index 0000000..b7e62ef
--- /dev/null
+++ b/repos/core-x86_64/0005-Add-wifi-support.patch
@@ -0,0 +1,10 @@
+--- a/drivers/net/wireless/intel/iwlwifi/pcie/drv.c
++++ b/drivers/net/wireless/intel/iwlwifi/pcie/drv.c
+@@ -797,6 +797,7 @@
+ 	{IWL_PCI_DEVICE(0xA370, 0x1010, iwl9260_2ac_cfg)},
+ 	{IWL_PCI_DEVICE(0xA370, 0x1030, iwl9560_2ac_cfg_soc)},
+ 	{IWL_PCI_DEVICE(0xA370, 0x1210, iwl9260_2ac_cfg)},
++	{IWL_PCI_DEVICE(0xA370, 0x1552, iwl9560_2ac_cfg_soc)},
+ 	{IWL_PCI_DEVICE(0xA370, 0x2030, iwl9560_2ac_cfg_soc)},
+ 	{IWL_PCI_DEVICE(0xA370, 0x2034, iwl9560_2ac_cfg_soc)},
+ 	{IWL_PCI_DEVICE(0xA370, 0x4030, iwl9560_2ac_cfg_soc)},
diff --git a/repos/core-x86_64/PKGBUILD b/repos/core-x86_64/PKGBUILD
index c571d68..8f03362 100644
--- a/repos/core-x86_64/PKGBUILD
+++ b/repos/core-x86_64/PKGBUILD
@@ -19,6 +19,7 @@ source=(
   60-linux.hook  # pacman hook for depmod
   90-linux.hook  # pacman hook for initramfs regeneration
   linux.preset   # standard config files for mkinitcpio ramdisk
+  0005-Add-wifi-support.patch
 )
 validpgpkeys=(
   'ABAF11C65A2970B130ABE3C479BE3E4300411886'  # Linus Torvalds
@@ -29,7 +30,8 @@ sha256sums=('SKIP'
             'aa7b6756f193f3b3a3fc4947e7a77b09e249df2e345e6495292055d757ba8be6'
             'ae2e95db94ef7176207c690224169594d49445e04249d2499e9d2fbc117a0b21'
             '75f99f5239e03238f88d1a834c50043ec32b1dc568f2cc291b07d04718483919'
-            'ad6344badc91ad0630caacde83f7f9b97276f80d26a20619a87952be65492c65')
+            'ad6344badc91ad0630caacde83f7f9b97276f80d26a20619a87952be65492c65'
+            '54b32090a6ac96e95da8cfd54634310adbff6fbebb8dbbef176d1d3facf4d1a5')

 _kernelname=${pkgbase#linux}
 : ${_kernelname:=-arch}
@@ -39,6 +41,36 @@ prepare() {
   scripts/setlocalversion --save-scmversion
   cp ../config .config
   make olddefconfig
+
+  # GS65 Wifi support
+  patch -Np1 -i ../0005-Add-wifi-support.patch
+
+  cat ../config - >.config <<END
+CONFIG_LOCALVERSION="${_kernelname}"
+CONFIG_LOCALVERSION_AUTO=n
+END
+
+  # set extraversion to pkgrel and empty localversion
+  sed -e "/^EXTRAVERSION =/s/=.*/= -${pkgrel}/" \
+      -e "/^EXTRAVERSION =/aLOCALVERSION =" \
+      -i Makefile
+
+  # don't run depmod on 'make install'. We'll do this ourselves in packaging
+  sed -i '2iexit 0' scripts/depmod.sh
+
+  # get kernel version
+  make prepare
+
+  # load configuration
+  # Configure the kernel. Replace the line below with one of your choice.
+  #make menuconfig # CLI menu for configuration
+  #make nconfig # new CLI menu for configuration
+  #make xconfig # X-based configuration
+  #make oldconfig # using old config from previous kernel version
+  # ... or manually edit .config
+
+  # rewrite configuration
+  yes "" | make config >/dev/null
 }

 build() {
-- 
2.18.0

```

Checkout the package and apply the above patch

```
$ asp checkout linux
$ cd linux/repos/core-x86_64
$ git am 0001-Add-patch-for-MSI-GS65-wifi.patch
$ makepkg -i

```

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

The Steel Series lights on the keyboard cannot be configured with [msi-keyboard-git](https://aur.archlinux.org/packages/msi-keyboard-git/) probably due to the udev rules not matching the usb vendor_id and product_id.

#### Button Mapping

On the US model, the `\|` key (to the right of space) has scancode `0x56` is incorrectly mapped to `<>`.

The mapping can be fixed temporarily by [adding a scancode mapping](/index.php/Map_scancodes_to_keycodes#Using_udev "Map scancodes to keycodes"):

 `/etc/udev/hwdb.d/85-msi-keyboard.hwdb` 
```
# MSI GS65 Stealth Thin has a physical backslash key next to the space bar
evdev:atkbd:dmi:bvn*:bvr*:bd*:svnMicro-Star*:pnGS65StealthThin*:pvr*
 KEYBOARD_KEY_56=backslash

```

And reloading the keymapping database:

```
# systemd-hwdb update
# udevadm trigger

```

The commit [[5]](https://github.com/systemd/systemd/commit/e05c8b44622afe4256f3bb361cfb2c7db32fff8e) to fix this in systemd has been merged and should be available in the next release of systemd (240).

##### Unmapped Buttons

The following buttons don't have any function or keycodes.

*   FN + F7
*   FN + F10 (airplane mode)
*   FN + Home

### Touchpad

Single tap and double finger scrolling work. Multi gestures do not work out the box though, they are detected with [libinput-gestures](https://aur.archlinux.org/packages/libinput-gestures/).

## Troubleshooting

### Webcam is not detected

If `/dev/video0` is unavailable and `lsusb` does not list the webcam, make sure that hard webcam switch is activated. The switch is indicated on the F6 key and can be toggled with `FN + F6`.

## Tips and Tricks

## Known Issues

### Lockup Issue (lspci and poweroff hang)

**Symptoms**:

*   lspci hangs
*   poweroff hangs

**Applies to**: Arch boot ISO and systems with nouveau or without nvidia driver installed. See [NVIDIA Optimus#Lockup issue (lspci hangs)](/index.php/NVIDIA_Optimus#Lockup_issue_.28lspci_hangs.29 "NVIDIA Optimus").

**Solutions**:

*   **Arch ISO:** Add `modprobe.blacklist=nouveau` to the kernel parameters ([https://superuser.com/a/1301487](https://superuser.com/a/1301487)).
*   **System without nouveau**: Install [nvidia](https://www.archlinux.org/packages/?name=nvidia).

### Cheese Hangs While Opening Camera

The issue can be fixed by installing [vlc](https://www.archlinux.org/packages/?name=vlc) and running:

```
$ vlc v4l:// :v4l-vdev="/dev/video0"

```

Following this, cheese should work correctly.

### Wifi is hardblocked (airplane mode) after waking up from suspend

Waking from suspend will have wifi in airplane mode. [[6]](https://askubuntu.com/questions/1043547/wifi-hard-blocked-after-suspend-in-ubuntu-on-gs65)

 `# rfkill list` 
```
1: phy0: Wireless LAN
	Soft blocked: no
	Hard blocked: yes

```

Wifi can be reactivated in a few ways:

```
   # rfkill unblock all

```

```
   # modprobe iwlwifi

```

Or by hibernating and rebooting.

### System freeze

From time to time the graphical interface will freeze and the keyboard will be unresponsive, though audio keeps running. It tends to happen when CPU temperature is high and CPUs are throttling.

There is no known solution for this.

It is not clear what causes this issue:

 `$ journalctl -r --boot -1 ` 
```
Jul 22 20:27:40 almsi kernel: nvidia-modeset: ERROR: GPU:0: Failed to allocate memory for the display color lookup table.

```

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
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```