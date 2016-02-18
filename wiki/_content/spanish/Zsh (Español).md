[Zsh](http://zsh.sourceforge.net/Intro/intro_1.html) es un potente intérprete de comandos que puede funcionar como shell interactiva y como intérprete de lenguaje de scripting. Aún siendo compatible con [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)") (no por defecto, solo si se ejecuta `emulate sh`), ofrece numerosas ventajas como:

*   Eficiencia
*   Completado de tabulador mejorado
*   Expansión de nombres de fichero mejorada
*   Manejo de arrays mejorado
*   Totalmente personalizable

El [FAQ de Zsh](http://zsh.sourceforge.net/FAQ/zshfaq01.html#l4) aporta más razones para usar Zsh.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Configuración Inicial](#Configuraci.C3.B3n_Inicial)
    *   [1.2 Hacer que Zsh sea la shell por defecto](#Hacer_que_Zsh_sea_la_shell_por_defecto)
*   [2 Archivos de configuración](#Archivos_de_configuraci.C3.B3n)
    *   [2.1 Archivos de configuración global](#Archivos_de_configuraci.C3.B3n_global)
*   [3 Configurar Zsh](#Configurar_Zsh)
    *   [3.1 Fichero .zshrc minimalista](#Fichero_.zshrc_minimalista)
    *   [3.2 Configurar el $PATH](#Configurar_el_.24PATH)
    *   [3.3 Autocompletado de comandos](#Autocompletado_de_comandos)
    *   [3.4 El gancho de "comando no encontrado"](#El_gancho_de_.22comando_no_encontrado.22)
    *   [3.5 Prevenir líneas duplicadas en el historial](#Prevenir_l.C3.ADneas_duplicadas_en_el_historial)
    *   [3.6 Asociaciones de teclas](#Asociaciones_de_teclas)
        *   [3.6.1 Asociar combinaciones de teclas con aplicaciones ncurses](#Asociar_combinaciones_de_teclas_con_aplicaciones_ncurses)
        *   [3.6.2 Otra forma de asociar una aplicación ncurses](#Otra_forma_de_asociar_una_aplicaci.C3.B3n_ncurses)
        *   [3.6.3 Asociaciones de teclas de gestor de archivos](#Asociaciones_de_teclas_de_gestor_de_archivos)
    *   [3.7 Búsqueda en el historial](#B.C3.BAsqueda_en_el_historial)
    *   [3.8 Prompts](#Prompts)
    *   [3.9 Personalizando el prompt](#Personalizando_el_prompt)
        *   [3.9.1 Colores](#Colores)
        *   [3.9.2 Ejemplo](#Ejemplo)
    *   [3.10 Dirstack](#Dirstack)
    *   [3.11 Comado de ayuda](#Comado_de_ayuda)
    *   [3.12 Resaltado de sintaxis estilo Fish](#Resaltado_de_sintaxis_estilo_Fish)
    *   [3.13 Archivos .zshrc de muestra](#Archivos_.zshrc_de_muestra)
    *   [3.14 Frameworks de configuración](#Frameworks_de_configuraci.C3.B3n)
    *   [3.15 Autoinicio de aplicaciones](#Autoinicio_de_aplicaciones)
    *   [3.16 Rehash persistente](#Rehash_persistente)
*   [4 Desinstalación](#Desinstalaci.C3.B3n)
*   [5 Vea también](#Vea_tambi.C3.A9n)

## Instalación

Antes de comenzar, puede que el usuario quiera comprobar cuál es la shell que está siendo usada:

```
$ echo $SHELL

```

[Instale](/index.php/Pacman_(Espa%C3%B1ol)#Instalar_paquetes "Pacman (Español)") el paquete [zsh](https://www.archlinux.org/packages/?name=zsh). Para definiciones de completado adicionales, instale también el paquete [zsh-completions](https://www.archlinux.org/packages/?name=zsh-completions).

### Configuración Inicial

Asegúrese de que Zsh ha sido instalado correctamente ejecutando lo siguiente en la terminal:

```
$ zsh

```

Debería ver **zsh-newuser-install**, que le dirigirá a través de la configuración básica. Si prefiere saltarse esto, presione `q`. Si no lo vió, puede invocarlo manualmente con:

```
$ zsh /usr/share/zsh/functions/Newuser/zsh-newuser-install -f

```

### Hacer que Zsh sea la shell por defecto

Véase [Command-line shell (Español)#Cambiando la shell por defecto](/index.php?title=Command-line_shell_(Espa%C3%B1ol)&action=edit&redlink=1 "Command-line shell (Español) (page does not exist)").

**Tip:** Si va a remplazar [bash](https://www.archlinux.org/packages/?name=bash), puede que quiera mover parte del código de `~/.bashrc` a `~/.zshrc` (p. ej: la definición del prompt y los [alias](/index.php/Bash_(Espa%C3%B1ol)#Los_alias "Bash (Español)")) y de `~/.bash_profile` a `~/.zprofile` (p. ej:Xinitrc (Español)

## Archivos de configuración

Al iniciar Zsh, Este cargará información de los siguiente archivos en el siguiente orden por defecto:

	`/etc/zsh/zshenv`

	Este archivo debería contener comandos para establecer la [ruta de búsqueda de comandos](#Configurar_el_.24PATH) global y otras variables de entorno a nivel de todo el sistema; no debería contener comandos que produzcan salidas por consola o que asuma que la shell está conectada a una tty.

	`~/.zshenv`

	Similar a `/etc/zsh/zshenv` pero dedicada exclusivamente a cada usuario. Se emplea normalmente para establecer variables de entorno que sean de utilidad.

	`/etc/zsh/zprofile`

	Este es un archivo de configuración global, Se cargará al iniciar la sesión. Usado por norma general para ejecutar algunos comandos generales en el inicio de sesión. Por favor, dése cuenta de que en Arch Linux, por defecto contiene [una linea](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) que carga `/etc/profile`, véase [abajo](#Archivos_de_configuraci.C3.B3n_global) para más detalles.

	`/etc/profile`

	Este archivo debería ser cargado por todas las shell Bourne-Compatibles al iniciar sesión: establece un entorno y configuraciones especificas de aplicación (`/etc/profile.d/*.sh`). Dése cuenta que en Arch Linux, Zsh también cargará esto por defecto.

	`~/.zprofile`

	Este se emplea generalmente para la ejecución automática de scripts de usuario al iniciar sesión.

	`/etc/zsh/zshrc`

	Archivo de configuración global, se cargará cuando se inicie una shell interactiva.

	`~/.zshrc`

	Archivo de configuración principal de usuario, se cargará cuando se inicie una shell interactiva.

	`/etc/zsh/zlogin`

	Archivo de configuración global, se cargará al finalizar el proceso de inicio de sesión en una shell de inicio de sesión.

	`~/.zlogin`

	Lo mismo que `/etc/zsh/zlogin` pero para cada usuario.

	`/etc/zsh/zlogout`

	Archivo de configuración global, se cargará cuando se cierra la sesión en la shell.

	`~/.zlogout`

	Lo mismo que `/etc/zsh/zlogout` pero para cada usuario.

**Nota:**

*   Las rutas usadas en el paquete [zsh](https://www.archlinux.org/packages/?name=zsh) de Arch son diferentes de las rutas por defecto usadas en las páginas del manual.
*   `/etc/profile` no forma parte de la lista normal de de ficheros para ejecutar en el arranque de Zsh, pero es cargado desde `/etc/zsh/zprofile` en el paquete [zsh](https://www.archlinux.org/packages/?name=zsh). Los usuarios deberían tener en cuenta que `/etc/profile` establece la variable `$PATH` que sobrescribirá cualquier otra variable `$PATH` establecida en `~/.zshenv`. Para prevenir esto, por favor, establezca la variable

```
`$PATH` en `~/.zshrc`. (No se recomienda reemplazar la [línea](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) por defecto en `/etc/zsh/zprofile` por otra cosa, ello romperá la integridad de otros paquetes que proporcionan algunos scripts en `/etc/profile.d`)

```

### Archivos de configuración global

Ocasionalmente, los usuarios pueden querer que algunas configuraciones se apliquen de forma global a todos los usuarios de Zsh. La página del manual zsh(1) dice que existen algunos archivos de configuración global, por ejemplo `/etc/zshrc`. Sin embargo, en Arch esto es ligeramente distinto, ya que ha sido compilado con flags pensadas de forma especificas para [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/zsh#n34) `/etc/zsh/` en su lugar.

Entonces, para configuraciones globales use `/etc/zsh/zshrc`, no `/etc/zshrc`. Lo mismo va para `/etc/zsh/zshenv`, `/etc/zsh/zlogin` y `/etc/zsh/zlogout`. Observe que estos archivos no se instalan por defecto, así que créelos si así lo desea.

Como única excepción tenemos a zprofile, use `/etc/profile` en su lugar.

## Configurar Zsh

Aunque Zsh es usable sin más, es seguro que no estará configurado al gusto de la mayoría de los usuarios, pero dado el gran espectro de posibles configuraciones disponibles para Zsh, configurar Zsh puede ser una experiencia abrumadora y que consuma gran cantidad de tiempo.

### Fichero .zshrc minimalista

Incluido más abajo se encuentra un archivo de configuración de muestra, proporciona un conjunto bastante bueno de opciones por defecto así como ejemplos de las muchas maneras en las que Zsh se puede personalizar. Para poder usar esta configuración guárdelo como un archivo que se llame `.zshrc`. Aplique los cambios sin necesidad de reiniciar la sesión ejecutando:

```
$ source ~/.zshrc

```

Este es un ejemplo de archivo `.zshrc`:

 `~/.zshrc` 
```
autoload -U compinit promptinit
compinit
promptinit

# Esto establecerá el prompt por defecto al tema walters
prompt walters
```

### Configurar el $PATH

Información de como establecer la ruta del sistema por cada usuario en zsh puede encontrarse aquí: [http://zsh.sourceforge.net/Guide/zshguide02.html#l24](http://zsh.sourceforge.net/Guide/zshguide02.html#l24)

En resumen, coloque lo siguiente en `~/.zshenv`:

 `~/.zshenv` 
```
typeset -U path
path=(~/bin /otras/cosas/en/la/ruta $path)
```

Véase también la nota en [#Archivos de configuración](#Archivos_de_configuraci.C3.B3n).

### Autocompletado de comandos

Quizás la característica más llamativa de Zsh es sus capacidades de autocompletado avanzadas. Como mínimo,active el autocompletado en `.zshrc`. Para habilitar el autocompletado, añada lo siguiente a su `~/.zshrc`:

 `~/.zshrc` 
```
autoload -U compinit
compinit

```

La configuración de arriba incluye autocompletado para ssh/scp/sftp pero para que esta característica funcione, los usuarios deben evitar que ssh haga hashing de los hostnames en `~/.ssh/known_hosts`.

**Advertencia:** Esto hace al ordenador vulnerable [ataques "Island-hopping"](http://blog.rootshell.be/2010/11/03/bruteforcing-ssh-known_hosts-files/). Con todo ello, comente la siguiente línea o establezca su valor a `no`: `/etc/ssh/ssh_config`  `#HashKnownHosts yes` 

Y mueva `~/.ssh/known_hosts` a otra parte de manera que ssh cree uno nuevo sin hostnames hasheados (evidentemente, los hosts conocidos anteriores se perderán). Para más información, vea el README de ssh para [hashed-hosts](http://nms.lcs.mit.edu/projects/ssh/README.hashed-hosts).

Para autocompletado mediante flechas de teclados, añada lo siguiente a:

 `~/.zshrc`  `zstyle ':completion:*' menu select` 

	*Para activar el menú, pulse tab dos veces.*

Para el autocompletado de parámetros de comandos en alias, añada lo siguiente a:

 `~/.zshrc`  `setopt completealiases` 

### El gancho de "comando no encontrado"

Vea [Pkgfile (Español)#Comando_no_encontrado](/index.php/Pkgfile_(Espa%C3%B1ol)#Comando_no_encontrado "Pkgfile (Español)").

### Prevenir líneas duplicadas en el historial

Para ignorar líneas duplicadas en el historial, use lo siguiente:

 `~/.zshrc`  `setopt HIST_IGNORE_DUPS` 

Para eliminar duplicadas existentes en el historial , ejecute:

```
$ awk -i inplace '!x[$0]++' ~/.zsh_history

```

### Asociaciones de teclas

Zsh no usa readline, en su lugar usa su propio y más potente zle. No lee `/etc/inputrc` o `~/.inputrc`. Zle tien un modo [emacs](/index.php/Emacs "Emacs") y un modo [vi](/index.php/Vi "Vi"). Por defecto, trata de adivinar el modo de la variable de entorno `$EDITOR`. Si esta vacía, usará emacs por defecto. Cambie esto con `bindkey -v` o `bindkey -e`.

Vea también [zshwiki: bindkeys](http://zshwiki.org/home/zle/bindkeys).

#### Asociar combinaciones de teclas con aplicaciones ncurses

Puede asociarse una aplicación ncurses a una combinación de teclas, pero no aceptará interacciones. Use la variable `BUFFER` para que funcione. El siguiente ejemplo permite a los usuarios abrir ncmpcpp usando `Alt+\`:

 `~/.zshrc` 
```
ncmpcppShow() { BUFFER="ncmpcpp"; zle accept-line; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

#### Otra forma de asociar una aplicación ncurses

Este método mantendrá todo lo que haya introducido en la línea antes de llamar a la aplicación

 `~/.zshrc` 
```
ncmpcppShow() { ncmpcpp <$TTY; zle redisplay; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

#### Asociaciones de teclas de gestor de archivos

Asociaciones de teclas al estilo de los gestores de archivos gráficos pueden ser muy útiles. El primero deja ir hacia atrás en el historial de directorios (`Alt+Left`), El segundo deja al usuario ir hacia el directorio padre (`Alt+Up`). Además de eso muestran el contenido del directorio.

 `~/.zshrc` 
```
cdUndoKey() {
  popd      > /dev/null
  zle       reset-prompt
  echo
  ls
  echo
}

cdParentKey() {
  pushd .. > /dev/null
  zle      reset-prompt
  echo
  ls
  echo
}

zle -N                 cdParentKey
zle -N                 cdUndoKey
bindkey '^[[1;3A'      cdParentKey
bindkey '^[[1;3D'      cdUndoKey

```

### Búsqueda en el historial

Añada estas líneas a .zshrc

 `~/.zshrc` 
```
[[ -n "${key[PageUp]}"   ]]  && bindkey  "${key[PageUp]}"    history-beginning-search-backward
[[ -n "${key[PageDown]}" ]]  && bindkey  "${key[PageDown]}"  history-beginning-search-forward

```

Haciendo esto, solo comandos anteriores que comiencen con la entrada actual se mostrarán.

### Prompts

Existe una forma rápida y fácil de establecer un prompt con colores en Zsh. Asegúrese que el prompt está establecido para autocargarse en `.zshrc`. Esto puede hacerse añadiendo las siguientes líneas:

 `~/.zshrc` 
```
autoload -U promptinit
promptinit

```

Prompts disponibles se pueden lista ejecutando el comando:

```
$ prompt -l

```

Por ejemplo, Para usar el prompt `walters`, introduzca:

```
$ prompt walters

```

Para previsualizar los temas disponibles, use el comando:

```
$ prompt -p

```

### Personalizando el prompt

Para usuarios no satisfechos con los prompts mencionados arriba (o que quieran expandir sus capacidades), Zsh ofrece la posibilidad de construir un prompt personalizado. Zsh soporta el tradicional prompt a la izquierda, así como un prompt a la derecha. Personalízelo usando `PROMPT=` con las siguiente variables:

Vea [Prompt Expansion](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html) para una lista completa de variables de prompt y subcadenas condicionales.

#### Colores

Zsh establece colores de manera diferente a [Bash](/index.php/Color_Bash_Prompt_(Espa%C3%B1ol) "Color Bash Prompt (Español)"). Añada `autoload -U colors && colors` antes de `PROMPT=` en `.zshrc` para usarlos. Normalmente querrá ponerlos dentro de `%{ [...] %}` de manera que el cursor no se mueva.

`$fg[color]` establecerá el color del texto (rojo, verde, azul, etc. - Si no encuentra el color introducido, volverá al formato anterior)

| Comando | Descripción |
| `%F{color} [...] %f` | tiene el mismo efecto que el anterior, sin tener que escribir tanto. Puede también añadir un número como prefijo a F en su lugar. |
| `$fg_no_bold[color]` | establece el texto al color sin negrita. |
| `$fg_bold[color]` | establece el texto al color con negrita. |
| `$reset_color` | resetea el color del texto al color por defecto. No resetea la negrita. usa `%b` to para resetear la negrita. Ahorra teclear si tan solo es `%f`. |
| `%K{color} [...] %k` | Establece el color de fondo. El mismo color que el color del texto sin negrita. Añadir un número de un solo dígito como prefijo hace que el fondo negro. |

| Posibles colores |
| `black` o `0` | `red` o `1` |
| `green` o `2` | `yellow` o `3` |
| `blue` o `4` | `magenta` o `5` |
| `cyan` o `6` | `white` o `7` |

**Nota:** El texto en negrita no usa necesariamente los mismo colores que el texto normal. Por ejemplo, `$fg['yellow']` parece marrón o un amarillo muy oscuro, mientras que `$fg_no_bold['yellow']` parece como un amarillo normal o brillante.

#### Ejemplo

Este es un ejemplo de un prompt de dos lados:

```
PROMPT="%{$fg[red]%}%n%{$reset_color%}@%{$fg[blue]%}%m %{$fg_no_bold[yellow]%}%1~ %{$reset_color%}%#"
RPROMPT="[%{$fg_no_bold[yellow]%}%?%{$reset_color%}]"

```

Y así es como se muestra:

```
username@host ~ %                                                         [0]

```

### Dirstack

Zsh puede configurarse para recordar los DIRSTACKSIZE últimos directorio visitados. Esto puede usarse para hacer *cd* a ellos rápidamente. Tiene que añadir algunas lineas a su archivo de configuración:

 `.zshrc` 
```
DIRSTACKFILE="$HOME/.cache/zsh/dirs"
if [[ -f $DIRSTACKFILE ]] && [[ $#dirstack -eq 0 ]]; then
  dirstack=( ${(f)"$(< $DIRSTACKFILE)"} )
  [[ -d $dirstack[1] ]] && cd $dirstack[1]
fi
chpwd() {
  print -l $PWD ${(u)dirstack} >$DIRSTACKFILE
}

DIRSTACKSIZE=20

setopt autopushd pushdsilent pushdtohome

## Elimina las entradas duplicadas
setopt pushdignoredups

## Esto revierte los operadores +/-.
setopt pushdminus

```

Ahora use

```
dirs -v

```

Para imprimir el dirstack. Use `cd -<NUM>` para volver a un directorio ya visitado. Use el autocompletado después del guión. Esto demuestra ser muy útil si se usa en conjunción con el menú de autocompletado.

### Comado de ayuda

Al contrario que [bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)"), *zsh* no habilita un comando de ayuda integrado `help`. Para usar `help` en zsh, añada lo siguiente a su archivo `zshrc`:

```
autoload -U run-help
autoload run-help-git
autoload run-help-svn
autoload run-help-svk
unalias run-help
alias help=run-help
```

### Resaltado de sintaxis estilo Fish

[Fish](/index.php/Fish "Fish") provee con un resalto de sintaxis para la shell muy potente. Para usarlo en fish, puede instalar [zsh-syntax-highlighting](https://www.archlinux.org/packages/?name=zsh-syntax-highlighting) desde los repositorios oficiales y añadir lo siguiente a su zshrc:

```
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

```

### Archivos .zshrc de muestra

*   Hay un paquete en los repositorios oficiales llamado [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) que viene de [http://grml.org/zsh](http://grml.org/zsh) y provee con un archivo zshrc que incluye un montón de ajustes para Zshell. Esta es la configuración por defecto para [los lanzamientos de ISOs mensuales](https://www.archlinux.org/download/).
*   Configuración básica, con prompt dinámico e información extra en el título de la ventana => [http://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc](http://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc);
*   [https://github.com/slashbeast/things/blob/master/configs/DOTzshrc](https://github.com/slashbeast/things/blob/master/configs/DOTzshrc) - zshrc con múltiples características, asegúrese de leer los comentarios. Características destacables: función de confirmación para asegurarse de que el usuario quiere realmente apagar, reiniciar o hibernar el ordenar, soporte para GIT en el prompt (hecho sin vcsinfo), completado de tabulador con menú, mostrar el comando ejecutado en la barra de título de la ventana y más.

### Frameworks de configuración

*   [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) es un framework popular, desarrollado por la comunidad para gestionar su configuración de zsh. Viene equipado con un montón de funciones útiles, helpers, plugins, temas.
*   [Prezto - Instantly Awesome Zsh](https://github.com/sorin-ionescu/prezto) (disponible en AUR como [prezto-git](https://aur.archlinux.org/packages/prezto-git/)) es un framework de configuración para Zsh. Viene con módulos, enriqueciendo el entorno de la interfaz de línea de comandos con valores por defecto seguros, alias, funciones, automcompletado, y temas para el prompt.
*   [Antigen](https://github.com/zsh-users/antigen) (disponible en AUR como [antigen-git](https://aur.archlinux.org/packages/antigen-git/)) - Un gestor de plugins para zsh, inspirado en oh-my-zsh y vundle.

### Autoinicio de aplicaciones

**Nota:** el valor por defecto de `$ZDOTDIR` es `$HOME`

Zsh siempre executa `/etc/zsh/zshenv` y `$ZDOTDIR/.zshenv` así que no cargue en exceso estos archivos.

Si la shell es una shell de inicio de sesión, los comandos son leídos desde `/etc/profile` y después desde `$ZDOTDIR/.zprofile`. Entonces, Si la shell es interactiva, los comando son leídos desde `/etc/zsh/zshrc` y luego desde `$ZDOTDIR/.zshrc`. Finalmente, si la shell es una shell de inicio de sesión, `/etc/zsh/zlogin` y `$ZDOTDIR/.zlogin` son leídos.

Vea tambiénla sección *STARTUP/SHUTDOWN FILES* de `man zsh`.

### Rehash persistente

Típicamente, compinit no encontrará de manera automática nuevos ejecutables en el $PATH. Por ejemplo, después de instalar un nuevo paquete, los ficheros en /usr/bin no sería inmediata o automáticamente incluidos en el autocompletado. Por lo tanto, tener estos nuevos ejecutables incluidos, uno ejecutaría:

```
$ rehash

```

Este 'rehash' puede establecerse para que se ejecute de forma automática. Simplemente incluyalo siguiente en su `zshrc`:

 `~/.zshrc`  `zstyle ':completion:*' rehash true` 
**Nota:** Este hack fue encontrado en un PR para Oh My Zsh [[2]](https://github.com/robbyrussell/oh-my-zsh/issues/3440)

## Desinstalación

Cambie la shell por defecto antes de eliminar el paquete [zsh](https://www.archlinux.org/packages/?name=zsh).

**Advertencia:** El fallo en seguir el procedimiento más abajo puede derivar en que el usuario no tengo acceso a una shell funcional.

Ejecute el siguiente comando:

```
$ chsh -s /bin/bash *user*

```

Úselo por cada usuario con *zsh* establecida como su shell de inicio de sesión (incluyendo root si fuera necesario). Una vez hecho, el paquete [zsh](https://www.archlinux.org/packages/?name=zsh) puede eliminarse.

Alternativamente, cambie la shell por defecto a Bash editando `/etc/passwd` como root.

**Advertencia:** Se recomienda encarecidamente usar `vipw` al editar `/etc/passwd` ya que ayuda a prevenir entradas invalidad y/o errores de sintaxis.

Por ejemplo, cambie lo siguiente:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/zsh

```

por esto:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/bash

```

## Vea también

*   [Guía de usuario para Zsh (Inglés)](http://zsh.sourceforge.net/Guide/zshguide.html)
*   [El manual de Z Shell](http://zsh.sourceforge.net/Doc/Release/index-frame.html) (diferentes formas disponibles [aquí (Inglés)](http://zsh.sourceforge.net/Doc/))
*   [FAQ Zsh (Inglés)](http://zsh.sourceforge.net/FAQ/zshfaq01.html)
*   [zsh-lovers(1)](http://grml.org/zsh/zsh-lovers.html) (Esto está disponible también como [zsh-lovers](https://www.archlinux.org/packages/?name=zsh-lovers) en los repositorios oficiales)
*   [Zsh Wiki (Inglés)](http://zshwiki.org/home/)
*   [Gentoo Wiki: Zsh/HOWTO (Inglés)](https://wiki.gentoo.org/wiki/Zsh/HOWTO)
*   [Bash2Zsh Tarjetas de referencia ( (Inglés))](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)