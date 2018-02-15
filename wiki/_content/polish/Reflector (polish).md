Related articles

*   [Mirrors](/index.php/Mirrors "Mirrors")
*   [Pacman (Polski)](/index.php/Pacman_(Polski) "Pacman (Polski)")

[Reflector](http://xyne.archlinux.ca/projects/reflector/) to skrypt, który pobriera najnowszą listę mirrorów ze strony [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtruje najbardziej aktualne mirrory, sortuje je według szybkości i zastąpia plik `/etc/pacman.d/mirrorlist`.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Użycie](#U.C5.BCycie)
    *   [2.1 Przykłady](#Przyk.C5.82ady)
    *   [2.2 Systemd Service](#Systemd_Service)
    *   [2.3 Systemd Timer](#Systemd_Timer)
        *   [2.3.1 Pakiet AUR](#Pakiet_AUR)

## Instalacja

[Zainstaluj](/index.php/Install "Install") pakiet [reflector](https://www.archlinux.org/packages/?name=reflector).

## Użycie

**Warning:**

*   W poniższych przykładach, `/etc/pacman.d/mirrorlist` zostanie nadpisany. Zrób kopię zapasową przed kontynuowaniem.
*   Upewnij się, że powstały `/etc/pacman.d/mirrorlist` nie zawierają wpisów, które uważasz za niewiarygodne przed synchronizacją lub aktualizacją za pomocą [Pacmana](/index.php/Pacman "Pacman").

Aby zobaczyć dostępne polecenia, uruchom następujące polecenie:

```
# reflector --help

```

### Przykłady

Dokładnie oceń i posortuj pięć ostatnio zsynchronizowanych mirrorów przez prędkość pobierania i zastąpia plik `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose --latest 5 --sort rate --save /etc/pacman.d/mirrorlist

```

Wybierz 200 ostatnio zsynchronizowanych mirrorów HTTP lub HTTPS, posortuj je według prędkości pobierania i zastąpia plik `/etc/pacman.d/mirrorlist`:

```
# reflector --latest 200 --protocol http --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

Wybierz mirrory HTTPS zsynchronizowane w ciągu ostatnich 12 godzin oraz umieszczonych w USA, sortuje je według prędkości pobierania i zastąpia plik `/etc/pacman.d/mirrorlist`:

```
# reflector --country 'United States' --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

### Systemd Service

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

```

Następne [uruchomienie](/index.php/Start "Start") `reflector.service` zaktualizuje twoją listę mirrorów.

Aby zaktualizować listę mirrorów przy każdym uruchomieniu komputera, możesz włączyć następującą definicję usługi.

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update
Requires=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

[Install]
RequiredBy=multi-user.target

```

Upewnij się, że [aktywowałeś odpowiednie usługi](http://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/), aby `network.target` rzeczywiście odzwierciedlało twój stan sieci.

### Systemd Timer

Jeśli chcesz uruchamiać `reflector.service` co tydzień:

 `/etc/systemd/system/reflector.timer` 
```
[Unit]
Description=Run reflector weekly

[Timer]
OnCalendar=weekly
RandomizedDelaySec=12h
Persistent=true

[Install]
WantedBy=timers.target

```

A potem [uruchom](/index.php/Start "Start") `reflector.timer`.

#### Pakiet AUR

[Zainstaluj](/index.php/Install "Install") pakiet [reflector-timer](https://aur.archlinux.org/packages/reflector-timer/) aby uruchamiać *reflector* tygodniowo.

Domyślna konfiguracja to:

 `/usr/share/reflector-timer/reflector.conf` 
```
AGE=6
COUNTRY=Germany
LATEST=30
NUMBER=20
SORT=rate

```

Aby nadpisać tę konfigurację, zedytuj `/etc/conf.d/reflector.conf`:

 `/etc/conf.d/reflector.conf` 
```
COUNTRY=US

```

Upewnij się, że [włączyłeś](/index.php/Enable "Enable") `reflector.timer`.