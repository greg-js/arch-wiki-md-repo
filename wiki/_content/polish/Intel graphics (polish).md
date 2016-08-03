Ponieważ Intel udostępnia i wspiera otwarte sterowniki, karty graficzne Intela zwykle działają bez problemów.

**Note:** Informacje dotyczące używawania sterowników w konsoli bez [X](/index.php/Xorg_(Polski) "Xorg (Polski)") znajdziesz w [Uvesafb](/index.php?title=Uvesafb_(Polski)&action=edit&redlink=1 "Uvesafb (Polski) (page does not exist)").

## Contents

*   [1 Modele](#Modele)
*   [2 Instalacja](#Instalacja)
*   [3 Konfiguracja](#Konfiguracja)
*   [4 KMS (Kernel Mode Setting)](#KMS_.28Kernel_Mode_Setting.29)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Ustawienie trybu skalowania](#Ustawienie_trybu_skalowania)
    *   [5.2 Problem z KMS: konsola jest ograniczona do małego obszaru](#Problem_z_KMS:_konsola_jest_ograniczona_do_ma.C5.82ego_obszaru)
    *   [5.3 Sprzętowa akceleracja wideo](#Sprz.C4.99towa_akceleracja_wideo)
    *   [5.4 Ustawienie jasności i gammy](#Ustawienie_jasno.C5.9Bci_i_gammy)
*   [6 Rozwiązania problemów](#Rozwi.C4.85zania_problem.C3.B3w)
    *   [6.1 Glxgears pokazuje niską wydajność](#Glxgears_pokazuje_nisk.C4.85_wydajno.C5.9B.C4.87)
        *   [6.1.1 Wyłączenie synchronizacji pionowej (vsync)](#Wy.C5.82.C4.85czenie_synchronizacji_pionowej_.28vsync.29)
    *   [6.2 Pusty ekran podczas startu systemu, w czasie "Loading modules"](#Pusty_ekran_podczas_startu_systemu.2C_w_czasie_.22Loading_modules.22)
    *   [6.3 Poszarpane wideo](#Poszarpane_wideo)
    *   [6.4 X zawiesza/wyłącza się](#X_zawiesza.2Fwy.C5.82.C4.85cza_si.C4.99)
    *   [6.5 Dodanie niewykrytych rozdzielczości](#Dodanie_niewykrytych_rozdzielczo.C5.9Bci)
*   [7 Zobacz także](#Zobacz_tak.C5.BCe)

## Modele

Myślenie, że "Intel 945G" i "Intel GMA 945" to ten sam układ graficzny, tylko z różnymi nazwami jest błędne. Dokładnie rzecz ujmując, ten drugi nie istnieje. Intel oznacza jako "GMA" układ graficzny lub GPU. Cokolwiek innego to model **chipsetu płyty głównej**, przykładowo "915G", "945GM", "G965" czy "G45".

Popularne GPU i odpowiadające im chipsety płyt głównych to:

```
GPU                Chipset/Mostek północny
Intel GMA 900         910, 915
Intel GMA 950         945

```

Chipset (płyty głównej; nie GPU) "i810" jest bardzo stary i był produkowany na długo przed linią produktów 9xx, która jako pierwsza była oznaczana skrótem GMA. Podobnie, inne nazwy dla układów 910, 915 i 945 mogą zawierać prefiks `i`.

[Tutaj](https://en.wikipedia.org/wiki/Intel_GMA#Table_of_GMA_graphics_cores_and_chipsets "wikipedia:Intel GMA") znajduje się lista układów GMA.

## Instalacja

Wymagany jest: [Xorg (Polski)](/index.php/Xorg_(Polski) "Xorg (Polski)")

[Zainstaluj](/index.php/Pacman_(Polski) "Pacman (Polski)") pakiet [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), który jest dostępny w [oficjalnych repozytoriach](/index.php?title=Official_Repositories_(Polski)&action=edit&redlink=1 "Official Repositories (Polski) (page does not exist)"). Pozwala on na wybranie pożądanej metody akceleracji. Zalecaną metodą jest od teraz SNA. Zobacz testy przeprowadzone przez Phoronix [[1]](http://www.phoronix.com/scan.php?page=news_item&px=MTEzOTE). Mogą być znalezione [tutaj](http://www.phoronix.com/scan.php?page=article&item=intel_glamor_first&num=1) dla Sandy Bridge i [tutaj](http://www.phoronix.com/scan.php?page=article&item=intel_ivy_glamor&num=1) dla Ivy Bridge. UXA jest dobrą alternatywą, jeśli SNA sprawia problemy z Twoją konfiguracją. Dodaj to do `/etc/X11/xorg.conf` lub stwórz `/etc/X11/xorg.conf.d/20-intel.conf` :

```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "AccelMethod"  "sna"
   #Option      "AccelMethod"  "uxa"
   #Option      "AccelMethod"  "xaa"
EndSection

```

Jeśli korzystasz z 64-bitowego systemu i chcesz używać akceleracji w 32-bitowych programach, musisz zainstalować [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri).

**Note:** [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) znajduje się w [repozytorium [multilib]](/index.php?title=Official_Repositories_(Polski)&action=edit&redlink=1 "Official Repositories (Polski) (page does not exist)").

## Konfiguracja

Aby uruchomić Xorg, nie ma potrzeby konfiguracji (plik `xorg.conf` jest niepotrzebny, jednak jeśli istnieje, musi być poprawny).

Rzeczą, która powinna być zrobiona już podczas instalacji to dodanie swojego użytkownika do odpowiedniej [grupy](/index.php?title=Users_and_Groups_(Polski)&action=edit&redlink=1 "Users and Groups (Polski) (page does not exist)"):

```
# gpasswd -a nazwauzytkownika video

```

## KMS (Kernel Mode Setting)

[KMS](/index.php?title=KMS_(Polski)&action=edit&redlink=1 "KMS (Polski) (page does not exist)") jest wymagany do uruchomienia X-ów i środowiska graficznego, t.j. [GNOME](/index.php/GNOME_(Polski) "GNOME (Polski)"), [KDE](/index.php/KDE_(Polski) "KDE (Polski)"), [Xfce](/index.php/Xfce_(Polski) "Xfce (Polski)"), [LXDE](/index.php/LXDE_(Polski) "LXDE (Polski)"), itd. KMS jest wspierany przez układy Intela korzystające ze sterownika i915 i jest domyślnie włączony od jądra w wersji 2.6.32\. Sterownik [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) od wersji 2.10 nie wspiera UMS, wymagając użycie KMS [(*)](https://www.archlinux.org/news/484/). Zwykle KMS jest inicjalizowany po załadowaniu jądra. Jest jednak możliwe włączenie KMS podczas uruchamiania jądra, pozwalając całemu procesowi uruchamiania systemu działać w natywnej rozdzielczości.

**Note:** Używając KMS, **musisz** usunąć wszystkie parametry `vga` i `nomodeset` z Twojej konfiguracji uruchamiania jądra.

Aby to zrobić, dodaj moduł `i915` do linii `MODULES` w pliku `/etc/mkinitcpio.conf`:

```
MODULES="**i915**"

```

**Note:** Jeśli posiadasz procesor Core i{3,5,7} pierwszej generacji ze zintegrowanym GPU, niedodanie `i915` do linii `MODULES` w `/etc/mkinitcpio.conf` prawdopodobnie spowoduje błąd `kernel: intel ips [...]: failed to get i915 symbols, graphics turbo disabled`.

**Note:** Twój system może także wymagać dodania modułu `intel_agp`, jeśli wyświetla błędy podczas uruchamiania.

Następnie, wygeneruj initramfs:

```
# mkinitcpio -p linux

```

i uruchom ponownie system. Wszystko powinno działać.

## Tips and tricks

### Ustawienie trybu skalowania

Może to być użyteczne dla kilku aplikacji pełnoekranowych:

```
xrandr --output LVDS1 --set PANEL_FITTING param

```

gdzie `param` może być:

*   `center`: rozdzielczość nie zostanie zmieniona,
*   `full`: przeskauj rozdzielczość tak, aby wykorzystać cały ekran,
*   `full_aspect`: przeskaluj rozdzielczość tak, aby wykorzystać cały ekran ale z zachowaniem proporcji.

Jeśli to nie zadziała, spróbuj:

```
xrandr --output LVDS1 --set "scaling mode" param

```

gdzie `param` to jedno z `"Full"`, `"Center"` i `"Full aspect"`.

### Problem z KMS: konsola jest ograniczona do małego obszaru

Jeden z portów wideo o małej rozdzielczości mógł zostać włączony podczas uruchamiania systemu i powoduje ten problem. Rozwiązaniem jest wyłączenie portu dopisując `video=SVIDEO-1:d` do linii komend kernela w Twoim bootloaderze. Więcej informacji znajdziesz w [Parametry jądra](/index.php?title=Kernel_parameters_(Polski)&action=edit&redlink=1 "Kernel parameters (Polski) (page does not exist)").

Jeśli to nie zadziała, możesz spróbować wyłączyć port TV1 lub VGA1 zamiast SVIDEO-1.

### Sprzętowa akceleracja wideo

Jeśli chcesz włączyć sprzętową akcelerację dekodowania/enkodowania wideo w aplikacjach multimedialnych (takich jak VLC czy MPlayer) w układach Intel HD (Ivy Bridge, Sandy Bridge), [zainstaluj](/index.php/Pacman_(Polski) "Pacman (Polski)") pakiet [libva-driver-intel](https://www.archlinux.org/packages/?name=libva-driver-intel), dostępny w [Oficjalnych Repozytoriach](/index.php?title=Official_Repositories_(Polski)&action=edit&redlink=1 "Official Repositories (Polski) (page does not exist)").

Jeśli posiadasz układ G45 (X4500MHD) będziesz potrzebować ([libva-g45-h264](https://aur.archlinux.org/packages/libva-g45-h264/)) i ([libva-driver-intel-g45-h264](https://aur.archlinux.org/packages/libva-driver-intel-g45-h264/)) z AUR, ponieważ dla G45 Intel dostarcza sprzętową akcelerację wideo z h264 tylko w gałęzi "g45-h264" - więcej informacji na [http://intellinuxgraphics.org/h264.html](http://intellinuxgraphics.org/h264.html)). [vlc](https://www.archlinux.org/packages/?name=vlc) i [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) działają bardzo dobrze, ([gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi)) z G45 aktualnie [nie działa](https://bugs.freedesktop.org/show_bug.cgi?id=50390).

Aby skorzystać z VA-API, trzeba używać odtwarzacza wideo obsługującego VAAPI. Jeśli używasz mplayera, zainstaluj [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/), i użyj parametru -vo vaapi. Aby włączyć sprzętowe dekodowanie wideo we Flashu, dodaj `EnableLinuxHWVideoDecode=1` do `/etc/adobe/mms.cfg`. Jeśli akceleracja sprzętowa dalej nie działa, spróbuj dodać `OverrideGPUValidation = 1`.

### Ustawienie jasności i gammy

Intel nie oferuje możliwości ich ustawienia na poziomie sterownika. Na szczęście, można je ustawić używając `xgamma` i `xrandr`.

Gamma może być ustawiona używając:

```
xgamma -gamma 1.0

```

lub:

```
xrandr --output VGA1 --gamma 1.0:1.0:1.0

```

Jasność można ustawić używając:

```
xrandr --output VGA1 --brightness 1.0

```

## Rozwiązania problemów

### Glxgears pokazuje niską wydajność

**Note:** `glxgears` nie jest narzędziem do porównywania wydajności pomiędzy różnymi systemami.

Jeśli uruchamiasz `glxgears` w celu sprawdzenia wydajności graficznej systemu, możesz zauważyć, że wyniki oscylują wokół 60 FPS. Przykładowo:

```
[...]
311 frames in 5.0 seconds = 61.973 FPS
311 frames in 5.0 seconds = 62.064 FPS
311 frames in 5.0 seconds = 62.026 FPS 
[...]

```

Nie jest to spowodowane niską wydajnością. System graficzny używa synchronizacji pionowej i wyświetla natywną dla Twojego ekranu liczbę klatek na sekundę.

#### Wyłączenie synchronizacji pionowej (vsync)

Żeby wyłączyć synchronizację pionową, dodaj do pliku `/etc/X11/xorg.conf.d/20-intel.conf` w `Section "Device"` tę linię `Option "SwapbuffersWait" "false"`.

Innym sposobem jest ustawienie `vblank_mode` na `0` w pliku `~/.drirc` i upewnienie się, że `driver` jest ustawiony na `dri2`:

 `~/.drirc` 
```
<device screen="0" driver="dri2">
    <application name="Default">
    <option name="vblank_mode" value="0"/>
    </application>
 </device>
```

### Pusty ekran podczas startu systemu, w czasie "Loading modules"

Jeśli używasz "późnego startu" KMS i ekran staje się pusty w czasie "Loading modules", dodanie `i915` i `intel_agp` do initramfs może pomóc. Zobacz paragraf [KMS](#KMS_.28Kernel_Mode_Setting.29) powyżej.

Dodanie poniższego parametru do linii parametrów jądra też może pomóc:

```
video=SVIDEO-1:d

```

### Poszarpane wideo

Szarpanie obrazu powinno ustąpić po włączeniu [sprzętowej akceleracji wideo](#Sprz.C4.99towa_akceleracja_wideo). Możesz też dodać

```
Option "TearFree" "true" 

```

do `/etc/X11/xorg.conf.d/20-intel.conf`

### X zawiesza/wyłącza się

Znany jest problem z [chipsetem i845G](https://bugs.freedesktop.org/show_bug.cgi?id=26345), który powoduje zawieszanie GPU po chwili.

Jeśli masz problem z wyłączaniem/zawieszaniem się X lub problemy z GPU, rozwiązaniem może być zablokowanie korzystania z GPU korzystając z opcji "NoAccel":

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
 Section "Device"
    Identifier "old intel stuff"
    Driver "intel"
    Option "AccelMethod"  "sna"
    Option "NoAccel" "True"
 EndSection
```

### Dodanie niewykrytych rozdzielczości

Ta kwestia jest opisana na [stronie Xrandr](/index.php?title=Xrandr_(Polski)&action=edit&redlink=1 "Xrandr (Polski) (page does not exist)").

## Zobacz także

*   [http://intellinuxgraphics.org/documentation.html](http://intellinuxgraphics.org/documentation.html) (zawiera listę wspieranego sprzętu)
*   [KMS](/index.php?title=KMS_(Polski)&action=edit&redlink=1 "KMS (Polski) (page does not exist)") — artykuł o KMS z wiki Archa
*   [Xrandr](/index.php?title=Xrandr_(Polski)&action=edit&redlink=1 "Xrandr (Polski) (page does not exist)") — Jeśli masz problem z ustawieniem rozdzielczości
*   Forum Arch Linuksa: [Intel 945GM, Xorg, Kernel - wydajność](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)