The HP 2560p is a subnotebook with an Intel i5 or Intel i7 processor inside.

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| Displayport | Yes |
| [Network](/index.php/Network "Network") | Yes |
| [Wireless](/index.php/Wireless_network_configuration "Wireless network configuration") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| [Audio](/index.php/Audio "Audio") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Not tested |
| [Fingerprit reader](/index.php/Fprint "Fprint") | Not tested |
| Pointstick | Yes |
| [eSATA Port](/index.php/Udev#Detect_new_eSATA_drives "Udev") | Not tested |
| Backlight | Yes |
| Function Keys | Yes |
| Cardreader | Limited |
| VGA | Yes |

## Hardware Support

### Touchpad

Without xf86-input-synaptics (see [Touchpad_Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")) the touchpad doesnt work, but the pointstick with the buttons are ready to use.

### Cardreader

The cardreader can not detect the inserted card. Run as root the following command:

```
# echo 1 | tee /sys/bus/pci/rescan

```