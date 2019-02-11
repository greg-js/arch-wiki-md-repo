**Estado de la traducción**
Este artículo es una traducción de [Acer Aspire 7720](/index.php/Acer_Aspire_7720 "Acer Aspire 7720"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Acer_Aspire_7720&diff=0&oldid=558206) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Para la instalación de 64 bits, primero actualice la BIOS para solucionar los problemas del ACPI y del wifi. Si usa 32 bits no debería haber problemas.

## Lo que no funciona

La hibernación (todavía está verde). La suspensión parece funcionar correctamente con el kernel 2.6.35, xorg 1.9.

| Hardware | Detalles | Estado |
| Disco duro | WDC WD2500BEVS-22UST0 250GB | Funciona. |
| Pantalla/Gráficos | Acer 17" (1440x900), Intel x3100 | Funciona perfectamente. |
| Wifi | Intel 3945 | Funciona después de instalar el firmware. Se utilizó netcfg2 o wicd para la gestión del WLAN. |
| Ethernet | Broadcom BCM5787 (controlador tg3) | Funciona sin necesidad de configuración. |
| Audio | Realtek ALC268 | Funciona correctamente. Sin embargo, la grabación desde el micrófono interno es defectuosa. |
| Lector de tarjetas | Lector de tarjetas 5 en 1 compatible con MultiMediaCard™ opcional, tarjeta Secure Digital, Memory Stick®, Memory Stick PRO™ o xD-Picture Card™ | ¿Funciona solo para las SD? ¿No reconoce las tarjetas MS? |
| Webcam | Acer "Crystal Eye" Webcam | Funciona (uvcvideo) |
| Panel táctil | ALPS PS/2 | Funciona (con las versiones actuales de X no es necesario configurar nada). |
| Bluetooth | Broadcom "A-Link BlueUsbA2" | Funciona |
| Sensor de control remoto | Funciona: instale LIRC, el controlador es lirc_ene0100\. Controlo satisfactoriamente MPD y MPlayer con este. |