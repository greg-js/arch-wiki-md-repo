## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Instalace](#Instalace)
*   [3 Konfigurace](#Konfigurace)
    *   [3.1 Základní nastavení](#Z.C3.A1kladn.C3.AD_nastaven.C3.AD)
*   [4 FastCGI](#FastCGI)
    *   [4.1 PHP](#PHP)
    *   [4.2 Ruby on Rails](#Ruby_on_Rails)

## Úvod

> lighttpd je bezpečný, rychlý a velmi flexibilní web-server, který byl optimalizovaný pro vysoký výkon. V porovnání s jinými webservery má velmi nízké nároky na paměť a na rychlost procesoru. Podporuje například FastCGI, CGI, Auth, Output-Compression, URL-Rewriting a plno dalších vymoženstí.

Zdroj: [Webová stránka projektu lighttpd](http://trac.lighttpd.net/).

## Instalace

Pro instalaci [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) spusťte:

```
# pacman -S lighttpd

```

## Konfigurace

### Základní nastavení

Hlavní konfigurační soubor tohoto [daemona](/index.php/Daemon_(%C4%8Cesky) "Daemon (Česky)") je: `/etc/lighttpd/lighttpd.conf`. Ve výchozím nastavení by se měla zobrazovat zkušební testovací stránka.

Pro kontrolu chyb ve vašem lighttpd.conf souboru můžete použít tento příkaz:

```
$ lighttpd -t -f /etc/lighttpd/lighttpd.conf

```

Jako kořenový adresář je v konfiguračním souboru nastaven `/srv/http/`.

Prevděpodobně budete muset přidat nového uživatele a skupinu http, pokud ji ještě nemáte vytvořenou. Tento uživatel musí mít právo zápisu do `/var/log/lighttpd`. Postup, jak nastavit správného vlastníka a skupinu složky je následující:

```
# groupadd http
# adduser http
# chown -R http /var/log/lighttpd

```

Pro otestování správnosti instalace

```
# /etc/rc.d/lighttpd start
# touch /srv/http/index.html
# chmod 755 /srv/http/index.html
# echo 'Hello World!' >> /srv/http/index.html

```

Následně zadejte do svého prohlížeče adresu localhost a měli byste vidět testovací stránku s nápisem 'Hello World!'.

Pravděpodobně si budte chtít přidat lighttpd do pole daemonů, kteří se automaticky spouští při startu počítače. To provedete přidáním lighttpd do souboru `[/etc/rc.conf](/index.php/Rc.conf_(%C4%8Cesky) "Rc.conf (Česky)")` mezi DAEMONS (...)

## FastCGI

Instalace fcgi

```
# pacman -S fcgi

```

Následně byste měli mít funkční podporu pro fcgi. Ten kdo by chtěl mít podporu Ruby on Rails, ať pokračuje dále.

**Note:** Nový defaultní uživatel a skupina: Nově místo skupiny "nobody" běží lighttpd defaultně pod uživatelem a skupinou "http".

Následující nastavení je potřeba přidat do konfiguračního souboru /etc/lighttpd/lighttpd.conf

```
server.modules = (
    "mod_access",
    "mod_fastcgi",
    "mod_accesslog"
)

server.indexfiles = ( "dispatch.fcgi", "index.php" ) #dispatch.fcgi if rails specified

server.error-handler-404   = "/dispatch.fcgi" #too
fastcgi.server = (
".fcgi" =>
  ( "localhost" =>
    (
      "socket" => "/tmp/rails-fastcgi.socket",
      "bin-path" => "/path/to/rails/application/public/dispatch.fcgi"
    )
  ),
".php" =>
  ( "localhost" =>
    (
      "socket" => "/tmp/php-fastcgi.socket",
      "bin-path" => "/usr/bin/php-cgi"
    )
  )
)

```

Pro podporu PHP nebo Ruby on Rails pokračujte dále.

### PHP

Nainstalujte PHP a ostatní potřebné moduly,

```
# pacman -S php php-cgi

```

Zkontrolujte, jestli [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) běží tak, jak má *php-cgi --version*

```
PHP 5.3.1 with Suhosin-Patch (cgi-fcgi) (built: Nov 23 2009 21:12:29)
Copyright (c) 1997-2009 The PHP Group
Zend Engine v2.3.0, Copyright (c) 1998-2009 Zend Technologies

```

Pokud dostanete podobný výstup, máte PHP nainstalováno správně.

**Poznámka**: Mějte prosím na paměti, že pokud se vám zobrazí chyby jako *No input file found* po zobrazení vašich PHP souborů, ujistěte se, že máte v `/etc/php/php.ini` zapnuty tyto direktivy:

```
cgi.fix_pathinfo=1
open_basedir = /home/:/tmp/:/usr/share/pear/:/another/path:/second/path

```

A že jsou soubory čitelné

```
# chmod -R 755

```

### Ruby on Rails

Vzhledem k tomu, že chcete používat Ruby on Rails, předpokládáme, že máte v počítači nainstalováno ruby. Pokud ne, nainstalujte jej.

Dále potřebujeme stáhnout rubygems a ruby-fcgi. Mrkněte do [AURu](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)")

Rubygems

```
$ sudo pacman -S rubygems

```

[ruby-fcgi](https://aur.archlinux.org/packages/ruby-fcgi/)

```
$ wget [https://aur.archlinux.org/packages/ruby-fcgi/ruby-fcgi/PKGBUILD](https://aur.archlinux.org/packages/ruby-fcgi/ruby-fcgi/PKGBUILD)
$ makepkg
$ sudo pacman -U ruby-fcgi-x.x.x-x-xxx.pkg.tar.gz

```

Teď už máme rubygems. Pojďme ještě nainstalovat rails!

```
$ sudo gem install rails --include-dependencies
$ sudo gem install fcgi --include-dependencies

```
Pokud výsledek skončí chybou, spusťte `# pacman -S fcgi` nebo si stáhněte [zdrojové kódy](http://fastcgi.com/dist/fcgi.tar.gz) a vše si zkompilujte sami.
```
$ wget [http://fastcgi.com/dist/fcgi.tar.gz](http://fastcgi.com/dist/fcgi.tar.gz)
$ tar zxvf fcgi.tar.gz
$ cd fcgi-2.4.0
$./configure
$ make
# make install

```

A znovu spusťte gem pro instalaci.

Zkontrolujte, jeslti náhodou nemáte v systému více jak jeden soubor `fcgi.so`

```
$ find /usr -name fcgi.so

```

Pokud ano, odstraňte ten, který nemá ve své cestě "/site_ruby/".

Pro dokumentaci jak používat Ruby on Rails navštivte [RubyOnRails.org](http://rubyonrails.org).