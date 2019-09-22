Related articles

*   [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")
*   [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [init](/index.php/Init "Init")
*   [systemd](/index.php/Systemd "Systemd")
*   [fstab](/index.php/Fstab "Fstab")
*   [Autostarting](/index.php/Autostarting "Autostarting")

Da bi se mogao bootati Arch Linux, potrebno je podesiti [boot loader](#Boot_loader) koji zna raditi sa Linuxom. Boot loader je odgovoran za učitavanje kernela i [inicijalnog ramdiska](/index.php/Initial_ramdisk "Initial ramdisk") prije započinjanja boot procesa. Procedura se razlikuje za [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") i [UEFI](/index.php/UEFI "UEFI") sisteme, detaljne instrukcije su date na ovoj ili na linkovanim stranicama.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Firmware tipovi](#Firmware_tipovi)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Inicijalizacija sistema](#Inicijalizacija_sistema)
    *   [2.1 Pod BIOS-om](#Pod_BIOS-om)
    *   [2.2 Pod UEFI-om](#Pod_UEFI-om)
    *   [2.3 Višestruko bootanje u UEFI-u](#Višestruko_bootanje_u_UEFI-u)
*   [3 Boot loader](#Boot_loader)
    *   [3.1 Uporedba feature-a](#Uporedba_feature-a)
*   [4 Kernel](#Kernel)
*   [5 initramfs](#initramfs)
*   [6 init proces](#init_proces)
*   [7 getty](#getty)
*   [8 Display menadžer](#Display_menadžer)
*   [9 Login](#Login)
*   [10 Shell](#Shell)
*   [11 GUI, xinit or wayland](#GUI,_xinit_or_wayland)
*   [12 Vidite i](#Vidite_i)

## Firmware tipovi

### BIOS

[BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") ili Basic Input-Output System (Osnovni ulazno-izlazni sistem) je prvi program(firmware) koji se pokreće kada se sistem uključi. U većini slučajeva, smješten je u flash memorije na matičnoj ploči i nezavisan od sistemskog skladišta.

### UEFI

[Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") ima podršku za čitanje tabele particija kao i fajl sistema. UEFI ne pokreće nikakav [boot kode iz Master Boot Recorda-a (MBR)](/index.php/Partitioning#Master_Boot_Record_(bootstrap_code) "Partitioning") bilo da on postoji ili ne, umjesto toga bootanje se oslanja na boot entry-e unutar [NVRAM](https://en.wikipedia.org/wiki/Non-volatile_random-access_memory "wikipedia:Non-volatile random-access memory")-a.

UEFI specifikacije obavezuju podršku za [FAT12, FAT16 i FAT32](/index.php/FAT "FAT") fajl sisteme (vidi [UEFI specifikacija verzija 2.8, sekcija 13.3.1.1](https://uefi.org/sites/default/files/resources/UEFI_Spec_2_8_final.pdf#G17.1019485))), ali drugi vendori mogu dodati podršku za dodatne fajl sisteme; npr, Apple [Mac](/index.php/Mac "Mac") podržava (i po defaultu koriste) svoje HFS+ fajl sistem drivere. UEFI implementacija također podržava ISO-9660 za optičke diskove.

UEFI pokreće EFI aplikacija, npr [boot loadere](#Boot_loader), boot menadžere, [UEFI shell](/index.php/UEFI_shell "UEFI shell")-ove itd. Ove aplikacije su obično spašene kao fajlovi u [EFI sistemskoj particiji](/index.php/EFI_system_partition "EFI system partition"). Svaki vendor može spasiti svoje fajlove u EFI sistemsku particiju pod `/EFI/*vendor_naziv*` folderom. Aplikacija može biti pokrenuta dodavanjem boot entry-a u NVRAM ili iz UEFI shella.

UEFI specifikacija također ima podršku za legacy BIOS bootanje sa svojim [[[Compatibility Support Module (CSM)](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface#CSM_booting "wikipedia:Unified Extensible Firmware Interface") (Modul za podršku kompatibilnosti). Ako je CSM uključen po defaultu, UEFI će generisati CSM boot entry za sve drive-ove. Ako je CSM boot entry odabran da se sistem boota sa njega, UEFI-ov CSM će pokušati da boota sa drive-ovogo MBR bootstrap koda.

## Inicijalizacija sistema

### Pod BIOS-om

1.  Sistem uključen, [power-on self-test (POST)](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test") se izvršava.
2.  Nakon POST-a, BIOS inicijalizira potrebni sistemski hardware za bootanje (disk, kontrolere tastature, itd.).
3.  BIOS pokreće prvih 440 bajtova ([Master Boot Record-a bootstrap koda](/index.php/Partitioning#Master_Boot_Record_(bootstrap_code) "Partitioning")) prvog diska u BIOS disk poretku bootanja.
4.  Boot loaderova prva faza je u MBR boot kodu i zatim pokreće drugu fazu (ako je ima) sa:
    *   sljedećeg disk sektora poslije MBR-a, tzv. post-MBR gap
    *   [volume boot record-a (VBR)](https://en.wikipedia.org/wiki/Volume_boot_record "wikipedia:Volume boot record") sa particije
    *   [BIOS boot particije](/index.php/BIOS_boot_partition "BIOS boot partition") ([GRUB](/index.php/GRUB "GRUB") na BIOS/GTP samo).
5.  Aktuelni [boot loader](#Boot_loader) je pokrenut.
6.  Boot loader zatim učitava operativni sistem za lančanim učitavanjem ili direktni učivanjem kernela operativnog sistema.

### Pod UEFI-om

1.  Sistem uključen, [power-on self-test (POST)](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test") se izvršava.
2.  UEFI inicijalizira hardware potreban za bootanje.
3.  Firmware čita boot entry-e iz NVRAM-a da zaključi koju EFI aplikaciju da pokrene i odakle (npr. sa kojeg diska i koje particije).
4.  Boot entry može jednostavno biti disk. U ovom slučaju, firmware traži [EFI sistemsku particiju](/index.php/EFI_system_partition "EFI system partition") na tom disku i pokušava da nađe EFI aplikaciju u fallback boot putanji `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI`) na [sistemima sa IA32 (32-bit) UEFI](/index.php/Unified_Extensible_Firmware_Interface#UEFI_firmware_bitness "Unified Extensible Firmware Interface")). Ovako radi bootabilni UEFI removable media.
5.  Firmware pokreće zatim EFI aplikaciju.
    *   Ovo može biti [boot loader](#Boot_loader) ili Arch [kernel](/index.php/Kernel "Kernel") koristeći [EFISTUB](/index.php/EFISTUB "EFISTUB").
    *   To može biti neka drugi EFI aplikacija, poput UEFI shella ili [boot menadžera](#Boot_loader) poput [systemd-boot](/index.php/Systemd-boot "Systemd-boot")-a ili [rEFInd](/index.php/REFInd "REFInd")-a.

Ako je [Secure Boot](/index.php/Secure_Boot "Secure Boot") uključen, boot process će verifikovati autentičnost EFI binary-a gledajući potpis.

**Note:** Neki UEFI sistemi se samo mogu bootati sa fallback boot putanje.

### Višestruko bootanje u UEFI-u

Pošto svaki OS ili vendor može održavati svoje fajlove unutar [EFI sistemske particija](/index.php/EFI_system_partition "EFI system partition") bez da utiče na druge, višestruko bootanje koristeći UEFI postaje stvar pokretanje druge EFI aplikacije koja odgovara boot loaderu toga operativnog sistema. Ovo uklanja potrebu za oslanjanjem na mehanizam [lančanog učitavanja](https://en.wikipedia.org/wiki/Chain_loading "wikipedia:Chain loading") jednog [boot loadera](#Boot_loader) da se učita drugi OS.

Vidite i [Dual boot sa Windowsom](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## Boot loader

Boot loader je dio software pokrenut od strane [BIOS-a](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") ili [UEFI](/index.php/UEFI "UEFI")-a. Odgovoran je za učitavanje kernela sa željenim [kernel parametrima](/index.php/Kernel_parameters "Kernel parameters") i [inicijalnim RAM diskom](/index.php/Mkinitcpio "Mkinitcpio") bazirano na konfiguracijskim fajlovima. U slučaju UEFI-a, kernel može se direktno pokrenuti od strane UEFI-a koristeći EFI boot stub. Odvojeni boot loader ili boot menadžer može i dalje biti korišten za editovanje kernel parametara prije bootanja.

**Note:** Učitavanje [update-a mikro koda](/index.php/Microcode "Microcode") zahtjeva podešavanja konfiguracije boot loadera. [[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

### Uporedba feature-a

**Note:**

*   Boot loaderi trebaju samo da podržavaju fajl sistem na kojem se nalaze kernel i initramfs (fajl sistem na kojem je `/boot`).
*   Pošto je GPT dio UEFI specifikacije, svi UEFI boot loaderi podržavaju GTP diskove. GPT na BIOS sistemima je moguć korištenjem ili "hibridnog bootanja" sa [Hybrid MBR](https://www.rodsbooks.com/gdisk/hybrid.html) ili novijim [GPT-only](http://repo.or.cz/syslinux.git/blob/HEAD:/doc/gpt.txt) protokolom. Ovaj protokol zna praviti probleme sa određenim BIOS implementacijama; vidite [rodsbooks](http://www.rodsbooks.com/gdisk/bios.html#bios) za detalje.
*   Metoda enkripcije spomenuta u podršci za fajl sistem je [filesystem-level encryption](https://en.wikipedia.org/wiki/Filesystem-level_encryption "wikipedia:Filesystem-level encryption") (Enkripcija na nivou fajl sistema), ne utiče na [block-level encryption](/index.php/Dm-crypt "Dm-crypt").

| Name | Firmware | [Partition table](/index.php/Partition_table "Partition table") | Multi-boot | [File systems](/index.php/File_systems "File systems") | Notes |
| BIOS | [UEFI](/index.php/UEFI "UEFI") | [MBR](/index.php/MBR "MBR") | [GPT](/index.php/GPT "GPT") | [Btrfs](/index.php/Btrfs "Btrfs") | [ext4](/index.php/Ext4 "Ext4") | ReiserFS | [VFAT](/index.php/VFAT "VFAT") | [XFS](/index.php/XFS "XFS") |
| [EFISTUB](/index.php/EFISTUB "EFISTUB") | – | Yes | Yes | Yes | – | – | – | – | ESP only | – | Kernel preveden u EFI executable da se učita direktno iz [UEFI](/index.php/UEFI "UEFI") firmware ili iz drugog boot loadera. |
| [Clover](/index.php/Clover "Clover") | emulates UEFI | Yes | Yes | Yes | Yes | No | bez enkripcije | No | Yes | No | Fork od rEFIt-a modifikovan da pokreće [macOS na non-Apple hardware-u](https://en.wikipedia.org/wiki/Hackintosh "wikipedia:Hackintosh"). |
| [GRUB](/index.php/GRUB "GRUB") | Yes | Yes | Yes | Yes | Yes | bez zstd kompresije | Yes | Yes | Yes | Yes | Na BIOS/GTP konfiguraciji zahtjeva [BIOS boot particiju](/index.php/BIOS_boot_partition "BIOS boot partition").
Podržava RAID, LUKS1 i LVM |
| [rEFInd](/index.php/REFInd "REFInd") | No | Yes | Yes | Yes | Yes | bez: enkripcije, zstd kompresije | bez enkripcije | bez tail-packing feature-a | Yes | No | Podržava automatsko detektovanje kernela i parametara bez eksplicitne konfiguracije. |
| [Syslinux](/index.php/Syslinux "Syslinux") | Yes | [Parcijalno](/index.php/Syslinux#Limitations_of_UEFI_Syslinux "Syslinux") | Yes | Yes | [Parcijalno](/index.php/Syslinux#Chainloading "Syslinux") | bez: multi-device volume-a, kompresije, enkripcije | bez enkripcije | No | Yes | MBR samo; bez prorijeđenih inode-ova | Bez podrške za određene [fajl sistem](/index.php/File_system "File system") feature. [[2]](https://wiki.syslinux.org/wiki/index.php?title=Filesystem)
Boot loader može samo pristupiti fajl sistemu na koji je instaliran.[[3]](https://bugzilla.syslinux.org/show_bug.cgi?id=33) |
| [systemd-boot](/index.php/Systemd-boot "Systemd-boot") | No | Yes | [Manuelna instalacija samo](https://github.com/systemd/systemd/issues/1125) | Yes | Yes | No | No | No | ESP only | No | Ne može pokrenuti binary-e iz particija mimo [ESP](/index.php/ESP "ESP"). |
| [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") | Yes | No | Yes | No | Yes | No | No | Yes | Yes | v4 only | [Zamijenjen](https://www.gnu.org/software/grub/grub-legacy.html) sa [GRUB](/index.php/GRUB "GRUB")-om. |
| [LILO](/index.php/LILO "LILO") | Yes | No | Yes | No | Yes | No | bez enkripcije | Yes | Yes | [Yes](http://xfs.org/index.php/XFS_FAQ#Q:_Does_LILO_work_with_XFS.3F) | [Zamijenjen](http://web.archive.org/web/20180323163248/http://lilo.alioth.debian.org/) zbog nekih limita (npr. sa Btrfs, GPT, RAID). |

1.  A [boot menadžer](https://www.rodsbooks.com/efi-bootloaders/principles.html). Može samo pokretati druge EFI aplikacije, npr, Linux kernel image buildan sa `CONFIG_EFI_STUB=y` i Windows `bootmgfw.efi`.

Vidite i [Uporedba boot loadera](https://en.wikipedia.org/wiki/Comparison_of_boot_loaders "wikipedia:Comparison of boot loaders").

## Kernel

[Kernel](/index.php/Kernel "Kernel") je jezgro operativnog sistema. Radi na niskom nivou (*kernelspace*) gdje vrši interakciju između hardware-a na mašini i programa koji koriste hardware da se pokreću. Da se iskoristi CPU efikasno, kernel koristi scheduler da određuje koji task ima prioritet izvršavanja u datom trenutku, te tako kreira iluziju da se više taskova izvršava simultano.

## initramfs

Nakon što [boot loader](#Boot_loader) učita [kernel (Bosanski)](/index.php/Kernel_(Bosanski) "Kernel (Bosanski)") i moguće initramfs fajlovu te izvrši kernel, kernel zatim raspakuje initramfs (inicijalni RAM fajl sistem) arhivu u (tada prazan) rootfs (inicijalni root fajl sistem, specifično ramfs ili tmpfs). Prvi ekstraktovani initramfs je onaj koji je ugrađen u kernel binary tokom buildanja kernela, zatim se eventualni drugi initramfs fajlovi ekstraktuju. Što znači da eksterni fajlovi sa istim imenom prepisuju one u ugrađenom initramfs-u. Kernel zatim izvršava `/init` (u rootfs-u) kao prvi proces. *Rani userspace* time je započeo.

Arch Linux koristi praznu arhivu kao ugrađeni initramfs (defaultno tokom buildanja Linuxa). Vidite [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") za više Arch specifičnih informacija o eksternom initramfs-u.

Svrha initramfs-a je da bootstrapa sistem do tačke gdje može da pristupi root fajl sistemu (vidite [FHS](/index.php/FHS "FHS") za detalje). To znači da bilo koji moduli koji su potrebni za uređaje, poput IDE, SCSI, SATA, USB/FW (ako se boota sa eksternog uređaja) moraju se moći učitati iz initramfs-a ako nisu buildani u kernel; nakon što su odgovarajući kernel moduli učitani (eksplicitno koristeći program ili skriptu ili implicitno sa [udev](/index.php/Udev "Udev")-om), boot proces se nastavlja. Iz ovog razloga, initramfs treba samo da sadržava module potrebne za pristup root fajl sistemu; ne treba da ima sve module koji će se koristiti. Većina modula će se kasnije učitati od strane udev-a, tokom init procesa.later on by udev, during the init process.

## init proces

Na zadnjoj fazi ranog userspace-a, stvarni root je mountan i zamjenjuje inicijalni root fajl sistem. `/sbin/init` se izvršava, zamjenjujući `/init` proces. Arch koristi [systemd](/index.php/Systemd "Systemd") kao defaultni [init](/index.php/Init "Init").

## getty

[init](/index.php/Init "Init") poziva [getty](/index.php/Getty "Getty") jednom za svaki [virtualni termina](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (obično 6 ih ima), koji inicijalizira svaki tty i pita za username i lozinku. Nakon što su username i lozinka ukucani, getty ih provjerava gledajući u `/etc/passwd` i `/etc/shadow` te zatim poziva [login](#Login). Alternativno, getty može pokrenuti display menadžera ukoliko postoji na sistemu.

## Display menadžer

[Display menadžer](/index.php/Display_manager "Display manager") može biti konfigurisan da zamijenit getty login prompt na tty-u.

Da bi se automatski inicijalizirao display menadžer nakon bootanja, potrebno je manuelno uključiti service unit-e sa [systemd](/index.php/Systemd "Systemd")-om. Za više informacija vezanih za enablanje i startanje service unit-a, vidite [systemd#Using units](/index.php/Systemd#Using_units "Systemd").

## Login

*login* program započinje sesiju za korisnika tako što podešava environment varijable i pokreće korisnički shell, bazirano na `/etc/passwd`.

*login* program prikaziju sadržaj [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (*m*essage *o*f *t*he *d*ay) (poruka dana) nakon uspješnog logovanja, prije nego što izvrši shell. To je dobro mjesto za prikazati Uslove korištenja da se podsjete korisnici lokalnih polica ili bilo čega drugog što želite da im kažete.

## Shell

Nakon što je korisnički [shell](/index.php/Shell "Shell") pokrenut, obično se pokreće runtime konfiguracijski fajl, poput [bashrc](/index.php/Bashrc "Bashrc") prije prikazivanja prompta korisniku. Ako je korisnički account podešen za [pokretanje X na loginu](/index.php/Start_X_at_login "Start X at login"), runtime konfiguracijski fajl će pozvati [startx](/index.php/Startx "Startx") ili [xinit](/index.php/Xinit "Xinit").

## GUI, xinit or wayland

[xinit](/index.php/Xinit "Xinit") pokreće korisnički [xinitrc](/index.php/Xinitrc "Xinitrc") runtime konfiguracijski fajl, koji obično pokreće [window menadžera](/index.php/Window_manager "Window manager"). Nakon što korisnik završi i izađe iz window menadžera, *xinit*, *startx*, shell i login će se izgasiti u ovom redu, vraćajući se na [getty](#getty).

## Vidite i

*   [Early Userspace in Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
*   [Kernel Newbie Corner: initrd and initramfs](https://www.linux.com/learn/kernel-newbie-corner-initrd-and-initramfs-whats)
*   [Rod Smith - Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/)