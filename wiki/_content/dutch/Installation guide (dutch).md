## Contents

*   [1 Introductie](#Introductie)
    *   [1.1 Wat is Arch Linux?](#Wat_is_Arch_Linux.3F)
    *   [1.2 Licentie](#Licentie)
*   [2 Arch Linux installeren](#Arch_Linux_installeren)
    *   [2.1 Alvorens te installeren](#Alvorens_te_installeren)
    *   [2.2 Arch Linux verkrijgen](#Arch_Linux_verkrijgen)
    *   [2.3 Installatie-media voorbereiden](#Installatie-media_voorbereiden)
    *   [2.4 Installatiemedia gebruiken](#Installatiemedia_gebruiken)
    *   [2.5 Algemene installatie procedure](#Algemene_installatie_procedure)
        *   [2.5.1 Inloggen en een niet-US keymap laden](#Inloggen_en_een_niet-US_keymap_laden)
        *   [2.5.2 Setup uitvoeren](#Setup_uitvoeren)
        *   [2.5.3 Bron selecteren](#Bron_selecteren)
            *   [2.5.3.1 CD-ROM of OTHER SOURCE](#CD-ROM_of_OTHER_SOURCE)
            *   [2.5.3.2 FTP/HTTP](#FTP.2FHTTP)
                *   [2.5.3.2.1 Netwerk configureren](#Netwerk_configureren)
                *   [2.5.3.2.2 Spiegelserver kiezen](#Spiegelserver_kiezen)
        *   [2.5.4 Klok instellen](#Klok_instellen)
        *   [2.5.5 Hardeschijf voorbereiden](#Hardeschijf_voorbereiden)
            *   [2.5.5.1 Automatisch partitioneren](#Automatisch_partitioneren)
            *   [2.5.5.2 Hardeschijf partitioneren](#Hardeschijf_partitioneren)
            *   [2.5.5.3 Aanhechtingspunten voor bestandssystemen instellen](#Aanhechtingspunten_voor_bestandssystemen_instellen)
        *   [2.5.6 Pakketten selecteren](#Pakketten_selecteren)
        *   [2.5.7 Pakketten installeren](#Pakketten_installeren)
        *   [2.5.8 Systeem configureren](#Systeem_configureren)
        *   [2.5.9 Bootloader installeren](#Bootloader_installeren)
        *   [2.5.10 Installatie afronden](#Installatie_afronden)
*   [3 Pakketbeheer](#Pakketbeheer)
*   [4 APPENDIX](#APPENDIX)

## Introductie

### Wat is Arch Linux?

Arch Linux is een onafhankelijk ontwikkelde Linux distributie, die geoptimaliseerd is voor i686 en x86_64 en die oorspronkelijk gebaseerd was op ideeën van CRUX. De ontwikkeling van Arch Linux is gefocused op een balans van simpelheid, elegantie, correcte code en de nieuwste software. Het lichtgewichte en simpele ontwerp maken het makkelijk om Arch Linux uit te breiden of om te vormen tot wat voor systeem je wil hebben.

### Licentie

Arch Linux en scripts zijn copyright

2002-2007 Judd Vinet

2007-2009 Aaron Griffin

en vallen onder de GNU General Public License (GPL).

## Arch Linux installeren

### Alvorens te installeren

Arch Linux is geoptimaliseerd voor i686 en x86_64 processors en zal daarom niet draaien op lagere of andere generaties van x86 processors, zoals i386, i486 en i586\. Een Pentium II of AMD K6-2 processor of hoger is vereist. Alvorens Arch Linux te installeren, moet je beslissen welk installatie-medium je wilt gaan gebruiken. Arch Linux voorziet in opstartbare ISO en USB disk images, die de GRUB bootloader gebruiken. De ISO images zullen op bijna elke machine met een cd-romspeler werken. De USB images zullen werken op elk systeem met de mogelijkheid om van een USB-apparaat op te starten. Voor degenen die problemen hebben met het niet starten van GRUB, zijn er ISO's met de ISOLINUX bootloader beschikbaar. Er zijn twee varianten van elk installatiemedium, die allen verschillen in meegeleverde pakketten.

*   De "core" images bevatten de [core] pakketten zoals ze op het moment van maken van de images in de repository's zaten. Deze images zijn bedoeld voor mensen met een langzame of moeilijk te configureren internetverbinding.
*   De "ftp" images bevatten geen pakketten, maar gebruiken het netwerk om de meest recente pakketten te installeren. Deze images hebben de voorkeur, omdat ze resulteren in een bijgewerkt systeem en zijn bedoeld voor mensen met een snelle internetverbinding.

Je kunt met beide images de installatie configureren om de pakketten via FTP te verkrijgen, en alle images kunnen worden gebruikt als een volledig functionerende herstelomgeving. De images draaien hetzelfde als een geinstalleerd Arch Linux systeem. In feite zijn ze exact hetzelfde, alleen dan geinstalleerd op een CD of USB image in plaats van een hardeschijf. De images bevatten de gehele "base" pakketenset, evenals diverse netwerkprogramma's en drivers. Als je tijdens het gebruik van deze images een software-pakket nodig hebt, dat niet op de CD staat, dan kun je het eenvoudigweg installeren via pacman, nadat je je internetverbinding hebt geconfigureerd. Een korte pacman handleiding is beschikbaar aan het eind van dit document. De meest gangbare (en aanbevolen) installatieprocedure is om de installatiemedia te gebruiken om alleen de "base" pakketten te installeren, evenals de pakketten en drivers die nodig zijn om online te kunnen. Vervolgens, als je het geinstalleerde systeem succesvol hebt opgestart, draai je een volledige systeem upgrade (met 'pacman -Syu') en installeer je de andere pakketten die je wilt.

### Arch Linux verkrijgen

*   Je kunt Arch Linux downloaden van elk van de spiegelservers in de lijst op de [download](https://www.archlinux.org/download/) pagina.
*   Je kunt ook een Arch Linux installatie CD kopen van Archux, OSDisc of LinuxCD en deze laten bezorgen waar dan ook in de wereld.

### Installatie-media voorbereiden

**CD-ROM**

*   Download iso/<release>/archlinux-XXX.iso
*   Download iso/<release>/sha1sums.txt
*   Controleer de integriteit van het .iso image met sha1sum:

```
 sha1sum --check sha1sums.txt
 archlinux-XXX.iso: OK

```

*   Brand het ISO image op een CD-R of een CD-RW, bijvoorbeeld met Wodim:

```
 wodim -v dev=/dev/cdrw archlinux-XXX.iso

```

**USB**

*   Download iso/<release>/archlinux-XXX.img
*   Download iso/<release>/sha1sums.txt
*   Controleer de integriteit van het .img image met sha1sum:

```
 sha1sum --check sha1sums.txt
 archlinux-XXX.img: OK

```

*   Schrijf het .img image naar een USB mass storage apparaat, zoals een usb stick, met dd:

```
 dd if=archlinux-XXX.img of=/dev/sdX

```

Verzeker jezelf ervan dat je /dev/sdX gebruikt en niet /dev/sdX1\. Dit commando zal alle bestanden op je USB stick onherroepelijk vernietigen, dus verzeker jezelf ervan dat er geen belangrijke bestanden meer op staan, alvorens je dit commando uitvoert.

### Installatiemedia gebruiken

Controleer dat je BIOS is geconfigureerd om het opstarten van een CD-ROM of USB apparaat toe te staan. Herstart je computer met de Arch Linux installatie CD in de cd-romspeler of de USB stick in de USB poort. Zodra het installatiemedium is opgestart, zul je het Arch Linux logo zien, alsmede een GRUB menu dat wacht op je selectie. In de meeste gevallen kun je op "enter" drukken om verder te gaan met opstarten. Aan het eind van de opstartprocedure zou je een login prompt moeten zien, met een aantal simpele instructies bovenin het scherm. Je moet inloggen als de gebruiker "root". Op dat moment ben je klaar om met de daadwerkelijke installatie te beginnen, tenzij je nog handmatig een aantal voorbereidingen wilt treffen.

Met gebruik van de beschikbare shell gereedschappen kan een ervaren gebruiker de hardeschijf of andere apparaten voorbereiden alvorens de installatie te starten. Merk op dat de Arch Linux installatiemedia ook een /arch/quickinst script bevatten voor ervaren gebruikers. Dit script installeert de "base" pakketten in een door de gebruiker gespecificeerde bestemming. Als je een installatie uitvoert met RAID of LVM, of als je de reguliere installatieroutine niet wilt gebruiken, is het quickinst script een goede keuze. Na uitvoeren van quickinst moet je het systeem wel zelf configureren, omdat het script geen enkele vorm van automatische configuratie uitvoert.

### Algemene installatie procedure

**Installatie stappen:**

1.  Een niet-US Keymap laden
2.  Setup uitvoeren
3.  Installatiebron selecteren
    1.  CD-ROM of OTHER SOURCE
    2.  FTP/HTTP
        1.  Netwerk configureren
        2.  Spiegelserver kiezen
4.  Klok instellen
5.  Hardeschijf voorbereiden
    1.  Automatisch partitioneren
    2.  Hardeschijf partitioneren
    3.  Aanhechtingspunten van bestandssysteem configureren
6.  Pakketten selecteren
7.  Pakketten installeren
8.  Systeem configureren
9.  Bootloader installeren
10.  Installatie afsluiten

#### Inloggen en een niet-US keymap laden

Als je een niet-US keymap moet laden en/of een ander console lettertype wilt instellen, kun je het "km" commando gebruiken.

```
 km

```

#### Setup uitvoeren

Nu kun je /arch/setup uitvoeren, om het installatieprogramma aan te roepen.

```
 /arch/setup

```

Na een informatief welkomstbericht word je het hoofdmenu van het installatieprogramma voorgeschoteld. Je kunt de pijltjestoetsen (alleen omhoog en omlaag) gebruiken om de menu's te navigeren. Gebruik TAB om te wisselen tussen knoppen en ENTER om een menu of knop selecteren. Op elk willekeurig moment in de installatieprocedure kun je overschakelen naar de zevende virtuele console (ALT-F7), om uitvoer van de commando's van het installatieprogramma te bekijken. Gebruik (ALT-F1) om terug te schakelen naar de eerste console, waar het installatieprogramma draait, of andere F-toetsen daartussenin, als je een andere console wilt openen om handmatig in te grijpen tijdens de installatie.

#### Bron selecteren

Als eerste stap moet je de methode kiezen die je wilt gebruiken om Arch Linux te installeren. Als je een snelle internetverbinding hebt, zal je voorkeur uitgaan naar de FTP installatie, om verzekerd te zijn van de meest recente pakketten. Indien je een langzame of moeilijk te configureren internetverbinding hebt, kun je kiezen voor een installatie van CD of USB image.

##### CD-ROM of OTHER SOURCE

Als je kiest voor een CD-ROM of OTHER SOURCE installatie, kun je alleen de pakketten kiezen die de CD bevat (die kunnen behoorlijk oud zijn), of pakketten die opgeslagen zijn op een medium dat je handmatig hebt aangehecht (DVD, USB stick, andere partitie) aan het bestandssysteem. Uiteraard is het voordeel van zo'n installatie, dat je geen internetverbinding nodig hebt. Installatie van een CD-ROM is de aanbevolen keuze voor gebruikers met een dial-up verbinding of gebruikers die niet in staat zijn om de pakketten te downloaden.

##### FTP/HTTP

###### Netwerk configureren

Het eerste menu "Setup Network" geeft je de mogelijkheid om je netwerkverbinding te configureren. Als je gebruik maakt van een draadloos netwerkapparaat, moet je nog steeds de gebruikelijke commando's gebruiken om de verbinding handmatig (in de console) te configureren. Er wordt een lijst met alle gevonden netwerkapparaten gepresenteerd. Als er nog geen ethernet apparaat beschikbaar is, of het ethernetapparaat dat je normaal gebruikt er niet tussen staat, kun je OK kiezen om het apparaat te zoeken, of naar een andere console overschakelen om de benodigde module handmatig te laden. Als je daarna je netwerkkaart nog steeds niet kunt configureren, controleer dan of de kaart fysiek goed geinstalleerd is en of de kaart wordt ondersteund door de Linux kernel.

Als de juiste module is geladen en je gewenste netwerkkaart wordt weergegeven, moet je het ethernet apparaat selecteren dat je wilt configureren. Je krijgt de mogelijkheid om het netwerk te configureren met DHCP. Als je netwerk gebruik maakt van DHCP, kies je YES, waarna het installatieprogramma de netwerkkaart configureert. Als je NO kiest, wordt je gevraagd om de informatie voor het configureren handmatig in te vullen. Hoe dan ook, je netwerk moet succesvol worden geconfigureerd, waarna je de internetverbinding in een andere console kunt testen met het commando "ping".

###### Spiegelserver kiezen

"Choose Mirror" geeft je de mogelijkheid om een spiegelserver te kiezen, om de pakketten van te downloaden die zullen worden geinstalleerd in je Arch Linux systeem. Je zou een spiegelserver moeten kiezen die zich het dichtst bij je huidige locatie bevindt, om de meest optimale downloadsnelheden te behalen. Op een later punt in de installatieprocedure word je de mogelijkheid gegeven om de gekozen spiegelserver te gebruiken als de standaard spiegelserver voor de nieuwe installatie.

**Note:** ftp.archlinux.org is gelimiteerd tot 50 KB/s.

Deze menu-opties zijn alleen beschikbaar als je een FTP installatie kiest. Na succesvolle voorbereiding, kies "Return" om naar het hoofdmenu van het installatieprogramma terug te keren.

#### Klok instellen

"Set Clock" geeft je de mogelijkheid om de datum en tijd van je systeem te configureren. Kies UTC als je BIOS klok is ingesteld op UTC, of localtime als je BIOS klok is ingesteld op de lokale tijd. Als je een besturingssysteem hebt geinstalleerd, dat niet overweg kan met UTC BIOS tijden, zoals Windows, kies dan voor localtime, anders heeft UTC de voorkeur. Daarna vraagt het installatieprogramma om het continent en land te kiezen, waarna de bijbehorende tijdzone wordt ingesteld.

#### Hardeschijf voorbereiden

"Prepare Hard Drive" leidt je naar een submenu, die twee mogelijkheden geeft om de hardeschijf van bestemming voor te bereiden voor de installatie.

##### Automatisch partitioneren

De eerste keuze is "Auto-Prepare", en zal je hardeschijf automatisch partitioneren in een /boot, swap, een root partitie en een /home voor de overgebleven ruimte, waarna op elke partitie een bestandssysteem wordt gemaakt. Deze partities worden vervolgens automatisch aangehecht op de juiste plaatsen. Om precies te zijn, Auto-Prepare maakt:

*   32 MB ext2 /boot partitie
*   256 MB swap partitie
*   7.5 GB root partitie
*   /home partitie met de overgebleven ruimte

Je wordt gevraagd om de groottes van de partities aan je eisen aan te passen, maar /home zal altijd de overgebleven ruimte gebruiken.

**AUTO-PREPARE ZAL ALLE GEGEVENS OP DE GEKOZEN HARDESCHIJF ONHERROEPELIJK VERWIJDEREN!**

Als je voorkeur uitgaat naar handmatig partitioneren, kun je de andere twee opties, "Partition Hard Drives" en "Set Filesystem Mountpoints", gebruiken om de bestemming voor te bereiden naar gelang jou specificaties, zoals hieronder beschreven. Na een succesvolle voorbereiding kies je Return om naar het hoofdmenu terug te keren.

##### Hardeschijf partitioneren

"Partition Hard Drives" moet worden overgeslagen als je "Auto-Prepare" al hebt gekozen!

In alle andere gevallen moet je de hardeschijf/hardeschijven selecteren, die je wilt partitioneren, waarna je in het cfdisk programma komt. In cfdisk kun je de partitiestructuur vrijelijk wijzigen, totdat je [Write] en [Quit] gebruikt. Je hebt minstens een root partitie nodig, om de installatie te kunnen voortzetten. Het is behulpzaam om ergens te noteren op welke plek je partities je gaat aanhechten in het bestandssysteem, aangezien dat wordt gevraagd in de volgende stap.

##### Aanhechtingspunten voor bestandssystemen instellen

"Set Filesystem Mountpints" moet ook worden overgeslagen, als je "Auto-Prepare" koos om de hardeschijf voor te bereiden. Je moet dit menu kiezen als je de partitiestructuur hebt aangepast aan je wensen, of als er al een geschikte partitiestructuur aanwezig was.

De eerste vraag die beantwoord moet worden, is welke partitie moet worden gebruikt als swap. Selecteer de hiervoor gemaakte swap partitie van de lijst, of kies NONE als je geen swap partitie wilt gebruiken. Het gebruik van een swapbestand wordt niet direct ondersteund door het installatieprogramma. Als je toch een swapbestand wilt gebruiken, kies je voor NONE, waarna je de andere aanhechtingspunten configureert. Daarna schakel je naar een andere console, waar je handmatig een swapbestand kunt activeren met het "swapon" commando. Als je ervoor kiest om een swap partitie te gebruiken, wordt er gevraagd of je een bestandssysteem op de gekozen partitie wilt maken. Omdat een swap partitie een specifiek bestandssysteem gebruikt, moet je hier altijd voor YES kiezen.

Na het configureren van de swap partitie word je gevraagd om de partitie aan te geven die gebruikt gaat worden als root partitie. Dit is verplicht. Het configureren van aanhechtingspunten en bestandssystemen voor partities wordt herhaald voor alle gekozen partities, tot je DONE kiest in het menu. Het installatieprogramma zal /boot suggereren voor alle volgende aanhechtingspunten na swap en root. Elke keer als je een een aan te hechten partitie geselecteerd hebt, word je gevraagd of je een bestandssysteem op de respectievelijke partitie wilt maken. Kiezen voor YES geeft je de mogelijkheid om het soort bestandssysteem te kiezen om te maken. De partities worden vervolgens geformatteerd met het gekozen bestandssysteem, waarbij alle gegevens op de gekozen partities worden vernietigd. Het is geen probleem om NO te kiezen, als je de bestaande gegevens op de partitie wilt bewaren. Alvorens het echte formatteren begint, zal het installatieprogramma al je keuzes presenteren en vragen of je door wilt gaan. Na het formatteren en aanhechten van de partities kies je Return om naar het hoofdmenu terug te keren en door te gaan met de volgende stap.

#### Pakketten selecteren

"Select Packages" geeft je de mogelijkheid om de pakketten te kiezen die je wilt installeren van CD, USB of een FTP spiegelserver. Je hebt de mogelijkheid om hele pakketgroepen te selecteren vanwaar je pakketten wilt installeren, waarna je de individuele pakketten kunt (de)selecteren met de spatiebalk. Het is aanbevolen om alle "base" pakketten te installeren, maar niets anders op dit moment. De enige uitzondering op de regel is het installeren van pakketten die benodigd zijn voor het configureren van je internetverbinding.

Als je klaar bent met de pakketselectie, kies je voor Return om naar het hoofdmenu terug te keren en door te gaan met de volgende stap.

#### Pakketten installeren

"Install Packages" zal nu het "base" systeem op de gekozen hardeschijf installeren, alsmede alle andere door jou geselecteerde pakketten en de bijbehorende afhankelijkheden.

#### Systeem configureren

"Configure System" geeft je de mogelijkheid om de configuratiebestanden te wijzigen, die cruciaal zijn voor je nieuwe installatie. Je wordt gevraagd om een programma te kiezen, waarmee je de configuratiebestanden wilt wijzigen, waarbij je kunt kiezen tussen VIM en nano.

**Configuratiebestanden**

Dit zijn de belangrijkste configuratiebestanden voor Arch Linux. Alleen de meest belangrijke configuratiebestanden worden hier opgesomd. Als je hulp nodig hebt bij het configureren van een specifiek programma, lees dan de respectievelijke manpages of gebruik online documentatie. In de meeste gevallen zijn de Arch Linux [Wiki](https://wiki.archlinux.org/) en het [forum](https://bbs.archlinux.org/) een goede bron van informatie.

*   /etc/rc.conf
*   [/etc/fstab](/index.php/Fstab "Fstab")
*   /etc/mkinitcpio.conf
*   /etc/modprobe.d/modprobe.conf
*   /etc/resolv.conf
*   /etc/hosts
*   /etc/hosts.deny
*   /etc/hosts.allow
*   /etc/locale.gen
*   /etc/pacman.d/mirrorlist

**/etc/rc.conf**

Dit is het hoofd configuratiebestand voor Arch Linux. Het geeft je de mogelijkheid om je keyboard, tijdzone, hostname en netwerk te configureren, alsmede daemons die moeten worden opgestart, kernel modules die moeten worden geladen of geblacklist, netwerk profielen die moeten worden gestart en meer.

**LOCALE:** Dit configureert je systeem taal, welke wordt gebruikt door alle i18n-vriendelijke programma's. Zie locale.gen hieronder voor beschikbare opties. De standaardinstelling is geschikt voor US English gebruikers.

**HARDWARECLOCK:** UTC in het geval je BIOS klok is geconfigureerd voor UTC, of localtime als je BIOS klok is geconfigureerd voor de lokale tijd. Als je een besturingssysteem hebt, dat niet overweg kan met UTC BIOS tijden, zoals Windows, kies dan voor localtime. In alle andere gevallen heeft UTC de voorkeur, omdat zomertijd/wintertijd dan geen probleem meer is. Ook heeft UTC een aantal andere positieve aspecten.

**USEDIRECTISA:** Indien ingesteld op "yes", gebruikt "hwclock" expliciete I/O instructies om de hardware klok te benaderen. Anders zal hwclock gebruik proberen te maken van het /dev/rtc apparaatbestand. De standaardinstellling "no" is geschikt voor niet-ISA machines.

**TIMEZONE:** Specificeert je tijdzone. Mogelijke tijdzones zijn het relative pad naar een zoneinfo bestand, beginnend bij de map /usr/share/zoneinfo. Een Duitse tijdzone zou bijvoorbeeld Europe/Berlin kunnen zijn, welke verwijst naar het bestand /usr/share/zoneinfo/Europe/Berlin. Als je de exacte naam van je tijdzone-bestand niet weet, kun je dit in de bovengenoemde map opzoeken.

**KEYMAP:** Definieert de keymap die wordt geladen met het "laodkeys" programma tijdens de opstartprocedure. Mogelijke keymaps kunnen worden gevonden in de map /usr/share/kbd/keymaps. Deze instelling is alleen gelding voor de TTY's, niet voor enige grafische windowmanager of X! Ook hier is de standaardinstelling geschikt voor US gebruikers.

**CONSOLEFONT:** Definieert het console lettertype dat wordt geladen met het "setfont" programma tijdens de opstartprocedure. Mogelijke lettertypes zijn te vinden in /usr/share/kbd/consolefonts.

**CONSOLEMAP:** Definieert de console map die moet worden geladen met het "setfont" programma tijdens de opstartprocedure. Mogelijke maps kunnen worden gevonden in /usr/share/kbd/consoletrans. Je zult deze parameter willen instellen op een map die geschikt is voor de locale die je hebt gekozen (8859-1 voor Latin1 bijvoorbeeld) als je een UTF-8 locale hebt gebruikt en gebruik maakt van programma's die 8-bit uitvoer genereren. Als je X11 gebruikt voor je dagelijkse werkzaamheden, hoef je hier niet op te letten, aangezien CONSOLEMAP alleen de uitvoer van Linux console applicaties beinvloed.

**USECOLOR:** Activeert of deactiveert gekleurde statusberichten tijdens het opstarten.

**MOD_AUTOLOAD:** Indien ingesteld op "yes", wordt udev toegestaan om benodigde modules te laden tijdens het opstarten.

**MODULES:** In deze array kun je de namen van de modules weergeven, die je geladen wilt hebben tijdens het opstarten, zonder deze te koppelen aan een hardware apparaat, zoals dat in modprobe.conf gebeurt. Voeg eenvoudigweg de naam van de module toe, en zet eventuele parameters voor de modules in modprobe.conf, indien nodig. Een uitroepteken (!) voor een module zal een module blacklisten. Als je een module wilt blacklisten, die niet in de array staat, kun je die toevoegen met het uitroepteken ervoor, om ervoor te zorgen dat de module nooit wordt geladen.

**USELVM:** Zet op "yes" om "vgchange" uit te voeren tijdens sysinit, waarbij LVM groepen worden geactiveerd.

**HOSTNAME:** Zet hier de hostname van de machine neer, zonder het domein-achtervoegsel. Dit is jouw keuze, zolang je het bij letters, cijfers en zwevende streepjes houdt.

**INTERFACES:** Hier definieer je de instellingen voor je netwerkapparaten. De standaard regels en het commentaar leggen de instellingen duidelijk uit. Als je DHCP gebruikt, zou 'eth0="dhcp"' moeten werken. Als je geen DHCP gebruikt, houdt dan in gedachten dat de waarde van de variabele (waarvan de naam gelijk moet zijn aan de naam van het apparaat dat het moet configureren) gelijk is aan de lijn die zou worden toegevoegd aan het "ifconfig" commando, als je het apparaat handmatig zou configureren in de shell.

**ROUTES:** Je kunt je eigen statische netwerkroutes hier definieren met willekeurige namen. Kijk naar het voorbeeld voor een standaard gateway voor het idee. Eigenlijk is het quoted gedeelte identiek aan hetgeen je meegeeft aan een handmatig "route add" commando. Daarom is "man route" aanbevolen als je niet weet wat je hier neer wilt zetten. De standaardinstelling is aanbevolen voor de meesten.

**[NET_PROFILES](/index.php/Network_Profiles "Network Profiles"):** Activeert bepaalde netwerkprofilen tijdens het opstarten. Netwerkprofielen bieden een makkelijke manier om meerdere netwerkconfiguraties te beheren en zijn bedoeld om de standaard INTERFACES/ROUTES te vervangen, welke nog steeds aanbevolen zijn voor systemen met slechts één netwerkconfiguratie. Als je computer deel uitmaakt van verschillende netwerken op verschillende tijden (bijvoorbeeld een laptop), dan moet je eens kijken naar de map /etc/network-profiles, om een aantal profielen te configureren. Er zijn sjablonen meegeleverd voor veschillende netwerkconfiguraties. Netwerkprofielen vereisen het "netcfg" pakket.

**DAEMONS:** Deze array bevat simpelweg de namen van de scripts die in /etc/rc.d/ staan, en die moeten worden uitgevoerd tijdens het opstartproces. Als een scriptnaam wordt voorafgegaan door een uitroepteken (!), dan wordt het script niet uitgevoerd (zelfde methode als blacklisten van kernel modules). Als een script wordt voorafgegaan door een apestaartje (@), dan zal het worden uitgevoerd in de achtergrond (het opstartproces zal dan niet wachten tot het script in zijn geheel is uitgevoerd, alvorens verder te gaan met het volgende script). Normaal hoef je de standaardinstelling niet te veranderen om een werkend systeem te krijgen, maar je zult deze array in de loop van de installatie gaan aanpassen, als je systeemservices als sshd of samba gaat installeren en deze automatisch gestart wil hebben als je systeem opstart.

**[/etc/fstab](/index.php/Fstab "Fstab")**

De instellingen voor de bestandssystemen en aanhechtingspunten worden hier geconfigureerd. Het installatieprogramma zal hier de benodigde regels hebben gemaakt, maar het is aan te raden om dit even te controleren. Als je gebruik maakt van een versleutelde root partitie, LVM of RAID, dan zul je waarschijnlijk de door het installatieprogramma ingevoegde UUIDs moeten veranderen in apparaatnamen.

**/etc/mkinitcpio.conf**

Dit bestand biedt de mogelijkheid om de initial ramdisk voor je systeem te configureren. De ramdisk is een gzipped image die wordt ingelezen door de kernel tijdens het opstarten. Het doel van een ramdisk is om het systeem te bootstrappen tot het punt waar de kernel het root bestandssysteem kan benaderen. Dit betekend dat de ramdisk alle modules moet laden, die vereist zijn om opslagapparaten als IDE, SCSI of SATA hardeschijven (of USB/Firewire) te kunnen herkennen. Zodra de ramdisk de juiste modules heeft geladen, handmatig of via udev, wordt de controle overgedragen aan de opstartscripts van Arch Linux, waarna het opstarten van het systeem doorgaat. Om deze reden hoeft de ramdisk alleen de modules te bevatten, die nodig zijn om het root bestandssysteem te kunnen benaderen. De ramdisk hoeft niet alle modules te bevatten die je ooit wilt gaan gebruiken. De overgrote meerderheid van de modules die je over het algemeen zult gebruiken, zullen tijdens de initprocedure worden geeladen bij udev.

Standaard is mkinitcpio.conf geconfigureerd om alle benodigde modules voor IDE, SCSI en SATA apparaten te detecteren met behulp van zogenoemde HOOKS. Dit betekend dat de standaard initrd (initrd is een afkorting voor Initial Ramdisk) voor bijna iedereen werkt. Je kunt mkinitcpio.conf wijzigen en de subsystem HOOKS (waaronder IDE, SCSI, RAID, USB, etcetera) verwijderen, als je die niet nodig hebt. Daarnaast kun je de initrd nog verder modificeren, door de benodigde modules exact te specificeren in de MODULES array, waarna nog meer HOOKS kunnen worden verwijderd. Wees hier extreem voorzichtig mee, omdat een niet functioneel initrd ervoor zorgt dat je systeem niet wil opstarten.

Als je gebruik maakt van RAID of versleuteling op je root bestandssysteem, dan zul je de RAID/CRYPT insteling onderaan het bestand willen optimaliseren. Zie de wiki pagina's voor RAID/LVM, versleuteling van het bestandssysteem en meer informatie over mkinitcpio. Als je gebruik maakt van een niet-US keyboard, dan moet je ook de 'keymap' HOOK toevoegen aan HOOKS. Als je een USB keyboard hebt, moet je de 'usbinput' hook toevoegen aan HOOKS.

**/etc/modprobe.d/modprobe.conf**

Dit bestand vertelt de kernel welke modules het moet laden voor systeemapparaten en welke parameters er aan die modules moeten worden meegegeven. Bijvoorbeeld: om de kernel je Realtek 8139 ethernet module te laten laden als het je netwerk start (eth0 configureren), kun je deze regel gebruiken:

```
 alias eth0 8139too

```

De meeste mensen zullen dit bestand niet hoeven te wijzigen.

**/etc/resolv.conf**

Gebruik dit bestand om handmatig je nameserver(s) te configureren, die je wil gebruiken. Het bestand ziet er ongeveer zo uit:

```
 search domain.tld
 nameserver 192.168.0.1
 nameserver 192.168.0.2

```

Vervang domain.tld en de IP-adressen door jouw instellingen. Het search domain specificeert het standaard domein dat automatisch wordt toegevoegd aan de unqualified hostnaam (unqualified hostname zou dan 'myhost' zijn en qualified hostname zou dan 'myhost.domain.tld' zijn). Door het toevoegen van de domain name wordt een 'ping myhost' wordt dan effectief een 'ping myhost.domain.tld' met de bovenstaande waardes. Deze instellingen zijn over het algemeen niet zo belangrijk en de meeste mensen zullen hier niets aan veranderen. Als je gebruik maakt van DHCP, zal de inhoud van dit bestand automatisch worden gevuld met de juiste waardes, als het netwerk wordt geconfigureerd, wat erop neer komt dat je dit bestand vrolijk kunt en zou moeten negeren.

**/etc/hosts**

In dit bestand associeer je de hostnamen van de computers op je netwerk met de bijbehorende IP-adressen. Als een hostnaam niet bekend is bij je DNS, dan kun je het hier toevoegen voor correcte resolving. Ook kun je hiermee DNS-antwoorden teniet doen. Normaal gesproken hoef je niets in dit bestand te vervangen, maar je zou de hostnaam + domain van je eigen machine kunnen toevoegen aan dit bestand, associërend met het IP-adres van je netwerkkaart. Sommige services, waaronde Postfix, zullen anders gaan flippen. Als je niet weet wat te doen, wijzig dan voorlopig niets, totdat je "man hosts" hebt gelezen.

**/etc/hosts.deny**

Dit bestand verbied netwerk services toegang. De standaardinstelling verbied netwerk services alle toegang.

```
 ALL: ALL: DENY

```

**/etc/hosts.allow**

Dit bestand geeft netwerk services toegang. Specificeer hier services die je wilt toestaan. Om machines toe te staan om via ssh in te loggen:

```
 sshd: ALL: ALLOW

```

**/etc/locale.gen**

Dit bestand bevat een lijst met alle ondersteunde locales en beschikbare charsets. Als je een LOCALE kiest in je /etc/rc.conf of als je een programma start, is het vereist om de respectievelijke locale te "uncommenten" (het weghalen van het hekje (#) aan het begin van een regel), om een gecompileerde versie van de locale beschikbaar te maken voor het systeem. Na het uncommenten van een locale moet je als root het commando 'locale-gen' uitvoeren, waarna alle uncommented locales worden gegenereerd. Je moet alle locales uncommenten, die je wilt gaan gebruiken.

Tijdens het installatieproces hoef je locale-gen niet handmatig uit te voeren, dit wordt automatisch gedaan, zodra je de veranderingen in dit bestand hebt opgeslagen. Standaard worden alle locales geactiveerd, die nodig zijn voor de LOCALE die je in rc.conf hebt gedefinieerd. Om je systeem goed te laten werken, moet je minimaal de locale uncommenten die je in rc.conf hebt gespecificeerd.

**/etc/pacman.d/mirrorlist**

Dit bestand bevat een lijst met spiegelservers, vanwaar pacman de pakketen zal downloaden voor de officiele Arch Linux repositories. De spiegelservers worden geprobeerd in de volgorde waarin ze worden weergegeven. De variabele "$repo" wordt automatisch vervangen door pacman, afhankelijk van de repository die pacman op dat moment gebruikt.

Als je een FTP installatie uitvoert, dan wordt de spiegelserver die je hebt gebruikt voor het downloaden van de pakketten automatisch toegevoegd bovenin het bestand, om ervoor te zorgen dat deze spiegelserver als standaard spiegelserver wordt gebruikt in je nieuwe Arch Linux systeem.

**Root wachtwoord instellen**

Nu moet je het wachtwoord voor de gebruiker "root" instellen voor je systeem. Kies dit wachtwoord zorgvuldig, bij voorkeur een mix van alfanumerieke en speciale karakters, aangezien het wachtwoord toestaat om belangrijke onderdelen van je systeem te wijzigen.

Als je klaar bent met het wijzigen van de configuratiebestanden, kies je Return om naar het hoofdmenu terug te keren. Het installatieprogramma zal de initrd opnieuw genereren, dit keer met de wijzigingen die je in mkinitcpio.conf hebt gemaakt.

#### Bootloader installeren

"Install Bootloader" zal GRUB als bootloader installeren op je hardeschijf. Je kunt kiezen voor NONE als je een boatloader hebt geinstalleerd en deze wilt gebruiken om je systeem op te starten. Als je ervoor kiest om GRUB te installeren, zal het installatieprogramma je het GRUB configuratiebestand voorschotelen, waarin je de instellingen even moet controleren en bevestigen.

**/boot/grub/menu.lst**

Je zou dit bestand moeten controleren en aanpassen, aan de hand van je eisen aan het opstartproces, als je ervoor hebt gekozen om GRUB te installeren. Als je al een bestaande bootloader hebt van een andere Linux-installatie of een ander besturingssysteem, moet je die bootloader configureren om je nieuwe installatie te herkennen en op te kunnen starten. Het installatieprogramma heeft menu.lst al gevuld met de juise UUID regels, die je eventueel moet wijzigen, als je die ook hebt gewijzigd in je fstab bestand, bijvoorbeeld bij gebruik van RAID, LVM of versleuteling.

Na het controleren van de configuratie van je bootloader, word je gevraagd voor een partitie om de bootloader op te installeren. Tenzij je al gebruik maakt van een andere bootloader, zou je GRUB moeten installeren op het MBR (Master Boot Record) van je hardeschijf, welke wordt vertegenwoordigd door het apparaatbestand zonder nummer als achtervoegsel (de apparaatbestanden MET nummer als achtervoegsel zijn de partities op de desbetreffende hardeschijf).

#### Installatie afronden

Sluit het installatieprogramma af, verwijder het installatiemedium en typ het commando "reboot" op de commandline. Als je systeem opstart, kun je inloggen als de gebruiker "root" met het wachtwoord dat je voor die gebruiker hebt ingesteld tijdens de installatie.

Gefeliciteerd! Welkom in je nieuwe Arch Linux systeem!

## Pakketbeheer

Pacman is het pakketbeheerprogramma dat alle software op je systeem bijhoudt. Het heeft ondersteuning voor het oplossen van afhankelijkheden van pakketten en maakt gebruik van standaard gzipped tar archiefbestanden (.tar.gz) voor alle pakketten. Sommige standaardtaken, die je nodig kunt hebben tijdens en na de installatie, zijn hieronder beschreven met hun bijbehorende commando's. Voor een uitgebreide uitleg van pacman's opties is het aanbevolen om "man pacman" te lezen, of de Arch Linux [Wiki](/index.php/Pacman "Pacman") te raadplegen.

**Typische taken:**

*   De lijst met beschikbare softwarepakketten en versies verversen

```
 # pacman --sync --refresh
 # pacman -Sy

```

Dit commando zal een versie master pakketlijst downloaden van de repository's die gedefineerd zijn in het /etc/pacman.conf configuratiebestand, waarna de pakketlijst wordt uitgepakt in de database-omgeving.

*   Zoek in de repository naar een pakket

```
 # pacman --sync --search <regexp>
 # pacman -Ss <regexp>

```

Zoek in elk pakket in de pakketlijst voor namen of beschrijvingen die aan de reguliere expressie voldoen.

*   Toon specifieke informatie voor niet-geinstalleerde pakketten

```
 # pacman --sync --info foo
 # pacman -Si foo

```

Toont informatie over het niet-geinstalleerde pakket 'foo' (grootte, installatie-datum, bouw datum, afhankelijkheden, conflicten, etcetera)

*   Installeer een pakket uit de repository's

```
 # pacman --sync foo
 # pacman -S foo

```

Download en installeer het pakket 'foo', samen met alle afhankelijkheden die het pakket vereist. Alvorens een sync optie te gebruiken, is het verstandig om de pakketlijst te verversen.

*   Toon geinstalleerde pakketten

```
 # pacman --query
 # pacman -Q

```

Toont een lijst van alle geinstalleerde pakketten op het systeem.

*   Controleer of een specifiek pakket is geinstalleerd

```
 # pacman --query foo
 # pacman -Q foo

```

Dit commando zal de naam en versie van het pakket 'foo' tonen, als het geinstalleerd is. Als 'foo' niet geinstalleerd is, wordt er niets getoond.

*   Toon specifieke pakketinformatie

```
 # pacman --query --info foo
 # pacman -Qi foo

```

Toont specifieke informatie over het geinstalleerde pakket 'foo' (grootte, installatie-datum, bouw datum, afhankelijkheden, conflicten, etcetera)

*   Toon een lijst van bestanden in een pakket

```
 # pacman --query --list foo
 # pacman -Ql foo

```

Toont een lijst van alle bestanden die bij het pakket 'foo' horen.

*   Zoek uit bij welk pakket een specifiek bestand hoort

```
 # pacman --query --owns /path/to/file
 # pacman -Qo /path/to/file

```

Deze zoekopdracht toont de naam en versie van het pakket dat het bestand bevat dat als parameter is meegegeven.

## APPENDIX

Zie de [Official Arch Linux Install Guide Appendix](/index.php/Official_Arch_Linux_Install_Guide_Appendix "Official Arch Linux Install Guide Appendix") voor gerelateerde maar onofficiele informatie, die handig kan zijn voor nieuwe gebruikers.