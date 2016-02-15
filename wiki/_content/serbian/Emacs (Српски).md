Emacs je prosiriv, prilagodljiv, samo-dokumentovan editor koji radi u realnom vremenu. U srzi Emacs-a lezi [Emacs Lisp](https://en.wikipedia.org/wiki/Emacs_Lisp "wikipedia:Emacs Lisp") interpreter, jezik u kom je vecina Emacs-ove funkcionalnosti i ekstenzija implementirano. GTK je osnovni X skup alata koji koristi GNU Emacs 22, ali on i dalje funkcionise odlicno i u CLI (komandna linija) okruzenju. Emacs kapaciteti za tekst editovanje se obicno porede sa [vim](/index.php/Vim "Vim")-ovim.

## Contents

*   [1 Instalacija](#Instalacija)
*   [2 Brzi start](#Brzi_start)
    *   [2.1 Pokretanje Emacs-a](#Pokretanje_Emacs-a)
    *   [2.2 Osnovna terminologija i konvencija](#Osnovna_terminologija_i_konvencija)
    *   [2.3 Pokretanje](#Pokretanje)
    *   [2.4 Fajlovi i baferi](#Fajlovi_i_baferi)
    *   [2.5 Editovanje](#Editovanje)
    *   [2.6 Ubijanje, yank-ovanje i regioni](#Ubijanje.2C_yank-ovanje_i_regioni)
    *   [2.7 Pretrazi i zameni](#Pretrazi_i_zameni)
    *   [2.8 Uvlake i prefiks argumenti](#Uvlake_i_prefiks_argumenti)
    *   [2.9 Prozori i okviri](#Prozori_i_okviri)
    *   [2.10 Dobijanje pomoci](#Dobijanje_pomoci)
    *   [2.11 Modovi](#Modovi)
*   [3 Saveti i trikovi](#Saveti_i_trikovi)
    *   [3.1 TRAMP](#TRAMP)
    *   [3.2 Makroi sa tastature i registri](#Makroi_sa_tastature_i_registri)
    *   [3.3 Regularni izrazi](#Regularni_izrazi)
    *   [3.4 Prilagodjavanje](#Prilagodjavanje)
    *   [3.5 Ekstenzije](#Ekstenzije)
*   [4 Resavanje problema](#Resavanje_problema)
    *   [4.1 Problemi sa obojenim izlazom](#Problemi_sa_obojenim_izlazom)
    *   [4.2 Meniji se prikazuju kao prazni](#Meniji_se_prikazuju_kao_prazni)
    *   [4.3 Problemi sa prikazivanjem karaktera u X prozorima](#Problemi_sa_prikazivanjem_karaktera_u_X_prozorima)
    *   [4.4 Sporo startovanje](#Sporo_startovanje)
        *   [4.4.1 Netacno podesavanje mreze](#Netacno_podesavanje_mreze)
        *   [4.4.2 Opterecenje init fajla](#Opterecenje_init_fajla)
    *   [4.5 Cannot open load e: ...](#Cannot_open_load_e:_...)
*   [5 Izvori](#Izvori)

## Instalacija

Emacs dolazi u nekoliko varijacija (ponekad se naziva _emacsen_). Najzastupljeniji od ovih je GNU Emacs koji moze da se instalira (kao root) preko:

```
# pacman -S emacs

```

Druga uobicajena varijacija je xemacs, koji je takodje dostupan za instalaciju preko pakmena.

## Brzi start

Iako je Emacs kompleksan, nece proci puno vremena pre nego sto pocnete da shvatate koristi koje nivo prilagodljivosti i prosirivosti donosi. Stavise, sveobuhvatna raznolikost dodataka (ekstenzija) koje su vec dostupne pruzaju mogucnost transformacije u mocno okruzenje za skoro svaki oblik tekst editovanja.

Emacs ima odlican ugradjen tutorijal kom se moze pristupiti klikom na prvi link na sples ekranu (pocetni ekran prilikom paljenja Emacs-a); selektovanjem _Help->Emacs Tutorial_ iz menija ili pritiskanjem 'F1' praceno sa 't'. Ova stranica je napravljena s ciljem da bude dodatni izvor za startovanje sa Emacs-om.

Emacs takodje sadrzi skup referentnih kartica, korisnih za pocetnike i eksperte, pogledajte `/usr/share/emacs/<version>/etc/refcards/` (zamenite <version> sa vasom verzijom emacs-a).

### Pokretanje Emacs-a

Da startujete Emacs izvrsite:

```
$ emacs

```

ili, da ga koristite iz konzole:

```
$ emacs -nw

```

Mozete da dodate ime fajla da bi ste odmah otvorili taj fajl:

```
$ emacs filename.txt

```

### Osnovna terminologija i konvencija

Emacs korisnici koriste terminologiju i konvencije koje mogu delovati neobicno u pocetku i zbog toga cemo ih predstavljati kako budu nailazile redom. Ipak, postoji deo terminologije koju treba predstaviti odmah, jer je od vitalnog znacaja za rad sa Emacs-om.

Deo terminologije koju je neophodno odmah predstaviti je koncept _bafera_. Bafer predstavlja podatke u okviru Emacs-a. Na primer, kada je fajl otvoren u Emacs-u, taj fajl je iscitan sa diska i njegov sadrzaj je skladisten u baferu, koji pruza mogucnost njegovog editovanja i cuvanja nazad na disk kasnije. Baferi nisu ograniceni na tekst i mogu da sadrze i slike i dodatke. Drugi nacin da razmisljate o tome: podaci dostupni na disku se nazivaju 'fajl', dok podaci dostupni u Emacs-u se nazivaju 'bafer' (eng. buffer).

Konvencija za imenovanje tastera u Emacs-u ce vam najverovatnije biti nepoznata.

**C-x** se odnosi na Control-x

**M-x** se odnosi na Meta-x

**Note:** 'Meta' odgovara Alt tasteru u vecini slucajeva. Alternativno moze da se koristi Esc taster.

Na primer, za izlazak iz Emacs-a se koristi sledeca sekvenca: **C-x C-c**. Ovo moze da se procita kao "Drzi kontrol i pritisni 'x'. Pusti. Drzi kontrol i pritisni 'c'." Iako Emacs pruza meni liniju, preporucljiva praksa je da se fokusira na ucenje taster sekvenci. Ovo uputstvo ce koristiti imena skracenica prema konvenciji koja se koristi u Emacs-u.

### Pokretanje

Pomeranje kursora je slicno kao i u drugim grafickim editorima. Mis i tasteri sa strelicama mogu da se koriste za promenu pozicije kursora (naziva se kao _point_ u Emacs-u). Standardne komande za kretanje koje se vrsi pomocu tastera sa strelicama takodje imaju pristupacnije skracenice u Emacs-u. Da se pomerite napred jedan karakter, upotrebite **C-f**, da se pomerite jedan karakter unazad, **C-b**. **C-n** i **C-p** se mogu upotrebiti za pomeranje na sledecu i prethodnu liniju, redom. Opet, generalno se preporucuje upotreba ovih precica u odnosu na mis ili tastere sa strelicama.

Kao sto se moze ocekivati, Emacs pruza naprednije komande za kretanje, ukljucujuci kretanje po rec i recenicu. **M-f** pomera napred jednu rec i **M-b** ce pomeriti kursor jednu rec unazad. Slicno, **M-e** pomera kursor jednu recenicu napred i **M-a** jednu recenicu nazad.

Do sada, sve komande za kretanje koje su predstavljene su bile relativne u odnosu na trenutnu poziciju. **M-<** se moze koristiti za pomeranje kursora na pocetak bafera, sa svojim kolegom, **M->**, koji vrsi pomeranje na kraj bafera. Da pomerite kursor na odredjeni broj linije, upotrebite **M-g g**. **M-g g** ce vas upozoriti za zeljeni broj linije. Takodje, da se pomerite na pocetak ili kraj tekuce linije, upotrebite **C-a** ili **C-e**.

**Note:** Skracenice za ove komande, ili bilo koju komandu, se mogu razlikovati _blago_ u zavisnosti od modova koji su trenutno aktivni. Ipak, te skracenice u najvecem broju slucajeva pruzaju jednaku funkcionalnost. Pogledajte [Modes](/index.php/Emacs#Modes "Emacs") za vise informacija.

### Fajlovi i baferi

Emacs pruza seriju komandi koje se primenjuju na fajlove. O najzastupljenijoj komandi ce biti vise detalja ovde. **C-x C-f** se koristi za otvaranje fajla (ova komanda se zove 'find-file' u Emacs-u). Ukoliko zadati fajl ne postoji, Emacs ce otvoriti prazan bafer. Cuvanje bafera ce kreirati fajl sa sadrzajem bafera. **C-x C-s** se moze koristiti za cuvanje bafera. Da sacuvate bafer sa razlicitim imenom fajla, upotrebite **C-x C-w** (ovo je mnemonika za komandu 'write-file'), koja ce upozoriti za novo ime fajla pre njegovog zapisivanja na disk. Takodje je moguce sacuvati sve trenutno otvorene bafere sa **C-x s**. Zadavanjem ove komande, ukoliko su baferi menjani od poslednjeg cuvanja, dobicete upozorenje koje ce vas pitati koju akciju zelite da sprovedete.

**Note:** **C-x C-f** ne cita opet fajl sa diska ako je bafer koji odgovara fajlu i dalje otvoren. Da ponovo iscitate fajl sa diska, ubite bafer (**C-x k**) pre **C-x C-f** ili upotrebite **M-x revert-buffer**.

Mnoge interaktivne komande poput "find-file" ili "write-file" daju upozorenje za unos u skroz donjoj liniji Emacs prozora. Ova linija se naziva _minibuffer_. Minibafer podrzava mnoge osnovne komande za editovanje kao i tab dovrsavanje komandi. Slicno onom koje je dostupno u mnogim *nix komandnim linijama. **<TAB>** se moze pritisnuti dva puta uzastopno za prikaz liste kompletnih komandi, i ako zelite, mozete da upotrebite mis da selektujete kompletnu komandu sa te liste. Kompletiranje u minibaferu je dostupno za mnoge forme unosa ukljucujuci komande i imena fajlova.

Minibafer takodje pruza mogucnost pracenja istorije. Prethodne unesene komande se mogu ponovo pozvati upotrebom **Up Arrow** ili **C-p**.

Da izadjete iz minibafera u bilo kom momentu, pritisnite **C-g**.

Nakon otvaranja nekoliko fajlova, metod za prelazak izmedju njih je neophodan. Otvaranjem fajla koji vec ima svoj bafer u okviru Emacs-a ce prouzrokovati prelazak na taj bafer. Ovo nije najefikasniji nacin. Emacs pruza **C-x b**, koji upozorava za prikaz novog bafera (tab kompletiranje je dostupno). Unosom imena bafera koje ne postoji, novi bafer sa tim imenom ce biti napravljen.

**Note:** Da predjete na prethodni bafer, upotrebite **C-x b <RET>**.

Lista svih otvorenih bafera se moze prikazati upotrebom **C-x C-b**. Ako bafer vise nije potreban, moze se ukloniti sa **C-x k**.

### Editovanje

Postoji veliki broj komandi za editovanje u okviru Emacs-a. Najbitnija komanda je verovatno ona koju jos nismo predstavili, a to je 'undo', koja se moze pokrenuti sa **C-_** ili **C-/**. Komande za kretanje generalno takodje imaju odgovarajuce komande za brisanje. Na primer, **M-<backspace>** se moze koristiti za brisanje reci unazad, i **M-d** za brisanje reci unapred. Da obrisete do kraja linije, ili kraj recenice, upotrebite **C-k** ili **M-k**.

Osnovno je pravilo da ni jedna linija ne treba da prelazi 80 karaktera. Ovo doprinosi citljivosti, pogotovo u slucajevima gde linija obavija na ivici prozora. Automatsko ubacivanje (ili uklanjanje) linije za razdvajanje je poznato kao _filling_ u Emacs-u. Paragraf moze biti popunjen upotrebom **M-q**.

Karakteri i reci mogu biti transponovani koriscenjem **C-t** i **M-t**. Naprimer: `Hello World!` → `World! Hello`

Velika i mala slova su takodje podesiva. **M-l** prebacuje u mala slova sledecu rec od kursora (`HELLO` → `hello`); **M-u** prebacuje u velika slova sledecu rec od kursora (`hello` → `HELLO`) i **M-c** pretvara prvi karakter sledece reci od kursora u veliko slovo, dok ostale karaktere pretvara u mala slova (`hElLo` → `Hello`).

### Ubijanje, yank-ovanje i regioni

Region je deo teksta izmedju dve pozicije. Jedna od ovih pozicija se naziva _mark_, a drugi je tacka. **C-<SPC>** se koristi za zadavanje pocetne pozicije za markiranje, nakon cega tacka moze da se pomera da bi se kreirao region. U okviru GNU Emacs-a 23.1 pa na dalje, ovaj region je vidljiv prema pocetnim podesavanjima. Postoji veliki broj komandi koje deluju na regione, medju kojima se najvise koriste _killing_ komande.

U Emacs-u, cut i paste se nazivaju _kill_ i 'yank_. Mnoge komande koje brisu vise od jednog karaktera (ukljucujuci mnoge od onih vec naponenutih gore, poput **C-k** i **M-d**) zapravo seku (cut-uju) tekst i dodaju ga na ono sto se zove "kill-ring_. Kill-ring je, jednostavno, lista ubijenog teksta. Kill-ring skladisti do 60 zadnjih ubistava, prema pocenim podesavanjima. Sukcesivna ubistva se skladiste na celo liste.

**C-w** i **M-w** se mogu koristiti za ubijanje i kopiranje regiona.

Za ubacivanje ubijenog teksta u bafer (poznato kao 'yank-ovanje'), upotrebite **C-y**. **C-y** se moze koristiti vise puta ako zelite da yank-ujete tekst uzastopno. Kao sto smo pomenuli, prethodna ubistva su skladistena u listi, ipak **C-y** preuzima samo prvi od njih. Ranijim ubistvima se moze pristupiti sa **M-y**. Ovo ce ukloniti tekst ubacen sa 'yank', i zameniti ga sa tekstom ubijenim ranije. **M-y** se mora upotrebiti odmah nakon **C-y** i moze se upotrebiti vise puta uzastopno da biste se kretali kroz kill-ring (ubistvo-prsten ma vazi).

### Pretrazi i zameni

Pretrazivanje za stringom je uobicajena praksa u tekst editovanju. Ovo se moze izvrsiti upotrebom **C-s** (da pretrazite unapred) ili **C-r** (da pretrazite unazad). Ove komande upozoravaju za string za koji vrsite pretragu. Pretraga se vrsi inkrementalno, pa ce traziti sledecu (ili prethodnu) instancu kako budete pisali. Da predjete na sledecu ili prethodnu instancu, pritisnite **C-s** ili **C-r** opet. Kada je instanca pronadjena**<RET>** se moze upotrebiti da zavrsite pretragu. Alternativno, ukoliko zelite da se vratite na poziciju sa koje ste inicirali pretragu, upotrebite **C-g**.

Kada je pretraga zavrsena (i.e., nije abortiran sa **C-g** ili slicno), string za kojim je vrsena pretraga ce biti difolt za sve naredne pretrage. Da iskoristite ovo, pritisnite **C-s C-s** ili **C-r C-r** da izvrsite opet pretragu unapred ili unazad.

Pregrage pomocu regularnih izraza se ponasaju isto kao i pretrage opisane gore izuzev komande koja se koristi za iniciranje pretrage. Upotrebite **C-M-s** ili **C-M-r** da inicirate regexp pretragu unapred ili unazad. Kada je pretraga pomocu regularnih izraza (Regular Expression) startovala, **C-s** i **C-r** se mogu koristiti da pretrazite unapred ili unazad, isto kao sa pretragom stringova.

Kao dodatak pretrazi, takodje je moguce vrsiti zamenu stringova i regularnih izraza (preko **M-%** i **C-M-%**). Upozoravanja su obezbedjena za oba, i inicijalni i tekst kojim vrsimo zamenu, a zatim jos jedno upozorenje koje nas pita koju akciju da izvrsimo na markiranu instancu. Iako je dostupan veliki broj opcija (cela lista je dostupna pritiskom na **?**), najcesce koriscena opcija je **y**, za vrsenje zamene, **n**, da preskocite ovu instancu, i **!** da zamenite ovu i sve ostale instance.

### Uvlake i prefiks argumenti

Uvlake se obicno postizu sa **<TAB>**, za uvlacenje jedne linije, ili sa **C-M-\**, da uvucete region.

Nacin na koji se tekst uvlaci obicno zavisi od _major-mode_-a (glavni mod) koji je aktivan. Glavni mod obicno definise stil uvlacenja u zavisnosti od tipa teksta koji trenutno obradjujemo. (Pogledajte [Modove](/index.php/Emacs#Modes "Emacs") za vise informacija.)

U nekim slucajevima moze da se desi odgovarajuci glavni-mod ne postoji za odredjeni tip fajla, i u tom slucaju je neophodno da rucno pravite uvlake. Napravite region (pogledajte [Ubijanje, jankovanje i regioni](/index.php/Emacs#Killing.2C_yanking_and_regions "Emacs")) zatim izvrsite uvlacenje sa **C-u <n> C-x <TAB>** (gde je '<n>' iznos broja kolona od kojih ce se sastojati uvlaka). Na primer:

Uvecajte uvlaku na regionu za cetiri kolone:

```
C-u 4 C-x <TAB>

```

Smanjige uvlaku na regionu za dve kolone.

```
C-u -2 C-x <TAB>

```

**Note:** Trik je u **C-u**, koji odgovara 'univerzalnom-argumentu' (unversal-argument) komandi. Zadavanje 'univerzalnog-argumenta' je nacin da prosledite vise informacija komandi (ova informacija se naziva 'prefiks argument'). U ovom slucaju, zadali smo broj kolona koji ce ciniti uvlaku koju zelimo da ostvarimo, i to sa komandom **C-x <TAB>**. Bez zadavanja prefiks argumenta, **C-x <TAB>** bi uvecao uvlaku za samo 1 kolonu.

### Prozori i okviri

Emacs je dizajniran za ugodno editovanje mnogih fajlova odjednom. To se postize razdvajanjem Emacs interfejsa na tri nivoa. Naime, baferi, koji su vec predstavljeni, kao i _prozori_ i _okviri_.

_prozor_ pogled koji se koristi za prikazivanje bafera. Prozor moze da prikazuje samo jedan bafer u datom momentu, ali vise bafera moze biti prikazano u vise prozora. Iza svakog prozora postoji _mode-line_ (mod linija), koja prikazuje informacije o tom baferu.

_frejm_ je Emacs-ov _prozor_ (u standardnoj terminologiji. i.e., 'prozor' u smislu moderne desktop paradigme) koji sadrzi naslovnu traku (eng. title bar), meni liniju i jos jednu ili vise 'prozora'.

Od sada pa na dalje cemo koristiti definiciju ovih termina kao sto postoje u Emacs-u.

Da podelite prozor vertikalno ili horizontalno, upotrebite **C-x 2** ili **C-x 3**. Ovo ima efekat kreiranja jos jednog prozora u trenutnom ramu. Da prelazite izmedju vise prozora, upotrebite **C-x o**.

Suprotno od deljenja prozora je njihovo brisanje. Da obrisete prozor u kom se trenutno nalazite, upotrebite **C-x 0** i **C-x 1** da obrisete sve prozore osim prozora u kom se trenutno nalazite.

Kao i kod prozora, takodje je moguce kreiranje i brisanje citavih ramova. **C-x 5 2** kreira ram. Sa **C-x 5 0** mozete da obrisete trenutni ram, a **C-x 5 1** brise sve osim tekuceg rama.

**Note:** Ove komande ne uticu na bafere. Naprimer, brisanje prozora ne ubija bafer koji on prikazuje.

### Dobijanje pomoci

Emacs je samo-dokumentovan po samom dizajnu. Shodno tome, velika kolicina informacija je dostupna za odredjivanje imena odgovarajuce komande ili njenih precica, naprimer. Sledeca lista prikazuje neke od najkorisnijih komandi za dobijanje pomoci:

```
**C-h t**        Startovanje Emacs tutorijala

**C-h b**       Lista precice na tastaturi za glavni mod koji trenutno koristimo

**C-h k**        Pronadji za koju je komandu vezan odredjeni taster

**C-h w**        Pronadji na koji  taster je vezana odredjena komanda

**C-h a**        Pronadji komandu koja odgovara zadatom opisu

**C-h m**        Prikaz informacije o trenutno aktivnim modovima

**C-h f**        Opisuje zadatu funkciju

```

### Modovi

Emacs mod je ekstenzija napisana u Emacs Lispu koji kontrolise ponsanje bafera za koji je vezan. Obicno pruza uvlake, isticanje sintakse i precice za editovanje tog oblika teksta. Sofisticirani modovi mogu da pretvore Emacs u punopravni IDE (integrisano okruzenje za programiranje). Emacs obicno koristi ekstenziju fajlova za odredjivanje modova koji ce biti ucitani.

Korisni modovi za editovanje shell skripti su sh-mode, line-number-mode i column-number-mode. Oni se mogu koristiti paralelno i pokrecu se sa.

**M-x sh-mode <RET>**

**M-x column-number-mode <RET>**

line-number-mode je omogucen prema pocetnim podesavanjima, ali moze se upaliti/ugasiti ponovnim izdavanjem komande:

**M-x line-number-mode <RET>**

sh-mode je _glavni-mod_ (major-mode). Glavni modovi podesavaju Emacs i vrlo cesto pruzaju specijalizovani skup komandi za editovanje odredjenog tipa teksta. Samo jedan glavni mod moze biti aktivan u svakom od bafera. Kao dodatak isticanju sintakse i podrske za uvlake, sh-mode definise nekoliko komandi ciji je cilj da pomogne u editovanju shell skripti. Sledi nekoliko tih komandi:

```
**C-c (**	 Umetanje definicije funkcije

**C-c C-f**	 Umetanje 'for' petlje

**C-c TAB**	 Umetanje 'if' izjave

**C-c C-w**	 Umetanje 'while' petlje

**C-c C-l**	 Umetanje indeksirane petlje od 1 do n

```

'line-number-mode' i 'column-number-mode', su _manji-modovi_ (minor-modes). Manji modovi mogu da se koriste za prosirivanje glavnih modova i mogu se koristiti u neogranicenom broju u datom trenutku.

## Saveti i trikovi

Dok je prethodna sekcija dala pregled osnovnih komandi za editovanje, nije predstavila mogucnosti Emacs-a. Sledeca sekcija ce pokriti neke od naprednijih tehnika i funkcionalnosti.

### TRAMP

TRAMP (Transparent Remote Access, Multiple Protocols) je ekstenzija koja, kao sto i ime sugerise, pruza transparentan pristup udaljenim fajlovima preko velikog broja protokola. Kada budete upitani za ime fajla, unosenjem odredjenog oblika cete pozvati TRAMP. Neki primeri:

Da otvorite /etc/hosts sa root dozvolama:

```
C-x C-f /su::/etc/hosts

```

Da se povezete na 'myhost' kao 'myuser' preko SSH-a i otvorite fajl ~/example.txt:

```
C-x C-f /ssh:myuser@myhost:~/example.txt

```

Staza za TRAMP je obicno u formi '/[protokol]:[[user@]host]:<fajl>'. TRAMP podrzava mnogo vise od primera navedenih gore. Za vise informacija pogledajte TRAMP info za korisnike koji dolazi uz Emacs.

### Makroi sa tastature i registri

Ovaj deo ce pruziti prakticnu demonstraciju upotrebe nekoliko mocnijih metoda za editovanje, a to su _makroi_ i _registri_.

Cilj je da proizvedemo listing serije karaktera i njihove odgovarajuce pozicije u toj listi. Iako je moguce formatirati svaki od njih rucno, to bi bilo sporo i podlozno pravljenju gresaka. Alternativno, neke od Emacs-ovih mocnijih funkcionalnosti za editovanje se mogu upotrebiti. Pre opisa metode, navescemo neke detalje koji stoje iza tehnike.

Prva funkcija koju cemo predstaviti su _registri_. Registri se koriste za skladistenje i preuzimanje raznih tipova podataka od brojeva do podesavanja za prozore. Svakom registru je dodeljeno ime jednog karaktera: ovaj karakter se koristi za pristupanje registru.

Druga funkcija koja ce biti demonstrirana su _makroi sa tastature_. Makro sa tastature skladisti niz komandi kako bi mogli na lak nacin da se izvrse ponovo kasnije.

Pocev od bafera koji sadrzi nas skup karaktera:

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

```

Pripremite registar pokretanjem `number-to-register' komande (**C-x r n**), a zatim uskladistite broj '0' u registar 'k':

```
C-x r n k

```

Sa kursorom na pocetku bafera, startujte makro (**C-x (**) i krenite da formatirate karaktere:

```
C-x ( C-f M-4 .

```

Ubacite (**C-x r i**) i inkrementirajte (**C-x r +**) registar 'k'. Prefiks argument (**C-u**) se kristi da ostavi pointer pozicioniran posle ubacenog teksta.

```
C-u C-x r i k C-x r + k

```

Zavrsite formatiranje ubacivanjem nove linije. Emacs zatim moze da ponovi proces tako sto ce poceti od tacke gde ste poceli sa definisanjem makroa, za ostatak karaktera. **C-x e** kompletira, a zatim pokrece makro. Prefiks argument, **M-0**, uzrokuje da makro bude ponovljen sve dok ne dodje do greske. U tom slucaju on prekida kada dostigne kraj bafera.

```
<RET> M-0 C-x e

```

Rezultat:

```
 A....0
 B....1
 C....2
 [...]
 x....49
 y....50
 z....51

```

### Regularni izrazi

Iz Emacs uputstva: "Regularni izraz, ili _regexp_ skraceno, je model koji podrazumeva (moguce beskonacan) skup stringova." Ova sekcija nece ici u detalje o samim regularnim izrazima (jer, prosto, postoji previse toga da se pokrije). Pruzicemo brzu demonstraciju o moci regularnih izraza. Pogledajte [Regularni izrazi](http://www.gnu.org/software/emacs/manual/html_node/elisp/Regular-ressions.html#Regular-Expressions) sekciju u Emacs uputstvu za vise informacija.

S obzirom na isti scenario predstavljen gore: Lista karaktera koji treba da bude formatiran tako da predstavljaju svoje mesto u listi. (pogledajte [Makroi sa tastature i registri](/index.php/Emacs#Keyboard_macros_and_registers "Emacs")). Opet, pocev sa sadrzajem bafera.

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

```

Na pocetku bafera, upotrebite **C-M-%** (ako vam je tesko da pritisnete skup tastera, upotrebite **M- query-replace-regexp**). Na liniji:

```
\(.\)

```

ch se poklapa sa jednim karakterom. Zatim, kada nas upozori za zamenu:

```
\1....\#^J

```

**Note:** '^J' predstavlja mesto gde bi trebala da se stavi nova linija. Nebi trebala da se unosi u liniji. Nova linija mora biti uneta bukvalno upotrebom **C-q C-j**.

Izraz za zamnu kaze: "Ubacite tekst koji se podudara izmedju prvog skupa zagrada (u ovom slucaju, jedan karakter), praceno sa 4 zareza i zatim jedan automatski uvecan broj pracen sa novom linijom.

Konacno, pritisnite **!** za y za ceo bafer. Sva formatiranja koja su izvrsena u prethodnoj sekciji si izvrsena sa jednim regexp-om.

### Prilagodjavanje

Emacs se moze podesavanjem editovanjem '~/.emacs' ili upotrebom komande **M-x customize**. Ova sekcija ce se fokusirati na rucno editovanje ~/.emacs, i pruziti neke primere za demonstraciju onih delova Emacs-a koji se obicno konfigurisu. Customize komanda pruza jednostavan interfejs za podesavanje, ali moze postati ogranicavajuce kako postajete upoznatiji sa Emacs-om.

Svi primeri se mogu izvrsiti dok Emacs radi. Da evaluirate izjavu u Emacs-u, upotrebite:

**eval-buffer** kao komandu ili,

**C-x C-e** da evaluirate zadnju izjavu

Za neke korisnike, ukucavanje 'yes' i 'no' je zamorno. Da umesto toga koristite 'y' i 'n' tastere dodajte ovo u .emacs:

```
(defalias 'yes-or-no-p 'y-or-n-p)

```

a zatim izvrsite **eval-buffer** u .emacs baferu.

Da zaustavite kursor upotrebite:

```
(blink-cursor-mode -1)

```

Slicno, da omogucite column-number-mode, kao sto je diskutovano u prethodnom delu:

```
(column-number-mode 1)

```

Slicnosti izmedju prethodne dve komande nisu slucajnost: blink-cursor-mode i column-number-mode su oba minor-modovi. Kao pravilo, manji modovi se mogu upaliti zadavanjem pozitivnog argumenta ili ugasiti sa negativnim argumentom. Ako se argument izostavi, manji mod ce biti naizmenicno zamenjen upaljen/ugasen.

Evo jos dodatnih primera manjih modova. Sledeci ce onemoguciti trake za skrolovanje, meni liniju i liniju za alatke.

```
(scroll-bar-mode -1)
(menu-bar-mode -1)
(tool-bar-mode -1)

```

Varijabla, 'auto--alist', se moze modifikovati da promeni glavni mod koji se koristi za odredjena imena fajlova. Sledeci primer ce napraviti difolt glavni mod za '.tut' i '.req' fajlove 'text-mode'.

```
(setq auto-mode-
  (
    '(("\\.tut$" . text-e)
      ("\\.req$" . text-e))
    auto-mode-alist))

```

Podesavanja se takodje mogu primeniti na nivou modova. Uobicajena metoda za ovo je dodavanje funkcije _hook_. Naprimer, da forsirate uvlake da koriste razmake umesto tabova, ali samo u text-mode:

```
(add-hook 'text-mode-ook (lambda () (setq indent-tabs-mode nil)))

```

Slicno, da samo koristite razmake za uvlake bilo gde:

```
(set-default indent--mode nil)

```

Precice na tastaturi se mogu podesiti na dva nacina. Prvi je pomocu 'define-key'. 'define-key' pravi precicu za komandu ali samo u jednom modu. Primer ispod ce napraviti da **F8** brise sve prazne prostore od kraja svake linije u 'text-mode' baferu:

```
(define-key text-mode-map (kbd "<f8>") 'delete-trailing-whitespace)

```

Drugi metod je 'global-set-key'. Ovo se koristi za bindovanje tastera na komandu bilo gde. Da bindujete 'query-replace-regexp' (**C-M-%**) na '<f7>'.

```
(global-set-key (kbd "<7>") 'query-replace-regexp)

```

Bindovanje komande na alternativni taster ne zamenjuje vec postojece bindove. Ukratko, 'query-replace-regexp' ce biti zdruzen sa obe precice **F7** i **C-M-%** nakon gornjeg primera.

Skoro sve u Emacs-u se moze podesiti. Pretrazivanje [Emacs Wiki](http://emacswiki.org/) ce vam dati solidno mesto za start.

### Ekstenzije

I pored toga sto Emacs sadrzi stotine modova, biblioteka i drugih ekstenzija, postoji jos dostupnih za dalje prosirenje Emacs-ovih sposobnosti. Vecina njih dolazi sa instrukcijama koje opisuju sve izmene koje je neophodno izvrsiti u ~/.emacs fajlu. Ove instrukcije se generalno mogu naci u delu sa komentarima na pocetku elisp sors koda, ili u README (ili slicno) fajlu u slucaju da ekstenzija sadrzi vise sors fajlova.

Veliki broj popularnih ekstenzija su dostupni kao paketi u 'community' repozitorijumu, a jos dosta je dostupno preko [AUR](/index.php/AUR "AUR")-a. Imena tih paketa imaju 'emacs-' prefiks (naprimer, emacs-lua-mode). U mnogo slucajeva, izmene koje moraju da se izvrse na ~/.emacs se prikazu tokom instalacije paketa.

Ukoliko se desi da instrukcije za aktiviranje odredjene ekstenzije nisu dostupne u gore napomenutim lokacijama, proverite odgovarajucu stranicu u [Emacs Wiki](http://emacswiki.org/), koja ce skoro sigurno obezbediti primer podesavanja. Emacs Wiki je isto poznat kao izvor za otkrivanje jos dodatnih ekstenzija.

Takodje mozete da upotrebite [Emacs Lisp Paket Arhiva (ELPA)](http://tromey.com/elpa/) da automatski instalirate pakete. Pogledajte web sajt za instrukcije. ELPA ce biti sadrzan u Emacs 24 (sledeca verzija Emacs-a); to je prihvacen deo Emacs ekosistema.

## Resavanje problema

### Problemi sa obojenim izlazom

Prema pocetnim podesavanjima, Emacs shell ce prikazati cudne simbole umesto zeljenog izlaza.

Ubacivanjem sledeceg u `~/.emacs` resava problem:

```
(add-hook 'shell-mode-ook 'ansi-color-for-comint-mode-on)

```

### Meniji se prikazuju kao prazni

Postoji bag u GNU Emacs-u 23.1 (ako koristite GTK skup alata) koji moze prouzrokovati da neki meniji budu prazni. Ovo je, izgleda, reseno u Emacs CVS stablu. [Debian bag izvestaj](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=550541) sadrzi resenje.

### Problemi sa prikazivanjem karaktera u X prozorima

Ako su, kada startujete emacs u X prozorima, svi karakteri u glavnom prozoru sa belim granicama (one koje vidite kada probate da vidite karaktere za koje nemate instalirane odgovarajuce fontove), neophodno je da instalirate xorg-fonts-75dpi i/ili xorg-fonts-100dpi i da restartujete X prozore.

### Sporo startovanje

Sporo startovanje obicno iz dva razloga.

Da odredite koji bi mogao da bude, pokrenite Emacs sa:

```
$ emacs -q

```

Ako Emacs i dalje startuje sporo, pogledajte [Neispravno podesavanje mreze](/index.php/Emacs#Incorrect_network_configuration "Emacs"). Ako ne, skoro je sigurno [problem u vasem .emacs](/index.php/Emacs#Init_file_ads_slowly "Emacs").

#### Netacno podesavanje mreze

Greske, obicno u /etc/hosts, ce obicno rezultirati sa 5+ sekundi kasnjenja prilikom startovanja Emacs-a. Pogledajte '[podesite ime hosta](/index.php/Configuring_network#Set_the_hostname "Configuring network")' uputstvo za podesavanje mreze za vise informacija.

#### Opterecenje init fajla

Jednostavan nacin da pronadjete uzrok je da stavite pod komentar (dodate kao prefiks liniji ';') na sumnjive delove vaseg ~/.emacs -a (ili ~/.emacs.d/init.el), a zatim da startujete Emacs ponovo da vidite da li ima promena. Imajte na umu da "require" i "load" mogu da uspore startovanje, posebno kada se koriste sa ekstenzijama. Njih treba, po pravilu, koristiti samo kad je njihov cilj: da budu u upotrebi odma po startovanju Emacs-a ili pruzaju malo vise od "ucitavanja" za ekstenziju. U suprotnom, koristite 'autoload funkciju direktno. Naprimer, umesto:

```
(require 'anything)

```

mozete da upotrebite:

```
(autoload 'anything "thing" "Select anything" t)

```

### Cannot open load e: ...

Najcesci uzrok ove greske je 'load-path' varijabla koja ne sadrzi stazu do direktorijuma u kom se ekstenzija nalazi. Da resite to, dodajte odgovarajucu stazu u listu koja ce biti pretrazena pre ucitavanja ekstenzije:

```
 (add-to-list 'load-path "/path/to/directory/")

```

Kada pokusavate da koristite pakete za ekstenzije i Emacs je podesen sa prefiksom drugim nego '/usr', load-path ce morati da bude osvezen. Stavite sledece u ~/.emacs pre instrukcija koja dolaze uz paket:

```
 (add-to-list 'load-path "/usr/share/emacs/site-lisp")

```

Ako rucno kompajlirate Emacs, imajte na umu da je difolt prefiks '/usr/local'.

## Izvori

*   [GNU Emacs home stranica](http://www.gnu.org/ftware/emacs/)
*   [GNU Emacs uputsvo](http://www.gnu.org/ftware/emacs/manual/emacs.html)
*   [Emacs Wiki](http://www.emacswiki.org/cgi-bin/wiki/)
*   [Korisno uvod u Emacs i njegove precice](http://www2.lib.go.edu/keith/tcl-course/emacs-tutorial.html)
*   [Emacs crkva](http://www.dina.kvl./~abraham/religion/)