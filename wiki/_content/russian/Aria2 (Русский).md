С домашней страницы [проекта](http://aria2.sourceforge.net/):

	*aria2 - это легкая мультипротокольная и многопоточная консольная утилита. Она поддерживает [HTTP](https://en.wikipedia.org/wiki/ru:HTTP и [Metalink](https://en.wikipedia.org/wiki/ru:Metalink "wikipedia:ru:Metalink").* aria2 *можно управлять с помощью встроенных интерфейсов [JSON-RPC](https://en.wikipedia.org/wiki/ru:JSON-RPC "wikipedia:ru:JSON-RPC") и [XML-RPC](https://en.wikipedia.org/wiki/ru:XML-RPC "wikipedia:ru:XML-RPC").*

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Выполнение](#.D0.92.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 aria2.conf](#aria2.conf)
    *   [3.2 Пример .bash_alias (псевдонимов Bash)](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.bash_alias_.28.D0.BF.D1.81.D0.B5.D0.B2.D0.B4.D0.BE.D0.BD.D0.B8.D0.BC.D0.BE.D0.B2_Bash.29)
    *   [3.3 Пример aria2.conf](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_aria2.conf)
        *   [3.3.1 Детали опций](#.D0.94.D0.B5.D1.82.D0.B0.D0.BB.D0.B8_.D0.BE.D0.BF.D1.86.D0.B8.D0.B9)
            *   [3.3.1.1 Пример входного файла #1](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D0.B2.D1.85.D0.BE.D0.B4.D0.BD.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.231)
            *   [3.3.1.2 Пример входного файла #2](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D0.B2.D1.85.D0.BE.D0.B4.D0.BD.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.232)
        *   [3.3.2 Дополнительные замечания](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B0.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [3.4 Пример aria2.rapidshare](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_aria2.rapidshare)
        *   [3.4.1 Детали опций](#.D0.94.D0.B5.D1.82.D0.B0.D0.BB.D0.B8_.D0.BE.D0.BF.D1.86.D0.B8.D0.B9_2)
        *   [3.4.2 Дополнительные замечания](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B0.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D1.8F_2)
    *   [3.5 Пример aria2.bittorrent](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_aria2.bittorrent)
        *   [3.5.1 Детали опций](#.D0.94.D0.B5.D1.82.D0.B0.D0.BB.D0.B8_.D0.BE.D0.BF.D1.86.D0.B8.D0.B9_3)
    *   [3.6 Пример aria2.daemon](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_aria2.daemon)
*   [4 Интерфейс](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81)
    *   [4.1 Веб-интерфейсы](#.D0.92.D0.B5.D0.B1-.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B)
    *   [4.2 Другие интерфейсы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B)
*   [5 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.1 Скачать пакеты без установки](#.D0.A1.D0.BA.D0.B0.D1.87.D0.B0.D1.82.D1.8C_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B_.D0.B1.D0.B5.D0.B7_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [5.2 pacman XferCommand](#pacman_XferCommand)
    *   [5.3 Минимальная пользовательская сборка](#.D0.9C.D0.B8.D0.BD.D0.B8.D0.BC.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B0.D1.8F_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B0)
    *   [5.4 Запуск aria2c при загрузке системы](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_aria2c_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [5.5 Изменение User Agent](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_User_Agent)
    *   [5.6 Использование Aria2 с makepkg](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Aria2_.D1.81_makepkg)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Установите [aria2](https://www.archlinux.org/packages/?name=aria2) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Также можете поставить [aria2-systemd](https://github.com/GutenYe/systemd-units/tree/master/aria2) для использования aria2 в качестве [демона](/index.php/Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemon (Русский)").

## Выполнение

Для исполняемого пакета aria2, есть имя `aria2c`. Такое имя было унаследовано для совместимости.

## Настройка

### aria2.conf

aria2 смотрит файл `~/.aria2/aria2.conf` для установки глобальных параметров по умолчанию. Это поведение может быть изменено переключателем `--conf-path`:

*   Скачайте `aria2.example.rar` используя параметры, указанные в файле настроек `/file/aria2.rapidshare`

```
$ aria2c --conf-path=/file/aria2.rapidshare http://rapidshare.com/files/12345678/aria2.example.rar

```

Если существует `~/.aria2/aria2.conf` и параметры, указанные в `/file/aria2.rapidshare` нужны, то переключатель `--no-conf` должен быть добавлен к команде:

*   Не использовать файл настроек по умолчанию и скачать `aria2.example.rar` используя параметры, указанные в файле настроек `/file/aria2.rapidshare`

```
$ aria2c --no-conf --conf-path=/file/aria2.rapidshare http://rapidshare.com/files/12345678/aria2.example.rar

```

Если `~/.aria2/aria2.conf` пока не существует, и вы хотите упростить управление параметрами настроек:

```
$ touch ~/.aria2/aria2.conf

```

### Пример .bash_alias (псевдонимов Bash)

```
alias down='aria2c --conf-path=${HOME}/.aria2/aria2.conf'
alias rapid='aria2c --conf-path=/file/aria2.rapidshare'

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

**Обратите внимание:** The example aria2.conf above may incorrectly use the $HOME variable. Some users have reported the curly brace syntax to explicitly create a separate ${HOME} subdirectory in the aria2 working directory. Such a directory may be difficult to traverse as bash will consider it to be the $HOME environment variable. For now, it is recommended to use absolute path names in aria2.conf.

#### Детали опций

	`continue`

	Продолжить загрузку частично загруженного файла.

	`dir=${HOME}/Desktop`

	Каталог для сохранения загруженных файлов `~/Desktop`.

	`file-allocation=none`

	Указать метод резервирования места для файла. **none** - не происходит предварительное резервирование места для файла. **prealloc** - предварительное резервирование места для файла перед началом загрузки. (По умолчанию: prealloc) 

	`input-file=${HOME}/.aria2/input.conf`

	Скачать список построчно, или разделённых TAB'ом URI, найденных в `~/.aria2/input.conf`

	`log-level=warn`

	Задать уровень вывода событий на консоль. warn - только для вывода предупреждений и ошибок (По умолчанию: debug)

	`max-connection-per-server=4`

	Максимально количество соединений (4) с одним сервером для каждой загрузки. (По умолчанию: 1)

	`min-split-size=5M`

	Разбить файл, только если размер больше, чем 2*5MB = 10MB. (По умолчанию: 20M)

	`on-download-complete=exit`

	Выполнить команду `exit` и выйти из оболочки, когда сессия загрузки завершена.

Для больших опций, смотрите [Основные параметры (Рус)](http://aria2.sourceforge.net/manual/ru/html/aria2c.html#id3).

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

	Рекомендуется для новых файловых систем, таких как ext4 (с поддержкой экстентов), Btrfs, или XFS, он выделяет большие файлы (ГБ) практически мгновенно. Не используйте falloc с наследием файловых систем, таких как ext3, prealloc потребляет примерно такое же количество времени в качестве стандартного распределения, возможна блокировка процесса aria2\. Подробнее о [возможных параметрах и рекомендациях](http://aria2.sourceforge.net/manual/ru/html/aria2c.html#cmdoption--file-allocation).

**Совет:** Также смотрите `aria2c --help=#all` и страницу man aria2.

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

#### Детали опций

	`http-user=USER_NAME`

	Установите HTTP [имя пользователя](https://en.wikipedia.org/wiki/User_(computing) как USER_NAME для входа в систему защищённого паролем. Это влияет на все [URIs](https://en.wikipedia.org/wiki/ru:Uniform_Resource_Identifier "wikipedia:ru:Uniform Resource Identifier").

	`http-passwd=PASSWORD`

	Установите HTTP [Пароль](https://en.wikipedia.org/wiki/ru:%D0%9F%D0%B0%D1%80%D0%BE%D0%BB%D1%8C "wikipedia:ru:Пароль") как PASSWORD для входа в систему защищённого паролем. то влияет на все URIs.

	`allow-overwrite=true`

	Удалять контрольный файл перед загрузкой. При использовании с --allow-overwrite=true файл всегда загружается с нуля. Это может понадобиться пользователям за прокси-сервером, который блокирует возобновление загрузки. (По умолчанию: false)

	`dir=/file/Downloads`

	Загружать файл(ы) в `/file/Downloads`.

	`file-allocation=falloc`

	Указать метод резервирования места для файла [posix_fallocate()](http://www.kernel.org/doc/man-pages/online/pages/man2/fallocate.2.html). (По умолчанию: prealloc) [Подробнее о возможных значениях](http://aria2.sourceforge.net/manual/ru/html/aria2c.html#cmdoption--file-allocation).

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

**Обратите внимание:** Параметры командной строки всегда имеют преимущество перед параметрами, перечисленных в файле настроек.

### Пример aria2.bittorrent

```
bt-seed-unverified
max-overall-upload-limit=1M
max-upload-limit=128K
seed-ratio=5.0
seed-time=240

```

#### Детали опций

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

**Обратите внимание:** Если оба `seed-ratio` и `seed-time` указаны, сидирование заканчивается, когда по крайней мере одно из условий выполнено.

### Пример aria2.daemon

Эта настройка может быть использована для запуска Aria2 в качестве службы. Также может использоваться в сочетании с несколькими фронтэндами, перечисленными ниже. Обратите внимание, что RPC-пользователя и rpc-pass устарели, но большинство фронтэндов не были ещё портированы на новую аутентификацию. Не забудьте изменить пароль пользователя, и каталог Загрузки.

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

**Обратите внимание:** Настройки осуществляемые во фронтэндах не влияют на собственные настройки `aria2`, и неясно, повторяют ли различные интерфейсы настройку `aria2`, если обычная была сделана. Пользователи должны гарантировать, что их желаемые параметры эффективно реализуется в рамках отдельных утилит, и что они хранятся постоянно (Uget, например, имеет командную строку своего собственного `aria2`, который прилипает после перезагрузки)

### Веб-интерфейсы

**Обратите внимание:** Для работы этих фронтэндов, `aria2c` нужно запускать с `--enable-rpc`. Они предназначены для работы на локальном компьютере, а не на удаленном сервере, используя aria для загрузок.

*   **YaaW** — Yet это Aria2 веб-интерфейс на чистом HTML/CSS/Javascirpt.

	[https://github.com/binux/yaaw](https://github.com/binux/yaaw) || [yaaw-git](https://aur.archlinux.org/packages/yaaw-git/)

*   **Webui** — Html фронтэнд для aria2.

	[https://github.com/ziahamza/webui-aria2](https://github.com/ziahamza/webui-aria2) || [webui-aria2](https://aur.archlinux.org/packages/webui-aria2/)

*   **aria2rpc** — Инструмент командной строки для подключения к удаленному экземпляру `aria2c`. Если `aria2c` установлена его можно найти в `/usr/share/doc/aria2/xmlrpc/aria2rpc`.

	[https://github.com/tatsuhiro-t/aria2/blob/master/doc/xmlrpc/aria2rpc](https://github.com/tatsuhiro-t/aria2/blob/master/doc/xmlrpc/aria2rpc) || [aria2](https://www.archlinux.org/packages/?name=aria2)

### Другие интерфейсы

**Обратите внимание:** Эти фронтэнды **не нужны** `aria2c` для запуска с функцией `--enable-rpc`.

*   **aria2fe** — Графический интерфейс CLI-based утилиты загрузок aria2.

	[http://sourceforge.net/projects/aria2fe/](http://sourceforge.net/projects/aria2fe/) || [aria2fe](https://aur.archlinux.org/packages/aria2fe/)

*   **Diana** — Инструмент командной строки для aria2

	[https://github.com/baskerville/diana](https://github.com/baskerville/diana) || [diana-git](https://aur.archlinux.org/packages/diana-git/)

*   **downloadm** — Загрузки ускоритель/менеджер использующий aria2c как бакэнд.

	[http://sourceforge.net/projects/downloadm/](http://sourceforge.net/projects/downloadm/) || [downloadm](https://aur.archlinux.org/packages/downloadm/)

*   **eatmonkey** — Менеджер загрузок для Xfce, который работает с aria2.

	[http://goodies.xfce.org/projects/applications/eatmonkey](http://goodies.xfce.org/projects/applications/eatmonkey) || [eatmonkey](https://aur.archlinux.org/packages/eatmonkey/)

*   **karia2** — QT4 интерфейс для aria2 менеджера загрузок.

	[http://sourceforge.net/projects/karia2/](http://sourceforge.net/projects/karia2/) || [karia2-svn](https://aur.archlinux.org/packages/karia2-svn/)

*   **uGet** — Многофункциональный, многопоточный, с поддержкой докачки GTK+/CLI менеджер загрузок, который может использовать aria2 как бэкэнд, встроенный плагин.

	[http://ugetdm.com](http://ugetdm.com) || [uget](https://www.archlinux.org/packages/?name=uget)

*   **yaner** — GTK+ интерфейс для менеджера загрузок aria2.

	[http://iven.github.com/Yaner](http://iven.github.com/Yaner) || [yaner-git](https://aur.archlinux.org/packages/yaner-git/)

Это удобно для добавления функции монитора на основе diana в файле настроек оболочки:

```
da(){
watch -ctn 1 "(echo -e '\033[32mGID\t\t Name\t\t\t\t\t\t\t%\tDown\tSize\tSpeed\tUp\tS/L\tTime\033[36m'; \
diana list| cut -c -112; echo -e '\033[37m'; diana stats)"
}

```

## Советы и хитрости

### Скачать пакеты без установки

Просто воспользуйтесь командой ниже:

```
 # pacman -Sp packages | aria2c -i -

```

`pacman -Sp` Список адресов пакетов на стандартный вывод вместо их загрузки, затем `|` пайпинг к следующей команде. И, наконец `-i` `aria2c -i -` переход к aria2c означает, что URL-адреса для скачиваемых файлов следует читать из указанного файла, но если `-` пропущен, то читать URL-адреса из стандартного ввода.

### pacman XferCommand

aria2 может быть использован в качестве менеджера загрузки по умолчанию для менеджера пакетов [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). Для подробностей смотрите статью ArchWiki [Повышение производительности pacman](/index.php/Improve_pacman_performance_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_aria2 "Improve pacman performance (Русский)").

### Минимальная пользовательская сборка

Можно получить выгоду в производительности, путем удаления неиспользуемых функций и протоколов. Дальнейшее повышение может быть достигнуто путем удаления поддержки внешних библиотек в пользовательской сборке. Доступные варианты видны через `./configure --help`. Смотрите страницу [сисетму сборки Arch](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") для более подробной информации.

### Запуск aria2c при загрузке системы

Save the following [systemd](/index.php/Systemd "Systemd") service file, adjust username and config path according to your setup. Ensure your config is set to deamonize (use `daemon=true`).

 `/etc/systemd/system/aria2c.service` 
```
[Unit]
Description=Aria2c download manager
After=network.target

[Service]
User=aria2
Type=forking
ExecStart=/usr/bin/aria2c --conf-path=/home/aria2/.aria2/aria2.daemon

[Install]
WantedBy=multi-user.target

```

Then [start and/or enable](/index.php/Systemd#Using_units "Systemd") the service.

### Изменение User Agent

Некоторые сайты могут фильтровать запросы на основе вашего User Agent, Aria2 не известный загрузчик, но он может использовать известные загрузчики или представляться браузером. Просто используйте опцию -U, как это:

```
$ aria2c -UWget http://some-url-to-download/file.xyz

```

Вы можете использовать все, что пожелаете, например **-UMozilla/5.0** и т.д.

### Использование Aria2 с makepkg

Вы можете использовать [Aria2](/index.php/Aria2 "Aria2") вместо curl для скачивания файлов-исходников, просто измените переменную `DLAGENTS` следующим образом:

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

**Обратите внимание:** Используйте параметр `-UWget` для изменения пользовательского агента на Wget. Это может предотвратить проблемы при загрузке с сайтов, которые фильтрует запросы, основанные на агенте пользователя (user agent), чтобы избежать проблемы доступа к URL-адресу. Смотрите [#Изменение User Agent](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_User_Agent)
.

## Смотрите также

*   [Руководство](http://aria2.sourceforge.net/manual/ru/html/aria2c.html) - Официальное руководство aria2 на Русском
*   [aria2](http://sourceforge.net/projects/aria2/) - Официальный сайт
*   [aria2 usage examples](http://sourceforge.net/apps/trac/aria2/wiki/UsageExample) - Official site
*   [aria2c downloader through VPN tunnel](http://gotux.net/arch-linux/aria2c-downloader-through-vpn-tunnel/) - Unofficial site