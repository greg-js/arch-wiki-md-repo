**Bash** (Bourne-again Shell) - это [оболочка командной строки](/index.php/Command-line_shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Command-line shell (Русский)")/язык программирования, созданная [GNU Project](/index.php/GNU_Project "GNU Project"). Название является отсылкой к предшественнику - давно устаревшей Bourne shell. Bash можно запустить на большинстве UNIX-like систем, включая GNU/Linux.

## Contents

*   [1 Обращение к Bash](#.D0.9E.D0.B1.D1.80.D0.B0.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA_Bash)
    *   [1.1 Конфигурационные файлы](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B)
    *   [1.2 Оболочка и переменные окружения](#.D0.9E.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B0_.D0.B8_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [2 Командная строка](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.B0.D1.8F_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B0)
    *   [2.1 Автодополнение (клавиша Tab)](#.D0.90.D0.B2.D1.82.D0.BE.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.28.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B0_Tab.29)
        *   [2.1.1 Однократное нажатие Tab](#.D0.9E.D0.B4.D0.BD.D0.BE.D0.BA.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B5_.D0.BD.D0.B0.D0.B6.D0.B0.D1.82.D0.B8.D0.B5_Tab)
        *   [2.1.2 Дополнительные программы и опции](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B_.D0.B8_.D0.BE.D0.BF.D1.86.D0.B8.D0.B8)
        *   [2.1.3 Настройка автодополнения вручную](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B0.D0.B2.D1.82.D0.BE.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
    *   [2.2 История команд](#.D0.98.D1.81.D1.82.D0.BE.D1.80.D0.B8.D1.8F_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4)
    *   [2.3 Быстрый переход между словами при помощи клавиши Ctrl](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9_.D0.BF.D0.B5.D1.80.D0.B5.D1.85.D0.BE.D0.B4_.D0.BC.D0.B5.D0.B6.D0.B4.D1.83_.D1.81.D0.BB.D0.BE.D0.B2.D0.B0.D0.BC.D0.B8_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_Ctrl)
    *   [2.4 Mimic Zsh run-help ability](#Mimic_Zsh_run-help_ability)
*   [3 Алиасы](#.D0.90.D0.BB.D0.B8.D0.B0.D1.81.D1.8B)
*   [4 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [4.1 Кастомизация приглашения командной строки](#.D0.9A.D0.B0.D1.81.D1.82.D0.BE.D0.BC.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D0.BF.D1.80.D0.B8.D0.B3.D0.BB.D0.B0.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8)
        *   [4.1.1 Кастомизация заголовка](#.D0.9A.D0.B0.D1.81.D1.82.D0.BE.D0.BC.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D0.B7.D0.B0.D0.B3.D0.BE.D0.BB.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [4.2 Команда не найдена (AUR)](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.B0_.D0.BD.D0.B5_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD.D0.B0_.28AUR.29)
    *   [4.3 Отключение Ctrl-z в терминале](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_Ctrl-z_.D0.B2_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B5)
    *   [4.4 Очистка экрана после выхода из системы](#.D0.9E.D1.87.D0.B8.D1.81.D1.82.D0.BA.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B0_.D0.B8.D0.B7_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [4.5 Автоматическая смена директории (cd) при вводе только пути](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D1.81.D0.BC.D0.B5.D0.BD.D0.B0_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B8_.28cd.29_.D0.BF.D1.80.D0.B8_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B5_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BF.D1.83.D1.82.D0.B8)
    *   [4.6 Autojump](#Autojump)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Перенос строк при изменении размера окна](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BD.D0.BE.D1.81_.D1.81.D1.82.D1.80.D0.BE.D0.BA_.D0.BF.D1.80.D0.B8_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B8_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.BE.D0.BA.D0.BD.D0.B0)
    *   [5.2 Происходит выход из оболочки даже при установленном ignoreof](#.D0.9F.D1.80.D0.BE.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D0.B8.D1.82_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4_.D0.B8.D0.B7_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8_.D0.B4.D0.B0.D0.B6.D0.B5_.D0.BF.D1.80.D0.B8_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.BC_ignoreof)
*   [6 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)
    *   [6.1 Туториалы](#.D0.A2.D1.83.D1.82.D0.BE.D1.80.D0.B8.D0.B0.D0.BB.D1.8B)
    *   [6.2 Сообщество](#.D0.A1.D0.BE.D0.BE.D0.B1.D1.89.D0.B5.D1.81.D1.82.D0.B2.D0.BE)
    *   [6.3 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)

## Обращение к Bash

Работа с Bash различается в зависимости от того каким образом она была вызвана. Далее приведены описания различных режимов работы с Bash.

Если Bash инициализирована командой `login` в терминале, службой (демоном) [SSH](/index.php/SSH "SSH") и т.п., она подразумевает под собой **login-оболочку** (оболочку авторизации). Этот режим также вызывается опциями `-l` или`--login` командной строки.

Bash является **interactive-оболочкой** (интерактивной оболочкой), если ее стандартные потоки ввода и ошибок направляются в терминал (например, когда запущен эмулятор терминала), а так же если она не запускается с параметром `-c` либо [аргументами без параметров](http://unix.stackexchange.com/a/96805) (например, `bash **script**`). Все interactive-оболочки берут данные из `/etc/bash.bashrc` и`~/.bashrc`, в то время, как login shells также ссылаются на `/etc/profile` и`~/.bash_profile`.

**Note:** В Arch Linux файл `/bin/sh` (который раньше был файлом запуска Bourne shell) символически ссылается на `/bin/bash`. Если Bash вызывается при помощи `sh`, Arch Linux пытается имитировать старый `sh`, включая совместимость с POSIX

### Конфигурационные файлы

Подробное описание см. [6.2 Bash Startup Files](http://www.gnu.org/software/bash/manual/bash.html#Bash-Startup-Files) и[DotFiles](http://mywiki.wooledge.org/DotFiles).

| Файл | Описание | Login-оболочки  | Interactive-оболочки (*non-login*) |
| `/etc/profile` | [Источник](/index.php?title=%D0%98%D1%81%D1%82%D0%BE%D1%87%D0%BD%D0%B8%D0%BA&action=edit&redlink=1 "Источник (page does not exist)")и настройки приложения в `/etc/profile.d/*.sh` и`/etc/bash.bashrc`. | Да | Нет |
| `~/.bash_profile` | Отдельно для каждого пользователя, после `/etc/profile`. Если этого файла не существует, идет обращение к `~/.bash_login` и `~/.profile` (в таком порядке). Файл-"рыба" `/etc/skel/.bash_profile` также берет данные из `~/.bashrc`. | Да | Нет |
| `~/.bash_logout` | После выхода из login-оболочки. | Да | Нет |
| `/etc/bash.bashrc` | Зависит от флага компиляции `-DSYS_BASHRC="/etc/bash.bashrc"`. Берет данные из `/usr/share/bash-completion/bash_completion`. | Нет | Да |
| `~/.bashrc` | Отдельно для каждого пользователя, после `/etc/bash.bashrc`. | Нет | Да |

**Note:**

*   Login-оболочки могут быть неинтерактивными (non-interactive), если вызываются при помощи аргумента `--login`..
*   Будучи интерактивными, *non-login*-оболочки **не** берут данные из `~/.bash_profile`, они по-прежнему наследуют окружение от родительских процессов (которые могут быть login-оболочками). См. [On processes, environments and inheritance](http://mywiki.wooledge.org/ProcessManagement#On_processes.2C_environments_and_inheritance) для получения дополнительной информации.

### Оболочка и переменные окружения

Поведение Bash, а так же программ, запущенных при помощи нее, может зависеть от целого ряда переменных окружения. [Переменные окружения](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "Переменные окружения") используются для хранения полезной информации, такой, как папки поиска для команды или браузер, который необходимо использовать. Когда запускается новый скрипт или оболочка, они наследуют родительские переменные окружения, таким образом, запускаясь с некоторым набором переменных оболочки [[1]](http://www.kingcomputerservices.com/unix_101/understanding_unix_shells_and_environment_variables.htm).

Переменные оболочки в Bash могут быть экспортированы в переменные окружения:

```
VARIABLE=content
export VARIABLE

```

Или с использованием сокращения:

```
export VARIABLE=content

```

Переменные окружения традиционно расположены в `~/.profile` или`/etc/profile`, таким образом, все bourne-совместимые оболочки могут их использовать.

См. [Переменные окружения](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "Переменные окружения") для более подробной информации.

## Командная строка

Командная строка Bash управляется отдельной библиотекой под названием [Readline](/index.php/Readline "Readline"). Readline позволяет использовать множество удобных действий с командной оболочкой, таких, как передвижение назад и вперед по словам, удаление слов и т.п. Так же Readline отвечает за [history](/index.php/Readline#History "Readline") историю введенных команд. Ну и, наконец, она позволяет вам создавать [macros](/index.php/Readline#Macros "Readline") макросы.

### Автодополнение (клавиша Tab)

[Wikipedia:Автодополнение](https://en.wikipedia.org/wiki/%D0%90%D0%B2%D1%82%D0%BE%D0%B4%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5 "wikipedia:Автодополнение") - это возможность автоматически заканчивать не полностью введенные команды путем нажатия клавиши `Tab` дважды (возможность присутствует по умолчанию).

#### Однократное нажатие Tab

For single press `Tab` results for when a partial or no completion is possible:

 `~/.inputrc` 
```
set show-all-if-ambiguous on

```

Alternatively, for results when no completion is possible:

 `~/.inputrc` 
```
set show-all-if-unmodified on

```

#### Дополнительные программы и опции

Bash изначально поддерживает автодополнение команд, имен файлов и переменных. Этот функционал может быть расширен при помощи пакета [bash-completion](https://www.archlinux.org/packages/?name=bash-completion); он расширяет возможности Bash, добавляя автодополнения для наиболее популярных команд и их параметров. С установленным пакетом [bash-completion](https://www.archlinux.org/packages/?name=bash-completion), однако, обычные автодополнения (такие, как `$ ls file.*<tab><tab>`) будут вести себя по-другому; но они могут быть возвращены в обычный режим при помощи `$ compopt -o bashdefault <prog>` (см.[[2]](https://bbs.archlinux.org/viewtopic.php?id=128471) и [[3]](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html) для дополнительной информации). Так же стоит отметить, что пакет [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) может существенно замедлить работу на старых системах.

#### Настройка автодополнения вручную

Для базовых команд используйте строки вида `complete -cf your_command` (это вызовет конфликт с настройками пакета [bash-completion](https://www.archlinux.org/packages/?name=bash-completion), если он установлен):

 `~/.bashrc` 
```
complete -cf sudo
complete -cf man

```

### История команд

Просмотр истории команд доступен по нажатию клавиш направления (вверх, вниз) (см: [Readline#History](/index.php/Readline#History "Readline") и[Readline Init File Syntax](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)):

 `~/.bashrc` 
```
 bind '"\e[A": history-search-backward'
 bind '"\e[B": history-search-forward'

```

или:

 `~/.inputrc` 
```
"\e[A": history-search-backward
"\e[B": history-search-forward

```

### Быстрый переход между словами при помощи клавиши Ctrl

[Xterm](/index.php/Xterm "Xterm") поддерживает переход между словами при помощи `Ctrl+Left` и`Ctrl+Right` [по умолчанию](http://stackoverflow.com/a/7783928). Для того, чтобы это заработало в других эмуляторах терминала, найдите нужные [коды терминала](http://wiki.bash-hackers.org/scripting/terminalcodes), и привяжите их к `backward-word` и `forward-word` в `~/.inputrc`. Коды можно посмотреть при помощи команды *cat*.

Пример для [urxvt](/index.php/Urxvt "Urxvt"):

 `~/.inputrc` 
```
"\eOd": backward-word
"\eOc": forward-word
```

### Mimic Zsh run-help ability

Zsh can invoke the manual for the written command pushing `Alt+h`. A similar behaviour is obtained in Bash by appending this line in your `inputrc` file:

 `/etc/inputrc` 
```
"\eh": "\C-a\eb\ed\C-y\e#man \C-y\C-m\C-p\C-p\C-a\C-d\C-e"

```

## Алиасы

[alias](https://en.wikipedia.org/wiki/Alias_(command) - это команда, которая позволяет заменить одним словом целую строку. Часто она используется для сокращения стандартных команд, а так же для добавления часто используемых аргументов к командам.

Созданные пользователем алиасы обычно хранятся в `~/.bashrc`, а общесистемные алиасы (доступные всем пользователям) - в `/etc/bash.bashrc`. См. примеры алиасов на [[4]](https://gist.github.com/anonymous/a9055e30f97bd19645c2) и [Pacman tips#Shortcuts](/index.php/Pacman_tips#Shortcuts "Pacman tips").

Для функций см.[Bash/Functions (Русский)](/index.php/Bash/Functions_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash/Functions (Русский)").

## Советы и хитрости

### Кастомизация приглашения командной строки

За приглашение командной строки Bash отвечает переменная окружения `$PS1`. Чтобы раскрасить приглашение Bash в разные цвета:

 `~/.bashrc` 
```
#PS1='[\u@\h \W]\$ '  # Закомментируйте значение по умолчанию
#DO NOT USE RAW ESCAPES, USE TPUT
reset=$(tput sgr0)
red=$(tput setaf 1)
blue=$(tput setaf 4)
green=$(tput setaf 2)

PS1='\[$red\]\u\[$reset\] \[$blue\]\w\[$reset\] \[$red\]\$ \[$reset\]\[$green\] '
```

Этот вариант `$PS1` полезен для приглашения командной строки root (красное обозначение и зеленый текст консоли). Символы `\[` и `\[` "оборачивают" непечатные символы для того, чтобы избежать неправильного отображения приглашения. Для дополнительной информации см.: [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt").

#### Кастомизация заголовка

Переменная `$PROMPT_COMMAND` позволяет запускать команду до приглашения командной строки. Например, такой вариант добавит в заголовок полный путь к текущей папке:

 `~/.bashrc` 
```
export PROMPT_COMMAND='echo -ne "\033]0;$PWD\007"'

```

А вот так можно изменить заголовок на имя последней запущенной команды и убедиться, что ваш файл истории команд всегда в актуальном состоянии:

 `~/.bashrc` 
```
export HISTCONTROL=ignoreboth
export HISTIGNORE='history*'
export PROMPT_COMMAND='history -a;echo -en "\e]2;";history 1|sed "s/^[ \t]*[0-9]\{1,\}  //g";echo -en "\e\\";'

```

### Команда не найдена (AUR)

[pkgfile](/index.php/Pkgfile "Pkgfile") включает хук "команда не найдена", который автоматически ищет в официальных источниках команды, похожие на ту, что не была распознана системой. Альтернативный хук "команда не найдена" имеется в репозитории AUR [command-not-found](https://aur.archlinux.org/packages/command-not-found/). пример использования:

 `$ abiword` 
```
The command 'abiword' is been provided by the following packages:
**abiword** (2.8.6-7) from extra
	[ abiword ]
**abiword** (2.8.6-7) from staging
	[ abiword ]
**abiword** (2.8.6-7) from testing
	[ abiword ]

```

Для автоматического запуска:

 `*~/.bashrc* or *~/.zshrc*` 
```
[ -r /etc/profile.d/cnf.sh ] && . /etc/profile.d/cnf.sh

```

### Отключение Ctrl-z в терминале

Вы можете отключить сочетание `Ctrl+z` (приостанавливает/закрывает текущую программу), например, так:

```
#!/bin/bash
trap "" 20
*adom*

```

Теперь, если вы случайно нажмете `Ctrl+z` в [adom](https://aur.archlinux.org/packages/adom/) вместо `Shift+z`, ничего не произойдет, потому что `Ctrl+z` будет проигнорировано.

### Очистка экрана после выхода из системы

Чтобы очистить экран после выхода из виртуального терминала:

 `~/.bash_logout` 
```
clear
reset

```

### Автоматическая смена директории (cd) при вводе только пути

Bash может автоматически подставлять `cd` при вводе только пути в командной строке. Например:

 `$ /etc` 
```
bash: /etc: Is a directory

```

Но после добавления одной строки в `.bashrc`:

 `~/.bashrc` 
```
...
shopt -s autocd
...

```

Вы получите:

```
[user@host ~]$ /etc
cd /etc
[user@host etc]$

```

### Autojump

[autojump](https://www.archlinux.org/packages/?name=autojump) позволяет перемещаться по файловой системе при помощи поиска строк в базе данных наиболее часто посещаемых пользователем путей.

После установки, файл `/etc/profile.d/autojump.bash` должен быть добавлен в [source](/index.php/Source "Source") для того, чтобы программа начала работать.

## Решение проблем

### Перенос строк при изменении размера окна

При изменении размера окна [terminal emulator](/index.php/Terminal_emulator "Terminal emulator"), Bash может не получить этот сигнал. Из-за этого введенный текст может неправильно перенестись и перекрыть собой приглашение командной строки. Опция командной строки `checkwinsize` проверяет размер окна при вводе каждой команды и, если это необходимо, обновляет значения переменных `LINES` и `COLUMNS`.

 `~/.bashrc` 
```
shopt -s checkwinsize

```

### Происходит выход из оболочки даже при установленном ignoreof

Если вы установили параметр `ignoreeof`, но повторное нажатие `ctrl-d` вызывает выход из оболочки, это происходит потому, что параметр ignoreof позволяет произвести только 10 последовательных нажатий этого сочетания клавиш (10 последовательных символов EOF, если быть точным) перед тем, как выйти из оболочки. Чтобы установить бОльшее значение, нужно использовать переменную IGNOREOF.

Например:

```
 export IGNOREEOF=100

```

## См. также

*   [Bash Reference](https://www.gnu.org/software/bash/manual/bashref.html)
*   [Bash manual page](https://www.gnu.org/software/bash/manual/bash.html)
*   [Readline Init File Syntax](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)
*   [The Bourne-Again Shell](http://www.aosabook.org/en/bash.html) - The third chapter of *The Architecture of Open Source Applications*
*   [Shellcheck](http://shellcheck.net) - Check bash scripts for common errors

### Туториалы

*   [BashGuide on Greg's Wiki](http://mywiki.wooledge.org/BashGuide)
*   [BashFAQ on Greg's Wiki](http://mywiki.wooledge.org/BashFAQ)
*   [Bash Hackers Wiki](http://wiki.bash-hackers.org/doku.php)
*   [Advanced Bash Scripting Guide](http://tldp.org/LDP/abs/html/)
*   [Quote Tutorial](http://www.grymoire.com/Unix/Quote.html)

### Сообщество

*   [An active and friendly IRC channel for Bash](irc://irc.freenode.net#bash)
*   [Bashscripts.org](http://bashscripts.org)

### Примеры

*   [How to change the title of an xterm](http://tldp.org/HOWTO/Xterm-Title-4.html)