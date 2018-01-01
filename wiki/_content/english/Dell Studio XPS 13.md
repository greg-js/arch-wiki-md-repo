I have just bought a new Dell Studio XPS 13\. I have not been able to find any information for installing Arch Linux on this machine. It is a very nice looking laptop, and runs fast and smooth. I have had a successful install (32-bit only, 64-bit). I still have a few things to get working, like the Bluetooth, and media buttons.

System Specs:

*   **Processor**
    *   Intel(R) Core(TM)2 Duo CPU P8600 @ 2.40GHz
*   **RAM Memory**
    *   4 GB DDR3
*   **Webcam**
    *   2.0 Megapixel Webcam
*   **Hard Disk**
    *   320GB SATA 7200 rpm HDD
    *   500GB SATA 7200 rpm HDD
*   **Video Card**
    *   NVIDIA 9400M
    *   NVIDIA 9500M (9400M G + 9200M GS)
*   **Wireless**
    *   Broadcom Corporation BCM4322 802.11a/b/g/n Wireless LAN Controller
    *   Atheros Communications Inc. AR928X Wireless Network Adapter

The basic installation performs normally, with the core cd, also the wireless modules ( Atheros wifi card ) were well recognised and worked out of the box.

## Power Management

### HDD important issue

See [Laptop#Hard drive spin down problem](/index.php/Laptop#Hard_drive_spin_down_problem "Laptop").

## Touchpad

The touchpad does not work completely out of the box. By default only the mouse buttons are working. To get the touchpad working, especially the area to move the mouse, follow the instructions described on the wiki page [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"). Just installing the package and an X restart should do the trick.