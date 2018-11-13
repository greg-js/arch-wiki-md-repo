## Contents

*   [1 Nastavení hostname](#Nastavení_hostname)
*   [2 Nahrání ovladače (modulu) zařízeni](#Nahrání_ovladače_(modulu)_zařízeni)
*   [3 Nastavení IP adresy](#Nastavení_IP_adresy)
    *   [3.1 DHCP](#DHCP)
    *   [3.2 Statická IP](#Statická_IP)
*   [4 Aktualizace konfigurace](#Aktualizace_konfigurace)
*   [5 Některá další nastavení](#Některá_další_nastavení)
    *   [5.1 Bezdrátové sítě](#Bezdrátové_sítě)
    *   [5.2 Firewall](#Firewall)
    *   [5.3 Ifplugd](#Ifplugd)
    *   [5.4 OpenVPN](#OpenVPN)
        *   [5.4.1 Příprava](#Příprava)
        *   [5.4.2 Generování certifikátů](#Generování_certifikátů)
        *   [5.4.3 Konfigurace serveru](#Konfigurace_serveru)
        *   [5.4.4 Spusteni OpenVPN serveru](#Spusteni_OpenVPN_serveru)
        *   [5.4.5 Konfigurace Klienta](#Konfigurace_Klienta)
*   [6 Řešení problémů](#Řešení_problémů)
    *   [6.1 Problém se škálováním TCP okénka (Window)](#Problém_se_škálováním_TCP_okénka_(Window))
        *   [6.1.1 Jak diagnostikovat problém?](#Jak_diagnostikovat_problém?)
        *   [6.1.2 Jak to opravit? (špatná cesta)](#Jak_to_opravit?_(špatná_cesta))
        *   [6.1.3 Jak to opravit? (dobrá cesta)](#Jak_to_opravit?_(dobrá_cesta))
        *   [6.1.4 Jak to opravit? (nejlepší cesta)](#Jak_to_opravit?_(nejlepší_cesta))
        *   [6.1.5 Více?](#Více?)
    *   [6.2 Problém s Realteky bez spojení/WOL](#Problém_s_Realteky_bez_spojení/WOL)
        *   [6.2.1 Metoda 1 - Vrácení / změna Win ovladače](#Metoda_1_-_Vrácení_/_změna_Win_ovladače)
        *   [6.2.2 Metoda 2 - Povolení WOL ve Win ovladači](#Metoda_2_-_Povolení_WOL_ve_Win_ovladači)
        *   [6.2.3 Metoda 3 - Novější ovladače Realtek pro Linux](#Metoda_3_-_Novější_ovladače_Realtek_pro_Linux)
    *   [6.3 DLink G604T/DLink G502T: problém DNS](#DLink_G604T/DLink_G502T:_problém_DNS)
        *   [6.3.1 Jak diagnostikovat tento problem?](#Jak_diagnostikovat_tento_problem?)
        *   [6.3.2 Jak jej odstranit?](#Jak_jej_odstranit?)
        *   [6.3.3 Něco více?](#Něco_více?)

## Nastavení hostname

Hostname (název hostitele/počítače) je jedinečné jméno vytvořené pro účel identifikace stroje na síti. V Arch Linuxu se hostname stroje dá nastavit buď v souboru `/etc/rc.conf` nebo dočasně až do restartu pomocí příkazu *hostname*. Hostname je omezen na alfanumerické znaky; je povoleno použít pomlčku (–), ale nesmí jí začínat ani končit. Délka je omezena na 63 znaků.

Otevřete `/etc/rc.conf` a nastavte `HOSTNAME` na vámi požadované jméno počítače (v tomto případě "archlinux"):

```
HOSTNAME="archlinux"

```

Po jeho nastavení je také dobrý nápad vložit stejný název do souboru `/etc/hosts`. Tím pomůžete najít IP počítače procesům, které na váš počítač odkazují právě pomocí jeho hostname.

Otevřete `/etc/hosts` a přidejte na konec řádku pro localhost stejný hostname, jaký jste zadali do souboru `/etc/rc.conf`:

```
127.0.0.1      localhost.localdomain      localhost    archlinux

```

Obdobně můžete přidávat i další záznamy.

Pro dočasné nastavení hostname (do příštího startu systému) použijte jako root příkaz *hostname*:

```
# hostname archlinux

```

## Nahrání ovladače (modulu) zařízeni

Pokud používáte udev, měl by být schopen rozpoznat vaši síťovou kartu a automaticky po startu zavést odpovídající moduly. V opačném případě potřebujete vědět název modulu potřebného pro chod vaší karty. Hledejte na webu výrobce vaší karty, ve vyhledávačích nebo zkuste některou z Live distribucí a podívejte se jaký modul používa – spusťte příkaz lsmod, který zobrazí všechny aktuálně načtené moduly.

Nyní předpokládejme, že znáte název potřebného modulu. Můžete ho do jádra zavést následujícím příkazem:

```
# modprobe jmenomodulu

```

Jestliže nechcete nebo nemůžete použít auto-loader jako například hwdetect, můžete přidat názvy potřebných modulů do /etc/rc.conf, potom už nebude potřeba zavádět moduly příkazem modprobe po každém startu počítače. Např. pokud se modul jemenuje tg3:

```
MODULES=(!usbserial tg3 snd-cmipci)

```

Další běžné moduly jsou 8139too pro karty s čipy od RealTek nebo sis900 pro SiS karty.

## Nastavení IP adresy

**Note:** U základních desek s integrovanými síťovými kartami je důležité vědět, která karta se považuje za primární (např. eth0) a která za sekundární (např. eth1). Mnoho problémů s konfigurací je způsobeno tím, že uživatelé nesprávně konfigurují v /etc/rc.conf rozhraní eth0 a přitom mají do lokální LAN sítě připojené rozhraní eth1.

### DHCP

DCHP je služba, která dokáže dynamicky na požádání přidělovat klientům IP adresu (a nejen ji). Pokud dhcp používáte, upravte [rc.conf](/index.php/Rc.conf "Rc.conf") následovně:

```
 eth0="dhcp"
 INTERFACES=(eth0)
 ROUTES=(!gateway)

```

Pokud z nějakého důvodu dhcpcd eth0 selhává, nainstalujte dhclienta (`pacman -S dhclient`) a použijte příkaz dhclient eth0 (samozřejmě pokud vaše síťová karta je označena jako eth0).

### Statická IP

Jestliže sdílíte internetové připojeni z windowsovského boxu bez routeru, použijte na statickou IP adresu jinak můžete mít problémy se sítí.

Pro konfiguraci statické IP potřebujete znát:

*   svoji statickou IP
*   masku sítě
*   adresu broadcastu (poslední možná IP v rozsahu vaší sítě)
*   bránu (gateway)
*   IP adresy jmenných serverů
*   jméno vaší domény

Pokud pracujete v soukromé síti, je bezpečné používat IP adresy v rozsahu 192.168.*.* , s maskou 255.255.0.0 a adresou všesměrového vysílání (broadcast) 192.168.255.255\. Dokud vaše síť nemá router, na adrese brány nezáleží. Upravte [rc.conf](/index.php/Rc.conf "Rc.conf") následovně, avšak nahraďte IP, masku sítě, broadcast a bránu svými vlastními hodnotami:

```
 eth0="eth0 192.168.10.1 netmask 255.255.0.0 broadcast 192.168.255.255"
 INTERFACES=(eth0)
 gateway="default gw 192.168.10.20"
 ROUTES=(gateway)

```

V souboru `/etc/resolv.conf` potom nahraďte IP nameserveru a jméno domény vašimi vlastními. Jméno domény pro vzhledávání není vždy podmínkou:

```
 nameserver 61.23.173.5
 nameserver 61.95.849.8
 search example.com

```

Můžete zadat tolik nameserverů, kolik chcete.

Pokud používáte DHCP a nechcete, aby se váš DNS server měnil při každém spuštění sítě, přidejte volbu `-R` do `DHCPCD_ARGS` v souboru `/etc/conf.d/dhcpcd` (používaném v /etc/rc.d/network). Tímto se zabrání, aby za každým spuštěním DHCP přepisoval váš `/etc/resolv.conf`:

```
DHCPCD_ARGS="-R -t 30 -h $HOSTNAME"

```

## Aktualizace konfigurace

K otestování konfigurace nemusíte restartovat počítač, stačí jako root spustit `/etc/rc.d/network restart`. Nyní zkuste příkazem ping otestovat spojení na vaši bránu, DNS servery, ISP a jiné internetové servery.

## Některá další nastavení

### Bezdrátové sítě

Konfigurace bezdrátových sítí je probírána v [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Firewall

Abyste se cítili bezpečněji, nainstalujte a nakonfigurujte si [firewall](/index.php/Firewall "Firewall").

### Ifplugd

Ifplugd je služba, která automaticky konfiguruje vaše síťová rozhraní, když zapojíte kabel a poté i konfiguraci vynuluje, pokud kabel zase odpojíte. To je velmi použitelné na laptopech s integrovanou síťovou kartou, protože se bude síť konfigurovat až opravdu v okamžiku, kdy je připojen kabel.

Instalace je velmi jednoduchá. Baliček se nachází v [extra]:

```
# pacman -S ifplugd

```

Ve výchozím stavu je služba nastavena pro spolupráci s eth0\. Toto a jiné nastavení se konfiguruje v `/etc/ifplugd/ifplugd.conf`.

ifplugd spusťte příkazem:

```
# /etc/rc.d/ifplugd start

```

nebo jej přidejte do výčtu DAEMONS v `/etc/rc.conf`.

### OpenVPN

#### Příprava

Instalace

```
# pacman -S openvpn openssl

```

#### Generování certifikátů

Zkopírujeme skripty pro jednoduché vytváření certifikátů:

```
cp -r /usr/share/openvpn/easy-rsa /etc/openvpn/easy-rsa/

```

Generování za pomoci Easy-RSA

```
cd /etc/openvpn/easy-rsa/

```

Doporučuji v souboru vars a vyplnit následující položky:

```
export KEY_COUNTRY="CZ"
export KEY_PROVINCE="NA" (NA znamená Not Applicable)
export KEY_CITY="Mesto"
export KEY_ORG="firma"
export KEY_EMAIL="me@myhost.cz"

```

Vygenerujeme certifikáty potřebné pro server:

```
source ./vars
./build-ca
./build-key-server MYSERVER
./build-dh

```

Vygenerujeme certifikáty pro uživatele:

```
./build-key FRANTA
./build-key PEPA

```

Veškeré vygenerované soubory jsou uložené v:

```
/etc/openvpn/easy-rsa/keys

```

Výsledek by měl zhruba vypadat takto:

```
ls -l /etc/openvpn/easy-rsa/keys/
total 84
-rw-r--r-- 1 root root 4079 May 21 09:53 01.pem
-rw-r--r-- 1 root root 3943 May 21 09:54 02.pem
-rw-r--r-- 1 root root 3958 May 21 09:54 03.pem
-rw-r--r-- 1 root root 1354 May 21 09:51 ca.crt
-rw------- 1 root root  916 May 21 09:51 ca.key
-rw-r--r-- 1 root root  245 May 21 09:54 dh1024.pem
-rw-r--r-- 1 root root 3958 May 21 09:54 FRANTA.crt
-rw-r--r-- 1 root root  716 May 21 09:54 FRANTA.csr
-rw------- 1 root root  916 May 21 09:54 FRANTA.key
-rw-r--r-- 1 root root 4079 May 21 09:53 MYSERVER.crt
-rw-r--r-- 1 root root  716 May 21 09:52 MYSERVER.csr
-rw------- 1 root root  916 May 21 09:52 MYSERVER.key
-rw-r--r-- 1 root root  395 May 21 09:54 index.txt
-rw-r--r-- 1 root root   21 May 21 09:54 index.txt.attr
-rw-r--r-- 1 root root   21 May 21 09:54 index.txt.attr.old
-rw-r--r-- 1 root root  261 May 21 09:54 index.txt.old
-rw-r--r-- 1 root root 3943 May 21 09:54 PEPA.crt
-rw-r--r-- 1 root root  708 May 21 09:54 PEPA.csr
-rw------- 1 root root  912 May 21 09:54 PEPA.key
-rw-r--r-- 1 root root    3 May 21 09:54 serial
-rw-r--r-- 1 root root    3 May 21 09:54 serial.old

```

Špatně jste něco vyplnili a chcete to celé udělat znovu? Pozor, následující příkaz vymaže všechny certifikáty vytvořené předcházejícími příkazy.

```
source ./vars
./clean-all

```

**Zdroje:**

1.  [http://www.openvpn.net/index.php/open-source/documentation/howto.html](http://www.openvpn.net/index.php/open-source/documentation/howto.html)
2.  [OpenVPN](/index.php/OpenVPN "OpenVPN")
3.  [http://openvpn.net/index.php/open-source/documentation/miscellaneous/77-rsa-key-management.html](http://openvpn.net/index.php/open-source/documentation/miscellaneous/77-rsa-key-management.html)

#### Konfigurace serveru

Vytvořte novou konfiguraci:

```
nano /etc/openvpn/vpn.conf 

```

```
port 1194
proto tcp
dev tun

ca /etc/openvpn/easy-rsa/keys/ca.crt
cert /etc/openvpn/easy-rsa/keys/MYSERVER.crt
key /etc/openvpn/easy-rsa/keys/MYSERVER.key
dh /etc/openvpn/easy-rsa/keys/dh1024.pem

server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
keepalive 10 120
comp-lzo
user nobody
group nobody
persist-key
persist-tun
status openvpn-status.log
verb 3

log-append /var/log/openvpn
status /tmp/vpn.status 10

```

#### Spusteni OpenVPN serveru

```
/etc/rc.d/openvpn start

```

Ať už všechno jde, jak má, nebo ne, překontrolujte log.

```
cat /var/log/openvpn

```

```
Fri May 21 09:58:59 2010 OpenVPN 2.1.1 x86_64-unknown-linux-gnu [SSL] [LZO2] [EPOLL] built on Apr  1 2010
Fri May 21 09:58:59 2010 NOTE: OpenVPN 2.1 requires '--script-security 2' or higher to call user-defined scripts or executables
Fri May 21 09:58:59 2010 Diffie-Hellman initialized with 1024 bit key
Fri May 21 09:58:59 2010 TLS-Auth MTU parms [ L:1544 D:140 EF:40 EB:0 ET:0 EL:0 ]
Fri May 21 09:58:59 2010 ROUTE default_gateway=10.0.0.1
Fri May 21 09:58:59 2010 TUN/TAP device tun0 opened
Fri May 21 09:58:59 2010 TUN/TAP TX queue length set to 100
Fri May 21 09:58:59 2010 /sbin/ifconfig tun0 10.8.0.1 pointopoint 10.8.0.2 mtu 1500
Fri May 21 09:58:59 2010 /sbin/route add -net 10.8.0.0 netmask 255.255.255.0 gw 10.8.0.2
Fri May 21 09:58:59 2010 Data Channel MTU parms [ L:1544 D:1450 EF:44 EB:135 ET:0 EL:0 AF:3/1 ]
Fri May 21 09:58:59 2010 GID set to nobody
Fri May 21 09:58:59 2010 UID set to nobody
Fri May 21 09:58:59 2010 Listening for incoming TCP connection on [undef]:1194
Fri May 21 09:58:59 2010 Socket Buffers: R=[87380->131072] S=[16384->131072]
Fri May 21 09:58:59 2010 TCPv4_SERVER link local (bound): [undef]:1194
Fri May 21 09:58:59 2010 TCPv4_SERVER link remote: [undef]
Fri May 21 09:58:59 2010 MULTI: multi_init called, r=256 v=256
Fri May 21 09:58:59 2010 IFCONFIG POOL: base=10.8.0.4 size=62
Fri May 21 09:58:59 2010 IFCONFIG POOL LIST
Fri May 21 09:58:59 2010 MULTI: TCP INIT maxclients=1024 maxevents=1028
Fri May 21 09:58:59 2010 Initialization Sequence Completed

```

#### Konfigurace Klienta

Bezpečnou cestou přeneseme certifikáty ze serveru na klienta, v tomto případě Windows 7.

```
/etc/openvpn/easy-rsa/keys/ca.crt
/etc/openvpn/easy-rsa/keys/FRANTA.crt
/etc/openvpn/easy-rsa/keys/FRANTA.key

```

Nahrajeme je do adresáře:

```
C:\Program Files (x86)\OpenVPN\config\

```

pro 32bitový systém:

```
C:\Program Files\OpenVPN\config\

```

Vytvoříme textový soubor s příponou .ovpn. Do něj vložíme vzorovou konfiguraci pro uživatele FRANTA a uložíme jej do stejného umístění jako certifikáty.

```
client
remote 10.0.0.102 1194
dev tun
proto tcp
resolv-retry infinite
nobind
persist-key
persist-tun
verb 2
ca ca.crt
cert FRANTA.crt
key FRANTA.key
comp-lzo

```

Doporučuji zadat u volby **verb** vyšší číslo kvůli podrobnějším logům. Až bude vše fungovat, přepište ji na 3.

Takovýto soubor OpenVPN automaticky načte. Pokud chcete mít na ploše ikonu OpenVPN, která se po spuštění sama připojí na server, upravte zástupce následovně:

```
"C:\Program Files (x86)\OpenVPN\bin\openvpn-gui-1.0.3.exe" --connect franta.ovpn

```

## Řešení problémů

### Problém se škálováním TCP okénka (Window)

TCP segmentu obsahují hodnoty "okének" ve hlavičkách indikujících kolik dat je schopný přijímací uzel akceptovat od vysílajícího. Okénka se definují v segmentech ACK, kdy přijímací uzel potvrzuje přijetí segmentů. Velikost okénka reprezentuje 16bitů a z tohoto důvodu je maximálně 64Kb. TCP segmenty jsou ukládány v cache (kde se zarovnávají).Cache je omezená a přijímací uzel by jí lehce mohl vyčerpat, pokud by neměl mechanizmus jak korigovat tok dat.

V roce 1992 rostlo množství dostupné paměti v počítačích. Bylo nepsán [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html) , aby zlepšil situaci škálování okénka. Hodnota okénka implementovaná do všech segmentů bude modifikována tzv. škálovacím faktorem (Scale Factor) definovaným jednou na počátku komunikace.

8-bitový Škálovací faktor umožňuje okénku být 32-krát vyšší než původních 64Kb.

Občas nastává problém v tom, že některé chybné routery a firewally na internetu přepisují škálovací faktor na 0, čímž způsobují nedorozumění mezi hosty.

Linuxové jádro 2.6.17 představilo nové kalkulační schéma generující vyšší škálovací faktor. Uměle zviditelňuje následky chyb routerů a firewallů.

Výsledné spojení je při nejlepším velmi pomalé, nebo nelze navázat.

#### Jak diagnostikovat problém?

Tento problém nastává zřídka kdy. V některých případech nebudete schopní použít TCP spojení (HTTP,FTP,...) vůbec a v jiných budete schopni pouze s některými hosty.

**Varování**: výstup z `dmesg` musí být v pořádku, logy čisté, `ifconfig` ukazuje normální stav — vše se jeví v pořádku.

Pokud nemůžete prohlížet zádnou webovou stránku, ale můžete pingnout některé hosty, šance jsou velké. Ping používá ICMP protokol a není ovlivněn TCP protokolem.

K detekci problému můžete vyzkoušet program WireShark. Je to výborný nástroj pro zkoumání síťové komunikace. Například můžete objevit úspěšné UDP a ICMP komunikace, ale neúspěšné TCP komunikace.

#### Jak to opravit? (špatná cesta)

Můžete změnit hodnotu *tcp_rmem*, na které je založen škálovací faktor. Přestože by to mohlo pomoci většine hostů, není zaručeno, že to bude funkční i na ty velmi vzdálené.

```
echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

#### Jak to opravit? (dobrá cesta)

Jednoduše vypněte škálování okének. Přestože je škálování příjemná vlastnost TCP, může být dosti nepohodlná. Zvláště pokud nemůžete upravit chybný router. Je několik cest jak vypnout škálování a vypadá to, že pracují na většině kernelů. Přidejte dásledující řádek do `/etc/rc.local`:

```
echo 0 > /proc/sys/net/ipv4/tcp_window_scaling

```

#### Jak to opravit? (nejlepší cesta)

Tento problém je způsoben chybným routerem/firewallem, tak jej vyměňte. Někteří uživatelé totiž nalezli problém na jejich vlastních DSL routerech.

#### Více?

Tato sekce je založena na LWN článku [TCP window scaling and broken routers](http://lwn.net/Articles/92727/) a Kernel Trap článku: [Window Scaling on the Internet](http://kerneltrap.org/node/6723).

A v poslední době se některým uživatelům Archu hodilo:

*   [Odd network issue](https://www.archlinux.org/pipermail/arch/2006-June/011250.html)
*   [Kernel 2.6.17 and TCP window scaling](https://www.archlinux.org/pipermail/arch/2006-September/011943.html) — téma, které inicializovalo teto článek

Několik dobrých vláken naleznete také na LKML.

### Problém s Realteky bez spojení/WOL

Uživatelé se síťovými kartami založenými na čipech Realtek 8168 8169 8101 8111 mohou zaznamenat problém, při kterém se karta po startu tváří jako vypnutá a nesvítí vůbec kontrolka Link. Toto se obvykle stává na systémech s duálním bootem, kde jsou nainstalovány Windows. Zdá se, že je příčinou používání oficiálních ovladačů Realteku (novějších než květen 2007). Tyto novější ovladače vypínají Wake-On-Lan tím, že během vypínání Windows vypnou síťovou kartu, přičemž zůstává vypnutá až do příštího spuštění Windows. To, zda se tento problém týká i vás, zjistíte podle kontrolky Link, která zůstává zhasnutá do té doby, než spustíte Windows, a po jejich vypnutí opět setrváva zhaslá. Za normálního stavu by měla tato kontrolka svítit po celou dobu, kdy je počítač zapnutý, a to i během POST. Tento problém postihuje též další operační systémy bez novějších ovladačů (např. Live CD). Zde následuje několik řešení tohoto problému.

#### Metoda 1 - Vrácení / změna Win ovladače

Odinstalujte váš ovladač síťové karty pro Windows a vraťte se k ovladači, který poskytl Microsoft (je-li k dispozici), nebo nainstalujte původní oficiální ovladač Realtek vydaný před květnem 2007 (snad by měl být na CD, které bylo přiloženo k vašemu hardware).

#### Metoda 2 - Povolení WOL ve Win ovladači

Pravděpodobně nejlepší a nejrychlejší oprava je změnit nastavení v ovladači ve Windows. Touto cestou by měl být síťový systém fixován nejenom pro Arch ale i např. pro live CD nebo jiné OS. Ve Správci zařízení pod Windows najděte váš Realtek Network adapter a dvakrát na něj klikněte. V kartě Rozšířené povolte možnost "wake-on-lan po vypnutí".

```
 In Windows XP (příklad)
 Pravým tlačítkem myši na ikonu Tento počítač
 --> Hardware tab
   --> Device Manager
     --> Network Adapters
       --> "double click" Realtek ...
         --> Advanced tab
           --> Wake-On-Lan After Shutdown
             --> Enable.

```

#### Metoda 3 - Novější ovladače Realtek pro Linux

Všechny novější linuxové ovladače pro tyto karty Realtek je možno stáhnout z webové stránky Realtek (netestováno ale snad by také měly vyřešit problém).

### DLink G604T/DLink G502T: problém DNS

Uživatelé routerů DLink G604T/DLink G502T, kteří používají DHCP a mají firmware v2.00+ (typicky uživatelé AUS firmware) mohou mít problémy, že některé programy nerozpoznají DNS. Jeden z těchto programů je naneštěstí pacman. V zásadě je problém v tom, že router v jistých situacích neposílá DNS přesně na DHCP, což způsobuje, že programy se pokoušejí se spojit se servery s IP adresou 1.0.0.0 a spojení se díky překročení časového limitu nepodaří.

#### Jak diagnostikovat tento problem?

Nejlepší metodou, jak zjistit tento problém je použití firefox/konqueror/links/seamonkey a povolení wget pro pacman. Jedná -li se o novou instalaci Arch Linuxu, pak byste měli chtít vzít v úvahu instalační linky z live CD.

Nejprve povolte wget pro pacman (protože wget nás informuje když pacman stahuje balíčky). Otevřete /etc/pacman.conf ve vašem oblíbeném editoru a odkomentujte následující řádek (odstraňte # ,jestli se tam nachází)

```
XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u

```

Zatímco jste v pacman.conf, zkontrolujte implicitní zrcadlo, které pacman používá pro download balíčků.

Otevřte stránku se zrcadlem v internetovém prohlížeči a podívejte se, zda zrcadlo opravdu funguje. Je-li tomu tak, potom zadejte příkaz pacman -Syy (pokud je zrcadlo mimo provoz, vezměte jiné a nastavte ho v pacmanu jako implicitní), a podívejte se, zdali se neobjeví něco podobného, co je popsáno níže (všimněte si IP 1.0.0.0)

```
ftp://mirror.pacific.net.au/linux/archlinux/extra/os/i686/extra.db.tar.gz                                                            
           => `/var/lib/pacman/community.db.tar.gz.part'                            
Resolving mirror.pacific.net.au... 1.0.0.0

```

Potom máte s největší pravděpodobností tento problém. IP 1.0.0.0 znamená, že pacman nemůže rozpoznat DNS, takže jej musíte přidat do souboru resolv.conf.

#### Jak jej odstranit?

V podstatě, jde o to, abyste přidali manuálně DNS do souboru `/etc/resolv.conf` . DHCP však stále ještě automaticky maže a mění tento soubor po startu systému, je tedy nutno ještě editovat `/etc/conf.d/dhcpcd` a změnit jej, aby se toto přes DHCP nedělo.

Po otvření souboru `/etc/conf.d/dhcpcd`, byste měli vidět něco podobného následujícímu řádku:

```
DHCPCD_ARGS="-t 30 -h $HOSTNAME"

```

přidejte flag `-R` do argumentů, tedy:

```
DHCPCD_ARGS="-R -t 30 -h $HOSTNAME"

```

**POZN.**: Používáte-li dhcpcd >= 4.0.2, flag -R byl potlačen, prosím přečtěte si informace na těchto stránkách: ([Configuring network#For_DHCP_IP](/index.php/Configuring_network#For_DHCP_IP "Configuring network")) sekce How to use a custom resolv.conf file

Uložte soubor a zavřete jej, potom znovu otevřete /etc/resolv.conf. Měli byste vidět jednu IP (nejpravděpodobněji 10.1.1.1), což je brána vašeho routeru, kterou potřebujete připojit, abyste dostali DNS vašeho ISP. Vložte IP do vašeho internetového prohlížeče a přihlaste se do routeru. V sekci DNS byste měli vidět IP preferovaného DNS serveru, zkopírujte ji a vložte do souboru NAD IP adresu brány.

T.zn., že resolv.conf by měl vypadat před změnou takto:

```
namespace 10.1.1.1

```

A pokud např. máte primární DNS Server 211.29.132.12 tak upravte resolv.conf následovně:

```
namespace 211.29.132.12
namespace 10.1.1.1

```

Teď restartujte síť následujícím příkazem: `/etc/rc.d/network restart` a proveďte `pacman -Syy`, jestliže se synchronizace se serverem zdařila.

#### Něco více?

Fórum whirlpool (australská komunita ISP), ve kterém se o tomto problému hovoří a poskytuje totéž řešení:

```
[http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html](http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html)

```