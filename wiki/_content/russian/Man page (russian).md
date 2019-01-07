**man-страницы** (от англ. *manual* — руководство) — справочные страницы, которые предоставляются почти всеми *nix-дистрибутивами, включая Arch Linux. Для их отображения служит команда `man`.

man-страницы изначально подразумевались как самодостаточные документы. Они ограничены в возможностях ссылаться друг на друга, в отличие от поддерживающих гиперссылки [info-файлов](https://en.wikipedia.org/wiki/Info_(Unix) — попытки GNU создать замену традиционному формату man-страниц.

## Contents

*   [1 Доступ к man-страницам](#Доступ_к_man-страницам)
*   [2 Формат страниц](#Формат_страниц)
*   [3 Поиск по страницам](#Поиск_по_страницам)
*   [4 Цветные man-страницы](#Цветные_man-страницы)
    *   [4.1 С помощью less (рекомендуется)](#С_помощью_less_(рекомендуется))
    *   [4.2 С помощью most (не рекомендуется)](#С_помощью_most_(не_рекомендуется))
    *   [4.3 Цветные страницы в xterm или rxvt-unicode](#Цветные_страницы_в_xterm_или_rxvt-unicode)
        *   [4.3.1 xterm](#xterm)
        *   [4.3.2 rxvt-unicode](#rxvt-unicode)
*   [5 Просмотр локальных страниц](#Просмотр_локальных_страниц)
    *   [5.1 Конвертирование страниц в HTML](#Конвертирование_страниц_в_HTML)
        *   [5.1.1 mandoc](#mandoc)
        *   [5.1.2 man2html](#man2html)
        *   [5.1.3 man -H](#man_-H)
        *   [5.1.4 roffit](#roffit)
    *   [5.2 Конвертирование в PDF](#Конвертирование_в_PDF)
*   [6 Просмотр онлайн-страниц](#Просмотр_онлайн-страниц)
*   [7 Полезные страницы](#Полезные_страницы)
*   [8 Смотрите также](#Смотрите_также)

## Доступ к man-страницам

Чтобы отобразить man-страницу, наберите

```
$ man *имя_страницы*

```

Все страницы разделены на несколько категорий:

1.  Основные команды
2.  Системные вызовы (функции, предоставляемые ядром linux)
3.  Библиотечные вызовы (функции стандартной библиотеки языка Си)
4.  Специальные файлы (обычно расположенные в `/dev`) и драйверы
5.  Форматы файлов и соглашения
6.  Игры
7.  Прочие страницы (также включая соглашения)
8.  Команды для системного администрирования (для которых обычно требуются права суперпользователя) и демоны

На man-страницы принято ссылаться по имени, с указанием номера категории в скобках. Часто существуют сразу несколько man-страниц с одинаковыми именами, но в разных категориях, например man(1) и man(7). В таком случае, команде man необходимо передать номер конкретной категории перед именем man-страницы, например:

```
$ man 5 passwd

```

отобразит man-страницу по файлу `/etc/passwd` вместо утилиты `passwd`.

Вместо того, чтобы отображать man-страницу целиком, вы можете вывести лишь ее краткое описание, используя команду `whatis`. Например,

```
$ whatis ls

```

выведет краткое описание команды *ls*: "list directory contents" ("отобразить содержимое каталога").

## Формат страниц

Для удобства навигации, все man-страницы соответствуют единому стандартному формату. Вот список некоторых разделов, которые часто используются на страницах:

*   NAME — имя команды и краткое однострочное описание ее назначения.
*   SYNOPSIS — список опций и аргументов командной строки, которые принимает команда, либо параметры функции и ее заголовочный файл.
*   DESCRIPTION — более подробное описание назначения и принципов работы команды или функции.
*   EXAMPLES — типовые примеры использования, обычно от самых простых к более сложным.
*   OPTIONS — описания для каждой из опций, которые принимает команда.
*   EXIT STATUS — коды возврата и их значения.
*   FILES — связанные с командой или функцией файлы.
*   BUGS — вероятные проблемы, связанные с работой команды или функции и ожидающие решения. Также известны как KNOWN BUGS.
*   SEE ALSO — список связанных команд и функций.
*   AUTHOR, HISTORY, COPYRIGHT, LICENSE, WARRANTY — информация о программе: ее история, условия использования, создатели программы.

## Поиск по страницам

Хотя команда `man` позволяет отображать man-страницы, возникает сложность, когда вы не знаете точного названия желаемой страницы. К счастью, вы можете воспользоваться опциями `-k` или `--apropos`, для поиска по ключевому слову в описаниях man-страниц.

Поиск работает только по индексированным страницам. Кеш индекса может устареть или вовсе отсутствовать, и на попытки поиска вы не будете получать ожидаемых результатов. Вы можете создать индекс или обновить его, выполнив

```
# mandb

```

Индексация страниц должна запускаться при каждом добавлении man-страниц.

Теперь вы можете воспользоваться поиском. Например, чтобы найти man-страницы, связанные с паролями ("password"), введите:

```
$ man -k password

```

или

```
$ man --apropos password

```

С тем же успехом, вы также можете воспользоваться командой `apropos`:

```
$ apropos password

```

По-умолчанию, ключевое слово интерпретируется как [регулярное выражение](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%80%D0%BD%D1%8B%D0%B5_%D0%B2%D1%8B%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "wikipedia:ru:Регулярные выражения").

Если вы хотите произвести более углубленный поиск по всему содержимому страниц, используйте опцию `-K`:

```
$ man -K password

```

## Цветные man-страницы

Текст man-страниц может отображаться в разных цветах, что упрощает их чтение. Есть два основных метода, позволяющих раскрасить страницы — с помощью утилит *less* и *most*.

### С помощью less (рекомендуется)

Преимущество этого способа в том, что less имеет более богатый набор возможностей, чем most, а также используется по умолчанию для отображения man-страниц.

Добавьте следующие строки в файл конфигурации вашей командной оболочки (для [Bash](/index.php/Bash "Bash") это файл `~/.bashrc`):

```
man() {
    env LESS_TERMCAP_mb=$'\E[01;31m' \
    LESS_TERMCAP_md=$'\E[01;38;5;74m' \
    LESS_TERMCAP_me=$'\E[0m' \
    LESS_TERMCAP_se=$'\E[0m' \
    LESS_TERMCAP_so=$'\E[38;5;246m' \
    LESS_TERMCAP_ue=$'\E[0m' \
    LESS_TERMCAP_us=$'\E[04;38;5;146m' \
    man "$@"
}

```

Выполните команды из файла, чтобы увидеть изменения:

```
# source ~/.bashrc

```

Для [Fish](/index.php/Fish "Fish") настройки будут выглядеть как-то так:

 `~/.config/fish/config.fish` 
```
set -xU LESS_TERMCAP_mb (printf "\e[01;31m")      # begin blinking
set -xU LESS_TERMCAP_md (printf "\e[01;31m")      # begin bold
set -xU LESS_TERMCAP_me (printf "\e[0m")          # end mode
set -xU LESS_TERMCAP_se (printf "\e[0m")          # end standout-mode
set -xU LESS_TERMCAP_so (printf "\e[01;44;33m")   # begin standout-mode - info box
set -xU LESS_TERMCAP_ue (printf "\e[0m")          # end underline
set -xU LESS_TERMCAP_us (printf "\e[01;32m")      # begin underline

```

Чтобы сразу увидеть изменения (без перезапуска fish или системы), выполните:

```
# source ~/.config/fish/config.fish

```

Чтобы изменить эти цвета, обратитесь к статье [Wikipedia:ru:Управляющие последовательности ANSI](https://en.wikipedia.org/wiki/ru:%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D1%8F%D1%8E%D1%89%D0%B8%D0%B5_%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B8_ANSI "wikipedia:ru:Управляющие последовательности ANSI").

### С помощью most (не рекомендуется)

Утилита most выполняет ту же задачу, что less и *more*, но имеет меньший набор возможностей. Настройка цветов для most проще, однако требуется дополнительная настройка для того, чтобы most работал наподобие less.

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_определенных_пакетов "Pacman (Русский)") пакет [most](https://www.archlinux.org/packages/?name=most), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

В файле `/etc/man_db.conf` раскомментируйте параметр `pager` и установите ему значение `most -s`:

```
DEFINE     pager     most -s

```

Откройте любую man-страницу для проверки.

Настройка цветов осуществляется в пользовательском файле `~/.mostrc` (нужно создать, если он отсутствует), либо в системном файле `/etc/most.conf`. Пример конфигурации:

```
% Color settings
color normal lightgray black
color status yellow blue
color underline yellow black
color overstrike brightblue black

```

Другой пример, показывающий, как настроить сочетания клавиш, подобно `less` (переход к строке назначен на клавишу `J`):

```
% less-like keybindings
unsetkey "^K"
unsetkey "g"
unsetkey "G"
unsetkey ":"

setkey next_file ":n"
setkey find_file ":e"
setkey next_file ":p"
setkey toggle_options ":o"
setkey toggle_case ":c"
setkey delete_file ":d"
setkey exit ":q"

setkey bob "g"
setkey eob "G"
setkey down "e"
setkey down "E"
setkey down "j"
setkey down "^N"
setkey up "y"
setkey up "^Y"
setkey up "k"
setkey up "^P"
setkey up "^K"
setkey page_down "f"
setkey page_down "^F"
setkey page_up "b"
setkey page_up "^B"
setkey other_window "z"
setkey other_window "w"
setkey search_backward "?"
setkey bob "p"
setkey goto_mark "'"
setkey find_file "E"
setkey edit "v"

```

### Цветные страницы в xterm или rxvt-unicode

Быстрый способ раскрасить цвета man-страниц, которые просматриваются через [xterm](https://www.archlinux.org/packages/?name=xterm) / `uxterm` или [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode), заключается в редактировании файла `~/.Xresources`.

В подразделах представлена конфигурация для xterm и rxvt-unicode.

#### xterm

```
*VT100.colorBDMode:     true
*VT100.colorBD:         red
*VT100.colorULMode:     true
*VT100.colorUL:         cyan

```

Эти настройки заменяют начертания текста цветами. Добавьте также:

```
*VT100.veryBoldColors: 6

```

если вы хотите видеть цвета и начертания одновременно. Смотрите также [xterm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xterm.1) для описания ресурса терминала `veryBoldColors`.

#### rxvt-unicode

Конфигурация:

```
URxvt.colorIT:      #87af5f
URxvt.colorBD:      #d7d7d7
URxvt.colorUL:      #87afd7

```

После внесения изменений в файл, выполните:

```
$ xrdb -load ~/.Xresources

```

Запустите `xterm`/`uxterm` или `rxvt-unicode` и вы должны увидеть цветные man-страницы. Эти настройки добавляют цвета для слов, написанных **полужирным** и <u>подчеркнутым</u> шрифтом в `xterm/uxterm`, и цвета для слов в **полужирном**, <u>подчеркнутом</u>, и *наклонном* начертаниях в `rxvt-unicode`. Вы можете также совмещать эти атрибуты в различные комбинации.

## Просмотр локальных страниц

Кроме утилиты man, для чтения man-страниц вы также можете использовать веб-браузер, например [lynx](https://www.archlinux.org/packages/?name=lynx) или [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)"). Просмотр страниц в браузере позволяет воспользоваться основным преимуществом info-страниц — гиперссылками. Пользователи [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") могут читать man-страницы в Konqueror, используя URL вида:

```
man:<name>

```

Кроме того, вы можете [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_определенных_пакетов "Pacman (Русский)") следующие пакеты из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

1\. [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman) для просмотра страниц в [X](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").

2\. [yelp](https://www.archlinux.org/packages/?name=yelp) — Help Browser из состава [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)").

### Конвертирование страниц в HTML

#### mandoc

Установите пакет [mandoc](https://aur.archlinux.org/packages/mandoc/). Чтобы конвертировать страницу, для примера, `free(1)`, наберите:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | mandoc -Thtml -Ostyle=style.css 1> free.html

```

Получившийся файл `free.html` теперь можно открыть в любом веб-браузере.

#### man2html

Установите [man2html](https://www.archlinux.org/packages/?name=man2html) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Сконвертируйте страницу командой:

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

Другая полезная функция `man2html` — экспорт в обычный текстовый файл, который можно распечатать:

```
$ man free | man2html -bare > ~/free.txt

```

#### man -H

Реализация утилиты man от GNU, также позволяет открыть страницу в веб-браузере:

```
$ man -H free

```

Команда запустит браузер, установленный в [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `BROWSER`. Вы можете указать браузер явно, передав путь до исполняемого файла сразу после опции `-H`.

#### roffit

Установите пакет [roffit](https://aur.archlinux.org/packages/roffit/).

Для конвертирования страницы выполните:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | roffit > free.html

```

### Конвертирование в PDF

Man-страницы всегда были удобны для печати: они написаны в формате troff, который является типографским языком. Если у вас установлен *ghostscript*, конвертирование man-страниц в PDF выполнить очень просто:

```
man -t *имя_страницы* | ps2pdf - *pdf_файл*

```

По [этой ссылке](https://www.google.com/search?q=manpage+pdf+troff&num=100&hl=en&prmd=imvns&source=lnms&tbm=isch&sa=X&ei=5BZpUI3oH6rI2AXvx4CoAw&ved=0CAoQ_AUoAQ&biw=1321&bih=1100) вы можете посмотреть, как будет выглядеть получившийся PDF-документ.

Обратите внимание, что шрифты главным образом ограничены набором Times и имеют жестко заданные размеры. Документ не будет содержать гиперссылок. Некоторые man-страницы форматировались так, чтобы выглядеть хорошо в терминале, однако могут отображаться некорректно в форме PostScript или PDF-документов.

Следующий perl-скрипт конвертирует man-страницы в PDF, кэшируя файлы в каталоге `$HOME/.manpdf/`, и открывает программу для просмотра документа [mupdf](https://www.archlinux.org/packages/?name=mupdf).

 `Usage: manpdf [<section>] <manpage>` 
```
#!/usr/bin/perl
use File::stat;

$pdfdir = $ENV{"HOME"}."/.manpdf";
-d $pdfdir || mkdir $pdfdir || die "can't create $pdfdir";
$manpage = $ARGV[0];
chop($manpath = `man -w $manpage`);
die if $?;

$maninfo = stat($manpath) or die;
$manpath =~ s@.*/man./(.*)(\.(gz|bz2))?$@$1@;
$pdfpath = "$pdfdir/$manpath.pdf";
$pdftime = 0;
if (-f $pdfpath) {
    $pdfinfo = stat($pdfpath) or die;
    $pdftime = $pdfinfo->mtime;
}
if (!-f $pdfpath || $maninfo->mtime > $pdftime) {
    system "man -t $manpage | ps2pdf -dPDFSETTINGS=/screen - $pdfpath";
}
die if !-f $pdfpath;
if (!fork) {
    open(STDOUT, "/dev/null");
    open(STDERR, "/dev/null");
    exec "mupdf", "-r", "96", $pdfpath;
    #exec "acroread", $pdfpath;
}

```

## Просмотр онлайн-страниц

Существуют множество онлайн-хранилищ man-страниц; вот небольшой список:

*   [Man7.org.](http://man7.org/linux/man-pages/index.html) Первоисточник страниц для [man-pages](https://www.archlinux.org/packages/?name=man-pages).
*   [man-страницы Debian GNU/Linux](http://manpages.debian.net/)
*   [man-страницы DragonFlyBSD](http://leaf.dragonflybsd.org/cgi/web-man)
*   [man-страницы FreeBSD Hypertext](http://www.freebsd.org/cgi/man.cgi)
*   [man-страницы Linux and Solaris 10](http://www.manpages.spotlynx.com/)
*   [man-страницы Linux/FreeBSD](http://manpagehelp.net) с комментариями пользователей
*   [man-страницы на die.net](http://linux.die.net/man/)
*   [man-страницы на kernel.org](http://www.kernel.org/doc/man-pages/)
*   [man-страницы NetBSD](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [man-страницы Mac OS X](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [man-страницы UNIX](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [man-страницы OpenBSD](http://www.openbsd.org/cgi-bin/man.cgi)
*   [Руководство Plan 9 — Том 1](http://man.cat-v.org/plan_9/)
*   [Руководство Inferno — Том 1](http://man.cat-v.org/inferno/)
*   [man-страницы Storage Foundation](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [man-страницы форума The UNIX and Linux Forums](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [репозиторий man-страниц Ubuntu](http://manpages.ubuntu.com/)

**Важно:** Некоторые дистрибутивы Linux предоставляют исправленные или устаревшие man-страницы, которые могут отличаться от тех, которые поставляются с пакетами Arch Linux. Имейте это в виду, просматривая man-страницы онлайн.

## Полезные страницы

Здесь приведен небольшой список полезных man-страниц, которые могут помочь вам получить более углубленные знания о множестве полезных вещей. Некоторые из них могут служить хорошими справочниками (например, таблица ASCII).

*   ascii(7)
*   boot(7)
*   charsets(7)
*   chmod(1)
*   credentials(7)
*   fstab(5)
*   hier(7)
*   systemd(1)
*   locale(1P)(5)(7)
*   printf(3)
*   proc(5)
*   regex(7)
*   signal(7)
*   term(5)(7)
*   termcap(5)
*   terminfo(5)
*   utf-8(7)

Вам могут быть интересны также и другие страницы седьмой категории:

```
$ man -s 7 -k ".*"

```

А также страницы, относящиеся непосредственно к Arch Linux:

*   archlinux(7)
*   mkinitcpio(8)
*   pacman(8)
*   pacman-key(8)
*   pacman.conf(5)

## Смотрите также

*   [Основные рекомендации](/index.php/General_recommendations_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "General recommendations (Русский)") — Основные рекомендации по Arch Linux.
*   [Man page](http://wiki.gentoo.org/wiki/Man_page) — статья на Gentoo wiki.