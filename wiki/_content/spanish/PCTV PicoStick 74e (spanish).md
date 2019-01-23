**Estado de la traducción**
Este artículo es una traducción de [PCTV PicoStick 74e](/index.php/PCTV_PicoStick_74e "PCTV PicoStick 74e"), revisada por última vez el **2019-01-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=PCTV_PicoStick_74e&diff=0&oldid=564168) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este artículo explica cómo utilizar el sintonizador *PCTV PicoStick 74e DVB-T* en Archlinux.

## Descargar el firmware

Ejecute las siguientes órdenes como root:

```
cd /lib/firmware
wget [http://www.kernellabs.com/firmware/as102/as102_data1_st.hex](http://www.kernellabs.com/firmware/as102/as102_data1_st.hex)
wget [http://www.kernellabs.com/firmware/as102/as102_data2_st.hex](http://www.kernellabs.com/firmware/as102/as102_data2_st.hex)

```

El firmware ya estará instalado.Puede conectar el sintonizador a un puerto USB y debería funcionar sin necesidad de configuración.

## Comprobar si funciona

Ejecute la siguiente orden (no se necesita ser root):

```
dmesg | tail

```

Debería obtener una salida como la que se muestra a continuación:

```
[  737.936943] usb 2-2.4.4: new high-speed USB device number 42 using ehci-pci
[  738.022688] as10x_usb: device has been detected
[  738.022707] DVB: registering new adapter (PCTV Systems picoStick (74e))
[  738.022991] usb 2-2.4.4: DVB: registering adapter 0 frontend 0 (PCTV Systems picoStick (74e))...
[  738.186315] as10x_usb: firmware: as102_data1_st.hex loaded with success
[  738.433948] as10x_usb: firmware: as102_data2_st.hex loaded with success

```

Como puede ver, ambos archivos de firmware se cargaron correctamente y el sintonizador ya está listo para ser utilizado.