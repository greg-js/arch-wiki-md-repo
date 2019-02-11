**Estado de la traducción**
Este artículo es una traducción de [ASUS A55VJ](/index.php/ASUS_A55VJ "ASUS A55VJ"), revisada por última vez el **2018-12-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ASUS_A55VJ&diff=0&oldid=558368) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Modelo A55VJ-SXH161 (también K55VJ):](#Modelo_A55VJ-SXH161_(también_K55VJ):)
    *   [1.1 Hardware](#Hardware)
    *   [1.2 lspci](#lspci)
    *   [1.3 Gráficos](#Gráficos)
    *   [1.4 Panel táctil](#Panel_táctil)
    *   [1.5 Lector de tarjetas](#Lector_de_tarjetas)

## Modelo A55VJ-SXH161 (también K55VJ):

### Hardware

*   **Procesador:** Intel Core i7-3630QM
*   **Monitor:** 15.4" 1366x768
*   **Gráficos:** Intel with NVIDIA GeForce GT 635M
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

### Gráficos

Funciona con [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). NVIDIA GT635M funciona con [Bumblebee](/index.php/Bumblebee_(Espa%C3%B1ol) "Bumblebee (Español)").

### Panel táctil

Funciona correctamente, utilize [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) para un mejor control. Agregue i8042.nomux=1 a la línea del kernel, parece ayudar con el temblor del panel táctil.

### Lector de tarjetas

Funciona con [rts_bpp-dkms-git](https://aur.archlinux.org/packages/rts_bpp-dkms-git/), recuerde poner en lista negra los módulos mmc existentes.