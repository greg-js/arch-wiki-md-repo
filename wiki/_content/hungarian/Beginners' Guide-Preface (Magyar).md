**Tip:** Ez az oldal a teljes Beginners' Guide (Magyar) útmutató egyik részoldala. Ha az útmutatót teljes egészében akarod olvasni, akkor **[kattints ide](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)")**.

## Contents

*   [1 Előszó](#El.C5.91sz.C3.B3)
    *   [1.1 Bevezetés](#Bevezet.C3.A9s)
    *   [1.2 Szerződés](#Szerz.C5.91d.C3.A9s)
    *   [1.3 Az Arch filozófia](#Az_Arch_filoz.C3.B3fia)
    *   [1.4 Az útmutatóról](#Az_.C3.BAtmutat.C3.B3r.C3.B3l)

## Előszó

### Bevezetés

Üdvözöllek. Ez a dokumentum végigvezet az [Arch Linux](/index.php/Arch_Linux "Arch Linux") telepítési lépésein: amely egy egyszerű és könnyed [GNU](/index.php/GNU_Project "GNU Project")/Linux disztribúció. Ez az útmutató elsősorban az új Arch felhasználókat célozza meg, de igyekszik egy jól használható tudásbázist nyújtani mindenkinek.

Mielőtt belevágnánk, kérlek tekintsd meg a leggyakrabban feltett kérdéseket: [FAQ](/index.php/FAQ "FAQ").

**Az Arch Linux Disztribúció Alapelvei:**

*   [Egyszerű](/index.php/The_Arch_Way "The Arch Way") tervezés és filozófia
*   [Minden csomag](https://www.archlinux.org/packages/?q=) elérhető [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)") és [x86_64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") architektúrákra
*   A [Rolling release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") modell lehetővé teszi a rendszer egyszeri installálása utáni folyamatos frissítését a legújabb stabil csomagokra. Így nincs szükség időközi disztribúciófrissítésre, hiszen a rendszer frissen tartása folyamatosan történik.
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") egy egyszerű és dinamikus [initramfs](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd") készítő
*   A [Pacman](/index.php/Pacman "Pacman") [csomagkezelő](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") könnyed, gyors, és kevés memóriát fogyaszt
*   Az [Arch Build System](/index.php/Arch_Build_System "Arch Build System") (röviden ABS) egy port-szerű csomagkészítő rendszer, melynek segítségével forráskódból készíthetünk installálható Arch csomagokat.
*   Az [Arch Közösségi Tároló](/index.php/Arch_User_Repository "Arch User Repository")-ban a közösség tagjai által készített több ezer csomag érhető el, valamint lehetőséget ad az általad készített csomagok megosztására is.

### Szerződés

Az Arch Linux, a pacman, a dokumentáció, és a szkriptek © 2002-2007 Judd Vinet és © 2007-2012 Aaron Griffin szerzői jogát képzik és a [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html) licensz alá tartoznak.

### Az Arch filozófia

_**Az Arch mögött álló tervezési elvek lényege az [egyszerűség](/index.php/The_Arch_Way_(Magyar) "The Arch Way (Magyar)").**_

'Egyszerű', ebben az összefüggésben azt jelenti, hogy 'felesleges kiegészítések, módosítások, vagy komplikációk' nélkül. Röviden, egy elegáns, minimalista megközelítést takar.

**Néhány idézet ezen egyszerűség könnyebb megértésére :**

*   _"Az egyszerűség technikai, nem pedig a könnyed használhatóság szempontjából értendő. Jobb egy hosszabb tanulási folyamat során nagyobb technikai tudásra szert tenni, mint tudatlanul, de könnyű kezelhetőség mellett technikailag butának maradni ." -Aaron Griffin_
*   _Entia non sunt multiplicanda praeter necessitatem_ vagy "Entities should not be multiplied unnecessarily." -Occam's razor. A _razor_ kifejezés arra utal, hogy söpörjünk félre minden szükségtelen bonyolítást azért, hogy a legegyszerűbb magyarázathoz, módszerhez eljuthassunk.
*   _"A módszerem rendkívüli része annak egyszerűségében rejlik. A nagy művek mindig az egyszerűségből születnek."_ - _Bruce Lee_

### Az útmutatóról

Az [Arch telepítő szkriptek](https://github.com/falconindy/arch-install-scripts) az Arch Linux telepítését megkönnyítő szkripteket jelentik. Ez az útmutató összefoglalóan bemutatja az alaprendszer telepítését ezen szkriptek használatával.

Ez a közösség által karbantartott [Arch wiki](/index.php/Main_Page_(Magyar) "Main Page (Magyar)") remek forrás és először itt érdemes tanácsot kérni a felmerülő kérdésekre. Az [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") csatorna ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) az [angol fórum](https://bbs.archlinux.org/) és a [magyar fórum](http://archlinux.hu/forum) ugyan csak elérhető, ha a válasz máshol nem található. Ezek mellett olvasgasd a `man` oldalakat minden olyan paranccsal kapcsolatban, amelyek még ismeretlenek számodra; ezt legkönnyebben a terminálba beírva a következő módon teheted meg: `man _parancs_`.

**Megjegyzés:** Az útmutató követése közel létfontosságú a jól konfigurált Arch Linux sikeres telepítéséhez, tehát _kérlek_ olvasd át alaposan. Erősen ajánlott minden egyes részt végigolvasása <u>mielőtt</u> bármilyen feladatba kezdenél.

Az útmutató öt fő részre osztható fel:

*   [Első rész: Előkészületek](/index.php/Beginners%27_Guide/Preparation_(Magyar)#El.C5.91k.C3.A9sz.C3.BCletek "Beginners' Guide/Preparation (Magyar)")
*   [Második rész: Telepítés](/index.php/Beginners%27_Guide/Installation_(Magyar)#Telep.C3.ADt.C3.A9s "Beginners' Guide/Installation (Magyar)")
*   [Harmadik rész: Telepítés után](/index.php/Beginners%27_Guide/Post-Installation_(Magyar)#Telep.C3.ADt.C3.A9s_ut.C3.A1n "Beginners' Guide/Post-Installation (Magyar)")
*   [Negyedik rész: Extra](/index.php?title=Beginners%27_Guide/Extra_(Magyar)&action=edit&redlink=1 "Beginners' Guide/Extra (Magyar) (page does not exist)")
*   [Ötödik rész: Függelék](/index.php?title=Beginners%27_Guide/Extra_(Magyar)&action=edit&redlink=1 "Beginners' Guide/Extra (Magyar) (page does not exist)")

**[Útmutató kezdőknek](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)")**

* * *

**Előszó** >> [Előkészületek](/index.php/Beginners%27_Guide/Preparation_(Magyar) "Beginners' Guide/Preparation (Magyar)") >> [Telepítés](/index.php/Beginners%27_Guide/Installation_(Magyar) "Beginners' Guide/Installation (Magyar)") >> [Telepítés után](/index.php/Beginners%27_Guide/Post-Installation_(Magyar) "Beginners' Guide/Post-Installation (Magyar)") >> [Extra/Függelék](/index.php?title=Beginners%27_Guide/Extra_(Magyar)&action=edit&redlink=1 "Beginners' Guide/Extra (Magyar) (page does not exist)")