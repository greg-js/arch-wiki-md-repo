<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Wstęp](#Wstęp)
*   [2 Instalacja](#Instalacja)
*   [3 Konfiguracja](#Konfiguracja)
    *   [3.1 USB](#USB)
    *   [3.2 Parallel port](#Parallel_port)
    *   [3.3 Sieć](#Sieć)
*   [4 Sterowniki](#Sterowniki)
    *   [4.1 CUPS](#CUPS)
    *   [4.2 Foomatic](#Foomatic)
    *   [4.3 Dedykowane sterowniki do drukarek](#Dedykowane_sterowniki_do_drukarek)
*   [5 Interfejs konfiguracyjny Web i jego narzędzia](#Interfejs_konfiguracyjny_Web_i_jego_narzędzia)
*   [6 Alternatywne interfejsy CUPS](#Alternatywne_interfejsy_CUPS)
*   [7 Informacje końcowe](#Informacje_końcowe)

## Wstęp

CUPS (Common UNIX Printing System) jest nowoczesnym, przenośnym systemem obsługi urządzeń drukujących dla systemów bazujących na architekturze UNIX.

## Instalacja

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") [cups](https://www.archlinux.org/packages/?name=cups).

Jeżeli chcesz zapisać wydruk jako dokument PDF, zainstaluj także [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf). Domyślnie, pliki pdf znajdują się w `/var/spool/cups-pdf/$USER`. Ta lokalizacja może zostać zmieniona w `/etc/cups/cups-pdf.conf`.

[Enable](/index.php/Enable "Enable") oraz [start](/index.php/Start "Start") dla serwisu `org.cups.cupsd.service`.

## Konfiguracja

Dodatkowe kroki w celu wykrycia drukarki są podane poniżej dla konkretnych interfejsów.

**Note:**

*   Programy pomocnicze używają użytkownika i grupy `cups`. Dzięki temu mają dostęp do sterowników drukarki i plików konfiguracyjnych w `/etc/cups/`, które należą do grupy `cups`.
*   Przed [cups](https://www.archlinux.org/packages/?name=cups) 2.2.6-2, grupa `lp` [była używana zamiast grupy cups](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/cups&id=a209bf21797a239c7ddb4614f0266ba1e5238622). Po aktualizacji `/etc/cups` powinna należeć do grupy `cups` oraz w pliku konfiguracyjnym `/etc/cups/cups-files.conf` powinny się znaleźć `User 209` i `Group 209`.

### USB

By sprawdzić, czy drukarka USB jest wykrywana:

 `$ lsusb` 
```
(...)
Bus 001 Device 007: ID 03f0:1004 Hewlett-Packard DeskJet 970c/970cse

```

### Parallel port

By użyć Parallel portu, wymagane są moduły `lp`, `parport` i `parport_pc` [kernel modules](/index.php/Kernel_modules "Kernel modules").

 `$ dmesg | grep -i parport` 
```
 parport0: Printer, Hewlett-Packard HP LaserJet 2100 Series
 lp0: using parport0 (polling)

```

### Sieć

[Avahi](/index.php/Avahi "Avahi") może zostać użyty do wykrycia drukarek w sieci lokalnej. By użyć hostname [Avahi](/index.php/Avahi "Avahi"), uzyskaj adres [hostname.local](/index.php/Avahi#Hostname_resolution "Avahi") i zainicjuj [restart](/index.php/Restart "Restart") `org.cups.cupsd.service`.

Jeżeli łączysz się drukarkę przez protokół [Samba](/index.php/Samba "Samba"), lub system ma być serwerem drukarki dla klientów Windows, zainstaluj pakiet [samba](https://www.archlinux.org/packages/?name=samba).

## Sterowniki

Sterowniki mogą pochodzić z wielu źródeł. Sprawdź [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems") by zobaczyć niekompletną listę sterowników, które zadziałały innym.

Do obsługi drukarki CUPS potrzebuje pliku PPD i dla większości drukarek [niektórych filtrów](https://www.cups.org/doc/man-filter.html). W celu dowiedzenia się jak CUPS używa plików PPD i filtrów, sprawdź [[1]](https://www.cups.org/doc/postscript-driver.html).

Lista [OpenPrinting Printer List](http://www.openprinting.org/printers) zawiera rekomendacje sterowników dla wielu drukarek. Dostarcza także plików PPD dla każdej drukarki, choć większość jest dostępna w [foomatic](#Foomatic) lub rekomendowanym pakiecie sterownika.

Kiedy dostarczysz plik PPD do CUPS, serwer CUPS zapisze go w `/etc/cups/ppd/`.

### CUPS

CUPS zawiera niektóre pliki PPD i filtry w standardzie, co powinno wystarczyć w większości przypadków. CUPS wspiera [AirPrint](https://en.wikipedia.org/wiki/AirPrint "wikipedia:AirPrint") i [IPP Everywhere](http://www.pwg.org/ipp/everywhere.html).

### Foomatic

Projekt [foomatic](https://wiki.linuxfoundation.org/openprinting/database/foomatic) dostarcza PPD dla wielu sterowników drukarek, zarówno wolnych jak niewolnych. By dowiedzieć się jak działa foomatic, sprawdź [Foomatic from the Developer's View](http://www.openprinting.org/download/kpfeifle/LinuxKongress2002/Tutorial/IV.Foomatic-Developer/IV.tutorial-handout-foomatic-development.html).

By używać foomatic, [Zainstaluj](/index.php/Zainstaluj "Zainstaluj") [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) i jedno z [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db), [foomatic-db-ppds](https://www.archlinux.org/packages/?name=foomatic-db-ppds), [foomatic-db-nonfree-ppds](https://www.archlinux.org/packages/?name=foomatic-db-nonfree-ppds) lub [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds).

Pliki PPD z pakietu foomatic mogą wymagać dodatkowych filtrów, takich jak [gutenprint](https://www.archlinux.org/packages/?name=gutenprint), [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) lub z innych źródeł (np. [min12xxw](https://aur.archlinux.org/packages/min12xxw/)). Dla [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) mogą być także wymagane.

### Dedykowane sterowniki do drukarek

Wielu producentów drukarek dostarcza swoje własne sterowniki dla Linuxa. Są one często dostępne w oficjalnym repozytorium Arch lub w [AUR](/index.php/AUR "AUR").

Niektóre z nich są dokładniej opisane w [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

## Interfejs konfiguracyjny Web i jego narzędzia

Gdy demon `cups` jest już uruchomiony, otwórz przeglądarkę i przejdź do strony [http://localhost:631](http://localhost:631).

Twoim oczom ukaże się panel administracyjny z masą różnych kreatorów dotyczących konfiguracji drukarki. Regułą jest, aby rozpocząć konfigurację klikając w `Adding Printers and Classes (Dodawanie Drukarki i klas)`, a następnie `Add Printer (Dodaj drukarkę)`. Gdy pojawi się monit o nazwę użytkownika i hasło, zaloguj się jako root. Nazwa przypisana do drukarki nie ma znaczenia, to samo dotyczy lokalizacji i opisu. Następnie, na liście urządzeń do wyboru zaznacz swoją drukarkę. Rzeczywista jej nazwa pojawia się obok etykiety (np. obok USB Printer # 1 dla drukarek USB). Na koniec wybierz odpowiednie sterowniki. Konfiguracja jest zakończona.

Teraz nadszedł test konfiguracji. Naciśnij w rozwijanym menu `Konserwacja`, następnie `Drukuj stronę testową`. Jeśli drukarka nie drukuje i nie ma pewności co do poprawności stosowanych ustawień, to problem jest najprawdopodobniej z powodu braku odpowiedniego sterownika drukarki.

**Note:** Podczas ustawiania drukarki USB, gdy zamierzamy dodać swoją drukarkę ale mamy do wyboru tylko tylko drukarkę SCSI, to prawdopodobnie oznacza, że CUPS nie rozpoznaje naszego urządzenia.

## Alternatywne interfejsy CUPS

Jeżeli używasz [GNOME](/index.php/GNOME_(Polski) "GNOME (Polski)"), w zarządzaniu i konfiguracji drukarki pomogą Tobie pakiety:

*   [gnome-cups-manager](https://aur.archlinux.org/packages/gnome-cups-manager/)
*   [system-config-printer-gnome](https://www.archlinux.org/packages/?name=system-config-printer-gnome)

W przypadku pakietu `system-config-printer` musisz wykonać poniższe czynności.

- Utwórz grupę `lpadmin` i dodaj do niej użytkownika:

```
# groupadd lpadmin
# usermod -aG lpadmin nazwa_użytkownika

```

- Dodaj w pliku `/etc/cups/cupsd.conf` wpis `lpadmin `do wiersza:``

`` `/etc/cups/cupsd.conf`  `SystemGroup sys root **lpadmin**` 

- Zrestartuj CUPS:

```
# /etc/rc.d/cups restart

```

Użytkownicy środowiska [KDE](/index.php/KDE_(Polski) "KDE (Polski)") mogą konfigurować swoje drukarki z Centrum Zarządzania (Control Center).

## Informacje końcowe

Przeczytaj także angielskojęzyczne artykuły:

*   [Konfiguracja drukarki sieciowej](/index.php/CUPS_printer_sharing "CUPS printer sharing")
*   [Rozwiązywanie problemów](/index.php/CUPS#Troubleshooting "CUPS")

``