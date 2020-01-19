Related articles

*   [Lenovo ThinkPad T490](/index.php/Lenovo_ThinkPad_T490 "Lenovo ThinkPad T490")
*   [Lenovo ThinkPad T480](/index.php/Lenovo_ThinkPad_T480 "Lenovo ThinkPad T480")
*   [Lenovo ThinkPad T480s](/index.php/Lenovo_ThinkPad_T480s "Lenovo ThinkPad T480s")
*   [Lenovo ThinkPad T470](/index.php/Lenovo_ThinkPad_T470 "Lenovo ThinkPad T470")

| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| [Mobile internet](/index.php/ThinkPad_mobile_Internet "ThinkPad mobile Internet") | not tested |
| Fingerprint Sensor | Yes¹ |
| MicroSD Reader | not tested |
| 

1.  Requires [libfprint-git](https://aur.archlinux.org/packages/libfprint-git/), [fprintd-libfprint2](https://aur.archlinux.org/packages/fprintd-libfprint2/), and a firmware update through [fwupd](/index.php/Fwupd "Fwupd"). See [[1]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181).

 |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 BIOS](#BIOS)
*   [3 FN Keys](#FN_Keys)
*   [4 Touchpad](#Touchpad)
*   [5 Fingerprint Sensor](#Fingerprint_Sensor)
*   [6 Known Issues](#Known_Issues)
*   [7 ACPI](#ACPI)

## Hardware

```
 Manufacturer: LENOVO
 Product Name: 20NX001RUS
 Version: ThinkPad T490s
 SKU Number: LENOVO_MT_20NX_BU_Think_FM_ThinkPad T490s
 Family: ThinkPad T490s

```

Additional hardware information from `lsusb` and `lspci` can be found bellow:

`lsusb`

```
00:00.0 Host bridge: Intel Corporation Coffee Lake HOST and DRAM Controller (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake) (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 30)
00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 30)
00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 30)
00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 30)
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
01:00.0 SD Host controller: Genesys Logic, Inc GL9750 SD Host Controller (rev 01)
02:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:01.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:02.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
04:00.0 System peripheral: Intel Corporation JHL6240 Thunderbolt 3 NHI (Low Power) [Alpine Ridge LP 2016] (rev 01)
3a:00.0 USB controller: Intel Corporation JHL6240 Thunderbolt 3 USB 3.1 Controller (Low Power) [Alpine Ridge LP 2016] (rev 01)
3d:00.0 Non-Volatile memory controller: Sandisk Corp Device 5006

```

`lspci`

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 06cb:00bd Synaptics, Inc. 
Bus 001 Device 002: ID 04ca:7070 Lite-On Technology Corp. Integrated Camera
Bus 001 Device 004: ID 8087:0aaa Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## BIOS

## FN Keys

Most FN keys should work out of the box, but if it doesn't, bind mentioned keys to below commands:

*   **F1** button: `amixer set Master toggle`.
*   **F2** button: `amixer set Master 5%-`.
*   **F3** button: `amixer set Master 5%+`.
*   **F4** button: `amixer set Capture toggle`.

## Touchpad

Touchpad works. But some users have reported issues with the related [Lenovo ThinkPad T490#Touchpad](/index.php/Lenovo_ThinkPad_T490#Touchpad "Lenovo ThinkPad T490").

## Fingerprint Sensor

The fingerprint sensor works with some recent firmware and software updates (2019-12-15). Driver development info: [[2]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181).

1.  Use [fwupd](/index.php/Fwupd "Fwupd") to install the latest firmware for "Synaptics Prometheus Fingerprint Reader". The update might have to be done manually as the released firmware is in testing; or you could [enable the testing remote in fwupd](https://github.com/fwupd/fwupd/wiki/LVFS-Testing-remote) to allow automated upgrade. The relevant firmwares are [Prometheus Fingerprint Reader](https://fwupd.org/lvfs/devices/com.synaptics.prometheus.firmware) and [Prometheus Fingerprint Reader Configuration](https://fwupd.org/lvfs/devices/com.synaptics.prometheus.config).
2.  Latest [fprintd and libfprint](https://fprint.freedesktop.org/) are required. [fprintd-libfprint2](https://aur.archlinux.org/packages/fprintd-libfprint2/) and [libfprint-git](https://aur.archlinux.org/packages/libfprint-git/) can be useful here.
3.  [fprint](/index.php/Fprint "Fprint") has more details on how to setup the fingerprint for [PAM](/index.php/PAM "PAM") authentication for example.

## Known Issues

## ACPI

The default `/etc/acpi/handler.sh` script has a check for the device that looks like this:

```
ac_adapter)
        case "$2" in
            AC|ACAD|ADP0)

```

This will not work, since the T490s device is called `ACPI0003:00` which is not matched by the above check. The instructions in [Acpid](/index.php/Acpid "Acpid") does mention a pattern that does work and it is recommended to use this instead.