Ссылки по теме

*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [ranger](/index.php/Ranger "Ranger")

**Состояние перевода:** На этой странице представлен перевод статьи [Midnight Commander](/index.php/Midnight_Commander "Midnight Commander"). Дата последней синхронизации: 10 сентября 2015‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Midnight_Commander&diff=0&oldid=399096).

[Midnight Commander](https://en.wikipedia.org/wiki/ru:Midnight_Commander "wikipedia:ru:Midnight Commander") — графический файловый менеджер, позволяющий копировать, перемещать и удалять файлы и деревья каталогов, производить поиск по файлам и запускать команды в командной оболочке. Он включает в себя встроенный просмотрщик и редактор файлов.

Midnight Commander имеет графический интерфейс, который отображается в текстовом режиме. Он работает в обычной консоли, внутри терминала [X](/index.php/Xorg "Xorg") и через [SSH-соединение](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)") на всех видах терминалов.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Дополнительные темы](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.82.D0.B5.D0.BC.D1.8B)
*   [2 Usage](#Usage)
    *   [2.1 Interface](#Interface)
    *   [2.2 Modules](#Modules)
*   [3 Configuration](#Configuration)
    *   [3.1 extfs](#extfs)
*   [4 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.1 Переназначение сочетаний клавиш](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BD.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BE.D1.87.D0.B5.D1.82.D0.B0.D0.BD.D0.B8.D0.B9_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
    *   [4.2 Навигация стрелками](#.D0.9D.D0.B0.D0.B2.D0.B8.D0.B3.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D1.82.D1.80.D0.B5.D0.BB.D0.BA.D0.B0.D0.BC.D0.B8)
    *   [4.3 Запуск из меню](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B8.D0.B7_.D0.BC.D0.B5.D0.BD.D1.8E)
    *   [4.4 Поддержка корзины](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.BA.D0.BE.D1.80.D0.B7.D0.B8.D0.BD.D1.8B)
        *   [4.4.1 Использование libtrash](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_libtrash)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Выход в текущий каталог](#.D0.92.D1.8B.D1.85.D0.BE.D0.B4_.D0.B2_.D1.82.D0.B5.D0.BA.D1.83.D1.89.D0.B8.D0.B9_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3)
    *   [5.2 Искаженное изображение](#.D0.98.D1.81.D0.BA.D0.B0.D0.B6.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [5.3 Opening files](#Opening_files)
    *   [5.4 Find file shows no results](#Find_file_shows_no_results)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [mc](https://www.archlinux.org/packages/?name=mc).

Последняя нестабильная версия доступна в пакете [mc-git](https://aur.archlinux.org/packages/mc-git/).

### Дополнительные темы

*   **mc-solarized-git** — Цветовая схема Solarized

	[https://github.com/nkulikov/mc-solarized-skin](https://github.com/nkulikov/mc-solarized-skin) || [mc-solarized-git](https://aur.archlinux.org/packages/mc-solarized-git/)

*   **mc-skin-candy** — Цветовая схема Candy

	[https://github.com/izmntuk/archiso/blob/master/configs/alter/root-image/usr/share/mc/skins/candy.ini](https://github.com/izmntuk/archiso/blob/master/configs/alter/root-image/usr/share/mc/skins/candy.ini) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

## Usage

The below section provides a short overview on usage of Midnight commander. References to [mc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mc.1) and the Help function (`F1`, available in every dialog) are made in this article as `**Section**`.

**Tip:** All hints are available in `/usr/share/mc/hints/`.

### Interface

In prominent view are two vertical panes. Either can list directory contents, show a plain text preview, file details, or a directory tree (see `**Directory Tree**`). File operations are accessible through the function keys or the mouse. More options are visible in a dynamic user menu (`F2`) and option menu (`F9`). Keys above `F12` (`F13` up to `F20`) are accessible through `Shift`. Menu and dialog options have one letter highlighted - pressing this letter (or `Alt+*Letter*` inside a text entry) directly activates the respective option.

Below, a command line is visible, connected to a subshell. This shell is generally of the same type *mc* was launched from, and may be switched to at will (`Ctrl-O`), see `**The subshell support**`. On this command line, *cd* is interpreted by Midnight Commander, and not passed to the shell for execution. As such, special completion (such as from [Zsh](/index.php/Zsh "Zsh")) is unavailable. Files in the pane interact with the command line; for example, `Alt+Enter` copies the name of a (selected) file to the command line.

Keybindings are generally similar to [GNU Emacs](/index.php/GNU_Emacs "GNU Emacs"). A more strict emacs keymap can be enabled (see `**Redefine hotkey bindings**`). New users may however use Lynx-like (arrow) keybindings (enabled in `F9 > Options > Panel options`) and mouse clicks for navigation.

### Modules

These can be called via the *mc* interface (with *Use internal* enabled in `F9 > Options > Configuration`), or separately as symbolic links to the *mc* binary.

*   *mcedit* - Text and binary file editor, with regex replace, syntax highlighting, macros and shell piping, see [mcedit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mcedit.1)
*   *mcview* - Text and hex viewer with goto marks and regex search
*   *mcdiff* - Compares and edits two files in-place (`C-x d`)

Per `mc` instance, multiple modules can be run concurrently (`Ctrl-``) (see `**Screen selector**`). External editors may be used instead, and parameters configured accordingly.

## Configuration

Most of the Midnight Commander settings can be changed from the menus. However, a small number of settings such as clipboard commands, codeset detection and parameters for external editors can only be changed from `~/.config/mc/ini`. See `**Special Settings**` and following for a complete description of options.

Additionally, the following environment variables are respected: `MC_SKIN`, `MC_KEYMAP`, `MC_XDG_OPEN`, `MC_COLOR_TABLE`, `MC_DATADIR`, `MC_HOME`, `KEYBOARD_KEY_TIMEOUT_US`, `PAGER`, `EDITOR`, `VIEWER`.

See also `**Files**`.

### extfs

extfs allows to easily create new virtual filesystems for mc. See `/usr/lib/mc/extfs.d/README` for details.

## Советы и рекомендации

### Переназначение сочетаний клавиш

Создайте копию стандартных комбинаций клавиш для текущего пользователя:

```
cp /etc/mc/mc.keymap ~/.config/mc/

```

и отредактируйте файл под свои нужды. Вы можете использовать также другие файлы *.keymap*. Например, можно установить `/etc/mc/mc.emacs.keymap` при помощи [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `MC_KEYMAP`:

```
export MC_KEYMAP=/etc/mc/mc.emacs.keymap

```

Смотрите также [mc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mc.1) для получения более подробной информации.

### Навигация стрелками

Чтобы иметь возможность навигации по каталогам с помощью клавиш со стрелками как в *Lynx*, перейдите в меню *Options* (`F9`, `o`) > *Panel Options* (`p`) и установите флажок *Lynx-like motion* в группе *Navigation* (`y`), затем нажмите *OK* (`o`).

### Запуск из меню

Midnight Commander можно запускать из меню, создав файл [desktop entry](/index.php/Desktop_entries "Desktop entries"). Пример:

```
[Desktop Entry]
Type=Application
Version=1.0
Name=Midnight Commander
Comment=Visual file manager
Exec=mc
Icon=folder
MimeType=inode/directory
Terminal=true
Categories=Utility;

```

### Поддержка корзины

Midnight Commander [не поддерживает](https://www.midnight-commander.org/ticket/3072) функцию корзины.

#### Использование libtrash

Библиотека libtrash перехватывает вызовы функций удаления файлов и вместо удаления выполняет перемещение файлов в корзину.

Установите [libtrash](https://aur.archlinux.org/packages/libtrash/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") и создайте псевдоним для *mc* в файле инициализации вашей командной оболочки (например, `~/.bashrc` или `~/.zshrc`):

```
alias mc='LD_PRELOAD=/usr/lib/libtrash.so.3.3 mc'

```

Чтобы изменения вступили в силу, переоткройте сеанс терминала или просто выполните скрипт инициализации командой *source*.

Стандартные настройки библиотеки находятся в файле `/etc/libtrash.conf.sys`. Вы можете переопределить их для текущего пользователя, создав пользовательский файл настроек `~/.libtrash`, например:

```
TRASH_CAN = .Trash
INTERCEPT_RENAME = NO
IGNORE_EXTENSIONS= o;exe;com

```

Теперь, после запуска *mc*, удаляемые файлы будут попадать в каталог корзины `~/.Trash`.

**Важно:**

*   У этого способа существует побочный эффект: программы, запущенные из *mc* наследуют переменную окружения `LD_PRELOAD`, которая может вызывать проблемы в их работе. Смотрите [[1]](http://pages.stern.nyu.edu/~marriaga/software/libtrash/) для более подробной информации.
*   С установленной опцией `GLOBAL_PROTECTION = YES` (значение по умолчанию), файлы вне домашнего каталога будут попадать в корзину, даже если они находятся на другом разделе диска. Такие файлы фактически перемещаются копированием и удалением из исходного расположения, поэтому процедура удаления в корзину файла на другом разделе может занимать продолжительное время.

Смотрите также [[2]](https://mail.gnome.org/archives/mc/2010-March/msg00041.html).

## Решение проблем

### Выход в текущий каталог

При выходе, командная оболочка вернет вас с тот каталог, в котором вы запустили Midnight Commander. Если вы хотите, чтобы оставался текущий каталог, выбранный в Midnight Commander, простым решением будет просто скрывать интерфейс, не прерывая сеанс программы, нажатием `Ctrl+O`.

### Искаженное изображение

Нажмите `Ctrl+L` для перерисовки интерфейса. Эта команда перерисует изображение, но не обновит список файлов в каталогах. Для обновления списка файлов на панелях используйте `Ctrl+R`.

### Opening files

*mc* uses [xdg-open](/index.php/Xdg-open "Xdg-open") to open files by default, as shown in `/usr/lib/mc/ext.d/`. While *stderr* is redirected, *stdout* is not, which may result in a garbled screen.

 `/usr/lib/mc/ext.d/*.sh` 
```
[ -n "${MC_XDG_OPEN}" ] || MC_XDG_OPEN="xdg-open"
...
open)
    "${MC_XDG_OPEN}" "${MC_EXT_FILENAME}" **2>/dev/null** || \
        do_open_action "${filetype}"
```

Create a script to wrap *xdg-open*:

 `~/bin/xdg-open-null` 
```
#!/bin/bash
xdg-open "$@" **>/dev/null**

```

If *mc* is blocked until *xdg-open* ends, detach the process:

 `~/bin/xdg-open-null` 
```
#!/bin/bash
nohup xdg-open "$@" >/dev/null &

```

and make *mc* aware of it by setting the `MC_XDG_OPEN` [environment variable](/index.php/Environment_variable "Environment variable"):

```
export MC_XDG_OPEN=~/bin/xdg-open-null

```

**Tip:** When [#Using libtrash](#Using_libtrash), add `unset LD_PRELOAD` before *xdg-open* in the script.

### Find file shows no results

If the *Find file* dialog (accessible with `Alt+?`) shows no results, check the current directory for symbolic links. Find file does not follow symbolic links, so use bind mounts (see [mount(2)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.2)) instead, or the *External panelize* command.

## Смотрите также

*   [Введение в Midnight Commander](http://www.tldp.org/LDP/LG/issue23/wkndmech_dec97/mc_article.html)
*   [Руководство пользователя GNU Midnight Commander](http://sunhe.jinr.ru/docs/mc/mc.html)
*   [Руководство по Midnight Commander](http://www.nawaz.org/media/docs/mc/mc.html)
*   [Учебник по Midnight Commander](http://www.trembath.co.za/mctutorial.html)
*   [Сочетания клавиш для Midnight Commander](http://www.softpanorama.info/OFM/MC/cheetsheet.shtml)