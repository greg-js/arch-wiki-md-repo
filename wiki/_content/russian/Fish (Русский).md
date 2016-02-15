**fish** (**friendly interactive shell**, т.е. **дружелюбная интерактивная оболочка**) представляет собой удобную интерактивную оболочку командной строки предназначенную в основном для интерактивного использования.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Ввод/Вывод](#.D0.92.D0.B2.D0.BE.D0.B4.2F.D0.92.D1.8B.D0.B2.D0.BE.D0.B4)
    *   [2.1 Файловые дескрипторы](#.D0.A4.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D0.B5_.D0.B4.D0.B5.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.BE.D1.80.D1.8B)
    *   [2.2 Перенаправление](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BD.D0.B0.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [2.3 Пайпинг (piping)](#.D0.9F.D0.B0.D0.B9.D0.BF.D0.B8.D0.BD.D0.B3_.28piping.29)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Веб-интерфейс](#.D0.92.D0.B5.D0.B1-.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81)
    *   [3.2 Приглашение командной строки (Prompt)](#.D0.9F.D1.80.D0.B8.D0.B3.D0.BB.D0.B0.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8_.28Prompt.29)
    *   [3.3 Завершение команд](#.D0.97.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4)
    *   [3.4 Совмещение /etc/profile и ~/.profile](#.D0.A1.D0.BE.D0.B2.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.2Fetc.2Fprofile_.D0.B8_.7E.2F.profile)
*   [4 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [4.1 История Замены](#.D0.98.D1.81.D1.82.D0.BE.D1.80.D0.B8.D1.8F_.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D1.8B)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 su запускает Bash](#su_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82_Bash)
    *   [5.2 Запуск X при входе в систему](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_X_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") пакет [fish](https://www.archlinux.org/packages/?name=fish) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"), - стабильную версию пакета [основного форка](http://fishshell.com/) проекта.

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") [fish-shell-git](https://aur.archlinux.org/packages/fish-shell-git/) из [AUR](/index.php/AUR "AUR"), - последнюю разрабатываемую версию.

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") [fish-git](https://aur.archlinux.org/packages/fish-git/) из [AUR](/index.php/AUR "AUR") [прекращённую разработку](http://www.mail-archive.com/fish-users@lists.sourceforge.net/msg02893.html) по его [оригинальной разработке](https://github.com/liljencrantz) в 2011.

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
_Перенаправление стандартного ввода:_
$ команда < исходный файл

_Перенаправление стандартного вывода:_
$ команда > назначение

_Добавление стандартного вывода в существующий файл:_
$ команда >> назначение

_Перенаправление стандартной ошибки:_
$ команда ^ назначение

_Добавить стандартную ошибку в существующий файл:_
$ команда ^^ назначение
```

Вы можете использовать один из следующих `назначений`:

*   Имя файла (выход будет записан в указанный файл).
*   `&` за которым следует номер другого дескриптора файла. Выход будет написан на другой файловый дескриптор.
*   `&` с последующим знаком `-`. Выход не будет записан.

Примеры:

```
_Перенаправление стандартного выхода в файл:_
$ команда > файл_назначения.txt

_Перенаправление стандартного вывода и стандартной ошибки в тот же файл:_
$ команда > файл_назначения.txt ^ &1

_Отключение стандартного вывода:_
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

Context-aware completions for Arch Linux-specific commands like _pacman_, _pacman-key_, _makepkg_, _cower_, _pbget_, _pacmatic_ are built into fish, since the policy of the fish development is to include all the existent completions in the upstream tarball. The memory management is clever enough to avoid any negative impact on resources.

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

В Arch есть много сценариев оболочки (shell scripts), написанных для Bash, и они небыли переведены для fish. Чтобы не устанавливать Fish оболочкой по умолчанию, самым лучшим вариантом будет открыть эмулятор терминала с возможностью командной строки fish. Для большинства терминалов это параметр `-e`, так например, чтобы открыть gnome-terminal, использующим fish, измените свой ярлык для использования:

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

Если _su_ запускается с Bash (потому что Bash оболочка по умолчания), определите функцию в fish:

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

**Обратите внимание:** Смотрите [это решение](https://github.com/fish-shell/fish-shell/issues/1772) пичины почему `startx` требует `-keeptty` Флаг при использовании fish.

## Смотрите также

*   [http://fishshell.com/](http://fishshell.com/) - Домашняя страница
*   [http://fishshell.com/docs/2.1/index.html](http://fishshell.com/docs/2.1/index.html) - Документация