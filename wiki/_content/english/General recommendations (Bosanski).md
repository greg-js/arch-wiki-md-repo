Related articles

*   [Često postavljena pitanja](/index.php/Frequently_asked_questions_(Bosanski) "Frequently asked questions (Bosanski)")
*   [Instalacijske upute](/index.php/Installation_guide_(Bosanski) "Installation guide (Bosanski)")
*   [Lista aplikacija](/index.php/List_of_applications_(Bosanski) "List of applications (Bosanski)")

Ovaj dokument je anotirani index popularnih članaka i važnih informacija za poboljšavanje i dodavanje funkcionalnosti u instalirati Arch sistem. Pretpostavlja se da su čitaoci pročitali instalacijske upute da dobiju osnovu Arch instalaciju. Pročitali i razumjeti koncepte u [#Sistemska administracija](#Sistemska_administracija) i [#Paket menadžment](#Paket_menadžment) je preduslov za ostale sekcije na ovoj stranici i ostale članke u wiki-u.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Sistemska administracija](#Sistemska_administracija)
    *   [1.1 Korisnici i grupe](#Korisnici_i_grupe)
    *   [1.2 Elevacija privilegija](#Elevacija_privilegija)
    *   [1.3 Menadžment servisa](#Menadžment_servisa)
    *   [1.4 Nadgledanje sistema](#Nadgledanje_sistema)
*   [2 Paket menadžment](#Paket_menadžment)
    *   [2.1 pacman](#pacman)
    *   [2.2 Repositories](#Repositories)
    *   [2.3 Mirori](#Mirori)
    *   [2.4 Arch Build System](#Arch_Build_System)
    *   [2.5 Arch User Repository](#Arch_User_Repository)
*   [3 Bootanje](#Bootanje)
    *   [3.1 Automatsko prepoznavanje hardware-a](#Automatsko_prepoznavanje_hardware-a)
    *   [3.2 Microcode](#Microcode)
    *   [3.3 Očuvanje boot poruka](#Očuvanje_boot_poruka)
    *   [3.4 Num Lock aktivacija](#Num_Lock_aktivacija)
*   [4 Graphical user interface](#Graphical_user_interface)
    *   [4.1 Display server](#Display_server)
    *   [4.2 Display driveri](#Display_driveri)
    *   [4.3 Desktop okruženja](#Desktop_okruženja)
    *   [4.4 Window menadžeri](#Window_menadžeri)
    *   [4.5 Display menadžeri](#Display_menadžeri)
    *   [4.6 Korisnički folderi](#Korisnički_folderi)
*   [5 Power menadžment](#Power_menadžment)
    *   [5.1 ACPI eventovi](#ACPI_eventovi)
    *   [5.2 Skaliranje CPU frekvencije](#Skaliranje_CPU_frekvencije)
    *   [5.3 Laptopu](#Laptopu)
    *   [5.4 Suspend i hibernate](#Suspend_i_hibernate)
*   [6 Multimedia](#Multimedia)
    *   [6.1 Zvuk](#Zvuk)
    *   [6.2 Browser plugini](#Browser_plugini)
    *   [6.3 Codecs](#Codecs)
*   [7 Networking](#Networking)
    *   [7.1 Sinhronizacija sata](#Sinhronizacija_sata)
    *   [7.2 DNS sigurnost](#DNS_sigurnost)
    *   [7.3 Podešavanje firewall-a](#Podešavanje_firewall-a)
    *   [7.4 Dijeljenje resursa](#Dijeljenje_resursa)
*   [8 Ulazni uređaji](#Ulazni_uređaji)
    *   [8.1 Layout tastature](#Layout_tastature)
    *   [8.2 Dugmići na mišu](#Dugmići_na_mišu)
    *   [8.3 Laptop touchpadi](#Laptop_touchpadi)
    *   [8.4 TrackPointi](#TrackPointi)
*   [9 Optimizacija](#Optimizacija)
    *   [9.1 Benchmarking](#Benchmarking)
    *   [9.2 Poboljšavanje performansi](#Poboljšavanje_performansi)
    *   [9.3 Solid state drives](#Solid_state_drives)
*   [10 Sistemski servisi](#Sistemski_servisi)
    *   [10.1 Indeksiranje fajlova i pretraga](#Indeksiranje_fajlova_i_pretraga)
    *   [10.2 Local mail delivery](#Local_mail_delivery)
    *   [10.3 Printanje](#Printanje)
*   [11 Izgled](#Izgled)
    *   [11.1 Fontovi](#Fontovi)
    *   [11.2 GTK i Qt teme](#GTK_i_Qt_teme)
*   [12 Konzolna poboljšavanje](#Konzolna_poboljšavanje)
    *   [12.1 Tab-completion enhancements](#Tab-completion_enhancements)
    *   [12.2 Aliasi](#Aliasi)
    *   [12.3 Alternativni shell-ovi](#Alternativni_shell-ovi)
    *   [12.4 Bash dodaci](#Bash_dodaci)
    *   [12.5 Obojeni output](#Obojeni_output)
    *   [12.6 Kompresovani fajlovi](#Kompresovani_fajlovi)
    *   [12.7 Konzolni prompt](#Konzolni_prompt)
    *   [12.8 Emacs shell](#Emacs_shell)
    *   [12.9 Mouse podrška](#Mouse_podrška)
    *   [12.10 Scrollback buffer](#Scrollback_buffer)
    *   [12.11 Session menadžment](#Session_menadžment)

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

Arch je rolling release sistem i ima brzi preokret paketa, što znači da korisnici moraju uložiti vrijeme da rade [nadgledanje sistema](/index.php/System_maintenance "System maintenance"). Procitaj [[Security] za savjete i najbolje prakse za hardening sistema.

## Paket menadžment

Ova sekcija sadrži korisne informacije vezano za paket menadžment. Za više, pogledajte [Paket menadžment](/index.php/Frequently_asked_questions_(Bosanski) "Frequently asked questions (Bosanski)") i [Category:Packet management](/index.php?title=Category:Packet_management&action=edit&redlink=1 "Category:Packet management (page does not exist)").

**Note:** Imperativ je da se bude up to date sa promjenama u Arch Linux koje zahtjevaju manuelnu intervenciju **prije** upgrade-anja sistema. Prijavi se na [arch-announce mailing listu](https://mailman.archlinux.org/mailman/listinfo/arch-announce) ili [RSS news feed](https://www.archlinux.org/feeds/news). Alternativno, provjeri početnu stranicu [Arch vijesti](https://www.archlinux.org/) prije svakog update-a.

### pacman

[pacman](/index.php/Pacman "Pacman") je Arch Linux *pac*kage*man*ager: svi korisnici su obavezi da se upoznaju sa njim prije čitanja ostalih članaka.

Vidi [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") za savjete kako poboljšati interakciju sa *pacman*-om i paket menadžmentom generalno.

### Repositories

Vidi [Official repositories](/index.php/Official_repositories "Official repositories") članke za detalje o svrsi svakog oficijalno održavanog repository-a.

Ako planiraš koristiti 32-bitne aplikacije, moraš enable [multilib](/index.php/Multilib "Multilib") repository.

[Neoficijalni korisnički repository](/index.php/Unofficial_user_repositories "Unofficial user repositories") članak izlistava nekoliko nepodržanih repository-a.

Možda bi trebao razmisliti o instaliranju [pkgstats](/index.php/Pkgstats "Pkgstats") servisa.

### Mirori

Posjeti [Mirori](/index.php/Mirrors "Mirrors") članak za korake da se u potpunosti iskoriste najbrži i oni mirori koji su up to date. Kao što je objašnjeno u članku, dobar savjet je periodično provjeriti [Status mirora](https://www.archlinux.org/mirrors/status) stranicu za listu mirora koji su nedavno sinhronizovani.

### Arch Build System

*Ports* je sistem koji je inicijalno korišten od strane BSD distribucije koji se sadrži od build skripti koje se nalaze u directory tree na lokalnom sistemu. Jednostavno rečeno, svaki port sadrži skriptu unutar folder intuitivno nazvana kao i instalabilna third-party aplikacija.

[Arch Build System](/index.php/Arch_Build_System "Arch Build System") nudi istu funkcionalnost tako što pruža build skripte nazvane [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), koje su popunjene informacijama za određeni software: hash-evi, URL projekta, verzija, licenca i build instrukcije. Ovi PKGBUILD-ovi su parsirane sa [makepkg](/index.php/Makepkg "Makepkg"), program koji generiše pakete kojima se upravlja sa *pacman*-om.

Svaki paket unutar repository zajedno sa paketima unutar AUR mogu se rekompajlirati sa *makepkg*.

### Arch User Repository

Dok Arch Build System dozvoljava buildanje software-a dostupnog u oficijelnim repository-ima, [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) je ekvivalent njemu za pakete submittane od strane korisnika. To je nepodržani repository build skripti dostupne preko [web interfejs](https://aur.archlinux.org) ili kroz [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface").

## Bootanje

Ova sekcija sadrži informacije vezano za proces bootanja. Overview proces Arch bootanja može se pronaći na [Arch boot process](/index.php/Arch_boot_process "Arch boot process"). Za više pogledaj [Category:Boot process](/index.php/Category:Boot_process "Category:Boot process").

### Automatsko prepoznavanje hardware-a

Hardware bi trebao automatski biti prepoznat od strane [udev](/index.php/Udev "Udev") tokom boot procesa. Potencijalno poboljšanje u vremenu bootanja može se postići isključivanje auto-loading-a i navesti željene module manuelno, kao što je opisano u [Kernel modules](/index.php/Kernel_modules "Kernel modules"). Dodatno, [Xorg](/index.php/Xorg "Xorg") bi trebao automatski detektovati potrebne drivere koristeći `udev`, ali korisnici imaju opciju manuelnog konfigurisanja X servera.

### Microcode

Procesori mogu imati [pogrešno ponašanje](https://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), koje kerne može riješiti ažuriranjem *mikrokoda* na startupu. Vidi [Microcode](/index.php/Microcode "Microcode") za detalje.

### Očuvanje boot poruka

Nakon što se boot proces završi, ekran se počisti i pojavi se login prompt što onemogućava korisnike da dobiju feedback od boot procesa. [Isljuči čišćenje ekrana od boot poruka](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") da prevaziđes ovaj limit.

### Num Lock aktivacija

[Num Lock](https://en.wikipedia.org/wiki/Num_Lock "wikipedia:Num Lock") je toggle tipka koja ima na većini tastatura. Za aktiviranje Num Lock-a tokom startup-a, vidi [Activating NumLock on Bootup](/index.php?title=Activating_NumLock_on_Bootup&action=edit&redlink=1 "Activating NumLock on Bootup (page does not exist)").

## Graphical user interface

Ova sekcija pruža orijentaciju za korisnike koji žele da pokrenu grafičke aplikacija na svom sistemu. Vidi [Category:Graphical user interfaces](/index.php/Category:Graphical_user_interfaces "Category:Graphical user interfaces") za dodatne resurse.

### Display server

[Xorg](/index.php/Xorg "Xorg") je public, open-source implementacija [X Window System-a](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (većinom X11 ili X). On je preduslov za pokretanje aplikacija GUI-em i većina korisnika će htjeti da ga instalira.

[Wayland](/index.php/Wayland "Wayland") je noviji, alternativni display server protokol i referenca implementacija od Westona je dostupna.

### Display driveri

Defaultni *vesa* display driver će raditi sa većinom grafičkih kartica, ali performanse se mogu poboljšati instaliranjem drivera za [AMD](/index.php/Xorg#AMD "Xorg"), [Intel](/index.php/Intel "Intel") ili [NVIDIA](/index.php/NVIDIA "NVIDIA") proizvode.

### Desktop okruženja

Iako Xorg pruža osnovni framework za buildanje grafičkog okruženja, dodatne komponente mogu biti potrebne za potpuni korisnički doživljaj. [Desktop okruženja](/index.php/Desktop_environment "Desktop environment") poput [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE") i [Xfce](/index.php/Xfce "Xfce") zapakuju unutar sebe veliki spektar *X klijenata*, poput window menadžera, panela, fajl menadžera, terminala, text editora, ikona i drugih alata. Korisnici sa manje iskustva bi trebali instalirati desktop okruženje sa kojim su više upoznati. Vidi [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") za dodatne resurse.additional resources.

### Window menadžeri

Iskusno desktop okruženje pruža potpuni i konzistentni GUI, ali troši dosta resursa. Korisnici koje žele da maksimiziraju performanse ili da pojednostave svoje okruženje, mogu instalirati [window menadžer](/index.php/Window_manager "Window manager") sami i odabrati željene dodatke. Većina desktop okruženja dozvoljava alternativne window menadžere. [Dinamični](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [stacking](/index.php/Category:Stacking_WMs "Category:Stacking WMs") i [tilling](/index.php?title=Category:Tilling_WMs&action=edit&redlink=1 "Category:Tilling WMs (page does not exist)") window menadžeri razlikuju se u tome kako operišu što se tiče pozicioniranje windowa.

### Display menadžeri

Većina desktop okruženja uključuje [display menadžer](/index.php/Display_manager "Display manager") za automatsko startanje desktop okruženja i menadžment korisničkih logina. Korisnici bez desktop okruženje mogu posebno instalirati jedan. Alternativno, možda moraš startati [X na loginu](/index.php/Start_X_at_login "Start X at login") kao jednostavnu alternativu display menadžeru.

### Korisnički folderi

Dobro poznati korisnički folderi poput Downloads ili Music su kreirani od strane `xdg-user-dirs-update.service` korisničkog servisa, koji je dostupan od strane [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) i enablan po defaultu prilikom instalacije. Ako tvoje desktop okruženje ili window menadžer ne pulla paket, možeš ga sam [instalirati](/index.php/Install "Install") i pokrenuti `xdg-user-dirs-update` manuelno kao što je navedeno u [XDG user directories#Creating default directories](/index.php/XDG_user_directories#Creating_default_directories "XDG user directories").

## Power menadžment

Ovaj sekcija može biti od koristi korisnicima sa laptopom ili generalno korisnicima željnim kontrole nad powerom. Za više, pogledaj [Category:Power management](/index.php/Category:Power_management "Category:Power management").

Vidi [Power management](/index.php/Power_management "Power management") za generalni pregled.

### ACPI eventovi

Korisnici mogu konfigurisati kako sistem reagira na ACPI eventove poput pritiskanja power tipke ili poklapanja laptopa. Za novije metode(bolje) koristeći [systemd](/index.php/Systemd "Systemd"), vidi [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management"). Za starije metode, koristi [acpid](/index.php/Acpid "Acpid").

### Skaliranje CPU frekvencije

Moderni procesori mogu sniziti svoju frekvenciju i napon da smanje toplotu i power consumption. Manje toplote rezultira tihih sistemom i produžuje život hardware-a. Vidi [Skaliranje CPU frekvencije](/index.php/CPU_frequency_scaling "CPU frequency scaling") za detalje.

### Laptopu

Za članke vezane za laptope zajedno sa specifičnim instalacijama za modele, vidi [Category:Laptops](/index.php/Category:Laptops "Category:Laptops"). Za generalni overview članaka vezanih za laptope i savjete, vidi [Laptop](/index.php/Laptop "Laptop").

### Suspend i hibernate

Vidi glavni artikal: [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate").

## Multimedia

[Category:Multimedia](/index.php/Category:Multimedia "Category:Multimedia") sadrži dodatne resurse.

### Zvuk

[Zvuk](/index.php/Sound "Sound") je omogućen od strane kernel drivera za zvuk:

*   [ALSA](/index.php/ALSA "ALSA") je uključen unutar kernel i preporučen je jer obično radi out of the box (samo mora biti [unmuted](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channes "Advanced Linux Sound Architecture")).
*   [OSS](/index.php/OSS "OSS") je alternativa u slučaju kada ALSA ne radi.

Korisnici mogu dodatno instalirati i konfigurasati [zvučni server](/index.php/Sound_system#Sound_servers "Sound system") poput [PulseAudio](/index.php/PulseAudio "PulseAudio"). Za napredne zahtjeva zvuka, vidi [professional audio](/index.php/Professional_audio "Professional audio").

### Browser plugini

Za pristup određenom web sadržaju, [browser plugin](/index.php/Browser_plugins "Browser plugins") poput Adobe Acrobat Reader-a, Adobe Flash Player-a i Jave mogu biti instalirani.

### Codecs

[Codecs](/index.php/Codecs "Codecs") su korišteni od strane multimedijalnih aplikacija za enkodiranje i dekodiranje streama zvuka ili videa. Da bi korisnici mogli pustiti određeni enkodirani stream, moraju imati pravi codec instaliran.

## Networking

Ova sekcija je vezana za male mrežne procedure. Idi na [mrežnu konfiguraciju](/index.php/Network_configuration "Network configuration") za puni guide. Za više, pogledaj [Category:Networking](/index.php/Category:Networking "Category:Networking").

### Sinhronizacija sata

[Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) je protokol za sinhronizovanje sata računara preko mreže. Vidi [vremensku sinhronizaciju](/index.php/Time_synchronization "Time synchronization") za implementaciju takvog protokola.

### DNS sigurnost

Za bolju sigurnost tokom browsanja interneta, plaćanja online, povezivanje na [SSH](/index.php/SSH "SSH") servise i slične taskove koristeći [DNSSEC](/index.php/DNSSEC "DNSSEC")-enabled [DNS resolver](/index.php/DNS_resolver "DNS resolver") koji može validirati potpisane [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") rekorde, i enkriptovani protokol poput [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS"), [DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") ili [DNSCrypt](https://en.wikipedia.org/wiki/DNSCrypt "wikipedia:DNSCrypt"). Vidi [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution") za detalje.

### Podešavanje firewall-a

Firewall može pružiti dodatni nivo zaštite na vrhu Linux network stacka. Dok je stock Arch kernel u mogućnosti koristiti [[Wikipedia:Netfilter|Netfilter-ove] [iptables](/index.php/Iptables "Iptables") i [nftables](/index.php/Nftables "Nftables"), ni jedan od njih nije enablan po defaultu. Preporučuje se podešavanje neke vrste firewalla. Vidi [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") za dostupne guidove.

### Dijeljenje resursa

Za dijeljenje fajlova između različitih mašina na mreži, prati [NFS](/index.php/NFS "NFS") ili [SSHFS](/index.php/SSHFS "SSHFS") članke.

Koristi [sambu](/index.php/Samba "Samba") da pristupis Windows mreži. Za konfiguraciju mašine da koristi Active Directory za autentifikaciju, pročitaj [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration").

Vidi također [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Ulazni uređaji

Ova sekcija sadrži popularne konfiguracijske savjete za ulazne uređaje. Za više, vidi [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Layout tastature

Neengleske ili druge nestandardne tastature mogu da ne funkcionišu očekivano po defaultu. Potrebni koraci za konfigurisanju keymapa za virtuelnu konzolu i [Xorg](/index.php/Xorg "Xorg"), opisani su [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") i [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

### Dugmići na mišu

Vlasnici naprednog ili neobičnog miša mogu primjetiti da tipke nisu prepoznate uopće po defaultu, ili žele da dodijele drukčije akcije za njih. Instrukcije se mogu pronaći na [Mouse buttons](/index.php/Mouse_buttons "Mouse buttons").

### Laptop touchpadi

Veliki broj laptopa koristi [Synaptics](https://www.synaptics.com/) ili [ALPS](https://www.alps.com) touchpad-e. Za ove i slične touchpad modele, možeš koristiti ili Synaptics ulazne drivere ili libinput; vidi [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") i [libinput](/index.php/Libinput "Libinput") za instalaciju i konfiguraciju.

### TrackPointi

Vidi [TrackPoint](/index.php/TrackPoint "TrackPoint") članak za konfiguraciju TrackPoint uređaja.

## Optimizacija

Ova sekcija pokušava da sumira tweak-ove, alate i dostupne opcije za poboljšanje sistema i performansi aplikacija.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") je akt mjerenja performansi i poređenja rezultata sa rezultatima drugog sistema ili široko prihvaćenog standarda.standard through a unified procedure.

### Poboljšavanje performansi

Članak [Improving performance](/index.php/Improving_performance "Improving performance") ima informacije vezano za to i osnova je za poboljšavanje performansi u Arch Linuxu.

### Solid state drives

[Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") članak pokriva mnoge aspekte solid state drives-a, uključujući njihovi konfiguraciju da se maksimizira njihov život.

## Sistemski servisi

Ova sekcija je vezana za [daemone](/index.php/Daemons "Daemons"). Za više, vidi [Category:Daemons](/index.php/Category:Daemons "Category:Daemons").

### Indeksiranje fajlova i pretraga

Većina distribucija ima *locate* komandu dostupnu za brzo pretraživanje fajlova. Da se ubaci ova funkcionalnost u Arch Linux, [mlocate](https://www.archlinux.org/packages/?name=mlocate) je preporučen da se instalira. Nakon instalacije, pokreni *updatedb* za indeksiranje fajlsistema.

[Desktop search engine](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities") pruža sličan servis dok je u isto vrijeme bolje integrisan u [desktop okruženja](/index.php/Desktop_environment "Desktop environment").

### Local mail delivery

Defaultni setup nema način za sinhronizaciju mailova. Za konfiguraciju *Postix*-a za jednostavan lokalni mailbox delivery, vidi [Postfix](/index.php/Postfix "Postfix"). Druge opcije su [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD"), [msmtp](/index.php/Msmtp "Msmtp") i [fdm](/index.php/Fdm "Fdm").

### Printanje

[CUPS](/index.php/CUPS "CUPS") je standardno bazirani, open source sistem za printanje razvijen od strane Apple-a. Vidi [Category:Printers](/index.php/Category:Printers "Category:Printers") za članke vezano za printere.

## Izgled

Ova sekcija sadrži "lijepe" tweak-ove za ugodno iskustvo za Arch-om. Za više, vidi [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Fontovi

Možda ćeš htjeti instalirati set TrueType fontova, jer su jedino neskalabilni bitmap fontovi uključeni u basic Arch sistem. Postoji nekoliko general-purpose [font familija](/index.php/Fonts#Families "Fonts") koje pružaju [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") podršku i čak [metric kompatibilnost](/index.php/Metric-compatible_fonts "Metric-compatible fonts") sa fontovima drugih operativnih sistema.

Dosta informacija o ovoj temi se može pronaći na [fontovi](/index.php/Fonts "Fonts") i [konfiguracija fonta](/index.php/Font_configuration "Font configuration") člancima.

Ukoliko korisnik provodi puno vremena za virtuelnom konsolom, korisnici mogu promijeniti konzolni font; vidi [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console").

### GTK i Qt teme

Veliki dio aplikacije za grafičkim interfejsom za Linux sisteme su bazirani na [GTK](/index.php/GTK "GTK") ili [Qt](/index.php/Qt "Qt") toolkit-ima. Vidi članke vezano za njih i [Uniform look for Qt and GTF applications](/index.php?title=Uniform_look_for_Qt_and_GTF_applications&action=edit&redlink=1 "Uniform look for Qt and GTF applications (page does not exist)") za ideje kako poboljšati izgled instaliranih programa i kako prilagoditi svom ukusu.

## Konzolna poboljšavanje

Ova sekcija se odnosi na male modifikacije koje mogu poboljšati konzolne programe. Za viši, vidi [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### Tab-completion enhancements

Preporučeno je pravilno podesiti [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"), kao što je navedeno u člancima vezano za shell-ove koji se koriste.

### Aliasi

Definiranje aliasa za komandu ili grupu komandi je jedan od načina uštede vremena na konzoli. Ovo je pogotovo od pomoći za repetitivne taskove koji ne zahtjevaju neku posebnu modifikaciju parametara između pokretanja. Česti aliasi koji štede vrijeme, mogu biti pronađeni na [Bash#Aliases](/index.php/Bash#Aliases "Bash"), koji su portabilni i na [zsh](/index.php/Zsh "Zsh").

### Alternativni shell-ovi

[Bash](/index.php/Bash "Bash") je shell koji je instaliran po defaultu. Live instalacijski mediji, koristi [zsh](/index.php/Zsh "Zsh") sa [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) addon paket. Vidi [Command-line shell#List of shells](/index.php/Command-line_shell#List_of_shells "Command-line shell") za više alternativa.

### Bash dodaci

Lista dodatnih Bash podešavanja, pretraživanja historije i [Readline](/index.php/Readline "Readline") makroi su dostupni u [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Obojeni output

Ova sekcija je pokrivena u [Color output u konzoli](/index.php?title=Color_output_u_konzoli&action=edit&redlink=1 "Color output u konzoli (page does not exist)").

### Kompresovani fajlovi

Kompresovani fajlovi ili arhive su česte na GNU/Linux sistemima. [Tar](/index.php/Tar "Tar") je jedan od najčešće korištenih alata za arhiviranje i korisnici bi trebali biti upoznati sa njegovom sintaksom (Arch Linux paketi su npr. jednostavno xzipovani tarball-i). Vidi [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression").

### Konzolni prompt

Konzolni prompt (PS1) može biti dosta customiziran. Vidi [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization") ili [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") u zavisnosti od shella koji koristiš.

### Emacs shell

Emacs je poznat po tome što ima feature mimo regularnog text editinga, jedan od toga je potpuni shell replacement. Vidi [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") za fix vezano za pokvareni izgled karaktera nakon enablanja kolornog outputa.

### Mouse podrška

Koristeći miš sa konzolom za copy-paste operacija može se preferirati u odnosu na [GNU Screen](/index.php/GNU_Screen "GNU Screen")-ov tradicionalni copy mode. Vidi [General purpose mouse](/index.php/General_purpose_mouse "General purpose mouse") za detaljne direkcije. Uzmi u obzir da ovo već možeš raditi u [terminal emulator](/index.php/Terminal_emulator "Terminal emulator")-u sa [clipboard](/index.php/Clipboard "Clipboard")-om.

### Scrollback buffer

Da bi se mogao spasiti i gledati tekst koji je odskrolan sa ekrana, vidi [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting").

### Session menadžment

Koristeći terminalne multipleksere poput [tmux](/index.php/Tmux "Tmux") ili [GNU screen](/index.php?title=GNU_screen&action=edit&redlink=1 "GNU screen (page does not exist)")-a, programi mogu se pokretati pod sesijama koji se sastoje od tabova i pane-ova koji se mogu otkačiti(detach) po želji, tako da kad program kill-a terminal ili [X](/index.php/X "X") ili se odjavi, programi mogu i dalje da rade u pozadini sve dok je multiplekser aktivan. Interakcija sa programom zahtjeva ponovno kačenje na njih.