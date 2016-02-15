## Contents

*   [1 Stap 1](#Stap_1)
*   [2 Installatie](#Installatie)
    *   [2.1 Drivers](#Drivers)
        *   [2.1.1 wlan-ng](#wlan-ng)
        *   [2.1.2 rt2x00](#rt2x00)
        *   [2.1.3 madwifi (verouderd)](#madwifi_.28verouderd.29)
        *   [2.1.4 ipw2100 and ipw2200](#ipw2100_and_ipw2200)
        *   [2.1.5 ipw3945 (verouderd)](#ipw3945_.28verouderd.29)
        *   [2.1.6 orinoco](#orinoco)
        *   [2.1.7 ndiswrapper](#ndiswrapper)
        *   [2.1.8 prism54](#prism54)
        *   [2.1.9 ACX100/111](#ACX100.2F111)
        *   [2.1.10 BCM43XX](#BCM43XX)
*   [3 Setup and Boot](#Setup_and_Boot)
    *   [3.1 Using the Archlinux Wireless Network settings (verouderd)](#Using_the_Archlinux_Wireless_Network_settings_.28verouderd.29)
    *   [3.2 Using the Arch Linux Roaming Network Profiles (verouderd)](#Using_the_Arch_Linux_Roaming_Network_Profiles_.28verouderd.29)
        *   [3.2.1 Quick Setup](#Quick_Setup)
    *   [3.3 Wifi-radar](#Wifi-radar)
    *   [3.4 NetworkManager](#NetworkManager)
    *   [3.5 Using phrakture's old scripts (very outdated)](#Using_phrakture.27s_old_scripts_.28very_outdated.29)
*   [4 Misc Links](#Misc_Links)

## Stap 1

1.  Zoek eerst even uit of Linux jouw specifieke hardware ondersteund. Je kunt uitzoeken wat voor een card je hebt met het 'lshwd' commando.
    *   [wlan-ng](http://www.linux-wlan.org/docs/wlan_adapters.html.gz) ondersteund een boel wireless kaarten, check hier dus eerst even.
    *   [madwifi](http://madwifi.org) voor Atheros chipsets (AR5210, AR5211, AR5212 en AR5213)
    *   [rt2x00](http://rt2x00.serialmonkey.com/wiki/index.php/Main_Page) voor Ralink's rt2400, rt2500, en rt2570 chipsets.
    *   [ipw2100](http://ipw2100.sourceforge.net/) voor Intel Pro/Wireless 2100 Mini PCI
    *   [ipw2200](http://ipw2200.sourceforge.net/) voor Intel Pro/Wireless 2200 Mini PCI
    *   [ipw3945](http://ipw3945.sourceforge.net/) voor Intel Pro/Wireless 3945 AB/G Mini PCI-E
    *   [orinoco](http://www.nongnu.org/orinoco/devices/) voor sommige Prism 2 gebaseerde kaarten
    *   [prism54](http://prism54.org/) voor Prism 54 gebaseerde kaarten
    *   Check ook even [Linux Wireless Support](http://linux-wless.passys.nl/) voor jouw hardware, of in de [hardware compatibility list](http://www.linuxquestions.org/hcl/index.php?cat=10) (HCL) waar ook een boel linux-vriendelijke kaarten in staan.
2.  Als je kaart alleen maar ondersteund word door Windows
    *   [ndiswrapper](http://ndiswrapper.sourceforge.net/wiki/index.php/List) voor hardware die alleen ondersteund word door Windows (Broadcom, 3com, etc)
    *   Je hebt dat de .inf en .sys bestanden nodig van je windows driver - [check hier](http://ndiswrapper.sourceforge.net/mediawiki/index.php/List)
3.  Als je hardware nergens vermeld staat
    *   Dan heb je een -of- een probleem, of je kunt nog
    *   Een websearch proberen met jouw exacte modelnaam, of hardware met 'linux' als keyword - je kunt ook nog om hulp vrage op [het forum](https://bbs.archlinux.org)

## Installatie

Je hebt sowieso **wireless-tools** nodig van pacman

 `pacman -S wireless_tools` 

Je hardware zal -niet- geinitialiseerd worden zonder deze software

### Drivers

Nu volgen de specifieke detail voor elke driver, onthoud dat je het beste even de [HCL](http://www.linuxquestions.org/hcl/index.php?cat=10%7CLQ) kunt checken om te kijken wat de beste driver is voor jouw kaart.

#### wlan-ng

 `pacman -S wlan-ng24` voor de Linux 2.4 kernel of `pacman -S wlan-ng26` voor de 2.6 kernel

#### rt2x00

Zie de [rt2x00 wiki page](/index.php/Using_the_new_rt2x00_beta_driver "Using the new rt2x00 beta driver")

#### madwifi (verouderd)

[AUR PKGBUILD](https://aur.archlinux.org/packages.php?do_Details=1&ID=785)
**Let op:**Madwifi-ng zit nu in de unstable package-repository. Je kunt dus gewoon de unstable repository gebruik in plaats van de pkgbuild..

**Let op:**Als je Madwifi drivers van voor Januari 23, 2006 gebruik, moet je de interface opgeven die je wilt gebruiken. Recentere versies hebben dit niet nodig, en dus kun je doorgaan naar ifconfig. Deze stap is door de meeste andere drivers niet nodig hebben. Als je van je wifi0 , ath0 wil maken, moet je het volgende commando uitvoeren: `wlanconfig ath0 create wlandev wifi0 wlanmode sta` Natuurlijk gevolgd door de volgende commando's:

```
ifconfig ath0 up
iwconfig ath0 essid <jouw-essid> key <jouw-wep-key>
dhclient ath0
```

Je kunt deze commando's het beste in /etc/rc.local zetten, zodat ze bij elke boot worden uitgevoerd.

Je kunt het ook in /etc/rc.conf of /etc/conf.d/wireless, hier een voorbeelde voor je rc.conf

```
ath0="ath0 192.168.100.1 netmask 255.255.255.0 broadcast 192.168.100.255" | ath0="dhcp"
wlan_ath0="ath0 essid <jouw-essid> key <jouw-wep-key>"
WLAN_INTERFACES=(ath0)

```

Vergeet ook niet (ath0) in de INTERFACE keyword te zetten, zodat ath0 opgestart word bij het booten.:

```
Voor:
INTERFACES=(lo eth0)
Na:
INTERFACES=(lo eth0 ath0)

```

*   **Let Op:** Het kan zijn dat je de 'country-code' instellen tijdens het laden van de module, om channels te gebruiken, en de tx-power in te kunnen stellen die legaal zijn in jouw land. In nederland zou je deze country-code moeten gebruiken:

 `modprobe ath_pci countrycode=528` 

*   Dit kun je ook tijdens het booten doen, door het in /etc/modprobe.d/modprobe.conf te zetten (voor 2.6 kernels)

```
#/etc/modprobe.d/modprobe.conf
options ath_pci countrycode=<jouw land-code>

```

*   Je kunt je instellingen verifieren door middel van het 'iwlist' commando, zie ook 'man iwlist'. Zie ook de [CountryCode](http://madwifi.org/wiki/UserDocs/CountryCode) pagina op de madwifi wiki.

#### ipw2100 and ipw2200

Om de correcte firmware met pacman te installeren:

 `pacman -S ipw2100-fw` 

Voor de ipw2200 chipset moet je wat anders doen, namelijk:

 `pacman -S ipw2200-fw` 

Nadat pacman de firmware heeft geinstalleerd, moet je er zeker van zijn dat de firmware geladen is. Als je dat niet zeker weet -> reboot.

Nu zou je wireless moeten werken. Als het nog niet werkt, check dan even of hij uberhaupt wel aanstaat. Op een Dell moet je vaak Fn + F2 drukken om het te activeren. Check [laptop matrix](http://rfswitch.sourceforge.net/?page=laptop_matrix) om uit te vinden welke toetsencombinatie jij moet gebruiken, of raadpleeg je handleiding.

#### ipw3945 (verouderd)

 `pacman -S ipw3945` 

dit zou de volgende packages moeten installeren: ipw3945-ucode, ipw3945, and ipw3945d (daemon)

en om de module bij startup te laden...

 `nano /etc/rc.conf` 

in de modules=() array, moet je ipw3945 aan het lijstje toevoegen

in de daemons=() array, moet je ipw3945d aan het lijstje toevoegen

CTRL + X, Y om op te slaan + sluiten.

De ipw3945 module moet laden tijden "Loading Modules.." en "Starting IPW3945d" moet verschijnen tijdens het initialiseren van de daemons, en dan zou ethX ook aanwezig moeten zijn. be present.

#### orinoco

Deze driver zit standaard al in de kernel, en zou dus al moeten werken.

#### ndiswrapper

Ndiswrapper is geen echte driver, maar je kunt het gebruiken wanneer er geen echte specifieke linux drivers zijn. Om het te gebruiken heb je de *.inf bestanden nodig van je Windows driver. Het installeren van ndiswrapper gaat als volgt:

 `pacman -S ndiswrapper ndiswrapper-utils` 

_Let op:_ AchrCK en Beyond kernels hebben de packages ndiswrapper-archck en ndiswrapper-beyond in plaats van de ndiswrapper package!

Zodra de installatie klaar is, moet je ndiswrapper configureren:

```
ndiswrapper -i filename.inf
ndiswrapper -l
ndiswrapper -m
depmod -a
```

Nu zijn we bijna klaar met installeren, alleen nog je /etc/rc.conf aanpassen, zodat hij de module tijdens het booten laad (hier beneden een voorbeeld van mijn config, die van jou zou er anders uit kunnen zijn):

 `MODULES=(ndiswrapper snd-intel8x0 !usbserial)` 

het is belangrijk dat ndiswrapper in deze lijn staat. Nu kun je testen of ndiswrapper laad:

```
modprobe ndiswrapper
iwconfig
```

en nu zou wlan0 moeten bestaan, check deze pagina als je problemen hebt: [Ndiswrapper installation wiki](http://ndiswrapper.sourceforge.net/mediawiki/index.php/Installation)

#### prism54

Download de firmware voor je kaart van: [prism54.org](http://www.prism54.org/). en rename de file naar 'isl3890'. Als hij nog niet bestaat, maak dan de directory /lib/firmware en zet de file daarin. Dit zou alles moeten zijn. ([forum source](https://bbs.archlinux.org/viewtopic.php?t=16569&start=0&postdays=0&postorder=asc&highlight=siocsifflags+such+file++directory))

#### ACX100/111

De ACX100/111 driver kan gevonden worden op [[1]](http://acx100.sourceforge.net/). Deze driver kan gebruikt worden voor WiFi kaarten die gebaseerd zijn op de Texas Instruments ACX100/111 chipset.

In tegenstelling tot wat mensen denken, is het reletief eenvoudig om dit op te zetten. Er is reeds een uitgebreide gids geschreven door Craig [here](http://www.houseofcraig.net/acx100_howto.php). Echter, de README die bij de driver zit is waarschijnlijk makkelijker te volgen.

1.  Download de laatste versie van de driver.
2.  Pak de driver uit naar een directory naar keuze. LET OP: er zit geen aparte directory structuur in het archief, let dus op waar je hem uitpakt gezien het grote aantal bestanden.
3.  Ga naar de directory met de zojuist uitgepakt bestanden.
4.  Voer uit `make -C /lib/modules/`uname -r`/build M=`pwd`` 
5.  Verander naar root user (su/sudo).
6.  Voer uit `make -C /lib/modules/`uname -r`/build M=`pwd` modules_install` 
7.  Voer uit `depmod -ae` so the kernel detects the new module.
8.  Voer nu de Driver CD in, die bij de kaart werd meegeleverd, de CD/DVD drive van jouw computer.
9.  Mount de CD/DVD met `mount <device>` 
10.  Kopieer de firmware van de CD naar /lib/firmware.
11.  Hernoem de firmware naar 'tiacxNNNcMM' (NNN=100/111, MM=radio module ID (in uppercase hex)) voor de PCI driver of tiacxNNNusbcMM voor de USB driver.
12.  Laad de acx module met `modprobe acx` 
13.  Voeg de acx module toe aan de MODULES regel in /etc/rc.conf zodat hij geladen wordt tijdens het starten van jouw computer.
14.  Volg de instructies voor het starten van een connectie met het netwerk m.b.v. iwconfig.

Extra: het is ook mogelijk de driver te compileren in de kernel tree. Hoe dit moet is gedocumenteerd in de README van de driver.

#### BCM43XX

De gebruikers van Broadcom die de 43xx reeks chipsets hebben, beschikken over een nieuw alternatief voor ndiswrapper! Eindelijk! In kernel versie 2.6.17, werd de driver bcm43xx geïntroduceerd, en ze hebben het je wel heel makkelijk gemaakt!

1.  Voer uit `iwconfig` of `hwd -s` om te bepalen dat je een aangewezen kaart hebt. Mijn 'output' van hwd - s zag er zo uit: `Network    : Broadcom Corp.|BCM94306 802.11g NIC module: unknown` 
2.  Voer uit `pacman -S bcm43xx-fwcutter` om de firmware cutter te installeren.
3.  Download de windows driver voor jouw netwerkkaart om de firmware te extrahere.
    *   I initially downloaded the driver from Dell's support site. When that didn't work I found a link on the Ubuntu Wiki and used that file instead: [[2]](http://drinus.net/airport/wl_apsta.o). I just saved this file to my desktop, you won't need it after the next step.
4.  Run `bcm43xx-fwcutter -w /lib/firmware /home/<user>/Desktop/wl_apsta.o` You may have to create /lib/firmware first.
5.  Restart, and configure your device as normal. You may want to add bcm43xx into the modules section of your rc.conf file. Good luck!

## Setup and Boot

Archlinux provides two methods for enabling wireless connections. The first method is based on the existing network script and is to be used for non-roaming wireless access. If you're only on 1 wireless network, this is the best setup to use. However, if you continually roam from network to network, the Network Profiles setup would be best, though slightly more complicated.

### Using the Archlinux Wireless Network settings (verouderd)

*   Typical Archlinux Wireless configuration is rather straight forward. The network itself is configured in the exact same way a non-wireless network is in /etc/rc.conf. For example:

```
# /etc/rc.conf
wlan0="dhcp"
INTERFACES=(lo eth0 wlan0)

```

*   Beyond this, the networking scripts need some way to determine that wlan0 is a wireless interface (as not all wireless interfaces are wlan*). This is done in the /etc/conf.d/wireless file. The setup here is very simple. For each wireless interface, you simply declare a setting called wlan_<interface name>. If your wireless interface is "wlan0", it uses wlan_wlan0\. If your wireless interface is "eth1", wlan_eth1 is what you need. The value for this setting is simply the parameters to iwconfig (see man iwconfig for details) _including the interface name_.
*   A simply, non encrypted setup for the above would look like:

```
# /etc/conf.d/wireless
wlan_wlan0="wlan0 essid MyEssid"

```

*   _phrakture's trick_
    *   My personal trick isn't much of a trick at all, it just simplifies a lot of the process. While /etc/conf.d/wireless is sourced (included) in the network script, it is not a requirement for having a wireless interface. Therefore, the actual settings for the wireless interface can exist in anything sourced by the network script. For that reason, I put all my settings in /etc/rc.conf:

```
# /etc/rc.conf
eth0="dhcp"
wlan0="dhcp"
wlan_wlan0="wlan0 essid MyEssid"
#wlan_wlan0="wlan0 essid MyEssid key 12345678"
#wlan_wlan0="wlan0 essid MyEssid key s:wirelesspassword"
INTERFACES=(lo eth0 wlan0)

```

If your wireless card is eth0 so you change wlan_wlan0 in wlan_eth0="eth0 essid ...."

### Using the Arch Linux Roaming Network Profiles (verouderd)

#### Quick Setup

1.  Create new profile
    1.  Create a new network profile in <tt>/etc/network-profiles/</tt> based on the <tt>template</tt> file. Let's call it <tt>home</tt>. Remember the filename you chose! We'll use it to refer to our new profile later.
    2.  Adjust the settings in the new profile to your needs.
2.  Remove outdated settings from <tt>rc.conf</tt>
    1.  Remove all interfaces which should be managed by the Network Profiles in the future from INTERFACES.
    2.  Remove any relevant routes from ROUTES.
    3.  Leave the "lo" interface in place.
3.  Add Network Profile settings to <tt>rc.conf</tt>
    1.  Add the name of your new network profile to <tt>NET_PROFILES=()</tt> `NET_PROFILES=(home)` 

So much for the quick setup... You can also set <tt>NET_PROFILES</tt> to "menu" and it will present a dialog/ncurses menu (which requires the [dialog](https://www.archlinux.org/packages/?name=dialog) package installed) at bootup where you can pick the profile you want.

Alternatively, you can pass a <tt>NET=</tt> value on the kernel boot line, telling netcfg which profile you wish to start with.

```
vmlinuz root=/dev/hda3 vga=773 ro NET=home

```

Picked from [Judd's explanation](https://www.archlinux.org/pipermail/arch/2005-June/004855.html).

**Simple Wireless Autodetection** iphitus created an autodetection patch for the official initscripts which has now been imported as standard. Please see [here](https://www.archlinux.org/pipermail/arch/2005-July/005251.html) for an explanation of how it works.

**WPA support** phydeaux created a great patch for WPA support which has been adopted straight into the main tree and will be in the next release (after 0.7.1). For informtion about how to use WPA with the Network Profiles see also [Ndiswrapper and wpa supplicant](/index.php/Ndiswrapper_and_wpa_supplicant "Ndiswrapper and wpa supplicant").

**Netcfg GUI** A simple GUI script to switch networkprofile from GNOME (or another window manager) can be found in [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=4197). ([Screenshots](http://mac-cain13.livejournal.com/tag/netswitch))

### Wifi-radar

**Wifi-radar** This is a nifty little GUI program that lets you switch wireless networks with ease. Simply do the following:

1.  # pacman -S wifi-radar
2.  # visudo

```
   here, add the following line: 
       yourusername     ALL=(ALL) NOPASSWD: /usr/sbin/wifi-radar
   then press ESC, then colon (:), then x, then ENTER to save and exit.

```

1.  now, just add wifi-radar to your daemons list in /etc/rc.conf, and run wifi-radar from your internet menu and you're all set :)
2.  oh, and you might need to edit /etc/conf.d/wifi-radar to set the particular network interface that you want to use

### NetworkManager

**NetworkManager** A more advanced network management system for Linux. This is included in various Linux distributions and now can be used in Arch Linux. It is very painless for roaming users, and includes an easy-to-use GUI program for selcting your desired network. One caveat however is that you are prompted for your keyring password every time you log into gnome and the program starts. This most likely won't be fixed until later versions, and can be quite annoying. More information on NetworkManager can be found at: [Networkmanager](/index.php/Networkmanager "Networkmanager").

### Using phrakture's old scripts (very outdated)

*   In order to use these scripts, place them where indicated. The main script is in /etc/rc.d and the profiles are in /etc/conf.d/wireless-profiles. Making a new profile involves copying the sample and renaming it. The script can be used in two ways. It can be added to the DAEMONS array, with an added WIRELESS_PROFILES collection in rc.conf that lists the profiles to start on boot. In addition, the script can be called manually: /etc/rc.d/wireless start/stop/restart will use the listed profiles in rc.conf, and /etc/rc.d/wireless profile sample up/down will use a named profile and bring it up or down.
*   [Wireless Bootup Script](/index.php?title=Wireless_Bootup_Script&action=edit&redlink=1 "Wireless Bootup Script (page does not exist)") - /etc/rc.d/wireless
*   [Sample Wireless Profile](/index.php?title=Sample_Wireless_Profile&action=edit&redlink=1 "Sample Wireless Profile (page does not exist)") - /etc/conf.d/wireless-profiles/sample/*

## Misc Links

*   [An overly wordy howto that rarely helps](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Wireless.html)