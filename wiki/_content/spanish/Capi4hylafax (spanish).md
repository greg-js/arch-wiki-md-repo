**Estado de la traducción**
Este artículo es una traducción de [Capi4hylafax](/index.php/Capi4hylafax "Capi4hylafax"), revisada por última vez el **2018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Capi4hylafax&diff=0&oldid=460331) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

### Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [capi4hylafax](https://www.archlinux.org/packages/?name=capi4hylafax).

### Configuración

Ejecute *faxsetup* como usuario root para ajustar hylafax a sus necesidades. Además, ajuste `/var/spool/hylafax/etc/config/config.faxCAPI` a sus necesidades.

**Advertencia:** ¡No intente de ninguna de manera ejecutar faxaddmodem para dispositivos capi20!

*c2faxaddmodem* es una buena herramienta para configurar su tarjeta RDSI.

[Inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `hylafax.service` y `c2faxrecv.service`.

Asegúrese de que su dispositivo tenga los permisos correctos 'uucp'.

Agregue la siguiente línea a `/var/spool/hylafax/etc/config`:

```
SendFaxCmd: /usr/bin/c2faxsend

```

**Nota:** Si necesita más de un controlador rdsi, por favor lea el manual de capi4hylafax.

Para sugerencias y consejos, véase [Hylafax](/index.php/Hylafax "Hylafax").