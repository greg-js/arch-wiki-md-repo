## Contents

*   [1 Nastavení pro laptopy](#Nastaven.C3.AD_pro_laptopy)
*   [2 Řízení spotřeby](#.C5.98.C3.ADzen.C3.AD_spot.C5.99eby)
    *   [2.1 Nástroje pro monitorování stavu baterie](#N.C3.A1stroje_pro_monitorov.C3.A1n.C3.AD_stavu_baterie)
    *   [2.2 Cpufrequtils](#Cpufrequtils)
    *   [2.3 Pm-utils](#Pm-utils)
    *   [2.4 Lapsus](#Lapsus)
    *   [2.5 Instalace powertopu](#Instalace_powertopu)
    *   [2.6 Laptop mode tools](#Laptop_mode_tools)
    *   [2.7 Powernowd](#Powernowd)
    *   [2.8 Návhry pro šetření energie](#N.C3.A1vhry_pro_.C5.A1et.C5.99en.C3.AD_energie)
        *   [2.8.1 Nastavení disků](#Nastaven.C3.AD_disk.C5.AF)
        *   [2.8.2 Další nastavení](#Dal.C5.A1.C3.AD_nastaven.C3.AD)
        *   [2.8.3 Problém s točícími se hlavičkami pevného disku](#Probl.C3.A9m_s_to.C4.8D.C3.ADc.C3.ADmi_se_hlavi.C4.8Dkami_pevn.C3.A9ho_disku)
        *   [2.8.4 Nastavení plánovače](#Nastaven.C3.AD_pl.C3.A1nova.C4.8De)
*   [3 Touchpad](#Touchpad)
*   [4 Speciální tlačítka](#Speci.C3.A1ln.C3.AD_tla.C4.8D.C3.ADtka)
*   [5 Ochrana pevného disku proti šoku](#Ochrana_pevn.C3.A9ho_disku_proti_.C5.A1oku)

# Nastavení pro laptopy

Tato stránka by měla obsahovat odkazy na stránky potřebné pro konfiguraci laptopu. Nastavení laptopu je v mnoha ohledech stejné jako nastavení stolního počítače. Přesto je zde několik odlišností. Při nastavování laptopu v Arch Linuxu je potřeba mít na paměti tyto body:

*   Spotřeba energie (jak donutit baterii aby vydržela co nejdéle nabitá). To vede k řízení spotřeby energie:
*   Roztáčení hlaviček pevného disku. Po kolika minutách neaktivity by se měly hlavičky usadit?
*   Vypnutí obrazovky. Po kolika minutách neaktivizy by se měla obrazovka vypnout?
*   Škálování frekvence procesoru. Jak by se měla měnit frekvence procesoru v závislosti na zátěži pro minimalizaci spotřeby energie?
*   Uspání a hibernace. Jak zprovoznit uspání a hibernaci na mém notebooku?
*   Jas obrazovky. Jak ovládat jas obrazovky?

*   Síť a bezdrát. Jak zprovoznit bezdrátovou síť?
*   Multimediální tlačítka. Jak nakonfigurovat těchto tlačítek na mém notebooku?
*   Touchpad. Jak nastavit citlivost, akceleraci, funkci tlačítek a rolovacích okrajů pro můj Synaptics nebo Alps touchpad?

Všechny tyto body je třeba mít na paměti při nastavování notebooku tak jak si přeješ. Arch Linux naštěstí poskytuje všechny nástroje a programy potřebné pro kompletní nastavení notebooku. Tyto nástroje a programy jsou zvýrazněny níže, spolu s odpovídajícími tutoriály.

Poznámka: následující odkazy mohou být užitečné:

*   [http://www.linux-on-laptops.com/](http://www.linux-on-laptops.com/)
*   [http://www.linlap.com/](http://www.linlap.com/)

# Řízení spotřeby

Řízení spotřeby je velice důležité pro každého, který chce dobře využít kapacity své baterie. Následující nástroje a programy pomáhají zvýšit výdrž baterie a udržet tvůj notebook chladný a tichý.

## Nástroje pro monitorování stavu baterie

Stave baterie může být samozřejmě odečítán pomocí acpi v terminálu. Acpi můžes nainstalovat tímto příkazem:

```
$ pacman -S acpi

```

Jednoduchý monitor baterie sídlící v tray je [batterymon](https://aur.archlinux.org/packages.php?ID=24694) a je možné jej nalézt v [AURu](/index.php/AUR "AUR").

## Cpufrequtils

[Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") poskytuje škálování frekvence procesoru, technologie užívaná především v noteboocích umožňuje operačnímu systému zvyšovat a snižovat frekvenci procesoru v závislosti na současném zatížení a schématu řízení spotřeby. Pro rychlou a snadnou instalaci a nastavení se podívej na článek [Škálování frekvence procesoru](/index.php/%C5%A0k%C3%A1lov%C3%A1n%C3%AD_frekvence_procesoru "Škálování frekvence procesoru").

## Pm-utils

[Pm-utils](/index.php/Pm-utils "Pm-utils") poskytuje framework pro nastavení uspání a hibernace. Pm-utils by měl být používáam spolu s cpufrequtils pro poskytnutí kompletního řešení řízení spotřeby.

## Lapsus

[Lapsus](/index.php/Asus_G1#The_Lapsus_daemon_.26_KDE_applet "Asus G1") je soubor programů poskytujících jednoduchý přístup k mnoha různým funkcím notebooků. Momentálně podporuje nejvíce funkcí poskytovaných modulem jádra asus-laptop z projektu ACPI4Asus, jedná se například o přídavné LED diody, změna podsícení atd. Má například podporu i pro některé funkce notebooků IBM poskytovaných ovladačem IBM ThinkPad ACPI Extras a ovladačem zařízení VRAM.

## Instalace powertopu

Tento užitečný nástroj od Intelu ti poví, který hardware resp. které aplikace konzumují nejvíce energie z tvého systému a poskytují instrukce jak zastavit/odstranit služby, které plýtvají energií. Výborně pracuje spolu s mobilními procesory Intel; poskytuje momentální stav procesoru a návrhy pro zvýšení úspory energie. Pracuje také spolu se systémy AMD, ale neposkytuje tolik informací ohledně stavu procesoru. Nainstaluj jej tímto příkazem:

```
# pacman -S powertop

```

## Laptop mode tools

Nainstaluj [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools"):

```
# pacman -S laptop-mode-tools

```

*   Konfigurační soubory můžeš nalézt zde: /etc/laptop-mode/laptop-mode.conf a /etc/laptop-mode.conf/conf.d/*
*   Ujisti se, že démon _laptop-mode_ je přidán v řádku DAEMONS v souboru /etc/rc.conf
*   Projdi všechni konfigurační soubory, mnoho úsporných funkcí totiž není implicitně povoleno.

Následuj [toto vlákno(anglicky)](https://bbs.archlinux.org/viewtopic.php?id=39258) s pro více informací.

## Powernowd

[Powernowd](/index.php/Powernowd "Powernowd") je program pro dynamické nastavování procesoru, může být použit na systémech založených na AMD-based Intel.

Nainstaluj jej příkazem:

```
# yaourt -S powernowd

```

Pro jeho konfiguraci prostě uprav soubor /etc/conf.d/powernowd tímto způsobem:

```
OPTIONS="-q -u 15 -l 5"

```

## Návhry pro šetření energie

	_Poznámka_: Ne všechny tyto tipy jsou nezbytné pokud používáš laptop-mode=tools, používání laptopmode ti navíc dá možnost aplikovat tyto funkce tehdy, kdy si přeješ(např. když je zdroj připojen nebo odpojen).

### Nastavení disků

Zakaž změnu času přístupu k souborům: pokaždé když přistopíš(čteš) soubor, souborový sysém zípíše přístupový čas do metadat souboru. Toto můžeš zakázat individuálně na jednotlivých souborech použitím příkazu chattr nebo pro celý disk nastavením _noatime_ v souboru /etc/fstab tímto způsobem:

```
/dev/sda1          /          ext3          defaults,noatime          1  2

```

[Zdroj](http://www.faqs.org/docs/securing/chap6sec73.html)

	_Poznámka_: zakázaní atime způsobuje problémy s aplikací [mutt](/index.php/Mutt "Mutt") a některými dalšími, které používají časové známky souborů. Zvaž kompromis mezi výkonem a kompaktibilitou při použití možností relatime místo atime, nebo se podívej na [mutt jak obejít noatime](http://wiki.mutt.org/?MaildirFormat)

Aby se po určitém čase přestaly točit hlavičky CD/DVD rom, spust následující:

```
/usr/bin/hal-disable-polling --device /dev/scd0

```

### Další nastavení

Zde je několik obecných návrhů, které fungují se všemi notebooky.

Přidej následující do _/etc/modprobe.d/modprobe.conf_:

```
options usbcore autosuspend=1

```

Přidej následující do `/etc/sysctl.d/99-sysctl.conf`

```
vm.dirty_writeback_centisecs=1500
vm.laptop_mode=5

```

Přidej následující do _/etc/rc.local_ (a ujisti se že to bude spuštěno při startu OS)

```
/usr/sbin/iwpriv your_wireless_interface set_power 5

```

Zdroj: [zde](http://www.nervous.it/2007/11/linux-dell-xps-m1330/)

### Problém s točícími se hlavičkami pevného disku

Dokuentováno [zde](https://bugs.launchpad.net/ubuntu/+source/acpi-support/+bug/59695)

Pro zabránění příliš častému roztáčení ploten pevného disku (výsledek příliš agresivních impicitních nastavení APM) udělěj následující

Přidej následující do _/etc/rc.local_

```
hdparm -B 254 /dev/sdX _kde X je tvůj pevný disk_

```

Hodnotu můžes také nastavit na 255 pro kompletní vypnutí roztáčení ploten. Můžeš si také přát nastavit nižší hodnotu pokud se s notebookem pohybuješ pro eliminování šance zničení pevného disku při pohybu. Pokud se s notebookem beěhem jeho užívání nepohybuješ, nastavení hodnoty na 254 nebo 255 je pravděpodobně nejlepší. Pokud však ano, můžes zkusit nastavit nížší hodnotu. Hodnota kolem 128 může být zlatým středem.

Přidej následující do _/etc/pm/sleep.d/50-hdparm_pm_

```
#!/bin/sh

if [ -n "$1" ] && ([ "$1" = "resume" ] || [ "$1" = "thaw" ]); then
	hdparm -B 254 /dev/tvůj-pevný-disk > /dev/null
fi

```

a spusť "chmod +x /etc/pm/sleep.d/50-hdparm_pm" pro ujištění se, že se to restartuje při uspání. Znovu, můžeš změnít hodnotu 254 dle libosti.

Nyní by měl být nastaven APM level pro tvůj pevný disk. Now the APM level should be set for your hard drive.

Pro některé notebooky může být relevantní volba -S nástroje hdparm (nastavuje čas pro dotočení hlaviček jednotky). Měj na paměti že všechny tyto volby mohou být nakonfigurovány pomocí [laptop-mode tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools"). To ti také umožní nastavit vyšší hodnotu pokud notebook nabíjíš a nižší při čerpání energie z baterie.

### Nastavení plánovače

Pro vícejádrové procesory a procesory s povoleným hyperthreadingem můžeš použít volbu sched_mc_power_savings resp. sched_smt_power_savings pro nastavení klidového klidu tolika jádrům, kolika je jen možno. Pro povolení této možnosti udělej toto

```
echo 1 > /sys/devices/system/cpu/sched_mc_power_savings

```

nebo

```
echo 1 > /sys/devices/system/cpu/sched_smt_power_savings

```

Pro zakázání použij 0\. Také laptop-mode může být použit pro nastavení shed_mc_power_savings (podívej se na odpovídající konfigurační soubor v /etc/laptop-mode/conf.d). --[Kasbah](/index.php?title=User:Kasbah&action=edit&redlink=1 "User:Kasbah (page does not exist)") 16:14, 14 August 2009 (EDT)

# Touchpad

Pro správnou funkcni touchpadu se podívej na tuto stránku [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"). Tvůj notebook může mít ALP touchpad (např. DELL Inspiron 6000) místo Synaptics touchpadu. Tak i tak, podívej se na odkaz viz výše.

# Speciální tlačítka

Pro konfiguraci speciálních tlačítek na tvém notebooku prosím následuj na následující článek: [Customize your laptop keyboard with X and KDE](http://www.linux.com/feature/118179). KDE není nutné.

# Ochrana pevného disku proti šoku

Několik notebooku různých výrobců má možnost ochrany proti šoku. Výrobci odmítli podpořit open source vývoj potřebného software, takže je podpora v Linuxu velice různá v závislosti na hardwarové implementaci.

Tuto možnost ochrany momentálně podporuje jen projekt HDAPS, který je připravován pro notebooky IBM/Lenovo Thinkpad.

Podívej se sem [Aktivní ochranný systém pevného disku](/index.php/HDAPS "HDAPS").