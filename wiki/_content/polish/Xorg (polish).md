## Contents

*   [1 Wstęp](#Wstęp)
    *   [1.1 Instalacja Xorg](#Instalacja_Xorg)
    *   [1.2 Konfiguracja Xorg](#Konfiguracja_Xorg)
*   [2 Informacje końcowe](#Informacje_końcowe)

## Wstęp

Xorg, czyli inaczej serwer X to nic innego jak graficzny interfejs użytkownika (GUI). Linux, oprócz zarządzania systemem za pomocą tekstu wprowadzanego za pomocą klawiatury, umożliwia pracę w trybie graficznym. Jeżeli chcemy z nich korzystać konieczny jest właśnie Xorg, który odpowiada za ich pracę.

### Instalacja Xorg

Na początek upewnij się, że system jest zaktualizowany:

```
# pacman -Syu

```

Aby zainstalować Xorg, wydajemy polecenie:

```
# pacman -S xorg-server xf86-input-evdev

```

W przypadku laptopa:

```
# pacman -S xorg-server xf86-input-evdev xf86-input-synaptics

```

Aby zainstalować wsparcie dla myszki i klawiatury:

```
# pacman -S xf86-input-mouse xf86-input-keyboard

```

Aby zainstalować pakiet Mesa (zawiera takie narzędzia, jak glxgears, glxinfo):

```
# pacman -S mesa

```

### Konfiguracja Xorg

Od wersji Xorg 1.8 X serwer używa `udev` zamiast `hal` do wykrywania urządzeń wejściowych i konfiguracji InputClass. Konfiguracja znajduje się w katalogu `/etc/X11/xorg.conf.d/` i w zasadzie nie wymaga ingerencji użytkownika.

**Note:** Aktualna wersja Xorg skutecznie automatycznie wykrywa większość sprzętu bez wcześniejszej konfiguracji. Ze względu na te ulepszenia, zaleca się rozpocząć bez pliku xorg.conf i nanosić własne zmiany tylko w razie potrzeby. Zaleca się stosowanie xorg.conf tylko wtedy, gdy powstają problemy z konfiguracją lub jeśli chcemy dodatkowych ustawień.

Jeżeli posiadasz wersję Xorg<1.8 lub z jakiś względów potrzebujesz pliku `/etc/X11/xorg.conf`, poniżej opisana jest jego konfiguracja.

Konfiguracja pliku `/etc/X11/xorg.conf` podzielona jest na następujące sekcje:

```
ServerLayout         # Ogólny układ
Screen               # Konfiguracja obrazu/ekranu
Device               # Konfiguracja karty graficznej
Monitor              # Konfiguracja monitora
InputDevice          # Konfiguracja urządzeń wejściowych
Files                # Ścieżki do katalogów/plików np. czcionek
DRI                  # Konfiguracja DRI
Module               # Konfiguracja modułów
ServerFlags          # Konfiguracja flag

```

Aby uzyskać kompletne informacje na temat składni pliku konfiguracyjnego xorg.conf:

```
# man xorg.conf

```

Automatyczną konfigurację `/etc/X11/xorg.conf` wykonujemy w trybie tekstowym (Ctrl+Alt+F1):

*   Zakańczamy sesję, np. dla środowiska GNOME (jako root):

```
# /etc/rc.d/gdm stop

```

*   Konfigurujemy plik xorg.conf:

```
# Xorg -configure

```

Spowoduje to utworzenie pliku `/root/xorg.conf.new`, który możemy przetestować poprzez wydanie polecenia:

```
# X -config /root/xorg.conf.new

```

*   Jeśli wszystko uruchamia się bez problemu, przenosimy plik do `/etc/x11/`:

```
# cp /root/xorg.conf.new /etc/X11/xorg.conf

```

*   Teraz wystarczy wylogować się z konta root'a, zalogować się na swoje konto i uruchomić sesję.

W przypadku nie używania pliku konfiguracyjnego `/etc/X11/xorg.conf`, domyślna konfiguracja Xorg'a zawarta jest w pliku `/var/log/Xorg.0.log` pomiędzy wierszami:

```
(==) --- Start of built-in configuration ---

```

i

```
(==) --- End of built-in configuration ---

```

## Informacje końcowe

Szczegółowy opis konfiguracji Xorg zawarty są w artykule [Xorg](/index.php/Xorg "Xorg").