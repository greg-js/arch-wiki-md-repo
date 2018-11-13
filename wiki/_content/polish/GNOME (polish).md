Related articles

*   [GTK+ (Polski)](/index.php?title=GTK%2B_(Polski)&action=edit&redlink=1 "GTK+ (Polski) (page does not exist)")
*   [KDE (Polski)](/index.php/KDE_(Polski) "KDE (Polski)")
*   [Xfce (Polski)](/index.php/Xfce_(Polski) "Xfce (Polski)")

GNOME 3 to nowoczesne środowisko, napisane od zera używając biblioteki GTK3.

## Contents

*   [1 Wprowadzenie](#Wprowadzenie)
*   [2 Instalacja](#Instalacja)
    *   [2.1 Demon D-Bus](#Demon_D-Bus)
    *   [2.2 Uruchomienie GNOME](#Uruchomienie_GNOME)
*   [3 Używanie Shella](#Używanie_Shella)
    *   [3.1 Ściąga GNOME](#Ściąga_GNOME)
    *   [3.2 Ponowne uruchomienie shella](#Ponowne_uruchomienie_shella)
    *   [3.3 Shell przestaje działać](#Shell_przestaje_działać)
    *   [3.4 Shell zawiesza się](#Shell_zawiesza_się)
*   [4 Personalizacja GNOME](#Personalizacja_GNOME)
    *   [4.1 Ogólny wygląd](#Ogólny_wygląd)
        *   [4.1.1 Gsettings](#Gsettings)
        *   [4.1.2 GNOME tweak tool](#GNOME_tweak_tool)
        *   [4.1.3 Temat GTK3 w pliku settings.ini](#Temat_GTK3_w_pliku_settings.ini)
        *   [4.1.4 Temat ikon](#Temat_ikon)
    *   [4.2 Nautilus](#Nautilus)
    *   [4.3 Panel GNOME](#Panel_GNOME)
        *   [4.3.1 Pokaż datę na górnym pasku](#Pokaż_datę_na_górnym_pasku)
        *   [4.3.2 Ukryj niechciane ikony znajdujące się na pasku](#Ukryj_niechciane_ikony_znajdujące_się_na_pasku)
            *   [4.3.2.1 Ukrywanie ikon z użyciem rozszerzeń](#Ukrywanie_ikon_z_użyciem_rozszerzeń)
            *   [4.3.2.2 Manualna educja plików panelu GNOME](#Manualna_educja_plików_panelu_GNOME)
        *   [4.3.3 Pokaż ikonę baterii](#Pokaż_ikonę_baterii)
        *   [4.3.4 Wyłącz "Uśpij" w menu statusu i GDM](#Wyłącz_"Uśpij"_w_menu_statusu_i_GDM)
        *   [4.3.5 Wyłącz opóźnienie przy wylogowywaniu](#Wyłącz_opóźnienie_przy_wylogowywaniu)
        *   [4.3.6 Pokaż monitor systemu](#Pokaż_monitor_systemu)
        *   [4.3.7 Pokaż informacje o pogodzie](#Pokaż_informacje_o_pogodzie)
    *   [4.4 Widok podglądu](#Widok_podglądu)
        *   [4.4.1 Usuń wpisy z widoku Programów](#Usuń_wpisy_z_widoku_Programów)
        *   [4.4.2 Zmniejsz rozmiar ikon aplikacji](#Zmniejsz_rozmiar_ikon_aplikacji)
        *   [4.4.3 Wyłącz "gorący róg" włączający widok Podglądu](#Wyłącz_"gorący_róg"_włączający_widok_Podglądu)
    *   [4.5 Pasek tytułu](#Pasek_tytułu)
        *   [4.5.1 Zmniejsz wysokość paska tytułu](#Zmniejsz_wysokość_paska_tytułu)
        *   [4.5.2 Zmień kolejność przycisków na pasku tytułu](#Zmień_kolejność_przycisków_na_pasku_tytułu)
        *   [4.5.3 Ukryj pasek tytułu przy maksymalizacji okna](#Ukryj_pasek_tytułu_przy_maksymalizacji_okna)
        *   [4.5.4 Zmiana tła logowania](#Zmiana_tła_logowania)
        *   [4.5.5 Większa czcionka przy logowaniu](#Większa_czcionka_przy_logowaniu)
        *   [4.5.6 Wyłączenie dźwięków](#Wyłączenie_dźwięków)
        *   [4.5.7 Interaktywny przycisk włączenia komputera](#Interaktywny_przycisk_włączenia_komputera)
        *   [4.5.8 Układ klawiatury w GDM](#Układ_klawiatury_w_GDM)
*   [5 Różne ustawienia](#Różne_ustawienia)
    *   [5.1 Automatyczne uruchamianie programu po zalogowaniu](#Automatyczne_uruchamianie_programu_po_zalogowaniu)
    *   [5.2 Editing applications menu](#Editing_applications_menu)
    *   [5.3 Część 'Ustawień systemu' nie jest zachowywana](#Część_'Ustawień_systemu'_nie_jest_zachowywana)
    *   [5.4 Włącz NumLock przy logowaniu](#Włącz_NumLock_przy_logowaniu)
    *   [5.5 Włącz przesuwanie okien dialogowych](#Włącz_przesuwanie_okien_dialogowych)
    *   [5.6 Rozszerzenia GNOME Shell](#Rozszerzenia_GNOME_Shell)
    *   [5.7 Domyślny menedżer plików/zastąp Nautilusa](#Domyślny_menedżer_plików/zastąp_Nautilusa)
    *   [5.8 Domyślny terminal](#Domyślny_terminal)
    *   [5.9 Środkowy przycisk myszy](#Środkowy_przycisk_myszy)
    *   [5.10 Przyciemnianie ekranu](#Przyciemnianie_ekranu)
    *   [5.11 Alternatywny menedżer okien](#Alternatywny_menedżer_okien)
*   [6 Ukryte funkcje](#Ukryte_funkcje)
    *   [6.1 Zmiana skrótów klawiszowych](#Zmiana_skrótów_klawiszowych)
    *   [6.2 Wyłączenie komputera w menu statusu](#Wyłączenie_komputera_w_menu_statusu)
*   [7 Zintegrowany komunikator (Empathy)](#Zintegrowany_komunikator_(Empathy))
*   [8 Wymuszenie trybu zastępczego](#Wymuszenie_trybu_zastępczego)
*   [9 Rozwiązania problemów](#Rozwiązania_problemów)
    *   [9.1 Logowanie do GNOME zajmuje bardzo dużo czasu](#Logowanie_do_GNOME_zajmuje_bardzo_dużo_czasu)
    *   [9.2 Kiedy rozszerzenie zepsuje GNOME](#Kiedy_rozszerzenie_zepsuje_GNOME)
    *   [9.3 Rozszerzenie nie działa po aktualizacji GNOME](#Rozszerzenie_nie_działa_po_aktualizacji_GNOME)
    *   [9.4 Ekran nie jest blokowany po wybudzeniu](#Ekran_nie_jest_blokowany_po_wybudzeniu)
    *   [9.5 Klawisz "Windows"](#Klawisz_"Windows")
    *   [9.6 Skróty klawiszowe nie działają przy uruchomionym conky](#Skróty_klawiszowe_nie_działają_przy_uruchomionym_conky)
    *   [9.7 Aplikacje GTK2+ nie uruchamiają się (Naruszenie ochrony pamięci)](#Aplikacje_GTK2+_nie_uruchamiają_się_(Naruszenie_ochrony_pamięci))
    *   [9.8 Sterownik ATI Catalyst powoduje artefakty](#Sterownik_ATI_Catalyst_powoduje_artefakty)
    *   [9.9 Sterownik xf86-video-ati: migotanie od czasu do czasu](#Sterownik_xf86-video-ati:_migotanie_od_czasu_do_czasu)
    *   [9.10 Sterownik xf86-video-intel "rwie" obraz niezależnie od ustawienia VSYNC](#Sterownik_xf86-video-intel_"rwie"_obraz_niezależnie_od_ustawienia_VSYNC)
    *   [9.11 Okna otwierają się za innymi oknami używając wielu monitorów](#Okna_otwierają_się_za_innymi_oknami_używając_wielu_monitorów)
    *   [9.12 Wiele monitorów i rozszerzenie dock](#Wiele_monitorów_i_rozszerzenie_dock)
    *   [9.13 Brak dźwięków zdarzeń Empathy i innych programów](#Brak_dźwięków_zdarzeń_Empathy_i_innych_programów)
    *   [9.14 Zmiana skrótów przez can-change-accels nie działa](#Zmiana_skrótów_przez_can-change-accels_nie_działa)
    *   [9.15 Panele nie reagują na kliknięcie prawym przyciskiem w trybie zastępczym](#Panele_nie_reagują_na_kliknięcie_prawym_przyciskiem_w_trybie_zastępczym)
    *   [9.16 Skrót klawiszowy "Pokaż pulpit" nie działa](#Skrót_klawiszowy_"Pokaż_pulpit"_nie_działa)
    *   [9.17 Nautilus się nie uruchamia](#Nautilus_się_nie_uruchamia)
    *   [9.18 Epiphany nie odtwarza filmów we Flashu](#Epiphany_nie_odtwarza_filmów_we_Flashu)
    *   [9.19 Nie można zastosować zapisanej konfiguracji monitorów](#Nie_można_zastosować_zapisanej_konfiguracji_monitorów)
    *   [9.20 Włączani touchpada nie działa](#Włączani_touchpada_nie_działa)
    *   [9.21 Ctrl+v wkleja ścieżkę zamiast pliku w Nautilusie](#Ctrl+v_wkleja_ścieżkę_zamiast_pliku_w_Nautilusie)
    *   [9.22 Nie mogę połączyć się z zabezpieczonymi sieciami Wi-Fi](#Nie_mogę_połączyć_się_z_zabezpieczonymi_sieciami_Wi-Fi)
    *   [9.23 "Any command has been defined 33"](#"Any_command_has_been_defined_33")
    *   [9.24 GDM i GNOME używają kursorów X11](#GDM_i_GNOME_używają_kursorów_X11)
    *   [9.25 Tracker & Dokumenty nie pokazują lokalnych plików](#Tracker_&_Dokumenty_nie_pokazują_lokalnych_plików)
*   [10 Linki zewnętrzne](#Linki_zewnętrzne)

## Wprowadzenie

GNOME 3 posiada *dwa* interfejsy: **GNOME Shell**, ustawiony jako domyślny; oraz **tryb zastępczy** (ang. fallback mode). GNOME-session automatycznie wykrywa czy Twój komputer jest w stanie uruchomić GNOME Shell; jeśli nie jest, uruchomi tryb zastępczy.

**Tryb zastępczy** jest podobny do GNOME 2 (używa gnome-panel/Metacity zamiast gnome-shell/Mutter).

Jeśli używasz trybu zastępczego, w dalszym ciągu możesz zastąpić domyślny menedżer okien GNOME swoim wybranym. W trybie GNOME Shell nie ma takiej możliwości.

## Instalacja

GNOME 3 znajduje się w repozytorium [extra]. Grupa [gnome](https://www.archlinux.org/groups/x86_64/gnome/) zawiera bazowe środowisko i aplikacje, a grupa [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) zawiera resztę aplikacji. Prawdopodobnie nie będziesz potrzebować wszystkich aplikacji, więc przeczytaj opis każdej z nich przed instalacją (lub usuń je później).

**Musisz zainstalować grupę gnome**. Potem możesz doinstalować wybrane pakiety z grupy gnome-extra.

Przykład:

```
# pacman -S gnome

```

Wybierz aplikacje z gnome-extra, które chcesz zainstalować. Nie musisz instalować całej grupy.

```
# pacman -S gnome-extra

```

### Demon D-Bus

GNOME wymaga uruchomionego demona [D-Bus](/index.php?title=D-Bus_(Polski)&action=edit&redlink=1 "D-Bus (Polski) (page does not exist)"). Instrukcję instalacji znajdziesz na stronie [D-Bus](/index.php?title=D-Bus_(Polski)&action=edit&redlink=1 "D-Bus (Polski) (page does not exist)").

### Uruchomienie GNOME

Menedżer logowania **GDM** jest rekomendowany, aby uzyskać dobrą integrację środowiska. Inne menedżery logowania (inaczej menedżery wyświetlania) takie jak SLiM mogą być użyte zamiast GDM. Z artykułu o [menedżerach logowania](/index.php?title=Display_Manager_(Polski)&action=edit&redlink=1 "Display Manager (Polski) (page does not exist)") dowiesz się, jak uruchamiane są środowiska graficzne.

Menedżer logowania to proces mający dostęp do ustawień systemowych. [PolicyKit](/index.php?title=PolicyKit_(Polski)&action=edit&redlink=1 "PolicyKit (Polski) (page does not exist)") zajmuje się kontrolą dostępu do różnych części systemu.

```
# pacman -S gdm

```

Jeśli wolisz uruchamiać GNOME z konsoli, dodaj następującą linię do twojego pliku `~/.xinitrc`. Upewnij się, że jest to jedyna linia w tym pliku (usuń blok `if/fi` ze standardowego `~/.xinitrc`) i jedyna komenda zaczynająca się od `exec`. Zobacz artykuł [xinitrc](/index.php?title=Xinitrc_(Polski)&action=edit&redlink=1 "Xinitrc (Polski) (page does not exist)").

 `~/.xinitrc` 
```
 #TYLKO TĘ LINIĘ
 exec gnome-session

```

Po wstawieniu polecenia `exec`, GNOME zostanie uruchomione po wpisaniu `startx`.

## Używanie Shella

### Ściąga GNOME

Strona GNOME zawiera pomocną [ściągę GNOME Shell](https://live.gnome.org/GnomeShell/CheatSheet) wyjaśniającą przełączanie zadań, użycie klawiatury, zarządzanie oknami, korzystanie z panelu, trybu podglądu i wiele więcej.

### Ponowne uruchomienie shella

Po dokonaniu różnych zmian często będziesz proszony(a) o ponowne uruchomienie GNOME shell. Możesz się wylogować i zalogować ponownie, jednak można to zrobić prościej i szybciej. Naciśnij `Alt` + `F2`, potem wpisz `r` i naciśnij `Enter`

### Shell przestaje działać

Niektóre zmiany ustawień i/lub powtarzające się restarty Shella mogą spowodować, że Shell przestanie działać. W takim przypadku otrzymasz powiadomienie o błędzie i koniecznym wylogowaniu. Część zmian, przykładowo przełączanie pomiędzy ***GNOME Shell*** i ***trybem zastępczym***, nie może być dokonana z klawiatury; musisz się wylogować i zalogować ponownie, aby weszły w życie.

Powinno to być nawykiem, warto jednak przypomnieć, że ważne dokumenty powinny być zapisane (a jeśli trzeba, zamknięte) przed próbą ponownego uruchomienia Shella. Nie jest to koniecznie potrzebne; otwarte okna i dokumenty powinny pozostać nietknięte.

### Shell zawiesza się

Niektóre rozszerzenia shella mogą powodować zawieszania się GNOME Shell. W takim przypadku, przełącz się do innego terminala naciskając `Alt` + `Ctrl` + `F1`, zaloguj się i uruchom ponownie X za pomocą:

```
# pkill X

```

GNOME shell powinien uruchomić się automatycznie.

## Personalizacja GNOME

### Ogólny wygląd

GNOME 3 został "napisany od zera", jednak jak większość dużych projektów jest złożony z części pochodzących z różnych okresów. Nie ma **jednego** całościowego narzędzia konfiguracyjnego. Narzędzie *Ustawienia systemu* jest dużym ulepszeniem w porównaniu do poprzedniego panelu kontrolnego. *Ustawienia systemu* dobrze zaprojektowane, możesz jednak potrzebować większej kontroli nad wyglądem systemu.

Możesz być zaznajomiony z istniejącymi narzędziami konfiguracyjnymi: część z nich będzie działać; wiele nie będzie. Część ustawień nie jest łatwo dostępna do modyfikacji. Niewątpliwie, wiele ustawień zostanie przeniesionych do nowych narzędzi i/lub zostanie udostępniona do konfiguracji z biegiem czasu i rozwojem GNOME.

#### Gsettings

Nowe narzędzie **gsettings** przechowuje dane w postaci binarnej, w przeciwieństwie do poprzedników używających formatu XML. Tutorial [Personalizacja GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html) opisuje możliwości gsettings.

#### GNOME tweak tool

To narzędzie umożliwia zmianę fontów, tematów, przycisków na paskach tytułu i innych ustawień.

```
# pacman -S gnome-tweak-tool

```

Wersja 3.0.3 działa tylko z włączonym Gnome Shell (lub trybem zastępczym). [Raport o błędzie.](https://bugzilla.gnome.org/show_bug.cgi?id=647132)

#### Temat GTK3 w pliku settings.ini

Podobnie do `~/.gtkrc-2.0` w GTK2, można ustawić temat GTK3 w pliku `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`.

Zmienna `$XDG_CONFIG_HOME` jest zwykle ustawiona na `~/.config`

*Adwaita*, domyślny temat w GNOME 3, jest częścią [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard). Dodatkowe tematy GTK3 mogą być znalezione na [stronie Deviantart](http://browse.deviantart.com/customization/skins/linuxutil/desktopenv/gnome/gtk3/). Przykład:

 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 
```
  [Settings]
  gtk-theme-name = Adwaita
  gtk-fallback-icon-theme = gnome
  # ta opcja działa tylko jeśli wybrany temat ją obsługuje
  gtk-application-prefer-dark-theme = true
  # ustaw nazwę fontu i rozmiar
  gtk-font-name = Sans 10

```

Wymagane jest [ponowne uruchomienie Shella](#Ponowne_uruchomienie_shella), aby ustawienia weszły w życie. Więcej opcji GTK znajdziesz w [dokumentacji dewelopera GNOME](http://developer.gnome.org/gtk3/3.0/GtkSettings.html#GtkSettings.properties).

#### Temat ikon

Używając [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) w wersji 3.0.3 lub późniejszej, możesz umieścić dowolny temat ikon w `~/.icons`.

GNOME 3 jest kompatybilne z tematami ikon GNOME 2\.

Aby zainstalować nowy zestaw ikon, skopiuj go do `~/.icons`. Przykładowo:

```
$ cp -R /home/user/Desktop/moj_zestaw_ikon ~/.icons

```

Nowy temat *moj_zestaw_ikon* zostanie udostępniony do wyboru w zakładce *Motyw* `gnome-tweak-tool`.

Możesz też wybrać swój temat ikon bez użycia gnome-tweak-tool. Dodaj jego nazwę do pliku `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`. Pamiętaj, żeby nie używać "", inaczej ustawienie nie zostanie rozpoznane.

 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 
```
... poprzednie linie ...

gtk-icon-theme-name = moj_nowy_temat_ikon
```

### Nautilus

*Zobacz [Nautilus](/index.php?title=Nautilus_(Polski)&action=edit&redlink=1 "Nautilus (Polski) (page does not exist)").*

### Panel GNOME

#### Pokaż datę na górnym pasku

Domyślnie GNOME pokazuje na pasku tylko dzień tygodnia i czas. Można to zmienić używając następującego polecenia. Zmiana nastąpi natychmiast.

```
# gsettings set org.gnome.shell.clock show-date true

```

#### Ukryj niechciane ikony znajdujące się na pasku

Po instalacji GNOME, pewnie niechciane ikony mogą pojawić się na panelu. Mogą zostać usunięte odpowiednimi rozszerzeniami GNOME Shell lub poprzez edycję plików panelu GNOME.

##### Ukrywanie ikon z użyciem rozszerzeń

Aby usunąć ikonę dostępności, możesz użyć pakietu z [AUR](/index.php/AUR_(Polski) "AUR (Polski)") o nazwie [gnome-shell-extension-noa11y-git](https://aur.archlinux.org/packages/gnome-shell-extension-noa11y-git/).

Podobne rozszerzenia istnieją dla innych ikon, przykładowo zamieniając 'a11y' na 'bluetooth', otrzymamy rozszerzenie usuwające ikonę Bluetooth.

##### Manualna educja plików panelu GNOME

Dla przykładu, usuniemy ikonę **dostępności**. Usuń 'a11y' z linii AREA_ORDER i zakomentuj linię 'a11y' znajdującą się w AREA_SHELL_IMPLEMENTATION:

 `/usr/share/gnome-shell/js/ui/panel.js` 
```
const STANDARD_STATUS_AREA_ORDER = ['ally', 'keyboard', 'volume', 'network', 'bluetooth', 'battery', 'userMenu'];
const STANDARD_STATUS_AREA_SHELL_IMPLEMENTATION = {
    'a11y': imports.ui.status.accessibility.ATIndicator
    'volume': imports.ui.status.volume.Indicator,
    'battery': imports.ui.status.power.Indicator,
    'keyboard': imports.ui.status.keyboard.XKBIndicator,
    'userMenu': imports.ui.userMenu.UserMenuButton
};

```

Zmień na:

 `/usr/share/gnome-shell/js/ui/panel.js` 
```
const STANDARD_STATUS_AREA_ORDER = ['keyboard', 'volume', 'network', 'bluetooth' 'battery', 'userMenu'];
const STANDARD_STATUS_AREA_SHELL_IMPLEMENTATION = {
    //'a11y': imports.ui.status.accessibility.ATIndicator
    'volume': imports.ui.status.volume.Indicator,
    'battery': imports.ui.status.power.Indicator,
    'keyboard': imports.ui.status.keyboard.XKBIndicator,
    'userMenu': imports.ui.userMenu.UserMenuButton
};

```

Zapisz zmiany i uruchom Shell ponownie, aby zobaczyć rezultat:

1.  `Alt+F2`
2.  `r`
3.  `Enter`

#### Pokaż ikonę baterii

Aby włączyć wyświetlanie ikony baterii, [zainstaluj](/index.php/Pacman_(Polski) "Pacman (Polski)") [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager) z [Oficjalnych Repozytoriów](/index.php?title=Official_Repositories_(Polski)&action=edit&redlink=1 "Official Repositories (Polski) (page does not exist)").

#### Wyłącz "Uśpij" w menu statusu i GDM

Zainstaluj [rozszerzenie GNOME Shell](#GNOME_shell_extensions) `alternative status menu` znajdujące się w pakiecie [gnome-shell-extension-alternative-status-menu](https://www.archlinux.org/packages/?name=gnome-shell-extension-alternative-status-menu).

#### Wyłącz opóźnienie przy wylogowywaniu

Poniższe ustawienie wyłącza pytanie o potwierdzenie i sześćdziesięcio-sekundowe opóźnienie przy wylogowywaniu.

To pytanie pojawia się przy wylogowywaniu z użyciem menu statusu. To ustawienie dotyczy także pytania przy ***Wyłącz komputer***. Nie dotyczy ono całego systemu; działa tylko dla użytkownika, który je zmienił. Zmiana jest widoczna natychmiast po wydaniu polecenia.

```
$ gsettings set org.gnome.SessionManager logout-prompt 'false'

```

#### Pokaż monitor systemu

Zainstaluj rozszerzenie [gnome-shell-system-monitor-applet-git](https://aur.archlinux.org/packages/gnome-shell-system-monitor-applet-git/) dostępne w [AUR](/index.php/AUR_(Polski) "AUR (Polski)").

#### Pokaż informacje o pogodzie

Zainstaluj [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/) z [AUR](/index.php/AUR_(Polski) "AUR (Polski)").

### Widok podglądu

#### Usuń wpisy z widoku Programów

Podobnie jak inne środowiska graficzne, GNOME używa plików .desktop, aby wypełnić widok Programy. Te pliki tekstowe znajdują się w **`/usr/share/applications`**. Nie można ich edytować z poziomu menedżera plików ‒ Nautilus nie traktuje ich jako pliki tekstowe. Użyj terminala do wyświetlania lub edycji plików .desktop.

```
# ls /usr/share/applications
# nano /usr/share/applications/foo.desktop

```

Jeśli zmiana ma objąć cały system, wyedytuj plik w **`/usr/share/applications`**. Jeśli zmiana ma być lokalna, sporządź kopię pliku *foo.desktop* w swoim folderze domowym.

```
$ cp /usr/share/applications/foo.desktop ~/.local/share/applications/

```

Wyedytuj plik .desktop według własnych potrzeb.

**Note:** Usunięcie pliku .desktop nie usuwa aplikacji. Zamiast tego usuwa jej integrację z systemem: typy MIME, skróty, itp.

Następujące polecenie dopisuje jedną linię do pliku .desktop file i ukrywa go z widoku Programów:

```
$ echo "NoDisplay=true" >> foo.desktop

```

#### Zmniejsz rozmiar ikon aplikacji

Jednym z dyskusyjnych wyborów projektantów GNOME jest ich wybór dużych ikon w widoku Programów. Jest on bardzo niewygodny przy korzystaniu z małych ekranów zawierających dużo ikon aplikacji. Możliwe jest zmniejszenie rozmiaru ikon. Można to zrobić edytując temat GNOME Shell.

Wyedytuj bezpośrednio pliki systemowe (zrób wcześniej ich kopię) lub skopiuj pliki tematu do swojego folderu domowego. Jeśli używasz domyślnego tematu, wyedytuj **`/usr/share/gnome-shell/theme/gnome-shell.css`**

Jeśli używasz innego tematu, wyedytuj **`/usr/share/themes/<Temat>/gnome-shell/gnome-shell.css`**

Wyedytuj *gnome-shell.css* i zamień następujące wartości. Następnie [uruchom ponownie GNOME shell](#Ponowne_uruchomienie_shella).

 `gnome-shell.css` 
```
 .icon-grid {
     spacing: 18px;
     -shell-grid-item-size: 82px;
 }

 .icon-grid .overview-icon {
     icon-size: 48px;
 }

```

#### Wyłącz "gorący róg" włączający widok Podglądu

Aby wyłączyć automatyczne włączanie widoku Podglądu przy dotknięciu rogu ekranu, wyedytuj **`/usr/share/gnome-shell/js/ui/layout.js`** (ten plik nazywał się *panel.js* w Gnome 3.0.x) :

 `layout.js` 
```
 this._corner = new Clutter.Rectangle({ name: 'hot-corner',
                                       width: 1,
                                       height: 1,
                                       opacity: 0,
                                       reactive: true });icon-size: 48px;
 }

```

i ustaw *reactive* na *false*. GNOME Shell musi zostać uruchomiony ponownie.

### Pasek tytułu

#### Zmniejsz wysokość paska tytułu

Otwórz plik `/usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml`, znajdź `title_vertical_pad` i zmień jego wartość z 14 na 0\. Następnie [uruchom ponownie GNOME Shell.](#Ponowne_uruchomienie_shella)

Aby przywrócić domyślne wartości, [zainstaluj](/index.php/Pacman_(Polski) "Pacman (Polski)") pakiet [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) z [[Official Repositories_(Polski)|oficjalnych repozytoriów].

#### Zmień kolejność przycisków na pasku tytułu

Kolejność przycisków można ustawić z użyciem **dconf-editor.**

Przykładowo, przeniesiemy przyciski zamknięcia i minimalizacji na lewą stronę paska. Otwórz **dconf-editor** i znajdź klucz ***org.gnome.shell.overrides.button_layout***. Zmień jego wartość na **`close,minimize:`** (dwukropek oznacza obszar pomiędzy lewą i prawą stroną paska). Nie możesz użyć danego przycisku więcej niż raz. Pamiętaj też, że niektóre przyciski zostały uznane za przestarzałe. [Uruchom shell ponownie](#Ponowne_uruchomienie_shella) aby zobaczyć nowy układ przycisków.

#### Ukryj pasek tytułu przy maksymalizacji okna

```
# sed -i -r 's|(<frame_geometry name="max")|\1 has_title="false"|' /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

[Uruchom GNOME Shell ponownie](#Ponowne_uruchomienie_shella). Przywrócenie okna z maksymalizacji może być kłopotliwe po zastosowaniu tej porady.

Użyj `Alt+Space`, `Alt+F5` lub `Alt+F10` aby przywrócić okno do normalnego rozmiaru.

Aby zapobiec nadpisaniu `metacity-theme-3.xml` przy aktualizacji pakietu [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard), dodaj jego nazwę do `/etc/pacman.conf` w linii `NoUpgrade`.

 `/etc/pacman.conf` 
```
... poprzednie linie ...

# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
# IgnorePkg   =
# IgnoreGroup =

NoUpgrade = usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml    # Nie dodawaj ukośnika na początku ścieżki

... pozostałe linie ...
```

Oryginalne wartości możesz przywrócić instalując pakiet [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard).

#### Zmiana tła logowania

Po wyeksportowaniu potrzebnych zmiennych w spodób opisany powyżej, możesz przystąpić do zmiany ustawień GDM.

Najprostszym sposobem na zmianę wszystkich ustawień jest uruchomienie graficznego edytora poleceniem:

```
$ dconf-editor

```

Lokalizacja każdego ustawienia jest taka sama jak w przykładach w linii poleceń, które znajdują się poniżej:

Przykładowe polecenia służące do odczytania lub zmiany pliku używanego przed GDM jako tapeta:

```
 $  GSETTINGS_BACKEND=dconf gsettings get org.gnome.desktop.background picture-uri
 $  GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-uri 'file:///usr/share/backgrounds/gnome/SundownDunes.jpg'

 $  GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-options 'zoom'
 ## Możliwe wartości: centered, none, scaled, spanned, stretched, wallpaper, zoom
```

**Note:** Musisz wybrać plik, który może być odczytany przez użytkownika "gdm". GDM nie może czytać plików z Twojego katalogu domowego.

Dostępne jest graficzne narzędzie do zmiany tematów (GTK3, ikon, kursora), tapety i kilku innych opcji. Zainstaluj pakiet [gdm3setup](https://aur.archlinux.org/packages/gdm3setup/) z AUR, aby go użyć.

#### Większa czcionka przy logowaniu

Ta opcja powiększa czcionkę o wybrany współczynnik. Ta sama metoda jest używana przez *Menedżer dostępności* w GNOME.

Musisz wyeksportować [zmienne sesji GDM](#Ekran_logowania) przed kontynuacją.

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.interface text-scaling-factor '1.25'

```

#### Wyłączenie dźwięków

To ustawienie wyłącza dźwięki słyszane przy ustawianiu głośności z użyciem klawiatury. Najpierw musisz wyeksportować zmienne sesji GDM.

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.sound event-sounds 'false'

```

Jeśli powyższe polecenie nie działa lub nie możesz wyeksportować zmiennych GDM, możesz po prostu wyciszyć lub zmniejszyć głośność dźwięków będąc w ekranie logowania używając przycisków multimedialnych.

#### Interaktywny przycisk włączenia komputera

Domyślnie naciśnięcie przycisku włączenia komputera powoduje jego uśpienie. ***Wyłączenie*** lub ***Wyświetlenie pytania*** to lepszy wybór. Najpierw wyeksportuj zmienne sesji GDM jak [pokazano wcześniej](#Ekran_logowania).

```
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-power 'interactive'
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-hibernate 'interactive'
 $ gsettings list-recursively org.gnome.settings-daemon.plugins.power

```

**Warning:** Demon [acpid](/index.php?title=Acpid_(Polski)&action=edit&redlink=1 "Acpid (Polski) (page does not exist)") także obsługuje zdarzenia "przycisk włączenia" i "przycisk hibernacji". Działanie obydwu naraz może prowadzić do nieprzewidzianych rezultatów.

#### Układ klawiatury w GDM

GDM nie wie o Twoich ustawieniach klawiatury w GNOME 3\. Aby zmienić układ klawiatury uźywany przez GDM, ustaw go w konfiguracji Xorg. Odwołaj się do tej sekcji [Przewodnika Początkującego.](/index.php/Beginners%27_guide_(Polski)#Nieamerykański_układ_klawiatury "Beginners' guide (Polski)")

## Różne ustawienia

### Automatyczne uruchamianie programu po zalogowaniu

Wybierz programy, które mają uruchomić się po zalogowaniu używając `gnome-session-properties`. To narzędzie jest częścią pakietu [gnome-session](https://www.archlinux.org/packages/?name=gnome-session).

```
$ gnome-session-properties

```

### Editing applications menu

[gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) dostarcza *gmenu-simple-editor*, który potrafi pokazywać/ukrywać elementy menu.

[alacarte](https://www.archlinux.org/packages/?name=alacarte) z AUR umożliwia edycję menu i dodawanie/edycję wpisów programów.

### Część 'Ustawień systemu' nie jest zachowywana

GNOME 3 używa [systemd](http://fedoraproject.org/wiki/Systemd) (demon uruchamiania dla Linuksa) z nowoczesnymi możliwościami. Poprzednio programy GNOME były dostosowywane do używania `init` znajdującego się w Archu do zarządzania ustawieniami. Zaprzestano tego z powodu kłopotliwego utrzymania i przechodzenia na nowy system startowania systemu (więcej przeczytasz [tutaj](https://bbs.archlinux.org/viewtopic.php?pid=1115208#p1115208)). Ustawienia, które nie są zachowywane to **Data i czas**, dodawanie profili ICC w menu **Kolor** i inne.

**Note:** systemd nie został jeszcze dokładnie przetestowany. Używanie go nie jest rekomendowane dla większości użytkowników.

Używanie systemd jest konieczne do przywrócenia tej funkcjonalności. Jak to zrobić znajdziesz w artykule [systemd](/index.php?title=Systemd_(Polski)&action=edit&redlink=1 "Systemd (Polski) (page does not exist)").

### Włącz NumLock przy logowaniu

[Zainstaluj](/index.php/Pacman_(Polski) "Pacman (Polski)") [numlockx](https://www.archlinux.org/packages/?name=numlockx) z [oficjalnych repozytoriów](/index.php?title=Official_Repositories_(Polski)&action=edit&redlink=1 "Official Repositories (Polski) (page does not exist)"). Następnie dodaj `numlockx` do isty programów uruchamianych razem z GNOME.

```
$ gnome-session-properties

```

Powyższe polecenie aplet **Preferencje programów startowych**. Kliknij ***Dodaj*** i wprowadź:

| Nazwa: | *Numlockx* |
| Polecenie: | */usr/bin/numlockx on* |
| Komentarz: | *Włącza numlock.* |

Nie jest to ustawienie systemowe. Powtórz je dla każdego użytkownika chcącego uruchamiać NumLock po zalogowaniu.

### Włącz przesuwanie okien dialogowych

Domyślna konfiguracja nie pozwala na przesuwanie okien dialogowych co może powodować problemy w niektórych przypadkach. Aby to zmienić, uruchom gconf-editor i zmień opcję:

```
/desktop/gnome/shell/windows/attach_modal_dialogs

```

Uruchom ponownie Shell aby zmiana weszła w życie.

### Rozszerzenia GNOME Shell

GNOME Shell może być spersonalizowany używając rozszerzeń napisanych przez innych użytkowników. Oferują one takie funkcje jak dock czy widget do zmiany tematu.

Rozszerzenia są dostępne na stronie [gnome.org](https://extensions.gnome.org/). Mogą być przeglądane i instalowane z użyciem przeglądarki.

Informacje na temat rozszerzeń można znaleźć na stronie [WEBUPD8](http://www.webupd8.org/2011/04/gnome-shell-extensions-additional.html). Najnowsze artykuły można wyszukać używając tego [linku](http://www.webupd8.org/search/label/gnome%20shell%20extensions?max-results=20).

Useful extensions provided in the [AUR](/index.php/AUR "AUR"):

| [gnome-shell-extension-presentation-mode-git](https://aur.archlinux.org/packages/gnome-shell-extension-presentation-mode-git/) | Dodaje możliwość wyłączenia wygaszacza ekranu w menu zasilania (ikona baterii). |
| [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/) | Wyświetla informacje pogodowe. |
| [gnome-shell-extension-alternative-status-menu-git](https://aur.archlinux.org/packages/gnome-shell-extension-alternative-status-menu-git/) | Dodaje "Hibernuj" i "Wyłącz komputer" do menu statusu. |
| [gnome-shell-extension-theme-selector](https://aur.archlinux.org/packages/gnome-shell-extension-theme-selector/) | Wybierz temat w widoku Podglądu.

Aby zainstalować własny temat GNOME, musisz zainstalować pakiet [gnome-shell-extension-user-theme-git](https://aur.archlinux.org/packages/gnome-shell-extension-user-theme-git/) z AUR.

 |
| [gnome-shell-frippery](https://aur.archlinux.org/packages/gnome-shell-frippery/) | Nieoficjalna paczka rozszerzeń dostarczająca funkcje z GNOME 2. |

[Uruchom ponownie GNOME Shell](#Ponowne_uruchomienie_shella) po instalacji rozszerzenia. Zobacz [when an extension breaks GNOME](#When_an_extension_breaks_GNOME) po rozwiązania możliwych problemów.

### Domyślny menedżer plików/zastąp Nautilusa

Możesz skonfigurować GNOME do używania innego menedżera plików edytując

```
/usr/share/applications/nautilus.desktop

```

i zamieniając

```
Exec=nautilus %U

```

na wybrany menedżer, przykładowo:

```
Exec=thunar /

```

### Domyślny terminal

`gsettings` (który zastąpił `gconftool-2`) jest używany do zmiany domyślnego terminala. To ustawienie wpływa na *nautilus-open-terminal* (roszerzenie Nautilusa). Aby ustawić [urxvt](/index.php?title=Rxvt-unicode_(Polski)&action=edit&redlink=1 "Rxvt-unicode (Polski) (page does not exist)") domyślnym terminalem, uruchom:

```
gsettings set org.gnome.desktop.default-applications.terminal exec urxvtc
gsettings set org.gnome.desktop.default-applications.terminal exec-arg "'-e'"

```

**Note:** Opcja `-e` oznacza uruchomienie polecenia. Kiedy *nautilus-open-terminal* uruchamia `urxvtc`, dodaje polecenie `cd` na końcu linii, dlatego nowy terminal zawiera katalog, z którego został uruchomiony. Inne terminale mogą wymagać innej (możliwe, że pustej) opcji `exec-arg`.

### Środkowy przycisk myszy

Domyślnie GNOME 3 wyłącza emulację środkowego przycisku myszy niezależnie od ustawień [Xorg](/index.php/Xorg_(Polski) "Xorg (Polski)") (**Emulate3Buttons**). Aby włączyć emulację środkowego przycisku myszy, uruchom:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### Przyciemnianie ekranu

Domyślnie GNOME 3 przyciemnia ekran po 10 sekundach braku aktywności niezależnie od rodzaju zasilania:

```
gsettings get org.gnome.settings-daemon.plugins.power idle-dim-time

```

Aby zmienić tę wartość, uruchom polecenie

```
gsettings set org.gnome.settings-daemon.plugins.power idle-dim-time <liczba>

```

gdzie <liczba> to wartość w sekundach

### Alternatywny menedżer okien

Możesz użyć alternatywnego menedżera okien w GNOME poprzez [wymuszenie trybu zastępczego](#Enabling_fallback_mode) i stworzenie dwóch plików:

**Note:** Xmonad jest tylko przykładem, działa to także z innymi menedżerami okien.
 `/usr/share/gnome-session/sessions/xmonad.session` 
```
[GNOME Session]
Name=Xmonad session
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=xmonad
DefaultProvider-notifications=notification-daemon
```
 `/usr/share/xsessions/xmonad-gnome-session.desktop` 
```
[Desktop Entry]
Name=Xmonad GNOME
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=gnome-session --session=xmonad
Type=XSession
```

Przy następnym logowaniu, powinieneś(aś) móc wybrać sesję *Xmonad GNOME*.

Jeśli plik .desktop dla Twojego menedżera nie istnieje, musisz go stworzyć. Przykład dla [wmii](/index.php?title=Wmii_(Polski)&action=edit&redlink=1 "Wmii (Polski) (page does not exist)"):

 `/usr/share/applications/wmii.desktop` 
```
[Desktop Entry]
Version=1.0
Type=Application
Name=wmii
TryExec=wmii
Exec=wmii
```

Po więcej informacji, zobacz [ten artykuł o awesome jako menedżer okien w GNOME](http://makandra.com/notes/1367-running-the-awesome-window-manager-within-gnome).

## Ukryte funkcje

GNOME 3 posiada wiele ukrytych opcji, które możesz modyfikować z użyciem **dconf-editor.** GNOME 3 wspiera także **gconf-editor** dla ustawień, które nie zostały jeszcze przeniesione do dconf.

### Zmiana skrótów klawiszowych

Najpierw użyj **dcon-editor**i zaznacz `can-change-accels` w kluczu o nazwie *org.gnome.desktop.interface.*

Dla przykładu zmienimy skrót służący do przenoszenia plików do kosza w Nautilusie.

Domyślnie ten skrót to `Ctrl` + `Delete`.

*   Otwórz Nautilusa, zaznacz dowolny plik i naciśnij **Edycja** na pasku menu.
*   Przejedź kursorem nad opcję *Przenieś do kosza*.
*   Trzymając tam kursor, naciśnij `Delete`. Domyślny skrót został usunięty.
*   Naciśnij klawisze, które mają stać się nowym skrótem.
*   Naciśnij `Delete`, aby nowym skrótem był klawisz Delete.

Dopóki nie zaznaczysz pliku lub folderu, opcja *Przenieś do kosza* będzie nieaktywna. Na koniec, wyłącz opcję `can-change-accels` aby zapobiec przypadkowym zmianom skrótów klawiszowych.

### Wyłączenie komputera w menu statusu

Projektanci GNOME usunęli opcję *Wyłącz komputer* z menu statusu. Aby wyłączyć komputer używając menu statusu, otwórz menu i przytrzymaj klawisz `Alt`, co zmieni opcję ***Uśpij*** na ***Wyłącz komputer***.

Jeśli wyłączysz "Uśpij" w menu dla całego systemu jak opisano [powyżej](#Wyłącz_"Uśpij"_w_menu_statusu_i_GDM) nie musisz tego robić.

Innym wyjściem jest zainstalowanie rozszerzenia *Alternative Status Menu*. Zobacz paragraf o rozszerzeniach shella. Rozszerzenie *Alternative Status Menu* instaluje nowe menu z dostępną opcją ***Power Off***.

## Zintegrowany komunikator (Empathy)

Empathy nie będzie działać poprawnie dopóki nie zostanie zainstalowana grupa pakietów [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) lub co najmniej jeden z backendów (przykładowo [telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble), [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze)).

Te pakiety nie są zawarte w domyślnej instalacji GNOME. Możesz zainstalować telepathy i dowolny backend używając:

```
# pacman -S telepathy

```

Bez telepathy, Empathy nie otworzy okna zarządzania kontami i zawiesi się. Jeśli tak się stanie -- nawet po poprawnym zamknięciu Empathy -- aplikacja /usr/bin/empathy-accounts może nadal działać i musi zostać zakończona przed dodaniem nowego konta.

Zobacz opisy komponentów telepathy na stronie [Freedesktop.org Telepathy Wiki](http://telepathy.freedesktop.org/wiki/Components).

## Wymuszenie trybu zastępczego

Twoja sesja automatycznie uruchomi się w trybie zastępczym jeśli **gnome-shell** nie jest zainstalowane lub posiadany sprzęt nie jest w stanie obsłużyć akceleracji graficznej -- przy uruchamianiu na starym sprzęcie lub w maszynie wirtualnej.

Jeśli chcesz korzystać z trybu zastępczego mając zainstalowane **gnome-shell**, wykonaj następujące kroki:

1.  Otwórz **gnome-control-center**,
2.  Kliknij ikonę *Szczegóły*,
3.  Kliknij zakładkę *Grafika*,
4.  Włącz *Wymuszenie trybu zastępczego*.

Możesz też wybrać typ sesji korzystając z terminala i polecenia *gsettings*:

```
$ gsettings set org.gnome.desktop.session session-name 'gnome-fallback'

```

Zaloguj się ponownie aby zobaczyć zmiany.

Żeby wyłączyć tryb zastępczy (uruchomić normalny GNOME Shell) użyj wartości 'gnome' zamiast 'gnome-fallback'.

## Rozwiązania problemów

### Logowanie do GNOME zajmuje bardzo dużo czasu

Sprawdź, czy włączona jest opcja *PulseAudio Network* w **paprefs**. Jeśli jakakolwiek sieć audio jest włączona, GNOME zawiesza się na około minutę podczas logowania.

Możliwym rozwiązaniem jest stworzenie nowego konta użytkownika i zalogowanie się na to konto. Innym wyjściem jest przeniesienie folderów `~/.gconf`, `~/.gconfd` i `~/.config/dconf` w inne miejsce. Zaloguj się ponownie i zobacz, czy opóźnienie zniknęło.

Jeśli tak, określ które ustawienie je powodowało metodą prób i błędów.

### Kiedy rozszerzenie zepsuje GNOME

Jeśli włączenie rozszerzenia Shella powoduje awarię GNOME, najpierw usuń rozszerzenia *user-theme* i *auto-move-windows* z folderu instalacji rozszerzeń.

Mogą to być **`~/.local/share/gnome‑shell/extensions`**, **`/usr/share/gnome‑shell/extensions`**, lub **`/usr/local/share/gnome‑shell/extensions`**. Sprawdź, które rozszerzenie powodowało problem metodą prób i błędów.

### Rozszerzenie nie działa po aktualizacji GNOME

Znajdź folder, w którym znajduje się to rozszerzenie. Może to być **`~/.local/share/gnome-shell/extensions`** lub **`/usr/share/gnome-shell/extensions`**.

Wyedytuj każdy plik **`metadata.json`** znajdujący się w podfolderach rozszerzenia.

| Wstaw: | **`"shell-version": ["3.0"]`** |
| Zamiast (przykładowo): | **`"shell-version": ["3.0.1"]`** |
| Możesz także użyć: | **`"shell-version": ["3.0.0", "3.0.1", "3.0.2"]`** |

**"3.0"** to najlepsze wyjście. Oznacza, że rozszerzenie działa z każdą wersją ***3.0.x*** GNOME Shell.

### Ekran nie jest blokowany po wybudzeniu

Blokowanie ekranu działa tylko, jeśli uśpiłeś(aś) system korzystając z menu statusu GNOME. Jeśli korzystałeś(aś) z przycisku zasilania, ekran nie będzie zablokowany po wybudzeniu. Problemem jest błąd w konfiguracji dconf.

Otwórz *dconf-editor* i odznacz **`lock-use-screensaver`** w kluczu *org.gnome.power-manager.*

```
# gsettings set org.gnome.power-manager lock-use-screensaver 'false'

```

Twój ekran powinien być blokowany niezależnie od sposobu usypiania komputera.

### Klawisz "Windows"

Domyślnie w GNOME ten klawisz jest zmapowany jako "overlay-key" i włącza Podgląd. Możesz usunać to mapowanie, aby uwolnić klawisz `Windows` (nazywany także `Mod4`), w Gnome nazwany `Super_L`, używając `gsettings`.

Przykład: `gsettings set org.gnome.mutter overlay-key 'Foo';`. Jeśli pominiesz **Foo**, usuniesz klawisz przypisany do tej funkcji.

**Note:** Gnome używa też `Alt+F1` do uruchomienia Podglądu.

### Skróty klawiszowe nie działają przy uruchomionym conky

Skróty klawiszowe, takie jak Alt+F2, Alt+F1 i klawisze multimedialne nie działają, jeśli conky jest jedyną działającą aplikacją. Jednak jeśli inna aplikacja, np. gedit jest uruchomion, skróty działają.

Rozwiązanie: edycja .conkyrc

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

### Aplikacje GTK2+ nie uruchamiają się (Naruszenie ochrony pamięci)

Zwykle dzieje się tak, jeśli **oxygen-gtk** jest zainstalowany. Ten temat wydaje się być w konflikcie z GNOME 3 lub ustawieniami GTK3\. Kiedy **oxygen-gtk** jest ustawiony jako temat GTK2, aplikacje GTK2 przestają działać z takimi błędami:

```
 (firefox-bin:14345): GLib-GObject-WARNING **: invalid (NULL) pointer instance

(firefox-bin:14345): GLib-GObject-CRITICAL **: g_signal_connect_data: assertion `G_TYPE_CHECK_INSTANCE (instance)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_colormap_get_visual: assertion `GDK_IS_COLORMAP (colormap)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed
(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_window_new: assertion `GDK_IS_WINDOW (parent)' failed
Naruszenie ochrony pamięci

```

Obejściem problemu jest usunięcie **oxygen-gtk** i korzystanie z innego tematu dla aplikacji.

### Sterownik ATI Catalyst powoduje artefakty

Na ten moment, Catalyst nie powinien być używany razem z GNOME Shell. Otwarty sterownik, xf86-video-ati, działa poprawnie z GNOME 3.

**Note:** Poprawka jest obiecana razem z wydaniem Catalyst 11.9\. Zobacz [http://ati.cchtml.com/show_bug.cgi?id=99](http://ati.cchtml.com/show_bug.cgi?id=99)

### Sterownik xf86-video-ati: migotanie od czasu do czasu

Jeśli używasz ten sterownik, Twój pulppit może migotać przy najechaniu kursorem na prawy dolny róg ekranu, a także podczas ładowania gdm. Wpisz to do pliku **`/etc/X11/xorg.conf.d/20-radeon.conf`** i sprawdź, czy problem zniknął:

```
Section "Device"
       Identifier "Radeon"
       Driver "radeon"
       Option "EnablePageFlip" "off"
EndSection

```

### Sterownik xf86-video-intel "rwie" obraz niezależnie od ustawienia VSYNC

Dodaj to do pliku /etc/environment:

CLUTTER_PAINT=disable-clipped-redraws:disable-culling Odwiedź [https://bugzilla.gnome.org/show_bug.cgi?id=657071#c2](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c2) po więcej szczegółów.

### Okna otwierają się za innymi oknami używając wielu monitorów

To najprawdopodobniej błąd w gnome-shell. Odznaczenie "workspaces_only_on_primary" w desktop/gnome/shell/windows używając gconf-editor rozwiązuje ten problem.

### Wiele monitorów i rozszerzenie dock

Jeśli korzystasz z wielu monitorów używając NVIDIA Twinview, rozszerzenie dock może ukrywać się pomiędzy monitorami. Może wyedytować pliki rozszerzenia aby ustalić wybrane położenie docka.

Otwórz **/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js** i znajdź tę linię:

```
this.actor.set_position(primary.width-this._item_size-this._spacing-2, (primary.height-height)/2);

```

Pierwszy parametr oznacza pozycję docka na osi X. Odejmując 15 pikseli zamiast dwóch, dock jest poprawnie wyświetlany na moim głównym monitorze. Wypróbuj różne wartości X, Y, dopóki dock nie będzie poprawnie wyświetlany.

```
this.actor.set_position(primary.width-this._item_size-this._spacing-15, (primary.height-height)/2);

```

### Brak dźwięków zdarzeń Empathy i innych programów

Jeśli używasz [OSS](/index.php?title=OSS_(Polski)&action=edit&redlink=1 "OSS (Polski) (page does not exist)"), zainstaluj [libcanberra-oss](https://aur.archlinux.org/packages/libcanberra-oss/) z [AUR](/index.php/AUR_(Polski) "AUR (Polski)").

### Zmiana skrótów przez can-change-accels nie działa

Możliwa jest także manualna zmiana klawiszy poprzez plik 'accel map' aplikacji. Znajduje się w różnych miejscach w zależności od aplikacji. Przykładowo, Thunar przechowuje go w `~/.config/Thunar/accels.scm`, a Nautilus w `~/.gnome2/accels/nautilus`. Plik powinien zawierać listę dostępnych skrótów, każda linia zaczynająca się od ";" jest traktowana jako komentarz i trzeba go usunąć, aby stała się aktywna.

### Panele nie reagują na kliknięcie prawym przyciskiem w trybie zastępczym

Sprawdź klucz /apps/metacity/general/mouse_button_modifier w dconf-editor. Ten klawisz modyfikujący (`Alt`, `Super`, etc.) używany przez normalne okna jest także używany przez panele i ich aplety.

### Skrót klawiszowy "Pokaż pulpit" nie działa

Deweloperzy GNOME uznali ten skrót za bug (zobacz [https://bugzilla.gnome.org/show_bug.cgi?id=643609](https://bugzilla.gnome.org/show_bug.cgi?id=643609)) z powodu zaniechania minimalizacji. Aby skrót działał, przypisz ponownie ALT+STRG+D do następującej opcji:

```
Ustawienia systemu --> Klawiatura --> Skróty --> Nawigacja --> Ukrycie wszystkich zwykłych okien

```

### Nautilus się nie uruchamia

1.  Naciśnij `ALT`+`F2`
2.  Wpisz `gnome-tweak-tool`
3.  Wybierz zakładkę *Pulpit*
4.  Wyłącz opcję *Have file manager handle the desktop*.

### Epiphany nie odtwarza filmów we Flashu

Adobe Flash Player jest zabugowany i nie działa bezpośrednio w Epiphany. Zobacz [Epiphany](/index.php?title=Epiphany_(Polski)&action=edit&redlink=1 "Epiphany (Polski) (page does not exist)") po obejście tego problemu.

### Nie można zastosować zapisanej konfiguracji monitorów

Jeśli napotkasz taki komunikat, spróbuj wyłączyć plugin xrandr gnome-settings-daemon:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### Włączani touchpada nie działa

Część laptopów posiada przycisk do włączania/wyłączania touchpada, żeby móc wygodnie pisać. Czasami GNOME potrafi wyłączyć touchpad, ale nie potrafi go włączyć. Jeśli Twój touchpad się zablokuje, spróbuj włączyć go w ten sposób:

1.  Otwórz terminal. Możesz to zrobić wciskając `Alt+F2`, wpisując `gnome-terminal` i naciskając `Enter`.
2.  Wpisz następujące polecenie

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### Ctrl+v wkleja ścieżkę zamiast pliku w Nautilusie

Jeśli napotkałeś(aś) taki problem, wyedytuj `~/.gnome2/accels/nautilus` znajdując dwie linie dotyczące `Ctrl+v`:

 `~/.gnome2/accels/nautilus` 
```
(gtk_accel_path "<Actions>/DirViewActions/Paste" "<Control>v")
...
(gtk_accel_path "<Actions>/ClipboardActions/Paste" "<Control>v")

```

Usunięcie drugiej z nich powinno naprawić problem. Po aktualizacji ten plik może zostać przywrócony.

Innym wyjściem jest przypisanie innej kombinacji klawiszy do jednej z tych akcji.

**Note:** Ten problem został naprawiony w GNOME 3.2.x.

### Nie mogę połączyć się z zabezpieczonymi sieciami Wi-Fi

Możesz zobaczyć listę dostępnych sieci, jednak wybranie zabezpieczonej sieci nie wyświetla pytania o hasło do niej. Musisz [zainstalować](/index.php/Pacman_(Polski) "Pacman (Polski)") [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet). Zobacz [NetworkManager w GNOME](/index.php?title=NetworkManager_(Polski)&action=edit&redlink=1 "NetworkManager (Polski) (page does not exist)").

### "Any command has been defined 33"

Jeśli po naciśnięciu przycisku `Print Screen` (czasami oznaczonego jako `PrntScr` lub `PrtSc`) otrzymujesz "Any command has been defined 33", [zainstaluj](/index.php/Pacman_(Polski) "Pacman (Polski)") [metacity](https://www.archlinux.org/packages/?name=metacity).

### GDM i GNOME używają kursorów X11

Aby naprawić ten problem, jako root stwórz plik `/usr/share/icons/default/index.theme` (stwórz katalog `/usr/share/icons/default` jeśli nie istnieje) i wpisz do niego:

 `/usr/share/icons/default/index.theme` 
```
[Icon Theme]
Inherits=Adwaita

```

Note: Zamiast "Adwaita", możesz wybrać inny temat kursorów (np. Human). Możesz też zainstalować [gnome-cursors-fix](https://aur.archlinux.org/packages/gnome-cursors-fix/) z [AUR](/index.php/AUR_(Polski) "AUR (Polski)").

### Tracker & Dokumenty nie pokazują lokalnych plików

Żeby Tracker (i Dokumenty) mogły znaleźć Twoje pliki, muszą one być przechowywane w odpowiednich folderach. Jeśli Twoje dokumenty znajdują się w jednym z katalogów XDG (takich jak "Dokumenty" czy "Muzyka"), zainstaluj [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) i uruchom:

```
 # xdg-user-dirs-update

```

To polecenie stworzy odpowiednie katalogi, jeśli jeszcze nie istnieją i utworzy pliki konfiguracyjne dla Trackera.

## Linki zewnętrzne

*   [Oficjalna strona GNOME](http://www.gnome.org/)
*   Tematy, ikony i tła:
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME Look](http://www.gnome-look.org/)
*   Programy GTK/GNOME:
    *   [GNOME Files](http://www.gnomefiles.org/)
    *   [GNOME Project Listing](http://www.gnome.org/projects/)