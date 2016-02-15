**Tip:** To część wielostronicowego artykułu Przewodnik Początkującego. **[Kliknij tutaj](/index.php/Beginners%27_Guide_(Polski) "Beginners' Guide (Polski)")** jeśli wolisz czytać przewodnik w całości.

## Contents

*   [1 Extra](#Extra)
    *   [1.1 Sudo](#Sudo)
    *   [1.2 Sound](#Sound)
    *   [1.3 **G**raficzny **I**nterfejs **U**żytkownika](#Graficzny_Interfejs_U.C5.BCytkownika)
        *   [1.3.1 Instalacja X-ów](#Instalacja_X-.C3.B3w)
        *   [1.3.2 Instalacja sterownika wideo](#Instalacja_sterownika_wideo)
            *   [1.3.2.1 Karty graficzne NVIDIA](#Karty_graficzne_NVIDIA)
            *   [1.3.2.2 Karty graficzne ATI](#Karty_graficzne_ATI)
            *   [1.3.2.3 Karty graficzne SiS](#Karty_graficzne_SiS)
        *   [1.3.3 Instalacja sterowników urządzeń wejściowych](#Instalacja_sterownik.C3.B3w_urz.C4.85dze.C5.84_wej.C5.9Bciowych)
        *   [1.3.4 Konfiguracja X (opcjonalnie)](#Konfiguracja_X_.28opcjonalnie.29)
            *   [1.3.4.1 Nieamerykański układ klawiatury](#Nieameryka.C5.84ski_uk.C5.82ad_klawiatury)
        *   [1.3.5 Test serwera X](#Test_serwera_X)
            *   [1.3.5.1 Szyna wiadomości](#Szyna_wiadomo.C5.9Bci)
            *   [1.3.5.2 Uruchomienie serwera X](#Uruchomienie_serwera_X)
            *   [1.3.5.3 W przypadku błędów](#W_przypadku_b.C5.82.C4.99d.C3.B3w)
            *   [1.3.5.4 Potrzebujesz pomocy?](#Potrzebujesz_pomocy.3F)
        *   [1.3.6 Fonty](#Fonty)
        *   [1.3.7 Wybierz i zainstaluj interfejs graficzny](#Wybierz_i_zainstaluj_interfejs_graficzny)
        *   [1.3.8 Sposoby uruchamiania środowiska graficznego](#Sposoby_uruchamiania_.C5.9Brodowiska_graficznego)
            *   [1.3.8.1 Manualny](#Manualny)
            *   [1.3.8.2 Automatically](#Automatically)
*   [2 Appendix](#Appendix)
*   [3 Zobacz także](#Zobacz_tak.C5.BCe)

## Extra

Powinieneś(aś) mieć teraz całkowicie funkcjonalny system Arch, który moze służyć jako baza do zbudowania systemu według twoich potrzeb. Większość użytkowników jest zainteresowana systemem desktopowym, razem z dźwiękiem i grafiką. Ta część przewodnika zawiera krótki przegląd procedur potrzebnych do ich zainstalowania.

### Sudo

[Sudo](/index.php?title=Sudo_(Polski)&action=edit&redlink=1 "Sudo (Polski) (page does not exist)") może znacznie ułatwić administrację systemu nie korzystając z konta roota.

### Sound

Jeśli potrzebujesz dźwięku, przejdź do [Advanced Linux Sound Architecture](/index.php?title=Advanced_Linux_Sound_Architecture_(Polski)&action=edit&redlink=1 "Advanced Linux Sound Architecture (Polski) (page does not exist)") po instrukcje. Ewentualnie najpierw przejdź do [następnej sekcji](#Graficzny_Interfejs_U.C5.BCytkownika) i skonfiguruj dźwięk później.

**Note:** ALSA działa zwykle od razu po instalacji, trzeba tylko wyłączyć wyciszenie.

[Advanced Linux Sound Architecture](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture") (Zaawansowana Architektura Dźwięku (w) Linuksie, ALSA) jest dołączona do jądra i zaleca się wypróbowanie jej najpierw. Jednak jeśli nie będzie działać lub nie jesteś zadowolony(a) z jakości, [Open Sound System](https://en.wikipedia.org/wiki/Open_Sound_System "wikipedia:Open Sound System") (Otwarty System Dźwięku, OSS) to dobra alternatywa. OSSv4 zostało wydane pod wolną licencją i jest uważane za znaczące udoskonalenie starszego OSSv3, które zastąpiła ALSA. Instrukcje mogą być znalezione w [tym artykule](/index.php?title=OSS_(Polski)&action=edit&redlink=1 "OSS (Polski) (page does not exist)").

Jeśli posiadasz zaawansowany sprzęt audio, odwiedź [Dźwięk](/index.php?title=Sound_(Polski)&action=edit&redlink=1 "Sound (Polski) (page does not exist)") po zbiór różnych artykułów na ten temat.

### **G**raficzny **I**nterfejs **U**żytkownika

#### Instalacja X-ów

**Note:** Jeśli instalujesz Archa jako gość w VirtualBox, musisz zainstalować X w inny sposób. Zobacz [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest") i przeskocz do konfiguracji poniżej.

[X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (nazywany **X11** lub **X**) to system okien używany w systemach uniksowych. Dostarcza protokół i podstawowe narzędzia do tworzenia graficznego interfejsu użytkownika (GUI).

Zainstalujemy teraz podstawowe pakiety **[Xorg](/index.php/Xorg_(Polski) "Xorg (Polski)")** używając pacmana.

Zainstaluj pakiety bazowe:

 `# pacman -S xorg-server xorg-xinit xorg-server-utils` 

Zainstaluj [mesa](https://en.wikipedia.org/wiki/Mesa_3D_(OpenGL) "wikipedia:Mesa 3D (OpenGL)") dla wsparcia 3D:

 `# pacman -S mesa` 

Narzędzia glxgears i [glxinfo](http://dri.freedesktop.org/wiki/glxinfo) znajdują się w pakiecie [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos). Zainstaluj go, jeśli ich potrzebujesz:

 `# pacman -S mesa-demos` 

#### Instalacja sterownika wideo

Następnie, powinieneś(aś) zainstalować sterownik do twojej karty graficznej.

Musisz wiedzieć, jaki układ graficzny posiadasz w komputerze. Jeśli nie wiesz, użyj programu `/usr/sbin/lspci`:

 `$ lspci | grep VGA` 
**Note:** Sterownik **vesa** jest najbardziej podstawowy i powinien działać z prawie każdym układem graficznym. Jeśli posiadasz rzadko spotykaną kartę i nie możesz znaleźć do niej sterownika, vesa _powinna_ zadziałać, oferuje jednak wyłącznie nieakcelerowaną grafikę 2D.

Aby znaleźć kompletną listę **otwartoźródłowych** sterowników wideo, przeszukaj bazę pakietów:

 `$ pacman -Ss xf86-video | less` 
**Note:** Własnościowe sterowniki dla NVIDIA i ATI są opisane w następnych sekcjach. Jeśli zamierzasz używać ich do tworzenia grafiki 3D, np. grając, rozważ ich użycie.

Użyj pacmana do zainstalowania odpowiedniego dla twojej karty sterownika wideo. Przykład dla sterownika Savage:

 `# pacman -S xf86-video-savage` 
**Tip:** Dla części kart Intela, konfiguracja może być wymagana, aby uzyskać odpowiednią wydajność 2D lub 3D, zobacz [Intel](/index.php/Intel_(Polski) "Intel (Polski)") po więcej informacji.

##### Karty graficzne NVIDIA

Użytkownicy kart NVIDIA mają trzy opcje w kwestii sterowników (oprócz sterownika vesa):

*   Otwarty sterownik nouveau, który oferuje szybką akcelerację 2D i podstawowe wsparcie 3D, które jest wystarczające dla menedżerów kompozycji. Nie obsługuje jeszcze w pełni oszczędzania energii. [Feature Matrix.](http://nouveau.freedesktop.org/wiki/FeatureMatrix)
*   Otwarty (ale przestarzały) sterownik nv, który jest bardzo wolny i obsługuje tylko 2D.
*   Własnościowy sterownik nvidia, który oferuje dobrą wydajność 3D performance i oszczędzanie energii. Nawet jeśli zamierzasz korzystać ze sterownika własnościowego, zalecane jest zainstalowanie nouveau i przełączenie na sterownik nvidia po skonfigurowaniu X-ów. Nouveau często działa od razu, podczas gdy nvidia wymaga konfiguracji. Zobacz [NVIDIA](/index.php?title=NVIDIA_(Polski)&action=edit&redlink=1 "NVIDIA (Polski) (page does not exist)") po więcej informacji.

Otwarty sterownik nouveau powinien być wystarczający dla większości użytkowników i jest rekomendowany:

 `# pacman -S xf86-video-nouveau` 

Dla eksperymentalnej akceleracji 3D:

 `# pacman -S nouveau-dri` 
**Tip:** Po zaawansowane instrukcje, zobacz [Nouveau](/index.php?title=Nouveau_(Polski)&action=edit&redlink=1 "Nouveau (Polski) (page does not exist)").

##### Karty graficzne ATI

Właściciele kart ATI mają dwie opcje dotyczące sterowników (oprócz sterwonika vesa):

*   Otwarty sterownik **radeon** dostarczany w pakiecie [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati). Zobacz [radeon feature matrix](http://wiki.x.org/wiki/RadeonFeature) po szczegóły.
*   Własnościowy sterownik **fglrx** dostarczany w pakiecie [catalyst](https://aur.archlinux.org/packages/catalyst/) znajdujący się w [AUR](/index.php/AUR_(Polski) "AUR (Polski)"). Wspiera tylko nowe karty (HD2xxx i nowsze). Znajdował się wcześniej w repozytorium **extra**, jednak od marca 2009, zaprzestano oficjalnego wsparcia z powodu niezadowolenia z jakości i tempa rozwoju sterownika. Zobacz [ATI Catalyst](/index.php?title=ATI_Catalyst_(Polski)&action=edit&redlink=1 "ATI Catalyst (Polski) (page does not exist)") po więcej informacji.

Otwarty sterownik jest rekomendowany. Zainstaluj go:

 `# pacman -S xf86-video-ati` 
**Tip:** Po zaawansowane instrukcje, zobacz [ATI](/index.php/ATI_(Polski) "ATI (Polski)").

##### Karty graficzne SiS

Karty SiS nie są oficjalne wspierane w Linuksie. Mimo to, trzy mniej lub bardziej przestarzałe sterowniki mogą być zainstalowane z [oficjalnych repozytoriów](/index.php?title=Official_repositories_(Polski)&action=edit&redlink=1 "Official repositories (Polski) (page does not exist)"):

 `# pacman -S xf86-video-sis` 

lub

 `# pacman -S xf86-video-sisusb` 

lub

 `# pacman -S xf86-video-sisimedia` 

Jeśli żaden z nich nie działa, szukanie sterownika w [AUR](/index.php/AUR_(Polski) "AUR (Polski)") i jego kompilacja (razem z możliwym downgradem pakietu [xorg-server](https://www.archlinux.org/packages/?name=xorg-server)) to jedyne wyjście.

**Tip:**

*   Możesz dowiedzieć się więcej o obecnym stanie sterowników sis na stronie [http://dri.freedesktop.org/wiki/SiS](http://dri.freedesktop.org/wiki/SiS).
*   Po zaawansowane instrukcje, zobacz [SiS](/index.php?title=SiS_(Polski)&action=edit&redlink=1 "SiS (Polski) (page does not exist)").

#### Instalacja sterowników urządzeń wejściowych

Udev powinien wykryć twój sprzęt bez problemów, a evdev ([xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)) to nowoczesny sterownik urządzeń wejściowych, obsługujący prawie wszystkie urządzenia. Dlatego, instalacja sterowników zwykle nie jest potrzebna. Evdev został już zainstalowany jako zależność Xorg.

Jeśli evdev nie obsługuje twojego urządzenia, zainstaluj potrzebne sterowniki z grupy xorg-input-drivers.

Po kompletną listę dostępnych sterowników, przeszukaj bazę pacmana:

 `# pacman -Ss xf86-input | less` 
**Note:** Potrzebujesz [xf86-input-keyboard](https://www.archlinux.org/packages/?name=xf86-input-keyboard) i [xf86-input-mouse](https://www.archlinux.org/packages/?name=xf86-input-mouse) jeśli zamierzasz wyłączyć automatyczne wykrywanie urządzeń, w przeciwnym przypadku, evdev będzie sterownikiem wszystkich urządzeń wejściowych.

Użytkownicy laptopów (lub ekranów dotykowych) powinni zainstalować pakiet synaptics, aby umożliwić konfigurację touchpada/ekranu dotykowego:

 `# pacman -S xf86-input-synaptics` 
**Tip:** Po informacje na temat ustawiania i rozwiązywania problemów z touchpadem, zobacz artykuł [Touchpad](/index.php?title=Touchpad_Synaptics_(Polski)&action=edit&redlink=1 "Touchpad Synaptics (Polski) (page does not exist)").

#### Konfiguracja X (opcjonalnie)

**Warning:** Własnościowe sterowniki zwykle wymagają ponownego uruchomienia komputera po instalacji i konfiguracji. Zobacz [NVIDIA](/index.php?title=NVIDIA_(Polski)&action=edit&redlink=1 "NVIDIA (Polski) (page does not exist)") lub [ATI Catalyst](/index.php?title=ATI_Catalyst_(Polski)&action=edit&redlink=1 "ATI Catalyst (Polski) (page does not exist)") po szczegóły.

Serwer X potrafi przeprowadzić autokonfigurację, dzięki temu może funkcjonować bez pliku `xorg.conf`. Jeśli chcesz skonfigurować X manualnie, zobacz stronę [Xorg](/index.php/Xorg_(Polski) "Xorg (Polski)").

##### Nieamerykański układ klawiatury

Jeśli nie używasz amerykańskiego układu klawiatury, musisz go ustawić w `/etc/X11/xorg.conf.d/10-evdev.conf`:

```
Section "InputClass"
    Identifier "evdev keyboard catchall"
    MatchIsKeyboard "on"
    MatchDevicePath "/dev/input/event*"
    Driver "evdev"
    **Option "XkbLayout" "pl"**
EndSection

```

Jeśli chcesz używać innego wariantu układu (np. Dvorak), dodaj następujące opcje do powyższej sekcji:

```
Option "XkbLayout" "pl"
Option "XkbVariant" "dvorak"

```

**Tip:** Większość środowisk graficznych ustawia układ klawiatury niezależnie i zwykle nie ma potrzeby ustawiać go w konfiguracji X.

**Note:** Opcja **XkbLayout** może używać innych oznaczeń niż polecenia km czy loadkeys. Lista dostępnych układów i wariantów może być znaleziona w `/usr/share/X11/xkb/rules/base.lst` (zobacz linie znajdujące się poniżej `! layout`). Przykładowo, układ **gb** odpowiada "English (UK)".

#### Test serwera X

Ta sekcja wyjaśnia, jak ustawić domyślne środowisko X z [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm), aby przetestować **X**y. [Poniższa sekcja](#Wybierz_i_zainstaluj_interfejs_graficzny) objaśnia instalację wybranego środowiska graficznego lub menedżera okien.

Zainstaluj domyślne środowisko:

 `# pacman -S xorg-twm xorg-xclock xterm` 

Jeśli Xorg został zainstalowany przed stworzeniem konta użytkownika, pozostanie w katalogu domowym szablon pliku `.xinitrc`, który musi zostać usunięty lub wyedytowany przed uruchomieniem X. Usunięcie go spowoduje uruchomienie domyślnego środowiska przy uruchomieniu serwera **X**.

 `$ rm ~/.xinitrc` 

##### Szyna wiadomości

**Note:** _Możesz_ pominąć tę sekcję, dopóki nie zainstalujesz pakietu, który zależy od [dbus](/index.php?title=Dbus_(Polski)&action=edit&redlink=1 "Dbus (Polski) (page does not exist)"), musisz jednak pamiętać o ustawieniu demona kiedy to zrobisz.

Zainstaluj [dbus](/index.php?title=Dbus_(Polski)&action=edit&redlink=1 "Dbus (Polski) (page does not exist)"):

 `# pacman -S dbus` 

Uruchom demon dbus:

 `# rc.d start dbus` 
**Note:** `/usr/sbin/rc.d` to polecenie specyficzne dla Archa, które działa jako skrót do uruchamiania [demon](/index.php/Daemon_(Polski) "Daemon (Polski)")ów zamiast korzystania z pełnej ścieżki `/etc/rc.d/_demon_`.

Dodaj dbus do linii `DAEMONS` w `/etc/rc.conf`, aby był uruchamiany razem z systemem:

 `DAEMONS=(... dbus ...)` 

##### Uruchomienie serwera X

**Note:** Skrót klawiszowy Ctrl-Alt-Backspace używany do zabijania serwera X jest uznany za przestarzały i nie umożliwi wyjścia z tego testu. Możesz włączyć skrót `Ctrl-Alt-Backspace` edytując `xorg.conf`, jak opisano [tutaj](/index.php/Xorg#Ctrl.2BAlt.2BBackspace_does_not_work "Xorg").

Obydwa następujące polecenia znajdują się w pakiecie [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit). W końcu, uruchom X:

 `$ startx` 

lub

 `$ xinit -- /usr/bin/X -nolisten tcp` 

Powinno pojawić się kilka okien, a mysz powinna działać. Możesz opuścić środowisko graficzne użwając polecenia `exit`, dopóki nie wrócisz do terminala.

Jeśli ekran staje się czarny, nadal możesz przełączyć się do innej konsoli (np. używając `CTRL-Alt-F2`), na ślepo wpisać root, nacisnąć `Enter`, wpisać hasło roota i nacisnąć `Enter`.

Możesz spróbować zakończyć proces serwera **X** używając `/usr/bin/pkill` (z wielką literą **X**):

 `# pkill X` 

Jeśli **pkill** nie działa, uruchom komputer ponownie używając:

 `# reboot` 

##### W przypadku błędów

Jeśli nastąpi jakiś problem, szukaj błędów w `/var/log/Xorg.0.log`. Linie zaczynające się na `(EE)` oznaczają błąd, a zaczynajace się na `(WW)` to ostrzeżenia, które mogą sygnalizować inne problemy.

 `$ grep EE /var/log/Xorg.0.log` 

Błędy mogą być także znalezione w wyjściu serwera **X** w konsoli, z której został uruchomiony.

Zobacz artykuł [Xorg](/index.php/Xorg_(Polski) "Xorg (Polski)") po szczegółowe instrukcje i rozwiązania problemów.

##### Potrzebujesz pomocy?

Jeśli po skonsultowaniu się z artykułem [Xorg](/index.php/Xorg_(Polski) "Xorg (Polski)") nadal masz problemy i potrzebujesz porady na forum Archa, zainstaluj [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste):

 `# pacman -S wgetpaste` 

Użyj **wgetpaste** i podaj linki do następujących plików szukając pomocy na forum:

*   `~/.xinitrc`
*   `/etc/X11/xorg.conf`
*   `/var/log/Xorg.0.log`
*   `/var/log/Xorg.0.log.old`

Przykład użycia:

 `$ wgetpaste /sciezka/do/pliku` 

Umieść odpowoednie linki w swoim poście na forum. Pamiętaj o dostarczeniu informacji o posiadanym sprzęcie i zainstalowanych sterownikach.

**Note:** Bardzo ważne jest dostarczenie dokładnych informacji przy rozwiązywaniu problemów z serwerem X. Kiedy szukasz pomocy na forum, umieść w poście wszystkie opisane wyżej informacje.

#### Fonty

W tym momencie, powinieneś(aś) zainstalować zbiór fontów TrueType fonts, ponieważ tylko nieskalowalne fonty binarne są dostępne domyślnie. DejaVu to zbiór wysokiej jakości fontów z dobrym wsparciem [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode"):

 `# pacman -S ttf-dejavu` 

*   Strona [Konfiguracja fontów](/index.php?title=Font_Configuration_(Polski)&action=edit&redlink=1 "Font Configuration (Polski) (page does not exist)") zawiera informacje o konfiguracji renderingu fontów, a strona [Fonty](/index.php?title=Fonts_(Polski)&action=edit&redlink=1 "Fonts (Polski) (page does not exist)") zawiera sugestie fontów i instrukcje instalacji.

#### Wybierz i zainstaluj interfejs graficzny

System X Window dostarcza podstawowego frameworku do tworzenia graficznego interfejsu użytkownika (GUI).

**Note:** Wybór środowiska graficznego lub menedżera okien to bardzo subiektywna decyzja. Wybierz środowisko najlepsze dla _twoich_ potrzeb.

	Menedżer okien (_Window Manager_, WM) 

	Kontroluje położenie i wygląd okien aplikacji łącznie z X Window System. **Zobacz [Menedżery okien](/index.php?title=Window_Manager_(Polski)&action=edit&redlink=1 "Window Manager (Polski) (page does not exist)") po więcej informacji.**

	Środowisko graficzne (_Desktop Environment_, DE)

	Wykorzystuje serwer X, aby dostarczyć funkcjonalny i dynamiczny interfejs użytkownika. Zwykle zawiera menedżer okien, ikony, aplety, panele, tapety, zbiór towarzyszacych aplikacji i różne ułatwienia. **Zobacz [Środowiska graficzne](/index.php?title=Desktop_Environment_(Polski)&action=edit&redlink=1 "Desktop Environment (Polski) (page does not exist)") po więcej informacji.**

**Note:** Możesz zbudować własne środowisko używając wybranych aplikacji i menedżera okien.

Po instalacji środowiska graficznego, możesz przejść do [Ogólne porady](/index.php?title=General_Recommendations_(Polski)&action=edit&redlink=1 "General Recommendations (Polski) (page does not exist)") po różne porady.

#### Sposoby uruchamiania środowiska graficznego

##### Manualny

Możesz uruchamiać serwer X manualnie z terminala zamiast uruchamiać go automatycznie przez system. Po polecenia specyficzne dla wybranego środowiska, zobacz jego stronę w wiki. Po bardziej ogólne komendy serwera **X**, zobacz [odpowiednią sekcję na stronie wiki Xorg](/index.php/Xorg_(Polski)#Metody_uruchamiania_.C5.9Brodowiska_graficznego "Xorg (Polski)").

##### Automatically

Możesz chcieć, aby pulpit uruchamiał się automatycznie razem z systemem zamiast uruchamiać X manualnie. Zobacz [Menedżer logowania](/index.php?title=Display_Manager_(Polski)&action=edit&redlink=1 "Display Manager (Polski) (page does not exist)") po instrukcje dotyczące menedżera logowania luub [Uruchamianie X przy starcie](/index.php?title=Start_X_at_Boot_(Polski)&action=edit&redlink=1 "Start X at Boot (Polski) (page does not exist)") po dwie metody, które nie wymagają użycia menedżera logowania.

## Appendix

Po listę aplikacji, które mogą być użyteczne, zobacz [Popularne aplikacje](/index.php?title=List_of_applications_(Polski)&action=edit&redlink=1 "List of applications (Polski) (page does not exist)").

Zobacz [Ogólne porady](/index.php?title=General_Recommendations_(Polski)&action=edit&redlink=1 "General Recommendations (Polski) (page does not exist)") po listę porad dotyczących skalowania prędkości procesora czy renderingu fontów.

## Zobacz także

*   [Easy Arch Linux Install Tutorial](http://gotux.net/tutorials/arch-linux-initial-install)