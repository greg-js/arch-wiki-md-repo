## Contents

*   [1 BIOS](#BIOS)
*   [2 Installation](#Installation)
*   [3 Networking](#Networking)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Frequent Kernel Panics](#Frequent_Kernel_Panics)

## BIOS

Ensure that you have the latest BIOS and EC firmware from [MSI's website](https://www.msi.com/product/notebook/support/GT72-6QE-DOMINATOR-PRO-G.html#!type=download). Once you have updated, disable C-States and [Secure Boot](/index.php/Secure_Boot "Secure Boot") in the BIOS.

## Installation

This notebook has a physical hardware button to switch between the Intel and discrete (Nvidia 980m) GPU. Before installing Arch, boot into Windows and use the button to switch to the Intel display adapter. Also [#Networking](#Networking) in Linux might not work out of the box, so you may need to use a USB networking dongle or prepare your own [installation media](/index.php/Archboot "Archboot").

Now you can follow the [installation guide](/index.php/Installation_guide "Installation guide") as usual. Remember to install the [NVIDIA](/index.php/NVIDIA "NVIDIA") driver as well ([Nouveau](/index.php/Nouveau "Nouveau") might not work). After installing, boot back into Windows and use the button to switch the display adapter back to the NVIDIA GPU.

## Networking

This notebook comes with "Killer" Ethernet and Wireless PCI adapters (Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32) Subsystem: Bigfoot Networks, Inc. Device 1535). Wireless uses the Ath10k driver library which is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware), though you may need to download the latest firmware files from [Github](https://github.com/FireWalkerX/ath10k-firmware) in order to get it working after installation.

1.  Download [board-2.bin](https://github.com/FireWalkerX/ath10k-firmware/blob/7e56cbb94182a2fdab110cf5bfeded8fd1d44d30/QCA6174/hw3.0/board-2.bin) and [firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1](https://github.com/FireWalkerX/ath10k-firmware/blob/7e56cbb94182a2fdab110cf5bfeded8fd1d44d30/QCA6174/hw3.0/firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1)
2.  Rename them to `board.bin` and `firmware-4.bin`, respectively, and mark them as executable (`chmod +x`).
3.  Move both files to `/lib/firmware/ath10k/QCA6174/hw3.0/`

Reboot and then the built-in wireless NIC should work.

## Troubleshooting

### Frequent Kernel Panics

By default, the linux kernel may have issues with the Intel Skylake architecture of this notebook resulting in frequent kernel panics. To resolve this issue, add these options to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

	`nomodeset nohz=off clocksource=tsc`