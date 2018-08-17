**Estado de la traducción:** este artículo es una versión traducida de [Environment variables](/index.php/Environment_variables "Environment variables"). Fecha de la última traducción/revisión: **2017-12-22**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [del historial ver cambios](https://wiki.archlinux.org/index.php?title=Environment_variables&diff=0&oldid=ID).

Artículos relacionados

*   [Default applications](/index.php/Default_applications "Default applications")

Una variable de entorno es un objeto con nombre que contiene información usada por uno o más programas. En términos simples, es una variable con un nombre y un valor. El valor de una variable de entorno puede ser, por ejemplo, la ubicación de todos los archivos ejecutables, el editor por defecto, o las configuraciones regionales del sistema. Puede que esta forma de administrar configuraciones parezca difícil de manejar; sin embargo, las variables de entorno representan un mecanismo simple para compartir configuraciones entre múltiples aplicaciones y procesos en Linux.

## Contents

*   [1 Utilidades](#Utilidades)
*   [2 Cómo definir variables](#C.C3.B3mo_definir_variables)
    *   [2.1 Globalmente](#Globalmente)
    *   [2.2 Por usuario](#Por_usuario)
        *   [2.2.1 Aplicaciones gráficas](#Aplicaciones_gr.C3.A1ficas)
    *   [2.3 Por sesión](#Por_sesi.C3.B3n)
*   [3 Ejemplos](#Ejemplos)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Utilidades

El paquete [coreutils](https://www.archlinux.org/packages/?name=coreutils) contiene los programas *printenv* y *env*. Se pueden enlistar las variables de entorno actuales con:

```
$ printenv

```

**Note:** Algunas variables de entorno son específicas a un usuario. Esto se puede comprobar comparando la salida de *printenv* como usuario sin privilegios contra la salida como *root*.

La utilidad `env` puede ser usada para ejecutar un comando bajo un entorno modificado. El siguiente ejemplo ejecutará *xterm* con la variable de entorno `EDITOR` ajustada a `vim`. Esto no afectará a la variable de entorno global `EDITOR`.

```
$ env EDITOR=vim xterm

```

El comando *set*, de [Bash](/index.php/Bash "Bash"), permite cambiar los valores de las opciones de shell y colocar los parámetros posicionales, o mostrar los nombres y valores de las variables de shell. Para más información, se puede consultar la documentación de *set*: [[1]](http://www.gnu.org/software/bash/manual/bash.html#The-Set-Builtin).

Cada proceso almacena sus variables de entorno en el archivo `/proc/$PID/environ`, el cuál contiene cada par de nombre y valor delimitados por un carácter nulo (`\x0`). Se pude obtener un formato más legible con [sed](/index.php/Sed "Sed"), por ejemplo, `sed 's:\x0:
:g' /proc/$PID/environ`.

## Cómo definir variables

### Globalmente

La mayoría de las distribuciones de Linux permiten agregar o cambiar las definiciones de las variables de entorno en `/etc/profile`. Existen también archivos de configuración con variables de entorno específicas para algunos paquetes, como `/etc/locale.conf`. En principio, cualquier script de shell se puede usar para inicializar variables de entorno, pero siguiendo convenciones tradicionales de UNIX, estas declaraciones deben estar presentes en sólo algunos archivos particulares.

Los siguientes archivos deben ser usados para definir variables de entorno globales: `/etc/environment`, `/etc/profile` y archivos shell de configuración específicos. Cada uno de estos archivos tiene diferentes limitaciones, por lo que se debe seleccionar el adecuado de acuerdo a los propósitos de la variable.

*   `/etc/environment` es usado por el módulo pam_env y es independiente del lenguaje de shell, por lo que no se deben insertar scritps. Este archivo solamente acepta pares de la forma `*variable=valor*`. Para más detalles se pueden consultar los manuales [pam_env(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) o [pam_env.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5).

*   Los archivos de configuración global de [shell](/index.php/Shell "Shell") inicializan variables y ejecutan scripts. Por ejemplo [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") o [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").

*   `/etc/profile` inicializa variables para shells con login solamente. Este archivo sí permite scripts y puede ser usado por todos los shells compatibles con [Bash](https://en.wikipedia.org/wiki/Bourne_shell "wikipedia:Bourne shell").

En este ejemplo se agrega la carpeta `~/bin` al `PATH` para el usuario respectivo. Para hacer esto, solamente es necesario colocar lo siguiente en un archivo de configuración (`/etc/profile` o `/etc/bash.bashrc`):

```
# Si el ID del usuario es mayor o igual a 1000 y la carpeta ~/bin existe y
# aún no se encuentra definida en el $PATH,
# entonces se agrega ~/bin al $PATH.
if [[ $UID -ge 1000 && -d $HOME/bin && -z $(echo $PATH | grep -o $HOME/bin) ]]
then
    export PATH="${PATH}:$HOME/bin"
fi

```

### Por usuario

**Note:** El demonio dbus y la instancia de usuario de systemd no heredan ninguna de las variables de entorno definidas en lugares como `~/.bashrc`. Esto significa que, por ejemplo, programas activados por dbus, como los archivos de Gnome no las usarán por defecto. Consulte [Systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User").

No siempre se requiere definir una variable de entorno de manera global. Por ejemplo, se puede querer agregar `/home/my_user/bin` a la variable `PATH` pero sin querer que todos los demás usuarios lo tengan en su `PATH` también. Las variables de entorno locales se pueden definir en muchos archivos distintos:

*   `~/.pam_environment` es el archivo de usuario equivalente a `/etc/security/pam_env.conf` [[2]](https://github.com/linux-pam/linux-pam/issues/6), usado por el módulo pam_env. Detalles en [pam_env(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) y [pam_env.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5).

*   Archivos de configuración de usuario de [shell](/index.php/Shell "Shell"), por ejemplo [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") o [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").

*   `~/.profile` es usado por muchos shells como alternativa por defecto, [wikipedia:Unix shell#Configuration files](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files "wikipedia:Unix shell").

Para agregar una carpeta al `PATH` para uso local, se puede colocar lo siguiente en `~/.bash_profile`:

```
export PATH="${PATH}:/home/nombre_de_usuario/bin"

```

Para actualizar la variable es necesario volver a iniciar sesión o evaluar el archivo como un script: `$ source ~/.bash_profile`.

#### Aplicaciones gráficas

Para colocar variables de entorno para aplicaciones gráficas, se pueden colocar las variables en [xinitrc](/index.php/Xinitrc "Xinitrc") (o [xprofile](/index.php/Xprofile "Xprofile") cuando se utiliza un [administrador gráfico](/index.php/Display_manager "Display manager")), por ejemplo:

 `~/.xinitrc` 
```
export PATH="${PATH}:~/scripts"
export GUIVAR=value
```

### Por sesión

En algunas ocasiones se necesitan definiciones aún más estrictas. Se puede querer correr temporalmente ejecutables desde un directorio específico sin tener que escribir la ruta absoluta de cada uno, o editar el archivo de configuración de shell para el poco tiempo que se ocuparán.

En estos casos, se puede definir la variable `PATH` solamente en la sesión actual, usando el comando *export*. Mientras no se cierre la sesión, la variable `PATH` usará las configuraciones temporales. Para agregar una carpeta al `PATH` específico de una sesión se debe ejecutar:

```
$ export PATH="${PATH}:/home/nombre_de_usuario/tmp/usr/bin"

```

## Ejemplos

Esta sección enlista algunas variables de entorno comunes usadas por un sistema Linux y describe sus valores.

*   `DE` indica el entorno de escritorio que está siendo usado (por sus siglas en inglés, *D*esktop *E*nviroment). [xdg-open](/index.php/Xdg-open "Xdg-open") la usa para seleccionar las aplicaciones por defecto según el entorno. Para usar esta característica se necesitan instalar algunos paquetes adicionales: para [GNOME](/index.php/GNOME "GNOME"), [libgnome](https://aur.archlinux.org/packages/libgnome/); para [Xfce](/index.php/Xfce "Xfce"), [exo](https://www.archlinux.org/packages/?name=exo). Algunos valores comunes para la variable `DE` son: `gnome`, `kde`, `xfce`, `lxde` and `mate`.

	La variable de entorno `DE` necesita ser exportada antes de iniciar el administrador de ventanas. Por ejemplo:

 `~/.xinitrc` 
```
export DE="xfce"
exec openbox
```

	Esto hará que *xdg-open* use *exo-open* (el cuál es más amigable con el usuario) porque asume que está corriendo dentro de Xfce. Se puede utilizar *exo-preferred-applications* para configurar.

*   `PATH` contiene una lista, separada por dos puntos, de directorios en los que el sistema buscará archivos ejecutables. Cuando un comando normal (por ejemplo, *ls*, *rc-upadte* o *ic|emerge*) es interpretado por el shell (por ejemplo, *bash* o *zsh*), este busca un archivo ejecutable con el mismo nombre en los directorios del `PATH` y lo ejecuta. Para correr un ejecutable cuyo directorio no está enlistado en el `PATH`, se debe escribir la ruta completa: `/bin/ls`.

**Note:** Por razones de seguridad es recomendable no incluir el directorio actual (`.`) en el `PATH`: se puede conducir al usuario a ejecutar archivos malignos
.

*   `HOME` contiene la ruta del directorio del usuario actual. Esta variable puede ser usada por las aplicaciones para asociar archivos de configuración (entre otros) al usuario actual.

*   `PWD` contiene la ruta al directori actual.

*   `OLDPWD` contiene la ruta al directorio anterior al actual; esot es, el valor de `PWD` andes de ejecutar *cd*.

*   `SHELL` contiene la ruta al [shell del usuario](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap08.html#tag_08_03). Nótese que este no es necesariamente el mismo shell que se está ejecutando, aunque [Bash](/index.php/Bash "Bash") coloca esta variable al iniciar.

*   `TERM` contiene el tipo de terminal que se está ejecutando, por ejemplo, `xterm-256color`. Es usado por programas que se ejecutan en la terminal y que desean ocupar características específicas a cada tipo.

*   `PAGER` contiene el comando para correr el programa con el que se enlista el contenido de un archivo, por ejemplo, `/bin/less`.

*   `EDITOR` contiene el comando para ejecutar el editor ligero de archivos de texto. Por ejemplo, se puede escribir un cambio interactivo entre *gedit* bajo [X](/index.php/X "X") o *nano*:

```
export EDITOR="$(if [[ -n $DISPLAY ]]; then echo 'gedit'; else echo 'nano'; fi)"

```

*   `VISUAL` contiene el comando para ejecutar el editor de texto usado para tareas más demandantes, tal como editar correo (por ejemplo, `vi`, [vim](/index.php/Vim "Vim"), [emacs](/index.php/Emacs "Emacs") etcétera).

*   `MAIL` contiene la ubicación de los correos electrónicos de entrada. La configuración tradicional es `/var/spool/mail/$LOGNAME`.

*   `BROWSER` contiene la ruta al navegador web. Es útil establecerla en un archivo de configuración de shell de manera que cambie de manera dinámica según el entorno gráfico:

```
if [ -n "$DISPLAY" ]; then
    export BROWSER=firefox
else 
    export BROWSER=links
fi

```

*   `ftp_proxy` y `http_proxy` contienen servidores FTP y HTTP, respectivamente:

```
ftp_proxy="ftp://192.168.0.1:21"
http_proxy="http://192.168.0.1:80"

```

*   `MANPATH` contiene una lista separada por dos puntos con directorios en los cuales *man* busca páginas de manuales.

**Note:** En `/etc/profile` hay un comentario que dice «Man es mucho mejor que nosotros en averiguar esto», por lo que, generalmente, es mucho mejor dejar esta variable con su valor por defecto: `/usr/share/man:/usr/local/share/man`

*   `INFODIR` contiene una lista de directorios en los cuales el comando *info* busca páginas de información, por ejemplo, `/usr/share/info:/usr/local/share/info`.

*   `TZ` Se puede usar para colocar una zona horaria, distinta de la del sistema, a un usuario.. Las zonas enlistadas en `/usr/share/zoneinfo/` se pueden usar como referencia.

## Véase también

*   [Documentación de Gentoo](https://wiki.gentoo.org/wiki/Handbook:X86/Working/EnvVar)
*   [Documentación de Ubuntu](https://help.ubuntu.com/community/EnvironmentVariables)