Related articles

*   [Frequently asked questions (Lietuviškai)](/index.php/Frequently_asked_questions_(Lietuvi%C5%A1kai) "Frequently asked questions (Lietuviškai)")
*   [Installation guide (Lietuviškai)](/index.php/Installation_guide_(Lietuvi%C5%A1kai) "Installation guide (Lietuviškai)")
*   [List of applications](/index.php/List_of_applications "List of applications")

Šis dokumentas tai anotuotas populiarių straipsnių ir svarbios informacijos indeksas skirtas pagerinti ir pridėti funkcionalumo įdiegtai Arch sistemai. Daroma prielaida, kad skaitytojai perskaitė ir sekdami [diegimo gidą](/index.php/Installation_guide_(Lietuvi%C5%A1kai) "Installation guide (Lietuviškai)") įsidiegė Arch Linux. Kitų skyrių, bei kitų straipsnių supratimui ir sekimui *reikalinga* perskaityti ir suprasti sąvokas esančias [#Sistemos administravimas](#Sistemos_administravimas) bei [#Paketų valdymas](#Paket.C5.B3_valdymas).

## Contents

*   [1 Sistemos administravimas](#Sistemos_administravimas)
    *   [1.1 Naudotojai ir grupės](#Naudotojai_ir_grup.C4.97s)
    *   [1.2 Privilegijos pakėlimas](#Privilegijos_pak.C4.97limas)
    *   [1.3 Servisų valdymas](#Servis.C5.B3_valdymas)
    *   [1.4 Sistemos priežiūra](#Sistemos_prie.C5.BEi.C5.ABra)
*   [2 Paketų valdymas](#Paket.C5.B3_valdymas)
    *   [2.1 pacman](#pacman)
    *   [2.2 Saugyklos](#Saugyklos)
    *   [2.3 Veidrodžiai](#Veidrod.C5.BEiai)
    *   [2.4 Arch Build sistema](#Arch_Build_sistema)
    *   [2.5 Arch User Repository](#Arch_User_Repository)
*   [3 Paleidimas](#Paleidimas)
    *   [3.1 Techninės įrangos auto-pažinimas](#Technin.C4.97s_.C4.AFrangos_auto-pa.C5.BEinimas)
    *   [3.2 Mikrokodas](#Mikrokodas)
    *   [3.3 Paleidimo pranešimų išsaugojimas](#Paleidimo_prane.C5.A1im.C5.B3_i.C5.A1saugojimas)
    *   [3.4 Num Lock aktyvacija](#Num_Lock_aktyvacija)
*   [4 Grafinė naudotojo sąsaja](#Grafin.C4.97_naudotojo_s.C4.85saja)
    *   [4.1 Ekrano serveris](#Ekrano_serveris)
    *   [4.2 Ekrano tvarkyklės](#Ekrano_tvarkykl.C4.97s)
    *   [4.3 Darbastalio aplinkos](#Darbastalio_aplinkos)
    *   [4.4 Langų tvarkyklės](#Lang.C5.B3_tvarkykl.C4.97s)
    *   [4.5 Ekrano valdyklės](#Ekrano_valdykl.C4.97s)
*   [5 Energijos valdymas](#Energijos_valdymas)
    *   [5.1 ACPI įvykiai](#ACPI_.C4.AFvykiai)
    *   [5.2 CPU dažnio kėlimas](#CPU_da.C5.BEnio_k.C4.97limas)
    *   [5.3 Nešiojamieji kompiuteriai](#Ne.C5.A1iojamieji_kompiuteriai)
    *   [5.4 Sustabdymas ir užmigdymas](#Sustabdymas_ir_u.C5.BEmigdymas)
*   [6 Multimedija](#Multimedija)
    *   [6.1 Garsas](#Garsas)
    *   [6.2 Naršyklės įskiepiai](#Nar.C5.A1ykl.C4.97s_.C4.AFskiepiai)
    *   [6.3 Kodekai](#Kodekai)
*   [7 Tinklas](#Tinklas)
    *   [7.1 Laikrodžio sinchronizacija](#Laikrod.C5.BEio_sinchronizacija)
    *   [7.2 DNS saugumas](#DNS_saugumas)
    *   [7.3 Užkardos nustatymas](#U.C5.BEkardos_nustatymas)
    *   [7.4 Dalinimasis resursais](#Dalinimasis_resursais)
*   [8 Įvesties įrenginiai](#.C4.AEvesties_.C4.AFrenginiai)
    *   [8.1 Klaviatūros išdėstymai](#Klaviat.C5.ABros_i.C5.A1d.C4.97stymai)
    *   [8.2 Pelės mygtukai](#Pel.C4.97s_mygtukai)
    *   [8.3 Nešiojamojo kompiuterio padelis](#Ne.C5.A1iojamojo_kompiuterio_padelis)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 Optimizavimas](#Optimizavimas)
    *   [9.1 Lyginamoji analizė](#Lyginamoji_analiz.C4.97)
    *   [9.2 Našumo gerinimas](#Na.C5.A1umo_gerinimas)
    *   [9.3 Solid state diskai](#Solid_state_diskai)
*   [10 Sistemos servisai](#Sistemos_servisai)
    *   [10.1 Failų indeksavimas ir paieška](#Fail.C5.B3_indeksavimas_ir_paie.C5.A1ka)
    *   [10.2 Vietinio pašto pristatymas](#Vietinio_pa.C5.A1to_pristatymas)
    *   [10.3 Spausdinimas](#Spausdinimas)
*   [11 Išvaizda](#I.C5.A1vaizda)
    *   [11.1 Šriftai](#.C5.A0riftai)
    *   [11.2 GTK+ ir Qt temos](#GTK.2B_ir_Qt_temos)
*   [12 Konsolės patobulinimai](#Konsol.C4.97s_patobulinimai)
    *   [12.1 Tab-užbaigimo patobulinimai](#Tab-u.C5.BEbaigimo_patobulinimai)
    *   [12.2 Trumpiniai](#Trumpiniai)
    *   [12.3 Alternatyvūs apvalkalai](#Alternatyv.C5.ABs_apvalkalai)
    *   [12.4 Bash papildymai](#Bash_papildymai)
    *   [12.5 Spalvota išvestis](#Spalvota_i.C5.A1vestis)
    *   [12.6 Suspausti failai](#Suspausti_failai)
    *   [12.7 Konsolės eilutė](#Konsol.C4.97s_eilut.C4.97)
    *   [12.8 Emacs apvalkalas](#Emacs_apvalkalas)
    *   [12.9 Pelės palaikymas](#Pel.C4.97s_palaikymas)
    *   [12.10 Atgalinės slinkties buferis](#Atgalin.C4.97s_slinkties_buferis)
    *   [12.11 Sesijos valdymas](#Sesijos_valdymas)

## Sistemos administravimas

Šis skyrius aprašo administracines užduotis ir sistemos valdymą. Dėl daugiau informacijos žiūrėti [Core utilities (Lietuviškai)](/index.php?title=Core_utilities_(Lietuvi%C5%A1kai)&action=edit&redlink=1 "Core utilities (Lietuviškai) (page does not exist)") ir [Category:System administration (Lietuviškai)](/index.php/Category:System_administration_(Lietuvi%C5%A1kai) "Category:System administration (Lietuviškai)").

### Naudotojai ir grupės

Naujas įdiegimas palieka jus tik su [superuser](https://en.wikipedia.org/wiki/Superuser "wikipedia:Superuser") paskyra, geriau žinoma kaip "root". Būnant prisijungus su root ilgus laiko tarpus, galimai net atskleidžiant jį serveryje per [SSH](/index.php/SSH "SSH"), [yra nesaugu](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). Vietoje to, daugumai užduočių derėtų sukurti ir naudoti neprivilegijuoto naudotojo paskyrą(as), o root paskyrą naudoti tik sistemos administravimui. Dėl detalių žiūrėti [Users and groups#User management](/index.php/Users_and_groups#User_management "Users and groups").

Naudotojai ir grupės yra *prieigos kontrolės* mechanizmas; administratoriai gali reguliuoti narystes grupėse bei nuosavyvės teises, taip suteikdami arba atimdami naudotojų, bei servisų prieigą prie sistemos resursų. Skaitykite [Users and groups](/index.php/Users_and_groups "Users and groups") straipsnį dėl daugiau detalių, bei galimų saugumo rizikų.

### Privilegijos pakėlimas

Komandos [su](/index.php/Su "Su") ir [sudo](/index.php/Sudo "Sudo") leidžia jums vykdyti komandas kaip kitam naudotojui. Pagal nutylėjimą *su* įmeta jus į root naudotojo prisijungimo langą, o *sudo* pagal nutylėjimą jums laikinai suteikia root privilegijas. Dėl skirtumų skaityti atitinkamus straipsnius.

### Servisų valdymas

Arch Linux naudoja [systemd](/index.php/Systemd "Systemd") kaip [init](/index.php/Init "Init") procesą, kuris yra Linux sistemos ir servisų tvarkyklė. Jūsų Arch Linux sistemos palaikymui, nebloga idėja išmokti jo pagrindus. Su *systemd* sąveikaujama per *systemctl* komandą. Dėl daugiau informacijos paskaitykite [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd").

### Sistemos priežiūra

Arch yra *rolling release* sistema su greita paketų kaitą, todėl naudotojai turėtų skirti šiek tiek laiko [sistemos priežiūrai](/index.php/System_maintenance "System maintenance"). Rekomendacijoms ir geriausioms praktikoms kaip grūdinti sistemą skaityti [Saugumas|](/index.php/Security "Security").

## Paketų valdymas

Šiame skyriuje yra naudinga informacija susijusi su paketų valdymu. For more, please see [Frequently asked questions (Lietuviškai)#Paketų valdymas](/index.php/Frequently_asked_questions_(Lietuvi%C5%A1kai)#Paket.C5.B3_valdymas "Frequently asked questions (Lietuviškai)") ir [Category:Package management](/index.php/Category:Package_management "Category:Package management").

**Note:** Būtina nuolat stebėti pasikeitimus, Arch Linux, kuriems reikia rankinio įsikišimo **prieš** atnaujinant savo sistemą. Prenumeruokite [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) arba tikrinkite pagrindinio puslapio [Arch naujienas](https://www.archlinux.org/) prieš kiekvieną atnaujinimą. Alternatyviai, galite prenumeruoti šį [RSS feed'ą](https://www.archlinux.org/feeds/news/).

### pacman

[pacman](/index.php/Pacman "Pacman") yra Arch Linux paketų tvarkyklė (*pac*kage *man*ager): visiems naudotojams privaloma susipažinti su ja prieš skaitant bet kokį kitą straipsnį.

Dėl pasiūlymų kaip pagerinti sąveiką su *pacman* ir bendrai paketų tvarkymui, skaityti [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks").

### Saugyklos

Dėl detalių apie kiekvienos oficialiai palaikomos saugyklos tiklą skaitykite [Official repositories](/index.php/Official_repositories "Official repositories") straipsnį.

Jeigu planuojate naudoti 32-bitų aplikacijas, turėsite įgalinti [multilib](/index.php/Multilib "Multilib") saugyklą.

[Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") straipsnyje rasite keletą nepalaikomų saugyklų.

Galimai norėsite įdiegti [pkgstats](/index.php/Pkgstats "Pkgstats") servisą.

### Veidrodžiai

Dėl žingsių kaip pilnai išnaudoti greičiausius ir naujausius oficialių saugyklų veidrodžius, skaitykite [Mirrors](/index.php/Mirrors "Mirrors") straipsnį. Kaip paaiškinta straipsnyje, ypatingai geras patarimas yra reguliariai tikrinti [Mirror Status](https://www.archlinux.org/mirrors/status/) puslapį, kuriame rasite naujausios sinchronizacijos veidrodžių sąrašą.

### Arch Build sistema

*Portai* yra sistema sudaryta iš kūrimo scenarijų esančių vietinės sistemos katalogo medyje, pradžioje naudota BSD distribucijose. Paprastai tariant, kiekvienas portas kataloge turi scenarijų intuityviai pavadintą pagal diegiamą trečiosios šalies aplikaciją.

[Arch Build sistema](/index.php/Arch_Build_System "Arch Build System") siūlo tą patį funkcionalumą, suteikdama kūrimo scenarijus vadinamus [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), kuriuose yra informacija skirta atitinkamai programinei įrangai; vientisumo hash'ai, projekto URL, versija, licenzija ir kūrimo instrukcijos. Šie PKGBUILDs yra analizuojami [makepkg](/index.php/Makepkg "Makepkg"), faktinės programos, kuri generuoja paketus švariai tvarkomus su *pacman*.

Kiekvienas paketas esantis saugyklose, kartu su tais esančiais AUR gali būti pakartotinai sukompiliuotas naudojantis *makepkg*.

### Arch User Repository

Kol Arch Build sistema suteikia galimybę kurti paketus esančius oficialiose saugyklose, [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) yra lygiavertis naudotojų pateiktiems paketams. Tai nepalaikoma kūrimo scenarijų saugykla prieinama per [interneto sąsają](https://aur.archlinux.org/) arba [Aurweb RPC sąsają](/index.php?title=Aurweb_RPC_s%C4%85saj%C4%85&action=edit&redlink=1 "Aurweb RPC sąsają (page does not exist)").

## Paleidimas

Šiame skyriuje yra informacija susijusi su paleidimo procesu. Arch paleidimo proceso apžvalgą galima rasti [Arch boot process](/index.php/Arch_boot_process "Arch boot process"). Dėl daugiau informacijos žiūrėti [paleidimo proceso kategorijoje](/index.php/Category:Boot_process "Category:Boot process").

### Techninės įrangos auto-pažinimas

Techninė įranga pagal nutylėjimą turėtų būti automatiškai aptinkama su [udev](/index.php/Udev "Udev") paleidimo proceso metu. Paleidimo laiką potencialiai pagerinti būtų galima, išjungiant automatinį modulių krovimą ir parenkant juos rankiniu būdų, kaip aprašyta [Kernel modules](/index.php/Kernel_modules "Kernel modules"). Papildomai, [Xorg](/index.php/Xorg "Xorg") turėtų automatiškai aptikti reikalingas tvarkykles su `udev`, bet naudotojai gali pasirinkti konfigūruoti X serverį rankiniu būdu.

### Mikrokodas

Procesoriai gali [elgtis netinkamai](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), ebt tą gali pataisyti branduolys atnaujindamas *mikrokodą' paleisties metu. Dėl daugiau detalių žiūrėti [Microcode](/index.php/Microcode "Microcode") straipsnį.*

### Paleidimo pranešimų išsaugojimas

Paleidimui pasibaigus ekranas yra išvalomas ir atsiranda prisijungimo laukelis, taip naudotojui negalint pamatyti kas tiksliai įvyko paleidimo proceso metu. [Išjunkite paleidimo pranešimų išvalymą](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") kad pašalintumėte šį trūkumą.

### Num Lock aktyvacija

Num Lock daugumoje klaviatūrų yra perjungimo klavišas. Num Lock aktyvavimui paleisties metu skaitykite [Activating Numlock on Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup").

## Grafinė naudotojo sąsaja

Šiame skyriuje informacija skirta vartotojams norintiems savo sistemoje paleisti grafines aplikacijas. Dėl daugiau žiūrėti [grafinės naudotojo sąsajos kategoriją](/index.php/Category:Graphical_user_interfaces "Category:Graphical user interfaces").

### Ekrano serveris

[Xorg](/index.php/Xorg "Xorg") is the public, open-source implementation of the [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (commonly X11, or X). It is required for running applications with graphical user interfaces (GUIs), and the majority of users will want to install it.

[Wayland](/index.php/Wayland "Wayland") is a newer, alternative display server protocol and the Weston reference implementation is available.

### Ekrano tvarkyklės

The default *vesa* display driver will work with most video cards, but performance can be significantly improved and additional features harnessed by installing the appropriate driver for [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel"), or [NVIDIA](/index.php/NVIDIA "NVIDIA") products.

### Darbastalio aplinkos

Although Xorg provides the basic framework for building a graphical environment, additional components may be considered necessary for a complete user experience. [Desktop environments](/index.php/Desktop_environment "Desktop environment") such as [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), and [Xfce](/index.php/Xfce "Xfce") bundle together a wide range of *X clients*, such as a window manager, panel, file manager, terminal emulator, text editor, icons, and other utilities. Users with less experience may wish to install a desktop environment for a more familiar environment. See [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") for additional resources.

### Langų tvarkyklės

A full-fledged desktop environment provides a complete and consistent graphical user interface, but tends to consume a considerable amount of system resources. Users seeking to maximize performance or otherwise simplify their environment may opt to install a [window manager](/index.php/Window_manager "Window manager") alone and hand-pick desired extras. Most desktop environments allow use of an alternative window manager as well. [Dynamic](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [stacking](/index.php/Category:Stacking_WMs "Category:Stacking WMs"), and [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") window managers differ in their handling of window placement.

### Ekrano valdyklės

Most desktop environments include a [display manager](/index.php/Display_manager "Display manager") for automatically starting the graphical environment and managing user logins. Users without a desktop environment can install one separately. Alternatively you may [start X at login](/index.php/Start_X_at_login "Start X at login") as a simple alternative to a display manager.

## Energijos valdymas

This section may be of use to laptop owners or users otherwise seeking power management controls. For more, please see [Category:Power management](/index.php/Category:Power_management "Category:Power management").

See [Power management](/index.php/Power_management "Power management") for more general overview.

### ACPI įvykiai

Users can configure how the system reacts to ACPI events such as pressing the power button or closing a laptop's lid. For the new (recommended) method using [systemd](/index.php/Systemd "Systemd"), see [Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management"). For the old method, see [acpid](/index.php/Acpid "Acpid").

### CPU dažnio kėlimas

Modern processors can decrease their frequency and voltage to reduce heat and power consumption. Less heat leads to more quiet system and prolongs the life of hardware. See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") for details.

### Nešiojamieji kompiuteriai

For articles related to portable computing along with model-specific installation guides, please see [Category:Laptops](/index.php/Category:Laptops "Category:Laptops"). For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

### Sustabdymas ir užmigdymas

Žiūrėti pagrindinį straipsnį: [Sustabdymas ir užmigdymas](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Multimedija

[Multimedijos kategorijoje](/index.php/Category:Multimedia "Category:Multimedia") rasite papildomų resursų.

### Garsas

[Garsas](/index.php/Sound "Sound") suteikiamas branduolio garso tvarkyklių:

*   [ALSA](/index.php/ALSA "ALSA") is included with the kernel and is recommended because usually it works out of the box (it just needs to be [unmuted](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")).

*   [OSS](/index.php/OSS "OSS") is a viable alternative in case ALSA does not work.

Users may additionally wish to install and configure a [sound server](/index.php/Sound_system#Sound_servers "Sound system") such as [PulseAudio](/index.php/PulseAudio "PulseAudio"). For advanced audio requirements, see [professional audio](/index.php/Professional_audio "Professional audio").

### Naršyklės įskiepiai

For access to certain web content, [browser plugins](/index.php/Browser_plugins "Browser plugins") such as Adobe Acrobat Reader, Adobe Flash Player, and Java can be installed.

### Kodekai

[Codecs](/index.php/Codecs "Codecs") are utilized by multimedia applications to encode or decode audio or video streams. In order to play encoded streams, users must ensure an appropriate codec is installed.

## Tinklas

This section is confined to small networking procedures. Head over to [Network configuration](/index.php/Network_configuration "Network configuration") for a full guide. For more, please see [Category:Networking](/index.php/Category:Networking "Category:Networking").

### Laikrodžio sinchronizacija

The [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) is a protocol for synchronizing the clocks of computer systems over packet-switched, variable-latency data networks. See [Time#Time synchronization](/index.php/Time#Time_synchronization "Time") for implementations of such protocol.

### DNS saugumas

For better security while browsing web, paying online, connecting to [SSH](/index.php/SSH "SSH") services and similar tasks consider using [DNSSEC](/index.php/DNSSEC "DNSSEC")-enabled client software which can validate signed [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") records, and [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") to encrypt DNS traffic.

### Užkardos nustatymas

A firewall can provide an extra layer of protection on top of the Linux networking stack. While the stock Arch kernel is capable of using [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")'s [iptables](/index.php/Iptables "Iptables") and [nftables](/index.php/Nftables "Nftables"), neither are enabled by default. It is highly recommended to set up some form of firewall. See [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") for available guides.

### Dalinimasis resursais

To share files among the machines in a network, follow the [NFS](/index.php/NFS "NFS") or the [SSHFS](/index.php/SSHFS "SSHFS") article.

Use [Samba](/index.php/Samba "Samba") to join a Windows network. To configure the machine to use Active Directory for authentication, read [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration").

See also [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Įvesties įrenginiai

This section contains popular input device configuration tips. For more, please see [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Klaviatūros išdėstymai

Non-English or otherwise non-standard keyboards may not function as expected by default. The necessary steps to configure the keymap are different for virtual console and [Xorg](/index.php/Xorg "Xorg"), they are described in [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") respectively.

### Pelės mygtukai

Owners of advanced or unusual mice may find that not all mouse buttons are recognized by default, or may wish to assign different actions for extra buttons. Instructions can be found in [Mouse buttons](/index.php/Mouse_buttons "Mouse buttons").

### Nešiojamojo kompiuterio padelis

Many laptops use [Synaptics](https://www.synaptics.com/) or [ALPS](http://www.alps.com/) "touchpad" pointing devices. For these, and several other touchpad models, you can use either the Synaptics input driver or libinput; see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") and [libinput](/index.php/Libinput "Libinput") for installation and configuration details.

### TrackPoints

See the [TrackPoint](/index.php/TrackPoint "TrackPoint") article to configure your TrackPoint device.

## Optimizavimas

This section aims to summarize tweaks, tools and available options useful to improve system and application performance.

### Lyginamoji analizė

[Benchmarking](/index.php/Benchmarking "Benchmarking") is the act of measuring performance and comparing the results to another system's results or a widely accepted standard through a unified procedure.

### Našumo gerinimas

The [Improving performance](/index.php/Improving_performance "Improving performance") article gathers information and is a basic rundown about gaining performance in Arch Linux.

### Solid state diskai

The [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") article covers many aspects of solid state drives, including configuring them to maximize their lifetimes.

## Sistemos servisai

This section relates to [daemons](/index.php/Daemons "Daemons"). For more, please see [Category:Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services").

### Failų indeksavimas ir paieška

Most distributions have a *locate* command available to be able to quickly search for files. To get this functionality in Arch Linux, [mlocate](https://www.archlinux.org/packages/?name=mlocate) is the recommended install. After the install you should run *updatedb* to index the filesystems.

[Desktop search engines](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities") provide a similar service, while better integrated into [desktop environments](/index.php/Desktop_environment "Desktop environment").

### Vietinio pašto pristatymas

A default setup does not provide a way to sync mail. To configure *Postfix* for simple local mailbox delivery, see [Postfix](/index.php/Postfix "Postfix"). Other options are [SSMTP](/index.php/SSMTP "SSMTP"), [msmtp](/index.php/Msmtp "Msmtp") and [fdm](/index.php/Fdm "Fdm").

### Spausdinimas

[CUPS](/index.php/CUPS "CUPS") is a standards-based, open source printing system developed by Apple. See [Category:Printers](/index.php/Category:Printers "Category:Printers") for printer-specific articles.

## Išvaizda

This section contains frequently-sought "eye candy" tweaks for an aesthetically pleasing Arch experience. For more, please see [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Šriftai

You may wish to install a set of TrueType fonts, as only unscalable bitmap fonts are included in a basic Arch system. There are several general-purpose [font families](/index.php/Fonts#Families "Fonts") providing large [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") coverage and even [metric compatibility](/index.php/Metric-compatible_fonts "Metric-compatible fonts") with fonts from other operating systems.

A plethora of information on the subject can be found in the [Fonts](/index.php/Fonts "Fonts") and [Font configuration](/index.php/Font_configuration "Font configuration") articles.

If spending a significant amount of time working from the virtual console (i.e. outside an X server), users may wish to change the console font to improve readability; see [Linux_console#Fonts](/index.php/Linux_console#Fonts "Linux console").

### GTK+ ir Qt temos

A big part of the applications with a graphical interface for Linux systems are based on the [GTK+](/index.php/GTK%2B "GTK+") or the [Qt](/index.php/Qt "Qt") toolkits. See those articles and [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for ideas to improve the appearance of your installed programs and adapt it to your liking.

## Konsolės patobulinimai

This section applies to small modifications that improve console programs' practicality. For more, please see [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### Tab-užbaigimo patobulinimai

It is recommended to properly set up extended [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") right away, as instructed in the article of your chosen shell.

### Trumpiniai

Aliasing a command, or a group thereof, is a way of saving time when using the console. This is specially helpful for repetitive tasks that do not need significant alteration to their parameters between executions. Common time-saving aliases can be found in [Bash#Aliases](/index.php/Bash#Aliases "Bash"), which are easily portable to [zsh](/index.php/Zsh "Zsh") as well.

### Alternatyvūs apvalkalai

[Bash](/index.php/Bash "Bash") is the shell that is installed by default in an Arch system. The live installation media, however, uses [zsh](/index.php/Zsh "Zsh") with the [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) addon package. See [Command-line shell#List of shells](/index.php/Command-line_shell#List_of_shells "Command-line shell") for more alternatives.

### Bash papildymai

A list of miscellaneous Bash settings, history search and [Readline](/index.php/Readline "Readline") macros is available in [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Spalvota išvestis

This section is covered in [Color output in console](/index.php/Color_output_in_console "Color output in console").

### Suspausti failai

Compressed files, or archives, are frequently encountered on a GNU/Linux system. [Tar](/index.php/Tar "Tar") is one of the most commonly used archiving tools, and users should be familiar with its syntax (Arch Linux packages, for example, are simply xzipped tarballs). See [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression").

### Konsolės eilutė

The console prompt (PS1) can be customized to a great extent. See [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization") or [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") if using Bash or Zsh, respectively.

### Emacs apvalkalas

Emacs is known for featuring options beyond the duties of regular text editing, one of these being a full shell replacement. Consult [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") for a fix regarding garbled characters that may result from enabling colored output.

### Pelės palaikymas

Using a mouse with the console for copy-paste operations can be preferred over [GNU Screen](/index.php/GNU_Screen "GNU Screen")'s traditional copy mode. Refer to [General purpose mouse](/index.php/General_purpose_mouse "General purpose mouse") for comprehensive directions. Note that you can already do this in [terminal emulators](/index.php/Terminal_emulator "Terminal emulator") with the [clipboard](/index.php/Clipboard "Clipboard").

### Atgalinės slinkties buferis

To be able to save and view text which has scrolled off the screen, refer to [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting").

### Sesijos valdymas

Using terminal multiplexers like [tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen"), programs may be run under sessions composed of tabs and panes that can be detached at will, so when the user either kills the terminal emulator, terminates [X](/index.php/X "X"), or logs off, the programs associated with the session will continue to run in the background as long as the terminal multiplexer server is active. Interacting with the programs requires reattaching to the session.