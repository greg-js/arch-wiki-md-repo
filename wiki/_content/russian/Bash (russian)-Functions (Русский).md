[Bash (Русский)](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)") также поддерживает функции. Добавляйте функции в `~/.bashrc` или в отдельный файл с `~/.bashrc` в качестве источника ([source](/index.php/Source "Source")). Больше примеров функций Bash тут: [BBS#30155](https://bbs.archlinux.org/viewtopic.php?id=30155).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Отображение кодов ошибок](#Отображение_кодов_ошибок)
*   [2 Компиляция и запуск кода C на лету](#Компиляция_и_запуск_кода_C_на_лету)
*   [3 Извлечение](#Извлечение)
*   [4 cd и ls в одной команде](#cd_и_ls_в_одной_команде)
*   [5 Простое создание заметок](#Простое_создание_заметок)
*   [6 Простой планировщик задач](#Простой_планировщик_задач)
*   [7 Калькулятор](#Калькулятор)
*   [8 Kingbash](#Kingbash)
*   [9 IP info](#IP_info)

## Отображение кодов ошибок

Чтобы установить `trap` для перехвата отличного от нуля кода ошибки последней выполненной команды, выполните:

 `~/.bashrc` 
```
EC() {
	echo -e '\e[1;33m'code $?'\e[m
'
}
trap EC ERR

```

## Компиляция и запуск кода C на лету

Эта функция скомпилирует (в папку `/tmp/`) и запустит файл с исходным кодом на языке [С](https://ru.wikipedia.org/wiki/%D0%A1%D0%B8_(%D1%8F%D0%B7%D1%8B%D0%BA_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F)) на лету (запуск будет произведен без аргументов). А после завершения работы программы, скомпилированный файл будет удален.

 `~/.bashrc` 
```
# Compile and execute a C source on the fly
csource() {
	[[ $1 ]]    || { echo "Missing operand" >&2; return 1; }
	[[ -r $1 ]] || { printf "File %s does not exist or is not readable
" "$1" >&2; return 1; }
	local output_path=${TMPDIR:-/tmp}/${1##*/};
	gcc "$1" -o "$output_path" && "$output_path";
	rm "$output_path";
	return 0;
}
```

## Извлечение

Эта функция позволяет извлекать данные из целого ряда различных типов архивов. Используется синтаксис `extract <file1> <file2> ...`.

 `~/.bashrc` 
```
extract() {
    local c e i

    (($#)) || return

    for i; do
        c=''
        e=1

        if [[ ! -r $i ]]; then
            echo "$0: file is unreadable: \`$i'" >&2
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
            *)     echo "$0: unrecognized file extension: \`$i'" >&2
                   continue;;
        esac

        command "${c[@]}" "$i"
        ((e = e || $?))
    done
    return "$e"
}

```

**Note:** Убедитесь, что `extglob` включен: `shopt -s extglob`,добавив его в `~/.bashrc` (см.: [Greg's Wiki:glob#Options which change globbing behavior](http://mywiki.wooledge.org/glob#Options_which_change_globbing_behavior)). Он включен по умолчанию, если используется [Bash completion](#Tab_completion).

Еще один способ сделать это - установить специальные пакеты:

*   [unp](https://www.archlinux.org/packages/?name=unp) - пакет из официальных источников, содержащий скрипт на Perl
*   [atool](https://www.archlinux.org/packages/?name=atool)
*   [dtrx](https://aur.archlinux.org/packages/dtrx/)

## cd и ls в одной команде

Очень часто после смены директории пользователь запускает ls, чтобы просмотреть ее содержимое. Таким образом, целесообразно объединить cd и ls в одну команду. В этом примере назовем ее `cl` (change list) и будем выводить сообщение об ошибке, если указанная директория не существует.

 `~/.bashrc` 
```
cl() {
	local dir="$1"
	local dir="${dir:=$HOME}"
	if [[ -d "$dir" ]]; then
		cd "$dir" >/dev/null; ls
	else
		echo "bash: cl: $dir: Directory not found"
	fi
}

```

Конечно, команда *ls* может быть изменена, чтобы соответствовать вашим потребностям, например `ls -hall --color=auto`.

## Простое создание заметок

 `~/.bashrc` 
```
note () {
    # if file doesn't exist, create it
    if [[ ! -f $HOME/.notes ]]; then
        touch "$HOME/.notes"
    fi

    if ! (($#)); then
        # no arguments, print file
        cat "$HOME/.notes"
    elif [[ "$1" == "-c" ]]; then
        # clear file
        printf "%s" > "$HOME/.notes"
    else
        # add all arguments to file
        printf "%s
" "$*" >> "$HOME/.notes"
    fi
}

```

## Простой планировщик задач

Inspired by [#Simple note taker](#Simple_note_taker)

 `~/.bashrc` 
```
todo() {
    if [[ ! -f $HOME/.todo ]]; then
        touch "$HOME/.todo"
    fi

    if ! (($#)); then
        cat "$HOME/.todo"
    elif [[ "$1" == "-l" ]]; then
        nl -b a "$HOME/.todo"
    elif [[ "$1" == "-c" ]]; then
        > $HOME/.todo
    elif [[ "$1" == "-r" ]]; then
        nl -b a "$HOME/.todo"
        eval printf %.0s- '{1..'"${COLUMNS:-$(tput cols)}"\}; echo
        read -p "Type a number to remove: " number
        sed -i ${number}d $HOME/.todo "$HOME/.todo"
    else
        printf "%s
" "$*" >> "$HOME/.todo"
    fi
}

```

## Калькулятор

 `~/.bashrc` 
```
calc() {
    echo "scale=3;$@" | bc -l
}

```

## Kingbash

Kingbash - это построенное на меню автодополнение (see [BBS#101010](https://bbs.archlinux.org/viewtopic.php?id=101010)).

Установите [kingbash](https://aur.archlinux.org/packages/kingbash/) from the [AUR](/index.php/AUR "AUR"), затем добавьте в `~/.bashrc`:

 `~/.bashrc` 
```
function kingbash.fn() {
    echo -n "KingBash> $READLINE_LINE" #Where "KingBash> " looks best if it resembles your PS1, at least in length.
    OUTPUT=$(/usr/bin/kingbash "$(compgen -ab -A function)")
    READLINE_POINT=$(echo "$OUTPUT" | tail -n 1)
    READLINE_LINE=$(echo "$OUTPUT" | head -n -1)
    echo -ne "\r\e[2K"
}
bind -x '"\t":kingbash.fn'

```

## IP info

Полная информация об IP-адресе и имени хоста на bash от [http://ipinfo.io](http://ipinfo.io):

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

**Note:** В Bash ограничен функционал использования регулярных выражений. В этом примере используются регулярные выражения языка Perl c *grep*. [[1]](http://unix.stackexchange.com/questions/84477/forcing-bash-to-use-perl-regex-engine)