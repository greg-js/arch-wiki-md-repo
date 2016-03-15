**Tip:** Ez az oldal a teljes Beginners' Guide (Magyar) útmutató egyik részoldala. Ha az útmutatót teljes egészében akarod olvasni, akkor **[kattints ide](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)")**.

## Contents

*   [1 Telepítés után](#Telep.C3.ADt.C3.A9s_ut.C3.A1n)
*   [2 GRATULÁLUNK!](#GRATUL.C3.81LUNK.21)
*   [3 Friss hírek!](#Friss_h.C3.ADrek.21)
*   [4 A Hálózat Beállítása (ha szükséges)](#A_H.C3.A1l.C3.B3zat_Be.C3.A1ll.C3.ADt.C3.A1sa_.28ha_sz.C3.BCks.C3.A9ges.29)
*   [5 Vezetékes hálózat](#Vezet.C3.A9kes_h.C3.A1l.C3.B3zat)
    *   [5.1 Wirelles Hálózat](#Wirelles_H.C3.A1l.C3.B3zat)
    *   [5.2 Proxy Szerver](#Proxy_Szerver)
    *   [5.3 Analóg Modem, ISDN, és DSL (PPPoE)](#Anal.C3.B3g_Modem.2C_ISDN.2C_.C3.A9s_DSL_.28PPPoE.29)
*   [6 Frissítés, szinkronizálás és disztribúciófrissítés a pacman-el](#Friss.C3.ADt.C3.A9s.2C_szinkroniz.C3.A1l.C3.A1s_.C3.A9s_disztrib.C3.BAci.C3.B3friss.C3.ADt.C3.A9s_a_pacman-el)
    *   [6.1 /etc/pacman.conf](#.2Fetc.2Fpacman.conf)
        *   [6.1.1 Csomagtárolók (repositories)](#Csomagt.C3.A1rol.C3.B3k_.28repositories.29)
        *   [6.1.2 AUR](#AUR)
    *   [6.2 /etc/pacman.d/mirrorlist](#.2Fetc.2Fpacman.d.2Fmirrorlist)
    *   [6.3 rankmirrors](#rankmirrors)
        *   [6.3.1 Tűkörellenörzés naprakész csomagokért](#T.C5.B1k.C3.B6rellen.C3.B6rz.C3.A9s_naprak.C3.A9sz_csomagok.C3.A9rt)
    *   [6.4 Barátkozzunk meg a pacman-el](#Bar.C3.A1tkozzunk_meg_a_pacman-el)
    *   [6.5 Frissítsük a rendszert](#Friss.C3.ADts.C3.BCk_a_rendszert)
        *   [6.5.1 Ignoring Packages](#Ignoring_Packages)

## Telepítés után

* * *

**[Útmutató kezdőknek](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)")**

* * *

[Előszó](/index.php/Beginners%27_Guide/Preface_(Magyar) "Beginners' Guide/Preface (Magyar)") >> [Előkészületek](/index.php/Beginners%27_Guide/Preparation_(Magyar) "Beginners' Guide/Preparation (Magyar)") >> [Telepítés](/index.php/Beginners%27_Guide/Installation_(Magyar) "Beginners' Guide/Installation (Magyar)") >> **Telepítés után** >> [Extra/Függelék](/index.php?title=Beginners%27_Guide/Extra_(Magyar)&action=edit&redlink=1 "Beginners' Guide/Extra (Magyar) (page does not exist)")

## GRATULÁLUNK!

Üdvözlünk a te új Arch Linux rendszereden! Ez a rész be fog mutatni különböző telepítés utáni teendőket mint például, hogy hogyan frissítsd az új rendszert, és hogyan hozz létre mezei, nem rendszergazda felhasználót.

Az új Arch Linux alap rendszer mostmár funkcionális GNU/Linux környezet és kész a testreszabásra. Innen, felépítheted ezt az elegáns alapvető ezközkészletet, illetve amit szeretnél, vagy szükséges a rendszeredhez.

Jelentkezz be root felhasználóként. Be fogjuk állítani a pacman-t és frissítjük a rendszert root felhasználóként.

Megjegyzés: A virtuális konzolok elérhetőek 1-től 6-ig. Ezek között válthatsz az <ALT>+F1...F6 billentyűkombinációval.

## Friss hírek!

```
Jó ötlet elolvasni mindíg a friss híreket, az egyes telepítési tippeket és munka-megkerülést. 
Példának okáért 16 áprilistől, a következő két tételt szükséges elolvasni: 

```

[https://www.archlinux.org/news/initscripts-update-manual-intervention-required/](https://www.archlinux.org/news/initscripts-update-manual-intervention-required/) [https://www.archlinux.org/news/filesystem-upgrade-manual-intervention-required/](https://www.archlinux.org/news/filesystem-upgrade-manual-intervention-required/)

Szükséged lesz ideiglenesen szerkeszteni a /etc/pacman.cond fájlt és beállítani a SigLevel-t 'Never'-re., ez ki fogja kapcsolni az aláírás ellenőrzését a csomagokban, és figyelmen kívül hagyja a figyelmeztetéseket a pacman frissítésnél...

Egy tipp: Ne pánikolj! Ha nem vagy otthon a key-készítésben, akkor várható a véletlenszerű key készítés entrópiája. Hogy ezt véghezvidd, nyomj véletlenszerű billentyűket a billentyűzeteden amíg a key létrejön. Ezt következőleg akkor kell megtenned mikor megjelenik, hogy a terminalod kéri.

```
pacman-key --init
pacman -S filesystem --force
rm /etc/profile.d/locale.sh
pacman -Syu

```

A rendszertelepítés elkészülte után, elolvashatod a [Pacman-key](/index.php/Pacman-key "Pacman-key") -ről szóló cikket, hogy hogyan engedélyezd az ellenörző aláírásokat a csomagokban.

## A Hálózat Beállítása (ha szükséges)

Ha helyesen beállítottad a rendszert, akkor kell működjön a hálózatod. Próbáld ping-elni a példa.com ot hogy ellenőrizd:

```
$ ping -c 3 példa.com 

```

```
PING példa.com (192.0.43.10) 56(84) bytes of data.
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=1 ttl=248 time=25.6 ms
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=2 ttl=248 time=22.9 ms
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=3 ttl=248 time=23.6 ms

```

```
--- példa.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 22.912/24.062/25.632/1.156 ms

```

Ha sikeresen létrehoztad a hálózati kapcsolatot, folyasd a [Update, Sync, and Upgrade the system with pacman](/index.php/Pacman "Pacman").

Hogyha mindhárom ping kísérlet "unknown host"error kimenetet ad, akkor a hálózatod nincs megfelelően beállítva. A hibaelhárítás a következő fájlok helyes beállításának ellenőrzésével lehetséges:

```
/etc/rc.conf  - Ellenőrizd az esetleges elírásokat és hibákat a HOSTNAME  és a NETWORKING részben.
/etc/hosts  - Ellenőrizd a formátum hibákat és elírásokat.
/etc/resolv.conf - Ezt csak akkor ellenőrizd ha statikus IP-címet használsz. Ha DHCP van használatban ez a fájl dinamikusan lessz létrehozva és törölve alapértelmezetten.

```

Tipp: Haladó használati utasításokat a hálózat beállításához a [Network](/index.php/Network "Network") cikkben találhatsz.

## Vezetékes hálózat

Ellenőrizd az Ethernet-et a következő paranccsalÉ

```
$ ip addr

```

Minden hálózati interfész ki lessz listázva. Láthatsz egy bejegyzést az eth0, vagy esetleg eth1-nek. Ezek a példák eth0-t fognak használni.

**Statikus IP**

Ha szükséges, beállíthatsz egy új statikus IP-címet a következő paranccsal:

```
# ip addr add <ip>/<netmask> dev <interfész>

```

```
Az alapértelmezett átjárót a követlező paranccsal állíthatjuk át:

```

```
# ip route add default via <ip>

```

Ellenőrizd, hogy a `/etc/resolv.conf` tartalmazza a DNS szervered, és ha nem add hozzá. Ellenőrizheted a hálozatot ismét a `ping -c 3 www.google.com` paranccsal. Ha ez működik állítsd be a `/etc/rc.conf`-ot fent leírtak szerint statikus IP-címhez.

Ha DHCP szerver/router-ed van a hálózatban próbáld a következő parancsot

`# dhcpcd eth`

Ha ez működik, állítsd be a `/etc/rc.conf`-ot a fent leírtak szerint dinamikus IP-címhez.

##### Wirelles Hálózat

Kérlek nézd a [Wireless Quickstart For the Live Environment](/index.php/Beginners%27_Guide/Installation#Setup_wireless_in_the_live_environment_.28optional.29 "Beginners' Guide/Installation") a részletekért a wireless hálózathoz való csatlakozáshoz. Habár már rég nem a telepítő rendszeren vagyunk, a parancsok hasonlóak az összes kapcsolodó wireless csomag telepítéséhez, a csomagválaszás közben. Emlékezz, a wireless ezközödnek szüksége lehet firmware-re a működése érdekében. Hibaelhárításért, nézd részletesen a [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") oltalt.

##### Proxy Szerver

Ha proxy szerver mögött vagy, nyisd meg a `/etc/wgetrc` fájlt és állítsd a http_proxy és ftp_proxy részt.

##### Analóg Modem, ISDN, és DSL (PPPoE)

Nézd a [Internet Access](/index.php/Internet_Access "Internet Access") cikket a részletes útmutatásért.

## Frissítés, szinkronizálás és disztribúciófrissítés a [pacman](/index.php/Pacman "Pacman")-el

Most frissíteni fogjuk a rendszert a [pacman](/index.php/Pacman "Pacman") segítségével. A [pacman](/index.php/Pacman "Pacman") a **pac**kage **man**ager az Arch Linuxban. Ez kezeli az egész csomagot a rendszerben, ez teszi lehetővé a telepítést, eltávolítást, csomag visszaállítást (a gyorsítótáron keresztül), egyéni összeállított csomagkezelést, automatikus függőségek kezelését, távolis és helyi keresést, és még sok mást. A pacman-t most csomagok letöltésére távoli adattárolókból és feltelepítésére használjuk a saját rendszerünkre.

**Megjegyzés:** Hogyha netinstall lemezképpel telepítettünk, valamennyi, ha nem az egész, a csomagjainkból máris naprakész. Azonban még mindíg ajánlatos futtatni a frissítést.

#### /etc/pacman.conf

Az csomagtárolók kiválasztásához és a pacman opcióihoz nyissuk meg a `/etc/pacman.conf`-ot.

Az csomagtárolók (repository) ebben a fájlban vannak felsorolva, ha aktiválni akarod a kívánt tárolót el kell távolítanod a # karaktert az eőtte található 'Include =' és '[repository]' sorokból.

**Megjegyzés:** Amikor kiválasztjuk az csomagtárolót, bizonyosodjunk meg hogy eltávolítottuk a # karaktert az adott tároló mindkét fejlécénél a [brackets] és ugyanúgy a 'Include =' soroknál. Elmúlasztása esetén az eredmény az lessz, hogy az adott tároló kimarad. Ez egy nagyon gyakori hiba.

##### Csomagtárolók (repositories)

Egy software repository az egy tárhely ahonnan a csomagok letölthetők és telepíthetők a számítógpre. Az Arch Linux csomagfenntartói és fejlesztői [package maintainers](/index.php/Package_Maintainer "Package Maintainer") (developers and [Trusted Users](/index.php/Trusted_Users "Trusted Users")) fenntartanak egy adott számú csomagtárolót amik tartalmaznak alapvető és népszerű szoftwereket,és könnyedén elérhetőek a [pacman](/index.php/Pacman "Pacman")-számára. Ez a cikk körvonalazza ezeket a hivatalosam támogatott tárolókat. Nézd az [Official repositories](/index.php/Official_repositories "Official repositories") cikket bővebb információkért.

Sok ember szeretne használni [core], [extra] and [community] csomagokat.. Ha 32-bites csomagokat szeretnél futtatni az Arch x86_64 rendszeren akkor aktiváld a [multilib] csomagtárolót, hozzáadva az alábbi sorokat a `/etc/pacman.conf`-fájlhoz:

```
 [multilib]
 Include = /etc/pacman.d/mirrorlist

```

##### AUR

Az **[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")** (AUR) függ a közösségtől,[community] és nem támogatott, [unsupported] ágazatoktól. Ellentétben a más ágazatoktól, a [unsupported] tartalmaz nem bináris csomagokat és nem érhető el közvetlenül a pacman-el. Ez az ágazat egy gyűjtemény, [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") shell script amit az Arch felhasználók írtak, hogy építsenek csomagokat a forrásokból az [Arch Build System](/index.php/Arch_Build_System "Arch Build System")-et használva. A nem támogatott,[unsupported] szoftverek általánosan nem elérhetők más ágazatokban. Amikor egy nem támogatott csomag összegyűjt elég népszerüségi szavazatot, áthelyezhető a közösségi [community] bináris csomagtárolóra ha egy a megbízott felhasználó [Trusted Users](/index.php/Trusted_Users "Trusted Users") hajlandó adoptálni és fenntartani ott.

**Megjegyzés:** Van egy adott számú pacman wrapper (**[AUR helpers](/index.php/AUR_helpers "AUR helpers")**) akik zökkenőmentes hozzáférést bíztosítanak az AUR-hoz.

#### /etc/pacman.d/mirrorlist

Meghatározza a pacman csomagtároló tűkroket és a prioritásokat.

**Megjegyzés:** Ha a telepítő médiumod régi, akkor a tűkörlistád (mirrorlist) elavult lehet, ami problémákhoz vezethet az Arch Linux frissítésénél pacman-el, (lásd a hibalistát [bug report](https://bugs.archlinux.org/task/22510)). Ezért fontos, hogy beszerezd a legfrissebb tűkörlistát (mirrorlist) erről a weboldalról [the pacman mirror list generator page](https://www.archlinux.org/mirrorlist/). Másold az újonnan létrehozott listát az `/etc/pacman.d/mirrorlist` fájlba a folytatáshoz.
Nyisd meg a `/etc/pacman.d/mirrorlist` fájlt egy szövegszerkesztővel és távolítsd el a # karakert attól a szervertől amelyik legközelebb található hozzád. Ezt követően add ki a teljes csomaglista frissítéséhez a parancsot: `# pacman -Syy` .

Leütve két `--refresh` vagy `-y` kényszerítjük a pacman-t, hogy frissítse az egész csomaglistát, még akkor is ha azok naprakésznek minősülnek.

A `pacman -Syy` parancsot használni (mindíg mikor a tűkörlista változik), jó dolog, és segít elkerülni az esetleges fejfájást.

#### rankmirrors

Esetlegesen használhatsz `rankmirrors`-okat. A `rankmirrors` egy shell script ami segít észlelni azokat az aktívra állított tűkröket a `/etc/pacman.d/mirrorlist` fájlban amelyek a legközelebb állnak a telepítő számítógéphez a telepítési idő alatt. A gyorsabb tűkrök nagymértékben tókéletesítik a pacman teljesítményét és a teljes Arch Linux tapasztalatot. Ez a script futtatható periódikusan, különosen ha a választott tűkör inkonzisztens teljesítményt nyújt. Nem árt megjegyezni, hogy a `rankmirrors` nem teszteli a teljesítményt. Azok az ezközök mint például a `wget` vagy `rsync` használhatóak hatékonyan tükrök tesztelésére miután az új `/etc/pacman.d/mirrorlist` fálj létrejött.

Használjuk a következő parancsot, hogy teljesen frissítsük az adatbázist, upgrade-elni és telepíteni `curl`

 `# pacman -Syyu curl` 

*   *Ha ebben a lépésben hibát kapunk használjuk a `nano /etc/pacman.d/mirrorlist` parancsot és tegyük aktívvá (távolítsuk el a # karaktert) a hozzánk illő szervert.*

`cd` a `/etc/pacman.d/` könyvárhoz:

 `# cd /etc/pacman.d` 

Csinájunk mentést a már létező `/etc/pacman.d/mirrorlist` fájlból:

 `# cp mirrorlist mirrorlist.backup` 

Nyissuk meg a mirrorlist.backup-ot és tegyük aktivvá az összes tükröt a kontinensünkön illetve a földrajzi környezetünkhöz közel állókat, hogy teszteljük a rankmirrorr-al:

 `# nano mirrorlist.backup` 

Futtassuk újra a mirrorlis.backup fájlt a -n opcióval és irányítsuk a kimenetet az új /etc/pacman.d/mirrorlist fájlba:

 `# rankmirrors -n 6 mirrorlist.backup > mirrorlist` 
**Megjegyzés:** A **-n 6** opció: rangsorolja a 6 legközelebbi tükört.

Kényszerítsük a packan-t, hogy frissítse az összes csomaglistát az új tűkörlistával:

 `# pacman -Syy` 

##### Tűkörellenörzés naprakész csomagokért

Mivel a `rankmirrors` nem veszi figyelembe, hogy a tükrök mennyire naprakészek, fontos megjegyeznünk, hogy egy vagy több tűkör a kiválasztottak közül elavult lehet. Az [Arch Linux MirrorStatus](https://www.archlinux.org/mirrors/status/) jelentéseket ad külömböző szempontok szerint a tükrökről mint például a tükrök hálózati problémáiról, adatgyüjtés hibákról, az utolsó alkalomról amikor a tükör szinkronizálva lett, stb. Egyesek kérhetik, hogy manuálisan ellenőrizd a `/etc/pacman.d/mirrorlist`-et, biztosítva, hogy a fálj csak naprakész tükröket tartalmaz és a legfissebb csomagok prioritást élveznek.

Esetlegesen, a [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) rangsorolhatja a tükröket automatikusan a hozzánk közel álló és naprakész szempontok szerint.

**Megjegyzés:** A scriptről amely automatizálja a processzt hogy beszerezze és telepítse a `mirrorlist` fájlt a Pacman Mirrorlis Generátorból, olvass a [Mirrors](/index.php/Mirrors#Script_to_automate_use_of_Pacman_Mirrorlist_Generator "Mirrors") oldalon.

**Megjegyzés:** Néhány problémát jelentettek a [Arch Linux forums](https://bbs.archlinux.org/) oldalon tekintettel a hálózati probémákra amelyek megakadályozzák a pacman-t a csomagtárolók frissítésében/szinkronizálásában lásd [https://bbs.archlinux.org/viewtopic.php?id=68944](https://bbs.archlinux.org/viewtopic.php?id=68944) és [https://bbs.archlinux.org/viewtopic.php?id=65728](https://bbs.archlinux.org/viewtopic.php?id=65728) oldalakat). Amikor natívan telepítjük az Arch-ot, ezek a problémák megoldódnak az alapértelmezett pacman fáljletöltő kicserélésével egy alternatív fáljletöltőre. (lásd [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance") a további információkért) Amikor az Arch-ot vendég operációs rendszerként telepítjük a [VirtualBox](/index.php/VirtualBox "VirtualBox") -ba, ez a probléma megoldható használva a "Host interface" helyett a "NAT"-ot a gép beállításainál.

#### Barátkozzunk meg a pacman-el

A pacman az Arch felhasználók legjobb barátja. Nagyon ajánlott tanulmányozni és megtanulni hogyan is kell használni a pacman ezközt. Próbáld:

 `$ man pacman` 
**Megjegyzés:** Ha olyan szöveg sorokat találsz amik túl hosszúak és nem átláthatóak a képernyőn, akkor kexprortálható a `$MANWIDTH` környezeti változó és készíthetsz egy `.profile` fájlt a root mappádba a következő bejelentkezéshez: `# export MANWIDTH=80` 

Több információért lásd a [pacman](/index.php/Pacman "Pacman") wiki bejegyzést a szabadidődben, vagy nézt át a [pacman rosetta](/index.php/Pacman_rosetta "Pacman rosetta") bejegyzést ahol összehasonlítódik más népszerű csomagkezelőkkel.

#### Frissítsük a rendszert

{{Figyelmeztetés|1=A frissítést fogozott figyelemmel, és óvatossággal kell végezni. Nagyon fontos, hogy elolvassuk ezt [this](https://bbs.archlinux.org/viewtopic.php?id=57205) mielőtt frissítenénk. A rendszerfrissítéshez olvasd a [news](https://www.archlinux.org/news/) (és opcionálisan a [announce mailing list](https://archlinux.org/pipermail/arch-announce/) oldalt.) Gyakran a fejlesztők fontos információkat nyújtanak a kötelező beállításokról és modifikációkról az észlelt problémákhoz. Az Ach Linux felhasználó konzultálhat ezekkel az oldalakkal mielőtt végigmegy a rendszerfrissítésen.

Szinkronizáld, frissítsd és rendszerfrissítsd az egész rendszert a következő paranccsal:

 `# pacman -Syu` 

vagy:

 `# pacman --sync --refresh --sysupgrade` 

A pacman most le fog tölteni egy friss másolatot a mester csomag listáról, azokról a szerverekről amiket definiáltunk a `/etc/pacman.conf` és véghezvisz minden elérhető rendszerfrissítést. A rendszer lehet kérni fogja, hogy a pacman önmagát is frissíthe ennél a pontnál. Ilyenkor adjuk neki az igen választ aztán újra írjuk be a `pacman -Syu` parancsot, hogy befejezze a rendszerfrissítést.

Ha kernel frissítés esetén újra kell indítani a rendszert.

**Note:** Néha, a beéllítások módosításához a felhasználó is jelen kell legyen a frissítésnél; olvasd a pacman kimenetét az erre vonatkozó információkért. További információért lásd a [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") oldalt.

A pacman kimenete lementődik automatikusan a `/var/log/pacman.log` fájlba. Lásd a [Package Management FAQ](/index.php/FAQ#Package_Management "FAQ") oldalt a GYIK-ért a rendszerfrissítéssel és szoftverkezeléssel kapcsolatban.

##### Ignoring Packages

After executing the command `pacman -Syu`, the entire system will be updated. It is possible to prevent a package from being upgraded. A typical scenario would be a package for which an upgrade may prove problematic for the system. In this case, there are two options; indicate the package(s) to skip in the pacman command line using the --ignore switch (`pacman -S --help` for details) or permanently indicate the package(s) to skip in the `/etc/pacman.conf` file in the IgnorePkg array. For more information, please see the [pacman](/index.php/Pacman "Pacman") wiki entry.

Please note that the power user is expected to keep the system up to date with pacman -Syu, rather than selectively upgrading packages. You may diverge from this typical usage as you wish; just be warned that there is a greater chance that things will not work as intended and that it could break your system. The majority of complaints happen when selective upgrading, unusual compilation or improper software installation is performed. Use of **IgnorePkg** in `/etc/pacman.conf` is therefore discouraged, and should only be used sparingly, if you know what you are doing.