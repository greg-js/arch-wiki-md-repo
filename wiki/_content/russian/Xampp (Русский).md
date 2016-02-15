## Contents

*   [1 Вступление](#.D0.92.D1.81.D1.82.D1.83.D0.BF.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [1.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
        *   [1.1.1 AUR](#AUR)
        *   [1.1.2 Инструкция по установке](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BA.D1.86.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B5)
    *   [1.2 Удаление](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [1.3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

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

**Обратите внимание:** Если у вас 64-битная система, необходимо установить пакеты [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc) и [lib32-gcc-libs](https://www.archlinux.org/packages/?name=lib32-gcc-libs)

## Удаление

Все файлы, необходимые XAMPP, размещены в папке, в которую мы извлекли архив (использовали `/opt/lampp`). То есть, нам нужно просто удалить данную папку.

**Обратите внимание:** Если вы создавали символьные ссылки, не забудьте удалить и их

## Смотрите также

*   [Сайт XAMPP](http://www.apachefriends.org/en/xampp.html)