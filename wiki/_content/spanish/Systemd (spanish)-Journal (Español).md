**Estado de la traducción**
Este artículo es una traducción de [systemd/Journal](/index.php/Systemd/Journal "Systemd/Journal"), revisada por última vez el **2019-09-20**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Systemd/Journal&diff=0&oldid=580996) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

*systemd* tiene un sistema de registro (*«log»*) propio llamado journal. Por tanto, ya no es necesario hacer funcionar el demonio syslog. Para leer el registro, utilice:

```
# journalctl

```

En Arch Linux, el directorio `/var/log/journal/` es parte del paquete [systemd](https://www.archlinux.org/packages/?name=systemd), y journal (cuando `Storage=` está definido a `auto` en `/etc/systemd/journald.conf`) escribirá en `/var/log/journal/`. Si usted o algún programa eliminan ese directorio, *systemd* **no** lo volverá a crear automáticamente y en su lugar escribirá sus registros en `/run/systemd/journal` de una manera no persistente. Sin embargo, la carpeta se volverá a crear cuando establezca `Storage=persistent` y [reinicie](#Utilizar_las_unidades) `systemd-journald.service` (o reinicie el equipo).

El journald de systemd clasifica los mensajes por [#Nivel de prioridad](#Nivel_de_prioridad) y [#Nivel del recurso](#Nivel_del_recurso). La clasificación del registro corresponde al protocolo clásico de [Syslog](https://en.wikipedia.org/wiki/es:Syslog "wikipedia:es:Syslog") ([RFC 5424](https://tools.ietf.org/html/rfc5424)).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Nivel de prioridad](#Nivel_de_prioridad)
*   [2 Nivel del recurso](#Nivel_del_recurso)
*   [3 Filtrar la salida](#Filtrar_la_salida)
*   [4 Límite del tamaño de journal](#Límite_del_tamaño_de_journal)
*   [5 Limpiar manualmente archivos journal](#Limpiar_manualmente_archivos_journal)
*   [6 Journald coexistiendo con syslog](#Journald_coexistiendo_con_syslog)
*   [7 Reenviar journald a /dev/tty12](#Reenviar_journald_a_/dev/tty12)
*   [8 Especificar un journal diferente para visulizar](#Especificar_un_journal_diferente_para_visulizar)

## Nivel de prioridad

Se utiliza el código de severidad de syslog (en systemd llamado prioridad) para marcar la importancia de un mensaje [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Valor | Severidad | Palabra clave | Descripción | Ejemplos |
| 0 | Emergencia | emerg | El sistema está inutilizable | Bug importante del kernel, núcleo de systemd volcado.
Este nivel no debe ser utilizado por las aplicaciones. |
| 1 | Alerta | alert | Debe corregirse inmediatamente | El subsistema vital parece no funcionar. Pérdida de datos.
`kernel: BUG: unable to handle kernel paging request at ffffc90403238ffc`. |
| 2 | Crítico | crit | Condiciones criticas | Quiebra, volcado del núcleo. Tales como:
`systemd-coredump[25319]: Process 25310 (plugin-containe) of user 1000 dumped core`
Error en la aplicación principal del sistema, como X11. |
| 3 | Error | err | Condiciones de error | Se informa de error no grave:
`kernel: usb 1-3: 3:1: cannot get freq at ep 0x84`,
`systemd[1]: Failed unmounting /var.`,
`libvirtd[1720]: internal error: Failed to initialize a valid firewall backend`). |
| 4 | Advertencia | warning | Puede indicar que se producirá un error si no se toman medidas. | Un sistema de archivos no root tiene solo 1GB libre.
`org.freedesktop. Notifications[1860]: (process:5999): Gtk-WARNING **: Locale not supported by C library. Using the fallback 'C' locale`. |
| 5 | Aviso | notice | Eventos que son inusuales, pero que no presuponen un error. | `systemd[1]: var.mount: Directory /var to mount over is not empty, mounting anyway`. `gcr-prompter[4997]: Gtk: GtkDialog mapped without a transient parent. This is discouraged`. |
| 6 | Informativo | info | Mensajes de operaciones normales que no requieren ninguna acción. | `lvm[585]: 7 logical volume(s) in volume group "archvg" now active`. |
| 7 | Depuración errores | debug | Información útil para los desarrolladores para depurar errores de la aplicación. | `kdeinit5[1900]: powerdevil: Scheduling inhibition from ":1.14" "firefox" with cookie 13 and reason "screen"`. |

Si no puede encontrar un mensaje en el nivel de prioridad esperado, puede buscar también un par de niveles por encima y por debajo: estas reglas son recomendaciones y el desarrollador de la aplicación afectada puede tener una percepción diferente de la importancia del problema con respecto a la suya.

## Nivel del recurso

Se utiliza un código de recursos de syslog para especificar el tipo de programa que está registrando el mensaje [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Código del recurso | Palabra clave | Descripción | Información |
| 0 | kern | mensajes del kernel |
| 1 | user | mensajes a nivel de usuario |
| 2 | mail | sistema de correo | El arcaico POSIX todavía se admite y se usa a veces (para más información [mail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mail.1)) |
| 3 | daemon | demonios del sistema | Todos los demonios, incluyendo systemd y sus subsistemas |
| 4 | auth | mensajes de seguridad/autorización | También tenga en cuenta los diferentes recursos del código 10 |
| 5 | syslog | mensajes generados internamente por syslogd | Para las implementaciones de syslogd (no utilizadas por systemd, consulte el código 3) |
| 6 | lpr | impresora de línea]] (subsistema arcaico) |
| 7 | news | subsistema de noticias de la red (subsistema arcaico) |
| 8 | uucp | subsistema [UUCP](https://en.wikipedia.org/wiki/es:Copiador_de_Unix_a_Unix "wikipedia:es:Copiador de Unix a Unix") (subsistema arcaico) |
| 9 | demonio para el reloj del sistema | systemd-timesyncd |
| 10 | authpriv | mensajes de seguridad/autorización | También tenga en cuenta los diferentes recursos del código 4 |
| 11 | ftp | subsistema [FTP](https://en.wikipedia.org/wiki/es:Protocolo_de_transferencia_de_archivos "wikipedia:es:Protocolo de transferencia de archivos") |
| 12 | - | subsistema [NTP](https://en.wikipedia.org/wiki/es:Network_Time_Protocol "wikipedia:es:Network Time Protocol") |
| 13 | - | auditoría de registro |
| 14 | - | alerta de registro |
| 15 | cron | demonio de programación |
| 16 | local0 | uso local 0 (local0) |
| 17 | local1 | uso local 1 (local1) |
| 18 | local2 | uso local 2 (local2) |
| 19 | local3 | uso local 3 (local3) |
| 20 | local4 | uso local 4 (local4) |
| 21 | local5 | uso local 5 (local5) |
| 22 | local6 | uso local 6 (local6) |
| 23 | local7 | uso local 7 (local7) |

Por lo tanto, son códigos útiles para observar: 0,1,3,4,9,10,15.

## Filtrar la salida

*journalctl* le permite filtrar los resultados por campos específicos. Tenga en cuenta que si hay muchos mensajes para mostrar o el filtrado que hay que hacer abarca mucho tiempo, la salida de esta orden puede retrasarse durante bastante tiempo.

Ejemplos:

*   Mostrar todos los mensajes del arranque: `# journalctl -b` Sin embargo, a veces a uno le interesan no los mensajes actuales, sino los mensajes desde el arranque anterior (por ejemplo, si ocurrió un fallo del sistema irrecuperable). Esto es posible pasando el parámetro `-b`: `journalctl -b -0` muestra los mensajes del arranque actual, `journalctl -b -1` muestra los mensajes del arranque anterior, `journalctl -b -2` muestra los mensajes desde los dos últimos arranques y así sucesivamente. Véase [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) para una descripción completa, dado que los argumentos que se pueden pasar a la orden hacen que el filtrado pueda ser mucho más potente.
*   Mostrar todos los mensajes de fecha (y hora opcional): `# journalctl --since="2012-10-30 18:17:16"` 
*   Mostrar todos los mensajes desde hace 20 minutos: `# journalctl --since "20 min ago"` 
*   Seguir los mensajes nuevos: `# journalctl -f` 
*   Mostrar todos los mensajes por un ejecutable específico: `# journalctl /usr/lib/systemd/systemd` 
*   Mostrar todos los mensajes para un proceso específico: `# journalctl _PID=1` 
*   Mostrar todos los mensajes por una unidad específica: `# journalctl -u man-db.service` 
*   Mostrar el búfer del kernel `# journalctl -k` 
*   Mostrar solo mensajes de error, críticos y de prioridad de alerta `# journalctl -p err..alert` También se pueden usar números, `journalctl -p 3..1`. Si se utiliza un solo número/palabra clave, `journalctl -p 3` —también se incluyen todos los niveles de prioridad más altos—.
*   Mostrar el equivalente de auth.log para filtrar en el código de instalación de syslog: `# journalctl SYSLOG_FACILITY=10` 
*   Si el directorio de journal (de manera predeterminada, ubicado en `/var/log/journal`) contiene una gran cantidad de datos de registro, entonces `journalctl` puede tardar varios minutos en filtrar la salida. Puede acelerarlo significativamente usando la opción `--file` para forzar a `journalctl` a buscar solo en el journal más reciente: `# journalctl --file /var/log/journal/*/system.journal -f` 

Véase [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1), [systemd.journal-fields(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.journal-fields.7) o esta [entrada de blog](http://0pointer.de/blog/projects/journalctl.html) de Lennert para obtener más detalles.

**Sugerencia:** De forma predeterminada, *journalctl* trunca las líneas más largas que exceden del ancho de la pantalla, pero en algunos casos, puede ser mejor activar el ajuste en lugar de fracturarlas. Esto puede ser controlado por la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `SYSTEMD_LESS`, que contiene opciones pasadas a [less](/index.php/Core_utilities#Essentials "Core utilities") (el paginador predeterminado) y, por defecto, a `FRSXMK` (consulte [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1) y [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) para más detalles).

Al omitir la opción `S`, la salida se ajustará en lugar de truncarla. Por ejemplo, inicie *journalctl* de la siguiente manera:

```
$ SYSTEMD_LESS=FRXMK journalctl

```
Si desea establecer este comportamiento como predeterminado, [exporte](/index.php/Environment_variables_(Espa%C3%B1ol)#Por_usuario "Environment variables (Español)") la variable desde `~/.bashrc` o `~/.zshrc`.

**Sugerencia:** mientras journal se almacena en un formato binario, el contenido de los mensajes almacenados no se modifica. Esto significa que se puede visualizar en forma de *strings* («*cadenas*»), por ejemplo, para la recuperación en un entorno que no tiene instalado *systemd*. Ejemplo de orden: `$ strings /mnt/arch/var/log/journal/af4967d77fba44c6b093d0e9862f6ddd/system.journal | grep -i *message*` 

## Límite del tamaño de journal

Si journal se ha creado como permanente (no volátil), el límite de su tamaño se establece con un valor predeterminado correspondiente al 10% del tamaño del sistema de archivos pero limitado a 4 GiB. Por ejemplo, con `/var/log/journal` alojado en una partición raíz de 20 GiB, esto permitiría almacenar hasta 2 GiB de datos en journal. En una de 50 GiB, tendría un máximo de 4 GiB.

El tamaño máximo del journal permanente puede ser controlado descomentando y modificando la correspondiente línea:

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

También es posible utilizar el mecanismo de sobrescribir la configuración con fragmentos insertados en lugar de editar el archivo de configuración global. En este caso, no olvide colocar el reemplazo debajo del encabezado de `[Journal]`:

 `/etc/systemd/journald.conf.d/00-journal-size.conf` 
```
[Journal]
SystemMaxUse=50M
```

[Reinicie](#Utilizar_las_unidades) el servicio `systemd-journald.service` después de cambiar esta configuración para aplicar inmediatamente el nuevo límite.

Vea [journald.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5) para más información.

## Limpiar manualmente archivos journal

Los archivos journal se pueden eliminar globalmente de `/var/log/journal/` utilizando *por ejemplo* `rm`, o se pueden recortar de acuerdo con varios criterios usando `journalctl`. Ejemplos:

*   Eliminar los archivos journal archivados hasta que el espacio en disco que utilizan esté por debajo de 100M: `# journalctl --vacuum-size=100M` 
*   Hacer que todos los archivos journal no contengan datos de más de 2 semanas. `# journalctl --vacuum-time=2weeks` 

Vea [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) para más información.

## Journald coexistiendo con syslog

La compatibilidad con una implementación clásica, [syslog](/index.php/Syslog-ng "Syslog-ng"), no reconocida por journald, se puede proporcionar al permitir que *systemd* reenvíe todos los mensajes a través del socket `/run/systemd/journal/syslog`. Para hacer que el demonio syslog funcione con journal, debe vincularse a este socket en lugar de a `/dev/log` ([anuncio oficial](http://lwn.net/Articles/474968/)).

El `journald.conf` predeterminado para reenviar al socket es `ForwardToSyslog=no` para evitar la sobrecarga del sistema, porque [rsyslog](/index.php/Rsyslog "Rsyslog") o [syslog-ng](/index.php/Syslog-ng "Syslog-ng") tiran de los mensajes de journal por [sí mismo](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

Vea [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") y [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng"), o [rsyslog](/index.php/Rsyslog "Rsyslog") respectivamente, para obtener detalles sobre la configuración.

## Reenviar journald a /dev/tty12

Cree un [directorio inclusivo](#Modificar_los_archivos_de_unidad_suministrados) `/etc/systemd/journald.conf.d` y cree un archivo `fw-tty12.conf` en él:

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 
```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

Depués [reinicie](#Utilizar_las_unidades) `systemd-journald.service`.

## Especificar un journal diferente para visulizar

Puede ser necesario verificar los registros de un sistema inoperativo, arrancado desde un sistema live para recuperar un sistema operativo. En tal caso, se puede montar el disco, por ejemplo en `/mnt`, y especificar la ruta de journal a través de `-D`/`--directory`, así:

```
$ journalctl -D */mnt*/var/log/journal -xe

```