## Contents

*   [1 Вступление](#Вступление)
    *   [1.1 Установка](#Установка)
        *   [1.1.1 AUR](#AUR)
        *   [1.1.2 Инструкция по установке](#Инструкция_по_установке)
    *   [1.2 Удаление](#Удаление)
    *   [1.3 Смотрите также](#Смотрите_также)

# Вступление

XAMPP - облегченный вариант установки Apache в связке с MySQL, PHP и Perl. Он содержит: Apache, MySQL, PHP & PEAR, Perl, ProFTPD, phpMyAdmin, OpenSSL, GD, Freetype2, libjpeg, libpng, gdbm, zlib, expat, Sablotron, libxml, Ming, Webalizer, pdf class, ncurses, mod_perl, FreeTDS, gettext, mcrypt, mhash, eAccelerator, SQLite и IMAP C-Client.

## Установка

### AUR

Установите пакет [xampp](https://aur.archlinux.org/packages/xampp/).

### Инструкция по установке

1.  Загружаем последнюю версию [отсюда](http://www.apachefriends.org/en/xampp-linux.html#374)
2.  Проверяем наличие в системе пользователя `nobody` и группы `nogroup`, если нет - создаем
3.  Открываем в терминале папку с только что скачанным файлом и запускаем его от имени суперпользователя
4.  Команды для управления XAMPP: `/opt/lampp/lampp {start,stop,restart`}

**Примечание:** Если у вас 64-битная система, необходимо установить пакеты [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc) и [lib32-gcc-libs](https://www.archlinux.org/packages/?name=lib32-gcc-libs)

## Удаление

Все файлы, необходимые XAMPP, размещены в папке, в которую мы извлекли архив (использовали `/opt/lampp`). То есть, нам нужно просто удалить данную папку.

**Примечание:** Если вы создавали символьные ссылки, не забудьте удалить и их

## Смотрите также

*   [Сайт XAMPP](http://www.apachefriends.org/en/xampp.html)