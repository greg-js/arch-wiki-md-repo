**Состояние перевода:** На этой странице представлен перевод статьи [ZoneMinder](/index.php/ZoneMinder "ZoneMinder"). Дата последней синхронизации: 22 ноября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=ZoneMinder&diff=0&oldid=556586).

[ZoneMinder](https://www.zoneminder.com/) — это интегрированный набор приложений, которые обеспечивают полное решение для видео наблюдения, позволяющее осуществлять захват, анализ, запись и мониторинг любых камер видеонаблюдения или камер безопасности, подключенных к компьютерам на базе Linux. Приложение предназначено для работы с дистрибутивами, поддерживающими интерфейс Video For Linux (V4L), и было протестировано с видеокамерами, подключенными к картам BTTV, различными USB-камерами, а также поддерживает большинство IP-камер.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Конфигурация](#Конфигурация)
    *   [2.1 Apache](#Apache)
    *   [2.2 PHP](#PHP)
    *   [2.3 MySQL](#MySQL)
        *   [2.3.1 Безопасность](#Безопасность)
    *   [2.4 Запуск](#Запуск)
*   [3 Решение проблем](#Решение_проблем)
    *   [3.1 Очистка данных приложения](#Очистка_данных_приложения)
        *   [3.1.1 Восстановление базы данных](#Восстановление_базы_данных)
        *   [3.1.2 Очистка папки кеша](#Очистка_папки_кеша)
    *   [3.2 Локальные видеоустройства](#Локальные_видеоустройства)
    *   [3.3 Несколько локальных USB-камер](#Несколько_локальных_USB-камер)
*   [4 Смотрите также](#Смотрите_также)

## Установка

**Примечание:** Очень важно установить и правильно настроить стек [LAMP](/index.php/LAMP "LAMP") для работы ZoneMinder.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [zoneminder](https://aur.archlinux.org/packages/zoneminder/). Также можно использовать ветку разработки, установив пакет [zoneminder-git](https://aur.archlinux.org/packages/zoneminder-git/).

Для создания миниатюр (используется редко) установите пакет [netpbm](https://www.archlinux.org/packages/?name=netpbm).

После завершения настройки и запуска системной службы, веб-интерфейс будет доступен по следующему адресу: [http://localhost/zoneminder/](http://localhost/zoneminder/).

## Конфигурация

### Apache

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") PHP, как описано в [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Раскомментируйте следующую строку в `/etc/httpd/conf/httpd.conf`:

```
LoadModule cgi_module modules/mod_cgi.so

```

Включите конфигурационный файл `httpd-zoneminder`, добавив эту строку в конец `httpd.conf`:

```
Include conf/extra/httpd-zoneminder.conf

```

### PHP

Отредактируйте `/etc/php/php.ini`. Убедитесь, что следующие расширения включены, раскомментируя эти строки:

```
extension=apcu
extension=ftp
extension=gd
extension=gettext
extension=pdo_mysql
extension=sockets
extension=zip

```

Также задайте часовой пояс, например:

```
date.timezone = "Europe/Kiev"

```

Смотрите [http://php.net/manual/en/timezones.php](http://php.net/manual/en/timezones.php) для просмотра списка часовых поясов.

Иногда может присутствовать следующий файл /etc/php/conf.d/zoneminder.ini:

```
extension=apcu
extension=ftp
extension=gd
extension=gettext
extension=pdo_mysql
extension=sockets
extension=zip

```

```
date.timezone = PLACEHOLDER

```

если часовой пояс не заполнен, выполните:

```
sed -i 's|PLACEHOLDER|'`timedatectl | grep "Time zone" | tr -s ' ' | cut -f4 -d ' '`'|g' /etc/php/conf.d/zoneminder.ini

```

### MySQL

Создание базы данных zm и пользователя с соответствующими разрешениями и паролем:

 `$ mysql -u root -p` 
```
CREATE DATABASE zm;
CREATE USER 'zmuser'@'localhost' IDENTIFIED BY 'zmpass';
GRANT ALL ON zm.* TO 'zmuser'@'localhost';
exit
```

Импортируйте предварительно сконфигурированные таблицы в недавно созданную базу данных zm:

```
$ mysql -u root -p zm < /usr/share/zoneminder/db/zm_create.sql

```

Обновите конфигурацию ZoneMinder с новыми параметрами:

 `/etc/zm.conf` 
```
ZM_DB_HOST=localhost
ZM_DB_NAME=zm
ZM_DB_USER=zmuser
ZM_DB_PASS=zmpass
```

#### Безопасность

Для повышения безопасности нужно установить пароль для пользователя root:

```
/usr/bin/mysqladmin' -u root password 'new-password'
/usr/bin/mysqladmin' -u root -h lilya-x64 password 'new-password'

```

Кроме того, вы можете запускать:

```
/usr/bin/mysql_secure_installation

```

### Запуск

[Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите")/[включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службы `httpd.service`, `zoneminder.service`, `fcgiwrap-multiwatch` и `php-fpm.service`.

```
systemctl start php-fpm
systemctl enable php-fpm 

```

```
systemctl start httpd
systemctl enable httpd 

```

```
systemctl start zoneminder
systemctl enable zoneminder

```

```
systemctl start fcgiwrap-multiwatch
systemctl enable fcgiwrap-multiwatch

```

## Решение проблем

По умолчанию, логи хранятся в `/var/log/zoneminder`. Вы также можете просматривать логи в веб-интерфейсе.

Также смотрите официальную wiki-страницу проекта: [Troubleshooting](http://www.zoneminder.com/wiki/index.php/Troubleshooting).

### Очистка данных приложения

Данная функция будет полезна разработчикам или пользователям, которым нужно очистить все данные ZoneMinder и начать настройку с нуля.

#### Восстановление базы данных

Удалите базу данных ZoneMinder и пользователя MySQL:

 `$ mysql -u root -p` 
```
DROP DATABASE zm;
DROP USER 'zmuser'@'localhost';

```

Пересоздайте базу данных и пользователя:

 `$ mysql -u root -p` 
```
CREATE DATABASE zm;
CREATE USER 'zmuser'@'localhost' IDENTIFIED BY 'zmpass';
GRANT CREATE, INSERT, SELECT, DELETE, UPDATE ON zm.* TO 'zmuser'@'localhost';
exit
```

Импортируйте предварительно сконфигурированные таблицы в недавно созданную базу данных zm:

```
$ mysql -u root -p zm < /usr/share/zoneminder/db/zm_create.sql

```

#### Очистка папки кеша

**Важно:** При выполнении команды ниже будут удалены все изображения и события.

```
$ rm -Rf /var/cache/zoneminder/events/* /var/cache/zoneminder/images/* /var/cache/zoneminder/temp/*

```

### Локальные видеоустройства

Важно, чтобы пользователь, выполняющий httpd (обычно **http**), мог получить доступ к вашим камерам, например:

 `$ groups http`  `video http`  `$ ls -l /dev/video0`  `crw-rw----+ 1 root video 81, 0 Oct 28 21:54 /dev/video0` 

То есть, добавьте пользователя **http** в группу **video**.

```
sudo usermod -aG video http

```

### Несколько локальных USB-камер

Если вы заметили ошибку, например, **libv4l2: error turning on stream: No space left on device** при использовании нескольких USB-видеоустройств (к примеру, нескольких веб-камер), вам может потребоваться увеличить пропускную способность шины.

Сначала проверьте это, [остановив](/index.php/%D0%9E%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Остановите") `zoneminder.service` и выполнив данные команды:

```
$ rmmod uvcvideo
$ modprobe uvcvideo quirks=128

```

[Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") `zoneminder.service` и если проблема решена, сохраните изменение, добавив параметр модуля в `/etc/modprobe.d/uvcvideo.conf`. Например:

```
options uvcvideo nodrop=1 quirks=128

```

([источник](http://renoirsrants.blogspot.com.au/2011/07/multiple-webcams-on-zoneminder.html))

## Смотрите также

*   [http://www.zoneminder.com/wiki/index.php/Arch_Linux](http://www.zoneminder.com/wiki/index.php/Arch_Linux) — Страница проекта.