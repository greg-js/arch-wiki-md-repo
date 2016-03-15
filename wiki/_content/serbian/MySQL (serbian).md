MySQL jе siroko rasprostranjena SQL baza podataka koja ima vise niti i namenjena je za vise korisnika. Za vise informacija o funkcijama pogledajte [oficijalnu home stranicu](http://www.mysql.com/).

## Contents

*   [1 Instalacija](#Instalacija)
*   [2 Konfigurisanje](#Konfigurisanje)
    *   [2.1 Omogucite udaljeni pristup](#Omogucite_udaljeni_pristup)
*   [3 Osvezavanje](#Osvezavanje)
*   [4 Resavanje problema](#Resavanje_problema)
    *   [4.1 Mysql daemon ne moze da startuje](#Mysql_daemon_ne_moze_da_startuje)
    *   [4.2 Nije moguce pokrenuti mysql_upgrade jer MySQL ne moze da startuje.](#Nije_moguce_pokrenuti_mysql_upgrade_jer_MySQL_ne_moze_da_startuje.)
    *   [4.3 Kako da resetujete Root sifru](#Kako_da_resetujete_Root_sifru)
*   [5 Vise izvora](#Vise_izvora)

## Instalacija

Instalirajte [mysql](https://aur.archlinux.org/packages/mysql/) paket.

Nakon instalacije MySQL-a pokrenite skriptu za podesavanje kao root:

```
# /etc/rc.d/mysqld start && mysql_secure_installation

```

Zatim restartujte MySQL:

```
# /etc/rc.d/mysqld restart

```

Da startujete MySQL automatski prilikom startovanja, editujte `/etc/rc.conf` i dodajte `mysqld` daemon:

```
DAEMONS=(... mysqld ...)

```

## Konfigurisanje

Kada ste startovali MySQL server, verovatno cete zeleti da dodate root nalog kako bi ste mogli da odrzavate Vase MySQL korisnike i baze. Ovo se moze uraditi rucno ili automatski, kao sto je napomenuto u izlazu gornje skripte. Ili izvrsite komande da podesite sifru za root nalog, ili izvrsite sigurnosnu instalacionu skriptu.

Sada bi trebalo da mozete da nastavite sa daljim konfigurisanjem preko Vaseg omiljenog interfejsa. Naprimer, mozete da koristite MySQL-ovu komandnu liniju za prijavljivanje kao root na Vas MySQL server:

```
$ mysql -p -u root

```

Da startujete MySQL prilikom startovanja dodajte `mysqld` u listu daemona u `/etc/rc.conf`.

### Omogucite udaljeni pristup

MySQL server ne slusa na TCP portu 3306 po difoltu. Da dozvolite (udaljene) TCP konekcije, stavite pod komentar sledecu liniju u `/etc/mysql/my.cnf`:

```
skip-networking

```

Zapamtite da izmenite `/etc/hosts.allow` dodavanjem sledecih linija:

```
mysqld: ALL : ALLOW
mysqld-max: ALL : ALLOW

```

## Osvezavanje

Pozeljno je izvrsiti ovu komandu nakon sto ste osvezili MySQL i startovali ga:

```
# mysql_upgrade -u root -p

```

## Resavanje problema

### Mysql daemon ne moze da startuje

Ako vidite nesto poput ovoga:

```
 # /etc/rc.d/mysqld restart
 :: Stopping MySQL  [FAIL] 
 :: Starting MySQL  [FAIL]

```

i nema unosa u log fajlovima, proverite dozvole fajlova u direktorijumima `/var/lib/mysql` i `/var/lib/mysql/mysql`. Ako vlasnik fajlova u ovim direktorijumima nije mysql:mysql, uradite sledece:

```
 # chown mysql:mysql /var/lib/mysql -R

```

Ako imate problema sa dozvolama uprkos sto ste pratili gornje uputstvo, uverite se da je Vas `my.cnf` kopiran u /etc/:

```
 # cp /etc/mysql/my.cnf /etc/my.cnf

```

Sada restartujte daemon.

Ako dobijete sledece poruke u Vasem `/var/lib/mysql/hostname.err`

```
 [ERROR] Can't start server : Bind on unix socket: Permission denied
 [ERROR] Do you already have another mysqld server running on socket: /var/run/mysqld/mysqld.sock ?
 [ERROR] Aborting

```

proverite dozvole od `/var/run/mysqld` na sledeci nacin:

```
 # chown mysql:mysql /var/run/mysqld -R

```

Ako pokrecete mysqld i slececa greska se pojavljuje:

```
 Fatal error: Can’t open and lock privilege tables: Table ‘mysql.host’ doesn’t exist

```

Izvrsite sledecu komandu da instalirate difolt tabele:

```
 # mysql_install_db --user=mysql --ldata=/var/lib/mysql/

```

### Nije moguce pokrenuti mysql_upgrade jer MySQL ne moze da startuje.

Pokusajte da izvrsite MySQL u safemode-u

```
# mysqld_safe --datadir=/var/lib/mysql/

```

I zatim izvrsite:

```
# mysql_upgrade -u root -p

```

### Kako da resetujete Root sifru

Zaustavite mysqld daemon

```
# /etc/rc.d/mysqld stop
# mysqld_safe --skip-grant-tables &

```

Konektujte se na mysql server

```
# mysql -u root mysql

```

Promenite root sifru:

```
 mysql> UPDATE user SET password=PASSWORD("NEW_PASSWORD") WHERE User='root';
 mysql> FLUSH PRIVILEGES;
 mysql> exit

```

Zatim restartujte daemon:

```
# /etc/rc.d/mysqld restart

```

To bi trebalo da je to

## Vise izvora

*   [LAMP (Српски)](/index.php/LAMP_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "LAMP (Српски)") - Arch wiki clanak koji pokriva podesavanje LAMP servera (Linux Apache MySQL PHP)
*   [http://www.mysql.com/](http://www.mysql.com/)
*   Front-end [mysql-gui-tools](https://aur.archlinux.org/packages/mysql-gui-tools/) [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench)