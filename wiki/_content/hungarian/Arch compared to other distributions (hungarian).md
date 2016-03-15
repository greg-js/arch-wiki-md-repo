| **Summary**  |
| Ez a cikk röviden összefoglalja az Arch Linux és más GNU/Linux disztribúciók közti hasonlóságokat és különbségeket. |
| **Kapcsolódó cikkek** |
| [Arch Linux](/index.php/Arch_Linux "Arch Linux") |
| [The Arch Way](/index.php/The_Arch_Way "The Arch Way") |
| **Külső linkek** |
| [DistroWatch.com](http://distrowatch.com/) |

Ez az oldal megpróbálja felvázolni az Arch Linux és más népszerű GNU/Linux disztribúciók, illetve <tt>UNIX</tt>-szerű operációs rendszerek közti hasonlóságokat és különbségeket. A következő leírások csak rövid összefoglalók, melyek célja, hogy segítsen az olvasónak eldönteni, hogy az Arch Linux megfelel-e igényeinek. Még ha ezek az összefoglaló törekednek is a minél jobb leírásra, a döntést a rendszer tényleges kipróbálása után érdemes meghozni.

## Contents

*   [1 Forráskód alapú disztribúciók](#Forr.C3.A1sk.C3.B3d_alap.C3.BA_disztrib.C3.BAci.C3.B3k)
    *   [1.1 Gentoo](#Gentoo)
    *   [1.2 Sorcerer/Lunar-Linux/Source Mage](#Sorcerer.2FLunar-Linux.2FSource_Mage)
*   [2 Minimalista](#Minimalista)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 Grafikus](#Grafikus)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Mandriva](#Mandriva)
    *   [3.4 openSUSE](#openSUSE)
    *   [3.5 PCLinuxOS](#PCLinuxOS)
*   [4 A *BSD-k](#A_.2ABSD-k)
    *   [4.1 FreeBSD](#FreeBSD)
    *   [4.2 NetBSD](#NetBSD)
    *   [4.3 OpenBSD](#OpenBSD)
*   [5 Egyéb](#Egy.C3.A9b)
    *   [5.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [5.2 Frugalware](#Frugalware)

## Forráskód alapú disztribúciók

A forráskód alapú disztribúciók legnagyobb előnye rugalmasságuk, hiszen a rendszer teljesen személyre szabható azáltal, hogy az egész operációs rendszer, valamint az alkalmazások a konkrét számítógép-architektúrára, és a felhasználási igényeknek megfelelően kerülnek telepítésre. Hátrányt jelent azonban a forráskódból való fordítás időigényes volta. Az Arch Linux és összes csomagja kifejezetten i686 és x86-64 architektúrájú számítógépekre készülnek. Így más i386/i486/i586 alapú bináris disztribúciókkal szemben nagyobb teljesítményt biztosítanak, és egyszerűen telepíthetők.

### Gentoo

Mind az Arch Linux, mind a Gentoo "rolling release" típusú disztribúciók, ami azt jelenti, hogy az egyes csomagok röviddel azután megjelennek a disztribúció tárolóiban, hogy a fejlesztők kiadják a programot. A Gentoo csomagok és az alaprendszer is forráskód formájában elérhető, azaz fordítással kerülnek telepítésre a számítógépre, aminek folyamatát a felhasználó az ún. "USE-flag"-ek segítségével befolyásolhatja. Az Arch Linux lehetőséget ad hasonlóan forrásból való telepítésre, de alapvetően úgy tervezték, hogy előre lefordított binárisoból telepítsék a rendszert. Emiatt az Arch Linux rendszer felépítése és karbantartása sokkal gyorsabb folyamat, ugyanakkor a Gentoo Linux rendszer egységes személyre szabása jóval egyszerűbb. Az Arch hivatalosan az i686 és x86-64, míg a Gentoo az x86, ppc, sparc, alpha, amd64, arm, mips, hppa, s390, sh, és itanium architektúrákat támogatja. Mivel a Gentoo és az Arch telepítője is csak egy alaprendszert telepít, így mindkettő nagymértékben személyre szabható. A Gentoot használók az Arch Linux-szal is jól meglesznek.

### Sorcerer/Lunar-Linux/Source Mage

Sorcerer/Lunar-Linux/Source Mage (SLS) mind forráskód alapú disztribúciók, amik eredtileg egy projektként indultak. Az SLS disztrók egyszerű script fájlokat használnak a csomagleírások készítéséhez, a fordítás beállításait pedig egy globális konfigurációs fájlban tárolják, ami nagyon hasonló az [Arch Build System](/index.php/Arch_Build_System "Arch Build System") logikájához. Az SLS telepítő eszközei teljes függőségi vizsgálatot végeznek (opcionális lehetőségeket is támogatnak), és a csomagok követése, eltávolítása és frissítése is elvégezhető velük. Nincsenek bináris csomagok ezen disztribúciókhoz. Előnyük, hogy könnyen vissza lehet térni régebbi verziójú csomagok használatához.

A rendszer-installálás az alaprendszer telepítését jelenti terminál és ncurses menük használatával, majd ezután van lehetőség az alaprendszer újrafordítására. Az Arch-hoz hasonlóan nincs "standard" grafikus felület, és az alap telepítőben a Xorg sincs benne. Számos X server alternatíva rendelkezésre áll (X.Org 6.8 vagy 7, XFree86).

Az SLS története elég komplikált, valószínűleg a legjobb leírás a [SourceMage wiki](http://wiki.sourcemage.org/SourceMage/History)n található.

## Minimalista

A minimalista disttribúciók könnyen összehasonlíthatók az Arch-al, mert sok a hasonlóság köztük: mindegyiket technikai szempontból egyszerűnek tekintik.

### LFS

Az LFS (vagy teljes nevén: Linux From Scratch) valójában csak egy dokumentáció. A könyv instrukciókat ad arra, hogy a felhasználó hogyan tud a semmiből, alapvető rendszercsomagok telepítése segítségével létrehozni egy működő GNU/Linux OS-t, majd frissíteni és beállítani azt. Az Arch alaprendszerként ugyanezen csomagokat nyújtja, plusz néhány extra eszközt, köztük a rendkívül hatékony [pacman](/index.php/Pacman "Pacman") csomagkezelőt, mindet i686/x86_64-re lefordítva. Az LFS-nek nincsenek online tárolói, a forrásokat különböző helyekről kell megszerezni, majd 'make' segítségével lefordítani és telepteni. (Csomagkezelésre számos manuális megoldás létezik, melyeket az LFS dokumentum megjegyzései közt meg lehet találni.) A minimailsta Arch Linux rendszer mellett az Arch közösség csomagok ezreit tartja karban, melyeket a pacman csomagkezelő segítségével lehet telepíteni. Emellett ún. [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") szkriptek is elérhetők, amik az [Arch Build System](/index.php/Arch_Build_System "Arch Build System")-mel használhatók ki. Az Arch tartlmazza a [makepkg](/index.php/Makepkg "Makepkg") eszközt is, ami `.pkg.tar.xz` kiterjesztésű csomagok létrehozását és módosítását teszi lehetővé, amik utána pacman-nel egyszerűen telepíthetők. Judd Vinet és az LFS-hez hasonlóan építette fel rendszerét, majd C-ben megírta a pacman-t. Régebben poénból gyakran emlegették az Arch-ot úgy, mint egy "Linux, okos csomagkezelővel."

### CRUX

Az Arch egy teljesen függtelenül fejlesztett rendszer, egy másik GNU/Linux disztribúció sem képezi alapját. Az Arch elkészítése előtt maga Judd Vinet is a Crux-ot használta, ami egy Per Lidén által fejlesztett minimalista disztró. Annak idején az Arch elkészítését a Crux inspirálta, teljesen a nulláról kezdték felépítését, majd C-ben megírták hozzá a pacman-t. A két rendszer hasonló alapelveket vall: mindkettő architektúra-optimalizált, minimalista és a K.I.S.S. elvét követi. Mindkettő előre portolt rendszert használ, *BSD stílusú init-tel, és a BSD-khez hasonlóan csak egy alaprendszert kínál, amire később építkezni lehet. Az Arch csomagkezelője a pacman, ami bináris csomagokat használ, és jól együttműködik az [Arch Build System](/index.php/Arch_Build_System "Arch Build System")-mel. A Crux egy közösség által létrehozott csomagkezelőt, a 'prt-get'-et használja, ami kezeli a függőségeket, és a csomagokat forrásból telepíti (maga a Crux alaprendszer azonban i686 binárisként települ). Az Arch hivatalosan x86-64 és i686 architektúrákat támogatja, míg a Crux csak i686-ot.

Az Arch 'rolling-release' rendszer, és sok csomagot tartalmazó tárolókkal rendelkezik, ami kiegészít a felhasználók által fenntartott [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). A Crux-nak mind a hivatalos, mind a közösségi tárolója szerényebb méretű.

### Slackware

A Slackware és az Arch nagyon hasonlítanak abban, higy mindkettő egyszerűnek titulált disztribúció abban a tekintetben, hogy az eleganciára és minimalizmusra koncentrálnak. Slackware híres arról, hogy módosítás nélkül használ fel rendszerében minden programot, a kernelen kívül. Az Arch tipikusan csak akkor módosít, ha súlyos hibák merülnek fel, vagy anélkül nem lehet lefordítani a forrást. Mindkettő BSD-stílusú init-szkripteket használ. Az Arch fejlett csomagkezlő rendszere, a pacman, a Slackware eszközeivel ellentétben, automatikus függőség-kezelést és könnyebb rendszerfrissítést biztosít. A Slackware használói általában preferálják az ő manuális függőségkezelésük, ami nagyfokú befolyást tesz lehetővé. Az Arch rolling-release disztró. A Slackware ilyen szempontból konzervatívabb, hiszen adott időközöként adnak ki frissítéseket, előnyben részesítve így a stabilnak bizonyult csomagok kiadását. Ilyen szempontból az Arch naprakészebb. Az Arch hivatalos tárolói csomagok ezreit biztosítják, a Slackware tárolói valamivel szegényebbek. Az Arch esetében még ott van az [Arch Build System](/index.php/Arch_Build_System "Arch Build System") és az [AUR](/index.php/AUR "AUR") is, amelyek nagyszámú PKGBUILD-eket biztosítanak, főleg felhasználóknak köszönhetően. A Slackware esetében is van hasonló kezdeményezés, mely elérhető a [slackbuilds.org](http://www.slackbuilds.org) oldalon, és egy olyan félhivatalos tároló, mely az Arch-féle PKGBUILD-ekhez nagyon hasonló Slackbuild-eket tárolja. A Slackware felhasználók valószínűleg könnyen megbarátkoznak az Arch-al is.

## Grafikus

Gyakran "újonc" disztribúcióknak is hívják őket, hisz a legújabb generációt képviselik. Sok köztük a hasonlóság, az Arch-tól azonban számos dologban eltérnek. Az Arch akkor jobb választás, ha szeretnél a GNU/Linux rendszerekről sokmindent megtanulni azáltal, hogy egy minimális alapról kell a rendszeredet felépíteni, hiszen a grafikus disztrókhoz mérten csak nagyon kevés dolog települ alapból. A grafikus disztribúciók általában grafikus telepítővel rendelkeznek (pl. az Anaconda a Fedora esetében), és a rendszerbeállítások többségére is rendelkezésre áll valamilyen grafikus felületű program (pl. a YaST a SUSE esetében). A lényegesebb különségek a grafikus disztrók között a folytatásban kerülnek tárgyalásra.

### Ubuntu

Az Ubuntu egy nagyon népszerű, Debian-alapú, a Canonical által üzletileg támogatott disztribúció, míg az Arch független. A két projektnek eltérő céljai és megcélzott felhasználói bázisa van. Az Arch-ot azoknak tervezték, akik inkább a csináld-magad megközelítés hívei, míg az Ubuntu egy automatikusan beállított rendszert ad, ami ezáltal inkább ajánlott az átéagos felhasználók többségének. Ha gyorsan egy működő rendszerre van szükséged, és nem szeretnél a rendszer állítgatásával foglalkozni, az Ubuntu inkáb neked való. Az Arch sokkal minimalistább, az alaprendszer telepítése után nagyrészt a felhasználóra hárul a feladat, hogy igényeinek megfelelően alakítsa rendszerét. A fejlesztőknek az Arch jobban megfelel, de sok jelenlegi Arch felhasználó kezdte Ubuntuval a Linux-szal való ismerkedést. Az Ubntunak 6 hónaponta jelenik meg új kiadása, míg az Arch rolling-release típusú. Az Arch esetében van lehetőség forrásból való telepítésre, portolásra az [Arch Build System](/index.php/Arch_Build_System "Arch Build System")-nek köszönhetően, míg az Ubuntuban nincs. A közözzégeikben is van eltérés: az Arch közösség jóval kisebb, így nagy szükség van az aktív részvételre, ami nagy arányban igaz is. Ezzel szemben, az Ubuntu közösség relatíve nagy, így úgy is képes működni, ha a nem-aktív felhasználók aránya nagy.

### Fedora

Fedora a Red Hat disztribúcióból vált ki, és napjainkig az egyik legnépszerűbb disztribúció. A Fedora-t gyyakran tekintik úgy mint egy naprakész teszt- és kiadó-rendszer, minthogy sok Fedora csomag és projekt végül átkerül a RHEL-be (Red Hat Enterprise Linux), ahonan pedig számos disztribúció átveszi. Az Arch-ot is nagyon naprakésznek tekintik, de rolling-release, és nem képezi teszt alapját egy más disztribúciónak sem. A Fedora hatalmas közösséggel, sok előre lefordított csomaggal és széleskörű támogatással büszkélkedhet. A Fedora csomagjai RPM-ek, és a csomagkezelője a YUM. Az Arch a [pacman](/index.php/Pacman "Pacman")-t használja a tar kiterjesztésű csomagja kezelésére. A Fedora híres arról, hogy nem támogatja az mp3 formátumot bizonyos szabadalmi okok miatt. Az Arch ilyen szempontból engedékenyebb. A Fedora grafikus felületű és szöveges telepítést is lehetővé tesz. Az Arch-nak nincs grafikus telepítője, csak ncurses alapú, ami a felhasználótól több interakciót igényel. A Fedora-nak ütemezett kiadási folyamata van, míg az Arch rolling-release. Az Arch sokkal inkább az minimalista eleganciára, mint az automatizmusra koncentrál. A Fedora számos innováció elkezdője, így a közösségek körében elismert. Ilyen az SELinux integrációja, vagy a GCJ-vel fordított csomagok létrehozása, hogy megszűnjön a Sun (most már Oracle) JRE (Java Runtime Environment)-tól való függés. Emellett számos egyéb szabad szoftveres projektet támogat. A Fedora alapból sem a JFS-t sem a ReiserFS fájlrendszereket nem támogatja, míg az Arch igen.

### Mandriva

A Mandriva Linux-ot (vagy korábbi nevén Mandrake Linux-ot) 1998-ban hozták létre azzal a céllal, hogy olyan GNU/Linux disztribúció legyen, amit bárki könnyen használni tud. Ismét csak az mondható el, hogy az Arch kisebb célt tűzött ki, így szöveg alapú telepítővel rendelkezik, és jobban hagyatkozik a felhasználó tudására, így elsősorban a közepes vagy nagyobb tudással rendelkező felhasználókat célozza meg.

### openSUSE

Az openSUSE alapja az RPM csomagformátum és a méltán elismert, grafikus felületű csomagkezelője és konfigurációs eszköze, a YaST2\. Az Arch nem biztosít ilyen eszközt, mivel az az [Arch módszerrel](/index.php/The_Arch_Way "The Arch Way") ellentétes. Az OpenSUSE így inkább való kevésbé tapasztalt felhasználóknak, vagy azoknak, akik grafikus felületű eszközöket szeretnének, és jobban rászorulnak az automatikus konfigurációra.

### PCLinuxOS

A PCLinuxOS egy olyan népszerű Mandriva alapú disztribúció, mely teljes grafikus felületet kinál. Kifejezetten felhasználóbarát disztróként fejlesztik és egyszerűnek mondják, de az ő esetükben mást jelent az egyszerűség, mint az Arch Linux-nál. Az Arch egy egyszerű alaprendszer, amit az alapoktól személyre lehet szabni, így a nagyobb tudású felhasználóknak van szánva. A PCLOS az apt csomagkezelőt használja az RPM-ek kezelésére. Az Arch a saját, függetlenül fejlesztett csomagkezelője a [pacman](/index.php/Pacman "Pacman"), ami `.pkg.tar.xz` csomagokkal dolgozik. A PCLOS sokmindenhez nyújt grafikus felületet: hardverek beállítása, a Synaptic csomagkezelőt az apt frontendjeként, és gyakorlatilag egyáltalán nincs szükség shell parancsok kiadására. Az Arch parancssoros megközelítést használ, így közvetlenebb rendszerkezeléssel dolgozik. A PCLOS 256MB RAM-ot ajánl minimum rendszerkövetelményként. Az Arch ennél jóval kevesebb rendszermemóriával rendelkező PC-ken is elfut, egy i686-os telepítés esetén mindössze 64MB-ot igényel, gyorsab gépeken pedig gond nélkül fut.

## A *BSD-k

A *BSD-k mind a UC Berkeley egyetemen kifejlesztett operációs rendszer leszármazottai. A projekt célja olyan UNIX operációs rendszer készítése volt, ami szabadon terjeszthető és ingyenes. Ezek nem GNU/Linux disztribúciók, inkább <tt>UNIX</tt>-szerű operációs renszereknek lehet őket hívni. Tehát bár az Arch és a *BSD-k is nagyon hasonló elveken működnek ('ports'-rendszer, hasonló init-környezet), mégis forráskód szempontjából semmi közük egymáshoz. A *BSD-k az eredeti AT&T <tt>UNIX</tt>-kódon alapulnak, így igazi <tt>UNIX</tt> örökségnek számítanak. Ha részletesebb információt szertnél kapni a *BSD-kről, akkor látogasd meg saját weboldalaikat.

### FreeBSD

Az Arch és a [FreeBSD](http://www.freebsd.org/about.html) is lehetővé teszi a programok mind bináris csomagként való telepítését, mind forrásból való telepítését ('ports' stílusú rendszereiknek köszönhetően). Mindkettő nagyon hasonló 'init' rendszert használ. A többi *BSD-hez hasonlóan a FreeBSD-t is alapvetően úgy fejlesztik, hogy egységes egészként működjön, minden programot a FreeBSD-re portolnak, meggyőzödve helyes működésükről. Ezzel szemben a GNU/Linux disztribúciók, mint az Arch, különböző forrásokból származó egységek fúziójaként jönnek létre. Az Arch és a FreeBSD is a `/etc/rc.conf` fájlt használja globális konfigurációs fájlként. A FreeBSD licensze inkább a kód íróját védi, míg a GPL inkább magát a forráskódot. Az Arch GPL licensz alatt áll. A FreeBSD-ben is, az Arch-hoz hasonlóan, a felhasználónak kell számos dologban döntés hoznia. Ilyen szempontból talán a legérdemesebb összehasonlítani, mert fej-fej mellett haladnak, ami a csomagok frissességét és a közösség aktívságát és mértetét illeti. A két rendszer sok hasonlóságot mutat, így a FreeBSD-t használók könnyen elboldolgulnak az Arch rendszerrel is.

### NetBSD

A NetBSD egy ingyenes, biztonságos és könnyen portolható <tt>UNIX</tt>-szerű, nyílt forráskodú operációs rendszer. Több, mint 50 platformra elérhető, a 64-bites Opteron gépektől kezdve a személyi számítógépeken át a hordozható eszközökig. Az átláthatósága és fejlettsége kiváló eszközzé teszi mind az ipari mind a kutatási felhasználásokhoz. A teljes forrákódja elérhető bárki számára. Sok program gyorsan és könnyen elérhető a pkgsrc segítségével, ami a NetBSD csomaggyűjteménye (NetBSD Packages Collection). Az Arch ugyan nem érhető el annyi fajta eszközre, azonban i686 archiketúrára több programot kínál. Emellett a pkgsrc-ben a elsődleges telepítési forma a forrás letöltése és lefordítása, míg az Arch bináris csomagokat kínál. Sok hasonlóságot mutatnak egymással, például mindkettőben a `/etc/rc.conf` fájl az elsődleges konfigurációs fájl, mindkettő manuális beállítást igényel, minmalisták, ports-stílusú rendszert és bináris csoamgokat is kínálnak, és mindkettőnek aktív közössége van. Az Arch és a NetBSD is ugyanazzal az init rendszerrel működik.

### OpenBSD

Az OpenBSD projekt egy ingyenes, multi-platform, 4.4BSD alapú, <tt>UNIX</tt>-szerű operációs rendszert készít. A legfontosabb céljaik az átportolás, sztandardizálás, kódhelyesség, biztonság és integrált kriptográfia. Ezzel szemben az Arch sokkal inkább az egyszerűségre, eleganciára, minimalizmusra és naprakészségre koncentrál. Au OpenBSD támogatja számos SVR4-ről (Solaris), FreeBSD-ről, GNU/Linux-ról, BSD/OS-ről, SunOS-ről és HP-UX-ről származó program bináris emulációját. Az OpenBSD-t gyakran "a legbiztonságosabb operációs rendszerként" emlegetik.

Az Arch-hoz hasolóan az OpenBSD is egy kicsi, elegáns alap telepítését kínálja egy olyan csomagkezelő rendszerrel, mellyel könnyen telepíthető és kezelhető, az alaprendszerbe nem integrált csomagrendszert kapunk. Az Arch-hoz hasonló GNU/Linux rendszerekkel szemben, de a többi BSD rendszerhez hasonlóan, az OpenBSD kernelje és legalapvetőbb programjai (mint az ls, cp, cat és ps) együtt kerülnek fejlesztésre.

## Egyéb

Ezeket az operációs renszereket nem igazán lehet a többi kategóriába besorolni.

### Debian GNU/Linux

A Debian egy sokkal nagyobb projekt, sokkal nagyobb közösséggel. Különböző ágai vannak: "stabil" (stable), "tesztelés alatt" (testing), "nem-stabil" (unstable); így több, mint 20000 csomag érhető el. Mivel az Arch nem különíti el így a csomagjait ("-dev","-common"), így tárolói sokkal kisebbnek tűnhetnek. A Debian sokkal inkább koncentrál a szabad szoftverek használatára, míg az Arch engedékenyebben kezeli a GNU által "nem-szabad" szoftverként definiált programokat. A Debiannak sokkal inkább célja a stabilitás és a szigorú tesztelés. Az Arch inkább az egyszerűség és minimalizmus filozófiájára koncentrál, és így sokkal naprakészebb szoftvereket kínál. Az Arch csomagjai frisebbek a Debian Testing és Stable ágánál, körülbelül az Unstable ággal egyezik meg naprakészségük. A Debian és az Arch is elismert csomagkezelő rendszert használ. Az Arch "rolling-release", míg a Debian "lefagyasztott" csomagokkal dolgozik. A Debian számos architektúrára elérhető: alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390, és sparc; míg az Arch csak i686 és x86-64-re. Az Arch jobban támogatja a külső forrásokból fordított csomagok telepítését, a "ports" stílusú renszerének köszönhetően. A Debian ilyen rendszerrel nem rendelkezik, sokkal inkább támaszkodik a saját, hatalmas mérteű, bináris tárolóira. Az Arch telepítő csak egy alaprendszert kínál, aminek telepítése végig átláthatóan történik. A Debian ennél jóval automatikusabb telepítést végez, de számos alternatív megoldással is rendelkezik. A Debian init rendszere a SysVinit, míg az Arch az egyszerűbb *BSD-stílusút használja. Az Arch a lehető legkevesebb módosítást viszi a porgramokba, hogy ne hozzanak létre olyan csomagokat, amik forrását az eredeti fejlesztők már nem tudják átlátni.

### Frugalware

Az Arch szöveges alapú, parancssoros megközelítést használ. A Frugalware átvette az Arch csomagkezelőjét, a [pacman](/index.php/Pacman "Pacman")-t, de bzip tömörítésű tar csomagokat használ. Az Arch xz tömörített (lzma) tar fájlokat használ a telepítés egyszerűsége érdekében. A Frugalware alapból nem támogatja a JFS fájlrendszert. A Frugalware már nem a Slackware-n alapuló disztribúció, mostanra önállóvá vált, és alapvetően i686 architektúrára készül. Az Arch alapvetően más megközelítést használ, hisz csak egy alaprendszer települ, és a pacman segítségével az kerül bővítésre a felhasználó igényeinek és döntéseinek megfelelően. A Frugalware telepítője DVD méretű, már előre kiválasztott grafikus környezettel (DE - Desktop Environment) és programokkal. A Frugalware-nek ütemezett kiadásai vannak. Ismét csak az mondható el, hogy az Arch sokkal inkább koncentrál az egyszerűségre, minimalizmusra, kódhelyességre és naprakész csomagokra, ahogy ezt a rolling-release megköveteli.