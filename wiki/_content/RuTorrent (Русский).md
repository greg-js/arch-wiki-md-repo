# RuTorrent (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

**[ruTorrent](http://code.google.com/p/rutorrent/)** это веб-интерфейс для rtorrent (консольный BitTorrent клиент). Он использует протокол XMLRPC для управления rtorrent'ом.

Он легкий, расширяемый и внешне схож с µTorrent.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка веб-сервера](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B2.D0.B5.D0.B1-.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [2.1 Apache](#Apache)
    *   [2.2 Nginx](#Nginx)
*   [3 Конфигурация ruTorrent](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F_ruTorrent)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)
*   [5 Внешние ссылки](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

Установите пакет [rutorrent](https://aur.archlinux.org/packages/rutorrent/)<sup><small>AUR</small></sup> и, дополнительно, [rutorrent-plugins](https://aur.archlinux.org/packages/rutorrent-plugins/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/rutorrent-plugins)]</sup>.

## Настройка веб-сервера

### Apache

Установите и настройте Apache с PHP в соответствии с [LAMP](/index.php/LAMP_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LAMP (Русский)")

*   Отредактируйте значение _open_basedir_ в /etc/php/php.ini включив:

```
/etc/webapps/rutorrent/conf/:/usr/share/webapps/rutorrent/php/:/usr/share/webapps/rutorrent/

```

Установите пакет [mod_scgi](https://aur.archlinux.org/packages/mod_scgi/)<sup><small>AUR</small></sup>.

*   Укажите SCGI модуль в `/etc/httpd/conf/httpd.conf`:

```
LoadModule scgi_module modules/mod_scgi.so

```

*   Подключите к rTorrent [XMLRPC шлюз](/index.php/RTorrent_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#XMLRPC_interface "RTorrent (Русский)")

*   Включите выбранный в rTorrent SCGI порт добавив в `/etc/httpd/conf/httpd.conf`:

```
SCGIMount /RPC2 127.0.0.1:5000

```

*   Добавьте каталог ruTorrent, указав в `/etc/httpd/conf/httpd.conf` нечто подобное:

```
<IfModule alias_module>
  Alias /rutorrent /usr/share/webapps/rutorrent
  <Directory "/usr/share/webapps/rutorrent">
    Order allow,deny
    Allow from all
  </Directory>
</IfModule>

```

Для Apache 2.4 будет примерно такого вида:

```
<IfModule alias_module>
  Alias /rutorrent /usr/share/webapps/rutorrent
  <Directory "/usr/share/webapps/rutorrent">
    Require all granted
  </Directory>
</IfModule>

```

**Обратите внимание:** Также пример конфигурации _httpd.conf_ можно взять в `/etc/webapps/rutorrent/apache.example.conf`, а для виртуального хоста _extra/httpd-vhosts.conf_ в `/etc/webapps/rutorrent/apache.example.site.conf`

**Обратите внимание:** Вы должны включить аутентификацию средствами Apache, если ваш сайт является открытым.

### Nginx

*   Отредактируйте значение _open_basedir_ в /etc/php/php.ini включив:

```
/etc/webapps/rutorrent/conf/:/usr/share/webapps/rutorrent/php/:/usr/share/webapps/rutorrent/

```

*   Подключите к rTorrent [XMLRPC шлюз](/index.php/RTorrent_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#XMLRPC_interface "RTorrent (Русский)")

*   Добавьте следующую секцию в вашей конфигурации nginx

```
           location /RPC2 {
               include scgi_params;
               scgi_pass localhost:5000;
           }

```

*   Перезапустите nginx:

```
# systemctl restart nginx

```

## Конфигурация ruTorrent

См. вики-страницу [тут](https://github.com/Novik/ruTorrent/wiki/Config.ru).

## Смотрите также

*   [LAMP](/index.php/LAMP_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LAMP (Русский)")
*   [RTorrent](/index.php/RTorrent_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "RTorrent (Русский)")

## Внешние ссылки

*   [https://github.com/Novik/ruTorrent/wiki/Home.ru](https://github.com/Novik/ruTorrent/wiki/Home.ru)
*   [http://httpd.apache.org/docs/2.2/configuring.html](http://httpd.apache.org/docs/2.2/configuring.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=RuTorrent_(Русский)&oldid=411605](https://wiki.archlinux.org/index.php?title=RuTorrent_(Русский)&oldid=411605)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications (Русский)](/index.php/Category:Internet_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Internet applications (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")