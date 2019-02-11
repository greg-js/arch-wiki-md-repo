Related articles

*   [Arch Linux (Lietuviškai)](/index.php/Arch_Linux_(Lietuvi%C5%A1kai) "Arch Linux (Lietuviškai)")
*   [The Arch Way (Lietuviškai)](/index.php/The_Arch_Way_(Lietuvi%C5%A1kai) "The Arch Way (Lietuviškai)")

Šitas puslapis bando sulyginti Arch Linux su kitomis populiariomis GNU/Linux distribucijomis ir UNIX tipo operacinėmis sistemomis. Sekantys apibūdinimai yra trumpi apibūdinimai, kurios galėtų padėti žmogui apsispręsti ar Arch Linux gali patenkinti jo poreikius. Nors apžvalgos ir apibūdinimai gali būti naudingi, patirtis iš pirmų rankų visada yra geriausias būdas palyginti distribucijas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Paremtos pradinio kodo kompiliavimu](#Paremtos_pradinio_kodo_kompiliavimu)
    *   [1.1 Gentoo](#Gentoo)
    *   [1.2 Sorcerer/Lunar-Linux/Source Mage](#Sorcerer/Lunar-Linux/Source_Mage)
*   [2 Minimalistinės distribucijos](#Minimalistinės_distribucijos)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 Grafinės distribucijos](#Grafinės_distribucijos)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Mandriva](#Mandriva)
    *   [3.4 SUSE](#SUSE)
    *   [3.5 PCLinuxOS](#PCLinuxOS)
*   [4 The *BSDs](#The_*BSDs)
    *   [4.1 FreeBSD](#FreeBSD)
    *   [4.2 NetBSD](#NetBSD)
    *   [4.3 OpenBSD](#OpenBSD)
*   [5 Kitos](#Kitos)
    *   [5.1 Debian GNU/Linux](#Debian_GNU/Linux)
    *   [5.2 Frugalware](#Frugalware)
*   [6 Išorinės nuorodos](#Išorinės_nuorodos)

## Paremtos pradinio kodo kompiliavimu

Pradinio kodo kompiliavimu pagrįstos distribucijos yra labai lanksčios. Yra suteikiama galimybė kontroliuoti ir kompiliuoti visą operacinę sistemą ir programas, optimizuojant prie tam tikros sistemos architektūros yra vartojimo schemos. Tuo pat natūraliai atsiranda laiko atimantis minusas. Arch bazė ir visi paketai yra sukompiliuoti i686 ir x86-64 architektūroms. Tai leidžią siūlyti potencialų greičio padidėjimą i386/i486/i586 binarinėms distribucijoms ir suteikia tikslų ir greitą įdiegimą.

### Gentoo

Tiek Arch Linux, tiek Gentoo Linux yra pagrindinės versijos modelio sistemos, kas reiškia, kad paketai yra pasiekiami distribucijai labai greitai, nuo to laiko, kai jie yra oficialiai paskelbiami kūrėjų. Gentoo paketai yra sukonstruoti tiesiai iš pradinio kodo, tuo tarpu oficialūs Arch paketai yra dalinai sukonstruoti iš pradinio kodo. Tai padaro Arch greitesnę sukonstruoti ar atnaujinti, ir leidžia Gentoo Linux būti lengvai konfigūruojama. Arch palaiko i686 ir x86-64, kai Gentoo oficialiai palaiko x86, ppc, sparc, alpha, amd64, arm, mips, hppa, s390, sh, ir itanium architektūra. Kadangi abiejų Gentoo ir Arch sistemų įdiegimas susideda tik iš pradinės sistemos, tai suteikia joms būti stipriai konfigūruojamos. Pagrinde Gentoo vartotojai turėtų jaustis gan patogiai ir su Arch.

### Sorcerer/Lunar-Linux/Source Mage

Sorcerer/Lunar-Linux/Source Mage (SLS) visos jos yra paremtos pradinio kodo, kaip ir Gentoo, skirtumas tik tas, kad jos tarpusavyje susietos. SLS distribucijos, palyginus naudoja paprastus skriptus paketo sukūrimui ir naudoja globalų konfigūracijos failą kompiliavimo procesui, kaip ir [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). SLS įrankiai tikriną paketų priklausomybes (įskaitant ir nebūtinas sąlygas) ir vykdo paketo priežiūrą (atnaujinimas/pašalinimas). Nėra binarinių (sukompiliuotų) paketų bet kuriai distribucijai iš SLS šeimos, tačiau galima labai lengvai iš naujesnės pereiti prie senesnės programos versijos.

Įdiegiamo procese dirbama su pagrindine sistema (kaip ir Arch'o: i686 optimizuota, CLI ir ncurses menu, tik pagrindiniai įrankiai), tada pagrindinės sistemos perkompiliavimas (nebūtinas). Nėra "standartinės" WM/DE/DM. Xorg nėra įtraukas į pagrindinės sistemos diegimą. Egzistuoja keletas X serverio alternatyvų (X.Org 6.8 arba 8, XFree86).

SLS turi labai komplikuotą istoriją. Turbūt geriausią straipsnį šia tema galima rasti [the SourceMage wiki](http://wiki.sourcemage.org/SourceMage/History).

## Minimalistinės distribucijos

Minimalistinės distribucijos, dalindamos keletas panašumų, yra gan palyginamos su Arch. Visos jos, techniškai žvelgiant, yra 'paprastos'.

### LFS

LFS, ( arba Linux From Scratch (Linux iš pagrindų. vert. past.)) egzistuoja paprastai dokumentacijos forma. Knyga supažindina vartotoją kaip pastatyti minimalią GNU/Linux pagrindinę sistemą ir kaip paskui rankiniu būdu kompiliuoti, lopyti ir konfigūruoti viską iš pagrindų. LFS yra minimali tiek, kiek įmanoma. Jinai siūlo tobulą ir informatyvų pagrindinės sistemos kompiliavimo procesą. Arch, kaip pagrindinę sistemą, siūlo tokius pat paketus su BSD stiliaus iniciaciją, keletas papildomų paketų ir galingą [pacman](/index.php/Pacman "Pacman") paketų valdiklį jau sukompiliuotą i686/x86-64 sistemoms. LFS nesuteikia internetu pasiekiamų paketų; pradinis kodas parsiunčiamas rankiniu būdu, kompiliuojamas ir įdiegiamas su "make". (Egzistuoja keletas technikų, kaip galima dirbti su paketais, paminėti LFS patarimuose) Kartu su minimalia Arch pagrindine sistema, Arch bendruomenė ir kūrėjai siūlo ir palaiko daugybę binarinių paketų, kuriuos labai lengvai galima įdiegti pasinaudojant pacman įrankiu. Taip pat ir [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") konstrukciniai skriptai, kurie naudojami [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). Arch taip pat turi [makepkg](/index.php/Makepkg "Makepkg") įrankį, su kuriuo galima tikslingai sukurti ar pakoreguoti `.pkg.tar.gz` paketus, kuriuos jau galima instaliuoti su pacman. Judd Vinet sukūrė Arch iš pagrindų, tada parašė su C programavimo kalba pacman. Istoriškai, Arch kartais juoko forma apibūdinamas kaip "Linux, su gera paketų valdykle."

### CRUX

Arch yra kuriamas nepriklausomai, iš pagrindų ir niekad nebuvo paremtas jokia distribucija. Prieš Arch, Judd Vinet susižavėjo ir naudojo CRUX; minimalistinę distrubucija, kurią sukūrė Per Lidén. Iš pradžių, įkvėptas bendrų CRUX idėjų, Arch buvo sukurtas iš pagrindų ir tada [pacman](/index.php/Pacman "Pacman") buvo parašytas su C. Abu jie dalinasi pagrindiniais principais: architektūriškai optimizuoti, minimalistiniai ir K.I.S.S. orientuoti. Abu krauna paketus portų paremta sistema, naudoja *BSD stiliaus iniciaciją ir vėl gi kaip ir *BSD, suteikia minimalią sistemą, kurią galima pritaikyti savo reikmėm. Arch turi pacman, kuris tvarko binarinės sistemos paketus ir sklandžiai dirba su [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). CRUX naudoja bendruomenės palaikomą sistemą, kuri vadinasi prt-get, kuri, kartu su sava portų sistema, prižiūri paketų priklausomybes, bet kurią paketus iš pradinio kodo (per CRUX pagrindinį i686 įdiegimą). Arch oficialiai palaiko x86-64 ir i686, tuo tarpu CRUX tik i686.

Arch naudoja dabartinės versijos modelį ir siūlo didelį binarinių paketų pasirinkimą, bei [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). CRUX oficialiai siūlo mažesnę portų sistemą, kartu su kuklia bendruomenės saugykla.

### Slackware

Slackware ir Arch yra gan panašios savo tikslais - elegancija ir minimalumu. Slackware įžymus dėl markinių (branding. vert.past) trūkumo ir visiškai lėkštų paketų, pradedant nuo branduolio. Arch tipiškai daro paketų lopymus tik tada, kai tai būtina, norint išvengti sunkaus paketų lūžimo ir išsaugoti funkcionalumą. Abu naudoja BSD stiliaus iniciacijos skriptus. Arch pateikia paketų tvarkyklę [pacman](/index.php/Pacman "Pacman") kuri, skirtingai nei Slackware standartiniai įrankiai, siūlo automatinį priklausomybių tikrinimą daugiau automatizuotai sistemai. Slackware vartotojai paprastai naudoja savo paketų priklausomybės tikrinimo metodą, su sistemos kontroliavimo lygiu, kuris jiems suteikiamas. Arch yra dabartinės versijos modelio. Slackware matomas kaip daugiau konservatyvi distribucija savo išleidimo cikle, teikdama pirmenybę stabiliems paketams. Arch šiuo atžvilgiu yra daugiau 'ant kraujavimo krašto'. Archlinux suteikia daugiau nei 4500 binarinių paketų jo [core], [extra] bei [community] saugykluose ir Slackware suteikia tik apie 1200 binarinių paketų. Arch suteikia [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), realią portų sistemą ir taip pat [AUR](/index.php/AUR "AUR"), PKGBUILD skriptų kolekciją (apie 22000), kuriuos suteikė bendruomenė. Slackware suteikia kažką panašaus į tai [slackbuilds.org](http://www.slackbuilds.org), kuri yra pusiau oficiali Slackware saugykla, Slackware ekvivalentas PKGBUILD (šiuo metu yra 2000 paketų). Slackware vartotojai jausis gan patogiai su daugeliais Arch aspektais.

## Grafinės distribucijos

Kartais vadinamos "naujokų" distribucijos, grafinės distribucijos dalinasi daugeliais panašumų, nors Arch turi nemažai skirtumų. Pasirinkti Arch turėtų tas, kuris norėtų išmokti daugiau apie GNU/Linux, statydamas sistemą iš minimumo, kadangi Arch, palyginus, įdiegimas suteikia labai mažai paketų. Grafinės distribucijos dažniausiai įdiegimą pateikia GUI aplinkoje (kaip Ferodos Anaconda) ir GUI sistemos konfigūravimo įrankius ( kaip SUSE-ės YaST). Specifiniai skirtumai tarp distribucijų yra pateikiamos žemiau.

### Ubuntu

Ubuntu yra be galo populiari Debian paremta distribucija, komerciškai remiama Canonical Ltd., tuo tarpu Arch yra nepriklausomai kuriama sistema, padaryta iš pagrindų. Abu projektai turi labai skirtingus tikslus ir yra nukreipti skirtingų interesų vartotojams. Arch yra suprojektuotas vartotojams, kurie vadovaujasi 'padarau pats' principu, tuo tarpu Ubuntu suteikia automatiškai sukonfigūruotą sistemą, kuri yra skirta būti daugiau negu paprasta distribucija. Jeigu Jūs norite paleisti sistemą greitai ir be jokių landinėjimų konfigūracijos failuose, Jums labiau tiks Ubuntu. Arch yra pateikiama daugiau kaip minimalistinio dizaino, visiškai nuo vartotojo priklausoma distribucija, kuri leidžia vartotojui ją pilnai pritaikyti savo reikmėm. Bendrai paėmus, programuotojai ir visų galų meistrai daugiau lenkiasi link Arch, negu į Ubuntu pusę, nors kai kurie Arch vartotojai teigia, kad pradžioje jie naudojo Ubuntu, o tik paskui perėjo prie Arch. Ubuntu išleidžia pagrindinę versiją kas 6 mėnesius, tuo tarpu Arch yra pagrindinės versijos modelio sistema. Arch siūlo portų sistemos paketų tvarkymo sistemą, [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), kai Ubuntu to nesiūlo. Dvi bendruomenės taip pat skiriasi kai kuriais aspektais. Arch bendruomenė yra žymiai mažesnė ir yra skatinama būti aktyvią; didelis bendruomenės narių procentas prisideda prie distribucijos. Kontrastui, Ubuntu bendruomenė yra palyginti tiek didesnė, kad gali toleruoti daug didesnį procentą vartotojų, kurie visiškai neprisideda prie distribucijos vystymo ir paketų palaikymo.

### Fedora

Fedora yra išsukta iš Red Hat distribucijos ir buvo nuolat viena iš populiariausiu distribucijų iki šiol. Kaip tokia, egzistuoja didelė bendruomenė, daugybės pusiau pastatytų (pre-build. vert.past.) paketų ir pagalba. Fedora paketai yra RPM-sai, naudojama YUM paketų valdymo sistema. Arch naudoja [pacman](/index.php/Pacman "Pacman"), valdant paprastus siunčiamus paketus. Fedora puikiai nebando palaikyti MP3 media formato, dėl patentų nesklandumų. Arch turi daug didesnį atlaidumo polinkį link MP3 ar kitokių media formatų. Fedora siūlo tiek grafinį, tiek tekstinį įdiegimą. Arch neteikia grafinio įdiegimo, o naudoja ncurses paremtą įdiegimo vedlį, besiremiančiu vartotojo rankiniu konfigūravimu. Fedora turi nustatytą išleidimo grafiką. Arch yra pagrindinės arba dabartinės versijos modelio. Arch projektavimo priėjimas yra orientuotas daugiau į lengvą eleganciją ir minimalumą, o ne į automatinį konfigūravimą. Fedora atnaujino ir neseniai įgyjo didelį pripažinimą dėl integracijos su SELinux ir GCJ sukompiliuotų paketų, pašalinant Sun JRE būtinybę. Fedora iš karto nepalaiko nei JFS, nei ReiserFS.

### Mandriva

Mandriva Linux (formaliai Mandrake Linux) buvo sukurta 1998, su tikslu padaryti GNU/Linux paprasta naudoti kiekvienam. Ji paremta RPM ir naudoja urpmi paketų tvarkyklę. Vėl gi, Arch padaro paprastesnį priėjimą, būdama tekstiškai paremta ir pilnai remdamasi rankiniu vartotojo konfigūravimu. Arch taip pat yra pasiryžus būti daugiau tiesiškai tarpinė pažengusiems vartotojams.

### SUSE

SUSE sukoncentruota aplink gerai laikomą YaST konfigūracinį įrankį, kuris yra pagrindė stotelė daugeliams vartotojų konfigūruojant sistemą jų poreikiams. Arch nesiūlo tokį įrenginį, kadangi tai eina prieš [The Arch Way (Lietuviškai)](/index.php/The_Arch_Way_(Lietuvi%C5%A1kai) "The Arch Way (Lietuviškai)"). SUSE, taip pat laikoma daugiau prieinama mažiau patyrusiems vartotojams, ir tiems, kurie nori daugiau GUI paremtos aplinkos, automatinio konfigūravimo ir funkcionalumo iškart.

### PCLinuxOS

PCLinuxOS yra populiari Mandriva paremta distribucija, siūlanti visišką DE, suprojektuotą vartotojo draugiškumui ir apibūdinama kaip "paprasta", nors paprastumo apibūdinimas yra gan kitoks, nei Arch apibūdinimas. Arch yra suprojektuotas kaip paprasta pagrindinė sistemą, kuri pritaikoma savo reikmėm nuo pagrindų ir su tikslu būti daugiau tiesinė pažengusiems vartotojams. PCLOS naudoja apt paketų tvarkyklę kaip tarpininką RPM paketams. Arch naudoja nuosavą nepriklausomai vystomą [pacman](/index.php/Pacman "Pacman") paketų tvarkyklę su `.pkg.tar.gz` paketais. PCLOS yra labai paremta GUI, suteikianti GUI geležies konfigūravimo įrankius ir Synaptic paketų tvarkymo išvaizdą. Taip pat ji teigia turinti mažai arba visišką nepriklausomybę nuo kiauto. Arch yra orientuota į komandinę eilutę ir suprojektuota daugiau paprastam priėjimui prie sistemos konfigūravimo, valdymo ir palaikymo. PCLOS rekomenduoja mažiausiai 256MB RAM kaip dalį minimalių sistemos reikalavimų. Būdama daug lengvesnė, Arch gali dirbti sistemose su daug mažesne atmintimi, reikalaudama tik 64MB RAM pagrindinės i686 sistemos įdiegimui. Jinai taip pat gali dirbti švariai ir daug modernesne sistemose.

## The *BSDs

Arch ir *BSD kartu siūlo mažai integruotą pagrindinę sistemą ir portų sistemą, kombinuotą su prieinamais binariniais paketais. BSD kilo iš Berkeley <tt>UNIX</tt>. Taip pat, *BSD nėra GNU/Linux distribucijos, o <tt>UNIX</tt> tipo operacinės sistemos.

### FreeBSD

Arch ir [FreeBSD](http://www.freebsd.org/about.html) kartu siūlo programinę įrangą, kuri yra pasiekiama binariniu pavidalu arba gali būti sukompiliuojama 'portų' sistemos dėka. Kartu dalinasi labai panašiomis iniciacijos sistemomis. FreeBSD giriasi būdama daugiau sistema, suprojektuota pilnai, lyginant su GNU/Linux distribucijomis, kurios kiekviena programa yra 'suportuota' su FreeBSD. Tokiu atveju duodamas garantas, kad viskas vyks sklandžiai. Abu naudoja `/etc/rc.conf` kaip pagrindinį konfigūracijos failą. FreeBSD licencija daugiau gina "programuotoją", palyginus su GPL, kuri apgina daugiau patį "kodą". Arch yra išleista pagal GPL. FreeBSD sistemoje, kaip ir Arch, viską apsprendžia vartotojas. Tai gali būti labai įdomus palyginimas su Arch, nes abidvi eina galva į galvą su paketų modernumu ir turi šiek tiek didelę, protingą, aktyvią, sąmoningą bendruomenę. Sistemos kartu dalinasi daugeliais panašumu ir FreeBSD vartotojai tikrai jausis jaukiai su daugeliais Arch aspektais.

### NetBSD

NetBSD yra nemokama, saugi ir labai portatyvi <tt>UNIX</tt> tipo atviro kodo operacinė sistema pasiekiama daugiau nei 50 platformų, pradedant nuo 64 bitų Opteron mašinom ir namų sistemom iki rankose laikomų ir įterptinių sistemų. Jo švarus dizainas ir išplėstos funkcijos padaro ją tobula gamybine, bei tiriama aplinka. Vartotojams pateikiamas pilnas pradinis kodas. Daugelis programų yra paprastai pasiekiamos per pkgsrc, NetBSD paketų kolekciją. Arch gali neoperuoti tiek įrenginių, kiek NetBSD operuoja, bet i686 sistemos ji siūlo daugiau programų. Taip pat, numatytas pkgsrc įdiegimo metodas yra parsisiųsti ir sukompiliuoti išeities kodą, kai Arch siūlo binarinius paketus. Arch dalinasi keletais panašumu su NetBSD; kartu naudoja `/etc/rc.conf` kaip pagrindinį konfigūracijos failą, yra minimalios ir lengvos, siūlo portų sistemas, kaip ir binarinius paketus įtraukiant aktyvius, sąmoningus programuotojus bei bendruomenę. Arch taip pat skolinasi iš *BSD sistemų iniciacijos sistemos konceptus.

### OpenBSD

OpenBSD projektas sukuria nemokamą, daugelio platforminę 4.4BSD paremtą <tt>UNIX</tt> tipo operacinę sistemą. Pastangos fokusuojamos prie lankstumo, standartizavimo, kodo teisingumo, iniciatyvios apsaugos ir įdiegtą kriptografiją. Palyginus, Arch fokusuojasi daugiau prie paprastumo, elegancijos, minimalumo ir naujausios programinės įrangos. OpenBSD palaiko binarinį emuliatorių daugumai SVR4 (Solaris), FreeBSD, GNU/Linux, BSD/OS, SunOS ir HP-UX programų. OpenBSD save apibūdina taip 'turbūt pati geriausia apsaugos OS'.

Bendrai su Arch, OpenBSD siūlo mažą, elegantišką, pagrindo įdiegimą ir naudoja portų bei paketų sistemas, kurios leidžia lengvą programų įdiegimą ir palaikymą, kurios nėra pagrindinės sistemos dalis. Palyginus su GNU/Linux sistema kaip Arch, bet turinti panašumu su daugeliais kitų BSD sistemų, OpenBSD branduolio ir vartotojo programos kaip kiautas ir pagrindiniai įrankiai (kaip ls, cp, cat ir ps) buvo kuriami kartu vienoje kodo saugykloje.

## Kitos

Šitos operacinės sistemos nukrito į 'kitos' kategoriją.

### Debian GNU/Linux

Debian yra daug didesnis projektas su didesne bendruomene, turinti stabilią, testavimo ir nestabilias atšakas, siūlanti apie 20,000 binarinius paketus. Arch neskaldo savo paketų į "-dev" ir "-common", priešingai nei Debian, užtat Arch saugyklos yra žymiai mažesnės. Debian turi daug karštesnę poziciją ties nemokama programinę įranga. Arch yra daug atlaidesne, kai reikalas ateina prie GNU pavadintų 'mokamų' paketų. Debian dizainas požiūris fokusuojamas daugiau prie stabilumo ir griežto testavimo. Arch sufokusuota daugiau prie paprastumo, minimalumo filosofijos. Ji taip pat siūlo pačius naujausius programinės įrangos paketus. Arch paketai daugiau yra dabartiniai, negu Debian Stabilūs ar Testuojami, dažniausiai jie yra ekvivalentiški su Debian nestabiliais. Kartu Debian ir Arch siūlo gerai išlaikoma paketų valdymo sistema. Arch yra pagrindinės versijos modelio, tuo tarpu Debian yra išleidžiama su "įšauliais" paketais. Debian yra pasiekiama daugeliams architektūrų: alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 ir sparc. Tuo tarpu Arch yra pasiekiamas tik i686 ir x86_64 architektūroms. Arch siūlo daugiau tikslingą palaikymą statant užsakomus paketus iš išorinio pradinio kodo, padedant portų paketų statymo sistemai. Debian nesiūlo portų sistemos, remdamasi tik savo didelėmis binarinių paketų saugyklomis. Arch įdiegimo sistema siūlo tik minimalų pagrindą, su skaidrius sistemos konfigūravimu. Tuo tarpu Debian metodas siūlo daugiau automatinį priėjimą prie konfigūracijos, kartu su keletais įdiegimo metodais. Debian naudoja SysVinit, tuo tarpu Arch naudoja paprastą *BSD stiliaus iniciaciją. Arch palaiko lopymą prie minimumo, taip vengdama problemų, kurias vystytojai negali apžvelgti.

### Frugalware

Arch yra tekstiškai paremta ir orientuota į komandinę eilutę. Frugalware prisijaukino Arch [pacman](/index.php/Pacman "Pacman") kaip savo paketų tvarkyklę, bet naudoja bzipped archyvus. Palyginus, Arch naudoja gzipped archyvus, nes tai leidžia palaikyti paketų įdiegimo tikslumo. Frugalware numatomai nepalaiko JFS failų sistemos. Frugalware daugiau nėra paremta Slackware. Jinai daugiau egzistuoja kaip savarankiška i686 distribucija. Arch fundamentaliai yra kitokia sistema, kuri yra įdiegiama kaip minimali aplinka ir plečiama su pacman, vartotojo nuožiūra. Frugalware įdiegiama per DVD, su numatyta programinę įranga ir darbine aplinka. Tai jau nuspręsta už vartotoją. Frugalware turi išleidimo grafiką. Vėl gi, Arch yra daugiau sufokusuota prie paprastumo, minimalumo, kodo teisingumo ir naujausių paketų su pagrindinės versijos modelio principu.

## Išorinės nuorodos

*   [DistroWatch.com](http://distrowatch.com/)