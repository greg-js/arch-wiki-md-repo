## Contents

*   [1 Uvod](#Uvod)
*   [2 Instalacija](#Instalacija)
    *   [2.1 Instaliranje Drupal-a](#Instaliranje_Drupal-a)
        *   [2.1.1 iz Arch repozitorijuma](#iz_Arch_repozitorijuma)
        *   [2.1.2 rucna instalacija](#rucna_instalacija)
    *   [2.2 Instaliranje GD-a](#Instaliranje_GD-a)
    *   [2.3 Instalacija Postfix-a](#Instalacija_Postfix-a)
*   [3 Saveti i trikovi](#Saveti_i_trikovi)
    *   [3.1 Zakazivanje preko Cron-a](#Zakazivanje_preko_Cron-a)
    *   [3.2 Xampp kompatibilnost](#Xampp_kompatibilnost)
*   [4 Resavanje problema](#Resavanje_problema)
    *   [4.1 Pretrazivac prikazuje trenutni PHP kod kada posecujete localhost](#Pretrazivac_prikazuje_trenutni_PHP_kod_kada_posecujete_localhost)
    *   [4.2 Drupalova stranica za podesavanje nije pocetna stranica kada pristupate localhost-u](#Drupalova_stranica_za_podesavanje_nije_pocetna_stranica_kada_pristupate_localhost-u)
    *   [4.3 Drupal-ova stranica za podesavanje ne startuje i pokazuje HTTP ERROR 500](#Drupal-ova_stranica_za_podesavanje_ne_startuje_i_pokazuje_HTTP_ERROR_500)
*   [5 Vise izvora](#Vise_izvora)

## Uvod

Ovaj dokument opisuje kako da podesite Drupal (6.x) sa Apach-om, MySQL-om ili PostgreSQL, PHP-om, i Postfix-om! Ovaj dokument pretpostavlja da imate neku vrstu [LAMP](/index.php/LAMP "LAMP")-a (Apache-a, MySQL-a, PHP-a) ili LAPP (Apache, PostgreSQL, PHP) servera vec podesenog.

## Instalacija

### Instaliranje Drupal-a

#### iz Arch repozitorijuma

*   [Drupal paket](https://www.archlinux.org/packages/community/any/drupal/) u [community](/index.php/Community "Community")

 `pacman -S drupal` 

1.  Otvorite fajl **`/etc/php/php.ini`** sa editorom vaseg izbora, npr. `# nano /etc/php/php.ini` 
2.  Nadjite liniju koja startuje sa, ";extension=json.so" i promenite je u, "extension=json.so". (Uklonite prefiks ";"). Ako ova linija ne postoji, dodajte je. Ova linija moze biti u "Dynamic Extensions" sekciji fajla ili na samom kraju fajla.
3.  Nadjite deo koji pocinje sa " <Directory "/srv/http">" ili sa direktorijumom u koji ste instalirali drupal. U tom odeljku cete naci liniju sa "AllowOverride None" i zamenite je sa "AllowOverride All", sto ce omoguciti ciste URL-ove
4.  Restartujte Apache web server `/etc/rc.d/httpd restart` 

NOTE: U verziji drupal-a koji sam preuzeo iz community repozitorijuma, primetio sam da je prva linija .htaccess fajla podesena na 'deny from all' nasuprot .htaccess fajlu iz drupal.org-a. Ovo onemogucava pristup drupal direktorijumu tako da niste u mogucnosti da aktivirate drupal. Dekomentovanje ove linije resava problem.

#### rucna instalacija

1.  Preuzmite najskoriji paket sa [http://drupal.org](http://drupal.org) i otpakujte ga.
2.  Premestite direktorijume u apache-ov htdocs direktorijum.
3.  Otvorite web pretrazivac i pozicionirajte se na "localhost"
4.  Pratite instrukcije na ekranu.

### Instaliranje GD-a

Mozda ce vam trebati GD biblioteka za vasu Drupal instalaciju.

1.  Instalirajte paket
     `# pacman -S php-gd` 
2.  Otvorite fajl **`/etc/php/php.ini`** sa vasim editorom izbora, npr. `# nano /etc/php/php.ini` 
3.  Nadjite liniju koja startuje sa, ";extension=gd.so" i promenite je u, "extension=gd.so". (Jednostavno uklonite prefiks ";"). Ako ova linija ne postoji, dodajte je. Ova linija moze biti u "Dynamic Extensions" odeljku fajla ili pri kraju fajla.
4.  Restartujte Apache web server `/etc/rc.d/httpd restart` 

### Instalacija Postfix-a

Da saljete e-mail-ove sa Drupal-om, morate da instalirate postfix. Drupal koristi e-mail-ove za verifikaciju naloga, resetovanje lozinki, itd...

1.  Instalirajte Postfix `# pacman -S postfix ` 
2.  Podesite Postfix po potrebi `# nano /etc/postfix/main.cf ` Sve sto treba da uradite je da promenite hostnames pod "Internet Host and Domain Names" ` myhostname = hostname1 ` 
    A zatim da startujete Postfix servis: `# /etc/rc.d/postfix start` 
3.  Posaljite test e-mail sebi ` mail vasekorisnickoime@localhost ` (Unesite temu, neke reci u telo, a zatim pritisnite ctrl+d da izadjete i posaljete pismo). Sacekajte 10 sekundi, a zatim ukucajte `mail` da proverite vas mejl. Ako ste ga primili, odlicno.
4.  Uverite se da je port 25 predupredjen, ako imate ruter, da bi mejlovi mogli da se salju i po internetu.
5.  Otvorite fajl **`/etc/php/php.ini`** sa vasim editorom izbora, npr. `# nano /etc/php/php.ini` 
6.  Nadjite liniju koja startuje sa, **`;sendmail_path=""` **i promenite je u, **`sendmail_path="/usr/sbin/sendmail -t -i"`**
7.  Restartujte Apache web server `/etc/rc.d/httpd restart` 

## Saveti i trikovi

### Zakazivanje preko Cron-a

Drupal preporucuje izvrsavanje cron poslova na svaki sat. Cron se moze izvrsiti iz browser-a posetom **`localhost/cron`** Takodje je moguce izvrsiti cron preko skripti tako sto cete kopirati odgovarajuci fajl iz "scripts" direktorijuma u "/etc/cron.hourly" i podesiti ga da bude izvrsan.

### Xampp kompatibilnost

5.x i 6.x serije Drupal-a ne podrzavaju PHP 5.3 i kao rezultat su nekompatibilne sa zadnjim verzijama [Xampp](/index.php/Xampp "Xampp")-a. Trenutno, zadnja Drupal-kompatibilna verzija Xampp-a je 1.7.1.

Note: Xampp-ov PHP memorijski limit je trenutno po difoltu 8MB. Takodje, Xampp ignorise php.ini fajlove u Drupal direktorijumu. Da ispravite ovo:

1.  izmenite Xampp-ov php.ini fajl upotrebom omiljenog editora. `nano /opt/lampp/etc/php.ini` 
2.  Pretrazite za "memory_limit" liniju i zamenite je sa odgovarajucom vrednoscu. (Vecina Drupal instalacija rade kako treba sa 32M, ali sajtovi sa dosta modula mogu zahtevati 100M ili vise.)
3.  Restartujte Xampp. `/opt/lampp/lampp restart` 

## Resavanje problema

### Pretrazivac prikazuje trenutni PHP kod kada posecujete localhost

Mogu postojati dva razloga zasto se ovo desava.

Prvi - mozda nemate php-apache instaliran.

Drugi - kada startujete httpd, dobijate gresku poput ove:

 `httpd: Ne moze pouzdano da utvrdi kvalifikovano ime domena servera, koristeci 127.0.0.1 za ServerName` 

Da popravite to, editujte httpd.conf sa

 `# nano /etc/httpd/conf/httpd.conf` 

U tom fajlu pronadjite liniju koja izgleda slicno kao

 `#ServerName www.example.com:80` i dekomentujte je (uklonite # sa pocetka linije). Restartujte httpd sa `# /etc/rc.d/httpd restart` i spremni ste da nastavite dalje!

### Drupalova stranica za podesavanje nije pocetna stranica kada pristupate localhost-u

U ovoj situaciji, trebalo bi da se pozicionirate u vasem /srv direktorijumu i potrazite drupal-ov direktorijum (najverovatnije ce biti u http direktorijumu). Zatim editujte httpd.conf sa

 `# nano /etc/httpd/conf/httpd.conf` i potrazite liniju koja startuje sa `DocumentRoot` i promenite stazu sa stazom tog direktorijuma (za mene to izgleda kao DocumentRoot "/srv/http/drupal") i takodje nadjite drugu liniju koja pocinje sa `<Directory` i podesite istu stazu i na tom mestu. Restartujte httpd sa `# /etc/rc.d/httpd restart` i to je to.

### Drupal-ova stranica za podesavanje ne startuje i pokazuje HTTP ERROR 500

Ovo moze biti slucaj jer drupal zahteva da //json// bude aktiviran u vasem php.ini. jednostavno dekomentujte liniju `;extension=json.so` sa `/etc/php/php.ini` brisanjem pocetnog ';' i restartovanjem httpd servisa kucanjem `/etc/rc.d/httpd restart`. (pogledajte [ovaj link](http://drupal.org/node/1018824) za informacije.)

## Vise izvora

*   [Oficijalna Drupal dokumentacija](http://drupal.org/handbook)
*   [Jednostavno uputstvo za instalaciju Drupal-a na Xampp](http://drupal.org/node/307956)
*   [LAMP (Kako da podesite apache server)](https://wiki.archlinux.org/index.php/LAMP)