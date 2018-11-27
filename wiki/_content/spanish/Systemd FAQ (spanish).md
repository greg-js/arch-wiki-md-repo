**Estado de la traducción**
Este artículo es una traducción de [Systemd FAQ](/index.php/Systemd_FAQ "Systemd FAQ"), revisada por última vez el **2018-11-25**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Systemd_FAQ&diff=0&oldid=550510) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [systemd/User (Español)](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)")
*   [Daemons (Español)#Listado de demonios](/index.php/Daemons_(Espa%C3%B1ol)#Listado_de_demonios "Daemons (Español)")

## Contents

*   [1 FAQ](#FAQ)
    *   [1.1 ¿Por qué recibo mensajes de registro en mi consola?](#¿Por_qué_recibo_mensajes_de_registro_en_mi_consola?)
    *   [1.2 ¿Cómo puedo cambiar el número de gettys ejecutadas por defecto?](#¿Cómo_puedo_cambiar_el_número_de_gettys_ejecutadas_por_defecto?)
    *   [1.3 ¿Cómo puedo obtener una salida con información más detallada durante el arranque?](#¿Cómo_puedo_obtener_una_salida_con_información_más_detallada_durante_el_arranque?)
    *   [1.4 ¿Cómo evitar que se borre la consola después del arranque?](#¿Cómo_evitar_que_se_borre_la_consola_después_del_arranque?)
    *   [1.5 ¿Qué opciones del kernel son requeridas por systemd?](#¿Qué_opciones_del_kernel_son_requeridas_por_systemd?)
    *   [1.6 ¿Qué otras unidades dependen de una unidad?](#¿Qué_otras_unidades_dependen_de_una_unidad?)
    *   [1.7 Mi ordenador se apaga, pero el *power* permanece encendido.](#Mi_ordenador_se_apaga,_pero_el_power_permanece_encendido.)
    *   [1.8 Después de migrar a systemd, ¿por qué no funciona el montaje de fakeRAID?](#Después_de_migrar_a_systemd,_¿por_qué_no_funciona_el_montaje_de_fakeRAID?)
    *   [1.9 ¿Cómo puedo hacer un script que se inicie durante el proceso de arranque?](#¿Cómo_puedo_hacer_un_script_que_se_inicie_durante_el_proceso_de_arranque?)
    *   [1.10 El estado de .service dice «active (exited)» en verde (por ejemplo, iptables)](#El_estado_de_.service_dice_«active_(exited)»_en_verde_(por_ejemplo,_iptables))
    *   [1.11 Error «Failed to issue method call: File exists»](#Error_«Failed_to_issue_method_call:_File_exists»)

## FAQ

Para obtener una lista actualizada de problemas conocidos, consulte [TODO](http://cgit.freedesktop.org/systemd/systemd/tree/TODO) de los desarrolladores.

### ¿Por qué recibo mensajes de registro en mi consola?

Debe establecer el nivel del registro del propio kernel. Históricamente, `/etc/rc.sysinit` hacía esto por nosotros y establecía el nivel del registro de dmesg a `3`, que era un nivel de registro razonablemente moderado. O bien, añada `loglevel=3` o `quiet` en los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").

### ¿Cómo puedo cambiar el número de gettys ejecutadas por defecto?

Actualmente, solo un [getty](https://en.wikipedia.org/wiki/esTerminal_(inform%C3%A1tica) (abreviatura de «*get teletype*») se inicia de forma predeterminada. Si cambia a otra tty, se lanzará un getty allí (estilo de activación por socket). En otras palabras, [Ctl] [Alt] [F2] lanzará un nuevo getty en tty2.

Por defecto, el número de gettys autoactivados está limitado a seis. Por lo tanto [F7] a [F12] no lanzará un getty.

Si desea cambiar este comportamiento, edite `/etc/systemd/logind.conf` y cambie el valor de `NAutoVTs`. Si desea que todas las teclas [F*x*] inicien un getty, aumente el valor de NAutoVTs a 12\. Si está [reenviando journald a tty12](/index.php/Systemd_(Espa%C3%B1ol)#Reenviar_journald_a_/dev/tty12 "Systemd (Español)"), ponga el valor de NAutoVTs a 11 (dejando tty12 libre).

También puede preactivar gettys para que se ejecuten desde el arranque.

Para agregar otro getty preactivada, solo tiene que colocar otro enlace simbólico para crear instancias a otro getty en la carpeta `/etc/systemd/system/getty.target.wants/`:

```
# ln -sf /usr/lib/systemd/system/getty@.service /etc/systemd/system/getty.target.wants/getty@tty9.service
# systemctl start getty@tty9.service

```

Para eliminar un getty, simplemente elimine los enlaces simbólicos del getty de la que quiera deshacerse en la carpeta `/etc/systemd/system/getty.target.wants/`:

```
# rm /etc/systemd/system/getty.target.wants/getty@{tty5,tty6}.service
# systemctl stop getty@tty5.service getty@tty6.service

```

systemd no usa el archivo `/etc/inittab`.

### ¿Cómo puedo obtener una salida con información más detallada durante el arranque?

Si no ve ninguna salida en absoluto en la consola después del mensaje initram, esto significa que tiene el parámetro `quiet` en la línea del kernel. Lo mejor es quitarlo, al menos la primera vez que arranque con systemd, para ver si todo está bien. A continuación, verá una lista `[ OK ]` en verde o `[ FAILED ]` en rojo.

Los mensajes se registrarán en el log del sistema y si quiere indagar sobre del estado del propio sistema ejecute `systemctl` (no necesita privilegios de root) o busque en el registro boot/system con `journalctl`.

### ¿Cómo evitar que se borre la consola después del arranque?

Cree un directorio llamado `/etc/systemd/system/getty@.service.d` y coloque `nodisallocate.conf` allí para [sobrescribir](/index.php/Systemd_(Espa%C3%B1ol)#Modificar_los_archivos_de_unidad_suministrados "Systemd (Español)") la opción `TTYVTDisallocate` a `no`.

 `/etc/systemd/system/getty@.service.d/nodisallocate.conf` 
```
[Service]
TTYVTDisallocate=no
```

### ¿Qué opciones del kernel son requeridas por systemd?

Los Kernels anteriores a 3.0 no son compatibles.

Si usa un kernel personalizado, deberá asegurarse de que las opciones de systemd estén seleccionadas.

Si está compilando un nuevo kernel para usar con una versión instalada de systemd, las opciones requeridas y recomendadas se enumeran en el archivo README de systemd `/usr/share/doc/systemd/README`.

Si se está preparando para instalar una nueva versión de systemd y está ejecutando un kernel personalizado, la versión más reciente del archivo se puede encontrar en [the systemd git](http://cgit.freedesktop.org/systemd/systemd/tree/README).

### ¿Qué otras unidades dependen de una unidad?

Por ejemplo, si desea averiguar qué servicios activa un target como `multi-user.target`, use algo como esto:

 `$ systemctl show -p "Wants" multi-user.target`  `Wants=rc-local.service avahi-daemon.service rpcbind.service NetworkManager.service acpid.service dbus.service atd.service crond.service auditd.service ntpd.service udisks.service bluetooth.service org.cups.cupsd.service wpa_supplicant.service getty.target modem-manager.service portreserve.service abrtd.service yum-updatesd.service upowerd.service test-first.service pcscd.service rsyslog.service haldaemon.service remote-fs.target plymouth-quit.service systemd-update-utmp-runlevel.service sendmail.service lvm2-monitor.service cpuspeed.service udev-post.service mdmonitor.service iscsid.service livesys.service livesys-late.service irqbalance.service iscsi.service` 

En lugar de `Wants` también podría probar `WantedBy`, `Requires`, `RequiredBy`, `Conflicts`, `ConflictedBy`, `Before`, `After` para conocer los correspondientes tipos de dependencias y viceversa.

### Mi ordenador se apaga, pero el *power* permanece encendido.

Utilice `systemctl poweroff`, en lugar de `systemctl halt`.

### Después de migrar a systemd, ¿por qué no funciona el montaje de fakeRAID?

Asegúrese de usar:

```
# systemctl enable dmraid.service

```

### ¿Cómo puedo hacer un script que se inicie durante el proceso de arranque?

Cree un nuevo archivo como `/etc/systemd/system/myscript.service` y añada el siguiente contenido:

 `/etc/systemd/system/*myscript*.service` 
```
[Unit]
Description=My script

[Service]
ExecStart=/usr/bin/my-script

[Install]
WantedBy=multi-user.target
```

Este ejemplo asume que quiere que el script arranque cuando el target multi-user sea lanzado. Asegúrese de hacer [ejecutable](/index.php/Executable "Executable") el script.

[Active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") *myscript*.service para iniciar el servicio en el arranque.

**Nota:** en el caso de que desee iniciar un script de intérprete de órdenes, asegúrese que tiene `#!/bin/sh` en la primera línea del script. **No** escriba algo como `ExecStart=/bin/sh /path/to/script.sh` porque eso no va a funcionar.

### El estado de .service dice «active (exited)» en verde (por ejemplo, iptables)

Esto es perfectamente normal. En el caso de las iptables es porque no hay ningún demonio corriendo, que es controlado en el kernel. Por lo tanto, se cierran después que las reglas han sido cargadas.

Para comprobar si las reglas iptables se han cargado correctamente:

```
# iptables --list

```

### Error «Failed to issue method call: File exists»

Esto sucede cuando se utiliza `systemctl enable` y el enlace simbólico que trata de crear en `/etc/systemd/system/` ya existe. Normalmente esto pasa cuando se cambia de un gestor de pantalla a otro (por ejemplo de GDM a KDM, que se pueden activar con `gdm.service` y `kdm.service`, respectivamente) y el enlace correspondiente `/etc/systemd/system/display-manager.service` ya existe.

Para resolver este problema, utilice `systemctl -f enable` para sobreescribir el enlace simbólico existente.