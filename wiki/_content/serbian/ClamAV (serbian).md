[Clam AntiVirus](http://www.clamav.net) je open source (GPL) anti-virus alat za UNIX. On pruža brojne alate uključujući fleksibilan i prilagodljivi daemon, Vrši skeniranje preko komandne linije,i napredni alat za automatsko ažuriranja baze podataka. Zbog toga ClamAV's glavna upotreba je na file/mail serverima za Windows i desktop računarima na kojima prvenstveno otkriva viruse i malware.

## Contents

*   [1 Instalacija](#Instalacija)
*   [2 Konfiguracija](#Konfiguracija)
*   [3 Ažuriranje baze podataka](#A.C5.BEuriranje_baze_podataka)
*   [4 Postavke Servera](#Postavke_Servera)
*   [5 Skeniranje virusa](#Skeniranje_virusa)
*   [6 Rešavanje problema](#Re.C5.A1avanje_problema)

## Instalacija

Instalirajte ClamAV sa sledećom komandom:

```
# pacman -S clamav

```

## Konfiguracija

Bilo da koristitw clamav kao daemon ili da ga koristite za povremeno proveravanje datoteka potrebno je da zakomentarišete (postavite tarabu #) na reč *Example*, koja se nalazi na početku fajla `/etc/clamav/freshclam.conf` Verovatno će biti potrebno da se isto uradi i kod `clamd.conf` koji se nalazi u istom direktorijumu, zatim kada ste ovo uradili možete da ažurirate bazu podataka za viruse.

## Ažuriranje baze podataka

Potrebno je pokrenuti ClamAV daemon da bi se mogla pokrenut baza podataka za viruse:

```
# /etc/rc.d/clamav start

```

Zatim ažurirajte bazu podataka za nove viruse:

```
# freshclam

```

Baza podataka je sačuvana ovde:

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd

```

## Postavke Servera

Da biste pokrenuli kao server uredite sledeće `/etc/clamav/clamd.conf` i `/etc/clamav/freshclam.conf` and comment out the *Example* flag. In `/etc/conf.d/clamav` promenite start opciju iz "no" u "yes".

```
# change these to "yes" to start
START_FRESHCLAM="yes"
START_CLAMD="yes"

```

*   Da se pokrene ClamAV tokom pokretanja računara uredite `/etc/rc.conf` i dodajte clamav.

## Skeniranje virusa

`clamscan` može da se koristi kod određenog fajla, home direktorijuma, ili celog sistema:

```
$ clamscan myfile
$ clamscan -r -i /home
$ clamscan -r -i --exclude-dir=^/sys\|^/proc\|^/dev /

```

Ako želite `clamscan` da uklonite zaraženu datoteku dodajte `--remove` opciju kao komandu.

## Rešavanje problema

Ako dobijete sledeću poruku nakon pokretanja freshclam:

```
WARNING: Clamd was NOT notified: Can't connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

Dodajte sock datoteku za clamav:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

Zatim, promenite /etc/clamav/clamd.conf

```
Uklonite komentar sa sledće linije: #LocalSocket /var/lib/clamav/clamd.sock

```

Sačuvajte datoteku i resetujte daemon (/etc/rc.d/clamav stop; /etc/rc.d/clamav start)

Ako dobijete sledeću grešku prilikom pokretanja daemona:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

Pokrenite freshclam kao root:

```
# freshclam -v

```

Ako se dobili:

```
# can't create temporary directory

```

error, along with a 'HINT' containing a UID and a GID number.

Uradite sledeće:

```
# chown UID:GID /var/lib/clamav & chmod 755 /var/lib/clamav 

```

```
# ex: chown 64:64

```