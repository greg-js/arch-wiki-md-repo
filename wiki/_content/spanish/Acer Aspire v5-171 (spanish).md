**Estado de la traducción**
Este artículo es una traducción de [Acer Aspire v5-171](/index.php/Acer_Aspire_v5-171 "Acer Aspire v5-171"), revisada por última vez el **2018-12-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Acer_Aspire_v5-171&diff=0&oldid=306540) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Contents

*   [1 Introducción](#Introducción)
*   [2 Hardware](#Hardware)
*   [3 Conexión](#Conexión)
*   [4 Xorg](#Xorg)
*   [5 Teclas especiales](#Teclas_especiales)

## Introducción

Este netbook tiene buena compatibilidad con Arch.

## Hardware

```
   00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
   00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
   00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
   00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
   00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
   00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
   00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
   00:1c.1 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 (rev c4)
   00:1c.2 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 3 (rev c4)
   00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
   00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
   00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
   00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
   03:00.0 Network controller: Qualcomm Atheros AR9462 Wireless Network Adapter (rev 01)
   04:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57785 Gigabit Ethernet PCIe (rev 10)
   04:00.1 SD Host controller: Broadcom Corporation NetXtreme BCM57765 Memory Card Reader (rev 10)

```

## Conexión

*   El wifi y el ethernet funcionan perfectamente.

## Xorg

El panel táctil funciona sin necesidad de configuración. Sin embargo, es posible que desee descomentar la línea Option "AreaBottomEdge", en /etc/X11/xorg.conf.d/50-synaptics.conf.

También es posible que desee bloquear el panel táctil mientras escribe. Ejecute

```
   syndaemon -k -i 2 -d

```

## Teclas especiales

*   Las teclas de volumen funcionan una vez que se instala volumeicon.
*   Brillo: En /etc/default/grub, agregue "acpi_osi=Linux acpi_backlight=vendor" en GRUB_CMDLINE_LINUX.
*   wifi: ok
*   bloqueo del panel táctil: ok
*   encender/apagar la pantalla: ok.