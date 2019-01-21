**Estado de la traducción**
Este artículo es una traducción de [Dell Inspiron 1521](/index.php/Dell_Inspiron_1521 "Dell Inspiron 1521"), revisada por última vez el **2019-01-19**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dell_Inspiron_1521&diff=0&oldid=563919) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Contents

*   [1 Especificaciones de hardware](#Especificaciones_de_hardware)
    *   [1.1 Salida de lspci](#Salida_de_lspci)
    *   [1.2 Salida de lsusb](#Salida_de_lsusb)
*   [2 Red](#Red)
    *   [2.1 Wifi](#Wifi)
        *   [2.1.1 Broadcom Corporation BCM4311](#Broadcom_Corporation_BCM4311)

## Especificaciones de hardware

### Salida de lspci

```
00:00.0 Host bridge: ATI Technologies Inc RS690 Host Bridge
00:01.0 PCI bridge: ATI Technologies Inc RS690 PCI to PCI Bridge (Internal gfx)
00:05.0 PCI bridge: ATI Technologies Inc RS690 PCI to PCI Bridge (PCI Express Port 1)
00:07.0 PCI bridge: ATI Technologies Inc RS690 PCI to PCI Bridge (PCI Express Port 3)
00:12.0 SATA controller: ATI Technologies Inc SB600 Non-Raid-5 SATA
00:13.0 USB Controller: ATI Technologies Inc SB600 USB (OHCI0)
00:13.1 USB Controller: ATI Technologies Inc SB600 USB (OHCI1)
00:13.2 USB Controller: ATI Technologies Inc SB600 USB (OHCI2)
00:13.3 USB Controller: ATI Technologies Inc SB600 USB (OHCI3)
00:13.4 USB Controller: ATI Technologies Inc SB600 USB (OHCI4)
00:13.5 USB Controller: ATI Technologies Inc SB600 USB Controller (EHCI)
00:14.0 SMBus: ATI Technologies Inc SBx00 SMBus Controller (rev 14)
00:14.1 IDE interface: ATI Technologies Inc SB600 IDE
00:14.2 Audio device: ATI Technologies Inc SBx00 Azalia (Intel HDA)
00:14.3 ISA bridge: ATI Technologies Inc SB600 PCI to LPC Bridge
00:14.4 PCI bridge: ATI Technologies Inc SBx00 PCI to PCI Bridge
00:18.0 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] HyperTransport Technology Configuration
00:18.1 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] Address Map
00:18.2 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] DRAM Controller
00:18.3 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] Miscellaneous Control
01:05.0 VGA compatible controller: ATI Technologies Inc RS690M [Radeon X1200 Series]
03:00.0 Ethernet controller: Broadcom Corporation BCM4401-B0 100Base-TX (rev 02)
03:01.0 FireWire (IEEE 1394): Ricoh Co Ltd R5C832 IEEE 1394 Controller (rev 05)
03:01.1 SD Host controller: Ricoh Co Ltd R5C822 SD/SDIO/MMC/MS/MSPro Host Adapter (rev 22)
03:01.2 System peripheral: Ricoh Co Ltd R5C592 Memory Stick Bus Host Adapter (rev 12)
03:01.3 System peripheral: Ricoh Co Ltd xD-Picture Card Controller (rev 12)
0b:00.0 Network controller: Broadcom Corporation BCM4311 802.11b/g WLAN (rev 01)

```

### Salida de lsusb

```
Bus 006 Device 001: ID 1d6b:0002  
Bus 003 Device 001: ID 1d6b:0001  
Bus 001 Device 001: ID 1d6b:0001  
Bus 002 Device 001: ID 1d6b:0001  
Bus 005 Device 001: ID 1d6b:0001  
Bus 004 Device 001: ID 1d6b:0001 

```

## Red

El internet iba extremadamente lento. Esto era debido a un problema de IPv6. Después de agregar la siguiente línea a `/etc/modprobe.d/modprobe.conf`, todo funcionaba correctamente.

```
alias net-pf-10 off

```

### Wifi

#### Broadcom Corporation BCM4311

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl).