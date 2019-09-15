Related articles

*   [Često postavljena pitanja](/index.php/Frequently_asked_questions_(Bosanski) "Frequently asked questions (Bosanski)")
*   [Instalacijske upute](/index.php/Installation_guide_(Bosanski) "Installation guide (Bosanski)")
*   [Lista aplikacija](/index.php?title=List_of_applications_(Bosanski)&action=edit&redlink=1 "List of applications (Bosanski) (page does not exist)")

Ovaj dokument je anotirani index popularnih članaka i važnih informacija za poboljšavanje i dodavanje funkcionalnosti u instalirati Arch sistem. Pretpostavlja se da su čitaoci pročitali instalacijske upute da dobiju osnovu Arch instalaciju. Pročitali i razumjeti koncepte u [#Sistemska administracija](#Sistemska_administracija) i [#Paket menadžment](#Paket_menadžment) je preduslov za ostale sekcije na ovoj stranici i ostale članke u wiki-u.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Sistemska administracija](#Sistemska_administracija)
    *   [1.1 Korisnici i grupe](#Korisnici_i_grupe)
    *   [1.2 Elevacija privilegija](#Elevacija_privilegija)
    *   [1.3 Menadžment servisa](#Menadžment_servisa)
    *   [1.4 Nadgledanje sistema](#Nadgledanje_sistema)

## Sistemska administracija

Ova sekcija se odnosi na administrativne taskove i sistem menadžment. Za više, pogledajte [Core utilities](/index.php/Core_utilities "Core utilities") i [Category:System administration (Bosanski)](/index.php/Category:System_administration_(Bosanski) "Category:System administration (Bosanski)").

### Korisnici i grupe

Svježa instalacija ima samo [superuser](https://en.wikipedia.org/wiki/Superuse za više detalja.

Korisnici i grupe imaju mehanizam za *access control*; administrator mogu fine-tunati članove grupa i ko je vlasnik fajlova da dodijlete ili oduzmu privilegije na sistemu. Pročitaj [Korisnici i grupe](/index.php?title=Korisnici_i_grupe&action=edit&redlink=1 "Korisnici i grupe (page does not exist)") članak za detalje i potencijalne sigurnosne rizike.

### Elevacija privilegija

Oba, i [su](/index.php/Su "Su") i [sudo](/index.php/Sudo "Sudo") komande omogućavaju pokretanja komandi kao drugi korisnik. *su* po defaultu starta interaktivni shell kao root user, a *sudo* by default privremeno dodijeli root privilegije za jednu komandu. Pogledaj njihove članke za više informacija.

### Menadžment servisa

Arch Linux koristi [systemd](/index.php/Systemd "Systemd") kao [init](/index.php/Init "Init") process, koji je menadžment alat servisa i sistema za Linux. Za održavanje tvog Arch Linuxa, dobra ideja je naučiti njegove osnove. Interakcija sa [systemd](/index.php/Systemd "Systemd") se radi korištenjem *systemctl* komande. Pročitaj [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd") za više informacija.

### Nadgledanje sistema

Arch je rolling release sistem i ima brzi preokret paketa, što znači da korisnsici moraju uložiti vrijeme da rade [nadgledanje sistema](/index.php/System_maintenance "System maintenance"). Procitaj [[Security] za savjete i najbolje prakse za hardening sistema.