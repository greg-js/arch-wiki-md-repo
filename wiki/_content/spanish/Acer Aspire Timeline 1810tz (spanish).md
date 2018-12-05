**Estado de la traducción**
Este artículo es una traducción de [Acer Aspire Timeline 1810tz](/index.php/Acer_Aspire_Timeline_1810tz "Acer Aspire Timeline 1810tz"), revisada por última vez el **2018-12-04**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Acer_Aspire_Timeline_1810tz&diff=0&oldid=558197) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Acer Aspire Timeline 1810tz**

## Contents

*   [1 lspci](#lspci)
*   [2 Control del ventilador](#Control_del_ventilador)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 Panel táctil](#Panel_táctil)
*   [4 Véase también](#Véase_también)

## lspci

```
00:00.0 Host bridge: Intel Corporation Mobile 4 Series Chipset Memory Controller Hub (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:02.1 Display controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:1a.0 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #4 (rev 03)
00:1a.7 USB Controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #2 (rev 03)
00:1b.0 Audio device: Intel Corporation 82801I (ICH9 Family) HD Audio Controller (rev 03)
00:1c.0 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 1 (rev 03)
00:1c.3 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 4 (rev 03)
00:1d.0 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #1 (rev 03)
00:1d.1 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #2 (rev 03)
00:1d.2 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #3 (rev 03)
00:1d.7 USB Controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #1 (rev 03)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev 93)
00:1f.0 ISA bridge: Intel Corporation ICH9M-E LPC Interface Controller (rev 03)
00:1f.2 SATA controller: Intel Corporation ICH9M/M-E SATA AHCI Controller (rev 03)
00:1f.3 SMBus: Intel Corporation 82801I (ICH9 Family) SMBus Controller (rev 03)
01:00.0 Ethernet controller: Atheros Communications Device 1063 (rev c0)
02:00.0 Network controller: Intel Corporation WiFi Link 1000 Series

```

## Control del ventilador

**Acerhdf** [[1]](http://piie.net/?section=acerhdf) es un módulo que se puede cargar para controlar la velocidad del ventilador. Descargue la última versión, descomprímala y siga las instrucciones del archivo "léame". Probablemente necesite agregar su versión de la BIOS al archivo de configuración. Su versión de la BIOS aparece en el mensaje de error cuando carga el módulo. Agregue acerhdf a su archivo rc.conf. Si no funciona, véase estas instrucciones: [Acer Aspire One#acerhdf](/index.php/Acer_Aspire_One#acerhdf "Acer Aspire One")

## Solución de problemas

### Panel táctil

Si el panel táctil deja de responder, agregue lo siguiente a su archivo xinitrc: [[2]](https://bbs.archlinux.org/viewtopic.php?id=107583)

 `~/.xinitrc` 
```
xinput --set-prop "SynPS/2 Synaptics TouchPad" "Synaptics Two-Finger Pressure" 280

```

## Véase también

*   [Linux Laptop](http://www.linlap.com/wiki/acer+aspire+1410)
*   [lesswatts.org](http://www.lesswatts.org)
*   [Ubuntu wiki](https://help.ubuntu.com/community/Aspire1810TZ/Karmic)
*   [Timeline en Notebookcheck](http://www.notebookcheck.net/Review-Acer-Aspire-Timeline-1810TZ-Subnotebook.21322.0.html)