Ссылки по теме

*   [Bash (Русский)](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)")
*   [Переменные окружения](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "Переменные окружения")

**Состояние перевода:** На этой странице представлен перевод статьи [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt"). Дата последней синхронизации: 2015-07-21\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Color_Bash_Prompt&diff=0&oldid=381378).

Существуют различные возможности настройки строки приглашения [Bash](/index.php/Bash "Bash")'а (PS1), которые могут сделать работу в командной строке комфортней и продуктивней. Например, можно добавить дополнительную информацию или цвет, чтобы приглашение ввода можно было легко обнаружить среди остального текста.

В этой статье рассказывается как *настроить персональное приглашение для обычного пользователя*.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Применение настроек](#Применение_настроек)
*   [2 Базовые приглашения](#Базовые_приглашения)
    *   [2.1 Обычный пользователь](#Обычный_пользователь)
    *   [2.2 Root](#Root)
*   [3 Профессиональные приглашения](#Профессиональные_приглашения)
    *   [3.1 Обычный пользователь](#Обычный_пользователь_2)
    *   [3.2 Root](#Root_2)
*   [4 Максимальные приглашения](#Максимальные_приглашения)
    *   [4.1 Статус нагрузки/памяти для 256colors](#Статус_нагрузки/памяти_для_256colors)
    *   [4.2 Список цветов для приглашений и Bash](#Список_цветов_для_приглашений_и_Bash)
    *   [4.3 Прерывания приглашения](#Прерывания_приглашения)
    *   [4.4 Позиционирование курсора](#Позиционирование_курсора)
    *   [4.5 Отображение кода возврата](#Отображение_кода_возврата)
*   [5 Советы и подсказки](#Советы_и_подсказки)
    *   [5.1 Разные цвета при вводе текста и при выводе](#Разные_цвета_при_вводе_текста_и_при_выводе)
    *   [5.2 Случайные цитаты при входе](#Случайные_цитаты_при_входе)
    *   [5.3 Раскрашенные последние новости Arch при входе](#Раскрашенные_последние_новости_Arch_при_входе)
    *   [5.4 Просмотр цветов](#Просмотр_цветов)
    *   [5.5 Раскрашенное git приглашение](#Раскрашенное_git_приглашение)
    *   [5.6 Раскрашенные существующие бесцветные приглашения](#Раскрашенные_существующие_бесцветные_приглашения)
*   [6 Смотрите также](#Смотрите_также)

## Применение настроек

Чтобы применить изменения, сделанные в файле `.bashrc`, без перезапуска shell, запустите команду:

```
$ source ~/.bashrc

```

## Базовые приглашения

Следующие настройки полезны для визуального различия приглашения root пользователя от приглашений обычных пользователей.

### Обычный пользователь

Зелёное приглашение для *обычных пользователей*:

[chiri@zetsubou ~]$ _
 `~/.bashrc` 
```
#PS1='[\u@\h \W]\$ '  # Default
PS1='\[\e[1;32m\][\u@\h \W]\$\[\e[0m\] '
```

### Root

Красное приглашение для *root* (скопируйте из `/etc/skel/`, если ещё не сделали этого):

[root@zetsubou ~]# _
 `/root/.bashrc` 
```
#PS1='[\u@\h \W]\$ '  # Default
PS1='\[\e[1;31m\][\u@\h \W]\$\[\e[0m\] '
```

## Профессиональные приглашения

### Обычный пользователь

Зелёное с синим приглашение для *обычных пользователей*:

chiri ~/docs $ echo "sample output text"
sample output text
chiri ~/docs $ _
 `PS1='\[\e[0;32m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[1;32m\]\$\[\e[m\] \[\e[1;37m\]'` 

Этот пример предоставляет очень приятное цветное приглашение и тему консоли с ярко-белым цветом текста.

Вышеописанная строка содержит управляющие последовательности для цветового набора (начало окраски: `\[\e[*color*\]`, конец окраски: `\[\e[m\]`) и информационные заполнители:

*   **\u** - Имя пользователя. Исходное приглашение также содержит **\h**, который печатает имя хоста.
*   **\w** - Текущий абсолютный путь. Используйте **\W** для текущего относительного пути.
*   **\$** - Символ приглашения (например, `#` для root, `$` для обычных пользователей).
*   **\[** и **\]** - Эти теги должны обрамлять цветовые коды, чтобы bash понимал как правильно позиционировать курсор.

Последняя цветовая управляющая последовательность `\[\e[1;37m\]` не закрыта, поэтому весь оставшийся текст (всё что вы набираете в терминале, вывод программ и т.д.) будет окрашено в этот (ярко белый) цвет. Вы можете захотеть изменить этот цвет или удалить последнюю управляющую последовательность для того, чтобы оставить последующий вывод в неизменном цвете.

 `PS1="\[\e[7;92m\]\u\[\e[7;93m\]\W\]\[\e[7;95m\]$\[\e[0m\] "` 

Этот пример отобразит строку приглашения с задним фоном. Строка очень хорошо отделяется посреди остального текста.

### Root

Красное с синим приглашение для *root*:

root ~/docs # echo "sample output text"
sample output text
root ~/docs # _
 `PS1='\[\e[0;31m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[0;31m\]\$ \[\e[m\]\[\e[0;32m\]'` 

Этот пример предоставляет красное выделение и зелёный цвет текста в консоли.

 `PS1="\[\e[7;92m\]\u\[\e[7;93m\]\W\]\[\e[7;91m\]#\[\e[0m\] "` 

В этом примере строка приглашения приобретает задний фон и очень хорошо выделяется среди остального текста, решётка с красным задним фоном.

## Максимальные приглашения

### Статус нагрузки/памяти для 256colors

Это даже не предел. Вместо использования `sed` для парсинга загрузки памяти и нагрузки (используя опцию `-u` для non-buffering) и встроенной команды *history* для сохранения вашей истории в `HISTFILE` после каждой команды, что может быть очень полезно, если у вас проблемы с вылетами оболочек или дочерних оболочек, этот пример по сути заставляет BASH печатать переменные, которые ему уже известны, таким обоазом делая его экстремально быстрым по сравнению с приглашениями, использующими не-встроенные команды.

Это приглашение из статьи [BASH Power Prompt](http://www.askapache.com/linux-unix/bash-power-prompt.html) с AskApache.com, в которой разбираются подробности. Это особенно полезно для тех, кто хочет понять 256 цветные терминалы, ncurses, termcap и terminfo.

Этот пример для **256 цветных терминалов**, из которых произошли `\033[38;5;22m` управляющие последовательности.

```
802/1024MB      1.28 1.20 1.13 3/94 18563
[5416:17880 0:70] 05:35:50 Wed Apr 21 [srot@host.sqpt.net:/dev/pts/0 +1] ~

(1:70)$ _
```

```
PROMPT_COMMAND='history -a;echo -en "\033[m\033[38;5;2m"$(( $(sed -nu "s/MemFree:[\t ]\+\([0-9]\+\) kB/\1/p" /proc/meminfo)/1024))"\033[38;5;22m/"$(($(sed -nu "s/MemTotal:[\t ]\+\([0-9]\+\) kB/\1/Ip" /proc/meminfo)/1024 ))MB"\t\033[m\033[38;5;55m$(< /proc/loadavg)\033[m"'
PS1='\[\e[m
\e[1;30m\][$$:$PPID \j:\!\[\e[1;30m\]]\[\e[0;36m\] \T \d \[\e[1;30m\][\[\e[1;34m\]\u@\H\[\e[1;30m\]:\[\e[0;37m\]${SSH_TTY} \[\e[0;32m\]+${SHLVL}\[\e[1;30m\]] \[\e[1;37m\]\w\[\e[0;37m\] 
($SHLVL:\!)\$ '
```

### Список цветов для приглашений и Bash

Добавьте это в ваш(и) Bash файл(ы), чтобы задать цвета для приглашений и команд:

```
txtblk='\e[0;30m' # Black - Обычный
txtred='\e[0;31m' # Red
txtgrn='\e[0;32m' # Green
txtylw='\e[0;33m' # Yellow
txtblu='\e[0;34m' # Blue
txtpur='\e[0;35m' # Purple
txtcyn='\e[0;36m' # Cyan
txtwht='\e[0;37m' # White
bldblk='\e[1;30m' # Black - Жирный
bldred='\e[1;31m' # Red
bldgrn='\e[1;32m' # Green
bldylw='\e[1;33m' # Yellow
bldblu='\e[1;34m' # Blue
bldpur='\e[1;35m' # Purple
bldcyn='\e[1;36m' # Cyan
bldwht='\e[1;37m' # White
unkblk='\e[4;30m' # Black - Подчёркнутый
undred='\e[4;31m' # Red
undgrn='\e[4;32m' # Green
undylw='\e[4;33m' # Yellow
undblu='\e[4;34m' # Blue
undpur='\e[4;35m' # Purple
undcyn='\e[4;36m' # Cyan
undwht='\e[4;37m' # White
bakblk='\e[40m'   # Black - Фоновый
bakred='\e[41m'   # Red
bakgrn='\e[42m'   # Green
bakylw='\e[43m'   # Yellow
bakblu='\e[44m'   # Blue
bakpur='\e[45m'   # Purple
bakcyn='\e[46m'   # Cyan
bakwht='\e[47m'   # White
txtrst='\e[0m'    # Text Reset
```

Или если вы предпочитаете названия цветов, вы сможете писать их без необходимости их вычисления и желания высоко интенсивных цветов:

```
# Сброс
Color_Off='\e[0m'       # Text Reset

# Обычные цвета
Black='\e[0;30m'        # Black
Red='\e[0;31m'          # Red
Green='\e[0;32m'        # Green
Yellow='\e[0;33m'       # Yellow
Blue='\e[0;34m'         # Blue
Purple='\e[0;35m'       # Purple
Cyan='\e[0;36m'         # Cyan
White='\e[0;37m'        # White

# Жирные
BBlack='\e[1;30m'       # Black
BRed='\e[1;31m'         # Red
BGreen='\e[1;32m'       # Green
BYellow='\e[1;33m'      # Yellow
BBlue='\e[1;34m'        # Blue
BPurple='\e[1;35m'      # Purple
BCyan='\e[1;36m'        # Cyan
BWhite='\e[1;37m'       # White

# Подчёркнутые
UBlack='\e[4;30m'       # Black
URed='\e[4;31m'         # Red
UGreen='\e[4;32m'       # Green
UYellow='\e[4;33m'      # Yellow
UBlue='\e[4;34m'        # Blue
UPurple='\e[4;35m'      # Purple
UCyan='\e[4;36m'        # Cyan
UWhite='\e[4;37m'       # White

# Фоновые
On_Black='\e[40m'       # Black
On_Red='\e[41m'         # Red
On_Green='\e[42m'       # Green
On_Yellow='\e[43m'      # Yellow
On_Blue='\e[44m'        # Blue
On_Purple='\e[45m'      # Purple
On_Cyan='\e[46m'        # Cyan
On_White='\e[47m'       # White

# Высоко Интенсивные
IBlack='\e[0;90m'       # Black
IRed='\e[0;91m'         # Red
IGreen='\e[0;92m'       # Green
IYellow='\e[0;93m'      # Yellow
IBlue='\e[0;94m'        # Blue
IPurple='\e[0;95m'      # Purple
ICyan='\e[0;96m'        # Cyan
IWhite='\e[0;97m'       # White

# Жирные Высоко Интенсивные
BIBlack='\e[1;90m'      # Black
BIRed='\e[1;91m'        # Red
BIGreen='\e[1;92m'      # Green
BIYellow='\e[1;93m'     # Yellow
BIBlue='\e[1;94m'       # Blue
BIPurple='\e[1;95m'     # Purple
BICyan='\e[1;96m'       # Cyan
BIWhite='\e[1;97m'      # White

# Высоко Интенсивные фоновые
On_IBlack='\e[0;100m'   # Black
On_IRed='\e[0;101m'     # Red
On_IGreen='\e[0;102m'   # Green
On_IYellow='\e[0;103m'  # Yellow
On_IBlue='\e[0;104m'    # Blue
On_IPurple='\e[0;105m'  # Purple
On_ICyan='\e[0;106m'    # Cyan
On_IWhite='\e[0;107m'   # White

```

Для использования в командах в окружении вашего shell:

$ echo -e "${txtblu}test"
test
$ echo -e "${bldblu}test"
**test**
$ echo -e "${undblu}test"
**test**
$ echo -e "${bakblu}test"
**test**
$ _
 `PS1="\[$txtblu\]foo\[$txtred\] bar\[$txtrst\] baz : "` 

Двойные кавычки позволяют разрешить переменную `$color`, а управляющие `\[ \]` вокруг них позволяют не учитывать их при расчёте количества символов, поэтому позиция курсора будет верной.

**Примечание:** Если у вас возникает преждевременный перенос строки при наборе команды, скорее всего причиной является пропущенные управляющие последовательности (`\[ \]`).

### Прерывания приглашения

Некоторые прерывания приглашения Bash перечислены в man странице:

```
Bash allows these prompt strings to be customized by inserting a
number of *backslash-escaped special characters* that are
decoded as follows:

	\a		an ASCII bell character (07)
	\d		the date in "Weekday Month Date" format (e.g., "Tue May 26")
	\D{format}	the format is passed to strftime(3) and the result
			  is inserted into the prompt string an empty format
			  results in a locale-specific time representation.
			  The braces are required
	\e		an ASCII escape character (033)
	\h		the hostname up to the first `.'
	\H		the hostname
	\j		the number of jobs currently managed by the shell
	\l		the basename of the shell's terminal device name
	
		newline
	\r		carriage return
	\s		the name of the shell, the basename of $0 (the portion following
			  the final slash)
	\t		the current time in 24-hour HH:MM:SS format
	\T		the current time in 12-hour HH:MM:SS format
	\@		the current time in 12-hour am/pm format
	\A		the current time in 24-hour HH:MM format
	\u		the username of the current user
	\v		the version of bash (e.g., 2.00)
	\V		the release of bash, version + patch level (e.g., 2.00.0)
	\w		the current working directory, with $HOME abbreviated with a tilde
	\W		the basename of the current working directory, with $HOME
			 abbreviated with a tilde
	\!		the history number of this command
	\#		the command number of this command
	\$		if the effective UID is 0, a #, otherwise a $
	
nn		the character corresponding to the octal number nnn
	\\		a backslash
	\[		begin a sequence of non-printing characters, which could be used
			  to embed a terminal control sequence into the prompt
	\]		end a sequence of non-printing characters

	The command number and the history number are usually different:
	the history number of a command is its position in the history
	list, which may include commands restored from the history file
	(see HISTORY below), while the command number is the position in
	the sequence of commands executed during the current shell session.
	After the string is decoded, it is expanded via parameter
	expansion, command substitution, arithmetic expansion, and quote
	removal, subject to the value of the promptvars shell option (see
	the description of the shopt command under SHELL BUILTIN COMMANDS
	below).
```

### Позиционирование курсора

Эта последовательность устанавливает позицию курсора:

 `\[\033[<row>;<column>f\]` 

Текущая позиция может быть сохранена так:

 `\[\033[s\]` 

Чтобы восстановить позицию, используйте:

 `\[\033[u\]` 

Следующий пример использует эти последовательности, чтобы отображать время в правом верхнем углу:

 `PS1=">\[\033[s\]\[\033[1;\$((COLUMNS-5))f\]\$(date +%H:%M)\[\033[u\]"` 

Переменная окружения *COLUMNS* содержит число столбцов в терминале. В примере выше из этого значения отнимается *5*, чтобы выровнять 5-символьный вывод команды `date` по правому краю.

### Отображение кода возврата

Используйте следующий промпт, чтобы видеть какое значение вернула последняя команда:

0 ;) : true
0 ;) : false
1 ;( :

```
#return value visualisation
PS1="\$? \$(if [[ \$? == 0 ]]; then echo \"\[\033[0;32m\];)\"; else echo \"\[\033[0;31m\];(\"; fi)\[\033[00m\] : "
```

*Ноль* - зелёный смайлик, а *не ноль* - красный. Таким образом, ваше приглашение будет со смайликом, если последняя операция была успешной.

Но вы возможно также захотите использовать имя пользователя и хоста, например так:

0 ;) andy@alba ~ $ true
0 ;) andy@alba ~ $ false
1 ;( andy@alba ~ $ _

```
#return value visualisation
PS1="\[\033[01;37m\]\$? \$(if [[ \$? == 0 ]]; then echo \"\[\033[01;32m\];)\"; else echo \"\[\033[01;31m\];(\"; fi) $(if [[ ${EUID} == 0 ]]; then echo '\[\033[01;31m\]\h'; else echo '\[\033[01;32m\]\u@\h'; fi)\[\033[01;34m\] \w \$\[\033[00m\] "
```

Или, если вы хотите создать ваш промпт с использованием юникод-символа ✓ для статуса *ноль* и юникод-символ ✗ для статуса *не ноль*:

0 ✓ andy@alba ~ $ true
0 ✓ andy@alba ~ $ false
1 ✗ andy@alba ~ $ I\ will\ try\ to\ type\ a\ wrong\ command...
bash: I will try to type a wrong command...: command not found
127 ✗ andy@alba ~ $ _

```
#return value visualisation
PS1="\[\033[01;37m\]\$? \$(if [[ \$? == 0 ]]; then echo \"\[\033[01;32m\]\342\234\223\"; else echo \"\[\033[01;31m\]\342\234\227\"; fi) $(if [[ ${EUID} == 0 ]]; then echo '\[\033[01;31m\]\h'; else echo '\[\033[01;32m\]\u@\h'; fi)\[\033[01;34m\] \w \$\[\033[00m\] "
```

Альтернативно, это можно сделать более [читабельно](http://stackoverflow.com/a/22362727/1821548) при помощи `PROMPT_COMMAND`:

```
set_prompt () {
    Last_Command=$? # Must come first!
    Blue='\[\e[01;34m\]'
    White='\[\e[01;37m\]'
    Red='\[\e[01;31m\]'
    Green='\[\e[01;32m\]'
    Reset='\[\e[00m\]'
    FancyX='\342\234\227'
    Checkmark='\342\234\223'

    # Add a bright white exit status for the last command
    PS1="$White\$? "
    # If it was successful, print a green check mark. Otherwise, print
    # a red X.
    if [[ $Last_Command == 0 ]]; then
        PS1+="$Green$Checkmark "
    else
        PS1+="$Red$FancyX "
    fi
    # If root, just print the host in red. Otherwise, print the current user
    # and host in green.
    if [[ $EUID == 0 ]]; then
        PS1+="$Red\\h "
    else
        PS1+="$Green\\u@\\h "
    fi
    # Print the working directory and prompt marker in blue, and reset
    # the text color to the default.
    PS1+="$Blue\\w \\\$$Reset "
}
PROMPT_COMMAND='set_prompt'
```

Вот пример, который показывает статус ошибки только в случае *не нулевого* статуса:

```
PROMPT_COMMAND='es=$?; [[ $es -eq 0 ]] && unset error || error=$(echo -e "\e[1;41m $es \e[40m")'
PS1="${error} ${PS1}"
```

## Советы и подсказки

### Разные цвета при вводе текста и при выводе

Если вы не сбросили цвет текста в конце вашего промпта, то этим цветом будут отображаться как текст который вы вводите, так и текст консоли. Если вы хотите задать определённый цвет для ввода, но при этом чтобы цвет вывода команд остался по умолчанию, вам нужно будет сбросить цвет после нажатия `Enter`, но до того, как какая-либо команда будет запущена. Вы можете сделать это установив DEBUG trap, например так:

 `~/.bashrc`  `trap 'printf "\e[0m" "$_"' DEBUG` 

### Случайные цитаты при входе

Для коричневого приглашения [Fortune](/index.php/Fortune "Fortune") добавьте:

 `~/.bashrc` 
```
[[ "$PS1" ]] && echo -e "\e[00;33m$(/usr/bin/fortune)\e[00m"

```

### Раскрашенные последние новости Arch при входе

Чтобы читать 10 latestпоследних пунктов новостей с [Arch official website](https://www.archlinux.org/news/), пользователь [grufo](https://aur.archlinux.org/account.php?Action=AccountInfo&ID=33208) [написал](https://bbs.archlinux.org/viewtopic.php?id=146850) маленький и цветной скрипт для извлечения RSS (*scrollable*):

   :: Arch Linux: Recent news updates ::
 [ https://www.archlinux.org/news/ ]

The latest and greatest news from the Arch Linux distribution.

 en-us Sun, 04 Nov 2012 16:09:46 +0000

   :: End of initscripts support ::
 [ https://www.archlinux.org/news/end-of-initscripts-support/ ]

Tom Gundersen wrote:
As systemd is now the default init system, Arch Linux is receiving minimal testing on initscripts systems. Due to a lack of resources and interest, we are unlikely to work on fixing initscripts-specific bugs, and may close them as WONTFIX.
We therefore strongly encourage all users to migrate to systemd as soon as possible. See the systemd migration guide [ https://wiki.archlinux.org/index.php/Systemd ].
To ease the transition, initscripts support will remain in the official repositories for the time being, unless otherwise stated. As of January 2013, we will start removing initscripts support (e.g., rc scripts) from individual packages without further notice.

 Tom Gundersen Sun, 04 Nov 2012 16:09:46 +0000 tag:www.archlinux.org,2012-11-04:/news/end-of-initscripts-support/

   :: November release of install media available ::
 [ https://www.archlinux.org/news/november-release-of-install-media-available/ ]

Pierre Schmitz wrote:
The latest snapshot of our install and rescue media can be found on our Download [ https://www.archlinux.org/download/ ] page. The 2012.11.01 ISO image mainly contains minor bug fixes, cleanups and new packages compared to the previous one:
 * First media with Linux 3.6
 * copytoram=n can be used to not copy the image to RAM on network boot. This is probably unreliable but an option for systems with very low memory.
 * cowfile_size boot parameter mainly for persistent COW on VFAT. See the README [ https://projects.archlinux.org/archiso.git/plain/docs/README.bootparams?id=v4 ] file for details.

 Pierre Schmitz Fri, 02 Nov 2012 17:54:15 +0000 tag:www.archlinux.org,2012-11-02:/news/november-release-of-install-media-available/

   :: Bug Squashing Day: Saturday 17th November ::
 [ https://www.archlinux.org/news/bug-squashing-day-saturday-17th-november/ ]

Allan McRae wrote:
The number of bugs in the Arch Linux bug tracker is creeping up so it is time for some extermination.
This is a great way for the community to get involved and help the Arch Linux team. The process is simple. First look at a bug for your favorite piece of software in the bug tracker and check if it still occurs. If it does, check the upstream project for a fix and test it to confirm it works. If there is no fix available, make sure the bug has been filed in the upstream tracker.
Join us on the #archlinux-bugs IRC channel. We are spread across timezones, so people should be around all day.

 Allan McRae Thu, 01 Nov 2012 12:28:51 +0000 tag:www.archlinux.org,2012-11-01:/news/bug-squashing-day-saturday-17th-november/

   :: ConsoleKit replaced by logind ::
 [ https://www.archlinux.org/news/consolekit-replaced-by-logind/ ]

Allan McRae wrote:
With GNOME 3.6, polkit and networkmanager moving to [extra], ConsoleKit has now been removed from the repositories. Any package that previously depended on it now relies on systemd-logind instead. That means that the system must be booted with systemd to be fully functional.
In addition to GNOME, both KDE and XFCE are also affected by this change.

 Allan McRae Tue, 30 Oct 2012 22:17:39 +0000 tag:www.archlinux.org,2012-10-30:/news/consolekit-replaced-by-logind/

   :: systemd is now the default on new installations ::
 [ https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/ ]

Thomas Bächler wrote:
The base group now contains the systemd-sysvcompat package. This means that all new installations will boot with systemd by default.
As some packages still lack native systemd units, users can install the initscripts package and use the DAEMONS array in /etc/rc.conf to start services using the legacy rc.d scripts.
This change does not affect existing installations. For the time being, the initscripts and sysvinit packages remain available from our repositories. However, individual packages may now start relying on the system being booted with systemd.
Please refer to the wiki [ https://wiki.archlinux.org/index.php/Systemd ] for how to transition an existing installation to systemd.

 Thomas Bächler Sat, 13 Oct 2012 09:29:38 +0000 tag:www.archlinux.org,2012-10-13:/news/systemd-is-now-the-default-on-new-installations/

   :: Install medium 2012.10.06 introduces systemd ::
 [ https://www.archlinux.org/news/install-medium-20121006-introduces-systemd/ ]

Pierre Schmitz wrote:
The October release of the Arch Linux install medium is available for Download [ https://www.archlinux.org/download/ ] and can be used for new installs or as a rescue system. It contains a set of updated packages and the following notable changes:
 * systemd is used to boot up the live system.
 * initscripts are no longer available on the live system but are still installed by default on the target system. This is likely to change in the near future.
 * EFI boot and setup has been simplified.
 * gummiboot is used to display a menu on EFI systems.
 * The following new packages are available on the live system: ethtool, fsarchiver, gummiboot-efi, mc, partclone, partimage, refind-efi, rfkill, sudo, testdisk, wget, xl2tpd

 Pierre Schmitz Sun, 07 Oct 2012 16:58:03 +0000 tag:www.archlinux.org,2012-10-07:/news/install-medium-20121006-introduces-systemd/

   :: New install medium 2012.09.07 ::
 [ https://www.archlinux.org/news/new-install-medium-20120907/ ]

Pierre Schmitz wrote:
As is customary by now there is a new install medium available at the beginning of this month. The live system can be downloaded from Download [ https://www.archlinux.org/download/ ] and be used for new installs or as a rescue system.
In addition to a couple of updated packages and bug fixes the following changes stand out:
 * First medium with Linux 3.5 (3.5.3)
 * The script boot parameter works again (FS#31022 [ https://bugs.archlinux.org/task/31022 ])
 * When booting via PXE and NFS or NBD the ISO will be copied to RAM to ensure a more stable usage.
 * The live medium contains usb_modeswitch and wvdial which e.g. allows to establish a network connection using an UMTS USB dongle
 * Furthermore the newest versions of initscripts, systemd and netcfg are included.

 Pierre Schmitz Sat, 08 Sep 2012 09:48:52 +0000 tag:www.archlinux.org,2012-09-08:/news/new-install-medium-20120907/

   :: Fontconfig 2.10.1 update - manual intervention required ::
 [ https://www.archlinux.org/news/fontconfig-2101-update-manual-intervention-required/ ]

Andreas Radke wrote:
The fontconfig 2.10.1 update overwrites symlinks created by the former package version. These symlinks need to be removed before the update:

rm /etc/fonts/conf.d/20-unhint-small-vera.conf
rm /etc/fonts/conf.d/20-fix-globaladvance.conf
rm /etc/fonts/conf.d/29-replace-bitmap-fonts.conf
rm /etc/fonts/conf.d/30-metric-aliases.conf
rm /etc/fonts/conf.d/30-urw-aliases.conf
rm /etc/fonts/conf.d/40-nonlatin.conf
rm /etc/fonts/conf.d/45-latin.conf
rm /etc/fonts/conf.d/49-sansserif.conf
rm /etc/fonts/conf.d/50-user.conf
rm /etc/fonts/conf.d/51-local.conf
rm /etc/fonts/conf.d/60-latin.conf
rm /etc/fonts/conf.d/65-fonts-persian.conf
rm /etc/fonts/conf.d/65-nonlatin.conf
rm /etc/fonts/conf.d/69-unifont.conf
rm /etc/fonts/conf.d/80-delicious.conf
rm /etc/fonts/conf.d/90-synthetic.conf
pacman -Syu fontconfig

Main systemwide configuration should be done by symlinks (especially for autohinting, sub-pixel and lcdfilter):

cd /etc/fonts/conf.d
ln -s ../conf.avail/XX-foo.conf

Also check Font Configuration [ https://wiki.archlinux.org/index.php/Font_Configuration ] and Fonts [ https://wiki.archlinux.org/index.php/Fonts ].

 Andreas Radke Thu, 06 Sep 2012 13:54:23 +0000 tag:www.archlinux.org,2012-09-06:/news/fontconfig-2101-update-manual-intervention-required/

   :: netcfg-2.8.9 drops deprecated rc.conf compatibility ::
 [ https://www.archlinux.org/news/netcfg-289-drops-initscripts-compatibility/ ]

Florian Pritz wrote:
Users of netcfg should configure all interfaces in /etc/conf.d/netcfg rather than /etc/rc.conf.

 Florian Pritz Sat, 11 Aug 2012 20:00:02 +0000 tag:www.archlinux.org,2012-08-11:/news/netcfg-289-drops-initscripts-compatibility/

   :: Install media 2012.08.04 available ::
 [ https://www.archlinux.org/news/install-media-20120804-available/ ]

Pierre Schmitz wrote:
The August snapshot of our live and install media comes with updated packages and the following changes on top of the previous ISO image [ /news/install-media-20120715-released/ ]:
 * GRUB 2.0 instead of the legacy 0.9 version is available.
 * The Installation Guide [ https://wiki.archlinux.org/index.php/Installation_Guide ] can be found at /root/install.txt.
 * ZSH with Grml's configuration [ http://grml.org/zsh/ ] is used as interactive shell to provide a user friendly and more convenient environment. This includes completion support for pacstrap, arch-chroot, pacman and most other tools.
 * The network daemon is started by default which will automatically setup your network if DHCP is available.
Note that all these changes only affect the live system and not the base system you install using pacstrap. The ISO image can be downloaded from our download page [ /download/ ]. The next snapshot is scheduled for September.

 Pierre Schmitz Sat, 04 Aug 2012 17:24:30 +0000 tag:www.archlinux.org,2012-08-04:/news/install-media-20120804-available/

andy@alba _
 `~/.bashrc` 
```
# Arch latest news
if [ "$PS1" ] && [[ $(ping -c1 www.google.com 2>&-) ]]; then
	# The characters "£, §" are used as metacharacters. They should not be encountered in a feed...
	echo -e "$(echo $(curl --silent https://www.archlinux.org/feeds/news/ | sed -e ':a;N;$!ba;s/
/ /g') | \
		sed -e 's/&amp;/\&/g
		s/&lt;\|&#60;/</g
		s/&gt;\|&#62;/>/g
		s/<\/a>/£/g
		s/href\=\"/§/g
		s/<title>/\
\
\
   :: \\e[01;31m/g; s/<\/title>/\\e[00m ::\
/g
		s/<link>/ [ \\e[01;36m/g; s/<\/link>/\\e[00m ]/g
		s/<description>/\
\
\\e[00;37m/g; s/<\/description>/\\e[00m\
\
/g
		s/<p\( [^>]*\)\?>\|<br\s*\/\?>/
/g
		s/<b\( [^>]*\)\?>\|<strong\( [^>]*\)\?>/\\e[01;30m/g; s/<\/b>\|<\/strong>/\\e[00;37m/g
		s/<i\( [^>]*\)\?>\|<em\( [^>]*\)\?>/\\e[41;37m/g; s/<\/i>\|<\/em>/\\e[00;37m/g
		s/<u\( [^>]*\)\?>/\\e[4;37m/g; s/<\/u>/\\e[00;37m/g
		s/<code\( [^>]*\)\?>/\\e[00m/g; s/<\/code>/\\e[00;37m/g
		s/<a[^§|t]*§\([^\"]*\)\"[^>]*>\([^£]*\)[^£]*£/\\e[01;31m\2\\e[00;37m \\e[01;34m[\\e[00;37m \\e[04m\1\\e[00;37m\\e[01;34m ]\\e[00;37m/g
		s/<li\( [^>]*\)\?>/
 \\e[01;34m*\\e[00;37m /g
		s/<!\[CDATA\[\|\]\]>//g
		s/\|>\s*<//g
		s/ *<[^>]\+> */ /g
		s/[<>£§]//g')

";
fi
```

Чтобы получить только самую последнюю новость, воспользуйтесь этим:

```
# Arch latest news
if [ "$PS1" ] && [[ $(ping -c1 www.google.com 2>&-) ]]; then
	# The characters "£, §" are used as metacharacters. They should not be encountered in a feed...
	echo -e "$(echo $(curl --silent https://www.archlinux.org/feeds/news/ | awk ' NR == 1 {while ($0 !~ /<\/item>/) {print;getline} sub(/<\/item>.*/,"</item>") ;print}' | sed -e ':a;N;$!ba;s/
/ /g') | \
		sed -e 's/&amp;/\&/g
		s/&lt;\|&#60;/</g
		s/&gt;\|&#62;/>/g
		s/<\/a>/£/g
		s/href\=\"/§/g
		s/<title>/\
\
\
   :: \\e[01;31m/g; s/<\/title>/\\e[00m ::\
/g
		s/<link>/ [ \\e[01;36m/g; s/<\/link>/\\e[00m ]/g
		s/<description>/\
\
\\e[00;37m/g; s/<\/description>/\\e[00m\
\
/g
		s/<p\( [^>]*\)\?>\|<br\s*\/\?>/
/g
		s/<b\( [^>]*\)\?>\|<strong\( [^>]*\)\?>/\\e[01;30m/g; s/<\/b>\|<\/strong>/\\e[00;37m/g
		s/<i\( [^>]*\)\?>\|<em\( [^>]*\)\?>/\\e[41;37m/g; s/<\/i>\|<\/em>/\\e[00;37m/g
		s/<u\( [^>]*\)\?>/\\e[4;37m/g; s/<\/u>/\\e[00;37m/g
		s/<code\( [^>]*\)\?>/\\e[00m/g; s/<\/code>/\\e[00;37m/g
		s/<a[^§|t]*§\([^\"]*\)\"[^>]*>\([^£]*\)[^£]*£/\\e[01;31m\2\\e[00;37m \\e[01;34m[\\e[00;37m \\e[04m\1\\e[00;37m\\e[01;34m ]\\e[00;37m/g
		s/<li\( [^>]*\)\?>/
 \\e[01;34m*\\e[00;37m /g
		s/<!\[CDATA\[\|\]\]>//g
		s/\|>\s*<//g
		s/ *<[^>]\+> */ /g
		s/[<>£§]//g')

";
fi
```

### Просмотр цветов

Страница по адресу [http://ascii-table.com/ansi-escape-sequences.php](http://ascii-table.com/ansi-escape-sequences.php) описывает некоторые доступные цветовые последовательности. Следующая Bash функция отображает таблицу с готовыми к копированию управляющими кодами.

 `~/.bashrc` 
```
colors() {
	local fgc bgc vals seq0

	printf "Color escapes are %s
" '\e[${value};...;${value}m'
	printf "Values 30..37 are \e[33mforeground colors\e[m
"
	printf "Values 40..47 are \e[43mbackground colors\e[m
"
	printf "Value  1 gives a  \e[1mbold-faced look\e[m

"

	# foreground colors
	for fgc in {30..37}; do
		# background colors
		for bgc in {40..47}; do
			fgc=${fgc#37} # white
			bgc=${bgc#40} # black

			vals="${fgc:+$fgc;}${bgc}"
			vals=${vals%%;}

			seq0="${vals:+\e[${vals}m}"
			printf "  %-9s" "${seq0:-(default)}"
			printf " ${seq0}TEXT\e[m"
			printf " \e[${vals:+${vals+$vals;}}1mBOLD\e[m"
		done
		echo; echo
	done
}

```

### Раскрашенное git приглашение

Укажите `/usr/share/git/completion/git-prompt.sh` вашему шеллу:

 `~/.bashrc` 
```
source /usr/share/git/completion/git-prompt.sh

```

и используйте `__git_ps1` внутри `PS1` или `PROMPT_COMMAND`. Смотрите [Don't Reinvent the Wheel](http://ithaca.arpinum.org/2013/01/02/git-prompt.html) для подробностей.

### Раскрашенные существующие бесцветные приглашения

Добавьте в свой `~/.bashrc`:

 `~/.bashrc` 
```
# Colorize prompts
for i in {1..4}; do
	PSi="PS$i"
	export $PSi="\[\e[1;37m\]${!PSi}\[\e[0m\]"
done
unset PSi
unset i

```

## Смотрите также

*   Community examples and screenshots in the Forum thread: [What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885)
*   The original *not modified* Gentoo's `/etc/bash.bashrc` file can be found [here](http://www.jeremysands.com/archlinux/gentoo-bashrc-2008.0). See also the [gentoo-bashrc](https://aur.archlinux.org/packages/gentoo-bashrc/) package from [AUR](/index.php/AUR "AUR").
*   tput(1)
    *   [tput reference on bash-hackers.org](http://wiki.bash-hackers.org/scripting/terminalcodes)
    *   [Colours and Cursor Movement With tput](http://tldp.org/HOWTO/Bash-Prompt-HOWTO/x405.html)
*   [Nice Xresources color schemes collection](http://xcolors.net/)
*   [Bash Prompt HOWTO](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)
*   [Giles Orr's collection of sample prompts](http://gilesorr.com/bashprompt/prompts/index.html)
*   [Bash tips: Colors and formatting](http://misc.flogisoft.com/bash/tip_colors_and_formatting)