## Contents

*   [1 Wstęp](#Wst.C4.99p)
*   [2 Instalacja](#Instalacja)
*   [3 Uruchomienie](#Uruchomienie)
*   [4 Konfiguracja](#Konfiguracja)
*   [5 Informacje końcowe](#Informacje_ko.C5.84cowe)
*   [6 Zobacz też](#Zobacz_te.C5.BC)

## Wstęp

LXDE (Lightweight X11 Desktop Environment) jest to lekkie środowisko graficzne, które z powodzeniem może być używane na słabszych komputerach. Zajmuje mało pamięci RAM, jest łatwo konfigurowalne, do czego korzysta z własnych narzędzi.

Środowisko LXDE jest:

*   Lekkie - nie obciążą zasobów.
*   Szybkie - działa dobrze nawet na starszych komputerach.
*   Funkcjonalne - oparte na GTK2.
*   Elastyczne - Komponenty mogą być użyte bez konieczności instalacji całego środowiska.
*   Zgodne ze standardami - stosuje się do specyfikacji projektu Freedesktop.

Najważniejsze komponenty LXDE:

*   PCManFM: Szybki menedżer plików z zakładkami.
*   LXPanel: Panel LXDE. Posiada GUI, dzięki któremu można łatwo zmodyfikować panel.
*   LXSession / LXSession_Lite: Menedżer sesji LXDE. Działa z HAL i GDM.
*   LXAppearance: Narzędzie do zmiany motywów GTK+.
*   Openbox: Szybki i lekki menedżer okien.
*   Obconf: Narzędzie do konfiguracji Openboksa.
*   GPicView: Prosty, szybki i lekki program do przeglądania obrazów.
*   Leafpad: Procesor tekstu używany jako domyślny w LXDE.
*   LXTerminal: Emulator terminala.
*   XArchiver: Lekki i szybki archiwizator danych.
*   LXNM (jeszcze w budowie): Menedżer połączeń LXDE.

## Instalacja

Po pierwsze, grupę `lxde`:

```
# pacman -S lxde

```

W skład grupy `lxde` wchodzą:

*   gpicview
*   lxappearance
*   lxde-common
*   lxde-icon-theme
*   lxlauncher
*   lxmenu-data
*   lxpanel
*   lxrandr
*   lxsession-lite
*   lxtask
*   lxterminal
*   menu-cache
*   openbox
*   pcmanfm

Po drugie, instalujemy pakiet `gamin`. Jest to proces który informuje nasze programy o zmianach, które nastąpiły na dysku.

```
# pacman -Sy gamin

```

## Uruchomienie

Dodajemy odpowieni wpis do `~/.xinitrc`:

 `~/.xinitrc`  `exec startlxde` 

Jeżeli zainstalowany jest HAL:

 `~/.xinitrc`  `exec startlxde` 

Samo środowisko uruchomimy odpowiednio:

```
$ xinit /usr/bin/startlxde

```

Znacznie szyciej to trwa jeśli wykorzystamy GDM, który jest zgodny z LXSession:

```
# pacman -S gdm

```

Pamiętajmy, że GDM należy dodać na końcu sekcji DAEMONS w `/etc/rc.conf`. Po tej operacji z menu sesji GDM wybieramy LXDE.

## Konfiguracja

Żeby PCManFM działał dobrze, zalecany jest HAL:

```
# pacman -S dbus hal

```

Następnie:

```
# /etc/rc.d/hal start

```

Na koniec dodajemy do sekcji DAEMONS w pliku `/etc/rc.conf`:

```
DAEMONS=(...hal...)

```

Dodajmy również grupy, żeby HAL mógł działać bezproblemowo:

```
# gpasswd -a nazwa_użytkownika optical
# gpasswd -a nazwa_użytkownika storage
# gpasswd -a nazwa_użytkownika dbus
# gpasswd -a nazwa_użytkownika disk
# gpasswd -a nazwa_użytkownika hal

```

## Informacje końcowe

Aby dowiedzieć się więcej o tym środowisku, przejdź do angielskojęzycznego artykułu [LXDE](/index.php/LXDE "LXDE").

## Zobacz też

*   [Strona projektu](http://lxde.org/)