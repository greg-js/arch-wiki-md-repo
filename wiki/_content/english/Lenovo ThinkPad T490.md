Related articles

*   [Lenovo ThinkPad T490s](/index.php?title=Lenovo_ThinkPad_T490s&action=edit&redlink=1 "Lenovo ThinkPad T490s (page does not exist)")
*   [Lenovo ThinkPad T480](/index.php/Lenovo_ThinkPad_T480 "Lenovo ThinkPad T480")
*   [Lenovo ThinkPad T480s](/index.php/Lenovo_ThinkPad_T480s "Lenovo ThinkPad T480s")
*   [Lenovo ThinkPad T470](/index.php/Lenovo_ThinkPad_T470 "Lenovo ThinkPad T470")

| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes¹ |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | partially |
| [Mobile internet](/index.php/ThinkPad_mobile_Internet "ThinkPad mobile Internet") | not tested |
| Fingerprint Sensor | Yes |
| MicroSD Reader | Yes |
| 

1.  Working, but the iwlwifi driver shows errors in the kernel log. [This is already fixed.](https://bugzilla.kernel.org/show_bug.cgi?id=203593)

 |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 BIOS](#BIOS)
    *   [2.1 BIOS configurations](#BIOS_configurations)
*   [3 FN Keys](#FN_Keys)
*   [4 Touchpad](#Touchpad)
*   [5 Fingerprint Sensor](#Fingerprint_Sensor)
*   [6 Known Issues](#Known_Issues)
    *   [6.1 CPU throttling issue](#CPU_throttling_issue)
    *   [6.2 Speaker noise issue](#Speaker_noise_issue)
    *   [6.3 MicroSD card reader issue](#MicroSD_card_reader_issue)
    *   [6.4 Bluetooth](#Bluetooth)
    *   [6.5 Slow wakeup after suspend](#Slow_wakeup_after_suspend)
*   [7 ACPI](#ACPI)
*   [8 Also See](#Also_See)

## Hardware

Using kernel 5.3.7-arch1-1-ARCH

```
Version: ThinkPad T490
Product Name: 20N2000KGE

```

additional hardware information from `lsusb` and `lspci` can be found bellow:

`lsusb`

```
00:00.0 Host bridge: Intel Corporation Coffee Lake HOST and DRAM Controller (rev 0c) 00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake) (rev 02) 00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c) 00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model 00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 30) 00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 30) 00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 30) 00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 30) 00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #0 (rev 30) 00:16.0 Communication controller: Intel Corporation Cannon Point-LP MEI Controller #1 (rev 30) 00:1c.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #1 (rev f0)
00:1c.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #5 (rev f0)
00:1d.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #9 (rev f0)
00:1d.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #13 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Cannon Point-LP LPC Controller (rev 30)
00:1f.3 Audio device: Intel Corporation Cannon Point-LP High Definition Audio Controller (rev 30)
00:1f.4 SMBus: Intel Corporation Cannon Point-LP SMBus Controller (rev 30)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP SPI Controller (rev 30)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (6) I219-V (rev 30)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
02:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:01.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:02.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
04:00.0 System peripheral: Intel Corporation JHL6240 Thunderbolt 3 NHI (Low Power) [Alpine Ridge LP 2016] (rev 01)
3a:00.0 USB controller: Intel Corporation JHL6240 Thunderbolt 3 USB 3.1 Controller (Low Power) [Alpine Ridge LP 2016] (rev 01)
3d:00.0 Non-Volatile memory controller: Sandisk Corp WD Black 2018/PC SN720 NVMe SSD
00:00.0 Host bridge: Intel Corporation Coffee Lake HOST and DRAM Controller (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake) (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 30)
00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 30)
00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 30)
00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 30)
00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #0 (rev 30)
00:16.0 Communication controller: Intel Corporation Cannon Point-LP MEI Controller #1 (rev 30)
00:1c.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #1 (rev f0)
00:1c.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #5 (rev f0)
00:1d.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #9 (rev f0)
00:1d.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #13 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Cannon Point-LP LPC Controller (rev 30)
00:1f.3 Audio device: Intel Corporation Cannon Point-LP High Definition Audio Controller (rev 30)
00:1f.4 SMBus: Intel Corporation Cannon Point-LP SMBus Controller (rev 30)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP SPI Controller (rev 30)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (6) I219-V (rev 30)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
02:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:01.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:02.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
04:00.0 System peripheral: Intel Corporation JHL6240 Thunderbolt 3 NHI (Low Power) [Alpine Ridge LP 2016] (rev 01)
3a:00.0 USB controller: Intel Corporation JHL6240 Thunderbolt 3 USB 3.1 Controller (Low Power) [Alpine Ridge LP 2016] (rev 01)
3d:00.0 Non-Volatile memory controller: Sandisk Corp WD Black 2018/PC SN720 NVMe SSD

```

`lspci`

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 006: ID 06cb:00bd Synaptics, Inc. 
Bus 001 Device 005: ID 04f2:b681 Chicony Electronics Co., Ltd Integrated Camera
Bus 001 Device 010: ID 2cb7:0210 FIBOCOM L830-EB
Bus 001 Device 013: ID 1050:0407 Yubico.com Yubikey 4 OTP+U2F+CCID
Bus 001 Device 007: ID 8087:0aaa Intel Corp. 
Bus 001 Device 002: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## BIOS

### BIOS configurations

*   `Config -> Thunderbolt BIOS Assist Mode - Set to "Enabled"`. This setting is recommended for Linux.

## FN Keys

Most FN keys should work out of the box, but if it doesn't, bind mentioned keys to below commands:

*   **F1** button: `amixer set Master toggle`.
*   **F2** button: `amixer set Master 5%-`.
*   **F3** button: `amixer set Master 5%+`.
*   **F4** button: `amixer set Capture toggle`.

## Touchpad

Touchpad is problematic. By default, if you hold the thumb over the button area, the pointer will not move. Once the system is installed, the problem disappears when using KDE, while GNOME still exhibits the issue. In GNOME, use the following to fix the problem:

```
xinput set-prop 'SynPS/2 Synaptics TouchPad' 'libinput Click Method Enabled' 1 0

```

Even after doing this, the mouse pointer still jumps around when clicking the button sometimes.

## Fingerprint Sensor

Fingerprint sensor seems to work with some recent firmware and software updates (2019-12-15). Driver development info: [[1]](https://gitlab.freedesktop.org/vincenth/libfprint/tree/synaptics-driver-20190617)[[2]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181).

1\. Use [fwupd](/index.php/Fwupd "Fwupd") to install the latest firmware for "Synaptics Prometheus Fingerprint Reader". The update might have to be done manually (the released firmware is in testing). [[3]](https://fwupd.org/lvfs/devices/com.synaptics.prometheus.firmware)[[4]](https://fwupd.org/lvfs/devices/com.synaptics.prometheus.config)

2\. Latest fprintd and libfprint are required[[5]](https://fprint.freedesktop.org/). [fprintd-libfprint2](https://aur.archlinux.org/packages/fprintd-libfprint2/) and [libfprint-git](https://aur.archlinux.org/packages/libfprint-git/) can be useful here.

3\. [fprint](/index.php/Fprint "Fprint") has more details on how to setup the fingerprint for [PAM](/index.php/PAM "PAM") authentication for example.

## Known Issues

### CPU throttling issue

With the BIOS Version 1.52 (this problem is known to occur on 1.52, it might still happen on other versions too), the CPU tends to throttle down to 400 MHz earlier than it should. In particular, this can be seen when using [Bumblebee](/index.php/Bumblebee "Bumblebee").

After installing BIOS Version 1.54, this problem is fixed.

### Speaker noise issue

The speaker on the Lenovo Thinkpad T490 may have a high static hissing noise, which doesn't change if you lower the volume, but stops if you mute the speaker or use the headphone jack. This problem can't be fixed completely as of now. Updating to the most current BIOS version will make the speaker silent while it's not playing anything without you having to mute it all the time. But as soon as the user is playing sound, the noise will be back, clearly audible in the background.

Check the [Lenovo Support Website](https://support.lenovo.com/) for the newest BIOS Version.

### MicroSD card reader issue

The MicroSD card reader works with the arch kernel 5.3.11-arch1-1\. There have been issues [with previous kernel](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T490&oldid=588258#MicroSD_card_reader_issue) versions.

### Bluetooth

Pairing with a bluetooth speaker and the initial connect works. Connecting to an already paired device currently fails (e.g. after a reboot). Furthermore an error message is shown in the kernel log:

```
[ 3183.282938] debugfs: File 'le_min_key_size' in directory 'hci0' already present!
[ 3183.282950] debugfs: File 'le_max_key_size' in directory 'hci0' already present!

```

An issue for this already exists on the kernel bugtracker [[6]](https://bugzilla.kernel.org/show_bug.cgi?id=204765). It is not clear whether this relates to the connection problem.

### Slow wakeup after suspend

After suspend the laptop takes a few second until it becomes responsive. Disallowing the access to the [WWAN](/index.php/ThinkPad_mobile_Internet "ThinkPad mobile Internet") device in the BIOS solves this issue.

## ACPI

The default `/etc/acpi/handler.sh` script has a check for the device that looks like this:

```
ac_adapter)
        case "$2" in
            AC|ACAD|ADP0)

```

This will not work, since the T490 device is called `ACPI0003` which is not matched by the above check. The instructions in [Acpid](/index.php/Acpid "Acpid") does mention a pattern that does work and it is recommended to use this instead.

## Also See

*   [Lenovo Forums: A throttling fix is being investigated by Lenovo](https://forums.lenovo.com/t5/Other-Linux-Discussions/X1C6-T480s-low-cTDP-and-trip-temperature-in-Linux/m-p/4535310/highlight/true#M13653).