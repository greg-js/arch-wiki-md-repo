## Contents

*   [1 Johdanto](#Johdanto)
    *   [1.1 Mikä on Arch Linux?](#Mik.C3.A4_on_Arch_Linux.3F)
*   [2 Lisenssi](#Lisenssi)
*   [3 Ennen asennusta](#Ennen_asennusta)
    *   [3.1 Arkkitehtuurit](#Arkkitehtuurit)
    *   [3.2 Saatavat levykuvatiedostot](#Saatavat_levykuvatiedostot)
    *   [3.3 AIF, asennustyökalu](#AIF.2C_asennusty.C3.B6kalu)
    *   [3.4 Arch Linuxin hankinta](#Arch_Linuxin_hankinta)
    *   [3.5 Asennusmedian valmistaminen](#Asennusmedian_valmistaminen)

# Johdanto

## Mikä on Arch Linux?

Arch Linux on yhteisön kehittämän i686-optimoitu Linux-jakelu, joka pohjautuu alun perin CRUX:ista saatuihin ideoihin. Sen kehittäminen keskittyy yksinkertaisuuteen, eleganssiin, oikeellisuuteen ja uusimpiin ohjelmistoihin. Sen kevyt ja yksinkertainen suunnittelu tekee sen helpoksi rakentaa minkälaisen järjestelmän vain haluaa.

# Lisenssi

Arch Linux ja skriptit ovat kopiosuojattuja (©2002-2007 Judd Vinet, ©2007-2009 Aaron Griffin) ja GNU General Public License-lisenssin alaisia.

# Ennen asennusta

## Arkkitehtuurit

Arch Linux on optimoitu i686 ja x86-64 suorittimille ja ei siten toimi vanhemman tai yhteensopimattoman sukupolven x86 suorittimilla (i386, i486 tai i586). Minimivaatimukset ovat Pentium Pro, Pentium II tai AMD Athlon (K7) suoritin tai korkeampi. (Teknisesti, suorittimet ilman cmov- ominaisuutta kuten AMD K6 ja VIA C3 ovat myös i686- suorittimia, mutta me käytämme GCC- kääntäjien kokoelmaa ja se tarvitsee cmov:ia) Ennenkuin asennat Arch Linuxin, sinun pitäisi valita mitä asennusmuotoa sinä käytät.

## Saatavat levykuvatiedostot

Arch Linux tarjoaa iso- levykuvia joita voi kirjoittaa CD-levyille tai muistitikuille.

Käyttöjärjestelmän lataaja on Isolinux. On kaksi vaihtoehtoa jokaiselle asennusmuodolle jotka eroavat toisistaan vain mukana olevilla paketeilla.

*   "core" levykuvat sisältävät tilannekuvan peruspaketeista. Nämä levykuvat parhaiten sopivat niille joilla on Internet-yhteys joka on hidas tai on vaikea säätää.
*   "net" levykuvat eivät sisällä mitään paketteja, ja käyttävät aina Internetiä asentaakseen paketteja.

Kummankin tyyppisellä levykuvalla voidaan tehdä "net" asennus, josta saadaan ajan tasalla oleva järjestelmä, tosin "core" levykuvalla niin ei tarvitse tehdä. Kaikkia levykuvia voidaan käyttää myös täysin toimivina palautusympäristöinä. Levykuvat toimivat niinkuin mikä tahansa tavallinen asennettu Arch Linux- järjestelmä. Itse asiassa ne ovat täysin samoja, vain asennettu CD-levylle tai muistitikulle kovalevyn sijaan. Ne sisältävät koko "base" ohjelmistopaketin sekä monia verkkoon liittyviä työkaluja ja ajureita ja aif paketin. Jos on jotain muuta jota tarvitset, kytke Internet-yhteytesi ja asenna se pacmanin avulla. Lyhyt pacman komentoreferenssi löytyy tämän dokumentin lopussa.

Kaikki levykuvat ovat saatavissa i686, x86-64 tai kaksois varianteilla. Jälkimmäinen sisältää kummatkin ja antaa sinun valita arkkitehtuurin käynnistyksessä.

## AIF, asennustyökalu

Arch Linux käyttää AIF eli 'Arch Linux Installation Framework' työkalua tehdäkseen asennuksia. Tämä työkalu, joka on toteutettu bash-kielellä, koostuu kirjastoista jotka tekevät monia toimintoja (asentaa paketteja, säätää levyjä jne.) ja joitakin niinsanottuja menettelyjä jotka käyttävät näitä kirjastoja tarjoakseen helpon tavan tehdä asennuksen tai pienempiä liittyviä tehtäviä ('osittaisia menettelyjä'). Nämä menettelyt tulevat oletuksena:

*   interactive: Vuorovaikutteinen asennus, joka kysyy joitakin kysymyksiä, opastaa asennuksen ja auttaa kohdejärjestelmän konfiguroinnissa muuttamalla joitakin asetuksia automaattisesti riippuen siitä mitä teit aiemmin (esim. verkkoasetukset). Asennetussa järjestelmässä on aluksi vain muokattavissa oleva joukko "base" paketteja asennettu millä tahansa apuohjelmilla tai ajureilla mitä tarvitset päästäksesi nettiin. Sitten kun olet onnistuneesti käynnistänyt asennettuun järjestelmään, voit suorittaa koko järjestelmän päivityksen ja asentaa muita paketteja mitä tarvitset (alias /arch/setup)
*   automatic: Automisoitu menettely joka on suunniteltu vähälle tai olemattomalle vuorovaikutukselle. Käyttää profiileja kohdejärjestelmän konfiguroinnissa.Katso /usr/share/AIF/examples/ esimerkki profiileille. Esimerkit totetuttavat melko yleisiä skenaarioita, mutta voit vapaasti muuttaa niitä miten haluisit asentaa lisää paketteja, tehdä muutoksia jne.
*   base: perus, pieni-vuorovaikutteinen asennus jossa on joitakin yleisiä oletusarvoja. Muut menettelyt perivät tästä asetteluja, se ei ole tarkoitettu käytettävän suoraan.
*   partial-configure-network: näyttää verkon konfigurointi askeleen interactive menettelystä, joka auttaa sinua konfiguroimaan verkon live ympäristössä.
*   partial-disks: Käsittele levyn alijärjestelmää tai tee rollback
*   partial-keymap: Vaihda sinun näppäimet / konsolin fontin asetuksia. (alias km)

Menettelyjen kuten partial-keymap ja partial-configure-network hyöty verrattuna loadkeys tai ifconfig työkalujen suoraan käyttöön on se, että kun käytät interactive menettelyä, sinua kysytään haluatko käyttää asetuksia kohdejärjestelmässä.

Jos haluat mennä vielä pidemmälle, voit myös:

*   Kirjoittaa sinun omia menettelyjä tai ohittaa tiettyjä osia muista menettelyistä
*   Kirjoittaa sinun omia kirjastoja jotka tarjoavat uusia toimintoja
*   Luoda sinun omia asetuksia menettelyille jotka tukevat niitä (esim. automatic)

Katso AIF readme-tiedostoa lisätiedoille.

## Arch Linuxin hankinta

*   Voit ladata Arch Linuxin mistä vaan peilistä joka on listattu [lataus-sivulla](https://www.archlinux.org/download/).
*   Voit myös ostaa asennus-CD:n Archux, OSDisc, tai LinuxCD sivuilta ja saada se lähetettyä minne tahansa maailmassa.

## Asennusmedian valmistaminen

*   Lataa sinun valitsemasi levykuva torrentin avulla (paras vaihtoehto) tai sinun suosikki peilistä.
*   Lataa iso/<release>/sha1sums.txt
*   Varmista .iso levykuvan eheys käyttämällä sha1sum-työkalua:

sha1sum --check sha1sums.txt

archlinux-XXX.iso:OK

*   Polta ISO levykuva CD-R tai CD-RW levylle käyttämällä sinun valitsemaasi ohjelmistoa, tai jos käytät USB-laitetta, kuten muistitikkua, käyttämällä dd ohjelmaa tai vastaavaa:

dd if=archlinux-XXX.iso of=/dev/sdX

Ole varma että käytät /dev/sdX polkua etkä /dev/sdX1 polkua. Tämä komento poistaa kaikki sinun muistitikun tiedostot peruuttamattomasti, joten ole varma että sinulla ei ole tärkeitä tiedostoja siinä ennenkuin teet tämän.