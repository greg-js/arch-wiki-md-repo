[Zabbix](http://zabbix.com) — полноценное решение для мониторинга крупных компьютерных сетей. Он может находить все типы сетевых устройств используя различные методы, проверять состояние оборудования и приложений, отправлять заданные сообщения о тревоге и визуализировать сложные взаимосвязи.

## Contents

*   [1 Сервер](#.D0.A1.D0.B5.D1.80.D0.B2.D0.B5.D1.80)
    *   [1.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [1.3 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [2 Клиент](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82)
    *   [2.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_2)
    *   [2.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_2)
    *   [2.3 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_2)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Отладка агента Zabbix](#.D0.9E.D1.82.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0_.D0.B0.D0.B3.D0.B5.D0.BD.D1.82.D0.B0_Zabbix)
    *   [3.2 Наблюдение системных обновлений ArchLinux](#.D0.9D.D0.B0.D0.B1.D0.BB.D1.8E.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D1.85_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B9_ArchLinux)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Сервер

### Установка

Если вы хотите использовать Zabbix server с [MariaDB](/index.php/MariaDB "MariaDB"), установите [zabbix-server-mysql](https://aur.archlinux.org/packages/zabbix-server-mysql/) из [AUR](/index.php/AUR "AUR"). Для использования с [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), вам следует использовать [zabbix-server](https://aur.archlinux.org/packages/zabbix-server/). Также вам необходимо выбрать веб-сервер с поддержкой PHP, например:

*   [Apache](/index.php/LAMP "LAMP")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [NginX](/index.php/NginX "NginX")

Или любой другой подходящий сервер, который вы можете найти в категории [веб-серверы](/index.php/Category:Web_server "Category:Web server").

Вы можете отредактировать файлы [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") если хотите использовать Nginx в качестве веб-сервера, так как по умолчанию они имеют зависимости от [apache](https://www.archlinux.org/packages/?name=apache) и [php-apache](https://www.archlinux.org/packages/?name=php-apache).

### Настройка

Создайте символическую ссылку на корневой каталог веб-приложения Zabbix в месте расположения html-документов вашего сервера, например:

```
$ ln -s /usr/share/webapps/zabbix /var/www

```

Убедитесь, что настройки в `php.ini` как минимум удовлетворяют минимальным требованиям из следующих настроек:

```
extension=bcmath.so
extension=gd.so
extension=sockets.so
post_max_size = 16M
max_execution_time = 300
max_input_time = 300
date.timezone = "UTC"
always_populate_raw_post_data = -1

```

В этом примере мы создадим на локальной машине (`localhost`) базу данных MariaDB `zabbix` для пользователя `zabbix`, с паролем `test` и импортируем шаблоны базы данных. Это соединение будет использоваться сервером Zabbix:

```
$ mysql -u root -p -e "create database zabbix"
$ mysql -u root -p -e "grant all on zabbix.* to zabbix@localhost identified by 'test'"
$ mysql -u zabbix -p zabbix < /etc/zabbix/database/schema.sql
$ mysql -u zabbix -p zabbix < /etc/zabbix/database/images.sql
$ mysql -u zabbix -p zabbix < /etc/zabbix/database/data.sql

```

### Запуск

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `zabbix-server`.

После запуска вы сможете локально зайти на панель Zabbix, то есть, [http://127.0.0.1/zabbix](http://127.0.0.1/zabbix), пройти установку и получить доступ к веб-интерфейсу. В качестве пользователя по умолчанию используется `Admin` с паролем `zabbix`.

Официальная документация содержит информацию по дальнейшей настройке и использованию Zabbix. Ссылку на документацию вы можете найти в конце статьи.

## Клиент

### Установка

Серверный пакет уже содержит клиент (агент) Zabbix, но вы можете установить его отдельно с пакетом [zabbix-agent](https://aur.archlinux.org/packages/zabbix-agent/), если вам не нужен сервер.

### Настройка

В файле настроек `zabbix_agentd.conf` добавьте IP сервера в список опции `Server`. Только серверы из этого списка смогут получить доступ к агенту.

```
Server=127.0.0.1
ServerActive=

```

Убедитесь, что порт `10050` на устройстве, где установлен агент не заблокирован межсетевым экраном и правильно пробрасывается.

### Запуск

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `zabbix-agentd`.

## Советы и рекомендации

### Отладка агента Zabbix

На сайте клиента вы можете проверить состояние объекта командой:

```
zabbix_agentd -t hdd.smart[sda,Temperature_Celsius]

```

На сервере команда будет выглядеть следующим образом:

```
zabbix_get -s *host* -k hdd.smart[sda,Temperature_Celsius]

```

### Наблюдение системных обновлений ArchLinux

Здесь приведен метод мониторинга клиентов с ArchLinux на наличие системных обновлений с использованием опции `UserParameter`:

 `/etc/zabbix/zabbix_agentd.conf`  `Include=/etc/zabbix/zabbix_agentd.conf.d/*.conf`  `/etc/zabbix/zabbix_agentd.conf.d/archlinuxupdates.conf`  `UserParameter=archlinuxupdates,checkupdates | wc -l` 

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") `zabbix-agentd` для того, чтобы изменения вступили в силу. Это создаст новый параметр мониторинга `archlinuxupdates`. Он возвращает число пакетов, которые нуждаются в обновлении.

## Смотрите также

*   [Official manual for version 2.0](https://www.zabbix.com/documentation/doku.php?id=2.0)