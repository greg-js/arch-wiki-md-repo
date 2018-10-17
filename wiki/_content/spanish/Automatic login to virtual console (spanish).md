Artículos relacionados

*   [Display manager (Español)](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)")
*   [Silent boot (Español)](/index.php/Silent_boot_(Espa%C3%B1ol) "Silent boot (Español)")
*   [Start X at login (Español)](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)")

En este artículo se describe cómo acceder automáticamente a una [consola virtual](https://en.wikipedia.org/wiki/es:Virtual_console se describen en [Start X at Login](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)").

## Contents

*   [1 Configuración](#Configuraci.C3.B3n)
    *   [1.1 Consola virtual](#Consola_virtual)
    *   [1.2 Consola de serie](#Consola_de_serie)
*   [2 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Configuración

La configuración cuenta con [los archivos drop-in](/index.php/Systemd#Editing_provided_units "Systemd") de systemd para sobrescribir los parámetros predeterminados que se pasan a agetty.

La configuración difiere según se trate de consolas virtuales o de serie. En la mayoría de los casos en que se desea configurar el inicio de sesión automático en la consola virtual, el nombre del dispositivo es `tty*N*`, donde `*N*` es un número. La configuración del inicio de sesión automático para las consolas de serie será un poco diferente. Los nombres de los dispositivos de las consolas de serie aparecen como `ttyS*N*`, donde `*N*` es un número.

### Consola virtual

Cree el siguiente archivo (y los directorios principales):

 `/etc/systemd/system/getty@tty1.service.d/autologin.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* --noclear %I 38400 linux
```

**Sugerencia:** La opción `Type=idle` retrasará la ejecución de agetty hasta que todos los trabajos (peticiones de cambio de estado de las unidades) se completen. Por otro lado, cuando se utiliza `Type=simple`, el servicio se pondrá en marcha de inmediato, pero puede producir mensajes relativos el arranque de systemd que se arrojen en el prompt del login. Esta opción es útil cuando [se inicia X automáticamente](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)"). Para usar esta opción, añada `Type=simple` en `autologin.conf`.

Si quiere utilizar otra *tty* distinta de *tty1* vea [Systemd FAQ](/index.php/Systemd_FAQ#Q:_How_do_I_change_the_number_of_gettys_running_by_default.3F "Systemd FAQ").

### Consola de serie

Cree el siguiente archivo (y los directorios principales):

 `/etc/systemd/system/getty@tty1.service.d/autologin.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* --noclear %I 38400 linux
```

## Véase también

*   [Cambiar el runlevel/target predefinido al arrancar](/index.php/Systemd_(Espa%C3%B1ol)#Cambiar_el_target_predeterminado_para_arrancar "Systemd (Español)").