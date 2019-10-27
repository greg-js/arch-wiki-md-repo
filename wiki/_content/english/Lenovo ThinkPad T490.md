| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes¹ |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | not tested |
| [Mobile internet](/index.php/ThinkPad_mobile_Internet "ThinkPad mobile Internet") | not tested |
| Fingerprint Sensor | No² |
| MicroSD Reader | No³ |
| 

1.  Working, but the iwlwifi driver shows errors in the kernel log. [This is already fixed.](https://bugzilla.kernel.org/show_bug.cgi?id=203593)
2.  No working Linux driver so far for Synaptics 06cb:009a. See [here](https://github.com/nmikhailov/Validity90) and [here](https://forums.lenovo.com/t5/Other-Linux-Discussions/Linux-on-T495/m-p/4474320/highlight/true#M13440).
3.  The MicroSD Reader will be supported in kernel 5.4 and works under the current AUR linux-mainline kernel

 |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 FN Keys](#FN_Keys)
*   [3 Touchpad](#Touchpad)
*   [4 Known Issues](#Known_Issues)
    *   [4.1 CPU throttling issue](#CPU_throttling_issue)
    *   [4.2 Speaker noise issue](#Speaker_noise_issue)
    *   [4.3 MicroSD card reader issue](#MicroSD_card_reader_issue)
*   [5 ACPI](#ACPI)
*   [6 Also See](#Also_See)

## Hardware

Using kernel 5.3.7-arch1-1-ARCH

```
Version: ThinkPad T490
Product Name: 20N2000KGE

```

`lspci` returns something like:

```
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

`lsusb` returns something like:

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

## Known Issues

### CPU throttling issue

With the BIOS Version 1.52 (this problem is known to occur on 1.52, it might still happen on other versions too), the CPU tends to throttle down to 400 MHz earlier than it should. In particular, this can be seen when using [Bumblebee](/index.php/Bumblebee "Bumblebee").

After installing BIOS Version 1.54, this problem is fixed.

### Speaker noise issue

The speaker on the Lenovo Thinkpad T490 may have a high static hissing noise, which doesn't change if you lower the volume, but stops if you mute the speaker or use the headphone jack. This problem can't be fixed completely as of now. Updating to the most current BIOS version will make the speaker silent while it's not playing anything without you having to mute it all the time. But as soon as the user is playing sound, the noise will be back, clearly audible in the background.

Check the [Lenovo Support Website](https://support.lenovo.com/) for the newest BIOS Version.

### MicroSD card reader issue

The microSD card reader does not work with the default kernel. Upon inserting a card, the Linux kernel version 5.3.4 continuously produces the following output and the card does not mount.

```
   mmc0: 1.8V regulator output did not became stable
   mmc0: Skipping voltage switch
   mmc0: Problem switching card into high-speed mode!

```

As of October 2019, the mainline kernel build includes a patchset that fixes this issue. Users can either wit for 5.4 to be released in late November or [install the mainline kernel package from AUR](https://aur.archlinux.org/packages/linux-mainline/) (bootloader will also have to be configured to use this kernel by default).

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