Related articles

*   [Arch terminology](/index.php/Arch_terminology "Arch terminology")
*   [Arch User Repository#FAQ](/index.php/Arch_User_Repository#FAQ "Arch User Repository")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 General](#General)
    *   [1.1 Šta je Arch Linux?](#Šta_je_Arch_Linux?)
    *   [1.2 Zašto ne bih htio koristiti Arch Linux](#Zašto_ne_bih_htio_koristiti_Arch_Linux)
    *   [1.3 Koje arhitekture Arch podržava](#Koje_arhitekture_Arch_podržava)
    *   [1.4 Da li Arch Linux prati Linux Foundation's Filesystem Hierarchy Standard (FHS)?](#Da_li_Arch_Linux_prati_Linux_Foundation's_Filesystem_Hierarchy_Standard_(FHS)?)
    *   [1.5 Ja sam GNU/Linux početnik. Da li bih trebao koristiti Arch](#Ja_sam_GNU/Linux_početnik._Da_li_bih_trebao_koristiti_Arch)
    *   [1.6 Da li je Arch namijenjen za bude korišten kao server? Desktop? Workstation?](#Da_li_je_Arch_namijenjen_za_bude_korišten_kao_server?_Desktop?_Workstation?)
    *   [1.7 Zaista volim Arch, osim što development tim mora implementirati feature X](#Zaista_volim_Arch,_osim_što_development_tim_mora_implementirati_feature_X)
    *   [1.8 Kada će novi release biti dostupan?](#Kada_će_novi_release_biti_dostupan?)
    *   [1.9 Da li je Arch Linux stabilna distribucija. Da li ću često imati crash-ove?](#Da_li_je_Arch_Linux_stabilna_distribucija._Da_li_ću_često_imati_crash-ove?)
    *   [1.10 Arch treba više reklamiranja](#Arch_treba_više_reklamiranja)
    *   [1.11 Arch treba više developera](#Arch_treba_više_developera)
    *   [1.12 Zašto je moj internet spor u poređenju sa drugim operativnim sistemima](#Zašto_je_moj_internet_spor_u_poređenju_sa_drugim_operativnim_sistemima)
    *   [1.13 Zašto Arch koristi sav moj RAM?](#Zašto_Arch_koristi_sav_moj_RAM?)
    *   [1.14 Gdje je otišao sav moj slobodni prostor?](#Gdje_je_otišao_sav_moj_slobodni_prostor?)
*   [2 Paket menadžment](#Paket_menadžment)
    *   [2.1 Našao sam error sa paketom X. Šta bih trebao da radim?](#Našao_sam_error_sa_paketom_X._Šta_bih_trebao_da_radim?)
    *   [2.2 Arch paketi moraju koristi unikatne konvencije imenovanja. ".pkg.tar.gz" i ".pkg.tar.xz" su preduge i zbunjujuće](#Arch_paketi_moraju_koristi_unikatne_konvencije_imenovanja._".pkg.tar.gz"_i_".pkg.tar.xz"_su_preduge_i_zbunjujuće)
    *   [2.3 Pacman treba library tako da druge aplikacije moze lagano da pristupe informacijama o paketima](#Pacman_treba_library_tako_da_druge_aplikacije_moze_lagano_da_pristupe_informacijama_o_paketima)
    *   [2.4 Pacman treba feature X!](#Pacman_treba_feature_X!)
    *   [2.5 Upravo sam instalirao Paket X. Kako da ga pokrenem?](#Upravo_sam_instalirao_Paket_X._Kako_da_ga_pokrenem?)
    *   [2.6 Zašto je samo jedna jedna verzija shared library-a dostupna u oficijelnim repository-ima?](#Zašto_je_samo_jedna_jedna_verzija_shared_library-a_dostupna_u_oficijelnim_repository-ima?)
    *   [2.7 Šta ako uradim full upgrade sistema i unutar njega bude update za shared library, ali ne i za aplikacije koje ovise o njemu?](#Šta_ako_uradim_full_upgrade_sistema_i_unutar_njega_bude_update_za_shared_library,_ali_ne_i_za_aplikacije_koje_ovise_o_njemu?)
    *   [2.8 Da li je moguće da postoji veliki kernel update u repository-u i da neki od driver paketa nisu update-ovani?](#Da_li_je_moguće_da_postoji_veliki_kernel_update_u_repository-u_i_da_neki_od_driver_paketa_nisu_update-ovani?)
    *   [2.9 Šta raditi poslije upgrade-a?](#Šta_raditi_poslije_upgrade-a?)
    *   [2.10 Paket update je release-ovan, ali pacman kaže da je sistem up to date](#Paket_update_je_release-ovan,_ali_pacman_kaže_da_je_sistem_up_to_date)
    *   [2.11 Upstream projekt *X* je pustio novu verziju. Koliko će trajati dok Arch paket update-uju na novu verziju?](#Upstream_projekt_X_je_pustio_novu_verziju._Koliko_će_trajati_dok_Arch_paket_update-uju_na_novu_verziju?)
    *   [2.12 Ako trebam stariju verziju shared library, da li mogu samo napraviti simbolički link?](#Ako_trebam_stariju_verziju_shared_library,_da_li_mogu_samo_napraviti_simbolički_link?)
    *   [2.13 Zašto su neesencijalni paketi(npr. netctl) unutar base grupe?](#Zašto_su_neesencijalni_paketi(npr._netctl)_unutar_base_grupe?)
*   [3 Instalacija](#Instalacija)
    *   [3.1 Arch treba installer. Možda GUI installer](#Arch_treba_installer._Možda_GUI_installer)
    *   [3.2 Instalirao sam Arch i ispred mene je shell! Šta sada?](#Instalirao_sam_Arch_i_ispred_mene_je_shell!_Šta_sada?)
    *   [3.3 Koje desktop okruženje ili window menadžer bih trebao koristiti?](#Koje_desktop_okruženje_ili_window_menadžer_bih_trebao_koristiti?)
    *   [3.4 Šta čini Arch unikatnim u odnosu na ostale "minimalne" distribucije?](#Šta_čini_Arch_unikatnim_u_odnosu_na_ostale_"minimalne"_distribucije?)
*   [4 64-bit](#64-bit)
    *   [4.1 Kako da saznam da li mi je procesor x86_64 kompatibilan?](#Kako_da_saznam_da_li_mi_je_procesor_x86_64_kompatibilan?)
    *   [4.2 Zašto 64-bit?](#Zašto_64-bit?)

## General

### Šta je Arch Linux?

Vidi [Arch Linux](/index.php/Arch_Linux_(Bosanski) "Arch Linux (Bosanski)") članak.

### Zašto ne bih htio koristiti Arch Linux

Možes **ne**koristiti Arch, ako:

*   nemaš sposobnost/vremena/želje za 'do-it-yourself' GNU/Linux distribuciju.
*   trebaš podršku za arhitekturu mimo x86_64.
*   imaš jak stav za korištenje arhitekturu koja samo omogućava besplatan software kao što je definisano od strane GNU.
*   vjeruješ da bi operativni sistem trebao sam sebe konfigurisati, raditi out of the box i uključiati defaultni set software-a i desktop okruženja na instalacijskom mediju.
*   ne želiš rolling release GNU/Linux distribuciju
*   sretan si sa trenutnim OS

### Koje arhitekture Arch podržava

Arch samo podržava x86_64(često nazivana amd64) arhitekturu. Podrška za i686 arhitekturu je prestala u novembru 2017\. godine [[1]](https://www.archlinux.org/news/the-end-of-i686-support/).

Postoje *neoficijalni* portovi za i686 arhitekturu [[2]](https://archlinux32.org/) i [ARM](https://en.wikipedia.org/wiki/ARM_architecture "wikipedia:ARM architecture") CPU-ove [http:/archlinuxarm.org/], svaki sa svojim community channel-om. [[3]](https://ix.io/73w/irc)

### Da li Arch Linux prati Linux Foundation's Filesystem Hierarchy Standard (FHS)?

Arch Linux prati *file system hierarchy* za operativni sistem koristeći [systemd](/index.php/Systemd "Systemd") servis menadžer. Vidi [file-hierarchy(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7) za objašnjenje svakog foldera sa njihovim oznakama. `/bin`, `/sbin` i `/usr/sbin/` su simbolički linkovi na `/usr/bin`; `/lib` i `/lib64` su simbolički linkovi na `/usr/lib`.

### Ja sam GNU/Linux početnik. Da li bih trebao koristiti Arch

Ako si početnik i želiš koristiti Arch, moraš biti voljan uložiti vrijeme za učenje novog sistema i prihvatiti da je Arch Linux 'do-it-yourself' distribucija; korisnik sklapa sistem.

Prije postavljanja pitanja, odradi research korištenjem Google-a, pretraživaj forum i dokumentaciju dostupnu na ArchWiki. *Postoji razlog zašto su ovi resursi dostupni javnosti.* Više hiljada *volontera* su uložili sate u kompajliranje ovih sjajnih informacija.

Vidi također [Arch terminology#RTFM](/index.php/Arch_terminology#RTFM "Arch terminology") i [Installation guide (Bosanski)](/index.php/Installation_guide_(Bosanski) "Installation guide (Bosanski)").

### Da li je Arch namijenjen za bude korišten kao server? Desktop? Workstation?

Arch nije dizajniran specifično za jednu upotrebu. Dizajniran je za specifičnu grupu *korisnika*. Arch cilja kompetentne korisnike koji uživaju u 'do-it-yourself' i koji dalje iskorištavaju sistem da odgovara njihovim potrebama. Dakle, u rukama ciljne skupine, Arch Linux može biti korišten za bilo koju upotrebu. Veliki broj koristi Arch kao desktop i workstation. Također, archlinux.org radi na Arch-u.

### Zaista volim Arch, osim što development tim mora implementirati feature X

Uključi se, kontributaj svoj kod/soluciju community-u. Ukoliko je procijenjeno kao dobro od strane community-a i development tima, možda će biti merge-ano. Arch community teži kontribuciji, te dijeljenju koda i alata.

### Kada će novi release biti dostupan?

Arch Linux release-ovi su jednostavno live okruženja za instalaciju ili rescue, koji sadrž [base](https://www.archlinux.org/packages/?name=base) grupu i nekoliko [drugih paketa](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64). Release-ovi se obično dešavaju i prvoj polovini svakog mjeseca.

### Da li je Arch Linux stabilna distribucija. Da li ću često imati crash-ove?

*Korisnik* je onaj koji je odgovoran za stabilnost svoj rolling release sistema. Korisnik odlučuje kada upgrade i merge-ati potrebne promjene. Ukoliko korisnik se obrati community-u za pomoć, obično se odgovor dobije u razumnom vremenskom periodu. Razlika između Arch-a i drugih distribucija je u tome što je Arch u potpunosti 'do-it-yourself' distribucija; žalbe na crash-ove su neproduktivne jer upstream promjene nisu odgovornost Arch developera.

Vidi [System maintenance](/index.php/System_maintenance "System maintenance") članak za savjete kako učinit Arch Linux sistem stabilnim koliko je to moguće.

### Arch treba više reklamiranja

Arch u svom obliku dobija dosta reklamiranja. Cilj Arch Linuxa nije da bude velik, nego se održivi rast odvija prirodno među ciljnom korisničkom bazom.

### Arch treba više developera

Vjerovatno. Slobodno volontiraj svoje vrijeme! Posjeti [forume](https://bbs.archlinux.org), [IRC kanale](/index.php/IRC_channels "IRC channels") i [mailing liste](https://mailman.archlinux.org/mailman/listinfo/) i vidi šta je potrebno da se uradi. Biti uključen u Community Contribution podforum je dobar način da se počne.

### Zašto je moj internet spor u poređenju sa drugim operativnim sistemima

Da li je mreža dobro konfigurisana. Pogledaj [Network configuration](/index.php/Network_configuration "Network configuration") članak.

Također, uzmi u obzir da Arch Linux ne dolazi sa [traffic shaping-om](https://en.wikipedia.org/wiki/Traffic_shaping "wikipedia:Traffic shaping") uključnim, što znači da ukoliko program na neki način koristi internet konekciju do maksimuma - nevezano da li je to P2P ili klasična server-klijent konekcija - drugi lokalni program će naletiti na zabušenu konekciju, što rezultira lag-ovima i timeout-ima. Poboljšanja može pružiti [firewall](/index.php/Firewalls "Firewalls") poput *Shorewall* ili *Vuurmuur*; također, tu su statičke skripte [iproute2](https://www.archlinux.org/packages/?name=iproute2) poput [ovog derivativa](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos) *Wondershaper-a* koji omogućava shape-ovanje na mrežnom layer-u.

### Zašto Arch koristi sav moj RAM?

Esencijalno, neiskorištena RAM memorija je wasted RAM.

Veliki broj novih korisnika primjeti kako Linux kernel upravlja memorijom drugačije nego na šta su navikli. Pošto je pristup podacima puno brže iz RAM-a nego sa storage uredjaja, kernel kešira pristupane podatke u memoriji. Keširani podaci su obrisani tek kada sistem se približava maksimalnoj iskorištenosti RAM memorije i kada novi podaci trebaju biti učitani.

Možemo primjetiti razliku sa `free` komandom:

 `$ free -h` 
```
              total        used        free      shared  buff/cache   available
Mem:           2.8G        1.1G        283M        224M        1.4G        1.2G
Swap:          3.0G        881M        2.1G

```

Važno je napraviti razliku između "slobodne" i "dostupne" memorije. U primjeru iznad, laptop sa 2.8G ukupnog RAM-a djeluje da koristi sve to sa samo 238M slobodne memorije. 1.4G je "buff/cache". Tu je i dalje 1.2 dostupno za startanje novih aplikacija, bez swappinga. Vidi `man free(1)` za detalje. Rezultati svega ovoga? Performanse!

Vidi [ovaj sjajni članak](http://www.linuxjournal.com/article/2770) ukoliko si zaintrigiran. Postoji i website posvoćen raščišćavanju ove konfuzije: [http://www.linuxatemyram.com/](http://www.linuxatemyram.com/)

### Gdje je otišao sav moj slobodni prostor?

Odgovor na ovo pitanje zavisi od sistema. Postoje neki [fini alati](/index.php/List_of_applications_(Bosanski)#Prikaz_korištenja_diska "List of applications (Bosanski)") koji mogu pomoći pri pronalasku odgovora.

## Paket menadžment

Vidi [pacman](/index.php/Pacman "Pacman"), [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") i [Official repositories](/index.php/Official_repositories "Official repositories") stranice za vise odgovora.

### Našao sam error sa paketom X. Šta bih trebao da radim?

Prvo, moras skontati da li je taj error nešto što Arch tim može popraviti. Nekada nije(npr. Firefox crash može biti na strani Mozilla tima); ovo se zove *upstream error*. Ako je Arch problem, postoji niz koraka:

1.  Pretraži forum za informacije. Provjeri da li je već neko to primjetio.
2.  Objavi [bug report](/index.php/Bug_report "Bug report") sa detaljnim informacijama na [https://bugs.archlinux.org](https://bugs.archlinux.org)
3.  Ako želiš, napiši detaljni post na forumu objašnjavajući problem. Ovo će spriječiti druge ljude da reportaju isti error.

### Arch paketi moraju koristi unikatne konvencije imenovanja. ".pkg.tar.gz" i ".pkg.tar.xz" su preduge i zbunjujuće

Diskusija o ovome se vodila na Arch mailing listi. Neki su predlagali *.pac* ekstenziju, ali nema plana da se promijeni ekstenzija. Kao što je Tobias Kieslic, jedan od Arch developera, rekao: "A package **is** a gzipped *[xz]* tarball! And it can be opened, investigated and manipulated by any tar-capable application. Moreover, the mime-type is automatically detected correctly by most applications." (Paket je gunzipovani xz tarball. Može biti otvoren, istražen i manipulisan od strane aplikacija koje znaju raditi sa tar fajlovima. Dalje, mime-type je automatski detektovan od strane većine aplikacija).

### Pacman treba library tako da druge aplikacije moze lagano da pristupe informacijama o paketima

Pacman je front-ent za [libalpm](https://www.archlinux.org/pacman/libalpm.3.html)-"Arch Linux Package Management" library koji omogućava alternativne front-ende, poput GUI front-enda da bude napisan.

### Pacman treba feature X!

Ukoliko misliš da ideja ima vrijednost, možeš odlučiti da prodiskutuješ na [pacman-dev](https://lists.archlinux.org//listinfo/pacman-dev/) mailing listi. Također, provjeri [https://bugs.archlinux.org/index.php?project=3](https://bugs.archlinux.org/index.php?project=3) za već postojeće feature zahtjeve.

Najbolji način da se doda feature unutar Arch Linuxa jeste da ga sam implementiraš. Patch ili code ne moraju biti oficijalno prihvaćeni, ali će možda drugi cijeniti, testirati i doprinijeti tvome trudu.

### Upravo sam instalirao Paket X. Kako da ga pokrenem?

Ako koristiš desktop okruženje poput [KDE](/index.php/KDE "KDE") ili [GNOME](/index.php/GNOME "GNOME"), program bi se trebao automatski pojaviti na meniju. Ako pokušavas da ga pokreneš koristeći terminal i ne znaš naziv binary-a, koristi:

```
$ pacman -Qlg *package_name* | grep /usr/bin/

```

### Zašto je samo jedna jedna verzija shared library-a dostupna u oficijelnim repository-ima?

Nekoliko distribucija, poput Debiana, imaju različite verzija shared library-a zapakovane kao različiti paketi: `libfoo1`, `libfoo2`, `libfoo3` itd. Na ovaj način, moguće je kompajlirati aplikaciju za različitu verziju `libfoo`-a na sistemu.

U slučaju distribucije poput Arch-a, samo je zadnja stabilna verzija paketa oficijalno podržana. Izbacivanjem podrške za outdated software, paket maintaineri mogu provesti više vremena osiguravajući da novije verzije radi u redu. Čim postoji novi release library-a od strane upstreama, biva dodana u repository-e i paketi koji koriste taj library se rekompajliraju.

### Šta ako uradim full upgrade sistema i unutar njega bude update za shared library, ali ne i za aplikacije koje ovise o njemu?

Ovaj scenario ne bi trebao da se dogodi. Pod pretpostavkom da aplikacija koja se zove `foobaz` je jedna iz oficijalnih repository-a i builda uspješno sa novom verzijom shared library-a (`libbaz`), biće update-ovano zajedno sa `libbay`. Ukoliko ne builda uspješno, paket će imati version dependency(npr. *libbaz 1.5*), i biće uklonjeno od strane pacmana za vrijeme `libbazz` upgrade-a, zbog konflikta.

Ako `foobaz` je paket koji si sam buildao i instaliran iz AUR-a, trebao bi pokušati rebuildati `foobaz` sa novom verzijom `libbaz`. Ako build faila, prijavi bug `foobay` developerima.

### Da li je moguće da postoji veliki kernel update u repository-u i da neki od driver paketa nisu update-ovani?

Ne, nije moguće. Major kernel update-i (npr. *linux 3.5.0-1* do *linux-3.6.0-1*) su uvijek praćeni rebuildom svih podržanih kernel driver paketa. S druge strane, ako imaš nepodržan driver paket instaliran na sistemu, poput [catalyst](https://aur.archlinux.org/packages/catalyst/), onda kernel update može uticati na sistem ukoliko se ne rebuilda za novi kernel. Korisnici su dužni za update-ovanje nepodržanih driver paketa koje su instalirali.

### Šta raditi poslije upgrade-a?

Vidi [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance") sekciju.

### Paket update je release-ovan, ali pacman kaže da je sistem up to date

*pacman* mirori su sinhroniziju trenutno. Može trajati 24 sata prije nego što update postane dostupan. Jedina opcija je biti strpljiv ili koristiti drugi mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) može pomoci da se identificiraju up-to-date mirori.

### Upstream projekt *X* je pustio novu verziju. Koliko će trajati dok Arch paket update-uju na novu verziju?

Paket update-i će biti releas-ani kada su spremni. Tačan vremenski period može trajati od nekoliko sati do nekoliko sedmica u zavisnosti od toga kakav je update. Vrijeme od nove upstream verzije do toga da Arch release novi paket zavisi od specifičnih paketa i dostupnosti paket maintainera. Dodatno, neki paketi provedu više vremena u [testing](/index.php/Testing "Testing") repository-u, što dodatno može produžiti vrijeme dok se paket ne update-uje. Ako nađeš paket paket unutar oficijalnog repository-a koji je zastario, otiđi na stranicu paketa na [paket website](https://www.archlinux.org/packages/) i označi ga.

### Ako trebam stariju verziju shared library, da li mogu samo napraviti simbolički link?

Ako si sretan, može raditi, s vremana na vrijeme. To nije prava solucija, radi:

*   Library-i ne mijenjaju verzije nasumično - API/ABI će se vjerovatno promijeniti (vjerovatno sa bitovima uklonjenim) i bilo koje promjene da djeluju na upotrebu su stvar sreće.
*   Simbolični link bi bio untracked od strane paket manadžera. Novi korisnici koji odmah pokušaju hakovati na fajlove library-a su u većem riziku da naprave neželjene promjene koje ne mogu diagnozirati/popraviti, šta paket menadžer spriječava.
*   Dumpanje starijeg library file-a na fajlsistem, untracked, bi bilo zaboravljeno i ne bi imalo potencijalne obavijesti za sigurnosne bugove.

Umjesto toga, npr. koristi/napiši [kompaktni paket](https://aur.archlinux.org/packages/?SeB=n&K=compat), koji omogućava potrebnu verziju library-a.

### Zašto su neesencijalni paketi(npr. netctl) unutar base grupe?

Postoji prijedlog da se ovo poboljša. Neke diskusije sa mailing liste:

[https://lists.archlinux.org/pipermail/arch-dev-public/2019-January/029435.html](https://lists.archlinux.org/pipermail/arch-dev-public/2019-January/029435.html)

[https://lists.archlinux.org/pipermail/arch-dev-public/2019-February/029452.html](https://lists.archlinux.org/pipermail/arch-dev-public/2019-February/029452.html)

## Instalacija

### Arch treba installer. Možda GUI installer

Arh je imao installer sa text-base korisničkim interface-om koji se zvao Arch Installation Framework (AIF). Nakon što je njegov [posljednji maintainer otišao](https://lists.archlinux.org/pipermail/arch-releng/2012-July/002628.html), on je [zamijenjen sa Arch Install Scripts](/index.php/Arch_Linux_(Bosanski)#Arch_instalacijske_skripte "Arch Linux (Bosanski)").

Pošto se instalacija ne vrši često (pročitaj ostatak ovog članka da saznaš više šta znači *rolling release*), nije visokog prioriteta za developere ili korisnike. [[Installation guide (Bosanski)|Instalacijske upute je u potpunosti update-ovan da koristi command-line metode.

### Instalirao sam Arch i ispred mene je shell! Šta sada?

Vidi [General recommendations (Bosanski)](/index.php/General_recommendations_(Bosanski) "General recommendations (Bosanski)").

### Koje desktop okruženje ili window menadžer bih trebao koristiti?

Pošto su ti mnogi dostupni, odaberi jedan koji odgovara tvojim potrebama. Pogledaj [desktop okruženja](/index.php?title=Desktop_environment_(Bosanski)&action=edit&redlink=1 "Desktop environment (Bosanski) (page does not exist)") i [windows manager](/index.php?title=Window_manager_(Bosanski)&action=edit&redlink=1 "Window manager (Bosanski) (page does not exist)") članke.

### Šta čini Arch unikatnim u odnosu na ostale "minimalne" distribucije?

Vidi [Arch u poredjenju sa drugim distribucijama](/index.php/Arch_compared_to_other_distributions_(Bosanski) "Arch compared to other distributions (Bosanski)").

## 64-bit

### Kako da saznam da li mi je procesor x86_64 kompatibilan?

Ako je tvoj procesor [x86-64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") komaptibilan, imat ćes `lm` flag unutar `/proc/cpuinfo`. Npr.

```
$ grep -w lm /proc/cpuinfo

```

Ukoliko koristiš Windows, korištenjem [CPU-Z](http://www.cpuid.com/cpuz.php) može se odrediti da li je procesor 64-bit kompatibilan. CPU-ovi sa AMD instruction set-om "AMD64" ili Intelova solucija "EM64T" bi trebali biti kompatibilni sa x86_64 releas-ovima i binarnim paketima.

### Zašto 64-bit?

Brži je u većini situacija i dodatno sigurniji radi [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") u kombinaciji sa [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") i [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") koji nisu dostupni na stock i686 kernelu radi isključenog PAE. Ukoliko računar ima više od 4GB RAM-a, samo će 64-bitni procesor moći da ga u potpunosti iskoristi.

Programeri također manje brinu o 32-bit ("legacy") pošto "novi" x86 CPU-ovi tipično podržavaju 64-bitne ekstenzije.

Tu su mnogi razlozi koje bismo mogli navesti zašto izbjegavati 32-bit, ali između kernela, userspace-a i individualnih programa prosto nije moguće navesti svaku stavku šta 64-bitni procesori rade bolje.