Un lugar para que los usuarios de Arch pongan sus consejos y trucos sobre el archivo `.bashrc`

## Contents

*   [1 PS1](#PS1)
*   [2 Los alias](#Los_alias)
    *   [2.1 Cambiar el uso por defecto de distintas órdenes](#Cambiar_el_uso_por_defecto_de_distintas_.C3.B3rdenes)
    *   [2.2 Atajos](#Atajos)
*   [3 Variables de entorno útiles](#Variables_de_entorno_.C3.BAtiles)
*   [4 Funciones/Guiones](#Funciones.2FGuiones)
*   [5 inputrc](#inputrc)

## PS1

Para colorear el indicador de bash: Comente la variable PS1 por defecto:

```
#PS1='[\u@\h \W]\$ '

```

La siguiente PS1 es útil para un indicador bash de root, con designación en rojo y texto verde en consola:

```
PS1='\[\e[0;31m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[0;31m\]\$ \[\e[m\]\[\e[0;32m\] '

```

Vea también [esta página de la wiki](/index.php/Colorear_Indicador_Bash_(Espa%C3%B1ol) "Colorear Indicador Bash (Español)")

## Los alias

### Cambiar el uso por defecto de distintas órdenes

Para hacer que bash nos indique que va a eliminar archivos

```
alias rm='rm -i'

```

Para que no importen determinados errores de tecleado

```
alias unmount='umount'
alias pakman='pacman'

```

(Visto en foros) Para obligar a la gente a aprender vim

```
alias nano='vi'

```

### Atajos

## Variables de entorno útiles

Establecer un editor de texto por defecto

```
EDITOR=nano
EDITOR=vi

```

## Funciones/Guiones

## inputrc