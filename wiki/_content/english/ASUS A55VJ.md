<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Model A55VJ-SXH161 (also K55VJ):](#Model_A55VJ-SXH161_(also_K55VJ):)
    *   [1.1 Hardware](#Hardware)
    *   [1.2 lspci](#lspci)
    *   [1.3 Graphics](#Graphics)
    *   [1.4 Touchpad](#Touchpad)
    *   [1.5 Cardreader](#Cardreader)

## Model A55VJ-SXH161 (also K55VJ):

### Hardware

*   **Processor:** Intel Core i7-3630QM
*   **Display:** 15.4" 1366x768
*   **Graphics:** Intel with NVIDIA GeForce GT 635M
*   **WLAN:** Intel Wireless-N 2230 802.11b/g/n
*   **LAN:** Realtek RTL8111/8168 Gigabit Ethernet controller

### lspci

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.1 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 (rev c4)
00:1c.3 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 4 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM76 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
01:00.0 VGA compatible controller: NVIDIA Corporation GF108M [GeForce GT 635M] (rev ff)
03:00.0 Network controller: Intel Corporation Centrino Wireless-N 2230 (rev c4)
04:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. Device 5289 (rev 01)
04:00.2 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168 PCI Express Gigabit Ethernet controller (rev 0a)

```

### Graphics

Works with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). NVIDIA GT635M works with [Bumblebee](/index.php/Bumblebee "Bumblebee").

### Touchpad

Works fine, use [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) for better control. Add i8042.nomux=1 to kernel line, seems to help with jittery touchpad.

### Cardreader

Works with [rts_bpp-dkms-git](https://aur.archlinux.org/packages/rts_bpp-dkms-git/), remember to blacklist existing mmc modules.