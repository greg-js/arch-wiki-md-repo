**Estado de la traducción**
Este artículo es una traducción de [TerraTec Cinergy T RC MKII USB Stick](/index.php/TerraTec_Cinergy_T_RC_MKII_USB_Stick "TerraTec Cinergy T RC MKII USB Stick"), revisada por última vez el **2019-01-26**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=TerraTec_Cinergy_T_RC_MKII_USB_Stick&diff=0&oldid=564896) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**TerraTec Cinergy T RC MKII** es un receptor USB DVB-T fabricado por TerraTec Electronic GmbH. Este artículo describe la instalación de TerraTec Cinergy T RC MKII USB Stick (USB ID 0ccd:0097). Es compatible con el kernel desde la versión 2.6.37.

## Verificar la ID del dispositivo

Asegúrese de tener el dispositivo 'correcto'. La ID del USB es '0ccd: 0097':

```
$ lsusb
Bus 001 Device 004: ID 0ccd:0097 TerraTec Electronic GmbH Cinergy T RC MKII

```

## Instalación

Si conecta el dispositivo, verá el siguiente mensaje del kernel:

```
$ dmesg
[ 4403.369654] usb 1-1: new high-speed USB device number 5 using ehci_hcd
[ 4403.862797] dvb-usb: found a 'TerraTec Cinergy T Stick RC' in cold state, will try to load a firmware
[ 4403.864076] dvb-usb: did not find the firmware file. (dvb-usb-af9015.fw) Please see linux/Documentation/dvb/ for more details on firmware-problems. (-2)
[ 4403.864103] dvb_usb_af9015: probe of 1-1:1.0 failed with error -2

```

Necesita instalar el archivo de firmware:

```
$ wget [http://www.otit.fi/~crope/v4l-dvb/af9015/af9015_firmware_cutter/firmware_files/4.95.0/dvb-usb-af9015.fw](http://www.otit.fi/~crope/v4l-dvb/af9015/af9015_firmware_cutter/firmware_files/4.95.0/dvb-usb-af9015.fw)
# cp dvb-usb-af9015.fw /usr/lib/firmware/

```

Vuelva a conectar el dispositivo y debería ver la siguiente salida. El dispositivo ya estará listo para su uso.

```
$ dmesg
[ 4867.138959] dvb-usb: generic DVB-USB module successfully deinitialized and disconnected.
[ 4870.056313] usb 1-1: new high-speed USB device number 6 using ehci_hcd
[ 4870.549447] dvb-usb: found a 'TerraTec Cinergy T Stick RC' in cold state, will try to load a firmware
[ 4870.551676] dvb-usb: downloading firmware from file 'dvb-usb-af9015.fw'
[ 4870.618834] dvb-usb: found a 'TerraTec Cinergy T Stick RC' in warm state.
[ 4870.618971] dvb-usb: will pass the complete MPEG2 transport stream to the software demuxer.
[ 4870.619381] DVB: registering new adapter (TerraTec Cinergy T Stick RC)
[ 4870.622186] af9013: firmware version:4.95.0.0
[ 4870.627936] DVB: registering adapter 0 frontend 0 (Afatech AF9013 DVB-T)...
[ 4870.630198] tda18218: NXP TDA18218HN successfully identified.
[ 4870.631940] Registered IR keymap rc-terratec-slim-2
[ 4870.632197] input: IR-receiver inside an USB DVB receiver as /devices/pci0000:00/0000:00:1d.7/usb1/1-1/rc/rc2/input11
[ 4870.632437] rc2: IR-receiver inside an USB DVB receiver as /devices/pci0000:00/0000:00:1d.7/usb1/1-1/rc/rc2
[ 4870.632446] dvb-usb: schedule remote query interval to 500 msecs.
[ 4870.632454] dvb-usb: TerraTec Cinergy T Stick RC successfully initialized and connected.

```

## Enlaces externos

*   [TerraTec Cinergy T RC MKII en Linux TV](http://www.linuxtv.org/wiki/index.php/TerraTec_Cinergy_T_USB_RC)
*   [Página web del producto](http://www.terratec.net/en/products/Cinergy_T_Stick_RC_97818.html)