Konfigurace wifi je dvoufázový proces. V první fázi je třeba identifikovat ovladač vhodný pro vaše síťové zařízení a ujistit se, že je ovladač správně nainstalován (ovladače jsou dostupné na instalačním médiu, je vhodné se ujistit, že jsou skutečně nainstalovány) a nastavit síťové rozhraní. V druhé fázi je třeba zvolit způsoby správy bezdrátové síťového připojení. Tento článek obě fáze popisuje a obsahuje odkazy na nástroje pro správu bezdrátových sítí.

**Instalace nového systému Archlinux:** Ovladače síťových karet a nástroje pro správu naleznete v kategorii *base-devel*. Zde je třeba zvolit k instalaci správný ovladač pro vaše zařízení. Udev si pak obvykle načte příslušný jaderný modul, čímž vytvoří bezdrátové rozhraní, které je použitelné už během instalace a samozřejmě také v nově instalovaném systému na pevném disku. Pokud jste nenastavili bezdrátovou síť během instalace a provádíte konfiguraci v již instalovaném systému, ujistěte se, že jste pomocí správce balíků pacman nainstalovali potřebný software (ovladač, případně i firmware, wireless_tools, wpa_supplicant) a dále postupujte podle návodu níže.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Fáze I: Identifikace zařízení / Instalace ovladače](#Fáze_I:_Identifikace_zařízení_/_Instalace_ovladače)
    *   [1.1 Identifikace a podpora zařízení](#Identifikace_a_podpora_zařízení)
    *   [1.2 Jak to funguje?](#Jak_to_funguje?)
    *   [1.3 Instalace](#Instalace)
        *   [1.3.1 Když máte k dispozici bezdrátový internet](#Když_máte_k_dispozici_bezdrátový_internet)
        *   [1.3.2 Když máte k dispozici pouze bezdrátový internet](#Když_máte_k_dispozici_pouze_bezdrátový_internet)
    *   [1.4 Ovladače a firmware](#Ovladače_a_firmware)
        *   [1.4.1 wlan-ng (zastaralé)](#wlan-ng_(zastaralé))
        *   [1.4.2 rt2860 and rt2870](#rt2860_and_rt2870)
        *   [1.4.3 w322u](#w322u)
        *   [1.4.4 rtl8180](#rtl8180)
        *   [1.4.5 rtl8192e](#rtl8192e)
        *   [1.4.6 rtl8192s](#rtl8192s)
        *   [1.4.7 rt2x00](#rt2x00)
        *   [1.4.8 rt2500, rt61, rt73 (zastaralé)](#rt2500,_rt61,_rt73_(zastaralé))
        *   [1.4.9 madwifi-ng](#madwifi-ng)
        *   [1.4.10 ath5k](#ath5k)
        *   [1.4.11 ath9k](#ath9k)
        *   [1.4.12 ath9k_htc](#ath9k_htc)
        *   [1.4.13 ipw2100 and ipw2200](#ipw2100_and_ipw2200)
            *   [1.4.13.1 Povolení radiotap rozhraní](#Povolení_radiotap_rozhraní)
            *   [1.4.13.2 Povolení LED](#Povolení_LED)
        *   [1.4.14 iwl3945, iwl4965 and iwl5000-series](#iwl3945,_iwl4965_and_iwl5000-series)
            *   [1.4.14.1 Instalace Firmwaru (Microcode)](#Instalace_Firmwaru_(Microcode))
            *   [1.4.14.2 Načtení Driveru](#Načtení_Driveru)
            *   [1.4.14.3 Vypnutí problikávání](#Vypnutí_problikávání)
            *   [1.4.14.4 Other Notes](#Other_Notes)
        *   [1.4.15 ipw3945 (obsolete)](#ipw3945_(obsolete))
        *   [1.4.16 orinoco](#orinoco)
        *   [1.4.17 ndiswrapper](#ndiswrapper)
        *   [1.4.18 prism54](#prism54)
        *   [1.4.19 ACX100/111](#ACX100/111)
        *   [1.4.20 zd1211rw](#zd1211rw)
        *   [1.4.21 carl9170](#carl9170)
    *   [1.5 Test instalace](#Test_instalace)
*   [2 Fáze II: Správa bezdrátových sítí](#Fáze_II:_Správa_bezdrátových_sítí)
    *   [2.1 Management methods](#Management_methods)
        *   [2.1.1 Manual setup](#Manual_setup)
        *   [2.1.2 Automatic setup](#Automatic_setup)
            *   [2.1.2.1 Standard network daemon](#Standard_network_daemon)
            *   [2.1.2.2 Netcfg](#Netcfg)
            *   [2.1.2.3 Netcfg Easy Wireless LAN (newlan)](#Netcfg_Easy_Wireless_LAN_(newlan))
            *   [2.1.2.4 Wicd](#Wicd)
            *   [2.1.2.5 NetworkManager](#NetworkManager)
            *   [2.1.2.6 Wifi Radar](#Wifi_Radar)
            *   [2.1.2.7 Wlassistant](#Wlassistant)
*   [3 See also](#See_also)
*   [4 Externí odkazy](#Externí_odkazy)

## Fáze I: Identifikace zařízení / Instalace ovladače

### Identifikace a podpora zařízení

Než začnete cokoliv dělat musíte si ověřit, zda je vaše karta podporována linuxovým jádrem nebo je-li dostupný tzv. user-space ovladač (ovladač, který může zavést uživatel).

	Identifikace karty

*   Model karty zjistíte příkazem

```
$ lspci | grep -i net

```

do příkazové řádky.

*   Pokud máte USB zařízení, příkazem

```
$ lsusb

```

**Note:** Interní wifi karty některých notebooků jsou ve skutečnosti USB zařízení.

	Jak zjistit, že je síťová karta podporována

*   [Ubuntu Wiki](https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported) obsahuje seznam síťových karet podporovaných linuxovým jádrem nebo user-space ovladačem.
*   Rozsáhlou databázi hardware podporovaného linuxovým kernelem najdete i na [Linux Wireless Support](http://linux-wless.passys.nl/) a The Linux Questions' [Hardware Compatibility List](http://www.linuxquestions.org/hcl/index.php?cat=10) (HCL).
*   Dalším zdrojem informací je seznam podporovaného hardware na [wireless.kernel.org](http://wireless.kernel.org/en/users/Devices).

	Když vaše karta není na seznamu

*   Pokud vaše bezdrátová síťová karta není v žádném seznamu, je pravděpodobně podporována pouze pod MS Windows (některé karty Broadcom, 3com a podobně.). V tomto případě budete muset použít [ndiswrapper](http://ndiswrapper.sourceforge.net/wiki/index.php/List). [Ndiswrapper (Česky)](/index.php?title=Ndiswrapper_(%C4%8Cesky)&action=edit&redlink=1 "Ndiswrapper (Česky) (page does not exist)") je softwarová mezivrstva, umožňující běh některých ovladačů windows v Linuxu. Seznam podporovaného hardwaru je [zde](http://ndiswrapper.sourceforge.net/mediawiki/index.php/List). Budete potřebovat soubory `.inf` a `.sys` z instalačních souborů ovladače pro Windows. Pokud máte hodně novou nebo neobvyklou síťovou kartu, budete asi muset před provedením tohoto kroku přesně zjistit model jejího hardware a vyhledat ho na internetu ve spojení se slovem 'linux'.

### Jak to funguje?

Výchozí jádro linux je *modulární*, to znamená, že ovladače pro různý hardware jsou dostupné na disku jako *moduly*. [Udev (Česky)](/index.php/Udev_(%C4%8Cesky) "Udev (Česky)") má při bootu k dispozici seznam vašeho hardwaru, pomocí kterého načte příslušné jaderné moduly (ovladače), čímž umožní vytvoření rozhraní.

Rozhraní jednotlivých ovladačů budou různá u jednotlivých typů karet. Např wlan0, eth1, ath0, ...

*   Upozornění: Udev není perfektní. Když dev nenačte správný modul při bootu, jednoduše ho načteme ručně příkazem "modprobe jméno_modulu" a přidáme jméno_modulu do /etc/rc.conf do řádku **MODULES=**. Udev může také občas načíst více modulů pro jedno zařízení, a výsledný konflikt může zabránit korektní konfiguraci. Nepotřebné moduly můžete zablokovat například [takto](#carl9170).

### Instalace

#### Když máte k dispozici bezdrátový internet

Pokud máte k dispozici bezdrátový internet, a je jednoduché přidat do systému podporu pro bezdrátové sitě, ale nemáte k dispozici nástroje pro správu těchto sítí, použijte pacmana k instalaci:

```
$ pacman -S wireless_tools

```

Balíčky, korespondující názvy s ovladači, jsou na této stránce zvýrazněny **tučně**. Balíčky mohou být nainstalovány při instalaci systému při volbě balíčků, nebo později, e.g.:

```
$ pacman -S madwifi

```

#### Když máte k dispozici pouze bezdrátový internet

**Wireless_tools** balíček je nyní k dispozici jako součást zádkladního systému a je také obsažen v live instalačním mediu (CD/USB stick image) v kategorii **base-devel**.

Nemůžete používat tato bezdrátová zařízení bez uživatelských nástrojů, ujistěte se tedy, že tyto nástroje jsou nainstalovány (při volbě balíčků), zvláště pokud nemáte k dispozici jiné, než bezdrátové sítě, jinak uvíznete v systému bez možnosti připojení.

### Ovladače a firmware

Metody a procedury pro instalaci ovladačů pro různé chip-sety jsou jsou uvedeny níže. Kromě toho, některé čipové sady-vyžadují instalaci odpovídajícího *firmware*(uvedeno také níže).

#### wlan-ng (zastaralé)

Balíčky: **wlan-ng26-utils**

Tento ovladač podporuje PRISM based karty, které jsou dnes těžko k nalezení. PRISM karty jsou IEEE 802.11 vyhovující 2.4 GHz DSSS WLAN síťová karta, která používá čip Intersil PRISM pro své radio funkce a AMD PCnet-Mobile čip (AM79C930) pro Media Access Controller (MAC) funkce. Podporované adaptéry zde: [http://www.linux-wlan.org/docs/wlan_adapters.html.gz](http://www.linux-wlan.org/docs/wlan_adapters.html.gz)

Pro wlan-ng nepotřebujete wireless_tools balíček. Namísto toho se musíte naučit s nástroji obsaženými v balíčku wlan-ng26-utils: **wlancfg and wlanctl-ng**.

Více na [http://www.linux-wlan.org/](http://www.linux-wlan.org/)

#### rt2860 and rt2870

Od jádra 2.6.29 netřeba žádné extra balíčky. Může být konfigurováno použitím standardních wpa_supplicant a iwconfig nástrojů. To bohužel neplatí pro Arch. Při snaze dát to do pořádku se ukázalo jako funkční řešení zakázání těchto modulů:

```
rt2800pci rt61pci rt2x00pci rt2800usb rt2800lib rt2x00usb rt2x00lib

```

Nabízí celou řadu možností konfigurace s iwpriv. Ty jsou zdokumentovány na [source tarballs](http://web.ralinktech.com/ralink/Home/Support/Linux.html) od Ralinku.

Pro rt2870sta, viz [Rt2870](/index.php/Rt2870 "Rt2870")

#### w322u

S touto Tenda kartou zacházejte jako s rt2870sta. Viz: [Rt2870](/index.php/Rt2870 "Rt2870")

#### rtl8180

Realtek rtl8180 PCI/Cardbus 802.11b plně podporovaná v jádře. Konfigurovatelná se standardními wpa_supplicant a iwconfig tools.

#### rtl8192e

Plně podporovaná v jádře. Konfigurovatelná se standardními wpa_supplicant a iwconfig tools.

#### rtl8192s

Driver je součástí jádra. Firmware může být třeba přidat ručně pokud se nenachází v /lib/firmware/RTL8192SU/rtl8192sfw.bin. (dmesg hlásí *"rtl819xU:FirmwareRequest92S(): failed"* když firmware chybí)

Stažení a instalace firmwaru:

```
$ wget http://launchpadlibrarian.net/33927923/rtl8192se_linux_2.6.0010.1012.2009.tar.gz
# mkdir /lib/firmware/RTL8192SU
# tar -xzOf rtl8192se_linux_2.6.0010.1012.2009.tar.gz \
  rtl8192se_linux_2.6.0010.1012.2009/firmware/RTL8192SE/rtl8192sfw.bin > \
  /lib/firmware/RTL8192SU/rtl8192sfw.bin
```

Upozornění: Alternativní verze firmwaru se nachází [zde](http://launchpadlibrarian.net/37387612/rtl8192sfw.bin.gz), ale tato verze může způsobit ztráty spojení.

Upozornění: [wicd](/index.php/Wicd "Wicd") může s tímto ovladačem ztrácet spojení, [NetworkManager](/index.php/NetworkManager "NetworkManager") funguje lépe.

#### rt2x00

Ovladač pro čipy Ralink (nahrazuje rt2500,rt61,rt73 etc). V jádře od 2.6.24, některá zařízení ale vyžadují extra firmware. Konfigurovatelné se standardními wpa_supplicant a iwconfig nástroji.

Některé čipy vyžadují firmware, který může být instalován následovně, v závislosti na čip-setu:

 `pacman -S linux-firmware` 

Viz: [Using the new rt2x00 beta driver](/index.php/Using_the_new_rt2x00_beta_driver "Using the new rt2x00 beta driver")

#### rt2500, rt61, rt73 (zastaralé)

Pro Ralink

```
* PCI/PCMCIA based rt2500 series chip-sets.
* PCI/PCMCIA based rt61 series chip-sets
* USB based rt73 series chip-sets. 

```

Ovladače jsou teď **zastaralé** a **nepodporované**. Namísto nich jsou tu stabilní ovladače z rodiny rt2x00.

Podpora standardních iwconfig nástrojů pro nešifrované a WEP spojení, ikdyž může být citlivý na pořadí příkazů. Driver nepodporuje WPA (pomocí hardwarového šifrování), ale nestandardní cestou wpa_supplicant, zdá se, zahrnuje speciální podporu pro tento ovladač, a je tedy možno, pomocí iwpriv příkazů, zajistit spojení šifrované pomocí WPA. Více najdete v [těchto instrukcích](http://rt2400.cvs.sourceforge.net/*checkout*/rt2400/source/rt2500/Module/iwpriv_usage.txt).

#### madwifi-ng

Balíček: **madwifi** (nebo **madwifi-utils**)

Modul se nazývá <tt>ath_pci</tt>.

Zde jsou novějšní moduly od MadWifi týmu:

*   [ath5k](#ath5k) v budoucnu eventuelně nahradí ath_pci. Dnes lepší pro některé čipsety.
*   [ath9k](#ath9k) je nový kvalitnější oficialní ovladač pro novější hardware od Atheros (viz níže).

```
modprobe ath_pci

```

pro starší ovladače, nebo:

```
modprobe ath5k

```

pro vývojovou verzi. Upozornění: Ne všechna zařízení již fungují s ath5k.

Když použijete ath_pci, možná budete muset zablokovat ath5k přidáním do řádku MODULES= in /etc/rc.conf, a použitím prefixu bang(!):

```
MODULES=(!ath5k forcedeth snd_intel8x0 ... ...)

```

Někteří uživatelé **mohou potřebovat** použít 'countrycode' k načtení MadWifi ovladače za účelem využití kanálů a vysílacích výkonů, které jsou legální v jejich zemi / regionu. V nizozemsku například načtete modul takto::

```
modprobe ath_pci countrycode=528

```

Nastavení můžete zkontrolovat příkazem <tt>iwlist</tt>. Viz. <tt>man iwlist</tt> a [CountryCode na MadWifi wiki](http://madwifi-project.org/wiki/UserDocs/CountryCode). Pro automatické načtení tohoto nastavení při bootu, přidejte následující do <tt>/etc/modprobe.d/modprobe.conf</tt>:

**Note:** Nový module-init-tools 3.8 balíček mění lokaci konfiguračního souboru: namísto /etc/modprobe.conf je to nyní /etc/modprobe.d/modprobe.conf. [link](https://www.archlinux.org/news/450/)

```
options ath_pci countrycode=528

```

**Note:** Uživatel musel zcela odstranit countrycode, nebo nebylo vytvořeno jiné ath0 zařízení (kernel 2.6.21).

#### ath5k

ath5k je preferovaný ovladač pro AR5xxx, a to včetně těch, které již pracují s madwifi-ng. Lze ho použít i pro některé chipsety starší než AR5xxx.

Pokud je ath5k v konfliktu s ath_pci, odstraňte následující moduly z paměti pomocí rmmod nebo vypněte jejich automatické načítaní pomocí blacklistu do `/etc/modprobe.d/wireless.conf`

```
ath_hal
ath_pci
ath_rate_amrr
ath_rate_onoe
ath_rate_sample
wlan
wlan_acl
wlan_ccmp
wlan_scan_ap
wlan_scan_sta
wlan_tkip
wlan_wep
wlan_xauth

```

Potom pomocí modprobe načtěte modul ath5k. Rozhraní wlan0 (nebo wlanX) by mělo být funkční.

Info:

*   [http://wireless.kernel.org/en/users/Drivers/ath5k](http://wireless.kernel.org/en/users/Drivers/ath5k)
*   [http://wiki.debian.org/ath5k](http://wiki.debian.org/ath5k)

**Note:** Některé notebooky mají problémy blikajícím bezdrátovým LED indikátorem. Řešení je zde:
```
echo none > "/sys/class/leds/ath5k-phy0::tx/trigger"
echo none > "/sys/class/leds/ath5k-phy0::rx/trigger"

```
Alternativní řešení {{[zde](https://bugzilla.redhat.com/show_bug.cgi?id=618232)}}

#### ath9k

ath9k je oficiálně podporovaný ovladač Atheros' pro novější 11n čip-sety. Všechny čipy s 11n schopnostmi jsou podporovány, s maximální šířkou pásma 180 Mbps. Pro kompletní seznam podporovaného hardwaru, čekujte tuto [stránku](http://wireless.kernel.org/en/users/Drivers/ath9k).

Funkční režimy: Station, AP a Adhoc.

ath9k byl součástí jádra 2.6.27, a zdá se že je podporován i v jádře 2.6.32 (viz [details on linuxwireless.org](http://linuxwireless.org/en/users/Drivers/ath9k/bugs#Minimal_kernel_requirements)). (Pokud máte problémy se stabilitou, můžete použít tento [compat-wireless](http://wireless.kernel.org/en/users/Download) balíček. Na tomto [ath9k mailing listu](https://lists.ath9k.org/mailman/listinfo/ath9k-devel) se nachází diskuse o podpoře a vývoji.)

Info:

*   [http://wireless.kernel.org/en/users/Drivers/ath9k](http://wireless.kernel.org/en/users/Drivers/ath9k)
*   [http://wiki.debian.org/ath9k](http://wiki.debian.org/ath9k)

#### ath9k_htc

ath9k_htc je oficiální podporovaný ovladač pro 11n USB zařízení Atheros'. Jsou podporovány režimy Station a Ad-Hoc. Od jádra 2.6.35 je ovladač zahrnut v jádře. Více informací viz [http://wireless.kernel.org/en/users/Drivers/ath9k_htc](http://wireless.kernel.org/en/users/Drivers/ath9k_htc) .

#### ipw2100 and ipw2200

Plně podporován v jádře, ale vyžaduje dodatečný firmware. Konfigurovatelné standardními wpa_supplicant a iwconfig nástroji.

V závislosti na čipu jaký máte, použijte:

**ipw2100-fw**

```
pacman -S ipw2100-fw

```

or:

**ipw2200-fw**

```
pacman -S ipw2200-fw

```

Když instalujete po instalaci systému, modul může být třeba znovunačíst kvůli načtení firmware; jako root použijte následující příkazy:

```
rmmod ipw2200
modprobe ipw2200

```

##### Povolení radiotap rozhraní

Spusttě následující (jako root):

```
rmmod ipw2200
modprobe ipw2200 rtap_iface=1

```

##### Povolení LED

Většina notebooků ma přední LED k indikaci funkce wifi (připojení). Spustte následující (jako root):

```
echo "options ipw2200 led=1" >> /etc/modprobe.d/ipw2200.conf

```

nebo pomocí sudo:

```
echo "options ipw2200 led=1" | sudo tee -a /etc/modprobe.d/ipw2200.conf

```

#### iwl3945, iwl4965 and iwl5000-series

**I**ntel's open source **W**iFi ovladače pro **L**inux (Viz [iwlwifi](http://intellinuxwireless.org)) funguje pro oba 3945 a 4965 čipsety od jádra 2.6.24\. Moduly pro iwl5000-series čipsety (včetně 5100BG, 5100ABG, 5100AGN, 5300AGN a 5350AGN) jsou podporovány od **kernelu 2.6.27**, ovladačem **iwlagn**.

##### Instalace Firmwaru (Microcode)

**Důležité:** Instalace tohoto firmware není potřeba od updatu jádra 2.6.34, kde byl firmware přesunut do balíčku linux-firmware:

```
# pacman -S linux-firmware

```

Pokud potřebujete bezdrátové připojení k zpřístupnění repositářů, Je firmware dostupný přímo od Intelu. Viz [this](http://intellinuxwireless.org/?n=downloads) , stačí zvolit a stáhnout archiv .

```
$ wget [http://intellinuxwireless.org/iwlwifi/downloads/iwlwifi-XXXX-ucode-XXX.XX.X.XX.tgz](http://intellinuxwireless.org/iwlwifi/downloads/iwlwifi-XXXX-ucode-XXX.XX.X.XX.tgz)

```

Po stažení musíte rozbalit a zkopírovat *.ucode soubor do správného umístění pro firmware, většinou /lib/firmware

```
# tar zxvf iwlwifi-XXXX-ucode-XXX.XX.X.XX.tgz
# cd iwlwifi-XXXX-ucode-XXX.XX.X.XX/
# cp iwlwifi-XXXX-X.ucode /lib/firmware/

```

##### Načtení Driveru

Když je MOD_AUTOLOAD (defaultně v /etc/rc.conf) nastaven na ano(yes), mělo by to být vše co je potřeba. Jednoduše zkontrolujete přítomnost ovladače příkazem **ifconfig -a** v terminálu. Tam by měl být seznam pro wlan0.

Toto proveďte POUZE když MOD_AUTOLOAD není nastaven: manualně načtěte ovladač při startupu, editujte <tt>/etc/rc.conf</tt> jako root a a přidejte **iwl3945** or **iwl4965** to řádku MODULES. Například takto:

```
MODULES=( ... b44 mii **iwl3945** snd-mixer-oss ...)

```

Drivery by ted měly najet při bootu systemu, a ve výpisu příkazu **ifconfig -a** v terminalu, by měly hlásit **wlan0** jako nové síťové rozhraní.

##### Vypnutí problikávání

V defaultním nastavení LED dioda indikující aktivní wifi problikává. Pokud je vám to nepříjemné, můžete toto nastavení změnit pomocí:

```
# echo "options iwlcore led_mode=1" >> /etc/modprobe.d/modprobe.conf
# rmmod iwlagn
# rmmod iwlcore
# modprobe iwlcore
# modprobe iwlagn

```

##### Other Notes

*   Windows NETw4x32 ovladač může být použit s ndiswrapperem jako alternativa k iwl3945 a ipw3945 ovladač
*   V některých případech (specificky [Dell Latitude D620](/index.php/Dell_Latitude_D620 "Dell Latitude D620") a Arch 2008.06, ikdyž by se mohlo stát i jinde) po instalaci můžete mít oba moduly iwl3945 i ipw3945 ve vašem <tt>MODULES=()</tt> sekci rc.conf. Karta se spuštěnými dvěma moduly nefunguje, takže zablokujte pomocí ! modul ipw3945 a restartujte system, nebo stopněte modul ručne, před použitím vaší síťové karty.
*   Defaultně je modul iwl3945 konfigurován k použití jen na síťových kanálech 1-11\. Vyšší rozsahy nejsou v některých částech světa (US) dovoleny. V EU jsou však zcela běžně používány i kanály 12 a 13\. Scan na všech kanálech s iwl3945 spustíte přídáním "options cfg80211 ieee80211_regdom=EU" do /etc/modprobe.d/modprobe.conf. S "iwlist f" můžete kontrolovat který kanál je povolen.
*   Pokud chcete povolit více kanálů s Intel Wifi 5100 (a pravděpodobně i s jinými) můžete to učinit s balíčkem crda. Po instalaci editujte /etc/conf.d/wireless-regdom a zakomentujte řádek kde najdete countrycode vaší země. Přidejte wireless-regdom do DAEMONS v rc.conf a restartujte (jednodušší způsob). Nyní můžete příkazem sudo iwlist wlan0 channel, mít přístup k více kanálům (v závislosti na vaší pozici).
*   Wifi správa napájení může být povolena přidáním:

iwconfig wlan0(změňte dle potřeby) power v /etc/rc.local.

#### ipw3945 (obsolete)

**Note:** *ipw3945 ovladač není nadále aktivně vyvíjen, a iwlwifi ovladač (popsán níže) funguje perfektně, ale může dojít ke konfliktu s předcházejícím. Proto by měl být nainstalován pouze jeden z nich. I pokud se rozhodnete používat iwlwifi **ipw3945-ucode** balíček je stále vyžadován.*

```
# pacman -S ipw3945 ipw3945-ucode ipw3945d

```

Pro inicializaci ovladače při startu, editujte <tt>/etc/rc.conf</tt> jako root a přidejte **ipw3945** do sekce MODULES a **ipw3945d** do sekce DAEMONS. Příklad:

```
MODULES=(... mii **ipw3945** snd-mixer-oss ...)

```

```
DAEMONS=(syslog-ng **ipw3945d** network ...)

```

**Upozornění:** **ipw3945d** démon *musí* být vložen PŘED všemi ostatními síťovýmí démony v dané sekci.

#### orinoco

Mělo by být součástí jádra a již nainstalován.

Upozornění: Některé čip-sety orinico jsou Hermes I/II. Můžete použít [https://aur.archlinux.org/packages.php?ID=9637](https://aur.archlinux.org/packages.php?ID=9637) k nahrazení ovladače orinoco a zpřístupnění WPA. Více [http://ubuntuforums.org/showthread.php?p=2154534#post2154534](http://ubuntuforums.org/showthread.php?p=2154534#post2154534) .

K použití ovladač zablokujte orinoco_cs v rc.conf (!orinoco_cs v sekci MODULES) a přidejte wlags49_h1_cs. Příklad:

```
MODULES=(!eepro100 *!orinoco_cs* **wlags49_h1_cs**)

```

#### ndiswrapper

Ndiswrapper není realný ovladač, ale můžete ho použít, když pro vaše zařízení neexituje nativní ovladač pro Linux. V některých situacích je velmi nápomocný. K funkci vyžaduje *.inf soubor z instalačních souborů Windows ovladačů (*.sys soubor musí být také přítomen ve stejné složce). Ujistěte se že máte ovladač určený pro svou architekturu (32/64bit). Pokud potřebujete tyto soubory extrahovat z *.exe souboru, můžete použít cabextract nebo wine. Ndiswrapper je v instalačním CD Archlinuxu.

Konfigurace ndiswrapperu.

```
#Instalujte ovladač do /etc/ndiswrapper/*
ndiswrapper -i filename.inf
#List instalovaných ovladačů pro ndiswrapper
ndiswrapper -l
#Konfigurační soubor pište v /etc/modprobe.d/ndiswrapper.conf
ndiswrapper -m
depmod -a
```

Instalace je temř u konce; upravte /etc/rc.conf pro načtení modulu při bootu. Příklad:

 `MODULES=(ndiswrapper snd-intel8x0 !usbserial)` 

Důležitá část je ujištěbí se, že ndiswrapper je v tomto řádku, takže ho stačí přidat k ostatním modulům. Nejlepší by bylo otestovat, jestli se nyní načte, takže:

```
modprobe ndiswrapper
iwconfig
```

a wlan0 by nyní mělo existovat. Pokud máte problémy, navštivte tuto stránku: [Ndiswrapper installation wiki](http://ndiswrapper.sourceforge.net/joomla/index.php?/component/option,com_openwiki/Itemid,33/id,installation/).

#### prism54

Stáhněte ovladač pro vaši kartu z [této stránky](http://linuxwireless.org/en/users/Drivers/p54). Přejmenujte soubor s firmwarem na 'isl3890'. Pokud neexistuje, vytvořte adresář /lib/firmware a soubor 'isl3890' do něj umístěte. To by měl být ten trik. [[1]](https://bbs.archlinux.org/viewtopic.php?t=16569&start=0&postdays=0&postorder=asc&highlight=siocsifflags+such+file++directory)

Pokud to nefunguje, zkuste toto:

*   Znovunačtěte prism modul (modprobe p54usb nebo modprobe p54pci, v závislosti na vašem hardware)

popřípadě vyjměte vaši wifi kartu a pak ji znovu připojte

*   Použíjte příkaz "dmesg", a na konci výstuúpu tohoto příkazu hledejte něco podobné tomuto:

```
firmware: requesting **isl3887usb_bare**
p54: LM86 firmware
p54: FW rev 2.5.8.0 - Softmac protocol 3.0

```

a zkuste přejmenovat soubor s firmwarem na jmeno korespondující s tím v tomto výstupu.

Pokud dostanete zprávu

```
SIOCSIFFLAGS: Operation not permitted

```

když provádíte 'ifconfig wlan0 up' NEBO pokud se

```
prism54: Your card/socket may be faulty, or IRQ line too busy :(

```

objeví v dmesg, máte pravděpodobně ve stejný čas načteny oba moduly "prism54" a novější modul "p54pci" nebo "p54usb", a ty spolu bojují o kontrolu nad IRQ. Použijte příkaz "lsmod | grep prism54" pro zjištění, zda je skutečně načten i zastaralý modul. Pokud potrebujete zastavit loadování modulu "prism54", použijte [blacklisting](/index.php/Blacklisting "Blacklisting")(existuje několik způsobů, jak toho dosáhnout, které jsou popsány jinde). Once blacklisted, you may find you have to rename the firmware as prism54 and p54pci/p54usb look for different firmware filenames (i.e. recheck the dmesg output after performing ifconfig wlan0 up).

#### ACX100/111

balíčky: tiacx tiacx-firmware

Ovladač by vám měl říci, jaký firmware je potřeba; zkontrolujte /var/log/messages.log nebo pouzijte příkaz dmesg.

Odpovídající firmware umístěte do '/lib/firmware':

```
ln -s /usr/share/tiacx/acx111_2.3.1.31/tiacx111c16 /lib/firmware

```

Pro zjištění jaká revize firmware je potřeba, čtěte ["Which firmware" sekci](http://acx100.sourceforge.net/wiki/Firmware) acx100.sourceforge wiki. For ACX100, you can follow the links provided there, to a table of card model number vs. "firmware files known to work"; v příponě tam můžete zjistit revizní číslo, které potřebujete. E.g. a dlink_dwl650+ uses "1.9.8.b", in which case you'd do this:

```
ln -s /usr/share/tiacx/acx100_1.9.8.b/* /lib/firmware

```

Pokud zjistíte, že modul spamuje váš kernel log, např. protože vám běží Kismet s channel-hopping, můžete toto umístit do /etc/modprobe.d/modprobe.conf:

```
options acx debug=0

```

**Note:** Open-source ovladač acx nepodporuje WPA/RSN šifrování. To můžete zprovoznit pomocí ovladače z windows přes ndiswrapper. Viz kapitola ndiswrapper na této stránce.

#### zd1211rw

[zd1211rw](http://zd1211.wiki.sourceforge.net/) je ovladač pro čipovou sadu ZyDAS ZD1211 802.11b/g USB WLAN a je obsažen v linuxovém jádře. Na [[2]](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices) naleznete seznam podporovaných zařízení. Potřebujete pouze nainstalovat firmware pro dané zařízení:

 `pacman -S zd1211-firmware` 

#### carl9170

[carl9170](http://wireless.kernel.org/en/users/Drivers/carl9170/) je 802.11n USB ovladač s GPLv2 firmwarem pro Atheros USB AR9170 zařízení. Podporována jsou tato [zařízení](http://wireless.kernel.org/en/users/Drivers/carl9170#available_devices). **Firmware** není součástí balíčku linux-firmware, je k dispozici v [AUR](https://aur.archlinux.org/packages.php?ID=44102/). **Driver** je součástí **kernel 2.6.37**, pro starší zařízení použijte ovladač z [AUR](https://aur.archlinux.org/packages.php?ID=44100/). Pro použití tohoto ovladače musí být zablokován starší ovladač ar9170usb. To provedete vytvořením souboru `/etc/modprobe.d/wireless.conf` s obsahem:

```
blacklist arusb_lnx
blacklist ar9170usb

```

### Test instalace

Po načtení vašeho ovladače spusťte

```
iwconfig

```

pro ujištění se, že rozhraní (wlan*x*, eth*x*, ath*x*) nyní existuje.

Pokud se žádné rozhraní nezobrazí, zkuste zavést modul pomocí modprobe. K načtení modulu použijte příkazy **rmmod** a **modprobe**.

Příklad: když by se modul jmenoval "driverXXX", použili byste příkazy:

```
$ rmmod driverXXX # Odstraní modul z paměti
$ modprobe driverXXX # Načte modul znovu do paměti

```

Rozhraní pak zapnete pomocí příkazu:

```
$ ifconfig <jmeno_rozhrani> up

```

## Fáze II: Správa bezdrátových sítí

Assuming that your drivers are installed and working properly, you will need to choose a method for managing your wireless connections. The following subsections will help you decide the best way to do just that.

Procedure and tools required will depend on several factors:

*   The desired nature of configuration management; from a completely manual command line setup procedure repeated at each boot to a software-managed, automated solution
*   The encryption type (or lack thereof) which protects the wireless network
*   The need for network profiles, if the computer will frequently change networks (such as a laptop)

### Management methods

This table shows the different methods that can be used to activate and manage a wireless network connection, depending on the encryption and management types, and the various tools that are required. Although there may be other possibilities, these are the most frequently used:

| Management | No encryption/WEP | WPA/WPA2 PSK |
| Manual, need to repeat at each computer reboot | `ifconfig + iwconfig + dhcpcd/ifconfig` | `ifconfig + iwconfig + wpa_supplicant + dhcpcd/ifconfig` |
| Automatically managed, centralized without network profile support | define interface in `/etc/rc.conf` | not covered |
| Automatically managed, with network profiles support | `Netcfg, newlan (AUR), wicd, NetworkManager, etc…` |

More choice guide:

| - | Netcfg+Newlan(AUR) | Wicd | NetworkManager+network-manager-applet |
| auto connect at boot | with net-profiles daemon config in rc.conf | yes | yes |
| auto connect if dropped
or changed location | with net-auto-wireless daemon config in rc.conf | yes | yes |
| support 3G Modem | yes |
| GUI (proposes to manage and connect/disconnect
profiles from a systray icon.
Automatic wireless detection is also availabl) | with ArchAssitant | yes | yes |
| console tools | with wifi-select (AUR) | wicd-curses(part of wicd package) | nmcli |
| connect speed | slow | fast |

Whatever your choice, you should try to connect using the manual method first. This will help you understand the different steps that are required and debug them in case a problem arose. Another tip: if possible (e.g. if you manage your wifi access point), try connecting with no encryption, to check everything works. Then try using encryption, either WEP (simpler to configure -- but crackable in a matter of minutes, so it's hardly more secure than an unencrypted connection) or WPA.

When it comes to easy of use, NetworkManager (with Gnome network-manager-applet) and wicd have good GUIs and can provide a list of available networks to connect, they prompt for passwords, which is straightforward and highly recommended. (Note Gnome network-manager-applet also works under xfce4 if you install xfce4-xfapplet-plugin first, also there are applet available for KDE.)

#### Manual setup

The programs provided by the package **wireless_tools** are the basic set of tools to set up a wireless network. Moreover, if you use WPA/WPA2 encryption, you will need the package **wpa_supplicant**. These powerful userspace console tools work extremely well and allow complete, manual control from the shell.

These examples assume your wireless device is `wlan0`. Replace `wlan0` with the appropriate device name.

**Note:** Depending on your hardware and encryption type, some of these steps may not be necessary. Some cards are known to require interface activation and/or access point scanning before being associated to an access point and being given an IP address. Some experimentation may be required. For instance, WPA/WPA2 users may directly try to activate their wireless network from step 3.

**Step 0.** *(Optional, may be required)* At this step you may need to set the proper operating mode of the wireless card. More specifically, if you're going to connect an ad-hoc network, you might need to set the operating mode to *ad-hoc:*

```
 # iwconfig wlan0 mode ad-hoc

```

**Note:** Ideally, you should a priori know, which type of network you are going to connect. If you don't, scan the network as described in step 2 below, then, if necessary, return back to this step and change the mode. Also, please, bear in mind that changing the operating mode might require the wlan interface to be *down* (`ifconfig wlan0 down`).

**Step 1.** *(Also optional, may be required)* Some cards require that the kernel interface be activated before you can use the wireless_tools:

```
 # ifconfig wlan0 up

```

**Step 2.** See what access points are available:

```
# iwlist wlan0 scan

```

**Note:** If it displays "*Interface does not support scanning*" then you probably forgot to install the firmware. You can also try bringing up the interface first as shown in point 1.

**Step 3.** Depending on the encryption, you need to associate your wireless device with the access point to use and pass the encryption key.

Assuming you want to use the ESSID named `MyEssid`:

*   *No encryption*

```
 # iwconfig wlan0 essid "MyEssid"

```

*   *WEP*

using an hexadecimal key:

```
 # iwconfig wlan0 essid "MyEssid" key 1234567890

```

using an ascii key:

```
 # iwconfig wlan0 essid "MyEssid" key s:asciikey

```

*   *WPA/WPA2*

You need to edit the `/etc/wpa_supplicant.conf` file as described in [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant"). Then, issue this command:

```
 # wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant.conf

```

This is assuming your device uses the `wext` driver. If this does not work, you may need to adjust these options. Check [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") for more information and troubleshooting.

Regardless of the method used, you can check if you have associated successfully as follows:

```
 # iwconfig wlan0

```

**Step 4.** Finally, provide an IP address to the network interface. Simple examples are:

```
# dhcpcd wlan0

```

for DHCP, or

```
# ifconfig wlan0 192.168.0.2
# ip route add default via 192.168.0.1

```

for static IP.

Note: If you get an timeout error due to a *waiting for carrier* problem then you might have to set channel mode to auto for the specific device.

```
# iwconfig wlan0 channel auto 

```

**Note:** Although the manual configuration method will help troubleshoot wireless problems, you will have to retype every command each time you reboot.

#### Automatic setup

There are many solutions to choose from, but remember that all of them are mutually exclusive; you should not run two daemons simultaneously.

##### Standard network daemon

**Note:** This method and configuration examples are only valid for unencrypted or WEP-encrypted networks, which are particularly unsecure. To use WPA/WPA2, you will need to use other solutions such as **[netcfg](/index.php/Netcfg "Netcfg")** or **[wicd](/index.php/Wicd "Wicd")**. Also, avoid mixing these methods as they may create a conflict and prevent the wireless card from functioning.

*   The **/etc/rc.conf** file is sourced by the network script. Therefore, you may define and configure a simple wireless setup within /etc/rc.conf for a centralized approach with **wlan_<interface>="<interface> essid <essid>"** and **INTERFACES=(<interface1> <interface2>)**. The name of the network goes in place of **MyEssid**.

For example:

```
# /etc/rc.conf
eth0="dhcp"
wlan0="dhcp"
wlan_wlan0="wlan0 essid MyEssid" # Unencrypted
#wlan_wlan0="wlan0 essid MyEssid key 1234567890" # hex WEP key
#wlan_wlan0="wlan0 essid MyEssid key s:asciikey" # ascii WEP key
INTERFACES=(eth0 wlan0)

```

Not all wireless cards are `wlan0`. Determine your wireless interface with ifconfig -a. Atheros-based cards, for example, are typically `ath0`, so change `wlan_wlan0` to:

```
wlan_ath0="ath0 essid MyEssid key 12345678" 

```

Also define ath0 in the INTERFACES=line.)

*   Alternatively, you may define wlan_<interface> within /etc/conf.d/wireless, (which is also sourced by the network script), for a de-centralized approach:

```
# /etc/conf.d/wireless
wlan_wlan0="wlan0 essid MyEssid"

```

These solutions are limited for a laptop which is always on the move. It would be good to have multiple [Network Profiles](/index.php/Network_Profiles "Network Profiles") and be able to easily switch from one to another. That is the aim of network managers, such as netcfg.

##### Netcfg

**netcfg** provides a *versatile, robust and fast* solution to networking on Arch.

It uses a profile based setup and is capable of detection and connection to a wide range of network types. This is no harder than using graphical tools. Following the directions above, you can get a list of wireless networks. Then, as with graphical tools, you will need a password.

See: [Network Profiles](/index.php/Network_Profiles "Network Profiles"), and [Network Profiles development](/index.php?title=Network_Profiles_development&action=edit&redlink=1 "Network Profiles development (page does not exist)")

##### Netcfg Easy Wireless LAN (newlan)

newlan is a mono console application that starts a user-friendly wizard to create netcfg profiles, it supports also wired connections.

Install from [AUR](/index.php/AUR "AUR"): [https://aur.archlinux.org/packages.php?ID=33649](https://aur.archlinux.org/packages.php?ID=33649)

Or use the [AUR](/index.php/AUR "AUR") helper of your choice.

newlan must be run with root privileges:

```
# sudo newlan -n mynewprofile

```

##### Wicd

Wicd is a network manager that can handle both wireless and wired connections. It is written in Python and Gtk with fewer dependencies than NetworkManager, making it an ideal solution for lightweight desktop users. Wicd is now available in the extra repository for both i686 and x86_64.

See: [Wicd](/index.php/Wicd "Wicd")

##### NetworkManager

NetworkManager is an advanced network management tool that is enabled by default in most popular GNU/Linux distributions. In addition to managing wired connections, NetworkManager provides worry-free wireless roaming with an easy-to-use GUI program for selecting your desired network.

See: [NetworkManager](/index.php/NetworkManager "NetworkManager")

##### Wifi Radar

WiFi Radar is Python/PyGTK2 utility for managing wireless profiles (and *only* wireless). It enables you to scan for available networks and create profiles for your preferred networks.

See: [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar")

##### Wlassistant

Wlassistant is a very intuitive and straightforward GUI application for managing your wireless connections.

Install from AUR: [https://aur.archlinux.org/packages.php?ID=1726](https://aur.archlinux.org/packages.php?ID=1726)

Wlassistant must be run with root privileges:

```
# sudo wlassistant

```

One method of using wlassistant is to configure your wireless card within /etc/rc.conf, specifying the access point you use most often. On startup, your card will automatically be configured for this ESSID, but if other wireless networks are needed/available, wlassistant can then be invoked to access them. Background the network daemon in /etc/rc.conf, by prefixing it with a @, to avoid boot delays.

## See also

*   [Sharing ppp connection with wlan interface](/index.php/Sharing_ppp_connection_with_wlan_interface "Sharing ppp connection with wlan interface")

## Externí odkazy

*   [NetworkManager](http://www.gnome.org/projects/NetworkManager/) -- Oficiální stránka NetworkManageru
*   [WICD](http://wicd.sourceforge.net/) -- Oficiální stránka WICD
*   [Wifi Radar](https://lists.anl.gov/mailman/listinfo/wifi-radar) -- Informace o Wifi Radaru