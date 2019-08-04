**Состояние перевода:** На этой странице представлен перевод статьи [Fish](/index.php/Fish "Fish"). Дата последней синхронизации: 12 февраля 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Fish&diff=0&oldid=420178).

**fish** (**friendly interactive shell**, т.е. **дружелюбная интерактивная оболочка**) представляет собой удобную интерактивную оболочку командной строки предназначенную в основном для интерактивного использования.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Ввод/Вывод](#Ввод/Вывод)
    *   [2.1 Файловые дескрипторы](#Файловые_дескрипторы)
    *   [2.2 Перенаправление](#Перенаправление)
    *   [2.3 Пайпинг (piping)](#Пайпинг_(piping))
*   [3 Настройка](#Настройка)
    *   [3.1 Веб-интерфейс](#Веб-интерфейс)
    *   [3.2 Приглашение командной строки (Prompt)](#Приглашение_командной_строки_(Prompt))
    *   [3.3 Завершение команд](#Завершение_команд)
    *   [3.4 Совмещение /etc/profile и ~/.profile](#Совмещение_/etc/profile_и_~/.profile)
*   [4 Советы и хитрости](#Советы_и_хитрости)
    *   [4.1 История Замены](#История_Замены)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 Скрипты не совместимые с fish](#Скрипты_не_совместимые_с_fish)
    *   [5.2 su запускает Bash](#su_запускает_Bash)
    *   [5.3 Запуск X при входе в систему](#Запуск_X_при_входе_в_систему)
*   [6 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") пакет [fish](https://www.archlinux.org/packages/?name=fish) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Либо установите [fish-git](https://aur.archlinux.org/packages/fish-git/) версию пакета для разработки.

Для того чтобы сделать fish оболочкой по умолчанию, выполните `chsh -s /usr/bin/fish`.

## Ввод/Вывод

### Файловые дескрипторы

Как и другие оболочки fish позволяет перенаправлять потоки ввода/вывода. Это полезно при использовании текстовых файлов для сохранения вывода программы или ошибок, или при использовании текстовых файлов в качестве входных данных. Большинство программ использует три входных/выходных потока, представленные набором номеров файловых дескрипторов (file descriptors (FD)). Это:

*   Стандартный ввод (FD 0), используется для чтения (клавиатуры по умолчанию).
*   Стандартный вывод (FD 1), используется для записи (экран по умолчанию).
*   Стандартная ошибка (FD 2), используется для отображения ошибок и предупреждений (экран по умолчанию).

### Перенаправление

Любой файловый дескриптор может быть перенаправлен в другой файл механизмом называемым перенаправлением:

```
*Перенаправление стандартного ввода:*
$ команда < исходный файл

*Перенаправление стандартного вывода:*
$ команда > назначение

*Добавление стандартного вывода в существующий файл:*
$ команда >> назначение

*Перенаправление стандартной ошибки:*
$ команда ^ назначение

*Добавить стандартную ошибку в существующий файл:*
$ команда ^^ назначение
```

Вы можете использовать один из следующих `назначений`:

*   Имя файла (выход будет записан в указанный файл).
*   `&` за которым следует номер другого дескриптора файла. Выход будет написан на другой файловый дескриптор.
*   `&` с последующим знаком `-`. Выход не будет записан.

Примеры:

```
*Перенаправление стандартного выхода в файл:*
$ команда > файл_назначения.txt

*Перенаправление стандартного вывода и стандартной ошибки в тот же файл:*
$ команда > файл_назначения.txt ^ &1

*Отключение стандартного вывода:*
$ команда > &-
```

### Пайпинг (piping)

Вы можете перенаправить стандартный вывод одной команды на стандартный ввод следующей команды. Это делается путем разделения команд вертикальной чертой (`|`). Пример:

```
cat example.txt | head

```

Вы можете перенаправить другие файловые дескрипторы пайпингом (кроме стандартного вывода). Следующий пример показывает, как использовать стандартную ошибку из одной команды в качестве стандартного ввода другой команды, передавая номер файлового дескриптора стандартной ошибки в пайп `>`:

```
$ команда 2>| less

```

Это выполнит `команда` и перенаправить его стандартную ошибку в `less`.

## Настройка

`~/.config/fish/config.fish` это Файл пользовательских настроек fish. Добавьте команды или функции в файл, и он будет выполнять/определять их, когда откроете терминал. Похож на `.bashrc`.

### Веб-интерфейс

The fish prompt and terminal colors can be set with the interactive web interface:

```
fish_config

```

Selected settings are written to your personal configuration file. You can also view defined functions and your history.

### Приглашение командной строки (Prompt)

Если хотите чтобы fish отображал "branch" и "dirty status" когда находитесь в git каталоге, добавьте следующую строку в ваш `~/.config/fish/config.fish`:

```
# fish git prompt
set __fish_git_prompt_showdirtystate 'yes'
set __fish_git_prompt_showstashstate 'yes'
set __fish_git_prompt_showupstream 'yes'
set __fish_git_prompt_color_branch yellow

# Status Chars
set __fish_git_prompt_char_dirtystate '⚡'
set __fish_git_prompt_char_stagedstate '→'
set __fish_git_prompt_char_stashstate '↩'
set __fish_git_prompt_char_upstream_ahead '↑'
set __fish_git_prompt_char_upstream_behind '↓'

function fish_prompt
        set last_status $status
        set_color $fish_color_cwd
        printf '%s' (prompt_pwd)
        set_color normal
        printf '%s ' (__fish_git_prompt)
       set_color normal
end

```

### Завершение команд

fish может генерировать автодополнение из страниц руководства man. Completions are written to `~/.config/fish/generated_completions/` and can be generated by calling:

```
fish_update_completions

```

You can also define your own completions in `~/.config/fish/completions/`. See `/usr/share/fish/completions/` for a few examples.

Context-aware completions for Arch Linux-specific commands like *pacman*, *pacman-key*, *makepkg*, *cower*, *pbget*, *pacmatic* are built into fish, since the policy of the fish development is to include all the existent completions in the upstream tarball. The memory management is clever enough to avoid any negative impact on resources.

### Совмещение /etc/profile и ~/.profile

Стандартный POSIX `sh` не совместим с fish, fish не может взять исходник `/etc/profile` (и, таким образом, все `*.sh` в `/etc/profile.d`) и `~/.profile`

Если вы хотите чтобы fish брал файлы-исходники, установите [dash](https://www.archlinux.org/packages/?name=dash) и добавьте следующую строку в ваш `config.fish`:

```
env -i HOME=$HOME dash -l -c printenv | sed -e '/PATH/s/:/ /g;s/=/ /;s/^/set -x /' | source

```

Альтернативный вариант позволит вам сэкономить один исполняемый вызов с помощью встроенной команды:

```
env -i HOME=$HOME dash -l -c 'export -p' | sed -e "/PATH/s/'//g;/PATH/s/:/ /g;s/=/ /;s/^export/set -x/" | source

```

## Советы и хитрости

### История Замены

Fish does not implement history substitution (e.g. `sudo !!`), and the fish developers have said that they [do not plan to](http://fishshell.com/docs/current/faq.html#faq-history). Still, this is an essential piece of many users' workflow. Reddit user, [crossroads1112](http://www.reddit.com/u/crossroads1112), created a function that regains some of the functionality of history substitution and with another syntax. The function is on [github](https://gist.github.com/crossroads1112/77badb2c3455e23b873b) and instructions are included as comments in it. There is a [forked version](https://gist.github.com/b-/981892a65837ab0a387e) that is closer to the original syntax and allows for `command !!` if you specify the command in the helper function.

## Решение проблем

### Скрипты не совместимые с fish

В Arch, некоторые скрипты написаны для Bash, и они не полностью совместимы с fish. Вы можете получатьошибки вскриптах, если ваша оболочка по умолчанию устанавливается как fish. В Arch есть много сценариев оболочки (shell scripts), написанных для Bash, и они небыли переведены для fish. Чтобы не устанавливать Fish оболочкой по умолчанию, самым лучшим вариантом будет открыть эмулятор терминала с возможностью командной строки fish. Для большинства терминалов это параметр `-e`, так например, чтобы открыть gnome-terminal, использующим fish, измените свой ярлык для использования:

```
gnome-terminal -e fish

```

С LilyTerm и другими легкими эмуляторами терминалов, которые не поддерживают заданную оболочку, команда будет выглядеть следующим образом:

```
SHELL=/usr/bin/fish lilyterm

```

Другой вариант: установить fish в качестве оболочки по умолчанию для терминала в настройках терминала или его профиле, - конечно если ваш эмулятор терминала поддерживает это. This is contrast to changing the default shell for the user which would cause the above mentioned problem.

Чтобы установить fish, как оболочку в tmux, установите это в вашем `~/.tmux.conf`:

```
set-option -g default-shell "/usr/bin/fish"

```

Not setting fish as system wide default allows the arch scripts to run on startup, ensure the environment variables are set correctly, and generally reduces the issues associated with using a non-Bash compatible terminal like fish.

If you decide to set fish as your default shell, you may find that you no longer have very much in your path. You can add a section to your `~/.config/fish/config.fish` file that will set your path correctly on login. This is much like `.profile` or `.bash_profile` as it is only executed for login shells.

```
if status --is-login
        set PATH $PATH /usr/bin /sbin
end

```

Обратите внимание, что вам нужно будет вручную добавлять различные другие переменные окружения, такие как `$MOZ_PLUGIN_PATH`. Это огромный объем работы, чтобы получить удобство работы с fish в качестве оболочки по умолчанию.

### su запускает Bash

Если *su* запускается с Bash (потому что Bash оболочка по умолчания), определите функцию в fish:

```
$ funced su
function su
        /bin/su --shell=/usr/bin/fish $argv
end
$ funcsave su

```

### Запуск X при входе в систему

Добавьте следующее в нижнюю часть `~/.config/fish/config.fish`.

```
# start X at login
if status --is-login
    if test -z "$DISPLAY" -a $XDG_VTNR -eq 1
        exec startx -- -keeptty
    end
end

```

**Примечание:** Смотрите [это решение](https://github.com/fish-shell/fish-shell/issues/1772), причины почему `startx` требует `-keeptty` Флаг при использовании fish.

## Смотрите также

*   [http://fishshell.com/](http://fishshell.com/) - Домашняя страница
*   [http://fishshell.com/docs/2.1/index.html](http://fishshell.com/docs/2.1/index.html) - Документация