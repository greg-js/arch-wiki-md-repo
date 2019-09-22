Related articles

*   [Arch Linux (Bosanski)](/index.php/Arch_Linux_(Bosanski) "Arch Linux (Bosanski)")
*   [Arch based distributions](/index.php/Arch_based_distributions "Arch based distributions")
*   [Pacman/Rosetta](/index.php/Pacman/Rosetta "Pacman/Rosetta")

Ova stranica upoređuje Arch Linux i druge popularne GNU/Linux distribucije i UNIX-like operativne sisteme. Ono što je u nastavku je kratak opis koji može pomoći pri odluci da li je Arch Linux pravi odabir za tebe. Iako review-ovi i opisi mogu biti od pomoci, iskustvo sa samim operativnim sistemom je najbolja mjera.

Za kompletnije poređenje, vidi [w:Comparison of operating systems](https://en.wikipedia.org/wiki/Comparison_of_operating_systems "w:Comparison of operating systems") i [w:Comparison of Linux distributions](https://en.wikipedia.org/wiki/Comparison_of_Linux_distributions "w:Comparison of Linux distributions").

U nastavku je jedino Arch Linux upoređen sa drugim distribucijama. Community portovi koji podržavaju arhitekture mimo x86_64 mogu biti pronađene na [Arch-based distributions](/index.php/Arch-based_distributions "Arch-based distributions").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Source-based](#Source-based)
    *   [1.1 CRUX](#CRUX)
    *   [1.2 LFS](#LFS)
    *   [1.3 Gentoo/Funtoo Linux](#Gentoo/Funtoo_Linux)
*   [2 Generalno](#Generalno)
    *   [2.1 Debian](#Debian)
    *   [2.2 Fedora](#Fedora)
    *   [2.3 Slackware](#Slackware)
*   [3 Za početnike](#Za_početnike)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Linux Mint](#Linux_Mint)
    *   [3.3 openSUSE](#openSUSE)
    *   [3.4 Mandriva/Mageia](#Mandriva/Mageia)
*   [4 BSD-ovi](#BSD-ovi)
*   [5 Vidi također](#Vidi_također)

## Source-based

Source-based distribucije su jako portabilne, dajući prednost kontroliranja i kompajliranja cijelog OS-a i aplikacija za određenu arhitekturu i svrhu, sa manom utroška vremena u kompajliranju. Arch base i svi paketi su kompajlirani samo za x86_64 arhitekturu.

### CRUX

*   [CRUX](https://crux.nu) je lightweight distrubucija koja se fokusira na [KISS](/index.php/Arch_terminology#KISS "Arch terminology") princip. CRUX je inspirisao Judd Vineta da kreira Arch.
*   CRUX koristi init skripte u stilu BSD-a, dok Arch koristi systemd.
*   Dok Arch korist rolling release sistem, CRUX je manje više na godišnjem nivou.
*   Oba dolaze sa port-like sistemima i kao i *BSD, oba imaju bazno okruženje nad kojim se dalje radi.
*   Arch koristi pacman, koji handla binary sistemske pakete i radi besprijekorno sa [Arch Build System](/index.php/Arch_Build_System "Arch Build System")-om. CRUX koristi community sistem nazvan *prt-get*, koji u kombinaciji sa svojim port sistemom handla rezoluciju dependency-a, ali builda sve pakete iz source (iako je CRUX base installation binary )
*   I Arch i CRUX oficijalno podržavaju samo x86_64 arhitekturu.
*   Arch ima veliki set binary paketa kao i [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). CRUX pruža manju verziju oficijalno podržani port sistem u dodatku sa community repository-ima.

### LFS

*   [LFS](http://www.linuxfromscratch.org/lfs) (LFS) postoji kao dokumentacija. Knjiga uči korisnika kako da dobije source code za minimalan set paketa za funkcionalan GNU/Linux sistem i kako manuelno kompajlirati, patchovati i konfigurisati od početka. LFS je minimalan i nudi odličan i edukacijski proces buildanja i prilagođavanja baznog sistema.
*   LFS pruža online repository; source-vi se preuzimaju manuelno, kompajliraju i instaliraju sa *make*. (Nekoliko metoda paket menadžmenta postoji, navedeno je u LFS Hints).
*   Arch ima iste pakete, plus [systemd](/index.php/Systemd "Systemd"), nekoliko dodatnih alata i moćni [pacman](/index.php/Pacman "Pacman") paket menadžer kao svoj bazni sistem, već kompajlirano za x86_64\. Zajedno sa minimalnim Arch baznim sistemom, Arch community i developeri omogućavaju i održavaju više hiljada binarnih paketa koji se mogu instalirati sa [pacman](/index.php/Pacman "Pacman")-om, kao i [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") skripte za [Arch Build System](/index.php/Arch_Build_System "Arch Build System").

Arch također uključuje [makepkg](/index.php/Makepkg "Makepkg") alat za buildanja i customiziranje *.pkg.tar.xz* paketa, kojima se može upravljati sa pacmanom.

*   Judd Vinet je napravio Arch od početka i onda napisao pacman u C programskom jeziku. Historički, Arch je često opisivan humoristički kao "Linux, with a nice package manager." (Linux, sa finim paket menadžerom)

### Gentoo/Funtoo Linux

*   Oba Arch Linux i [Gentoo Linux](https://gentoo.org) su rolling release sistemi, pravljeći pakete dostupnim distribuciji kratko vrijeme nakon releasanog upstreama.
*   Gentoo paketi i bazni sistem su buildani direktno iz source code-a na osnovu korisničko definisane *USE flags*. Arch omogućava port-like sistem za buildanje paketa iz source code, ali je Arch bazni sistem dizajniran da bude instaliran kao prebuildan x86_64 binary. Generalno, ovo čini Arch bržim da se builda i updateuje i omogućava Gentoo da bude više sistematski customiziran.
*   Arch samo podržava x86_64 dok Gentoo oficijalno podržava x86 (i486/i686), x86_64, PPC/PCC64, SPARC, Alpha, ARM, MIPS, HPPA, S/390 i Itanium arhitekture.
*   Gentoo-ovi oficijalni paketski i sistemsko menadžmentski alati su uglavnom kompleksni i "moćniji" nego što je to slučaj sa Arch Linuxom, i neki feature koji su u srcu Gentoo-a *([USE flags](https://wiki.gentoo.org/wiki/Handbook:X86/Working/USE), [SLOTs](https://wiki.gentoo.org/wiki/Handbook:X86/Working/Portage#Terminology), itd.)* nemaju ekvivalente u Arch Linuxu. Razlog nekim od tih je u tome sto je Arch primarno binary distribucija, ali razlike u [design filozofija](/index.php/Arch_Linux#Principles "Arch Linux") također igra veliku uloguv gdje Arch zauzima principijalniji stav vezano za arhitekturalnu jednostavnost i izbjegavanja pretjeranog inžinjeringa.
*   Zato jer oba i Gentoo i Arch instalacije samo uključuju bazni sistem, oba se smatraju kao operativni sistem koji se mogu jako customizirati. Ako su upoznati sa [systemd](/index.php/Systemd "Systemd"), Gentoo korisnici će generalno lako preći na Arch linux.

## Generalno

Ove distribucije pružaju širok spektar prednosti i snaga i mogu biti napravljene da služe većini upotreba operativnog sistema.

### Debian

*   [Debian](https://www.debian.org/) je najveća upstream Linux distribucija sa većim community-em i ima stabilne, test i nestabilne branchove, koja pruža više od 43,000 [paketa](https://packages.debian.org/unstable/). Broj dostupnih Arch binarnih paketa je skromniji. Ukoliko se uključi AUR, poprilično je isto.
*   Debian ima žestok stav za besplatan software, ali i dalje uključuje software koji se plaća. Arch je blaži i, prema tome, sveobuhvatniji u vezi s "neslobodnim paketima" kako je definirano u GNU.
*   Debian se fokusira na stroga ispitivanja stabilne branche, koja je "zaleđena" i podržana do [pet godina](https://wiki.debian.org/LTS "debian:LTS"). Arch paketi su noviji nego Debian stable, gdje su više ekvivalent debian testing i unstable branch-ovima i nema fixni release raspored.
*   Debian je dostupan za različite arhitekture, uključujući alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 i sparc. Arch je x86_64 samo.
*   Arch pruža slobodniju podršku za buildanje custom, instalabilnih paketa sa vanjskih izvora, sa port-like paket build sistemom. Debian ne pruža port sistem, već uzda se u svoje velike binary repositorye.
*   Arch instalacijski sistem samo pruža minimalni bazni sistem, dok Debianove metode, poput apt *tasks* za instaliranje unaprijed odabranih grupa paketa, pružaju više automatsko konfigurisani pristup kao i nekoliko alternativnih metoda instalacije.
*   Arch generalno pakuje library-e zajedno sa njihovim header fajlovima, gdje Debian header fajlovi moraju biti posebno download-ovani.
*   Arch čuva patching na minimumu, i tako izbjegava probleme koje upstream ne može da pregleda, gdje su Debian patchevi više slobodni za šire mase.

### Fedora

*   [Fedora](https://getfedora.org/) je razvijend od strane community-a, a sa druge strane podržan od strane Red Hat-a; često je predstavljen kao test release sistem. Fedora paketi i projekti migriraju to RHEL i neki budu prihvaćeni do strane drugih distribucija. Arch nema fixne release-ove i ne služi kao testni branch za drugu distribuciju.
*   Fedora paketi koriste RPM format sa DNF paket menadžerom. Arch koristi [pacman](/index.php/Pacman "Pacman") da upravlja tar.xz paketima.
*   Fedora odbija da uključi nebesplatni software unutar svojih repository-a radi privrženosti open source-u, iako su third-party repository-i dostupni za takve pakete. Arch je blaži u odnosi prema nebesplatnom software-u, ostavljajući izbor korisniku.
*   Fedora nudi više različitih instalacijskih opcija uključujući grafički instaler kao i minimalnu opciju. Fedora "spins" također nude alternativni asortiman desktop okruženja za odabir, svaki sa svojim asortimanom defaultnih paketa. Arch, s druge strane, samo nudi nekoliko skripti namjenjenih za olakšavanje procesa instalacije minimalnog baznog sistema.
*   Fedora ima zakazani release ciklus, ali oficijalno podržava diskretne verzije upgrade-a sa FedUp alatom. Arch is rolling-release sistem.
*   Arch ima port sistem, dok Fedora nema.
*   Arch i Fedora su ciljani za iskusne korisnike i developere. Oba podstiču korisnike da doprinose developmentu projekta.
*   Fedora je zaradila više prepoznavanja unutar community-a radi integracije SELinux-a, GCJ kompajliranih paketa (da se ukloni potreba za Oracle-ovim JRE) i profilnu upstream kontribuciju.; Red Hat i Fedora developeri najviše doprinose Linux kernel kodu u poređenju sa drugim distribucijama.
*   Arch Linux ima najdetaljniju wiki što je opće poznato. Fedora wiki se koristi u originalnom značenju riječi "wiki", ili način da se razmijene informacije između developera, testera i korisnika rapidno. Nije namijenjeno da bude baza znanja za krajnjeg korisnika kao što je to slučaj sa Arch Linux-om. Fedorin wiki podsjeća na tracker issue-a ili korporativni wiki.

### Slackware

*   [Slackware](http://www.slackware.com/) koristi init skripte poput BSD-a, dok Arch koristi [systemd](/index.php/Systemd "Systemd").
*   Arch pruža paket menadžment u [pacman](/index.php/Pacman "Pacman"), koji za razliku od Slackware standardnih alata, pruža automatsku rezoluciju dependency-a i omogućava za više automatizirani sistemski upgrade. Slackware korisnici obično preferiraju njihovu manuelno metode rješavanja dependency-a, iskorištavajući kontrolu koju im sistem pruža, kao i Slackware-ove unaprijed instalirane library-e i dependency-e.
*   Arch je rolling-release sistem, Slackware je konzervativniji gdje preferira stabilne pakete. Arch je više *bleeding-edge* u ovom aspektu.
*   Arch Linux pruža hiljade binarnih paketa unutar oficijalnih repository-a, dok su Slackware repository skromniji.
*   Arch pruža [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), sistem nalik na portove i [AUR](/index.php/AUR "AUR"), veliku kolekciju PKGBUILD skripti od strane korisnika. Slackware pruža sličnu stvari, ali manji sistem na [slackbuilds.org](http://www.slackbuilds.org) koji je polu oficijalni repository Slackbuild-ova, koji su ekvivalent PKGBUILD-ovima. Slackware korisnici će se lako snaći na Arch Linuxu.

## Za početnike

Nekada nazivane "newbie distribucije", namjenjene za početnike distribucije dijele puno sličnosti; Arch Linux je dosta različit od njih. Arch je možda bolji izbor ako želiš naučiti o GNU/Linuxu pravljeći sistem od male baze jer instalacija Arch Linuxa instalira samo nekoliko paketa. Specifične razlike između distribucije su opisane ispod.

### Ubuntu

*   [Ubuntu](https://www.ubuntu.com) je popularna distribucija bazirana na Debianu komercijalno sponzorisana od strane Canonical Ltd., dok je Arch nezavisno razvijeni sistem od početka.
*   Ubuntu i Arch imaju različite ciljeve i ciljane su na različite grupe korisnika. Arch je dizajniran za korisnike sa željom za do-it-yourself pristupom, dok Ubuntu pruža prekonfigurisani sistem. Arch predstavlja jednostavniji dizajn od bazne instalacije pa na dalje, oslanjajući se na korisnika da ga customizira po svojoj želji. Veliki broj Arch korisnika su krenuli sa Ubuntu-om i migrirali na Arch.
*   Arch development nije orijentisan niti prema jednom korisničkom interfejsu mimo onoga što community podržava. Dalje, komercijalna priroda Canonicala ih je odvela do nekih kontroverznih odluka, poput reklama u *Dash* meni i kolekciju korisničkih podataka. Arch je nezavisan, community-driven projekat bez komercijalne agende.
*   Ubuntu pušta diskretne relase-ove svakih 6 mjeseci, dok je Arch rolling-release sistem.
*   Arch pruža build sistem nalik na portove i [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") gdje korisnici mogu dijeliti source pakete za [pacman](/index.php/Pacman "Pacman") paket menadžera. Ubuntu koristi kompleksniji [apt](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool "wikipedia:Advanced Packaging Tool") i omogućava redistribuciju binarnih paketa preko [Personal Package Archives](https://launchpad.net/ubuntu/+ppas)].
*   Čak dva community-a se razlikuju. Arch community je puno manji i ohrabruju se da doprinose Arch projektima. S druge strane, Ubuntu community je relativno velik i zbog toga može trpiti veći procenat korisnika koji ne doprinose developmentu, pravljenju paketa ili održavanje repository-a.

### Linux Mint

*   [Linux Mint](https://www.linuxmint.com/) je nastao kao [Ubuntu](#Ubuntu) derivat i kasnije dodao LDME (Linux Mint Debian Edition) koja je bazirana na [#Debian](#Debian)-u. S druge strane, Arch je nezavisna distribucija koja se oslanja na svoj [build sistem](/index.php/ABS "ABS") i [repository-e](/index.php/Official_repositories "Official repositories").
*   Mint uključuje nekoliko grafičkih alata za lakše nadgledanje, nazivane *MintTools*(Mint alati). Arch samo pruža CLI alate poput [pacman](/index.php/Pacman "Pacman")-a i ostavlja menadžment sistema korisniku.
*   Mint uglavnom dolazi sa [Cinnamon](/index.php/Cinnamon "Cinnamon")-om ili [MATE](/index.php/MATE "MATE")-om za GUI i alternativno [KDE](/index.php/KDE "KDE") ili [Xfce4](/index.php/Xfce4 "Xfce4").
*   Nove verzije Minta se puštaju svakih 6 mjeseci, oko mjesec dana iza Ubuntu-a. Svaki release je bazirano na najnovijem Ubuntu LTS i podržan je 5 godina. Linux Mint Debian Edition (LDME) je baziran na Debian Stable i samo dobija update-e za Mint pakete i sigurnosne update. Arch je u potpunosti rolling-release distribucija.

### openSUSE

[openSUSE](https://www.opensuse.org/) je centralisan oko RPM paket formata i svog dobro GUI konfiguracijskog alata YaST2\. Arch nema takvu opciju. Radi toga openSUSE može biti biti prikladniji za korisnike koji žele okruženje koje se fokusira na GUI, automatsku konfiguraciju ili očekivanu funkcionalnost out of the box, dok s druge strane dozvoljava duboku customizaciju.

### Mandriva/Mageia

Mandriva Linux (prije Mandrake Linux) je kreiran 1998 sa ciljem pravljenja GNU/Linux lakim za svakoga; RPM baziran i koristi urpmi paket menadžer. Mageia je fork Mandrive kreiran od strane nekadašnjeg zaposlenika Mandriva-e koji se protivi komercijalnoj poziciji Mandriva-e tako što je neprofitna i community-driven projekat. Arch ima jednostavniji pristup od Mandriva-e i od Mageia-e, time što je text-based i oslanja se na manuelnu konfiguraciju, i cljan je srednje i napredne korisnike.

## BSD-ovi

*   BSD-ovi dijele zajedničko porijeklo, dolaze direktno od posla na UC Berkeley da se kreira besplatno distribuirajuci, besplatan UNIX sistem. Oni nisu GNU/Linux distribucija, nego više sistem nalik na UNIX, nastali direktno iz originalnog AT&T UNIX koda.
*   Arch i BSD-ovi dijelete koncept usko integrisanog baznog i sistema portova. S druge strane, za razliku od GNU/Linux distribucija poput Arch-a, BSD-ov kernel i userland programi (poput shell-a i core alata poput *ls*, *cp*, *cat* i *ps*) su razvijeni zajedno u jednom source repository-u.
*   [BSD licenca](https://en.wikipedia.org/wiki/BSD_licenses "wikipedia:BSD licenses") je popustljiva u poređenju sa [GPL](https://en.wikipedia.org/wiki/GNU_General_Public_License "wikipedia:GNU General Public License") koja govori da derivativi moraju biti pod istom licencom. Arch koristi GPL.
*   Da saznaš više o BSD varijantama, vidi [Komparacija BSD operativnih sistema](https://en.wikipedia.org/wiki/Comparison_of_BSD_operating_systems "wikipedia:Comparison of BSD operating systems").

## Vidi također

*   [DistroWatch](https://distrowatch.com/) - Novosti i review-ovi o Linux distribucijama
*   [The Live CD List](https://www.livecdlist.com) - Lista image-a Live operativnih sistema