## Contents

*   [1 Įžanga](#.C4.AE.C5.BEanga)
    *   [1.1 DON'T PANIC! (be panikos!)](#DON.27T_PANIC.21_.28be_panikos.21.29)
*   [2 Naujausių ISO parsisiuntimas](#Naujausi.C5.B3_ISO_parsisiuntimas)
*   [3 Bazinės dalies diegimas](#Bazin.C4.97s_dalies_diegimas)
    *   [3.1 Arch Linux CD įkrovimas](#Arch_Linux_CD_.C4.AFkrovimas)
    *   [3.2 Klaviatūros išdėstymo keitimas](#Klaviat.C5.ABros_i.C5.A1d.C4.97stymo_keitimas)
    *   [3.3 Diegimo pradžia](#Diegimo_prad.C5.BEia)
        *   [3.3.1 Pasirink instaliacijos šaltinį](#Pasirink_instaliacijos_.C5.A1altin.C4.AF)
        *   [3.3.2 HDD paruošimas](#HDD_paruo.C5.A1imas)
        *   [3.3.3 Bylų sistemų prijungimo taškų pasirinkimas (Set Filesystem Mountpoints)](#Byl.C5.B3_sistem.C5.B3_prijungimo_ta.C5.A1k.C5.B3_pasirinkimas_.28Set_Filesystem_Mountpoints.29)
    *   [3.4 Paketų pasirinkimas](#Paket.C5.B3_pasirinkimas)
    *   [3.5 Paketų diegimas](#Paket.C5.B3_diegimas)
    *   [3.6 Sistemos konfigūravimas](#Sistemos_konfig.C5.ABravimas)
    *   [3.7 Pradinio įkroviklio diegimas](#Pradinio_.C4.AFkroviklio_diegimas)
        *   [3.7.1 Windows nustatymai skirti GRUB](#Windows_nustatymai_skirti_GRUB)
*   [4 Bazinės sistemos konfigūravimas](#Bazin.C4.97s_sistemos_konfig.C5.ABravimas)
    *   [4.1 Pacman konfigūravimas](#Pacman_konfig.C5.ABravimas)
    *   [4.2 Tinklo konfigūravimas](#Tinklo_konfig.C5.ABravimas)
        *   [4.2.1 LAN](#LAN)
        *   [4.2.2 DHCP suderinimas](#DHCP_suderinimas)
        *   [4.2.3 WLAN](#WLAN)
        *   [4.2.4 ISDN](#ISDN)
        *   [4.2.5 DSL (PPPoE)](#DSL_.28PPPoE.29)
    *   [4.3 Atnaujinimas](#Atnaujinimas)
*   [5 Pridedame vartotoją (user)](#Pridedame_vartotoj.C4.85_.28user.29)
    *   [5.1 Grupių nustatymai](#Grupi.C5.B3_nustatymai)
*   [6 Aparatinės įrangos diegimas ir konfigūravimas](#Aparatin.C4.97s_.C4.AFrangos_diegimas_ir_konfig.C5.ABravimas)
    *   [6.1 Garso plokštė](#Garso_plok.C5.A1t.C4.97)
    *   [6.2 CPU dažnio mažinimas](#CPU_da.C5.BEnio_ma.C5.BEinimas)
    *   [6.3 Nešiojamiems kompiuteriams](#Ne.C5.A1iojamiems_kompiuteriams)
*   [7 Xorg instaliavimas ir konfigūravimas](#Xorg_instaliavimas_ir_konfig.C5.ABravimas)
    *   [7.1 Klaviatūros išdėstymo keitimas](#Klaviat.C5.ABros_i.C5.A1d.C4.97stymo_keitimas_2)
    *   [7.2 Raiškos keitimas](#Rai.C5.A1kos_keitimas)
    *   [7.3 Pelės derinimas](#Pel.C4.97s_derinimas)
    *   [7.4 Naudojam firminius draiverius (Nvidia, Ati)](#Naudojam_firminius_draiverius_.28Nvidia.2C_Ati.29)
        *   [7.4.1 Nvidia](#Nvidia)
        *   [7.4.2 ATI](#ATI)
*   [8 Grafinės aplinkos instaliavimas ir konfigūravimas](#Grafin.C4.97s_aplinkos_instaliavimas_ir_konfig.C5.ABravimas)
    *   [8.1 Šriftų instaliavimas](#.C5.A0rift.C5.B3_instaliavimas)
    *   [8.2 Gnome](#Gnome)
        *   [8.2.1 Apie Gnome](#Apie_Gnome)
        *   [8.2.2 Instaliavimas](#Instaliavimas)
        *   [8.2.3 pagražinimas](#pagra.C5.BEinimas)
    *   [8.3 KDE](#KDE)
        *   [8.3.1 Apie KDE](#Apie_KDE)
        *   [8.3.2 Instaliavimas](#Instaliavimas_2)
    *   [8.4 Xfce](#Xfce)
        *   [8.4.1 About Xfce](#About_Xfce)
        *   [8.4.2 Instaliavimas](#Instaliavimas_3)
    *   [8.5 *box](#.2Abox)
        *   [8.5.1 Fluxbox](#Fluxbox)
        *   [8.5.2 Openbox](#Openbox)
    *   [8.6 fvwm2](#fvwm2)
*   [9 Naudingos programos](#Naudingos_programos)
    *   [9.1 Internetas](#Internetas)
    *   [9.2 Biuras](#Biuras)
    *   [9.3 Bylų tvarkyklės](#Byl.C5.B3_tvarkykl.C4.97s)
*   [10 Multimedia](#Multimedia)
    *   [10.1 Video grotuvai](#Video_grotuvai)
        *   [10.1.1 VLC](#VLC)
        *   [10.1.2 Mplayer](#Mplayer)
        *   [10.1.3 Totem](#Totem)
        *   [10.1.4 Kaffeine](#Kaffeine)
    *   [10.2 Audio grotuvai](#Audio_grotuvai)
        *   [10.2.1 Skirti Gnome](#Skirti_Gnome)
        *   [10.2.2 Veikiantys konsolėje](#Veikiantys_konsol.C4.97je)
        *   [10.2.3 kiti veikiantys grafinėje aplinkoje](#kiti_veikiantys_grafin.C4.97je_aplinkoje)
        *   [10.2.4 Turintys galingas redagavimo funkcijas](#Turintys_galingas_redagavimo_funkcijas)
    *   [10.3 Kodekai ir kiti pagalbiniai dalykai](#Kodekai_ir_kiti_pagalbiniai_dalykai)
        *   [10.3.1 DVD](#DVD)
        *   [10.3.2 Flash](#Flash)
        *   [10.3.3 Quicktime](#Quicktime)
        *   [10.3.4 Realplayer](#Realplayer)
    *   [10.4 CD and DVD "kepimas"](#CD_and_DVD_.22kepimas.22)
    *   [10.5 Skaitmeninės kameros, naujausi telefonai grotuvai](#Skaitmenin.C4.97s_kameros.2C_naujausi_telefonai_grotuvai)
    *   [10.6 USB raktai](#USB_raktai)
    *   [10.7 Floppy(vis dar naudojama?)](#Floppy.28vis_dar_naudojama.3F.29)
*   [11 Sistemos priežiūra](#Sistemos_prie.C5.BEi.C5.ABra)
    *   [11.1 Pacman](#Pacman)
        *   [11.1.1 Naudingos komandos](#Naudingos_komandos)
*   [12 Tolesnė informacija](#Tolesn.C4.97_informacija)

## Įžanga

Šis tekstas padės įdiegti ir suderinti Arch Linux, net jeigu Linux matote pirmą kartą. Nors šitas gidas padeda suderinti pilnai parengtą sistemą (grafinė aplinka, DVD žiūrėjimas, puslapių naršymas, darbas su elektroniniu paštu, muzikos klausymas), tačiau neįmanoma parodyti visų galimybių ir nustatymų. Šitas gidas aprašo esminius, svarbiausius žingsnius; išmoksite daug daugiau, kai naudosi veikiančią sistemą, o jei iškils neaiškumų, galite klausti forumuose ar IRC.

##### DON'T PANIC! (be panikos!)

_Arch Linux_ instaliacija gerokai skiriasi nuo kitų bandytų Linux GNU/Linux distribucijų. Čia nėra jokios grafinio instaliavimo programėlės, kuri padarytų viską automatiškai (ką nori ir ko nenori), kol 20 minučių veiksite ką kita. Bet čia viskas yra jūsų rankose, ką ir kaip instaliuoti. Instaliacija susideda vien tik iš komandinės eilutės sąsajos (CLI) ir jos įrankių. Grafinę aplinką, jei norėsite, galėsite instaliuoti tik pabaigoje, bet net ir po to nebus jokių "control panel" ar panašių derinimo įrankių. Iš komandinės eilutės kuri nieko daugiau neturi, išskyrus tai kas būtina OS veikimui, jūs patys redaguosite nustatymų bylas su _nano_ ir instaliuosite programas su _pacman_ kol gausis tai ko norite, kas atitinka jūsų poreikius ir būsimą kompiuterio paskirtį. Tai užtikrina maksimalų lankstumą, valdymą ir patogumą vėliau. Ne paslaptis, kad tai kas tinka viskam, dažniausiai normaliai netinka niekam, būtent todėl Arch Linux tiek daug dėmesio skiria **specializacijai**. OS bus nuo pamatų pastatyta taip, kad atliktų tik tai ko jūs asmeniškai norite ir ko jums reikia.

Be to, patys viską pastatę, labai gerai žinosite, kaip pas jus viskas veikia. O žinojimas irgi ne mažiau gerai.

Arch principas yra _keep it simple_ (~ laikyk tai paprastai), kur _simple_ nereiškia nei lengva, nei daug visokių šokinėjančių lentelių kur tik _yes/no/cancel_ spaudyti reikia, o tai, kad nėra nieko nereikalingo. Arch tai elegantiškas ir minimalistinis požiūris. Arch tai jokiu būdu nėra keli DVD diskai pagal nutylėjimą suinstaliuojamų programų, kurių daugumos tu net pavadinimų niekad nesužinosi.

**Jei neseksite šiuo tekstu ar jo versijos kitomis kalbomis ir ypač jei dar neesate patyręs Linux naudotojas, tai vargu ar jums išvis kas nors gausis**

* * *

Welcome to Arch! Dabar pradėkim.

## Naujausių ISO parsisiuntimas

Tu gali visiškai nemokamai ir be jokių sąlygų parsisiųsti Arch Linux iš [čia](https://www.archlinux.org/download/).

## Bazinės dalies diegimas

Ši nuoroda [Installation guide](/index.php/Installation_guide "Installation guide") taip pat naudingas. To teksto spausdinimui skirta versija yra [čia](https://www.archlinux.org/static/docs/arch-install-guide.html).

### Arch Linux CD įkrovimas

Įdėkite CD į cdrom įrenginį ir užkraukite sistemą iš jo. Jums gali tekti pakeisti įkrovos (boot) tvarką BIOS sistemoje. Tam reikia spausti tam tikrą mygtuką vos tik įjungus kompiuterį. Dažniausiai tai F11 ar F12, be to, beveik visada rašo "press kažką to enter setup", tą kažką ir reikia spausti. Paskui reik surasti "boot order" parametrą ir cdrom padaryti kaip "primary".

Kai kurie įkrovos nustatymai:

*   ide-legacy jei turi problemų su IDE įrenginiais (būdinga LABAI seniems kompiuteriams)
*   noapic acpi=off pci=routeirq nosmp jei paprasčiausiai užstringa kitaip
*   memtest86+ atminties testas

Rinkis "Arch Linux Installation / Rescue System". Jei nori pakeisti įkrovos nustatymus spausk "e". Sistema dabar užsikraus ir parodys pasisveikinimo ekraną ir truputėlį naudingos informacijos.

### Klaviatūros išdėstymo keitimas

Spauskite "enter" pasveikinimo ekrane. Parašykite

```
km

```

komandinėje eilutėje ir susiraskite reikiamą išdėstymą. Dirbant konsolėje, patartina pasirinkti "default8x16.psfu.gz".

### Diegimo pradžia

Įrašome

```
/arch/setup 

```

paspaudžiame ENTER ir pradėsime diegimą.

#### Pasirink instaliacijos šaltinį

Jūsų paklaus, kokį instaliacijos šaltinį renkatės. Rinkitės CD, jei turite pilną dabartinį (current) ISO (tikriausiai tai ir yra, ko jums reikia) arba rinkitės ftp jei naudosite ftp ISO.

#### HDD paruošimas

Rinkitės pirmą meniu punktą "Prepare Hard Drive". Atsargiai! "Auto-Prepare" punktas suformatuoja visą diską!!! Mes viską darysim rankiniu būdu. Rinkitės "2\. Partition Hard Drives", po to pasirinkite norimą diską (/dev/sdx), ir sukurkite skirsnius.

Nėra jokio konkretaus būdo kokius skirsnius ir kaip daryti, kiekvienas turi savo mėgstamiausią konfigūraciją. Ko minimaliai mums reikia, tai "primary" skirsnio kuriame bus root bylų sistema. Dar galima sukurti /boot (kuriame sudėti branduoliai) ir /home (kuriame sudedami naudotojų duomenys ir bylos). Jei tokių skirsnių nekursite, tai tam vėliau bus tiesiog sukurti aplankai root skirsnyje. Mes čia darysime vieną / (root) ir vieną /home.

Bazinė informacija apie swap: Swap(mainų sritis) skirsnis yra tartum RAM padidinimas panaudojat HDD. Jei apkrausite sistemą taip, kad RAM bus užpildyta, tai baigsis klaidos pranešimu. Windows sistemoje tada pradedama kurti paslėpta milžiniška byla esanti tiesiog C:\ kataloge. Swap skirsnis Linux sistemoje yra patogesnis tos gremėzdiškos bylos variantas. Taip niekad nereikia rūpintis papildoma laisva vieta "normaliam darbui".

Kokio dydžio turi būti swap skirsnis? Nėra konkretaus atsakymo. Paprasčiausia tiesiog pasinaudoti plačiai žinoma formule: RAM (kiekis) x 2\. Bet jei labai gaila HDD vietos, galima ir mažiau. Kadangi HDD yra DAUG lėtesnis, nei RAM, išmintingiau įsigyti daugiau RAM, nei didinti swap skirsnį.

Metas kurti "primary" skirsnį, skirtą "root". Rinkitės New -> Primary ir įveskite tokį dydį kokio norite. Dydis nuo 4 ir 8 GB idealu, bet gali būti ir taip mažai kaip 200Mb (tokiu atveju tilps tik bazinė sistema, o papildomoms programoms neliks vietos) ir bet kiek daugiau. Tą skirsnį gerai būtų padėti į disko pradžią. Pasirinkite šį naują skirsnį ir uždėkite žymę "Bootable" tam, kad sistema krautųsi būtent iš šio skirsnio. Pridėk dar vieną skirsnį savo "home" aplankui. Jo dydis priklauso nuo to, ką dėsite į savo home aplanką (galbūt kompiuteryje laikysite DVD filmus, tada prisireiks daug gigabaitų, gal tik dokumentus, tada tai užteks ir mažiau 1 Gb. Jei kompiuteryje daugiau nėra jokių kitų operacinių sistemų, paprasčiausiai palikite home viską, kas liko po "root" ir "swap". Lygiai taip sukuriame "swap". Bylų sistemos tipas "Linux swap"

Tavo darbo rezultatas turėtų būti panašus į tai:

```
Name    Flags  Part Type   FS Type         [Label]         Size (MB)
-------------------------------------------------------------------------
sda1    Boot   Primary     Linux                           (4096 - 8192)
sda2           Primary     Linux                           (> 100)
sda3           Primary     Linux swap / Solaris            (512 - 1024)

```

Jei taip, rinkitės "write" ir spauskite "yes". Po to spauskite "Quit" ir "Done". Taip pereisite į kitą žingsnį "Set Filesystem Mountpoints"

#### Bylų sistemų prijungimo taškų pasirinkimas (Set Filesystem Mountpoints)

Pirmiausia būsite paklausti apie "swap", rinkitės savo "swap" (sda3 pavyzdyje). Jūsų paklaus ar norite sukurti "swap" bylų sistemą, spauskite "yes". Tada paklaus apie "root" tada vėl pasirinkite reikiamą skirsnį ir bylų sistemą "Ext3", nebent turite kažkokią rimtą priežastį rinktis kitokią.

Analogiškai elgiamės su "home", paskyrę jai visą likusį skirsnį ir "ext3" failų sistemą. Grįžtame į pagrindinį meniu.

### Paketų pasirinkimas

Dabar turime ką nors instaliuoti. Pasirinkite CD šaltinį. Mes instaliacijos metu neužsiiminėsime grafinių aplinkų ir biuro paketų diegimu, taigi nesirenkame dabar nieko daugiau nei pagrindas (base) (rinktis viską, kas yra "base" yra saugus pasirinkimas). Be abejo, niekaip negaliu priversti neįrašinėti daugiau nei "base", bet mes dabar užsiimam tiesiog sistemos įdiegimu ir tikriausiai labai skubame (kaip visada), o visa kita galėsime įrašyti ir bet kada vėliau.

### Paketų diegimas

Dabar galim eiti išsivirti kavos. Viskas vyksta automatiškai. Bet gali tekti paspausti "continue".

### Sistemos konfigūravimas

Jūsų paklaus ar norite panaudoti "hwdetect", kad gautume informacijos. Kadangi informacijos gavimas visad yra gerai, tai padarysime. Dabar jūsų paklaus ar norite palaikymo įvairiems dalykams. Rinkitės taip, jei to reikia. Jūsų paklaus ir kokį teksto redaktorių naudosite linksmiausioje instaliacijos dalyje. Rinkitės mėgstamiausią arba "nano". Dabar pateksite į meniu su esminėmis, tekstinėmis "config" bylomis. Jei norite pasižiūrėti galimus nustatymus rc.conf, spauskite Alt+F2, kad pereitumėte į komandinę eilutę, susirastumėte ko reikia ir grįžtumėte į diegimo seką paspausdami Alt+F1\. Redaguojame /etc/rc.conf:

*   Keičiame LOCALE, jei reikia (pvz. "lt_LT.utf8")
*   Keičiame TIMEZONE, jei reikia (pvz. "Europe/Vilnius")
*   Keičiame KEYMAP, jei reikia (pvz. "lt.baltic.map" arba "lt.map")
*   Keičiame CONSOLEFONT, jei norime matyti lietuviškas raides (pvz. "lat4-16", lietuviškas raides turi „lat4“ grupės šriftai)
*   Keičiame CONSOLEMAP, jei reikia lietuviškų raidžių (keičiame į "8859-4", būtent tai grupei priklauso Lietuvių kalba)
*   Keičiame MODULES jei žinome, kokio trūksta
*   Keičiame HOSTNAME
*   Keičiame tinklo nustatymus "network settings":
    *   Nekeičiame lo eilutės
    *   Keičiame IP address, netmask and broadcast address jei turite statinį ip
    *   Keičiame eth0="dhcp" jei turite maršrutizatorių (angl. router), kuris skiria jums ip
    *   Jei turite statinį IP, nustatykite "gateway address" į maršrutizatorių (angl. router) ir pašalinkite "!" iš ROUTES punkto pradžios.

Kol kas nereikia keisti [daemons](/index.php/Daemons "Daemons") eilutės, bet gal paaiškinsime, kas "daemons" - "demonai" yra, nes su jais anksčiau ar vėliau visvien teks susidurti. Demonas yra programa, tyliai laukianti, kol kas nors nutiks ir reaguodama į įvykius siūlo paslaugas. Interneto puslapio serveris tai geras demono pavyzdys. Nors jie ir yra pilnavertės programos, tačiau jų darbas nematomas tiesiogiai, o tik rezultatas: sistemos žurnalai, cpu dažnio sumažinimas kai sistema neapkrauta...

Paspaudę Ctrl+X išeiname iš redaktoriaus. Sistema paklaus ar norite išsaugoti pakeitimus. Pasirinkite "yes".

Dabar redaguosime /etc/hosts:

*   Pridėkite "hostname" (tą patį kaip rc.conf) po localhost
*   Jei naudojate statinį ip, sukurkite naują eilutę <static-ip> hostname.domainname hostname

Mums nereikia redaguoti /etc/fstab, mkinitcpio.conf ir modprobe.con dabar ([fstab](/index.php/Fstab "Fstab") tvarko bylų sistemas, mkinitcpio derina ramdiską (skirta tokiems dalykams kaip RAID) ir modprobe gali būti panaudotas modulių nustatymui.

Jei nustatote statinį IP, įveskite DNS serverį į /etc/[resolv.conf](/index.php/Resolv.conf "Resolv.conf") (nameserver <ip-address>)

Dabar redaguosime /etc/locale.gen ir pasirinksime lokalizacijas (pašalinkite # iš norimos eilutės pradžios). Galiausiai nustatome "root" slaptažodį. Grįžtame į pagrindinį meniu ir tada įdiegsime branduolį.

### Pradinio įkroviklio diegimas

Kad paleistume mūsų ArchLinux iš hdd, mums prireiks pradinio įkėliklio (bootmanager). GRUB yra geras pasirinkimas ir su juo viską daryti yra kiek paprasčiau nei su kitu įkėlikliu LILO. Duota pradinė konfigūracinė byla (menu.lst) turėtų būti saugus pasirinkimas. Jums tik reikėtų pakeisti raišką. Pridėkite vga=<number> prie pirmos branduolio eilutės, bet tai nėra būtina. Skaičių ir juos atitinkančių raiškų lentelė yra parašyta menu.lst komentaruose. Jei dar ko nors reikia, pakeiskite ir tai. Pavyzdžiui, teksto ir fono spalvas, bet galėsite tai padaryti ir vėliau. Dabar jau išeikite iš instaliacijos ir surinkite: reboot. Jei viskas eisis gerai, netrukus atsidursite prisijungimo lange į savo naujai įdiegtą Archlinux. Jei ne, BIOS'e pakeiskite krovimosi tvarką - hdd pirmiausiai.

#### Windows nustatymai skirti GRUB

Jei dar su tuo pačiu _GRUB_ norėsite leisti ir _Windows_ sistemą, tai _menu.lst_ byloje nutrinkite "#" visus ženklus pastraipoje apie _Windows_. Tada su

```
fdisk -l

```

Pažiūrėkite, kuriame skirsnyje yra _Windows_. Tarkim, tai /dev/sd**a1**. Tada žiūrime į eilutę:
rootnoverify (hd**0,0**)
Jei raidė a, tai toje eilutėje pirmas skaičius turi būti 0, jei b tai 1\.
Jei po to eina skaičius 1, tai toje eilutėje turi būti 0, jei 2 tai toje eilutėje 1 ir t.t.
Dažniausiai pasitaiko standartinis variantas "0,0", bet jei daug kaitaliojote, gali būti ir kitaip.
Jei nesigauna, galite paeksperimentuoti su kitais skaičiais, jei skaičiai blogi _GRUB_ tiesiog nesugebės rasti kur tie _Windows_.

## Bazinės sistemos konfigūravimas

Dabar parodysiu kaip galima šį bei tą pakeisti. Prisiregistruok į savo naują sistemą su root vartotoju.

### Pacman konfigūravimas

Redaguok /etc/pacman.conf

```
nano -w /etc/pacman.conf

```

Ir pašalink # (komentaro simbolį kuris reiškia, kad ta eilutė nėra naudojama ji tik komentaras arba priminimas) iš eilutės "Include = /etc/pacman.d/community"-ir tada galėsi naudoti bendruomenės paketus. Dabar su tekstiniu redaktoriumi atverk failą /etc/pacman.d/mirrorlist ir atkomentuok(nuimk # nuo eilutės pradžios) veidrodžius kurie netoli Lietuvos(arba tos šalies kurioje gyveni). Lietuva oficialaus veidrodžio neturi, bet yra neoficialus. Jei nori naudoti neoficialų, failo pradžioj įrašyk _Server = [http://edacval.homelinux.org/mirrors/archlinux/$repo/os/$arch](http://edacval.homelinux.org/mirrors/archlinux/$repo/os/$arch)_. Nuo 4 pacman versijos, visi paketai yra pasirašyti pgp raktu, tai dėl saugumo neverta sukt galvos, nes jei parašas tinkamas nesvarbu iš kur tu paėmei tą paketą. Jei naudoji _nano_ tai Alt+A pradeda žymėti tekstą, rodyklė žemyn pažymi eilutes, Ctrl+K atkerpa pažymėtą vietą, o Ctrl+U atkuria pažymėtą vietą.

### Tinklo konfigūravimas

Išsamesnes instrukcijas anglų kalba rasi [čia](/index.php/Network "Network")

#### LAN

Paprastai tai nieko tokiu atveju nereikia turėtų viskas veikti. Bandyk komandą _ping www.google.lt_ tam, kad tai patikrintum. Jei gauni "unknown host" klaidą, tavo tinklas tada dėja neveikia. Pažiūrėk su komanda:

```
_ifconfig_

```

tu turėtum matyti pastraipą skirtą _eth0_. Tu gali priskirti IP su komanda:

```
_ifconfig eth0 <ip address> netmask <netmask> up_

```

ir "default gateway" su

```
# ip route add default via <ip address of the gateway>

```

Patikrink ar į /etc/resolv.conf įvestas tavo DNS serveris ir įvesk jei ten jo nėra. Vėl mėgink ar veikia internetas su

```
ping www.google.lt

```

#### DHCP suderinimas

Jei tu turi _dhcp_ serverį/maršrutizatorių savo tinkle mėgink

```
_dhcpcd eth0_

```

Jei tai padeda ir internetas pradėjo veikti, suderink /etc/rc.conf

```
 nano /etc/rc.conf 

```

Ir žemiau _lo="lo 127.0.0.1"_ pridėk dar vieną naują eilutę _eth0="dhcp"_. Jei jau _eth0=kažkam_ yra tai pašalink tau netinkamą vertę. Tada daugiau anksčiau minėtos komandos vesti nereiks tam, kad įjungtum internetą.

#### WLAN

Žiūrėk [Wireless Setup čia](/index.php/Wireless_Setup "Wireless Setup")

#### ISDN

Kas nors tokį turi Lietuvoje!? Tikriausiai ne.

#### DSL (PPPoE)

Labai gerai jei turite modemą-maršrutizatorių kuris pilnai valdomas per interneto naršyklę (net neduota jokių tvarkyklių diskų su juo). Tokiu atveju internetas tikriausiai jau veikia. Jei ne žiūrėkit skiltį apie _dhcp_. Jei jums dar reikia suderinti tą maršrutizatorių tai galite pasinaudoti naršykle _links_

```
links

```

Toliau vadovaukitės įrenginio instrukcija.

Jei naudojat paprastą modemą tada pridėkit savo kortą kuri jungiasi su DSL modemu/maršrutizatorium prie modules.conf/modprobe.conf arba į MODULES skiltį čia

```
nano /etc/rc.conf

```

Instaliuokite _rp-pppoe_ ir paleiskite pppoe-setup scenarijų

```
rp-pppoe

```

tam, kad suderintumėte savo interneto nustatymus. Tada prisijunkite su:

```
/etc/rc.d/adsl start

```

ir atsijunkite su:

```
/etc/rc.d/adsl stop

```

Jei norite prisijungti vos tik įjungus kompiuterį tai pridėkite adsl prie savo demonų (DAEMONS) čia

```
nano /etc/rc.conf

```

### Atnaujinimas

dabar mes atsinaujinsim su _pacman_. Tai _Arch Linux_ paketų valdymo programa. Ji skirta instaliuoti ar ištrinti paketus (paketai ~= programos). Pirmiausia geriau įsitikinti ar tikrai internetas jau veikia, tai galima padaryti įvedus komandą:

```
ping google.lt

```

Jei gaunate atsakymą "64 bytes from..." vadinasi jūsų internetas veikia gerai ir tada galite naudotis _pacman_ paketų tvarkykle. Paspauskite ctrl+c tam kad išjungtumėte _ping_. Veskite:

```
pacman -Syu

```

_Pacman_ dabar iš interneto surinks informaciją apie naujausius paketus. Kai matysite mirksintį ženkliuką "_" tai spauskite _y_ ir enter. Jei _Pacman_ atnaujino tik pats save tai dar kartą pakartokite:

```
pacman -Syu 

```

Ar tiesiog rodyklė į viršų ir enter.

## Pridedame vartotoją (user)

Taip kaip Windows'uose viską daryti su administratoriumi (root) Linux'uose yra mažiausiai nekultūringa. Be to nesaugu. Taigi sukuriam eilinį naudotoją su komanda:

```
adduser

```

Viskas toliau paprasta tiesiog reikia atsakyti į klausimus arba tiesiog spaudyti enter. Įdomesni punktai tai priskirti grupei "Audio" kuri leidžia naudoti garso plokštę ir "video" kuri leidžia naudoti vaizdo plokštės nustatymus.

### Grupių nustatymai

Kiekvienas vartotojas *nix tipo sistemose priskiriamas grupems pagal tai ką jis gali daryti. Taip realizuojamas aukšto lygio saugumas. Tarkim ne kiekvienas gali spauzdinti ir taip švaistyti dažus. Administratoriaus pareiga kiekvienam vartotojui priskirti tinkamas grupes. Grupei priskiriama taip:

```
usermod -aG [grupė] [naudotojas] 

```

Visų grupų sąrašas yra byloje:

```
/etc/group

```

Norint sužinoti kuriai grupei jūs priklausote galite naudoti komandą:

```
groups

```

Čia pateiksiu svarbiausių grupių sąrašą:

*   disk - gali tvarkyti atjungiamus diskus
*   storage - gali tvarkyti kietuosius diskus
*   video - gali keisti vaizdo parametrus
*   optical - gali tvarkyti optinius diskus
*   floppy - gali naudoti magnetinius diskelius (jei jie išvis yra)
*   camera - gali naudoti kameras
*   scanner - gali naudoti skenerius
*   lp - gali naudoti spausdintuvą

## Aparatinės įrangos diegimas ir konfigūravimas

### Garso plokštė

Tavo garso plokštė yra išjungta. Tam, kad ją ijungtum instaliuok alsa-utils

```
pacman -S alsa-utils alsa-lib alsa-oss

```

ir naudok alsamixer (įvesdamas komandą _alsamixer_) tam, kad suderintum kanalus. Įjunk bent jau "master" ir "pcm" kanalus (spausk M) ir padidink garsą su rodykle į viršų. Išeik su ESC ir įvesk komandą _alsactl store_ tam, kad išsaugotum nustatymus. Pridėk _alsa_ prie savo demonų /etc/rc.conf byloje ( DAEMONS=(syslog-ng network ... alsa ) ) ir tada vos tik kompiuteriui įsijungus garsas bus valdomas ir nereiks daugiau vesti komandų.

### CPU dažnio mažinimas

Nauji CPU gali sumažinti savo dažnį ir darbinę įtampą ir taip taupyti energiją ir mažinti triukšmą. Tam kad tai būtų realizuota mūsų sistemoje įrašom:

```
pacman -S cpufrequtils

```

ir pridedam _cpufreq_ prie demonų /etc/rc.conf. Redaguojam nustatymų bylą /etc/conf.d/cpufreq ir keičiam:

```
governor="conservative"

```

Taip CPU dažnis automatiškai padidinamas tada kai to reikia. Suderinam min_freq ir max_freq taip, kad atitiktų CPU techninius duomenis. Pridedam modulius prie /etc/rc.conf modulių eilutės (pvz.: speedstep_centrino jei turim Pentium M procesorių arba powernow-k8 jei turim Athlon 64). Užkraunam modulį su:

```
modprobe <modulname> 

```

Ir paleidžiam _cpufreq_ su:

```
/etc/rc.d/cpufreq start

```

### Nešiojamiems kompiuteriams

ACPI gali praversti jei ketini naudoti tokias funkcijas kaip "sleep" ir pan. Taigi instaliuojam acpid:

```
pacman -S acpid

```

ir pridedam jį prie demonų /etc/rc.conf (acpid). Paleidžiam su:

```
/etc/rc.d/acpid start

```

Dar gera mintis yra instaliuoti _powersave_ ir priedėti prie demonų byloje /etc/rc.conf (powersaved). Paleidžiam jį su:

```
/etc/rc.d/powersaved start

```

Daugiau informacijos šia tema, anglų kalba [čia](/index.php/Category:Laptops "Category:Laptops")

## Xorg instaliavimas ir konfigūravimas

Dabar instaliuosim Xorg. Jo mums reiks jei norėsim grafinės aplinkos. Rašom matyt jau žinot ką jei skaitot iš eilės:

```
pacman -S xorg xorg-server

```

ir įvedam Y. Dabar turim pagrindą kurio reikia norint paleisti X Serverį. Dabar tau reiktų dar ir vaizdo plokštės draiverių (kurie gaunami taip xf86-video-<name>). jei nori sužinot koks pasirinkimas tai:

```
pacman -Ss xf86-video | less

```

Jei nežinai kokia pas tave vaizdo plokštė tai gali sužinoti taip:

```
lspci | grep VGA

```

Dabar vesk Xorg -configure ir sukursi savo pradinę X konfigūraciją. jei nori ją išmėginti instaliuok _xterm_ ir _twm_ su:

```
pacman -S xterm xorg-twm

```

Perkelk xorg.conf.new (mv /root/xorg.conf.new /etc/X11/xorg.conf) ir spausk startx. kai jau norėsi išeiti tai: Ctrl+Alt+Backspace. Tada galbūt norėsi šį bei ta pakeisti savo xorg.conf byloje.

Dėmesio! Nuo 7.3 versijos Xorg automatiškai suranda jūsų įrenginius todėl konfigūruoti xorg.conf jums nebereikės. jei vis dėl to iškilo problemų, skaitykite toliau.

Išsamiais instrukcijas anglų kalba gali rasti [čia](/index.php/Xorg "Xorg")

### Klaviatūros išdėstymo keitimas

Tu tikriausiai norėsi pakeisti klaviatūros išdėstymą. Jei nori tai padaryti redaguok savo /etc/X11/xorg.conf ir pridėk tokias eilutes į _Section "InputDevice"_. Pirma nurodo, kad naudosim JAV ir Lietuvišką raidžių išdėstymą, o antra, kad išdėstymus keisim paspaudimu _alt+shift_ mygtukų.

```
       Option          "XkbLayout"     "us,lt"
       Option          "XkbOptions"    "grp:alt_shift_toggle"

```

### Raiškos keitimas

Raiška nurodoma taip

```
       SubSection     "Display"
            Depth       8
            Modes      "1024x768"
       EndSubSection

```

### Pelės derinimas

Jei ratukas neveikia ir nori, kad veiktų pridėk tai į (mouse0):

```
       Option      "ZAxisMapping" "4 5 6 7"

```

### Naudojam firminius draiverius (Nvidia, Ati)

#### Nvidia

Instaliuojam su:

```
pacman -S nvidia

```

Redaguojam /etc/X11/xorg.conf įrangos skiltį pakeisdami "nv" į "nvidia". O jei jum reik DRI dar įvedat tai:

```
Section "DRI"
       Mode    0666
EndSection

```

Dar kai kurie naudingi arba gal neveikiantys pakeitimai kuriuos galit išmėgint jei neturit ką veikt:

```
       Option          "RenderAccel" "true"
       Option          "NoLogo" "true"
       Option          "AGPFastWrite" "true"
       Option          "EnablePageFlip" "true"

```

Tai pridedama į modulių skiltį:

```
Load "glx"

```

Įvesk '_modprobe nvidia_ tam, kad įjungtum draiverius ir išmėgink savo darbo rezultatą su _startx_.

Išsamios intrukcijos anglų kalba [čia](/index.php/How_to_install_NVIDIA_driver "How to install NVIDIA driver")

#### ATI

ATI savininkai gali rinkis iš dviejų. Kuris geriau? - atviro kodo, kadangi jis yra geriau palaikomas naujausia programine įranga ir technologijomis.

Uždarojo kodo valdyklės (fglrx) Arch linux jau nebepalaiko, dėl to jums teks instaliuoti valdykles per AUR.

Instaliuojame atvirojo kodo valdykles:

```
pacman -S xf86-video-ati

```

## Grafinės aplinkos instaliavimas ir konfigūravimas

Pasirinkti grafinę aplinką yra labai sunku nes tikrai yra iš ko rinktis. Jei neturi jokio supratimo apie jas, tai esminiai punktai pagal kuriuos gali rinktis:

*   Jei nori darbastalio su gausybe funkcijų ir grafinių pagražinimų ir kažko tokio kaip Windows, KDE tau patiks.
*   Jei nori darbastalio su gausybe funkcijų ir grafinių pagražinimų, bet labiau orginalaus tai tau turėtų patikti GNOME.
*   Jei nori greitesnio darbastalio kuris mažai apkrauna kompiuterį, bet turi daug funkcijų tai xfce4.
*   Jei lengvumas, greitis, paprastumas, galimybė keisti ir valdyti viską tau svarbi tai Openbox, Fluxbox ar Fvwm2\. Tai derinasi su bendra Archlinux idėja, bet tai nereiškia, kad būtinai turi rinktis tai.
*   Jei nori kažko labai neįprasto ir atrodančio netikėtai, bet kartu greito ir lengvo rinkis Ion, Wmii arba Dwm.

### Šriftų instaliavimas

```
pacman -S ttf-ms-fonts ttf-dejavu ttf-bitstream-vera

```

### Gnome

#### Apie Gnome

GNOME tai du dalykai. Visų pirma tai grafinė aplinka ir antra GNOME kūrimo platforma su kuria galima integruoti programas į darbastalį. Jei turite P4 ir 256 Mb RAM ar galingesnį kompiuterį tai GNOME tikriausiai ir yra ta grafinė aplinka kurios jums reikia. Tai labiausiai išbaigta tiek grafiniu tiek patogumo požiūriu aplinka. Ir kartu ji siūlo iškirtinumą būdama palyginus mažai panaši į windows darbastalį. Minusas tai gan dideli sisteminiai reikalavimai.

#### Instaliavimas

Įvedam:

```
pacman -S gnome

```

Arba jei norim su visokiais priedais tai galim:

```
pacman -S gnome-extra

```

Geriausia rinktis viską. Dar galbūt norėsite vos tik įjungę kompiuterį neatsidurti konsolėje tokiu atvėju jums reik _gdm_. instaliuojam jį:

```
pacman -S gdm

```

Išbandom su:

```
/etc/rc.d/gdm start

```

Jei viskas veikia pridėk jį prie demonų į /etc/rc.conf.

Tau dar reiks redaktoriaus ir terminalo veikiančio GNOME aplinkoje:

```
pacman -S geany gnome-terminal

```

Išsamios instrukcijos anglų kalba [čia](/index.php/Gnome "Gnome")

#### pagražinimas

Jei GNOME neatrodo labai gražiai reik temų (skinų). Pvz.:

```
pacman -S gtk-engine-murrine

```

Ir aktyvuok ją per: System->Preferences->Theme. Daugiau temų ir visko ko reikia pagražinimui gali rasti [čia](http://www.gnome-look.org)

### KDE

#### Apie KDE

KDE tai dar viena grafinė aplinka. Ji kitokia nei GNOME, bet turi tą patį minusą: reiklumą sistemai. Jei nepatiko GNOME, galima tada ir KDE išmėginti.

#### Instaliavimas

```
pacman -S kde

```

Pasirenkam viską. KDM (Alternatyva GDM) yra kdemod-kdebase pakete. Išbandom jį su:

```
/etc/rc.d/kdm start

```

Ir jei veikia pridedam prie demonų, kaip visad /etc/rc.conf.

Daugiau informacijos anglų kalba [čia](/index.php/KDE "KDE").

### Xfce

#### About Xfce

Xfce puikiai tiks senesniems kompiuteriams - ji paprasta ir greita. Kartu turi daugybę funkcijų ir funkcionalumu nuo GNOME ar KDE beveik neatsilieka.

#### Instaliavimas

```
pacman -S xfce4 xfce4-goodies 

```

Dar gali praversti _gdm_ (žr. GNOME ir jį reik instaliuoti pirmiau) tada xfce atsiras kaip nauja sesija. Arba tiesiog komanda paleidimui iš konsolės:

```
startxfce4

```

Išsamios instrukcijos anglų kalba [čia](/index.php/Xfce "Xfce")

### *box

#### Fluxbox

Tai itin greitas, lengvas, mažai sistemą apkraunantis ir paprastai konfigūruojamas darbastalis su patogiu meniu, iššaukiamu dešiniu pelės paspaudimu, kurį nesunku keisti pagal savo poreikius. Kartu galima keisti stilius kurių yra daugybė.

Instaliuojam:

```
pacman -S fluxbox fluxconf menumaker

```

Jei naudoji gdm/kdm fluxbox sesija turėtų ten automatiškai atsirasti. Arba redaguojam ~/.xinitrc (kaip naudotojas) į:

```
exec startfluxbox 

```

tam kar įkeltume fluxbox į savo startx komandą.

Daugiau informacijos anglų kalba [čia](/index.php/Fluxbox "Fluxbox")

#### Openbox

Openbox Dar vienas iš *box serijos. Su tais pačiais privalumais. Instaliuojam su:

```
pacman -S openbox obconf menumaker

```

Po instaliacijos gausim žinutę perkelti tam tikras bylas taip ir padarom:

```
mkdir -p ~/.config/openbox/
cp /etc/xdg/openbox/rc.xml ~/.config/openbox/
cp /etc/xdg/openbox/menu.xml ~/.config/openbox/

```

Byloje "rc.xml" yra nustatymai (arba gali naudoti OBconf). "menu.xml" Gali keisti meniu.

Redaguojam ~/.xinitrc (as user) į:

```
exec openbox 

```

tam kar įkeltume openbox į savo startx komandą.

Jei norite, kad su openbox kartu startuotų ir autostart.sh skriptas, vietoj exec openbox, į ~/.xinitrc įrašykite:

```
openbox-session

```

Naudingos programos:

*   pyPanel
*   feh
*   Rox

Daugiau informacijos anglų kalba [čia](/index.php/Openbox "Openbox")

### fvwm2

Fvwm2 - tai labai greitas ir turintis dideles konfigūravimo galimybes darbastalis (Window Manager). Labiau skirtas pažengusiesiems. Instaliuojama su šia komanda:

```
pacman -S fvwm 

```

fvwm bus automatiškai pridėtas prie kdm/gdm sesijų. Kitu atveju įrašome į savo naudotojo .xinitrc (~/.xinitrc) šią komandą:

```
exec fvwm

```

## Naudingos programos

Čia apžvelgsime keletą naudingų programų kurios praverčia kasdien.

### Internetas

Firefox ir Thunderbird yra geros programos interneto naršymui ir elektroninio pašto tvarkymui. Jei naudoji GNOME tai epiphany ir evolution, o jei KDE konqueror ir kmail gali rinktis. Jei nori gali naudoti Opera ir įvairias tekstines naršymo programas, kaip pavyzdžiui links kuri veikia ir tiesiai iš konsolės. Pidgin (seniau vadinosi Gaim) ir Kopete tai yra žinučių programos geros (messengeriai).

### Biuras

Openoffice yra pilnas programų rinkinys biurui (panašus į Microsoft Office).

```
pacman -S openoffice-base

```

LibreOffice yra pilnas programų rinkinys biurui (panašus į Microsoft Office). Tai yra atšaka(fork) atskilusi nuo openoffice. Tai yra numatytasis biuro programų paketas tokiuose distributyvuose kaip Fedora, Linux Mint, openSUSE ir Ubuntu.

```
pacman -S libreoffice 

```

Abiword yra geras sumažintas variantas jei nesiruošiate dirbti su ofisu daug, bet visgi norėsite atidaryti jo bylas, arba turite intin seną kompiuterį, gnumeric tai dar viena programa panaši į MS Exel. KOffice yra dar vienas biuro programų rinkinys skirtas KDE. Gimp tai paveikslėlių redaktorius panašus į Adobe Photoshop. Inkscape irgi gali būti naudinga dirbant su grafika. Ir dar arch linux turi visą rinkinį LaTeX-Programms.

### Bylų tvarkyklės

Tikriausiai norėsite turėti bylų tvarkymo įrankį su windows stiliaus "folderiais", šiukšliadėže ir pan. Tai galite naudoti XFE, jis labai primena MS-Explorer ir windows naudotojai jausis kaip namie. Dar galite naudoti EmelFM jis kiek primena DOS skirtą Norton Commander, bet atsisakyta to mėlynos lentelės stiliaus. Kiti:

*   FDclone - veikia ir terminale
*   Midnight Commander - norton comander klonas
*   FileRunner
*   Gentoo - niekaip nesusijęs su Linux distribucija tuo pat vardu
*   GNOME Commander
*   Krusader - skirtas KDE
*   Worker
*   Desktop File Manager
*   TKDesk
*   ROX-Filer

## Multimedia

### Video grotuvai

#### VLC

VLC Player yra daugialypės terpės grotuvas skirtas Linux sistemoms. Paskutiniu metu jis populiarėja ir windows sistemose.

```
pacman -S vlc

```

#### Mplayer

MPlayer yra dar vienas daugialypės terpės grotuvas skirtas Linux sistemai. Jei nori instaliuoti jį:

```
pacman -S mplayer

```

Daugumai žmonių turbūt yra priimtiniau naudot mplayer su grafine sąsaja, viena iš geriausių mplayer grafinių sąsajų(frontend) yra smplayer.

```
pacman -S smplayer

```

Jis dar turi priedą leidžiantį žiūrėti bylas per interneto naršyklę. Jei nori tą priedą instaliuoti tai:

```
pacman -S mplayer-plugin

```

Be to mplayer veikia ir tiesiai iš konsolės, todėl jį gali rinktis jei neketini naudoti grafinės aplinkos, bet visgi norėsi tarkim leisti mp3 bylas.

#### Totem

Daugiausia filmams žiūrėti skirtas grotuvas.

```
pacman -S totem

```

#### Kaffeine

Dar vienas grotuvas skirtas KDE. Instaliuojam jį taip:

```
pacman -S kaffeine

```

### Audio grotuvai

#### Skirti Gnome

Banshee, Quodlibet, Exaile, Rhythmbox, Listen: tavo laisvė rinktis.

#### Veikiantys konsolėje

Moc ir mpd.

#### kiti veikiantys grafinėje aplinkoje

Xmms, audacious, bmpx.

#### Turintys galingas redagavimo funkcijas

Audacity

### Kodekai ir kiti pagalbiniai dalykai

#### DVD

gali naudoti totem-xine, mplayer arba kaffeine jei nori =i8r4ti dvd. Tau dar reiks libdvdcss kuris nėra labai legalus, bet kam tai rūpi.

#### Flash

Jei nori matyti flash animacijas tai:

```
pacman -S flashplugin

```

#### Quicktime

Quicktime ir kiti kodekai:

```
pacman -S codecs

```

#### Realplayer

Realplayer 10 gali gauti iš [čia](https://aur.archlinux.org/packages.php?do_Details=1&ID=1590&O=0&L=0&C=0&K=realplay&SB=&SO=&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd)

### CD and DVD "kepimas"

Brasero, k3b, cdrecord, graveman ir kitos programos gali būti tam panaudotos.

### Skaitmeninės kameros, naujausi telefonai grotuvai

Dauguma tokių įrenginių gali veikti USB rato principu. Jei taip yra tai nieko daryti nereikia tiesiog prijungiam įrenginį ir atliekam reikiamas operacijas su bylomis. Kai kurios senos kameros naudoja _ptp_ (Picture Transfer Protocol) kuriam reikia specialios programinės įrangos Gphoto2 leidžia turėti tokią įrangą konsolėje. Digikam tai suteikia KDE aplinkai. Gthumb ir gtkam leidžia naudoti tokią įrangą be to turi patogią grafinę sąsają. Į Creative kurtus grotuvus (Zen, zen micro, zen photo, jukebox...) galima įkelti dainas su Gnomad įrankiu.

### USB raktai

USB raktai veikia be jokių papildomų derinimų ir atsiranda kaip naujas įrenginys (/dev/sdX). Jei naudoji KDE arba Gnome tu gali naudoti dbus ir hal (pridėdamas juos prie demonų byloje /etc/rc.conf) ir tuomet raktas bus automatiškai prijungiamas, nereikės įvesti komandos mount. Kitoms grafinėsms aplinkoms gali padėti ivman.

### Floppy(vis dar naudojama?)

Manau pastebėjote, jog kraunantis HAL, nepasikrauna "flopikų" įrenginys. Visko ko jums reiks tai įdėti reikiamą modulį į /etc/rc.conf

Atsidarome /etc/rc.conf root teisėmis su patinkama naršykle(nano, kwrite, gedit ir t.t.)

Modules gale prirašome eilutę:

```
MODULES=(....floppy....)

```

Jei naudojate savo flopiką retai, tiesiog, kada jį naudosite, konsolėje rašykite šią komandą(modprobe floppy) ir į atmintį bus įkeltas reikalingas modulis.

## Sistemos priežiūra

### Pacman

[Pacman](/index.php/Pacman "Pacman") yra paketų valdymo programa kuri gali parsiųsti instaliuoti ir atnaujinti paketus, sutvarkyti jų priklausomybės klausimus. Taip pat su pagalbiniais įrankiais nesunku sukurti savo paketus skirtus pacman. Tuos paketus galima įdėti į [AUR](/index.php/AUR "AUR") ([https://aur.archlinux.org/](https://aur.archlinux.org/)) ir taip nesunkiai pasidalinti su visais.

Išsamus pacman aprašymas anglų kalba [čia](/index.php/Pacman "Pacman").

#### Naudingos komandos

Norint sulyginti turimus paketus su naujausiais vedam (tai reikėtų padaryti kiekvieną kart prieš ką nors instaliuojant arba norint atnaujinti sistemą):

```
pacman -Sy

```

Norint instaliuoti vieną ar kelis paketus vedam (instaliuoja ir nuo jų priklausomus paketus):

```
pacman -S paketasA paketasB

```

Norint pašalinti paketą ir palikti visus nuo jo priklausomus paketus vedam:

```
pacman -R paketas

```

Norint pašalinti paketą ir visus nuo jo priklausomus paketus kurie nepriklausomi nuo daugiau jokių paketų vedam:

```
pacman -Rs paketas

```

Norėdami atnaujinti sistemą vedam:

```
pacman -Su

```

Norėdami ieškoti tam tikro paketo duomenų bazėje vedame:

```
pacman -Ss paieškos_žodis

```

## Tolesnė informacija

Daugiau informacijos galite rasti [namų puslapis](https://www.archlinux.org), [wiki](/index.php/Main_Page_(Lietuvi%C5%A1kai) "Main Page (Lietuviškai)"), [forumas](https://bbs.archlinux.org), [IRC](/index.php/ArchChannel "ArchChannel") ar [pašto sąrašas](https://www.archlinux.org/mailman/listinfo/).