**Readline** - это библиотека, созданная [GNU Project](/index.php/GNU_Project "GNU Project"), используемая [Bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)") и другими программами с интерфейсом CLI для того, чтобы взаимодействовать с командной строкой. Перед прочтением этой статьи пожалуйста ознакомьтесь с домашней [страницей](http://www.gnu.org/s/readline/) проекта, т.к. здесь размещена только общая информация.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Редактирование в командной строке](#Редактирование_в_командной_строке)
    *   [2.1 Индикатор режима при вводе](#Индикатор_режима_при_вводе)
    *   [2.2 Различные формы курсора для каждого из режимов](#Различные_формы_курсора_для_каждого_из_режимов)
*   [3 История команд](#История_команд)
    *   [3.1 Поиск по истории](#Поиск_по_истории)
        *   [3.1.1 Избежание повторов](#Избежание_повторов)
        *   [3.1.2 Удаление пробелов в начале строки](#Удаление_пробелов_в_начале_строки)
*   [4 Макросы](#Макросы)
*   [5 Советы и хитрости](#Советы_и_хитрости)
    *   [5.1 Отключение ^C](#Отключение_^C)

## Установка

Пакет [readline](https://www.archlinux.org/packages/?name=readline), скорее всего, уже установлен как зависимость [Bash](/index.php/Bash "Bash")

## Редактирование в командной строке

По умолчанию Readline использует стиль сокращений Emacs для взаимодействия с командной строкой. Однако стиль редактирования [vi](/index.php/Vi "Vi") также поддерживается. Для включения сочетаний клавиш в стиле [vi](/index.php/Vi "Vi"):

 `~/.inputrc`  ` set editing-mode vi` 

Чтобы включить такой режим только для [Bash](/index.php/Bash "Bash"):

 `~/.bashrc`  ` set -o vi` 

### Индикатор режима при вводе

Имеется два режима редактирования vi - командый и вставочный. Вы можете включить отображение текущего режима:

 `~/.inputrc` 
```
set show-mode-in-prompt on

```

Команда выше отображает строчку в вводе (по умолчанию `(cmd)`/`(ins)`). Ее можно отредактировать посредством переменных `vi-ins-mode-string` и `vi-cmd-mode-string`.

### Различные формы курсора для каждого из режимов

Вы можете установить различную форму курсора для каждого мода, используя ["\1 .. \2" escapes](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html#index-vi_002dcmd_002dmode_002dstring):

 `~/.inputrc` 
```
set vi-ins-mode-string \1\e[6 q\2
set vi-cmd-mode-string \1\e[2 q\2

```

This will set a block shaped cursor when in command mode and a pipe cursor when in insert mode.

The Virtual Console uses different escape codes, so you should check first which term is being used:

 `~/.inputrc` 
```
$if term=linux
	set vi-ins-mode-string \1\e[?0c\2
	set vi-cmd-mode-string \1\e[?8c\2
$else
	set vi-ins-mode-string \1\e[6 q\2
	set vi-cmd-mode-string \1\e[2 q\2
$endif
```

See [software cursor for VGA](https://www.kernel.org/doc/Documentation/admin-guide/vga-softcursor.rst) for further details.

## История команд

Обычно при нажатии кнопки "стрелка вверх", в приглашение командной строки подставляется последняя введенная команда вне зависимости от того, что набрал пользователь в момент нажатия. Однако, некоторые пользователи предпочитают, чтобы нажатие кнопки "стрелка вверх" вызывало список только тех команд, которые подходят к тому, что они набрали в момент нажатия.

Например, если пользователь вводил следующие команды:

*   `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`
*   `who`
*   `mount`
*   `man mount`

В данной ситуации, набрав `ls` и нажав клавишу "стрелка вверх", введенный текст будет заменен на `man mount`, то есть на последнюю выполненную команду. Если включен поиск по истории, будут показаны только последние команды, начинающиеся на `ls` (текущий введенный текст), в нашем случае - `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`.

Вы можете включить поиск по истории, добавив следующие строки в `/etc/inputrc` или `~/.inputrc`:

```
"\e[A":history-search-backward
"\e[B":history-search-forward

```

Если вы пользуетесь режимом vi, добавьте следующие строки в `~/.inputrc` (из [этого поста](https://bbs.archlinux.org/viewtopic.php?pid=428760#p428760)):

```
set editing-mode vi
$if mode=vi
set keymap vi-command
# these are for vi-command mode
"\e[A": history-search-backward
"\e[B": history-search-forward
set keymap vi-insert
# these are for vi-insert mode
"\e[A": history-search-backward
"\e[B": history-search-forward
$endif

```

Также рекомендуется добавить следующую строка в начало файла `~/.inputrc`, если вы хотите избежать странных вещей вроде [этой](https://bbs.archlinux.org/viewtopic.php?id=112537):

```
$include /etc/inputrc

```

В качестве альтернативы можно использовать реверсивную историю поиска путем нажатия `Ctrl+R`. Реверсивная история поиска основана не на предыдущем вводе, а вместо этого ищет в буфере истории команд те, которые похожи на текущий ввод. Повторное нажатие `Ctrl+R` в этом режиме отобразит предыдущую строку из буфера, которая подходит под текущее условие поиска, а нажатие `Ctrl+G` отменит поиск и вернет текущую введенную строку. Таким образом, чтобы выполнить поиск среди ранее введенных команд `mount`, нажмите `Ctrl+R`, введите 'mount' и продолжайте нажимать `Ctrl+R` до тех пор, пока не отобразится нужная вам строка.

Обратный эквивалент этого режима называется forward-search-history и по умолчанию привязан к `Ctrl+S`. Имейте в виду, что большинство эмуляторов терминала переназначает комбинацию `Ctrl+S` на приостановку текущей задачи до нажатия `Ctrl+Q` (так называемый контроль потока XON/XOF). Для активации forward-search-history/деактивации контроля потока выполните:

```
$ stty -ixon

```

либо переназначьте комбинацию клавиш в `inputrc`, например, на `Alt+S`, которая ничем не занята по умолчанию:

```
"\es":forward-search-history

```

### Поиск по истории

#### Избежание повторов

Если вы несколько раз повторяете ввод одной и той же команды, она запишется в историю ввода несколько раз. Чтобы избежать этого, добавьте в `~/.bashrc`:

```
export HISTCONTROL=ignoredups

```

#### Удаление пробелов в начале строки

Чтобы отключить запись в историю команд строк, начинающихся с пробелов, добавьте в `~/.bashrc`:

```
export HISTCONTROL=ignorespace

```

Если `~/.bashrc` уже содержит

```
export HISTCONTROL=ignoredups

```

замените строку на:

```
export HISTCONTROL=ignoreboth

```

## Макросы

В Readline также реализована поддержка назначения клавиш на клавиатурные макросы. Вот простой пример, запустите эту команду в Bash:

```
bind '"\ew":"\C-e # macro"'

```

Или добавьте ее часть в inputrc:

```
"\ew":"\C-e # macro"

```

Теперь наберите команду и нажмите `Alt`+`W`. Readline отреагирует на это, как если бы была нажата комбинация `Ctrl+E` (end-of-line, конец строки).

Используйте любые сочетания клавиш с макросами Readline для автоматизации часто используемых задач. Например, такой макрос при нажатии `Ctrl+Alt+L` добавляет к строке " | less" и запускает команду (`Ctrl+M` is equivalent to `Enter`):

```
"\e\C-l":"\C-e | less\C-m"

```

Следующий макрос добавляет в начало команды "yes | " при нажатии `Ctrl+Alt+Y` для того, чтобы согласиться на любой вопрос "yes/no", задаваемый командой:

```
"\e\C-y":"\C-ayes | \C-m"

```

Этот пример разрывает строку на `su -c ''`, если была нажата комбинация `Alt+S`:

```
"\es":"\C-a su -c '\C-e'\C-m"

```

Следующий пример добавляет в начало команды `sudo` при нажатии `Alt+S`. Она безопаснее, т.к. не передает нажатие клавиши {{ic|Enter}.

```
"\es":"\C-asudo \C-e"

```

В последнем примере показано, как быстро отправить команду на выполнение в бэкграунд используя сочетание `Ctrl+Alt+B` и игнорируя весь ее вывод:

```
"\e\C-b":"\C-e > /dev/null 2>&1 &\C-m"

```

## Советы и хитрости

### Отключение ^C

После обновления [readline](https://www.archlinux.org/packages/?name=readline) терминал выводит на экран `^C` после нажатия `Ctrl+C`. Если вы хотите отключить это, просто добавьте следующую строку в `~/.inputrc`:

```
set echo-control-characters off

```