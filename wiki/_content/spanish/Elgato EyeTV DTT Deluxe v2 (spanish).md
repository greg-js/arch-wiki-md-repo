**Estado de la traducción**
Este artículo es una traducción de [Elgato EyeTV DTT Deluxe v2](/index.php/Elgato_EyeTV_DTT_Deluxe_v2 "Elgato EyeTV DTT Deluxe v2"), revisada por última vez el **2019-01-25**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Elgato_EyeTV_DTT_Deluxe_v2&diff=0&oldid=564700) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

No hay demasiada información sobre EyeTV DTT Deluxe v2 en la web, así que allá vamos.

## Contents

*   [1 lsusb](#lsusb)
*   [2 Instalación](#Instalación)
*   [3 dmesg](#dmesg)
*   [4 Véase también](#Véase_también)

## lsusb

```
Bus 002 Device 005: ID 0fd9:002c Elgato Systems GmbH EyeTV DTT Deluxe v2

```

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [linuxtv-dvb-apps](https://aur.archlinux.org/packages/linuxtv-dvb-apps/) usando [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")

```
pacman -S linuxtv-dvb-apps

```

Descargue el firmware y copie los archivos a `/lib/firmware`

```
wget [http://kernellabs.com/firmware/as102/as102_data1_st.hex](http://kernellabs.com/firmware/as102/as102_data1_st.hex)
wget [http://kernellabs.com/firmware/as102/as102_data2_st.hex](http://kernellabs.com/firmware/as102/as102_data2_st.hex)
sudo mv as102_data* /usr/lib/firmware 
sudo chmod 644 /usr/lib/firmware/as102_data*

```

Ahora ya puede conectarlo y estará listo para su uso.

## dmesg

```
[  484.336751] usb 2-1: new high-speed USB device number 5 using ehci_hcd
[  484.804400] dvb_as102: module is from the staging directory, the quality is unknown, you have been warned.
[  484.804853] as10x_usb: device has been detected
[  484.804865] DVB: registering new adapter (Elgato EyeTV DTT Deluxe)
[  484.805121] DVB: registering adapter 0 frontend 0 (Elgato EyeTV DTT Deluxe)...
[  484.964484] as10x_usb: fimrware: as102_data1_st.hex loaded with success
[  485.199985] as10x_usb: fimrware: as102_data2_st.hex loaded with success
[  485.200015] usbcore: registered new interface driver Abilis Systems as10x usb driver

```

Véase más información sobre DVB-T en el artículo [DVB-S](/index.php/DVB-S "DVB-S"). Ejecute algo así como

```
pacman -S vlc
scan /usr/share/dvb/dvb-t/de-Nordrhein-Westfalen |tee channels.conf
vlc channels.conf 

```

## Véase también

[http://www.kernellabs.com/blog/?p=1378](http://www.kernellabs.com/blog/?p=1378)