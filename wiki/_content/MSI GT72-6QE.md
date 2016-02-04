# MSI GT72-6QE

Please ensure that you have the latest bios and EC firmware from MSI's website here: [https://www.msi.com/product/notebook/support/GT72-6QE-DOMINATOR-PRO-G.html#!type=download](https://www.msi.com/product/notebook/support/GT72-6QE-DOMINATOR-PRO-G.html#!type=download)

The latest bios will expose some new switches in the bios. Disable the switch labelled C-States. (Also disable secureboot while you are in the BIOS) Once you've disabled the C-States you will be able to boot normally.

This notebook has a physical hardware button to switch between the Intel and discrete (Nvidia 980m) GPU. While in windows, press this button to switch it from the default Nvidia to the Intel display adaptor. Now you will be able to boot from the Arch USB media. While the open source nouveau may be able to handle the 980m in the future, at this time you will need to use the proprietary nvidia drivers. Follow the absolute beginner's guide wiki to finish the base arch install and remember to install the nvidia package as well. Now you will need to boot back into windows and use the button to switch the display adapter in use back to the nvidia gpu. Once you've rebooted again into Linux you can complete your install.

This notebook also comes with "Killer" Ethernet and Wireless PCI adapters. Neither are working out of the box with Linux at this time. A usb wifi dongle could have to be used to get up and running and then get the internal wifi working afterwards. The wireless NIC in my notebook is the Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32) Subsystem: Bigfoot Networks, Inc. Device 1535\. It uses the Ath10k driver library which is included in linux-firmware. For some reason, the drivers in linux-firmware at the time of this writing did not work. As a workaround you may have to install two files into /lib/firmware/ath10k/QCA6174/hw3.0/ from FireWalkerX's github page here

sudo wget [https://github.com/FireWalkerX/ath10k-firmware/blob/7e56cbb94182a2fdab110cf5bfeded8fd1d44d30/QCA6174/hw3.0/board-2.bin?raw=true](https://github.com/FireWalkerX/ath10k-firmware/blob/7e56cbb94182a2fdab110cf5bfeded8fd1d44d30/QCA6174/hw3.0/board-2.bin?raw=true) /lib/firmware/ath10k/QCA6174/hw3.0/board.bin

sudo wget [https://github.com/FireWalkerX/ath10k-firmware/blob/7e56cbb94182a2fdab110cf5bfeded8fd1d44d30/QCA6174/hw3.0/firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1?raw=true](https://github.com/FireWalkerX/ath10k-firmware/blob/7e56cbb94182a2fdab110cf5bfeded8fd1d44d30/QCA6174/hw3.0/firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1?raw=true) /lib/firmware/ath10k/QCA6174/hw3.0/firmware-4.bin

The files you need to overwrite are /lib/firmware/ath10k/QCA6174/hw3.0/board.bin and /lib/firmware/ath10k/QCA6174/hw3.0/firmware-4.bin Don't forget to make these files executable with sudo chmod +x /lib/firmware/ath10k/QCA6174/hw3.0/*

After you reboot then the wireless NIC will be working and you will be on your way to enjoying Arch Linux with your MSI GT72 6QE

Retrieved from "[https://wiki.archlinux.org/index.php?title=MSI_GT72-6QE&oldid=418799](https://wiki.archlinux.org/index.php?title=MSI_GT72-6QE&oldid=418799)"