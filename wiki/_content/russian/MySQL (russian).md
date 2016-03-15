MySQL - это широко применяемая свободная многопоточная многопользовательская система управления реляционными базами данных. MySQL использует один из диалектов языка [SQL](http://http://ru.wikipedia.org/wiki/SQL) для управления базами данных. Более подробную информацию об особенностях MySQL можно посмотреть на [официальном сайте](http://www.mysql.com/).

**Примечание:** На сегодняшний день в Archlinux к использованию по умолчанию предлагается MariaDB - официальный форк сервера MySQL. Настоятельно рекомендуется всем пользователям обновиться до [MariaDB](/index.php/MariaDB "MariaDB"). Oracle MySQL был перемещен из официальных репозиториев Archlinux в AUR. Для получения более подробной информации прочтите [объявление](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Автоматический запуск при загрузке системы](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [1.2 Апгрейд с Oracle MySQL до MariaDB](#.D0.90.D0.BF.D0.B3.D1.80.D0.B5.D0.B9.D0.B4_.D1.81_Oracle_MySQL_.D0.B4.D0.BE_MariaDB)
    *   [1.3 После обновления](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Добавление пользователя](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
    *   [2.2 Включение удалённого доступа](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D0.B4.D0.B0.D0.BB.D1.91.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0)
    *   [2.3 Отключение удаленного доступа](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0)
    *   [2.4 Режим автодополнения](#.D0.A0.D0.B5.D0.B6.D0.B8.D0.BC_.D0.B0.D0.B2.D1.82.D0.BE.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.5 Использование кодировки UTF-8](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B8_UTF-8)
    *   [2.6 Использование файловой системы TMPFS для каталога tmpdir](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_TMPFS_.D0.B4.D0.BB.D1.8F_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.B0_tmpdir)
*   [3 Бэкап](#.D0.91.D1.8D.D0.BA.D0.B0.D0.BF)
*   [4 Поиск и устранение неисправностей](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.B8_.D1.83.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.B8.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BD.D0.BE.D1.81.D1.82.D0.B5.D0.B9)
    *   [4.1 Не запускается демон MySQL](#.D0.9D.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD_MySQL)
    *   [4.2 Не могу запустить mysql_upgrade из-за невозможности запуска MySQL](#.D0.9D.D0.B5_.D0.BC.D0.BE.D0.B3.D1.83_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D1.8C_mysql_upgrade_.D0.B8.D0.B7-.D0.B7.D0.B0_.D0.BD.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_MySQL)
    *   [4.3 Сброс пароля для root](#.D0.A1.D0.B1.D1.80.D0.BE.D1.81_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8F_.D0.B4.D0.BB.D1.8F_root)
    *   [4.4 Проверка и восстановление всех таблиц](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B8_.D0.B2.D0.BE.D1.81.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D1.81.D0.B5.D1.85_.D1.82.D0.B0.D0.B1.D0.BB.D0.B8.D1.86)
    *   [4.5 Оптимизация всех таблиц](#.D0.9E.D0.BF.D1.82.D0.B8.D0.BC.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D0.B2.D1.81.D0.B5.D1.85_.D1.82.D0.B0.D0.B1.D0.BB.D0.B8.D1.86)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

MariaDB - так именуется форк популярного сервера баз данных MySQL, выбранный сообществом Archlinux. [Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") пакет [mariadb](https://www.archlinux.org/packages/?name=mariadb) из [официальных репозиториев](/index.php/Official_Repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official Repositories (Русский)"). В качестве альтернативы вы можете установить, например:

*   **Oracle MySQL** — Официальный релиз от компании Oracle.

	[https://www.mysql.com/](https://www.mysql.com/) || [mysql](https://aur.archlinux.org/packages/mysql/)

*   **Percona Server** — Альтернатива, которая обещает высокую производительность и разные широкие возможности.

	[http://www.percona.com/software/percona-server/](http://www.percona.com/software/percona-server/) || [percona-server](https://www.archlinux.org/packages/?name=percona-server)

**Tip:** Если база данных, размещаемая в каталоге `/var/lib/mysql`, расположена на разделе с файловой системой [btrfs](/index.php/Btrfs "Btrfs"), то необходимо отключить механизм [Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs") для этого каталога перед тем как создавать новую базу данных:

`# chattr +C /var/lib/mysql`

Перед запуском демона `mysqld` обязательно необходимо выполнить команду для создания таблиц по умолчанию:

```
# mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql

```

[Запустите](/index.php/Daemons#Starting_manually "Daemons") демон `mysqld` и выполните настроечный скрипт:

```
# mysql_secure_installation

```

и [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") `mysqld`.

Если есть необходимость во фронтендах к MariaDB, то можете использовать [mysql-gui-tools](https://aur.archlinux.org/packages/mysql-gui-tools/) или [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench).

### Автоматический запуск при загрузке системы

Для автоматического запуска сервера баз данных MySQL при загрузке операционной системы, добавьте демон `mysqld` в систему инициализации [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)").

```
# systemctl enable mysqld
# systemctl start mysqld

```

### Апгрейд с Oracle MySQL до MariaDB

**Примечание:** Перед перезапуском демона `mysqld` на следующем шаге, возможно, понадобится удалить следующие файлы из каталога `/var/lib/mysql`, а именно: `ib_logfile0`, `ib_logfile1` и `aria_log_control`.

Пользователи, желающие произвести переход, должны остановить процесс `mysqld`, установить *mariadb*, *libmariadbclient* или *mariadb-clients*, после чего перезапустить `mysqld` и выполнить:

```
# mysql_upgrade -p

```

### После обновления

После обновления MySQL можно запустить полезную утилиту mysql_upgrade для автоматической проверки и обновления MySQL-таблиц на предмет совместимости структур данных с текущей версией MySQL.

```
# mysql_upgrade -u root -p

```

## Настройка

После установки и запуска MySQL необходимо настроить учетную запись root для администрирования MySQL. Задайте пароль для пользователя root. Это можно осуществить вручную или автоматически на стадии выполнения предыдущего скрипта. Ручная установка пароля для root возможна при помощи утилиты `mysqladmin`

```
mysqladmin -u root password newpass

```

MySQL построен по клиент-серверной архитектуре. Это значит, что систему управления базами данных MySQL можно трактовать как сервер, обменивающийся сообщениями с MySQL-клиентами. Консольный клиент, запускаемый в терминале при помощи команды `mysql`, позволяет подключиться к серверу баз данных MySQL. Осуществим такое подключение от имени пользователя root:

```
$ mysql -p -u root

```

### Добавление пользователя

Создание нового пользователя состоит из двух действий: создание пользователя; установка прав. Пример: создадим пользователя *monty* с паролем *some_pass*.

 `$ mysql -u root -p` 
```
MariaDB> CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
MariaDB> GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost'
   ->     WITH GRANT OPTION;
MariaDB> quit
```

### Включение удалённого доступа

Если Вы хотите подключаться к Вашему серверу MySQL удалённо с других хостов, то Вам необходимо раскомментировать (убрать символ #) следующие строки в файле `/etc/mysql/my.cnf`:

```
[mysqld]
   ...
   #skip-networking
   #bind-address = <some ip-address>
   ...

```

Таким образом Вы позволите удалённо подключаться любом пользователю (в том числе и root): Подключить к базе с правами пользователя root:

```
$ mysql -u root -p -h IPorHOSTNAME

```

Проверка прав пользователей на удаленное подключение:

```
SELECT User, Host FROM mysql.user WHERE Host <> 'localhost';

```

Предоставить права удаленного доступа пользователю (в данном случе root):

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.1.%' IDENTIFIED BY 'my_optional_remote_password' WITH GRANT OPTION;

```

При необходимости шаблон '%' можно заменить на конкретное значение хоста. Пароль пользователя в базе может отличаться от пароля пользователя в системе.

### Отключение удаленного доступа

MySQL-сервер по умолчанию доступен из внешней сети. Если вы используете MySQL локально, то можно усилить безопасность, отключив прослушивание TCP-порта 3306\. Для отключения удаленного доступа раскомментируйте в файле `/etc/mysql/my.cnf` строку:

```
skip-networking

```

Теперь вы сможете соединиться с MySQL-сервером только через localhost.

### Режим автодополнения

**Примечание:** Активация этого режима может увеличить время инициализации MySQL-клиента.

По умолчанию механизм автодополнения команд и имен в клиенте mysql отключен. Для включения автоматического дополнения отредактируйте общий конфигурационный файл `/etc/mysql/my.cnf`, заменив параметр `no-auto-rehash` на параметр `auto-rehash`. Автодополнение вступит в силу после очередного запуска клиента mysql.

### Использование кодировки UTF-8

В файле `/etc/mysql/my.cnf` добавьте к настройкам секции `mysqld` следующие параметры:

```
[mysqld]
init_connect                = 'SET collation_connection = utf8_general_ci,NAMES utf8'
collation_server            = utf8_general_ci
character_set_client        = utf8
character_set_server        = utf8

```

### Использование файловой системы TMPFS для каталога tmpdir

MySQL использует специальный каталог *tmpdir* для хранения временных файлов (например, для хранения временных таблиц). На самом деле *tmpdir* является внутренним алиасом MySQL, под маской которого может скрываться произвольный каталог.

Создаем этот каталог с соответствующими правами доступа:

```
# mkdir -pv /var/lib/mysqltmp
# chown mysql:mysql /var/lib/mysqltmp

```

Определим UID и GID для пользователя `mysql`:

```
$ id mysql
uid=27(mysql) gid=27(mysql) groups=27(mysql)

```

Добавим в файл `/etc/fstab` строку вида:

```
 tmpfs   /var/lib/mysqltmp   tmpfs   rw,gid=27,uid=27,size=100m,mode=0750,noatime   0 0

```

Не забудем в файле `/etc/mysql/my.cnf` связать алиас *tmpdir* с реальным каталогом. Добавьте к группе настроек секции `mysqld` строчку:

```
 tmpdir      = /var/lib/mysqltmp

```

Перезагрузитесь или ( остановите сервер MySQL, примонтируйте tmpdir, запустите сервер MySQL ).

## Бэкап

Легкий бэкап баз данных можно осуществить с помощью утилиты mysqldump. Нижеследующий скрипт помещает дамп всех баз данных в файл `db_backup.gz`, который будет расположен в той же папке, что и сам скрипт, и удаляет все бинарные логи старше одной недели:

```
#!/bin/bash

THISDIR=$(dirname $(readlink -f "$0"))

mysqldump --single-transaction --flush-logs --master-data=2 --all-databases -u root -p | gzip > $THISDIR/db_backup.gz
mysql -u root -p -e 'purge master logs before date_sub(now(), interval 7 day);'
```

Смотрите также страницу официального [руководства по работе с mysqldump](http://dev.mysql.com/doc/refman/5.6/en/mysqldump.html).

## Поиск и устранение неисправностей

### Не запускается демон MySQL

Если MySQL не запускается, а в логах отсутствуют записи, то можно проверить содержимое каталогов `/var/lib/mysql` и `/var/lib/mysql/mysql` на предмет прав доступа. Если владельцами файлов в этих директориях является не пользователь `mysql` из одноименной группы, то проделайте следующее:

```
 # chown mysql:mysql /var/lib/mysql -R

```

Ежели у вас остаются проблемы, связанные с доступом, несмотря на вышеозначенную рекомендацию, попробуйте скопировать `my.cnf` в `/etc/`. Для этого выполните команду:

```
 # cp /etc/mysql/my.cnf /etc/my.cnf

```

Теперь попробуйте [запустить](/index.php/Daemons#Starting_manually "Daemons") mysqld.

Ежели вы получите в файле `/var/lib/mysql/hostname.err` такие строки:

```
 [ERROR] Can't start server : Bind on unix socket: Permission denied
 [ERROR] Do you already have another mysqld server running on socket: /var/run/mysqld/mysqld.sock ?
 [ERROR] Aborting

```

Виной этому могут быть некорректные права доступа на `/var/run/mysqld`. Выполните:

```
 # chown mysql:mysql /var/run/mysqld -R

```

Если вы запустили mysqld, но получили следующее сообщение об ошибке:

```
 Fatal error: Can’t open and lock privilege tables: Table ‘mysql.host’ doesn’t exist

```

Выполните следующую команду из каталога /usr для создания таблиц по умолчанию:

```
 # cd /usr
 # mysql_install_db --user=mysql --ldata=/var/lib/mysql/

```

### Не могу запустить mysql_upgrade из-за невозможности запуска MySQL

Попытайтесь запустить MySQL в безопасном режиме:

```
# mysqld_safe --datadir=/var/lib/mysql/

```

После этого выполните:

```
# mysql_upgrade -u root -p

```

### Сброс пароля для root

[Остановите](/index.php/Daemons#Starting_manually "Daemons") демона mysqld и выполните:

```
# mysqld_safe --skip-grant-tables &

```

Подсоединитесь к серверу MySQL:

```
# mysql -u root mysql

```

Измените пароль для пользователя root:

```
 mysql> UPDATE mysql.user SET Password=PASSWORD('MyNewPass') WHERE User='root';
 mysql> FLUSH PRIVILEGES;
 mysql> exit

```

[Запустите](/index.php/Daemons#Starting_manually "Daemons") mysqld.

### Проверка и восстановление всех таблиц

Можно выполнить автоматическую проверку и восстановление всех таблиц во всех базах данных. Более подробно смотрите [здесь](http://dev.mysql.com/doc/refman/5.7/en/mysqlcheck.html).

```
# mysqlcheck -A --auto-repair -u root -p

```

### Оптимизация всех таблиц

Для принудительной оптимизации всех таблиц с автоматической фиксацией возникающих ошибок, выполните:

```
# mysqlcheck -A --auto-repair -f -o -u root -p

```

## Смотрите также

*   [LAMP](/index.php/LAMP_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LAMP (Русский)") - статья на ArchWiki, описывающая установку и базовую настройку LAMP-сервера (Linux, Apache, MySQL, PHP).
*   [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") - статья на ArchWiki, описывающая веб-ориентированный фронтенд для управления базами данных MySQL.
*   [PHP](/index.php/PHP "PHP") - статья на ArchWiki, посвященная установке и настройке интерпретатора PHP.
*   [MySQL Performance Tuning Scripts and Know-How](http://www.askapache.com/mysql/performance-tuning-mysql.html) - англоязычная статья про MySQL.