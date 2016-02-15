A következő öt alapelv magába foglalja mindazt, amit általában az Arch Módszernek vagy Arch Filozófiának hívnak, és talán legjobban a KISS mozaikszóval lehet összegezni, azaz Keep It Simple, Stupid.

## Contents

*   [1 Egyszerűség](#Egyszer.C5.B1s.C3.A9g)
*   [2 Kódhelyesség kényelem felett](#K.C3.B3dhelyess.C3.A9g_k.C3.A9nyelem_felett)
*   [3 Felhasználóközpontúság](#Felhaszn.C3.A1l.C3.B3k.C3.B6zpont.C3.BAs.C3.A1g)
*   [4 Nyíltság](#Ny.C3.ADlts.C3.A1g)
*   [5 Szabadság](#Szabads.C3.A1g)

## Egyszerűség

_Az egyszerűség a végső kifinomultság._ – Leonardo da Vinci

Az egyszerűség az Arch fejlesztésének legfőbb célja. Sok GNU/Linux disztribúció titulálja magát „egyszerűnek”, viszont az egyszerűségnek sok definíciója van.

**Az Arch Linux _szükségtelen kiegészítések, módosítások vagy bonyolítások nélküliként_ határozza meg az egyszerűséget, és egy könnyed, <tt>UNIX</tt>-szerű alapszerkezetet biztosít, ami lehetővé teszi az egyes felhasználók számára, hogy maguk formálják meg rendszerüket a saját igényeiknek megfelelően. Röviden: egy elegáns, minimalista felfogás.**

Egy magas szintű programozási szabványokon alapuló könnyed alapszerkezet jellemzően kevesebb rendszererőforrást igényel. Az alaprendszer mentes minden zavartól, ami elhomályosítaná a rendszer lényeges részeit, vagy megnehezítené, túlbonyolítaná a hozzáférést. Tömör magyarázattal ellátott konfigurációs fájlok rendezett sora áll rendelkezésre, amelyek a gyors elérést és szerkesztést figyelembe véve lettek elhelyezve. Nincsenek nehézkes grafikus beállítóeszközök, amik hajlamosak elrejteni a lehetőségeket a felhasználó elől. Egy Arch Linux rendszer tehát könnyedén beállítható a legapróbb részletig.

**Komplexitás komplikáció nélkül.**

Az Arch Linux érintetlenül hagyja a GNU/Linux rendszerekben lévő komplexitást, miközben jól szervezetten és átláthatóan tartja azt. Az Arch Linux fejlesztői és felhasználói hisznek abban, hogy egy rendszer bonyolultságának elrejtésére tett kísérlet valójában egy még bonyolultabb rendszert eredményez, és ezért elkerülendő.

## Kódhelyesség kényelem felett

_A korrektség egyértelműen a tökéletes minőség. Ha egy rendszer nem azt csinálja, amit kellene, akkor minden más arról keveset számít._ – Bertrand Meyer

Az Arch Linux rendszer előtérbe helyezi a tervezés eleganciáját, valamint a tiszta, korrekt, egyszerű kódot a szükségtelen foltozással, automatizálással, látványelemekkel vagy „felhasználóbarátsággal” szemben. A szoftverfoltok ezért abszolút minimális szintre vannak szorítva, ideális esetben nullára. Egyszerű tervezésnek és implementációnak mindig egyszerű felhasználói felületet kell adnia.

**Az implementáció egyszerűsége, a kódhelyesség és a minimalizmus mindig uralkodó prioritásai kell, hogy maradjanak az Arch fejlesztésének.**

A koncepciók, tervek és funkciók az Arch Módszer alapelveit útmutatóként használva kerültek megalkotásra és implementálásra, ahelyett, hogy meghajoltak volna külső befolyás előtt. A fejlesztői csapat eltökélt az Arch Módszer filozófia iránti elkötelezettségükben és felajánlásukban. Ha osztja a nézetüket, arra buzdítjuk, hogy használjon Arch-ot.

## Felhasználóközpontúság

Amíg sok GNU/Linux disztribúció próbál _felhasználóbarátabb_ lenni, addig az Arch Linux jelenleg és később is _felhasználóközpontú_ kell, hogy maradjon.

**Az Arch Linux a hozzáértő GNU/Linux felhasználókat veszi célba és fogadja be, teljes irányítást és _felelősséget_ adva nekik a rendszer felett.**

Az Arch Linux felhasználók teljes mértékben maguk kezelik rendszerüket. Maga a rendszer kevés segítséget nyújt, kivéve néhány egyszerű karbantartó eszközt, amelyek úgy lettek megtervezve, hogy tökéletesen továbbítsák a felhasználó utasításait a rendszer felé. Az Arch ésszerű tervezésen és kiváló dokumentáción alapul.

A felhasználóközpontú tervezés szükségszerűen magába foglal egyfajta „csináld magad” megközelítést az Arch disztribúció használatához. Ahelyett, hogy a felhasználók a fejlesztőkhöz fordulnának segítségért, vagy kérnék egy új funkció implementálását, hajlamosak maguk megoldani a problémákat, és bőkezűen megosztani az eredményeket a közösséggel és a fejlesztőcsapattal – egy „először csináld, aztán kérdezz” filozófia. Ez különösen igaz a felhasználók által készített csomagokra, amelyek az Arch User Repository-ban találhatók – a hivatalos Arch Linux tároló a közösség által karbantartott csomagoknak.

## Nyíltság

A nyíltság az egyszerűséggel kéz a kézben jár, és szintén az Arch Linux fejlesztésének egyik vezérelve.

**Az Arch Linux egyszerű eszközöket használ, amelyek a forrás és a kimenetük nyíltságát figyelembe véve lettek kiválasztva vagy építve.**

A nyíltság eltörli az összes határt és absztrakciót a felhasználó és a rendszer között, ezzel több irányítást biztosít, miközben ezzel párhuzamosan megkönnyíti a rendszer karbantartását.

Az Arch Linux nyílt természete szintén magába foglal egy meglehetősen meredek tanulási görbét, de a tapasztalt Arch Linux felhasználók más, zártabb rendszereket jellemzően sokkal kényelmetlenebben irányíthatónak tartanak.

A nyíltság alapelve kiterjed a közösségi tagokra is, mivel az Arch Linux felhasználók nagyon nyitottak a segítségnyújtásban és a közreműködésben.

## Szabadság

Az Arch Linux fejlesztésének egy másik vezérelve a szabadság. A felhasználók nemcsak a rendszer beállításában hozhatnak meg minden döntést, de abban is, hogy mi lesz a rendszerük.

**Azzal, hogy ragaszkodunk a rendszer egyszerűségéhez, az Arch Linux szabadságot biztosít minden, a rendszerrel kapcsolatos választásban.**

Egy frissen telepített Arch Linux rendszer csak az alapvető komponenseket tartalmazza automatikus beállítások végrehajtása nélkül. A felhasználók kedvük szerint állíthatják be a rendszert parancssorból. A telepítési folyamat elejétől kezdve a rendszer minden része 100%-osan átlátható és hozzáférhető a gyors eléréshez, eltávolításhoz vagy lecseréléshez alternatív komponensekre.

A különböző Arch Linux tárolókban lévő nagy számú csomag és építő szkript szintén a választás szabadságát szolgálja. Szabad és nyílt forráskódú szoftvereket kínál azoknak, akik ezt részesítik előnyben, valamint zárt forráskódú szoftvereket azoknak, akiknek _a funkcionalitás fontosabb az ideológiánál_. A felhasználó az, aki választ.

Ahogy Judd Vinet, az Arch Linux projekt alapítója mondta: „Az [Arch Linux] az, amivé teszed.”