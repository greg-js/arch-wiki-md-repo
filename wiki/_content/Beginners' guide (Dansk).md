# Beginners' guide (Dansk)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** needs updating for systemd and possibly other things (Discuss in [Talk:Beginners' guide (Dansk)#](https://wiki.archlinux.org/index.php/Talk:Beginners%27_guide_(Dansk)))

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**This article or section needs to be [translated](/index.php/ArchWiki:Contributing#Translating "ArchWiki:Contributing").**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Beginners' guide (Dansk)#](https://wiki.archlinux.org/index.php/Talk:Beginners%27_guide_(Dansk)))

## Contents

*   [1 Forord](#Forord)
    *   [1.1 Introduktion](#Introduktion)
    *   [1.2 Licens](#Licens)
    *   [1.3 Arch principper og filosofi](#Arch_principper_og_filosofi)
    *   [1.4 Alt du vil vide om at installere Arch Linux, men ikke kunne få dig til at spørge om](#Alt_du_vil_vide_om_at_installere_Arch_Linux.2C_men_ikke_kunne_f.C3.A5_dig_til_at_sp.C3.B8rge_om)
    *   [1.5 DON'T PANIC!](#DON.27T_PANIC.21)
*   [2 Forberedelse](#Forberedelse)
    *   [2.1 Skaf det seneste installationsmedie](#Skaf_det_seneste_installationsmedie)
        *   [2.1.1 Check integriteten af den downloadede fil](#Check_integriteten_af_den_downloadede_fil)
        *   [2.1.2 CD installer](#CD_installer)
        *   [2.1.3 Flash memory device eller USB stick](#Flash_memory_device_eller_USB_stick)
            *   [2.1.3.1 *nix metode](#.2Anix_metode)
            *   [2.1.3.2 Microsoft Windows metode](#Microsoft_Windows_metode)
        *   [2.1.4 Installer over netværket](#Installer_over_netv.C3.A6rket)
        *   [2.1.5 Installer på en virtuel maskine](#Installer_p.C3.A5_en_virtuel_maskine)
    *   [2.2 Boot Arch Linux installer](#Boot_Arch_Linux_installer)
        *   [2.2.1 Boot fra mediet](#Boot_fra_mediet)
        *   [2.2.2 OS system-start](#OS_system-start)
            *   [2.2.2.1 Troubleshooting boot-problemer](#Troubleshooting_boot-problemer)
        *   [2.2.3 Skift keymap](#Skift_keymap)
        *   [2.2.4 Dokumentation](#Dokumentation)
*   [3 Installation](#Installation)
    *   [3.1 Vælg en installationskilde](#V.C3.A6lg_en_installationskilde)
        *   [3.1.1 Netværks-setup](#Netv.C3.A6rks-setup)
            *   [3.1.1.1 Setup ADSL bridging i live-miljøet (valgfri)](#Setup_ADSL_bridging_i_live-milj.C3.B8et_.28valgfri.29)
            *   [3.1.1.2 Setup af trådløs i live-miljøet (valgfri)](#Setup_af_tr.C3.A5dl.C3.B8s_i_live-milj.C3.B8et_.28valgfri.29)
    *   [3.2 Vælg editor](#V.C3.A6lg_editor)
    *   [3.3 Indstil klokken](#Indstil_klokken)
        *   [3.3.1 Indstil region og tidszone](#Indstil_region_og_tidszone)
        *   [3.3.2 Indstil tid og dato](#Indstil_tid_og_dato)
            *   [3.3.2.1 Indstil tiden i et Windows dual boot setup](#Indstil_tiden_i_et_Windows_dual_boot_setup)
    *   [3.4 Forbered harddisken](#Forbered_harddisken)
        *   [3.4.1 Partitionering af hardiske: Generel information](#Partitionering_af_hardiske:_Generel_information)
            *   [3.4.1.1 Partition-type](#Partition-type)
            *   [3.4.1.2 Swap partition](#Swap_partition)
            *   [3.4.1.3 Valg af partitionering](#Valg_af_partitionering)
            *   [3.4.1.4 Hvor stor bør mine partitioner være?](#Hvor_stor_b.C3.B8r_mine_partitioner_v.C3.A6re.3F)
        *   [3.4.2 Oprettelse af filsystemer: Generel information](#Oprettelse_af_filsystemer:_Generel_information)
            *   [3.4.2.1 Filesystem-typer](#Filesystem-typer)
            *   [3.4.2.2 Journalisering](#Journalisering)
        *   [3.4.3 Mulighed 1: Auto prepare](#Mulighed_1:_Auto_prepare)
        *   [3.4.4 Mulighed 2: Manually partition hard drives](#Mulighed_2:_Manually_partition_hard_drives)
        *   [3.4.5 Mulighed 3: Manually configure block devices, filesystems, and mountpoints](#Mulighed_3:_Manually_configure_block_devices.2C_filesystems.2C_and_mountpoints)
    *   [3.5 Vælg pakker](#V.C3.A6lg_pakker)
        *   [3.5.1 Bootloader](#Bootloader)
        *   [3.5.2 Pakkegrupper](#Pakkegrupper)
    *   [3.6 Installér pakker](#Install.C3.A9r_pakker)
    *   [3.7 Konfigurér systemet](#Konfigur.C3.A9r_systemet)
        *   [3.7.1 Kan installeren håndtere dette mere automatisk?](#Kan_installeren_h.C3.A5ndtere_dette_mere_automatisk.3F)
        *   [3.7.2 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [3.7.2.1 Sektionen LOCALIZATION](#Sektionen_LOCALIZATION)
            *   [3.7.2.2 Sektionen HARDWARE](#Sektionen_HARDWARE)
            *   [3.7.2.3 Sektionen NETWORKING](#Sektionen_NETWORKING)
            *   [3.7.2.4 Sektionen DAEMONS](#Sektionen_DAEMONS)
                *   [3.7.2.4.1 Generel information](#Generel_information)
        *   [3.7.3 /etc/fstab](#.2Fetc.2Ffstab)
        *   [3.7.4 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
        *   [3.7.5 /etc/modprobe.d/modprobe.conf](#.2Fetc.2Fmodprobe.d.2Fmodprobe.conf)
        *   [3.7.6 /etc/resolv.conf](#.2Fetc.2Fresolv.conf)
        *   [3.7.7 /etc/hosts](#.2Fetc.2Fhosts)
        *   [3.7.8 /etc/locale.gen](#.2Fetc.2Flocale.gen)
            *   [3.7.8.1 Root-adgangskode](#Root-adgangskode)
            *   [3.7.8.2 Pacman-spejle](#Pacman-spejle)
    *   [3.8 Install and configure a bootloader](#Install_and_configure_a_bootloader)
        *   [3.8.1 For BIOS motherboards](#For_BIOS_motherboards)
            *   [3.8.1.1 Syslinux](#Syslinux)
            *   [3.8.1.2 GRUB](#GRUB)
        *   [3.8.2 For UEFI motherboards](#For_UEFI_motherboards)
            *   [3.8.2.1 Gummiboot](#Gummiboot)
            *   [3.8.2.2 GRUB](#GRUB_2)
*   [4 Konfigurere grundsystemet](#Konfigurere_grundsystemet)
    *   [4.1 Netværkskonfiguration (hvis nødvendigt)](#Netv.C3.A6rkskonfiguration_.28hvis_n.C3.B8dvendigt.29)
        *   [4.1.1 Kablet LAN](#Kablet_LAN)
        *   [4.1.2 Trådløs LAN](#Tr.C3.A5dl.C3.B8s_LAN)
        *   [4.1.3 Analogt modem](#Analogt_modem)
        *   [4.1.4 ISDN](#ISDN)
        *   [4.1.5 DSL (PPPoE)](#DSL_.28PPPoE.29)
*   [5 Opdatering synkronisering og opgradering med Pacman](#Opdatering_synkronisering_og_opgradering_med_Pacman)
    *   [5.1 Hvad er Pacman ?](#Hvad_er_Pacman_.3F)
    *   [5.2 Opdatér Pacman](#Opdat.C3.A9r_Pacman)
    *   [5.3 Konfigurering af Pacman](#Konfigurering_af_Pacman)
        *   [5.3.1 Pakkekilder og /etc/pacman.conf](#Pakkekilder_og_.2Fetc.2Fpacman.conf)
        *   [5.3.2 /etc/pacman.conf](#.2Fetc.2Fpacman.conf)
        *   [5.3.3 /etc/pacman.d/mirrorlist](#.2Fetc.2Fpacman.d.2Fmirrorlist)
*   [6 Opdatere systemet](#Opdatere_systemet)
    *   [6.1 _Læg mærke til, om der sker en større kerneopdatering._](#L.C3.A6g_m.C3.A6rke_til.2C_om_der_sker_en_st.C3.B8rre_kerneopdatering.)
    *   [6.2 Det gode ved 'Rolling Release'](#Det_gode_ved_.27Rolling_Release.27)
    *   [6.3 Lær Pacman at kende](#L.C3.A6r_Pacman_at_kende)
    *   [6.4 Tilføj en bruger og sæt grupper op](#Tilf.C3.B8j_en_bruger_og_s.C3.A6t_grupper_op)
*   [7 **TRIN 2**: Installation af X og konfiguration af ALSA](#TRIN_2:_Installation_af_X_og_konfiguration_af_ALSA)
    *   [7.1 Konfigurér lydkortet med 'alsamixer'](#Konfigur.C3.A9r_lydkortet_med_.27alsamixer.27)
        *   [7.1.1 Test af lyden](#Test_af_lyden)
    *   [7.2 Installation og konfiguration af X](#Installation_og_konfiguration_af_X)
*   [8 **TRIN 3:** Installation og konfiguration af dit skrivebord](#TRIN_3:_Installation_og_konfiguration_af_dit_skrivebord)
    *   [8.1 Installér fonte](#Install.C3.A9r_fonte)
    *   [8.2 ~/.xinitrc](#.7E.2F.xinitrc)
    *   [8.3 GNOME](#GNOME)
        *   [8.3.1 Om GNOME](#Om_GNOME)
        *   [8.3.2 Installation](#Installation_2)
            *   [8.3.2.1 Nyttige GNOME-dæmoner](#Nyttige_GNOME-d.C3.A6moner)
        *   [8.3.3 Guf for øjet](#Guf_for_.C3.B8jet)
    *   [8.4 KDE](#KDE)
        *   [8.4.1 Om KDE](#Om_KDE)
        *   [8.4.2 Installation](#Installation_3)
        *   [8.4.3 Nyttige KDE-dæmoner](#Nyttige_KDE-d.C3.A6moner)
    *   [8.5 Xfce](#Xfce)
        *   [8.5.1 Om Xfce](#Om_Xfce)
        *   [8.5.2 Installation](#Installation_4)
    *   [8.6 *box](#.2Abox)
        *   [8.6.1 Fluxbox](#Fluxbox)
        *   [8.6.2 Openbox](#Openbox)
    *   [8.7 fvwm2](#fvwm2)
*   [9 Tilretning og finpudsning](#Tilretning_og_finpudsning)
    *   [9.1 HAL](#HAL)
    *   [9.2 Sætte dæmoner i baggrunden under opstart](#S.C3.A6tte_d.C3.A6moner_i_baggrunden_under_opstart)
    *   [9.3 Pænere fonte for LCD-er](#P.C3.A6nere_fonte_for_LCD-er)
    *   [9.4 Musehjul](#Musehjul)
    *   [9.5 evdev](#evdev)
    *   [9.6 Tastaturlayout](#Tastaturlayout)
    *   [9.7 Yderligere tilretninger til bærbare computere](#Yderligere_tilretninger_til_b.C3.A6rbare_computere)
    *   [9.8 Konfiguration af CPU frekvensskalering](#Konfiguration_af_CPU_frekvensskalering)
*   [10 Nyttige programmer](#Nyttige_programmer)
    *   [10.1 Internet](#Internet)
        *   [10.1.1 Firefox](#Firefox)
    *   [10.2 Kontor](#Kontor)
*   [11 Multimedie](#Multimedie)
    *   [11.1 Videoafspiller](#Videoafspiller)
        *   [11.1.1 VLC](#VLC)
        *   [11.1.2 Mplayer](#Mplayer)
        *   [11.1.3 Xine](#Xine)
        *   [11.1.4 GNOME](#GNOME_2)
            *   [11.1.4.1 Totem](#Totem)
        *   [11.1.5 KDE](#KDE_2)
            *   [11.1.5.1 Kaffeine](#Kaffeine)
    *   [11.2 Lydafspillere](#Lydafspillere)
        *   [11.2.1 GNOME/Xfce](#GNOME.2FXfce)
            *   [11.2.1.1 Exaile](#Exaile)
            *   [11.2.1.2 Rhythmbox](#Rhythmbox)
            *   [11.2.1.3 Quod Libet](#Quod_Libet)
        *   [11.2.2 KDE](#KDE_3)
            *   [11.2.2.1 Amarok](#Amarok)
        *   [11.2.3 Konsol](#Konsol)
        *   [11.2.4 Andre X-baserede](#Andre_X-baserede)
    *   [11.3 Kodeks og andre typer af multimedieindhold](#Kodeks_og_andre_typer_af_multimedieindhold)
        *   [11.3.1 DVD](#DVD)
        *   [11.3.2 Flash](#Flash)
        *   [11.3.3 Quicktime](#Quicktime)
        *   [11.3.4 Realplayer](#Realplayer)
    *   [11.4 CD- og DVD-brænding](#CD-_og_DVD-br.C3.A6nding)
        *   [11.4.1 GNOME](#GNOME_3)
            *   [11.4.1.1 Brasero](#Brasero)
        *   [11.4.2 KDE](#KDE_4)
            *   [11.4.2.1 K3b](#K3b)
            *   [11.4.2.2 (Todo) cdrecord, graveman...](#.28Todo.29_cdrecord.2C_graveman...)
    *   [11.5 TV-kort](#TV-kort)
    *   [11.6 Digitale kameraer](#Digitale_kameraer)
    *   [11.7 USB-hukommelsessticks og -harddiske](#USB-hukommelsessticks_og_-harddiske)
*   [12 Systemvedligeholdelse](#Systemvedligeholdelse)
    *   [12.1 Pacman](#Pacman)
        *   [12.1.1 Nyttige kommandoer](#Nyttige_kommandoer)
*   [13 Finpudsning og yderligere information](#Finpudsning_og_yderligere_information)
    *   [13.1 Ofte stillede spørgsmål](#Ofte_stillede_sp.C3.B8rgsm.C3.A5l)
    *   [13.2 Terminologi](#Terminologi)

## Forord

### Introduktion

Dette dokument vil guide dig igennem installation og konfiguration af [Arch Linux](/index.php/Arch_Linux_(Dansk) "Arch Linux (Dansk)"); en simpel, letvægts GNU/Linux distribution målrettet erfarne brugere. Denne guide er rettet mod nye brugere af Arch Linux, men tilstræber at være en stærk reference og en basis for indlæring for alle.

**Arch Linux distributions højdepunkter:**

*   [Simpel](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)") design og filosofi
*   [Alle pakker](https://www.archlinux.org/packages/?q=) kompileret til i686- og x86_64-arkitekturene
*   [Rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") model, tillader en engangs installation og problemfri opgradering til seneste stabile installerede software
*   [BSD stil](/index.php?title=Arch_Boot_Process_(Dansk)&action=edit&redlink=1 "Arch Boot Process (Dansk) (page does not exist)") opstartsscripts, med en centraliseret konfigurationsfil
*   [mkinitcpio](/index.php/Mkinitcpio_(Dansk) "Mkinitcpio (Dansk)"): En simpel og dynamisk initramfs-skaber
*   [Pacman](/index.php/Pacman_(Dansk) "Pacman (Dansk)") pakkehåndtering er letvægt og hurtigt, med et minimalt hukommelsesforbrug
*   [Arch byggesystem](/index.php/Arch_Build_System_(Dansk) "Arch Build System (Dansk)"): Et _ports_-lignende pakkebygningssystem; giver en simpel metode til at skabe pakker til Arch Linux
*   [Arch brugerpakkelager](/index.php/Arch_User_Repository_(Dansk) "Arch User Repository (Dansk)"): Tilbyder tusindvis af brugerbidragede pakkescripts samt muligheden for at dele dine egne

### Licens

Arch Linux, Pacman, dokumentationen og scripts er copyrightede ©2002-2007 Judd Vinet, ©2007-2011 Aaron Griffin, og er licenserede under [GNU General Public License v2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### Arch principper og filosofi

_**Princippet bag Arch Linux' design er at holde det [enkelt](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)").**_

Bemærk at 'enkelt' i denne kontekst ikke betyder, at det er let eller begyndervenligt, men nærmere at det er uden unødvendige tillæg, ændringer eller komplikationer. Kort sagt er det en elegant og minimalistisk tilnærmelse.

_"Enkelt' defineres ud fra et teknisk standpunkt og ikke i brugsøjemed. Det er bedre at bære teknisk elegant med en højere indlæringskurve, end at være let anvendeligt og teknisk noget juks." -Aaron Griffin_

Occam's barberblad : _Entia non sunt multiplicanda praeter necessitatem_ eller "Entiteten bør ikke multiplikeres unødvendigt." Med udtrykket 'barberblad' menes: Handlingen at barbere unødvendige forudsætninger og komplikationer væk for at opnå den enkleste forklaring, metode eller teori.

*   Du vil måske printe guiden ud (ca. 52 sider). Den kan være nyttig som brugerreference.
*   Hvis du vil føje noget til denne wiki, så inkludér venligst såvel 'hvorfor' som 'hvordan', hvor det er passende. Den bedste dokumentation lærer os både 'hvordan' og 'hvorfor'!

### Alt du vil vide om at installere Arch Linux, men ikke kunne få dig til at spørge om

Formålet med denne guide er, at vise dig, hvordan du opnår et fuldt konfigureret Arch Linux system (grafisk skrivebordsmiljø, afspille DVD, browse internettet, arbejde med e-mail, lytte til musik). Det er umuligt at vise, for ikke at tale om at forudsige, alle muligheder og valg. Denne guide er udformet med fokus på nogle kritiske og brugbare trin. Du vil sikkert søge mere information i [Arch Linux Wiki-en](/index.php/Main_page "Main page") eller på [Arch Linux' Forum](https://bbs.archlinux.org/), der er på engelsk eller det [danske Arch Linux forum](http://forum.archlinux.dk/index.php). Du burde også læse om [Arch-måden](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)"), der forklarer om de grundlæggende principper i Arch Linux.

**Note:** At følge denne guide er essentielt for succesfuldt at installere et rigtigt konfigureret Arch linux system, så læs den <u>venligst</u> igennem før du starter.

Artiklen er delt op i 5 hovedafsnit:

*   [Del I: Forberedelse](#Forberedelse)

*   [Del II: Installation](#Installation)

*   [TRIN 2 - Installation af X og konfiguration af ALSA](/index.php/Dansk_Begynderguide#TRIN_2:_Installation_af_X_og_konfiguration_af_ALSA "Dansk Begynderguide")

*   [TRIN 3 - Installation af dit skrivebord](/index.php/Dansk_Begynderguide#TRIN_3:_Installation_og_konfiguration_af_dit_skrivebord "Dansk Begynderguide")

### DON'T PANIC!

Vær klar over, at Arch Linux' installationprocedure, sikkert er noget forskellig fra de fleste andre GNU/Linux-distributioner, du har prøvet, specielt hvis du er begynder. Systemet i Arch Linux er bygget **af brugeren**, fra installationsprogrammet **ncurses** til et grundsystem med intet andet en en 'bash-skal' og basale systemværktøjer. Fra kommandolinjen tilføjer du pakker fra Arch-kilder med værktøjet [pacman](/index.php/Pacman "Pacman") via din internetforbindelse, indtil systemet er tilpasset dine ønsker og krav. Dette tillader maksimal fleksibilitet, frit valg og kontrol over systemressourcer. Fordi **du** byggede det, vil du ufravigeligt kende 'hver en skrue og møtrik' i dit system, og du bliver fortrolig med, hvad der gemmer sig indeni.

Systemet i Arch Linux konfigureres ved at redigere tekstfiler. Det tilbyder ingen grafiske værktøjer og vil ikke "holde dig i hånden" under opsætning og tilpasning. Det er heller ikke designet til at stille dig hindringer i vejen. Husk også at Arch Linux er rettet mod kompetente brugere af GNU/Linux, ligesom det er rettet mod brugere, der er villige til at investere den fornødne tid til at lære om systemet mekanismer.

_Formålet med Arch Linux' designprincipper er at holde det enkelt._

Bemærk at ordet 'enkelt' i denne kontekst ikke nødvendigvis er ensbetydende med hverken let eller brugervenligt, men nærmere 'uden unødvendige tillæg, ændringer eller komplikationer'. Kort sagt er Arch Linux en elegant og minimalistisk tilnærmelse.

## Forberedelse

**Note:** Hvis du ønsker at installere på en anden partition fra en eksisterende GNU/Linux distribution eller LiveCD, læs [denne wiki-artikel](/index.php/Install_from_Existing_Linux "Install from Existing Linux") for vejledning. Dette kan være brugbart især hvis du ønsker at fjern-installere Arch via [VNC](/index.php/VNC "VNC") eller [SSH](/index.php/SSH "SSH"). Følgende gælder installation på traditionel vis.

### Skaf det seneste installationsmedie

Du kan finde Arch's officielle installationsmedie [her](https://archlinux.org/download/) fra. Denne guide er lavet til version 2011.08.19.

*   Både **Core** og **Netinstall** images indeholder kun de nødvendige pakker for at oprette et **Arch Linux grundsystem**. _Bemærk at grundsystemet ikke inkluderer et GUI. Det indeholder stort set kun GNU-værktøjer (compiler, assembler, linker, libraries, shell og utilities), Linux-kernen, pacman (Arch's pakkemanager) og nogle få ekstra libraries og moduler._
*   **Core** images tilbyder både installation fra CD og net.
*   **Netinstall** images er mindre og indeholder ingen pakker i sig selv; hele systemet hentes via nettet.
*   [Arch64 FAQen](/index.php/Arch64_FAQ "Arch64 FAQ") kan hjælpe dig med at vælge mellem 32- og 64-bit versionerne. **Dual Architecture** image har pakker til begge arkitekturer, så du kan bruge en CD til at installere på både 32- og 64-bit computere.
*   Husk at downloade checksum txt-filerne sammen med den valgte ISO.

Pre-release images er også tilgængelige og kan downloades [her](https://releng.archlinux.org/isos/). **De er ikke-officielle releases og er derfor ikke officielt supporteret.** De bør kun bruges hvis de officielle installations images ikke virker på det nuværende hardware på dit system og du tror at nyere images kan indeholde de nødvendige drivere.

#### Check integriteten af den downloadede fil

`cd` til mappen hvor de downloadede filer er placeret og kør `sha1sum`:

 `$ sha1sum --check name_of_checksum_file.txt` 

Det skulle returnere et "OK" for den du har. (Ignorer øvrige linjer.) Hvis ikke, så download alle filer igen.

md5sum check virker på samme måde.

#### CD installer

Brænd .iso image-filen til en CD- eller DVD-skive med dit foretrukne CD/DVD-brænder-drev og -software og fortsæt med [Boot Arch Linux installer](#Boot_Arch_Linux_installer).

**Note:** Kvaliteten af optiske drev og CD-medier varierer meget. Generelt anbefales det at brænde med langsom hastighed for at få en god brænding; nogle brugere anbefaler hastigheder _**helt ned til 4x eller 2x.**_ Hvis du oplever uventet opførsel fra CD'en, så prøv at brænde ved den mindste hastighed understøttet af dit system.

#### Flash memory device eller USB stick

Se [Installer fra et USB flash drev](/index.php/Install_from_a_USB_flash_drive "Install from a USB flash drive") for mere detaljerede instruktioner.

Denne metode vil virke for en hver type af flashmedie, som din BIOS kan boote fra, det gælder både fra en kortlæser eller en USB-port.

Bemærk at alle data på det flytbare medie vil blive slettet!

##### *nix metode

**Warning:** Vær meget forsigtig med hvor du sender ISO-filen hen, da `dd` uden varsel skrive til den destinition du udpeger, selv hvis det skulle være din harddisk (hvilket kan føre til potentiel data-tab og/eller ødelagt filsystem).

Indsæt en tom eller undværlig flash-enhed, find dens sti og skriv ISO-filen til enheden med `dd`-programmet:

 `# dd if=archlinux-2011.08.19-''{core|netinstall}''-''{i686|x86_64|dual}''.iso of=/dev/sd''x''` 

hvor `if=` er stien til ISO-filen og `of=` er din flash enhed. Sørg for at bruge `/dev/sd**x**` og ikke `/dev/sd**x1**`. Du har brug for en flash-enhed med plads nok til at indeholde image-filen.

For at verificere at image-filen blev rigtig skrevet til flash-enheden, noteres antallet af records (blocks) der er læst ind og skrevet ud og så udfør følgende check:

 `# dd if=/dev/sd''x'' count=''number_of_records'' status=noxfer | md5sum` 

Den md5sum der returneres skal matche [md5sum'en fra den downloadede archlinux image-fil (2011.08.19)](https://www.archlinux.org/iso/2011.08.19/md5sums.txt); de skal begge matche md5sum'en for image-filen, som er listet i md5sum-filen på mirror-distribution-sitet. En typisk kørsel vil se sådan ud:

Skriv ISO-filen til drevet

 `# dd if=archlinux-2011.08.19-core-i686.iso of=/dev/sdc` 

```
 744973+0 records in
 744973+0 records out
 381426176 bytes (381 MB) copied, 106.611 s, 3.6 MB/s

```

Verificer integriteten:

 `# dd if=/dev/sdc count=744973 status=noxfer | md5sum` 

```
 4850d533ddd343b80507543536258229  -
 744973+0 records in
 744973+0 records out
```

Forstæt med [Boot Arch Linux installer](#Boot_Arch_Linux_installer)

##### Microsoft Windows metode

Download Disk Imager fra [here](https://launchpad.net/win32-image-writer/+download). Indsæt flash-medie. Start Disk Imager og vælg image-filen (Disk Imager accepterer kun *.img filer, så du er nødt til at skrive "*.iso" i file open dialogen for at vælge Arch snapshot). Vælg drev-bogstavet der er associeret med flash-drevet. Klik "Write".

Der er også andre løsninger til at [skrive bootable ISO-filer til USB-sticks](/index.php/Install_from_a_USB_flash_drive#On_Windows "Install from a USB flash drive"). Hvis du har problemer med USB-sticks der disconnecter, så prøv med en anden USB-port og/eller kabel.

Forstæt med [Boot Arch Linux installer](#Boot_Arch_Linux_installer).

#### Installer over netværket

Istedet for at skrive boot-mediet til en disk eller USB-drev, kan du boote ISO-filen over netværket. Det virker godt hvis du allerede har en server sat op. Læs [denne artikkel](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") for mere information og så fortsæt til [Boot Arch Linux installer](#Boot_Arch_Linux_installer).

#### Installer på en virtuel maskine

At installere på en [virtuel maskine](https://en.wikipedia.org/wiki/Virtual_machine "wikipedia:Virtual machine") er en god måde at stifte bekendtskab med Arch Linux og dens installationsprocedure og samtidig bevare dit nuværende operativsystem og slippe for at repartitionere harddisken. Det gør det også muligt at du kan have denne Beginners' Guide åben i din browser gennem hele installationen. Nogle brugere ser det som en fordel, at have et uafhængigt Arch Linux system på et virtuelt drev, til at teste på.

Eksempler på virtualiseringssoftware er [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

Den nøjagtige metode til at forberede en virtuel maskine afhænger af softwaren, men følger generelt disse trin:

1.  Opret det virtuelle-disk-image som skal indeholde operativsystemet.
2.  Configurer parameterne til den virtuelle maskine.
3.  Boot den downloadede ISO-fil på et virtuelt CD-drev.
4.  Fortsæt med [Boot Arch Linux installer](#Boot_Arch_Linux_installer).

Følgende artikler kan være nyttige:

*   [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Installing Arch Linux in VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")

### Boot Arch Linux installer

**Tip:** Kravene til hukommelse på et basis-system er 64MB RAM.

**Tip:** Under processen kan den automatiske skærm-blanker blive aktiveret. Hvis det sker, kan man trykke på Alt-knappen for at få skærmbilledet frem igen.

#### Boot fra mediet

Indsæt CD- eller flash-mediet du har forberedt og boot fra den. Måske er du nødt til at ændre boot-rækkefølgen i din computers BIOS. For at gøre det, skal du trykke på en knap (typisk `Delete`, `F1`, `F2`, `F11` or `F12`) under POST (Power On Self-Test) fasen.

**Main Menu:** Hovedmenuen bør blive vist på dette tidspunkt. Vælg det menupunkt du ønsker, ved at benytte pile-tasterne til at markere det du ønsker og så trykke `Enter`. Menuer kan variere lidt imellem de forskellige ISO-filer.

#### OS system-start

Vælg "Boot Arch Linux" fra hovedmenuen og tryk `Enter` for at starte installationen. Systemet vil nu loade og vise en shell prompt. Du bliver automatisk logget ind som root.

**Note:** Brugere som ønsker at lave en Arch Linux installation remotely via en [SSH](/index.php/SSH "SSH") forbindelse opfordres til at lave nogle små ændringer på dette tidspunkt for at tillade SSH-forbindelser direkte til live CD-miljøet. Hvis det har interesse, så læs artiklen [Install from SSH](/index.php/Install_from_SSH "Install from SSH").

##### Troubleshooting boot-problemer

Hvis du bruger Intel video chipset og skærmen bliver blank under processen, skyldes det sandsynligvis et problem med kerne-mode-settings. En mulig løsning kan opnåes ved at reboote og trykke `Tab` ved GRUB-menuen for at komme til kerne-options. I slutningen af kerne-linjen, tilføjes følgende:

```
i915.modeset=0

```

Alternativt, tilføj:

```
video=SVIDEO-1:d

```

som (hvis det virker) ikke disabler kerne-mode-settings.

Se [Intel](/index.php/Intel "Intel")-artiklen for mere information.

Hvis skærmen _ikke_ bliver blank og boot-processen hænger når den prøver at loade kernen, tryk `Tab` for at ændre i kerne-linjen og tilføj følgende:

```
acpi=off

```

Når du har lavet ændringer i en kommando-linje, skal du simpelthen trykke `Enter` for at boote med ændringerne.

#### Skift keymap

Hvis du har et ikke-US keyboard kan du selv vælge at din keymap/console font med kommandoen:

 `# km` 

eller brug loadkeys-kommandoen:

 `# loadkeys _layout_` 

hvor _layout_ er dit keyboard-layout, som f.eks. `fr` or `be-latin1`

#### Dokumentation

Den officielle installations-guide (som er et andet dokument end denne uofficielle begynder-guide) er tilgængelig på live-systemet. For at tilgå den, skal du skifte til tty2 (virtuel-konsol #2) ved at trykke `Alt+F2` og logge ind som root. Her kan du bruge `less` til at bladre igennem dokumentet:

 `# less /usr/share/aif/docs/official_installation_guide_en` 

Skift tilbage til tty1 med `Alt+F1` for at følge resten af installtionsprocessen. Nu kan du til hver en tid skifte tilbage til tty2 hvis du har brug for at kigge i den officielle guide, efterhånden som du kommer igennem installtionsprocessen.

**Tip:** Læg venligst mærke til at den officielle guide kun dækker installation og configuration af basis-systemet. Når det er installeret anbefales det kraftigt at læse wikien for finde oplysninger omkring post-installation og andre lignende ting.

## Installation

**Note:** Hvis du tilgår internettet gennem en HTTP og/eller FTP proxy _og_ bruger DHCP til at configurere dit netkort, skal du måske sætte environment variables `http_proxy` og/eller `ftp_proxy` i shellen før du kører `/arch/setup` som vist nedensfor:

```
export http_proxy=http://<http_proxy_address>:<proxy_port>
export ftp_proxy=ftp://<ftp_proxy_address>:<proxy_port>
```

Som root køres installer-scriptet fra tty1:

 `# /arch/setup` 

Det næste du skulle se er Arch Installations-skærmbilledet.

### Vælg en installationskilde

Efter en Velkommen-skærm, bliver du bedt om at vælge installationskilde.

Select Source dialogen beder dig vælge hvilke [repositories](/index.php/Official_repositories "Official repositories") du ønsker at bruge.

Netinstall

Hvis du bruger Netinstall image, vil du udelukkende være i stand til at vælge **remote** repositories.

Core

Hvis du har valgt Core installer og ønsker at bruge pakkerne på CD'en, vælges **core-local**.

**Warning:** Du kan også vælge flere **remote** repositories, men bemærk beskeden fra installeren: "DO NOT combine a local repository with remote mirrors unless you know what you're doing (this will cause BROKEN packages)!" - altså lad være med at vælge både pakker fra CD og fra nettet, med mindre du ved hvad du gør.

Hvis du er i tvivl om hvilken du skal vælge, så vælg 'extra' and '[community](/index.php/Community "Community")' sammen med 'core'. Hvis du installerer en 64-bit Arch, bør du også vælge '[multilib](/index.php/Multilib "Multilib")'. Disse indstillinger vælges for systemet senere i installationsprocessen.

**Warning:** Det forventes at du læser [arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public) mailinglisten hvis du bruger testing repositories. Du bør vide hvordan man laver [downgrade packages](/index.php/Downgrade_packages "Downgrade packages") og [chroot](/index.php/Chroot "Chroot") ind i din Arch installation for reparere hvis noget ikke virker.

#### Netværks-setup

**Note:** ftp.archlinux.org er neddroslet til 50KB/s.

Du får en liste over yderligere FTP-og HTTP-mirrors.

**Tip:** For at opnå højest download-hastighed bør du vælge et mirror i dit eget land og som er hostet af nogen du ved er pålidelige (f.eks. universiteter). Den relative hastighed samt opdateringsstatus af source repository mirrors kan checkes [her](https://www.archlinux.org/mirrors/status/).

Hvis du valgte **core-local** og samtidig **remote** repositories, vil du nu få muligheden for at vælge enten kun at gå til remote sources hvis den ønskede pakke ikke er tilgængelig lokalt, eller omvendt.

På den næste skærm vælges _Yes_ til at sætte netværket op. Du får tilbudt selv at indlæse netkortsdrivere manuelt hvis du ønsker det. UDev er ganske effektiv til at indlæse de nødvendige moduler, så du kan gå ud fra at det allerede er i orden. Du kan verificere det ved at trykke `Alt+F3` og skrive `ip addr`. Når du er færdig returnerer du til tty1 ved at trykke `Alt+F1`.

Tilgængelige netkort vil blive vist. Hvis et netkort og HWaddr (**H**ard**W**are **addr**ess) vises, så er de rette moduler allerede indlæst. Hvis dit netkort ikke vises, kan installeren søge efter det eller du kan gøre det manuelt fra en anden konsol. Vælg dit netkort for at fortsætte.

Installeren spørger så om du ønsker at benytte DHCP. Vælger du "Yes" vil den køre `dhcpcd` for at finde en tilgængelige gateway og efterspørger en IP-adresse; vælger du "No", bliver du bedt om at indtaste en statisk IP-adress, netmaske, broadcast (valgfri), gateway, DNS server, HTTP proxy (valgfri), og FTP proxy (valgfri).

Efterfølgende vil du returneres til hovedmenuen _Main Menu_

##### Setup ADSL bridging i live-miljøet (valgfri)

(Hvis du har et modem eller en router i bridge mode til at forbinde til din ISP (=internetudbyder))

Skift til en anden virtuel konsol (`Alt+F2`), login som root og skriv:

 `# pppoe-setup` 

Hvis alt er rigtigt konfigureret vil du, når den er færdig, kunne forbinde til din ISP med:

 `# pppoe-start` 

Returner til den første virtuelle konsol (`Alt+F1`) og fortsæt med [Vælg editor](#V.C3.A6lg_editor).

##### Setup af trådløs i live-miljøet (valgfri)

(Hvis du har brug for trådløs forbindelse under installationsprocessen)

De trådløse drivere og værktøjer er nu tilgængelige i live-miljøet på installationesmediet. Et godt kendskab til dit trådløse hardware er vigtigt for at opnå en successfuld konfiguration. Bemærk at følgende quick-start procedure _udført på dette tidspunkt i installationen_ vil aktivere dit trådløse hardware til brug _i live-miljøet på installationsmediet_. Disse trin (eller en anden form for aktivering af trådløst udstyr **skal gentages i det egentlige installerede system efter at du er bootet til det**.

Bemærk også at disse trin er valgfrie hvis du ikke er afhængig af trådløs forbindelse på dette sted i installationen; trådløs adgang kan også aktiveres senere.

**Note:** De følgende eksempler benytter `wlan0` trådløs interface og `linksys` som ESSID. Husk at ændre disse værdier, så de svarer til dit setup.

Proceduren er som følger:

*   Skift til en ledig virtuel konsol, f.eks. `Alt+F3`
*   Login som root
*   (valgfri) Identificer det trådløse interface:

 `# lspci | grep -i net` 

*   Sikr dig at udev har indlæst driveren og at driveren har oprettet et brugbart trådløs-kerne-interface med `/usr/sbin/iwconfig`:

 `# iwconfig` 

```
 lo no wireless extensions.
 eth0 no wireless extensions.
 wlan0    unassociated  ESSID:""
          Mode:Managed  Channel=0  Access Point: Not-Associated
          Bit Rate:0 kb/s   Tx-Power=20 dBm   Sensitivity=8/0
          Retry limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

`wlan0` er det tilgængelige trådløse interface i dette eksempel.

**Note:** Hvis du ikke ser et output svarende til dette, er den trådløse driver ikke indlæst. Hvis det er tilfældet, må du indlæse driveren selv. Se [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") for mere detaljeret information.

*   Aktiver interfacet med:

 `# ip link set wlan0 up` 

En lille procentdel at trådløse chipsæt kræver også firmware sammen med den tilsvarende driver. Hvis det trådløse chipsæt kræver firmware, får du sandsynligvis denne fejl når du prøver at aktivere interfacet:

 `# ip link set wlan0 up`  `SIOCSIFFLAGS: No such file or directory` 

Hvis du ikke er sikker, kør kommandoen `/usr/bin/dmesg` for at se i kerne-loggen efter en firmware-forespørgsel fra det trådløse chipsæt. Her er et eksempel på et output fra et Intel chipsæt der kræver og har forespurgt firmware fra kernen under boot:

 `$ dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Hvis der ikke er noget output, kan det sluttes at systemets trådløse chipsæt ikke kræver firmware.

**Note:** Trådløse chipsæt-firmware-pakker (til kort som kræver dem) er pre-installeret under `/lib/firmware` i live-miljøet (på CD/USB sticken) **men skal eksplicit installeres på dit aktuelle system for at det trådløse fungerer efter at du booter på det!** Pakkevalg og installation beskrives senere i denne guide. Husk at installere både dit trådløse modul og firmware ved det trin med pakkevalg! Se [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") hvis du er usikker på om der skal installeres firmware til netop dit chipsæt. Dette er en meget almindelig fejlkilde.

*   Hvis ESSID er glemt eller ukendt, kan du bruge `/sbin/iwlist <interface> scan` for at scanne nærliggende netværk:

 `# iwlist wlan0 scan` 

```
Cell 01 - Address: 04:25:10:6B:7F:9D
                    Channel:2
                    Frequency:2.417 GHz (Channel 2)
                    Quality=31/70  Signal level=-79 dBm  
                    Encryption key:off
                    ESSID:"dlink"
                    Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s
                    Bit Rates:6 Mb/s; 9 Mb/s; 12 Mb/s; 18 Mb/s; 24 Mb/s
                              36 Mb/s; 48 Mb/s; 54 Mb/s

```

*   Hvis du bruger WPA kryptering:

For at bruge WPA kryptering kræves det at nøglen krypteres og gemmes i en fil sammen med ESSID, som skal bruges til at forbinde via `wpa_supplicant`. Derfor kræves et par ekstra trin:

For at gøre det nemt og samtidig bevare originalen, omdøbes originalfilen `wpa_supplicant.conf`:

 `# mv /etc/wpa_supplicant.conf /etc/wpa_supplicant.conf.original` 

Brug `wpa_passphrase` til at kryptere dit trådløse netværksnavn og WPA-nøgle og skrive det til `/etc/wpa_supplicant.conf`.

Følgende eksempel krypterer nøglen "my_secret_passkey" til det trådløse netværk "linksys" og genererer en ny konfigurationsfil (`/etc/wpa_supplicant.conf`) og endelig skrives den krypterede nøgle til filen:

 `# wpa_passphrase linksys "my_secret_passkey" > /etc/wpa_supplicant.conf` 

**Note:** Hvis ovenstående fejler med `bash: event not found` fejlmelding, kan det skyldes at specialtegn (f.eks. `!`) indgår i dit trådløse netværksnavn. Er det tilfældet, kan følgende prøves: `# sh -c 'wpa_passphrase linksys "my_secret_passkey" > /etc/wpa_supplicant.conf'` 

Check [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") for yderligere information og troubleshooting.

**Note:** `/etc/wpa_supplicant.conf` gemmes i almindelig tekstformat. Det er ikke risikabelt i installationsmiljøet, men når du rebooter til dit nye system og reconfigurerer WPA, skal du huske at ændre rettighederne på `/etc/wpa_supplicant.conf` (f.eks. `chmod 0600 /etc/wpa_supplicant.conf` så den kun er læsbar af root).

*   Associér dit trådløse netkort med accesspointet du ønsker at bruge. Proceduren afhænger af hvilken kryptering der bruges (ingen, WEP eller WPA). Du skal kende navnet på det ønskede trådløse netværk (ESSID).

<table class="wikitable">

<tbody>

<tr>

<th>Kryptering</th>

<th>Kommando</th>

</tr>

<tr>

<td>Ingen kryptering</td>

<td>`iwconfig wlan0 essid "linksys"`</td>

</tr>

<tr>

<td>WEP med Hex Key</td>

<td>`iwconfig wlan0 essid "linksys" key "0241baf34c"`</td>

</tr>

<tr>

<td>WEP med ASCII kodeord</td>

<td>`iwconfig wlan0 essid "linksys" key "s:pass1"`</td>

</tr>

<tr>

<td>WPA</td>

<td>`wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant.conf`</td>

</tr>

</tbody>

</table>

**Note:** Netværksforbindelsesprocessen kan automatiseres senere ved at vælge en af Arch's standard netværks-daemons, [netcfg](/index.php/Netcfg "Netcfg"), [wicd](/index.php/Wicd "Wicd") eller en anden netværksmanager du foretrækker.

*   Efter at have brugt den rette metode beskrevet ovenfor, ventes et øjeblik og det kontrolleres om der er skabt forbindelse til accesspunktet før du fortsætter:

 `# iwconfig wlan0` 

Output skal indikere at der er forbindelse til det trådløse netværk.

*   Bed om en IP-adresse med `/sbin/dhcpcd <interface>`, f.eks.:

 `# dhcpcd wlan0` 

*   Endelig, sikr dig at du kan route vha. `/bin/ping`:

 `# ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=49 time=87.7 ms
64 bytes from 74.125.224.146: icmp_req=2 ttl=49 time=87.0 ms
64 bytes from 74.125.224.146: icmp_req=3 ttl=49 time=94.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 87.052/89.812/94.634/3.430 ms

```

Forhåbentlig har du en fungerende netværksforbindelse. For troubleshooting, check den detaljerede side, [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

Returner til tty1 med (`Alt+F1`) og fortsæt med [Set editor](#Set_editor).

### Vælg editor

Nu bliver du spurgt hvilken teksteditor du vil bruge til at rette i konfigurationsfiler. Valget står imellem `nano` eller `vi`. nano anses generelt for at være lettest at bruge for begyndere, da dens opførsel er mere intuitiv og minder om grafiske tekstbehandlere. F.eks. gør piletasterne, backspace og delete-knappen som man må forvente. En menu for de mest almindelig kommandoer vises nederst i vinduet (f.eks. klip er `Ctrl-k`, indsæt er `Ctrl-u`, afslut er `Ctrl-x`). Læs wikisiderne om [Nano](/index.php/Nano "Nano") og [Vi](/index.php/Vi "Vi") for detaljerede oplysninger.

### Indstil klokken

#### Indstil region og tidszone

Vælg din region og tidszone vha. piletasterne eller tast det første bogstav for at springe til den rigtige sektion. Vælg med Enter-knappen.

#### Indstil tid og dato

Indstil hardwareklokkens mode. Hvis dette ikke matcher indstillingen for dine øvrige operativsystemer, vil de overskrive tiden og være skyld i tidsforskydelser.

*   [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") (anbefalet)

**Note:** At du vælger at bruge UTC til hardwaretiden betyder ikke at tiden vises i UTC i softwaren.

*   **localtime** (frarådes) - Bruges default i Windows. Hvis tiden sættes til localtime, vil sommer/vintertid ikke virke i Linux.

**Warning:** Brug af _localtime_ kan føre til flere kendte og uløselige fejl. På trods af det er der ikke planer om at droppe supporten på _localtime_.

**Note:** Alle andre værdier resulterer i at der ikke ændres på hardwaretiden (nyttig for virtualisering).

##### Indstil tiden i et Windows dual boot setup

Hvis du sætter dual-boot med Windows op på dit system, har du to valgmuligheder:

*   Anbefalet: Sæt Arch Linux til UTC og få Windows til også at bruge UTC (Det gøres med en lille hurtig registry-ændring, se [this page](https://help.ubuntu.com/community/UbuntuTime#Make_Windows_use_UTC) for instruktioner). Du skal også sørge for at Windows ikke synkroniserer tiden med internettet, da det igen vil sætte hardwaretiden til _localtime_. Hvis du ønsker en sådan funktionalitet (NTP sync), bør du bruge [ntpd](/index.php/Ntpd "Ntpd") på din Arch Linux installation istedet.

*   Ikke anbefalet: Sæt Arch Linux til _localtime_ og senere (i [Configure the system](#Configure_the_system)) fjernes `hwclock` fra `DAEMONS` arrayet i `/etc/rc.conf` (Windows vil tage sig af korrektioner af hardwaretiden).

### Forbered harddisken

**Warning:** Partitionering af harddisken kan slette data. Du opfordres på det kraftigste til at tage backup af kritiske data.

**Note:** Partitionering kan foretages før påbegyndelse af Arch installationen ved at benytte [GParted](http://gparted.sourceforge.net/download.php) eller andre tilgængelige værktøjer. Hvis installationsdrevet allerede er partitioneret ifølge specifikationerne, fortsæt med [#Mulighed 3: Konfigurer block devices, filsystemer og mountpoints manuelt](#Mulighed_3:_Konfigurer_block_devices.2C_filsystemer_og_mountpoints_manuelt).

Verificer identiteter og layout på den aktuelle disk ved at taste `/sbin/fdisk` med `-l` (lille L).

Åbn en anden konsol (`Alt+F3`) og skriv:

 `# fdisk -l` 

Noter disken(e) og/eller partitionerne der skal bruges til Arch installationen.

Skift tilbage til installationsscriptet med `Alt+F1`.

Vælg menupunktet "Prepare Hard Drive". En liste med fire valgmuligheder præsenteres:

*   **Mulighed 1**: [Auto-Prepare](#Mulighed_1:_Auto_prepare)

Dette vil slette HELE harddiske og partitionere den automatisk . Der er mulighed for nogle ændringer.

*   **Mulighed 2**: [Manually Partition Hard Drives](#Mulighed_2:_Manually_partition_hard_drives)

Anbefalet. Denne mulighed benytter cfdisk og giver den mest robuste og tilpassede partitionering. Efter at partitioneringen er færdig, fortsættes til Mulighed 3.

*   **Mulighed 3**: [Manually configure block devices, filesystems and mountpoints](#Mulighed_3:_Manually_configure_block_devices.2C_filesystems_and_mountpoints)

Du kan springe direkte til denne mulighed hvis din harddisk allerede er partitioneret som du øsnker. Mulighed 3 er også næste trin forberedelse af disken. Systemet vil liste de filsystemer og monteringspunkter det har fundet og spørge om du ønsker at bruge dem. Du får mulighed for at vælge hvordan du ønsker at identificere monteringspunkterne, f.eks. ved dev, label eller uuid.

*   **Mulighed 4**: Rollback last filesystem changes

Vend tilbage til foregående ændringer.

Mulighed 1, 2 og 3 forklares i flere detaljer nedenfor. For at forstå hvad valgene indebærer, præsenteres en kort gennemgang af Linux-partitioneringer og filsystemer. Advanced GNU/Linux-brugere som er godt bekendt med manuelt at partitionere en disk kan springe ned til [Select packages](#Select_packages) nedenfor.

**Note:** Hvis du installerer på en USB-nøgle, se [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").

#### Partitionering af hardiske: Generel information

##### Partition-type

Partitionering af en harddisk definerer et specifikt område på disken. Disse kaldes partitioner. Hver partition opfører sig som en separat disk og formateres med et bestemt filsystem (se nedenfor).

Der er 3 typer af disk-partitioner:

*   Primær
*   Udvidet
    *   Logisk

**Primære** partitioner kan være bootbare og er begrænset af fire partitioner pr. disk eller RAID. Hvis det er påkrævet med mere end fire partitioner, bruges en **udvidet** partition indeholdende **logiske** partitioner. Man kan tænke på udvidede partitioner som "containers" for logiske partitioner. En harddisk kan kun indeholde én udvidet partition. En udvidet partition tæller også som en primær partition, så hvis en disk har en udvidet partition, er det kun muligt at have tre primære partitioner (dvs. tre primære partitioner og en udvidet partition). Antallet af logiske partitioner i en udvidet partition er ubegrænset. Et system som som dual-booter med Windows kræver at Windows ligger på en primær partition.

Den sædvanlige nummerering er at oprette primære partitioner `sda1` til `sda3` efterfulgt af en udvidet partition `sda4`. De logiske partitioner på `sda4` nummereres `sda5`, `sda6`, osv.

##### Swap partition

En swap partition er et område på disken, som bruges som virtual RAM. Dette tillader kernen at tilgå data på disken, som ikke kan være i den fysiske RAM.

Historisk er det en tommelfingerregel at størrelsen af en swap partition er dobbelt så stor som den fysiske RAM. Efterhånden som computere har fået mere hukommelseskapacitet gælder denne regel ikke mere. På maskiner med op til 512MB RAM gælder reglen om 2x stadig. Hvis der er RAM nok (mere end 1024MB) kan man godt have en mindre swap partition eller helt udelade den. Med mere en 2GB fysisk RAM, kan man godt forvente god performance uden en swap partition. Det er altid muligt at oprette en [swap fil](/index.php/HOW_TO:_Create_swap_file "HOW TO: Create swap file") efter at systemet er sat op.

**Note:** Hvis du bruger suspend-to-disk (hibernate), er det påkrævet med en swap partition som er mindst **lig med** størrelsen af fysisk RAM. Nogle Arch-brugere anbefaler endda at man laver den 10-15% større end den fysiske RAM, så der er plads til nogle bad sectors.

##### Valg af partitionering

Der er ingen faste regler for partitionering af en harddisk, selvom man godt kan bruge nedenstående generelle råd. En diskpartitionering afgøres af forskellige ting, såsom fleksibilitet, hastighed, sikkerhed og begrænsninger af diskplads. I bund og grund er det et spørgsmål om personlige preferencer. To simple muligheder er: i) en partition til root og en til swap eller ii) bare en root partition uden swap. Læs følgende diskussion og eksempler for at forstå fordele og ulemper ved de forskellige beslutninger. Hvis du vil lave dual boot med Arch Linux og Windows, læs [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot").

Følgende monteringspunkter er mulige valg til separate partitioner:

`/` (root)

root-biblioteket/mappen er toppen af hierarkiet, stedet hvor det primære filsystem monteres og hvorfra alle andre filsystemer stammer. Alle filer og mapper ligger under root-mappen _`/`_, også selvom de er gemt på forskellige fysiske drev. Indholdet af root-filsystemet skal være tilstrækkelig til at boote, genskabe og/eller reparere systemet. Derfor er det ikke alle mapper under _`/`_ , som kan ligge på separate partitioner (se nedenstående advarsel).

`/boot`

Denne mappe indeholder kernen og ramdisk-images såvel som bootloader-konfigurationsfilen og bootloader trin. Den indeholder også data, som bruges før kernen begynder at køre bruger-programmer. Dette inkluderer gemte master boot sektorer og sektor-billed-filer. Denne mappe er essentiel for at man kan boot, men den er også unik idet den kan ligge på sin egen partition.

**Warning:** Sammen med `/boot`, er følgende mapper essentielle for at man kan boote: `/bin`, `/etc`, `/lib` og `/sbin`. Ulig `/boot`, kan disse mapper ikke ligge på separate partitioner men skal ligge under **`/`**.

`/home`

Indeholder undermapper for hver systembruger. Den indeholder diverse personlige data og bruger-konfigurationsfiler til applikationer og programmer.

`/tmp`

Mappen er til programmer, som benytter midlertidig lagerplads til filer, som f.eks. _`.lck`_ , som kan bruges til at forhindre flere samtidige brugere af et program. Når programmet afsluttes, slettes _`.lck`_ filen automatisk. Programmer kan ikke antage at filer eller mapper i _`/tmp`_ bliver bevaret imellem at et givet program afvikles. Filer og mapper under _`/tmp`_ vil typisk blive slettet når systemet genstartes.

`/var`

Indeholder forskellige data såsom spool-mapper og filer, log-filer, [pacman](/index.php/Pacman "Pacman")'s cache, [ABS](/index.php/Arch_Build_System "Arch Build System") træet, osv. Mappen er der for at gøre det muligt at mounte _`/usr`_ som read-only. Alt som tidligere lå under _`/usr`_ , som bliver skrevet til under almindelig kørsel (i modsætning til installation og softwarevedligeholdelse) skal ligge under _`/var`_.  

**Note:** `/var` indeholder mange små filer. Ved valget af filsystemtype (se nedenfor) bør man tage højde for det, hvis man ønsker at bruge en separat partition.

Der er flere fordele ved at bruge enkeltvise filsystemer i modsætning til at placere alt i en partition:

*   Sikkerhed: Hvert filsystem kan konfigureres i `/etc/fstab` som 'nosuid', 'nodev', 'noexec', 'readonly', osv.
*   Stabilitet: En bruger eller et fejlbehæftet program kan fylde et helt filsystem med skrammel hvis de har skriverettighed til det. Kritiske programmer, som ligger på et andet filsystem forbliver upåvirket.
*   Hastighed: Et filsystem som der skrives til ofte kan blive fragmenteret. Separate filsystemer forbliver upåvirket og de kan hver især blive defragmenteret. Fragmentering kan undgåes ved at sørge for at hvert filsystem aldrig bliver helt fyldt op.
*   Integritet: Hvis et filsystem bliver ødelagt, forbliver separate filsystemer upåvirkede.
*   Alsidighed: At dele data imellem flere systemer bliver mere smart hvis man bruger uafhængige filsystemer. Man kan også vælge forskellige filsystemtyper afhængig af hvilken type data det er eller hvad de bruges til.

##### Hvor stor bør mine partitioner være?

Størrelsen af partitioner afhænger af personlige preferencer, men følgende information kan være til hjælp:

*   root-filsystemet (`/`) vil indeholde `/usr` mappen, som kan vokse sig meget stor afhængig af mængden af installeret software. 15-20 GB skulle være tilstrækkelig til de fleste brugere med moderne harddiske.

*   `/var` filsystemet vil blandt andre data indeholde [ABS](/index.php/Arch_Build_System "Arch Build System") træet og [pacman](/index.php/Pacman "Pacman") cacheen. At bevare cached pakker er nyttigt, da det giver muligheden for at nedgradere. Af den grund har `/var` tendens til at vokse i størrelse. Især vil pacman cacheen vokse efterhånden som systemet udvides og opdateres. Man kan dog roligt slette det hvis man kommer i pladsmangel. Hvis du bruger en SSD kan det være en god ide at lægge din `/var` på en HDD og beholde `/` og `/home` partitionerne på din SSD for at undgå unødige læsninger/skrivninger på din SSD. 8-12 GB på et desktop system skulle være nok til `/var`, afhængigt af hvor meget software der bliver installeret. Servere har tendens til at have et relativ stort `/var` filsystem.
*   `/home`-filesystemet er typisk stedet hvor brugerdata, downloads og multimedier ligger. På et desktopsystem er `/home` typisk det største filsystem på drevet. Hvis det bliver nødvendigt at reinstallere Arch, vil alle data på `/home` partitionen blive bevaret hvis det sættes op på sin egen partition.
*   En `/boot`-partition kræver kun ca. 100MB.
*   Hvis det er tilgængeligt vil yderligere 25% diskplads til hvert filsystem give en god elastik til fremtidige udvidelser og hjælpe på at disken bliver for fragmenteret.

#### Oprettelse af filsystemer: Generel information

##### Filesystem-typer

Individuelle drev-partitioner kan sættes op med et af de mange tilgængelige filsystemer. De har hver deres fordele, ulemper og unikke egenskaber. En kort oversigt over filsystemer følger; linkene er til wikipedia, som giver meget mere information.

1.  [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") **Second Extended Filesystem** er et etableret, modent GNU/Linux filsystem som er meget stabilt. En ulempe er at det ikke har journaliseringsunderstøttelse (se nedenfor) eller barrierer. Mangel på journalisering kan resultere i tab af data i tilfælde af strømafbrydelse eller systemnedbrud. Det kan også være uhensigtsmæssigt til root (`/`) og `/home` partitioner da filsystem-check kan tage lang tid. Et ext2-filsystem kan konverteres til ext3.
2.  [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") **Third Extended Filesystem** er i bund og grund ext2-systemet med journaliseringsunderstøttelse og skrive-barrierer. Det er bagudkompatibelt med ext2, godt testet og ekstremt stabilt.
3.  [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") **Fourth Extended Filesystem** er et nyere filsystem, som også er kompatibelt med ext2 og ext3\. Det giver support for drev-størrelser op til 1 exabyte (dvs. 1,048,576 terabytes) og filstørresler op til 16 terabytes. Den øger grænsen på 32.000 undermapper for ext3 til 64.000\. Den har også mulighed for online defragmentering.
4.  [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") (V3) Hans Reiser's højtydende journaliseringsfilsystem bruger en meget interessant metode med datagennemgang baseret på en ukonventionel og kreativ algoritme. ReiserFS er kendetegnet ved at være meget hurtigt, især når der er mange små filer invovleret. ReiserFS er hurtig til at formattere, men tilsvarende langsom til at mounte. Ganske moden og stabil. ReiserFS (V3) bliver ikke aktivt udviklet for tiden. Generelt anset for at være et godt valg til `/var`.
5.  [JFS](https://en.wikipedia.org/wiki/JFS_(file_system) "wikipedia:JFS (file system)") IBM's **Journaled File System** var det første filsystem der tilbød journalisering. Det blev udviklet i mange år i IBM AIX® styresystem før det blev overført til GNU/Linux. JFS er det GNU/Linux filsystem der kræver mindst CPU-ressourcer. Det er meget hurtigt til at formatere, mounte og filsystem-check (fsck). JFS tilbyder meget god all-around ydelse især i forbindelse med deadline I/O scheduler. Det er ikke så udbredt som ext-serien eller ReiserFS, men stadig meget modent og stabilt.

    **Note:** JFS filsystemet kan ikke formindskes af disk-værktøjer som f.eks. **gparted** eller **parted magic**.

6.  [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") er endnu et journaliserings filsystem, som oprindeligt udviklet af Silicon Graphics for IRIX operativsystemet og oversat til GNU/Linux. Det leverer meget hurtig adgang til store filer og filsystemer og er meget hurtigt til at formatere og mounte. Sammenlignende benchmark-tests har vist at det er langsommere når det skal håndtere mange små filer. XFS er meget modent og tilbyder online defragmentering.

    **Note:** XFS filsystemet kan ikke formindskes af disk-værktøjer som f.eks. **gparted** eller **parted magic**.

7.  [vfat](https://en.wikipedia.org/wiki/vfat "wikipedia:vfat") eller **Virtual File Allocation Table** er teknisk simpelt og supporteres af stort set alle eksisterende operativsystemer. Det gør det til et brugbart format til solid-state hukommelseskort og en nem måde at dele data mellem operativsystemer. VFAT understøtter lange filnavne.
8.  [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") Også kendt som "Better FS", **Btrfs** er et nyt filsystem med stærke egenskaber som Sun/Oracle's udmærkede [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS"). Disse indbefatter snapshots, multi-disk striping og mirroring (software RAID uden mdadm), checksums, incremental backup, og on-the-fly compression som kan give et signifikant performance boost såvel som spare plads. I skrivende stund, januar 2011, anses Btrfs for at være ustabil selvom det er kommet med i mainline kernen med en eksperimentel status. Btrfs tyder på at blive fremtiden indenfor GNU/Linux filsystemer og tilbydes som root-filsystem i alle større distributioner.

    **Warning:** Btrfs har endnu ikke implementeret et fsck-værktøj. Filsystemet kan ikke repareres hvis der opstår fejl.

9.  [nilfs2](https://en.wikipedia.org/wiki/nilfs "wikipedia:nilfs") **New Implementation of a Log-structured File System** blev udviklet af NTT. Det gemmer alle data i et kontinuert log-lignende format, som kun tilføjer og aldrig overskriver. Det er designet til at reducere søgetid og minimere typen af datatab, som opstår efter at et konventionelt Linux-filsystem går ned.

##### Journalisering

Alle ovenstående filsystemer med undtagelse af ext2 bruger [journalisering](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journalisering giver fejlsikkerhed ved at logge ændringer før de udføres på filsystemet. I tilfælde af systemnedbrud eller strømsvigt er sådanne filsystemer hurtigere online igen og der er mindre sandsynlighed for fejl. Logningen finder sted i et dedikeret område af filsystemet.

Ikke alle journaliseringstekniker er ens. Kun ext3 og ext4 tilbyder data-mode journalisering, som logger både data og metadata. Data-mode journalisering koster noget hastighed og er ikke slået til som standard. De andre filsystemer tilbyder ordered-mode journalisering, som kun logger meta-data. Selvom alle journaliseringssystemer vil returnere et brugbart filsystem efter et nedbrud, vil data-mode give den bedste beskyttelse mod fejl og datatab. Der er dog et konpromis i systemydelse, da data-mode journalisering udfører to skrive-operationer: først til journalen og så til disken. Man bør overveje hvad man vægter af systemhastighed eller datasikkerhed når man vælger filsystemtype.

#### Mulighed 1: Auto prepare

Auto-Prepare sletter hele drevet og inddeler den i følgende fire partitioner:

*   En `/boot` partition formateret med ext2\. Defaultstørreslen på 100MB kan ændres.
*   En `/swap` partition med defaultstørrelse på 256MB (justerbar).
*   Separér `/` og `/home` partitioner med justerbare størrelser og filsystemer. Tilgængelige filsystemer er ext2, ext3, ext4, reiserfs, xfs, jfs, vfat, nilfs2 (experimentel), og btrfs (experimentel). Både `/` og `/home` får samme filsystem-type hvis man vælger Auto Prepare-muligheden.

Vær opmærksom på at Auto Prepare formaterer og sletter hele harddisken. Læs **advarslen** fra installeren meget nøjagtigt og sørg for at det er det rigtige drev der er valgt til at blive partitioneret.

Hvis du ikke ønsker at bruge standard-konfigurationen fra Auto Prepare, kan du manuelt vælge partitioneringen. Dette er f.eks. nødvendigt hvis du konfigurerer et dual-boot system med en eksisterende Windows-partition. Manuel partitionering fåes ved at vælge mulighed Manual partitioning can be accomplished with Option 2 (followed by Option 3) or by using a live media utility such as GParted.

#### Mulighed 2: Manually partition hard drives

Når du vælger disken der manuelt skal partitioneres, åbnes [cfdisk](https://en.wikipedia.org/wiki/cfdisk "wikipedia:cfdisk") (hvis du har et [SSD](/index.php/SSD "SSD") drev er programmer som [gdisk](/index.php/GUID_Partition_Table "GUID Partition Table") eller [GNU Parted](http://www.gnu.org/software/parted/manual/html_mono/parted.html) ønskelige). Virkemåden kan illustreres med et eksempel, hvor der laves fire partitioner til root, var, swap og home på et 160 GB drev. Ifølge ovenstående guidelines, vil eksempel-systemet få en 15GB root (`/`) partition, en 10GB `/var` partition, en 1GB swap partition og en `/home` partition til den resterende diskplads. Det skal atter fremhæves at partitionering er spørgsmål om personligt valg og dette eksempel er kun til illustration.

Vælg **N**ew -> 'Primary' og tast den ønskede størrelse (15.44 GB i dette eksempel) til **root** (`/`) filsystemet. Partitionen vil blive placeret i starten af disken. Vælg **T**ype og gør den til `83 Linux`. Den oprettede `/` partition vil optræde som `sda1`.

På tilsvarende vis oprettes en anden primær partition med en størrelse på 10.256 GB til `/var` med **T**ype `83 Linux`. Den oprettede `/var` partition vil optræde som `sda2`.

Nu oprettes en tredje partition til _swap_. Vælg en passende størrelse (~1 GB her) og vælg **T**ype til `82 (Linux swap / Solaris)`. Den oprettede swap-partition vil optræde som `sda3`.

Den resterende plads bruges til at oprette en fjerde partition til `/home`. Sæt den som primær partition vælg størrelsen. Vælg **T**ype som `83 Linux`. Den oprettede `/home` partition vil optræde som `sda4`.

Dette er som eksemplet vil se ud:

```
Name    Flags     Part Type    FS Type           [Label]         Size (MB)
-------------------------------------------------------------------------
sda1               Primary     Linux                             15440 #root
sda2               Primary     Linux                             10256 #/var
sda3               Primary     Linux swap / Solaris              1024  #swap
sda4               Primary     Linux                             133000 #/home

```

Vælg **W**rite og skriv `yes`. Vær opmærksom på at denne operation kan destruere data på din disk. Vælg **Q**uit for at lade partitionerne være som de var.

Gør dig bekendt med de forskellige filsystemer, som blev diskutteret ovenfor og fortsæt til Mulighed 3.

**Note:** Siden den seneste udvikling af Linux-kernen, som indeholder libata og PATA moduler, er alle IDE, SATA og SCSI drev gået over til navngivningen sd_x_. Det er meningen at det skal være sådan, så det skal ikke vække bekymring.

#### Mulighed 3: Manually configure block devices, filesystems, and mountpoints

Denne mulighed kræver at der allerede eksisterer partitioner (genereret i Mulighed 2 f.eks.) og vises som [dev](https://en.wikipedia.org/wiki//dev "wikipedia:/dev"), label eller [UUID](/index.php/UUID "UUID"). Listen af genkendte partitioner vil blive vist. Hver partition identificeres med et nummer. F.eks. betyder `sda1` den første partition på et drev, mens `sda` betegner hele drevet.

Formater hver partition med det ønskede filsystem og specifiser monteringspunkterne. Du kan vælge en lavel og yderligere options til [mkfs](https://en.wikipedia.org/wiki/mkfs "wikipedia:mkfs").

**Note:** Hvis du ikke har oprettet og ikke ønsker en separat `/boot` partition, kan du roligt ignorere advarslen om at den ikke eksisterer.

Returner til hovedmenuen.

### Vælg pakker

Alle softwarepakker, som er tilgængelige under installation er fra [[core]](/index.php/Official_repositories#core "Official repositories") arkivet. De er yderligere delt i **base** <sup>([i686](https://www.archlinux.org/groups/i686/base/)|[x86_64](https://www.archlinux.org/groups/x86_64/base/))</sup> og **base-devel** <sup>([i686](https://www.archlinux.org/groups/i686/base-devel/)|[x86_64](https://www.archlinux.org/groups/x86_64/base-devel/))</sup> grupper. Pakkeinformation og en kort beskrivelse for [core] kan findes [her](https://www.archlinux.org/packages/?repo=Core&arch=any&arch=i686&arch=x86_64&limit=all&sort=pkgname).

#### Bootloader

Du bliver bedt om at vælge enten [GRUB](/index.php/GRUB "GRUB") eller [syslinux](/index.php/Syslinux "Syslinux") som bootloader.

#### Pakkegrupper

Nu skal du vælge pakkekategori:

**Note:** Af praktiske hensyn er alle pakker i **base** valgt på forhånd. Brug mellemrums-tasten til at vælge eller fravælge pakker.

*   **base:** Softwarepakker fra [core]-arkivet, som giver et minimal basesystem. Vælg altid dette og lad være med at fravælge nogen af dem, da alle pakker i Arch Linux antager at _base_ er installeret.
*   **base-devel:** Ekstra værktøjer fra [core] såsom `make` og `automake`. De fleste nybegyndere bør vælge at installere den, da det sikkert skal bruges til at udvide dit nye system. _base-devel_-gruppen skal bruges for at kunne installere software fra [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Efter valg af kategori vil du få vist en liste af tilgængelige pakker, så du kan finjustere dine valg. Brug mellemrums-tasten til at vælge og fravælge. Hvis du usikker på hvilke yderligere pakker du skal installere på dette tidspunkt, kan du bare springe det over og tilføje dem senere med [pacman](/index.php/Pacman "Pacman").

**Note:** Hvis det er påkrævet at komme på trådløst netværk, husk at installere [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools)-pakken. Nogle trådløse netkort kræver også [**ndiswrapper**](/index.php/Wireless_network_configuration#ndiswrapper "Wireless network configuration") og/eller en specifik [**firmware**](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration"). Hvis du ønsker at bruge WPA kryptering, får du brug for [**wpa_supplicant**](/index.php/WPA_supplicant "WPA supplicant"). På siden [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") vil du finde mere hjælp til at vælge de rigtige pakker til dit trådløse netkort. Du bør også kraftigt overveje at installere **[netcfg](/index.php/Netcfg "Netcfg")**, som bruges til at sætte netværksforbindelsen op og lave profiler når du rebooter til dit nye system.

Efter at have valgt de ønskede pakker, fortsætter du til næste trin, **Installér pakker**.

### Installér pakker

_Install Packages_ vil installere de valgte pakker på dit nye system. Hvis du vælger lokale kilder, vil pakkeversionerne fra CD-ROM/USB blive installeret.

Hvis du valgte fjern-kilder vil du få den nyeste tilgængelige pakke downloadet og installeret af [pacman](/index.php/Pacman "Pacman").

**Note:** Med nogle installere vil du blive spurgt om du ønsker at gemme pakkerne i pacman cachen, som ligger i `/var/cache/pacman/pkg`. Hvis du vælger

"yes", vil du have muligheden for at [downgrade](/index.php/Downgrade "Downgrade") pakker til tidligere versioner. Dette er anbefalet hvis der er tilstrækkelig med diskplads. Med tiden vil

cachen vokse efterhånden som systemet bliver opdateret, men kan tømmes efter behov vha. [pacman](/index.php/Pacman "Pacman")

### Konfigurér systemet

**Tip:** Det er meget vigtigt at følge og forstå disse trin for at sikre et ordentligt konfigureret system.

På dette sted i installationen skal du konfigurere de primære konfigurationsfiler til dit Arch Linux grundsystem.

Du vil blive præsenteret for en menu, som indeholder de vigtigste konfigurationsfiler til dit system.

**Note:** Det er meget vigtigt at rette eller i hvert fald åbne alle konfigurationsfiler. Installer-scriptet har brug for dit input for at oprette disse filer på dit system. Det er en almindelig fejl at springe let hen over dette kritiske trin i konfigurationen.

#### Kan installeren håndtere dette mere automatisk?

At skjule processen med systemkonfiguration er direkte i strid med **[The Arch Way](/index.php/The_Arch_Way "The Arch Way")**. Selvom det er sandt at de seneste versioner af kernen og

hardware-registrerings-værktøjer yder god hardwaresupport og auto-konfiguration, vil Arch vise brugeren alle vigtige konfigurationsfiler under installationen

af hensyn til _gennemsigtighed og system resource kontrol_. Når du er færdig med at modificere disse filer, vil du have lært den simple måde man manuelt

konfigurerer Arch Linux systemet og blevet mere bekendt med grundsystemet, så du er bedre rustet til produktivt at vedligeholde din nye installation.

#### /etc/rc.conf

Arch Linux bruger filen `/etc/rc.conf` som hovedlokation til systemkonfiguration. Denne ene fil indeholder en bred vifte af konfigurationsinformationer,

såsom tidszone, keymap, kernemoduler, netværk og startup daemons. Den indeholder også indstillinger, som bruges af forskellige `/etc/rc*` filer.

##### Sektionen LOCALIZATION

LOCALE

Dette indstiller dit lokationsmiljø, som vil blive brugt af alle programmer og værktøjer der benytter i18n. Du kan få en liste med tilgængelige

værdier ved at køre `locale -a` fra kommandolinjen. Denne default er typisk fin for engelske brugere. Hvis du oplever problemer som at alfanummeriske

tegn erstattes af firkanter, skal du evt. ændre "en_US.UTF-8" til "en_US". (Til dansk vælges "da_DK").

DAEMON_LOCALE

Sættes til _yes_ for at bruge daemon locale med environmentvariablen $LOCALE. Sættes til _no_ for at bruge C locale (default).

HARDWARECLOCK

Specifiserer om hardwareklokken, som synkroniseres ved opstart og nedlukning, skal gemme **UTC** tid eller **local time**. Se [[#Set

clock|Indstil klokken]].

TIMEZONE

Specifiser din tidszone. (Alle tilgængelige zoner findes under `/usr/share/zoneinfo/`).

KEYMAP

De tilgængelige keymaps er i `/usr/share/kbd/keymaps`. Bemærk at denne indstilling kun gælder for dine TTY'ere, ikke for nogen grafisk

windowsmanager eller **X**.

CONSOLEFONT 

Tilgængelige alternative konsolfonte ligger i `/usr/share/kbd/consolefonts/`. Default (blank) er god.

CONSOLEMAP 

Definerer konsoloversigten, som indlæses med setfont-programmet ved boot. Mulige værdier findes i `/usr/share/kbd/consoletrans`.

Default (blank) er god.

USECOLOR 

Vælg "yes" hvis du har en farveskærm og ønsker at bruge farver i konsolen.

**Eksempel på LOCALIZATION:**

```
LOCALE="en_US.utf8"
DAEMON_LOCALE="no"
HARDWARECLOCK="UTC"
TIMEZONE="US/Eastern"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

```

##### Sektionen HARDWARE

MODULES 

Hvis du kender til et modul der mangler, kan det tilføjes her. F.eks. hvis du vil bruge loopback filsystemer, tilføjes "loop".

**Note:** Normalt indlæses alle nødvendige moduler af udev, så det er sjældent nødvendigt at tilføje noget her.

**Eksempel på HARDWARE:**

```
# Scan hardware and load required modules at boot
MODULES=()

```

##### Sektionen NETWORKING

HOSTNAME

Sæt hostnavnet som du ønsker. Dette er din computers navn. Det du skriver her, vil blive indsat i `/etc/hosts`.

**Eksempel:**

```
HOSTNAME="arch"

```

interface

Vælg det netkort du ønsker at bruge til at forbinde til netværket.

address

Hvis du ønsker at bruge en statisk IP til din computer, kan det specifiseres her. **Lad det være blank for DHCP.**

netmask

Valgfri, default er _255.255.255.0_. Hvis du øsnker en selvvalgt netmaske, skrives den her. **Lad det være blank for DHCP.**

broadcast

Valgfri. Hvis du øsnker en selvvalgt broadcast adresse, skrives den her. **Lad det være blank for DHCP.**

gateway

Hvis du øsnker en statisk IP i "address", skrives IP adressen til default gateway (f.eks. dot modem/router) her. **Lad det være blank for**

DHCP.

NETWORK_PERSIST 

Sættes denne til "yes" vil resultere i at brugere der er logget ind via ssh, vil blive logget pænt af hvis maskinen bliver genstartet

eller slukket. Dette er krævet hvis root-drevet er på NFS.

NETWORKS

Dette er en valgfri indstilling, som kun skal bruges hvis du bruger [netcfg](/index.php/Netcfg "Netcfg") pakken evt med pakken _dialog_. Den slår disse netcfg-profiler

til ved boot-op. Det er nyttigt hvis du har brug for mere avancerede netværksfunktioner end den simple netværksservice tilbyder, som f.eks. flere

netværkskonfigurationer (typisk brugt til bærbare).

**Eksempel med statisk IP:**

```
HOSTNAME="arch"
interface=eth0
address=192.168.1.100
netmask=255.255.255.0
broadcast=192.168.1.255
gateway=192.168.1.1
#NETWORKS=(main)
```

**Eksempel med dynamisk IP (DHCP):**

```
HOSTNAME="arch"
interface=eth0
address=
netmask=
broadcast=
gateway=
#NETWORKS=(main)
```

**Andre noter**

Hvis du bruger statisk IP, skal du redigere `/etc/resolv.conf` for at specificere de ønskede DNS servere. Se [afsnittet nedenfor](#.2Fetc.2Fresolv.conf)

angånede denne fil.

**Note:** For automatisk at slutte til et trådløst netværk, kræver et par trin mere og det kan blive nødvendigt at sætte en netværksmanager op som f.eks. [netcfg](/index.php/Netcfg "Netcfg") eller [wicd](/index.php/Wicd "Wicd"). Læs siden [Wireless Setup](/index.php/Wireless_network_configuration#Part_II:_Wireless_management "Wireless network configuration") for mere information.

**Tip:** Hvis du bruger en ikke-standard MTU-størrelse (a.k.a. jumbo frames) OG maskinens hardware understøtter det, se [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames") wiki-artikkel for yderligere konfiguration.

##### Sektionen DAEMONS

Denne liste indeholder simpelthen navnene på scripts der ligger i `/etc/rc.d/`, som skal startes under boot-processen og rækkefølgen de skal startes.

Asynkron initialisering ved at køre dem i baggrunden er også understøttet og nyttigt for at forkorte bootning:

```
DAEMONS=(network @syslog-ng netfs @crond)

```

*   Hvis et scriptnavn startes med et udråbstegn (!), bliver den ikke kørt.
*   Hvis et scriptnavn startes med et "at" symbol (@), skal det køres i baggrunden; startup-sekvensen venter ikke på den afslutter med success før

den starter den næste. (Brugbart til at forkorte bootning). Lad være med at sætte daemons i baggrunden, som skal bruges af andre daemons. F.eks. afhænger

"mpd" af "network", derfor kan det få mpd til at fejle hvis network startes i baggrunden.

*   Ret i listen hvis du installerer nye services, som du ønsker bliver startet automatisk under bootning.

**Note:** Denne "BSD-style" init, er Arch's måde at håndtere hvad andre distributioner håndterer med diverse symlinks til en /etc/init.d/-mappe.

###### Generel information

Linjen med [daemons](/index.php/Daemons "Daemons") behøver ikke blive redigeret på dette tidspunkt, men det er nyttigt at forklare hvad daemons er, da de bliver nævnt igen senere i

denne guide.

En [daemon](https://en.wikipedia.org/wiki/Daemon_(computing) "wikipedia:Daemon (computing)") er et program, som kører i baggrunden og venter på bestemte begivenheder og reagerer på disse. Et godt eksempel er

en webserver der venter på en forespørgsel på en hjemmeside (f.eks. httpd) eller en SSH-server venter på et brugerlogin (f.eks. sshd). Disse er fuldstændige

programmer, men der er også daemons hvis opgave ikke er helt så synlige. Eksempler er daemons som skriver beskeder i en logfil (f.eks. syslog eller metalog)

eller en daemon som giver en grafisk loginskærm (f.eks. gdm eller kdm). Alle disse programmer kan tilføjes i daemons-linjen og vil blive startet når systemet

booter. Nyttige daemons bliver præsenteret i løbet af denne guide.

**Tip:** Alle Arch daemon-scripts ligger under /etc/rc.d/

#### /etc/fstab

Filen [fstab](https://en.wikipedia.org/wiki/fstab "wikipedia:fstab") (for **f**ile **s**ystems **tab**le) er en del af systemkonfigurationen, der viser en liste over alle tilgængelige diske og partitioner, og samtidig indikerer den, hvordan disse skal initialiseres og på anden måde integreres i filsystemet i systemet. Filen `/etc/fstab` bruges almindeligvis af monteringskommandoen **mount**. Mount kommandoen tager filsystemet på en partition/drev og tilføjer det til hovedsystemet, som du ser når du bruger systemet. **mount -a** kaldes fra `/etc/rc.sysinit`, omkring 3/4 inde i boot-processen og læser `/etc/fstab` for at se hvilke options der skal bruges ved montering. Hvis der står **noauto** ved et filsystem i `/etc/fstab`, vil **mount -a** ikke montere den ved boot.

_Et eksempel på en `/etc/fstab`_

```
# <file system>                            <dir>     <type>  <options>            <dump> <pass>
tmpfs                                      /tmp      tmpfs   nodev,nosuid         0      0
UUID=0ddfbb25-9b00-4143-b458-bc0c45de47a0  /         ext4    defaults             0      1
UUID=da6e64c6-f524-4978-971e-a3f5bd3c2c7b  /var      ext4    defaults             0      2
UUID=440b5c2d-9926-49ae-80fd-8d4b129f330b  none      swap    defaults             0      0
UUID=95783956-c4c6-4fe7-9de6-1883a92c2cc8  /home     ext4    defaults             0      2

```

**Note:** Læs [fstab-artikel](/index.php/Fstab "Fstab") for mere information og performance-indstillinger som f.eks. "noatime" eller "relatime".

<file system>

Beskriver en block-device eller fjern-filsystem der skal monteres. Ved almindelige mounteringer vil dette felt indeholde et link til et blok-device-punkt (som oprettes af mknod der bliver kaldt af udev under boot) for det device der skal monteres; for eksempel, `/dev/cdrom` eller `/dev/sda1`.

**Note:** Hvis dit system har mere end en harddisk, vil installeren bruge UUID frem for sd_x_-navngivningen, for at opnå en konsistent mapning. **[Brugen af UUID](/index.php/Persistent_block_device_naming "Persistent block device naming") har flere fordele og bør bruges for at undgå problemer hvis der tilføjes en harddisk på et senere tidspunkt.** Pga. aktiv udvikling af kernen og udev, kan den rækkefølge driverne til disk-kontrollerne indlæses ændres og resultere i et system der ikke kan boote/kernel panic. Nærmest alle bundkort har flere controllere (onboard SATA, onboard IDE) og pga. den omtalte udvikling kan `/dev/sda` blive til `/dev/sdb` ved næste reboot. For mere information, se [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

<dir>

Beskriver monteringspunktet for filsystemet. For swap-partitionen skal der i dette felt stå 'none'; (Swap partitioner bliver faktisk ikke monteret.)

<type>

Beskriver typen af filsystemet. Linux-kernen understøtter mange filsystem-typer. (For at se hvilke filsystemer der er understøttet af den kerne der kører i øjeblikket, se `/proc/filesystems`). Hvis der står 'swap' betegner det en fil eller partition som bruges til swapping. Hvis der står 'ignore' vil linjen bliver ignoreret. Det er nyttigt hvis man vil vise de partitioner der ikke bruges i øjeblikket.

<options>

Beskriver de options der er forbundet med filsystemet. Det formateres som en komma separeret liste uden mellemrum. Den indeholder som minimum monteringstypen plus et antal yderligere options passende til den type filsystem. For dokumentation på mulige options på ikke-nfs filsystemer, læs mount(8).

<dump>

Bruges af dump(8) kommandoen til at afgøre hvilket filsystem der skal droppes. dump er et backup-værktøj. Hvis det femte felt ikke er der, returneres værdien nul og dump vil antage at filsystemet ikke skal backes up. _Bemærk at dump ikke installeres pr. default._

<pass>

Bruges af programmet fsck(8) til at afgøre rækkefølgen af filsystem-check under boot. root-filsystemet bør have den højeste prioritet med <pass> på 1 og andre filsystemer du ønsker checket bør have en <pass> på 2\. Filsystemer med <pass> på 0 vil ikke blive checket. Filsystemer på et drev bliver checket i rækkefølge, men filsystemer på forskellige drev bliver checket samtidigt ved at bruge den parallellitet der er tilgængelig i hardwaren. Hvis det sjette felt ikke er tilstede eller er nul returnerer et nul og fsck vil antage at filsystemet ikke behøver blive checket.

*   For mere information, se [fstab](/index.php/Fstab "Fstab").

#### /etc/mkinitcpio.conf

**Note:** De fleste brugere vil ikke have brug for at rette i denne fil på dette tidspunkt, men læs venligst følgende forklarende information.

Denne fil tillader yderligere fin-justeringer, via [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), af det initerende ram-filsystem eller initramfs (historisk også kaldt initial ramdisk eller "initrd"). initramfs er et gzipped image som læses af kernen under boot. Formålet med initramfs er at bootstrappe systemet, så det får adgang til root filsystemet. Det betyder at den må loade alle moduler der skal bruges til IDE-, SCSI- eller SATA-drev (eller USB/FW hvis du booter fra et USB/FW-drev). Når initramfs har indlæst de rigtige moduler, enten manuelt eller gennem udev, overgives kontrollen til kernen og din boot fortsætter. Derfor er det nok for initramfs at indlæse de moduler der skal til for at få adgang til root filsystemet. Den behøver ikke alle de moduler du kunne tænkes at få brug for på et eller andet tidspunkt. Størstedelen af de almindelige kernemoduler indlæses af udev lidt senere ved init-processen.

**mkinitcpio** er den nye generation af **initramfs creation**. Den har mange fordele i forhold til den gamle **mkinitrd** og **mkinitramfs** scripts.

*   Den bruger **glibc** og **busybox** til at tilbyde en lille og letvægts base til tidlig userspace.
*   Den kan bruge **udev** til hardware autodetektering under afvikling og undgår på den måde at indlæse en masse unødvendigte moduler.
*   Dens hook-baserede init script kan nemt udvides med selvvalgte hooks, som nemt kan inkluderes i pacman uden at skulle ændre selve mkinitcpio.
*   Den understøtter allerede **lvm2**, **dm-crypt** for både legacy og luks volumes, **raid**, **swsusp** og **TuxOnIce** resuming og booting fra **usb mass storage** drev.
*   Mange features kan konfigureres fra kerne-kommando-linjen uden at skulle rekompilere.
*   **mkinitcpio** scriptet gør det muligt at inkludere imaget i en kerne.
*   Dens fleksibilitet gør det i mange tilfælde unødvendigt at rekompilere kernen.

Hvis man bruger RAID eller LVM på root filsystemet, skal de rette HOOKS konfigureres. Se wiki-siderne for [LVM/RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") og [Configuring mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio") for mere information. Hvis du bruger et non-US keyboard, tilføjes `keymap` hook for at indlæse din lokale keymap under boot. Tilføj `usbinput` hook hvis du bruger et USB keyboard (ellers, hvis den fejler under boot af en eller anden grund, vil du blive bedt om at indtaste root's adgangskode for at komme ind og reparere systemet, men du vil ikke være i stand til det). Husk at tilføje `usb` hook når du installere Arch på en etstern harddisk, Compact Flash eller SD kort, som er forbundet via USB, f.eks.:

```
HOOKS="base udev autodetect pata scsi sata usb filesystems keymap usbinput"

```

Hvis du har brug for at kunne boote fra USB-enheder, FireWire-enheder, PCMCIA-enheder, NFS shares, software RAID arrays, LVM2 partitions, krypterede partitions eller DSDT, skal dine HOOKS konfigureres tilsvarende.

#### /etc/modprobe.d/modprobe.conf

Denne fil kan bruges til at sætte specielle konfigurationer på kernemoduler. Det er unødvendigt at konfigurere denne fil i tilfælde. Artiklen om [kernel modules](/index.php/Kernel_modules "Kernel modules") har mere information.

#### /etc/resolv.conf

**Note:** Hvis du bruger DHCP, kan du roligt ignorere denne fil, da den som standard bliver dynamisk oprettet og slettet af dhcpcd-dæmonen. Du kan ændre denne opførsel hvis du ønsker det. Se [netwærk](/index.php/Network#For_DHCP_IP "Network") og [resolv.conf](/index.php/Resolv.conf "Resolv.conf") sider for mere information.

_resolver_ er en mængde af routiner i C-biblioteket som giver adgang til the Internet Domain Name System (DNS). En af hoved-funktionerne for DNS er at oversætte domænenavne til IP addreser for at gøre nettet til et venligere sted. Resolve konfigurationsfilen eller `/etc/resolv.conf`, indeholder information som læses af resolver-rutinerne første gang de bliver kaldt af en process.

Hvis du bruger en statisk IP skal du sætte dine DNS servere i `/etc/resolv.conf` (nameserver <ip-address>). Du kan have så mange som du ønsker.

Et eksempel med OpenDNS:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

Hvis du bruger en router, kan du specificere dine DNS servere i routeren selv og simpelthen pege på den fra din `/etc/resolv.conf`, ved at bruge din routers IP (som også er din gateway fra `/etc/rc.conf`). Eksempel:

```
nameserver 192.168.1.1

```

HVis du bruger **DHCP**, kan du også specificere dine DNS servere i routeren eller tillade at de bliver automatisk tilføjet fra din ISP, hvis din ISP tilbyder det.

#### /etc/hosts

Denne fil kobler IP-adresser med hostnavne og aliaser. Hver host er repræsenteret med én linje.

```
<IP-address> <hostname> [aliases...]

```

Tilføj dit _hostname_, som er det samme som specificeret i `/etc/rc.conf`, som en alias, så det ser ud som:

```
127.0.0.1   localhost.localdomain   localhost **yourhostname**
::1         localhost.localdomain   localhost **yourhostname**

```

**Note:** ::1 er IPv6 udgaven af 127.0.0.1

**Warning:** Dette format, **at inkludere "localhost" og dit faktiske host navn**, er krævet for programkompatibilitet! Så hvis du har givet

din computer navnet "arch", skal ovenstående linje se ud som følger:

```
127.0.0.1   localhost.localdomain   localhost arch

```

Fejl i denne linje kan være skyld i langsomt netværk og/eller få nogle programmer til at åbne meget langsomt eller slet ikke virke. Dette er

en meget almindelig fejl for begyndere.

**Note:** Nyere versioner af Arch Linux Installeren tilføjer automatisk dit hostnavn til denne fil hvis du har skrevet det i `/etc/rc.conf`. Hvis det af en eller anden grund ikke er tilfældet, må du selv tilføje det som beskrevet.

Hvis du bruger en statisk IP-adresse, tilføjes endnu en linje med følgende syntaks: <static-IP> <hostname.domainname.org> <hostname>

f.eks.:

```
192.168.1.100 **yourhostname**.domain.org  **yourhostname**

```

**Tip:** Du kan med fordel også bruge `/etc/hosts` aliases til hosts på dit netværk og/eller på internettet f.eks.:

```
192.168.1.90 media
192.168.1.88 data

```

Ovenstående eksempel vil at du kan tilgå en media- og data-server på dit netværk vha. navnet uden at skulle skrive deres IP-adresse.

#### /etc/locale.gen

Kommandoen `/usr/sbin/locale-gen` læser fra `/etc/locale.gen` for at generere specifikke regionaldata (locales). Disse kan så

anvendes af **glibc** og ethvert andet regionalbevidst program eller bibliotek til at gengive tekst, vise regionale møntenheder korrekt,

tid og datoformater, specielle tegn og bogstaver og andre lokal-specifikke standarder.

Som standard er `/etc/locale.gen` en tom fil med kommenteret dokumentation. Når den først er redigeret, røres filen ikke igen.

`locale-gen` køres hver gang **glibc** opgraderes, og genererer alle regionaldata angivet i `/etc/locale.gen`.

Vælg de regionaldata du har brug for ved at fjerne #-tegnet foran de linjer du øsnker, f.eks.:

```
en_US ISO-8859-1
en_US.UTF-8

```

Installationsprogrammet vil nu køre scriptet locale-gen, der genererer de regionaldata, som du angav. Du kan ændre dine regionaldata senere

ved at redigere filen `/etc/locale.gen` og derefter køre `locale-gen` som root.

**Note:** hvis du ikke vælger dine regionaldata, vil det medføre fejlen: "The current locale is invalid...". Dette er måske den mest almindelige begynderfejl i Arch Linux.

##### Root-adgangskode

Tilsidst angiver du en 'root'-adgangskode, som du absolut ikke må glemme senere. Gå tilbage til hovedmenuen, hvor du fortsætter med at installere en opstartsindlæser (bootloader).

##### Pacman-spejle

Vælg en spejl-kilde til Pacman. Husk at archlinux.org er indskrænket, så download begrænses til 50KB/s.

*   _Hvis du ikke kender de præsenterede spejle og deres respektive placeringer, kan du vælge et hvilket som helst spejl. Du får lejlighed til at køre scriptet **rankmirrors** senere i denne guide, for automatisk at konfigurere de nærmeste spejle._

Gå tilbage til hovedmenuen.

### Install and configure a bootloader

#### For BIOS motherboards

For BIOS systems, several boot loaders are available, see [Boot loaders](/index.php/Boot_loaders "Boot loaders") for a complete list. Choose one as per your convenience. Here, two of the possibilities are given as examples:

*   [Syslinux](/index.php/Syslinux "Syslinux") is (currently) limited to loading only files from the partition where it was installed. Its configuration file is considered to be easier to understand. An example configuration can be found in the [syslinux](/index.php/Syslinux#Examples "Syslinux") article.
*   [GRUB](/index.php/GRUB "GRUB") is more feature-rich and supports more complex scenarios. Its configuration file(s) is more similar to 'sh' scripting language, which may be difficult for beginners to manually write. It is recommended that they automatically generate one.

##### Syslinux

If you opted for a GUID partition table (GPT) for your hard drive earlier, you need to install the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package now for the installation of _syslinux_ to work:

```
# pacman -S gptfdisk

```

Install the [syslinux](https://www.archlinux.org/packages/?name=syslinux) package and then use the `syslinux-install_update` script to automatically _install_ the bootloader (`-i`), mark the partition _active_ by setting the boot flag (`-a`), and install the _MBR_ boot code (`-m`):

```
# pacman -S syslinux
# syslinux-install_update -iam

```

After installing Syslinux, configure `syslinux.cfg` to point to the right root partition. This step is vital. If it points to the wrong partition, Arch Linux will not boot. Change `/dev/sda3` to reflect your root partition (if you partitioned your drive as in [the example](#Prepare_the_storage_drive), your root partition is `/dev/sda1`).

 `# nano /boot/syslinux/syslinux.cfg` 

```
...
LABEL arch
        ...
        APPEND root=**/dev/sda3** rw
        ...
```

If adding [UUID](/index.php/UUID "UUID") rather than partition number the syntax is `APPEND root=UUID=_partition_uuid_ rw`.

Do the same for the fallback entry.

For more information on configuring and using Syslinux, see [Syslinux](/index.php/Syslinux "Syslinux").

##### GRUB

Install the [grub](https://www.archlinux.org/packages/?name=grub) package and then run `grub-install` to install the bootloader:

```
# pacman -S grub
# grub-install --target=i386-pc --recheck **/dev/sda**

```

**Note:**

*   Change `/dev/sda` to reflect the drive you installed Arch on. Do not append a partition number (do not use `sda_X_`).
*   For GPT-partitioned drives on BIOS motherboards, you also need a "BIOS Boot Partition". See [GPT-specific instructions](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") in the GRUB page.
*   A sample `/boot/grub/grub.cfg` gets installed as part of the [grub](https://www.archlinux.org/packages/?name=grub) package, and subsequent `grub-*` commands may not over-write it. Ensure that your intended changes are in `grub.cfg`, rather than in `grub.cfg.new` or some such file.

While using a manually created `grub.cfg` is absolutely fine, it is recommended that beginners automatically generate one:

**Tip:** To automatically search for other operating systems on your computer, install [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`) before running the next command.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:** It is possible that multiple redundant menu entries will be generated. See [GRUB#Redundant_menu_entries](/index.php/GRUB#Redundant_menu_entries "GRUB").

For more information on configuring and using GRUB, see [GRUB](/index.php/GRUB "GRUB").

#### For UEFI motherboards

For UEFI systems, several boot loaders are available, see [Boot loaders](/index.php/Boot_loaders "Boot loaders") for a complete list. Choose one as per your convenience. Here, two of the possibilities are given as examples:

*   [gummiboot](/index.php/Gummiboot "Gummiboot") is a minimal UEFI Boot Manager which provides a menu for [EFISTUB](/index.php/EFISTUB "EFISTUB") kernels and other UEFI applications.
*   [GRUB](/index.php/GRUB "GRUB") is a more complete bootloader, useful if you run into problems with Gummiboot.

No matter which one you choose, first install the [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) package, so you can manipulate your EFI System Partition after installation:

```
# pacman -S dosfstools

```

**Note:** For UEFI boot, the drive needs to be GPT-partitioned and an [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (512 MiB or larger, gdisk type `EF00`, formatted with FAT32) must be present. In the following examples, this partition is assumed to be mounted at `/boot`. If you have followed this guide from the beginning, you have already done all of these.

##### Gummiboot

Install the [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) package and run `gummiboot install` to install the bootloader to the EFI System Partition:

```
# pacman -S gummiboot
# gummiboot install

```

**Warning:** Gummiboot and the Linux Kernel will not automatically update if your EFI System Partition is not mounted at `/boot`.

You will need to manually create a configuration file to add an entry for Arch Linux to the gummiboot manager. Create `/boot/loader/entries/arch.conf` and add the following contents, replacing `/dev/sdaX` with your **root** partition, usually `/dev/sda2`:

 `# nano /boot/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

For more information on configuring and using gummiboot, see [gummiboot](/index.php/Gummiboot "Gummiboot").

##### GRUB

Install the [grub](https://www.archlinux.org/packages/?name=grub) and [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) packages and run `grub-install` to install the bootloader:

```
# pacman -S grub efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch_grub --recheck

```

Next, while using a manually created `grub.cfg` is absolutely fine, it is recommended that beginners automatically generate one:

**Tip:** To automatically search for other operating systems on your computer, install [os-prober](https://www.archlinux.org/packages/?name=os-prober) before running the next command. However _os-prober_ is not known to properly detect UEFI OSes.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

For more information on configuring and using GRUB, see [GRUB](/index.php/GRUB "GRUB").

## Konfigurere grundsystemet

Dit nye Arch Linux grundsystem er nu et funktionsdygtigt GNU/Linux-miljø klar til at blive tilpasset dine ønsker og behov. Herfra kan du bygge dette elegante sæt værktøj om til netop det, du har brug for eller kræver.

Lad os komme i gang.

* * *

Log ind med din root-konto. Vi vil konfigurere 'Pacman' og opdatere systemet som 'root', for derefter at tilføje en alm. bruger.

### Netværkskonfiguration (hvis nødvendigt)

*   _Dette afsnit hjælper dig med at konfigurere de fleste typer netværk, hvis installations-scriptets autokonfiguration ikke virker for dig._

* * *

Hvis alt gik godt, burde du have et fungernede netværk. Prøv at pinge www.google.com for at tjekke.

```
ping -c 3 www.google.com

```

_Hvis det lykkedes at etablere en netværksforbindelse, kan du gå videre til_ [_Opdatering, Synkronisering og opgradering med Pacman_](/index.php/Dansk_Begynderguide#Opdatering_synkronisering_og_opgradering_med_Pacman "Dansk Begynderguide")

Hvis du, efter at have prøvet at pinge www.google.com, får en "unknown host"-fejlmelding, kan du konkludere, at dit netværk ikke er konfigureret ordentligt. Du kan vælge at dobbelttjekke indstillingerne og integriteten i følgende filer:

**/etc/rc.conf** # Tjek specielt afsnittene HOSTNAME= og NETWORKING for fejl.

**/etc/hosts** # Dobbelttjek dit format. (Se ovenfor.)

**/etc/resolv.conf** # Hvis du benytter statisk IP. Hvis du anvender DHCP, bliver denne fil dynamisk oprettet og slettet som standard, men kan dog ændres som du ønsker. (Se eventuelt [Network](/index.php/Network "Network"), som er på engelsk.)

Avancerede instruktioner for konfiguration af netværk findes i artiklen [Network](/index.php/Network "Network").

#### Kablet LAN

Tjek dit 'ethernet' med

```
ifconfig

```

hvor du skulle se en indgang for 'eth0'. Hvis det kræves, kan du sætte en ny statisk IP med

```
ifconfig eth0 <IP-adresse> netmask <netmaske> up 

```

og standard-gateway med

```
ip route add default via <gatewayens IP-adresse>

```

Tjek om /etc/resolv.conf indeholder din DNS-server og tilføj den, hvis den mangler. Tjek igen dit netværk ved at pinge www.google.com. Hvis alt virker nu, skal du rette /etc/rc.conf som beskrevet ovenfor (statisk IP). Hvis du har en DHCP-server/-router i dit netværk, kan du prøve

```
dhcpcd eth0

```

Hvis dette virker, skal du rette /etc/rc.conf som beskrevet i afsnit 2.6 (dynamisk IP).

#### Trådløs LAN

Detaljeret opsætningsguide: [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")

#### Analogt modem

For at kunne bruge et eksternt Hayes-kompatibelt analog modem, skal du i det mindste have pakken 'ppp' installeret. Ændr filen /etc/ppp/options så den passer til dine behov ifølge 'man pppd'. Du skal definere et 'chat-script' til at give dit brugernavn og adgangskode til din ISP (Internet Service Provider = udbyder) efter etablering af den initierende forbindelse. 'man'-siderne for 'pppd' og 'chat' indeholder eksempler, der skulle række til at få en forbindelse op at køre, hvis du enten er erfaren eller stædig nok. Med 'udev' er dine serielle porte normalt /dev/tts/0 og /dev/tts/1. Vink: Læs [Dialup without a dialer HOWTO](/index.php/Dialup_without_a_dialer_HOWTO "Dialup without a dialer HOWTO").

I stedet for at kæmpe en indædt kamp med den enkle 'pppd', vil du måske hellere installere 'wvdial' eller et lignende værktøj, for at lettte opsætningsprocessen betydeligt. Hvis du har et såkaldt 'WinModem', hvilket i grunden er et PCI plugin-kort, der virker som et internt analog-modem, skulle du prøve at føje den rigelige information på hjemmesiden [LinModem](http://www.linmodems.org/).

#### ISDN

Opsætning af ISDN gøres i tre trin:

1.  Installér og konfigurér hardware
2.  Installér og konfigurér ISDN-værktøjer
3.  Tilføj indstillinger for din ISP

Den nuværende kerne i Arch inkluderer de nødvendige ISDN-moduler, hvilket betyder, at du ikke behøves at rekompilere din kerne medmindre du vil benytte noget meget specielt ISDN-hardware. Når du fysisk har installeret dit ISDN-kort eller koblet din USB ISDN-boks til, kan du prøve at indlæse modulerne med 'modprobe'. Næsten alle passive ISDN PCI-kort behandles af modulet 'hisax', som behøver 2 parametre: 'type' og 'protocol'. Du skal sætte 'protocol' til '1' hvis di land benytter standarden 1TR6, '2' hvid det benytter EuroISDN (EDSS1), '3' hvis du er hægtet på en såkaldt 'leased-line' uden 'D-channel' og '4' for US NI1.

Detaljer omkring alle disse indstillinger, og hvordan de sættes, er inkluderet i dokumentationen for kernen i undermappen 'isdn'. De er også tilgængelige online. Parameteren 'type' afhænger af dit kort. En liste over alle mulige typer findes i kernedokumentationen README.HiSax. Vælg dit kort og indlæs modulet med de passende valgmuligheder som i dette eksempel:

```
modprobe hisax type=18 protocol=2

```

Dette indlæser 'hisax'-modulet for mit ELSA Quickstep 1000PCI, der anvendes i Tyskland med EDSS1-protokollen. Du kan finde hjælpsomt 'debugging-output' i filen /var/log/everything.log, hvor du burde se at dit kort forberedes. Bemærk at du sikkert skal indlæse nogle USB-moduler, før du kan få en ekstern USB ISDN-Adapter til at virke.

Når det bekræftes, at dit kort virker med bestemte indstillinger, kan du føje modulvalgmulighederne til din /etc/modprobe.d/modprobe.conf:

```
alias ippp0 hisax
options hisax type=18 protocol=2

```

Alternativt kan du nøjes med kun at tilføje linjen med valgmuligheder her, og føje 'hisax' til 'MODULES' i rc.conf. Det er dit valg, men dette eksempel har den fordel, at modulet ikke indlæses, før det er nødvendigt.

Når dette er gjort, burde du have et fungerende og understøttet hardware. Nu mangler du så de basale værktøjer, for at kunne bruge det.

Installér pakken 'isdn4k-utils' og læs 'man'-siden for 'isdnctrl', der vil få dig i gang. Længere nede på 'man'-siden kan du finde enforklaring på, hvordan du opretter en konfigurationsfil, der kan fortolkes af 'isdnctrl', lige som nogle opsætningseksempler. Bemærk at du skal føje din 'SPID' til din MSN-indstilling adskilt med ':', hvis du bruger US NI1.

Efter at du har konfigureret dit ISDN-kort med værktøjet 'isdnctrl', skulle du kunne kalde den maskine, du har angivet med parameteren PHONE_OUT, men få en fejl ved autentificering af brugernavn og adgangskode. For at få det til at virke, skal du føje brugernavn og adgangskode til /etc/ppp/pap-secrets eller /etc/ppp/chap-secrets, som hvis du konfigurerede et normalt analogt PPP-link, afhængig af hvilken protokol din ISP benytter til autentificering. Hvis du er i tvivl, så læg dine data ind i begge filer.

Hvis du har sat det hele rigtigt op, skulle du kunne etablere en opkaldsforbindelse med

```
isdnctrl dial ippp0

```

som root. Hvis du har problemer, så husk at tjekke dine logfiler!

#### DSL (PPPoE)

Disse instruktioner er relevante, hvis det er din PC, der håndterer forbindelsen til din ISP. Du behøver blot at at definere en korrekt standard-gateway, hvis du benytter en separat router til at klare ISP-tilslutningen.

Du skal fysisk installere det netværkskort, der skal tilsluttes dit DSL-modem, før du kan bruge din DSL-forbindelse. Når du har tilføjet dit nyinstallerede netværkskort i modules.conf/modprobe.conf eller i MODULES-linjen, skal du installere pakken 'rp-pppoe' og køre scriptet 'pppoe-setup' for at konfigurere tin tilslutning. Når du har angivet alle data, kan du tilslutte din linje med

```
/etc/rc.d/adsl start

```

og afbryde igen med

```
/etc/rc.d/adsl stop

```

Opsætningen er ret let og ligetil, men du kan sikkert finde et par fif i man-siderne. Hvis du ønsker automatisk tilslutning ved boot, skal du føje 'adsl' til din DAEMONS-linje.

## Opdatering synkronisering og opgradering med [Pacman](/index.php/Pacman "Pacman")

Vi vil nu opdatere systemet med [Pacman](/index.php/Pacman "Pacman").

##### Hvad er Pacman ?

[Pacman](/index.php/Pacman "Pacman") - fra engelsk **pac**kage **man**ager - er Arch Linux' pakkehåndtering. Pacman er skrevet i C, og er hurtig, enkel og ekstremt kraftfuld. Det håndterer hele dit pakkesystem og tager sig af installation, fjernelse og nedgradering (gennem cache) af pakker. Udover dette tager Pacman sig af brugerkompileret pakkehåndtering, automatisk afhængighedsløsning, ekstern og lokal søgning og meget meget mere. Vi vil bruge Pacman til at downloade software-pakker fra eksterne kilder (repositories) og installere dem på dit system.

Pacman er det vigtigste af alle værktøjer i Arch Linux til at bygge kernesystemet om til, hvad som helst du har lyst til.

##### Opdatér Pacman

Du kan blive promptet for at opdatere selve Pacman, afhængig af hvor gammel dit installationsmedie er:

```
pacman -Syu

```

Lad Pacman opdatere sig selv. Der kan forekomme konfigurationsændringer, så læs derfor uddata fra opgraderingen.

*   _**Bemærk: Vær sikker på, at du benytter kommandoen 'pacman -Syu' på dette punkt, da det ellers kan forårsage utallige problemer for førstegangsbrugere.**_

_**Konfigurationsændringer forekommer, der kræver en indsats af brugeren under opdateringer. Læs derfor uddata fra 'Pacman' for relevant information.**_

### Konfigurering af Pacman

##### Pakkekilder og /etc/pacman.conf

Arch Linux tilbyder for tiden de følgende software-kilder, der er tilgængelige gennem 'Pacman':

**[core]**

Princippet bag [core] er ganske enkelt at tilbyde ét af hvert af de nødvendige værktøjer for et basalt Arch Linux-system. En vindueshåndtering, en browser osv. Der er dog undtagelser. For eksempel er der to editorer - 'nano' og 'vi' - hvor brugeren kan vælge den ene eller begge.

**HER MANGLER TEKST - RESTEN FINDES UNDER DISKUSSIONSFANEBLADET HER PÅ SIDEN**

##### /etc/pacman.conf

Pacman prøver at læse filen /etc/pacman.conf, hver gang den påkaldes. Denne konfigurationsfil er inddelt i sektioner - eller software-kilder. Hver sektion angiver en software-kilde, som Pacman kan benytte, når der søges efter pakker. Undtagelsen til dette er sektionen for valgmuligheder (options), der angiver globale valgmuligheder.

```
nano -w /etc/pacman.conf

```

Eksempel:

```
[core]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

[extra]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

#[unstable]
# Add your preferred servers here, they will be used first
#Include = /etc/pacman.d/mirrorlist

#[aur]
#Server = https://aur.archlinux.org/packages.php

```

Aktivér alle de ønskede software-kilder (fjern # foran linjerne "Include = /etc/pacman.d/mirrorlist" og "['software-kilde']")

*   Hvis linjerne "Server =" er afkommenterede, tvinges søgning på den angivne server først og fremmest. Yderligere konfiguration af kilder er under /etc/pacman.d/
*   **VINK:** Du kan roligt inkludere software-kilden [Unstable], da pakkerne på dit system fra alle de andre software-kilder kan sameksistere med pakkerne fra [Unstable].

*** _Bemærk: Husk at afkommentere både overskriftlinjen i firkantede paranteser '[ ]' og_ Include=_-linjerne, når du vælger software-kilder. Hvis du ikke gør dette, udelades de valgte software-kilder. Dette er en meget almindelig fejl._**

#### /etc/pacman.d/mirrorlist

Hurtigere serverspejle (mirrors) forbedrer Pacmans ydelse væsentligt, samt helhedsoplevelsen af Arch Linux.

Scriptet **rankmirrors** rangerer automatisk software-spejlene efter hastighed. Redigér filen /etc/pacman.d/mirrorlist:

```
nano /etc/pacman.d/mirrorlist

```

Fjern alle spejle, der ikke er på dit kontinent, eller ligger særligt langt væk. (Hvis du bruger 'nano', kan du anvende 'Ctrl+K' til at fjerne hver unødvendig linje). Gem filen og afslut.

Eftersom 'rankmirrors' er et Python-script, skal du have Python installeret. Hent det med:

```
pacman -S python

```

Sæt så _rankmirrors_ til at vælge spejl efter hastighed med:

```
rankmirrors -v /etc/pacman.d/mirrorlist

```

Uddata viser så en liste over alle spejlene og deres respektive hastighed - Eksempelvis:

```
# United States
# http://mirrors.easynews.com/linux/archlinux/core/os/i686 ... 1.14
# ftp://ftp.archlinux.org/core/os/i686 ... 1.38
# ftp://ftp.nethat.com/pub/linux/archlinux/core/os/i686 ... unreachable
# ftp://locke.suu.edu/linux/dist/archlinux/core/os/i686 ... 2.42
# ftp://mirrors.unixheads.org/archlinux/core/os/i686 ... 1.91
# ftp://ftp-linux.cc.gatech.edu/pub/linux/distributions/archlinux/core/os/i686 ... 1.42
# ftp://mirror.cs.vt.edu/pub/ArchLinux/core/os/i686 ... 1.12
# ftp://ftp.ibiblio.org/pub/linux/distributions/archlinux/core/os/i686 ... 1.39

```

Scriptet sorterer så disse spejle efter hastighed - Eksempelvis:

```
Server = ftp://mirror.cs.vt.edu/pub/ArchLinux/core/os/i686
Server = http://mirrors.easynews.com/linux/archlinux/core/os/i686
Server = ftp://ftp.archlinux.org/core/os/i686
Server = ftp://ftp.ibiblio.org/pub/linux/distributions/archlinux/core/os/i686
Server = ftp://ftp-linux.cc.gatech.edu/pub/linux/distributions/archlinux/core/os/i686
Server = ftp://mirrors.unixheads.org/archlinux/core/os/i686
Server = ftp://locke.suu.edu/linux/dist/archlinux/core/os/i686
Server = ftp://ftp.nethat.com/pub/linux/archlinux/core/os/i686

```

Bemærk at dette er kun en løs henvisning til, hvordan du skal arrangere filen - spejle tættest på din bopæl, eller med laveste svarhastighed, er ikke nødvendigvis det bedste valg. Du vinder intet med et hurtigtsvarende ikke-opdateret spejl, eller et spejl med lille forsinkelse men med dårlig båndbredde.

Redigér filen /etc/pacman.d/mirrorlist ved at placere det bedste spejl øverst i listen. Du vilsikkert vende tilbage til denne konfigurationsfil for at forsøge med forskellige spejle. Tænk dig om og vælg klogt.

## Opdatere systemet

Opdatér, synkronisér og **opgradér** hele dit nye system med:

```
pacman -Syu

```

Pacman henter nu den seneste information om tilgængelige pakker og udfører alle tilgængelige opdateringer. (Du kan også blive promptet for at opgradere selve Pacman. Hvis det sker så acceptér og gentag kommandoen 'pacman -Syu', når den er færdig.)

##### _Læg mærke til, om der sker en større kerneopdatering._

_Hvis (Linux-)kernen gennemgår en større opgradering, sættes moduler som f.eks **nvidia** og **madwifi** (som installeres senere i denne guide, hvis det er nødvendigt) ud af funktion, da de opgraderede pakkeversioner af disse moduler er bygget til den nye kerne, og dit system stadig bruger den ældre kerne. Det vil være nødvendigt at genstarte._

##### Det gode ved 'Rolling Release'

Glem ikke, at Arch er en **rolling release**-distribution. (Rolling Release = rullende/dynamisk udgivelse.) Dette betyder, at der aldrig er grund til at geninstallere eller udføre detaljerede genopbygninger af systemet, for at opgradere til den nyeste version. Ved blot en gang imellem at køre kommandoen **pacman -Syu**, kan du holde dit system opdateret til 'det sidste nye'. Efter en sådan opgradering er dit system 100% aktuelt.

##### Lær Pacman at kende

Pacman er Arch-brugerens bedste ven. Det anbefales på det kraftigste at læse om - og lære at bruge - værktøjet Pacman. Prøv:

```
man pacman

```

Se i bunden af denne artikel og tag dig tid til et kig på wiki-en om [Pacman](/index.php/Pacman "Pacman").

### Tilføj en bruger og sæt grupper op

Du bør ikke lave dit daglige arbejde som brugeren 'root'. Det er ikke kun meget dårlig praksis, det er direkte farligt. 'Root' er til administrative opgaver. I stedet tilføjer du en brugerkonto med:

```
adduser

```

Selv om det er udmærket at benytte standardmulighederne, vil du sikkert tilføje 'storage', 'audio', 'video', 'optical', og 'wheel' til dine yderligere grupper - især hvis du har planer om at have et fuldt funktionsdygtigt skrivebordsmiljø.

Grupper og deres brugere angives i /etc/group.

De inkluderer:

*   audio - for opgaver der involverer lydkort og det relaterede software
*   wheel - for at bruge 'sudo'
*   storage - for håndtering af lagringsenheder
*   video - for videoopgaver og 3d-acceleration
*   optical - for håndtering af opgaver relaterede til optiske drev
*   floppy - for adgang til et floppy-drev (hvis nødvendigt)
*   lp - for håndtering af printer-opgaver
*   hal & dbus - for automontering

Se artiklen om [grupper](/index.php/Groups "Groups") for at forstå, hvilke grupper du bør tilmeldes. Du kan også føje din bruger til de ønskede grupper sådan her (som 'root'):

```
usermod -aG audio,video,floppy,lp,optical,network,storage,wheel,dbus,hal BRUGERNAVN

```

Kig man-siderne for 'usermod' og 'gpasswd' for mere information.

## **TRIN 2**: Installation af X og konfiguration af ALSA

### Konfigurér lydkortet med 'alsamixer'

Den avancerede linux lydarkitektur ALSA (**A**dvanced **L**inux **S**ound **A**rchitecture) er en Linux kernekomponent, hvis hensigt er at erstatte den originale OSS (**O**pen **S**ound **S**ystem), for at tilbyde enheds-drivere til lydkort. Udover drivere til lydenheder, indeholder **ALSA** et bibliotek med brugerområde til programudviklere, der ønsker at trække de interaktive faciliteter fra kerne-driverne op til en programbrugerflade på et højere niveau. Pakken 'alsa-utils' indeholder 'alsamixer', som tillader os at konfigurere lydenheden fra terminalen. (Du kan senere køre 'alsamixer' fra et X-miljø.)

* * *

Enhedshåndteringen _udev_ undersøger automatisk dit hardware under boot, og indlæser det korresponderende modul for dit lydkort. Din lyd burde allerede virke, men du kan sikkert ikke høre noget, da det - som standard - er lydløst.

Installér pakken 'alsa-utils':

```
 pacman -S alsa-utils

```

Har du tilføjet din normale bruger til gruppen 'audio'? Hvis ikke; bør du gøre det nu.  
Skriv (som 'root'):

```
gpasswd -a yourusername audio

```

Som normal bruger skriver du:

```
alsamixer

```

Ved hjælp af piletasterne højre/venstre vælger du kanalerne 'Master' og 'PCM', hvorefter du sætter 'lyd på' ved at trykke **M**. Skru op for lyden med piletasten 'op'. (70-90 er et godt valg.) Forlad 'alsamixer' ved at trykke ESC.

#### Test af lyden

Test din lydkonfiguration som normal bruger med 'aplay':

```
aplay /usr/share/sounds/alsa/Front_Center.wav

```

Så skulle du høre en meget veltalende dame sige "Front center".

Som 'root' kør kommandoen:

```
alsactl store

```

Dette opretter filen /etc/asound.state, og gemmer indstillingerne.

Tilføj også 'alsa' til sektionen DAEMONS i /etc/rc.conf, for automatisk at genoprette mixer-indstillingerne under boot.

```
nano /etc/rc.conf

```

```
DAEMONS=(syslog-ng network crond **alsa**)

```

_Bemærk: Dæmonen 'alsa' genopretter kun dine lydindstillinger under opstart. Den er adskilt fra lydbiblioteket i 'Alsa' (og API på kerneniveau)._

Yderliger information findes i [ALSA](/index.php/ALSA "ALSA") wiki-en.

### Installation og konfiguration af X

See [Xorg](/index.php/Xorg "Xorg").

## **TRIN 3:** Installation og konfiguration af dit skrivebord

Hvis du spørger to mennesker om, hvilket skrivebordsmiljø - eller vindueshåndtering - er det bedste, vil du få seks forskellige svar. Vælg det miljø, der passer bedst til _dine_ behov.

*   Hvis du vil have et 'fuldblods', der svarer til Windows eller Mac OSX er **KDE** et godt valg.
*   Hvis du vil have et lidt mere minimalistisk, der bedre følger K.I.S.S.-princippet, er **GNOME** sikkert det rigtige.
*   **Xfce4** opfattes generelt som lignende GNOME, men lettere og kræver mindre systemressourcer, men giver stadigt et komplet skrivebordsmiljø.
*   Hvis du vil have noget endnu 'lettere', er det **openbox, fluxbox eller fvwm2**, du skal kigge på (for ikke at nævne alle de andre letvægtere som f.eks. **windowmaker og twm**).
*   Hvis du vil have noget totalt anderledes, så prøv **ion, wmii, eller dwm**.

### Installér fonte

På dette tidspunkt vil du sikkert installere nogle pæne fonte, **før** du installerer et skrivebordsmiljø eller vindueshåndtering. 'Dejavu' og 'bitstream-vera' er nogle pæne font-sæt. Til web-sider vil du sikkert også have nogle Microsoft fonte. Installér med:

```
pacman -S ttf-ms-fonts ttf-dejavu ttf-bitstream-vera

```

### ~/.xinitrc

Denne konfigurationsfil kontrollerer, hvad der sker, når du skriver 'startx'.

Skift til 'normal bruger' med:

```
su _dit-brugernavn_

```

Redigér din /home/brugernavn/.xinitrc for at anvende det ønskede skrivebordsmiljø:

```
nano ~/.xinitrc

```

Afkommentér eller tilføj linjen 'exec ..' for det rette skrivebordsmiljø/vindueshåndtering:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#
# exec xterm
# exec wmaker
# exec startkde
# exec gnome-session
exec startxfce4
# exec icewm
# exec blackbox
# exec fluxbox

```

(For Xfce4 skrivebordsmiljøet.)

Husk kuin at have én afkommenteret 'exec...'-linje i din ~/.xinitrc.

### GNOME

#### Om GNOME

**G**NU **N**etwork **O**bject **M**odel **E**nvironment. GNOME-projektet tilbyder to ting:

1.  GNOME-skrivebordsmiljøet - et intuitivt og attraktivt skrivebord til slutbrugere
2.  GNOME udviklingsplatform - et udvidet rammeværk til programbygning der integrerer ind i resten af miljøet

#### Installation

Installér det komplette GNOME-miljø med:

```
pacman -S gnome gnome-extra

```

Du kan roligt vælge alle de viste pakker. Alternativt kan du installere et mere basalt og skrabet GNOME:

```
pacman -S gnome

```

##### Nyttige GNOME-dæmoner

Længere oppe i guiden blev det beskrevet, at en dæmon er et program, der kører i baggrunden, og venter på at der sker en handling, hvor den så tilbyder service. Her er et par af de vigtigste dæmoner:

*   **hal** automatiserer bl.a. montering af diske, optiske drev og USB-drev/sticks til brug i den grafiske brugerflade.
*   **fam** tillader realtidsvisning af filændringer i den grafiske brugerflade, ved straksat tillade adgang til nyinstallerede programmer eller ændringer i filsystemet.

Både **hal** og **fam** gør livet lettere for GNOME-brugeren. Pakkerne _hal_ og _fam_ installeres, når du installerer GNOME, men de skal kaldes, før de kan benyttes.

Du vil sikkert også have en grafisk login-håndtering. Til GNOME er dæmonen **gdm** et godt valg. Installér _gdm_ with

```
pacman -S gdm

```

Du vil elt sikkert have dæmonerne **hal** og **fam**.

Start hal og fam:

```
/etc/rc.d/hal start

```

```
/etc/rc.d/fam start

```

Tilføj dem i sektionen DAEMONS i filen /etc/rc.conf, så de kaldes under opstart:

```
nano /etc/rc.conf

```

```
DAEMONS=(syslog-ng network crond alsa **hal fam gdm**)

```

(Hvis du foretrækker, at gå direkte i konsol, og derfra manuelst starte X - i bedste 'Slackware-tradition' - skal du blot udelade gdm.)

Start X som 'normal bruger':

```
startx

```

Du vil sikkert installere en terminal og en editor. Jeg vil anbefale 'gnome-terminal' (en del af pakkegruppen 'gnome-extra') og 'geany':

```
pacman -S geany gnome-terminal

```

Avancerede instruktioner i installation og konfiguration af GNOME findes i artiklen [GNOME](/index.php/GNOME "GNOME").

#### Guf for øjet

Måske finder du ikke standardtemaet i GNOME særligt attraktivt. Et pænt tema er 'murrine'. Installér det med:

```
pacman -S gtk-engine-murrine

```

Vælg det ved at gå i System->Preferæncer->Tema. Du finder flere temaer, ikoner og baggrundsbilleder på [GNOME Look](http://www.gnome-look.org).

### KDE

#### Om KDE

**K** **D**esktop **E**nvironment. KDE er et kraftfuldt fri-software grafisk skrivebordsmiljø til GNU/Linux- og UNIX-arbejdsstationer. Det kombinerer brugervenlighed, funktionalitet og enestående grafisk design med den teknologiske overlegenhed i UNIX-agtige operativsystemer.

#### Installation

Arch tilbyder følgende versioner af KDE: **kde, kdebase og KDEmod**. Vælg **én** af de følgende, og fortsæt længere nede med **"Nyttige KDE-dæmoner"**:

**1.)** Pakken **kde** er den kompklette vanilla-KDE, ~300MB.

```
pacman -S kde

```

**2.)** Pakken **kdebase** er en skrabet version med mindre programmer, ~80MB.

```
pacman -S kdebase

```

**3.)** Den sidste pakke **KDEmod** er et Arch Linux eksklusivt fællesskabsdrevet system, der er ændret med henblik på ekstrem god ydelse og tilpasningsmuligheder. Projektet KDEmod har sin hjemmeside her [http://kdemod.ath.cx/](http://kdemod.ath.cx/) [http://kdemod.ath.cx/](http://kdemod.ath.cx/) .  
KDEmod er ekstremt hurtigt letvægtet og modtageligt med et behageligt tilpasset tema.

#### Nyttige KDE-dæmoner

KDE kræver dæmonerne **hal** (**H**ardware **A**bstraction **L**ayer) og **fam** (**F**ile **A**lteration **M**onitor). Dæmonen **kdm** (**K** **D**isplay **M**anager) tilbyder **grafisk login**, hvis dette ønskes.

Længere oppe i guiden blev det beskrevet, at en dæmon er et program, der kører i baggrunden, og venter på at der sker en handling, hvor den så tilbyder service. Her er et par af de vigtigste dæmoner:

*   **hal** automatiserer bl.a. montering af diske, optiske drev og USB-drev/sticks til brug i den grafiske brugerflade.
*   **fam** tillader realtidsvisning af filændringer i den grafiske brugerflade, ved straksat tillade adgang til nyinstallerede programmer eller ændringer i filsystemet.

Både **hal** og **fam** gør livet lettere for KDE-brugeren. Pakkerne _hal_, _fam_ og _kdm_ installeres, når du installerer KDE, men de skal kaldes, før de kan benyttes.

* * *

Start hal og fam:

```
/etc/rc.d/hal start

```

```
/etc/rc.d/fam start

```

*   **BEMÆRK:** _Dæmonen 'hal' afhænger af og starter automatisk dæmonen 'dbus'._

Redigér sektionen DAEMONS i din /etc/rc.conf:

```
nano /etc/rc.conf

```

Tilføj **hal** and **fam** for at kalde dem under opstart. Tilføj også **kdm**, hvis du foretrækker grafisk logind:

```
DAEMONS=(syslog-ng network crond alsa **hal fam kdm**)

```

*   På denne måde starter systemet i kørselsniveau 3, (/etc/inittab default, multiuser mode), og starter så KDM som dæmon.

*   Nogle brugere foretrækker at starte skærmhåndteringen - som f.eks. KDM - op på en alternativ måde, nemlig ved at benytte kørselsniveau-5 i /etc/inittab. Se [Display manager](/index.php/Display_manager "Display manager") for yderligere information.

*   Hvis du hellere vil logge ind i **konsollen** på kørselsniveau 3, og derfra manuelt starte X i bedste 'Slackware tradition', skal du udelade 'kdm', eller udkommentere det med et udråbstegn ( ! ).

Start X som 'normal bruger':

```
startx

```

Avancerede instruktioner i installation og konfiguration af KDE findes i artiklen [KDE](/index.php/KDE "KDE").

Tillykke! Velkommen til dit KDE skrivebordsmiljø på dit nye Arch Linux system! Du kan fortsætte med at kigge på [Tilretning og finpudsning](/index.php/Dansk_Begynderguide#Tilretning_og_finpudsning "Dansk Begynderguide") eller resten af informationen længer nede.  
Artiklen [Post Installation Tips](/index.php/Post_Installation_Tips "Post Installation Tips") kunne også være af interesse.

### Xfce

#### Om Xfce

Xfce er - som GNOME og KDE - et skrivebordsmiljø. Det indeholder en vifte af programmer som f.eks. et rodvindues-applet, en vindueshåndtering, filhåndtering, panel osv. Xfce er skrevet ved hjælp af værktøjssættet GTK2, og indeholder dets eget udviklingsmiljø (biblioteker, dæmoner osv.), ligesom de store skrivebordsmiljøer. Til forskel fra GNOME og KDE er Xfce meget letvægtigt og designet mere omkring CDE end Windows eller Mac. Det har en langsommere udviklingscyklys, men er meget stabil og ekstremt hurtigt. Xfce er ideel til ældre hardware.

#### Installation

Installér et komplet **xfce** skrivebordsmiljø med temaer og ekstra 'guf':

```
pacman -S xfce4 xfce4-goodies gtk2-themes-collection

```

Hvis du benytter 'kdm' eller 'gdm', skulle en ny Xfce-session komme frem. Alternativt kan du bruge

```
startxfce4

```

Avancerede instruktioner for installation og konfiguration af Xfce findes i artiklen [Xfce](/index.php/Xfce "Xfce").

### *box

#### Fluxbox

Fluxbox © er endnu en vindueshåndteringfor X. Det er baseret på kode fra Blackbox 0.61.1\. Fluxbox ligner Blackbox og behandler stile, farver, vinduesplacering og lignende ting nøjagtigt som Blackbox (100% tema-/stil-kompatibilitet).

Installér Fluxbox med

```
pacman -S fluxbox fluxconf

```

Hvis du benytter 'kdm' eller 'gdm', skulle en ny Fluxbox-session komme frem.  
Ellers skal du ændre din brugers .xinitrd og tilføje:

```
exec startfluxbox 

```

Mere information er tilgængelig i artiklen [Fluxbox](/index.php/Fluxbox "Fluxbox").

#### Openbox

Openbox følger standarder, og er en hurtig og letvægts vindueshåndtering med mulighed for udvidelser.

Openbox virker med dine programmer, og gør det nemmere at håndtere dit skrivebord. Dette fordi det i udviklingen - modsat de fleste andre vindueshåndteringer - først blev skrevet til at rette sig efter standarder og fungere ordentligt. Først da dette var i orden, gik holdet over til arbejdet med den visuelle brugerflade.

Openbox er fuldt funktionelt som eneste arbejdsmiljø, eller det kan anvendes som en indsættelserstatning for standard-vindueshåndteringen i GNOME eller KDE skrivebordsmiljøerne.

Installér Openbox med

```
pacman -S openbox obconf obmenu

```

Når Openbox er installeret, får du besked på at flytte menu.xml & rc.xml til ~/.config/openbox/ i din hjemmemappe:

```
mkdir -p ~/.config/openbox/
cp /etc/xdg/openbox/rc.xml ~/.config/openbox/
cp /etc/xdg/openbox/menu.xml ~/.config/openbox/

```

I filen "rc.xml" kan du ændre flere indstillinger for Openbox (eller du kan benytte OBconf). I "menu.xml" kan du ændre din højre-klik-menu.

For at kunne logge ind i Openbox, kan du enten foretage grafisk logind med KDM/GDM eller kommandoen 'startx', Hvor du så skal have ændret din fil ~/.xinitrc (som bruger) og tilføje/afkommentere følgende:

```
exec openbox

```

Med KDM behøver du ikke at gøre mere. Openbox bliver vist i sessionsmenuen i KDM.

Nogle nyttige programmer for Openbox:

*   PyPanel eller LXpanel - hvis du vil have et panel
*   feh - Hvis du vil indstille baggrunden
*   ROX - hvis du vil have en simpel filhåndtering og skrivebordsikoner

Mere information i artiklen [Openbox](/index.php/Openbox "Openbox").

### fvwm2

FVWM er en ekstremt kraftfuld og multivirtuel skrivebords- og vindueshåndtering for X vinduessystemet, der retter sig efter ICCCM. Udviklingen er meget aktiv, og der er god understøttelse.

Installér fvwm2 med

```
pacman -S fvwm 

```

FVWM listes automatisk i sessionsmenuen i KDM/GDM. Ellers tilføj eller afkommenter:

```
exec fvwm 

```

Til din brugers .xinitrc.

Bemærk! Den stabile version a FVWM er et par år gammel. Hvis du vil have en nyere version, findes pakken 'fvwm-devel' i softwarekilden 'Unstable'.

## Tilretning og finpudsning

### HAL

Når du nu har installeret et skrivebordsmiljø, og hvis du ikke allerede har gjort det, er det nu på tide at installere HAL. HAL tillader 'plug-and-play' (tilslut og spil) for din mobiltelefon, din iPod, dine eksterne lagringsmedier os.. Det monterer enheden og laver et pænt og synligt ikon på dit skrivebord og/eller 'Min computer', der giver dig adgang til enheden, uden først manuelt at skulle konfigurere filen /etc/fstab eller 'udev'-regler for hver enkel ny enhed.

KDE, GNOME og XFCE bruger alle HAL-dæmonen.

Installationsproceduren beskrives i artiklen [HAL](/index.php/HAL "HAL"). Der er mere information i [Wikipedia](https://en.wikipedia.org/wiki/HAL_(software) "wikipedia:HAL (software)").

### Sætte dæmoner i baggrunden under opstart

Du kan sætte dine dæmoner i /etc/rc.conf i baggrunden, således at opstartsproceduren bliver hurtigere ved at sætte et snabel-a - @ - foran, som f.eks.:

```
DAEMONS=(@syslog-ng @network crond @alsa @hal @fam @kdm)

```

Dette gør, at dæmoner indlæses i baggrunden, uden at vente på at den foranstående indlæses først.

Sæt et udråbstegn - ! - foran de dæmoner, du ikke behøver som f.eks.:

```
DAEMONS=(@syslog-ng @network !crond @alsa @hal @fam @kdm)

```

### Pænere fonte for LCD-er

Se [artiklen om fonte](/index.php/Fonts "Fonts"). (Engelsk)

### Musehjul

Selv om din mus burde virke ud-af-æsken, vil du sikkert bruge musehjulet. Tilføj dette til sektionen 'Input' (mouse0):

```
       Option      "ZAxisMapping" "4 5 6 7"

```

### evdev

Hvis du har en moderne USB-mus med flere knapper og/eller funktioner, kan du installere musedriveren 'evdev', der tillader dig at nyde den fulde funktionalitet af din mus:

```
pacman -S xf86-input-evdev

```

Indlæs driveren:

```
modprobe evdev

```

Find navnet på din mus ved at skrive nøjagtigt sådan her:

```
cat /proc/bus/input/devices | egrep "Name"

```

Ved hjælp af navnet på musen, konfigurér sektionen 'InputDevice' i din /etc/X11/xorg.conf som f.eks.:

```
Section "InputDevice"
 Identifier      "Evdev Mouse"
 Driver          "evdev"
 Option          "Name" "Logitech USB-PS/2 Optical Mouse"
 Option          "CorePointer"
EndSection

```

Du kan kun have **én** "CorePointer"-enhed angivet i /etc/X11/xorg.conf, så husk at udkommentere enhver anden museindgang, indtil du føler dig sikker nok til at fjerne de gamle og ubrugte indgange.

Redigér også sektionen 'ServerLayout' til at inkludere 'Evdev Mouse* som din CorePointer som f.eks.:

```
Section "ServerLayout"
   Identifier     "Layout0"
   Screen      0  "Screen0"
   InputDevice    "Keyboard0" "CoreKeyboard"
   InputDevice    "Evdev Mouse" "CorePointer"

```

### Tastaturlayout

Hvis du vil ændre dit tastaturlayout, skal du redigere din /etc/X11/xorg.conf, og tilføje disse linjer sektionen 'Input' i (keyboard0) (Eksemplet viser et dansk tastaturlayout uden 'døde taster' - ændr dette efter behov).

```
       Option          "XkbLayout"     "dk"
       Option          "XkbVariant"    "nodeadkeys"

```

### Yderligere tilretninger til bærbare computere

ACPI-understøttelse er nødvendigt, hvis du vil benytte nogle specielle funktioner på din bærbare computer som f.eks. slumringstilstand, - når låget lukkes, specielle taster osv. Installér 'acpid'

```
pacman -S acpid

```

og føj det til dæmonerne i /etc/rc.conf (acpid). Start det med

```
/etc/rc.d/acpid start

```

Yderliger information om Arch Linux på diverse bærbare computere findes her: [Category:Laptops](/index.php/Category:Laptops "Category:Laptops")

### Konfiguration af CPU frekvensskalering

Moderne processorer kan nedsætte deres frekvens og spænding for at formindske varmeudvikling og strømforbrug. Mindre varme betyder mindre støj fra systemet. Specielt brugere af bærbare computere ønsker dette, men også almindelige stationære computere høster fordele heraf. Installér 'cpufrequtils' med

```
pacman -S cpufrequtils

```

og føj 'cpufreq' til dine dæmoner i /etc/rc.conf. Redigér konfigurationsfilen /etc/conf.d/cpufreq og ændr

```
governor="conservative"

```

der dynamisk øger CPU-frekvensen, når det er nødvendigt, hvilket også er en fordel på stationære systemer. Ret 'min_freq' og 'max_freq' så det matcher CPU-specifikationerne på dit system. Hvis du ikke kender frekvenserne, kan du køre _cpufreq-info_, når du har indlæst et af modulerne for frekvensskalering. Du kan også slette eller udkommentere linjerne 'min_freq' og 'max_freq', hvorefter tingene fungerer automatisk. Føj modulet til modullinjen i din /etc/rc.conf. De fleste moderne bærbare og stationære computere er i stand til ganske enkelt at anvende driveren _acpi-cpufreq_. Andre valgmuligheder inkluderer driverne _p4-clockmod, powernow-k6, powernow-k7, powernow-k8_ og _speedstep-centrino_. Indlæs modulet med

```
modprobe <modulnavn> 

```

og start 'cpufreq' med

```
/etc/rc.d/cpufreq start

```

For flere detaljer se [Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils")

## Nyttige programmer

Denne sektion bliver aldrig komplet. Den viser blot nogle gode programmer til hverdagsbrug.

**Bemærkning til KDE-brugere**: Da KDE ligger i /opt, skal du sikkert logge ud og ind efter første installation for at opdatere dine søgestier, før du kan anvende disse programmer.

### Internet

##### Firefox

Den altid populære web-browser - Firefox - er tilgængelig igennem Pacman. Installér med

```
pacman -S firefox

```

Husk også at installere 'flashplugin', 'mplayer', 'mplayer-plugin' og 'codecs'-pakken for en komplet web-oplevelse:

```
pacman -S flashplugin mplayer mplayer-plugin codecs

```

(Pakken 'codecs' indeholder kodeks til Quicktime- og Realplayer-indholdet.)

Mozilla's Thunderbird håndterer dine e-mail. Hvis du bruger GNOME, vil du sikkert kigge på Epiphany og Evolution. Hvis du bruger KDE, vælger du sikkert Konqueror og KMail. Hvis du ønsker noget anderledes, kan du stadig benytte Opera. Og til sidst - hvis du arbejder fra systemkonsollen (eller i en terminal-session) kan du vælge mellem flere tekstbaserede browsere som ELinks, Links og Lynx, og du kan håndtere dine e-mail med [Mutt](/index.php/Mutt "Mutt"). Pidgin (tidligere kendt som Gaim) og Kopete er gode til kvikbeskeder (Instant Messenger) til hhv. GNOME og KDE. PSI og Gajim er ideelle, hvis du kun bruger Jabber eller Google Talk.

### Kontor

OpenOffice er en komplet ifte af kontorprogrammer (i stil med Microsoft Office). Abiword er en god lille alternativ tekstbehandler og Gnumeric et godt regneark til GNOME. KOffice er en komplet kontorpakke til KDE. GIMP (eller GIMPShop) er et pixel-baseret grafikprogram (i stil med Adobe Photoshop), mens Inkscape er et program til vektor-baseret grafik (som Adobe Illustrator). Og - selvfølgelig - Arch kommer med et fuldt sæt af LaTex-programmer: Programmet 'tetex' har været populær i mange år (og virker stadig), og dets efterfølger [Texlive](/index.php/Texlive "Texlive") er tilgængelig fra software-kilden [AUR](/index.php/AUR "AUR").

## Multimedie

### Videoafspiller

#### VLC

VLC Player er en multimedieafspiller til Linux. Installér det med

```
pacman -S vlc

```

(TODO) Instructions for VLC mozilla plug-in

#### Mplayer

MPlayer er en multimedieafspiller til Linux. Installér det med

```
pacman -S mplayer

```

Det har også en Mozilla plug-in til video og indlejrede strømme i web-sider. Installér det med

```
pacman -S mplayer-plugin

```

Bruger du KDE, er KMplayer et bedre valg. Det kommer med plug-in til video og indlejrede strømme i web-sider, der virker med Konqueror. Installér det med

```
pacman -S kmplayer

```

(TODO) GMPlayer instructions

#### Xine

Xine er en glimrende afspiller - specielt til DVD-er.

```
pacman -S xine-ui

```

Biblioteket 'libdvdcss' afkoder krypterede DVD-er. _Vær sikker på, at det ikke er i strid med loven, hvor du bor, før du installerer!_

```
pacman -S libdvdcss

```

#### GNOME

##### Totem

[Totem](http://www.gnome.org/projects/totem/) er den officielle filmafspiller til GNOME skrivebordsmiljøet. Det er baseret på 'xine-lib' eller GStreamer (som standard installeres GStreamer med Arch-pakken 'totem'). Det tilbyder spilleliste, fuldskærmstilstand, søgefunktion, volumen-kotrol samt tastaturnavigation. Det kommer med ekstrafunktioner såsom:

*   Video-miniaturer i din filhåndtering
*   Nautilus egenskabsfaneblad
*   Epiphany / Mozilla (Firefox) plugin til at se film i din browser
*   Webcam-værktøj (Under udvikling)

Totem-xine er stadig det bedste valg, hvis du vil se DVD.

Totem er en del af pakkegruppen 'gnome-extra group' - Totem webbrowser-plugin er ikke.

For at installere separat:

```
pacman -S totem

```

For at installere Totem webbrowser-plugin:

```
pacman -S totem-plugin

```

#### KDE

##### Kaffeine

Kaffeine er et godt valg for KDE-brugere. Installér det med

```
pacman -S kaffeine

```

### Lydafspillere

#### GNOME/Xfce

##### Exaile

[Exaile](/index.php/Exaile "Exaile") er en musikafspiller skrevet i Python, der gør brug af GTK+ værktøjssættet. Den prøver at ligne Amarok, men i Gtk. Den findes i [community], så den kan installeres med:

```
pacman -S exaile

```

##### Rhythmbox

[Rhythmbox](http://www.gnome.org/projects/rhythmbox/) er et integreret musikhåndteringsprogram, der originalt er inspireret af Apple's iTunes. Det er frit software, designet til at arbejde godt under GNOME, og baseret på det kraftfulde rammeværk i GStreamer-mediet.

Rhythmbox tilbyder bl.a.:

*   Letanvendelig musikbrowser
*   Søgning og sortering
*   Omfattende understøttelse af lydformater gennem GStreamer
*   Understøtter internetradio
*   Spillelister

Installér rhythmbox:

```
pacman -S rhythmbox

```

##### Quod Libet

[Quod Libet](http://www.sacredchao.net/quodlibet) er en musikhåndtering, der benytter medierammeværket fra GStreamer til at afspille lydfiler. Dette sætter den i stand til at spille alle lydfiler, som Rhythmbox (der benytter samme rammeværk) kan afspille.  
Quod Libet er mere egnet til ikke-GNOME skrivebordsmiljøer, da sætter mindre spor og har mindre afhængigheder end Rhythmbox, der er afhængig af Nautilus, der igen kræver at store dele af GNOME installeres.

Ud over afspiller og musikhåndtering inkludere Quod Libet tillige Ex Falso, der er en editor til mærker.

Funktionerne i Quod Libet inkluderer:

*   Let anvendelig musikgennemsøger.
*   Søgefunktion.
*   Omfattende understøttelse af lydformater gennem Rhythmbox.
*   Let håndtering af spillelister.

Installér Quod Libet:

```
pacman -S quodlibet

```

Andre gode lydafspillere er: Banshee og Listen. Se [Gnomefiles](http://gnomefiles.org/) for at sammenligne dem.

#### KDE

##### Amarok

[Amarok](http://amarok.kde.org/) er en af de bedste systemer af lydafspillere og musikbiblioteker tilgængelige for KDE. Installér det med

```
pacman -S amarok-base

```

#### Konsol

[Moc](http://moc.daper.net/) er en 'ncurses'-baseret lydafspiller til konsollen.  
Et andet godt valg er [mpd](http://musicpd.org/). Og et tredje er [cmus](http://freshmeat.net/projects/cmus/).

#### Andre X-baserede

(TODO) Xmms, audacious, bmpx.

### Kodeks og andre typer af multimedieindhold

#### DVD

Du kan bruge 'xine-ui', 'totem-xine', MPlayer eller Kaffeine (for blot at nævne nogle af de store) til at se DVD. Det eneste, du måske mangler, er filen 'libdvdcss'. Vær opmærksom på, at det i visse lande kan være ulovligt at benytte den.

#### Flash

Installér flash-plugin med

```
pacman -S flashplugin

```

for at aktivere Macromedia (nu Adobe) Flash i din browser.

#### Quicktime

Quicktime-kodeks er med i pakken [codecs](https://aur.archlinux.org/packages/codecs/)<sup><small>AUR</small></sup>. Skriv blot

```
pacman -S codecs

```

for at installere dem.

#### Realplayer

Kodeks til Realplayer 9 s er med i pakken [codecs](https://aur.archlinux.org/packages/codecs/)<sup><small>AUR</small></sup>. Skriv blot

```
pacman -S codecs

```

for at installere dem. Realplayer 10 er tilgængelig som binær pakke til Linux. Du kan få den fra AUR: [realplayer](https://aur.archlinux.org/packages/realplayer/)<sup><small>AUR</small></sup>.

### CD- og DVD-brænding

#### GNOME

##### Brasero

[Brasero](http://www.gnome.org/projects/brasero/) er et program, der brænder CD/DVD i GNOME. Det er designet til at være så enkelt som muligt, og har nogle unikke særpræg, der tillader brugere at oprette deres diske let og hurtigt.

Installér med:

```
pacman -S brasero

```

#### KDE

##### K3b

K3b (fra **K**DE **B**urn **B**aby **B**urn) er et fri-software CD- og DVD-udviklingsprogram for GNU/Linux og andre Unix-lignende operativsystemer, der er designet for KDE. Som det er tilfældet med de fleste KDE-programmer, er K3b skrevet i C++ programsproget og anvender Qt GUI-værktøjssættet. K3b tilbyder en grafisk brugergrænseflade til at udføre de fleste CD-/DVD-brændingsopgaver såsom at brænde en lyd-CD udfra et sæt af lydfiler eller at kopiere en CD/DVD, ligesom de mere avancerede opgaver, som at brænde 'eMoviX'-CD/DVD. Det kan også lave direkte disk-til-disk kopiering. Programmet har mange standardindstillinger, der kan tilpasses af de mere erfarne brugere. Selve diskoptagelsen i K3b foretages af kommandolinje-værktøjet 'cdrecord' eller 'wodim', 'cdrdao' og 'growisofs'. Fra version 1.0 har K3b indbygget en DVD-ripper, der er under GPL-licens

K3b blev valgt som årets multimedieværktøj i 2006 på LinuxQuestions.org af flertallet af brugere (70%).

* * *

Installér K3b med

```
pacman -S k3b

```

##### (Todo) cdrecord, graveman...

De fleste programmer til CD-brænding er bygget op omkring 'cdrecord':

```
pacman -S cdrkit

```

Når du installerer programpakker til CD-/DVD-brænding som Brasero og K3b, installeres CD-/DVD-brændingsbiblioteket til det også, såsom 'libburn' eller 'cdrkit'.

Et godt DVD-brænderprogram til kommandolinjen er 'growisofs':

```
pacman -S dvd+rw-tools

```

### TV-kort

Der er flere ting, der skal gøres, hvis du vil se TV under (Arch) Linux. Den vigtigste opgave er at finde ud af, hvilket chipset din tuner anvender. En del er imidlertid understøttet. Husk at tjekke en hardware database som f.eks. [denne liste](http://en.opensuse.org/HCL/TV_Cards). Når du kender din model, er du kun nogle få skridt fra at det virker.

I de fleste tilfælde vil du få brug for 'bttv'-driverne (andre eksisterer såsom [V4L](http://linux.bytesex.org/v4l2/drivers.html)) sammen med I2C-modulerne. At konfigurere disse er den sværeste opgave. Hvis du er heldig vil

```
modprobe bttv

```

automatisk opdage kortet (tjek 'dmesg' for resultater). I så fald kan du nøjes med at installere et program til at se TV med. Det ser vi på senere. Hvis det ikke lykkedes at finde kortet automatisk, skal du tjekke filen 'CARDLIST', som er inkluderet i tar-arkivet i [bttv](http://dl.bytesex.org/releases/video4linux/), for at finde ud af de rette parametre for dit kort. Et 'PV951' uden understøttelse for radio skal bruge denne linje:

```
modprobe bttv card=42 radio=0

```

Nogle kort skal bruge cenne linje, for at kunne producere lyd:

```
modprobe tvaudio

```

Dette varierer imidlertid, så prøv dig frem! Nogle kort kræver følgende linje:

```
modprobe tuner

```

Dette er også en ting til at forsøge-og-fejle.

TODO: Redegøre for installationsproceduren

For egentlig at se TV installeres pakken 'zawtv' med

```
pacman -S xawtv 

```

og læs man-siderne.

TODO: Redegøre for nogle mulige problemer. Introduktion til XAWTV - evt. på anden side?

### Digitale kameraer

De fleste nyere digitalkameraer understøttes som USB-lagringsenheder, hvilket betyder, at du blot skal slutte det til og kopiere billederne. Ældre kameraer anvender måske protokollen PTP (Picture Transfer Protocol), som kræver en "speciel driver". 'gPhoto2' leverer denne driver og tillader en skal-baseret overførsel af billederne. Programmerne 'digikam' ( KDE) og 'gthumb' (GNOME - 'gtkam' kunne være et andet valg) benytter denne og tilbyder en god grafisk brugerflade.

### USB-hukommelsessticks og -harddiske

USB-hukommelsessticks og -harddiske understøttes ud-af-æsken med driveren for USB-lagringsenheder, og kommer frem som nye SCSI-enheder (`/dev/sdX`). Hvis du bruger KDE eller GNOME, skal du bruge dæmonerne 'dbus' og 'hal' (tilføj dem i `/etc/rc.conf`), og de monteres automatisk. Hvis du bruger et andet skrivebordsmiljø, skulle du måske kigge på 'ivman'.

## Systemvedligeholdelse

### Pacman

[Pacman](/index.php/Pacman "Pacman") er både en binær- og en kildepakkehåndtering, der kan downloade, installere og opdatere pakker fra både eksterne og lokale software-kilder. Den har fuld afhængighedsbehandling udover letforståelige værktøjer til fremstilling af dine egne pakker.

En mere detaljeret bekrivelse findes i artiklen om [Pacman](/index.php/Pacman "Pacman").

#### Nyttige kommandoer

Til synkronisering og opdatering af den lokale pakkedatabase med de eksterne software-kilder (Det er en god idé, at gøre dette for du installerer/opgraderer pakker):

```
pacman -Sy

```

For at **opgradere** alle pakker på dit system:

```
pacman -Su

```

Synkronisér, opdatér og **opgradér** alle pakker på dit system med én kommando:

```
pacman -Syu

```

For at installere/opgradere en pakke/flere pakker (inklusiv afhængigheder):

```
pacman -S pakke-A pakke-B

```

Du kan også synkronisere, opdatere og installere pakker med én kommando:

```
pacman -S pakke-A pakke-B

```

For at fjerne en enkelt pakke, uden at fjerne dens afhængigheder:

```
pacman -R pakke

```

For at fjerne enpakke og alle dens afhængigheder (der ikke benyttes af andre installerede pakker):

```
pacman -Rs pakke

```

For at fjerne alle pakkens nu unødvendige afhængigheder og også slette konfigurationsfiler:

```
pacman -Rsn pakke

```

For at søge i den eksterne (software-kilde) pakkedatabase efter en liste over pakker, der matcher et givet nøgleord:

```
pacman -Ss nøgleord

```

Få en liste over alle pakker på dit system med

```
pacman -Q

```

Lav en forespørgsel (query) i den lokale pakkedatabase (din maskine) efter en given pakke:

```
pacman -Q pakke

```

Lav en forespørgsel (query) i den lokale pakkedatabase (din maskine) efter en given pakke med en liste over alle relevante oplysninger:

```
pacman -Qi pakke

```

For at defragmentere Pacmans cache-database og optimere hastigheden:

```
pacman-optimize

```

For at tælle hvor mange pakker, der i øjeblikket er på dit system:

```
pacman -Q | wc -l

```

For at installere en pakke, der er kompileret fra kilde med ABS og 'makepkg':

```
pacman -U pakkenavn.pkg.tar.gz

```

Bemærk: Der er yderligt utallige funktioner opg kommandoer i Pacman. Prøv

```
man pacman

```

og se iøvrigt wiki-indgangene i [pacman](/index.php/Pacman "Pacman").

## Finpudsning og yderligere information

Yderligere information og hjælp:  
Arch Linux' [hjemmeside](https://www.archlinux.org), eller [søge her på wiki](/index.php/Special:Search "Special:Search").  
Det [engelske](https://bbs.archlinux.org) og det [danske Arch Linux forum](http://forum.archlinux.dk/index.php)  
[ArchChannel IRC-kanal](/index.php?title=ArchChannel_IRC-kanal&action=edit&redlink=1 "ArchChannel IRC-kanal (page does not exist)") og [mailing-lister](https://www.archlinux.org/mailman/listinfo/).

##### Ofte stillede spørgsmål

Se artiklen om [ofte stillede spørgsmål for nybegyndere](/index.php/Arch_FAQs_for_newbies "Arch FAQs for newbies"). (Engelsk)

##### Terminologi

For yderligere information om jargongen i Arch Linux kan du læse [denne artikel](/index.php/Arch_Terminology/Jargon_for_newbies "Arch Terminology/Jargon for newbies"). (Engelsk)

Efter installation er du måske også interesseret i:

*   [Post_Installation_Tips](/index.php/Post_Installation_Tips "Post Installation Tips")
*   [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working")
*   [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")
*   [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation")
*   [Pm-utils](/index.php/Pm-utils "Pm-utils")
*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(Dansk)&oldid=411521](https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(Dansk)&oldid=411521)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Dansk](/index.php/Category:Dansk "Category:Dansk")
*   [Eye candy (Dansk)](/index.php/Category:Eye_candy_(Dansk) "Category:Eye candy (Dansk)")