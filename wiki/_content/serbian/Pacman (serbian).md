Related articles

*   [Unazadjivanje paketa](/index.php?title=Unazadjivanje_paketa&action=edit&redlink=1 "Unazadjivanje paketa (page does not exist)")
*   [Unapredjivanje pacman performansi](/index.php?title=Unapredjivanje_pacman_performansi&action=edit&redlink=1 "Unapredjivanje pacman performansi (page does not exist)")
*   [pacman frontendovi sa GUI-jem](/index.php?title=Pacman_frontendovi_sa_GUI-jem&action=edit&redlink=1 "Pacman frontendovi sa GUI-jem (page does not exist)")
*   [pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta")
*   [pacman saveti](/index.php?title=Pacman_saveti&action=edit&redlink=1 "Pacman saveti (page does not exist)")

**[pacman](https://archlinux.org/pacman/)** paket menadzer je jedan od glavnih funkcija Arch Linux-a. On kombinuje jednostavni formati binarnih paketa sa jednostavnim sistemom za izgradnju paketa (pogledajte [makepkg (Српски)](/index.php/Makepkg_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Makepkg (Српски)") i [Arch Build System (Српски)](/index.php?title=Arch_Build_System_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Arch Build System (Српски) (page does not exist)"). Cilj pacman-a je da ucini mogucim jednostavno upravljanje paketima, bez obzira da li su oni iz oficijalnih Arch repozitorijuma ili ih je korisnik sam napravio.

pacman zadrzava sistem aktuelnim tako sto sinhronizuje paket liste sa master serverom. Ovaj server/klijent model takodje pruza mogucnost da preuzmete/instalirate pakete sa jednostavnom komandom, zajedno sa svim neophodnim zavisnostima.

pacman je napisan u C programskom jeziku i koristi `.pkg.tar.xz` paket format.

## Contents

*   [1 Podesavanje](#Podesavanje)
    *   [1.1 Opste opcije](#Opste_opcije)
        *   [1.1.1 Preskakanje odredjenog paketa prilikom osvezavanja sistema(apgrejdovanja)](#Preskakanje_odredjenog_paketa_prilikom_osvezavanja_sistema(apgrejdovanja))
        *   [1.1.2 Preskakanje grupe paketa prilikom osvezavanja sistema(apgrejdovanja)](#Preskakanje_grupe_paketa_prilikom_osvezavanja_sistema(apgrejdovanja))
    *   [1.2 Repozitorijumi](#Repozitorijumi)
*   [2 Upotreba](#Upotreba)
    *   [2.1 Instaliranje paketa](#Instaliranje_paketa)
    *   [2.2 Uklanjanje paketa](#Uklanjanje_paketa)
    *   [2.3 Osvezavanje paketa](#Osvezavanje_paketa)
    *   [2.4 Izdavanje upita bazama paketa](#Izdavanje_upita_bazama_paketa)
    *   [2.5 Dodatne komande](#Dodatne_komande)
*   [3 Resavanje problema](#Resavanje_problema)
    *   [3.1 Zakrpa za paket XYZ je razbila moj sistem!](#Zakrpa_za_paket_XYZ_je_razbila_moj_sistem!)
    *   [3.2 Znam da je izbacena zakrpa za paket ABC, ali pacman kaze da je moj sistem tekuci(nema novih zakrpa)!](#Znam_da_je_izbacena_zakrpa_za_paket_ABC,_ali_pacman_kaze_da_je_moj_sistem_tekuci(nema_novih_zakrpa)!)
    *   [3.3 Dobijam gresku prilikom osvezavanja: "fajl postoji u fajlsistemu"!](#Dobijam_gresku_prilikom_osvezavanja:_"fajl_postoji_u_fajlsistemu"!)
    *   [3.4 Dobijam gresku kada instaliram paket: "not found in sync db"](#Dobijam_gresku_kada_instaliram_paket:_"not_found_in_sync_db")
    *   [3.5 pacman stalno osvezava isti paket!](#pacman_stalno_osvezava_isti_paket!)
    *   [3.6 pacman puca tokom osvezavanja sistema!](#pacman_puca_tokom_osvezavanja_sistema!)
    *   [3.7 Instalirao sam softver sa make install; ovi fajlovi ne pripadaju ni jednom paketu!](#Instalirao_sam_softver_sa_make_install;_ovi_fajlovi_ne_pripadaju_ni_jednom_paketu!)
    *   [3.8 pacman je potpuno slomljen! Kako da ga instaliram?](#pacman_je_potpuno_slomljen!_Kako_da_ga_instaliram?)
*   [4 Izvori](#Izvori)

## Podesavanje

pacman podesavanja se nalaze u `/etc/pacman.conf`. To je mesto gde korisnik moze da podesi program na nacin kako njemu odgovara. Detaljne informacije o ovom fajlu i podesavanjima se mogu naci u [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html).

### Opste opcije

Opste opcije su u `[options]` delu. Procitajte man stranicu ili pogledajte u difoltu `pacman.conf` za informacije o tome sta sve mozete da podesite u njemu.

#### Preskakanje odredjenog paketa prilikom osvezavanja sistema(apgrejdovanja)

Da preskocite osvezavanje odredjenog paketa, zadajte to na sledeci nacin:

```
IgnorePkg=kernel26

```

Za vise paketa upotrebite prazan prostor.

#### Preskakanje grupe paketa prilikom osvezavanja sistema(apgrejdovanja)

Kao sa paketima, preskakanje cele grupe paketa je isto moguce:

```
IgnoreGroup=gnome

```

### Repozitorijumi

Ovaj deo opisuje repozitorijume koje mozete da koristite, kao sto je naznaceno u `pacman.conf`. Mogu se zadati u tom fajlu direktno ili se uvesti (includovati ili sadrzati) iz drugog fajla.

Svi oficijalni repozitorijumi koriste isti `/etc/pacman.d/mirrorlist` fajl koji sadrzi varijablu, '`$repo`', sto je neophodno da se odrzi samo jedna lista.

Sledece je primer za [oficijalne repozitorijume](/index.php?title=Official_repositories_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Official repositories (Српски) (page does not exist)") koji odlazu [mirore](/index.php?title=Mirrors_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Mirrors (Српски) (page does not exist)") u miror listu.

```
[core]
# Add your preferred servers here, they will be used first
Include=/etc/pacman.d/mirrorlist

[extra]
# Add your preferred servers here, they will be used first
Include=/etc/pacman.d/mirrorlist

[community]
# Add your preferred servers here, they will be used first
Include=/etc/pacman.d/mirrorlist

```

**Note:** Treba biti na oprezu kada koristite `[testing]` repozitorijum. On je u aktivnom razvoju i osvezavanje sistema preko njega moze prouzrokovati prestanak rada nekih paketa. Ljudima koji koriste `[testing]` repozitorijum se preporucuje da se prijave na [arch-dev-public mejling lista](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public) za tekuce informacije.

## Upotreba

Da procitate druge primere u vezi mogucnosti pacman-a, pogledajte [man pacman](https://archlinux.org/pacman/pacman.8.html). Primeri ispod su samo mali uzorak operacija koje se mogu izvrsiti.

### Instaliranje paketa

Da instalirate jedan paket ili listu paketa (ukljucujuci zavisnosti), izvrsite sledecu komandu:

```
# pacman -S ime_paketa1 ime_paketa2

```

Ponekad postoji vise verzija paketa u razlicitim repozitorijumima (npr. extra i testing). Zadajte koji zelite da instalirate:

```
# pacman -S extra/package_name
# pacman -S testing/package_name

```

**Note:** **Nemojte** da osvezavate listu paketa kada instalirate paket (npr. `pacman -Sy ime_paketa`); ovo moze uzrokovati probleme sa zavisnostima. [[1]](https://bbs.archlinux.org/viewtopic.php?id=89328) [Osvezavanje](#Upgrading_packages) prvo eksplicitno; pre instaliranja novih paketa.

### Uklanjanje paketa

Da uklonite jedan paket, ostavljajuci sve njegove zavisnosti instalirane:

```
# pacman -R ime_paketa

```

Da uklonite paket i sve njegove zavisnosti koje nisu neophodne od strane drugih instaliranih paketa:

```
# pacman -Rs ime_paketa

```

pacman cuva vazne konfiguracione fajlove kada uklanja odredjene aplikacije i imenuje ih sa ekstenzijom: `.pacsave`. Da obrisete ove bekapovane fajlove upotrebite -n opciju:

```
# pacman -Rn ime_paketa
# pacman -Rns ime_paketa

```

**Note:** pacman nece ukloniti podesavanja koje sama aplikacija kreira (naprimer `.dot` fajlove u home direktorijumu).

### Osvezavanje paketa

pacman moze da osvezi sve pakete na sistemu sa samo jednom komandom. To moze da potraje u zavisnosti od toga u koliko meri je Vas sistem neosvezen, tj. kada ste ga zadnji put osvezili. Ova komanda moze da sinhronizuje baze repozitorijuma *i* osvezi pakete sistema:

```
# pacman -Syu

```

**Note:** Kao *rolling-release* distribucija, osvezavanje Vaseg Arch Linux sistema nije uvek jednostavno kao sa drugim distribucijama koje imaju fiksna izdanja. Pored toga, pacman nije "upali-i-zaboravi" paket menadzer. Kao rezultat toga, ispravno odrzavanje Arch Linux sistema sa pacman-om tezi da zbuni nove korsnike (kao sto i povremene diskusije na forumu ukazuju). Molim Vas procitajte sledecu sekciju *temeljno* pre nego sto nastavite.

pacman je mocni paket menadzer, ali ne pokusava da "ucini sve". Procitajte [The Arch Way (Српски)](/index.php/The_Arch_Way_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "The Arch Way (Српски)") ako Vas ovo zbunjuje. Pre svega, korisnici moraju biti na oprezu i preuzeti odgovornost za odrzavanje njihovih sistema. Kada obavljate osvezavanje sistema (`pacman -Syu`), naprimer, **od kljucnog znacaja je da korisnik procita sav izlaz od pacman-a i koristi se zdravim razumom.**

Umesto da odmah osvezi sistem cim su novi paketi dostupni, korisnik mora da shvati da jedno osvezenje za *kriticni* paket moze imati nepredvidjene posledice. Ovo znaci da nije pametno osveziti `xorg-server` ako on trenutno isporucuje vaznu prezentaciju, naprimer. Umesto toga, osvezite tokom slobodnog vremena i pripremite se za razresavanje eventualnih problema koji se mogu pojaviti prilikom samog procesa.

Sledece, posecivanje [Arch Linux home stranicu](https://archlinux.org/) se uvek preporucuje. Cesto kada osvezenja zahtevaju intervenciju korisnika, odgovarajuci post na [https://archlinux.org](https://archlinux.org) ce se pojaviti. Obicno postoje i postovi na forumu koji opisuju isti problem i to ukratko nakon sto zakrpa postane dostupna preko mirora, detaljisuci resenje za taj problem.

Kada osvezite, obavezno procitajte poruke u izlazu pacman-a. Ljudi koji prave pakete obicno opisu promene i ocekivane probleme, i upucuju korisnike na odgovarajucu wiki stranicu ili izvor. Konacno, **uvek procitajte sve informacije u izlazu pacman-a!**

**Tip:** Zapamtite da se pacman-ov izlaz loguje u `/var/log/pacman.log`.

### Izdavanje upita bazama paketa

pacman izdaje upite lokalnoj bazi paketa sa -Q zastavom; pogledajte:

```
$ pacman -Q --help

```

a upite za sinhronizaciju baza podataka sa -S zastavom; pogledajte:

```
$ pacman -S --help

```

pacman moze da izvrsi pretragu za paketima u bazama, pretrazujuci i imena paketa i opise paketa:

```
$ pacman -Ss paket

```

Da pretrazite za vec instaliranim paketima:

```
$ pacman -Qs package

```

Da prikazete detaljne informacije za dati paket:

```
$ pacman -Si paket

```

za lokalno instalirane pakete:

```
$ pacman -Qi package

```

Da biste preuzeli spisak datoteka instaliranih od strane paketa:

```
$ pacman -Ql package

```

Takodje mozete da pitate bazu kom paketu pripada odredjeni fajl u fajl sistemu:

```
$ pacman -Qo /staza/do/fajla

```

Da izlistate sve pakete koji nisu vise neophodni kao zavisnosti (sirocici):

```
$ pacman -Qdt

```

### Dodatne komande

Preuzmite paket bez njegovog instaliranja:

```
# pacman -Sw paket

```

Instalirajte 'lokalni' paket koji nije iz repozitorijuma:

```
# pacman -U /staza/do/paketa/ime_paketa-verzija.pkg.tar.xz

```

Instalirajte 'udaljeni' paket (ne iz repozitorijuma):

```
# pacman -U http://www.primer.com/repo/primer.pkg.tar.xz

```

Ocistite kes paketa koji nisu trenutno instalirani (`/var/cache/pacman/pkg`):

```
# pacman -Sc

```

Ocistite ceo paket kes:

**Warning:** Uradite ovo samo kad ste sigurni da [unazadjivanje paketa](/index.php?title=Downgrading_Packages_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Downgrading Packages (Српски) (page does not exist)") nece biti neophodno, jer pacman -Scc uklanja "sve" pakete iz kesa.

```
# pacman -Scc

```

## Resavanje problema

### Zakrpa za paket XYZ je razbila moj sistem!

Arch Linux je **rolling-release** distribucija koja je stalno aktuelna. Zakrpe za pakete su dostupne cim se proglase za dovoljno stabilnim za generalnu upotrebu. Kako god, zakrpe ponekad mogu da zahtevaju intervenciju korisnika: konfiguracioni fajlovi mozda moraju da se osveze, opcione zavisnosti se mogu promeniti, itd.

Najvazniji savet koji treba da zapamtite je da ne osvezavate vas sistem "slepo". Uvek procitajte listu paketa koji osvezavate. Proverite da li ce "kriticni" paketi biti osvezeni (`kernel26`, `xorg-server`, i tako dalje). Ako je to slucaj, obicno je dobra ideja da proverite vesti na [https://archlinux.org](https://archlinux.org) i skenirate najskorije postove na forumu da vidite da li ostali korisnici imaju eventualne probleme kao rezultat osvezenja sistema.

Ako ocekujete/znate da ce zakrpa paketa uzrokovati probleme, ljudi koji obezbedjuju pakete ce obezbediti da pacman prikaze odgovarajucu poruku kada se paket osvezi. Ako imate probleme nakon osvezenja, proverite dva puta tekstualni izlaz pacman-a tako sto cete proveriti log u (`/var/log/pacman.log`).

U ovom momentu, **samo nakon sto ste se uverili da nema informacija dostupnih preko pacman-a, ne postoje vesti u vezi problema na [https://archlinux.org](https://archlinux.org), i nema postova na forumu u vezi te zakrpe**, mozete uzeti u obzir da zatrazite pomoc na forumu, preko [IRC-a](/index.php/IRC_channel "IRC channel"), ili [unazadjivanje problematicnih paketa](/index.php?title=Downgrading_Packages_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Downgrading Packages (Српски) (page does not exist)").

Ponovo procitajte zadnji paragraf.

### Znam da je izbacena zakrpa za paket ABC, ali pacman kaze da je moj sistem tekuci(nema novih zakrpa)!

pacman mirori nisu sinhronizovani odmah. Ponekad je neophodno preko 24 casa pre nego sto zakrpa postane dostupna na vasem miroru.

Jedina opcija je da budete strpljivi ili da koristite drugi miror. [Stanje mirora](https://www.archlinux.de/?page=MirrorStatus) moze da vam pomogne da odredite miror koji je aktuelan.

### Dobijam gresku prilikom osvezavanja: "fajl postoji u fajlsistemu"!

ASIDE: *Preuzeto sa [https://bbs.archlinux.org/viewtopic.php?id=56373](https://bbs.archlinux.org/viewtopic.php?id=56373) by Misfit138.*

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
package: /path/to/file exists in filesystem
Errors occurred, no packages were upgraded.

```

Zasto se ovo desava: pacman je detektovao konflikt fajlova, i po dizajnu, nece prepisati fajlove za vas. Ovo je odlika dizajna, a ne mana.

Odgovornost je korisnika da odrzava svoj sistem, ne paket menadzera. (`pacman -Qo` se moze izvrsiti da proverite koji paket poseduje odredjeni fajl, ako postoji.)

Problem je obicno trivijalne prirode. Bezbedan nacin je da prvo proverite da li drugi paket poseduje fajl (`pacman -Qo /staza/do/fajla`). Ako drugi paket poseduje fajl, [fajl bag izvestaj](/index.php/Reporting_bug_guidelines "Reporting bug guidelines"). Ako fajl nije u posedstvu drugog paketa, preimenujte fajl koji 'vec postoji u fajlsistemu' i ponovo izvrsite update komandu. Ako sve prodje kako treba, mozete ukloniti fajl.

### Dobijam gresku kada instaliram paket: "not found in sync db"

Prvo, proverite da li paket uopste postoji (i obratite paznju na greske u kucanju!). Ako ste sigurni da paket postoji, vasa lista paketa je mozda neaktuelna ili vasi repozitorijumi mogu biti nepravilno podeseni. Pokusajte sa `pacman -Syy` da forsirate osvezenje svih lista paketa.

### pacman stalno osvezava isti paket!

Ovo se desava zbog duplog unosa u `/var/lib/pacman/local/`, kao dve `kernel26` instance. `pacman -Qi` daje izlaz sa ispravnom verzijom, ali `pacman -Qu` prepoznaje staru verziju i zbog toga ce pokusati da ga osvezi.

Solution: obrisite unos koji ometa proces `/var/lib/pacman/local/`.

**Note:** pacman verzija 3.4 bi trebalo da prikaze gresku u slucaju duplih unosa, sto bi trebalo da ucini ovu napomenu suvisnom.

### pacman puca tokom osvezavanja sistema!

U slucaju da pacman puca sa "database error" greskom dok uklanjate pakete, i reinstaliranje ili osvezavanje paketa se ne obavlja uspesno:

1.  Startujte sa Arch live CD-om
2.  Nasadite vas root fajlsistem
3.  Osvezite pacman bazu sa `pacman -Syy`
4.  Reinstalirajte pokvareni paket sa `pacman -r /path/to/root -S package`

### Instalirao sam softver sa `make install`; ovi fajlovi ne pripadaju ni jednom paketu!

Ako dobijate "conflicting files" gresku, imajte na umu da ce pacman prepisati rucno instalirani softver ako zadate komandu sa `--force` prekidacem (`pacman -S --force`).

Pogledajte [preuzimanje liste fajlova koje nisu u posedu ni jednog paketa](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips") za skriptu koja vrsi pretragu fajlsistema za fajlove koji *nisu u posedu*.

### pacman je potpuno slomljen! Kako da ga instaliram?

U slucaju da je pacman slomljen bez mogucnosti da se popravi, rucno preuzmite i napravite neophodne pakete (openssl, libarchive, libfetch i pacman) i otpakujte ih u root. Pacman binarni kod ce biti obnovljen zajedno sa svojim difolt konfiguracionim fajlom. Nakon toga, reinstalirajte ove pakete sa pacman-om da odrzite integritet baze paketa. Dodatne informacije i primer (zastarele) skripte koja automatizuje proces je dostupna u [ovom](https://bbs.archlinux.org/viewtopic.php?id=95007) forum postu.

## Izvori

*   [libalpm(3) Manual Page](https://www.archlinux.org/pacman/libalpm.3.html)
*   [pacman(8) Manual Page](https://www.archlinux.org/pacman/pacman.8.html)
*   [pacman.conf(5) Manual Page](https://www.archlinux.org/pacman/pacman.conf.5.html)
*   [repo-add(8) Manual Page](https://www.archlinux.org/pacman/repo-add.8.html)