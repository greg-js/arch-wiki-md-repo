[proFtpd](http://proftpd.org/) (Pro FTP daemon) jest wysoce funkcjonalnym serwerem FTP, odsłaniającym dużą liczbę opcji konfiguracyjnych dla użytkownika.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
    *   [2.1 Dostęp anonimowy](#Dost.C4.99p_anonimowy)
*   [3 Zobacz również](#Zobacz_r.C3.B3wnie.C5.BC)

## Instalacja

[proftpd](https://aur.archlinux.org/packages/proftpd/) jest dostępny w AUR. [Włącz](https://wiki.archlinux.org/index.php/Systemd#Using_units) i uruchom `proftpd.service`.

## Konfiguracja

[Plik konfiguracyjny](http://www.proftpd.org/docs/howto/ConfigFile.html) jest dostępny w `/etc/proftpd.conf`. Strona internetowa projektu zawiera obszerną [dokumentacje](http://www.proftpd.org/docs/).

### Dostęp anonimowy

Aby naprawić powszechny problem, żeby anonimowy dostęp do pracy działał z `/bin/false` jako powłoką dla użytkownika ftp (domyślna konfiguracja), musisz dodać linię `RequireValidShell off` do `/etc/proftpd.conf`. W przeciwnym razie anonimowe logowania otrzymają błąd 530.

## Zobacz również

*   [BLFS: ProFTPD](http://www.linuxfromscratch.org/blfs/view/7.6/server/proftpd.html)