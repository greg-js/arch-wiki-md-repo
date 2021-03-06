| **Device** | **Working** |
| Fan is throttled | No |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| HDMI | Yes |
| VGA | Yes |
| [Audio](/index.php/Audio "Audio") | Yes |
| USB 3.0 | Yes |
| [Ethernet](/index.php/Ethernet "Ethernet") | Yes |
| [WLAN](/index.php/Wireless "Wireless") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Not tested |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Backlight control](/index.php/Backlight "Backlight") | Yes |
| [Function keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") | Yes |
| [Hardware switches](/index.php/Extra_keyboard_keys "Extra keyboard keys") | Yes |
| Card reader | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |

## Contents

*   [1 Hardware support](#Hardware_support)
    *   [1.1 Fan throttling](#Fan_throttling)
    *   [1.2 Intel CPU microcode](#Intel_CPU_microcode)
    *   [1.3 Synaptics Touchpad](#Synaptics_Touchpad)
    *   [1.4 WLAN BIOS whitelist workaround](#WLAN_BIOS_whitelist_workaround)
*   [2 Documentation](#Documentation)

## Hardware support

The hardware support is indicated in the table on the right.

### Fan throttling

The fan can be controlled (throttled) in software, otherwise it never shuts off, even if the BIOS option "Fan always on while on AC power" is disabled. There are two programs supporting the 4330s:

*   [NoteBook FanControl](https://github.com/hirschmann/nbfc)
*   [probook_ec.pl script](http://ubuntuforums.org/showthread.php?t=2008756&p=12422983#post12422983) daemonized [in Python](https://github.com/deanrock/probook-fan-control) and [in Ruby](https://github.com/opinsys/puavo-hw-tools/tree/master/bin)

### Intel CPU microcode

See [Microcode#Installation](/index.php/Microcode#Installation "Microcode").

Related articles

*   [HP_ProBook_4530s](/index.php/HP_ProBook_4530s "HP ProBook 4530s")
*   [HP_ProBook_4730s](/index.php/HP_ProBook_4730s "HP ProBook 4730s")
*   [Intel_graphics](/index.php/Intel_graphics "Intel graphics")
*   [Power_management](/index.php/Power_management "Power management")
*   [GRUB](/index.php/GRUB "GRUB")
*   [GRUB/Tips and tricks](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks")

### Synaptics Touchpad

The `xf86-input-synaptics` driver is needed (see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")) for the touchpad to work, but the pointstick works out of the box.

### WLAN BIOS whitelist workaround

HP BIOS allows only certain WLAN cards (whitelisting) to be used. This can be worked around by adding the following as the first GRUB command in every OS entry:

```
write_dword 0xFED1F418 0x1F501FEB

```

You can read more on engineering this hack [here](http://milksnot.com/content/project-dirty-laundry-how-defeat-whitelisting-without-bios-modding).

## Documentation

*   [Linux User Guide](https://h20565.www2.hp.com/hpsc/doc/public/display?sp4ts.oid=5045444&docId=emr_na-c02879204&docLocale=en_US)
*   [Specifications](http://www8.hp.com/h20195/v2/getpdf.aspx/c04288440.pdf)
*   [Maintenance and Service Guide](http://h10032.www1.hp.com/ctg/Manual/c03054507.pdf)
*   [EoL Disassembly Guide](http://www.hp.com/hpinfo/globalcitizenship/environment/productdata/Countries/_MultiCountry/disassembly_notebo_201132222595.pdf)