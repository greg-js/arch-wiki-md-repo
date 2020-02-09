Bareos (Backup Archiving Recovery Open Sourced) — высоконадежное сетевое кроссплатформенное программное обеспечение для резервного копирования, архивирования и восстановления данных. Bareos, основанный в 2010 году как 100-процентное открытое ответвление проекта Bacula, активно развивается и пополняется многими новыми функциями.

Сайт проекта: [https://www.bareos.com](https://www.bareos.com)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Описание пакетов](#Описание_пакетов)
*   [2 Установка серверной части](#Установка_серверной_части)
*   [3 Настройка базы данных MySQL](#Настройка_базы_данных_MySQL)
*   [4 Примеры конфигурационных файлов](#Примеры_конфигурационных_файлов)

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

## Настройка базы данных MySQL

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

Чтобы bareos-dir начал работать с MySQL, нужно настроить конфигурационный файл в секции `Catalog`.

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

## Примеры конфигурационных файлов

Примеры конфигурационных файлов находятся в `/usr/share/bareos/config`.