Related articles

*   [Default applications](/index.php/Default_applications "Default applications")

**Estado de la traducción:** este artículo es una versión traducida de [Environment variables](/index.php/Environment_variables "Environment variables"). Fecha de la última traducción/revisión: **22/12/17**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [del historial ver cambios](https://wiki.archlinux.org/index.php?title=Environment_variables&diff=0&oldid=ID).

Una variable de entorno es un objeto con nombre que contiene información usada por uno o más programas. En términos simples, es una variable con un nombre y un valor. El valor de una variable de entorno puede ser, por ejemplo, la ubicación de todos los archivos ejecutables, el editor por defecto, o las configuraciones regionales del sistema. Puede que esta forma de administrar configuraciones parezca difícil de manejar; sin embargo, las variables de entorno representan un mecanismo simple para compartir configuraciones entre múltiples aplicaciones y procesos en Linux.

## Contents

*   [1 Utilidades](#Utilidades)
*   [2 Cómo definir variables](#C.C3.B3mo_definir_variables)
    *   [2.1 Globalmente](#Globalmente)
    *   [2.2 Por usuario](#Por_usuario)
        *   [2.2.1 Aplicaciones gráficas](#Aplicaciones_gr.C3.A1ficas)
    *   [2.3 Por sesión](#Por_sesi.C3.B3n)
*   [3 Véase también](#V.C3.A9ase_tambi.C3.A9n)

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

*   `/etc/environment` es usado por el módulo pam_env y es independiente del lenguaje de shell, por lo que no se deben insertar scritps. Este archivo solamente acepta pares de la forma `*variable=valor*`. Para más detalles se pueden consultar los manuales [pam_env(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) o [pam_env.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5).

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

*   `~/.pam_environment` es el archivo de usuario equivalente a `/etc/security/pam_env.conf` [[2]](https://github.com/linux-pam/linux-pam/issues/6), usado por el módulo pam_env. Detalles en [pam_env(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) y [pam_env.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5).

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

## Véase también

*   [Documentación de Gentoo](https://wiki.gentoo.org/wiki/Handbook:X86/Working/EnvVar)
*   [Documentación de Ubuntu](https://help.ubuntu.com/community/EnvironmentVariables)