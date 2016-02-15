Este artículo trata los utilidades de los sistemas GNU/Linux denominadas utilidades _core_, como _less_, _ls_, y _grep_. El ámbito de este artículo incluye, pero no está limitado a, aquellas utilidades incluidas en el paquete de GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils). Lo siguiente son varios trucos y consejos y otras informaciones útiles relacionadas con estas utilidades.

## Contents

*   [1 Comandos básicos](#Comandos_b.C3.A1sicos)
*   [2 cat](#cat)
*   [3 dd](#dd)
    *   [3.1 Comprobar el progreso de dd en ejecución](#Comprobar_el_progreso_de_dd_en_ejecuci.C3.B3n)
        *   [3.1.1 Usando el visor de tubería (pv)](#Usando_el_visor_de_tuber.C3.ADa_.28pv.29)
    *   [3.2 derivados de dd](#derivados_de_dd)
*   [4 grep](#grep)
    *   [4.1 Salida con colores](#Salida_con_colores)
    *   [4.2 Salida de error estándar](#Salida_de_error_est.C3.A1ndar)
*   [5 iconv](#iconv)
    *   [5.1 Convertir el fichero reemplazándolo](#Convertir_el_fichero_reemplaz.C3.A1ndolo)
*   [6 ip](#ip)
*   [7 less](#less)
    *   [7.1 Salida en color mediante variables de entorno](#Salida_en_color_mediante_variables_de_entorno)
    *   [7.2 Salida en color mediante wrappers](#Salida_en_color_mediante_wrappers)
    *   [7.3 Vim como visualizador alternativo](#Vim_como_visualizador_alternativo)
    *   [7.4 Salida coloreada cuando lee de entrada estándar](#Salida_coloreada_cuando_lee_de_entrada_est.C3.A1ndar)
*   [8 ls](#ls)
*   [9 mkdir](#mkdir)
*   [10 mv](#mv)
*   [11 rm](#rm)
*   [12 sed](#sed)
*   [13 seq](#seq)
*   [14 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Comandos básicos

La siguiente tabla lista los comandos de consola básicos que todo usuario linux debería conocer. Comandos en **negrita** son parte de la línea de comandos, otros son programas separados llamados desde la consola. Véase las siguientes secciones y _Artículos relacionados_ para más detalles.

| Comando | Descripción | Ejemplo |
| man | Muestra la página del manual para ese comando | man ed |
| **cd** | Cambia de directorio | cd /etc/pacman.d |
| mkdir | Crea un directorio | mkdir ~/newfolder |
| rmdir | Elimina un directorio vacío | rmdir ~/emptyfolder |
| rm | Elimina un fichero | rm -r ~/file.txt |
| rm -r | Elimina directorios y sus contenidos | rm -r ~/.cache |
| ls | Lista archivos | ls *.avi |
| ls -a | Lista archivos ocultos | ls -a /home/archie |
| ls -al | Lista archivos ocultos y propiedades de los archivos |
| mv | Mueve un fichero | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | Copia un fichero | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | Da permisos de ejecución a un fichero | chmod +x ~/.local/bin/myscript.sh |
| cat | Muestra el contenido de un archivo | cat /etc/hostname |
| strings | Muestra caracteres imprimibles en un fichero binario | strings /usr/bin/free |
| find | Busca un archivo | find ~ -name myfile |
| mount | Mointa una partición | mount /dev/sdc1 /media/usb |
| df -h | Muestra el espacio disponible en todas las particiones |
| ps -A | Muestra todos los procesos en ejecución |
| killall | Mata todas las instancias de un proceso en ejecución |

## cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) "wikipedia:cat (Unix)") (_catenate_) es una utilidad estándar de unix que concatena y lista ficheros.

*   Dado que _cat_ no es un comando integrado en la consola, en bastantes ocasiones encontrará más conveniente usar una [redirección (English)](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), por ejemplo en scripts, o si le preocupa el rendimiento . De hecho `< _file_` hace lo mismo que `cat _file_`.

*   _cat_ es capaz de trabajar con múltiples líneas, aunque esto se ve a veces como una mala práctica.

```
$ cat << EOF >> _ruta/al/fichero_
_primera linea_
...
_últimalinea_
EOF

```

	Una alternativa mejor es el comando _echo_:

```
$ echo "\
_primera línea_
...
_última línea_" \
>> _ruta/al/fichero_

```

*   Si necesita lista las lineas del fichero en orden inverso, existe una utilidad llamada tac [tac](https://en.wikipedia.org/wiki/tac_(Unix) "wikipedia:tac (Unix)") (_cat_ invertido).

## dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) "wikipedia:dd (Unix)") es un comando de sistemas operativos Unix y similares cuyo propósito principal es convertir y copiar un fichero.

**Note:** _cp_ hace lo mismo que _dd_ sin pasarle argumentos pero no esta diseñado para procedimientos de borrado de discos más versátiles.

### Comprobar el progreso de dd en ejecución

Por defecto, no hay salida para _dd_ hasta que la tarea ha terminado. Con _kill_ y la señal `USR1` puede forzar a imprimir el estatus sin matar al programa. Habra una segunda terminal como root e introduzca el siguiente comando:

```
# killall -USR1 dd

```

**Note:** Esto afectará de igual manera a todas las instancias en ejecución de _dd_.

Or:

```
# kill -USR1 _pid_del_comando_dd_

```

For example:

```
# kill -USR1 $(pidof dd)

```

Esto provoca que _dd_ imprima de forma inmediatael progreso en la terminal. Por ejemplo:

```
605+0 records in
605+0 records out
634388480 bytes (634 MB) copied, 8.17097 s, 77.6 MB/s

```

#### Usando el visor de tubería (pv)

Como alternative puede usar [pv](https://www.archlinux.org/packages/?name=pv) para monitorizar el pipeline de dd:

```
# dd if=_/origen/de/flujo_de_archivo_ | pv -_opciones_de_monitorización_ -s _tamaño_del_archivo_ | dd of=_/destino/de/flujo_de_archivo_

```

Para usar el visor de tuberías con mayor facilidad puede añadir esto a bashrc o a zshrc:

```
copy() {
    size=$(stat -c%s $1)
    dd if=$1 &> /dev/null | pv -petrb -s $size | dd of=$2
}

```

Y usarlo con:

```
# copy _/fichero/de/origen_ _/fichero/de/destino_

```

### derivados de dd

Otros programas por el estilo de _dd_ muestra un estatus de salida periódico, p.ej: una simple barra de progreso.

	dcfldd 

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd) es una versión mejorada de dd con características utiles para análisis forense y seguridad. Acepta la mayoría de los parámetros de dd e incluye salida de estatus. La última versión estable de dcfldd fue el 19 de diciembre de 2006.

	ddrescue 

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) es una herramienta de recuperación de datos. Es capaz de ignorar errores de lectura, lo que es una característica útil en situaciones de borrado de disco en casi cualquier caso. Véase [official manual](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html) para más detalles.

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (de [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed") _g/re/p_, _global/regular expression/print_) es una utilidad para busqueda de texto en línea de comandos escrito originalmente para Unix. El comando _grep_ busca ficheros o en la entrada estándar de manera global líneas que coincidan con una expresión regular dada y las imprime a la salida estándar del programa.

*   Recuerde que _grep_ maneja ficheros files, por lo que un comando como `cat _archivo_ | grep _patrón_` es remplazable por `grep _patrón_ _archivo_`

*   Alternativas a _grep_ optimizadas para codigo fuente existe , como [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) y [ack](https://www.archlinux.org/packages/?name=ack).

### Salida con colores

La salida con colores de `grep` puede ser muy útil para aprender [expresiones regulares](https://en.wikipedia.org/wiki/regexp "wikipedia:regexp") y características adicionales de `grep`.

Para habilitar el coloreado de _grep_ la siguiente entrada en el archivo de configuración de su terminal (p.ej:. si usa [Bash](/index.php/Bash "Bash")):

 `~/.bashrc`  `alias grep='grep --color=auto'` 

Para incluir numeración de las líneas en la salida, incluya `-n` a la entrada anterior.

La variable de entorno `GREP_COLOR` puede usarse para definir el color de resaltado por defecto (por defecto es rojo). Para cambiar el color busque en [secuencia de escape ANSI](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html) para el color que desee y añádalo con:

```
export GREP_COLOR="1;32"

```

`GREP_COLORS` puede usarse para definir búsquedas específicas.

### Salida de error estándar

Algunos comandos envían sus resultados a la salida de error estándar, por lo que grep no parece tener efecto aparente. En este caso redirija la salida de error a la salida estándar con:

```
$ _comando_ 2>&1 | grep _argumentos_

```

o usando el método abreviado de Bash 4:

```
$ _comando_ |& grep _argumentos_

```

Véase también [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html).

## iconv

`iconv` convierte la codificación de caracteres de una codificación a otra.

El siguiente comando convertirá el fichero `foo` de ISO-8859-15 a UTF-8 guardándolo en `foo.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 foo >foo.utf

```

Vea `man iconv` para más detalles.

### Convertir el fichero reemplazándolo

**Tip:** puede usar [recode](https://www.archlinux.org/packages/?name=recode) en lugar de iconv si no quiere tocar el mtime.

Al contrario que [sed](#sed), _iconv_ no provee una opción para convertir remplazando el propio fichero. Sin embargo, `sponge` puede usarse para tal fin, esta incluido en [moreutils](https://www.archlinux.org/packages/?name=moreutils).

```
$ iconv -f WINDOWS-1251 -t UTF-8 foobar.txt | sponge foobar.txt

```

Vea `man sponge` para más detalles.

## ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") permite mostrar información sobre los dispositivos de red, direcciones IP, tablas de enrutamiento y otros objetos en la pila de procotolos [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") de Linux. Añadiendo varios comandos, puede manipular y configurar la mayoría de estos objetos.

**Note:** La utilidad _ip_ la provee el paquete [iproute2](https://www.archlinux.org/packages/?name=iproute2), que está incluido en el grupo [base](https://www.archlinux.org/groups/x86_64/base/).

| Objecto | Propósito | Nombre de página en el manual |
| ip addr | manejo de dirección de protocolo | ip-address |
| ip addrlabel | manejo etiquetado protocolo | ip-addrlabel |
| ip l2tp | Tunel ethernet sobre IP (L2TPv3) | ip-l2tp |
| ip link | configuración dispositivo de red | ip-link |
| ip maddr | manejo direcciones multicast | ip-maddress |
| ip monitor | monitorizado de mensajes netlink | ip-monitor |
| ip mroute | manejo de cache de enrutado multicast | ip-mroute |
| ip mrule | manejo la base de datos de politicas de enrutado multicast |
| ip neigh | manejo de tablas ARP/Vecinos | ip-neighbour |
| ip netns | manejo de proceso del espacio de nombres en red | ip-netns |
| ip ntable | configuración tabla de vecinos | ip-ntable |
| ip route | manejo de la tabla de enrutamiento | ip-route |
| ip rule | manejo de la base de datos de políticas de enrutamiento | ip-rule |
| ip tcp_metrics | manejo de metricas TCP | ip-tcp_metrics |
| ip tunnel | configuración de tunel | ip-tunnel |
| ip tuntap | manejo de dispositivos TUN/TAP |
| ip xfrm | manejo de políticas IPsec | ip-xfrm |

El comando `help` está disponible para todos los objetos. Por ejemplo, escribiendo `ip addr help` se mostrará la sintaxis de comando disponible para el objeto address. Para un uso avanzado véase [documentación iproute2](http://www.policyrouting.org/iproute2.doc.html).

El artículo [Configuración de Red](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)") muestra como el comando _ip_ es usado en la práctica para varias tareas típicas.

**Nota:** Puede que esté familiarizado con el comando [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") , que era usado versiones anteriores de Linux para la configuración de interfaces. Ahora está obsoleto en Arch Linux; debería usar _ip_ en su lugar.

## less

[less](https://en.wikipedia.org/wiki/less_(Unix) "wikipedia:less (Unix)") es un visualizados de archivos de texto en consola. Al contrario que otros visualizadores similares como [more](https://en.wikipedia.org/wiki/more_(command) "wikipedia:more (command)") y [pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)"), _less_ ofrece una interfaz mucho más avanzada y completa [feature-set](http://www.greenwoodsoftware.com/less/faq.html).

Véase [List of applications#Terminal pagers](/index.php/List_of_applications#Terminal_pagers "List of applications") para más alternativas.

### Salida en color mediante variables de entorno

Añada las siguientes líneas a su archivo de configuración de la terminal:

 `~/.bashrc` 

```
export LESS=-R
export LESS_TERMCAP_me=$(printf '\e[0m')
export LESS_TERMCAP_se=$(printf '\e[0m')
export LESS_TERMCAP_ue=$(printf '\e[0m')
export LESS_TERMCAP_mb=$(printf '\e[1;32m')
export LESS_TERMCAP_md=$(printf '\e[1;34m')
export LESS_TERMCAP_us=$(printf '\e[1;32m')
export LESS_TERMCAP_so=$(printf '\e[1;44;1m')
```

Cambio los valores a su gusto. Referencias: [ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors "wikipedia:ANSI escape code").

### Salida en color mediante wrappers

Puede habilitar el resaltado de sintaxis en _less_. Primero, instale [source-highlight](https://www.archlinux.org/packages/?name=source-highlight), y a continuación añada estás lineas a su archivo de configuración de la terminal:

 `~/.bashrc` 

```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

Usuarios asíduos de la línea de comandos pueden querar instalar [lesspipe](https://www.archlinux.org/packages/?name=lesspipe).

Los usarios puede listar archivos comprimidos dentro de un archivador usando su visualizador:

 `$ less _compressed_file_.tar.gz` 

```
==> usa archivo_tar:fichero_contenido para ver un fichero en el archivador
-rw------- _usuario_/_grupo_  695 2008-01-04 19:24 _archivo_comprimido_/_contenido1_
-rw------- _usuario_/_grupo_   43 2007-11-07 11:17 _archivo_comprimido_/_contenido2_
_archivo_comprimido_.tar.gz (END)
```

_lesspipe_ también concede a _less_ la capacidad para interactuar con ficheros que no sean archivadores, sirviendo como alternativa para el comando específico asociado a según el tipo de archivo en concreto (como ver HTML mediante [python-html2text](https://www.archlinux.org/packages/?name=python-html2text)).

Vuelva a loguearse tras instalar _lesspipe_ para activarlo, o usando source `/etc/profile.d/lesspipe.sh`.

### Vim como visualizador alternativo

[Vim](/index.php/Vim "Vim") (_visual editor improved_) tiene un script para ver el contenido de fichero de texto, binarios, directorios. Añada la siguiente línea a su archivo de configuración de la terminal para usarlo como visualizador:

 `~/.bashrc`  `alias less='/usr/share/vim/vim74/macros/less.sh'` 

Existe una alternativa a la macro _less.sh_, que puede funcionar como la variable de entorno `PAGER`. Instale [vimpager](https://www.archlinux.org/packages/?name=vimpager) añada lo siguiente a su archivo de configuración de la terminal:

 `~/.bashrc` 

```
export PAGER='vimpager'
alias less=$PAGER
```

Ahora los programas que use la variable de entorno `PAGER`, como [git](/index.php/Git "Git"), usarán _vim_ como un visualizador.

### Salida coloreada cuando lee de entrada estándar

**Nota:** Se recomienda añadir [#Salida en color mediante variables de entorno](#Salida_en_color_mediante_variables_de_entorno) a su `~/.bashrc` o `~/.zshrc`, ya que lo siguiente esta basado en `export LESS=R`

Cuando ejecuta un comando y redirige su [salida estándar](https://en.wikipedia.org/wiki/Standard_output "wikipedia:Standard output") (_stdout_) a _less_ para visualizarla (p.ej: `pacman -Qe | less`), puede encontrarse con que la salida ya no sale coloreada. Esto suele pasar porque el programa intentar detectar si su _salida estándar_ es un terminal interactivo, en cuyo caso imprime el texto coloreado,y en caso contrario no. Esto es un buen comportamiento cuando quiere redirigir la _salida estándar_ a un fichero, p.ej: `pacman -Qe > pkglst-backup.txt`, pero menos indicado cuando quiere visualizar la salid con `less`.

Algunos programas proveen una opción para deshabilitar la detección de tty interactiva:

```
# dmesg --color=always | less

```

En el caso de que el programa no proporcione una opción similar, es posible engañarlo para que crea que la _salida estándar_ es un terminal interactivo con las siguientes utilidades:

*   **stdoutisatty** — Un pequeño programa que captura la llamada a la función `isatty` .

	[https://github.com/lilydjwg/stdoutisatty](https://github.com/lilydjwg/stdoutisatty). || [stdoutisatty-git](https://aur.archlinux.org/packages/stdoutisatty-git/)

	Ejemplo: `stdoutisatty _program_ | less`

*   **socat** — Un relevo para transferencia de datos bidireccional entre dos canales de datos independientes. Esta basado en el programa de GNU [readline](https://www.archlinux.org/packages/?name=readline).

	[http://www.dest-unreach.org/socat/](http://www.dest-unreach.org/socat/) || [socat](https://www.archlinux.org/packages/?name=socat)

	Ejemplo: `socat EXEC:"_program_",pty STDIO | less`

*   **[script](https://en.wikipedia.org/wiki/Script_(Unix) "wikipedia:Script (Unix)")** — Una utilidad que hace typescript de una sesión de terminal.

	[http://man7.org/linux/man-pages/man1/script.1.html](http://man7.org/linux/man-pages/man1/script.1.html) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

	Ejemplo: `script -fqc "_program_" | less` or [[2]](http://stackoverflow.com/questions/1401002/trick-an-application-into-thinking-its-stdin-is-interactive-not-a-pipe/20401674#20401674)

*   **unbuffer** — Un script basado en _sh_ y [Tcl](http://tcl.tk/).

	[http://expect.sourceforge.net/example/unbuffer.man.html](http://expect.sourceforge.net/example/unbuffer.man.html) || [expect](https://www.archlinux.org/packages/?name=expect)

	Ejemplo: `unbuffer _program_ | less`

De forma alternativa, usando el módulo [zpty](http://zsh.sourceforge.net/Doc/Release/Zsh-Modules.html#The-zsh_002fzpty-Module) de [zsh](/index.php/Zsh "Zsh"): [[3]](http://lilydjwg.is-programmer.com/2011/6/29/using-zpty-module-of-zsh.27677.html)

 `~/.zshrc` 

```
zmodload zsh/zpty

pty() {
	zpty pty-${UID} ${1+$@}
	if [[ ! -t 1 ]];then
		setopt local_traps
		trap '' INT
	fi
	zpty -r pty-${UID}
	zpty -d pty-${UID}
}

ptyless() {
	pty $@ | less
}
```

Uso:

```
$ ptyless _program_

```

Para redirigirlo a un visualizador (less en este ejemplo):

```
$ pty _program_ | less

```

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") (_list_) es un comando para lista fichero en sistemas operativos Unix y similares.

*   _ls_ puede listar [permisos de ficheros](/index.php/File_permissions_and_attributes#Viewing_permissions "File permissions and attributes").

*   Salida coloreada puede ser habilitadac con un simple alias. El fichero `~/.bashrc` debería tener la siguiente entrada copiada de `/etc/skel/.bashrc`:

	`alias ls='ls --color=auto'`

El siguiente paso mejorará aún más la salida coloreada de _ls_; por ejemplo, enlaces simbólicos rotos (huérfanos) se mostrarán en un tono rojo. Añada la siguiente línea a su archivo de configuración de la terminal:

	`eval $(dircolors -b)`

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") (_make directory_) es un comando para crear directorios.

*   Para crear un directorio y toda su jerarquía, es usado el argumento `-p`, de otra forma se monstraría un error. Como se supone que los usuario saben lo que quieren, ,el argumento `-p` puede usarse por defecto:

	 `alias mkdir='mkdir -p -v'` 

	El argumento `-v` hace que la salida sea más detallada.

*   Cambiar los permisos con _chmod_ tras crear el directorio no es necesario pues la opción `-m` permite definir los permisos de acceso.

**Sugerencia:** Si tan solo quiere un directorio temporal, una mejor alternativa es [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file") (_make termporary_): `mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") (_move_) es un comando para renombrar y mover ficheros y directorios.

*   Puede ser muy peligroso, por lo que se recomiendo limitar su ámbito:

	 `alias mv=' timeout 8 mv -iv'` 

	Este alias suspende _mv_ tras ocho segundos, pide confirmación para borrar tres o más ficheros, lista las operaciones en curso y no almacena en el historial de la terminal si la terminal esta configurada para no almacenar aquellos comandos que empiezen por un espacio.

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) "wikipedia:rm (Unix)") (_remove_) es un comando que sirve para eliminar ficheros y directorios.

*   Puede ser muy peligroso, por lo que se recomiendo limitar su ámbito:

	 `alias rm=' timeout 3 rm -Iv --one-file-system'` 

	Este alias suspende _rm_ tras 3 segundos, pide confirmación para borrar tres o más ficheros, lista las operaciones en curso, no involucra mñas de un sistema de ficheros y no almacena en el historial de la terminal si la terminal esta configurada para no almacenar aquellos comandos que empiezen por un espacio. Sustituya `-I` por `-i` si prefiere confirmación por cada fichero.

	Usuarios de Zsh pueden querer poner `noglob` antes de `timeout` para evitar expansiones implicitas.

*   Para eliminar directorios que estén vacíos, use _rmdir_ ya que falla en cada de que el objetivo contengo ficheros.

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") (_stream editor_) is una utilidad de Unix que parsea y transforma texto

Aquí hay un puñado [list](http://sed.sourceforge.net/sed1line.txt) de ejemplo de una línea de como usar sed muy útiles.

**Sugerencia:** Alternativas más potentes son [AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") e incluso el lenguaje [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl").

## seq

**seq** (_sequence_) es una utilidad para generar secuencias de números. Hay alternativas integradas en la shell disponibles, por lo que es una buena práctica usarlas como se explica en [Wikipedia](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)").

## Véase también

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils

*   [GNU Coreutils Manpage](http://www.gnu.org/software/coreutils/manual/coreutils.html)

*   [Learn the DD command](http://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)