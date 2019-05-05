[Clam AntiVirus](http://www.clamav.net) es una suite de antivirus de código abierto (GPL) para UNIX. Proporciona una serie de utilidades que incluyen un demonio multiproceso flexible y escalable, un escáner de línea de comandos y una herramienta avanzada para la actualización automática de las bases de las definiciones de virus. Dado que ClamAV viene usado principalmente en servidores de archivos/correos para escritorios Windows, el mismo detecta, sobretodo, virus y malware de Windows.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
*   [3 Iniciar el demonio](#Iniciar_el_demonio)
*   [4 Actualizar las bases de datos](#Actualizar_las_bases_de_datos)
*   [5 Escanear en busca de virus](#Escanear_en_busca_de_virus)
*   [6 Solución de problemas](#Solución_de_problemas)
    *   [6.1 Error: Clamd was NOT notified](#Error:_Clamd_was_NOT_notified)
    *   [6.2 Error: No supported database files found](#Error:_No_supported_database_files_found)
    *   [6.3 Error: Can't create temporary directory](#Error:_Can't_create_temporary_directory)

## Instalación

ClamAV puede ser [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [clamav](https://www.archlinux.org/packages/?name=clamav), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Configuración

Ya sea que vaya a utilizar clamav como un demonio o como un simple analizador de archivos, es necesario comentar la línea que contiene la palabra *Example*, que, por lo general, se encuentra en el inicio de los archivos `/etc/clamav/freshclam.conf` y `/etc/clamav/clamd.conf`.

**Nota:** En algunas configuraciones no se creará ningún archivo, y `/etc/clamav` contendrá archivos similares marcados con una extensión *.sample en su lugar. Modifiquelos cambiándoles el nombre con los nombres de los archivos mencionados anteriormente, con lo cual obtendrá el mismo resultado.

## Iniciar el demonio

El servicio se llama `clamav-daemon.service`. Léase [Daemons](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)") para más información sobre cómo iniciarlo y cómo activarlo en el arranque.

Cambie también las opciones de inicio de `no` a `yes`:

 `/etc/conf.d/clamav` 
```
# cambiaar a "yes" para iniciar
START_FRESHCLAM="yes"
START_CLAMD="yes"

```

## Actualizar las bases de datos

Edite el archivo de abajo y comente la línea que dice «Example».

 `/etc/clamav/freshclam.conf` 
```
# Comentar o quitar la línea de abajo.
# Example

```

Actualice las definiciones de virus con:

```
# freshclam

```

Los archivos de las bases de datos se guardan en:

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd

```

Puede iniciar/habilitar el demonio `clamav-freshclam.service` para mantener las bases de datos actualizadas.

## Escanear en busca de virus

La orden `clamscan` se puede utilizar para escanear determinados archivos, directorios (como la carpeta home) o el sistema completo:

```
$ clamscan miarchivo
$ clamscan -r -i /home
$ clamscan -r -i --exclude-dir=^/sys\|^/proc\|^/dev /

```

Si desea, puede hacer que `clamscan` elimine el archivo infectado utilizando la opción `--remove` en la orden.

La utilización de la opción `-l <ruta al archivo>` imprimirá el registro `clamscan` en un archivo de texto para localizar las infecciones notificadas.

## Solución de problemas

### Error: Clamd was NOT notified

Si recibe el siguiente mensaje después de ejecutar freshclam:

```
WARNING: Clamd was NOT notified: Cannot connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

Agregue un archivo *«sock»* para clamav:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

Después, edite el archivo `/etc/clamav/clamd.conf` y descomente esta línea:

 `LocalSocket /var/lib/clamav/clamd.sock` 

Guarde el archivo y [reinicie el demonio](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)").

### Error: No supported database files found

Si obtiene el siguiente error al iniciar el demonio:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

Ejecute freshclam como root:

 `# freshclam -v` 

### Error: Can't create temporary directory

Si obtiene el siguiente error, junto con un 'AVISO' que contiene un UID y un número GID:

 `# can't create temporary directory` 

Haga lo siguiente:

 `# chown UID:GID /var/lib/clamav & chmod 755 /var/lib/clamav`