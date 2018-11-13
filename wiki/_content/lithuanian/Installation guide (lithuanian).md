Šis dokumentas, tai [Arch Linux](/index.php/Arch_Linux_(Lietuvi%C5%A1kai) "Arch Linux (Lietuviškai)") įdiegimo iš "live" sistemos naudojantis oficialiu įdiegimo atvaizdu vadovas. Prieš diegiant, patariama paskaityti [DUK](/index.php/FAQ_(Lietuvi%C5%A1kai) "FAQ (Lietuviškai)"). Dėl pačio dokumento supratimo, žiūrėti [Help:Reading](/index.php/Help:Reading "Help:Reading"). Tiksliau, kodo pavyzdžiai gali turėti išryškintas vietas (formatuotas kaip `*italics*`) kurias reikės pakeisti patiems.

Dėl detalesnių instrukcijų, žiūrėti atitinkamus [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") straipsnius arba įvairių programų [man puslapius](/index.php/Man_page "Man page"), į kuriuos bus nukreipimai šiame vadove. Norint interaktyvios pagalbos, eiti į [IRC kanalą](/index.php/IRC_channel "IRC channel") ir/arba [forumus](https://bbs.archlinux.org/).

Arch Linux turėtų veikti bet kokioje [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") architektūros mašinoje turinčioje bent 512 MB RAM. Pradinis diegimas su paketais iš [base](https://www.archlinux.org/groups/x86_64/base/) grupės turėtų užimti mažiau nei 800 MB disko vietos. Kadangi diegimo procese reikia gauti paketų iš nuotolinės saugyklos, šiame vadove daroma prielaida kad yra vikiantis interneto ryšys.

## Contents

*   [1 Prieš diegimą](#Prieš_diegimą)
    *   [1.1 Nustatykite klaviatūros išdėstymą](#Nustatykite_klaviatūros_išdėstymą)
    *   [1.2 Patikrinkite įkrovos rėžimą](#Patikrinkite_įkrovos_rėžimą)
    *   [1.3 Prisijunkite prie interneto](#Prisijunkite_prie_interneto)
    *   [1.4 Atnaujinkite sistemos laikrodį](#Atnaujinkite_sistemos_laikrodį)
    *   [1.5 Padalinkite diskus](#Padalinkite_diskus)
    *   [1.6 Suformatuokite particijas](#Suformatuokite_particijas)
    *   [1.7 Prijunkite failų sistemas](#Prijunkite_failų_sistemas)
*   [2 Įdiegimas](#Įdiegimas)
    *   [2.1 Pasirinkite veidrodžius](#Pasirinkite_veidrodžius)
    *   [2.2 Įdiekite pagrininius paketus](#Įdiekite_pagrininius_paketus)
*   [3 Sukonfigūruokite sistemą](#Sukonfigūruokite_sistemą)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Laiko zona](#Laiko_zona)
    *   [3.4 Lokalizacija](#Lokalizacija)
    *   [3.5 Tinklo konfigūracija](#Tinklo_konfigūracija)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root slaptažodis](#Root_slaptažodis)
    *   [3.8 Įkroviklis](#Įkroviklis)
*   [4 Perkrovimas](#Perkrovimas)
*   [5 Po diegimo](#Po_diegimo)

## Prieš diegimą

Parsisiųskite ir paleiskite diegimo terpę kaip nurodyta [Getting and installing Arch](/index.php/Getting_and_installing_Arch "Getting and installing Arch"). Jūs kaip root vartotojas būsite prijungti pirmoje [virtualioje konsolėje](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") ir pateksite į [Zsh](/index.php/Zsh "Zsh") apvalkalo eilutę.

Jei norite pereiti į kitą konsole, pvz.: kad galėtumėte skaityti šį vadovą per [ELinks](/index.php/ELinks "ELinks") ir kartu diegti, naudokitės `Alt+*arrow*` [komanda](/index.php/Keyboard_shortcuts "Keyboard shortcuts"). Konfigūracijos failų [keitimui](/index.php/Textedit "Textedit") galite naudoti: [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") ar [vim](/index.php/Vim#Usage "Vim").

### Nustatykite klaviatūros išdėstymą

Pradinis [išdėstymas](/index.php/Console_keymap "Console keymap") yra [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Galimus išdėstymus rasite:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

Išdėstymui pakeisti, po [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) pridėkite failo pavadinimą, praleisdami kelią ir failo plėtinį. Pavyzdžiui, [vokiečių kalbos](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") klaviatūros išdėstymui:

```
# loadkeys de-latin1

```

[Konsolės šriftai](/index.php/Console_fonts "Console fonts") randasi `/usr/share/kbd/consolefonts/` ir taip pat gali būti nustatyti su [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Patikrinkite įkrovos rėžimą

Jeigu [UEFI](/index.php/UEFI "UEFI") pagrindinėje plokštėje įjungtas UEFI rėžimas, [Archiso](/index.php/Archiso "Archiso") [užkraus](/index.php/Boot "Boot") Arch linux atitinkamai per [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Patikrinimui, pasiekite [efivars](/index.php/UEFI#UEFI_variables "UEFI") katalogą:

```
# ls /sys/firmware/efi/efivars

```

Jei katalogas neegzistuoja, sistema užkrauta [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") arba CSM rėžimu. Dėl detalių skaityti pagrindinės plokštės naudotojo vadovą.

### Prisijunkite prie interneto

Diegimo atvaizdas [laidinio tinklo įrenginiams](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) [dhcpcd](/index.php/Dhcpcd "Dhcpcd") įgalina įkrovos metu. Ryšį galima patikrinti su [ping](https://en.wikipedia.org/wiki/ping_(networking_utility) "wikipedia:ping (networking utility)"):

```
# ping archlinux.org

```

Jei ryšys negalimas, [sustabdykite](/index.php/Stop "Stop") *dhcpcd* tarnybą su `systemctl stop dhcpcd@*interface*` kur `*interface*` pavadinimas gali būti [tab-užbaigtas](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"). Tuomet sukonfigūruokite tinklą kaip nurodyta - [Network configuration](/index.php/Network_configuration "Network configuration").

### Atnaujinkite sistemos laikrodį

Kad užtikrintumėte sistemos laikrodžio tikslumą, naudokite [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1):

```
# timedatectl set-ntp true

```

Tarnybos statusui patikrinti naudokite `timedatectl status`.

### Padalinkite diskus

Kai "live" sistema atpažįsta diskus, jie priskiriami prie [bloko įrenginio](https://en.wikipedia.org/wiki/Device_file#Naming_conventions "wikipedia:Device file") kaip `/dev/sda` ar `/dev/nvme0n1`. Šiems įrenginiams identifikuoti, naudokite [lsblk](/index.php/Lsblk "Lsblk") arba *fdisk*.

```
# fdisk -l

```

Rezultatai besibaigiantys `rom`, `loop` ar `airoot` gali būti nuignoruoti.

Sekančios *particijos* yra **reikalingos** pasirinktam įrenginiui:

*   Viena particija root katalogui `/`.
*   Jei įjungtas [UEFI](/index.php/UEFI "UEFI") , reikės [EFI sitemos particijos](/index.php/EFI_system_partition "EFI system partition").

**Note:** [Swap](/index.php/Swap "Swap") vietai gali būti priskirta atskiroa particija arba [swap faile](/index.php/Swap_file "Swap file").

*Particijų lentelės* modifikacijai naudokite [fdisk](/index.php/Fdisk "Fdisk") ar [parted](/index.php/Parted "Parted").

```
# fdisk /dev/*sda*

```

Dėl daugiau informacijos žiūrėti [Partitioning](/index.php/Partitioning "Partitioning").

**Note:** Jei norite sukurti sukrautus blokinius įrenginius [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") ar [RAID](/index.php/RAID "RAID"), darykite tai dabar.

### Suformatuokite particijas

Kai particijos sukurtos, kiekviena turėtų būti suformatuota atitinkamai [failų systemai](/index.php/File_system "File system"). Pavyzdžiui root particiją esančią `/dev/*sda1*` suformatuoti `*ext4*` sistemai, paleiskite:

```
# mkfs.*ext4* /dev/*sda1*

```

Jei sukūrėte swap particiją (pavyzdžiui `/dev/*sda3*`), inicijuokite ją su *mkswap*:

```
# mkswap /dev/*sda3*
# swapon /dev/*sda3*

```

[Failų sistemos kūrimas](/index.php/File_systems#Create_a_file_system "File systems") rasite daugiau detalių.

### Prijunkite failų sistemas

[Prijunkite](/index.php/Mount "Mount") root particijos failų sistemą prie `/mnt`, pavyzdžiui:

```
# mount /dev/*sda1* /mnt

```

Sukurkite prijungimo taškus visoms likusioms particijoms ir jas atititinkamai prijunkite:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) vėliau aptiks prijungtas failų sistemas ir swap vietą.

## Įdiegimas

### Pasirinkite veidrodžius

Įdiegiami paketai turi būti parsisiųsti iš [mirror servers|veidrodinių serverių](/index.php/Mirrors "Mirrors"), kurie nurodomi `/etc/pacman.d/mirrorlist`. "Live" sistemoje, visi veidrodžiai yra įjungti, surūšiuoti pagal sinchronizacijos statusą ir greitį įdiegimo atvaizdo kūrimo metu.

Kuo sąraše veidrodis aukščiau, tuo didesnis prioritetas jam skiriamas siunčiantis paketą. Failą galima atitinkamai redaguoti, geografiškai artimesnius veidrodžius perkeliant į aukštesnę sąrašo vietą, bet reiktų atsižvelgti ir į kitus kriterijus.

Šį failą į naują sistemą vėliau nukopijuos*pacstrap*, tad viską derėtų atlikti tinkamai.

### Įdiekite pagrininius paketus

Naudokitės [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) skriptu ir įdiekite [base](https://www.archlinux.org/groups/x86_64/base/) paketų grupę:

```
# pacstrap /mnt base

```

Į šią grupę nėra įtrauka viskas kas yra "live" diegime, kaip kad [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) ar specifinė belaidė įranga; palyginimui žiūrėti [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64).

Kitų paketų ir grupių [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) [įdiegimui](/index.php/Install "Install"), pavadinimus pridėkite prie *pacstrap* (atskirdami tarpais) arba inividualiai su [pacman](/index.php/Pacman "Pacman") po [#Chroot](#Chroot) žingsnio.

## Sukonfigūruokite sistemą

### Fstab

Sugeneruokite [fstab](/index.php/Fstab "Fstab") failą (naudokite `-U` arba `-L` nurodant [UUID](/index.php/UUID "UUID") arba etiketes, atitinkamai):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Po to patikrinkite rezultatą faile `/mnt/etc/fstab` , kad nebūtų klaidų.

### Chroot

[Pakeiskite root](/index.php/Change_root "Change root") į naują sistemą:

```
# arch-chroot /mnt

```

### Laiko zona

Nustatykite [laiko zoną](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

Paleiskite [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) norėdami sugeneruoti `/etc/adjtime`:

```
# hwclock --systohc

```

Ši komanda daro prielaidą ka techninės įrangos laikrodis nustatytas į [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). Daugiau detalių čia - [Laiko standartas](/index.php/System_time#Time_standard "System time").

### Lokalizacija

Nukomentuokite `en_US.UTF-8 UTF-8` ir kitas reikalingas [lokales](/index.php/Locale "Locale") `/etc/locale.gen` faile, tada jas sugeneruokite su:

```
# locale-gen

```

Atitinkmai nustatykite `LANG` [kintamąjį](/index.php/Variable "Variable") [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) faile, pavyzdžiui:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

Jeigu [nustatėte klaviatūros išdėstymą](#Nustatykite_klaviatūros_išdėstymą), padarykite pakeitimus pastovius [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) faile:

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### Tinklo konfigūracija

Sukurkite [hostname](/index.php/Hostname "Hostname") failą:

 `/etc/hostname` 
```
*myhostname*

```

Pridėkite atitinkamus įrašus į [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*myhostname*.localdomain	*myhostname*

```

Jei sistema turi nuolatinį IP adresą, naudokite jį vietoje `127.0.1.1`.

Užbaikite naujai įdiegto aplinkos [tinklo konfigūraciją](/index.php/Network_configuration "Network configuration").

### Initramfs

Sukurti naują *initramfs* dažnai nėra reikalinga, nes [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") buvo paleistas [linux](https://www.archlinux.org/packages/?name=linux) paketo diegimo su *pacstrap* metu.

Specialioms konfigūracijoms, modifikuokite [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) failą ir perkurkite failą su:

```
# mkinitcpio -p linux

```

### Root slaptažodis

Nustatykite root [slaptažodį](/index.php/Password "Password"):

```
# passwd

```

### Įkroviklis

Norint įkrauti Arch Linux, turi būti įdiegtas Linux-veikiantis įkroviklis. [Įkrovikliai](/index.php/Category:Boot_loaders "Category:Boot loaders") yra keletas pasirinkimo variantų. Jeigu turite Intel ar AMD CPU, įgalinkite [mikrokodo](/index.php/Microcode "Microcode") atnaujinimus.

## Perkrovimas

Išeikite iš chroot aplinkos parašydami `exit` arba paspaudę `Ctrl+D`.

Papildomai rankiniu būdu galite atjungti visas particijas `umount -R /mnt`: tai leidžia pamatyti "busy" particijas, ir rasti to priežastį su [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Galiausiai, perkraukite sistemą parašę `reboot`: bet kurią visdar prijungtą particiją *systemd* automatiškai atjungs. Nepamirškite pašalinti diegimo laikmenos ir į naują sistemą prisijungti su root paskyra.

## Po diegimo

Sistemos valdymo rekomendacijas ir įvairias po diegimines pamokas (kaip nustatyti grafinę naudotojo aplinką ar sureguliuti garsą) rasite[bendroise rekomendacijose](/index.php/General_recommendations "General recommendations")

Taip pat aplankykite [programų sąrašą](/index.php/List_of_applications "List of applications"), kur galbūt rasite jus dominančių programų.