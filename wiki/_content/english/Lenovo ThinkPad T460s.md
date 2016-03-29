This article covers the installation and configuration of Arch Linux on a Lenovo T460s laptop.

## Contents

*   [1 Model Description](#Model_Description)
    *   [1.1 Support](#Support)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Touchpad](#Touchpad)
    *   [2.2 Fingerprint Sensor](#Fingerprint_Sensor)

## Model Description

Lenovo ThinkPad T460s

### Support

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") | Manual |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Manual |
| Trackpad | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| Fingerprint Sensor | No |
| Mobile Broadband |  ? |
| Bluetooth |  ? |

## Troubleshooting

### Touchpad

There is an open [kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=114321) which causes the physical mouse button (belonging to the TrackPoint) to report release events immediately even when pressing and holding the button. This prevents drag and drop and similar actions from working.

### Fingerprint Sensor

The fingerprint sensor built into the T460s is currently not supported by [Fprint](/index.php/Fprint "Fprint").