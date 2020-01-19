**Состояние перевода:** На этой странице представлен перевод статьи [nano](/index.php/Nano "Nano"). Дата последней синхронизации: 18 января 2020\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Nano&diff=0&oldid=590241).

[GNU nano](https://www.nano-editor.org/) (или просто "nano") — текстовый редактор с простым и интуитивно понятным интерфейсом, включающим в себя основные команды для редактирования текста. *Nano* поддерживает подсветку синтаксиса, конвертацию файлов DOS/Mac, проверку орфографии и кодировку [UTF-8](https://en.wikipedia.org/wiki/ru:UTF-8 "wikipedia:ru:UTF-8"). Программа *Nano* (с пустым буфером) занимает в оперативной памяти менее 4 Мб.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Подсветка синтаксиса](#Подсветка_синтаксиса)
        *   [2.1.1 PKGBUILD](#PKGBUILD)
        *   [2.1.2 Forth](#Forth)
    *   [2.2 Фоновый режим](#Фоновый_режим)
    *   [2.3 Перенос текста](#Перенос_текста)
*   [3 Использование](#Использование)
    *   [3.1 Специальные функции](#Специальные_функции)
*   [4 Советы и рекомендации](#Советы_и_рекомендации)
    *   [4.1 Замена vi на nano](#Замена_vi_на_nano)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 Оконный менеджер перехватывает горячие клавиши](#Оконный_менеджер_перехватывает_горячие_клавиши)
*   [6 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [nano](https://www.archlinux.org/packages/?name=nano).

## Настройка

Вид, поведение и функции nano управляются посредством аргументов командной строки или настроек в файле `~/.config/nano/nanorc`.

Пример конфигурационного файла находится в `/etc/nanorc`. Чтобы настроить nano, сначала скопируйте данный файл в `~/.config/nano/nanorc`:

```
$ cp /etc/nanorc ~/.config/nano/nanorc

```

Продолжите настройку nano путём установки и/или отключения команд в файле `~/.config/nano/nanorc`.

**Совет:** Подробный список команд настроек для nano доступен на странице справочного руководства [nanorc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nanorc.5).

**Примечание:** Аргументы командной строки переопределяют и имеют приоритет над командами настроек, заданных в `~/.config/nano/nanorc`.

### Подсветка синтаксиса

Nano поставляется с предопределенными правилами [подсветки синтаксиса](https://en.wikipedia.org/wiki/ru:%D0%9F%D0%BE%D0%B4%D1%81%D0%B2%D0%B5%D1%82%D0%BA%D0%B0_%D1%81%D0%B8%D0%BD%D1%82%D0%B0%D0%BA%D1%81%D0%B8%D1%81%D0%B0 "wikipedia:ru:Подсветка синтаксиса"), заданными в `/usr/share/nano/*.nanorc`. Чтобы включить их, добавьте следующую строку в `~/.config/nano/nanorc` или `/etc/nanorc`:

```
include "/usr/share/nano/*.nanorc"

```

Для получения улучшенной подсветки синтаксиса, расширяющей стандартные возможности, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [nano-syntax-highlighting](https://www.archlinux.org/packages/?name=nano-syntax-highlighting) или [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/) и добавьте следующий параметр в дополнение к вышеуказанному:

```
include "/usr/share/nano-syntax-highlighting/*.nanorc"

```

#### PKGBUILD

Сохраните [https://paste.xinu.at/4ss/](https://paste.xinu.at/4ss/) в `/etc/nano/pkgbuild.nanorc` и включите его:

```
include "/etc/nano/pkgbuild.nanorc"

```

**Совет:** В [nano-syntax-highlighting](https://www.archlinux.org/packages/?name=nano-syntax-highlighting) доступна альтернативная версия.

#### Forth

См. [https://paste.xinu.at/wc17YG/](https://paste.xinu.at/wc17YG/) для получения конфигурации подсветки синтаксиса языка программирования [Forth](https://en.wikipedia.org/wiki/ru:%D0%A4%D0%BE%D1%80%D1%82_(%D1%8F%D0%B7%D1%8B%D0%BA_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F) "wikipedia:ru:Форт (язык программирования)").

### Фоновый режим

В отличие от большинства интерактивных программ, фоновый режим не включен по умолчанию. Чтобы изменить это, раскомментируйте строку 'set suspend' в `/etc/nanorc`. Это позволит использовать сочетание клавиш `Ctrl+z` для отправки nano в фоновый режим.

### Перенос текста

До версии 4.0, в отличие от многих текстовых редакторов, nano автоматически вставлял перенос строки. Чтобы изменить это поведение, добавьте следующую строку в `~/.config/nano/nanorc`

```
set nowrap

```

## Использование

Сочетания клавиш можно просмотреть из *nano*. См. справочные файлы nano онлайн с помощью `Ctrl+g` из nano или [nano Command Manual](https://www.nano-editor.org/dist/latest/nano.html) (англ.) для получения полных описаний и дополнительной поддержки.

См. также [шпаргалку о nano](https://www.nano-editor.org/dist/latest/cheatsheet.html) (англ.).

### Специальные функции

Сочетания клавиш с наиболее используемыми функциями приведены на двух строках внизу экрана nano.

Их можно переключать следующим образом:

*   `Ctrl` для включения сочетаний клавиш, основанных на `^`
*   *`Meta`* (обычно `Alt`) или `Esc` для включения сочетаний клавиш, основанных на `M-`

**Совет:** В разделе [Feature Toggles](https://www.nano-editor.org/dist/latest/nano.html#Feature-Toggles) (англ.) приведён список глобальных переключателей, доступных в nano.

## Советы и рекомендации

### Замена vi на nano

Чтобы заменить `vi` на `nano` в качестве стандартного текстового редактора при использовании таких команд, как [visudo](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_visudo "Sudo (Русский)"), задайте [переменные окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_переменных "Environment variables (Русский)") `VISUAL` и `EDITOR`, например:

```
export VISUAL=nano
export EDITOR=nano

```

## Решение проблем

### Оконный менеджер перехватывает горячие клавиши

Некоторые оконные менеджеры используют сочетания клавиш, конфликтующие с nano, например, `Alt+Enter`. Удалите и переназначьте их, к примеру, на `Super` (с помощью [dconf](https://www.archlinux.org/packages/?name=dconf) для [mutter](https://www.archlinux.org/packages/?name=mutter), [muffin](https://www.archlinux.org/packages/?name=muffin) и [marco](https://www.archlinux.org/packages/?name=marco)) и перезапустите оконный менеджер.

## Смотрите также

*   [nano](https://en.wikipedia.org/wiki/ru:nano "wikipedia:ru:nano") — статья в Википедии
*   [Домашняя страница GNU nano](https://www.nano-editor.org/) — официальный сайт (англ.)
*   [GNU nano Bugs](https://savannah.gnu.org/bugs/?group=nano) — отчёты об ошибках (англ.)
*   [Улучшенные файлы подсветки синтаксиса (англ.)](https://github.com/scopatz/nanorc)