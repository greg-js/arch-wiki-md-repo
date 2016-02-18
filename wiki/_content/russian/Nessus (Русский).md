**Состояние перевода:** На этой странице представлен перевод статьи [Nessus](/index.php/Nessus "Nessus"). Дата последней синхронизации: 2014-05-17\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Nessus&diff=0&oldid=315375).

[Nessus](https://en.wikipedia.org/wiki/ru:Nessus "wikipedia:ru:Nessus") — это проприетарный [сканер уязвимостей](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%BA%D0%B0%D0%BD%D0%B5%D1%80%D1%8B_%D1%83%D1%8F%D0%B7%D0%B2%D0%B8%D0%BC%D0%BE%D1%81%D1%82%D0%B5%D0%B9 "wikipedia:ru:Сканеры уязвимостей"), бесплатный для личного пользования. Для него имеется [более 40 000 плагинов](http://www.tenable.com/plugins/), охватывающих широкий спектр локальных и удаленных проблемных мест системы.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка после установки](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
*   [3 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [4 Удаление](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Скачайте и распакуйте архив [nessus](https://aur.archlinux.org/packages/nessus/), доступный в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

Зайдите на [http://tenable.com/products/nessus/nessus-download-agreement](http://tenable.com/products/nessus/nessus-download-agreement), примите условия лицензии и скачайте пакет `Nessus-6.2.1-fc20.x86_64.rpm`.

Переместите файл RPM в каталог `nessus` (например, каталог, в который вы распаковали содержимое архива).

Теперь [соберите и установите](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Arch User Repository (Русский)") пакет, как обычно.

## Настройка после установки

Создайте SSL-сертификат для веб-интерфейса Nessus:

```
# /opt/nessus/sbin/nessuscli mkcert

```

Зарегистрируйте ваш почтовый ящик на [http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code](http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code) и дождитесь, пока вам пришлют ключ. После этого скачайте все плагины при помощи команды:

```
# /opt/nessus/bin/nessuscli fetch --register *ваш_ключ*

```

Создайте администратора Nessus (пользователи Nessus не имеют никакого отношения к пользователям Unix):

```
# /opt/nessus/sbin/nessuscli adduser *имя_пользователя*

```

## Использование

Пакет [nessus](https://aur.archlinux.org/packages/nessus/) предоставляет файл юнита `nessusd.service`, для получения дополнительной информации смотрите раздел [systemd (Русский)#Использование юнитов](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)").

Зайдите в веб-интерфейс по адресу [https://localhost:8834](https://localhost:8834) и/или используйте интерфейс командной строки (`/opt/nessus/sbin/nessuscli`). В большинстве браузеров вам потребуется вручную принять SSL-сертификат, который вы создали для сервера.

## Удаление

Пакет может быть удален при помощи [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)"), но файлы, созданные Nessus — например, база данных установленных плагинов, должны быть удалены вручную:

```
# rm -r /opt/nessus

```

**Обратите внимание:** Эта команда удалит ваши настройки Nessus.

## Смотрите также

*   [Официальная документация](http://www.tenable.com/products/nessus/documentation)