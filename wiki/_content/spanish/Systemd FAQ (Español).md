## Contents

*   [1 FAQ](#FAQ)
    *   [1.1 ¿Por qué recibo mensajes de registro en mi consola?](#.C2.BFPor_qu.C3.A9_recibo_mensajes_de_registro_en_mi_consola.3F)
    *   [1.2 ¿Cómo puedo cambiar el número de gettys ejecutadas por defecto?](#.C2.BFC.C3.B3mo_puedo_cambiar_el_n.C3.BAmero_de_gettys_ejecutadas_por_defecto.3F)
    *   [1.3 ¿Cómo puedo obtener una salida con información más detallada durante el arranque?](#.C2.BFC.C3.B3mo_puedo_obtener_una_salida_con_informaci.C3.B3n_m.C3.A1s_detallada_durante_el_arranque.3F)
    *   [1.4 ¿Cómo evitar que se borre la consola después del arranque?](#.C2.BFC.C3.B3mo_evitar_que_se_borre_la_consola_despu.C3.A9s_del_arranque.3F)
    *   [1.5 ¿Qué opciones del kernel tengo que activar en caso de que no utilice el kernel oficial de Arch?](#.C2.BFQu.C3.A9_opciones_del_kernel_tengo_que_activar_en_caso_de_que_no_utilice_el_kernel_oficial_de_Arch.3F)
    *   [1.6 ¿Qué otras unidades dependen de una unidad?](#.C2.BFQu.C3.A9_otras_unidades_dependen_de_una_unidad.3F)
    *   [1.7 Mi ordenador se apaga, pero el power permanece encendido.](#Mi_ordenador_se_apaga.2C_pero_el_power_permanece_encendido.)
    *   [1.8 Después de migrar a systemd, ¿por qué no funciona el montaje de fakeRAID?](#Despu.C3.A9s_de_migrar_a_systemd.2C_.C2.BFpor_qu.C3.A9_no_funciona_el_montaje_de_fakeRAID.3F)
    *   [1.9 ¿Cómo puedo hacer un script de inicio durante el proceso de arranque?](#.C2.BFC.C3.B3mo_puedo_hacer_un_script_de_inicio_durante_el_proceso_de_arranque.3F)
    *   [1.10 El estado de .service dice «active (exited)» en verde (por ejemplo, iptables)](#El_estado_de_.service_dice_.C2.ABactive_.28exited.29.C2.BB_en_verde_.28por_ejemplo.2C_iptables.29)
    *   [1.11 Error Failed to issue method call: File exists](#Error_Failed_to_issue_method_call:_File_exists)

## FAQ

Para obtener una lista actualizada de problemas conocidos, consulte el upstream [TODO](http://cgit.freedesktop.org/systemd/systemd/tree/TODO).

### ¿Por qué recibo mensajes de registro en mi consola?

Debe establecer el nivel del registro del propio kernel. Históricamente, `/etc/rc.sysinit` hacía esto por nosotros y establecía el nivel del registro de dmesg a `3`, que era un *loglevel* razonablemente *moderado*. O bien, añada `loglevel=3` o `quiet` en los [parámetros del kernel](/index.php/Kernel_parameters "Kernel parameters").

### ¿Cómo puedo cambiar el número de gettys ejecutadas por defecto?

Para agregar otra getty, solo tiene que colocar otro enlace simbólico para crear instancias a otra getty en la carpeta `/etc/systemd/system/getty.target.wants/`:

```
# ln -sf /usr/lib/systemd/system/getty@.service /etc/systemd/system/getty.target.wants/getty@tty9.service
# systemctl start getty@tty9.service

```

Para eliminar una getty, simplemente elimine los enlaces simbólicos de la getty de la que quiera deshacerse en la carpeta `/etc/systemd/system/getty.target.wants/`:

```
# rm /etc/systemd/system/getty.target.wants/getty@{tty5,tty6}.service
# systemctl stop getty@tty5.service getty@tty6.service

```

Los usuarios también pueden cambiar el número de gettys, editando `/etc/systemd/logind.conf` y cambiando el valor de `NAutoVTs`. Al hacer esto, la activación bajo demanda se conserva, mientras que con el método anterior simplemente tendrá las gettys funcionando desde el arranque. systemd no utiliza el archivo `/etc/inittab`.

**Nota:** A partir de systemd 30, sólo una getty se pondrá en marcha de forma predeterminada. Si cambia a otra tty, una nueva getty se lanzará allí (socket-activation style). Aún entonces puede forzar procesos agetty adicionales utilizando los métodos anteriores.

### ¿Cómo puedo obtener una salida con información más detallada durante el arranque?

Si no ve ninguna salida en absoluto en la consola después del mensaje initram, esto significa que tiene el parámetro `quiet` en la línea del kernel. Lo mejor es quitarlo, al menos la primera vez que arranque con systemd, para ver si todo está bien. A continuación, verá una lista `[ OK ]` en verde o `[ FAILED ]` en rojo.

Los mensajes se registrarán en el log del sistema y si quiere indagar sobre del estado del propio sistema ejecute `systemctl` (no necesita privilegios de root) o busque en el registro boot/system con `journalctl`.

### ¿Cómo evitar que se borre la consola después del arranque?

Cree un archivo personalizado `getty@tty1.service` para copiar `/usr/lib/systemd/system/getty@.service` a `/etc/systemd/system/getty@tty1.service` y cambie `TTYVTDisallocate` a `no`.

### ¿Qué opciones del kernel tengo que activar en caso de que no utilice el kernel oficial de Arch?

Los Kernels anteriores a 2.6.39 no son compatibles.

Esta es una lista parcial de las opciones requeridas/recomendadas, podría haber más:

```
**General setup**
 CONFIG_FHANDLE=y
 CONFIG_AUDIT=y (recommended)
 CONFIG_AUDIT_LOGINUID_IMMUTABLE=y (not required, may break sysvinit compatibility)
 CONFIG_CGROUPS=y
 **-> Namespaces support**
    CONFIG_NET_NS=y (for private network)
**Networking support -> Networking options**
 CONFIG_IPV6=[y|m] (highly recommended)
**Device Drivers**
 **-> Generic Driver Options**
    CONFIG_UEVENT_HELPER_PATH=""
    CONFIG_DEVTMPFS=y
    CONFIG_DEVTMPFS_MOUNT=y (required if you don't use an initramfs)
 **-> Real Time Clock**
    CONFIG_RTC_DRV_CMOS=y (highly recommended)
**File systems**
 CONFIG_FANOTIFY=y (required for readahead)
 CONFIG_AUTOFS4_FS=[y|m]
 **-> Pseudo filesystems**
    CONFIG_TMPFS_POSIX_ACL=y (recommended, if you want to use pam_systemd.so)
```

### ¿Qué otras unidades dependen de una unidad?

Por ejemplo, si desea averiguar qué servicios activa un target como `multi-user.target`, use algo como esto:

 `$ systemctl show -p "Wants" multi-user.target`  `Wants=rc-local.service avahi-daemon.service rpcbind.service NetworkManager.service acpid.service dbus.service atd.service crond.service auditd.service ntpd.service udisks.service bluetooth.service org.cups.cupsd.service wpa_supplicant.service getty.target modem-manager.service portreserve.service abrtd.service yum-updatesd.service upowerd.service test-first.service pcscd.service rsyslog.service haldaemon.service remote-fs.target plymouth-quit.service systemd-update-utmp-runlevel.service sendmail.service lvm2-monitor.service cpuspeed.service udev-post.service mdmonitor.service iscsid.service livesys.service livesys-late.service irqbalance.service iscsi.service` 

En lugar de `Wants` también podría probar `WantedBy`, `Requires`, `RequiredBy`, `Conflicts`, `ConflictedBy`, `Before`, `After` para conocer los correspondientes tipos de dependencias y viceversa.

### Mi ordenador se apaga, pero el power permanece encendido.

Utilice:

```
$ systemctl poweroff

```

En lugar de `systemctl halt`.

### Después de migrar a systemd, ¿por qué no funciona el montaje de fakeRAID?

Asegúrese de usar:

 `# systemctl enable dmraid.service` 

### ¿Cómo puedo hacer un script de inicio durante el proceso de arranque?

Cree un nuevo archivo `/etc/systemd/system` (por ejemplo, *myscript*.service) y añada el siguiente contenido:

```
[Unit]
Description=My script

[Service]
ExecStart=/usr/bin/my-script

[Install]
WantedBy=multi-user.target 

```

Luego:

```
# systemctl enable *myscript*.service

```

Este ejemplo asume que quiere que el script arranque cuando el target multi-user sea lanzado.

**Nota:** En el caso de que desee iniciar un script de shell, asegúrese que tiene:

```
#!/bin/sh

```

en la primera línea del script. No escriba algo como:

```
ExecStart=/bin/sh /path/to/script.sh # NO FUNCIONA

```

porque eso no va a funcionar.

### El estado de .service dice «active (exited)» en verde (por ejemplo, iptables)

Esto es perfectamente normal. En el caso de las iptables es porque no hay ningún demonio corriendo, que es controlado en el kernel. Por lo tanto, se cierran después que las reglas han sido cargadas.

Para comprobar si las reglas iptables se han cargado correctamente:

 `# iptables --list` 

### Error `Failed to issue method call: File exists`

Esto sucede cuando se utiliza `systemctl enable` y el enlace simbólico que trata de crear en `/etc/systemd/system/` ya existe. Normalmente esto sucede cuando se cambia de un gestor de pantalla a otro (por ejemplo de GDM a KDM, que se pueden activar con `gdm.service` y `kdm.service`, respectivamente) y el enlace correspondiente `/etc/systemd/system/display-manager.service` ya existe.

Para resolver este problema, utilice `systemctl -f enable` para sobreescribir el enlace simbólico existente.