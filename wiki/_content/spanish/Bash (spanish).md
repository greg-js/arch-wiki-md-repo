**Estado de la traducción**
Este artículo es una traducción de [Bash](/index.php/Bash "Bash"), revisada por última vez el **2019-10-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Bash&diff=0&oldid=571526) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Bash/Funciones](/index.php/Bash/Functions_(Espa%C3%B1ol) "Bash/Functions (Español)")
*   [Bash/Personalización del indicador](/index.php/Bash/Prompt_customization_(Espa%C3%B1ol) "Bash/Prompt customization (Español)")
*   [Variables de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)")
*   [Readline](/index.php/Readline_(Espa%C3%B1ol) "Readline (Español)")
*   [Fortune](/index.php/Fortune "Fortune")
*   [Pkgfile](/index.php/Pkgfile_(Espa%C3%B1ol) "Pkgfile (Español)")
*   [Intérprete de línea de órdenes](/index.php/Command-line_shell_(Espa%C3%B1ol) "Command-line shell (Español)")

[Bash](https://www.gnu.org/software/bash/) (Bourne-again Shell) es un [intérprete de línea de órdenes](/index.php/Command-line_shell_(Espa%C3%B1ol) "Command-line shell (Español)")/lenguaje de programación por el [proyecto GNU](/index.php/GNU_Project_(Espa%C3%B1ol) "GNU Project (Español)"). Su nombre es un homenaje en referencia a su predecesor, el intérprete de línea de órdenes Bourne, que ha estado en desuso desde hace mucho tiempo. Bash se puede ejecutar en la mayoría de los sistemas operativos similares a UNIX, incluido GNU/Linux.

Bash es el intérprete de línea de órdenes predeterminado en Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Invocación](#Invocación)
    *   [1.1 Archivos de configuración](#Archivos_de_configuración)
    *   [1.2 Variables del intérprete de línea de órdenes y de entorno](#Variables_del_intérprete_de_línea_de_órdenes_y_de_entorno)
*   [2 Línea de órdenes](#Línea_de_órdenes)
    *   [2.1 Completar con tabulador](#Completar_con_tabulador)
        *   [2.1.1 Pulsación única del tabulador](#Pulsación_única_del_tabulador)
        *   [2.1.2 Órdenes comunes y opciones](#Órdenes_comunes_y_opciones)
        *   [2.1.3 Personalizar por órdenes](#Personalizar_por_órdenes)
    *   [2.2 Historial](#Historial)
        *   [2.2.1 Completado del historial](#Completado_del_historial)
        *   [2.2.2 Historial más corto](#Historial_más_corto)
        *   [2.2.3 Desactivar historial](#Desactivar_historial)
    *   [2.3 Imitación de la capacidad de ejecutar la ayuda como Zsh](#Imitación_de_la_capacidad_de_ejecutar_la_ayuda_como_Zsh)
*   [3 Alias](#Alias)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Personalización del indicador](#Personalización_del_indicador)
    *   [4.2 No se encontró la orden](#No_se_encontró_la_orden)
    *   [4.3 Desactivar Control+z en el terminal](#Desactivar_Control+z_en_el_terminal)
    *   [4.4 Borrar la pantalla después de cerrar la sesión](#Borrar_la_pantalla_después_de_cerrar_la_sesión)
    *   [4.5 Auto "cd" al introducir solo una ruta](#Auto_"cd"_al_introducir_solo_una_ruta)
    *   [4.6 Autojump](#Autojump)
    *   [4.7 Impedir la sobreescritura de archivos](#Impedir_la_sobreescritura_de_archivos)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 Ajuste de línea al redimensionar la ventana](#Ajuste_de_línea_al_redimensionar_la_ventana)
    *   [5.2 Intérprete de línea de órdenes sale incluso si ignoreeof está definido](#Intérprete_de_línea_de_órdenes_sale_incluso_si_ignoreeof_está_definido)
*   [6 Véase también](#Véase_también)
    *   [6.1 Tutoriales](#Tutoriales)
    *   [6.2 Comunidad](#Comunidad)
    *   [6.3 Ejemplos](#Ejemplos)

## Invocación

El comportamiento de Bash se puede alterar dependiendo de como se invoca. A continuación se describen distintos modos.

Si Bash es iniciado por `login` en un TTY, por un demonio [SSH](/index.php/SSH_(Espa%C3%B1ol) "SSH (Español)"), o por algo similar, se considera un **intérprete de línea de órdenes de inicio de sesión**. Este modo también se puede activar mediante la opción de línea de órdenes `-l`/`--login`.

Bash se considera un **intérprete de línea de órdenes interactivo** cuando su entrada estándar y de error están conectadas a un terminal (por ejemplo, cuando se ejecuta en un emulador de terminal), y no se inicia con la opción `-c` o con [argumentos no opcionales](http://unix.stackexchange.com/a/96805) (por ejemplo, `bash **script**`). Todos los intérpretes de línea de órdenes interactivos cargan `/etc/bash.bashrc` y `~/.bashrc`, mientras que los intérpretes de línea de órdenes interactivos de *inicio de sesion* también cargan `/etc/profile` y { {ic|~/.bash_profile}}.

**Nota:** En Arch `/bin/sh` (que solía ser el ejecutable del interprete de línea de órdenes Bourne) es un enlace simbólico a `/bin/bash`. Si Bash se invoca con el nombre `sh`, intenta imitar el comportamiento de inicio de las versiones históricas de `sh`, incluida la compatibilidad con POSIX.

### Archivos de configuración

Véase la sección "6.2 Archivos de inicio de Bash" en `/usr/share/doc/bash/bashref.html` ([enlace en línea](https://www.gnu.org/software/bash/manual/bash.html#Bash-Startup-Files)) y [GregsWiki:DotFiles](https://mywiki.wooledge.org/DotFiles "gregswiki:DotFiles") para una completa descripción.

| Archivo | Descripción | Intérprete de inicio de sesión  | Intérprete interactivo *sin inicio de sesión* |
| `/etc/profile` | [Carga](/index.php/Source_(Espa%C3%B1ol) "Source (Español)") las configuraciones de la aplicación en `/etc/profile.d/*.sh` y `/etc/bash.bashrc`. | Sí | No |
| `~/.bash_profile` | Por usuario, después de `/etc/profile`. Si este archivo no existe, `~/.bash_login` y `~/.profile` son comprobados en ese orden. El archivo de estructura `/etc/skel/.bash_profile` también carga `~/.bashrc`. | Sí | No |
| `~/.bash_logout` | Después de salir de un intérprete de línea de órdenes de incoo de sesión. | Sí | No |
| `/etc/bash.bashrc` | Depende de la opción de compilación `-DSYS_BASHRC="/etc/bash.bashrc"`. Carga `/usr/share/bash-completion/bash_completion`. | No | Sí |
| `~/.bashrc` | Por usuario, después de `/etc/bash.bashrc`. | No | Sí |

**Nota:**

*   Los intérpretes de línea de órdenes de inicio de sesión pueden ser no interactivos cuando se llaman con el argumento `--login`.
*   Mientras que los intérpretes de línea de órdenes interactivos que *no son de inicio de sesión* **no** cargan `~/.bash_profile`, aún heredan el entorno de su proceso principal (que puede ser un intérprete de línea de órdenes de inicio de sesión). Véase [sobre procesos, entornos y herencia](https://mywiki.wooledge.org/ProcessManagement#On_processes.2C_environments_and_inheritance "gregswiki:ProcessManagement") para obtener más información.

### Variables del intérprete de línea de órdenes y de entorno

El comportamiento de Bash y los programas ejecutados por él puede verse influido por una serie de variables de entorno. Las [variables de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") se utilizan para almacenar valores útiles, como los directorios de búsqueda de órdenes, o qué navegador utilizar. Cuando se inicia un nuevo intérprete de línea de órdenes o un script, hereda las variables de su padre (el proceso que lo lanza), por lo que comienza con un conjunto interno de variables del intérprete de línea de órdenes [[1]](http://www.kingcomputerservices.com/unix_101/understanding_unix_shells_and_environment_variables.htm).

Estas variables del intérprete de línea de órdenes en Bash se pueden exportar para convertirse en variables de entorno:

```
VARIABLE=contenido
export VARIABLE

```

o con un atajo

```
export VARIABLE=contenido

```

Las variables de entorno se colocan convencionalmente en `~/.profile` o `/etc/profile` para que otras intérpretes de línea de órdenes compatibles con Bourne puedan utilizarlas.

Véase [Variables de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") para más información en general.

## Línea de órdenes

La línea de órdenes Bash es administrada por la biblioteca separada llamada [Readline](/index.php/Readline_(Espa%C3%B1ol) "Readline (Español)"). Readline proporciona los estilos de accesos directos de [emacs](/index.php/Emacs_(Espa%C3%B1ol) "Emacs (Español)") y [vi](/index.php/Vi_(Espa%C3%B1ol) "Vi (Español)") para interactuar con la línea de órdenes, es decir, moverse hacia adelante y atrás en la base de palabras, eliminar palabras, etc. También es responsabilidad de Readline el administrar [historial](/index.php/Readline_(Espa%C3%B1ol)#Historial "Readline (Español)") de órdenes de entrada. Por último, pero no menos importante, le permite crear [macros](/index.php/Readline_(Espa%C3%B1ol)#Macros "Readline (Español)").

### Completar con tabulador

[Completar con tabulador](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") es la opción para completar automáticamente las órdenes escritas presionando `Tabulador` (habilitada de manera predeterminada).

**Nota:** **(del traductor):** `Tabulador` también es conocido como `Tab`.

#### Pulsación única del tabulador

Puede requerirse hasta tres pulsaciones de tabulador para mostrar todas las terminaciones posibles para una orden. Para reducir el número necesario de pulsaciones de tabulador, véase [Readline (Español)#Completado más rápido](/index.php/Readline_(Espa%C3%B1ol)#Completado_más_rápido "Readline (Español)").

#### Órdenes comunes y opciones

De forma predeterminada, Bash solo completa con tabulador órdenes, nombres de archivo y variables. El paquete [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) lo extiende añadiendo opciones de completado más especializadas para las órdenes comunes y sus opciones, que se pueden habilitar mediante la obtención de `/usr/share/bash-completed/bash_completion`. Con [bash-completion](https://www.archlinux.org/packages/?name=bash-completion), las opciones de completado normales (tales como `$ ls file.*<tab><tab>`) se comportarán de manera distinta; sin embargo, se pueden volver a habilitar con `$ compopt -o bashdefault *programa*` (véase [[2]](https://bbs.archlinux.org/viewtopic.php?id=128471) y [[3]](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html) para más detalles).

#### Personalizar por órdenes

**Nota:** El uso de la orden incorporada `complete` puede causar conflictos con [bash-completion](https://www.archlinux.org/packages/?name=bash-completion).

De forma predeterminada, Bash solo completa los nombres de archivo que siguen a una orden. Puede cambiarlo para completar los nombres de los comandos utilizando `complete -c`:

 `~/.bashrc` 
```
complete -c man which

```

o completar los nombres de las órdenes y los nombres de archivos con `-cf`:

 `complete -cf sudo` 

Véase la página del manual de Bash para más opciones de completado.

### Historial

#### Completado del historial

Puede enlazar las teclas de flecha arriba y abajo para buscar en el historial de Bash (véase: [Readline (Español)#Historial](/index.php/Readline_(Espa%C3%B1ol)#Historial "Readline (Español)") y [Sintaxis del archivo Init de Readline](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)):

 `~/.bashrc` 
```
 bind '"\e[A": history-search-backward'
 bind '"\e[B": history-search-forward'

```

o que afecte a todos los programas de readline:

 `~/.inputrc` 
```
"\e[A": history-search-backward
"\e[B": history-search-forward

```

#### Historial más corto

La variable `HISTCONTROL` puede evitar que ciertas órdenes se registren en el historial. Por ejemplo, para detener el registro de órdenes idénticas y repetidas

 `~/.bashrc`  `export HISTCONTROL=ignoredups` 

o configúrelo en `erasedups` para asegurarse de que el historial de Bash solo contenga una copia de cada orden (independientemente de su ordenación). Véase la página del manual de Bash para más opciones.

#### Desactivar historial

Para desactivar el historial de bash solo temporalmente:

```
set +o history

```

Las órdenes introducidas ​​ahora no se registrarán en `$HISTFILE`.

Por ejemplo, ahora puede convertir en hash contraseñas mediante `printf secret | sha256sum`, u oculta la utilización de GPG como `gpg -eaF secret-pubkey.asc` y su secreto no se escribirá en el disco.

Para activar el historial:

```
set -o history

```

**Sugerencia:** Si la variable `HISTCONTROL` contiene `ignorespace`, las órdenes que comiencen con un espacio no se guardarán en el archivo del historial. Véase [bash(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bash.1#Shell_Variables) para más detalles.

Para desactivar todo el historial de bash:

 `~/.bashrc or /etc/profile` 
```
export HISTSIZE=0

```

... y sólo para asegurarse:

```
# Advertencia: esto destruirá su antiguo archivo del historial para siempre
wipe -i -l2 -x4 -p4 "$HISTFILE"
ln -sv /dev/null "$HISTFILE"

```

### Imitación de la capacidad de ejecutar la ayuda como Zsh

[Zsh](/index.php/Zsh "Zsh") puede invocar el manual para la orden que precede al cursor presionando `Alt+h`. Un comportamiento similar se obtiene en Bash utilizando este enlace [Readline](/index.php/Readline_(Espa%C3%B1ol) "Readline (Español)"):

 `~/.bashrc` 
```
bind '"\eh": "\C-a\eb\ed\C-y\e#man \C-y\C-m\C-p\C-p\C-a\C-d\C-e"'

```

Esto asume que está utilizando el (predeterminado) [modo de edición](/index.php/Readline_(Espa%C3%B1ol)#Modo_de_edición "Readline (Español)") Emacs.

## Alias

[alias](https://en.wikipedia.org/wiki/es:Alias_(Unix) es una orden que permite reemplazar una palabra con otra cadena. A menudo se usa para abreviar una orden del sistema o para añadir argumentos predeterminados a una orden que se utiliza regularmente.

Los alias personales se almacenan preferiblemente en `~/.bashrc`, y los alias de todo el sistema (que afectan a todos los usuarios) pertenecen a `/etc/bash.bashrc`. Véase [[4]](https://gist.github.com/anonymous/a9055e30f97bd19645c2) para obtener ejemplos de alias.

Para las funciones, véase [Bash/Funciones](/index.php/Bash/Functions_(Espa%C3%B1ol) "Bash/Functions (Español)").

## Consejos y trucos

### Personalización del indicador

Véase [Bach/Personalización del indicador](/index.php/Bash/Prompt_customization_(Espa%C3%B1ol) "Bash/Prompt customization (Español)").

### No se encontró la orden

[pkgfile](/index.php/Pkgfile "Pkgfile") incluye un *hook* de "No se encontró la orden" que buscará automáticamente en los repositorios oficiales, al ingresar una orden no reconocida.

Necesita [cargar](/index.php/Source_(Espa%C3%B1ol) "Source (Español)") el *hook* para activarlo, por ejemplo:

 `~/.bashrc`  `source /usr/share/doc/pkgfile/command-not-found.bash` 

Luego, cuando intente ejecutar una orden que no esté disponible se mostrará la siguiente información:

 `$ abiword` 
```
abiword may be found in the following packages:
  extra/abiword 3.0.1-2	/usr/bin/abiword

```

**Nota:** Es posible que deba actualizarse la base de datos pkgfile antes de que esto funcione. Véase [pkgfile (Español)#Instalación](/index.php/Pkgfile_(Espa%C3%B1ol)#Instalación "Pkgfile (Español)") para más detalles.

Un *hook* alternativo a "No se encontró la orden" lo proporciona [command-not-found](https://aur.archlinux.org/packages/command-not-found/), que se ve así:

 `$ abiword` 
```
The command 'abiword' is provided by the following packages:
**abiword** (2.8.6-7) from extra
	[ abiword ]
**abiword** (2.8.6-7) from staging
	[ abiword ]
**abiword** (2.8.6-7) from testing
	[ abiword ]

```

### Desactivar Control+z en el terminal

Puede desactivar la función `Control+z` (detiene/cierra su aplicación) envolviendo su orden de la siguiente forma:

```
#!/bin/bash
trap "" 20
*adom*

```

Ahora, cuando presione accidentalmente `Control+z` en [adom](https://aur.archlinux.org/packages/adom/) en lugar de `Mayúsculas+z` no pasará nada porque se ignorará `Control+z`.

### Borrar la pantalla después de cerrar la sesión

Para borrar la pantalla después de cerrar la sesión en un terminal virtual:

 `~/.bash_logout` 
```
clear
reset

```

### Auto "cd" al introducir solo una ruta

Bash puede añadir automáticamente `cd` al introducir solo una ruta en el intérprete de línea de órdenes. Por ejemplo:

 `$ /etc` 
```
bash: /etc: Es un directorio

```

Pero después de añadir una línea al archivo `.bashrc`:

 `~/.bashrc` 
```
...
shopt -s autocd
...

```

Obtiene:

```
[user@host ~]$ /etc
cd /etc
[user@host etc]$

```

### Autojump

[autojump](https://www.archlinux.org/packages/?name=autojump) permite navegar por el sistema de archivos buscando cadenas en una base de datos con las rutas más visitadas del usuario.

Después de la instalación, `/etc/profile.d/autojump.bash` debe ser [cargado](/index.php/Source_(Espa%C3%B1ol) "Source (Español)") para comenzar a utilizar la aplicación.

### Impedir la sobreescritura de archivos

Para la sesión actual, para no permitir que los archivos regulares existentes se sobrescriban mediante la redirección de la salida del intérprete de línea de órdenes:

```
$ set -o noclobber

```

Esto es idéntico a `set -C`.

Para hacer los cambios persistentes para su usuario:

 `~/.bashrc` 
```
...
set -o noclobber
```

Para sobrescribir manualmente un archivo mientras `noclobber` está establecido:

```
$ echo "output" >| file.txt

```

## Solución de problemas

### Ajuste de línea al redimensionar la ventana

Al redimensionar un [emulador de terminal](/index.php/Terminal_emulator "Terminal emulator"), Bash puede no recibir la señal de redimensionamiento. Esto hará que el texto escrito no se ajuste correctamente y se superponga en el indicador. La opción `checkwinsize` del intérprete de línea de órdenes comprueba el tamaño de la ventana después de cada comando y, si es necesario, actualiza los valores de `LÍNEAS` y `COLUMNAS`.

 `~/.bashrc` 
```
shopt -s checkwinsize

```

### Intérprete de línea de órdenes sale incluso si ignoreeof está definido

Si ha configurado la opción `ignoreeof` y se encuentra que al presionar repetidamente `ctrl-d` hace que se cierre el intérprete de línea de órdenes, es porque esta opción solo permite 10 invocaciones consecutivas de esta combinación de teclas (o 10 caracteres EOF consecutivos, para ser precisos), antes de salir del intérprete de línea de órdenes.

Para permitir valores más altos, tiene que utilizar la variable IGNOREEOF.

Por ejemplo:

```
export IGNOREEOF=100

```

## Véase también

*   [Wikipedia:es:Bash](https://en.wikipedia.org/wiki/es:Bash "wikipedia:es:Bash")
*   [Manual de referencia de Bash](https://www.gnu.org/software/bash/manual/bashref.html), o `/usr/share/doc/bash/bashref.html`
*   [Sintaxis del archivo Init de Readline](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)
*   [El intérprete de línea de órdenes Bourne-Again](http://www.aosabook.org/en/bash.html) - El capitulo tercero de *La arquitectura de las aplicaciones de código abierto*
*   [Shellcheck](http://shellcheck.net) - Compruebe los scripts de bash en busca de errores comunes (basado en [shellcheck](https://github.com/koalaman/shellcheck))
*   [PS1 generator](http://bashrcgenerator.com/) - genera su indicador de bash en .bashrc/PS1 con una interfaz de arrastrar y soltar
*   [Órdenes aún más útiles en .bashrc](https://serverfault.com/questions/3743/what-useful-things-can-one-add-to-ones-bashrc)

### Tutoriales

*   [Wiki de Greg](https://mywiki.wooledge.org/ "gregswiki:")
*   [GregsWiki:BashGuide](https://mywiki.wooledge.org/BashGuide "gregswiki:BashGuide")
*   [GregsWiki:BashFAQ](https://mywiki.wooledge.org/BashFAQ "gregswiki:BashFAQ")
*   [Wiki para Hackers de Bash](http://wiki.bash-hackers.org/doku.php)
*   [Wiki para Hackers de Bash: Lista de tutoriales en línea de Bash](http://wiki.bash-hackers.org/scripting/tutoriallist)
*   [Quote Tutorial](http://www.grymoire.com/Unix/Quote.html)

### Comunidad

*   [Un canal de IRC activo y amistoso para Bash](ircs://chat.freenode.net#bash)

### Ejemplos

*   [Cómo cambiar el título de un xterm](http://tldp.org/HOWTO/Xterm-Title-4.html)