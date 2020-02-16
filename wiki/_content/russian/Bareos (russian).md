Bareos (Backup Archiving Recovery Open Sourced) — высоконадежное сетевое кроссплатформенное программное обеспечение для резервного копирования, архивирования и восстановления данных. Bareos, основанный в 2010 году как 100-процентное открытое ответвление проекта Bacula, активно развивается и пополняется многими новыми функциями.

Сайт проекта: [https://www.bareos.com](https://www.bareos.com)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Описание пакетов](#Описание_пакетов)
*   [2 Установка серверной части](#Установка_серверной_части)
    *   [2.1 Настройка базы данных MySQL](#Настройка_базы_данных_MySQL)
    *   [2.2 Настрока места хранения бекапов Storage (SD)](#Настрока_места_хранения_бекапов_Storage_(SD))
*   [3 Примеры конфигурационных файлов](#Примеры_конфигурационных_файлов)

## Описание пакетов

| Имя пакета | Описание |
| [bareos-common](https://aur.archlinux.org/packages/bareos-common/) | Общие файлы для пакетов bareos |
| [bareos-bconsole](https://aur.archlinux.org/packages/bareos-bconsole/) | Admin Tool (CLI) |
| [bareos-database-common](https://aur.archlinux.org/packages/bareos-database-common/) | Общие абстракции библиотеки и инструменты для баз SQL |
| [bareos-database-mysql](https://aur.archlinux.org/packages/bareos-database-mysql/) | Библиотеки и инструменты для варианта использования базы MySQL |
| [bareos-database-postgresql](https://aur.archlinux.org/packages/bareos-database-postgresql/) | Библиотеки и инструменты для варианта использования базы postgresql |
| [bareos-database-sqlite3](https://aur.archlinux.org/packages/bareos-database-sqlite3/) | Библиотеки и инструменты для варианта использования базы sqlite3 |
| [bareos-database-tools](https://aur.archlinux.org/packages/bareos-database-tools/) | CLI инструменты с зависимостями баз данных (dbcheck, bscan) |
| [bareos-devel](https://aur.archlinux.org/packages/bareos-devel/) | Заголовки Devel |
| [bareos-director](https://aur.archlinux.org/packages/bareos-director/) | Director (DIR), главный демон отвечающий за все выполняемые операции (управляет операциями резервного копирования и восстановления, выполняемыми демонами File и Storage.) |
| [bareos-director-python-plugin](https://aur.archlinux.org/packages/bareos-director-python-plugin/) | Python плагин для director-демона |
| [bareos-filedaemon-python-plugin](https://aur.archlinux.org/packages/bareos-filedaemon-python-plugin/) | Python плагин для файлового демона |
| [bareos-filedaemon](https://aur.archlinux.org/packages/bareos-filedaemon/) | Файловый демон (устанавливается на клиентской части) |
| [bareos-storage](https://aur.archlinux.org/packages/bareos-storage/) | Storage Daemon (SD): программное обеспечение, которое выполняет операции чтения и записи на устройствах хранения, используемых для резервного копирования. |
| [bareos-storage-fifo](https://aur.archlinux.org/packages/bareos-storage-fifo/) | Поддержка FIFO для демона хранилища |
| [bareos-storage-python-plugin](https://aur.archlinux.org/packages/bareos-storage-python-plugin/) | Python плагин для демона хранения |
| [bareos-storage-tape](https://aur.archlinux.org/packages/bareos-storage-tape/) | Поддержка лентовых хранилищ |
| [bareos-tools](https://aur.archlinux.org/packages/bareos-tools/) | CLI инструменты (bcopy, bextract, bls, bregeq, bwild) |
| [bareos-webui](https://aur.archlinux.org/packages/bareos-webui/) | Webui (веб-интерфейс администрирования Bareos) |

## Установка серверной части

Для минимальной установки серверной части достаточно установить следующие пакеты:

Пакет главного демона (Директора):

```
  # pacman -S bareos-director 

```

**Примечание:** Конфигурационные файлы Director по умолчанию находятся в каталоге: /etc/bareos/bareos-dir.d

Пакет предпочитаемой базы данных (допустим MySQL):

```
  # pacman -S bareos-database-mysql

```

Пакет хранилища архивных данных (можно устанавливать на другом сервере или даже на нескольких серверах):

```
  # pacman -S bareos-storage

```

**Примечание:** Конфигурационные файлы Storage по умолчанию находятся в каталоге: /etc/bareos/bareos-sd.d

### Настройка базы данных MySQL

Для создания mysql базы данных на localhost и пользователя root выполним:

```
  /usr/lib/bareos/scripts/create_bareos_database --user root --password

```

Создание таблиц:

```
  /usr/lib/bareos/scripts/make_bareos_tables --user root --password

```

Создадим пользователя bareos и настроим привилегии:

```
  /usr/lib/bareos/scripts/grant_bareos_privileges --user root --password

```

Будет создана база данных `bareos`, а также пользователь `bareos` без пароля (желательно пароль позже установить).

Чтобы bareos-dir начал работать с MySQL, нужно настроить конфигурационный файл с секцией `Catalog`.

По умолчанию файл располагается в /etc/bareos/bareos-dir.d/catalog и может иметь произвольное имя с расширением `.conf`.

Пример содержания файла:

```
  Catalog {
  Name = DatabaseCatalog
  dbdriver = "mysql"
  dbname = "bareos"
  dbuser = "bareos"
  dbpassword = ""
  }

```

### Настрока места хранения бекапов Storage (SD)

**Примечание:** Устанавливается Storage не обязательно вместе с Director, а может располагаться на любом доступном по сети компьютере

Структура каталога с конфигурационными файлами может иметь следующий вид:

/etc/bareos/bareos-sd.d/device - каталог содержит файлы конфигураций с настройками физический устройств (названия файлов может быть произвольным)

Пример файла конфигурации:

```
 Device {
   # Название устройства хранения
   # Директор должен иметь то же Имя и MediaType.
   Name = archive1
   Media Type = archive-file
   # Путь к устройству или папке
   Archive Device = /archive1/bareos
   # Разрешить автоматически размечать тома
   LabelMedia = yes;
   # Для одновременного доступа при одновременном выполнении нескольких задач
   Random Access = yes;
   # Автоматически монтировать устройство
   AutomaticMount = yes;
   RemovableMedia = no;
   AlwaysOpen = no;
   Maximum Concurrent Jobs = 1
   Description = "/archive1"
 }

```

/etc/bareos/bareos-sd.d/director - каталог с файлами конфигураций Директора.

Пример файла конфигурации:

```
 Director {
   # Параметры директора, который может подключаться к Storage
   Name = bareos_dir
   # Пароль для подключкния к этому Storage
   Password = ""
   Description = "Director, who is permitted to contact this storage daemon."
 }

```

/etc/bareos/bareos-sd.d/messages - каталог с файлами сообщений.

Пример файла конфигурации:

```
 Messages {
   Name = standard
   Director = bareos_dir = all
   Description = "Send all messages to the Director."
 }

```

/etc/bareos/bareos-sd.d/storage - каталог с конфигурационными файлами хранилища.

```
 Storage {
   Name = storage1
   # Максимальное количество одновременно выполняющихся Job
   Maximum Concurrent Jobs = 20
   # remove comment from "Plugin Directory" to load plugins from specified directory.
   # if "Plugin Names" is defined, only the specified plugins will be loaded,
   # otherwise all storage plugins (*-sd.so) from the "Plugin Directory".
   #
   # Plugin Directory = "/usr/lib/bareos/plugins"
   # Plugin Names = ""
 }

```

Запуск демона Storage:

```
 systemctl start bareos-sd

```

## Примеры конфигурационных файлов

Примеры конфигурационных файлов находятся в `/usr/share/bareos/config`.