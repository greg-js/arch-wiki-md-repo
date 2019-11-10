Ze [strony GTK+](http://www.gtk.org):

	GTK+, lub GIMP Toolkit, to wieloplatformowy zestaw narzędzi do tworzenia graficznych interfejsów użytkownika. Oferując kompletny zestaw widżetów, GTK+ jest odpowiedni dla projektów, od małych jednorazowych narzędzi do kompletnych zestawów aplikacji.

GTK+, GIMP Toolkit, został stworzony przez [GNU Project](/index.php/GNU_Project "GNU Project") dla [GIMPa](/index.php/GIMP "GIMP"), ale obecnie jest bardzo popularnym zestawem narzędzi z bindingami dla wielu języków. W tym artykule omówimy narzędzia używane do konfigurowania motywu, stylu, ikony, czcionki i rozmiaru czcionki GTK+, a także ręcznej konfiguracji szczegółów.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalacja](#Instalacja)
*   [2 Motywy](#Motywy)
    *   [2.1 GTK+ i Qt](#GTK+_i_Qt)
*   [3 Narzędzia konfiguracyjne](#Narzędzia_konfiguracyjne)
*   [4 Konfiguracja](#Konfiguracja)
    *   [4.1 Podstawowa konfiguracja motywu](#Podstawowa_konfiguracja_motywu)
    *   [4.2 Pomiń ostrzeżenie dotyczące dostępności](#Pomiń_ostrzeżenie_dotyczące_dostępności)
    *   [4.3 Ciemny wariant motywu](#Ciemny_wariant_motywu)
    *   [4.4 Skróty klawiszowe](#Skróty_klawiszowe)
        *   [4.4.1 Skróty klawiszowe Emacs](#Skróty_klawiszowe_Emacs)
    *   [4.5 Opóźnienie menu GNOME](#Opóźnienie_menu_GNOME)
    *   [4.6 Zmniejsz wielkość widżetów](#Zmniejsz_wielkość_widżetów)
    *   [4.7 Ukryj przyciski CSD](#Ukryj_przyciski_CSD)
    *   [4.8 Wyłącz wklejanie myszką](#Wyłącz_wklejanie_myszką)
    *   [4.9 Lokalizacja startu selektora plików](#Lokalizacja_startu_selektora_plików)
    *   [4.10 Starsza metoda przewijania](#Starsza_metoda_przewijania)
*   [5 Backendy GDK](#Backendy_GDK)
    *   [5.1 Backend Broadway](#Backend_Broadway)
    *   [5.2 Backend Waylanda](#Backend_Waylanda)
*   [6 Rozwiązywanie problemów](#Rozwiązywanie_problemów)
    *   [6.1 Różne motywy między aplikacjami GTK+ 2 i GTK+ 3](#Różne_motywy_między_aplikacjami_GTK+_2_i_GTK+_3)
    *   [6.2 Motyw nie został zastosowany do programów roota](#Motyw_nie_został_zastosowany_do_programów_roota)
    *   [6.3 Dekoracje client-side](#Dekoracje_client-side)
    *   [6.4 Powstrzymaj ostrzeżenia o dostępnośći](#Powstrzymaj_ostrzeżenia_o_dostępnośći)
    *   [6.5 Niedopasowanie koloru tła paska tytułu](#Niedopasowanie_koloru_tła_paska_tytułu)
    *   [6.6 Nieprawidłowe zdarzenia fokusu z tiling menedżerami okien](#Nieprawidłowe_zdarzenia_fokusu_z_tiling_menedżerami_okien)
    *   [6.7 Obsługa miniaturek dla okna dialogowego pliku GTK+ 2](#Obsługa_miniaturek_dla_okna_dialogowego_pliku_GTK+_2)
    *   [6.8 Ikony przycisków/menu w niektórych aplikacjach w sesji Waylanda GNOME](#Ikony_przycisków/menu_w_niektórych_aplikacjach_w_sesji_Waylanda_GNOME)
    *   [6.9 GTK+ 3 bez polkitu](#GTK+_3_bez_polkitu)
    *   [6.10 Niektóre motywy GTK+ 2 zmieniają tylko palete kolorów UI](#Niektóre_motywy_GTK+_2_zmieniają_tylko_palete_kolorów_UI)
*   [7 Przykłady](#Przykłady)
*   [8 Zobacz również](#Zobacz_również)

## Instalacja

Dwie wersje GTK+ są obecnie dostępne w [oficjalnych repozytoriach](/index.php/Official_repositories "Official repositories"). Mogą być [zainstalowane](/index.php/Zainstal "Zainstal") za pomocą następujących pakietów:

*   **GTK+ 3.x** jest dostępny z pakietem [gtk3](https://www.archlinux.org/packages/?name=gtk3).
*   **GTK+ 2.x** jest dostępny z pakietem [gtk2](https://www.archlinux.org/packages/?name=gtk2).
*   **GTK+ 1.x** jest dostępny z pakietem [gtk](https://aur.archlinux.org/packages/gtk/).

## Motywy

W GTK+ 2 domyślnym motywem jest *Raleigh*, ale Arch Linux ma niestandardowy plik konfiguracyjny znajdujący się w `/usr/share/gtk-2.0/gtkrc`, który ustawia domyślny motyw na *Adwaita*. W GTK+ 3 domyślnym motywem jest *Adwaita*, ale są również uwzględnione motywy *HighContrast*, *HighContrastInverse* i *Raleigh*.

Żeby wymusić motyw , ustaw [wartość środowiska](/index.php/Environment_variables "Environment variables").

*   Dla GTK+ 2, użyj `GTK2_RC_FILES`. Dla przykładu żeby uruchomić [GIMPa](/index.php/GIMP "GIMP") z motywem *Raleigh*:

```
$ GTK2_RC_FILES=/usr/share/themes/Raleigh/gtk-2.0/gtkrc gimp

```

**Tip:** `gtkrc` może być także niestandardowym plikiem w twoim katalogu domowym utworzonym przez dowolne [#Narzędzia konfiguracyjne](#Narzędzia_konfiguracyjne).

*   Dla GTK+ 3, użyj `GTK_THEME`. Dla przykładu żeby uruchomić GNOME Kalkulator z czarnym wariantem *Adwaita*:

```
$ GTK_THEME=Adwaita:dark gnome-calculator

```

Więcej motywów może być zainstalowane z oficjalnych repozytoriów albo z [AUR](/index.php/AUR "AUR"). Manualnie rozpakuj motyw do katalogu `~/.themes/` lub `~/.local/share/themes`.

**GTK+ 2 i GTK+ 3.20 lub nowsze wspierane:**

*   **Adapta** — Adaptacyjny motyw GTK+ oparty na wytycznych Material Design. Zawiera: *Adapta*, *Adapta-Eta*, *Adapta-Nokto*, *Adapta-Nokto-Eta*

	[https://github.com/tista500/Adapta](https://github.com/tista500/Adapta) || [adapta-gtk-theme](https://www.archlinux.org/packages/?name=adapta-gtk-theme)

*   **Arc** — Płaski motyw o nowoczesnym wyglądzie i przezroczystych elementach. Zawiera: *Arc*, *Arc-Dark*, *Arc-Darker*

	[https://github.com/nicohood/arc-theme](https://github.com/nicohood/arc-theme) || z przezroczystością: [arc-gtk-theme](https://www.archlinux.org/packages/?name=arc-gtk-theme), bez przezroczystości: [arc-solid-gtk-theme](https://www.archlinux.org/packages/?name=arc-solid-gtk-theme)

*   **Breeze** — Wersja GTK+ domyślnego motywu KDE widgetów. Obejmuje: *Breeze*, *Breeze-Dark*

	[https://cgit.kde.org/breeze-gtk.git](https://cgit.kde.org/breeze-gtk.git) || [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk)

*   **Deepin** — Domyślny motyw dla pulpitu Deepin. Zawiera: *deepin*, *deepin-dark*

	[https://github.com/linuxdeepin/deepin-gtk-theme](https://github.com/linuxdeepin/deepin-gtk-theme) || [deepin-gtk-theme](https://www.archlinux.org/packages/?name=deepin-gtk-theme)

*   **GNOME Extra Themes** — Dodatkowe motywy dla pulpitu GNOME. Zawiera: *Adwaita*, *Adwaita-dark*, *HighContrast*

	[https://gitlab.gnome.org/GNOME/gnome-themes-extra](https://gitlab.gnome.org/GNOME/gnome-themes-extra) || [gnome-themes-extra](https://www.archlinux.org/packages/?name=gnome-themes-extra)

*   **MATE Themes** — Domyślne motywy dla pulpitu MATE. Zawiera: *BlackMATE*, *Blue-Submarine*, *BlueMenta*, *ContrastHighInverse*, *Green-Submarine*, *GreenLaguna*, *Menta*, *TraditionalGreen*, *TraditionalOk*

	[https://github.com/mate-desktop/mate-themes](https://github.com/mate-desktop/mate-themes) || [mate-themes](https://www.archlinux.org/packages/?name=mate-themes)

*   **Materia Theme** — Płaski motyw ala Material Design GTK3, GTK2, i GNOME-Shella.

	[https://github.com/nana-4/materia-theme](https://github.com/nana-4/materia-theme) || [materia-gtk-theme](https://www.archlinux.org/packages/?name=materia-gtk-theme)

*   **Numix** — Płaski i jasny motyw o nowoczesnym wyglądzie (GNOME, Openbox, Unity, Xfce). Zawiera: *Numix*

	[https://github.com/shimmerproject/Numix](https://github.com/shimmerproject/Numix) || [numix-gtk-theme](https://aur.archlinux.org/packages/numix-gtk-theme/)

*   **Blackbird** — Ciemny motyw dla Xfce.

	[https://github.com/shimmerproject/Blackbird](https://github.com/shimmerproject/Blackbird) || [xfce-theme-blackbird](https://aur.archlinux.org/packages/xfce-theme-blackbird/)

*   **Greybird** — Szary i niebieski motyw Xfce, używany domyślnie w Xubuntu 12.04.[https://github.com/shimmerproject/Greybird](https://github.com/shimmerproject/Greybird)

	[xfce-theme-greybird](https://aur.archlinux.org/packages/xfce-theme-greybird/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Vertex** — Motyw dla GTK 3, GTK 2, GNOME Shella i Cinnamona.

	[https://github.com/horst3180/vertex-theme](https://github.com/horst3180/vertex-theme) || [vertex-themes](https://aur.archlinux.org/packages/vertex-themes/)

*   **Zuki** — Motywy dla GTK, GNOME Shella i więcej.

	[https://github.com/lassekongo83/zuki-themes](https://github.com/lassekongo83/zuki-themes) || [zuki-themes-git](https://aur.archlinux.org/packages/zuki-themes-git/)

**Tylko GTK+ 2 wspierane:**

*   **GTK+ Engines** — Silniki motywów dla GTK+ 2\. Zawiera: *Clearlooks*, *Crux*, *Industrial*, *Mist*, *Redmond*, *ThinIce*

	[https://github.com/GNOME/gtk-engines](https://github.com/GNOME/gtk-engines) || [gtk-engines](https://www.archlinux.org/packages/?name=gtk-engines)

*   **Xfce Gtk+ Engine** — Silnik i motyw Xfce GTK+ 2.0

	[http://git.xfce.org/xfce/gtk-xfce-engine/](http://git.xfce.org/xfce/gtk-xfce-engine/) || [gtk-xfce-engine](https://www.archlinux.org/packages/?name=gtk-xfce-engine)

*   **Oxygen-Gtk** — Port domyślnego motywu KDE widżetów (Oxygen) do GTK2

	[https://cgit.kde.org/oxygen-gtk.git](https://cgit.kde.org/oxygen-gtk.git) || [oxygen-gtk2](https://www.archlinux.org/packages/?name=oxygen-gtk2)

*   **QtCurve** — Konfigurowalny zestaw stylów widżetów dla KDE i GTK.

	[https://cgit.kde.org/qtcurve.git](https://cgit.kde.org/qtcurve.git) || [qtcurve-gtk2](https://www.archlinux.org/packages/?name=qtcurve-gtk2)

W AUR istnieje wiele dodatkowych motywów GTK+, na przykład: [wyszukanie dla gtk-theme](https://aur.archlinux.org/packages.php?K=gtk-theme) lub [wyszukanie dla gtk2-theme](https://aur.archlinux.org/packages.php?K=gtk2-theme).

**Note:** Ponieważ GTK+3 szybko się rozwija, motywy GTK+ 3 często wymagają poprawek po wydaniu nowej wersji GTK+ 3\. Z tego powodu nie wszystkie motywy GTK+ 3 mogą wyglądać niepoprawnie jeśli są używane z najnowszą wersją GTK+ 3.

### GTK+ i Qt

Jeśli masz programy GTK+ i Qt (KDE), to wiesz, że ich wygląd nie miesza się dobrze. Jeśli chcesz, aby twoje style GTK+ pasowały do twoich stylów Qt, przeczytaj [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

## Narzędzia konfiguracyjne

Większość głównych [Środowisk graficznych](/index.php/Desktop_environment "Desktop environment") udostępnia narzędzia do konfiguracji motywu, ikon, czcionki i rozmiaru czcionki GTK+ oraz zarządzania tymi ustawieniami za pomocą [XSettings](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html):

*   Jeżeli korzystasz z [Cinnamon](/index.php/Cinnamon "Cinnamon"), użyj programu Motywy (*cinnamon-settings themes*): idź do *Ustawienia systemowe > Motywy*.
*   Jeżeli korzystasz z [Enlightenment (Polski)](/index.php/Enlightenment_(Polski) "Enlightenment (Polski)"): idź do *Ustawienia > Wszystkie > Wygląd > Motyw aplikacji*.
*   Jeżeli korzystasz z [GNOME (Polski)](/index.php/GNOME_(Polski) "GNOME (Polski)"), użyj Dostrajanie środowiska GNOME (*gnome-tweaks*): zainstaluj pakiet [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).
*   Jeżeli korzystasz z [MATE](/index.php/MATE "MATE"), użyj programu Preferencje wyglądu (*mate-appearance-properties*): idź do *System > Ustawienia > Wygląd*.
*   Jeżeli korzystasz z [Xfce (Polski)](/index.php/Xfce_(Polski) "Xfce (Polski)"), użyj narzędzia Dostrajania: idź do *Ustawienia > Wygląd*.

Other GUI tools generally overwrite the [pliki konfiguracyjne](#Konfiguracja).

**Również GTK+ 2 i GTK+ 3 są wspierane:**

*   **KDE GTK Configurator** — Aplikacja która pozwala zmienić styl i czcionke programów GTK+ 2 i GTK+ 3.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

	Po instalacji, `kde-gtk-config` może być również znaleziony w *Ustawienia Systemowe > Styl Aplikacji > GTK*.

*   **LXAppearance** — Niezależne od pulpitu narzędzie do konfiguracji stylu GTK+ 2 i GTK+ 3 z projektu LXDE (nie wymaga innych części pulpitu LXDE)

	[http://wiki.lxde.org/en/LXAppearance](http://wiki.lxde.org/en/LXAppearance) || [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)

*   **Oomox** — Graficzna aplikacja do generowania różnych odmian kolorów motywu Numix i Flat-Plat (GTK+ 2 i 3), Archdroid i Gnome-Colors. Umożliwia także generowanie wstępnie skalowanych motywów GTK+ 2 dla wyświetlaczy HiDPI.

	[https://github.com/actionless/oomox](https://github.com/actionless/oomox) || [oomox](https://aur.archlinux.org/packages/oomox/)

**Tylko GTK+ 2 jest wspierane:**

*   **GTK+ Change Theme** — Mały program który pozwala tobie zmienić twój motyw GTK+ 2.0 (uważany jako lepsza alternatywa *switch2*).

	[http://plasmasturm.org/code/gtk-chtheme/](http://plasmasturm.org/code/gtk-chtheme/) || [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)

*   **GTK+ Preference Tool** — Selektor motywów GTK+ i przełącznik czcionek.

	[http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool](http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool) || [gtk2_prefs](https://aur.archlinux.org/packages/gtk2_prefs/)

*   **GTK+ Theme Switch** — Prosty przełącznik motywów GTK+.

	[http://muhri.net/nav.php3?node=gts](http://muhri.net/nav.php3?node=gts) || [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)

## Konfiguracja

Ustawienia GTK+ ustawienia można określić ręcznie w plikach konfiguracyjnych, ale środowiska graficzne i aplikacje mogą zastąpić te ustawienia. W zależności od wersji GTK+ pliki te znajdują się pod:

*   GTK+ 2 specyficzne dla użytkownika: `~/.gtkrc-2.0`
*   GTK+ 2 systemowe ustawienia: `/etc/gtk-2.0/gtkrc`
*   GTK+ 3 specyficzne dla użytkownika: `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, or `$HOME/.config/gtk-3.0/settings.ini` jeżeli `$XDG_CONFIG_HOME` nie jest ustawione
*   GTK+ 3 systemowe ustawienia: `/etc/gtk-3.0/settings.ini`

**Note:**

*   Zobacz [właściwości *GtkSettings* GTK+ 3](http://library.gnome.org/devel/gtk3/stable/GtkSettings.html#GtkSettings.properties) i [właściwości GTK+ 2](http://library.gnome.org/devel/gtk2/stable/GtkSettings.html#GtkSettings.properties)) w podręczniku do programowania GTK+ dla pełnej listy aktualnie obsługiwanych opcji konfiguracyjnych GTK+.
*   Niektóre z opcji wypisanych poniżej (takie jak `gtk-icon-sizes`) są przestarzałe i ignorowane w GTK+ 3.10.
*   Jeżeli edytujesz swoje pliki konfiguracyjne GTK+, tylko na nowo otworzone aplikacje wyświetlą zmiany.

### Podstawowa konfiguracja motywu

### Pomiń ostrzeżenie dotyczące dostępności

Aby ręcznie zmienić motyw GTK+, ikony, czcionkę i rozmiar czcionki, dodaj następujące elementy do plików konfiguracyjnych, na przykład:

**GTK+ 2:**

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "Adwaita"
gtk-theme-name = "Adwaita"
gtk-font-name = "DejaVu Sans 11"
```

**GTK+ 3:**

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings]
gtk-icon-theme-name = Adwaita
gtk-theme-name = Adwaita
gtk-font-name = DejaVu Sans 11
```

**Note:** Nazwa paczek ikon to nazwa zdefiniowana w pliku indeksu motywu, a *nie* nazwa jego katalogu.

### Ciemny wariant motywu

Niektóre motywy GTK+ 3 zawierają ciemny wariant motywu, ale jest on używany domyślnie tylko wtedy, gdy aplikacja wyraźnie go zażąda. Aby użyć ciemnego motywu w wszystkich aplikacjach GTK+ 3, ustaw:

```
gtk-application-prefer-dark-theme = true

```

### Skróty klawiszowe

Skróty klawiaturowe (zwane również *akceleratorami* w GTK+) można zmienić, umieszczając kursor myszy nad odpowiednim elementem menu i naciskając odpowiednią kombinację klawiszy. Aby włączyć tę funkcję, ustaw:

```
gtk-can-change-accels = 1

```

#### Skróty klawiszowe Emacs

Aby mieć skróty klawiszowe podobne do Emacsa w aplikacjach GTK+, dodaj:

 `~/.gtkrc-2.0`  `gtk-key-theme-name = "Emacs"`  `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-key-theme-name = Emacs
```

Dla GTK+ 3 również uruchom:

```
$ gsettings set org.gnome.desktop.interface gtk-key-theme "Emacs"

```

XFCE ma również podobną opcje:

```
$ xfconf-query -c xsettings -p /Gtk/KeyThemeName -s Emacs

```

The config files in `/usr/share/themes/Emacs/` determine what the Emacs bindings are, and can be changed. Copying sections to the users `~/.gtkrc-2.0` file allows for changes on a per user basis.

### Opóźnienie menu GNOME

To ustawienie ustawia opóźnienie między wskazywaniem myszy w menu a otwieraniem menu. To opóźnienie jest mierzone w milisekundach.

```
gtk-menu-popup-delay = 0

```

### Zmniejsz wielkość widżetów

Jeśli masz mały ekran lub po prostu nie lubisz dużych ikon i widżetów, możesz łatwo zmienić ich rozmiar.

Aby mieć ikony bez tekstu na paskach narzędzi ([poprawne wartości](https://developer.gnome.org/gtk3/stable/gtk3-Standard-Enumerations.html#GtkToolbarStyle)), użyj

```
gtk-toolbar-style = GTK_TOOLBAR_ICONS

```

Żeby mieć mniejsze ikony użyj takiej linii:

```
gtk-icon-sizes = "panel-menu=16,16:panel=16,16:gtk-menu=16,16:gtk-large-toolbar=16,16\
:gtk-small-toolbar=16,16:gtk-button=16,16"

```

Albo żeby usunać ikony z przycisków kompletnie:

```
gtk-button-images = 0

```

Możesz usunać rownież ikony z menu:

```
gtk-menu-images = 0

```

Zobacz również [[1]](http://martin.ankerl.com/2008/10/10/how-to-make-a-compact-gnome-theme/) i [[2]](http://gnome-look.org/content/show.php/Simple+eGTK?content=119812).

### Ukryj przyciski CSD

Żeby usunąć przyciski minimalizacji i maksymalizacji z okien *gtk3*:

```
gtk-decoration-layout=menu:close

```

aby ukryć również przycisk wyłączania użyj wzamian:

```
gtk-decoration-layout=menu:

```

Zobacz [[3]](https://developer.gnome.org/gtk3/3.22/GtkSettings.html#GtkSettings--gtk-decoration-layout).

### Wyłącz wklejanie myszką

Żeby wyłączyć wklejanie środkowym przyciskiem myszy:

```
gtk-enable-primary-paste=false

```

### Lokalizacja startu selektora plików

Otwórz selektor plików w "bieżącym katalogu roboczym", a nie w **ostatniej** lokalizacji. Zwykle **bieżący katalog roboczy** jest katalogiem *domowym*.

**GTK+ 3**

Zmień [konfiguracje](/index.php/GNOME#Configuration "GNOME") poniższą komendą:

```
$ gsettings set org.gtk.Settings.FileChooser startup-mode cwd

```

**GTK+ 2**

Dodaj poniższą rzecz do `~/.config/gtk-2.0/gtkfilechooser.ini`:

```
StartupMode=cwd

```

### Starsza metoda przewijania

**Note:** To ustawienie nie jest przestrzegane przez wszystkie aplikacje GTK+.

**Tip:** Starsze zachowanie przewijania można uzyskać niezawodnie po prostu za pomocą prawego kliknięcia zamiast lewego kliknięcia.

Przed wersją GTK+ 3.6 kliknięcie dowolnej strony suwaka na pasku przewijania przesuwa pasek przewijania w kierunku kliknięcia o około jedną stronę. Od GTK+ 3.6 suwak przesunie się bezpośrednio na pozycję kliknięcia. To zachowanie można cofnąć w niektórych aplikacjach, tworząc plik z zawartością poniżej:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-primary-button-warps-slider = false

```

## Backendy GDK

GDK (podstawowa warstwa abstrakcji GTK+) wspiera kilka backendów żeby wyświetlać programy GTK+. Domyślnym backendem jest *x11*.

### Backend Broadway

Backend GDK, Broadway dostarcza wsparcie do wyświetlania programów GTK+ w przeglądarce internetowej, używając HTML5 i web sockety. [[4]](https://developer.gnome.org/gtk3/3.8/gtk-broadway.html)

Używając broadwayd, określ numer wyświetlacza, który ma być użyty, poprzedzony dwukropkiem, podobnie jak w X. Domyślny numer wyświetlacza to 1.

```
$ display_number=:5

```

Wystartuj go.

```
$ broadwayd $display_number 

```

Port używany domyślnie

```
port = 8080 + $display_number

```

Ustaw swoją przeglądarke na [http://127.0.0.1:port](http://127.0.0.1:port)

Żeby wystartować program

```
$ GDK_BACKEND=broadway BROADWAY_DISPLAY=$display_number *<<app>>*

```

Alternatywnie możesz ustawić adres i port

```
$ broadwayd --port $port_number --address $address $display_number

```

### Backend Waylanda

The GDK [Wayland](/index.php/Wayland "Wayland") backend can be enabled by setting the `GDK_BACKEND=wayland` environment variable.

**Tip:** To disable GTK window decorations in Wayland, [install](/index.php/Install "Install") the [gtk3-optional-csd](https://aur.archlinux.org/packages/gtk3-optional-csd/) package and set the environment variable `GTK_CSD=0`.

## Rozwiązywanie problemów

### Różne motywy między aplikacjami GTK+ 2 i GTK+ 3

In general, if a selected theme has support for both GTK+ 2 and GTK+ 3, the theme will be applied to all GTK+ 2 and GTK+ 3 applications. If a selected theme has support for only GTK+ 2, it will be used for GTK+ 2 applications and the default GTK+ theme will be used for GTK+ 3 applications. If the selected theme has support for only GTK+ 3, it will be used for GTK+ 3 applications and the default GTK+ theme will be used for GTK+ 2 applications. Thus for application theme consistency, it is best to use a theme which has support for both GTK+ 2 and GTK+ 3.

You could find what themes installed on your system have both an GTK+ 2 and GTK+ 3 version by using this command (does not work with names containing spaces):

```
find $(find ~/.themes /usr/share/themes/ -wholename "*/gtk-3.0" | sed -e "s/^\(.*\)\/gtk-3.0$/\1/") -wholename "*/gtk-2.0" | sed -e "s/.*\/\(.*\)\/gtk-2.0/\1"/

```

### Motyw nie został zastosowany do programów roota

As user theme files (`$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, `~/.gtkrc-2.0`) are not read by other accounts, the selected theme will not apply to [X applications run as root](/index.php/Running_X_apps_as_root "Running X apps as root"). Possible solutions include:

*   Create symlinks, e.g

```
# ln -s /home/[username]/.gtkrc-2.0 /etc/gtk-2.0/gtkrc
# ln -s /home/[username]/.config/gtk-3.0/settings.ini /etc/gtk-3.0/settings.ini

```

*   Configure system-wide theme files: `/etc/gtk-3.0/settings.ini` (GTK+ 3) or `/etc/gtk-2.0/gtkrc` (GTK+ 2)
*   Adjust the theme as root

```
# sudo lxappearance

```

*   Use a settings daemon (this is what most desktop environments do). A desktop-agnostic variant using [XSettings](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html) is available in the [AUR](/index.php/AUR "AUR") under [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/).

### Dekoracje client-side

GTK 3.12 wprowadziło [dekoracje client-side](http://blogs.gnome.org/mclasen/2013/12/05/client-side-decorations-in-themes/), które przenoszą pasek tytułowy od window managera. To może powodować problemy, takie jak [podwójny pasek tytułowy](http://redmine.audacious-media-player.org/boards/1/topics/1135) czy brak paska tytułowego lub [podwójne cienie](https://github.com/chjj/compton/issues/189) z włączonym kompozytorem.

Żeby usunąć cień i luki wokół okna (naprzykład w kombinacji w tilling window managerem), stwórz następujący plik:

 `~/.config/gtk-3.0/gtk.css` 
```
.window-frame, .window-frame:backdrop {
 box-shadow: 0 0 0 black;
 border-style: none;
 margin: 0;
 border-radius: 0;
}

.titlebar {
 border-radius: 0;
}

.window-frame.csd.popup {
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2), 0 0 0 1px rgba(0, 0, 0, 0.13);
}

.header-bar {
  background-image: none;
  background-color: #ededed;
  box-shadow: none;
}
/* Możesz użyć tego, jeśli nie podoba ci się podwójny tytułu.
GtkLabel.title {
    opacity: 0;
}*/

```

Aby dostosować przyciski na pasku tytułowym, ustaw `gtk-decoration-layout`. [[5]](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings--gtk-decoration-layout) Poniższe przykłady usuwają wszystkie przyciski:

 `~/.config/gtk-3.0/settings.ini`  `gtk-decoration-layout=menu:` 

### Powstrzymaj ostrzeżenia o dostępnośći

Jeżeli nie używasz żadnych funkcji [dostępnośći GNOME](https://wiki.gnome.org/Accessibility), możesz otrzymać błędy takie jak te:

```
WARNING **: Couldn't connect to accessibility bus:

```

Żeby powstrzymać te błędy uruchom programy z `NO_AT_BRIDGE=1` lub ustaw jako globalną [wartość środowiska](/index.php/Environment_variables "Environment variables").

### Niedopasowanie koloru tła paska tytułu

Jeśli używasz [window managera](/index.php/Window_manager "Window manager"), który używa motywu dekoracji okna, który naśladuje kolor tła motywu GTK+, może się okazać, że kolor paska tytułowego nie jest już całkowicie zgodny z kolorem aplikacji w niektórych aplikacjach GTK+ 3\. Aby obejść ten problem, stwórz następujący plik:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Zawsze używaj koloru tła */
GtkWindow {
    background-color: @theme_bg_color;
}

/* Napraw nadpisanie tła tooltipu */
.tooltip {
    background-color: rgba(0, 0, 0, 0.8);
}

.tooltip * {
    background-color: transparent;
}

/* Napraw nadpisanie tła okna pulpitu Nautilusa */
NautilusWindow {
     background-color: transparent; 
}

```

### Nieprawidłowe zdarzenia fokusu z tiling menedżerami okien

**Note:** Spowoduje to wyłączenie obsługi ekranu dotykowego dla aplikacji GTK+ 3\. [[6]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c14)

Zdefiniuj `GDK_CORE_DEVICE_EVENTS=1` żeby używać wejścia typu GTK2 zamiast xinput2\. [[7]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c10)

### Obsługa miniaturek dla okna dialogowego pliku GTK+ 2

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") pakiet [gtk2-patched-filechooser-icon-view](https://aur.archlinux.org/packages/gtk2-patched-filechooser-icon-view/) żeby mieć opcje do podglądu plików jako miniaturki zamiast listy w selektorze plików GTK+.

### Ikony przycisków/menu w niektórych aplikacjach w sesji Waylanda GNOME

Twój plik `~/.config/gtk-3.0/settings.ini` jest źle skonfigurowany. Może to się zdarzyć, jeśli wypróbujesz inne środowiska graficzne oparte na GTK+. To są obraźliwe wartości:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-button-images=1
gtk-menu-images=1
```

Po prostu ustaw je na 0 lub usuń cały plik, aby użyć domyślnych ustawień GNOME.

### GTK+ 3 bez polkitu

GTK+ 3 zależy od polkitu przez colord, który jest wymagany do drukowania. Jednak drukowanie działa dobrze bez zainstalowanego polkitu; przynajmniej z monochromatyczną drukarką i wersjami pakietów gtk3-print-backends=3.22.19-2 and colord=1.4.1-1.

### Niektóre motywy GTK+ 2 zmieniają tylko palete kolorów UI

W zależności od wyboru motywu wsparcia opcji obsługi GTK+ 2, UI może nadal mieć domyślny wygląd Raleigh, prawdopodobnie z inną paletą kolorów. Jest to spowodowane tym że wymagają one silnika Murrine GTK+ 2, którego brakuje (programy GTK+ 2 powinny narzekać na to na standardowym wyjściu błędów). Zainstaluj pakiet [gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine).

## Przykłady

Przykład konfiguracji GTK+ 2:

 `~/.gtkrc-2.0` 
```
# GTK theme
include "/usr/share/themes/Clearlooks/gtk-2.0/gtkrc"

# Font
style "myfont" {
    font_name = "DejaVu Sans 8"
}
widget_class "*" style "myfont"
gtk-font-name = "DejaVu Sans 8"

# Icon theme
gtk-icon-theme-name = "Tango"

# Toolbar style
gtk-toolbar-style = GTK_TOOLBAR_ICONS
```

Przykład konfiguracji GTK+ 3 skonfigurowanej z GTK+ 2.x do GTK+ 3.x przez [lxappearance](https://www.archlinux.org/packages/?name=lxappearance):

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings] 
gtk-theme-name=TraditionalOk
gtk-icon-theme-name=Fog
gtk-font-name=Luxi Sans 12
gtk-cursor-theme-name=mate
gtk-cursor-theme-size=24
gtk-toolbar-style=GTK_TOOLBAR_BOTH_HORIZ
gtk-toolbar-icon-size=GTK_ICON_SIZE_LARGE_TOOLBAR
gtk-button-images=1
gtk-menu-images=1
gtk-enable-event-sounds=0
gtk-enable-input-feedback-sounds=0
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle=hintslight
gtk-xft-rgba=rgb
```

## Zobacz również

*   [Oficjalna strona GTK+](http://www.gtk.org/)
*   [Artykuł na Wikipedii o GTK+](https://pl.wikipedia.org/wiki/GTK%2B)]
*   [Poradnik GTK+ 2.0](http://developer.gnome.org/gtk-tutorial/stable/)
*   [Samouczek referencyjny GTK+ 3](http://developer.gnome.org/gtk3/stable/)
*   [Poradnik gtkmm](http://developer.gnome.org/gtkmm-tutorial/stable/)
*   [Samouczek referencyjny gtkmm](http://developer.gnome.org/gtkmm/stable/)