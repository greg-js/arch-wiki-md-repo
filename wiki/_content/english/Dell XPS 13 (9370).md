| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | ath10k |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | hid_multitouch |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working |  ? |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working |  ? |
| Fingerprint sensor | Not working |  ? |

The Dell XPS 13 Early 2018 (9370) is the fifth-generation model of the XPS 13 line. The laptop was released in January 2018 in both a standard edition with Windows installed as well as a Developer Edition with Ubuntu 16.04 installed, featuring kernel 4.4 as of now. There are only minor hardware differences between them, mostly in regards to the mainboard microchip manufacturers. Just like the older versions ([9333](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)"), [9343](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)"), [9350](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)"), and [9360](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")) it is available in different hardware configurations as well. These fifth gen models includes Intel's eighth generation Kaby Lake processors, and can be configured with up to 16GB LPDDR3 2133 MHz RAM and a 1TB PCI SSD.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

## Booting

To boot from a USB device attached via the USB-C to USB-A adapter included in the box, you'll need to enable Thunderbolt boot in the BIOS (press F2 while the Dell logo is displayed). Once enabled, F12 on boot will enter the boot menu. It is also possible to use the right USB-C port directly without any BIOS adjustment.

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Intel graphics#Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

If you have the QHD+ (3200x1800) model, also check out [HiDPI](/index.php/HiDPI "HiDPI") for UI scaling configurations.

Note that the 'enable_psr=1' option appears not to work properly, at least on the touchscreen model.

## Wifi

Wifi should work out of the box with the `ath10k_pci` driver in recent [linux](https://www.archlinux.org/packages/?name=linux) kernels. (In my case) the Wifi firmware sometimes crashes when waking up from suspend. (firmware version `WLAN.RM.4.4.1-00051-QCARMSWP-1`; [dmesg](https://gist.github.com/dsprenkels/eb1c7095385fe16ee9b128ab0834be21))