Из [домашней страницы](http://www.webmin.com/) проекта:

	*Webmin - это веб-интерфейс для системного администрирования Unix. Используя современный веб-браузер, вы можете настроить учётные записи пользователей, Apache, DNS, файл-сервер и многое другое. Webmin избавляет от необходимости вручную редактировать конфигурационные файлы Unix, такие как `/etc/passwd`, а также позволяет управлять системой из консоли или удалённо. Смотрите страницу [стандартных модулей](http://www.webmin.com/standard.html) Webmin или [скриншоты](http://www.webmin.com/demo.html).*

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [4 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)

## Установка

Установите [webmin](https://aur.archlinux.org/packages/webmin/) из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Чтобы иметь возможность взаимодействовать с Webmin по [https](https://en.wikipedia.org/wiki/https "wikipedia:https") протоколу нужно также установить пакет [perl-net-ssleay](https://www.archlinux.org/packages/?name=perl-net-ssleay).

## Настройка

Чтобы иметь доступ к Webmin с удаленного компьютера, необходимо в файле настроек `/etc/webmin/miniserv.conf` разрешить доступ с нужного адреса или подсети. По умолчанию в панель Webmin можно заходить только с локальной (127.0.0.1) машины.

```
allow=127.0.0.1 192.168.1.0

```

В этом примере к Webmin будут иметь доступ компьютеры, находящиеся в подсети 192.168.1.0.

## Запуск

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `webmin.service`, которая управляет демоном Webmin.

## Использование

В веб-браузере наберите адрес сервера, на котором установлен Webmin, указав порт 10000\. Например:

```
http://192.168.1.1:10000
https://192.168.1.1:10000
https://myserver.example.net:10000

```

Для доступа нужно будет ввести root-пароль от сервера.

## Решение проблем

Если вы получаете подобное сообщение об ошибке:

```
Can't locate timelocal.pl in @INC (@INC contains: /opt/webmin /usr/lib/perl5/site_perl /usr/share/perl5/site_perl /usr/lib/perl5/vendor_perl /usr/share/perl5/vendor_perl /usr/lib/perl5/core_perl /usr/share/perl5/core_perl . /opt/webmin/ ..) at /opt/webmin/useradmin/edit_user.cgi line 6.

```

например, при добавлении нового пользователя в систему,тогда [необходимо установить](https://bbs.archlinux.org/viewtopic.php?id=142757) пакет [perl-perl4-corelibs](https://www.archlinux.org/packages/?name=perl-perl4-corelibs).