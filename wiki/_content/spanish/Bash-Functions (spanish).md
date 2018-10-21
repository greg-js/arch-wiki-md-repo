**Estado de la traducción**
Este artículo es una traducción de [Bash/Functions](/index.php/Bash/Functions "Bash/Functions"), revisada por última vez el **2018-10-20**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Bash/Functions&diff=0&oldid=549134) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)") también admite funciones. Añada las funciones a `~/.bashrc`, o a un archivo separado que sea [cargado](/index.php/Source_(Espa%C3%B1ol) "Source (Español)") desde `~/.bashrc`. Se pueden encontrar más ejemplos de la función Bash en [BBS#30155](https://bbs.archlinux.org/viewtopic.php?id=30155).

## Contents

*   [1 Mostrar códigos de error](#Mostrar_c.C3.B3digos_de_error)
*   [2 Compilar y ejecutar una código fuente en C sobre la marcha](#Compilar_y_ejecutar_una_c.C3.B3digo_fuente_en_C_sobre_la_marcha)
*   [3 Extraer](#Extraer)
*   [4 cd y ls en uno](#cd_y_ls_en_uno)
*   [5 Tomador de notas simple](#Tomador_de_notas_simple)
*   [6 Utilidad de tarea simple](#Utilidad_de_tarea_simple)
*   [7 Calculadora](#Calculadora)
*   [8 Kingbash](#Kingbash)
*   [9 Información IP](#Informaci.C3.B3n_IP)

## Mostrar códigos de error

Para configurar `trap` para interceptar un código de retorno distinto de cero de la última ejecución del programa:

```
EC() {
	echo -e '\e[1;33m'code $?'\e[m
'
}
trap EC ERR

```

## Compilar y ejecutar una código fuente en C sobre la marcha

La siguiente función compilará (dentro del directorio `/tmp/`) y ejecutará el código fuente en [C](https://en.wikipedia.org/wiki/es:C_(lenguaje_de_programaci%C3%B3n) del argumento sobre la marcha (y la ejecución será sin argumentos). Y finalmente, después de que el programa termine, eliminará el archivo compilado.

```
# Compilar y ejecutar un código fuente en C sobre la marcha
csource() {
	[[ $1 ]]    || { echo "Falta el operando" >&2; return 1; }
	[[ -r $1 ]] || { printf "El archivo %s no existe o no se puede leer
" "$1" >&2; return 1; }
	local output_path=${TMPDIR:-/tmp}/${1##*/};
	gcc "$1" -o "$output_path" && "$output_path";
	rm "$output_path";
	return 0;
}
```

## Extraer

La siguiente función extraerá una amplia gama de tipos de archivos comprimidos. Utilícelo con la sintaxis `extract <archivo1> <archivo2> ...`.

```
extract() {
    local c e i

    (($#)) || return

    for i; do
        c=''
        e=1

        if [[ ! -r $i ]]; then
            echo "$0: el archivo es ilegible: \`$i'" >&2
            continue
        fi

        case $i in
            *.t@(gz|lz|xz|b@(2|z?(2))|a@(z|r?(.@(Z|bz?(2)|gz|lzma|xz)))))
                   c=(bsdtar xvf);;
            *.7z)  c=(7z x);;
            *.Z)   c=(uncompress);;
            *.bz2) c=(bunzip2);;
            *.exe) c=(cabextract);;
            *.gz)  c=(gunzip);;
            *.rar) c=(unrar x);;
            *.xz)  c=(unxz);;
            *.zip) c=(unzip);;
            *)     echo "$0: extensión de archivo no reconocida: \`$i'" >&2
                   continue;;
        esac

        command "${c[@]}" "$i"
        ((e = e || $?))
    done
    return "$e"
}

```

**Nota:** Asegúrese de que `extglob` esté activado: `shopt -s extglob`, añadiéndolo a `~/.bashrc` (véase [Opciones que cambian el comportamiento de englobado](https://mywiki.wooledge.org/glob#Options_which_change_globbing_behavior "gregswiki:glob")).

Otra forma de hacer esto es instalar un paquete especializado, véase [Herramientas de conveniencia de archivado y compresión](/index.php/Archiving_and_compression_tools#Convenience_tools "Archiving and compression tools").

## cd y ls en uno

Muy a menudo, al cambiar a un directorio le sigue la orden `ls` para listar su contenido. Por lo tanto, es útil tener una segunda función que haga ambas cosas a la vez. En este ejemplo lo llamaremos `cl` (*change list*, o listar al cambiar) y mostraremos un mensaje de error si el directorio especificado no existe.

```
cl() {
	local dir="$1"
	local dir="${dir:=$HOME}"
	if [[ -d "$dir" ]]; then
		cd "$dir" >/dev/null; ls
	else
		echo "bash: cl: $dir: Directorio no encontrado"
	fi
}

```

Por supuesto, la orden *ls* puede modificarse para adaptarse a sus necesidades, por ejemplo, `ls -hall --color=auto`.

## Tomador de notas simple

```
note () {
    # si el archivo no existe, créalo
    if [[ ! -f $HOME/.notes ]]; then
        touch "$HOME/.notes"
    fi

    if ! (($#)); then
        # sin argumentos, imprimir archivo
        cat "$HOME/.notes"
    elif [[ "$1" == "-c" ]]; then
        # limpiar archivo
        printf "%s" > "$HOME/.notes"
    else
        # añadir todos los argumentos al archivo
        printf "%s
" "$*" >> "$HOME/.notes"
    fi
}

```

## Utilidad de tarea simple

Inspirado en [#Tomador de notas simple](#Tomador_de_notas_simple).

```
todo() {
    if [[ ! -f $HOME/.todo ]]; then
        touch "$HOME/.todo"
    fi

    if ! (($#)); then
        cat "$HOME/.todo"
    elif [[ "$1" == "-l" ]]; then
        nl -b a "$HOME/.todo"
    elif [[ "$1" == "-c" ]]; then
        > $HOME/.todo
    elif [[ "$1" == "-r" ]]; then
        nl -b a "$HOME/.todo"
        eval printf %.0s- '{1..'"${COLUMNS:-$(tput cols)}"\}; echo
        read -p "Introduzca un número para eliminar: " number
        sed -i ${number}d $HOME/.todo "$HOME/.todo"
    else
        printf "%s
" "$*" >> "$HOME/.todo"
    fi
}

```

## Calculadora

```
calc() {
    echo "scale=3;$@" | bc -l
}

```

## Kingbash

Kingbash - autocompletado dirigido por menú (véase [BBS#101010](https://bbs.archlinux.org/viewtopic.php?id=101010)).

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [kingbash-gb-git](https://aur.archlinux.org/packages/kingbash-gb-git/) de [AUR](/index.php/AUR "AUR"), luego inserte lo siguiente en su `~/.bashrc`:

```
function kingbash.fn() {
    echo -n "KingBash> $READLINE_LINE" #Where "KingBash> " se ve mejor si se parece a su PS1, al menos en longitud.
    OUTPUT=$(/usr/bin/kingbash "$(compgen -ab -A function)")
    READLINE_POINT=$(echo "$OUTPUT" | tail -n 1)
    READLINE_LINE=$(echo "$OUTPUT" | head -n -1)
    echo -ne "\r\e[2K"
}
bind -x '"\t":kingbash.fn'

```

## Información IP

Información detallada sobre una dirección IP o nombre de máquina *(hostname)* en bash a través de [http://ipinfo.io](http://ipinfo.io):

```
ipif() { 
    if grep -P "(([1-9]\d{0,2})\.){3}(?2)" <<< "$1"; then
	 curl ipinfo.io/"$1"
    else
	ipawk=($(host "$1" | awk '/address/ { print $NF }'))
	curl ipinfo.io/${ipawk[1]}
    fi
    echo
}

```

**Nota:** Bash está limitado a expresiones regulares extendidas; este ejemplo utiliza expresiones regulares perl con *grep*. [[1]](http://unix.stackexchange.com/questions/84477/forcing-bash-to-use-perl-regex-engine)