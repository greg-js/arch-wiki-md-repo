[ZoneMinder](https://www.zoneminder.com/) - это интегрированный набор приложений, которые обеспечивают полное решение для видео наблюдения, позволяющее осуществлять захват, анализ, запись и мониторинг любых камер видеонаблюдения или камер безопасности, подключенных к компьютерам на базе Linux. Приложение предназначено для работы с дистрибутивами, поддерживающими интерфейс Video For Linux (V4L), и было протестировано с видеокамерами, подключенными к картам BTTV, различными USB-камерами, а также поддерживает большинство IP-камер.

## Contents

*   [1 Установка](#Установка)
*   [2 Конфигурация](#Конфигурация)
    *   [2.1 Apache](#Apache)
    *   [2.2 PHP](#PHP)
    *   [2.3 MySQL](#MySQL)
    *   [2.4 Запуск](#Запуск)
*   [3 Поиск проблем](#Поиск_проблем)
    *   [3.1 Flushing application data](#Flushing_application_data)
        *   [3.1.1 Восстановить базу данных](#Восстановить_базу_данных)
        *   [3.1.2 Очистка папки кеша](#Очистка_папки_кеша)
    *   [3.2 Локальные видеоустройства](#Локальные_видеоустройства)
    *   [3.3 Несколько локальных USB-камер](#Несколько_локальных_USB-камер)
*   [4 Смотрите также](#Смотрите_также)

## Установка

**Примечание:** Очень важно, для работы ZoneMinder, должен установлен и правильно настроен стек [LAMP](/index.php/LAMP "LAMP").

[установка](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0 "Установка") the [zoneminder](https://aur.archlinux.org/packages/zoneminder/) package. The development branch is also available with [zoneminder-git](https://aur.archlinux.org/packages/zoneminder-git/).

Для создания миниатюр (используется редко) установите пакет: [netpbm](https://www.archlinux.org/packages/?name=netpbm).

После завершения настройки и запуска демона, веб-интерфейс будет доступен: [http://localhost/zoneminder/](http://localhost/zoneminder/).

## Конфигурация

### Apache

Включите PHP, как описано в [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Раскомментируйте следующую строку в `/etc/httpd/conf/httpd.conf`:

```
LoadModule cgi_module modules/mod_cgi.so

```

Включите конфигурационный файл `httpd-zoneminder`, добавив эту строку в конец `httpd.conf`:

```
Include conf/extra/httpd-zoneminder.conf

```

### PHP

Привить: `/etc/php/php.ini`. Убедитесь, что следующие расширения включены, раскомментируя эти строки:

```
 extension=ftp
 extension=gd
 extension=gettext
 extension=mcrypt
 extension=pdo_mysql
 extension=sockets
 extension=zip

```

Также установите часовой пояс, пример:

```
date.timezone = "Europe/Kiev"

```

Смотреть [http://php.net/manual/en/timezones.php](http://php.net/manual/en/timezones.php) для просмотра списка часовых поясов.

### MySQL

Создание базы данных zm и пользователя с соответствующими разрешениями и паролем:

 `$ mysql -u root -p` 
```
CREATE DATABASE zm;
CREATE USER 'zmuser'@'localhost' IDENTIFIED BY 'choose_password';
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
ZM_DB_PASS=chosen_password
```

### Запуск

[Запустить](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D1%8C "Запустить")/[Включить](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C "Включить") `httpd.service` и `zoneminder.service`.

## Поиск проблем

Журналы по умолчанию хранятся в `/var/log/zoneminder`. Вы также можете смотреть журнал в веб-интерфейсе.

Страница wiki, [Troubleshooting](http://www.zoneminder.com/wiki/index.php/Troubleshooting).

### Flushing application data

This is useful for developers or users that need to wipe all ZoneMinder and start fresh.

#### Восстановить базу данных

Удалить базу данных и пользователя ZoneMinder MySQL:

 `$ mysql -u root -p` 
```
DROP DATABASE zm;
DROP USER 'zmuser'@'localhost';

```

Пересоздать базу данных и пользователя:

 `$ mysql -u root -p` 
```
CREATE DATABASE zm;
CREATE USER 'zmuser'@'localhost' IDENTIFIED BY 'choose_password';
GRANT CREATE, INSERT, SELECT, DELETE, UPDATE ON zm.* TO 'zmuser'@'localhost';
exit
```

Импортировать данные в недавно созданную базу данных zm:

```
$ mysql -u root -p zm < /usr/share/zoneminder/db/zm_create.sql

```

#### Очистка папки кеша

Примечание: при этом удаляются все изображения и события!

```
$ rm -Rf /var/cache/zoneminder/events/* /var/cache/zoneminder/images/* /var/cache/zoneminder/temp/*

```

### Локальные видеоустройства

Важно, чтобы пользователь, работающий с httpd (обычно *'http'* ), мог получить доступ к вашим камерам, например:

 `$ groups http`  `video http`  `$ ls -l /dev/video0`  `crw-rw----+ 1 root video 81, 0 Oct 28 21:54 /dev/video0` 

То есть, добавьте пользователя **http** в группу **video**.

 `$ sudo usermod -aG video http` 

### Несколько локальных USB-камер

Если вы заметили ошибку, например, **libv4l2: error turning on stream: при использовании нескольких USB-видеоустройств (например, нескольких веб-камер) на устройстве не осталось места, вам может потребоваться увеличить пропускную способность на шине.**

Сначала проверьте, остановив `zoneminder.service`, затем:

```
$ rmmod uvcvideo
$ modprobe uvcvideo quirks=128

```

Запустите `zoneminder.service`, и если проблема решена, сохраните изменение, добавив параметр модуля в `/etc/modprobe.d/uvcvideo.conf`. например:

```
options uvcvideo nodrop=1 quirks=128

```

([ссылка](http://renoirsrants.blogspot.com.au/2011/07/multiple-webcams-on-zoneminder.html))

## Смотрите также

*   [http://www.zoneminder.com/wiki/index.php/Arch_Linux](http://www.zoneminder.com/wiki/index.php/Arch_Linux) — Страница проекта.