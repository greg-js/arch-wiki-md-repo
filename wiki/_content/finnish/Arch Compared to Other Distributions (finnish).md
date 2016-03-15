Tämä sivu kiteyttää joitakin yhtäläisyyksiä ja eroja Arch Linuksin ja muiden GNU/Linux jakeluiden tai `UNIX`in kaltaistaisten käyttöjärjestelmien välillä. Huomioi että paras tapa verrata Archia muihin jakeluihin on asentaa ja kokeilla muita jakeluita itse. Archilla on mahtava käyttäjäyhteisö joka on aina valmis auttamaan uutta käyttäjää. Alla oleva yhteenveto on tarkoitettu antamaan sinulle tarpeeksi tietoa päättääksesi onko Arch Linux sinulle sopiva.

## Contents

*   [1 Lähdekoodipohjainen](#L.C3.A4hdekoodipohjainen)
    *   [1.1 Arch vs Gentoo](#Arch_vs_Gentoo)
    *   [1.2 Arch vs Sorcerer/Lunar-linux/Sourcemage](#Arch_vs_Sorcerer.2FLunar-linux.2FSourcemage)
    *   [1.3 Arch vs Rock](#Arch_vs_Rock)
*   [2 Minimalistinen](#Minimalistinen)
    *   [2.1 Arch vs Crux](#Arch_vs_Crux)
    *   [2.2 Arch vs Slackware](#Arch_vs_Slackware)
*   [3 Graafiset Jakelut](#Graafiset_Jakelut)
    *   [3.1 Arch vs Ubuntu](#Arch_vs_Ubuntu)
    *   [3.2 Arch vs Zenwalk](#Arch_vs_Zenwalk)
    *   [3.3 Arch vs Fedora](#Arch_vs_Fedora)
    *   [3.4 Arch vs Mandriva](#Arch_vs_Mandriva)
    *   [3.5 Arch vs SUSE](#Arch_vs_SUSE)
    *   [3.6 Arch vs PCLinuxOS](#Arch_vs_PCLinuxOS)
*   [4 The *BSDt](#The_.2ABSDt)
    *   [4.1 Arch vs FreeBSD](#Arch_vs_FreeBSD)
    *   [4.2 Arch vs NetBSD](#Arch_vs_NetBSD)
    *   [4.3 Arch vs OpenBSD](#Arch_vs_OpenBSD)
*   [5 Muut](#Muut)
    *   [5.1 Arch vs Debian GNU/Linux](#Arch_vs_Debian_GNU.2FLinux)
    *   [5.2 Arch vs Frugalware](#Arch_vs_Frugalware)
    *   [5.3 Arch vs Gobolinux](#Arch_vs_Gobolinux)
    *   [5.4 Arch vs Minix 3](#Arch_vs_Minix_3)

# Lähdekoodipohjainen

Lähdekoodipohjaiset jakelut ovat erittäin alustariippumattomia antaen hyödyn siitä että käyttöjärjestelmä on käännetty juuri kyseenomaiselle alustalle. Haittapuolina voidaan mainita koodin kääntämiseen kuluva aika. Archin pohja ja kaikki paketit ovat optimoituja i686 ja x86-64 arkitehtuureille tarjoten potentiaalisen suorituskyky edun i386/i486/i586 jakeluihin nähden.

## Arch vs Gentoo

Koska Arch asennus on binäärinen, on se paljon nopeampi suorittaa kuin lähdekoodipohjaisen Gentoon asennus. Sekä Gentoo että Arch tarjovat binääri että lähdekoodipohjaisia paketteja mutta Gentoon perusasennus on lähdekoodipohjainen kun taas Arch on binääripohjainen. Molemmat käyttävät 'liukuvaa julkaisua' Archin PKGBUILD:it ovat laajalti nähty helpommiksi ja nopeammiksi tehdä kuin Gentoon ebuildit. Gentoo tarjoaa tukea x86, ppc, sparc, alpha, amd64, mips, hppa ja itanium alustoille kun Arch tarjoaa vain i686 ja x86-64 alustoille (käyttäjäpohjainen i586-sivuprojekti on tekeillä). Ei ole olemassa dokumentoitua todistetta että Gentoo olisi yhtään nopeami kuin Arch ja päinvastoin. Archin suunnittelun lähtökohdat ovat enemmän keskittyneitä yksinkertaisuuteen ja minimalistisuuteen kun taas Gentoo keskittyy globaalisti koko koodin käännös jokaisen yksityiskohdan hallintaan. Molemmat jakelut sallivat kattavan kustomoinnin joten Gentoon käyttäjät tuntevat itsensä kotoisaksi käyttäessään Archia.

## Arch vs Sorcerer/Lunar-linux/Sourcemage

Sorcerer/Lunar-linux/Sourcemage (SLS) ovat kaikki lähdekoodipohjaisia kuten Gentookin mutta ovat sukua toisilleen. SLS jakelut käyttävät varsin yksinkertaisia skriptejä pakettien luomiseen ja käyttävät globaalia asennustiedostoa käännösprosessin kustomointiin kuten Archin ABS systeemi. SLS työkalut tekevät täyden riippuvuuksien tarkistuksen (ja hanskaavat valinnaisen ominaisuudet) and paketin seurannan (ja poiston/päivityksen). SLS jakeluille ei ole binääri-paketteja vaikka kaikki pystyvät palaamaan aikaisemmin asennettuun pakettiin jos tarve vaatii.

Asennus koostuu perusjärjestelmän asennuksesta (kuten Archikin: i686-optimoitu, CLI ja ncurses menut, vain runkotyökalut) ja koko pohjan uudelleen (valinnaisesta) kääntämisestä jälkeenpäin. Selvästikkään millään jakeluilla ei ole "standardi" ikkunamanageria eivätkä ne asenna X palvelinta perusasennuksen yhteydessä. Mutta ne tarjoavat helpon tavan X palvelimen asennukseen (X.Org 6.8 tai 7, XFree86).

SLS on monimutkainen historia. Parhaan yhteenvedon asiasta voit lukea: [http://wiki.sourcemage.org/SourceMage/History](http://wiki.sourcemage.org/SourceMage/History)

Lunar Linux: [http://lunar-linux.org/](http://lunar-linux.org/)
SourceMage: [http://www.sourcemage.org/](http://www.sourcemage.org/)
Sorcerer: [http://sorcerer.berlios.de/](http://sorcerer.berlios.de/)

## Arch vs Rock

*Vapaa käännös osoitteesta [http://www.rocklinux.org/wiki/About](http://www.rocklinux.org/wiki/About)*

ROCK Linux on joustava Linux jakelun rakennussarja eli se on työkalukokoelma oman Linux jakelun rakentamiseen. Katso myös Tehtävä tavoitteemme. Jos sinua ei kiinnosta rakentaa omaa jakelu mutta olet kiinnostunut hyvästä peruskäyttöön soveltuvasta jakelusta sinun kannattaa katsastaa Crystal ROCK. [http://www.rocklinux.org/wiki/Crystal_ROCK](http://www.rocklinux.org/wiki/Crystal_ROCK)

Jakelu joka on periaatteessa vain jakelun rakennustyökalukokoelma. Samat syyt pätee tähänkin kuten muilla lähdekoodipohjaisille, aika mikä kuluu koodin kääntymistä odottamiseen. Näyttäisi toimivan usealla prosessoriarkitehtuurilla jne.

# Minimalistinen

Minimalistiset jakelut ovat hyvin verrattavissa Archin kanssa sillä näillä on monia yhtäläisyyksiä.

## Arch vs Crux

*   K: Perustuuko Arch `CRUX`iin?
*   V: Ei. Arch on itsenäisesti kehitetty ja se ei perustu mihinkään toiseen GNU/Linux jakeluun.

Arch Linuxin perustaja, Judd Vinet, käytti `CRUX` ennen kuin hän loi Archin. Arch on `CRUX`in ideoiden inspiroimana rakennettu tyhjästä johon sitten C -ohjelmointikielellä koodattu pacman lisättiin. Molemmat jakavat jotain periaatteita; esimerkiksi molemmat ovat arkitehtuurioptimoija, minimalistisia, P.S.S.T. Molemmat tulevat ports-kaltaisen systeemillä, käyttävät *BSD-tyylisiä aloitusskriptejä ja (kuten *BSD) molemmat tarjoavat minimaalisen perusympäristön jota käyttäjät voivat laajentaa. Archissa on pacman joka hallitsee binääri-pohjaiset paketit ja toimii saumattomasti ABSin kanssa, Archin ports-kaltainen systeemi. `CRUX` käyttää järjestelmää nimeltä prt-get, joka sen oman ports-järjestelmän kanssa hoitaa riippuvuuksien hallinnan mutta kääntää kaikki paketit suoraan lähdekoodista. Arch tukee virallisesti x86-64 ja i686 arkitehtuureja mutta `CRUX` vain i686\.

## Arch vs Slackware

Slackware ja Arch ovat melko samanlaisia siinä että molemmat ovat yksinkertaisia jakeluita jotka keskittyvät eleganttiin ja minimalistisuuteen. Slackware on kuuluisa muokkaamattomista paketeistaan aina ytimestä saakka. Arch tyypillisesti paikkaa paketteja hieman (vähenevässä määrin ajan kuluessa). Molemmat käyttävät BSD-tyylisiä käynnistysskriptejä. Arch tarjoo paketin hallintaan pacmanin joka toisin kuin Slackwaren perustyökalut, tarjoaa automaattisen riippuvuuksien hallinnan ja sallii helpot järjestelmän päivitykset. Slackwaren käyttäjät tyypillisesti suosivat manuaalista riippuvuuksien ratkomista vannoen sen tuoman järjestelmän hallinnan puoleen. Arch on liukuvaa julkaisua käyttäjä järjestelmä. Slackware on maltillisempi julkasuidensa suhteen suosien vakaiksi todettuja paketteja. Arch on 'tuoreempi' näin ollen. Arch tukee i686 ja x86_64 kun taas Slackware on tehty pyörimään i486 järjestelmissä. Molemmissa on saatavilla ports-kaltainen järjestelmä normaalien paketinhallinta ohjelmien lisäksi, - (epävirallinen) Slackbuild järjestelmä on erittäin samanlainen Arch Build System:in (ABS) vaikka jälkimmäinen onkin automaattisempi. Arch on erittäin hyvä järjestelmä Slackwaren käyttäjille jotka tahtovat automaattisen riippuvuuksien ratkonnan ja uudempia paketteja.

# Graafiset Jakelut

Joskus 'aloittelija' jakeluiksi kutsutuilla graafisilla jakeluilla on paljon yhtäläisyyksiä keskenään, ja Arch on hyvin erillainen näistä. Arch on teksti-pohjainen ja komentorivi suuntautunut. Arch voi ehkä olla parempi vaihtoehto jos haluat oppia GNU/Linuksia rakentamalla sen alusta asti itse. Graafiset jakelut tapaavat tulla graafisella asennusohjelmalla (kuten Fedoran Anaconda) ja graafisilla järjestelmän asennustyökaluilla (kuten SuSE:n YaST). Tarkemmat erot listattuna alla.

## Arch vs Ubuntu

Ubuntu on erittäin suosittu Debian-pohjainen jakelu joka on Canonical Ltd. sponsoroima, kun taas Arch on itsenäisesti kehitetty järjestelmä joka on rakennettu alusta asti itse. Archilla on yksinkertaisempi perusta kuin Ubuntulla. Jos haluat kääntää oman ytimesi, kokeilet kehityksen kärjessä olevia CVS:n kautta jaettavia projekteja tai käännät ohjelmia lähdekoodista niin Arch on paremmin suunnattu sinulle. Jos halut järjestelmän joka toimii suoraan ilman mitään ylimääräistä säätämistä Ubuntu on parempi vaihtoehto sinulle. Arch on minimalistisempi jo asennuksesta lähtien luottaen käyttäjän taitoihin kustomoida järjestelmä heidän tarpeihinsa sopivaksi. Yleisesti, kehittäjät ja säätäjät tuntevat itsensä kotoisammaksi Archin äärellä kuin Ubuntun. Monet entiset Ubuntun käyttäjät ovat siirtyneet käyttämään Archia.

## Arch vs Zenwalk

Zenwalk on pohjautettu Slackwaresta ja on käytettävä ja moderni. Suurin ero on siinä että Zenwalk sentaa paketit jotka kehittäjä ovat valinneet sinulle. Tämä säästää aikaa jos pidät heidän valinnastaan mutta on haitaksi jos haluat asentaa jotain muuta.

## Arch vs Fedora

Fedora on Red Hat:stä erotettu jakelu ja on jatkuvasti yksi suosituimmista jakeluista. Sellaisena Fedoran taustalla vaikuttaa massiivinen käyttäjäyhteisö ja paljon valmiiksi käännettyjä binääripaketteja. Fedora on RPM-pohjainen. Arch käyttää pacmania hallitsemaan tar.gz paketteja. Fedora on kuuluisa siitä ettei se tuo esim MP3 formaattia patentti syistä. Arch on joustavampi tämän ja muiden medioiden suhteen. Fedora käyttää graafista asennusohjelmaa. Arch käyttää ncurses-pohjaista asennusta. Fedora on grafiikka-vetoinen. Arch on yksinkertaisempi kuin Fedora, luottaen käyttäjien suorittamaan manuaaliseen säätöön. Fedoralla on säännölliset julkaisut. Arch käyttää 'liukuvaa julkaisua'. Archin suunnittelu lähtökohdat ovat suunnattu kevyeen eleganttiin ja minimalistista näkökantaa silmällä pitäen eikä automaattista konfigurointia kohden kuten Fedora. Fedora on innovatiivinen ja hiljattain sai ylistystä sisällyttäen SELinux ja GCJ käännetyt paketit poistaakseen SUNin JRE:n. Versiosta 8 lähtien Fedora ei tuo JFS tai ReiserFS tiedostojärjestelmiä.

## Arch vs Mandriva

Mandriva Linux (entinen Mandrakelinux) luotiin 1998 tavoitteena luoda GNU/Linux jota kaikkien on helppo käyttää. Se on RPM-pohjainen ja käyttää urpmi paketin hallintaa. Taas, Archilla on yksinkertaisempi lähtökohta, luottaen manuaaliseen konfigurointiin ja on suunnattu osaavammille käyttäjille.

## Arch vs SUSE

SUSE on keskittynyt kattavan YaST asennustyökalun ympärille jolla lähes kaikki käyttäjän säädöt voidaan toteuttaa. Arch ei tarjoa vastaavaa sillä se olisi ristiriidassa Arhin [TheArchWay_(Suomi)periaatteiden](/index.php?title=TheArchWay_(Suomi)&action=edit&redlink=1 "TheArchWay (Suomi) (page does not exist)") kanssa. SUSE on täten yleisesti ottaen suunnattu vähemmin Linuksia osaaville tai heille jotka haluavat GUI-suuntaisen ympäristön, automaattiset säädöt ja suoraan laatikosta toimivan järjestelmän.

## Arch vs PCLinuxOS

PCLinuxOS on suosittu Mandriva-pohjainen jakelu tarjoten täydellisen työpöytäympäristön joka on suunniteltu käyttäjäystävällisyyttä ja yksinkertaiseksi vaikka yksinkertainen tässä tapauksessa poikkeaa Archin näkemyksestä. Arch on suunniteltu yksinkertaiseksi perustaksi joka on kustomoitavissa alusta asti ja on suunnattu edistyneimmille käyttäjille. PCLOS käyttää apt paketinhallintaa liittymänä RPM-paketeille. Arch käyttää omaa itsenäisesti kehitettyä pacman paketinhallintaa .tar.gz paketeilla. PCLOS on GUI-suuntainen tarjoten GUI raudan tunnistustyökaluja ja Synaptic paketinhallinnan graafisen ulkoasun and lupaa ettei käyttäjän tarvitse käyttää komentoriviä mihinkään. Arch on komentorivi suuntautunut ja suunniteltu yksinkertaisempaa lähestymistapaa järjestelmän säätämiseen, hallintaa ja ylläpitoon. PCLOS suosittelee 256MB RAM minimivaatimuksena. Kevyempänä Arch pyörii järjestelmissä joissa on huomattavasti vähemmän muistia, vaatien noin 64MB muistia perusasennukselle ja pyörii sulavasti millä tahansa modernilla koneella.

# The *BSDt

Archilla on ehkä enemmän yhtäläisyyksiä eri BSD:n kanssa suunnittelu näkökannan puolesta kuin muilla GNU/Linux jakeluilla. BSDt juontavat juurensa Berkeley `UNIX`sta. Siksi *BSDn eivät ole GNU/Linux jakeluita vaan `UNIX`-kaltaisia käyttöjärjestelmiä.

## Arch vs FreeBSD

Sekä Arch ja [FreeBSD](http://www.freebsd.org/about.html) tarjoavat ohjelmia jotka voidaan asentaa joko binääripaketeista tai kääntää ports-järjestelmästä. Molemmat käyttävät samanlaista aloitusjärjestelmää. FreeBSD kehuu sillä että järjestelmä on 'kokonaisempi' kuin GNU/Linux jakelut ja jokainen sovellus on 'portattu' FreeBSD:lle ja varmistettu että se toimii. Arch suuntaa enemmänkin julkaisemaan viimeisimpiä sovelluksia. Molemmat käyttävät /etc/rc.conf tiedostoa pääasiallisena konfigurointitiedostona. FreeBSD:n lisenssi on enemmän 'vapaa-kuin-olut' kuin mitä jotkin GNU/Linux käyttäjät suosivat. Arch on julkaistu GPL-lisenssillä. FreeBSD:ssä, kuten Archissa, päätökset on annettu käyttäjälle. Tämä on ehkä kaikkein kovin kilpailija Archille sille molemmat järjestelmät ovat hyvin samanlaisia.

## Arch vs NetBSD

NetBSD on ilmainen, turvallinne ja erittäin alustariippumaton `UNIX`-kaltainen avoimen lähdekoodin käyttöjärjestelmä joka on saatavilla yli 50 alustalle, 64-bittisistä Opteroneista ja työasemista aina kämmentietokoneisiin ja sulautettuihin järjestelmiin saakka. Sen selkeä suunnittelu ja edistykselliset ominaisuudet tekevät siitä erinomaisen tuotanto ja tutkimusympäristöihin ja käyttäjätuotte koko lähdekoodilla. Monet ohjelmat ovat helposti saatavilla pkgsrc:n, NetBSD Packages Collecionin kautta. Arch ei ehkä toimi niin monella alustalla kuin NetBSD mutta i686 alustalla se saattaa tarjota enemmän ohjelmia. Myös, oletuksena pkgsrc lataa koneelle lähdekoodin ja kääntää ohjelman siitä missä taas Arch käyttää binääripaketteja. Arch jakaa monta yhtäläisyyttä NetBSD:n kanssa; molemmat käyttävät /etc/rc.conf tiedostoa pääasiallisena konfigurointitiedostona, molemmat ovat minimalistisia ja kevyitä, molemmat tarjovat ports-kaltaisen järjestelmän ja binääripaketteja. Molemmilla on myös asiallinent ja osaavat kehittäjät ja käyttäjäyhteisöt. Arch myös lainaa BSD:stä käynnistys rutiinin.

## Arch vs OpenBSD

OpenBSD projekti tuottaa vapaan, monialustaisen 4.4BSD:hen pohjautujan`UNIX`in-kaltaisen käyttöjärjestelmän. Kehitys keskittyy portattavuuteen, standardien noudattamiseen, koodin oikeellisuuteen, turvallisuuteen ja integroituun kryptokrafiaan. Arch keskittyy enemmän yksinkertaisuuteen, eleganssiin ja minimalistisuuteen ja uusimpiin paketteihin. OpenBSD tukee binääriemuloinnin avulla useimpia ohjelmia SVR4 (Solaris), FreeBSD, GNU/Linux, BSD/OS, SunOS ja HP-UX käyttöjärjestelmistä. OpenBSD on ehkä turvallisin kaikista käyttöjärjestelmistä. Archin ja OpenBSD:n yhtäläisyyksiä on pieni, elegantti perusasennus ja molemmat käyttävät ports-järjestelmää ja paketinhallinta järjetelmiä jotta ohjelmien asentamiseen jota ei tule perusasennuksen mukana. Toisin kuin GNU/Linux käyttöjärjestelmissä kuten Archissa ydin ja yleisimmät työkalut kehitetään samaan aikaan suuressa lähdekoodin säilytyspaikassa.

# Muut

Muut käyttöjärjestelmät kuuluvat tähän kategoriaan.

## Arch vs Debian GNU/Linux

Debian on paljon suurempi projekti ja yhteisö ja jossa on vakaa, testi ja epävakaat haarat, tarjoten yli 18,000 binääripakettia. Arch ei jaa pakettejaan -dev ja -common paketteihin kuin Debian, siksi Archin varastot voivat näyttää pienemmiltä. Arch on joustavampi kun tullaan 'ei-vapaiden' pakettien äärein kuin GNU. Debianin lähtökohta on olla vakaa ja suorittaa kunnon testaus. Arch on keskittynyt enemmän yksinkertaisuuden periaatteelle ja tarjoaa uusimpia paketteja. Arhin paketit ovat uudempia kuin mitä löytyy Debianin Vakaasta tai Testi haaroista ollen samalla tasolla Epävakaan haaran kanssa. Molemmissa on erinomaiset paketinhallinta työkalut. Arch käyttää 'liukuvaa julkaisua' kun taas Debianin Vakaa haara julkaistaan 'jäädytetyin' paketein. Debian on saatavilla useille arkitehtuureille kuten alpha, arm, hppa, i386, ia64, m68k, mips, mipsel, powerpc, s390 ja sparc. Arch on saatavilla vain i686 ja x86_64 alustoille. Arch tarjoaa suoraan tukea omien pakettien luomiseen ja tarjoaa myös ports-kaltaisen järjestelmän. Debian ei tarjoa ports-järjestelmää luottaen suureen binääripakettiensa määrään. Archin asennus suuntaa minimalistiseen perusasennukseen siinä missä Debian tarjoaa automaattisempaa lähtökohtaa.

## Arch vs Frugalware

Arch on teksti-pohjainen ja komentorivi suuntautunut. Frugalware tarjoaa paremman monikielisyyden tuen. Frugalware on ottanut Archin pacmanin käyttöön paketin hallinta järjestelmäkseen vaikka paketit eivät ole suoraan yhteensopivia. Frugalware ei tuo JFS-tiedostojärjestelmää oletuksena. Frugalware ei enää pohjaudu Slackwareen vaan on oma jakelunsa ja joka on optimoitu i686 alustalle. Arch on pohjimmiltaan erillainen järjestelmä. Frugalware tulee DVD:llä ja sisältää oletussovellukset ja työpöytäympäristön joka on valittu jo käyttäjälle kun taas Arch asentaa vain perustan jota käyttäjä itse laajentaa. Frugalware tulee säännöllisin julkaisuin kun taas Arch käyttää liukuvaa mallia.

## Arch vs Gobolinux

Gobolinux:lla on oma uniikki paketin hallinta siten ettei siinä ole sellaista. Tiedostojärjestelmä tunnistaa että kaikki ohjelmat ovat /Programs hakemistossa ja kaikki toimii symlink magian avulla. Pääset eroon Ohjelmasta X poistamalla sen symbolisen linkin /Programs kansiosta. Gobolinux ei ole optimoitu i686 alustalle. Se tukee lähdekoodista asentamista.

## Arch vs Minix 3

Arch on kokonainen jakelu modernilla yhteisöllä ja rauta tuolla. Minix 3 on sutjakka, käytettävä kehityskäyttöön suunnattu käyttöjärjestelmä mielenkiintoisilla ominaisuuksilla kuten [mikroydin](https://en.wikipedia.org/wiki/Microkernel "wikipedia:Microkernel"). [http://www.minix3.org/](http://www.minix3.org/)