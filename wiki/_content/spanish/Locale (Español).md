Los locales se utilizan en Linux para definir el idioma que el usuario utiliza. En la medida que los locales definen los juegos de caracteres utilizados, establecer la configuración regional correcta es especialmente importante si el idioma contiene caracteres no ASCII.

Los nombres de los «locales» `(configuración regional)` se definen utilizando el siguiente formato:

```
<idioma>_<territorio>.<codeset>[@<modificadores>]

```

## Contents

*   [1 Activar el «locale» necesario](#Activar_el_.C2.ABlocale.C2.BB_necesario)
    *   [1.1 Ejemplo ES Español](#Ejemplo_ES_Espa.C3.B1ol)
*   [2 Configuración del locale de todo el sistema](#Configuraci.C3.B3n_del_locale_de_todo_el_sistema)
*   [3 Configuración de locales de reserva](#Configuraci.C3.B3n_de_locales_de_reserva)
*   [4 Configuración de locales de usuarios](#Configuraci.C3.B3n_de_locales_de_usuarios)
    *   [4.1 Establecer la configuración regional en el archivo de inicio de la shell](#Establecer_la_configuraci.C3.B3n_regional_en_el_archivo_de_inicio_de_la_shell)
    *   [4.2 Establecer la configuración regional en .locale.conf](#Establecer_la_configuraci.C3.B3n_regional_en_.locale.conf)
*   [5 Configuración de la intercalación](#Configuraci.C3.B3n_de_la_intercalaci.C3.B3n)
*   [6 Configuración del primer día de la semana](#Configuraci.C3.B3n_del_primer_d.C3.ADa_de_la_semana)
*   [7 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [7.1 Mi terminal no es compatible con UTF-8](#Mi_terminal_no_es_compatible_con_UTF-8)
        *   [7.1.1 Xterm no es compatible con UTF-8](#Xterm_no_es_compatible_con_UTF-8)
        *   [7.1.2 Gnome-terminal o rxvt-unicode no es compatible con UTF-8](#Gnome-terminal_o_rxvt-unicode_no_es_compatible_con_UTF-8)
*   [8 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Activar el «locale» necesario

Antes de que un locale puede utilizarse en el sistema, tiene que ser activado primero. Para mostrar una lista de todos las versiones locales disponibles, utilice la orden:

```
$ locale -a

```

Para habilitar un locale, descomente el nombre del locale en el archivo `/etc/locale.gen`. Este archivo contiene todos los locales disponibles que se pueden utilizar en el sistema. El proceso es reversible deshabilitando (comentando) el locale. Después de que los locales necesarios están habilitados, el sistema necesita ser actualizado con las nuevas configuraciones regionales:

```
# locale-gen

```

Para mostrar ahora los locales actualmente en uso, escriba:

```
$ locale

```

**Sugerencia:** Aunque lo más probable es que se utilice un solo idioma en su máquina, puede ser útil o incluso necesario habilitar otros locales también. Si usted está funcionando en un sistema multi-usuario con usuarios que no hablan, por ejemplo, en_US, sus otros locales personales deben, del mismo modo, ser soportados en su sistema.

### Ejemplo ES Español

Primero descomente los locales siguientes en `/etc/locale.gen`:

```
es_ES.UTF-8 UTF-8

```

A continuación, actualice el sistema como root:

```
# locale-gen

```

## Configuración del locale de todo el sistema

Para definir la configuración regional de todo el sistema, establezca la variable `LANG` en `/etc/locale.conf`.

El contenido de `locale.conf` es una lista de líneas separadas que definen las variables del entorno: además de `LANG`, es compatible con todas las variables `LC_*`, con excepción de `LC_ALL`.

**Nota:** El archivo `/etc/locale.conf` no existe por defecto, hay que crearlo manualmente.

**Sugerencia:** Si la salida de `locale` durante la instalación es de su agrado, puede guardarla haciendo: `# locale | cat > /etc/locale.conf` mientras se encuentra en el entorno chroot.

 `/etc/locale.conf`  `LANG="es_ES.UTF-8"` 

He aquí un ejemplo de configuración avanzada:

 `/etc/locale.conf` 

```
# Habilitar UTF-8 con valores españoles.
LANG="es_ES.UTF-8"

# Mantener el orden predeterminado (por ejemplo, los archivos que comienzan con un '.' (punto)
# se mostrarán al principio en un listado del contenido del directorio).
LC_COLLATE="C"

# Establecer la fecha al formato DD-MM-YYYY  (comprobación con «date +%c»)
LC_TIME="es_ES.UTF-8"
```

Puede establecer la configuración regional («locale») por defecto en `locale.conf` o bien usando `localectl`, por ejemplo:

```
# localectl set-locale LANG="es_ES.UTF-8"

```

Consulte `man 1 localectl` y `man 5 locale.conf` para más detalles.

La configuración regional de todo el sistema estará completamente actualizada después de reiniciar y quedará establecida para las sesiones individuales iniciadas.

## Configuración de locales de reserva

En los programas que usan gettext para las traducciones comparadas, la opción `LANGUAGE` se añade además de las variables habituales. Esto permite a los usuarios especificar una [lista](http://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable) de locales que se utilizarán en ese orden. Si la traducción de la configuración regional preferida no está disponible, otra de un escenario similar se utilizará en lugar de la predeterminada. Por ejemplo, un usuario argentino puede desear recurrir a la ortografía española, en defecto de la argentina, antes que a la de Chile, por ejemplo:

 `~/.bashrc`  `export LANGUAGE="es_AR:es_ES:es"` 

o, para todo el sistema:

 `/etc/locale.conf` 

```
LANG="es_AR"
LANGUAGE="es_AR:es_ES:es"
```

## Configuración de locales de usuarios

Como mencionamos anteriormente, algunos usuarios podrían querer definir una configuración regional distinta a la definida de forma global para todo el sistema.

### Establecer la configuración regional en el archivo de inicio de la shell

Para ello, exporte la variable `LANG` con el local especificado al archivo `~/.bashrc`. Por ejemplo, para utilizar el locale `es_ES.UTF-8`:

```
export LANG=es_ES.UTF-8

```

Los locales se actualizarán la próxima vez que sea leído `~/.bashrc`. Puede actualizar, ya sea reiniciando sesión o de forma manual:

```
$ source ~/.bashrc

```

### Establecer la configuración regional en `.locale.conf`

El script `etc/profile.d/locale.sh` sobrescribe la configuración regional _para todo el sistema_ con la que se encuentra en `$HOME/.config/locale.conf`, si existe. Este archivo no existe de forma predeterminada, con lo que habrá que crearlo y poner la configuración regional del idioma deseado.

 `$HOME/.config/locale.conf` 

```
LANG="es_ES.UTF-8"
LANGUAGE="es_ES.UTF-8"

```

## Configuración de la intercalación

La intercalación, (colación o clasificación), es un poco diferente a lo anterior. La clasificación es un mecanismo torpe, dado que locales diferentes se comportan de modo diverso. Para evitar posibles problemas, Arch utiliza la configuración `LC_COLLATE="C"` en `/etc/profile`. Sin embargo, este método es considerado obsoleto. Para habilitar este comportamiento, solo tiene que añadir la siguiente variable a `/etc/locale.conf`:

```
LC_COLLATE="C"

```

Ahora, la orden `ls` mostrará primero los archivos que comienzan con un punto, luego los nombres de los archivos que comiencen con mayúsculas y, después, los que comiencen con minúsculas. Tenga en cuenta que sin una opción `LC_COLLATE`, las aplicaciones volverán a los valores especificados en `LC_ALL` o `LANG`, pero la configuración de `LC_COLLATE` se sobrescribirá si `LC_ALL` está definida. Si ésto crea problemas, asegúrese de que no se ha establecido ningún valor para LC_ALL añadiendo lo siguiente en el archivo `/etc/profile`:

```
export LC_ALL=

```

Tenga en cuenta que LC_ALL es la única variable LC que **no puede** ser configurada en `/etc/locale.conf`.

## Configuración del primer día de la semana

En muchos países, el primer día de la semana es el lunes. Para regular este comportamiento, cambie o agregue las líneas siguientes de la sección `LC_TIME` en `/usr/share/i18n/locales/<tus_locales> (por ejemplo, es_ES)`:

```
week            7;19971130;5
first_weekday   2
first_workday   2

```

Y a continuación, actualice el sistema:

```
 # locale-gen

```

## Solución de problemas

### Mi terminal no es compatible con UTF-8

Desafortunadamente, algunos terminales no son compatibles con UTF-8\. En este caso, usted tiene que utilizar un terminal diferente. Aquí tiene una lista con algunos terminales que tienen soporte para UTF-8:

*   vte-based terminals
*   gnustep-terminal
*   konsole
*   [mlterm](/index.php/Mlterm "Mlterm")
*   [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode")
*   [xterm](/index.php/Xterm "Xterm")

#### Xterm no es compatible con UTF-8

xterm solo es compatible con UTF-8 si lo ejecuta como `uxterm` o `xterm -u8`.

#### Gnome-terminal o rxvt-unicode no es compatible con UTF-8

Es necesario poner en marcha estas aplicaciones desde una localización UTF-8 o caerá el soporte UTF-8\. Activar el locale `en_US.UTF-8` (o su locale UTF-8 alternativo) como se explicó anteriormente, y establézcalo como el idioma por defecto, reiniciando, a continuación, el sistema.

## Véase también

*   [Guía de Gentoo Linux sobre localización](http://www.gentoo.org/doc/en/guide-localization.xml)
*   [Gentoo Wiki Archives: Locales](http://www.gentoo-wiki.info/Locales)
*   [Test interactivo ICU sobre la clasificación](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open Internationalisation Initiative](http://www.openi18n.org/)
*   [_The Single UNIX Specification_ definition of Locale](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) by The Open Group
*   [Locale environment variables](https://help.ubuntu.com/community/EnvironmentVariables#Locale_setting_variables)