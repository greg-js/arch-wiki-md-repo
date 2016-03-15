**Xorg** je veřejná open-source implementace systému X window verze 11\. Jelikož je Xorg nejpopulárnější volbou mezi uživateli Linuxu, jeho všudypřítomnost vedla k tomu, že se stal základním předpokladem pro provozování grafických aplikací a byl tak masově adoptován většinou distribucí. Pro více informací viz článek [Xorg](https://en.wikipedia.org/wiki/X.Org_Server "wikipedia:X.Org Server") na Wikipedii nebo můžete navštívit [stránky Xorg (anglicky)](http://www.x.org/wiki/).

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace](#Konfigurace)
    *   [2.1 Touchpad/Synaptics](#Touchpad.2FSynaptics)
    *   [2.2 Grafická karta a ovladače](#Grafick.C3.A1_karta_a_ovlada.C4.8De)
        *   [2.2.1 Uživatelé karet Nvidia](#U.C5.BEivatel.C3.A9_karet_Nvidia)
    *   [2.3 Nastavení monitoru](#Nastaven.C3.AD_monitoru)
        *   [2.3.1 Karty Nvidia](#Karty_Nvidia)
        *   [2.3.2 Na začátek](#Na_za.C4.8D.C3.A1tek)
        *   [2.3.3 Více monitorů/Dual screen](#V.C3.ADce_monitor.C5.AF.2FDual_screen)
        *   [2.3.4 TwinView](#TwinView)
            *   [2.3.4.1 Více než jedna grafická karta](#V.C3.ADce_ne.C5.BE_jedna_grafick.C3.A1_karta)
    *   [2.4 Vypnutí automatického přidávání zařízení (hot plugging)](#Vypnut.C3.AD_automatick.C3.A9ho_p.C5.99id.C3.A1v.C3.A1n.C3.AD_za.C5.99.C3.ADzen.C3.AD_.28hot_plugging.29)
    *   [2.5 InputClass](#InputClass)
        *   [2.5.1 Ukázkové konfigurace](#Uk.C3.A1zkov.C3.A9_konfigurace)
            *   [2.5.1.1 Příklad: Emulace kolečka (pro Trackpoint)](#P.C5.99.C3.ADklad:_Emulace_kole.C4.8Dka_.28pro_Trackpoint.29)
            *   [2.5.1.2 Příklad: Kliknutí po ťuknutí (tap to click)](#P.C5.99.C3.ADklad:_Kliknut.C3.AD_po_.C5.A5uknut.C3.AD_.28tap_to_click.29)
            *   [2.5.1.3 Příklad: Rozložení a model klávesnice na laptopu Acer 5920G](#P.C5.99.C3.ADklad:_Rozlo.C5.BEen.C3.AD_a_model_kl.C3.A1vesnice_na_laptopu_Acer_5920G)
    *   [2.6 Velikost displeje a DPI](#Velikost_displeje_a_DPI)
    *   [2.7 Nastavení klávesnice](#Nastaven.C3.AD_kl.C3.A1vesnice)
        *   [2.7.1 Nastavení rozložení klávesnice s hot pluggingem](#Nastaven.C3.AD_rozlo.C5.BEen.C3.AD_kl.C3.A1vesnice_s_hot_pluggingem)
        *   [2.7.2 Nastavení rozložení klávesnice bez hot pluggingu (zavrhováno)](#Nastaven.C3.AD_rozlo.C5.BEen.C3.AD_kl.C3.A1vesnice_bez_hot_pluggingu_.28zavrhov.C3.A1no.29)
        *   [2.7.3 Přepínání mezi rozloženími klávesnice](#P.C5.99ep.C3.ADn.C3.A1n.C3.AD_mezi_rozlo.C5.BEen.C3.ADmi_kl.C3.A1vesnice)
        *   [2.7.4 Trvalé vypnutí mousekeys (myš na klávesnici)](#Trval.C3.A9_vypnut.C3.AD_mousekeys_.28my.C5.A1_na_kl.C3.A1vesnici.29)
    *   [2.8 DPMS](#DPMS)
    *   [2.9 Proprietární ovladače](#Propriet.C3.A1rn.C3.AD_ovlada.C4.8De)
*   [3 Spouštění Xorg](#Spou.C5.A1t.C4.9Bn.C3.AD_Xorg)
*   [4 Tipy a triky](#Tipy_a_triky)
    *   [4.1 X startup (/usr/bin/startx) tweaking](#X_startup_.28.2Fusr.2Fbin.2Fstartx.29_tweaking)
    *   [4.2 Virtual X session](#Virtual_X_session)
    *   [4.3 Nested X session](#Nested_X_session)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Common problems](#Common_problems)
    *   [5.2 Ctrl-Alt-Backspace doesn't work](#Ctrl-Alt-Backspace_doesn.27t_work)
        *   [5.2.1 With input hot-plugging](#With_input_hot-plugging)
            *   [5.2.1.1 System-wide](#System-wide)
            *   [5.2.1.2 User-specific](#User-specific)
        *   [5.2.2 Without input hot-plugging](#Without_input_hot-plugging)
    *   [5.3 Apple keyboard issues](#Apple_keyboard_issues)
    *   [5.4 Touchpad tap-click issues](#Touchpad_tap-click_issues)
    *   [5.5 Extra mouse buttons not recognized](#Extra_mouse_buttons_not_recognized)
    *   [5.6 X clients started with "su" fail](#X_clients_started_with_.22su.22_fail)
    *   [5.7 Missing libraries](#Missing_libraries)
    *   [5.8 Packages fail to build; missing X11 includes](#Packages_fail_to_build.3B_missing_X11_includes)
    *   [5.9 Program requests "font '(null)'"](#Program_requests_.22font_.27.28null.29.27.22)
    *   [5.10 Frame-buffer mode problems](#Frame-buffer_mode_problems)
    *   [5.11 DRI with Matrox cards stops working](#DRI_with_Matrox_cards_stops_working)
    *   [5.12 Recovery: disabling Xorg before GUI login](#Recovery:_disabling_Xorg_before_GUI_login)
*   [6 Vizte též](#Vizte_t.C3.A9.C5.BE)

## Instalace

Nejprve plně zaktualizujte svůj systém:

```
# pacman -Syu

```

Poté můžete nainstalovat skupinu Xorg

```
# pacman -S xorg

```

Od verze 1.8 Xorg-server **nevyžaduje HAL pro přístup k hardwaru**. Udev dokáže detekovat váš hardware sám o sobě.

Nezapomeňte nainstalovat [evdev](/index.php/Evdev "Evdev").

```
# pacman -S xf86-input-evdev

```

HAL můžete bez problémů odstranit z démonů v `/etc/rc.conf`, ale **pouze pokud nemáte v systému žádnou jinou aplikaci, která by na něm byla závislá.** Z `/etc/X11/xorg.conf` se navíc stalo `/etc/X11/xorg.conf.d/*`.

Používání `X -configure` pro generaci `xorg.conf` je zavrhováno ze dvou důvodů:

*   Od verze 1.8 xorg-server používá namísto jednotného souboru xorg.conf vícero konfiguračních souborů v /etc/X11/xorg.conf.d
*   `xorg.conf` je z většiny zavrhnut, i když je během inicializace Xorg-serveru zpracováván.

Udev by měl být schopen rozpoznat váš hardware bez problémů. Pro případ, že by mohl nastat nějaký problém, můžete nainstalovat celou skupinu **xorg-input-drivers**.

Xorg-server můžete spustit příkazem **startx**, který byste ovšem měli používat pouze tehdy, pokud jste správně zeditovali soubor `~/.**xinitrc**`.

**Note:** V případě, že používáte desktopové prostředí (GNOME, KDE atp.), je pro spouštění doporučováno používat správce displeje (KDM, GDM atp.), jenž se postará o aplikace a knihovny, které by měly být předem nahrány.

Zkratka Ctrl+Alt+Bksp, která restartovala Xorg-server, byla z výchozího nastavení Xorg odstraněna. Můžete použít Ctrl+Alt+F1 pro přepnutí do virtuálního terminálu a zastavit činnost Xorg odtud.

**Note:** V hlavních desktopových prostředích (KDE, GNOME, Xfce4) je v korespondujícím nástroji pro konfiguraci klávesnice volba, pomocí které můžete tuto zkratku povolit (pro každého uživatele zvlášť).

## Konfigurace

Konfigurační soubory se nacházejí v `/etc/X11/xorg.conf.d/`.

Měli byste mít soubor `10-evdev.conf`, který spravuje klávesnici, myš, touchpad a dotykové obrazovky. Můžete vytvářet nové konfigurační soubory, přičemž jejich názvy musí začínat na **XX-** (kde XX je číslo) a končit příponou **.conf**. Načítány jsou postupně v pořadí od nejnižšího čísla.

### Touchpad/Synaptics

Pokud máte laptop, možná budete muset nainstalovat ovladač pro touchpad.

```
# pacman -S xf86-input-synaptics

```

Po instalaci naleznete v `/etc/X11/xorg.conf.d` soubor `10-synaptics.conf`. Můžete tedy v souboru `10-evdev.conf` zakomentovat/smazat "InputClass" týkající se vašeho touchpadu.

### Grafická karta a ovladače

Výchozí ovladač grafické karty je Vesa. Dokáže pracovat s většinou chipsetů, nicméně pokud chcete grafickou akceleraci, budete muset nainstalovat a používat ovladač specifický pro vaši konkrétní grafickou kartu.

Nejdříve najděte odkaz na svoji kartu v:

```
$ lspci | grep VGA

```

Poté nainstalujte ovladač příslušný k dané kartě. Tyto soubory můžete *vyhledat* spuštěním následujícího příkazu:

```
# pacman -Ss xf86-video

```

#### Uživatelé karet Nvidia

Během instalace proprietárního ovladače od Nvidie se nainstaluje do vaší složky `/etc/X11/xorg.conf.d` konfigurační soubor (se jménem `20-nvidia.conf`). Ten umožní Xorg nahrát kýžený ovladač při startu.

**Warning:** `nvidia-xconfig` již není nadále potřeba, tento příkaz je zavrhován, protože vytváří soubor `xorg.conf`. Pokud jste ztratili svůj konfigurační soubor pro Nvidie, jenž se nacházel v `/etc/X11/xorg.conf.d`, jenoduše přeinstalujte svůj ovladač.

### Nastavení monitoru

#### Karty Nvidia

`nvidia-settings` nezaktualizuje vaše soubory v `/etc/X11/xorg.conf.d/*`, nýbrž vytvoří soubor `xorg.conf`.

#### Na začátek

Nejprve vytvořte nový konfigurační soubor, například `/etc/X11/xorg.conf.d/10-monitor.conf`.

```
# nano /etc/X11/xorg.conf.d/10-monitor.conf

```

Zkopírujte a vložte do něj následující kód.

```
Section "Monitor"
    Identifier    "Monitor0"
EndSection

Section "Device"
    Identifier    "Device0"
    Driver        "vesa" #Zvolte ovladač použitý pro tento monitor
EndSection

Section "Screen"
    Identifier    "Screen0"  #Odkaz na sekce Monitor a Device
    Device        "Device0"
    Monitor       "Monitor0"
    DefaultDepth  16 #Zvolte hloubku (16||24)
    SubSection "Display"
        Depth     16
        Modes     "1024x768_75.00" #Zvolte rozlišení
    EndSubSection
EndSection

```

#### Více monitorů/Dual screen

**Warning:** `nvidia-settings` a `xrandr` jsou uživatelsky přívětivé nástroje, *nicméně* vytváří `xorg.conf`, jenž je postupně zatracován.

Abyste získali dvojí obrazovku, musíte upravit předešle vytvořený soubor `10-monitor.conf`. Přidejte pro každý monitor jednu sekci Monitor, Device a Screen a nakonec přidejte sekci ServerLayout pro jejich správu.

```
Section "ServerLayout"
    Identifier     "DualSreen"
    Screen       0 "Screen0"
    Screen       1 "Screen1" RightOf "Screen0" #Screen1 napravo od Screen0
    Option         "Xinerama" "1" #Pro přesun oken mezi obrazovkami
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true" 
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    Screen         0
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Screen         1
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1280x800_75.00"
    EndSubSection
EndSection

Section "Screen"
    Identifier     "Screen1"
    Device         "Device1"
    Monitor        "Monitor1"
    DefaultDepth   24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
    EndSubSection
EndSection

```

#### TwinView

Chcete-li pouze jednu velkou obrazovku namísto dvou, změňte argument pro TwinView na 1.

```
Option "TwinView" "1"

```

##### Více než jedna grafická karta

Musíte určit příslušný správný ovladač a vložit BusID svých grafických karet.

```
Section "Device"
    Identifier      "Screen0"
    Driver          "nvidia"
    BusID           "PCI:0:12:0"
EndSection

Section "Device"
    Identifier      "Screen1"
    Driver          "radeon"
    BusID           "PCI:1:0:0"
EndSection

```

Pro získání BusID:

```
$ lspci | grep VGA
01:00.0 VGA compatible controller: nVidia Corporation G96 [GeForce 9600M GT] (rev a1) 

```

Zde je BusID 1:0:0.

### Vypnutí automatického přidávání zařízení (hot plugging)

Od verze **1.8** Xorg-server pro rozpoznávání zařízení používá udev. Následující řádky udev vypnou.

```
Section "ServerFlags"
    Option "AutoAddDevices" "False"
EndSection

```

**Note:** Tímto vypnete hot plugging v Xorg pro **všechna** vstupní zařízení a navrátíte se ke stejnému chování jako ve verzi Xorg-server 1.4\. Je mnohem vhodnější nechat udev zkonfigurovat vaše zařízení. **Proto není vypínání hot pluggingu doporučeno!** Viz [Xorg Input Hotplugging (anglicky)](/index.php/Xorg_Input_Hotplugging "Xorg Input Hotplugging")

### InputClass

**Převzato z [https://fedoraproject.org/wiki/Input_device_configuration](https://fedoraproject.org/wiki/Input_device_configuration)**

InputClass je nový druh konfigurační sekce, která není specifická pro jedno zařízení, nýbrž se týká jisté třídy zařízení, včetně zařízení přidávaných za běhu. Sekce InputClass je omezena specifikovanými *shodami* (matches) — aby se pro určité vstupní zařízení aplikovala, všechna kritéria musí být pro dané zařízení splněna. Příklad sekce InputClass následuje níže:

```
Section "InputClass"
    Identifier      "Zachycuje všechny touchpady"
    MatchIsTouchpad "on"
    Driver           "synaptics"
EndSection

```

Pokud je tento úryvek přítomný v souboru `xorg.conf` nebo v některém ze souborů v xorg.conf.d, k jakémukoliv touchpadu přítomném v systému je přiřazen ovladač synaptics. Kvůli pořadí nahrávání (alfanumerické řazení úryvků v xorg.conf.d) přepisuje nastavení určené volbou Driver jakoukoliv *předešlou* volbu ovladače — čím obecnější je třída, tím dříve by měla být uvedena. Výchozí úryvek dodávaný s balíčkem xorg-x11-drv-Xorg je `00-evdev.conf` a aplikuje na všechna zařízení ovladač evdev.

Volby Match určují, na která zařízení lze danou sekci aplikovat. Aby nastala shoda s nějakým zařízením, musí být splněna všechna kritéria určená Match řádky. Tyto jsou podporovány následující (s příklady):

*   `MatchIsPointer`, `MatchIsKeyboard`, `MatchIsTouchpad`, `MatchIsTouchscreen`, `MatchIsJoystick` – booleovské volby (pravda, nepravda) pro aplikaci na určitou skupinu zařízení.
*   `MatchProduct "foo|bar"`: shoduje se, pokud jméno produktu zařízení obsahuje buď "foo" nebo "bar"
*   `MatchVendor "foo|bar|baz"`: shoduje se, pokud řetězec výrobce zařízení obsahuje "foo", "bar" nebo "baz"
*   `MatchDevicePath "/dev/input/event*"`: shoduje se, pokud se cesta k zařízení shoduje se zadanou cestou (viz fnmatch(3) pro povolené šablony)
*   `MatchTag "foo|bar"`: shoduje se, pokud má zařízení tag "foo" nebo "bar". Tagy mohou být přiřazeny konfiguračním backendem — tím je v tomto případě udev — zařízením, jenž vyžadují nějakou okliku nebo zvláštní konfiguraci.

Příklad uživatelem specifikované konfigurace:

```
Section "InputClass"
    Identifier     "lasermouse slowdown"
    MatchIsPointer "on"
    MatchProduct   "Lasermouse"
    MatchVendor    "LaserMouse Inc."
    Option         "ConstantDeceleration" 20
EndSection

```

Tato sekce by se shodovala s ukazovacím zařízením "Lasermouse" od "Lasermouse Inc." a aplikovala by na tomto zařízení konstantní zpomalení 20.

Některá zařízení mohou být použita X serverem, i když by ve skutečnosti být neměla. Tato zařízení lze nakonfigurovat, aby byla ignorována:

```
Section "InputClass"
    Identifier     "V X není potřeba mít akcelerometry"
    MatchProduct   "accelerometer"
    Option         "Ignore" "on"
EndSection

```

#### Ukázkové konfigurace

Následující podsekce popisují ukázkové konfigurace pro běžně používané konfigurační volby. Měli byste vědět, že pokud používáte desktopové prostředí, jako GNOME nebo KDE, volby nastavené v `xorg.conf` *mohou* být po přihlášení přepsány nastaveními konkrétního uživatele.

##### Příklad: Emulace kolečka (pro Trackpoint)

Pokud vlastníte počítač s Trackpointem (například Thinkpad), pro použití prostředního tlačítka k emulaci kolečka u myši můžete do souboru `xorg.conf` přidat následující:

```
Section "InputClass"
    Identifier     "Emulace kolečka"
    MatchIsPointer "on"
    MatchProduct   "TrackPoint"
    Option         "EmulateWheelButton" "2"
    Option "EmulateWheel" "on"
EndSection

```

Pro plnou podporu Trackpointů (včetně horizontálního skrolování) můžete použít následující:

```
Section "InputClass"
    Identifier	"Emulace kolečka u Trackpointu"
    MatchProduct	"TPPS/2 IBM TrackPoint|DualPoint Stick|Synaptics Inc. Composite TouchPad / TrackPoint|ThinkPad USB Keyboard with TrackPoint|USB Trackpoint pointing device"
    MatchDevicePath	"/dev/input/event*"
    Option		"EmulateWheel"		"true"
    Option		"EmulateWheelButton"	"2"
    Option		"Emulate3Buttons"	"false"
    Option		"XAxisMapping"		"6 7"
    Option		"YAxisMapping"		"4 5"
EndSection

```

##### Příklad: Kliknutí po ťuknutí (tap to click)

Kliknutí po ťuknutí na touchpad můžete povolit v dialogu konfigurace myši (v záležce Touchpad), ale pokud potřebujete ťukání povolené již ve správci displeje (GDM), následující úryvek vám to umožní:

```
Section "InputClass"
    Identifier "tap-by-default"
    MatchIsTouchpad "on"
    Option "TapButton1" "1"
EndSection

```

##### Příklad: Rozložení a model klávesnice na laptopu Acer 5920G

Model a rozložení klávesnice lze nastavit v souboru `/etc/X11/xorg.conf.d/keyboard.conf` nebo jakomkoliv jiném .conf souboru ve stejném adresáři.

*   `MatchIsKeyboard "yes"`: Provést pouze u klávesnic
*   `Option "XkbLayout" "be"`: Nastaví rozložení klávesnice na belgické. `be` můžete nahradit za jakékoliv konkrétní rozložení, jaké potřebujete.
*   `Option "XkbModel" "acer_laptop"`: Nastaví model klávesnice na klávesnici laptopů Acer. `acer_laptop` můžete nahradit za váš konkrétní model klávesnice.

Seznam rozložení a modelů klávesnic můžete nalézt v `/usr/share/X11/xkb/rules/base.lst`.

```
Section "InputClass"
    Identifier             "Výchozí nastavení klávesnice"
    MatchIsKeyboard        "yes"
    Option                 "XkbLayout" "be"
    Option                 "XkbModel" "acer_laptop"
EndSection

```

### Velikost displeje a DPI

**Otázka:** Jak vypočítávají Xorg servery hodnotu DPI?
**Odpověď:** DPI X serveru je zjištěno následujícím způsobem:

1.  Nejvyšší prioritu má volba `-dpi` na příkazové řádce.
2.  Pokud není tato volba uvedena, k odvození hodnoty DPI pro dané rozlišení obrazovky je použito nastavení DisplaySize v konfiguračním souboru X.
3.  Pokud není přítomné žádné nastavení DisplaySize, jsou pro odvození DPI pro dané rozlišení obrazovky použity hodnoty velikosti monitoru získané z DDC.
4.  Pokud DDC neříká nic o velikosti, ve výchozím nastavení je použito DPI 75.

Abyste získali správnou hodnotu bodů na palec (DPI), musí být rozpoznána nebo nastavena velikost displeje. Správné nastavení DPI je zvláště nutné tam, kde jsou vyžadovány jemné detaily (například vykreslování fontů). V minulosti se výrobci pokoušeli vytvořit standard 96 DPI (monitor s uhlopříčkou 10.3" by měl 800x600 a monitor 13.2" 1024x768). V dnešní době mohou mít obrazovky rozličné hodnoty DPI, které ani nemusí být shodné vertikálně a horizontálně. Aby byl Xorg server schopný nastavit DPI, pokouší se automaticky zjistit fyzickou velikost vašeho monitoru skrze grafickou kartu pomocí [DDC (anglicky)](https://en.wikipedia.org/wiki/Display_Data_Channel "wikipedia:Display Data Channel"). Pokud Xorg server zná fyzickou velikost obrazovky, bude schopný v závislosti na rozlišení nastavit správnou hodnotu DPI.

Abyste zjistili, zda jsou velikost vašeho displeje a DPI zjištěny/vypočítány správně:

```
$ xdpyinfo | grep dimensions
$ xdpyinfo | grep "dots per inch"

```

Ověřte si, zda udané rozměry souhlasí s velikostí vašeho displeje. Pokud Xorg server není schopen správně vypočítat velikost obrazovky, použije výchozí nastavení 75x75 DPI a budete ji muset spočítat sami.

Pokud máte specifikace fyzické velikosti obrazovky, můžete je zadat do konfiguračního souboru Xorg, aby tak mohla být vypočítána správná hodnota DPI:

```
Section "Monitor"
    Identifier "Monitor0"
    DisplaySize 286 179    #V milimetrech
EndSection

```

Pokud nemáte specifikace pro fyzickou šířku a výšku (většina dnešních specifikací uvádí pouze úhlopříčku), můžete pro výpočet horizontálního a vertikálního rozměru použít nativní rozlišení (nebo poměr stran) a délku úhlopříčky monitoru. Použití Pythagorovy věty pro obrazovku s úhlopříčkou 13.3" a nativním rozlišením 1280x800 (nebo poměrem stran 16:10):

```
echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

Případně, nemáte-li program bc a nechce se vám ho instalovat:

```
awk 'function x(w,h) {return sqrt(w*w + h*h)} BEGIN {print x(1280, 800)}'

```

Výsledek je délka úhlopříčky v pixelech. Pomocí této hodnoty můžete zjistit fyzickou šířku a výšku displeje (a převést je na milimetry):

```
echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
echo 'scale=5;(13.3/1509)*800*25.4' | bc   # 179.01920

```

Případně opět pomocí `awk`:

```
awk 'BEGIN {print (13.3/1509)*1280*25.4}'
awk 'BEGIN {print (13.3/1509)*800*25.4}'

```

**Note:** Tento výpočet funguje pro většinu velikostí obrazovek, nicméně můžete narazit na nějaký levný monitor, který bude poměr stran roztahovat, např. z 16:10 na 16:9\. Pokud je to váš případ, měli byste změřit velikost obrazovky ručně.

Pokud budete používat pouze jedno rozlišení obrazovky, lze DPI též nastavit napevno:

```
Section "Monitor"
    Identifier "Monitor0"
    Option   "DPI" "96 x 96"
EndSection

```

Pokud z nějakého podivného důvodu nenastaví ovladače Nvidia správné DPI, můžete vypnout automatickou detekci:

```
Option   "UseEdidDpi" "false"

```

Pro ovladače podporující RandR můžete DPI nastavit tímto způsobem:

```
xrandr --dpi 96

```

Tento příkaz můžete přidat do svého souboru `.xinitrc`, abyste tak měli nastavené správné DPI, když spustíte X ručně.

### Nastavení klávesnice

Xorg nemusí správně rozpoznat vaši klávesnici. To může způsobit problémy s nesprávně nastaveným rozložením nebo modelem klávesnice.

Pro zobrazení úplného seznamu modelů, rozložení, variant a voleb, vizte soubor:

```
/usr/share/X11/xkb/rules/xorg.lst

```

Pro nastavení rozložení klávesnice pro momentálně spuštěné sezení Xorg:

```
# setxkbmap dvorak

```

##### Nastavení rozložení klávesnice s hot pluggingem

Abyste permanentně změnili své rozložení klávesnice, přidejte do `xorg.conf` následující:

```
Section "InputClass"
    Identifier             "Keyboard Defaults"
    MatchIsKeyboard	   "yes"
    Option	           "XkbLayout" "dvorak"
EndSection

```

Všimněte si, že je použita sekce InputClass a ne sekce InputDevice pro konkrétní klávesnici.

##### Nastavení rozložení klávesnice bez hot pluggingu (zavrhováno)

**Note:** Pro změnu rozložení klávesnice tímto způsobem musíte vypnout hot plugging pro vstupní zařízení.

Abyste změnili rozložení klávesnice, použijte volbu XkbLayout v sekci InputDevice pro konkrétní klávesnici. Pokud například máte klávesnici s anglickým rozložením, InputDevice sekce vaší klávesnice by mohla vypadat nějak takto:

```
Section "InputDevice"
    Identifier     "Keyboard0"
    Driver         "kbd"
    Option "XkbLayout" "gb"
EndSection

```

Abyste změnili model klávesnice, použijte v InputDevice sekci vaší klávesnice volbu XkbModel. Máte-li například klávesnici Microsoft Wireless Multimedia Keyboard:

```
Option "XkbModel" "microsoftmult"

```

##### Přepínání mezi rozloženími klávesnice

Abyste mohli snadno přepínat rozložení klávesnice, pozměňte volby použité v některé z výše zmíněných metod. Například pro přepínání mezi americkým a švédským rozložením pomocí klávesy Caps Lock můžete použít:

```
Option "XkbLayout"  "us, se"
Option "XkbOptions" "grp:caps_toggle"

```

Toto je zejména užitečné, pokud používáte desktopové prostředí, které se za vás o rozložení klávesnice nepostará.

##### Trvalé vypnutí mousekeys (myš na klávesnici)

Abyste na stálo vypnuli mousekeys a předešli tím povolení kombinace Shift+NumLock nebo Shift+Alt+NumLock, otevřete soubor `/usr/share/X11/xkb/compat/complete` a zakomentujte:

```
augment "mousekeys"
augment "accessx(full)"

```

### DPMS

DPMS (Display Power Management Signaling) je technologie umožňující snížit spotřebu monitorů, není-li počítač používán. Toho dociluje samočinným přechodem monitorů do režimu standby po předem určené době. Viz [DPMS](/index.php?title=DPMS_(%C4%8Cesky)&action=edit&redlink=1 "DPMS (Česky) (page does not exist)").

### Proprietární ovladače

Pokud si přejete používat grafické ovladače třetích stran, ověřte si, že X server funguje. Xorg by měl hladce běžet i bez oficiálních ovladačů, jenž jsou typicky potřebné pouze pro pokročilé funkce, jakými jsou akcelerované 3D renderování pro hry, dual-screen nebo televizní výstup. Vizte [NVIDIA](/index.php/NVIDIA_(%C4%8Cesky) "NVIDIA (Česky)") a [ATI](/index.php/ATI "ATI") pro rady ohledně instalace ovladačů.

## Spouštění Xorg

HAL automaticky spouští dbus. Pokud jste ale HAL ze svého seznamu DAEMONS odstranili, měli byste na jeho místo dbus přidat.

```
 DAEMONS=(syslog-ng **dbus** network netfs crond)

```

Pokud potřebujete spustit dbus ručně, zadejte:

```
# /etc/rc.d/dbus start

```

Nakonec nastartujte Xorg:

```
$ startx

```

nebo

```
$ xinit

```

**Note:** Pokud jste právě Xorg nainstalovali, ve vašem domovském adresáři se bude nacházet prázdný soubor `.xinitrc`, který musíte, aby se X mohlo správně spustit, buď změnit nebo smazat. Pokud tak neučiníte, X ukáže jen prázdnou obrazovku a ve vašem souboru `Xorg.0.log` nebude zmínka o žádné chybě. Tím, že tento soubor jednoduše odstraníte, ho přinutíte spustit výchozí prostředí X.

Výchozí prostředí X je poněkud prosté a typicky budete chtít nainstalovat okenního správce nebo desktopové prostředí, aby X doplnily. Seznam vhodných voleb se nachází [zde](/index.php/Common_Applications_(%C4%8Cesky)#Desktopov.C3.A1_prost.C5.99ed.C3.AD "Common Applications (Česky)").

Pokud by nastal nějaký problém, podívejte se do logu v `/var/log/Xorg.0.log`. Dívejte se po všech řádcích začínajících na `(EE)`, ty představují chyby, a též `(WW)`, což jsou varování, která by mohla poukazovat na další problémy.

## Tipy a triky

### X startup (/usr/bin/startx) tweaking

For X's option reference see:

```
$ man Xserver

```

The following options have to be appended to the variable `"defaultserverargs"` in the `/usr/bin/startx` file:

*   Enable deferred glyph loading for 16 bit fonts:

```
-deferglyphs 16

```

Note: If you start X with kdm, the startx script does not seem to be executed. X options must be appended to the variable `"ServerArgsLocal"` or `"ServerCmd"` in the `/usr/share/config/kdm/kdmrc` file. By default kdm options are:

```
  ServerArgsLocal=-nolisten tcp
  ServerCmd=/usr/bin/X

```

### Virtual X session

To start another X session in for example CTRL + ALT + F8 you need to type this on a console:

```
xinit /path/to/wm -- :1

```

Change "/path/to/wm" to your window manager start file or to your login manager like gdm, kdm and slim.

### Nested X session

To run a nested session of another desktop environment:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

This will launch a Window Maker session in a 1024 by 768 window within your current X session.

## Troubleshooting

### Common problems

If Xorg will not start, or the screen is completely black, the keyboard and mouse is not working, etc., first take these simple steps:

*   Check the log file: `cat /var/log/Xorg.0.log`
*   Install input driver (keyboard, mouse, joystick, tablet, etc...):

```
 # pacman -S xf86-input-evdev

```

*   Finally, search for common problems in [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel") and [NVIDIA](/index.php/NVIDIA "NVIDIA") articles.

### Ctrl-Alt-Backspace doesn't work

There are two ways of restoring `Ctrl`+`Alt`+`Backspace`; with and without input-hotplugging. Using hot-plugging is recommended.

#### With input hot-plugging

In most situations, using user-specific configuration might be preferred over system-wide.

**Note:** On GNOME, this system-wide setting has no effect. Every user must go to System -> Preferences -> Keyboard -> Layouts -> Options [button] -> Key sequence to kill the X server [expand with triangle on left]. Then check Ctrl + Alt + Backspace option.

##### System-wide

Add

```
Option  "XkbOptions" "terminate:ctrl_alt_bksp"

```

to InputClass as so:

```
Section "InputClass"
    Identifier          "Keyboard Defaults"
    MatchIsKeyboard	"yes"
    Option              "XkbOptions" "terminate:ctrl_alt_bksp"
EndSection

```

##### User-specific

Another way is to add the following line to `~/.xinitrc`

```
setxkbmap -option terminate:ctrl_alt_bksp

```

**Note:** If you use a login/display manager like (K/G/X)DM or Slim, you will need to run the above setxkbmap command around your WM/DE's login time. ~/.config/autostart is usually respected for such (using .desktop files). It also works in ~/.bashrc.

#### Without input hot-plugging

New Xorg disables zapping with `Ctrl`+`Alt`+`Backspace` by default. You can enable it by adding the following line to `/etc/X11/xorg.conf`,

```
Option  "XkbOptions" "terminate:ctrl_alt_bksp" 

```

to `InputDevice` section for keyboard.

### Apple keyboard issues

	*See: [Apple Keyboard](/index.php/Apple_Keyboard "Apple Keyboard")*

### Touchpad tap-click issues

	*See: [Synaptics](/index.php/Synaptics "Synaptics")*

### Extra mouse buttons not recognized

	*See: [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working")*

### X clients started with "su" fail

If you are getting "Client is not authorized to connect to server", try adding the line:

```
session        optional        pam_xauth.so

```

to `/etc/pam.d/su`. `pam_xauth` will then properly set environment variables and handle `xauth` keys.

### Missing libraries

*   Error message: "*libX... does not exist*"

In most cases, all you need to do is take the name of the library (e.g., `libXau.so.1`), convert it all to lowercase, remove the extension, and install it:

```
# pacman -S libxau

```

### Packages fail to build; missing X11 includes

Reinstall the packages xproto and libx11:

```
# pacman -S xproto libx11

```

### Program requests "font '(null)'"

*   Error message: "*unable to load font `(null)'.*"

Some programs only work with bitmap fonts. Two major packages with bitmap fonts are available, xorg-fonts-75dpi and xorg-fonts-100dpi. You do not need both; one should be enough. To find out which one would be better in your case, try this:

```
$ xdpyinfo | grep resolution

```

and use what is closer to you (75 or 100 instead of XX)

```
# pacman -S xorg-fonts-XXdpi

```

### Frame-buffer mode problems

If X fails to start with the following log messages,

```
(WW) Falling back to old probe method for fbdev
(II) Loading sub module "fbdevhw"
(II) LoadModule: "fbdevhw"
(II) Loading /usr/lib/xorg/modules/linux//libfbdevhw.so
(II) Module fbdevhw: vendor="X.Org Foundation"
       compiled for 1.6.1, module version=0.0.2
       ABI class: X.Org Video Driver, version 5.0
(II) FBDEV(1): using default device

Fatal server error:
Cannot run in framebuffer mode. Please specify busIDs for all framebuffer devices

```

uninstall fbdev:

```
# pacman -R xf86-video-fbdev

```

### DRI with Matrox cards stops working

If you use a Matrox card and DRI stops working after upgrading to Xorg, try adding the line:

```
Option "OldDmaInit" "On"

```

to the Device section that references the video card in xorg.conf.

### Recovery: disabling Xorg before GUI login

If Xorg is set to boot up automatically and for some reason you need to prevent it from starting up before the login/display manager appears (if the system is wrongly configured and Xorg does not recognize your mouse or keyboard input, for instance), you can accomplish this task with two methods.

*   Change default target to rescue.target. See [systemd#Change default target to boot into](/index.php/Systemd#Change_default_target_to_boot_into "Systemd").
*   If you have not only a faulty system that makes Xorg unusable, but you have also set the GRUB menu wait time to zero, or cannot otherwise use GRUB to prevent Xorg from booting, you can use the Arch Linux live CD. Boot up the live CD and log in as root. You need a mount point, such as `/mnt`, and you need to know the name of the partition you want to mount.

You can use the command,

```
# fdisk -l

```

to see your partitions. Usually, the one you want will be resembling `/dev/sda1`. Then, to mount this to `/mnt`, use

```
# mount /dev/sda1 /mnt

```

Then your filesystem will show up under `/mnt`. From here you can delete the `gdm` daemon to prevent Xorg from booting up normally or make any other necessary changes to the configuration.

## Vizte též

*   [Správci displeje](/index.php/Display_manager_(%C4%8Cesky) "Display manager (Česky)")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login") (anglicky)
*   [Font configuration](/index.php/Font_configuration "Font configuration") (anglicky)
*   Proprietární grafické ovladače
    *   [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") (anglicky)
    *   [NVIDIA](/index.php/NVIDIA_(%C4%8Cesky) "NVIDIA (Česky)")
*   Desktopová prostředí
    *   [KDE](/index.php/KDE_(%C4%8Cesky) "KDE (Česky)")
    *   [GNOME](/index.php/GNOME_(%C4%8Cesky) "GNOME (Česky)")
    *   [Xfce](/index.php/Xfce_(%C4%8Cesky) "Xfce (Česky)")
    *   [Enlightenment](/index.php/Enlightenment_(%C4%8Cesky) "Enlightenment (Česky)")
    *   [LXDE](/index.php/LXDE_(%C4%8Cesky) "LXDE (Česky)")
*   Okenní správci
    *   [Awesome](/index.php/Awesome_(%C4%8Cesky) "Awesome (Česky)")
    *   [Fluxbox](/index.php/Fluxbox_(%C4%8Cesky) "Fluxbox (Česky)")
    *   [Openbox](/index.php/Openbox_(%C4%8Cesky) "Openbox (Česky)")
*   [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working") (anglicky)
*   [Compiz](/index.php/Compiz "Compiz") (anglicky)