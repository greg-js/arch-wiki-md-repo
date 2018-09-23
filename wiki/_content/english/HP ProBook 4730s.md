Related articles

*   [HP_ProBook_4330s](/index.php/HP_ProBook_4330s "HP ProBook 4330s")
*   [HP_ProBook_4530s](/index.php/HP_ProBook_4530s "HP ProBook 4530s")
*   [Intel_graphics](/index.php/Intel_graphics "Intel graphics")
*   [Power_management](/index.php/Power_management "Power management")
*   [GRUB](/index.php/GRUB "GRUB")
*   [GRUB/Tips and tricks](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks")

## Contents

*   [1 Hardware support](#Hardware_support)
    *   [1.1 Fan throttling](#Fan_throttling)
    *   [1.2 Intel CPU microcode](#Intel_CPU_microcode)
    *   [1.3 Synaptics Touchpad](#Synaptics_Touchpad)
    *   [1.4 WLAN BIOS whitelist workaround](#WLAN_BIOS_whitelist_workaround)

## Hardware support

### Fan throttling

The fan can be controlled (throttled) in software, otherwise it never shuts off, even if the BIOS option "Fan always on while on AC power" is disabled. There are two programs supporting the 4730s:

*   [NoteBook FanControl](https://github.com/hirschmann/nbfc)
*   [probook_ec.pl script](http://ubuntuforums.org/showthread.php?t=2008756&p=12422983#post12422983) daemonized [in Python](https://github.com/deanrock/probook-fan-control) and [in Ruby](https://github.com/opinsys/puavo-hw-tools/tree/master/bin)

### Intel CPU microcode

See [Microcode#Installation](/index.php/Microcode#Installation "Microcode").

### Synaptics Touchpad

The `xf86-input-synaptics` driver is needed (see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")) for the touchpad to work, but the pointstick works out of the box.

### WLAN BIOS whitelist workaround

HP BIOS allows only certain WLAN cards (whitelisting) to be used. This can be worked around by adding the following as the first GRUB command in every OS entry:

```
write_dword 0xFED1F418 0x1F501FEB

```

You can read more on engineering this hack [here](http://milksnot.com/content/project-dirty-laundry-how-defeat-whitelisting-without-bios-modding).