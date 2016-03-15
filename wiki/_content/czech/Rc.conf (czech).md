Soubor `rc.conf` (`/etc/rc.conf`) je základní konfigurační soubor používaný v Arch Linuxu. V tomto jediném souboru se nachází základní nastavení systému jako časové pásmo, rozložení kláves, jaderné moduly nebo spouštěné daemony.

## Contents

*   [1 Přehled](#P.C5.99ehled)
*   [2 Lokalizace](#Lokalizace)
*   [3 Hardware](#Hardware)
*   [4 Sítě](#S.C3.ADt.C4.9B)
*   [5 Démony](#D.C3.A9mony)

## Přehled

Takto vypadá soubor `rc.conf` po čerstvé instalaci ([zdroj](https://projects.archlinux.org/initscripts.git/tree/rc.conf)):

 `/etc/rc.conf` 
```
#
# /etc/rc.conf - Main Configuration for Arch Linux
#

# -----------------------------------------------------------------------
# LOCALIZATION
# -----------------------------------------------------------------------
#
# LOCALE: available languages can be listed with the 'locale -a' command
#   LANG in /etc/locale.conf takes precedence
# DAEMON_LOCALE: If set to 'yes', use $LOCALE as the locale during daemon
# startup and during the boot process. If set to 'no', the C locale is used.
# HARDWARECLOCK: set to "", "UTC" or "localtime", any other value will result
#   in the hardware clock being left untouched (useful for virtualization)
#   Note: Using "localtime" is discouraged, using "" makes hwclock fall back
#   to the value in /var/lib/hwclock/adjfile
# TIMEZONE: timezones are found in /usr/share/zoneinfo
#   Note: if unset, the value in /etc/localtime is used unchanged
# KEYMAP: keymaps are found in /usr/share/kbd/keymaps
# CONSOLEFONT: found in /usr/share/kbd/consolefonts (only needed for non-US)
# CONSOLEMAP: found in /usr/share/kbd/consoletrans
# USECOLOR: use ANSI color sequences in startup messages
#
LOCALE="en_US.UTF-8"
DAEMON_LOCALE="no"
HARDWARECLOCK="UTC"
TIMEZONE="Canada/Pacific"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

# -----------------------------------------------------------------------
# HARDWARE
# -----------------------------------------------------------------------
#
# MODULES: Modules to load at boot-up. Blacklisting is no longer supported.
#   Replace every !module by an entry as on the following line in a file in
#   /etc/modprobe.d:
#     blacklist module
#   See "man modprobe.conf" for details.
#
MODULES=()

# Udev settle timeout (default to 30)
UDEV_TIMEOUT=30

# Scan for FakeRAID (dmraid) Volumes at startup
USEDMRAID="no"

# Scan for BTRFS volumes at startup
USEBTRFS="no"

# Scan for LVM volume groups at startup, required if you use LVM
USELVM="no"

# -----------------------------------------------------------------------
# NETWORKING
# -----------------------------------------------------------------------
#
# HOSTNAME: Hostname of machine. Should also be put in /etc/hosts
#
HOSTNAME="myhost"

# Use 'ip addr' or 'ls /sys/class/net/' to see all available interfaces.
#
# Wired network setup
#   - interface: name of device (required)
#   - address: IP address (leave blank for DHCP)
#   - netmask: subnet mask (ignored for DHCP) (optional, defaults to 255.255.255.0)
#   - broadcast: broadcast address (ignored for DHCP) (optional)
#   - gateway: default route (ignored for DHCP)
# 
# Static IP example
# interface=eth0
# address=192.168.0.2
# netmask=255.255.255.0
# broadcast=192.168.0.255
# gateway=192.168.0.1
#
# DHCP example
# interface=eth0
# address=
# netmask=
# gateway=

interface=
address=
netmask=
broadcast=
gateway=

# Setting this to "yes" will skip network shutdown.
# This is required if your root device is on NFS.
NETWORK_PERSIST="no"

# Enable these netcfg profiles at boot-up. These are useful if you happen to
# need more advanced network features than the simple network service
# supports, such as multiple network configurations (ie, laptop users)
#   - set to 'menu' to present a menu during boot-up (dialog package required)
#   - prefix an entry with a ! to disable it
#
# Network profiles are found in /etc/network.d
#
# This requires the netcfg package
#
#NETWORKS=(main)

# -----------------------------------------------------------------------
# DAEMONS
# -----------------------------------------------------------------------
#
# Daemons to start at boot-up (in this order)
#   - prefix a daemon with a ! to disable it
#   - prefix a daemon with a @ to start it up in the background
#
# If you are sure nothing else touches your hardware clock (such as ntpd or
# a dual-boot), you might want to enable 'hwclock'. Note that this will only
# make a difference if the hwclock program has been calibrated correctly.
#
# If you use a network filesystem you should enable 'netfs'.
#
DAEMONS=(syslog-ng network crond)

```

## Lokalizace

*   `[LOCALE](/index.php/LOCALE "LOCALE")`: Nastavuje jazyk systému, který bude použit všemi aplikacemi podporujícími i18n. Seznam dostupných locales získáte pomocí konzolového příkazu `locale -a`. České locales jsou k dispozici ve dvou kódováních: UTF-8 a ISO-8859-2.

Nastavení českého UTF-8 locale:

V souboru `/etc/locale.gen` nalezněte řádek

```
#cs_CZ.UTF-8 UTF-8

```

odstraňte dvojkřížek ze začátku řádku a soubor uložte:

```
cs_CZ.UTF-8 UTF-8

```

Poté zaktualizujte systémová locales příkazem

```
$ sudo locale-gen

```

Řádek LOCALE v souboru `rc.conf` upravte následovně:

```
LOCALE="cs_CZ.UTF-8"

```

*   `HARDWARECLOCK`: Určuje, jestli systémové hodiny pracují s `UTC` časem nebo místním časem (`localtime`). `UTC` je smysluplný vzhledem k jednodušším změnám časových pásem a nastavení letního času.`localtime` je ale nutný, pokud máte nainstalované jiné operační systémy, které pracují jenom s místním časem v systémových hodinách, jako např. Windows.

**Note:** GNU/Linux změní čas automaticky při přechodu na letní čas a zpět pouze, když je `HARDWARECLOCK` nastavený na `UTC`; bez ohledu na to, zda při samotném přechodu byl spuštěn nebo ne. Pokud je `HARDWARECLOCK` nastaven na `localtime`, GNU/Linux čas nepřenastaví, protože předpokládá, že na počítači jsou provozováný jiný operační systém, který se o nastavení letního času postará. Pokud tomu tak není, musí být letní čas nastaven manuálně.

*   `TIMEZONE`: Určuje časové pásmo. Dostupná časová pásma jsou relativní cesty k pásmovým souborům začínající od adresáře `/usr/share/zoneinfo`. Například časové pásmo pro Českou republiku je `Europe/Prague`, což odkazuje na soubor `/usr/share/zoneinfo/Europe/Prague`. Odpovídající řádek v `rc.conf`:

```
TIMEZONE="Europe/Prague"

```

*   `[KEYMAP](/index.php/KEYMAP "KEYMAP")`: Rozložení klávesnice, které budeme používat v konzoli. Pro ČR to bude pravděpodobně cz-qwertz. Dostupná rozložení naleznete v adresáři `/usr/share/kbd/keymaps`. Berte na vědomí, že toto nastavení platí pouze pro konzoli, nikoli pro grafické správce oken nebo X!

*   `[CONSOLEFONT](/index.php/Fonts#Console_fonts "Fonts")`: Určuje, který konzolový font se nahraje při startu systému programem `setfont`. Dostupné fonty naleznete v `/usr/share/kbd/consolefonts`. Příklad nastavení fontu s podporou českých znaků:

```
CONSOLEFONT="Lat2-Terminus16"

```

*   `[CONSOLEMAP](/index.php/Fonts#Console_fonts "Fonts")`: Určuje, které mapování konzole (např. 8859-1_to_uni) se má nahrát při startu systému. Dostupná mapování naleznete v `/usr/share/kbd/consoletrans`. Nastavení by mělo odpovídat vašemu locale (např. 8859-2 pro Latin2), pokud výše používáte utf8 locale a provozujete programy, které generují 8bitový výstup. Jestli při každodenní práci používáte X11, uvědomte si, že toto nastavení ovlivní pouze výstup konzolových aplikací.

*   `USECOLOR`: Povolí (nebo zakáže) použití barevně zvýrazněných zpráv během startovacího procesu.

## Hardware

*   `MOD_AUTOLOAD`: Pokud je nastavený na "yes", proběhne při startu autodetekce hardwaru a potřebné moduly budou nahrány automaticky pomocí [udev](/index.php/Udev "Udev").

**Tip:** Automatické nahrávání modulů můžete zakázat, a tím urychlit startovací proces. Musíte si ale být jisti, že všechny potřebné moduly máte uvedeny v poli `MODULES`. Zjistit potřebné moduly můžete pomocí utility [hwdetect](/index.php/Hwdetect "Hwdetect") nebo pomocí [lshwd](https://aur.archlinux.org/packages/lshwd/), což je alternativa, kterou naleznete v [AUR](/index.php/AUR "AUR").

*   `MOD_BLACKLIST`: Pole je označené jako zastaralé. Pokud chcete modul blacklistovat (zabránit jeho načtení), zapište ho do pole MODULES a použijte před ním prefix `!jméno_modulu`.

*   `MODULES`: Do tohoto pole můžete vypsat moduly, které chcete načíst během startovacího procesu, aniž byste je museli přiřazovat k nějakému hardwarovému zařízení jako v `modprobe.conf`. Jednoduše sem napište jméno modulu, jednotlivé moduly od sebe oddělujte mezerou. Pokud chcete modul nastavit, učiňte tak v `modprobe.conf`. Pokud před jméno modulu napíšete vykřičník (!), modul se nebude načítat během startu systému.

**Tip:** Stává-li se vám, že při každém startu mají síťové adaptéry jiné označení, je výhodné zde uvést jejich moduly; síťové adaptéry pak budou detekovány pokaždé ve stejném pořadí podle pořadí modulů. Ještě lepší způsob je odpovídajícím způsobem nakonfigurovat [udev](/index.php/Udev "Udev") a používat statická jména jednotlivých rozhraní.

*   `USELVM`: Volba pro načítání [LVM](/index.php/LVM "LVM") svazků při startu systému, nutná, pokud používáte LVM. Nastavení na "YES" spustí během inicializace systému vgchange.

## Sítě

*   `[HOSTNAME](/index.php/HOSTNAME "HOSTNAME")`: Nastavte jméno počítače (bez doménové části). Může být libovolné, pokud použijete písmena bez diakritiky, číslice nebo některé speciální znaky jako pomlčka. Nebuďte zde příliš kreativní, pokud nevíte přesně co nastavit, ponechte předvolenou hodnotu.

*   `INTERFACES`: Zde nastavujete síťová rozhraní. Přednastavené řádky včetně komentářů vysvětlují nastavení dostatečně. Pokud ke konfiguraci nepoužíváte DHCP, nezapomeňte, že hodnota proměnné (jejíž jméno musí odpovídat jménu zařízení, které má být konfigurováno) je stejná s parametry, které byste zapsali za příkaz `ifconfig`, kdybyste zařízení konfigurovali ručně v konzoli.

*   `ROUTES`: Zde můžete definovat vlastní statické síťové cesty s libovolnými názvy. Nastavení je zřejmé již z uvedeného příkladu. Část v uvozovkách je to, co byste napsali za příkaz `route add` při ruční konfiguraci.

*   `NETWORKS`: Toto aktivuje síťové profily při startu. Síťové profily jsou příhodný způsob správy více síťových konfigurací a mají nahradit standardní nastavení `INTERFACES`/`ROUTES`, které je doporučováno pro stroje s jedinou síťovou konfigurací. Pokud se váš počítač bude připojovat pravidelně do různých sítí (např. notebook), můžete nakonfigurovat profily v adresáři `/etc/network.d`. Nové profily můžete vytvořit podle předloh v `/etc/network.d/examples`.

## Démony

*   `[DAEMONS](/index.php/DAEMONS "DAEMONS")`: Toto pole je jednoduše seznam skriptů nacházejících se v `/etc/rc.d/`, které se mají spouštět při startu systému. Jednotlivé položky se oddělují mezerou. Pokud je před jménem skriptu vykřičník (!), tak není spouštěn. Pokud je před jménem skriptu symbol zavináče (@), je spouštěn na pozadí, tj. startovací proces nečeká na úspěšné dokončení před svým dalším pokračováním. Toto pole budete upravovat, kdykoli nainstalujete nějakou systémovou službu (např. `sshd`), a budete chtít, aby se spouštěla automaticky při startu systému.

**Note:** Záleží na pořadí, ve kterém jsou démony uvedeny, ve stejném pořadí jsou spouštěny.