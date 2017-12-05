## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace](#Konfigurace)
    *   [2.1 Přídání blowfish tajného klíče](#P.C5.99.C3.ADd.C3.A1n.C3.AD_blowfish_tajn.C3.A9ho_kl.C3.AD.C4.8De)
*   [3 Přístup k phpMyAdmin](#P.C5.99.C3.ADstup_k_phpMyAdmin)
*   [4 Konfigurace Lighttpd](#Konfigurace_Lighttpd)
*   [5 Další (starší) informace](#Dal.C5.A1.C3.AD_.28star.C5.A1.C3.AD.29_informace)

## Instalace

Pro instalaci programu [phpMyAdmin](http://www.phpmyadmin.net/) nainstalujte balíček [phpmyadmin](https://www.archlinux.org/packages/?name=phpmyadmin) spuštěním:

```
# pacman -S phpmyadmin

```

## Konfigurace

Ujistěte se, že už phpMyAdmina v počítači nemáte, pokud ano, smažte ho.

```
# rm -r /srv/http/phpMyAdmin

```

Zkopírujte vzorový konfigurační soubor do svého httpd `conf` adresáře.

```
# cp /etc/webapps/phpmyadmin/apache.example.conf /etc/httpd/conf/extra/httpd-phpmyadmin.conf

```

Následující řádky přidejte do `/etc/httpd/conf/httpd.conf`:

```
# phpMyAdmin configuration
Include conf/extra/httpd-phpmyadmin.conf

```

V souboru `/usr/share/webapps/phpMyAdmin/.htaccess`, zakomentujte *deny from all*. Řádek by měl potom vypadat takto:

```
#deny from all

```

Pokud tak neuděláte, bude se vám při vstupu do adresáře s instalací phpMyAdmin zobrazovat chybová hláška "Error 403 - Access forbidden!".

Ve vašem souboru `/etc/httpd/conf/extra/httpd-phpmyadmin.conf` byste měli mít ještě toto:

```
       Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"
       <Directory "/usr/share/webapps/phpMyAdmin">
               AllowOverride All
               Options FollowSymlinks
               Order allow,deny
               Allow from all
       </Directory>

```

Otevřete soubor `/etc/php/php.ini`, běžte na řádek začínající na *open_basedir* a přidejte cestu ke složce s instalací phpMyAdmin následovně:

```
:/usr/share/webapps/:/etc/webapps/

```

Můj například obsahuje toto:

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/srv/:/usr/share/webapps/:/etc/webapps/

```

Dále budete potřebovat moduly mcrypt a mysql, proto odkomentujte tyto řádky v `/etc/php/php.ini`:

	z

```
 ;extension=mcrypt.so
 ;extension=mysql.so

```

	na

```
 extension=mcrypt.so
 extension=mysql.so

```

### Přídání blowfish tajného klíče

Pokud se vám zobrazuje následující chybová hláška ve spodní části stránky phpMyAdmina:

```
ERROR: The configuration file now needs a secret passphrase (blowfish_secret)

```

Je potřeba přidat tzv. blowfish heslo do konfiguračního souboru phpMyAdmina. Upravte `/etc/webapps/phpmyadmin/config.inc.php` a vložte náhodnou kombinaci znaků do pole **blowfish_secret**:

```
$cfg['blowfish_secret'] = *; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */*

```

Pokud si chcete svůj blowfish jednoduše vygenerovat, běžte na [generátor](http://www.question-defense.com/tools/phpmyadmin-blowfish-secret-generator). Potom ho už jen stačí vložit mezi znaky *. Mělo by to vypadat následovně:*

```
$cfg['blowfish_secret'] = 'qtdRoGmbc9{8IZr323xYcSN]0s)r$9b_JUnb{~Xz'; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */

```

Chybová hláška by se už po znovunačtení stránky ukazovat neměla.

## Přístup k phpMyAdmin

Vaše instalace phpMyAdmina by měla být kompletní. Než ho ale začnete používat, musíte ješte restartovat apache daemona:

```
# /etc/rc.d/httpd restart

```

Teď už jen ve svém prohlížeči zadejte tuto URL:

```
[http://localhost/phpmyadmin/](http://localhost/phpmyadmin/)

```

nebo

```
[http://localhost/phpmyadmin/index.php](http://localhost/phpmyadmin/index.php)

```

**Note:** 'localhost' je váš hostname (ze souboru `/etc/rc.conf`).

Pokud chcete ke svému phpMyAdminovi přistupovat bez zadání koncového lomítka v URL:

```
[http://localhost/phpmyadmin](http://localhost/phpmyadmin)

```

v souboru `/etc/httpd/conf/extra/httpd-phpmyadmin.conf` změňte:

```
Alias /phpmyadmin/ "/usr/share/webapps/phpMyAdmin/"

```

na

```
Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"

```

Můžete si také přečist [toto vlákno](https://bbs.archlinux.org/viewtopic.php?pid=632500).

Pokud dástáváte chybu "#2002 - The server is not responding (or the local MySQL server's socket is not correctly configured)", potom byste měli změnit hodnotu "localhost" ve svém `/etc/webapps/phpmyadmin/config.inc.php` na řádku:

```
$cfg['Servers'][$i]['host'] = 'localhost';

```

na váš hostname, který je definován v souborech /etc/hosts a /etc/rc.conf pod názvem proměnné HOSTNAME.

## Konfigurace Lighttpd

Nastavení pro lighttpd je úplně stejné jako pro apache. Vytvořte alias pro phpMyAdmina ve svém konfiguračním souborů pro lighttpd.

```
 alias.url = ( "/phpmyadmin/" => "/usr/share/webapps/phpMyAdmin/")

```

Potom v konfiguračním souboru zapněte mod_alias, mod_fastcgi a mod_cgi (v sekci server.modules).

Upravte open_basedir v souboru `/etc/php/php.ini` a přidejte do něj "/usr/share/webapps/".

```
 open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/usr/share/webapps/

```

Ujistěte se, že lighttpd je nastaveno tak, aby spouštělo soubory typu php. Více na [Lighttpd (Česky)](/index.php/Lighttpd_(%C4%8Cesky) "Lighttpd (Česky)").

Restartujte lighttpd a běžte v prohlížeči na adresu [http://localhost/phpmyadmin/index.php](http://localhost/phpmyadmin/index.php)

## Další (starší) informace

Zde najdete příklady konfigurace 'config.inc.php'.

**Věci, které byste měli udělat jako první**

Vytvořte uživatele 'controluser', aby phpMyAdmin mohl číst z mysql databáze.

```
# mysql -u root -pVASE_HESLO
# mysql> grant usage on mysql.* to controluser@localhost identified by 'CONTROLPASS';

```

**Kde je phpMyAdmin**

v phpMyAdmin verze 3.2.2-3 se nezobrazuje v /srv/http/, proto vytvořte symlink:

```
# ln -s /usr/share/webapps/phpMyAdmin/ /srv/http/phpmyadmin

```

**Věci, které byste měli změnit**

Proměnná *controluser* musí být nastavena na **controluser**
Proměnná *controlpass* musí být nastavena na **heslo**
Proměnná *verbose* je nastavena na jmeno_serveru

**Příklad konfiguračního souboru 'config.inc.php'**

```
<?php
/*
 * Generated configuration file
 * Generated by: phpMyAdmin 2.11.8.1 setup script by Michal Čihař <michal@cihar.com>
 * Version: $Id: setup.php 11423 2008-07-24 17:26:05Z lem9 $
 * Date: Mon, 01 Sep 2008 20:34:02 GMT
 */

/* Servers configuration */
$i = 0;

/* Server ravi-test-mysql (http) [1] */
$i++;
$cfg['Servers'][$i]['host'] = 'localhost';
$cfg['Servers'][$i]['extension'] = 'mysql';
$cfg['Servers'][$i]['port'] = '3306';
$cfg['Servers'][$i]['connect_type'] = 'tcp';
$cfg['Servers'][$i]['compress'] = false;
$cfg['Servers'][$i]['controluser'] = 'controluser';
$cfg['Servers'][$i]['controlpass'] = 'heslo';
$cfg['Servers'][$i]['auth_type'] = 'http';
$cfg['Servers'][$i]['verbose'] = 'jmeno_serveru';

/* End of servers configuration */

$cfg['LeftFrameLight'] = true;
$cfg['LeftFrameDBTree'] = true;
$cfg['LeftFrameDBSeparator'] = '_';
$cfg['LeftFrameTableSeparator'] = '__';
$cfg['LeftFrameTableLevel'] = 1;
$cfg['LeftDisplayLogo'] = true;
$cfg['LeftDisplayServers'] = false;
$cfg['DisplayServersList'] = false;
$cfg['DisplayDatabasesList'] = 'auto';
$cfg['LeftPointerEnable'] = true;
$cfg['DefaultTabServer'] = 'main.php';
$cfg['DefaultTabDatabase'] = 'db_structure.php';
$cfg['DefaultTabTable'] = 'tbl_structure.php';
$cfg['LightTabs'] = false;
$cfg['ErrorIconic'] = true;
$cfg['MainPageIconic'] = true;
$cfg['ReplaceHelpImg'] = true;
$cfg['NavigationBarIconic'] = 'both';
$cfg['PropertiesIconic'] = 'both';
$cfg['BrowsePointerEnable'] = true;
$cfg['BrowseMarkerEnable'] = true;
$cfg['ModifyDeleteAtRight'] = false;
$cfg['ModifyDeleteAtLeft'] = true;
$cfg['RepeatCells'] = 100;
$cfg['DefaultDisplay'] = 'horizontal';
$cfg['TextareaCols'] = 40;
$cfg['TextareaRows'] = 7;
$cfg['LongtextDoubleTextarea'] = true;
$cfg['TextareaAutoSelect'] = false;
$cfg['CharEditing'] = 'input';
$cfg['CharTextareaCols'] = 40;
$cfg['CharTextareaRows'] = 2;
$cfg['CtrlArrowsMoving'] = true;
$cfg['DefaultPropDisplay'] = 'horizontal';
$cfg['InsertRows'] = 2;
$cfg['EditInWindow'] = true;
$cfg['QueryWindowHeight'] = 310;
$cfg['QueryWindowWidth'] = 550;
$cfg['QueryWindowDefTab'] = 'sql';
$cfg['ForceSSL'] = false;
$cfg['ShowPhpInfo'] = false;
$cfg['ShowChgPassword'] = false;
$cfg['AllowArbitraryServer'] = false;
$cfg['LoginCookieRecall'] = 'something';
$cfg['LoginCookieValidity'] = 1800;
?>

```