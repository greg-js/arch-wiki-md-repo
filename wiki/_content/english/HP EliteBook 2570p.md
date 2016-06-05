| **Device** | **Working** |
| Fan is throttled | Yes |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| DisplayPort | Not tested |
| VGA | Yes |
| [Audio](/index.php/Audio "Audio") | Yes |
| USB 3.0 | Yes |
| [Ethernet](/index.php/Network "Network") | Yes |
| [WLAN](/index.php/Wireless "Wireless") | Yes |
| [WWAN](#WWAN) | Yes |
| [GPS](/index.php/GPS "GPS") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Buggy device |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| Pointstick | Yes |
| [Backlight control](/index.php/Backlight "Backlight") | Yes |
| [Function keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") | Yes |
| [Hardware switches](/index.php/Extra_keyboard_keys "Extra keyboard keys") | Yes |
| Card reader | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Fingerprint reader](/index.php/Fprint "Fprint") | Not tested |

HP EliteBook 2570p is a powerful and customizable 12.5-inch notebook with a socketted Ivy Bridge processor and interesting [specifications](https://www.fajnykomputer.pl/pl/p/file/b7a0ac330691b6f4eec20261b93dfaab/quick_spec_hp_elitebook_2570p.pdf) (and even a [SuSE certificate](https://www.suse.com/yes/138109.htm)). Arch Linux installs and runs on it without major problems. There are a few hacks needed to enable all of the [power management](/index.php/Power_management "Power management") functions and gain the maximum battery life.

## Contents

*   [1 Hardware support](#Hardware_support)
    *   [1.1 Intel CPU microcode](#Intel_CPU_microcode)
    *   [1.2 Synaptics Touchpad](#Synaptics_Touchpad)
    *   [1.3 WWAN (and GPS) adapter](#WWAN_.28and_GPS.29_adapter)
    *   [1.4 Bluetooth adapter](#Bluetooth_adapter)
*   [2 Power management](#Power_management)
    *   [2.1 Intel graphics](#Intel_graphics)
    *   [2.2 ASPM](#ASPM)
    *   [2.3 Relevant links](#Relevant_links)
*   [3 Documentation](#Documentation)
    *   [3.1 Schematics](#Schematics)
*   [4 See also](#See_also)

## Hardware support

The hardware support is indicated in the table on the right.

### Intel CPU microcode

See [Microcode#Enabling Intel microcode updates](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

### Synaptics Touchpad

The `xf86-input-synaptics` driver is needed (see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")) for the touchpad to work, but the pointstick works out of the box.

### WWAN (and GPS) adapter

[modemmanager](https://www.archlinux.org/packages/?name=modemmanager) is needed besides NetworkManager for the WWAN card (`ID 03f0:371d Hewlett-Packard`) to function properly. For GPS test, see [GPS#ModemManager](/index.php/GPS#ModemManager "GPS").

### Bluetooth adapter

The integrated [Bluetooth](/index.php/Bluetooth "Bluetooth") device [BCM20702A0](http://www.broadcom.com/products/Bluetooth/Bluetooth-RF-Silicon-and-Software-Solutions/BCM20702) (`ID 0a5c:21e1 Broadcom Corp. HP Portable SoftSailing`) seems a bit buggy as a few random disconnects were observed in combination with some BT4.0 devices. One possible way to circumvent this HP engineers' bad choice is to replace the integrated Wi-Fi card with Wi-Fi+BT combo one sucj as Intel® Centrino® Advanced-N 6235 or similar (later 2570p BIOS-es should have WLAN whitelisting [removed](https://www.techinferno.com/index.php?/forums/topic/1982-125-hp-elitebook-2570p-owners-lounge/&page=41#comment-109982)) and then [connecting](https://www.techinferno.com/index.php?/forums/topic/1982-125-hp-elitebook-2570p-owners-lounge/&page=47#comment-132577) the Bluetooth interface of the card to the pins used by the docking connector. This is necessary as this laptop has no USB pins connected on the WLAN miniPCIe interface and the user also benefits from the Intel® Centrino® Advanced-N 6235's improved power efficiency over 6205.

## Power management

Hardware-specific power management functions are described below, for more generic ones [power management](/index.php/Power_management "Power management") should also be reviewed thoroughly. For a nice all in one power management package consider [TLP](/index.php/TLP "TLP").

### Intel graphics

The following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") can be enabled to provide additional power management for [Intel graphics](/index.php/Intel_graphics "Intel graphics"). However, some of them are experimental on Ivy Bridge hardware and can lead to problems.

```
GRUB_CMDLINE_LINUX="i915.i915_enable_rc6=7 i915.i915_enable_fbc=1 i915.lvds_downclock=1 i915.semaphores=1 drm.vblankoffdelay=1"

```

### ASPM

This laptop has [ASPM](/index.php/Power_management#Active_State_Power_Management "Power management") disabled by default and even later versions of BIOS do not provide any options for enabling it. As this feature improves battery life for around 25%, it is a very useful one to have. It is possible to forcibly enable ASPM by using GRUB to write the proper bits to the configuration registers before the kernel is executed. The easiest way is to add the following to the `/etc/grub.d/01_enable-aspm`:

```
 #! /bin/sh
 set -e

 prefix="/usr"
 exec_prefix="/usr"
 datarootdir="/usr/share"

 . "${datarootdir}/grub/grub-mkconfig_lib"

 export TEXTDOMAIN=grub
 export TEXTDOMAINDIR="${datarootdir}/locale"

 # HP EliteBook 2570p ASPM hardware enable
 #cho "write_byte 0xB9CF506D 0x03" # Enable in ACPI FADT/FACP (BIOS F.40-)
 echo "write_byte 0xB9FFC06D 0x03" # Enable in ACPI FADT/FACP (BIOS F.40+)
 echo "write_byte 0xB9FFC019 0x10" # Correct checksum

```

If ASPM has been successfully enabled, there will be no complaints in `dmesg | grep ASPM`. Forcing ASPM in software with `pcie_aspm=force` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") is not needed, however ASPM still needs to be enabled for every PCI device after the kernel is booted. This can be done by a [startup script](/index.php/Autostarting "Autostarting") such as `/etc/rc.local` and its contents should be:

```
 # HP EliteBook 2570p ASPM hardware enable
 setpci -s "00:1c.0" "50.b=0x43" # PCI Express Root Port 1
 setpci -s "00:1c.1" "50.b=0x43" # ExpressCard (alternatively 50.b=0x03)
 setpci -s "00:1c.2" "50.b=0x43" # PCI Express Root Port 3
 #etpci -s "00:1c.3" "50.b=0x43" # PCI Express Root Port 4
 setpci -s "02:00.0" "90.b=0x43" # SD/MMC Host Controller
 setpci -s "02:00.2" "90.b=0x43" # SD Host Controller
 #etpci -s "03:00.0" "f0.b=0x43" # Network controller

```

Some of the lines are commented out because ASPM does not work properly with some WLAN cards (Intel® Centrino® Advanced-N 6235 for example), causing the kernel to not detect the card after some time (a reboot is needed). The final check if everything is set up correctly can be performed after a reboot by running `lspci -vv | grep ASPM.*abled\;` (as root).

### Relevant links

*   Possible PM tweaks: [1](https://www.techinferno.com/index.php?/forums/topic/1982-125-hp-elitebook-2570p-owners-lounge/#comment-35271) and [2](https://www.techinferno.com/index.php?/forums/topic/1982-125-hp-elitebook-2570p-owners-lounge/&page=41#comment-111566)
*   Enabling ASPM with GRUB: [1](https://www.techinferno.com/index.php?/forums/topic/1982-125-hp-elitebook-2570p-owners-lounge/&page=42#comment-117096) and [2](http://forum.notebookreview.com/threads/hp-elitebook-2560p-owners-lounge.586353/page-15#post-8375856)

## Documentation

*   [Linux User Guide](http://h20565.www2.hp.com/portal/site/hpsc/template.PAGE/action.process/public/psi/manualsDisplay/?sp4ts.oid=5259393&javax.portlet.action=true&spf_p.tpst=psiContentDisplay&javax.portlet.begCacheTok=com.vignette.cachetoken&spf_p.prp_psiContentDisplay=wsrp-interactionState%3DdocId%253Demr_na-c03500525%257CdocLocale%253Den_US&javax.portlet.endCacheTok=com.vignette.cachetoken)
*   [Specifications](https://www.fajnykomputer.pl/pl/p/file/b7a0ac330691b6f4eec20261b93dfaab/quick_spec_hp_elitebook_2570p.pdf)
*   [Maintenance and Service Guide](http://h20628.www2.hp.com/km-ext/kmcsdirect/emr_na-c03559419-1.pdf)
*   [EoL Disassembly Guide](http://www.hp.com/hpinfo/globalcitizenship/environment/productdata/Countries/_MultiCountry/disassembly_notebo_2012627193535.pdf)

### Schematics

There is [HP EliteBook 2560p](/index.php/HP_EliteBook_2560p "HP EliteBook 2560p") schematic [available](http://notebookschematic.org/data/NOTEBOOK/attachments/SC/products_files/HP%20EliteBook%202560%20Inventec%20STYX%20MV%20Schematic%20Diagram%20AX2.pdf) and it is also useful for 2570p as the models differ more or less only in addition of the Ivy Bridge CPU and USB 3.0 in 2570p.

## See also

*   **HP Battery Check** tool in [HP Support Assistant](http://h20565.www2.hp.com/hpsc/swd/public/detail?sp4ts.oid=5284308&swItemId=ob_156672_1&swEnvOid=4059) package is a Windows-only tool to display additional battery info such as per-cell readings and recharge cycle count
*   [HP EliteBook 2570p users' forum](https://www.techinferno.com/index.php?/forums/topic/1982-125-hp-elitebook-2570p-owners-lounge/)
*   [NotebookReview's review](http://www.notebookreview.com/notebookreview/hp-elitebook-2570p-review/)