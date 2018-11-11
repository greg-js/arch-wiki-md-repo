**[dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")**

* * *

[Preparar dispositivo](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") – [Cifrar dispositivo](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol) "Dm-crypt/Device encryption (Español)") – [Cifrar sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)") – [Cifrar un sistema completo](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt/Swap encryption (Español)") – <a class="mw-selflink selflink">Montar y acceder a /home cifrado</a> – [Configurar el sistema](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)") – [Especialidades](/index.php/Dm-crypt/Specialties_(Espa%C3%B1ol) "Dm-crypt/Specialties (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Dm-crypt/Mounting at login](/index.php/Dm-crypt/Mounting_at_login "Dm-crypt/Mounting at login"), revisada por última vez el **2018-09-26**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt/Mounting_at_login&diff=0&oldid=543817) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [pam_mount](/index.php/Pam_mount "Pam mount")

Es posible configurar [PAM](/index.php/PAM "PAM") y [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") para montar automáticamente una partición «home» cifrada con [dm-crypt](/index.php/Dm-crypt "Dm-crypt") cuando su propietario inicie sesión y desmontarla cuando la cierre.

Este tutorial supone que ya ha creado su partición cifrada, como se describe en [Dm-crypt/Encrypting a non-root file system (Español)](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)").

**Nota:**

*   Debe usar la misma contraseña para su cuenta de usuario y para LUKS.
*   En todos los ejemplos, reemplace `*SUNOMBRE*` con su nombre de usuario, `*1000*` con su ID de usuario y `*PARTICIÓN*` con el nombre del dispositivo de la partición cifrada.

## Montar al iniciar sesión

*pam_exec* se puede usar para desbloquear el dispositivo al iniciar sesión. Edite `/etc/pam.d/system-login` y añada la línea siguiente resaltada en negrita después de `auth include system-auth`:

**Nota:** GDM, LightDM, y tal vez otros administradores de inicio de sesión podrían requerir `pam_exec` para `session` también, vea [Talk:Dm-crypt/Mounting at login#pam_exec required for session & using script](/index.php/Talk:Dm-crypt/Mounting_at_login#pam_exec_required_for_session_.26_using_script "Talk:Dm-crypt/Mounting at login").
 `/etc/pam.d/system-login` 
```
...

auth       include    system-auth
**auth       optional   pam_exec.so expose_authtok quiet /usr/bin/cryptsetup open /dev/*PARTICIÓN* home-*SUNOMBRE***

...
```

Ahora edite `/etc/fstab` para montar el dispositivo desbloqueado utilizando [systemd.automount](/index.php/Fstab#Automount_with_systemd "Fstab"):

 `/etc/fstab` 
```
...

/dev/mapper/home-*SUNOMBRE*  /home/*SUNOMBRE*     ext4            rw,noatime,noauto,x-systemd.automount 0 2

...
```

Su directorio «home» se montará automáticamente en el primer acceso realizado por su entorno de escritorio o intérprete de órdenes.

## Desmontar al cerrar sesión

Después de cerrar todas sus sesiones, *systemd-logind* cierra automáticamente `user@*1000*.service`. Por lo tanto, puede especificar qué punto de montaje se requerirá y *systemd* lo desmontará automáticamente:

 `/etc/systemd/system/home-*SUNOMBRE*.mount.d/logout.conf` 
```
[Unit]
Requires=user@*1000*.service
```

Sin embargo, esto creará un bucle de dependencia circular que no puede resolverse automáticamente por *systemd* , por lo que debe describir las dependencias y ordenarlas de forma explícita:

 `/etc/systemd/system/user@*1000*.service.d/homedir.conf` 
```
[Unit]
Requires=home-*SUNOMBRE*.mount
After=home-*SUNOMBRE*.mount
```

**Nota:** Si su entorno de escritorio o alguna otra aplicación no cancela todos sus procesos al cerrar la sesión, es posible que deba establecer `KillUserProcesses=yes` en `/etc/systemd/logind.conf`.

### Bloquear

Después de desmontar, el dispositivo seguirá desbloqueado, y será posible montarlo sin volver a ingresar la contraseña. Puede configurar y [activar](/index.php/Enable "Enable") un servicio que se inicie cuando el dispositivo se desbloquea (`BindsTo=dev-mapper-home\x2d*SUNOMBRE*.device`) y expire después de que el dispositivo se desmonta (`Requires,Before=home-*SUNOMBRE*.mount`), bloqueando el dispositivo en el proceso (`ExecStop=cryptsetup close`):

 `/etc/systemd/system/cryptsetup-*SUNOMBRE*.service` 
```
[Unit]
DefaultDependencies=no
BindsTo=dev-*PARTICIÓN*.device
After=dev-*PARTICIÓN*.device
BindsTo=dev-mapper-home\x2d*SUNOMBRE*.device
Requires=home-*SUNOMBRE*.mount
Before=home-*SUNOMBRE*.mount
Conflicts=umount.target
Before=umount.target

[Service]
Type=oneshot
RemainAfterExit=yes
TimeoutSec=0
ExecStop=/usr/bin/cryptsetup close home-*SUNOMBRE*

[Install]
RequiredBy=dev-mapper-home\x2d*SUNOMBRE*.device
```

**Nota:** `dev-*PARTICIÓN*` es el resultado de `systemd-escape -p /dev/*PARTICIÓN*`