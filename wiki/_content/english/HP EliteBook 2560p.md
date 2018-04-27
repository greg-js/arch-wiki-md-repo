The HP 2560p is a subnotebook with an Intel i5 or Intel i7 processor inside. Due to similarity, see also [HP EliteBook 2570p](/index.php/HP_EliteBook_2570p "HP EliteBook 2570p").

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| Displayport | Yes |
| [Network](/index.php/Network "Network") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| [Audio](/index.php/Audio "Audio") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Fingerprint reader](/index.php/Fprint "Fprint") | No |
| Pointstick | Yes |
| [eSATA Port](/index.php/Udev#Detect_new_eSATA_drives "Udev") | Not tested |
| Backlight | Yes |
| Function keys | Yes |
| Cardreader | Yes |
| VGA | Yes |

## Contents

*   [1 Hardware Support](#Hardware_Support)
    *   [1.1 Touchpad](#Touchpad)
    *   [1.2 Fingerprint Reader](#Fingerprint_Reader)
    *   [1.3 Cardreader](#Cardreader)

## Hardware Support

### Touchpad

Without xf86-input-synaptics (see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")) the touchpad doesn't work, but the pointstick with the buttons are ready to use.

### Fingerprint Reader

```
# Validity Sensors, Inc. VFS471 Fingerprint Reader

```

The model of fingerprint sensor in this laptop does not have available Linux drivers, open source or otherwise. Therefore the fingerprint sensor will NOT work with Arch Linux.

### Cardreader

If the cardreader does not detect the inserted card, try running the following command:

```
echo 1 | sudo tee /sys/bus/pci/rescan

```