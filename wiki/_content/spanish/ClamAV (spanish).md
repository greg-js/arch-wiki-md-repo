**Estado de la traducción**
Este artículo es una traducción de [ClamAV](/index.php/ClamAV "ClamAV"), revisada por última vez el **2019-12-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ClamAV&diff=0&oldid=575975) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Clam AntiVirus](https://www.clamav.net) es un conjunto de herramientas de antivirus de código abierto (GPL) para UNIX. Proporciona una serie de utilidades que incluyen un demonio multiproceso flexible y escalable, un escáner de línea de órdenes y una herramienta avanzada para actualizaciones automáticas de las bases de datos. Debido a que el uso principal de ClamAV es en servidores de archivos/correos electrónicos para escritorios de Windows, detecta principalmente virus y malware de Windows con sus firmas incorporadas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Actualizar la base de datos](#Actualizar_la_base_de_datos)
*   [3 Iniciar el demonio](#Iniciar_el_demonio)
*   [4 Comprobar el software](#Comprobar_el_software)
*   [5 Añadir más repositorios de firmas/base de datos](#Añadir_más_repositorios_de_firmas/base_de_datos)
    *   [5.1 Configurar clamav-unofficial-sigs](#Configurar_clamav-unofficial-sigs)
        *   [5.1.1 Base de datos MalwarePatrol](#Base_de_datos_MalwarePatrol)
*   [6 Analizar en busca de virus](#Analizar_en_busca_de_virus)
*   [7 Utilizar milter](#Utilizar_milter)
*   [8 OnAccessScan](#OnAccessScan)
*   [9 Solución de problemas](#Solución_de_problemas)
    *   [9.1 Error: Clamd was NOT notified](#Error:_Clamd_was_NOT_notified)
    *   [9.2 Error: No supported database files found](#Error:_No_supported_database_files_found)
    *   [9.3 Error: Can't create temporary directory](#Error:_Can't_create_temporary_directory)
*   [10 Consejos y trucos](#Consejos_y_trucos)
    *   [10.1 Ejecutar en múltiples hilos](#Ejecutar_en_múltiples_hilos)
        *   [10.1.1 Utilizar clamscan](#Utilizar_clamscan)
        *   [10.1.2 Utilizar clamdscan](#Utilizar_clamdscan)
*   [11 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [clamav](https://www.archlinux.org/packages/?name=clamav).

## Actualizar la base de datos

Actualice las definiciones de virus con:

```
# freshclam

```

Si está detrás de un proxy, edite `/etc/clamav/freshclam.conf` y actualice HTTPProxyServer, HTTPProxyPort, HTTPProxyUsername y HTTPProxyPassword.

Los archivos de la base de datos se guardan en:

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd
/var/lib/clamav/bytecode.cvd

```

[Inicie/active](/index.php/Start/enable "Start/enable") `clamav-freshclam.service` para que las definiciones de virus se mantengan recientes.

## Iniciar el demonio

**Nota:** deberá ejecutar `freshclam` antes de iniciar el servicio por primera vez o se encontrará con errores que evitarán que ClamAV se inicie correctamente.

El servicio se llama `clamav-daemon.service`. [Inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") y [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") el servicio para que se inicie en el arranque del sistema.

## Comprobar el software

Para asegurarse de que ClamAV y las definiciones están instaladas correctamente, escanee el [archivo de prueba EICAR](https://www.eicar.org/86-0-Intended-use.html) (una firma inofensiva sin código de virus) con clamscan.

```
$ curl [https://www.eicar.org/download/eicar.com.txt](https://www.eicar.org/download/eicar.com.txt) | clamscan -

```

La salida **debe** incluir:

```
stdin: Eicar-Test-Signature FOUND

```

De lo contrario, lea la sección sobre [#Solución de problemas](#Solución_de_problemas) o solicite ayuda en [Arch Forums](https://bbs.archlinux.org/).

## Añadir más repositorios de firmas/base de datos

ClamAV puede usar bases de datos/firmas de otros repositorios o proveedores de seguridad.

Para añadir los más importantes en un solo paso, instale [clamav-unofficial-sigs](https://aur.archlinux.org/packages/clamav-unofficial-sigs/).

Esto agregará firmas/bases de datos de, por ejemplo, MalwarePatrol, SecuriteInfo, Yara, Linux Malware Detect, etc. Para ver la lista completa de bases de datos, [vea la descripción del repositorio de GitHub](https://github.com/extremeshok/clamav-unofficial-sigs#description).

### Configurar clamav-unofficial-sigs

[Active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `clamav-unofficial-sigs.timer`.

Esto actualizará regularmente las firmas no oficiales basadas en los archivos de configuración presentes en el directorio `/etc/clamav-unofficial-sigs`.

Para actualizar las firmas manualmente, ejecute lo siguiente:

```
# clamav-unofficial-sigs.sh

```

Para cambiar cualquier configuración predeterminada, remítase y modifique `/etc/clamav-unofficial-sigs/user.conf`.

**Nota:** no obstante lo anterior, debe tener el servicio `clamav-freshclam.service` [iniciado](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") para tener actualizaciones de las firmas oficiales de los servidores de réplicas de ClamAV.

#### Base de datos MalwarePatrol

Si desea utilizar la base de datos de MalwarePatrol, regístrese para obtener una cuenta en [https://www.malwarepatrol.net/free-guard-upgrade-option](https://www.malwarepatrol.net/free-guard-upgrade-option).

En `/etc/clamav-unofficial-sigs/user.conf`, cambie lo siguiente para activar esta funcionalidad:

```
malwarepatrol_receipt_code="SU-NÚMERO-DE-RECIBO" # Introduzca su número de recibo aquí.
malwarepatrol_product_code="8" # Utilice «8» si tiene una cuenta gratuita o «15» si es un cliente Premium.
malwarepatrol_list="clamav_basic" # clamav_basic o clamav_ext
malwarepatrol_free="yes" # Establezca «yes» si tiene una cuenta gratuita o «no» si es un cliente Premium.

```

Fuente: [https://www.malwarepatrol.net/clamav-configuration-guide/](https://www.malwarepatrol.net/clamav-configuration-guide/)

## Analizar en busca de virus

`clamscan` se puede usar para escanear ciertos archivos, directorios como /home o un sistema completo:

```
$ clamscan miarchivo
$ clamscan --recursive --infected /home
$ clamscan --recursive --infected --exclude-dir='^/sys|^/dev' /

```

Si desea que `clamscan` elimine el archivo infectado, agregue la opción `--remove` a la orden, o puede usar `--move=/directorio` para ponerlos en cuarentena.

También es posible que desee utilizar `clamscan` para escanear archivos más grandes. En este caso, añada las opciones `--max-filesize=4000M` y `--max-scansize=4000M` a la orden. «4000M» es el mayor valor posible y puede reducirse según sea necesario.

El uso de la opción `-l /ruta/al/archivo` imprimirá los registros de `clamscan` en un archivo de texto para poder localizar las infecciones notificadas.

## Utilizar milter

[Milter](https://en.wikipedia.org/wiki/es:Milter "wikipedia:es:Milter") escaneará su servidor sendmail en busca de correos electrónicos que contengan virus. Copie `/etc/clamav/clamav-milter.conf.sample` en `/etc/clamav/clamav-milter.conf` y ajústelo a sus necesidades. Por ejemplo:

 `/etc/clamav/clamav-milter.conf` 
```
MilterSocket /run/clamav/clamav-milter.sock
MilterSocketMode 660
FixStaleSocket yes
User clamav
PidFile /run/clamav/clamav-milter.pid
TemporaryDirectory /tmp
ClamdSocket unix:/var/lib/clamav/clamd.sock
LogSyslog yes
LogInfected Basic
```

Cree `/etc/systemd/system/clamav-milter.service`:

 `/etc/systemd/system/clamav-milter.service` 
```
[Unit]
Description='ClamAV Milter'
After=clamav-daemon.service

[Service]
Type=forking
ExecStart=/usr/bin/clamav-milter --config-file /etc/clamav/clamav-milter.conf

[Install]
WantedBy=multi-user.target
```

[Active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") e [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `clamav-milter.service`.

## OnAccessScan

El análisis en acceso (o análisis en tiempo real) requiere que el kernel se haya compilado con el módulo del kernel *fanotify* (kernel >= 3.8). Compruebe si *fanotify* está activado antes de habilitar escáner «On-Access».

```
$ zgrep FANOTIFY /proc/config.gz

```

El monitoreo en tiempo real analizará el archivo mientras lo lee, escribe o ejecuta.

Primero, edite el archivo de configuración `/etc/clamav/clamd.conf` añadiendo lo siguiente al final del archivo (también puede cambiar cada opción de forma individual):

 `/etc/clamav/clamd.conf` 
```
# Permite la exploración en acceso, requiere la ejecución de clamav-daemon.service
ScanOnAccess true

# Establezca el punto de montaje donde realizar el análisis de forma recursiva,
# esto podría consistir en cada ruta o ruta múltiple (una línea por ruta)
OnAccessMountPath /usr
OnAccessMountPath /home/
OnAccessExcludePath /var/log/

# Marca fanotify para bloquear cualquier evento
# en los archivos monitoreados para realizar el análisis
OnAccessPrevention false

# Realizar monitoreos en archivos recién creados, movidos o renombrados
OnAccessExtraScanning true

# Verificar el UID del evento de fanotify
OnAccessExcludeUID 0

# Especificar una acción a realizar cuando clamav detecte un archivo malicioso,
# también es posible especificar una orden en línea
VirusEvent /etc/clamav/detected.sh

# ADVERTENCIA: clamd debe ejecutarse como root
User root

```

A continuación, cree el archivo `/etc/clamav/detected.sh` y añada lo siguiente. Esto le permite cambiar/especificar el mensaje de depuración de errores cuando el servicio de análisis en tiempo real de clamd haya detectado un virus:

 `/etc/clamav/detected.sh` 
```
#!/bin/bash
PATH=/usr/bin
alert="Firma detectada: $CLAM_VIRUSEVENT_VIRUSNAME en $CLAM_VIRUSEVENT_FILENAME"

# Enviar la alerta al registro de systemd si existe, de lo contrario a /var/log
if [[ -z $(command -v systemd-cat) ]]; then
        echo "$(date) - $alert" >> /var/log/clamav/detections.log
else
        # Esto podría hacer que su entorno de escritorio muestre una alerta visual. Sucede en Plasma, pero la siguiente alerta visual es mucho mejor.
        echo "$alert" | /usr/bin/systemd-cat -t clamav -p emerg
fi

# Enviar una alerta a todos los usuarios de la interfaz gráfica.
XUSERS=($(who|awk '{print $1$NF}'|sort -u))

for XUSER in $XUSERS; do
    NAME=(${XUSER/(/ })
    DISPLAY=${NAME[1]/)/}
    DBUS_ADDRESS=unix:path=/run/user/$(id -u ${NAME[0]})/bus
    echo "run $NAME - $DISPLAY - $DBUS_ADDRESS -" >> /tmp/testlog 
    /usr/bin/sudo -u ${NAME[0]} DISPLAY=${DISPLAY} \
                       DBUS_SESSION_BUS_ADDRESS=${DBUS_ADDRESS} \
                       PATH=${PATH} \
                       /usr/bin/notify-send -i dialog-warning "clamAV" "$alert"
done

```

Si está utilizando [AppArmor](/index.php/AppArmor "AppArmor"), también es necesario permitir que clamd se ejecute como root:

```
# aa-complain clamd

```

[Reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") el servicio `clamav-daemon.service`.

Fuente: [http://blog.clamav.net/2016/03/configuring-on-access-scanning-in-clamav.html](http://blog.clamav.net/2016/03/configuring-on-access-scanning-in-clamav.html)

## Solución de problemas

### Error: Clamd was NOT notified

Si recibe los siguientes mensajes después de ejecutar freshclam:

```
WARNING: Clamd was NOT notified: Cannot connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

Añada un archivo sock para ClamAV:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

Luego, edite `/etc/clamav/clamd.conf` y descomente esta línea:

```
LocalSocket /var/lib/clamav/clamd.sock

```

Guarde el archivo y [reinicie](/index.php/Restart_(Espa%C3%B1ol) "Restart (Español)") `clamav-daemon.service`.

### Error: No supported database files found

Si obtiene el siguiente error al iniciar el demonio:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

Esto sucede debido a la falta de coincidencia entre la configuración de `DatabaseDirectory` de `/etc/clamav/freshclam.conf` y la configuración de `DatabaseDirectory` de `/etc/clamav/clamd.conf`. El archivo `/etc/clamav/freshclam.conf` apunta a `/var/lib/clamav`, pero `/etc/clamav/clamd.conf` (directorio por defecto) apunta a `/usr/share/clamav`, o a otro directorio. Edite `/etc/clamav/clamd.conf` y reemplace con el mismo DatabaseDirectory que el de `/etc/clamav/freshclam.conf`. Después de eso, clamav se iniciará con éxito.

### Error: Can't create temporary directory

Si obtiene el siguiente error, junto con una 'HINT' que contiene un UID y un número GID:

```
# can't create temporary directory

```

Corrija los permisos:

```
# chown UID:GID /var/lib/clamav & chmod 755 /var/lib/clamav

```

## Consejos y trucos

### Ejecutar en múltiples hilos

#### Utilizar clamscan

Al escanear un archivo o directorio desde la línea de órdenes usando `clamscan` solo se usa un hilo de la CPU. Esto puede estar bien en los casos en que el tiempo no es crítico o no desea que el equipo se ralentice. Si es necesario escanear carpetas grandes o unidades USB rápidamente, podría utilizar todas las CPU disponibles para acelerar el proceso.

`clamscan` está diseñado para usarse en un solo subproceso, pero esto no es obvice para que con el argumento `xargs` se puede utilizar para ejecutar escaneos en paralelo:

```
$ find /home/archie -type f -print | xargs -P $(nproc) clamscan

```

En este ejemplo, el parámetro `-P` para `xargs` ejecuta `clamscan` en tantos procesos como CPU existan (según informa `nproc`) al mismo tiempo. Las opciones `--max-lines` y `--max-args` permitirán un control aún más preciso de los procesamientos por lotes de la carga de trabajo entre los distintos hilos.

Utilice la siguiente versión si los nombres de archivos pueden contener espacios u otros caracteres especiales (como suelen hacer las unidades USB y otras antiguas de Windows):

```
$ find /home/archie -type f -print0 | xargs -0 -P $(nproc) clamscan

```

#### Utilizar clamdscan

Si ya tiene el demonio `clamd` ejecutandose, `clamdscan` puede usarse en su lugar (vea [#Iniciar el demonio](#Iniciar_el_demonio)):

```
$ clamdscan --multiscan --fdpass /home/archie

```

Aquí el parámetro `--multiscan` permite que `clamd` escanee el contenido del directorio en paralelo utilizando los hilos disponibles. El parámetro `--fdpass` es necesario para pasar los permisos del descriptor del archivo a `clamd` ya que el demonio se ejecuta bajo el usuario y grupo `clamav`.

El número de subprocesos disponibles para `clamdscan` se determina en `/etc/clamav/clamd.conf` a través del parámetro `MaxThreads` de [clamd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/clamd.conf.5). Aunque puede ver que el número de `MaxThreads` especificado es más de uno (el valor predeterminado actual es 10), cuando inicia la exploración utilizando `clamdscan` desde la línea de órdenes y no especifica `--multiscan`, solo se usará un hilo de CPU efectivo para escanear.

## Véase también

*   [Wikipedia:ClamAV](https://en.wikipedia.org/wiki/ClamAV "wikipedia:ClamAV")
*   [ClamSMTP](/index.php/ClamSMTP "ClamSMTP")