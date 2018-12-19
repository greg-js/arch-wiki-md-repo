**Estado de la traducción**
Este artículo es una traducción de [HP Compaq nc4400](/index.php/HP_Compaq_nc4400 "HP Compaq nc4400"), revisada por última vez el **2018-12-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=HP_Compaq_nc4400&diff=0&oldid=559434) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Contents

*   [1 Especificaciones del sistema](#Especificaciones_del_sistema)
*   [2 Configuración](#Configuración)
    *   [2.1 Gráficos](#Gráficos)
    *   [2.2 Panel táctil](#Panel_táctil)
    *   [2.3 Wifi](#Wifi)
    *   [2.4 SD/MMC](#SD/MMC)
    *   [2.5 Sensores defectuosos del HDD](#Sensores_defectuosos_del_HDD)

## Especificaciones del sistema

salida de lshwd:

```
00:00.0 Class 0600: Intel Corp.|Mobile Memory Controller Hub (intel-agp)
00:02.0 Class 0300: Intel Corp.|Mobile Integrated Graphics Controller (i810)
00:02.1 Class 0380: Intel Corp.|Mobile Integrated Graphics Controller (vesa)
00:1b.0 Class 0403: Intel Corp.|I/O Controller Hub High Definition Audio (snd-hda-intel)
00:1c.0 Class 0604: Intel Corp.|I/O Controller Hub PCI Express Port 1 (unknown)
00:1c.1 Class 0604: Intel Corp.|I/O Controller Hub PCI Express Port 2 (unknown)
00:1d.0 Class 0c03: Intel Corp.|I/O Controller Hub UHCI USB #1 (unknown)
00:1d.1 Class 0c03: Intel Corp.|I/O Controller Hub UHCI USB #2 (unknown)
00:1d.2 Class 0c03: Intel Corp.|I/O Controller Hub UHCI USB #3 (unknown)
00:1d.3 Class 0c03: Intel Corp.|I/O Controller Hub UHCI USB #4 (unknown)
00:1d.7 Class 0c03: Intel Corp.|I/O Controller Hub EHCI USB (unknown)
00:1e.0 Class 0604: Intel Corp.|82801 Hub Interface to PCI Bridge (hw_random)
00:1f.0 Class 0601: Intel Corp.|Mobile I/O Controller Hub LPC (i8xx_tco)
00:1f.1 Class 0101: Intel Corp.|I/O Controller Hub PATA (piix)
00:1f.2 Class 0106: Intel Corp.|Mobile I/O Controller Hub SATA cc=AHCI (ahci)
02:06.0 Class 0607: Texas Instruments|PCIxx12 CardBus Controller (yenta_socket)
02:06.2 Class 0180: Texas Instruments|5-in-1 Multimedia Card Reader (SD/MMC/MS/MS PRO/xD) (unknown)
02:06.3 Class 0805: Texas Instruments|5-in-1 Multimedia Card Reader (SD/MMC/MS/MS PRO/xD) (unknown)
02:06.4 Class 0780: Texas Instruments|5-in-1 Multimedia Card Reader (SD/MMC/MS/MS PRO/xD) (unknown)
08:00.0 Class 0200: Broadcom Corp.|NetXtreme BCM5753M Gigabit Ethernet PCI Express (tg3)
10:00.0 Class 0280: Intel Corporation|PRO/Wireless 3945ABG (ipw3945)

```

## Configuración

### Gráficos

Véase [gráficos Intel](/index.php/Intel_graphics_(Espa%C3%B1ol) "Intel graphics (Español)").

### Panel táctil

Véase [Touchpad Synaptics](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)").

### Wifi

Véase [Configuración de red inalámbrica#iwlegacy](/index.php/Wireless_network_configuration_(Espa%C3%B1ol)#iwlegacy "Wireless network configuration (Español)")

### SD/MMC

Esto requiere el [módulo del kernel](/index.php/Kernel_module_(Espa%C3%B1ol) "Kernel module (Español)") *tifm*.

```
# modprobe tifm_core
# modprobe tifm_7xx1
# modprobe tifm_sd

```

### Sensores defectuosos del HDD

Véase [SMART](/index.php/SMART "SMART"). Ejemplo `/etc/smartd.conf`:

```
/dev/sda -a -d sat -m root@localhost

```