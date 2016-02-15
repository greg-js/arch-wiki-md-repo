[NetworkManager](http://projects.gnome.org/NetworkManager/) je program pro poskytování detekce a konfigurace pro systém automatického připojování k síti. Funkcionalita NetworkManageru může být použitelná jak pro bezdrátové tak i pro drátové sítě. Pro bezdrátové sítě, NetworkManager upřednostňuje známé bezdrátové sítě a má schopnost vhodně přepínat do nejspolehlivějších sítí. NetworkManager-vnímající aplikace mohou přepínat mezi online a offline módem. NetworkManager také upřednostňuje kabelové spoje před bezdrátovými, obsahuje podporu modemových připojení a určitých druhů VPN. NetworkManager byl původně vyvinut společností RedHat a nyní je hostován projektem [GNOME](/index.php/GNOME "GNOME").

## Contents

*   [1 Základní instalace](#Z.C3.A1kladn.C3.AD_instalace)
*   [2 Grafická nástavba](#Grafick.C3.A1_n.C3.A1stavba)
    *   [2.1 GNOME](#GNOME)
    *   [2.2 KDE4](#KDE4)
    *   [2.3 Openbox](#Openbox)
    *   [2.4 Ostatní desktopy a Okenní manažery](#Ostatn.C3.AD_desktopy_a_Okenn.C3.AD_mana.C5.BEery)
    *   [2.5 Příkazový řádek](#P.C5.99.C3.ADkazov.C3.BD_.C5.99.C3.A1dek)
*   [3 Nastavení](#Nastaven.C3.AD)
    *   [3.1 Vypnutí současného síťového nastavení](#Vypnut.C3.AD_sou.C4.8Dasn.C3.A9ho_s.C3.AD.C5.A5ov.C3.A9ho_nastaven.C3.AD)
    *   [3.2 Úprava démonů](#.C3.9Aprava_d.C3.A9mon.C5.AF)
    *   [3.3 Síťové služby s NetworkManager Dispatcher](#S.C3.AD.C5.A5ov.C3.A9_slu.C5.BEby_s_NetworkManager_Dispatcher)
        *   [3.3.1 Použití dispatcheru k připojení vpn přes již navázané síťové připojení](#Pou.C5.BEit.C3.AD_dispatcheru_k_p.C5.99ipojen.C3.AD_vpn_p.C5.99es_ji.C5.BE_nav.C3.A1zan.C3.A9_s.C3.AD.C5.A5ov.C3.A9_p.C5.99ipojen.C3.AD)
    *   [3.4 Nastavení proxy](#Nastaven.C3.AD_proxy)
*   [4 Testování](#Testov.C3.A1n.C3.AD)
*   [5 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
    *   [5.1 Network Management Disabled](#Network_Management_Disabled)
    *   [5.2 NetworkManager zabraňuje DHCPCD aby používal resolv.conf.head and resolv.conf.tail](#NetworkManager_zabra.C5.88uje_DHCPCD_aby_pou.C5.BE.C3.ADval_resolv.conf.head_and_resolv.conf.tail)
    *   [5.3 Zamezení změnám v resolv.conf](#Zamezen.C3.AD_zm.C4.9Bn.C3.A1m_v_resolv.conf)
    *   [5.4 Problémy s DHCP](#Probl.C3.A9my_s_DHCP)
    *   [5.5 Jak se vyhnout Gnome keyring při normálním uživatelském připojení bezdrátové sítě](#Jak_se_vyhnout_Gnome_keyring_p.C5.99i_norm.C3.A1ln.C3.ADm_u.C5.BEivatelsk.C3.A9m_p.C5.99ipojen.C3.AD_bezdr.C3.A1tov.C3.A9_s.C3.ADt.C4.9B)
    *   [5.6 Chybějící default route](#Chyb.C4.9Bj.C3.ADc.C3.AD_default_route)
    *   [5.7 3G modem není detekován](#3G_modem_nen.C3.AD_detekov.C3.A1n)
    *   [5.8 VPN problémy v Networkmanageru 0.7.999](#VPN_probl.C3.A9my_v_Networkmanageru_0.7.999)
    *   [5.9 Vypínání WLAN na laptopech](#Vyp.C3.ADn.C3.A1n.C3.AD_WLAN_na_laptopech)
    *   [5.10 Nastavení statické IP se vrací k DHCP](#Nastaven.C3.AD_statick.C3.A9_IP_se_vrac.C3.AD_k_DHCP)
*   [6 Tipy and triky](#Tipy_and_triky)
    *   [6.1 Kontrola jestli je networking spouštěn cronem nebo skriptem](#Kontrola_jestli_je_networking_spou.C5.A1t.C4.9Bn_cronem_nebo_skriptem)
    *   [6.2 Automatické odemknutí keyring po přihlášení](#Automatick.C3.A9_odemknut.C3.AD_keyring_po_p.C5.99ihl.C3.A1.C5.A1en.C3.AD)
        *   [6.2.1 Gnome](#Gnome_2)
        *   [6.2.2 KDE](#KDE)
    *   [6.3 Automatické připojení při bootu](#Automatick.C3.A9_p.C5.99ipojen.C3.AD_p.C5.99i_bootu)
    *   [6.4 Ignorování určitých zařízení](#Ignorov.C3.A1n.C3.AD_ur.C4.8Dit.C3.BDch_za.C5.99.C3.ADzen.C3.AD)

## Základní instalace

NetworkManager je dostupný z oficiálních repozitářů:

```
# pacman -S networkmanager

```

## Grafická nástavba

Ke konfiguraci a snadnému přístupu k NetworkManageru bude mnoho lidí chtít nainstalovat miniaplikaci. Tato GUI nástavba se obvykle usadí v system tray (nebo oznamovací oblasti) a dovolí výběr sítě a nastavení NetworkManageru. Různé miniaplikace existují pro rozdílné druhy desktopů.

### GNOME

GNOME aplety (dříve gnome-network-manager) je dostatečně odlehčené a pracuje přes všechna prostředí:

```
# pacman -S network-manager-applet

```

Jestliže chcete uchovávat autentizační detaily (Wireless/DSL) a zapnout globální nastavení připojení, např "dostupnost pro všechny uživatele":

```
# pacman -S gnome-keyring

```

### KDE4

KNetworkManager nadstavba je dostupná v KDE verzy 4.4 jako plasma widget:

```
# pacman -S kdeplasma-applets-networkmanagement

```

GNOME protějšek pracuje stejně pěkně nebo dokonce lépe (má více prvků a detekuje víc hardwaru).

**Note:** Jestliže přecházíte z jiného nástroje pro správu sítí jako např. Wicd nezapomeňte nastavit základní 'Network Management Backend' v System Settings -> Hardware -> Information Sources

### Openbox

GNOME aplet pracuje dobře s xfce4-notifyd notification daemon:

```
# pacman -S network-manager-applet xfce4-notifyd hicolor-icon-theme gnome-icon-theme

```

Jestliže chcete uchovávat autentizační detaily (Wireless/DSL):

```
# pacman -S gnome-keyring

```

Aby Openboxový autostart.sh nastartoval nm-applet dobře, bude možná potřeba smazat soubor /etc/xdg/autostart/nm-applet.desktop (Je možné, že bude potřeba mazat tento soubor po každé změně v network-manager-apletu)

Potom v autostart.sh, nastartuje nm-applet tímto řádkem:

```
(sleep 3 && /usr/bin/nm-applet --sm-disable) &

```

### Ostatní desktopy a Okenní manažery

Je doporučeno používat GNOME aplety. Také je potřeba zajistit, že GNOME hicolor theme je nainstalováno, kvůli zobrazení tohoto apletu:

```
# pacman -S hicolor-icon-theme gnome-icon-theme

```

### Příkazový řádek

Balíček Networkmanager od verze 0.8.1 obsahuje [nmcli](http://manpages.ubuntu.com/manpages/maverick/man1/nmcli.1.html)

## Nastavení

NetworkManager vyžaduje pár dodatečných kroků, aby mohl pracovat korektně.

Ověřte zda je váš `/etc/hosts` je správný, před tím než budete pokračovat. Jestliže jste se předčasně pokoušeli připojit před následujícím krokem, NetworkManager to může oznámit. Příklad hostname řádku v `/etc/hosts`:

```
#<ip-address> <hostname.domain.org>           <hostname>                        
127.0.0.1     localhost.localdomain localhost dell-latitude

```

### Vypnutí současného síťového nastavení

Abyste správně otestovali NetworkManagera, změnte své současné síťové nastavení. Nejdříve (Při použítí Arch Linux síťových skriptů) zastavte sítě:

```
/etc/rc.d/network stop

```

Ukončete vaše NIC's (Network Interface Controllers, tj. síťové karty). Například:

```
ifconfig eth0  down
ifconfig wlan0 down

```

Upravte `/etc/rc.conf` a kde je definováno DHCP nebo statická IP adresa, okomentujte:

```
#eth0="dhcp"                                                                    
#wlan0="dhcp"                                                                   
INTERFACES=(!eth0 !wlan0)

```

### Úprava démonů

Musíte _odstranit_ základního **network** démona a přidat **networkmanager** démona, za dbus démona:

```
DAEMONS=( ...**dbus networkmanager**... )

```

Ujistěte se, že balíček [dbus](https://www.archlinux.org/packages/?name=dbus) je nainstalován tak jak to NetworkManager vyžaduje. Ke nastartování ostatních služeb (démonů) které vyžaduje síťové připojení si ukážeme v následující sekcí na jejich nastavení. Ačkoliv je zde NetworkManager démon nastartován, nepřipojí se (v základu) do sítě dokud není aplet nahrany a specifikace apletu potřebné k připojení. To znamená, že síťové služby je potřeba specifikovat NetworkManageru až když běží.

### Síťové služby s NetworkManager Dispatcher

Je zde pár síťových služeb, které nebudou chtít běžet na rozhraní spuštěném NetworkManagerem. Dobrým příkladem jsou **openntpd** a síťová souborová připojení různých typů (například **netfs**). NetworkManager má schopnost spustit tyto služby když se připojujete k síti (interface up), a zastavit je když už nejsou potřeba (interface down).

Pro použítí těchto pruvku může být přidán skript do adresáře `/etc/NetworkManager/dispatcher.d`. Tyto skripty potřebují mít uživatelské právo ke spuštění. Kvůli bezpečnosti je dobrým zvykem udělat jejich vlastníkem uživatele **root:root** a příznak zápisu jen pro vlastníka.

**Warning:** Z bezpečnostních důvodů byste měli vypnout právo zápisu pro skupiny a ostatní. Například použít masku 755. Jinak Dispatcher může odmítnout vykonat skrip s chybovou zprávou "nm-dispatcher.action: Script could not be executed: writable by group or other, or set-UID." in /var/log/messages.log

Skripty budou spouštěny v abecedním pořadí v čase připojení (s argumenty _interface up_), a v obráceném abecedním pořadí v čase odpojení (_interface down_). Pro zajištění správného pořadí, je běžné použití číslic před jménem skriptu (například `10_portmap` nebo `30_netfs` (který zajišťuje že portmapper je spuštěn před pokusem o přimountování NFS).

Následují skript nastartuje démona openntpd když je rozhraní spouštěno. Uložte soubor jako `/etc/NetworkManager/dispatcher.d/20_openntpd` a udělte mu práva ke spuštění.

```
#!/bin/sh

INTERFACE=$1 # The interface which is brought up or down
STATUS=$2 # The new state of the interface

case "$STATUS" in
    'up') # $INTERFACE is up
	exec /etc/rc.d/openntpd start
	;;
    'down') # $INTERFACE is down
	# Check for active interface and down if no one active
	if [ ! `nm-tool|grep State|cut -f2 -d' '` == "connected" ]; then
		exec /etc/rc.d/openntpd stop
	fi
	;;
esac

```

**Warning:** Jestliže se připojujete k cizím nebo veřejným sítím, uvědomte si které služby spouštíte a které servery očekáváte, že budou dostupné pro ty kteří se chtějí připojit. Mohl byste vytvořit bezpečnostní riziko spuštěním špatné služby během připojení k veřejné síti.

#### Použití dispatcheru k připojení vpn přes již navázané síťové připojení

V tomto případě se chceme automaticky připojit k vpn definovaném pomocí NetworManager-skriptu - viz. předešlý příklad. Nejdříve vytvoříme dispather skript, který definuje co se bude dělat po připojení síti.

1\. Vytvořte dispatcher sckipt v `/etc/NetworkManager/dispatcher.d/vpn-up`

```
case "$2" in
       up)
               sudo -u username DISPLAY=:0 /usr/bin/python /etc/NetworkManager/vpn-up.py
               ;;
esac

```

Nezapomeňte změnit příznak spustitelný pomocí chmod +x a správný **username**.

2\. Vytvořte `/etc/NetworkManager/vpn-up.py` a změňte **network-ESSID** na vámi požadované. Kók najdete [zde](http://dpaste.com/hold/203441/).

Nyní by se měl NetworkManager pokusit připojik k vaší vpn, která je definována ve vašem profilu.

### Nastavení proxy

Network Manager nezvládá přímé nastavení proxy, ale jestliže používáte GNOME, mohli by jste použít [proxydriver](http://marin.jb.free.fr/proxydriver/), který zvládá proxy nastavení s použitím informací z Network Manageru. Balíček [proxydriver](https://aur.archlinux.org/packages/proxydriver/) je dostupný v [AUR](/index.php/AUR "AUR").

Aby byl proxydriver schopen měnit nastavení proxy, měl by jste vykonoat tento příkaz jako součást GNOME startovacího procesu ( System->Preferences->Startup Applications):

```
xhost +si:localuser:your_username

```

Podívejte se: [Proxy settings](/index.php/Proxy_settings "Proxy settings")

## Testování

NetworkManager applety jsou konstruovány tak aby byli nahrány před přihlášením, proto by žádná další konfigurace, pro většínu uživatelů, neměla být nutná. Jestliže jste si již vypnuli předchozí síťové nastavení a odpojili jste se od vaší sítě, nyní můžete otestovat, zda-li váš NetworkManager fungujue. Nejdříve spustíme démona:

```
/etc/rc.d/networkmanager start

```

Některé aplety vám jsou poskytovány jako .desktop soubory, takže aplet NetworkManageru může být nahrán skrz aplikační menu. A když ne, buď budete muset objevit příkaz k použití nebo se odhlásit a znovu příhlásit ke spuštění apletu. Jakmile je aplet nastartován, pravděpodobně vám dovolí volit síťová připojení s podporou automatického nastavení pomocí DHCP serveru.

Ke spuštění GNOME apletu v non-xdg-compliant Window Manageru jako Awesome:

```
nm-applet --sm-disable &

```

Pro statické IP budete muset nakonfigurovat NetworkManager tak aby je znal. Proces obvykle zahrnuje kliknutí pravým tlačítkem myši na aplet a výběr něčeho jako je 'Správa spojení' nebo 'Edit Connections'.

## Řešení problémů

Řešení některých běžných problémů.

### Network Management Disabled

Někdy při vypnutí NM, není pid (statusový) soubor vymazán a obdržíte zprávu 'Network management disabled'. Jakmile se toto stane budete muset tento soubor vymazat manuálně:

```
rm /var/lib/NetworkManager/NetworkManager.state

```

Jestliže se toto stane po restartu, můžete přidat tuto akci do vašeho `etc/rc.local` pro vymazání při startu systému:

```
nmpid=/var/lib/NetworkManager/NetworkManager.state
[ -f $nmpid ] && rm $nmpid
```

### NetworkManager zabraňuje DHCPCD aby používal resolv.conf.head and resolv.conf.tail

Občas je problematické přidat statické položky do resolv.con když je neustále přepisován nm a dhcpcd. Můžete použít balíček networkmanager-dhclient z AUR, ale lepším řešením je použití následujícího skriptu:

```
#!/bin/bash
# 
# /etc/NetworkManager/dispatcher.d/99-resolv.conf-head_and_tail
# Include /etc/resolv.conf.head and /etc/resolv.conf.tail to /etc/resolv.conf
#
# scripts in the /etc/NetworkManager/dispatcher.d/ directory
# are called alphabetically and are passed two parameters:
# $1 is the interface name, and $2 is “up” or “down” as the
# case may be.

resolvconf='/etc/resolv.conf';
cat "$resolvconf"{.head,,.tail} 2>/dev/null > "$resolvconf".tmp
mv -f "$resolvconf".tmp "$resolvconf"

```

### Zamezení změnám v resolv.conf

NetworkManager se pokusí zapsat DNS informace z DHCP do `/etc/resolv.conf`, přepsáním již existujícího obsahu. K zamezení můžete použít immutable(neměnný) bit na souboru (jako root):

```
# chattr +i /etc/resolv.conf

```

Pro budoucí upravy tohoto souboru, nejdříve odstraňte immutable (neměnný) bit:

```
# chattr -i /etc/resolv.conf

```

### Problémy s DHCP

Jestliže máte problémy s obdržením IP adrasy skrz DHCP, zkuste přidat následující řádky do vašeho `/etc/dhclient.conf`:

```
 interface "eth0" {
   send dhcp-client-identifier 01:aa:bb:cc:dd:ee:ff;
 }

```

Kde `aa:bb:cc:dd:ee:ff` je MAC-adresa tohoto NIC.

### Jak se vyhnout Gnome keyring při normálním uživatelském připojení bezdrátové sítě

Je to velice jednoduché! Nejdříve vytvořte skupinu zvanou **networkmanager** následujícím příkazem (nebo jiným způsobem, jenž upřednostňujete):

```
# groupadd networkmanager

```

Po té předejte uživatele do této skupiny použítím nasledujícího příkazu (nebo jiným způsobem, jenž upřednostňujete):

```
# gpasswd -a username networkmanager

```

Nahraďte, v předchozím príkazu, username vaším aktuálním uživatelským jménem.

Nyní jako root spusťte nm-connection-editor a nastavte připojení:

```
# nm-connection-editor

```

Označte zatržítko vedle "Available to all users" a použijte nastavení.

Od teď nebudete vyrušováni Gnome keyringem! _(citation needed)_ Také, případně zapnete-li "connect automatically", vaše připojení bude dostupné a připojené dokonce předtím než se nalogujete k vašemu desktopu a dělá tím celý startovací proces ještě rychlejší!

### Chybějící default route

Přinejmenším v KDE4 systému, není vytvořena default route při navázání bezdrátového spojení pomocí NetvworkManageru. Pro změnu route nastavení bezdrátového připojení odstraňte základní výběr "Use only for resources on this noccection",které řeší tuto zálažitost.

### 3G modem není detekován

Jestliže NetworkManager (od verze 0.7.999) nedetekuje váš 3G modem, ale i nadále jste schopní se připojit přes [wvdial](/index.php/Wvdial "Wvdial"), zkuste nainstalovat balíček [modemmanager](https://www.archlinux.org/packages/extra/i686/modemmanager/) příkazem `pacman -S modemmanager` a restartujte NetworkManager démona `/etc/rc.d/networkmanager restart`. Odpojte a znovu připojte váš modem nebo restartujte. Tato utilita poskytuje podporu pro hardware, který není v základní databázi networkmanageru.

### VPN problémy v Networkmanageru 0.7.999

Jestliže obdržíte chybovou zprávu "invalid secrets" když se pokoušíte připojit k vašemu VPN poskytovateli prostřednictvím PPTP protokolu, zkuste místotoho nainstalovat (git version): [networkmanager](https://www.archlinux.org/packages/?name=networkmanager), [nm-applet](https://aur.archlinux.org/packages.php?ID=26516) a [pptp plugin](https://aur.archlinux.org/packages.php?ID=29178).

### Vypínání WLAN na laptopech

Občas networkmanager nebude pracovat když vypnete váš Wifi adaptér vaším vypínačem na vašem laptopu a později se pokusíte o znovuzapnutí. Toto je častý problém s rfkill. Nainstalujte rfkill z repa: Sometimes networkmanager won't work when you disable your Wifi-adapter with a switch on your laptop and try to enable it again afterwards. This is often a problem with rfkill. Install rfkill from the repo:

```
# pacman -S rfkill

```

a použíjte

```
$ watch -n1 rfkill list all

```

ke kontrole, že váš ovladač oznámil stav bezdrátového adaptéru. Jestliže jeden identifikátor zůstane blokován poté co jste zapnulí adaptér, zkuste to manuálně odemnknout tímto příkazem (kde X je číslo identifikátoru poskytnuté předchzím výstupem):

```
# rfkill event unblock X

```

### Nastavení statické IP se vrací k DHCP

Kvůli nevyřešenému bugu, když měníme základní připojení na statické IP, nm-applet nemusí přesně uložit konfigurační změny a vrátí se automaticky k DHCP. Ke zprovoznění postupujte podle následujících pokynů.

Editujte defaultní nastavení připojení (eg "Auto eth0) v nm-appletu. Změňte jméno připojení (eg "my eth0"), odškrtněte v zaškrtávacím políčku "Available to all users", dále změňte vaši statickou IP tak jak požadujete a klikněte na Applay (Použít).

Dále budete chtít aby se defaultní připojení nepřipojovalo automaticky. To uděláte tak, že spustíte:

```
$ sudo nm-connection-editor  # you must use sudo, not su

```

V connection editor editujte defalult conection (eg "Auto eth0") a odškrtněte "Connect automatically". Klikněte na Applay(Použít) a zavřete connection editor.

## Tipy and triky

### Kontrola jestli je networking spouštěn cronem nebo skriptem

Některé úlohy cronu k úspěchu vyžadují, aby byla síť funkční. Možná si bude přát vyhnout se spouštění těchto úloh, když je síť vypnutá. K dokončení tohoto přidejte **if** test pro síť, který je vyžadován NetworkManager **nm-tool** a zkontroluje status sítě. Test zde uspěje jestliže některé rozhraní je činné a selže jesltiže jsou všechna rozhraní nečinná. Toto je vhodné pro laptopy, které mohoubýt připojeni drátově, bezdrátově nebo nepřipojeny.

```
if [ `nm-tool|grep State|cut -f2 -d' '` == "connected" ]; then
       #Whatever you want to do if the network is online
else
       #Whatever you want to do if the network is offline - note, this and the else above are optional
fi

```

Toto je užitečné pro skrip cron.hourly který například spouští **fpupdate** pro F-Prot virus skaner update. Další způsosb, který může být užitečný jen s malími úpravami, je rozdíl mezi sítěmi používající různé výstupy z **nm-tool**; například od té doby co je aktivní bezdrátová síť označena hvězdičkou, můžete použít grep pro vyfiltrování síťového jména a pak pomocí grepu odfiltrovat znak hvězdička.

### Automatické odemknutí keyring po přihlášení

#### Gnome

1.  Klikněte pravým tlačítkem na ikonu NM ve vašem panelu a vyberte Edit Connections a otevřete záložku Wireless
2.  Vyberte to spojení které chcete upravovat a klikněte na tlačítko Edit
3.  Zaškrtněte "Connect Automatically" a "Available to all users"

K dokončení se odhlašte a znovu přihlašte.

**Note:** Následující metoda je zastaralá a je známo, že nepracuje na úplně každém stroji!

_*V `/etc/pam.d/gdm` (nebo vašem odpovídajícím démonu v /etc/pam.d), přidejte tyto řádky na konec bloku "auth" a "session" za předpokladu, že ještě neexistují:_

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   V `/etc/pam.d/passwd`, použijte tento řádek pro blok 'password':

```
 password    optional    pam_gnome_keyring.so

```

	Příště až se přihlásíte, měli by jste být dotázáni, jestli chcete aby heslo bylo odemknuto automaticky při přihlášení.

#### KDE

**Note:** Pro podrobnosti se podívejte na [http://live.gnome.org/GnomeKeyring/Pam](http://live.gnome.org/GnomeKeyring/Pam) a pokud používáte kde / kdm, můžete použít pam-keyring-tool z AUR.

*   Vložte skript jako je ten následující do ~/.kde4/Autostart:

```
 $!/bin/sh
 echo PASSWORD | /usr/bin/pam-keyring-tool --unlock --keyring=default -s

```

	Podobné by měli pracovat s openbox, lxde, etc.

### Automatické připojení při bootu

Od verze 0.7 je NetworkManager schopen se připojit při bootu, před přihlášením uživatele a odemknutí keyringu.

*   Nejdříve se ujistěte, že keyfile plugin je nahrán; `/etc/NetworkManager/NetworkManager.conf` měl by vypadat takhle:

```
 [main]
 plugins=keyfile

```

*   Jestliže to nebylo v souboru předtím, budete muset restartovat **nm-system-settings**:

```
 # killall -TERM nm-system-settings

```

	nebo jednoduše restartovat celý systém.

*   Nyní garantujte přístupová práva vašemu uživateli modifikovat system-connection (systémová připojení):

Pomocí **polkit**:

Umístěte následující v /etc/polkit-1/localauthority/50-local.d/10-org-freedesktop-network-manager-settings.pkla

```
[Allow user YOURUSERNAME to create wireless connections for all users]
Identity=unix-user:YOURUSERNAME
Action=org.freedesktop.network-manager-settings.system.modify
ResultAny=no
ResultInactive=no
ResultActive=yes

```

	Konečeně, v editoru připojení (z gnome appletu), zaškrtněte **Available to all users**.

Připojení je nyní uloženo v **/etc/NetworkManager/system-connections/"CONNECTION NAME"**. Při startu se NetworkManager pokusí připojit, pokud je v dosahu sítě.

**Note:** Podle [tohoto](https://bugs.kde.org/show_bug.cgi?id=204340) nahlášení bugu, <tt>knetworkmanager</tt> ještě nemá implementován tento prvek. Budete potřebovat použít GNOME síťový applet (<tt>nm-applet</tt>). Nainstalování bylo popsáno výše na této stránce, <tt>"killall knetworkmanager"</tt>, po té nastartujte <tt>nm-applet</tt>.
Prosím hlasujte pro tento bug!

### Ignorování určitých zařízení

Občas může být vyžadována, aby network manager ignoroval některá zařízení a nepokoušel se získat IP.

*   Nejprve musíte zjistit Hal UDI (např. pomocí lshal):

```
 ...
 info.product = 'Networking Interface'  (string)
 info.subsystem = 'net'  (string)
 info.udi = '/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55'  (string)
 linux.hotplug_type = 2  (0x2)  (int)
 linux.subsystem = 'net'  (string)
 ...

```

*   Přidat toto udi do /etc/NetworkManager/nm-system-settings.conf:

```
 [keyfile]
   unmanaged-devices=/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55

```

	Složená zařízení mohou být specifikovaána, ohraničena středníky:

```
 [keyfile]
   unmanaged-devices=/org/freedesktop/Hal/devices/net_00_1f_11_01_06_55;/org/freedesktop/Hal/devices/net_00_2c_6d_e2_08_af

```

Po aplikování změn nebude potřeba restartovat NetworkManager.

*   Ignoring a type of device at boot time.

this script was used to ignore all ethernet devices at boot time of a archiso build, it can be changed to ignore wifi devices etc. /!\being used on a non-persistant filesystem, the nm-system-settings.conf is default at run time

```
  #!/bin/sh
  # author: tim noise <darknoise@drkns.net>
  COUNT=0
  TARGET_FILE="/etc/NetworkManager/nm-system-settings.conf"
  for i in `lshal | grep -A6 'Networking Interface' | awk -F "'" '/info.udi = / {print $2}'`; do
      if [ $COUNT = 0 ]; then
          COUNT=$COUNT+1;
          echo "unmanaged-devices=$i" >> $TARGET_FILE
      else
          echo -n ";$i" >> $TARGET_FILE
      fi
  done
  printf "\n" >> $TARGET_FILE

```