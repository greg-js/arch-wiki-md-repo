Arch Linux je nezavisno razvijena, x86-64 general purpose [GNU](/index.php/GNU "GNU")/Linux distribucija koja teži da pruži zadnje verzije software-a prateći rolling-release model. Defaultna instalacije je minimal base system, konfigurisana od strane korisnika da doda samo ono što mu je potrebno.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Principi](#Principi)
    *   [1.1 Jednostavnost](#Jednostavnost)
    *   [1.2 Modernost](#Modernost)
    *   [1.3 Centralnost oko korisnika](#Centralnost_oko_korisnika)
    *   [1.4 Versatilnost](#Versatilnost)
*   [2 Historija](#Historija)
    *   [2.1 Rani počeci](#Rani_počeci)
    *   [2.2 Srednje godine](#Srednje_godine)
    *   [2.3 Rođendan ArchWiki-a](#Rođendan_ArchWiki-a)
    *   [2.4 Početak doba A. Griffina](#Početak_doba_A._Griffina)
    *   [2.5 Arch instalacijske skripte](#Arch_instalacijske_skripte)
    *   [2.6 systemd era](#systemd_era)
    *   [2.7 Pad podrške za i686](#Pad_podrške_za_i686)

## Principi

### Jednostavnost

Arch Linux definiše jednostavnost kao *bez nepotrebnih dodavanje ili modifikacija*. Unutar njega se nalazi software koji je u pušten od strane originalnih developera ([upstream](https://en.wikipedia.org/wiki/Upstream_(software_development) "wikipedia:Upstream (software development)")) sa minimalnim specifičnim promjenama po distribuciji: patchevi koji nisu prihvaćeni od strane upstreama se izbjegavaju i Arch downstream patchevi sadrže skoro samo od backported bug fixova koji su obsolete od strane idućeg release projekta.

Slično tome, Arch sadrži konfiguracijske fajlove dobijene od strane upstreama sa promjenama koje su limitirane na specifične propuste vezane za distribucije, poput podešavanje putanja sistemskih fajlova. Arch ne dodaje feature za automatizaciju poput enablanje servisa samo zato što je instaliran package. Package-i se splitaju samo ukoliko postoje prednosti toga, poput spašavanja prostora na disku u posebno lošim wastanjima memorije. Alati za konfiguraciju GUI-a se automatski se ne pakuju unutar Arch distribucije da bi se podstakli useri da urade sistemsku konfiguraciju korištenjem shella i text editora.

### Modernost

Arch Linux teži na održavanju zadnjih stabilnih verzija software-a. Baziran je na rolling-release sistemu, koji omogućava jednu instalaciju za kontinualnim upgrade-ima. Arch uključuje veliki broj novih feature-a koji su dostupni GNU/Linux korisnicima, uključujući [systemd](/index.php/Systemd "Systemd") init sistem, moderne [fajlsisteme](/index.php/Filesystems "Filesystems"), LVM2, software RAID, udev podrška i initcpio (sa [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")), kao i zadnje dostupne verzije kernela.

### Centralnost oko korisnika

Za razliku od većine distribucija koje su *user friendly*, Arch Linux je uvijek bio i nastavit će biti *user centric*. Distribucija je namijenjena da ispuni potrebe onih koji doprinose Arch Linux više nego privlačenje što većeg broja korisnika. Namijenjen je iskusnik GNU/Linux korisnicima ili korisnicima sa stavom do-it-yourself koji su voljni da čitaju dokumentaciju i sami riješe probleme.

Svi korisnici se podstiču da [učestvuju](/index.php/Getting_involved "Getting involved") i doprinose distribuciji. Prijavljivanje i pomaganje u rješavanju [bug-ova](https://bugs.archlinux.org/) je visoko cijenjeno, također patchevi koji poboljšavaju pakete ili core [projekte](https://projects.archlinux.org/) su cijenjeni: Arch developeri su volenteri i aktivni kontributori će često postati dio tima. *Archeri* mogu slobodno kontributati paketima u [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), poboljšavajuci [ArchWiki dokumentaciju](/index.php/Main_page_(Bosanski) "Main page (Bosanski)"), pružanje tehničke pomoci drugima ili jednostavno razmjena mišljenja na [forumu](https://bbs.archlinux.org/), [mailing liste](https://mailman.archlinux.org/mailman/listinfo/) ili [IRC channels](/index.php/IRC_channels "IRC channels"). Arch Linux je operativni sistem mnogih ljudi širom svijeta, također postoji nekoliko [internacionalnih community-a](/index.php/International_communities "International communities") koji pružaju pomoć i dokumentaciju u raznim svjetskim jezicima.

### Versatilnost

Arch Linux je general-purpose distribucija. Prilikom instalacije, samo je CLI okruženje dostupno: radije nego brisati neželjene i nepotrebne pakete, korisniku je data mogućnost da kreira custom sistem tako što bira izmedju hiljade visokokvalitetnih paketa dostupnih u [official repositories](/index.php/Official_repositories "Official repositories") za [x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") arhitekturu.

Arch Linux koristi [pacman](/index.php/Pacman "Pacman"), lagani, jednostavni i brzi paket menadžer koji omogućava upgrade-ovanje cijelog sistema jednom komandom. Arch također ima [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), port-like system koji pruža lakoću buildanja i instaliranja paketa direktno iz source file-ova, koji mogu biti sinhronizovani jednom komandom. Također, *Arch User Repository* sadrži više hiljada community-contributed [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") skripti za kompajliranje paketa iz source file-ova korištenjem [makepkg](/index.php/Makepkg "Makepkg") alata. Također, korisnici mogu sami buildati i održavati pakete sa lakoćom.

## Historija

Arch community je porastao i sazreo da postane jedan od najpopularnijih i najuticajnijih Linux distibucija, tome svjedoče [pažnja i review-ovi](/index.php/Arch_Linux_press_coverage "Arch Linux press coverage") koji su primljeni tokom godina.

Arch developeri ostaju neplaćeni, part-time volonteri i nema prospekta monetizirati Arch Linux, tako da će ostati free u svim značenjima riječi. Radoznali koji žele više detalja o historiji Arch developmenta mogu browsati [Arch entry unutar Internet Archive Wayback Machine](http://web.archive.org/web/*/archlinux.org) i [Linux News Arhive](https://www.archlinux.org/news/Arch)]

### Rani počeci

Judd Vinet, kanadski programer i povremeni gitarista je počeo sa developmentom Arch Linuxa početkom 2001\. Prvi formalni release je bio Arch Linux 0.1, 11\. marta 2002\. godine. [Inspirisan](https://distrowatch.com/dwres.php?resource=interview-arch) elegantom jednostavnošću Slackware-a, BSD-a, PLD Linux-a i CRUX-a i razočaran njihovim nedostatkom paket menadžmenta u to vrijeme, Vinet je napravio svoju distibuciju na sličnim principima kao i navedene distribucije. Također, napisao je paket menadžment program koji se zove [pacman](/index.php/Pacman "Pacman") da automatski upravlja instalacijom paketa, uklanjanjem i upgrade-ima.

### Srednje godine

Rani Arch community je rastao polako, što potvrđuje [chart forum postova, korisnika i bug reporta](/index.php/File:Archstats2002-2011.png "File:Archstats2002-2011.png"). Od početka je bio poznat kao [otvoren, prijateljski i community voljan pomoći](http://www.osnews.com/story/4827).

### Rođendan ArchWiki-a

Datuma 8.7.2005\. godine, ArchWiki je prvi put [postavljen](/index.php/ArchWiki:About#Early_history "ArchWiki:About") na MediaWiki engine-u.

### Početak doba A. Griffina

Krajem 2007\. godine, Judd Vinet je otišao u mirovinu što se tiče aktivnog učestovanja kao Arch developer i [prebacio](https://bbs.archlinux.org/viewtopic.php?id=38024) ovlasti na Američkog programera Aaron Griffin-a, poznatog kao Phrakture.

### Arch instalacijske skripte

15.7.2012\. godine, release instalacijskog image-a je [zamijenio](https://www.archlinux.org/news/install-media-20120715-released/) *Arch Installation Framework* (AIF) sa *Arch Instalacijskim skriptama* (*Arch Install Scripts*).

### systemd era

U razdoblju od 2012\. do 2013\. godine, tradicionalni System V init sistem je zamijenjen systemd-om.[[1]](https://www.archlinux.org/news/install-medium-20121006-introduces-systemd/)[[2]](https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/)[[3]](https://www.archlinux.org/news/end-of-initscripts-support/)[[4]](https://www.archlinux.org/news/final-sysvinit-deprecation-warning/)

### Pad podrške za i686

25.1.2017\. godine je [objavljeno](https://www.archlinux.org/news/phasing-out-i686-support/) da će podrška za i686 arhitekturu iščeznuti radi smanjene popularnosti među developerima i community-u. Do [kraja novembra 2017\. godine](https://www.archlinux.org/news/the-end-of-i686-support/), svi i686 paketi su uklonjeni sa mirror-a.