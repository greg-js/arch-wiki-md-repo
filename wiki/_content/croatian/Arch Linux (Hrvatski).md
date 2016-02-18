Arch Linux je nezavisno razvijana, i686/x86-64 GNU/Linux distrubucija opče namjene dovoljno raznolika za svaku upotrebu. Programiranje se svodi na jednostavnošću, minimalizmu i eleganciji kôda. Arch je instaliran kao minimalni sustav, koga konfigurira korisnik tako što instalira ono ukruženje koje je potrebno samo tako što će instalirati određene ili zahtjevane pakete za određene svrhe. Alatke za konfiguraciju grafičkog sučelja (GUI) nisu službeno dostavljene, i većina konfiguracije sustava se radi preko terminala tako što se uređuju osnove tekstualne datoteke. Pošto je osnovan na sustavu *rolling release*, Arch uvijek uspjeva biti najnoviji i tipično odmah pruža najnovije inačice većine softwarea čim izađu.

## Contents

*   [1 Povijest](#Povijest)
*   [2 Jednostavnost](#Jednostavnost)
*   [3 Modernost](#Modernost)
*   [4 Pakovanje software-a](#Pakovanje_software-a)
*   [5 Cjelokupnost izvornih datoteka](#Cjelokupnost_izvornih_datoteka)
*   [6 Zajednica](#Zajednica)
*   [7 Sažetak](#Sa.C5.BEetak)

## Povijest

Arch Linux-a je osnovao kanadski programer Judd Vinet. Prvo Arch izdanje, Arch Linux 0.1 bilo je 11\. ožujka 2002\. godine. Iako je Arch potpuno nezavisan, inspiriran je jednostavnošću ostalih distribucija kao što su [Slackware](http://slackware.com), [CRUX](http://www.crux.nu) i [BSD](http://en.wikipedia.org/wiki/Berkeley_Software_Distribution). 2007\. godine, Judd Vinet je prestao biti glavni programer radi ostalih interesa i zamijenio ga je Aaron Griffin tko i dalje nastavlja sa radom kao glavni zaduženi za projekt.

## Jednostavnost

Slijedivši [put Archa](/index.php/The_Arch_Way_(Hrvatski) "The Arch Way (Hrvatski)"), Arch Linux je lagan, fleksibilan, jednostavan i cilja biti sličan UNIX-u. Minimalno okruženje (bez korisničkog sučelja) kompajlirano za i686/x86-64 arhitekture je pružano nakon instalacije: umijesto da se nude dosadni i ponekad nepotrebni paketi, korisniku je pružena mogućnost da sagradi sustav od dna pa prema gore, bez ikakvih preventivno odabranih paketa ili postavki. Arch-ova dizajnerska filozofija i implementacija čine lakim da se može nadograditi i/ili nadovezati što god treba na postojeći sustav, od minimalističkog računala sa terminalom, do raskošnog korisničkog sučelja punog značajki: *korisnik* je onaj koji odlučuje kakav će njegov/njen sustav biti.

Archov jednostavni *init* sustav je snažno inspiriran *BSD načinom spremanja većinu postavki u *jednu datoteku* ([rc.conf](/index.php/Rc.conf "Rc.conf")) radije nego cijelu *SysVinit* mapovnu strukturu koja se sadrži od nekolicine sym poveznica na svakoj razini. Postavke sustava se namještaju uređivanjem jednostavnih tekstualnih datoteka.

## Modernost

Arch Linux nastoji nabavljati najnovije stabilne inačice svog software-a, koji je baziran na *rolling-release* sustavu rada, koji omogućuje jednokratnu instalaciju i kontinuirane djelotvorne nadogradnje, bez potrebe ponovne instalacije ili zasebne instalacije paketa s jedne inačice na drugu. Sa jednom naredbom, Arch sustav može se dovesti na najnovije izdanje, tako reći, te će uvijek biti najnoviji.

Arch u sebi sadrži mnoštvo najnovijih značajki dostupnih GNU/Linux korisnicima, uključujući moderne datotečne sustave (Ext2/3/4, Reiser, XFS, JFS), LVM2/EVMS, software RAID, udev podrška i initcpio, kao i najnoviji Linux kerneli.

## Pakovanje software-a

Arch je baziran na [pacmanu](/index.php/Pacman "Pacman"), lakom za korišćenje binarnom upravitelju paketa koji vam dopušta da nadogradite cijeli sustav s jednom naredbom.

Pacman je kodiran u *C* programskom jeziku i dizajniran je od temelja da bude lagan, jednostavan i brz. Arch također ima i Arch Build System, sustav koji omogućava laku izgradnju i instalaciju paketa iz izvornih datoteka, koji se također mogu sinkronizirati s jednom naredbom. Možete čak i ponovo izgraditi čitav sustav s jednom naredbom.

Pošto Arch podržava i686 i x86-64 arhitekture, njegovi službeni repozitoriji pružaju tisuće kvalitetnih paketa za vaše potrebe. Naravno, Arch želi posteći rast i doprinos zajednice pružajući *Arch Korisnički Repozitorij*, koji sadrži mnoštvo tisuća aplikacija sa korisničko-održavanim PKGBUILD skriptama za kompajliranje instaliranih paketa iz izvornih paketa koristeći *makepkg* aplikaciju. Također je lako za korisnike da naprave i održavaju vlastite repozitorije.

## Cjelokupnost izvornih datoteka

Arch pruža software koji nije patchovan niti mjenjan u bilo kojem smislu; paketi su pruženi od upstream izvornih datoteka, baš kao što je autor i želio da budu distribuirane. Patching se jedino može dogoditi u ekstremnim slučajevima, da se spriječe ozbiljni kvarovi tako da se inačice ne podudaraju ili podudaraju sa istim imenom u *rolling release* modelu rada.

## Zajednica

Arch zajednica je zbilja pouzdana, i živahna, te su svi *Archeri* dobro došli, te se potiču na sudjelovanje i doprinošenje distribuciji, bilo to da je pomoć sa programiranjem core software-a, održavanje paketa, prijavljivanje ili popravljanje [bugova](https://bugs.archlinux.org/) (*kvarova*), poboljšavanje ArchWiki dokumentacije na [početnoj strani](/index.php/Main_Page_(Hrvatski) "Main Page (Hrvatski)"), pomaganje drugima ili izraživanje mišljenja na sljedećima mjestima: [forumima](https://bbs.archlinux.org/), [mailing listama](https://mailman.archlinux.org/mailman/listinfo/) ili IRC kanalima, kao i djeljenje svog znanja ili vlastitih aplikacija. Arch je operativni sustav koga ljudi biraju širom svijeta, i postoji nekolicina internacionalnih zajednica koje pružaju pomoć ili pružaju dokumentaciju na mnogim jezicima (kao što je ova na hrvatskom).

## Sažetak

Da skratimo: Arch Linux je svestrana i jednotavna distribucija dizajnirana za potrebe sposobnih Linux korisnika. Ne samo da je moćan operativni sustav, već i lak za upotrebu, što ga čini idealnom distribucijom za servere i radne stanice. Idite u kom god smjeru hoćete: ako djelite pogled na ovakav smisao toga što GNU/Linux distribucija treba biti, tada ste dobrodošli i potičemo vas da se uključite u zajednicu. Dobrodošli u Arch!