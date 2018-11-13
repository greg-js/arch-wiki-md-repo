Az Arch Linux egy függetlenül fejlesztett, [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")/[x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") architektúrára épülő általános célú GNU/Linux disztribúció, ami elég sokoldalú ahhoz, hogy alkalmas legyen bármilyen szerepre. A fejlesztés az egyszerűségre, minimalizmusra és kódhelyességre fókuszál. Az Arch egy minimális alaprendszerként települ, és a felhasználó állítja be, aki csak az egyéni céljaira szükséges vagy kívánatos dolgokat telepítve összeállítja a számára ideális környezetet. Nincsenek hivatalos GUI-val ellátott konfigurációs eszközök, és a legtöbb rendszerbeállítás a parancssorból vagy szövegszerkesztőből végrehajtható. Rolling-release modellen alapulva az Arch törekszik arra, hogy bleeding edge maradjon, és jellemzően a szoftverek legújabb verzióit kínálja.

## Contents

*   [1 Történet](#Történet)
*   [2 Egyszerűség](#Egyszerűség)
*   [3 Korszerűség](#Korszerűség)
*   [4 Szoftvercsomagolás](#Szoftvercsomagolás)
*   [5 Forrásintegritás](#Forrásintegritás)
*   [6 Közösség](#Közösség)
*   [7 Összefoglalás](#Összefoglalás)

## Történet

	*Fő cikk: [Arch Linux története](/index.php/History_of_Arch_Linux "History of Arch Linux")*

Az Arch Linuxot Judd Vinet kanadai programozó alapította. Az első kiadása, az Arch Linux 0.1, 2002\. március 11-én jelent meg. Habár az Arch teljesen független, ihletet merít más disztribúciók egyszerűségéből, beleértve a [Slackware-t](http://slackware.com), a [CRUX-ot](http://www.crux.nu) és a [BSD-t](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"). 2007-ben Judd Vinet elhagyta a projektvezetői státuszt egyéb érdekeltségek miatt, és Aaron Griffin amerikai programozó vette át, aki folytatta a projekt vezetését napjainkig.

## Egyszerűség

[Az Arch Módszert](/index.php/The_Arch_Way_(Magyar) "The Arch Way (Magyar)") követve az Arch Linux könnyed, rugalmas, egyszerű, és célja, hogy nagyon UNIX-szerű legyen. Telepítés után egy, az i686/x86-64 architektúrákra fordított minimális környezetet (GUI nélkül) nyújt: a szükségtelen és felesleges csomagok kigyomlálása helyett a felhasználó megkapja a lehetőségét, hogy egy minimális alapról építkezzen bármiféle előzetesen kiválasztott alapértelmezés nélkül. Az Arch tervezési filozófiája és implementációja könnyedén lehetővé teszi, hogy kibővíthető és alakítható legyen bármilyen fajta rendszerré a minimalista konzolgéptől az elérhető leghatalmasabb és funkciókban gazdag asztali környezetig: *a felhasználó* az, aki eldönti, mi lesz az ő Arch rendszere.

## Korszerűség

Az Arch Linux törekszik arra, hogy szoftverei legújabb stabil verzióit tartsa karban mindaddig, amíg a rendszerszintű csomagtörés még ésszerűen elkerülhető. [Rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") rendszeren alapul, ami lehetővé teszi az egyszeri telepítést folyamatos frissítésekkel, újratelepítés szükségessége, és a bonyolult műveletek végrehajtása nélkül, ami az egyik kiadott verzióról a következőre történő rendszerfrissítés során jelentkezik. Egyetlen parancs kiadásával az Arch Linux frissen tartható, és bleeding edge marad.

Az Arch a GNU/Linux felhasználók számára elérhető funkciók sokaságát tartalmazza, beleértve a [systemd](/index.php/Systemd "Systemd") init rendszert, korszerű fájlrendszereket (Ext2/3/4, Reiser, XFS, JFS, BTRFS), LVM2-t, szoftver RAID-et, udev támogatást és initcpio-t ([mkinitcpio-val](/index.php/Mkinitcpio "Mkinitcpio")), valamint a legújabb elérhető kernelt.

## Szoftvercsomagolás

Az Arch egy könnyen használható bináris [csomagkezelőre](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager"), a [pacmanra](/index.php/Pacman "Pacman") támaszkodik, ami lehetővé teszi az egész rendszer frissítését egyetlen paranccsal. A pacmant *C* nyelven írták, és az alapjaitól könnyednek, egyszerűnek és nagyon gyorsnak tervezték. Az Arch biztosít egy ports-szerű rendszert, az [Arch Build Systemet](/index.php/Arch_Build_System "Arch Build System") is, hogy egyszerűvé tegye csomagok forrásból történő építését és telepítését, és szintén egyetlen paranccsal szinkronizálható. Akár az egész rendszer újraépíthető egyetlen paranccsal.

Az i686 és x86-64 architektúrák támogatásával az Arch [hivatalos tárolói](/index.php/Official_repositories "Official repositories") több ezer magas minőségű csomagot nyújtanak, hogy megfeleljenek a szoftverigényeknek. Ezen túlmenően az Arch ösztönzi a közösség növekedését és hozzájárulását az [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") felkínálásával, ami sok ezer, felhasználók által karbantartott PKGBUILD szkriptet tartalmaz telepíthető csomagok forrásból történő fordításához a *makepkg* alkalmazás használatával. Szintén lehetséges, hogy a felhasználók egyszerűen építsék és tartsák karban saját egyéni tárolóikat.

## Forrásintegritás

Az Arch foltozás nélküli vanilla szoftvereket nyújt; a csomagokat a tiszta [upstream](https://en.wikipedia.org/wiki/upstream_(software_development) forrásokból nyújtja, ahogy a szerző eredetileg szánta terjesztésre. Foltozás csak rendkívül kivételes esetben történik, hogy megakadályozzon erős töréseket, például verzióeltérések esetén, ami előfordulhat egy rolling release modellben.

## Közösség

Az Arch közösség nagyon megbízható, élénk és barátságos: minden Arch felhasználót arra ösztönzünk, hogy vegyen részt, és járuljon hozzá a disztribúcióhoz, segítve akár az alapszoftver fejlesztését, csomagok karbantartását, [hibák](https://bugs.archlinux.org/) jelentését vagy javítását, az [ArchWiki dokumentáció](/index.php/Main_page_(Magyar) "Main page (Magyar)") javítását, segítve más felhasználóknak problémáik megoldásában, vagy csak véleménycserével a [fórumokban](https://bbs.archlinux.org/), [levelezőlistákon](https://mailman.archlinux.org/mailman/listinfo/), [IRC csatornákon](/index.php/IRC_channels "IRC channels"), vagy megosztva a saját ismereteiket vagy akár saját fejlesztésű alkalmazásaikat. Az Arch Linux a választott operációs rendszere számos embernek a világon, és számos [nemzetközi közösség](/index.php/International_communities "International communities") létezik, akik segítséget kínálnak és dokumentációt nyújtanak több nyelven.

Lásd a [Vegyél részt benne!](/index.php/Getting_involved "Getting involved") lapot, ha úgy érzed, hogy szeretnél a közösség aktív tagja lenni.

## Összefoglalás

Összefoglalva: az Arch Linux egy sokoldalú és egyszerű disztribúció, amit úgy terveztek, hogy illeszkedjen a hozzáértő Linux® felhasználó igényeihez. Egyszerre erőteljes és könnyen kezelhető, így ideális disztribúció a szerverek és munkaállomások számára. Alakítsd bármilyen irányba, ahogy tetszik: ha osztod ezt az elképzelést, amilyennek egy GNU/Linux disztribúciónak lennie kell, akkor köszöntünk, és arra ösztönzünk, hogy használd szabadon, vegyél részt benne, és járulj hozzá a közösséghez. Üdvözlünk az Arch-nál!