[Zabbix](http://www.zabbix.com/) — свободная система мониторинга и отслеживания статусов разнообразных сервисов компьютерной сети, серверов и сетевого оборудования, написанная Алексеем Владышевым.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Установка необходимой зависимости iksemel для zabbix-server](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D0.BE.D0.B9_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B8.D0.BC.D0.BE.D1.81.D1.82.D0.B8_iksemel_.D0.B4.D0.BB.D1.8F_zabbix-server)
    *   [1.2 Установка zabbix-server](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_zabbix-server)
*   [2 Настройка PostgreSQL](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_PostgreSQL)
    *   [2.1 Подготовка PostgreSQL к первому запуску](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_PostgreSQL_.D0.BA_.D0.BF.D0.B5.D1.80.D0.B2.D0.BE.D0.BC.D1.83_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D1.83)
    *   [2.2 Запуск PostgreSQL](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_PostgreSQL)
    *   [2.3 Установка пароля пользователю системы postgres](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8F_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8E_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_postgres)
    *   [2.4 Установка пароля роли postgres и разрешение подключения к базам данных только через протокол Unix](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8F_.D1.80.D0.BE.D0.BB.D0.B8_postgres_.D0.B8_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BA_.D0.B1.D0.B0.D0.B7.D0.B0.D0.BC_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_.D0.BF.D1.80.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.BB_Unix)
    *   [2.5 Создание и настройка базы данных zabbix для работы с Zabbix](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B1.D0.B0.D0.B7.D1.8B_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_zabbix_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_.D1.81_Zabbix)
    *   [2.6 ДОПОЛНИТЕЛЬНО. Настройка контроля за объемом используемого Zabbix и PostgreSQL дискового пространства для редко изменяющейся базы данных](#.D0.94.D0.9E.D0.9F.D0.9E.D0.9B.D0.9D.D0.98.D0.A2.D0.95.D0.9B.D0.AC.D0.9D.D0.9E._.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D1.8F_.D0.B7.D0.B0_.D0.BE.D0.B1.D1.8A.D0.B5.D0.BC.D0.BE.D0.BC_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC.D0.BE.D0.B3.D0.BE_Zabbix_.D0.B8_PostgreSQL_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D1.81.D1.82.D0.B2.D0.B0_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B5.D0.B4.D0.BA.D0.BE_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D1.8F.D1.8E.D1.89.D0.B5.D0.B9.D1.81.D1.8F_.D0.B1.D0.B0.D0.B7.D1.8B_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85)
    *   [2.7 Включение PostgreSQL в автозапуск](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_PostgreSQL_.D0.B2_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [3 Настройка PHP и FastCGI Process Manager](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_PHP_.D0.B8_FastCGI_Process_Manager)
    *   [3.1 Проверка значений параметров в файле /etc/php/php.ini](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.B5_.2Fetc.2Fphp.2Fphp.ini)
    *   [3.2 Проверка значений параметров в файле /etc/php/php-fpm.conf](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.B5_.2Fetc.2Fphp.2Fphp-fpm.conf)
    *   [3.3 Запуск FastCGI Process Manager](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_FastCGI_Process_Manager)
    *   [3.4 Включение FastCGI Process Manager в автозапуск](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_FastCGI_Process_Manager_.D0.B2_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [4 Настройка NGINX](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_NGINX)
    *   [4.1 Создание самоподписанных сертификатов для подключения к Zabbix через HTTPS](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B0.D0.BC.D0.BE.D0.BF.D0.BE.D0.B4.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D0.B2_.D0.B4.D0.BB.D1.8F_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BA_Zabbix_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_HTTPS)
    *   [4.2 Перемещение и изменение прав доступа на файл приватного ключа zabbix.key](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B0.D0.B2_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0_.D0.BD.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB_.D0.BF.D1.80.D0.B8.D0.B2.D0.B0.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BA.D0.BB.D1.8E.D1.87.D0.B0_zabbix.key)
    *   [4.3 Перемещение и изменение прав доступа на файл сертификата zabbix.pem](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B0.D0.B2_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0_.D0.BD.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.B0_zabbix.pem)
    *   [4.4 Изменение файла /etc/nginx/nginx.conf](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.2Fetc.2Fnginx.2Fnginx.conf)
    *   [4.5 Запуск NGINX](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_NGINX)
    *   [4.6 Включение NGINX в автозапуск](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_NGINX_.D0.B2_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [5 Установка и настройка агента Zabbix](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B0.D0.B3.D0.B5.D0.BD.D1.82.D0.B0_Zabbix)
    *   [5.1 Установка zabbix-agent](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_zabbix-agent)
    *   [5.2 Проверка значений параметров в файле /etc/zabbix/zabbix_agentd.conf](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.B5_.2Fetc.2Fzabbix.2Fzabbix_agentd.conf)
    *   [5.3 Запуск агента Zabbix](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B0.D0.B3.D0.B5.D0.BD.D1.82.D0.B0_Zabbix)
    *   [5.4 Включение агента Zabbix в автозапуск](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B3.D0.B5.D0.BD.D1.82.D0.B0_Zabbix_.D0.B2_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [6 Установка и настройка клиента NTP](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0_NTP)
    *   [6.1 Установка ntp](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_ntp)
    *   [6.2 Запуск клиента NTP](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0_NTP)
    *   [6.3 Включение клиента NTP в автозапуск](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0_NTP_.D0.B2_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [7 Настройка Zabbix](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Zabbix)
    *   [7.1 Установка аппаратных часов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B0.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D1.8B.D1.85_.D1.87.D0.B0.D1.81.D0.BE.D0.B2)
    *   [7.2 Проверка значений параметров в файле /etc/zabbix/zabbix_server.conf](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.B5_.2Fetc.2Fzabbix.2Fzabbix_server.conf)
    *   [7.3 Запуск Zabbix](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Zabbix)
    *   [7.4 Включение Zabbix в автозапуск](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_Zabbix_.D0.B2_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [8 Настройка Zabbix для работы с NetFlow](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Zabbix_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_.D1.81_NetFlow)
*   [9 Внешние источники](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D0.B8.D1.81.D1.82.D0.BE.D1.87.D0.BD.D0.B8.D0.BA.D0.B8)

## Установка

### Установка необходимой зависимости iksemel для zabbix-server

Установите [iksemel](https://aur.archlinux.org/packages/iksemel/) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

### Установка zabbix-server

Загрузите и распакуйте архив, содержащий необходимые файлы для сборки [zabbix-server](https://www.archlinux.org/packages/?name=zabbix-server) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

Измените строку в файле `PKGBUILD`:

 `$ nano ./PKGBUILD` 
```
...
depends=('apache' 'postgresql' 'php' 'php-pgsql' 'php-gd' 'fping' 'net-snmp' 'curl' 'iksemel')
...

```

на

```
...
depends=('nginx' 'postgresql' 'php' 'php-pgsql' 'php-gd' 'php-fpm' 'fping' 'net-snmp' 'curl' 'iksemel')
...

```

Соберите пакет:

```
$ makepkg -s

```

Установите [zabbix-server](https://www.archlinux.org/packages/?name=zabbix-server):

```
$ sudo pacman -U zabbix-server-2.0.5-1-x86_64.pkg.tar.xz

```

## Настройка PostgreSQL

### Подготовка PostgreSQL к первому запуску

Создайте файл `tmpfiles.d` для `/run/postgresql`:

```
$ sudo systemd-tmpfiles --create postgresql.conf

```

Создайте папку для хранения баз данных:

```
$ sudo mkdir /var/lib/postgres/data

```

Установите права доступа на папку только для пользователя `postgres` и группы `postgres`:

```
$ sudo chown -c postgres:postgres /var/lib/postgres/data

```

Создайте новый кластер базы данных от пользователя `postgres`:

```
$ sudo su - postgres -c "initdb -D '/var/lib/postgres/data'"

```

### Запуск PostgreSQL

```
$ sudo systemctl start postgresql.service

```

### Установка пароля пользователю системы postgres

```
$ sudo passwd postgres

```

### Установка пароля роли postgres и разрешение подключения к базам данных только через протокол Unix

Войдите в консоль [PostgreSQL](/index.php/PostgreSQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PostgreSQL (Русский)") от роли `postgres`:

```
$ psql -U postgres

```

Установите пароль роли `postgres`:

```
postgres=# alter user postgres with password '<PASSWORD>';

```

Выйдите из консоли [PostgreSQL](/index.php/PostgreSQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PostgreSQL (Русский)"):

```
postgres=# \q

```

Измените файл `/var/lib/postgres/data/pg_hba.conf`:

```
$ sudo nano /var/lib/postgres/data/pg_hba.conf

```

Измените следующие строки для установки доступа ролей к базам данных только через протокол Unix:

```
...
host    all             all             127.0.0.1/32            trust
...
host    all             all             ::1/128                 trust
...

```

на

```
...
#host    all             all             127.0.0.1/32            trust
...
#host    all             all             ::1/128                 trust
...

```

Измените следующие строки для установки всем ролям метода аутентификации md5 через протокол Unix:

```
...
local   all             all                                     trust
...

```

на

```
...
local   all             all                                     md5
...

```

Измените строку в файле `/var/lib/postgres/data/postgresql.conf` для подключения к базам данных только через протокол Unix:

 `$ sudo nano /var/lib/postgres/data/postgresql.conf` 
```
...
#listen_addresses = 'localhost'         # what IP address(es) to listen on;
...

```

на

```
...
listen_addresses = ''                   # what IP address(es) to listen on;
...

```

Перезапустите [PostgreSQL](/index.php/PostgreSQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PostgreSQL (Русский)"):

```
$ sudo systemctl restart postgresql.service

```

### Создание и настройка базы данных zabbix для работы с Zabbix

Создайте роль `zabbix`:

```
$ createuser -U postgres -d -S -R -P zabbix

```

где `-d` - роль с правом создания баз данных; `-S` - роль без полномочий суперпользователя; `-R` - роль без права создания ролей; `-P` - назначить пароль новой роли.

ДОПОЛНИТЕЛЬНО. Измените пароль роли `zabbix`:

```
$ psql -U postgres
postgres=# \password zabbix
postgres=# \q

```

Создайте базу данных `zabbix` от роли `zabbix`:

```
$ createdb --username zabbix -E UTF8 zabbix

```

Проверьте успешность создания базы данных `zabbix`:

 `$ psql -U postgres -l` 
```
                                  Список баз данных
    Имя    | Владелец | Кодировка | LC_COLLATE  |  LC_CTYPE   |     Права доступа     
-----------+----------+-----------+-------------+-------------+-----------------------
 postgres  | postgres | UTF8      | ru_RU.UTF-8 | ru_RU.UTF-8 | 
 template0 | postgres | UTF8      | ru_RU.UTF-8 | ru_RU.UTF-8 | =c/postgres          +
           |          |           |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8      | ru_RU.UTF-8 | ru_RU.UTF-8 | =c/postgres          +
           |          |           |             |             | postgres=CTc/postgres
 zabbix    | zabbix   | UTF8      | ru_RU.UTF-8 | ru_RU.UTF-8 | 
(4 строки)

```

Заполните базу данных `zabbix` от роли `zabbix` необходимой информацией:

```
$ cd /etc/zabbix/database/postgresql
$ psql -U zabbix zabbix < schema.sql
$ psql -U zabbix zabbix < images.sql
$ psql -U zabbix zabbix < data.sql

```

Измените следующие строки в файле `/etc/zabbix/zabbix_server.conf` для работы Zabbix с [PostgreSQL](/index.php/PostgreSQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PostgreSQL (Русский)"):

 `$ sudo nano /etc/zabbix/zabbix_server.conf` 
```
...
# Default:
# DBHost=localhost
...
# Default:
# DBName=
...
# Default:
# DBUser=
...
# Default:
# DBPassword=
...
# Default (for MySQL):
# DBPort=3306
...

```

на

```
...
# Default:
# DBHost=localhost

DBHost=
...
# Default:
# DBName=

DBName=zabbix
...
# Default:
# DBUser=

DBUser=zabbix
...
# Default:
# DBPassword=

DBPassword=<PASSWORD>
...
# Default (for MySQL):
# DBPort=3306

DBPort=5432

```

### ДОПОЛНИТЕЛЬНО. Настройка контроля за объемом используемого Zabbix и PostgreSQL дискового пространства для редко изменяющейся базы данных

Измените файл `/etc/zabbix/zabbix_server.conf`:

```
$ sudo nano /etc/zabbix/zabbix_server.conf

```

Измените следующие строки для установки периодичности запуска процедуры очистки базы данных `zabbix` от устаревшей информации (в часах):

```
...
# Default:
# HousekeepingFrequency=1
...

```

на

```
...
# Default:
# HousekeepingFrequency=1

HousekeepingFrequency=24
...

```

Измените следующие строки для установки ограничения на количество удаляемых за один проход записей:

```
...
# Default:  
# MaxHousekeeperDelete=500
...

```

на

```
...
# Default:  
# MaxHousekeeperDelete=500

MaxHousekeeperDelete=5000
...

```

Проверьте включенность процедуры очистки:

```
...
# Default:  
# DisableHousekeeping=0
...

```

Измените файл `/var/lib/postgres/data/postgresql.conf`:

```
$ sudo nano /var/lib/postgres/data/postgresql.conf

```

Измените следующую строку для установки большего объема памяти для операций:

```
...
#maintenance_work_mem = 16MB            # min 1MB
...

```

на

```
...
maintenance_work_mem = 512MB            # min 1MB
...

```

Измените следующую строку для выключения процесса `autovacuum`:

```
...
#autovacuum = on                        # Enable autovacuum subprocess?  'on'
...

```

на

```
...
autovacuum = off                        # Enable autovacuum subprocess?  'on'
...

```

Перезапустите [PostgreSQL](/index.php/PostgreSQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PostgreSQL (Русский)"):

```
$ sudo systemctl restart postgresql.service

```

Для включения запуска `vacuumdb` в расписание `cron` пользователя системы `postgres` создайте и измените файл `/var/lib/postgres/.pgpass`:

 `$ sudo -u postgres nano /var/lib/postgres/.pgpass` 
```
*:*:zabbix:postgres:<PASSWORD>

```

Измените права доступа на файл `/var/lib/postgres/.pgpass`:

```
$ sudo chmod 400 /var/lib/postgres/.pgpass

```

Включите запуск `vacuumdb` в расписание `cron` пользователя системы `postgres` ежедневно в заданное время:

 `$ sudo -u postgres crontab -e` 
```
00 00 * * * vacuumdb -U postgres -w -d zabbix -q -z &

```

Запустите [cron](/index.php/Cron "Cron"):

```
$ sudo systemctl start cronie.service

```

Включите [cron](/index.php/Cron "Cron") в автозапуск:

```
$ sudo systemctl enable cronie.service

```

Во время проведения профилактических работ запустите `vacuumdb` для высвобождения дискового пространства:

```
$ sudo -u postgres vacuumdb -U postgres -w -d zabbix -f -v -z

```

### Включение PostgreSQL в автозапуск

```
$ sudo systemctl enable postgresql.service

```

## Настройка PHP и FastCGI Process Manager

### Проверка значений параметров в файле /etc/php/php.ini

 `$ sudo nano /etc/php/php.ini` 
```
...
max_execution_time = 600
...
max_input_time = 600
...
memory_limit = 256M
...
post_max_size = 32M
...
cgi.fix_pathinfo = 0
...
upload_max_filesize = 16M
...
extension=bcmath.so
...
extension=curl.so
...
extension=gd.so
...
extension=gettext.so
...
extension=pgsql.so
...
extension=sockets.so
...
date.timezone = Europe/Moscow
...

```

### Проверка значений параметров в файле /etc/php/php-fpm.conf

 `$ sudo nano /etc/php/php-fpm.conf` 
```
...
;listen = 127.0.0.1:9000
...
listen = /run/php-fpm/php-fpm.sock
...

```

### Запуск FastCGI Process Manager

```
$ sudo systemctl start php-fpm.service

```

### Включение FastCGI Process Manager в автозапуск

```
$ sudo systemctl enable php-fpm.service

```

## Настройка NGINX

### Создание самоподписанных сертификатов для подключения к Zabbix через HTTPS

```
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout zabbix.key -out zabbix.pem

```

### Перемещение и изменение прав доступа на файл приватного ключа zabbix.key

```
$ sudo mv zabbix.key /etc/ssl/private/
$ sudo chown root:root /etc/ssl/private/zabbix.key
$ sudo chmod 400 /etc/ssl/private/zabbix.key

```

### Перемещение и изменение прав доступа на файл сертификата zabbix.pem

```
$ sudo mv zabbix.pem /etc/ssl/certs/
$ sudo chown root:root /etc/ssl/certs/zabbix.pem
$ sudo chmod 400 /etc/ssl/certs/zabbix.pem

```

### Изменение файла /etc/nginx/nginx.conf

 `$ sudo nano /etc/nginx/nginx.conf` 
```
worker_processes  4;

error_log  /var/log/nginx/error.log;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;

    keepalive_timeout  65;

    gzip  off;

    server_tokens  off;

    server {
        listen <IP-ADDRESS>:80;
        server_name  <IP-ADDRESS>;
        rewrite ^ https://$server_name$request_uri? permanent;
    }

    server {
        listen       <IP-ADDRESS>:443;
        server_name  <IP-ADDRESS>;

        charset  utf-8;

        access_log  /var/log/nginx/host.access.log  main;

        ssl                  on;
        ssl_certificate      /etc/ssl/certs/zabbix.pem;
        ssl_certificate_key  /etc/ssl/private/zabbix.key;

        ssl_session_timeout  5m;

        ssl_protocols  SSLv3 TLSv1;
        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;

        location / {
            root   /srv/http/zabbix;
            index  index.php;
        }

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /usr/share/nginx/html;
        }

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
            root           html;
            fastcgi_pass   unix:/run/php-fpm/php-fpm.sock;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  /srv/http/zabbix$fastcgi_script_name;
            include        fastcgi_params;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        location ~ /\.ht {
            deny  all;
        }

        # deny access to Zabbix files
        location ~* /(?:api|conf|include)/ {
            return 301 $server_name/index.php;
        }
    }
}

```

### Запуск NGINX

```
$ sudo systemctl start nginx.service

```

### Включение NGINX в автозапуск

```
$ sudo systemctl enable nginx.service

```

## Установка и настройка агента Zabbix

### Установка zabbix-agent

Установите [zabbix-agent](https://www.archlinux.org/packages/?name=zabbix-agent) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

### Проверка значений параметров в файле /etc/zabbix/zabbix_agentd.conf

 `$ sudo nano /etc/zabbix/zabbix_agentd.conf` 
```
...
# Default:
# Server=

Server=127.0.0.1
...
# Default:
# ListenIP=0.0.0.0

ListenIP=127.0.0.1
...
# Default:
# ServerActive=

ServerActive=127.0.0.1
...

```

### Запуск агента Zabbix

```
$ sudo systemctl start zabbix-agentd.service

```

### Включение агента Zabbix в автозапуск

```
$ sudo systemctl enable zabbix-agentd.service

```

## Установка и настройка клиента NTP

### Установка ntp

Установите [ntp](/index.php/Network_Time_Protocol_daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network Time Protocol daemon (Русский)") из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

```
$ sudo pacman -S ntp

```

### Запуск клиента NTP

```
$ sudo systemctl start ntpdate.service

```

### Включение клиента NTP в автозапуск

```
$ sudo systemctl enable ntpdate.service

```

## Настройка Zabbix

### Установка аппаратных часов

```
$ sudo hwclock --systohc --utc

```

### Проверка значений параметров в файле /etc/zabbix/zabbix_server.conf

 `$ sudo nano /etc/zabbix/zabbix_server.conf` 
```
...
# Default:
# StartPollers=5

StartPollers=50
...
# Default:
# ListenIP=0.0.0.0

ListenIP=<IP-ADDRESS>
...

```

### Запуск Zabbix

```
$ sudo systemctl start zabbix-server.service

```

### Включение Zabbix в автозапуск

```
$ sudo systemctl enable zabbix-server.service

```

## Настройка Zabbix для работы с NetFlow

## Внешние источники

*   [http://umgum.com:80/zabbix-server-installation](http://umgum.com:80/zabbix-server-installation)
*   [http://umgum.com:80/zabbix-nginx-php-fastcgi](http://umgum.com:80/zabbix-nginx-php-fastcgi)
*   [http://umgum.com:80/zabbix-housekeeper-postgresql-vacuum](http://umgum.com:80/zabbix-housekeeper-postgresql-vacuum)
*   [http://habrahabr.ru/post/139165/](http://habrahabr.ru/post/139165/)
*   [http://help.ubuntu.ru/wiki/nginx-phpfpm](http://help.ubuntu.ru/wiki/nginx-phpfpm)
*   [http://www.postgresql.org/docs/8.1/static/libpq-pgpass.html](http://www.postgresql.org/docs/8.1/static/libpq-pgpass.html)