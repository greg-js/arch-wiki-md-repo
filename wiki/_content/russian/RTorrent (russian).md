[rTorrent](http://libtorrent.rakshasa.no/) - это быстрый и эффективный клиент BitTorrent использующий библиотеку libtorrent. rTorrent написан на C++ и использует программную библиотеку [ncurses](https://en.wikipedia.org/wiki/ncurses "wikipedia:ncurses"), которая означает, что он использует текстовый интерфейс. В сочетании с [GNU Screen](/index.php/GNU_Screen "GNU Screen") и [Secure Shell](/index.php/Secure_Shell "Secure Shell"), он становится удобным удаленным клиентом [BitTorrent](https://en.wikipedia.org/wiki/BitTorrent_(protocol)#Operation "wikipedia:BitTorrent (protocol)").

## Contents

*   [1 Установка](#Установка)
*   [2 Конфигурация](#Конфигурация)
    *   [2.1 Производительность](#Производительность)
    *   [2.2 Создание и управление файлами](#Создание_и_управление_файлами)
    *   [2.3 Настройка портов](#Настройка_портов)
    *   [2.4 Дополнительные настройки](#Дополнительные_настройки)
*   [3 Привязка клавиш](#Привязка_клавиш)
    *   [3.1 Избыточные привязки клавиш](#Избыточные_привязки_клавиш)
*   [4 Дополнительные советы](#Дополнительные_советы)
    *   [4.1 Разделить сессию с помощью Screen'а](#Разделить_сессию_с_помощью_Screen'а)
        *   [4.1.1 Запуск в качестве демона](#Запуск_в_качестве_демона)
    *   [4.2 Резерв места, предупреждение фрагментации (pre-allocation)](#Резерв_места,_предупреждение_фрагментации_(pre-allocation))
    *   [4.3 Управление законченными файлами](#Управление_законченными_файлами)
        *   [4.3.1 Уведомления с почтой Гугла](#Уведомления_с_почтой_Гугла)
    *   [4.4 Displaying active torrents](#Displaying_active_torrents)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 CA certificates](#CA_certificates)
*   [6 Web interface](#Web_interface)
    *   [6.1 XMLRPC interface](#XMLRPC_interface)
*   [7 See also](#See_also)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [rtorrent](https://www.archlinux.org/packages/?name=rtorrent). Кроме того, существуют пакеты [rtorrent-svn](https://aur.archlinux.org/packages/rtorrent-svn/) или [rtorrent-extended](https://aur.archlinux.org/packages/rtorrent-extended/).

## Конфигурация

**Примечание:** Смотрите статью rTorrent для получения дополнительной информации: [Common Tasks in rTorrent for Dummies](http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks)

До запуска rTorrent, найдите пример конфигурационного файла `/usr/share/doc/rtorrent/rtorrent.rc` и скопируйте его в `~/.rtorrent.rc`:

```
$ cp /usr/share/doc/rtorrent/rtorrent.rc ~/.rtorrent.rc

```

### Производительность

**Примечание:** Смотрите статью rTorrent для получения дополнительной информации: [Performance Tuning](http://libtorrent.rakshasa.no/wiki/RTorrentPerformanceTuning)

Значения следующих параметров зависят от аппаратной части системы и скорости интернет-соединения. Чтобы найти оптимальные значения, читайте статью: [Optimize Your BitTorrent Download Speed](http://torrentfreak.com/optimize-your-BitTorrent-download-speed)

```
min_peers = 40
max_peers = 52

min_peers_seed = 10
max_peers_seed = 52

max_uploads = 8

download_rate = 200
upload_rate = 28

```

Опция `check_hash` выполняет проверку хэш-кода, когда загрузка завершена или запущен rTorrent. При запуске, она проверяет на наличие ошибок завершенные (загруженные) файлы.

```
check_hash = yes

```

### Создание и управление файлами

Опция `directory` будет определять место, где ваши данные будут сохраняться. Обязательно указывайте абсолютный путь, так как rTorrent не поддерживает относительные пути:

```
directory = /home/[пользователь]/torrents/

```

Опция `session` позволяет rTorrent сохранять текущее состояние (прогресс) ваших загрузок. Рекомендуется создать директорию с названием `.session` (например: `$ mkdir ~/.session`).

```
session = /home/[пользователь]/.session/

```

Опция `schedule` в rTorrent наблюдает за определенным каталогом на наличие новых торрент-файлов. Сохранение торрент-файла в эту директорию, автоматически начнет загрузку. Не забудьте создать каталог, для автоматической загрузки (например: `$ mkdir ~/obs`). Будьте осторожны, при использовании этой опции так как rTorrent переместит торрент-файл в вашу папку `.session` и переименует его в хэш-значение.

```
schedule = watch_directory,5,5,load_start=/home/[user]/watch/*.torrent
schedule = untied_directory,5,5,stop_untied=
schedule = tied_directory,5,5,start_tied=

```

Следующая опция `schedule` предназначена для остановки rTorrent от загрузки данных, когда не хватает дискового пространства.

```
schedule = low_diskspace,5,60,close_low_diskspace=100M

```

### Настройка портов

Параметр `port_range` задает порт(ы) для прослушивания. Рекомендуется использовать порт, который больше чем 49152 (см.: [List of port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers")). Несмотря на то, что rTorrent позволяет использовать диапазон портов, рекомендуется использовать один.

```
port_range = 49164-49164

```

Кроме того, убедитесь, что переадресация включена для надлежащих портов (см.: [Port Forward Guides](http://portforward.com/english/routers/port_forwarding/routerindex.htm)).

### Дополнительные настройки

Параметр `encryption` включает или отключает шифрование. Очень важно включить эту опцию, не только для Вас, но так же для Ваших коллег (пиров). Некоторым пользователям нужно скрыть использование своей пропускной способности от их интернет-провайдера.

```
encryption = allow_incoming,try_outgoing,enable_retry

```

Последняя опция `dht` включает поддержку [DHT](https://en.wikipedia.org/wiki/Distributed_hash_table "wikipedia:Distributed hash table"). DHT распространен среди открытых трекеров и позволяет клиенту получить больше пиров.

```
dht = auto
dht_port = 6881
peer_exchange = yes

```

**Примечание:** См. статью rTorrent для получения дополнительной информации: [Using DHT](http://libtorrent.rakshasa.no/wiki/RTorrentUsingDHT)

## Привязка клавиш

rTorrent управляется горячими клавишами. Краткий справочник доступен в таблице ниже. Полное руководство доступно в статье rTorrent (см.: [rTorrent User Guide](http://libtorrent.rakshasa.no/wiki/RTorrentUserGuide)).

**Примечание:** Двойное быстрое нажатие `Ctrl-q` заставит rTorrent завершить работу не дожидаясь отправки сигнала стоп к подключенным трекерам.

| Команда | Действие |
| Ctrl-q | Выход из приложения |
| Ctrl-s | Начать загрузку. В первую очередь запускает хэширование, если оно еще не было сделано. |
| Ctrl-d | Остановка активной загрузки или удаление остановленной загрузки. |
| Ctrl-k | Остановить и закрыть файлы активной загрузки. |
| Ctrl-r | Инициировать хэш-проверку торрента. Без запуска загрузки/отдачи. |
| Влево | Возврат к предыдущему экрану. |
| Вправо | Переход к следующему экрану |
| Backspace/Return(Enter) | Добавляет указанный *.torrent |
| a|s|d | Регулировка увеличения глобальной скорости отдачи на 1|5|50 КБ/с |
| A|S|D | Регулировка увеличения глобальной скорости загрузки на 1|5|50 КБ/с |
| z|x|c | Регулировка уменьшения глобальной скорости отдачи на 1|5|50 КБ/С |
| Z|X|C | Регулировка уменьшения глобальной скорости загрузки на 1|5|50 КБ/с |

### Избыточные привязки клавиш

`Ctrl-s` Часто используется в управлении терминалом для того что-бы остановить вывод на экран, тогда как `Ctrl-q` используется для того что-бы его включить. Эти назначения могут конфликтовать с rTorrent'ом. Проверьте и посмотрите, не совпадают ли эти опции терминала с назначенными клавишами:

 `$ stty -a` 
```
...
swtch = <undef>; start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V;
...

```

Для того что-бы удалить назначения, измените свойства терминала стерев определения вышеупомянутых специальных символов (i.e. `stop` and `start`):

```
# stty stop undef
# stty start undef

```

Для того что-бы эти назначения удалялись автоматически, предыдущие две команды можно добавить в файл `~/.bashrc` file.

## Дополнительные советы

### Разделить сессию с помощью Screen'а

[GNU Screen](/index.php/GNU_Screen "GNU Screen") это обертка которая позволяет разделить текстовую программу и консоль с которой она была запущена.

Контроль потока Screen'а взаимодействует с привязкой `Ctrl-q` (см.: [Избыточные привязки клавиш](#Redundant_mapping)). Что-бы отключить это, вставьте следующее в файл `~/.screenrc`:

```
defflow off

```

Альтернативой может быть заключение команды в ESC последовательность и отправлением ее напрямую на терминал. Другими словами, используйте `Ctrl-a` `q` для того что-бы выйти из rTorrent'а внутри GNU Screen'а.

Для того что-бы автоматически запускать rTorrent изнутри Screen'а добавьте следующее в конфигурационный файл `~/.screenrc`:

```
screen -t rtorrent rtorrent 

```

#### Запуск в качестве демона

**Примечание:** См. викистатью об rTorrent по этой теме для получения дополнительной информации: [Starting rTorrent on System Startup](http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks#StartingrTorrentonSystemStartup)

Альтернативно, GNU Screen и rTorrent могут быть запущены совместно в качестве демона [daemon](/index.php/Daemon "Daemon") (см. также: [Arch Linux Forums thread](https://bbs.archlinux.org/viewtopic.php?id=53395), [Gentoo Discussion Forums thread](https://forums.gentoo.org/viewtopic-t-600362-postdays-0-postorder-asc-start-0.html)).

Для того что-бы использовать этот скрипт с [tmux](/index.php/Tmux "Tmux"), замените строку 9 следующим `su - USER -c 'tmux new -s rtorrent -d rtorrent' &> /dev/null` (см.: [rTorrent демон вместе с tmux](https://bbs.archlinux.org/viewtopic.php?id=126718)).

При привилегиях администратора создайте следующий файл:

 `/etc/rc.d/rtorrent` 
```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

case "$1" in
  start)
    stat_busy "Запускается rtorrent"
    su - USER -c 'screen -d -m -S rtorrent rtorrent' &> /dev/null
    if [ $? -gt 0 ]; then
      stat_fail
    else
      add_daemon rtorrent
      stat_done
    fi
    ;;
  stop)
    stat_busy "Останавливается rtorrent"
    killall -w -s 2 /usr/bin/rtorrent &> /dev/null
    if [ $? -gt 0 ]; then
      stat_fail
    else
      rm_daemon rtorrent
      stat_done
    fi
    ;;
  restart)
    $0 stop
    sleep 1
    $0 start
    ;;
  *)
    echo "usage: $0 {start|stop|restart}"
esac
exit 0

```

Убедитесь в том, чтобы заменить USER на имя пользователя, который будет запускать rtorrent.

Сделайте файл исполняемым:

```
# chmod +x /etc/rc.d/rtorrent

```

Создание файла `.rtorrent.rc` с относительными путями в домашнем каталоге пользователя сорвет выполнение скрипта rc.d. Для того что-бы запускать множество экземпляров rTorrent с относительными путями под разными учетными записями замените строку 9 в файле `/etc/rc.d/rtorrent` следующим содержимым:

```
   su username -c 'cd /home/username && screen -d -m -S rtorrent rtorrent' &> /dev/null

```

Альтернативно вы можете установить абсолютные пути в конфигурационном файле.

To run the daemon user multiple users create one rc.d script for each user. Then replace line 9 in `/etc/rc.d/rtorrent` with the following:

```
   su - username -c 'killall -w -s 2 /usr/bin/rtorrent' &> /dev/null

```

Для соединения с процессом демона на удаленной машине используйте [SSH](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)"):

```
$ ssh -t rtorrent@192.168.1.10 'screen -r'

```

Или если вы использовали [tmux](/index.php/Tmux "Tmux") вместо [GNU Screen](/index.php/GNU_Screen "GNU Screen"):

```
$ ssh -t rtorrent@192.168.1.10 'tmux attach -t rtorrent'

```

Для дополнительной информации о скриптах работающих в фоновом режиме смотрте: [Writing rc.d scripts](/index.php/Writing_rc.d_scripts "Writing rc.d scripts")

Этот скрипт может быть найден в [rtorrent-daemon-git](https://aur.archlinux.org/packages.php?ID=56458) репозитория AUR.

Другие скрипты могут быть найдены на следующих страницах: [Joyent CodeSnippets](http://codesnippets.joyent.com/posts/show/1947) и [ByteTouch](http://www.bytetouch.com/blog/linux/how-to-rtorrent-with-screen-on-debian/).

### Резерв места, предупреждение фрагментации (pre-allocation)

Пакету rTorrent не хватает резерва места (pre-allocation). Компиляция rTorrent с резервом места позволяет выделить место для файлов до загрузки торрента. Главная выгода заключается в том что это ограничивает и предотвращает фрагментацию файловой системы. Однако, это создает задержку во время резерва места если файловая система не поддерживает системный вызов fallocate естественным путем.

Таким образом этот ключ рекомендуется для файловых систем, таких как: xfs, ext4 и btrfs, которые имеют "родную" поддержку системного вызова fallocate. В них не происходит задержки во время резерва места и фрагментирования файловой системы. Резерв места на других файловых системах создает задержку но не фрагментирует файлы.

Для того что-бы сделать резерв места доступным, перекомпилируйте libtorrent из дерева [ABS](/index.php/ABS "ABS") со следующим ключом:

```
 $ ./configure --prefix=/usr --disable-debug --with-posix-fallocate

```

Для того что-бы его включить добавьте следующие строки в ваш конфигурационный файл `~/rtorrent.rc`:

 `~/rtorrent.rc` 
```
  # Резервирование места под файлы; сокращает фрагментацию файлов на файловой системе.
  system.file_allocate.set = yes

```

### Управление законченными файлами

**Примечание:** Currently, this part requires either the svn version of rtorrent/libtorrent or having applied the patch to 0.8.6 that adds 'equal'.

**Примечание:** If you're having trouble with this tip, it's probably easier to follow [this](http://libtorrent.rakshasa.no/wiki/RTorrentCommonTasks#Movecompletedtorrentstodifferentdirectorydependingonwatchdirectory)

Возможно задать приложению rtorrent сортировать законченные данные по указанным каталогам согласно тому в какой 'watch' каталог вы закинули тот или иной торрент во процессе продолжения его раздачи. It is possible to have rtorrent sort completed torrent data to specific folders based on which 'watch' folder you drop the *.torrent into while continuing to seed. Множество примеров показывают как этого добиться с торрентами загруженными с помощью rtorrent. Основное осложнение заключается в том что если вы попытаетесь закинуть на 100% законченный торрент и указать приложению rtorrent сверить данные и продолжить, данные не будут сортированными.

В качестве решения используйте следующий пример в вашем ~/.rtorrent.rc. Убедитесь в том что поменяли пути на нужные вам.

```
# месторасположение данных нового торрента и место куда должны быть помещены
# 'законченные' данные перед тем как вы поместите файлы торрентов в каталог наблюдения
directory = /home/user/torrents/incomplete

# назначить событие таймера под названием 'watch_directory_1':
# 1) срабатывать через 10 секунд после запуска rtorrent"а
# 2) а затем срабатывать с интервалом в каждые 10 секунд
# 3) По срабатыванию пытаться загрузить (и запустить) новые файлы торрентов найденные в /home/user/torrents/watch/
# 4) передать переменной под названием 'custom1' значение "/home/user/torrents/complete"
# На заметку: если вы не желаете что-бы скрипт автоматически запускал торрент, измените 'load_start' на 'load'
schedule = watch_directory_1,10,10,"load_start=/home/user/torrents/watch/*.torrent,d.set_custom1=/home/user/torrents/complete"

# вставить метод с псевдонимом 'checkdirs1'
# 1) вернуть "истинно" (true) если текущий путь данных торрента не равен значению переменной custom1
# 2) в противном случае вернуть "ложно" (false)
system.method.insert=checkdirs1,simple,"not=\"$equal={d.get_custom1=,d.get_base_path=}\""

# вставить метод с псевдонимом 'movecheck1'
# 1) вернуть "истинно" если все 3 команды вернули "истинно"
#    ('результат checkdirs1' && 'торрент на 100% завершен', 'поставлена переменная custom1')
# 2) в противном случае вернуть "ложно"
system.method.insert=movecheck1,simple,"and={checkdirs1=,d.get_complete=,d.get_custom1=}"

# вставить метод с псевдонимом 'movedir1'
# (последовательность команд разделенных с помощью ';') 
# 1) "установить путь равным значению переменной custom1";
# 2) "mv -u <current data path> <custom1 path>";
# 3) "очистить custom1", "остановить торрент","возобновить торрент"
# 4) остановить торрент
# 5) запустить торрент (дать торренту обновить "базовый путь")
system.method.insert=movedir1,simple,"d.set_directory=$d.get_custom1=;execute=mv,-u,$d.get_base_path=,$d.get_custom1=;d.set_custom1=;d.stop=;d.start="

# поставить ключ с именем 'move_hashed1' который будет запускаться событием hash_done.
# 1) По завершению хеширования торрента сработает этот пользовательский ключ.
# 2) по срабатыванию выполнить метод 'movecheck1' и проверить возвращаемое значение.
# 3) если метод 'movecheck' возвращает "истинно" выполнить метод 'movedir1' вставленный нами ранее.
# На заметку: 'branch' это условный оператор 'if': if(movecheck1){movedir1}
system.method.set_key=event.download.hash_done,move_hashed1,"branch={$movecheck1=,movedir1=}"
```

Вы можете добавить дополнительные каталоги наблюдения если вы хотите отсортировать ваши торренты в особом порядке.

На пример, если вы хотите что-бы ваши торренты загружались в:

```
/home/user/torrents/incomplete

```

а затем отсортировать данные торрентов основываясь на том куда вы закинули файл торрента:

```
/home/user/torrents/watch => /home/user/torrents/complete
/home/user/torrents/watch/iso => /home/user/torrents/complete/iso
/home/user/torrents/watch/music => /home/user/torrents/complete/music

```

Вы можете записать следующие строки в ваш .rtorrent.rc:

```
directory = /home/user/torrents/incomplete
schedule = watch_directory_1,10,10,"load_start=/home/user/torrents/watch/*.torrent,d.set_custom1=/home/user/torrents/complete"

schedule = watch_directory_2,10,10,"load_start=/home/user/torrents/watch/iso/*.torrent,d.set_custom1=/home/user/torrents/complete/iso"

schedule = watch_directory_3,10,10,"load_start=/home/user/torrents/watch/music/*.torrent,d.set_custom1=/home/user/torrents/complete/music"

system.method.insert=checkdirs1,simple,"not=\"$equal={d.get_custom1=,d.get_base_path=}\""
system.method.insert=movecheck1,simple,"and={checkdirs1=,d.get_complete=,d.get_custom1=}"
system.method.insert=movedir1,simple,"d.set_directory=$d.get_custom1=;execute=mv,-u,$d.get_base_path=,$d.get_custom1=;d.set_custom1=;d.stop=;d.start="
system.method.set_key=event.download.hash_done,move_hashed1,"branch={$movecheck1=,movedir1=}"
```

Смотрите также [pyroscope](http://code.google.com/p/pyroscope/) особенно примеры rtcontrol. Там также есть пакет AUR.

#### Уведомления с почтой Гугла

Сотовые операторы позволяют вам отправлять электронные письма на ваш телефон:

```
Verizon: 10digitphonenumber@vtext.com
AT&T: 10digitphonenumber@txt.att.net
Former AT&T customers: 10digitphonenumber@mmode.com
Sprint: 10digitphonenumber@messaging.sprintpcs.com
T-Mobile: 10digitphonenumber@tmomail.net
Nextel: 10digitphonenumber@messaging.nextel.com
Cingular: 10digitphonenumber@cingularme.com
Virgin Mobile: 10digitphonenumber@vmobl.com
Alltel: 10digitphonenumber@alltelmessage.com OR
10digitphonenumber@message.alltel.com
CellularOne: 10digitphonenumber@mobile.celloneusa.com
Omnipoint: 10digitphonenumber@omnipointpcs.com
Qwest: 10digitphonenumber@qwestmp.com
Telus: 10digitphonenumber@msg.telus.com
Rogers Wireless: 10digitphonenumber@pcs.rogers.com
Fido: 10digitphonenumber@fido.ca
Bell Mobility: 10digitphonenumber@txt.bell.ca
Koodo Mobile: 10digitphonenumber@msg.koodomobile.com
MTS: 10digitphonenumber@text.mtsmobility.com
President's Choice: 10digitphonenumber@txt.bell.ca
Sasktel: 10digitphonenumber@sms.sasktel.com
Solo: 10digitphonenumber@txt.bell.ca

```

*   Установите программу mailx предоставляемую через [mailx-heirloom](https://www.archlinux.org/packages/?name=mailx-heirloom) пакет расположенный в официальных репозиториях [Official repositories (Русский)](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

*   Очистите файл `/etc/mail.rc` и введите:

**Примечание:** Older versions of Heirloom's mailx use `/etc/nail.rc`.

```
set sendmail="/usr/bin/mailx"
set smtp=smtp.gmail.com:587
set smtp-use-starttls
set ssl-verify=ignore
set ssl-auth=login
set smtp-auth-user=USERNAME@gmail.com
set smtp-auth-password=PASSWORD

```

Теперь для того что-бы передать сообщение мы должны перенаправить его на стандартный вход программы mailx.

*   Make a Bash script:

 `/path/to/mail.sh` 
```
echo "$@: Done" | mailx 5551234567@vtext.com

```

Где $@ это переменная содержащая все аргументы переданные нашему скрипту.

*   И на конец, добавьте одну важную строку в файл `~/.rtorrent.rc` :

```
system.method.set_key = event.download.finished,notify_me,"execute=/path/to/mail.sh,$d.get_name="

```

Breaking it down:

`notify_me` идентификатор команды который может быть использован другими командами которые могут быть абсолютно любыми пока они уникальны.

`execute=` это команда rtorrent'а, в данном случае для выполнения команды оболочки.

`/path/to/mail.sh` это имя нашего скрипта (или любой команды которую вы хотите исполнить) с последующим списком передаваемых ключей/аргументов разделенных запятыми.

`$d.get_name=` 'd' это псевдоним для чего угодно запускаемого командой, get_name это имя функции возвращающей имя нашей загрузки и '$' говорит rTorrent'у заменить команду ее выводом перед тем как он вызовет запуск.

The end result? When that torrent, 'All Live Nudibranches', that we started before leaving for work finishes, we will be texted:

```
All Live Nudibranches: Done

```

### Displaying active torrents

The rtorrent doesn't list the active tab properly by default, add this line to your `.rtorrent.rc` to show only active torrents

```
schedule = filter_active,30,30,"view_filter = active,\"or={d.get_up_rate=,d.get_down_rate=}\""

```

Then press `9` in your rTorrent client to see the changes in action.

## Troubleshooting

### CA certificates

To use rTorrent with a tracker that uses HTTPS, do the following as root:

```
# cd /etc/ssl/certs

# wget --no-check-certificate [https://www.geotrust.com/resources/root_certificates/certificates/Equifax_Secure_Global_eBusiness_CA-1.cer](https://www.geotrust.com/resources/root_certificates/certificates/Equifax_Secure_Global_eBusiness_CA-1.cer)

# mv Equifax_Secure_Global_eBusiness_CA-1.cer Equifax_Secure_Global_eBusiness_CA-1.pem

# c_rehash

```

And from now on run rTorrent with:

```
$ rtorrent -o http_capath=/etc/ssl/certs

```

If you use GNU Screen, update the `.screenrc` configuration file to reflect this change:

```
$ screen -t rtorrent rtorrent -o http_capath=/etc/ssl/certs

```

In rTorrent 0.8.9, set `network.http.ssl_verify_peer.set=0` to fix the problem.

For more information see: [rTorrent Error & CA Certificate](https://bbs.archlinux.org/viewtopic.php?pid=331850) and [rTorrent Certificates Problem](https://bbs.archlinux.org/viewtopic.php?id=45800)

## Web interface

There are numerous web interfaces and front ends for rTorrent including:

*   [WTorrent](/index.php/WTorrent "WTorrent") is a web interface to rtorrent programmed in php using Smarty templates and XMLRPC for PHP library.
*   [nTorrent](http://code.google.com/p/ntorrent/) is a graphical user interface client to rtorrent (a cli torrent client) written in Java.
*   [rTWi](http://projects.cyla.homeip.net/rtwi/) is a simple rTorrent web interface written in PHP.
*   [Rtgui](/index.php/Rtgui "Rtgui") is a web based front end for rTorrent written in PHP and uses XML-RPC to communicate with the rTorrent client.
*   [rutorrent](http://code.google.com/p/rutorrent/) and [Forum](http://forums.rutorrent.org/) - A web-based front-end with an interface very similar to uTorrent which supports many plugins and advanced features (см. также: [RuTorrent](/index.php/RuTorrent_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "RuTorrent (Русский)") и [Guide for rTorrent + ruTorrent Installation](https://bbs.archlinux.org/viewtopic.php?pid=897577#p897577)).

**Примечание:** rTorrent is currently built using [XML-RPC for C/C++](http://xmlrpc-c.sourceforge.net/), which is required for some web interfaces (e.g. ruTorrent).

### XMLRPC interface

If you want to use rtorrent with some web interfaces (e.g. rutorrent) you need to add the following line to the configuration file:

```
scgi_port = localhost:5000

```

For more information see: [Using XMLRPC with rtorrent](http://libtorrent.rakshasa.no/wiki/RTorrentXMLRPCGuide)

## See also

*   [GNU Screen](/index.php/GNU_Screen "GNU Screen")
*   [Comparison of BitTorrent clients](https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients "wikipedia:Comparison of BitTorrent clients") on Wikipedia
*   [rTorrent Community Wiki](http://community.rutorrent.org/) - A public place for information on rTorrent and any project related to rTorrent, regarding setup, configuration, operations, and development
*   [PyroScope](https://code.google.com/p/pyroscope/) - A collection of command line tools for rTorrent. It provides commands for creating and modifying torrent files, moving data on completion without having multiple watch folders, and mass-controlling download items via rTorrent's XML-RPC interface: searching, start/stop, deleting items with or without their data, etc. It also offers a documented [Python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)") API
*   [How-to Install rTorrent and Hellanzb on CentOS 5 64-bit VPS](http://wiki.theaveragegeek.com/howto/installing_rtorrent_and_hellanzb_on_centos5_64-bit_vps)
*   [Installation Guide for rTorrent and Pryoscope on Debian](https://code.google.com/p/pyroscope/wiki/DebianInstallFromSource) - A collection of tools for the BitTorrent protocol and especially the rTorrent client
*   [mktorrent](http://mktorrent.sourceforge.net/) - A command line application used to generate torrent files, which is available as [mktorrent](https://www.archlinux.org/packages/?name=mktorrent) in the [Official repositories (Русский)](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

**Forum threads**

*   2009-03-11 - Arch Linux - [HOWTO: rTorrent stats in Conky](https://bbs.archlinux.org/viewtopic.php?id=67304)