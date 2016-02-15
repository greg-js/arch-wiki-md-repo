## Contents

*   [1 Apache, PHP, a MySQL](#Apache.2C_PHP.2C_a_MySQL)
    *   [1.1 Nainstaluje balíčky](#Nainstaluje_bal.C3.AD.C4.8Dky)
    *   [1.2 Konfigurace Apache](#Konfigurace_Apache)
    *   [1.3 Konfigurace PHP4 & PHP5](#Konfigurace_PHP4_.26_PHP5)
    *   [1.4 Nastavení podpory MySQL](#Nastaven.C3.AD_podpory_MySQL)
        *   [1.4.1 Intial Configuration](#Intial_Configuration)
        *   [1.4.2 Další konfigurace](#Dal.C5.A1.C3.AD_konfigurace)
    *   [1.5 Instalace PHPMyAdmin](#Instalace_PHPMyAdmin)
    *   [1.6 externi odkazy](#externi_odkazy)

### Apache, PHP, a MySQL

Tento dokument popisuje jak nastavit Apache web server na Arch Linuxu. Také popisuje instalaci PHP a MySQL a jejich integraci do Apache serveru.

#### Nainstaluje balíčky

```
# pacman -S apache php mysql

```

Pokud chcete, můžete nainstalovat jenom Apache, Apache a PHP, nebo všechny tři. Tento dokumetn obsahuje instalaci všech tří, ale pokud chcete, můžete některé části vynechat.

#### Konfigurace Apache

*   Přidejte řádek do `/etc/hosts` (pokud tento soubor neexistuje vytvořte ho)

```
127.0.0.1  localhost.localdomain   localhost

```

**Note:** pokud chcete jiiný hostname, připište jej nakonec:

```
127.0.0.1  localhost.localdomain   localhost myhostname

```

*   Editujte `/etc/rc.conf`:

Pokud jste v předchozím korku nastavili vlastní hostname, musíte sem uvést to samé. V opačném případě napište localhost

```
#
# Networking
#
HOSTNAME="localhost"

```

*   Okomentujte jeden řádek v httpd.conf

```
# nano /etc/httpd/conf/httpd.conf

```

```
LoadModule unique_id_module        modules/mod_unique_id.so

```

na

```
#LoadModule unique_id_module        modules/mod_unique_id.so

```

*   Spustťe v terminálu (jako root)

```
# /etc/rc.d/httpd start

```

*   Apache by nyní měl běžet. Můžete se o tom přesvědčit na adrese `[http://localhost/](http://localhost/)`. Měloa by se zobrazit jednoduchá stránka _Powered by Apache_

*   Pokud chcete spouštět Apache automaticky při bootování, upravte `/etc/rc.conf`:

```
DAEMONS=(... httpd ...)

```

**nebo** přidejte následující řádku do `rc.local`:

```
/etc/rc.d/httpd start

```

*   Pokud chcete, aby uživatelské adresáře (třeba `~/public_html` v počítači byly přístupné z internetu jako `[http://localhost/~user/](http://localhost/~user/)`, odkomentujte následující řádky v `/etc/httpd/conf/extra/httpd-userdir.conf`:

```
UserDir public_html

```

a

```
<Directory /home/*/public_html>
  AllowOverride FileInfo AuthConfig Limit Indexes
  Options MultiViews Indexes SymLinksIfOwnerMatch ExecCGI
  <Limit GET POST OPTIONS PROPFIND>
    Order allow,deny
    Allow from all
  </Limit>
  <LimitExcept GET POST OPTIONS PROPFIND>
    Order deny,allow
    Deny from all
  </LimitExcept>
</Directory>

```

Nezapomeňte, že váš domovský adresář musí mít správná přístupová práva, aby se tam Apache dostal. Vaše domovská složka a adresář `~/public_html` musejí být přísupné pro ostatní ("pro zbytek světa"). Tohle by mělo stačit:

```
$ chmod o+x ~
$ chmod o+x ~/public_html

```

#### Konfigurace PHP4 & PHP5

PHP je dostupné prakticky hned:

*   Vložte tyto řádky do `/etc/httpd/conf/httpd.conf`:

	Vložte tento řádek do seznamu modulů, kamkoliv za `LoadModule dir_module modules/mod_dir.so`:

```
LoadModule php5_module modules/libphp5.so

```

	pro PHP4 jednoduše nahraďte 5 za 4

```
LoadModule php4_module modules/libphp4.so

```

	Vložte tento řádek na konec "Include" seznamu:

```
 Include conf/extra/php5_module.conf

```

*   Pro obsluhu souborů je už PHP5 nastaveno:

```
<IfModule mod_php5.c>
 DirectoryIndex index.php index.html
 AddType application/x-httpd-php .php
 AddType application/x-httpd-php-source .phps
</IfModule>

DirectoryIndex index.html index.html.var

```

	Nicméně PHP4 vyžaduje pár drobných změn:

```
#<IfModule mod_php5.c>
 DirectoryIndex index.php index.html index.html.var
 AddType application/x-httpd-php .php
 AddType application/x-httpd-php-source .phps
#</IfModule>

#DirectoryIndex index.html index.html.var

```

*   Pokud používáte PHP4 nebo PHP5 nezapomeňte přidat obsluhu pro .phtml, pokud ji potřebujete:

```
DirectoryIndex index.php index.phtml index.html

```

*   Pokud chcete používat libGD modul, odkomentujte v /etc/php.ini

```
;extension=gd.so

```

na

```
extension=gd.so

```

*   Restartujte Apache, aby se projevily změny (jako root):

```
# /etc/rc.d/httpd restart

```

*   Otestujte PHP jednoduchou, ale velmi informativní stránkou:

```
<html>
<head>
<title>Zkušební stránka PHP</title>
</head>

<body>
Toto je Arch Linux a PHP

<?php
  phpinfo();
?>
</p>
</body>
</html>

```

Uložte tento soubor jako `test.php` a zkopírujte ho do `/home/httpd/html/` nebo `~/public_html`. Také udělat skript spustitelným (`chmod a+x test.php`)

*   Test PHP:

```
 [http://localhost/test.php](http://localhost/test.php) nebo [http://localhost/~mujucet/test.php](http://localhost/~mujucet/test.php)

```

#### Nastavení podpory MySQL

Pokud chcete používat MySQL, proveďte následující kroky:

##### Intial Configuration

*   Odkomentujte náledující řádky v `/etc/php.ini` (ve starších systémech je to v `/usr/etc`) odstraněním znaku `;`</i> na začátku:

```
`;extension=mysql.so`

```

*   Pro nastavení spusťte `/etc/rc.d/mysqld start` jako **root** _**OR**_ proveďte následující kroky:
*   Vytvořte skupinu _mysql_

```
# groupadd -g 89 mysql

```

*   Přidejte uživatele _mysql_

```
# useradd -u 89 -g mysql -d /var/lib/mysql -s /bin/false mysql

```

*   Změňte přísupová práva adresáře s MySQL

```
# chown -R mysql:mysql /var/lib/mysql

```

*   Nainstalujte databázi. Pokud pouze chcete spouštět MySQL jako root, můžete vynechat přepínač --user a příkaz chown

```
# mysql_install_db --datadir=/var/lib/mysql --user=mysql
# chown -R mysql:mysql /var/lib/mysql

```

*   Spusťte `/etc/rc.d/mysqld start`.

##### Další konfigurace

*   Otestujte MySQL (jako root):

```
# mysql

```

*   Vytvořte administrátorské heslo pro MySQL (v terminálu, jako root):

```
# mysqladmin -u root password 'roots_password'

```

*   Přidejte `mysqld` do seznamu démonů v `/etc/rc.conf` (jako u httpd - viz výše)

*   Pro přihlášení do MySQL, napište (do terminálu, _hostname_ jako je nastavený v `/etc/hosts`)

```
# mysql -u root -h _hostname_ -p

```

*   Můžete přidat další uživatele s omezenými oprávněními úpravou tabulek nacházejících se v `mysql` databázi. Aby se změny projevily, je nutné vždy restartovat MySQL (`/etc/rc.d/mysqld restart` jako root). Nezapomeňte zkontrolovat tabulku `mysql/users`. Pokud obsahuje další položky pro roota a váš hostname bez uvedeného hesla, každý ze serveru může mít kompletní přístup k databází.

#### Instalace PHPMyAdmin

Pokud chcete k přístupu do databáze používat PHPMyAdmin, musíte provést tyto kroky:

*   Nainstalovat balíček

```
# pacman -S phpmyadmin

```

*   Vytvořte adresář pro nastavení:

```
# cd /home/httpd/html/phpMyAdmin/
# mkdir config
# chmod o+rw config

```

*   Pro vytvoření konfiguračního adresáře jděte na:

```
[http://localhost/phpMyAdmin/scripts/setup.php](http://localhost/phpMyAdmin/scripts/setup.php)

```

*   Přidejte alespoň jeden server v sekci "Servers". Pro autentifikaci použijte "cookie", které umožní přihlašování přes webové rozhraní.
*   Uložte nastavení přes webové rozhraní v sekci "Configuration".

*   Pro použití nastavení přesuňte soubor config.inc.php do kořenového adresáře phpMyAdmina:

```
# mv config/config.inc.php config.inc.php

```

*   phpMyAdmin se nachází zde: [http://localhost/phpMyAdmin/](http://localhost/phpMyAdmin/)

*   Pro zjednodušení můžete vytvořit link, který je malými písmeny:

```
# cd /home/httpd/html
# ln -sv phpMyAdmin phpmyadmin

```

#### externi odkazy

*   `[http://cihan.me/installing-sugarcrm-community-edition-on-arch-linux/](http://cihan.me/installing-sugarcrm-community-edition-on-arch-linux/)`