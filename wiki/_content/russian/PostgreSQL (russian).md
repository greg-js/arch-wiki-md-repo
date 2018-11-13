Эта статья описывает как настроить PostgreSQL и интегрировать ее с [PHP](/index.php/PHP "PHP") и [Apache](/index.php/Apache "Apache"). Она также описывает, как сделать PostgreSQL доступным из клиента удалённого доступа. Считаем, что [PHP](/index.php/PHP "PHP") и [Apache](/index.php/Apache "Apache") уже установлены. Если вам нужна помощь настройки любой из этих программ, смотрите [LAMP](/index.php/LAMP "LAMP") и следуйте всем разделам, кроме связанного с [MySQL](/index.php/MySQL "MySQL").

## Contents

*   [1 Установка PostgreSQL](#Установка_PostgreSQL)
*   [2 Создание Вашей первой базы данных](#Создание_Вашей_первой_базы_данных)
*   [3 Знакомство с PostgreSQL](#Знакомство_с_PostgreSQL)
    *   [3.1 Доступ к оболочке базы данных](#Доступ_к_оболочке_базы_данных)
*   [4 Настройка удалённого доступа к PostgreSQL](#Настройка_удалённого_доступа_к_PostgreSQL)
*   [5 Настройка PostgreSQL для работы с PHP](#Настройка_PostgreSQL_для_работы_с_PHP)
*   [6 Настройка PostgreSQL для работы с HHVM](#Настройка_PostgreSQL_для_работы_с_HHVM)
*   [7 Изменение кодировки новой базы данных на UTF-8 (по вашему усмотрению)](#Изменение_кодировки_новой_базы_данных_на_UTF-8_(по_вашему_усмотрению))
*   [8 Решение проблем](#Решение_проблем)
    *   [8.1 Ускорение мелких транзакций](#Ускорение_мелких_транзакций)
    *   [8.2 Запретить запись на диск во время бездействия](#Запретить_запись_на_диск_во_время_бездействия)
    *   [8.3 Направлять лог в syslog](#Направлять_лог_в_syslog)
*   [9 Больше информации](#Больше_информации)

## Установка PostgreSQL

*   Устанавливаем postgresql

```
$ sudo pacman -S postgresql

```

*   Инициализируем кластер с нужной локалью (она должна быть доступна в системе). Обратите внимание, что в данном примере используем `ru_RU.UTF-8`

```
$ sudo su - postgres -c "initdb --locale ru_RU.UTF-8 -E UTF8 -D '/var/lib/postgres/data'"

```

*   Если получили ошибку "Невозможно создать директорию, недостаточно прав", то изменяем владельца PGROOT директории и пробуем еще раз

```
$ sudo chown -R postgres:postgres /var/lib/postgres/

```

*   Запускаем сервер PostgreSQL

```
$ systemctl start postgresql

```

*   Проверяем запустилось ли:

```
$ systemctl status postgresql

```

*   Дополнительно его можно добавить в автозагрузку

```
$ systemctl enable postgresql

```

## Создание Вашей первой базы данных

*   Становимся пользователем postgres (пользователь postgres не имеет пароля по умолчанию, поэтому таким вот образом)

```
$ sudo su - postgres

```

*   Добавляем нового пользователя базы данных

```
$ [createuser](http://www.postgresql.org/docs/8.3/static/app-createuser.html) -DRSP <username>

```

-D Пользователь не может создавать базы данных
-R Пользователь не может создавать аккаунты
-S Пользователь не является суперпользователем
-P Запрашивать пароль при создании

С другой стороны, вы можете использовать команду `createuser` без параметров. Вывод в терминале выглядит так:

```
$ createuser <username>
Shall the new role be a superuser? (y/n)  n
Shall the new role be allowed to create databases? (y/n)  y
Shall the new role be allowed to create more new roles? (y/n)  y

```

*   Если имя созданного пользователя совпадает с именем пользователя ($USER), вы получите доступ к базе данных оболочки PostgreSQL без указания имени пользователя (что весьма удобно).

*   Создаём новую базу данных. Создавать можно только от пользователя (например, postgres, за которого мы зашли), имеющего разрешение на чтение и запись (read/write). Если кодировку не указать, то она будет той, что вы указали в разделе [«Установка PostgreSQL»](#Установка_PostgreSQL).

```
$ [createdb](http://www.postgresql.org/docs/8.3/static/app-createdb.html) -O username databasename [-E database_encoding]

```

*   Вот и всё! Ваша база данных создана. Теперь можете уже под любым пользователем управлять БД:

```
$ psql имя_базы -U имя_пользователя_бд

```

*   Если имя базы данных **И** имя пользователя БД совпадают с текущим именем пользователя ($USER), то можно просто:

```
$ psql

```

## Знакомство с PostgreSQL

### Доступ к оболочке базы данных

*   Становимся postgres пользователем, чтобы иметь возможность задать ваши права (как у основного пользователя)

```
$ sudo su postgres

```

*   Запускаем основную оболочку базы данных, в которой мы сможем создавать, удалять базы данных/таблицы, задавать права и запускать команды SQL.

```
$ [psql](http://www.postgresql.org/docs/8.3/static/app-psql.html)

```

	*— Вы также можете использовать `psql <database_name>` для редактирования конкретной базы данных.*

*   Список всех возможных команд (например, `CREATE TABLE`) для запросов

```
=> \h

```

*   Подробное описание команды

```
=> \h CREATE_TABLE

```

*   Подключаем определённую базу данных

```
=> \c <database>

```

*   Список всех пользователей и их уровни доступа

```
=> \du

```

*   Краткая информация о всех таблицах в текущей базе данных

```
=> \dt

```

*   Меняем пароль

```
=> \password

```

*   Показать все используемые настройки

```
=> SHOW ALL;

```

*   Выйти из psql

```
=> \q или CTRL+d

```

Есть, конечно, много других мета-команд, но именно эти должны помочь вам начать работу.

## Настройка удалённого доступа к PostgreSQL

Файл настроек сервера баз данных PostgreSQL `postgresql.conf`. Этот файл находится в папке данных сервера, обычно `/var/lib/postgres/data`. В этой же папке находятся основные файлы настроек включая и `pg_hba.conf`.

**Примечание:** По умолчанию эта папка не доступна даже для просмотра (или поиска) от лица обычного пользователя.
Из-под пользователя root редактируем файл `$ sudoedit /var/lib/postgres/data/postgresql.conf` 

В разделе connections and authentications раскомментируйте или исправьте строку `listen_addresses` по вашему желанию на

```
listen_addresses = '*'

```

либо

```
listen_addresses = 'localhost,ip_у_сервера_в_сети'

```

и внимательно просмотрите другие строки.
Далее добавляем следующую строку в основной файл настройки проверки подлинности `/var/lib/postgres/data/pg_hba.conf`. (если вы планируете подключатся только со своего компьютера, то пропустите данный шаг) Этот файл определяет, каким хостам разрешено подключаться, **так что будьте осторожны**.

```
# IPv4 local connections:
host   all   all   your_desired_ip_address/32   trust

```

где `your_desired_ip_address` — IP-адрес клиента.

После этого необходимо перезапустить демон, чтобы изменения вступили в силу
 `$ systemctl restart postgresql` 
**Примечание:** PostgreSQL по умолчанию использует порт 5432 для удалённого доступа. Поэтому убедитесь, что этот порт открыт и может принимать входящие соединения.

Если возникли проблемы взгляните на лог-файл сервера

```
$ journalctl -u postgresql

```

Не менее важные ошибки можно увидеть командой:

```
$ systemctl status postgresql.service

```

## Настройка PostgreSQL для работы с PHP

1.  Установите модуль PHP-PostgreSQL `$ pacman -S php-pgsql ` 
2.  Откройте файл **`/etc/php/php.ini`** в удобном для вас текстовом редакторе, например, `$ sudoedit /etc/php/php.ini` 
3.  Найдите строку, начинающуюся с `;extension=pgsql.so`, и из неё уберите `;` (`;` значит, что строка закомментирована). Если вы используете PDO, сделайте то же самое с `;extension=pdo.so` и `;extension=pdo_pgsql.so`. Если этих строк нет, добавьте их (без `;`). Эти строки надо искать в разделе файла «Dynamic Extensions» (по умолчанию) или в самом конце файла.
4.  Перезапустите веб-сервер Apache `# systemctl restart httpd` 
5.  Либо, если у вас nginx + php-fpm, то `# systemctl reload php-fpm` 

## Настройка PostgreSQL для работы с HHVM

```
$ git clone [https://github.com/PocketRent/hhvm-pgsql.git](https://github.com/PocketRent/hhvm-pgsql.git)
$ cd hhvm-pgsql

```

Если вы используете не ночную версию, то выполните это команду (проверено на HHVM 3.6.1), чтобы избежать ошибок компиляции:

```
$ git checkout tags/3.6.0

```

Затем надо собрать (если улучшенная поддержка языка Hack не нужна, то уберите -DHACK_FRIENDLY=ON):

```
$ hphpize
$ cmake -DHACK_FRIENDLY=ON .
$ make

```

Скопируем скомпилированное расширение:

```
$ sudo cp pgsql.so /etc/hhvm/

```

Затем в /etc/hhvm/server.ini добавляем:

```
extension_dir = /etc/hhvm
hhvm.extensions[pgsql] = pgsql.so
```

## Изменение кодировки новой базы данных на UTF-8 (по вашему усмотрению)

Когда создаётся новая база данных (например, `createdb blog`) PostgreSQL просто копирует шаблон базы данных. Есть два стандартных шаблона: template0 - ваниль, и template1 используемый по умолчанию. Один из вариантов изменения кодировки новой базы данных, заключается в изменении шаблона template1\. Для этого, заходим в оболочку PostgresSQL (psql) и делаем вот что:

1\. Первое, мы должны сбросить template1\. Шаблоны не могут быть сброшены, так что мы сначала изменим его, как обычную базу данных:

```
UPDATE pg_database SET datistemplate = FALSE WHERE datname = 'template1';

```

2\. Сейчас уже можно сбросить её:

```
DROP DATABASE template1;

```

3\. Создаём новую базу данных, с новой кодировкой по умолчанию из template0:

```
CREATE DATABASE template1 WITH TEMPLATE = template0 ENCODING = 'UNICODE';

```

4\. Теперь снова сделаем template1 шаблоном:

```
UPDATE pg_database SET datistemplate = TRUE WHERE datname = 'template1'; 

```

5\. (Рекомендация) Документация по PostgreSQL [advises](http://www.postgresql.org/docs/8.1/interactive/manage-ag-templatedbs.html) рекомендует "замораживать" изменения шаблона функцией VACUUM FREEZE:

```
\c template1
VACUUM FREEZE;

```

6\. (По желанию) Если вы не хотите, чтобы кто-либо подключался к этому шаблону, присвойте параметру datallowconn значение FALSE:

```
UPDATE pg_database SET datallowconn = FALSE WHERE datname = 'template1';

```

Теперь вы можете создать базу данных используя стандартные команды в терминале:

```
su - 
su - postgres
createdb blog;

```

Если снова войти в PSQL и проверить базу данных, вы должны увидеть правильную кодировку новой базы данных:

```
\l

```

returns

```
                              List of databases
  Name    |  Owner   | Encoding  | Collation | Ctype |   Access privileges   
-----------+----------+-----------+-----------+-------+----------------------
blog      | postgres | UTF8      | C         | C     | 
postgres  | postgres | SQL_ASCII | C         | C     | 
template0 | postgres | SQL_ASCII | C         | C     | =c/postgres
                                                     : postgres=CTc/postgres
template1 | postgres | UTF8      | C         | C     |

```

## Решение проблем

### Ускорение мелких транзакций

Если вы используете PostgreSQL на своей локальной машине для разработки и он медленный, то можете попробовать [отключить synchronous_commit](http://www.postgresql.org/docs/current/static/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT) в конфигурации. Однако, не забывайте про его [особенности](http://www.postgresql.org/docs/current/static/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT).

### Запретить запись на диск во время бездействия

PostgreSQL периодически обновляет свою статистику, лежащую в файле. По умолчанию этот файл находится на диске, что не даёт отдыхать (и изнашивает) жёсткому диску, заставляя его шуршать. Однако можно легко и безопасно поменять локацию файла внутрь ФС (/run) расположенной в ОЗУ с помощью такой настройки:

 `/var/lib/postgres/data/postgresql.conf`  `stats_temp_directory = '/run/postgresql'` 

### Направлять лог в syslog

Находим и меняем данную строчку:

 `/var/lib/postgres/data/postgresql.conf`  `log_destination = 'syslog'` 

И вуаля, все работает.

## Больше информации

*   [Официальная страница PostgreSQL](http://www.postgresql.org/)