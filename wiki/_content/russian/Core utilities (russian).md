**Состояние перевода:** На этой странице представлен перевод статьи [Core utilities](/index.php/Core_utilities "Core utilities"). Дата последней синхронизации: 2015-03-07\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Core_utilities&diff=0&oldid=364226).

Эта статья описывает так называемые *базовые* утилиты для системы GNU/Linux, такие как *less*, *ls* и *grep*. В этой статье будут описаны утилиты GNU, находящиеся в пакете [coreutils](https://www.archlinux.org/packages/?name=coreutils), а также некоторые другие. Ниже будут описаны различные полезные советы и другая полезная информация, связанная с этими утилитами.

## Contents

*   [1 Основные команды](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D1.8B)
*   [2 cat](#cat)
*   [3 dd](#dd)
    *   [3.1 Проверка прогресса dd во время исполнения](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B5.D1.81.D1.81.D0.B0_dd_.D0.B2.D0.BE_.D0.B2.D1.80.D0.B5.D0.BC.D1.8F_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [3.1.1 Используя pipe viewer](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_pipe_viewer)
    *   [3.2 Аналоги для dd](#.D0.90.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.B8_.D0.B4.D0.BB.D1.8F_dd)
*   [4 grep](#grep)
    *   [4.1 Разноцветный вывод](#.D0.A0.D0.B0.D0.B7.D0.BD.D0.BE.D1.86.D0.B2.D0.B5.D1.82.D0.BD.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4)
    *   [4.2 Стандартная ошибка](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D0.B0.D1.8F_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B0)
*   [5 iconv](#iconv)
    *   [5.1 Конвертирование файла на месте](#.D0.9A.D0.BE.D0.BD.D0.B2.D0.B5.D1.80.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BD.D0.B0_.D0.BC.D0.B5.D1.81.D1.82.D0.B5)
*   [6 ip](#ip)
*   [7 less](#less)
    *   [7.1 Цветной вывод с помощью переменных окружения](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BD.D0.BE.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [7.2 Цветной вывод с помощью программ-обёрток](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BD.D0.BE.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC-.D0.BE.D0.B1.D1.91.D1.80.D1.82.D0.BE.D0.BA)
    *   [7.3 Vim в качестве альтернативного просмотрщика](#Vim_.D0.B2_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D0.B0.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.D1.89.D0.B8.D0.BA.D0.B0)
    *   [7.4 Цветной вывод при чтении с stdin](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BD.D0.BE.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D0.BF.D1.80.D0.B8_.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D0.B8_.D1.81_stdin)
*   [8 ls](#ls)
*   [9 mkdir](#mkdir)
*   [10 mv](#mv)
*   [11 rm](#rm)
*   [12 sed](#sed)
*   [13 seq](#seq)
*   [14 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Основные команды

В таблице ниже привидены основные shell команды, которые должен знать каждый пользователь Linux. Команды, выделенные **жирным** являются частью shell, остальные программы являются внешними и вызываются shell'ом. Смотрите нижеследующие разделы и *Статьи по теме* для дополнительной информации.

| Команда | Описание | Пример |
| man | Показать страницу справочного руководства по программе | man ed |
| **cd** | Сменить директорию | cd /etc/pacman.d |
| mkdir | Создать директорию | mkdir ~/newfolder |
| rmdir | Удалить пустую директорию | rmdir ~/emptyfolder |
| rm | Удалить файл | rm -r ~/file.txt |
| rm -r | Удалить директорию с её содержимым | rm -r ~/.cache |
| ls | Отобразить список файлов | ls *.avi |
| ls -a | Отобразить скрытые файлы | ls -a /home/archie |
| ls -al | Отобразить скрытые файлы и их свойства |
| mv | Переместить файл | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | Скопировать файл | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | Сделать файл исполняемым | chmod +x ~/.local/bin/myscript.sh |
| cat | Отобразить содержимое файла | cat /etc/hostname |
| strings | Отобразить печатные символы в бинарных файлах | strings /usr/bin/free |
| find | Поиск файла | find ~ -name myfile |
| mount | Монтирование раздела | mount /dev/sdc1 /media/usb |
| df -h | Отобразить оставшееся место на всех разделах |
| ps -A | Отобразить все выполняющиеся процессы |
| killall | Убить все запущенные экземпляры процесса |

## cat

[cat](https://en.wikipedia.org/wiki/ru:Cat "wikipedia:ru:Cat") (*объединить*) - это стандартная Unix утилита для конкатенации и отображения файлов.

*   Поскольку *cat* не встроена в shell, во многих случаях более подходящим может оказаться использование [перенаправлений](https://en.wikipedia.org/wiki/ru:%D0%9F%D0%B5%D1%80%D0%B5%D0%BD%D0%B0%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B2%D0%B2%D0%BE%D0%B4%D0%B0-%D0%B2%D1%8B%D0%B2%D0%BE%D0%B4%D0%B0 "wikipedia:ru:Перенаправление ввода-вывода"), например в скриптах или когда вам важна производительность. На самом деле `< *файл*` делает то же самое, что и `cat *файл*`.

*   *cat* может работать с несколькими строками, хотя иногда это расценивается как плохая практика:

```
$ cat << EOF >> *путь/файл*
*первая строка*
...
*последняя строка*
EOF

```

	Более хорошей альтернативой является команда *echo*:

```
$ echo "\
*первая строка*
...
*последняя строка*" \
>> *путь/файл*

```

*   Если вам нужно отобразить строки файла в обратном порядке, воспользуйтесь утилитой [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* в обратную сторону).

## dd

[dd](https://en.wikipedia.org/wiki/ru:dd "wikipedia:ru:dd") - это команда Unix и Unix подобных операционных систем, основным назначением которой является конвертация и копирование файлов.

**Примечание:** *cp* может делать то же самое, что и *dd* без каких либо операндов, однако она не предназначена для более гибких процедур зачисток диска.

### Проверка прогресса dd во время исполнения

По умолчанию *dd* ничего не выводит на экран до того момента, как задание будет выполнено. При помощи команды *kill* и сигнала `USR1` вы можете заставить её вывести статус, а программа на самом деле не будет убита. Откройте ещё один терминал с правами root и выполните следующую команду:

```
# killall -USR1 dd

```

**Примечание:** Это также затронет все остальные выполняющиеся процессы *dd*.

Или:

```
# kill -USR1 *pid_команды_dd*

```

Например:

```
# kill -USR1 $(pidof dd)

```

При этом *dd* немедленно выведет свой прогресс в терминале. Например:

```
605+0 records in
605+0 records out
634388480 bytes (634 MB) copied, 8.17097 s, 77.6 MB/s

```

#### Используя pipe viewer

В качестве альтернативного варианта вы можете использовать [pv](https://www.archlinux.org/packages/?name=pv), чтобы просматривать dd поток:

```
# dd if=*/source/filestream* | pv -*monitor_options* -s *size_of_file* | dd of=*/destination/filestream*

```

Чтобы было проще использовать pipe viewer, вы можете добавить это в ваш bashrc или zshrc:

```
copy() {
    size=$(stat -c%s $1)
    dd if=$1 &> /dev/null | pv -petrb -s $size | dd of=$2
}

```

И использовать следующим образом:

```
# copy */source/file* */destination/file*

```

### Аналоги для dd

Другие аналогичные *dd* программы могут периодически выводить статус, например в виде простой полосы прогресса.

	dcfldd 

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd) - это расширенная версия программы dd с дополнительными полезными возможностями для восстановления(?) и безопасности. Она принимает большинство из параметров для dd и включает вывод статуса. Последняя стабильная версия dcfldd вышла 19 декабря 2006.

	ddrescue 

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) - это инструмент для восстановления данных. Он умеет игнорировать ошибки чтения, однако почти во всех случаях не подходит для зачистки диска. Смотрите [официальную документацию](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html) для подробностей.

## grep

[grep](https://en.wikipedia.org/wiki/ru:grep "wikipedia:ru:grep") (произошло от [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed") *g/re/p*, *глобально/регулярное выражение/печатать*) - это утилита для текстового поиска из командной строки, изначально созданная для Unix. Команда *grep* глобально ищет в файле или в потоке стандартного ввода строки, удовлетворяющие заданному регулярному выражению и печатает их на свой стандартный вывод.

*   Запомните, что *grep* обрабатывает файлы, так что такие конструкции как `cat *файл* | grep *паттерн*` можно заменить на `grep *паттерн* *файл*`

*   Существуют альтернативы *grep*, оптимизированные для VCS исходного кода, такие как [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) и [ack](https://www.archlinux.org/packages/?name=ack).

### Разноцветный вывод

Цветовой вывод команды `grep` может быть полезен для изучения [регулярных выражений](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%80%D0%BD%D1%8B%D0%B5_%D0%B2%D1%8B%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "wikipedia:ru:Регулярные выражения") и другой функциональности `grep`.

Чтобы включить цветной текст в *grep* напишите следующую запись в конфигурационном файле shell'а (например, если вы используете [bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)")):

 `~/.bashrc`  `alias grep='grep --color=auto'` 

Чтобы в выводе отображались номера строк файла, добавьте опцию `-n`.

Для задания цвета подсветки по умолчанию может быть использована переменная окружения `GREP_COLOR` (по умолчанию используется красный). Чтобы изменить цвет, найдите [ANSI escape последовательность](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html) для понравившегося вам цвета и добавьте её:

```
export GREP_COLOR="1;32"

```

`GREP_COLORS` можно использовать для задания цвета специфичного поиска.

### Стандартная ошибка

Некоторые команды отправляют свой вывод в стандартный поток ошибок, а grep не имеет такого эффекта. В этом случае перенаправьте стандартный поток ошибок прямо в стандартный поток вывода:

```
$ *command* 2>&1 | grep *args*

```

или упрощённый вариант для Bash 4:

```
$ *command* |& grep *args*

```

Смотрите также [Перенаправление ввода/вывода](http://www.tldp.org/LDP/abs/html/io-redirection.html).

## iconv

`iconv` перекодирует символы из одной кодировки в другую.

Следующая команда сконвертирует файл `foo` из кодировки ISO-8859-15 в UTF-8, сохранив конечный файл как `foo.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 foo >foo.utf

```

Смотрите `man iconv` для дополнительной информации.

### Конвертирование файла на месте

**Совет:** Если вы не хотите изменять время модификации файла, вы можете использовать [recode](https://www.archlinux.org/packages/?name=recode) вместо iconv.

В отличие от [sed](#sed), *iconv* не предоставляет опции для конвертирования файла на месте. Однако для его обработки можно использовать `sponge`, который распространяется в пакете [moreutils](https://www.archlinux.org/packages/?name=moreutils).

```
$ iconv -f WINDOWS-1251 -t UTF-8 foobar.txt | sponge foobar.txt

```

Смотрите `man sponge` для дополнительной информации.

## ip

[ip](https://en.wikipedia.org/wiki/ru:Iproute2 "wikipedia:ru:Iproute2") позволяет вам узнать информацию о сетевых устройствах, IP адресах, таблицах маршрутизации и о других объектах программного обеспечения [IP](https://en.wikipedia.org/wiki/ru:IP "wikipedia:ru:IP") стека в Linux. При помощи добавления различных команд вы также можете манипулировать и настраивать большинство из этих объектов.

**Примечание:** Утилита *ip* распространяется в пакете [iproute2](https://www.archlinux.org/packages/?name=iproute2), который включён в группу [base](https://www.archlinux.org/groups/x86_64/base/).

| Объект | Назначение | Название страницы руководства |
| ip addr | управление адресом протокола | ip-address |
| ip addrlabel | управление названиями адресов протокола | ip-addrlabel |
| ip l2tp | туннель Ethernet по IP (L2TPv3) | ip-l2tp |
| ip link | настройка сетевых устройств | ip-link |
| ip maddr | управление широковещательными адресами | ip-maddress |
| ip monitor | просматривать сообщения netlink | ip-monitor |
| ip mroute | управление кешем широковещательной маршрутизации | ip-mroute |
| ip mrule | правила в бд политики широковещательной маршрутизации |
| ip neigh | управление таблицами neighbour/ARP | ip-neighbour |
| ip netns | управление обработкой сетевого пространства имён | ip-netns |
| ip ntable | настройка таблицы соседей | ip-ntable |
| ip route | настройка таблицы маршрутизации | ip-route |
| ip rule | управление базой данных политики маршрутизации | ip-rule |
| ip tcp_metrics | управление показателями TCP | ip-tcp_metrics |
| ip tunnel | настройка туннелей | ip-tunnel |
| ip tuntap | управление TUN/TAP устройствами |
| ip xfrm | управление политиками IPsec | ip-xfrm |

Для всех объектов доступна команда `help`. Например, выполните `ip addr help`, чтобы узнать синтаксис команды для объекта address. Для продвинутого использования смотрите [документацию iproute2](http://www.policyrouting.org/iproute2.doc.html).

Статья [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети") объясняет как использовать команду *ip* на практике в различных типовых случаях.

**Примечание:** Возможно вы знаете команду [ifconfig](https://en.wikipedia.org/wiki/ru:ifconfig "wikipedia:ru:ifconfig"), которая использовалась в старых версиях Linux для настройки интерфейсов. Теперь она устарела в Arch Linux; вы должны вместо неё использовать *ip*.

## less

[less](https://en.wikipedia.org/wiki/ru:less "wikipedia:ru:less") - это прогрмма для постраничного просмотра в терминале содержимого текстовых файлов. Несмотря на то, что он похож на другие пейджеры, такие как [more](https://en.wikipedia.org/wiki/ru:more "wikipedia:ru:more") и [pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)"), *less* предоставляет более продвинутый интерфейс и полноценный [функционал](http://www.greenwoodsoftware.com/less/faq.html).

Смотрите альтернативы в [Список приложений#Консольные утилиты постраничного просмотра](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.9A.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B_.D0.BF.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.D0.B0 "Список приложений").

### Цветной вывод с помощью переменных окружения

Добавьте следующие строки в ваш конфигурационный файл для shell:

 `~/.bashrc` 
```
export LESS=-R
export LESS_TERMCAP_me=$(printf '\e[0m')
export LESS_TERMCAP_se=$(printf '\e[0m')
export LESS_TERMCAP_ue=$(printf '\e[0m')
export LESS_TERMCAP_mb=$(printf '\e[1;32m')
export LESS_TERMCAP_md=$(printf '\e[1;34m')
export LESS_TERMCAP_us=$(printf '\e[1;32m')
export LESS_TERMCAP_so=$(printf '\e[1;44;1m')
```

Можете изменять значения на предпочитаемые вами. Ссылки: [Управляющие последовательности ANSI](https://en.wikipedia.org/wiki/ru:%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D1%8F%D1%8E%D1%89%D0%B8%D0%B5_%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B8_ANSI "wikipedia:ru:Управляющие последовательности ANSI").

### Цветной вывод с помощью программ-обёрток

Вы можете включить подсветку синтаксиса кода в *less*. Сначала установите [source-highlight](https://www.archlinux.org/packages/?name=source-highlight), затем добавьте следующие строки в ваш конфигурационный файл для shell:

 `~/.bashrc` 
```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

Пользователи, часто работающие в командной строке могут установить [lesspipe](https://www.archlinux.org/packages/?name=lesspipe).

Теперь вы можете отображать список сжатых файлов внутри архива при помощи вашего пейджера:

 `$ less *сжатый_файл*.tar.gz` 
```
==> use tar_file:contained_file to view a file in the archive
-rw------- *username*/*group*  695 2008-01-04 19:24 *сжатый_файл*/*content1*
-rw------- *username*/*group*   43 2007-11-07 11:17 *сжатый_файл*/*content2*
*сжатый_файл*.tar.gz (END)
```

Также *lesspipe* предоставляет *less* возможность взаимодействовать с файлами, не являющимися архивами, выступая в качестве альтернативы специальной программы, ассоциированной с этим типом файлов (таким как просмотрщик HTML через [python-html2text](https://www.archlinux.org/packages/?name=python-html2text)).

Перезайдите в систему после установки *lesspipe*, чтобы активировать его, или же укажите файл `/etc/profile.d/lesspipe.sh`.

### Vim в качестве альтернативного просмотрщика

[Vim](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Vim (Русский)") (*улучшенный визуальный редактор*) имеет скрипт для просмотра содержимого текстовых файлов, сжатых файлов, бинарников и директорий. Добавьте следующую строку в файл конфигурации вашего shell, чтобы использовать его в качестве пейджера:

 `~/.bashrc`  `alias less='/usr/share/vim/vim74/macros/less.sh'` 

Также существует альтернатива макросу *less.sh*, которая может работать как переменная окружения `PAGER`. Установите [vimpager](https://www.archlinux.org/packages/?name=vimpager) и добавьте следующее в файл настроек вашего shell:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

Теперь программы, использующие переменную окружения `PAGER`, такие как [git](/index.php/Git "Git"), будут использовать *vim* в качестве просмотрщика.

### Цветной вывод при чтении с stdin

**Примечание:** Рекомендуется добавить [#Цветной вывод с помощью переменных окружения](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BD.D0.BE.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F) в ваш `~/.bashrc` или `~/.zshrc`, поскольку нижеследующее основывается на `export LESS=R`

При использовании команды и перенаправлении её [стандартного вывода](https://en.wikipedia.org/wiki/ru:%D0%A1%D1%82%D0%B0%D0%BD%D0%B4%D0%B0%D1%80%D1%82%D0%BD%D1%8B%D0%B5_%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%B8 "wikipedia:ru:Стандартные потоки") (*stdout*) по конвейеру команде *less* для постраничного просмотра (например, `pacman -Qe | less`), вы можете заметить, что вывод больше не раскрашивается цветами. Обычно это происходит из-за того, что программа пытается определить, является ли её *stdout* интерактивным терминалом, и только в этом случае будет раскрашивать вывод, иначе текст будет нецветным. Такое поведение подходит когда вы хотите перенаправить *stdout* в файл, например, `pacman -Qe > pkglst-backup.txt`, но не подходит, когда вы хотите посмотреть вывод с помощью `less`.

Некоторые программы предоставляют опцию для отключения обнаружения интерактивного tty:

```
# dmesg --color=always | less

```

В случае, если программа такой опции не предоставляет, при помощи следующих утилит есть возможность обмануть программу, чтобы она думала, что её *stdout* является интерактивным терминалом:

*   **stdoutisatty** — Небольшая программка, которая отлавливает вызов функции `isatty`.

	[https://github.com/lilydjwg/stdoutisatty](https://github.com/lilydjwg/stdoutisatty). || [stdoutisatty](https://aur.archlinux.org/packages/stdoutisatty/)

	Пример: `stdoutisatty *программа* | less`

*   **socat** — Реле для двунаправленой передачи данных между двумя независимыми каналами данных. Она основана на GNU [readline](https://www.archlinux.org/packages/?name=readline).

	[http://www.dest-unreach.org/socat/](http://www.dest-unreach.org/socat/) || [socat](https://www.archlinux.org/packages/?name=socat)

	Пример: `socat EXEC:"*программа*",pty STDIO | less`

*   **[script](https://en.wikipedia.org/wiki/Script_(Unix) "wikipedia:Script (Unix)")** — Утилита, которая делает машинопись терминальной сессии.

	[http://man7.org/linux/man-pages/man1/script.1.html](http://man7.org/linux/man-pages/man1/script.1.html) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

	Пример: `script -fqc "*программа*" | less` или [[2]](http://stackoverflow.com/questions/1401002/trick-an-application-into-thinking-its-stdin-is-interactive-not-a-pipe/20401674#20401674)

*   **unbuffer** — Скрипт, основанный на *sh* и [Tcl](http://tcl.tk/).

	[http://expect.sourceforge.net/example/unbuffer.man.html](http://expect.sourceforge.net/example/unbuffer.man.html) || [expect](https://www.archlinux.org/packages/?name=expect)

	Пример: `unbuffer *программа* | less`

В качестве альтернативы можно использовать модуль [zpty](http://zsh.sourceforge.net/Doc/Release/Zsh-Modules.html#The-zsh_002fzpty-Module) для [zsh](/index.php/Zsh "Zsh"): [[3]](http://lilydjwg.is-programmer.com/2011/6/29/using-zpty-module-of-zsh.27677.html)

 `~/.zshrc` 
```
zmodload zsh/zpty

pty() {
	zpty pty-${UID} ${1+$@}
	if [[ ! -t 1 ]];then
		setopt local_traps
		trap '' INT
	fi
	zpty -r pty-${UID}
	zpty -d pty-${UID}
}

ptyless() {
	pty $@ | less
}
```

Использование:

```
$ ptyless *программа*

```

Чтобы передать по конвейеру другому пейджеру (в данном примере less):

```
$ pty *программа* | less

```

## ls

[ls](https://en.wikipedia.org/wiki/ru:ls "wikipedia:ru:ls") (*список*) - это команда для отображения списка файлов в Unix иUnix-подобных операционных системах.

*   *ls* может отображать [права доступа к файлам](/index.php/File_permissions_and_attributes#Viewing_permissions "File permissions and attributes").

*   Цветовой вывод можно включить с помощью простого алиаса. В файл `~/.bashrc` уже должна быть скопирована запись из `/etc/skel/.bashrc`:

	`alias ls='ls --color=auto'`

Следующий шаг заключается в дальнейшем улучшении цветного вывода *ls*; например, не работающие (сироты) симлинки будут отображаться красными оттенками. Добавьте следующее в ваш конфигурационный файл для shell:

	`eval $(dircolors -b)`

## mkdir

[mkdir](https://en.wikipedia.org/wiki/ru:mkdir "wikipedia:ru:mkdir") (*создать директорию*) - это команда для создания директорий.

*   Чтобы сразу создать директорию со вложенными директориями используйте опцию `-p`, иначе будет выведено сообщение об ошибке. Если вы понимаете, что вы делаете, вы можете использовать опцию `-p` по умолчанию.

	 `alias mkdir='mkdir -p -v'` 

	Опция `-v` сделает команду говорливой.

*   Нет необходимости изменять режим доступа с помощью *chmod* для только что созданных директорий, поскольку опция `-m` позволяет вам задать права доступа.

**Совет:** Если директория нажна вам временно, лучше будет использовать [mktemp](https://en.wikipedia.org/wiki/ru:%D0%92%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B9_%D1%84%D0%B0%D0%B9%D0%BB "wikipedia:ru:Временный файл") (*создать временный файл*): `mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/ru:mv "wikipedia:ru:mv") (*переместить*) - это команда для перемещения и переименования файлов и директорий. * Команда является очень опасной, поэтому нужно ограничить её возможности:

: `alias mv=' timeout 8 mv -iv'` 

	Этот алиас приостановит *mv*, если он выполняется более восьми секунд, будет спрашивать подтверждение на удалёние трёх и более файлов, отображать список выполняемых операций и не хранить себя в файле истории shell, если shell настроен так, чтобы игнорировать команды, начинающиеся с пробела.

## rm

[rm](https://en.wikipedia.org/wiki/ru:rm "wikipedia:ru:rm") (*удалить*) - это команда для удаления файлов и директорий.

*   Команда является очень опасной, поэтому нужно ограничить её возможности:

	 `alias rm=' timeout 3 rm -Iv --one-file-system'` 

	Этот алиас будет приостанавливать *rm*, если она выполняется более трёх секунд, спрашивать подтверждение на удаление трёх и более файлов, отображать текущие операции, не давать возможность работать на более чем одной файловой системе и не хранить себя в файле истории shell, если он настроен так, чтобы игнорировать команды, начинающиеся с пробела. Замените `-I` на `-i`, если вы хотите, чтобы спрашивалось подтверждение даже для одного файла.

	Пользователи zsh могут захотеть вписать `noglob` перед `timeout`, чтобы избежать неявных расширений.

*   Чтобы удалять директории, которые по вашему предположению пусты, пользуйтесь *rmdir*, так как она выдаст ошибку, в случае если внутри удаляемой директории находятся файлы.

## sed

[sed](https://en.wikipedia.org/wiki/ru:sed "wikipedia:ru:sed") (*редактор потока*) - это Unix утилита для анализа и трансформации текста.

Вот удобный [список](http://sed.sourceforge.net/sed1line.txt) однострочных примеров использования *sed*.

**Совет:** Более мощной альтернативой является [AWK](https://en.wikipedia.org/wiki/ru:AWK "wikipedia:ru:AWK") и даже язык [Perl](https://en.wikipedia.org/wiki/ru:Perl "wikipedia:ru:Perl").

## seq

**seq** (*последовательность*) - это утилита для генерации последовательности чисел. Существуют встроенные в shell альтернативы, поэтому рекомендуется использовать именно их, как описано в [Википедии](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)").

## Смотрите также

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils

*   [GNU Coreutils Manpage](http://www.gnu.org/software/coreutils/manual/coreutils.html)

*   [Learn the DD command](http://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)