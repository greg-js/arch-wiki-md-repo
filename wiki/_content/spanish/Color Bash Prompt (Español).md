Existe una gran variedad de posibilidades para mejorar el indicador de bash y personalizandolo ayudara a ser más productivo en la linea de comandos. Se puede agregar información adicional al indicador, o simplemente colorearlo para hacer el indicador más atractivo.

## Contents

*   [1 Indicadores Basicos](#Indicadores_Basicos)
*   [2 Distinguir Indicadores de root y otros usuarios](#Distinguir_Indicadores_de_root_y_otros_usuarios)
*   [3 Más personalizaciones para el indicador de Bash](#M.C3.A1s_personalizaciones_para_el_indicador_de_Bash)
*   [4 Indicadores Avanzados](#Indicadores_Avanzados)
    *   [4.1 Wolfman](#Wolfman)
*   [5 External Resources](#External_Resources)

## Indicadores Basicos

Las siguientes configuraciones son útiles para distinguir el indicador de root de otros usuarios sin privilegios:

*   Edita el archivo de configuración personal de Bash:

```
$ nano ~/.bashrc

```

*   Commenta el indicador por defecto:

```
#PS1='[\u@\h \W]\$ '

```

*   Agrega el siguiente indicador verde para usuarios comunes:

 `[chiri@zetsubou ~]$ _` 

```
PS1='\[\e[1;32m\][\u@\h \W]\$\[\e[0m\] '

```

*   Edita el archivo .bashrc del root; copialo desde /etc/skel si no existe aún:

```
# nano /root/.bashrc

```

*   Asigna un indicador rojo para root:

 `[root@zetsubou ~]# _` 

```
PS1='\[\e[1;31m\][\u@\h \W]\$\[\e[0m\] '

```

## Distinguir Indicadores de root y otros usuarios

Utilizar el archivo `~/.bashrc`; uno del usuario root, y uno para usuarios normales:

```
vim ~/.bashrc

```

Comentar el PS1 inicial:

```
#PS1='[\u@\h \W]\$ '

```

Utilizar el siguiente indicador como usuario normal:

```
PS1='\[\e[0;32m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[1;32m\]\$\[\e[m\]\[\e[1;37m\] '

```

Este indicador tiene las caracteristicas de que el nombre de usuario esta en verde, el directorio de trabajo en azul claro, un indicador $ en verde claro y la escritura de texto en blanco.

Editar el indicador del usuario root:

```
sudo vim /root/.bashrc

```

Comentar el PS1 inicial:

```
#PS1='[\u@\h \W]\$ '

```

Utilizar el siguiente indicador como usuario root:

```
PS1='\[\e[0;31m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[0;31m\]\$\[\e[m\]\[\e[0;32m\] '

```

Este indicador tiene las caracteristicas de que el nombre 'root' esta en rojo, el directorio de trabajo en azul claro, un indicador # en rojo y la escritura de texto en un horrible, tipo matrix, verde. ;)

Esta es la lista de algunos códigos de color para bash:

```
Negro       0;30     Gris Obscuro  1;30
Azul        0;34     Azul Claro    1;34
Verde       0;32     Verde Claro   1;32
Cyan        0;36     Cyan Claro    1;36
Rojo        0;31     Rojo Claro    1;31
Purpura     0;35     Fiuscha       1;35
Café        0;33     Amarillo      1;33
Gris Claro  0;37     Blanco        1;37

```

Reemplazar el digito 0 con 1 para obtener la versión del color claro, experimenta a tu gusto, y revisa el extracto de las páginas del manual de bash a continuación para además personalizar los carácteres especiales de escape.

**Consejo**:

```
\[     comienza un secuencia de carácteres no imprimibles
\]     termina un secuencia de carácteres no imprimibles

```

## Más personalizaciones para el indicador de Bash

*   Editar el archivo `~/.bashrc` comentando el indicador inicial de Arch:

```
# PS1='[\u@\h \W]\$ '

```

*   Agrega las siguientes entradas en el archivo `~/.bashrc`

```
BLUE=`tput setf 1`
GREEN=`tput setf 2`
CYAN=`tput setf 3`
RED=`tput setf 4`
MAGENTA=`tput setf 5`
YELLOW=`tput setf 6`
WHITE=`tput setf 7`
PS1='\[$GREEN\]\u@\h \[$BLUE\]\w/\[$GREEN\] \$\[$WHITE\] '

```

Los carácteres `\[` y `\]` son necesarios para evitar problemas con saltos de linea en la terminal.

Para recargar el ambiente hacer:

```
source ~/.bashrc

```

También puede ser deseable editar el archivo `/root/.bashrc` con un conjunto de entradas similares, usando RED para distiguir al usuario en la opción `\u`.

Diferentes opciones pueden ser personalizadas con la secuencia de escape de la forma `\x` (extraidas de las páginas del manual de bash):

```
     Bash permite agregar estas cadenas al indicador mediante la inserción de _caracteres especiales escapados con diagonal invertida_ que se decodifican como sigue:

```

```
            \a     carácter de campana ASCII (07)
            \d     la fecha en formato día mes día (p.ej., "mié jul 02")
            \D{format}
                   el formato es proporcionado a strftime(3) y el resultado es insertado en la cadena dle indicador; un formato vacío
                   resulta en una representación de fecha especifica local. Las llaves son requeridas.
            \e     caracter de escape ASCII (033)
            \h     el nombre del host hasta el primer `.'
            \H     el nombre del la máquina completo (FQDN)
            \j     el número de trabajos actualmente gestionados por el interprete
            \l     el nombre base del dispositivo de terminal del interprete
            \n     carácter de nueva línea
            \r     retorno de carro
            \s     el nombre del interprete, el nombre base de $0 (el fragmento que sigue a la última diagonal)
            \t     la hora actual en formato 24-horas HH:MM:SS
            \T     la hora actual en formato 12-horas HH:MM:SS
            \@     la hora actual en formato 12-horas AM/PM
            \A     la hora actual en formato 24-houras HH:MM
            \u     el nombre del usuario actual
            \v     la versión del pquete bash (p.ej., 2.00)
            \V     la versión del paquete bash + el nivel de parche (p.ej., 2.00.0)
            \w     el directorio actual de trabajo, con el directorio $HOME abreviado con una tilde
            \W     el nombre base del directorio actual de trabajo, con el directorio $HOME abreviado con una tilde
            \!     el número del comando actual en el histórico
            \#     el número de comando del comando actual
            \$     si el UID efectivo es 0, un #; en otro caso, $
            \nnn   el caracter correspondiente al número en octal nnn
            \\     una diagonal invertida
            \[     inicio de una secuencia de caracteres no imprimibles que pueden usarse para ingresar una secuencia de control
                   en el indicador de la terminal
            \]     fin de una secuencia de carácteres no imprimibles

```

```
     El número de comando y el número histórico son generalmente diferentes: el número histórico de un comando es su posición  en  la
     lista del historil, el cual puede incluir comandos restaurados desde el archivo histórico (ver HISTORY a continuación), mientras
     que el número de comando es la posición en la secuencia de comandos ejecutadas durante la sesión actual del interprete.  Después
     ls cadena es decodificada, esto es expandida mediante la expansión de parametros, substitucion de comandos, expansion aritmetica
     y eliminacion de comillas, sujeto al valor de las opciones de variables del indicador del  interprete  (ver  la  descripción del
     comando shopt en SHELL BUILTIN COMMANDS a continuación=.

```

## Indicadores Avanzados

### Wolfman

After reading through most of the [Bash Prompt Howto](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/index.html), I developed a color bash prompt that displays the last 25 characters of the current working directory. This prompt should work well on terminals with a black background. The following code goes in your home directory's `.bashrc` file.

*   Comment out Arch's default prompt.

```
# PS1='[\u@\h \W]\$ '

```

*   Next add the bash_prompt_command function. If you have a couple directories with long names or start entering a lot of subdirectories, this function will keep the command prompt from wrapping around the screen by displaying at most the last pwdmaxlen characters from the PWD. This code was taken from the Bash Prompt Howto's section on [Controlling the Size and Appearance of $PWD](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x783.html) and modified to replace the user's home directory with a tilde.

```
##################################################
# Fancy PWD display function
##################################################
# The home directory (HOME) is replaced with a ~
# The last pwdmaxlen characters of the PWD are displayed
# Leading partial directory names are striped off
# /home/me/stuff          -> ~/stuff               if USER=me
# /usr/share/big_dir_name -> ../share/big_dir_name if pwdmaxlen=20
##################################################
bash_prompt_command() {
    # How many characters of the $PWD should be kept
    local pwdmaxlen=25
    # Indicate that there has been dir truncation
    local trunc_symbol=".."
    local dir=${PWD##*/}
    pwdmaxlen=$(( ( pwdmaxlen < ${#dir} ) ? ${#dir} : pwdmaxlen ))
    NEW_PWD=${PWD/#$HOME/\~}
    local pwdoffset=$(( ${#NEW_PWD} - pwdmaxlen ))
    if [ ${pwdoffset} -gt "0" ]
    then
        NEW_PWD=${NEW_PWD:$pwdoffset:$pwdmaxlen}
        NEW_PWD=${trunc_symbol}/${NEW_PWD#*/}
    fi
}

```

*   This code generates the command prompt. There's not much to this. A bunch of colors are defined. The user's color for the username, hostname, and prompt ($ or #) is set to cyan, and if the user is root (root's UID is always 0), set the color to red. The command prompt is set to a colored version of Arch's default with the NEW_PWD from the last function.
*   Also, make sure that your color variables are enclosed in double and not single quote marks. Using single quote marks seems to give bash problems with line wrapping correctly.

```
bash_prompt() {
    case $TERM in
     xterm*|rxvt*)
         local TITLEBAR='\[\033]0;\u:${NEW_PWD}\007\]'
          ;;
     *)
         local TITLEBAR=""
          ;;
    esac
    local NONE="\[\033[0m\]"    # unsets color to term's fg color

    # regular colors
    local K="\[\033[0;30m\]"    # black
    local R="\[\033[0;31m\]"    # red
    local G="\[\033[0;32m\]"    # green
    local Y="\[\033[0;33m\]"    # yellow
    local B="\[\033[0;34m\]"    # blue
    local M="\[\033[0;35m\]"    # magenta
    local C="\[\033[0;36m\]"    # cyan
    local W="\[\033[0;37m\]"    # white

    # emphasized (bolded) colors
    local EMK="\[\033[1;30m\]"
    local EMR="\[\033[1;31m\]"
    local EMG="\[\033[1;32m\]"
    local EMY="\[\033[1;33m\]"
    local EMB="\[\033[1;34m\]"
    local EMM="\[\033[1;35m\]"
    local EMC="\[\033[1;36m\]"
    local EMW="\[\033[1;37m\]"

    # background colors
    local BGK="\[\033[40m\]"
    local BGR="\[\033[41m\]"
    local BGG="\[\033[42m\]"
    local BGY="\[\033[43m\]"
    local BGB="\[\033[44m\]"
    local BGM="\[\033[45m\]"
    local BGC="\[\033[46m\]"
    local BGW="\[\033[47m\]"

    local UC=$W                 # user's color
    [ $UID -eq "0" ] && UC=$R   # root's color

    PS1="$TITLEBAR ${EMK}[${UC}\u${EMK}@${UC}\h ${EMB}\${NEW_PWD}${EMK}]${UC}\\$ ${NONE}"
    # without colors: PS1="[\u@\h \${NEW_PWD}]\\$ "
    # extra backslash in front of \$ to make bash colorize the prompt
}

```

*   Finally, append this code. This ensures that the NEW_PWD variable will be updated when you cd somewhere else, and it sets the PS1 variable, which contains the command prompt.

```
PROMPT_COMMAND=bash_prompt_command
bash_prompt
unset bash_prompt

```

*   If you want to play around with the colors of this prompt, open your `.bashrc` file in a text editor. When you want to see what the new prompt looks like, enter the following from your home directory, and the prompt will immediately change.

```
$ source ~/.bashrc

```

## External Resources

*   Forum Discussion here: [https://bbs.archlinux.org/viewtopic.php?t=1817](https://bbs.archlinux.org/viewtopic.php?t=1817)
*   [http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)
*   [http://www.shelluser.net/~giles/bashprompt/prompts/index.html](http://www.shelluser.net/~giles/bashprompt/prompts/index.html)