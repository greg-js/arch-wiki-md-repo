## Wstęp

Z tego artykułu dowiesz się jak zainstalować oraz wstępnie skonfigurować serwer apache bazę danych [MYSQL](/index.php?title=MYSQL&action=edit&redlink=1 "MYSQL (page does not exist)") i środowisko [PHP](/index.php/PHP "PHP") .

Jeśli potrzebujesz serwer środowisko do prowadzenia testów polecam prostsze rozwiązanie jakim jest [Xampp](/index.php/Xampp "Xampp")

## Instalacja

Najprostszym sposobem instalacji a zarazem najszybszym będzię użycie użycie zasobów repozytorium

```
# pacman -S apache php php-apache mysql

```

## Konfiguracja APACHE

Tworzymy nowego użytkownika przypisujemy mu katalog /srv/http/

```
# useradd -d /srv/http -r -s /bin/false -U http

```

	Dzięki tej komendzie utworzyliśmy użytkownika http jako katalog przypisaliśmy mu ścieżkę do folderu /srv/http/ i dodaliśmy go do grupy o nazwie również http:

	Edytujemy plik hosts ; vim/etc/hosts

```
127.0.0.1 localhost.localdomain localhost

```

	Jeżeli chcemy ustawić naszą własną uroczą nazwę hosta dopisujemy sowoją nazwę w pole myhostanem

```
127.0.0.1 localhost.localdomain localhost myhostname

```

Następnie edytujemy plik rc.d jeżeli ustawiliśmy nazwę hostna na localhost równiez do zmieniej Hostname przypisujemy localhost

vim /etc/rc.d

```
#
# Networking
#
HOSTNAME="localhost"

```

Aby uruchomić serwer http

```
 /etc/rc.d/httpd start

```

Aby serwer http uruchamiał się automatycznie należy dopisąc go do demona w rc.conf

vim /etc/rc.conf

```
DAEMONS = ( ... httpd .... )

```

lub należy dopisac linijkę do pliku starotwego rc.local

```
vim /etc/rc.local
/etc/rc.d/httpd start

```

...