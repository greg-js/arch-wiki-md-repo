Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [GNOME_(Polski)](/index.php/GNOME_(Polski) "GNOME (Polski)")
*   [LightDM](/index.php/LightDM "LightDM")

[DDE](https://www.deepin.org/en/?language=en) (Deepin Desktop Environment) jest domyślnym środowiskiem graficznym stworzonym na potrzeby dystrybucji Linux Deepin.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Uruchamianie środowiska graficznego Deepin](#Uruchamianie_środowiska_graficznego_Deepin)
    *   [2.1 Poprzez menadżer logowania](#Poprzez_menadżer_logowania)
*   [3 Rozwiązywanie problemów](#Rozwiązywanie_problemów)
    *   [3.1 Brak tła po powrocie ze stanu wstrzymania](#Brak_tła_po_powrocie_ze_stanu_wstrzymania)
*   [4 Raportowanie błędów](#Raportowanie_błędów)

## Instalacja

Aby uzyskać podstawowe środowisko graficzne, należy zainstalować grupę [deepin](https://www.archlinux.org/groups/x86_64/deepin/). Pobierze ona i skonfiguruje wszystkie wymagane elementy.

```
# pacman -S deepin

```

Grupa [deepin-extra](https://www.archlinux.org/groups/x86_64/deepin-extra/) zawiera dodatkowe aplikacje dostępne do instalacji w każdej chwili w celu uzupełnienia funkcjonalności środowiska podstawowego.

W celu użycia zintegrowanej w środowisko Deepin obsługi sieci, pakiet [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) jest wymagany, a usługa `NetworkManager.service`[Systemd#Using units](/index.php/Systemd#Using_units "Systemd") musi być włączona i uruchomiona.

## Uruchamianie środowiska graficznego Deepin

### Poprzez menadżer logowania

Aby użyć domyślnego dla Deepina menadżera lightdm musisz zmodyfikować plik konfiguracyjny w sekcji `[Seat:*]` w następujący sposób:.

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
...
greeter-session=lightdm-deepin-greeter
```

Uwaga - użytkownik(wykluczając konto administratora - root) musi dysponować własnym katalogiem home.

## Rozwiązywanie problemów

### Brak tła po powrocie ze stanu wstrzymania

Ze względu na to jak sterowniki NVIDIA przechowują FBO [[1]](https://devtalk.nvidia.com/default/topic/787748/linux/-nvidia340xx-archlinux64-gnome3-14-the-background-of-desktop-and-lockscreen-mess-after-resume-from-/post/4367179/#4367179), zdarza się, że po powrocie ze stanu wstrzymania tło nagle znika, zostawiając tylko białe pole. Błąd wydaje się na naprawiony w środowisku graficznym Gnome. Deepin jednak dalej cierpi na ową przypadłość.

Możliwym obejściem problemu jest restartowanie menadżera okien za każdym razem gdy komputer powraca ze stanu wstrzymania. Aby to zrobić należy stworzyć następującą usługę w systemd:

 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStart=/usr/bin/deepin-wm-restart.sh

[Install]
WantedBy=suspend.target

```

Który z kolei uruchamia następujący skrypt:

 `/usr/bin/deepin-wm-restart.sh` 
```
#!/bin/bash
export DISPLAY=:0
deepin-wm --replace

```

Gdy oba te pliki zostaną stworzone w odpowiednich ścieżkach (nazwy plików i ścieżki podane są w nagłówkach), w celu automatyzacji całego procesu należy wykonać następujące komendy:

```
# chmod +x /usr/bin/deepin-wm-restart.sh
# systemctl enable resume@*nazwa_użytkownika*
# systemctl start resume@*nazwa_użytkownika* 

```

Pierwsza komenda sprawia, że skrypt, który właśnie stworzyłeś dostaje prawa do uruchamiania się jako plik wykonywalny. Druga upewnia się, że usługa zawsze startuje razem z systemem, ostatnia zaś uruchamia usługę w tej chwili w celu uniknięcia restartu komputera, można ją pominąć, wtedy jednak restart komputera jest wymagany.

## Raportowanie błędów

Każdy błąd związany bezpośrednio ze środowiskiem Deepin powinien być raportowany w tym [miejscu](https://github.com/linuxdeepin/developer-center/issues). Dzięki temu developerzy Deepin mają wgląd do sprawy i naprawią problem najszybciej jak to tylko możliwe.