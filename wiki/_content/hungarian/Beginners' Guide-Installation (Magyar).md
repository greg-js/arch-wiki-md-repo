**Tip:** Ez az oldal a teljes Beginners' Guide (Magyar) útmutató egyik részoldala. Ha az útmutatót teljes egészében akarod olvasni, akkor **[kattints ide](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)")**.

## Contents

*   [1 Telepítés](#Telep.C3.ADt.C3.A9s)
    *   [1.1 Telepítési forrás kiválasztása](#Telep.C3.ADt.C3.A9si_forr.C3.A1s_kiv.C3.A1laszt.C3.A1sa)
        *   [1.1.1 Hálózat beállítása](#H.C3.A1l.C3.B3zat_be.C3.A1ll.C3.ADt.C3.A1sa)
            *   [1.1.1.1 ADSL bridging beállítása (opcionális)](#ADSL_bridging_be.C3.A1ll.C3.ADt.C3.A1sa_.28opcion.C3.A1lis.29)
            *   [1.1.1.2 Vezeték nélküli hálózati beállítások (opcionális)](#Vezet.C3.A9k_n.C3.A9lk.C3.BCli_h.C3.A1l.C3.B3zati_be.C3.A1ll.C3.ADt.C3.A1sok_.28opcion.C3.A1lis.29)
    *   [1.2 Szövegszerkesztő kiválasztása](#Sz.C3.B6vegszerkeszt.C5.91_kiv.C3.A1laszt.C3.A1sa)
    *   [1.3 Óra beállítása](#.C3.93ra_be.C3.A1ll.C3.ADt.C3.A1sa)
        *   [1.3.1 Régió és időzóna kiválasztása](#R.C3.A9gi.C3.B3_.C3.A9s_id.C5.91z.C3.B3na_kiv.C3.A1laszt.C3.A1sa)
        *   [1.3.2 Dátum és idő beállítása](#D.C3.A1tum_.C3.A9s_id.C5.91_be.C3.A1ll.C3.ADt.C3.A1sa)
            *   [1.3.2.1 Idő beállítása Windows dual boothoz.](#Id.C5.91_be.C3.A1ll.C3.ADt.C3.A1sa_Windows_dual_boothoz.)
    *   [1.4 A merevlemez előkészítése](#A_merevlemez_el.C5.91k.C3.A9sz.C3.ADt.C3.A9se)
        *   [1.4.1 Merevlemezek partícionálása: Általános információk](#Merevlemezek_part.C3.ADcion.C3.A1l.C3.A1sa:_.C3.81ltal.C3.A1nos_inform.C3.A1ci.C3.B3k)
            *   [1.4.1.1 Partíció típusok](#Part.C3.ADci.C3.B3_t.C3.ADpusok)
            *   [1.4.1.2 Lapozó (swap) partíció](#Lapoz.C3.B3_.28swap.29_part.C3.ADci.C3.B3)
            *   [1.4.1.3 Partícionálási séma kiválasztása](#Part.C3.ADcion.C3.A1l.C3.A1si_s.C3.A9ma_kiv.C3.A1laszt.C3.A1sa)
            *   [1.4.1.4 Mekkora méretű partícióim legyenek?](#Mekkora_m.C3.A9ret.C5.B1_part.C3.ADci.C3.B3im_legyenek.3F)
        *   [1.4.2 Fájlrendszerek létrehozása: Általános információk](#F.C3.A1jlrendszerek_l.C3.A9trehoz.C3.A1sa:_.C3.81ltal.C3.A1nos_inform.C3.A1ci.C3.B3k)
            *   [1.4.2.1 Fájlrendszer típusok](#F.C3.A1jlrendszer_t.C3.ADpusok)
            *   [1.4.2.2 Naplózó fájlrendszerek](#Napl.C3.B3z.C3.B3_f.C3.A1jlrendszerek)
        *   [1.4.3 I. opció: Automatikus partícionálás](#I._opci.C3.B3:_Automatikus_part.C3.ADcion.C3.A1l.C3.A1s)
        *   [1.4.4 II. opció: Lemezek manuális partícionálása](#II._opci.C3.B3:_Lemezek_manu.C3.A1lis_part.C3.ADcion.C3.A1l.C3.A1sa)
        *   [1.4.5 III. opció: Partíciók, fájlrendszerek, csatolási pontok konfigurációja](#III._opci.C3.B3:_Part.C3.ADci.C3.B3k.2C_f.C3.A1jlrendszerek.2C_csatol.C3.A1si_pontok_konfigur.C3.A1ci.C3.B3ja)
    *   [1.5 Csomagok kiválasztása](#Csomagok_kiv.C3.A1laszt.C3.A1sa)
        *   [1.5.1 Rendszerbetöltő (bootloader)](#Rendszerbet.C3.B6lt.C5.91_.28bootloader.29)
        *   [1.5.2 Csomag csoportok](#Csomag_csoportok)
    *   [1.6 Csomagok telepítése](#Csomagok_telep.C3.ADt.C3.A9se)
    *   [1.7 A rendszer konfigurációja](#A_rendszer_konfigur.C3.A1ci.C3.B3ja)
        *   [1.7.1 Van-e lehetőség a konfiguráció automatizálására?](#Van-e_lehet.C5.91s.C3.A9g_a_konfigur.C3.A1ci.C3.B3_automatiz.C3.A1l.C3.A1s.C3.A1ra.3F)
        *   [1.7.2 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [1.7.2.1 LOCALIZATION szekció](#LOCALIZATION_szekci.C3.B3)
            *   [1.7.2.2 HARDWARE szekció](#HARDWARE_szekci.C3.B3)
            *   [1.7.2.3 NETWORKING szekció](#NETWORKING_szekci.C3.B3)
            *   [1.7.2.4 DAEMONS szekció](#DAEMONS_szekci.C3.B3)
                *   [1.7.2.4.1 Általános információk](#.C3.81ltal.C3.A1nos_inform.C3.A1ci.C3.B3k)
        *   [1.7.3 /etc/fstab](#.2Fetc.2Ffstab)
        *   [1.7.4 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
        *   [1.7.5 /etc/modprobe.d/modprobe.conf](#.2Fetc.2Fmodprobe.d.2Fmodprobe.conf)
        *   [1.7.6 /etc/resolv.conf](#.2Fetc.2Fresolv.conf)
        *   [1.7.7 /etc/hosts](#.2Fetc.2Fhosts)
        *   [1.7.8 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [1.7.9 /etc/pacman.conf](#.2Fetc.2Fpacman.conf)
        *   [1.7.10 /etc/pacman.d/mirrorlist](#.2Fetc.2Fpacman.d.2Fmirrorlist)
        *   [1.7.11 Root password](#Root_password)
        *   [1.7.12 Done](#Done)
    *   [1.8 Install bootloader](#Install_bootloader)
    *   [1.9 Reboot](#Reboot)

## Telepítés

**Megjegyzés:** Ha az Internetet HTTP és/vagy FTP proxy-n keresztül éred el _és_ DHCP-t használsz a hálózati interfész (felület) konfigurálásához, lehet, hogy be kell állítanod a `http_proxy` és/vagy az `ftp_proxy` környezeti változót a shellben, mielőtt a `/arch/setup`-t futtatnád, az alábbiak szerint:

```
export http_proxy=http://<http_proxy_címe>:<proxy_port>
export ftp_proxy=ftp://<ftp_proxy_címe>:<proxy_port>
```

Rendszergazdaként futtasd az alábbi telepítő szkriptet az első virtuális konzolból (tty1, `Alt+F1`):

 `# /arch/setup` 

Ezután az ún. Arch Linux Installation Framework képernyőjét kell(ene) látnod.

### Telepítési forrás kiválasztása

Az üdvözlőképernyő után meg kell adnod a telepítési forrást.

A "_Select Source_" (forrás kiválasztása) párbeszédablak megkér, hogy válaszd ki azokat a [csomagtárolókat](/index.php/Official_repositories "Official repositories"), amelyeket engedélyezni szeretnél.

	Core

	Ha a Core telepítőlemezt használod és a csomagokat erről a CD-ről szeretnéd telepíteni, akkor válaszd a **core-local** lehetőséget. Ha a legfrissebb csomagokat szeretnéd letölteni és nem a CD-n lévőket telepíteni, akkor válaszd a **core-remote** lehetőséget, és ha gondolod egyéb tárolókat is kiválaszthatsz.

**Figyelem:** Több **remote** csomagtárolót is kiválaszthatsz, de vedd figyelembe a telepítő üzenetét: "NE HASZNÁLD egyszerre a helyi csomagtárolót a távolival, csak akkor ha tudod mit csinálsz. (Csomagproblémákat okozhat!)"

	Netinstall

	Ha a netinstall telepítőlemezt használod, akkor csak a **remote** csomagtárolók közül választhatsz.

Ha nem tudod melyik tárolót válaszd, akkor válaszd a **core-remote**, **extra-remote** és **community-remote** tárolókat. 64-bit-es Arch installálása esetén talán szükséged lehet a '[multilib](/index.php/Multilib "Multilib")' tárolóra. Viszont ezekre a beállításokra a telepítés folyamán később kerül sor.

**Figyelem:** A **testing** csomagtároló választása esetén folyamatosan figyelemmel kell kísérned a [arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public) levelezőlistát, ugyanis ebben a tárolóban a tesztelés alatt álló csomagok vannak. Ezzel együtt tisztában kell lenned, hogyan kell a [csomagok régebbi verzióját visszaállítani](/index.php/Downgrade_packages "Downgrade packages") és [chroot-olni](/index.php/Chroot "Chroot") az Arch rendszeredbe, hogy kijavítsd az esetleges rendszerhibákat. Tehát a testing-et is csak akkor használd, ha tudod mit csinálsz.

#### Hálózat beállítása

**Megjegyzés:** Az ftp.archlinux.org sebessége 50KB/s -ra van korlátozva.

Egy megadott listából viszont választhatsz további FTP és/vagy HTTP tükörszerverek közül.

**Tip:** A legjobb kapcsolat és letöltési sebesség elérése érdekében ajánlott a tartózkodási helyedhez legközelebb lévő tükörszerverek közül választani, amelyek magas megbízhatóságú kiszolgálással rendelkeznek (pl. egyetemek). A tükörszerverek relatív sebességét és frissítési állapotát megtekintheted [itt](https://www.archlinux.org/mirrors/status/).

Ha a **core-local** és a **remote** (távoli) csomagtárolókat választottad, akkor most dönthetsz arról is, hogy csak azok a csomagok legyenek letöltve a távoli szerverről, amelyek helyileg nem elérhetőek, illetve legyen minden csomag letöltve.

A következő képernyőn a hálózati beállítás elkezdéséhez válaszd a _"Yes"_-t. Lehet, hogy kapsz egy kiírást arról, hogy az ethernet drivert manuálisan kell betöltened. Az UDev egy hasznos eszköz a megfelelő modulok betöltésére, és nagy valószínűséggel már automatikusan betöltötte neked. A működést leellenőrizheted az `Alt+F3` megnyomása után az `ip addr` parancsot beütve. Ez után visszaléphetsz a tty1-re az `Alt+F1` megnyomásával.

Meg fognak jelenni az elérhető hálózati interfészek. Ha egy interfész és a hozzá tartozó HWaddr (**H**ard**W**are **addr**ess) (fizikai cím) látható, akkor a hálózati modul már sikeresen be lett töltve. Ha nem látszik a listában a hálózati interfészed, akkor megpróbálhatod a telepítővel megkerestetni, vagy manuálisan be kell töltened egy másik virtuális konzolon. A folytatáshoz válaszd ki a hálózati eszközt.

A telepítő ez után meg fogja kérdezni, hogy akarod-e DHCP-vel konfigurálni a hálózati eszközödet. _"Yes"_ válasz esetén lefut a `dhcpcd` program, amely elvégzi az automatikus címkiosztást számodra. _"No"_ válasz esetén manuálisan kell beállítanod a statikus IP címet _(IP address)_, maszkot _(netmask)_, szórási címet (_broadcast_, opcionális), alapértelmezett átjárót _(gateway)_, DNS szervert, HTTP proxyt (opcionális), FTP proxyt (opcionális).

Ez után visszakerülsz a főmenübe _(Main Menu)_.

##### ADSL bridging beállítása (opcionális)

(Ha modemmel vagy routerrel bridge módban csatlakozol az internet szolgáltatóhoz)

Válts át egy másik virtuális konzolra (`Alt+F2`), jelentkezz be root-ként és írd be a következőt:

 `# pppoe-setup` 

Ha mindent sikeresen konfiguráltál, csatlakozz a szolgáltatóhoz:

 `# pppoe-start` 

Térj vissza az első virtuális konzolba (`Alt+F1`) hogy folytasd a telepítést az alapértelmezett [szövegszerkesztő kiválasztásával](#Sz.C3.B6vegszerkeszt.C5.91_kiv.C3.A1laszt.C3.A1sa).

##### Vezeték nélküli hálózati beállítások (opcionális)

(Ha a telepítés alatt vezeték nélküli hálózatra van szükséged.)

A vezeték nélküli driverek és segédprogram elérhetőek a telepítőlemezről. A vezeték nélküli interfész pontos adatainak meghatározása kulcsfontosságú lehet az eszköz sikeres beállításához. Fontos itt megjegyezni, hogy a következő leírás vezeték nélküli beállításai csak a telepítési időszakra (átmenetileg) érvényesek. A telepítés végeztével, **a frissen installált rendszeren, újból el kell végezni a beállításokat** ha vezeték nélküli eszközt akarunk használni.

A következő beállítások a telepítés ezen szakaszában opcionálisak, és akkor kell elvégezni ha csak vezeték nélküli eszközzel tudunk csatlakozni az internetre.

**Megjegyzés:** A következő példákban az interfész neve `wlan0` míg a hozzá tartozó ESSID: `linksys`. Ne felejtsd el ezeket az jelöléseket a te beállításaidnak megfelelően megváltoztatni!

Az alaplépések a következőképpen néznek ki:

*   Válts át egy szabad virtuális konzolra, például: `Alt+F3`
*   Jelentkezz be root-ként
*   (Opcionális) A vezeték nélküli interfész azonosítása:

 `# lspci | grep -i net` 

vagy, USB eszköz esetén:

 `# lsusb ` 

*   Győződj meg arról, hogy az UDev betöltötte-e a drivert, és hogy létrejött-e használható vezeték nélküli kernel interfész: `/usr/sbin/iwconfig` :

 `# iwconfig` 

```
 lo no wireless extensions.
 eth0 no wireless extensions.
 wlan0    unassociated  ESSID:""
          Mode:Managed  Channel=0  Access Point: Not-Associated
          Bit Rate:0 kb/s   Tx-Power=20 dBm   Sensitivity=8/0
          Retry limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

Az elérhető vezeték nélküli eszköz ebben a példában a `wlan0`.

**Megjegyzés:** Ha nem valami hasonlót látsz magadnál, mint itt a fenti példában, akkor a vezeték nélküli driver nem töltődött be. Ebben az esetben manuálisan kell betöltened a megfelelő drivert. Az ezzel kapcsolatos részletes leírást a [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")-ban találhatod.

*   Helyezd aktív állapotba az interfészt:

 `# ip link set wlan0 up` 

A wireless chipset-ek egy bizonyos százalékának a driveren kívül még firmware-re is szüksége van. Ha egy wireless chipset-nek firmware-re is szüksége van, akkor jelen esetben a következő hibaüzenetet fogod kapni:

 `# ip link set wlan0 up`  `SIOCSIFFLAGS: No such file or directory` 

A hiba megtekintéséhez írd be: `/usr/bin/dmesg`. Ez a kernelnaplót fogja kiadni, amiben megtalálható a hibaüzenet arról, hogy a wireless chip firmware kérelmet nyújtott a kernel felé. Példa egy Intel chipset-ről amely firmware kérelmet nyújtott be a kernel felé a rendszer betöltése alatt:

 `$ dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Ha nem látható ilyen üzenet, akkor a chipsetnek nincs szüksége firmware-re.

**Megjegyzés:** A wireless cipset firmware csomagok (azon eszközök számára, amelyek igénylik) megtalálhatóak a telepítőlemez (CD vagy USB) `/lib/firmware` könyvtárában, **de ahhoz, hogy az installált rendszeren is működjön külön fel kell telepítened majd a rendszerre újraindítás után a megfelelő firmware-t!** A csomagok kiválasztására és telepítésére az útmutató egy későbbi pontjában térünk ki. Ne felejtsd majd el mind a megfelelő drivert és firmware-t kiválasztani a telepítés azon pontján, ahol a szükséges csomagokat telepítjük. Részletes leírást a [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")-ban találsz arról, hogyan kell a megfelelő firmware-t kiválasztani. A nem megfelelő firmware kiválasztása nagyon gyakori hibaként szokott előfordulni.

*   Ha az ESSID-t elfelejtetted, vagy ismeretlen akkor használd a `iwlist <interface> scan` parancsot az elérhető hálózatok megjelenítéséhez. Példa:

 `# iwlist wlan0 scan` 

```
Cell 01 - Address: 04:25:10:6B:7F:9D
                    Channel:2
                    Frequency:2.417 GHz (Channel 2)
                    Quality=31/70  Signal level=-79 dBm  
                    Encryption key:off
                    ESSID:"dlink"
                    Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s
                    Bit Rates:6 Mb/s; 9 Mb/s; 12 Mb/s; 18 Mb/s; 24 Mb/s
                              36 Mb/s; 48 Mb/s; 54 Mb/s

```

*   WPA titkosítás használata esetén:

A WPA titkosításhoz szükség van a kulcs titkosításához és ennek egy fájlban való tárolásához az ESSID-vel együtt. Ezt használjuk később a kapcsolat létrehozásához a `wpa_supplicant` segítségével. Ehhez néhány plusz lépés szükséges:

Az egyszerűség és a biztonsági mentés érdekében nevezzük át az alapértelmezett `wpa_supplicant.conf` fájlt:

 `# mv /etc/wpa_supplicant.conf /etc/wpa_supplicant.conf.original` 

A `wpa_passphrase` segítségével hozhatjuk létre a hálózat nevét és a WPA kulcsot titkosító konfigurációt, amelyet beírhatunk a `/etc/wpa_supplicant.conf` -ba.

A következő példa titkosítja a "linksys" hálózat "my_secret_passkey" kulcsát, létrehoz egy új konfigurációs fájlt (`/etc/wpa_supplicant.conf`), amibe beleírja a létrehozott titkosított adatokat :

 `# wpa_passphrase linksys "my_secret_passkey" > /etc/wpa_supplicant.conf` 
**Megjegyzés:** Ha a fenti parancs a következő hibába ütközik: `bash: event not found`, az valószínűleg azért lehet, mert speciális karaktert (pl.`!`) használsz a hálózati névben. Ebben az esetben próbáld a következőt: `# sh -c 'wpa_passphrase linksys "my_secret_passkey" > /etc/wpa_supplicant.conf'` 

További információkért és hibakeresésért nézd meg a [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") leírását.

**Megjegyzés:** A `/etc/wpa_supplicant.conf` formátuma egyszerű szövegfájl. Installáláskor ez még nem kockázati tényező, viszont a telepítés végeztével, miután bejelentkezel a rendszerbe és újrakonfigurálod a WPA-t, ne felejtsd el a `/etc/wpa_supplicant.conf` fájl jogosultságait megváltoztatni (pl. `chmod 0600 /etc/wpa_supplicant.conf`, azért, hogy csak root-ként lehessen olvasni.

*   Csatlakozz a wireless eszközöddel a kívánt hozzáférési ponthoz! A titkosítástól függően (nincs, WEP, vagy WPA), a cstlakozási folyamat eltérő lehet. Szükséged lesz a csatlakozni kívánt hozzáférési pont nevére (ESSID).

| Titkosítás | Parancs |
| Nincs | `iwconfig wlan0 essid "linksys"` |
| WEP Hexa Kulccsal | `iwconfig wlan0 essid "linksys" key "0241baf34c"` |
| WEP ASCII jelszóval (passphrase) | `iwconfig wlan0 essid "linksys" key "s:pass1"` |
| WPA | `wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant.conf` |

**Megjegyzés:** A hálózati kapcsolódást később automatizálni lehet az Arch alapértelmezett hálózati démonjaival [netcfg](/index.php/Netcfg "Netcfg"), [wicd](/index.php/Wicd "Wicd"), vagy bármely más általad választott hálózati beállító programmal.

**Megjegyzés:** Ha live CD-ről bootoltad a rendszert és chroot-oltál a már korábban feltelepített rendszeredbe, akkor elindíthatod a hálózati menedzsert a következő parancsokkal `/etc/rc.d/dbus start` és `/etc/rc.d/networkmanager start`. Kilistázhatod az elérhető hálózatokat: `nmcli con list` és kiválaszthatsz egyet a csatlakozásra: `nmcli con up id NAME`, ahol a NAME a csatlakozás nevét takarja.

*   Miután kiadtad a fentebb leírt szükséges parancsokat a csatlakozáshoz, várj pár pillanatot a kapcsolat létrejöttéhez és győződj meg róla, hogy sikeresen kapcsolódtál a hozzáférési ponthoz:

 `# iwconfig wlan0` 

A kimenet meg kell jelenjen, hogy sikeresen csatlakoztál a kívánt hálózathoz.

*   Állíts be az eszközöd címét automatikus hálózati címkiosztást alkalmazva `/sbin/dhcpcd <interface>`, például.:

 `# dhcpcd wlan0` 

*   Végül próbáld ki, hogy működik-e a kapcsolat: `/bin/ping`:

 `# ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=49 time=87.7 ms
64 bytes from 74.125.224.146: icmp_req=2 ttl=49 time=87.0 ms
64 bytes from 74.125.224.146: icmp_req=3 ttl=49 time=94.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 87.052/89.812/94.634/3.430 ms

```

Remélhetőleg most már rendelkezel egy működőképes hálózati kapcsolattal. Hibakereséshez fordulj a részletes információkat tartalmazó [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")-hoz!

Térj vissza a tty1-re az (`Alt+F1`) billentyűkombinációval, majd folytasd a [szövegszerkesztő kiválasztásával](#Sz.C3.B6vegszerkeszt.C5.91_kiv.C3.A1laszt.C3.A1sa).

### Szövegszerkesztő kiválasztása

A következő lépésben kiválaszthatod, melyik alapértelmezett szövegszerkesztőt szeretnéd használni a konfigurációs fájlok szerkesztéséhez. A `nano` vagy a `vi` nevű programok közül választhatsz. A "nano" kezdők számára egyszerűbb mert a kezelése és a benne alapvetően elvégezhető feladatok megegyeznek a grafikus szövegszerkesztő programokkal. A nyílbillentyűk, a backspace, a törlés gomb az elvárt funkcióknak megfelelően működnek. A leggyakrabban használt szövegszerkesztési funkciók a program alján egy kis menüben láthatóak. Pl. kivágás: `Ctrl-k`, beillesztés: `Ctrl-u`, mentés: `Ctrl-o`, kilépés: `Ctrl-x`. A programok részletesebb leírásáért tekintsd meg a [nano](/index.php/Nano "Nano") illetve [Vi](/index.php/Vi "Vi") wiki oldalakat!

### Óra beállítása

#### Régió és időzóna kiválasztása

A nyílgombok segítségével válaszd ki a régiód és időzónád, vagy gyors ugráshoz nyomd le a régió nevének kezdőbetűjét, majd nyomd meg az "Enter"-t a kiválasztáshoz.

#### Dátum és idő beállítása

Válaszd a "hardware clock mode"-ot! Ha ez nem egyezik a többi operációs rendszered beállításával, akkor felül fogják írni az időt és így az időeltolódási korrekciók se lesznek jól kalibrálva.

*   [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") (ajánlott)

**Megjegyzés:** Az UTC használata a hardver órához nem jelenti azt, hogy az idő a szoftverben is UTC-ben fog megjelenni.

*   **localtime** (nem ajánlott) - A Windows alapértelmezett beállítása. Ha az idő "localtime"-ra van állítva, akkor a Linux nem fogja elvégezni a téli-nyári időszámítás szerinti automatikus óraátállítást.

**Figyelem:** A _localtime_ használata számos ismert hibához vezethet, és sajnos tervben sincs, hogy ezen hibák javításra kerüljenek.

**Megjegyzés:** Minden egyéb érték a hardver órát érintetlenül hagyja.(Virtualizációhoz hasznos lehet).

##### Idő beállítása Windows dual boothoz.

Ha az Arch Linux-ot Windows rendszerrel együtt szeretnéd használni, két lehetőséged van:

*   Ajánlott: Állíts be UTC-t Arch Linuxban és Windows-ban is. (ehhez Windows-ban egy gyors registry változtatás szükséges. A részletekért nézd meg [ezt az oldalt](https://help.ubuntu.com/community/UbuntuTime#Make_Windows_use_UTC)). Ezek mellett kapcsold ki Windows-ban az idő automatikus internetes szinkronizációját, mert ez a hardver órát "localtime"-ra változtatja. Ha internetes időszinkronizációt szeretnél használni, akkor használd inkább az [ntpd](/index.php/Ntpd "Ntpd")-t az Arch Linux rendszereden.

*   Nem ajánlott: Állítsd az Arch Linux-ot _localtime_ -ra és később a [rendszer beállításánál](#Rendszer_be.C3.A1ll.C3.ADt.C3.A1sa) töröld a `hwclock`-ot a `/etc/rc.conf`-ban található `DAEMONS` sorból. (Windows will take care of hardware clock corrections).

### A merevlemez előkészítése

**Figyelem:** A merevlemezek partícionálása adatvesztéshez vezethetnek. Erősen ajánlott a partícionálás előtti biztonsági másolat készítése a lemezen található összes szükséges fájlról.

**Megjegyzés:** A partícionálás az Arch Linux installálása előtt is elvégezhető bármely partícionáló programmal, például a [GParted](http://gparted.sourceforge.net/download.php)-del. Ha a lemez már előre meg lett partícionálva akkor ugorhatsz a következő részhez: [#III. opció: Partíciók, fájlrendszerek, csatolási pontok konfigurációja](#III._opci.C3.B3:_Part.C3.ADci.C3.B3k.2C_f.C3.A1jlrendszerek.2C_csatol.C3.A1si_pontok_konfigur.C3.A1ci.C3.B3ja).

Nézd meg a lemez jelenlegi partícióinak azonosítóját és elhelyezkedésüket az `/sbin/fdisk` `-l` (kicsi L) parancs kiadásával!

Nyiss meg egy másik virtuális konzolt (`Alt+F3`) és írd be:

 `# fdisk -l` 

Jegyezd le a lemez(ek) és/vagy partíció(k) nevét, amire az Arch-ot telepíteni akarod.

Térj vissza a telepítési segédprogramhoz: `Alt+F1`.

Válaszd ki a "Prepare Hard Drive" menüt. Itt négy opció fog megjelenni:

*   **I. opció**: [Auto-Prepare](#I._opci.C3.B3:_Automatikus_part.C3.ADcion.C3.A1l.C3.A1s)

Ez törölni fogja a TELJES lemezt, és automatikusan beállítja a partíciókat. Néhány beállítás testre szabható.

*   **II. opció**: [Manually Partition Hard Drives](#II._opci.C3.B3:_Lemezek_manu.C3.A1lis_part.C3.ADcion.C3.A1l.C3.A1sa)

Ajánlott. Ez az opció a "cfdisk" nevű segédprogramot használja, amellyel elvégezhetjük az igényeinknek megfelelő partícionálást és testreszabást. Miután ezzel megvagyunk, továbbléphetünk a 3\. opcióra.

*   **III. opció**: [Manually configure block devices, filesystems and mountpoints](#III._opci.C3.B3:_Part.C3.ADci.C3.B3k.2C_f.C3.A1jlrendszerek.2C_csatol.C3.A1si_pontok_konfigur.C3.A1ci.C3.B3ja)

Közvetlenül is ugorhatunk ehhez a részhez, ha már előre partícionáltuk a lemezünket. A 3\. opció egyben a lemez előkészítésének következő lépése a 2\. opció után. A rendszer megmutatja milyen fájlrendszerek és csatolási pontok érhetők el a lemezen, és megkérdezi, hogy akarod-e használni őket. Lehetőséged nyílik annak kiválasztására, hogy az egyes partícióknak milyen azonosítási módszerét szeretnéd használni. Például dev, label, vagy uuid.

*   **IV. opció**: Rollback last filesystem changes

Fájlrendszer változtatások visszaállítása a változtatások előtti értékekre.

Az I. II. és III. opciót az alábbiakban részletesen tárgyaljuk. Az opciókban történő beállítások könnyebb megértése érdekében előbb magyarázatra kerülnek a Linux partíciókkal és fájlrendszerekkel kapcsolatos tudnivalók. Azon haladó GNU/Linux felhasználók, akik ismerik a Linux fájlrendszereket és otthonosan mozognak a manuális partícionálás terén, ők ugorhatnak a [csomagok kiválasztása](#Csomagok_kiv.C3.A1laszt.C3.A1sa) részhez.

**Megjegyzés:** Ha egy USB-s Pen Drive-ra szeretnéd telepíteni a rendszert, nézd meg az [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key") leírást!

#### Merevlemezek partícionálása: Általános információk

##### Partíció típusok

A merevlemez partícionálása azt jelenti, hogy a lemezen egymástól elkülönülő tároló helyeket hozunk létre. Ezeket a helyeket partícióknak hívjuk. Minden partíció egy külön lemezként fogható fel, és formázásuktól függően különböző típusúak lehetnek. (lásd lentebb)

3 partíciótípust különböztetünk meg:

*   Primary (elsődleges)
*   Extended (kiterjesztett)
    *   Logical (logikai)

A **Primary (elsődleges)** partíciók bootolhatóak, és egy lemezen vagy RAID köteten összesen 4 lehet belőlük. Ha a partícionálási séma szerint több partícióra van szükségünk, akkor egy **extended (kiterjesztett)** partíciót tartalmazó **logical (logikai)** partíciót kell létrehoznunk. A kiterjesztett partíciót a logikai partíciók hordozójaként képzelhetjük el. Egy merevlemez nem tartalmazhat egynél több kiterjesztett partíciót. A kiterjesztett partíció elsődlegesként számít abból a szempontból, hogy hány darab elsődleges partíció lehet a lemezen. Tehát ha van egy kiterjesztett partíciónk, akkor mellette már csak maximum 3 elsődleges partíció hozható létre. A kiterjesztett partíción belüli logikai partíciók száma viszont nincs limitálva. Egy dual-boot rendszeren, ahol az egyik a Windows, ott a Windows-nak elsődleges partíción kell elhelyezkednie.

A partíciók számozása úgy történik, hogy a létrehozott elsődleges partíciók `sda1` és `sda3` számozását követi a kiterjesztett partíció `sda4`. A kiterjesztett partíción `sda4` megtalálható logikai partíciók számozása pedig `sda5`, `sda6`, stb.

##### Lapozó (swap) partíció

A swap partíció a merevlemezen létrehozott virtuális memória szerepét tölti be. A virtuális memória lehetőséget ad a kernel számára, hogy a merevlemez egy bizonyos részét használja, abban az esetben ha a fizikai memória betelt.

A swap partíció méretére a régi fő szabály az volt, hogy legyen legalább a kétszerese a fizikai memóriának. Manapság, ahogy a személyi számítógépek egyre nagyobb memóriákat tartalmaznak, ez a szabály már elavultnak tekinthető. 512MB vagy kevesebb memóriát tartalmazó számítógépeknél viszont ajánlott betartani. Ha elegendő memória áll rendelkezésre (több mint 1024MB), akkor kisebb swap partíció is elegendő, vagy akár meg is lehet szüntetni. 2GB RAM felett már teljesen elfogadható sebességen működhet a rendszerünk swap partíció nélkül is. A lehetőség adott egy [swap fájl létrehozására](/index.php/HOW_TO:_Create_swap_file "HOW TO: Create swap file") bármikor a rendszer telepítése után is.

**Megjegyzés:** Ha a "hibernálás" lehetőséget használni szeretnénk a számítógépen, akkor a swap partíció szükséges mérete legyen **legalább** akkora mint a fizikai memória mérete. Néhány Arch felhasználó viszont azt ajánlja, hogy érdemes ennél a méretnél körülbelül 10-15%-kal nagyobbat választani, a rossz szektorokból adódó hibák elkerülése végett.

##### Partícionálási séma kiválasztása

Nem vonatkoznak szigorú szabályok a merevlemez partícionálására, de aki úgy gondolja az követheti az alább leírt általános útmutatót. A partícionálási sémát több szempont alapján szokták megválasztani, úgy mint rugalmasság, sebesség, biztonság, valamint a lemez limitált méretéből adódó megfontolások. Tehát lényegében a személyes döntéstől függ. Két egyszerű lehetőség kínálkozik: **a.)** egy partíció a gyökérfájlrendszernek és egy másik a swap-nek vagy **b.)** egyetlen gyökér partíció swap nélkül. Olvasd át az alábbi példákkal kiegészített leírást, annak érdekében, hogy megértsd az egyes partícionálási sémák előnyeit és hátrányait. Ha dual-boot-os rendszert szeretnél, amin egyszerre akarod használni az Arch Linuxot és a Windows is, olvasd el a [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot") cikket!

A következő csatolási pontokat lehetőség van különböző partíciókon használni:

	`/` (root)

	A root (gyökér) könyvtár a hierarchia csúcsán helyezkedik el. Ezen a ponton van csatolva az elsődleges fájlrendszer és ebből származik az összes többi fájlrendszer. Minden fájl és könyvtár megjelenik a gyökérkönyvtár _`/`_ alatt, még akkor is ha különböző fizikai lemezen helyezkednek el. A gyökér fájlrendszer tartalmának megfelelőnek kell lennie bootra, helyreállításra, helyrehozásra, és/vagy a rendszer kijavítására. Ezen oknál fogva bizonyos könyvtárak a _`/`_ alatt nem helyezhetőek el külön partíción. Nézd meg a [figyelmeztetést lejjebb](#root-figyelmeztetes).
**Megjegyzés:** A `/usr` külön partícióként való használata alapértelmezésként nem támogatott [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1006924#p1006924). Ha minden áron külön partíción szeretnéd elhelyezni, akkor olvasd el a [mkinitcpio#/usr as a separate partition](/index.php/Mkinitcpio#.2Fusr_as_a_separate_partition "Mkinitcpio") cikket.

	`/boot`

	Ez a könyvtár tartalmazza a kernelt, a ramdisk képfájlokat, a boot betöltő program konfigurációs fájlját és boot betöltő szakaszait. Olyan adatokat is tárol, amelyek a kernel felhasználói szintű programjainak elindítása előtt használatosak. Ezek között szerepelhetnek az elmentett master boot szektorok és szektor térkép fájljai. Ez a könyvtár és a tartalma létfontosságú a bootoláshoz, valamint egyedi is hiszen akár egy számára létrehozott különálló partíción is elhelyezhető.
**Figyelem:** A `/boot` könyvtáron kívül az összes többi alapvetően szükséges könyvtárnak a **`/`** partíción **kell** elhelyezkednie. Ezek a könyvtárak a `/bin`, `/etc`, `/lib`, `/sbin` és a `/usr` [[2]](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken).

	`/home`

	Minden egyes felhasználó saját könyvtára és azok alkönyvtárai találhatóak meg itt: felhasználói adatfájlok, képek, dokumentumok, személyes dolgok és a felhasználó által futtatott programokhoz tartozó egyéni konfigurációs fájlok.

	`/tmp`

	Könyvtár azon programok számára, amelyek futásuk során átmeneti fájlokat hoznak létre, úgy mint a _`.lck`_ , ami arra használandó, hogy megakadályozza hogy egy bizonyos program egy fájlból több átmeneti példányt hozzon létre egy bizonyos feladat elvégzése előtt. A feladat elvégeztével a _`.lck`_ fájl automatikusan eltávolításra kerül. A programok nem várják el, hogy bármilyen fájlnak vagy könyvtárnak szükségszerűen a _`/tmp`_ -ben kell elhelyezkednie. A _`/tmp`_ -ben megtalálható fájlok és könyvtárak a rendszerindításkor mindig törlődnek.

	`/var`

	Különféle változó fájlokat, könyvtárakat, adminisztrációs és napló fájlokat, a [pacman](/index.php/Pacman "Pacman")-nel letöltött csomagokat, az [ABS](/index.php/Arch_Build_System "Arch Build System") által létrehozott fastruktúrát és egyéb változó fájlokat tartalmaz. Lehetőség van a _`/usr`_ csak olvashatóként történő csatolására. Minden ami korábban a _`/usr`_ -be íródott a rendszer működése alatt (a telepítéssel és szoftver karbantartással ellentétben) a _`/var`_-ban kell elhelyezkednie.

**Megjegyzés:** A `/var` sok kis fájlt tartalmaz. A fájlrendszer típus megválasztásakor gondoljuk át, hogy biztos szükségünk van-e számára különálló partícióra.

Az egyetlen partíción való elhelyezés mellett több előnye is vannak annak, ha különböző partíciókra rakjuk az egyes fájlrendszereket:

*   Biztonság: Minden fájlrendszer tulajdonságai konfigurálhatóak az `/etc/fstab` fájlban úgy mint 'nosuid', 'nodev', 'noexec', 'readonly', stb.
*   Stabilitás: Egy felhasználó, vagy egy meghibásodott program írási jog birtokában teljes mértékben megtöltheti hasztalan fájlokkal a partíciót. Viszont a rendszer működése szempontjából szükséges kritikus fájlrendszerek érintetlenül maradnak.
*   Gyorsaság: Azon a fájlrendszerben, ahol sok törlés, felülírás történik, könnyebben töredezetté válhat. A különálló fájlrendszerekre ez nincs hatással, és egyenként lehet töredezettség-mentesíteni őket. A töredezettség elkerülhető, ha odafigyelünk arra, hogy az egyes fájlrendszerek soha ne kerüljönek a partíciót teljesen megtöltő állapotba.
*   Integritás: Ha egy fájlrendszerrel valami probléma történik, attól még a többire ez nem lesz hatással.
*   Rugalmasság: Különböző operációs rendszerek közötti fájlmegosztás esetén célszerű független fájlrendszert használni. Különböző fájlrendszerek alkalmazására az adatok bizonyos típusú használata esetén is szükség lehet.

##### Mekkora méretű partícióim legyenek?

A partíciók méretét mindenki egyéni ízlés szerint megválaszthatja, viszont van pár tipp és hasznos információ ezzel kapcsolatban:

	`/boot` — 100 MB 

	A `/boot` partíciónak körülbelül csak 100 MB-ra van szüksége.

	`/` — 15-20 GB 

	A gyökér fájlrendszernek (`/`) tartalmaznia **kell** a `/usr` könyvtárat, ami igen csak nagyra tud növekedni, attól függően, hogy mennyi programot telepítünk később a rendszerre. A legtöbb felhasználónak 15-20 GB elegendő modern merevlemezeket használva.

	`/var` — 8-12 GB 

	A `/var` fájlrendszer más adatok mellett tartalmazni fogja az [ABS](/index.php/Arch_Build_System "Arch Build System") fastruktúráját és a [pacman](/index.php/Pacman "Pacman")-nel letöltött csomagokat. A letöltött csomagokból ajánlott mindig megtartani a legutóbbi működőképes verziót, arra az esetre ha egy új verziójú csomag hibát okozna, vissza tudjuk telepíteni a legutóbbi működőképes változatot. Ennek következtében a letöltött programok mennyiségétől függően a `/var` mérete nagyobbra is növekedhet, ahogy egyre több csomaggal frissítjük rendszerünket. Azonban biztonsággal törölhetjük az összes csomagot, ha nincs már elég helyünk a lemezen. Ha SSD-t használsz, akkor a `/var` könyvtárat tárolhatod egy HDD-n is, a `/` és `/home` partíciók pedig lehetnek az SSD-n, megakadályozva ezzel az SSD-ről történő szükségtelen írás/olvasásokat. 8-12GB-nak egy személyi számítógépen elegendőnek kell lennie a `/var` számára, attól függően, hogy mennyi szoftver lesz telepítve. A szervereknek ennél viszonylag nagyobb méretű `/var` fájlrendszerre van szükségük.

	`/home` — [nagyon nagy] 

	A `/home` könyvtár az, ahol a személyes adatok, multimédia fájlok, letöltések tárolódnak. Egy otthoni számítógépen a `/home` könyvtár tipikusan a legnagyobb méretű a lemezen. Ha szükségszerűvé válik az Arch újratelepítése, akkor a külön partíción lévő `/home` tartalma nem fog elveszni, és telepítés után újra használható lesz.

**Megjegyzés:** Ha van rá lehetőség, akkor ajánlott minden fájlrendszerre +25% szabad helyet rászámolni, azért, hogy tartalékot képezzünk a rendszer bővítése számára, valamint megakadályozzuk a partíció töredezetté válását.

#### Fájlrendszerek létrehozása: Általános információk

##### Fájlrendszer típusok

Az egyes partíciókon több különböző fájlrendszer közül választhatunk. Mindegyiknek megvan a maga előnye, hátránya, és egyéni sajátossága. A következőkben néhány támogatott fájlrendszer rövid ismertetője olvasható. A mellettük lévő linkek a wikipédián megtalálható részletesebb leírásokra mutatnak.

1.  Az [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") **Second Extended Filesystem** (második kiterjesztett fájlrendszer) egy erős alapokon álló kiforrott, nagyon stabil GNU/Linux fájlrendszer. A hátránya viszont, hogy nem rendelkezik naplózó (journaling) támogatással (lásd lejjebb) és a fájlrendszer korlátozás kezelésével. A naplózás hiánya viszont rendszerösszeomlás vagy áramkimaradás esetén adatvesztéshez vezethet. Továbbá kényelmetlen lehet a használata root (`/`) és `/home` partíciókként hiszen a fájlrendszer ellenőrzések hosszú ideig is eltarthatnak. Az ext2 fájlrendszert lehetőség van átkonvertálni ext3-mas fájlrendszerré.
2.  Az [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") **Third Extended Filesystem** (harmadik kiterjesztett fájlrendszer) lényegében egy ext2 fájlrendszer kiegészítve a naplózás és a fájlrendszer korlátok írásának képességével. Visszafelé kompatiblis az ext2-vel, jól tesztelt és nagyon stabil.
3.  Az [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") **Fourth Extended Filesystem** (negyedik kiterjeszett partíció) egy még újabb fájlrendszer, ami szintúgy visszafelé kompatiblis az ext2 és ext3-mal. Támogatást nyújt nagyobb kötetek kezelésére egészen 1 EXAbájt méretig (1,048,576 Terabájt), valamint 16 Terabájtos fájlméretig. Az ext3-nál élő 32,000 alkönyvtár limitet megnöveli 64,000-re. Ezek mellett támogatja az online töredezettség-mentesítést, azaz nem muszáj a fájlrendszert lecsatolni töredezettség-mentesítsés alatt.
4.  A [JFS](https://en.wikipedia.org/wiki/JFS_(file_system) "wikipedia:JFS (file system)") **Journaled File System** (naplózó fájlrendszer) az IBM által fejlesztett legelső fájlrendszer, amely képes volt a naplózásra. Több éves IBM AIX® operációs rendszeren való tesztelés/fejlesztés előzte meg a GNU/Linux-ra történő bevezetést. A JFS a legkevésbé processzor erőforrás igényes bármely GNU/Linux fájlrendszert tekintve. A formázás, csatolások és fájlrendszer ellenőrzések (fsck), nagyon gyorsan elvégezhetőek rajta. A JFS nagyon jó általános teljesítményt nyújt különösen a határidős I/O ütemezéssel kapcsolatban. A ReiserFS és az ext szériákhoz képest a JFS kevésbé támogatott, de egy kiforott és stabil fájlrendszer.
    **Megjegyzés:** A JFS fájlrendszert nem lehet összezsugorítani partíciókezelő programokkal, úgy mint a **gparted** vagy **parted magic**.

5.  Az [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") egy másik korai naplózó fájlrendszer, amit még eredetileg Silicon Graphics fejlesztett az IRIX operációs rendszerre, majd később bevezették a GNU/Linux-ra is. Jó teljesítményt nyújt nagy fájlok és fájlrendszerek esetében, valamint gyorsan formázható és csatolható. Összehasonlító tesztek alapján az állapítható meg, hogy sok kis fájl kezelése esetén lassabban működik. Az XFS is egy kiforott, online töredezettség-mentesítést is támogató fájlrendszer.
    **Megjegyzés:** Az XFS fájlrendszert nem lehet összezsugorítani partíciókezelő programokkal, úgy mint a **gparted** vagy **parted magic**.

6.  A [vfat](https://en.wikipedia.org/wiki/vfat "wikipedia:vfat") **Virtual File Allocation Table**(virtuális fájl elosztási tábla) egy technikailag egyszerű fájlrendszer és virtuálisan minden létező operációs rendszer támogatja. Ennek köszönhetően a szilárdtest memóriakártyák hasznos formátuma lehet, hiszen ezért könnyebbé válik az operációs rendszerek közötti adatmozgatás. A VFAT támogatja a hosszú fájlnevek használatát.
7.  A [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") vagy "Better FS" egy új fájlrendszer, amely hasonló kiváló funkciókat tartalmaz mint a Sun/Oracle által fejlesztett [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS"). Ezek között szerepel a pillanatképek készítése, multi-disk striping és mirroring (szoftveres RAID mdadm nélkül), hibaellenőrzés, növekvő adatmentés, és használat közben elvégzett tömörítés, amely teljesítménynövekedést és helymegtakarítást okoz. 2011 januárjában a Btrfs instabilnak van kinyílvánítva, bár már bele van építve a jelenlegi kernelbe, de még csak kísérleti jelleggel. A Btrfs lesz valószínűleg a jövő GNU/Linux fájlrendszere és jelenleg opcióként lehet választani a gyökérfájlrendszerhez minden főbb disztribúció installálásakor.
    **Figyelem:** A Btrfs még nem tartalmaz stabil fájlrendszer-ellenőrző/javító eszközt. Hiba fellépése esetén a fájlrendszert nem lehet javítani.

8.  A [nilfs2](https://en.wikipedia.org/wiki/nilfs "wikipedia:nilfs") **New Implementation of a Log-structured File System** az NTT által fejlesztett fájlrendszer. Jellemzője, hogy minden adatot felvesz egy log formátumban, ami folyamatosan növekszik és sosem íródik felül. Arra lett tervezve, hogy csökkentse a lemezelérési időket és az adatvesztést, ami rendszerösszeomlás esetén a hagyományos Linux fájlrendszereknél fennállhat.

##### Naplózó fájlrendszerek

Az ext2 kivételével, az összes fentebb látható fájlrendszer [naplózó fájlrendszer](http://hu.wikipedia.org/wiki/Naplózó_fájlrendszer). Naplózás alatt azt értjük, hogy a rendszer a fájlokkal történő módosításokat lejegyzi, mielőtt véghezvinné. Rendszerösszeomlás, vagy áramkimaradás esetén ezeket a fájlrendszereket sokkal hamarabb vissza lehet állítani és kisebb eséllyel lépnek lesznek fájlrendszerhibák. A naplózás a fájlrendszer egy erre kitüntetett pontján történik.

Nem minden naplózási technika megegyező. Csak az ext3 és ext4 működik adat-mód naplózással, amik mind az adatokat, mind a meta-adatokat naplózzák. Az adat-mód naplózás az írási sebesség csökkenésével jár, és alapértelmezésben nincs bekapcsolva. Más fájlrendszerek a rendezett-módú naplózást alkalmazzák, amik csak meta-adatokat tárolnak. Rendszerösszeomlás esetén a naplózásnak köszönhetően minden fájlrendszer egy működőképes állapotba kerül vissza, viszont csak az adat-mód naplózás adja a megfelelő védelmed az adatvesztés és egyéb fájlproblémák ellen. Kompromisszumot kell kötni annak érdekében, hogy az adat-mód naplózás miatt a rendszer teljesítménye lassabb, hiszen két írási operációnak kell megtörténnie egyszerre: először a naplózás, utána a lemezre írás. A fájlrendszer-típus kiválasztásánál megfontolandó, hogy mi a fontosabb: az adatbizonság, vagy a maximális sebesség.

#### I. opció: Automatikus partícionálás

Az automatikus partícionálás alkalmával minden törlődik a lemezről, és a következő négy partíció jön létre:

*   Egy `/boot` partíció ext2-re formázva. Az alapértelmezett mérete 100MB, de meg lehet változtatni.
*   Egy `/swap` partíció alapértelmezetten 256MB-tal (változtatható).
*   Különálló `/` és `/home` partíciók változtatható mérettel és választható fájlrendszerrel. Az elérhető fájlrendszerek: ext2, ext3, ext4, reiserfs, xfs, jfs, vfat, nilfs2 (kísérleti), and btrfs (kísérleti). A `/` és a `/home`-nak azonos fájlrendszer típusa lesz, ha az "Auto Prepare" opciót választjuk.

Az "Auto-Prepare" opció a teljes lemezt formázni fogja, tehát **minden** adatot töröl. Olvasd el alaposan a **warning** részt, amelyet az installer ezen a ponton ír, és győződj meg róla, hogy biztosan azt a lemezd fogod formázni, amelyiket szeretnéd.

Ha nem szeretnéd az "Auto-Prepare" által felkínált alapértelmezett beállítások szerint formázni a lemezed, akkor ezt manuálisan is megteheted. Ez akkor lehet szükséges, ha például dual-boot rendszert szeretnél egy már meglévő Windows partícióval. A manuális partícionálást elvégezheted a II. opció majd ezt követően a III. opció utasításaival, vagy akár egy Live CD-ről is, a GParted program segítségével.

#### II. opció: Lemezek manuális partícionálása

Kiválasztva a kívánt partíciót a [cfdisk](https://en.wikipedia.org/wiki/cfdisk "wikipedia:cfdisk") nevű partícionáló program fog megjelenni. (Ha [SSD](/index.php/SSD "SSD") lemezed van, akkor más programok előnyösebbek lehetnek, például a [gdisk](/index.php/GUID_Partition_Table "GUID Partition Table") vagy a [GNU Parted](http://www.gnu.org/software/parted/manual/html_mono/parted.html)). A partícionálás folyamata egy példán keresztül könnyebben érthetővé válik, ahol négy partíciót hozunk létre egy 160GB-os merevlemezen a root, var, swap és home fájlrendszereknek. A fentebb említett példákat követve a példarendszerünk egy 15GB-os root (`/`), egy 10GB-os `/var`, egy 1GB-os swap, és a maradék lemezterület számára a `/home` partíciót fogja tartalmazni. Hangsúlyozzuk, hogy a megválasztott méretek a személyes igények alapján dőlnek el, és ez a példa csak illusztrációként szerepel.

Válaszd ki a **N**ew -> 'Primary'-t és írd be a kívánt méretét (ebben a példában 15.44GB) a **root** (`/`) fájlrendszernek. A partíció a lemez elejére fog kerülni. Válaszd ki a **T**ype típust és jelöldi ki a `83 Linux` lehetőséget. A létrehozott `/` partíció `sda1`-jelöléssel fog megjelenni.

Hasonló módon hozz létre egy második "primary" partíciót 10.256 GB mérettel a `/var` számára, és válaszd ki a **T**ype `83 Linux` partíciótípust. A létrehozott `/var` partíció `sda2` -ként fog megjelenni.

Következő lépésben hozz létre egy harmadik partíciót a swap számára. Válassz egy megfelelő méretet (itt most 1 GB) és a partíció típusa **T**ype pedig legyen `82 (Linux swap / Solaris)`. A létrehozott swap partíció `sda3` -ként fog megjelenni.

A lemez fennmaradó szabad helyén pedig létrehozzuk a `/home` részére szánt partíciót. Válaszd ki primary partícióként majd állítsd be a méretét. Típusa**T**ype legyen `83 Linux`. A létrehozott `/home` partíció `sda4` -ként fog megjelenni.

A példánk alapján így fog kinézni a lemez:

```
Name    Flags     Part Type    FS Type           [Label]         Size (MB)
-------------------------------------------------------------------------
sda1               Primary     Linux                             15440 #root
sda2               Primary     Linux                             10256 #/var
sda3               Primary     Linux swap / Solaris              1024  #swap
sda4               Primary     Linux                             133000 #/home

```

Válaszd a **W**rite (írás) opciót, és írd be: `yes`. Minden adat törlődni fog a lemezről. Válaszd a **Q**uit (kilépést) a partícionálóból való kilépéshez.

Ismerkedj meg a különböző fájlrendszerekkel, amelyeket fentebb említettünk, majd lépj tovább a III. opcióra.

**Megjegyzés:** A Linux kernel legújabb fejlesztése óta, amely tartalmazza a libata és PATA modulokat, az összes IDE, SATA és SCSI lemez sd"x" jelölési sémával rendelkezik. Ez teljesen normális, és nem adhat okot aggodalomra.

#### III. opció: Partíciók, fájlrendszerek, csatolási pontok konfigurációja

Erre az opcióra való ugrás feltétele az, hogy már vannak létrehozott partícióink (például a II. opció által) és ki lett választva, a lemezek jelölési módja [dev](https://en.wikipedia.org/wiki//dev "wikipedia:/dev"), címke, vagy [UUID](/index.php/UUID "UUID"). Az észlelt partíciók listája meg fog jelenni. Minden partíció egy számmal van jelölve. Például `sda1` -gyel van jelölve az első partíció míg az `sda` jelölés a teljes lemezre utal.

Formázd meg az egyes partíciókat a választott fájlrendszerrel, majd határozd meg a csatolási pontjaikat. Lemezcímke és egyéb beállításokat eszközölhetsz az [mkfs](https://en.wikipedia.org/wiki/mkfs "wikipedia:mkfs")-szel.

**Megjegyzés:** Ha nem hoztál létre különálló `/boot` partíciót, akkor biztonsággal figyelmen kívül hagyhatod azt a figyelmeztetést, ami arra utal, hogy ez a partíció nem létezik.

Lépj vissza a főmenübe (Main Menu).

### Csomagok kiválasztása

A telepítés során minden elérhető szoftvercsomag a [[core]](/index.php/Official_repositories#core "Official repositories") csomagtárolóból származik. Továbbá ez a csomagtároló ketté van osztva **base** , és **base-devel**  csoportokra. Csomaginformációk és rövid leírások a [core]-ról elérhetőek [itt](https://www.archlinux.org/packages/?repo=Core&arch=any&arch=i686&arch=x86_64&limit=all&sort=pkgname).

#### Rendszerbetöltő (bootloader)

Rendszerbetöltő programként választhatod a [GRUB](/index.php/GRUB "GRUB")-ot vagy a [syslinux](/index.php/Syslinux "Syslinux")-ot.

#### Csomag csoportok

Válassz a csomagkategóriák közül:

**Megjegyzés:** Az egyszerűség kedvéért alapértelmezésként a [base](https://www.archlinux.org/groups/x86_64/base/) csoport összes csomagja ki van jelölve. Használd a "space" billentyűt a csomagok kijelöléséhez, illetve a kijelölés elvetéséhez.

*   [base](https://www.archlinux.org/groups/x86_64/base/): Szoftvercsomagok a [core] csomagtárolóból a minimális rendszerkörnyezet telepítéséhez. Mindig válaszd ki ezt, és ne távolíts el semmilyen csomagot belőle, mert az Arch Linux összes csomagja feltételezi a _base_ meglétét.
*   [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/): Extra programok a [core]-ból, úgy mint a `make` és `automake`. A legtöbb kezdőnek is ajánlott feltelepíteni, hiszen valószínűleg szükségük lesz rá új szoftverek telepítése végett. A _base-devel_ csoport telepítése szükséges, az [Arch közösségi tárolóból](/index.php/Arch_User_Repository "Arch User Repository") való programok telepítéséhez.

A kategória-választás után az elérhető csomagok listája tárul eléd, amelyekből kiválaszthatod a számodra szükséges programokat. Használd a "space" billentyűt a csomagok kijelöléséhez illetve a kijelölés elvetéséhez. Ha nem tudod most eldönteni, hogy milyen csomagokra van szükséged, akkor kihagyhatod ezt a lépést, és majd később feltelepítheted őket a [pacman](/index.php/Pacman "Pacman") használatával.

**Megjegyzés:** Ha vezeték nélküli hálózati csatlakozás szükséges, akkor ne felejtsd el kijelölni és telepíteni a [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) csomagot. Néhány vezeték nélküli interfésznek szüksége lehet az [**ndiswrapper**](/index.php/Wireless_network_configuration#ndiswrapper "Wireless network configuration")-re és/vagy egy meghatározott [**firmware**](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration")-re. Ha WPA titkosítást szeretnél használni, akkor a [**wpa_supplicant**](/index.php/WPA_supplicant "WPA supplicant") nevű segédprogramra is szükséged lesz. A [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") oldal segítségedre lehet a vezeték nélküli hálózati eszközhöz tartozó megfelelő csomag kiválasztásában. Fontold meg a **[netcfg](/index.php/Netcfg "Netcfg")** program feltelepítését is, ugyanis ez megkönnyíti a hálózati beállítások konfigurálását, miután elindítottad a frissen települt rendszert.

A kívánt csomagok kiválasztása után továbbléphetsz a következő pontra a **Csomagok telepítésére**.

### Csomagok telepítése

Az _Install Packages_ telepíteni fogja a kiválasztott csomagokat a rendszeredre. Ha a helyi csomagtárolót választottadl, akkor azok a CD/USB-ről fognak települni. Ha viszont távolit, akkor a jelenlegi legújabb csomagverziók fognak letöltődni, majd települni a [pacman](/index.php/Pacman "Pacman") által.

**Megjegyzés:** Néhány telepítésnél előfordulhat, hogy megjelenik egy kérdés azzal kapcsolatban, hogy meg akarod-e tartani a pacman által letöltött csomagokat, amelyek a `/var/cache/pacman/pkg`-ban találhatóak meg. Ha a "yes"-t választod, akkor lehetőséged lesz arra, hogy hiba esetén egy régebbi csomagverziót újra tudj telepíteni. További információkat ennek menetéről a [downgrade](/index.php/Downgrade "Downgrade") leírásban olvashatsz. Ha a lemezen elegendő hely áll a rendelkezésedre, akkor ajánlott a régebbi csomagverziók megtartása. Ez a csomagtár-méret idővel a rendszer folyamatos frissítése miatt növekedni fog, de a csomagok bármikor törölhetőek a [pacman](/index.php/Pacman "Pacman") segítségével.

### A rendszer konfigurációja

**Tip:** A következő lépések megértése és pontos követése kulcsfontosságú a jól konfigurált rendszerhez.

A telepítés ezen pontján az Arch Linux alaprendszerének elsődleges konfigurációs fájljait fogod szerkeszteni.

Meg fog jelenni egy menü, amely a rendszer fő konfigurációs fájljait tartalmazza.

**Megjegyzés:** Feltétlen fontos, hogy szerkeszd, de legalább ellenőrizd le, hogy miket tartalmaznak ezek a konfigurációs fájlok. A telepítő szkript az általad beírt információkat figyelembe véve fogja létrehozni ezeket a fájlokat. Gyakori hibaként merül fel, hogy sokan kihagyják a konfigurációnak ezen fontos lépését.

#### Van-e lehetőség a konfiguráció automatizálására?

A konfiguráció folyamatának elrejtése ellentétben áll az **[Arch filozófiájával](/index.php/The_Arch_Way_(Magyar) "The Arch Way (Magyar)")**. Míg újabb kernel verziók és hardver eszközök kiváló támogatást nyújtanak az automatikus konfigurációhoz, úgy az Arch minden lehetséges konfigurációs fájlt megad a felhasználónak a rendszer jobb átláthatósága és az erőforrások kezelése szempontjából. Miközben a saját igényeid szerint szerkeszted ezeket a fájlokat, megtanulod az Arch Linux manuális konfigurációját, megismerkedsz az alapstruktúrájával, és felkészültebb leszel az új rendszered könnyebb kezelésére és karbantartására.

#### /etc/rc.conf

Az Arch Linux az `/etc/rc.conf` fájlt használja a rendszer fő konfigurációs fájljaként. Ez az egy fájl többféle konfigurációs információt tartalmaz úgy mint az időzóna, billentyűkiosztás, kernel modulok, hálózati beállítások és automatikusan induló démonok. Ezen kívül olyan beállítások is megtalálhatóak itt, amelyek forrását az `/etc/rc*` fájlok adják.

##### LOCALIZATION szekció

	HARDWARECLOCK

	Megadja, hogy a hardver óra, ami a rendszerbetöltéskor és leállításkor szinkronizálásra kerül **UTC** vagy **localtime** -ban legyen elmentve. Lásd az [óra beállítása](#.C3.93ra_be.C3.A1ll.C3.ADt.C3.A1sa) részt.

	TIMEZONE

	Időzóna megadása. (Az összes választható időzóna megtalálható az `/usr/share/zoneinfo/` fájlban).

	KEYMAP

	Az elérhető billentyűzetkiosztások a `/usr/share/kbd/keymaps` található meg. Ez a beállítás csak a TTY konzolokra lesz érvényes, a grafikus környezetre vagy **X** -re nincs hatással.

	CONSOLEFONT 

	Az elérhető konzolbetűkészletek az `/usr/share/kbd/consolefonts/`-ban vannak. Az alapértelmezett (blank) védett betűkészlet.

	CONSOLEMAP 

	A konzol map beállítása arra, hogy a `setfont` programot használja bootolásnál. Az elérhető map-ek az `/usr/share/kbd/consoletrans`, találhatóak. Az alapértelmezett (blank) védett.

	LOCALE

	Lokális környezet beállítása, amit az i18n-et támogató programok fognak használni, azaz magyarra beállítva, amelyik programnál elérhetőek a magyar fordítások, az magyarul fog megjelenni. Az elérhető lokálok listája megtekinthető a `locale -a` parancsot kiadva. Ahhoz, hogy magyar nyelvet állíthassunk be ki kell kommentelnünk a megfelelő sort az `/etc/locale.conf` fájlban (például **hu_HU.UTF-8**). Ez után le kell generálnunk a locale fájlt az `locale-gen` parancsot kiadva. Majd végül írjuk be a **hu_HU.UTF-8** -at ide a LOCALE után. További információkért olvasd el a [Locale](/index.php/Locale "Locale") cikket.

	DAEMON_LOCALE

	Állítsd "**yes**" -re ha a démonokhoz is a `$LOCALE` környezetet akarod használni. Ha "**no**" -ra állítjuk akkor a C lokál lesz használatban alapértelmezettként.

	USECOLOR 

	Válassz "**yes**"-t ha színeket is szeretnél látni a konzolokban.

**Példal a LOCALIZATION szekcióra:**

```
HARDWARECLOCK="UTC"
TIMEZONE="Europe/Budapest"
KEYMAP=""hu
CONSOLEFONT=
CONSOLEMAP=
LOCALE=hu_HU.UTF-8
DAEMON_LOCALE="yes"
USECOLOR="yes"

```

##### HARDWARE szekció

	MODULES 

	Ha egy kernel modul nincs betöltve amely egy programnak szükséges, akkor azt itt megadva boot-olásnál be fog töltődni. Például ha fel van telepítve a CUPS a nyomtatáshoz, akkor be kell tölteni a szükséges modulokat úgy mint: **lp**, **parport**, **parport_pc**

**Megjegyzés:** Alap esetben minden szükséges modul automatikusan betöltődik az udev által, tehát ritkán lesz szükséged arra, hogy manuálisan kelljen itt hozzáadnod valamit.

**Példa a HARDWARE szekcióra:**

```
MODULES=()
USEDMRAID="no"
USEBTRFS="no"
USELVM="no"
```

##### NETWORKING szekció

	HOSTNAME

	Bármilyen nevet választhatsz, amit szeretnél. Ez lesz a számítógéped neve. Bármit is írsz ide, utána írd be ugyan ezt a `/etc/hosts` fájlba is!

**Példa:**

```
HOSTNAME="arch"

```

	interface

	Add meg az ethernet interfész nevét, amin keresztül csatlakozni fogsz a helyi hálózatra.

	address

	Ha statikus IP beállításokat akarsz használni, az interfészed IP címe ide kerül. **Hagyd ezt a részt üresen DHCP használata esetén!**

	netmask

	Opcionális, alapértelmezett _255.255.255.0_. Ha egyéni hálózati maszkot szeretnél használni, akkor itt add meg. **Hagyd ezt a részt üresen DHCP használata esetén!**

	broadcast

	Opcionális. Ha egyéni szórási címet akarsz használni, akkor itt add meg. **Hagyd ezt a részt üresen DHCP használata esetén!**

	gateway

	Ha statikus IP címet állítottál be az "address" résznél, akkor itt meg kell adnod az alapértelmezett átjáró (pl. modem/router) IP címét. **Hagyd ezt a részt üresen DHCP használata esetén!**

	NETWORK_PERSIST 

	Ezen beállítás "yes"-re kapcsolása könnyített kilépést használ az ssh-n keresztül a gépre bejelentkezett felhasználóknak a gép kikapcsolása, vagy újraindítása esetén. Ha a gép NFS-en keresztül működik, akkor ez a beállítás szükséges.

	NETWORKS

	Ez az opcionális beállítás csak akkor szükséges, ha a [netcfg](/index.php/Netcfg "Netcfg") csomagot az opcionális _dialog_ csomaggal együtt használjuk. A rendszer betöltésnél netcfg profilokat lehet beállítani. Ez akkor hasznos, ha bővített hálózati funkciókra van szükséged, például több különböző hálózati beállítás szüksége esetén (laptop használók).

**Példa statikus IP beállításra:**

```
HOSTNAME="arch"
interface=eth0
address=192.168.1.100
netmask=255.255.255.0
broadcast=192.168.1.255
gateway=192.168.1.1
#NETWORKS=(main)
```

**Példa Dinamikus címkiosztás beállítására (DHCP):**

```
HOSTNAME="arch"
interface=eth0
address=
netmask=
broadcast=
gateway=
#NETWORKS=(main)
```

**Egyéb megjegyzések**

Statikus IP használata esetén írd be a `/etc/resolv.conf`-ba az általad használni kívánt DNS szolgáltató címét. További információért nézd meg a [resolv.conf](#.2Fetc.2Fresolv.conf) részt.

**Megjegyzés:** Vezeték nélküli hálózatra való automatikus csatlakozáshoz néhány további beállítás és hálózati menedzser program használata úgy mint a [netcfg](/index.php/Netcfg "Netcfg") vagy [wicd](/index.php/Wicd "Wicd") szükséges. Részletekért nézd meg a [Wireless Setup](/index.php/Wireless_network_configuration#Part_II:_Wireless_management "Wireless network configuration") leírást.

**Tip:** Ha nem szabványis MTU méretet akarsz használni (pl. jumbo frames) ÉS az eszközöd támogatja ezt a lehetőséget, akkor olvasd el a [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames") wiki bejegyzést további információkért.

##### DAEMONS szekció

Itt az `/etc/rc.d/`-ben megtalálható szkriptek neveit adhatjuk meg, amelyek a rendszer indulásakor lefutnak abban a sorrendben, ahogy mi megadtuk őket. A szkriptek aszinkron betöltésére is lehetőség van, amivel a rendszerbetöltési folyamat gyorsítható:

```
DAEMONS=(network @syslog-ng netfs @crond)

```

*   Ha egy szkript neve elé egy felkiáltó jelet (`!`) teszünk, akkor az adott szkript nem fog lefutni rendszerindításnál.
*   Ha szkript neve elé egy "kukac" szimbólumot rakunk (`@`), akkor a szkript a háttérben fog lefutni és betöltési folyamat ugrik tovább a következő betöltendő szkript-re, így nem kell megvárni minden egyes szkript betöltődését ahhoz, hogy folytatódjon a rendszer indulása. Ne futtass a háttérben olyan szkripteket, amelyek egy másik démon elindulásától függenek. Például az `mpd` a `network` démontól függ, ezért a network későbbi betöltése az`mpd` hibájához vezethet.
*   Akkor szerkeszd ezt a szekciót, ha egy új rendszerszolgáltatást telepítettél, aminek szüksége van a rendszer betöltésével együtt indulni.

**Megjegyzés:** Ezt a "BSD-stílusú" betöltést használja az Arch annak kezelésére, amit más linux disztribúciók különféle szimbolikus linkekkel oldanak meg az `/etc/init.d/` könyvtárba mutatva.

###### Általános információk

A [daemons](/index.php/Daemons "Daemons") sor elemeit nem szükséges most módosítani, de jó tudni, mik azok a "démonok" ugyanis később még említésre kerülnek ebben az útmutatóban.

A [daemon](https://en.wikipedia.org/wiki/Daemon_(computing) "wikipedia:Daemon (computing)") az egy háttérben futó program, ami valamilyen esemény bekövetkeztére vár, illetve egyéb szolgáltatásokat kínál. Egy jó példa erra a webszerver démona, (pl.: `httpd`), amely a weboldalak betöltési kérelmét teljesíti, vagy például egy SSH szerver démona, ami egy felhasználó beléptetésére vár (pl.: `sshd`). Ezek mellett egyéb funkciókat elvégző démonok is léteznek, amelyek például rendszerüzeneteket írnak egy naplófájlba (pl.: `syslog`, `metalog`), vagy olyanok, amelyek a grafikus bejelentkezést szolgáltatják (pl.: `gdm`, `kdm`). Mindezen démonok hozzáadhatóak a listához, és rendszerindítással együtt el fognak indulni. A hasznos démonokról az útmutató későbbi részében lesz szó.

**Tip:** Az összes Arch démon szkript a `/etc/rc.d/` könyvtárban található meg.

#### /etc/fstab

Az [fstab](https://en.wikipedia.org/wiki/fstab "wikipedia:fstab") (**f**ile **s**ystems **tab**le) (fájlrendszer tábla) a rendszer beállítások részét képezi. Az **fstab** az összes elérhető lemezt és lemezpartíciót tartalmazza, valamint megmutatja milyen módon épülnek be az egyes lemezek a teljes rendszer fájlrendszerébe. A `/etc/fstab` fájlt legtöbb esetben a `mount` parancs használja. A `mount` parancs segítségével tudunk egy lemezt vagy egy partíciót csatolni a rendszerünk fő fájlhierarchiájába, azért hogy a csatolt lemez használható legyen az operációs rendszerben. A `mount -a` parancs a `/etc/rc.sysinit` fájlból rendszerindításkor futtatásra kerül, ami beolvassa a `/etc/fstab`-ban található sorokat, hogy mely lemezek, partíciók legyen csatolva és milyen opciókkal. Ha például a `noauto` résszel van kiegészítve egy sor a`/etc/fstab`-ban, akkor a `mount -a` hatására az adott fájlrendszer **nem** lesz rendszerindításkor automatikusan felcsatolva.

Egy példa a `/etc/fstab` fájlra:

```
# <file system>                            <dir>     <type>  <options>            <dump> <pass>
tmpfs                                      /tmp      tmpfs   nodev,nosuid         0      0
UUID=0ddfbb25-9b00-4143-b458-bc0c45de47a0  /         ext4    defaults             0      1
UUID=da6e64c6-f524-4978-971e-a3f5bd3c2c7b  /var      ext4    defaults             0      2
UUID=440b5c2d-9926-49ae-80fd-8d4b129f330b  none      swap    defaults             0      0
UUID=95783956-c4c6-4fe7-9de6-1883a92c2cc8  /home     ext4    defaults             0      2

```

**Megjegyzés:** További információkért és teljesítménnyel kapcsolatos beállításokért úgy mint `noatime` vagy `relatime` nézd meg a részletesebb [fstab cikket](/index.php/Fstab "Fstab")!

	<file system>

	Describes the block device or remote filesystem to be mounted. For regular mounts, this field will contain a link to a block device node (as created by mknod which is called by udev at boot) for the device to be mounted; for instance, `/dev/cdrom` or `/dev/sda1`.
**Note:** If your system has more than one hard drive, the installer will default to using UUID rather than the sd_x_ naming scheme, for consistent device mapping. **[Utilizing UUID](/index.php/Persistent_block_device_naming "Persistent block device naming") has several advantages and may also be preferred to avoid issues if hard disks are added to the system in the future.** Due to active developments in the kernel and also udev, the ordering in which drivers for storage controllers are loaded may change randomly, yielding an unbootable system/kernel panic. Nearly every motherboard has several controllers (onboard SATA, onboard IDE), and due to the aforementioned development updates, `/dev/sda` may become `/dev/sdb` on the next reboot. For more information, see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

	<dir>

	Describes the mount point for the filesystem. For swap partitions, this field should be specified as `none` (swap partitions are not actually mounted).

	<type>

	Describes the type of the filesystem. The Linux kernel supports many filesystem types. (For the filesystems currently supported by the running kernel, see `/proc/filesystems`). An entry `swap` denotes a file or partition to be used for swapping. An entry `ignore` causes the line to be ignored. This is useful to show disk partitions which are currently unused.

	<options>

	Describes the mount options associated with the filesystem. It is formatted as a comma-separated list of options with no intervening spaces. It contains at least the type of mount plus any additional options appropriate to the filesystem type. For documentation on the available options for non-nfs file systems, see `mount(8)`.

	<dump>

	Used by the `dump(8)` command to determine which filesystems are to be dumped. dump is a backup utility. If the fifth field is not present, a value of zero is returned and dump will assume that the filesystem does not need to be backed up. _Note that dump is not installed by default._

	<pass>

	Used by the `fsck(8)` program to determine the order in which filesystem checks are done at boot time. The root filesystem should have the highest priority with `<pass>` of `1`, and other filesystems you want to have checked should have a `<pass>` of `2`. Filesystems with `0` `<pass>` will not be checked. Filesystems within a drive will be checked sequentially, but filesystems on different drives will be checked at the same time to utilize parallelism available in the hardware. If the sixth field is not present or zero, a value of zero is returned and fsck will assume that the filesystem does not need to be checked.

*   For more information, see [fstab](/index.php/Fstab "Fstab").

#### /etc/mkinitcpio.conf

**Note:** Most users will not need to modify this file at this time, but please read the following explanatory information.

This file allows further fine-tuning, through [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), of the initial ram filesystem, or initramfs, (also historically referred to as the initial ramdisk or "initrd") for your system. The initramfs is a gzipped image that is read by the kernel during boot. The purpose of the initramfs is to bootstrap the system to the point where it can access the root filesystem. This means it has to load any modules that are required for devices like IDE, SCSI, or SATA drives (or USB/FW, if you are booting from a USB/FW drive). Once the initrramfs loads the proper modules, either manually or through udev, it passes control to the kernel and your boot continues. For this reason, the initramfs only needs to contain the modules necessary to access the root filesystem. It does not need to contain every module you would ever want to use. The majority of common kernel modules will be loaded later on by udev, during the init process.

**mkinitcpio** is the next generation of **initramfs creation**. It has many advantages over the old **mkinitrd** and **mkinitramfs** scripts.

*   It uses **glibc** and **busybox** to provide a small and lightweight base for early userspace.
*   It can use **udev** for hardware autodetection at runtime, thus preventing numerous unnecessary modules from being loaded.
*   Its hook-based init script is easily extendable with custom hooks, which can easily be included in pacman packages without having to modifiy mkinitcpio itself.
*   It already supports **lvm2**, **dm-crypt** for both legacy and luks volumes, **raid**, **swsusp** and **TuxOnIce** resuming and booting from **usb mass storage** devices.
*   Many features can be configured from the kernel command line without having to rebuild the image.
*   The **mkinitcpio** script makes it possible to include the image in a kernel, thus making a self-contained kernel image is possible.
*   Its flexibility makes recompiling a kernel unnecessary in many cases.

If using RAID or LVM on the root filesystem, the appropriate HOOKS must be configured. See the wiki pages for [LVM/RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") and [Configuring mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio") for more information. If using a non-US keyboard. add the `keymap` hook to load your local keymap during boot. Add the `usbinput` hook if using a USB keyboard (otherwise, if boot fails for some reason you will be asked to enter root's password for system maintenance but will be unable to do so). Remember to add the `usb` hook when installing arch on an external hard drive, Compact Flash, or SD card, which is connected via usb, e.g.:

```
HOOKS="base udev autodetect pata scsi sata usb filesystems keymap usbinput"

```

If you need support for booting from USB devices, FireWire devices, PCMCIA devices, NFS shares, software RAID arrays, LVM2 volumes, encrypted volumes, or DSDT support, configure your HOOKS accordingly.

#### /etc/modprobe.d/modprobe.conf

This file can be used to set special configuration options for the kernel modules. It is unnecessary to configure this file in the example. The article on [kernel modules](/index.php/Kernel_modules "Kernel modules") has more information.

#### /etc/resolv.conf

**Note:** If you are using DHCP, you may safely ignore this file, as by default, it will be dynamically created and destroyed by the dhcpcd daemon. You may change this default behavior if you wish. See the [network](/index.php/Network#For_DHCP_IP "Network") and [resolv.conf](/index.php/Resolv.conf "Resolv.conf") pages for more information.

The _resolver_ is a set of routines in the C library that provide access to the Internet Domain Name System (DNS). One of the main functions of DNS is to translate domain names into IP addresses, to make the Web a friendlier place. The resolver configuration file, or `/etc/resolv.conf`, contains information that is read by the resolver routines the first time they are invoked by a process.

If you use a static IP, set your DNS servers in `/etc/resolv.conf` (nameserver <ip-address>). You may have as many as you wish.

An example, using OpenDNS:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

If you are using a router, you may specify your DNS servers in the router itself, and merely point to it from your `/etc/resolv.conf`, using your router's IP (which is also your gateway from `/etc/rc.conf`). Example:

```
nameserver 192.168.1.1

```

If using **DHCP**, you may also specify your DNS servers in the router, or allow automatic assignment from your ISP, if your ISP is so equipped.

#### /etc/hosts

This file associates IP addresses with hostnames and aliases. Each host is represented by a single line.

```
<IP-address> <hostname> [aliases...]

```

Add your _hostname_, coinciding with the one specified in `/etc/rc.conf`, as an alias, so that it looks like this:

```
127.0.0.1   localhost.localdomain   localhost **yourhostname**

```

**Warning:** This format, **including the "localhost" and your actual host name**, is required for program compatibility! So, if you have named your computer "arch", then that line above should look like this:

```
127.0.0.1   localhost.localdomain   localhost arch

```

Errors in this entry may cause poor network performance and/or certain programs to open very slowly, or not work at all. This is a very common error for beginners.

**Note:** Recent versions of the Arch Linux Installer automatically add your hostname to this file once you edit `/etc/rc.conf` with such information. If, for whatever reason, this is not the case, you may add it yourself with the given instructions.

If you use a static IP, add another line using the syntax: <static-IP> <hostname.domainname.org> <hostname> e.g.:

```
192.168.1.100 **yourhostname**.domain.org  **yourhostname**

```

**Tip:** For convenience, you may also use `/etc/hosts` aliases for hosts on your network, and/or on the Web, e.g.:

```
192.168.1.90 media
192.168.1.88 data

```

The above example would allow you access a media and data server on your network by name and without the need for typing out their respective IP addresses.

#### /etc/locale.gen

The `/usr/sbin/locale-gen` command reads from `/etc/locale.gen` to generate specific locales. They can then be used by **glibc** and any other locale-aware program or library for rendering text, correctly displaying regional monetary values, time and date formats, alphabetic idiosyncrasies, and other locale-specific standards.

By default `/etc/locale.gen` is an empty file with commented documentation. Once edited, the file remains untouched. `locale-gen` runs on every **glibc** upgrade, generating all the locales specified in `/etc/locale.gen`.

Choose the locale(s) you need by removing the # in front of the lines you want, e.g.:

```
en_US ISO-8859-1
en_US.UTF-8

```

The installer will now run the locale-gen script, which will generate the locales you specified. You may change your locale in the future by editing `/etc/locale.gen` and subsequently running `locale-gen` as root.

**Note:** If you fail to choose your locale, this will lead to a "The current locale is invalid..." error. This is perhaps the most common mistake by new Arch users.

#### /etc/pacman.conf

pacman will attempt to read `/etc/pacman.conf` each time it is invoked. This configuration file is divided into sections, or repositories. Each section defines a package [repository](/index.php/Official_repositories "Official repositories") that pacman can use when searching for packages. The exception to this is the `options` section, which defines global options.

Enable all desired repositories by removing the # in front of the 'Include =' and '[repository]' lines.

**Note:**

*   The defaults should work, so modifying at this point may be unnecessary, but verification is always recommended. Further info available in the [Official repositories](/index.php/Official_repositories "Official repositories") article.
*   If you are using a 64-bit installation, you should consider enabling the multilib repository to allow access to 32-bit software. All 32-bit software is in the multilib repository for 64-bit installations. Enabling multilib is not necessary for proper functioning, but it must be enabled to access 32-bit software.
*   When choosing repos, be sure to uncomment both the repository header lines in [brackets] as well as the 'Include =' lines. Failure to do so will result in the selected repository being omitted! This is a very common error.

#### /etc/pacman.d/mirrorlist

Mirror sites are Internet locations where exact copies of data reside. Multiple mirrors provide reliability, redundancy, and allow for faster data transfer depending on geographic location. Closer sites generally give faster data rates. Choose a mirror repository for `pacman` by uncommenting the desired mirror locations in this file. Remember that ftp.archlinux.org is throttled, limiting downloads to 50 kB/s. Read the [Mirrors](/index.php/Mirrors "Mirrors") wiki page for more details about setting up pacman mirrors. Note that the mirrors chosen here will carry over into your installation.

#### Root password

Finally, set a root password and make sure that you remember it later. Return to the Main Menu and continue with **Installing Bootloader**.

#### Done

When you select "Done", the system will rebuild the images and put you back to the Main Menu. This may take some time.

### Install bootloader

**Note:** If you already have an installed distro that you intend to keep with a bootloader such as GRUB or GRUB2, you may choose to skip this step and instead run `update-grub` in the existing distro after installation

Because we have no secondary operating system in our example, we will need a bootloader. [GRUB](/index.php/GRUB "GRUB") (**GR**and **U**nified **B**ootloader) will be used in the following examples. Alternatively, you may choose [LILO](/index.php/LILO "LILO"), [Syslinux](/index.php/Syslinux "Syslinux") or [GRUB2](/index.php/GRUB2 "GRUB2"). Please see the related wiki and documentation pages if you choose to use a bootloader other than GRUB.

The provided **GRUB** configuration (`/boot/grub/menu.lst`) should be sufficient, but verify its contents to ensure accuracy (specifically, ensure that the root (/) partition is specified by UUID on line 3). You may want to alter the resolution of the console by adding a vga=<number> kernel argument corresponding to your desired virtual console resolution. (A table of resolutions and the corresponding numbers is printed in the `menu.lst`.)

**Explanation:**

	title

	A printed menu selection. "Arch Linux (Main)" will be printed on the screen as a menu selection.

	root

	**GRUB'**s root; the drive and partition where the kernel (`/boot`) resides, according to system BIOS. (More accurately, where GRUB's stage2 file resides). **NOT necessarily the root (/) file system**, as they can reside on separate partitions. GRUB's numbering scheme starts at 0, and uses an hd_x,x_ format regardless of IDE or SATA, and enclosed within parentheses. The example indicates that `/boot` is on the first partition of the first drive, according to the BIOS, so (hd0,0).

	kernel

	This line specifies:

*   The path and filename of the kernel _**relative to GRUB's root**_. In the example, `/boot` is merely a directory residing on the same partition as `/` and **vmlinuz-linux** is the kernel filename; `/boot/vmlinuz-linux`. If `/boot` were on a separate partition, the path and filename would be simply `/vmlinuz-linux`, being relative to **GRUB'**s root.
*   The `root=` argument to the kernel statement specifies the partition containing the root (`/`) directory in the booted system, (more accurately, the partition containing `/sbin/init`). An easy way to distinguish the 2 appearances of "root" in `/boot/grub/menu.lst` is to remember that the first root statement _informs GRUB where the kernel resides_, whereas the second `root=` kernel argument _tells the kernel where the root filesystem (`/`) resides_.
*   Kernel options: In our example, **ro** mounts the filesystem as read-only during startup, which is usually a safe default; you may wish to change this in case it causes problems booting. **quiet** sets the default kernel log level so that all messages during boot are suppressed except serious ones. Depending on hardware, **rootdelay=8** may need to be added to the kernel options in order to be able to boot from an external usb hard drive.

	initrd

	The path and filename of the initial RAM filesystem **relative to GRUB'**s root. Again, in the example, `/boot` is merely a directory residing on the same partition as `/` and **initramfs-linux.img** is the initrd filename; `/boot/initramfs-linux.img`. If `/boot` were on a separate partition, the path and filename would be simply **/initramfs-linux.img**, being relative to **GRUB'**s root.

Example:

```
title  Arch Linux (Main)
root   (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sda1 ro quiet
initrd /boot/initramfs-linux.img

```

Example for /boot on a separate partition:

```
title  Arch Linux (Main)
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda3 ro quiet
initrd /initramfs-linux.img

```

Install the [GRUB](/index.php/GRUB "GRUB") bootloader to the **Master Boot Record** (`/dev/sda` in our example).

**Note:** Arch Linux installers prior to the 2011.08.19 release included an option to install the bootloader to either a partition or the MBR. This option has been removed and so it is no longer possible to install the bootloader to a partition using AIF (see [FS#25726](https://bugs.archlinux.org/task/25726)). If you wish to install the bootloader to a [partition boot record](https://en.wikipedia.org/wiki/Volume_boot_record "wikipedia:Volume boot record"), simply exit AIF without invoking the "Install bootloader" step and install the bootloader manually.

### Reboot

That is it; You have configured and installed your Arch Linux base system. Exit the install, and reboot:

 `# reboot` 
**Tip:** Be sure to remove the installation media and perhaps change the boot preference in your BIOS; otherwise you may boot back into the installation!

**[Útmutató kezdőknek](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)")**

* * *

[Előszó](/index.php/Beginners%27_Guide/Preface_(Magyar) "Beginners' Guide/Preface (Magyar)") >> [Előkészületek](/index.php/Beginners%27_Guide/Preparation_(Magyar) "Beginners' Guide/Preparation (Magyar)") >> **Telepítés** >> [Telepítés után](/index.php/Beginners%27_Guide/Post-Installation_(Magyar) "Beginners' Guide/Post-Installation (Magyar)") >> [Extra/Függelék](/index.php?title=Beginners%27_Guide/Extra_(Magyar)&action=edit&redlink=1 "Beginners' Guide/Extra (Magyar) (page does not exist)")