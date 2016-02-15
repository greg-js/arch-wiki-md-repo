## Contents

*   [1 Cómo restaurar la base de datos local de Pacman](#C.C3.B3mo_restaurar_la_base_de_datos_local_de_Pacman)
    *   [1.1 Introducción](#Introducci.C3.B3n)
        *   [1.1.1 Ausencia de responsabilidad](#Ausencia_de_responsabilidad)
        *   [1.1.2 Línea de órdenes](#L.C3.ADnea_de_.C3.B3rdenes)
    *   [1.2 Instrucciones](#Instrucciones)
*   [2 Coloreando la salida de pacman](#Coloreando_la_salida_de_pacman)
    *   [2.1 Scripts](#Scripts)
    *   [2.2 Alternativas](#Alternativas)
    *   [2.3 Usando 'acoc'](#Usando_.27acoc.27)
    *   [2.4 Links](#Links)
    *   [2.5 Alternativa](#Alternativa)

## Cómo restaurar la base de datos local de Pacman

### Introducción

Algo ha ido mal con pacman. 'Pacman -Q' no da resultados en absoluto, y 'pacman -Syu' le dice que sus sistema está actualizado, pero usted sabe que no es así. Cuando intenta instalar un paquete usando 'pacman -S package', se le presenta una lista de dependencias, aunque usted sepa positivamente que ya están todas ellas instaladas.

Su problema es que la base de datos de software instalado de pacman, '/var/lib/pacman/local' se ha corrompido o borrado. Este es un problema serio, pero afortunadamente puede restaurar '/var/lib/pacman/local' siguiendo las instrucciones que se indican a continuación.

#### Ausencia de responsabilidad

Antes de comenzar, quiero recalcar que aunque estas instrucciones me funcionaron a mí, puede que no funcionen para usted. De hecho, sus sistema podría no volver a ser el mismo nunca más.

PROCEDA ASUMIENDO EL RIESGO!

#### Línea de órdenes

La línea a continuación indica una orden tecleada por el usuario 'me' en un terminal, esto es, cualquier usuario excepto root.

```
[me@linuxbox]$ ls

```

La línea a continuación indica una orden tecleada en un terminal por el usuario 'root', esto es, el usuario con todos los derechos en su sistema.

```
[root@linuxbox]# ls

```

La mayoría de las instrucciones descritas a continuación suponen que tiene usted acceso como root a su sistema.

### Instrucciones

*   En primer lugar, tiene que asegurarse de que tiene el archivo de anotaciones de pacman.

```
[me@linuxbox]$ ls /var/log/pacman.log
/var/log/pacman.log

```

Si no existe su archivo de anotaciones de pacman, NO debe continuar. La única opción que tiene es reinstalar su sistema desde cero.

De acuerdo, su archivo '/var/log/pacman.log' existe. ¿Va a continuar?

*   cree el archivo 'pkglist.sh'.

```
[root@linuxbox]# touch pkglist.sh

```

*   Copie y pegue las líneas siguientes en su archivo 'pkglist.sh'.

```
#!/bin/bash
#
SEDEXP='s/^\[[^ ]* *[0-9][0-9]:[0-9][0-9]\] \([^ ]*\) *\([^ ]*\) .*/\1 \2/'
GRPEXP='(upgraded)|(installed)'
AWKEXP='{print $2}'
#
sed -e "$SEDEXP" /var/log/pacman.log | grep -E "$GRPEXP" | awk "$AWKEXP" | sort -u
# End

```

Gracias a 'rdt' [https://bbs.archlinux.org/viewtopic.php?id=38531](https://bbs.archlinux.org/viewtopic.php?id=38531)

grabe y salga.

*   Haga al archivo 'pkglist.sh' ejecutable.

```
[root@linuxbox]# chmod 744 pkglist.sh

```

*   Ahora ejecute 'pklglist.sh' y redireccione la salida a 'pkglist'.

```
[root@linuxbox]# ./pkglist.sh > pkglist

```

*   'pkglist' conendrá ahora una lista de todo el software que instaló o actualizó. Edite 'pkglist' y elimine todo lo que no quiera reinstalar. Usted podría querer hacer esto si por ejemplo constryó un paquete personalizado y lo instaló con 'abs'.

```
[root@linuxbox]# vi pkglist

```

*   Una vez esté satisfecho con el contenido de 'pkglist', puede utilizarlo para reinstalar su software, y restaurar '/var/lib/pacman/local'.

No hay ninguna necesidad de comprobar las dependencias, y tiene que 'forzar' la instalación dado que los programas ya existen.

```
[root@linuxbox]# pacman -Sdf `cat pkglist`

```

Pacman le presentará ahora una larga lista de software que va a ser instalado. Diga 'yes' y espere a que termine pacman.

*   Finalmente, necesitará descubrir todos los archivos de configuración que han cambiado. Puede hacer esto actualizando primero la base de datos 'locate'.

```
[root@linuxbox]# updatedb

```

*   Ahora puede buscar todos los archivos de configuración que hayan cambiado.

```
[root@linuxbox]# locate pacorig

```

Esto le dará una lista de todos los archivos de configuración que han sido reemplazados. Su archivo original tendrá la extensión '.pacorig'. Borre los nuevos archivos, y renombre los archivos '.pacorig' para restaurar su configuración inicial para cada paquete de software que pueda estar afectado. Pueden haber cambido también algunos permisos de directorio. Compruebe esto si algo se niega a arrancar.

Felicidades, acaba de restaurar con éxito su base de datos local de pacman.

## Coloreando la salida de pacman

Ahora que makepkg tiene una salida colorizada, ¿por qué no pacman también? El administrador de paquetes en [Gentoo](http://www.gentoo.org/) llamado 'portage' usa colores ampliamente, y como pueden ver en esta [screenshot](http://gentoo-portage.com/up_img/1026.png), se mejora enormemente la legibilidad.

#### Scripts

El usuario citral usa el siguiente script en su .bashrc:

```
alias pacs="pacsearch"
pacsearch () {
       echo -e "$(pacman -Ss $@ | sed \
       -e 's#core/.*#\\033[1;31m&\\033[0;37m#g' \
       -e 's#extra/.*#\\033[0;32m&\\033[0;37m#g' \
       -e 's#community/.*#\\033[1;35m&\\033[0;37m#g' \
       -e 's#^.*/.* [0-9].*#\\033[0;36m&\\033[0;37m#g' )"
}

```

Que es la solución más limpia. Sin embargo, si deseas un script para todo el sistema, ejecuta **como root**:

```
 touch /usr/bin/pacs && chmod 755 /usr/bin/pacs

```

y copia esto dentro de /usr/bin/pacs también como root:

```
 #!/bin/bash
 echo -e "$(pacman -Ss $@ | sed \
 -e 's#core/.*#\\033[1;31m&\\033[0;37m#g' \
 -e 's#extra/.*#\\033[0;32m&\\033[0;37m#g' \
 -e 's#community/.*#\\033[1;35m&\\033[0;37m#g' \
 -e 's#^.*/.* [0-9].*#\\033[0;36m&\\033[0;37m#g' )"

```

Puedes sustituir "pacs" en esas lineas por lo que quieras. Puedes crear tambien un alias de "pacs" por otra cosa en tu .bashrc, como se hizo antes..

El uso de estos comandos es muy sencillo; solo usa tu nuevo comando en vez de 'pacman', el resto sigue siendo lo mismo!

#### Alternativas

Una alternativa es usar este script en python, que emula la salida de pacman -Ss (¡con colores!) pero obtiene la lista de paquetes eso si desde el sitio web. Busca los repositorios oficiales y AUR (las dos community y unsupported).

```
#!/usr/bin/python

import os
import re
import sys
import urllib2

OFFICIAL_QUERY = "[https://archlinux.org/packages/search/\?q=](https://archlinux.org/packages/search/\?q=)"
AUR_QUERY = "[https://aur.archlinux.org/packages.php?K=](https://aur.archlinux.org/packages.php?K=)"

# Repos and colors
repos = {"Core":'32',"Extra":'36',"Testing":'31',"community":'33',"unsupported":'35'}

def strip_html(buffer):
    buffer = re.sub('<[^>]*>','',buffer)
    buffer = re.sub('(?m)^[ \t]*','',buffer)
    return buffer

def cut_html(beg,end,buffer):
    buffer = re.sub('(?s).*' + beg,'',buffer)
    buffer = re.sub('(?s)' + end + '.*','',buffer)
    return buffer

class RepoSearch:
    def __init__(self,keyword):
        self.keyword = keyword
        self.results = ''
        for name in ['official','aur']:
            self.get_search_results(name)
            self.parse_results(name)
        self.colorize()

    def get_search_results(self,name):
        if name == "official":
            query = OFFICIAL_QUERY
        elif name == "aur":
            query = AUR_QUERY

        f = urllib2.urlopen( query + self.keyword )
        self.search_results = f.read()
        f.close()

    def preformat(self,header,a,b):
        self.buffer = cut_html('<table class=\"' + header + '\"[^>]*>','</table',self.search_results)
        self.buffer = strip_html(self.buffer)
        self.buffer = self.buffer.split('\n')
        self.buffer = [line for line in self.buffer if line]
        del self.buffer[a:b]

    def parse_results(self,name):
        self.buffer = ''
        if name == 'official':
            if re.search('<table class=\"results\"',self.search_results):
                self.preformat('results',0,6)
            elif re.search('<div class=\"box\">',self.search_results):
                temp = re.search('<h2 class=\"title\">([^<]*)</h2>',self.search_results)
                temp = temp.group(1)
                temp = temp.split()
                self.preformat('listing',7,-1)
                for i in range(0,3): del self.buffer[i]
                for i in temp: self.buffer.insert(temp.index(i) + 2,i)

        elif name == 'aur':
            p = re.compile('<td class=.data[^>]*>')
            self.buffer = self.search_results.split('\n')
            self.buffer = [strip_html(line) for line in self.buffer if p.search(line)]

        l = len(self.buffer)/6
        parsed_buf = ''

        for i in range(l):
            parsed_buf += self.buffer[i*6] + '/'
            parsed_buf += self.buffer[i*6+1] + ' '*(24-len(self.buffer[i*6] + self.buffer[i*6+1]))
            parsed_buf += self.buffer[i*6+2]
            if name == "official":
                parsed_buf += ' ' + self.buffer[i*6+3]
            parsed_buf += '\n' + self.buffer[i*6+4] + '\n'

        self.results += parsed_buf

    def colorize(self):
        for repo,repo_color in repos.iteritems():
            self.results = re.sub(repo + '/.*','\\033[1;' + repo_color + 'm' + '\g<0>' + '\\033[0;0m',self.results)

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print "Usage: " + sys.argv[0] + " <keyword>"
        sys.exit(2)
    reposearch = RepoSearch(sys.argv[1])
    sys.stdout.write(reposearch.results)

```

#### Usando 'acoc'

Hay otra, una posibilidad más general de colorear arbitrariamente la salida de los comandos. Puedes descargar la pequeña herramienta en [Ruby](http://www.ruby-lang.org/en/), llamada [acoc](http://raa.ruby-lang.org/project/acoc/) (y sus dependencias, [term-ansicolor](http://raa.ruby-lang.org/project/ansicolor/) y [tpty](http://raa.ruby-lang.org/cache/ruby-tpty/). ). tpty no es realmente requerida, pero algunas aplicaciones como "ls" no funcionan con acoc (necesitan ser iniciadas en la terminal (o pseudo terminal, en este caso), o bien se comportarán diferente).

La instalación es relativamente fácil, aquí hay un paseo rápido:

```
$ tar xvzf tpty-0.0.1.tar.gz
$ cd tpty-0.0.1
$ ruby extconf.rb
$ make
$ ruby ./test.rb
# make install

```

```
$ tar xvzf term-ansicolor-1.0.1.tar.gz
$ cd term-ansicolor-1.0.1
# ruby install.rb

```

Y ahora acoc en si:

```
$ tar xvzf acoc-0.7.1.tar.gz
$ cd acoc-0.7.1
# make install

```

Ahora, solo lee la sección "Advanced Installation" en el archivo INSTALL de acoc, y configura acoc como se te plazca. Crea un enlace para 'pacman' también, ya que es principalmente para eso que lo estamos haciendo. Una vez ejecutes acoc, puedes añadir estas lineas a tu acoc.conf:

```
[pacman -Si]
/^Name\s+:\s([\w.-]+)/                              bold
[pacman -Qi]
/^Name\s+:\s([\w.-]+)/                              bold
[pacman -Qi$]
/^([\w.-]+)\s([\w.-]+)/                 bold,clear
[pacman -Ss]
/^([\w.-]+)\/([\w.-]+)\s+([\w.-]+)/     clear,bold,clear
[pacman -Qs]
/^([\w.-]+)\/([\w.-]+)\s+([\w.-]+)/     clear,bold,clear
[pacman -Sl]
/^([\w.-]+)\s([\w.-]+)\s([\w.-]+)/              clear,bold,clear
[pacman -Qo]
/^([\w.-\/]+)\sis\sowned\sby\s([\w.-]+)\s([\w.-]+)/     clear,bold,clear
[pacman -Qe$]
/^([\w.-]+)\s([\w.-]+)/                 bold,clear
[pacman -Qg$]
/^([\w.-]+)\s([\w.-]+)/                 clear,bold

```

Puede no ser perfecto, o particulármente bonito, pero por lo menos funciona bien para mí. Las lineas de arriba solo hacen que pacman imprima todos los nombres de los paquetes en negrita, que es particularmente útil en p.ej. "pacman -Ss xfce". Si lo que quieres son más colores, puedes modificar las lineas a tu gusto. Lee la documentación de acoc contenida en la paquete con las fuentes del programa para más información.

#### Links

[Forum thread](https://bbs.archlinux.org/viewtopic.php?t=12430&postdays=0&postorder=asc&start=15)

#### Alternativa

En AUR está disponible un [PKGBUILD](https://aur.archlinux.org/packages.php?do_Details=1&ID=11827) con el parche para los colores para pacman de Vogo.