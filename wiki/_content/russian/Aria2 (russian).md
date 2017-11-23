**Состояние перевода:** На этой странице представлен перевод статьи [Aria2](/index.php/Aria2 "Aria2"). Дата последней синхронизации: 21 ноября 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Aria2&diff=0&oldid=497127).

С домашней страницы [проекта](https://aria2.github.io/):

	*aria2 - это легкая мультипротокольная и многопоточная консольная утилита загрузки. Она поддерживает [HTTP](https://en.wikipedia.org/wiki/ru:HTTP и [Metalink](https://en.wikipedia.org/wiki/ru:Metalink "wikipedia:ru:Metalink"). aria2 можно управлять с помощью встроенных интерфейсов [JSON-RPC](https://en.wikipedia.org/wiki/ru:JSON-RPC "wikipedia:ru:JSON-RPC") и [XML-RPC](https://en.wikipedia.org/wiki/ru:XML-RPC "wikipedia:ru:XML-RPC").*

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 aria2.conf](#aria2.conf)
    *   [2.2 Пример aria2.conf](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_aria2.conf)
        *   [2.2.1 Детали опций](#.D0.94.D0.B5.D1.82.D0.B0.D0.BB.D0.B8_.D0.BE.D0.BF.D1.86.D0.B8.D0.B9)
            *   [2.2.1.1 Пример входного файла #1](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D0.B2.D1.85.D0.BE.D0.B4.D0.BD.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.231)
            *   [2.2.1.2 Пример входного файла #2](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D0.B2.D1.85.D0.BE.D0.B4.D0.BD.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.232)
        *   [2.2.2 Дополнительные замечания](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B0.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [2.3 Пример aria2.rapidshare](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_aria2.rapidshare)
        *   [2.3.1 Описание опций](#.D0.9E.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D0.BF.D1.86.D0.B8.D0.B9)
        *   [2.3.2 Дополнительные замечания](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B0.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D1.8F_2)
    *   [2.4 Пример aria2.bittorrent](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_aria2.bittorrent)
        *   [2.4.1 Описание опций](#.D0.9E.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D0.BF.D1.86.D0.B8.D0.B9_2)
    *   [2.5 Пример aria2.daemon](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_aria2.daemon)
*   [3 Интерфейс](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81)
    *   [3.1 Веб-интерфейсы](#.D0.92.D0.B5.D0.B1-.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B)
    *   [3.2 Другие интерфейсы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B)
*   [4 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [4.1 Скачать пакеты без установки](#.D0.A1.D0.BA.D0.B0.D1.87.D0.B0.D1.82.D1.8C_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B_.D0.B1.D0.B5.D0.B7_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [4.2 pacman XferCommand](#pacman_XferCommand)
    *   [4.3 Изменение User Agent](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_User_Agent)
    *   [4.4 Использование Aria2 с makepkg](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Aria2_.D1.81_makepkg)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Установите [aria2](https://www.archlinux.org/packages/?name=aria2) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Также можете поставить [aria2-systemd](https://github.com/GutenYe/systemd-units/tree/master/aria2) для использования aria2 в качестве [демона](/index.php/Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemon (Русский)").

**Примечание:** Для запуска пакета aria2 используется команда `aria2c`. Данное наименование было сохранено для обратной совместимости.

## Настройка

### aria2.conf

aria2 использует файл `$XDG_CONFIG_HOME/aria2/aria2.conf` для установки глобальных параметров по умолчанию. Это поведение может быть изменено переключателем `--conf-path`:

*   Скачайте `aria2.example.rar` используя параметры, указанные в файле настроек `/file/aria2.rapidshare`

```
$ aria2c --conf-path=/file/aria2.rapidshare http://rapidshare.com/files/12345678/aria2.example.rar

```

Если существует `$XDG_CONFIG_HOME/aria2/aria2.conf` и параметры, указанные в `/file/aria2.rapidshare` нужны, то переключатель `--no-conf` должен быть добавлен к команде:

*   Не использовать файл настроек по умолчанию и скачать `aria2.example.rar`, используя параметры, указанные в файле настроек `/file/aria2.rapidshare`

```
$ aria2c --no-conf --conf-path=/file/aria2.rapidshare http://rapidshare.com/files/12345678/aria2.example.rar

```

Если `$XDG_CONFIG_HOME/aria2/aria2.conf` пока не существует, и вы хотите упростить управление параметрами настроек:

```
$ touch $XDG_CONFIG_HOME/aria2/aria2.conf

```

### Пример aria2.conf

```
continue
dir=${HOME}/Desktop
file-allocation=none
input-file=${HOME}/.aria2/input.conf
log-level=warn
max-connection-per-server=4
min-split-size=5M
on-download-complete=exit

```

Это по существу тоже самое, что и при выполнении:

```
$ aria2c dir=${HOME}/Desktop file-allocation=none input-file=${HOME}/.aria2/input.conf on-download-complete=exit log-level=warn FILE

```

**Примечание:** Пример файла aria2.conf, приведенный выше, может неверно использовать переменную $HOME. Некоторые пользователи сообщали о том, что использование фигурных скобок приводит к созданию отдельной поддиректории ${HOME} в рабочем каталоге aria2\. Такую директорию может быть сложно обработать, так как bash будет принимать ее за переменную окружения $HOME. В текущий момент рекомендуется использовать абсолютные пути в aria2.conf.

#### Детали опций

	`continue`

	Продолжить загрузку частично загруженного файла, если существует соответствующий файл управления.

	`dir=${HOME}/Desktop`

	Каталог для сохранения загруженных файлов `~/Desktop`.

	`file-allocation=none`

	Указать метод резервирования места для файла. **none** - не происходит предварительное резервирование места для файла. **prealloc** - предварительное резервирование места для файла перед началом загрузки. (По умолчанию: prealloc) 

	`input-file=${HOME}/.aria2/input.conf`

	Скачать список построчно, или разделённых TAB'ом URI, найденных в `./aria2/input.conf`

	`log-level=warn`

	Задать уровень вывода событий на консоль. warn - только для вывода предупреждений и ошибок (По умолчанию: debug)

	`max-connection-per-server=4`

	Максимально количество соединений (4) с одним сервером для каждой загрузки. (По умолчанию: 1)

	`min-split-size=5M`

	Разбить файл, только если размер больше, чем 2*5MB = 10MB. (По умолчанию: 20M)

	`on-download-complete=exit`

	Выполнить команду `exit` и выйти из оболочки, когда сессия загрузки завершена.

##### Пример входного файла #1

*   Загрузка `aria2-1.10.0.tar.bz2` из двух отдельных источников, до соединения в `~/Desktop` `aria2-1.10.0.tar.bz2`

```
http://aria2.net/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2    http://sourceforge.net/projects/aria2/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2

```

##### Пример входного файла #2

*   Загрузить `aria2-1.9.5.tar.bz2` и сохранить в `/file/old` как `aria2.old.tar.bz2` &
*   Загрузить `aria2-1.10.0.tar.bz2` и сохранить в `~/Desktop` как `aria2.new.tar.bz2`

```
http://aria2.net/files/stable/aria2-1.9.5/aria2-1.9.5.tar.bz2
  dir=/file/old
  out=aria2.old.tar.bz2
http://aria2.net/files/stable/aria2-1.10.0/aria2-1.10.0.tar.bz2
  out=aria2.new.tar.bz2

```

#### Дополнительные замечания

	 `--file-allocation=falloc`

	Рекомендуется для новых файловых систем, таких как ext4 (с поддержкой экстентов), btrfs или xfs, потому что он выделяет большие файлы (ГБ) практически мгновенно. Не используйте falloc с устаревшими файловыми системами, такими как ext3, так как prealloc потребляет примерно такое же количество времени как и стандартное распределение, возможна блокировка процессов загрузки aria2.

**Совет:** Для ознакомления с полным перечнем опций настройки смотрите `aria2c --help=#all` и страницу документации aria2.

### Пример aria2.rapidshare

```
http-user=USER_NAME
http-passwd=PASSWORD
allow-overwrite=true
dir=/file/Downloads
file-allocation=falloc
enable-http-pipelining=true
input-file=/file/input.rapidshare
log-level=error
max-connection-per-server=2
summary-interval=120

```

#### Описание опций

	`http-user=USER_NAME`

	Устанавливает HTTP [имя пользователя](https://en.wikipedia.org/wiki/User_(computing) как USER_NAME для входа в систему защищённую паролем. Это влияет на все [URIs](https://en.wikipedia.org/wiki/ru:Uniform_Resource_Identifier "wikipedia:ru:Uniform Resource Identifier").

	`http-passwd=PASSWORD`

	Устанавливает HTTP [Пароль](https://en.wikipedia.org/wiki/ru:%D0%9F%D0%B0%D1%80%D0%BE%D0%BB%D1%8C "wikipedia:ru:Пароль") как PASSWORD для входа в систему защищённую паролем. Это влияет на все URIs.

	`allow-overwrite=true`

	Удалять контрольный файл перед загрузкой. При использовании с --allow-overwrite=true файл всегда загружается с нуля. Это может понадобиться пользователям за прокси-сервером, который блокирует возобновление загрузки. (По умолчанию: false)

	`dir=/file/Downloads`

	Загружать файл(ы) в `/file/Downloads`.

	`file-allocation=falloc`

	Указать метод резервирования места для файла [posix_fallocate()](http://www.kernel.org/doc/man-pages/online/pages/man2/fallocate.2.html). (По умолчанию: prealloc)

	`enable-http-pipelining=true`

	Включить [HTTP/1.1 конвейерную обработку](https://en.wikipedia.org/wiki/ru:HTTP_Pipelining "wikipedia:ru:HTTP Pipelining") чтобы преодолеть задержки в сети и уменьшить нагрузку на сеть. (По умолчанию: false)

	`input-file=/file/input.rapidshare`

	Загрузить URI, перечисленные в файле input.rapidshare. Вы можете указать различные источники для одного объекта, перечислив различные URI в строке, разделенных символом TAB (табуляция). Дополнительные параметры можно указывать после каждой URI-строки. Cтроки параметров должны начинаться с одного или нескольких пробелов (SPACE или TAB) и содержать один параметр на строку. `/file/input.rapidshare`

	`log-level=error`

	Задать уровень вывода журнала событий.В данном случае вывод только ошибок. (По умолчанию: debug)

	`max-connection-per-server=2`

	Максимально количество соединений с одним сервером для каждой загрузки 2\. (По умолчанию: 1)

	`summary-interval=120`

	Задать интервал в секундах (120) до вывода сообщения о прогрессе загрузки. Установка 0 запрещает вывод. (По умолчанию: 60) 

#### Дополнительные замечания

*   Так как файл `aria2.rapidshare` содержит имя пользователя и пароль, рекомендуется установить права на файл 600, или аналогичные.

```
$ cd /file
$ chmod 600 /file/aria2.rapidshare
$ ls -l
total 128M
-rw------- 1 arch users  167 Aug 20 00:00 aria2.rapidshare

```

	 `summary-interval=0`

	Подавляет ход процесса загрузки и может улучшить общую производительность. Журнал будет продолжать выводиться в соответствии со значениями, указанными в опции журнала уровней `log-level`.

**Совет:** Пример файла настройки также может быть применён к [Hotfile](http://www.hotfile.com/), [DepositFiles](http://depositfiles.com/), и т.д. и т.п.

**Примечание:** Параметры командной строки всегда имеют преимущество перед параметрами, перечисленных в файле настроек.

### Пример aria2.bittorrent

```
bt-seed-unverified
max-overall-upload-limit=1M
max-upload-limit=128K
seed-ratio=5.0
seed-time=240

```

#### Описание опций

	`bt-seed-unverified=false`

	Не проверять хеш файла (ов), перед раздачей. (По умолчанию: true)

	`max-overall-upload-limit=1M`

	Установить максимальную скорость загрузки в 1MB/сек. (По умолчанию: 0)

	`max-upload-limit=128K`

	Задать максимальную скорость отдачи каждого узла торрента в 128K/сек. (По умолчанию: 0)

	`seed-ratio=5.0`

	Указать рейтинг. Сидировать завершенные торренты, пока рейтинг не станет больше 5.0\. (По умолчанию: 1.0)

	`seed-time=240`

	Указать время сидирования (раздачи) 240 минут.

**Примечание:** Если оба `seed-ratio` и `seed-time` указаны, сидирование заканчивается, когда по крайней мере одно из условий выполнено.

### Пример aria2.daemon

Эта настройка может быть использована для запуска Aria2 в качестве службы. Также может использоваться в сочетании с несколькими интерфейсами, перечисленными ниже. Обратите внимание, что RPC-пользователя и rpc-pass устарели, но большинство интерфейсов не были ещё портированы на новую аутентификацию. Не забудьте изменить пароль пользователя, и каталог Загрузки.

```
continue
daemon=true
dir=/home/aria2/Downloads
file-allocation=falloc
log-level=warn
max-connection-per-server=4
max-concurrent-downloads=3
max-overall-download-limit=0
min-split-size=5M
enable-http-pipelining=true

enable-rpc=true
rpc-listen-all=true
rpc-user=rpcuser
rpc-passwd=rpcpass

```

## Интерфейс

**Примечание:** Настройки осуществляемые во фронтэндах не влияют на собственные настройки `aria2`, и неясно, повторяют ли различные интерфейсы настройку `aria2`, если обычная была сделана. Пользователи должны гарантировать, что их желаемые параметры эффективно реализуется в рамках отдельных утилит, и что они хранятся постоянно (Uget, например, имеет командную строку своего собственного `aria2`, который сохраняется после перезагрузки)

### Веб-интерфейсы

**Примечание:** Для работы этих фронтэндов, `aria2c` нужно запускать с `--enable-rpc`. Они предназначены для работы на локальном компьютере, а не на удаленном сервере, используя aria для загрузок.

*   **YaaW** — Yet это Aria2 веб-интерфейс на чистом HTML/CSS/Javascirpt.

	[https://github.com/binux/yaaw](https://github.com/binux/yaaw) || [yaaw-git](https://aur.archlinux.org/packages/yaaw-git/)

*   **Webui** — Html фронтэнд для aria2.

	[https://github.com/ziahamza/webui-aria2](https://github.com/ziahamza/webui-aria2) || [webui-aria2](https://aur.archlinux.org/packages/webui-aria2/)

*   **aria2rpc** — Инструмент командной строки для подключения к удаленному экземпляру `aria2c`. Если `aria2c` установлена его можно найти в `/usr/share/doc/aria2/xmlrpc/aria2rpc`.

	[https://github.com/tatsuhiro-t/aria2/blob/master/doc/xmlrpc/aria2rpc](https://github.com/tatsuhiro-t/aria2/blob/master/doc/xmlrpc/aria2rpc) || [aria2](https://www.archlinux.org/packages/?name=aria2)

### Другие интерфейсы

**Примечание:** Эти фронтэнды **не нужны** `aria2c` для запуска с функцией `--enable-rpc`.

*   **aria2fe** — Графический интерфейс CLI-based утилиты загрузок aria2.

	[http://sourceforge.net/projects/aria2fe/](http://sourceforge.net/projects/aria2fe/) || [aria2fe](https://aur.archlinux.org/packages/aria2fe/)

*   **Diana** — Инструмент командной строки для aria2

	[https://github.com/baskerville/diana](https://github.com/baskerville/diana) || [diana-git](https://aur.archlinux.org/packages/diana-git/)

*   **downloadm** — Ускоритель/менеджер загрузки использующий aria2c как бакэнд.

	[http://sourceforge.net/projects/downloadm/](http://sourceforge.net/projects/downloadm/) || [downloadm](https://aur.archlinux.org/packages/downloadm/)

*   **eatmonkey** — Менеджер загрузок для Xfce, который работает с aria2.

	[http://goodies.xfce.org/projects/applications/eatmonkey](http://goodies.xfce.org/projects/applications/eatmonkey) || [eatmonkey](https://aur.archlinux.org/packages/eatmonkey/)

*   **karia2** — QT4 интерфейс для aria2 менеджера загрузок.

	[http://sourceforge.net/projects/karia2/](http://sourceforge.net/projects/karia2/) || [karia2-svn](https://aur.archlinux.org/packages/karia2-svn/)

*   **uGet** — Многофункциональный, многопоточный, с поддержкой докачки GTK+/CLI менеджер загрузок, который может использовать aria2 как бэкэнд, встроенный плагин.

	[http://ugetdm.com](http://ugetdm.com) || [uget](https://www.archlinux.org/packages/?name=uget)

*   **yaner** — GTK+ интерфейс для менеджера загрузок aria2.

	[http://iven.github.com/Yaner](http://iven.github.com/Yaner) || [yaner-git](https://aur.archlinux.org/packages/yaner-git/)

## Советы и хитрости

### Скачать пакеты без установки

Просто воспользуйтесь командой, приведенной ниже:

```
 # pacman -Sp packages | aria2c -i -

```

`pacman -Sp` покажет список адресов пакетов в стандартном выводе (stdout) вместо того, чтобы загрузить, затем `|` передаст их для следующей команды. И, наконец `-i` в `aria2c -i -` скажет aria2c, что URL-адреса для скачиваемых файлов должны быть считаны из указанного файла, но так как добавлен `-`, значит URL-адреса нужно брать из стандартного ввода (stdin).

### pacman XferCommand

Смотрите [pacman/Tips and tricks#aria2](/index.php/Pacman/Tips_and_tricks#aria2 "Pacman/Tips and tricks").

### Изменение User Agent

Некоторые сайты могут фильтровать запросы на основе вашего User Agent, поскольку Aria2 малоизвестный загрузчик, может оказаться полезным изменить User Agent, представляясь известным загрузчиком или браузером. Просто используйте опцию -U, как здесь:

```
$ aria2c -UWget http://some-url-to-download/file.xyz

```

Вы можете использовать все, что пожелаете, например **-UMozilla/5.0** и т.д.

### Использование Aria2 с makepkg

Вы можете использовать <a class="mw-selflink selflink">Aria2 (Русский)</a> вместо curl для скачивания файлов-исходников, просто измените переменную `DLAGENTS` следующим образом:

 `/etc/makepkg.conf` 
```
[...]
DLAGENTS=('ftp::/usr/bin/aria2c -UWget -s4 %u -o %o'
          'http::/usr/bin/aria2c -UWget -s4 %u -o %o'
          'https::/usr/bin/aria2c -UWget -s4 %u -o %o'
          'rsync::/usr/bin/rsync -z %u %o'
          'scp::/usr/bin/scp -C %u %o')
[...]
```

**Примечание:** Используйте параметр `-UWget` для изменения пользовательского агента на Wget. Это может предотвратить проблемы при загрузке с сайтов, которые фильтрует запросы, основанные на агенте пользователя (user agent), чтобы избежать проблемы доступа к URL-адресу. Поскольку Aria2 малоизвестный загрузчик, он может быть ошибочно распознан как браузер. Изменение пользовательского агента на Wget может решить большинство проблем.

## Смотрите также

*   [Руководство](https://aria2.github.io/manual/ru/html/index.html) - Официальное руководство aria2 на Русском
*   [Примеры использования](https://aria2.github.io/manual/ru/html/aria2c.html#id28) - официальный сайт