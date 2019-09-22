Alla katettujen kysymysten lisäksi voit tarkistaa [The Arch Way](/index.php/Arch_Linux_(Suomi) "Arch Linux (Suomi)"), [Arch Linux](/index.php/Arch_Linux "Arch Linux") artikkelit. Kaikki kolme sisältävät paljon hyvää materiaalia Arch Linuksista.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Yleistä](#Yleistä)
    *   [1.1 Q) Olen GNU/Linux -aloittelija. Pitäisikö minun käyttää Arch Linuxia?](#Q)_Olen_GNU/Linux_-aloittelija._Pitäisikö_minun_käyttää_Arch_Linuxia?)
    *   [1.2 Q) Milloin uusi julkaisu on valmis?](#Q)_Milloin_uusi_julkaisu_on_valmis?)
    *   [1.3 Q) Arch tarvitsee enemmän/vähemmän julkisuutta (esim. mainontaa)](#Q)_Arch_tarvitsee_enemmän/vähemmän_julkisuutta_(esim._mainontaa))
    *   [1.4 Q) Arch tarvitsee enemmän dokumentaatiota](#Q)_Arch_tarvitsee_enemmän_dokumentaatiota)
    *   [1.5 Q) Arch tarvitsee enemmän kehittäjiä](#Q)_Arch_tarvitsee_enemmän_kehittäjiä)
    *   [1.6 Q) Miksi Arch on niin hidas? Luulin että sen pitäisi olla nopea!](#Q)_Miksi_Arch_on_niin_hidas?_Luulin_että_sen_pitäisi_olla_nopea!)
    *   [1.7 Q) Miksi internet on hitaampi verrattuna muihin käyttöjärjestelmiin?](#Q)_Miksi_internet_on_hitaampi_verrattuna_muihin_käyttöjärjestelmiin?)
*   [2 Paketinhallinta](#Paketinhallinta)
    *   [2.1 Q) Löysin virheen paketista X. Mitä minun pitäisi tehdä?](#Q)_Löysin_virheen_paketista_X._Mitä_minun_pitäisi_tehdä?)
    *   [2.2 Q) Arch paketit tarvitsevat yhtenäisen nimeämiskäytännön. .pkg.tar.gz on liian pitkä ja monimutkainen](#Q)_Arch_paketit_tarvitsevat_yhtenäisen_nimeämiskäytännön._.pkg.tar.gz_on_liian_pitkä_ja_monimutkainen)
    *   [2.3 Q) Pacman tarvitsee kirjaston jotta muut ohjelmat pääsevät helposti käsiksi pakettien tietoihin](#Q)_Pacman_tarvitsee_kirjaston_jotta_muut_ohjelmat_pääsevät_helposti_käsiksi_pakettien_tietoihin)
    *   [2.4 Q) Miksei Pacmanilla ole virallista graafista käyttöliittymää?](#Q)_Miksei_Pacmanilla_ole_virallista_graafista_käyttöliittymää?)
    *   [2.5 Q) Pacman tarvitsee Ominaisuuden X!](#Q)_Pacman_tarvitsee_Ominaisuuden_X!)
*   [3 Asennus](#Asennus)
    *   [3.1 Q) Arch tarvitsee paremman asennusohjelman, ehkä jopa graafisen sellaisen.](#Q)_Arch_tarvitsee_paremman_asennusohjelman,_ehkä_jopa_graafisen_sellaisen.)

# Yleistä

## Q) Olen GNU/Linux -aloittelija. Pitäisikö minun käyttää Arch Linuxia?

**A)** Tämä kysymys on herättänyt paljon keskustelua. Arch on suunnattu kokeneemmille GNU/Linux -käyttäjille, mutta joidenkin mielestä Arch ei ole huono paikka lähteä liikkeelle. Jos olet aloittelija joka haluaisi käyttää Archia, ymmärrä että sinun täytyy oppia ja hyväksyä Archin olevan pitkälti tee-se-itse -jakelu jonka käyttäjä itse kokoaa ja jota hallitsee. Ennen lisäkysymysten esittämistä tee oma tutkimuksesi googlaamalla, Wikiä tutkimalla, keskustelupalstalta etsimällä ja vanhat FAQ:t lukemalla. Näin tehtyäsi tulet pärjäämään hyvin. Yritä myös muistaa että kovin moni ei jaksa vastata uudelleen ja uudelleen samoihin peruskysymyksiin; syyttä ei tätäkään tietolähdettä kirjoitettu ja saatettu luettavaksi.

## Q) Milloin uusi julkaisu on valmis?

**A)** Arch Linuxin julkaisut tapahtuvat samaan aikaan isompien kernelpäivitysten kanssa. Ne ovat kuitenkin lähinnä /core-pakettivaraston tilannevedoksia ja asennusskriptin ominaisuuspäivityksiä. Rolling release -mallin ansiosta jokainen Arch Linux -järjestelmä pysyy ajan tasalla ja kehityksen kärjessä yhdellä komennolla.

Tästä syystä uudet julkaisut eivät ole erityisen tärkeitä Arch-maailmassa, sillä rolling release -järjestelmä tekee uusista julkaisuista vanhentuneita heti pakettien päivittyessä uusiin versioihin. Jos etsit tapaa päivittää uusimpaan Arch Linux -julkaisuun, sinun ei tarvitse asentaa mitään uudestaan. Sinun tarvitsee vain ajaa *pacman -Syu* -komento, ja järjestelmäsi on pian identtinen ihkauuden asennuksen kanssa.

Samasta syystä uudet Arch Linux -julkaisut eivät yleensä ole täynnä uusia ja jännittäviä ominaisuuksia. Kaikki uusi ja jännittävä julkaistaan tarvittaessa samalla kun pakettivaraston paketteja päivitetään, ja voidaan asentaa järjestelmään komennolla *pacman -Syu*.

## Q) Arch tarvitsee enemmän/vähemmän julkisuutta (esim. mainontaa)

**A)** Arch saa nykyiselläänkin varsin paljon julkisuutta. Arch Linuxin päämäärä ei ole kasvaa suureksi, vaan tarjota elegantti, minimalistinen ja kehityksen kärjessä oleva ohjelmistokokonaisuus joka keskittyy yksinkertaisuuteen ja koodin oikeellisuuteen. Kasvua tapahtuu luonnostaan kohdekäyttäjien keskuudessa. Kasvun pakottaminen tulisi aiheuttamaan ongelmia.

Samaan tapaan kehitysmalli ei rajoita luonnollista kasvua. Enemmän käyttäjiä merkitsee enemmän kehittäjiä työskentelemään Arch Linuxin parissa. Tämä saattaa aiheuttaa joitain hallinnollisia ongelmia projektin huipulla, mutta niistä huolehditaan sitä mukaa kun niitä ilmestyy.

## Q) Arch tarvitsee enemmän dokumentaatiota

**A)** Tämä on totta, joten voit halutessasi auttaa muita Arch Linuxin käyttäjiä. Esimerkiksi jos et löydä wikistä haluamaasi tietoa, voit auttaa kirjoittamalla aiheesta uuden artikkelin. Voit myös kysyä muiden käyttäjien tietoja ja mielipiteitä asiasta ja lisätä niitä artikkeliin tarpeen mukaan. Tällä tavalla voit auttaa muita käyttäjiä. Tiedolle on aina tarvetta.

## Q) Arch tarvitsee enemmän kehittäjiä

**A)** Tämä on mahdollista. Voit liittyä vapaaehtoiseksi jäseneksi Archlinux-yhteisön hyväksi. Vilkaise foorumia, IRC-kanavaa tai sähköpostilistoja saadaksesi selville asioita joiden tiimoilta apu kelpaisi. Ja ainahan voit olla avuksi myös Wikin kautta kirjoittamalla tai kääntämällä lisää artikkeleita.

## Q) Miksi Arch on niin hidas? Luulin että sen pitäisi olla nopea!

**A)** Pidä huoli että hostname (isäntäkoneen nimi) on asetettu oikein /etc/host-tiedostoon, ja se on yhtenevä /etc/rc.conf-tiedostossa. Ohjelmat saattavat toimia hyvinkin hitaasti mikäli nimet eivät täsmää.

## Q) Miksi internet on hitaampi verrattuna muihin käyttöjärjestelmiin?

**A)** Ennen lisäkysymyksiä on syytä tarkastaa verkkoasetukset. Tuplatarkasta tiedostot /etc/rc.conf, /etc/host sekä /etc/resolv.conf. Lisätietoja tässä vaiheessa valitettavasti suomenkielisestä Wikistä ei löydy.

# Paketinhallinta

## Q) Löysin virheen paketista X. Mitä minun pitäisi tehdä?

**A)** Ensinnäkin sinun tulee varmistaa että virhe on Arch-lähtöinen eikä sovelluskohtainen. Mikäli olet varma että bugi on Archissa, voit toimia esimerkiksi seuraavasti:

1.  Selaa foorumilta onko joku toinenkin huomannut saman virheen.
2.  Ilmoita asiasta paketin ylläpitäjälle. Tämän saat selville esimerkiksi "pacman -Qi <paketin nimi>"-komennolla.
3.  Lähetä yksityiskohtainen selonteko bugista osoitteessa [https://bugs.archlinux.org](https://bugs.archlinux.org).
4.  Voit myös kirjoittaa foorumille viestin bugista ja sen yksityiskohdista, sekä sen että olet jo tehnyt bugiraportin. Tämä edesauttaa muita mahdollisesti ongelmaan törmääviä.

## Q) Arch paketit tarvitsevat yhtenäisen nimeämiskäytännön. .pkg.tar.gz on liian pitkä ja monimutkainen

**A)** Tästä on ollut jo puhetta sähköpostilistan puolella, ja jotkut ehdottivat .pac-päätettä. Tällä hetkellä ei ole kuitenkaan suunnitelmissa muuttaa pakettien tiedostopäätettä. Kysymys on kuitenkin vain vanhasta kunnon gzipatusta tar-pallosta jota monet ohjelmat ymmärtävä mikäli tiedostoja haluaa tutkia tai muokata. Miksi vaihtaa pääte?

## Q) Pacman tarvitsee kirjaston jotta muut ohjelmat pääsevät helposti käsiksi pakettien tietoihin

**A)** Version 3.0.0 jälkeen pacman on ollut käyttöliittymä libalpm (Arch Linux Package Management)-kirjastolle. Kirjasto sallii sille ohjelmoitavan esimerkiksi graafisen käyttöliittymän ilman pacmanin osallisuutta.

## Q) Miksei Pacmanilla ole virallista graafista käyttöliittymää?

**A)** Luitko jo Wikitekstin aiheesta [The Arch Way](/index.php/Arch_Linux_(Suomi) "Arch Linux (Suomi)")? Varsinainen kehitystiimi ei aio sellaista toteuttaa, mutta voit vapaasti käyttää muiden Arch-käyttäjien tekemiä graafisia käyttölittymiä. Englanninkieliseltä Wikisivulta [Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends") löytyy listattuna näitä.

## Q) Pacman tarvitsee Ominaisuuden X!

**A)** Archin kantavaan filosofiaan kuuluu ajatus yksinkertaisuuden arvostamisesta, näinollen ns. tarpeettomia ominaisuuksia pyritään välttämään Archin ydinohjelmistoissa. Mikäli koet että ideasi on niin hyvä ja kätevä että sillä olisi mahdollisuus edistää filosofian mukaista kehitystä, voit ilman muuta keskustella aiheesta Arch Linuxin foorumissa.

Kaikenkaikkiaan yksinkertaisin keino saada haluttu ominaisuus Arch Linuxiin - tai sen ydinkomponentteihin - on toteuttaa se itse. Ei tietenkään voida luvata että kehittämäsi ominaisuus hyväksyttäisiin virallisesti. Puhumattakaan että se hyväksyttäisiin osaksi jakelua. Voit olla kuitenkin varma että lukuisat muut Archin käyttäjät tulevat arvostamaan tekemääsi työtä tuli siitä virallinen ominaisuus tai ei.

# Asennus

## Q) Arch tarvitsee paremman asennusohjelman, ehkä jopa graafisen sellaisen.

**A)** Tällainen asia on aina kiinni henkilökohtaisesta näkemyksestä. Tässä tapauksessa on parempi yrittää oivaltaa Arch Linuxin yksinkertainen ja kevyt lähestymisfilosofia ja tulla toimeen nykyisenkaltaisen asennusohjelman kanssa. Ja koska kysymyksessä on rolling release-jakelu ei asennusohjelmaan törmätä vasta kun käyttäjä vapaaehtoisesti haluaa asentaa Archin uudelleen ns. puhtaalta pöydältä.