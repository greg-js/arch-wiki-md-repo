### Instalación

```
pacman -S capi4hylafax

```

### Configuración:

*   Ejecute 'faxsetup' como root para ajustar hylafax a sus necesidades.
*   No intente de ninguna manera ejecutar faxaddmodem para dispositivos capi20!!!
*   c2faxaddmodem' es una buena herramienta para configurar su tarjeta isdn.
*   Ajuste var/spool/hylafax/etc/config/config.faxCAPI a sus necesidades, si es que necesita algo más.
*   Añada 'hylafax' y 'capi4hylafax' a su lista de demonios en /etc/rc.conf.
*   Asegúrese de que su dispositivo tenga los permisos correctos 'uucp', usuarios de udev deben
*   reiniciar udev después de la instalación.

*   Añada las siguientes dos líneas a /var/spool/hylafax/etc/config:

```
   SendFaxCmd: /usr/bin/c2faxsend

```

### Notas:

*   para grabar su configuración, no olvide por favor añadir a /etc/pacman.conf

```
 NoUpgrade   = var/spool/hylafax/etc/config/config.faxCAPI

```

*   Si necesita más de un controlador isdn lea por favor el manual de capi4hylafax.

Para hacer comentarios acerca del paquete utilice por favor este hilo: [https://bbs.archlinux.org/viewtopic.php?t=11089](https://bbs.archlinux.org/viewtopic.php?t=11089)

Para pistas y consejos eche un vistazo por favor a la wiki [Hylafax](/index.php/Hylafax "Hylafax").