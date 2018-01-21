[irssi](http://www.irssi.org) es un cliente IRC (*Internet Relay Chat*) modular cuya interfaz gráfica está basada en la biblioteca `ncurses`.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Instalando Scripts](#Instalando_Scripts)
*   [4 Enlaces Externos](#Enlaces_Externos)

## Instalación

irssi se encuentra disponible en los repositorios de Arch; simplemente ejecute, como *root*:

 `# pacman -S irssi` 

## Configuración

Puede configurarlo editando cualquiera de estos dos ficheros (vea la *man page*, [irssi(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/irssi.1), para más información):

*   `/etc/irssi.conf`
    Los cambios que realice en este fichero afectarán a todas las instancias de irssi.
*   `~/.irssi/config`
    Si por el contrario desea especificar opciones separadas para su usuario, edite este fichero. (Si el directorio no existe, irssi lo creará junto al fichero `config` al arrancar).

## Instalando Scripts

El ejemplo que sigue muestra cómo instalar el *script* para verificar la escritura (*spell checking*). En una terminal, ejecute:

```
# pacman -S ispell
$ mkdir -p ~/.irssi/scripts/autorun
$ cd ~/.irssi/scripts
$ wget [http://scripts.irssi.org/scripts/spell.pl http://scripts.irssi.org/scripts/spell.pl]
# perl -MCPAN -e 'install Lingua::Ispell'
$ irssi

```

**Nota:** Recuerde que los comandos marcados con el caracter **#** deberán ser ejecutados como *root*.

Si no desea utilizar CPAN, vea: [http://search.cpan.org/~jdporter/Lingua-Ispell-0.07/lib/Lingua/Ispell.pm](http://search.cpan.org/~jdporter/Lingua-Ispell-0.07/lib/Lingua/Ispell.pm)

Ahora, en irssi:

 `/script load spell.pl` 

Si funcionó, deberá aprecer algo como lo siguiente:

```
- - Irssi: Loaded script spell
/bind meta-s /_spellcheck

```

**Nota:** Podrá verificar la escritura de la línea actual utilizando la combinación **meta-s**, siendo *meta* normalmente *Alt*.

Si desea que el *script* se ejecute automáticamente al correr irssi, puede hacer lo siguiente:

```
$ cd ~/.irssi/scripts/autorun
$ ln -s ../ispell.pl .

```

## Enlaces Externos

*   [Puesta en marcha de irssi](http://linuxtidbits.wordpress.com/2008/01/09/setting-up-irssi/) (en inglés)
*   [Sitio oficial de irssi](http://www.irssi.org/) (en inglés)
*   [Guións de Irssi](http://scripts.irssi.org/) (en inglés)