## Contents

*   [1 Wstęp](#Wst.C4.99p)
*   [2 Instalacja wymaganych pakietów i sterownika drukarki](#Instalacja_wymaganych_pakiet.C3.B3w_i_sterownika_drukarki)
*   [3 Konfiguracja](#Konfiguracja)
    *   [3.1 Drukarka USB](#Drukarka_USB)
    *   [3.2 Drukarka LPT](#Drukarka_LPT)
*   [4 Interfejs konfiguracyjny Web i jego narzędzia](#Interfejs_konfiguracyjny_Web_i_jego_narz.C4.99dzia)
*   [5 Alternatywne interfejsy CUPS](#Alternatywne_interfejsy_CUPS)
*   [6 Informacje końcowe](#Informacje_ko.C5.84cowe)

## Wstęp

CUPS (Common UNIX Printing System) jest nowoczesnym, przenośnym systemem obsługi urządzeń drukujących dla systemów bazujących na architekturze UNIX.

## Instalacja wymaganych pakietów i sterownika drukarki

Na początek zainstaluj podstawowe pakiety:

```
# pacman -S cups ghostscript gsfonts

```

Aby uruchomić `cups`, wpisz:

```
# /etc/rc.d/cups start

```

Aby `cups` ładował się przy każdym uruchomieniu systemu, dodajmy odpowiedni wpis do sekcji DAEMONS w `/etc/rc.conf`:

 `/etc/rc.conf`  `DAEMONS=(... cups ...)` 

Następnie wybierz odpowiedni sterownik do swojej drukarki i go także zainstaluj:

*   [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) - sterowniki do drukarek Canon, Epson, Lexmark, Sony, Olympus.
*   [hplip](https://www.archlinux.org/packages/?name=hplip) - sterowki do drukarek firmy HP.
*   [splix](https://www.archlinux.org/packages/?name=splix) - sterowki do drukarek firmy Samsung.
*   [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) - pakiet, który pozwala na konfigurację wirtualnej drukarki PDF tworzącej dokumenty o tym właśnie formacie.

W przypadku, gdy drukarka pomimo zainstalowanych wymaganych pakietów nie działa, spróbuj zainstalować wszystkie sterowniki. Zdarzają się bowiem takie sytuacje, że drukarki mogą działać na innych sterownikach. Na przykład do prawidłowego działania drukarki Brother HL-2140 wymagany jest pakiet `hplip`.

## Konfiguracja

Teraz, kiedy już masz zainstalowane podstawowe pakiety do obsługi drukarki, możesz przejść do etapu jej konfiguracji. W środowiskach graficznych, takich jak GNOME czy KDE, znajdziesz przydatne programy, które mogą pomóc w zarządzania drukarką. Jako, że nie wszyscy używają tych środowisk, poniższa konfiguracja koncentruje się na zastosowaniach dostarczonych przez interfejs sieciowy `cups`.

### Drukarka USB

Użytkownicy podłączający swoją drukarkę za pomocą USB mogą być zmuszeni do wyłączenia modułu `usblp`, choć i tu są wyjątki - drukarki Epson i Canon nie zostaną rozpoznane bez niego. Aby wyłączyć `usblp`, dodaj do `/etc/rc.conf` odpowiedni wpis:

 `/etc/rc.conf`  `MODULES=(... !usblp ...)` 

Jeżeli posiadasz skompilowany przez siebie kernel, możesz potrzebować ręcznie załadować moduł `usbcore`:

```
# modprobe usbcore

```

Gdy moduły są już zainstalowane, podłącz drukarkę i sprawdź, czy system ją wykrywa:

```
# tail /var/log/messages.log

```

albo

```
# dmesg

```

Jeśli używasz `usblp`, wynik powinien wskazywać wykrycie drukarki, jak na poniższym przykładzie:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

Jeśli wyłączyłeś `usblp` w `/etc/rc.conf`, otrzymasz wynik:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

### Drukarka LPT

Jeśli planujesz połączyć drukarkę za pomocą portu równoległego, musisz załadować poniższe moduły:

```
# modprobe lp
# modprobe parport
# modprobe parport_pc

```

Sprawdź, czy system wykrywa drukarkę:

```
# tail /var/log/messages.log

```

Powinieneś otrzymać:

```
lp0: using parport0 (polling).

```

Aby system automatycznie ładował wymagany moduł przy każdym uruchomieniu, użyj swojego edytora tekstu i otwórz `/etc/rc.conf`, następnie dopisz odpowiedni wpis do sekcji MODULES.Oto przykład:

 `/etc/rc.conf`  `MODULES=(... lp parport parport_pc ...)` 

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

- Dodaj w pliku `/etc/cups/cupsd.conf` wpis `lpadmin<code> do wiersza:`

` `/etc/cups/cupsd.conf`  `SystemGroup sys root **lpadmin**` 

- Zrestartuj CUPS:

```
# /etc/rc.d/cups restart

```

Użytkownicy środowiska [KDE](/index.php/KDE_(Polski) "KDE (Polski)") mogą konfigurować swoje drukarki z Centrum Zarządzania (Control Center).

## Informacje końcowe

Przeczytaj także angielskojęzyczne artykuły:

`

`*   [Konfiguracja drukarki sieciowej](/index.php/CUPS_printer_sharing "CUPS printer sharing")`
*   `[Rozwiązywanie problemów](/index.php/CUPS#Troubleshooting "CUPS")`