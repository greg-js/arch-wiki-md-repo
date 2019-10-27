<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Úvod](#Úvod)
*   [2 Instalace](#Instalace)
*   [3 Nastavení](#Nastavení)
*   [4 Používání XAMPP](#Používání_XAMPP)
*   [5 Odinstalace XAMPP](#Odinstalace_XAMPP)
*   [6 Soubory mimo defaultní adresář htdocs](#Soubory_mimo_defaultní_adresář_htdocs)
*   [7 Odkazy](#Odkazy)

# Úvod

XAMPP je balíček, který obsahuje: Apache, MySQL, PHP & PEAR, Perl, ProFTPD, phpMyAdmin, OpenSSL, GD, Freetype2, libjpeg, libpng, gdbm, zlib, expat, Sablotron, libxml, Ming, Webalizer, pdf class, ncurses, mod_perl, FreeTDS, gettext, mcrypt, mhash, eAccelerator, SQLite a IMAP C-Client.

# Instalace

*   [xampp](https://aur.archlinux.org/packages/xampp/) v repozitáři [AUR](/index.php/AUR "AUR")
*   Pokud nechcete stahovat z AURu, postupujte takto:

1.  Stáhněte si aktuální verzi [odsud](http://www.apachefriends.org/en/xampp-linux.html#374).
2.  Přesuňte se v terminálu do složky se staženým souborem a proveďte příkaz `sudo tar xvfz xampp-linux-*.tar.gz -C /opt` 

**UPOZORNĚNÍ:** Pokud používáte 64-bitový systém, musíte také nainstalovat balíčky <tt>lib32-glibc</tt> and <tt>lib32-gcc-libs</tt>.

 `sudo pacman -S lib32-glibc lib32-gcc-libs` 

# Nastavení

Nastavení jednotlivých částí lze provést v následujících souborech.

**/opt/lampp/etc/httpd.conf** - konfigurační soubor Apache. Lze například změnit nastavení uložiště pro zdrojové soubory webových stránek.

**/opt/lampp/etc/php.ini** - konfigurační soubor pro nastavení php

**/opt/lampp/phpmyadmin/config.inc.php** - konfigurační soubor pro nastavení phpMyAdmin

**/opt/lampp/etc/proftpd.conf** - konfigurační soubor pro nastavení proFTP

**/opt/lampp/etc/my.cnf** - konfigurační soubor MySQL

Nastavení zabezpečení se provede jednoduchým příkazem:

 `sudo /opt/lampp/lampp security` 

Postupně budete poptávání pro zadání hesla pro přístup ke stránkám, uživatele pma pro phpMyAdmin, uživatele root pro MySQL a nastavení hesla uživatel nobody pro FTP.

# Používání XAMPP

Pro ovládání XAMPP jsou tyto příkazy:

 `sudo /opt/lampp/lampp {start,stop,restart}` 

# Odinstalace XAMPP

Všechny soubory potřebné k chodu XAMPP se nacházejí v adresáři **/opt/lampp**, pro odinstalaci je stačí smazat:

 `# rm -rf /opt/lampp` 

**UPOZORNĚNÍ:** Pokud jste si vytvořili symlinky, je potřeba je smazat také!

# Soubory mimo defaultní adresář htdocs

Defaultní adresář pro zdrojové soubory webových aplikací je zde: **/opt/lampp/htdocs/**.

K nastavení jiných adresářů si můžete nastavit tento alias:

1.  Upravte httpd.conf - např. takto: `nano /opt/lampp/etc/httpd.conf` 
2.  Přidejte alias do Alias sekce:

```
Alias /shortname /full_file_path
    <directory /full_file_path> 
        AllowOverride FileInfo Limit Options Indexes
        Order allow,deny
        Allow from all
    </directory>

```

Změny se projeví až po restartu:

 `/opt/lampp/lampp restart` 

Toto Vám umožní přistupovat i k souborům z jiných adresářů, ve výše uvedeném příkladu se na nastavený adresář dostanete přes **localhost/shortname**.

# Odkazy

*   [web XAMPP](http://www.apachefriends.org/en/xampp.html)