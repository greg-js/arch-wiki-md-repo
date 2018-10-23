Related articles

*   [Flatpak](/index.php/Flatpak "Flatpak")

*[Snap](https://snapcraft.io/)* to system wdrażania oprogramowania i zarządzania pakietami. Pakiety nazywają się "snapami", a narzędziem do ich używania jest snapd, który działa w [wielu dystrybucjach GNU/Linuxa](https://docs.snapcraft.io/installing-snapd/6735) i umożliwia w ten sposób proste wdrażanie oprogramowania niezależnie od dystrybucji. Snap został pierwotnie zaprojektowany i stworzony przez Canonical.

[snapd](https://github.com/snapcore/snapd) jest demonem REST API dla zarządzania pakietami snap. Użytkownicy mogą zarządzać nim korzystając z klienta *snap*, który jest częścią tego samego pakietu.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
*   [3 Użycie](#U.C5.BCycie)
    *   [3.1 Wyszukiwanie](#Wyszukiwanie)
    *   [3.2 Instalowanie](#Instalowanie)
    *   [3.3 Aktualizowanie](#Aktualizowanie)
    *   [3.4 Usuwanie](#Usuwanie)
*   [4 Wskazówki i porady](#Wskaz.C3.B3wki_i_porady)
    *   [4.1 Klasyczne snapy](#Klasyczne_snapy)
*   [5 Wsparcie](#Wsparcie)
*   [6 Zobacz również](#Zobacz_r.C3.B3wnie.C5.BC)

## Instalacja

[Zainstaluj](https://wiki.archlinux.org/index.php/Help:Reading#Installation_of_packages) [snapd](https://aur.archlinux.org/packages/snapd/) lub pakiet [snapd-git](https://aur.archlinux.org/packages/snapd-git/).

**Tip:** `snapd` instaluje skrypt `/etc/profile.d/snapd.sh` żeby wyeksportować ścieżki plików binarnych zainstalowanych z pakietem snapd. Uruchom ponownie komputer, aby zmiana zaczęła obowiązywać.

## Konfiguracja

Aby uruchomić demona `snapd`, gdy *snap* spróbuje go użyć, [uruchom](https://wiki.archlinux.org/index.php/Systemd#Using_units) i/lub [włącz](https://wiki.archlinux.org/index.php/Systemd#Using_units) `snapd.socket`.

## Użycie

Narzędzie *snap* służy do zarządzania snapami.

### Wyszukiwanie

Aby znaleźć snapy do zainstalowania, możesz wyszukać je w sklepie Snap:

```
$ snap find *szukany termin*

```

### Instalowanie

Po znalezieniu szukanego snapa możesz go zainstalować za pomocą:

```
# snap install *nazwa-snapa*

```

Wymaga to uprawnień root'a. Instalacja snapów dla tylko jednego użytkownika nie jest jeszcze możliwa. Spowoduje to pobranie snapa do `/var/lib/snapd/snaps` i zainstalowanie go w `/var/lib/snapd/snap/*nazwa-snapa*`, aby udostępnić je systemowi.

Utworzy także jednostki montowania dla każdego snapa i doda je do `/etc/systemd/system/multi-user.target.wants/` jako linki symbolizczne, aby wszystkie snapy były dostępne po uruchomieniu systemu. Gdy to zrobisz, powinieneś znaleźć go na liście zainstalowanych snapów wraz z numerem wersji, wersją i deweloperem używając:

```
$ snap list

```

Możesz również zainstalować snapy z lokalnego dysku za pomocą:

```
# snap install --dangerous */ścieżka/do/snapa*

```

### Aktualizowanie

Żeby zaktualizować swoje snapy ręcznie wpisz:

```
# snap refresh

```

Snapy są automatycznie odświeżane zgodnie z ustawieniem snap `refresh.timer`.

Żeby zobaczyć ostatnie odświeżenie użyj:

```
# snap refresh --time

```

Żeby ustawić inny czas odświeżania, np. 2 razy w ciągu dnia:

```
# snap set core refresh.timer=0:00~24:00/2

```

Zobacz [strone dokumentacji](https://forum.snapcraft.io/t/system-options/87) dla więcej informacji o zmienianiu czasu odświeżania.

### Usuwanie

Snapy mogą być usunięte poprzez wpisanie tej komendy:

```
# snap remove *nazwa_snapa*

```

## Wskazówki i porady

### Klasyczne snapy

Niektóre snapy (np. Skype i Pycharm) używają klasycznego ograniczenia. Jednak klasyczne ograniczenie wymaga katalogu `/snap`, który nie jest zgodny z FHS. Dlatego pakiet snapd nie jest dostarczany z tym katalogiem. Jednakże, jeśli użytkownik tego chce, może ręcznie utworzyć link symboliczny z `/snap` do `/var/lib/snapd/snap`, aby umożliwić instalację klasycznych snapów:

```
# ln -s /var/lib/snapd/snap /snap

```

## Wsparcie

Listy dyskusyjne związane z Arch Linuxem i inne oficjalne kanały wsparcia dla Arch Linuxa nie są odpowiednim miejscem, aby prosić o pomoc ze snapami na Arch Linuxie. Odpowiednim miejscem do poproszenia o pomoc jest [forum Snapcraft](https://forum.snapcraft.io).

## Zobacz również

*   [Oficjalna strona](https://snapcraft.io/)
*   [Repozytorium na GitHubie](https://github.com/snapcore/snapd)
*   [Artykuł na Arstechnica](http://arstechnica.com/information-technology/2016/06/goodbye-apt-and-yum-ubuntus-snap-apps-are-coming-to-distros-everywhere/) (06/16) o snapach Ubuntu które stają się dostępne dla Archa i innych dystrybucji.