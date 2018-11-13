Related articles

*   [Remastering the Install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO")
*   [Archiso as pxe server](/index.php/Archiso_as_pxe_server "Archiso as pxe server")

**Archiso** je malá skupina bashových skriptov schopných vybudovať plne funkčný Arch Linux obraz pre CD a USB. Je to nástroj na generovanie oficiálnych CD/USB obrazov, avšak je to veľmi všeobecný nástroj a potenciálne môže byť využitý na generovanie hocičoho od záchranných systémov, inštalačných diskov, špeciálne zameraných CD/DVD/USB systémov a ktovie čoho ešte. Srdcom a dušou Archisa je mkarchiso. Všetky jeho možnosti sú popísané v jeho výpise použitie, takže tu nebude popísané jeho priame použitie. Miesto toho bude tento wiki článok v pozícii príručky pre veľmi rýchle vytvorenie live média.

## Contents

*   [1 Nastavenie](#Nastavenie)
*   [2 Konfigurácia nášho live média](#Konfigurácia_nášho_live_média)
    *   [2.1 Inštalácia balíčkov](#Inštalácia_balíčkov)
        *   [2.1.1 Vlastný lokálny repozitár](#Vlastný_lokálny_repozitár)
        *   [2.1.2 Vyhnutie sa inštalácii balíčkov patriacich do základnej skupiny](#Vyhnutie_sa_inštalácii_balíčkov_patriacich_do_základnej_skupiny)
    *   [2.2 Pridávanie užívateľa](#Pridávanie_užívateľa)
    *   [2.3 Pridávanie súborov do obrazu](#Pridávanie_súborov_do_obrazu)
    *   [2.4 Boot Loader](#Boot_Loader)
    *   [2.5 Login manažér](#Login_manažér)
    *   [2.6 Zmena automatického prihlasovania](#Zmena_automatického_prihlasovania)
*   [3 Budovanie ISO obrazu](#Budovanie_ISO_obrazu)
    *   [3.1 Prebudovanie ISO obrazu](#Prebudovanie_ISO_obrazu)
*   [4 Použitie ISO obrazu](#Použitie_ISO_obrazu)
    *   [4.1 CD](#CD)
    *   [4.2 USB](#USB)
    *   [4.3 GRUB](#GRUB)
    *   [4.4 grub4dos](#grub4dos)
*   [5 Inštalácia bez prístupu na internet](#Inštalácia_bez_prístupu_na_internet)
    *   [5.1 Inštalácia archisa do nového koreňového adresára](#Inštalácia_archisa_do_nového_koreňového_adresára)
    *   [5.2 Zmena práv (chroot) a konfigurácia základného systému](#Zmena_práv_(chroot)_a_konfigurácia_základného_systému)
        *   [5.2.1 Obnova konfigurácie journald](#Obnova_konfigurácie_journald)
        *   [5.2.2 Obnova konfigurácie pam](#Obnova_konfigurácie_pam)
        *   [5.2.3 Zmazanie špeciálneho udev pravidla](#Zmazanie_špeciálneho_udev_pravidla)
        *   [5.2.4 Zablokovanie a zmazanie služieb vytvorených archisom](#Zablokovanie_a_zmazanie_služieb_vytvorených_archisom)
        *   [5.2.5 Zmazanie špeciálnych skriptov live prostredia](#Zmazanie_špeciálnych_skriptov_live_prostredia)
        *   [5.2.6 Opravenie prístupových práv k domovskému adresáru roota](#Opravenie_prístupových_práv_k_domovskému_adresáru_roota)
        *   [5.2.7 Nastavte archu heslo](#Nastavte_archu_heslo)
*   [6 Pozrite tiež](#Pozrite_tiež)
    *   [6.1 Dokumentácia a tutoriály](#Dokumentácia_a_tutoriály)
    *   [6.2 Príklad šablony na prispôsobenie](#Príklad_šablony_na_prispôsobenie)

## Nastavenie

**Note:** Pri nasledujúcich krokoch sa odporúča byť prihlásený ako root. V opačnom prípade je pravdepodobné, že budete mať problémy s prístupovými právami.

Skôr než začneme, musíme [nainštalovať](/index.php/Pacman "Pacman") [archiso](https://www.archlinux.org/packages/?name=archiso) z [oficiálnych repozitárov](/index.php/Official_repositories "Official repositories"). Alternatívne sa môže použiť [archiso-git](https://aur.archlinux.org/packages/archiso-git/) z [AURu](/index.php/AUR "AUR").

Vytvorte adresár, v ktorom budete pracovať. Ten bude priestorom, kde sa budú nachádzať všetky modifikácie. `~/archlive` by malo byť postačujúce.

```
$ mkdir ~/archlive

```

Archiso skripty, ktoré sa skôr nainštalovali do hostiteľského systému, je teraz potrepné prekopírovať do novovytvoreného adresára, v ktorom sa bude pracovať.

Archiso prichádza s dvoma "profilmi": *releng* a *baseline*.

Ak si želáte vytvoriť plne prispôsobenú live verziu Arch Linuxu predinštalovanú so všetkými vašimi obľúbenými programami a konfiguráciami, použite *releng*.

Ak len chcete vytvoriť čo najzákladnejšie live médium so žiadnymi predinštalovanými balíčkami a minimalistickou konfiguráciu, použite *baseline*.

Vzhľadom na váš výber, spustite nasledovný príkaz, pričom nahraďte 'PROFILE' reťazcom **releng** alebo **baseline**.

```
# cp -r /usr/share/archiso/configs/**PROFILE**/ ~/archlive

```

Ak používate profil *releng* k vytvoreniu plne prispôsobeného obrazu, potom pokračujte sekciou [#Konfigurácia nášho live média](#Konfigurácia_nášho_live_média)

Ak používate profil *baseline* k vytvoreniu okliešteného obrazu, potom nebudete potrebovať robiť žiadne prispôsobenia a môžete pokračovať sekciou [#Budovanie ISO obrazu](#Budovanie_ISO_obrazu).

## Konfigurácia nášho live média

Táto sekcia detailne popisuje konfiguráciu obrazu, ktorý vytvoríte. Popisuje definíciu balíčkov a konfigurácii ktoré chcete mať vo vašom live obraze.

Vojdite do adresára, ktorý sme vytvorili skôr (~/archlive/releng/ ak postupujete podľa tejto príručky). Uvidíte v ňom množstvo súborov a adresárov. My sa zameráme len na pár z nich, predovšetkým: packages.* - toto je miesto, kde napíšete do samostatných riadkov názvy balíčkov, ktoré chcete mať predinštalované, a adresár airootfs - tento adresár je v úlohe medzivrstvy a tu sa vykonávajú všetky prispôsobenia.

Vo všeobecnosti každá administratívna úloha, ktorú by ste normálne spravili po čistej inštalácii (okrem inštalácie balíčkov), môže byť naskriptovaná v súbore `~/archlive/releng/airootfs/root/customize-airootfs.sh`. Musí byť písaný z pohľadu nového prostredia, takže / v skripte znamená koreňový adresár live-iso média, ktoré bude vytvorené.

### Inštalácia balíčkov

Budete chcieť vytvoriť zoznam balíčkov, ktoré budú obsiahnuté vo vašom live systéme. Do súboru sa napíšu riadok za riadkom názvy baličkov. Je to ***skvelé*** pre špeciálne zamerané live CD. Stačí špecifikovať balíčky v súbore packages.both a vytvoriť image. Súbory packages.i686 a packages.x84_64 umožnia inštalovať software pre 32bitový systém, resp. pre 64 bitový.

Ak budete chcieť neskôr nainštalovať systém v prostredí bez internetového pripojenia, alebo budete chcieť preskočiť opätovné sťahovanie súborov, odporúčam nainštalovať "rsync".

#### Vlastný lokálny repozitár

Taktiež môžete [vytvoriť vlastný lokálny repozitár](/index.php/Custom_local_repository "Custom local repository") pre účel prípravy vlastný balíčkov alebo balíčkov z [AUR](/index.php/AUR "AUR")/[ABS](/index.php/ABS "ABS"). Keď tak spravíte s balíčkami pre obe architektúry, mali by ste dodržať presnú adresárovú štruktúru, aby ste sa nedostali do problémov.

Napríklad:

*   `~/vlastnarepo`
    *   `~/vlastnarepo/x86_64`
        *   ~/vlastnarepo/x86_64/foo-x86_64.pkg.tar.xz
        *   ~/vlastnarepo/x86_64/vlastnarepo.db.tar.gz
        *   ~/vlastnarepo/x86_64/cvlastnarepo.db (odkaz vytvorený pomocou `repo-add`)
    *   `~/vlastnarepo/i686`
        *   ~/vlastnarepo/i686/foo-i686.pkg.tar.xz
        *   ~/vlastnarepo/i686/vlastnarepo.db.tar.gz
        *   ~/vlastnarepo/i686/vlastnarepo.db (odkaz vytvorený pomocou `repo-add`)

Potom môžete pridať váš repozitár pridaním nasledovného kódu do `~/archlive/releng/pacman.conf`. Umiestnite ho nad ostatné záznamy (pre najvyššiu prioritu).

```
# vlastný repozitár
[vlastnyrepo]
SigLevel = Optional TrustAll
Server = file:///home/**užívateľ**/vlastnarepo/$arch

```

Budovacie skripty sú tým pripravené pre vybrané balíčky.

Ak tomu tak nie je, môžu sa objaviť chybové správy podobné nasledujúcej:

```
error: failed to prepare transaction (package architecture is not valid)
:: package foo-i686 does not have a valid architecture

```

#### Vyhnutie sa inštalácii balíčkov patriacich do základnej skupiny

Vo všeobecnosti `/usr/bin/mkarchiso`, skript využívaný v `~/archlive/releng/build.sh`, volá skript nazvaný `pacstrap`, patriaci do balíčka [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts), bez parametra `-i`, čo spôsobí, že [Pacman](/index.php/Pacman "Pacman") nebude čakať na vstup užívateľa počas inštalačného procesu.

Tým, že balíčky (zo základnej skupiny), ktoré sa nemajú inštalovať, pridáte do riadku `IgnorePkg` v súbore `~/archlive/releng/pacman.conf`, sa [Pacman](/index.php/Pacman "Pacman") aj napriek tomu spýta, či si tieto balíčky želáte nainštalovať. A keďže je vstup užívateľa potlačený, balíčky sa nakoniec nainštalujú. Existuje niekoľko možností, ako sa tomu vyhnúť:

*   **Nepekné**: Pridajte parameter `-i` do každého riadku volajúceho `pacstrap` v súbore `/usr/bin/mkarchiso`.

*   **Čisté**: Vytvorte kópiu súboru `/usr/bin/mkarchiso`, do ktorého pridáte parameter a upravte `~/archlive/releng/build.sh` tak, aby volal modifikovanú verziu skriptu mkarchiso.

*   **Pokročilé**: Vytvorte funkciu pre `~/archlive/releng/build.sh`, ktorá explicitne zmaže balíčky po základnej inštalácii. Tým sa zbavíte otravného enetrovania počas inštalačného procesu.

### Pridávanie užívateľa

So správou užívateľov môžete zaobchádzať rovnako, ako počas bežnej inštalácie, až na to, že vaše príkaze musíte umiestniť do skriptu `~/archlive/releng/airootfs/root/customize_airootfs.sh`. Ďalšie informácie nájdete na stránke [správy užívateľov](/index.php/Users_and_groups#User_management "Users and groups").

### Pridávanie súborov do obrazu

**Note:** Aby ste to mohli spraviť, musíte byť prihlásený ako root. Nemeňte vlastníctvo žiadneho kopírovaného súboru. **Všetko** v rámci adresára airootfs musí vlastniť root. Vhodné nastavenie vlastníctva bude riešené zachvíľu.

Adresár airootfs vystupuje ako medzivrstva, predstavujte si ho ako rootovský adresár '/' na vašom aktuálnom systéme. Všetky tu umiestnené súbory sa budú nachádzať aj vo vytvorenom live systéme.

Takže ak máte v súčasnom systéme naskriptované IP tabuľky a chcete ich používať aj vo vašom live systéme, skopírujte ich nasledovne:

```
# cp -r /etc/iptables ~/archlive/releng/airootfs/etc

```

Umiestňovanie súborov do domovského adresára sa mierne líši. Neumiestňujte ich do adresára airootfs/home, ale radšej vytvorte adresár skel v airootfs/etc a umiestnite ich doňho. Neskôr pridáme určité príkazy do skriptu customize_root_image.sh, ktorý využijeme na prekopírovanie týchto súborov a nastavení prístupových práv pri bootovaní systému.

Najprv vytvorte prázdny adresár. Uistite sa, že ste v adresári ~/archlive/releng/airootfs/etc (ak je to ten, z ktorého pracujete):

```
# cd ~/archlive/releng/airootfs/etc && mkdir skel

```

Teraz skopírujte 'domovské' súbory do adresára skel, stále všetko robte ako root! Napríklad pre .bashrc.

```
# cp ~/.bashrc ~/archlive/releng/airootfs/etc/skel/

```

Po spustení skriptu `~/archlive/releng/airootfs/root/customize-airootfs.sh` a vytvorení nového užívateľa sa súbory z adresára skel automaticky nakopírujú do nového domovského adresára so správnymi prístupovými právami.

### Boot Loader

Predvolený súbor by mal fungovať, takže by nemalo byť potrebné do neho zasahovať.

Vzhľadom na modularitu isolinuxu máte možnosť použiť množstvo add-onov. Pozrite si [oficiálne stránky syslinuxu](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) a [git repozitár archisa](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). Využitím spomínaných add-onov je možné vytvoriť vizuálne atraktívnejšie a komplexnejšie menu. Pozrite sa [sem](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

### Login manažér

X server je možné spustiť automaticky po nabootovaní povolením [systemd](/index.php/Systemd "Systemd") služby vášho login manažéra. Ak viete, na ktorý .service je potrebné vyvoriť odkaz, tak je to skvelé. Ak neviete, môžete to jednoducho zistiť v prípade, že používate rovnaký program ako ten, ktorý chcete použiť v live médiu. Stačí zadať príkaz

```
# systemctl disable **nazovVashoLoginManazera**

```

pre jeho dočasné vypnutie. Teraz zadajte rovnaký príkaz, akurát nahraďte slovo "disable" za "enable", aby sa služba znova aktivovala. Systemctl zobrazí informáciu o odkaze, ktorý práve vytvoril. Teraz vojdite do adresára ~/archiso/releng/airootfs/etc/systemd/system a vytvorte tu rovnaký odkaz.

Napríklad (uistite sa, že ste buď v adresári ~/archiso/releng/airootfs/etc/systemd/system, alebo pridajte adresu do príkazu):

```
# ln -s /usr/lib/systemd/system/lxdm.service display-manager.service

```

Týmto sa povolí služba LXDM po spustení vášho live systému.

### Zmena automatického prihlasovania

Konfigurácia automatického prihlasovania pre getty sa nachádza v súbore airootfs/etc/systemd/system/getty@tty1.service.d/autologin.conf.

Ak chcete zmeniť automaticky prihlasovaného užívateľa, mali by ste modifikovať tento súbor:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --autologin **isouzivatel** --noclear %I 38400 linux

```

Alebo ho zmažte, ak chcete zabrániť automatickému prihlasovaniu.

## Budovanie ISO obrazu

Teraz ste pripravený vytvoriť z pripravených súborov obraz .iso, ktorý potom môžete napáliť na CD, alebo nahrať na USB: Z adresára, v ktorom ste pracovali (buď ~/archlive/releng, alebo ~/archlive/baseline), spustite:

```
# ./build.sh -v

```

Tento skript najprv stiahne a nainštaluje balíčky, ktoré ste si zvolili, do adresára work/*/airootfs, vytvorí kernel a inicializačné obrazy, aplikuje všetky požadované prispôsobenia a na záver vytvorí iso obraz do adresára out/.

**Note:** Ak chcete používať na vašom Live CD nejakého [správcu okien](/index.php/Window_manager "Window manager"), musíte pridať všetky potrebné a správne [grafické ovládače](/index.php/Video_drivers "Video drivers"), pretože inak môže správca pri načítaní zamrznúť.

### Prebudovanie ISO obrazu

Ak si želáte prebudovať váš iso obraz po pár modifikáciách, musíte zmazať zámkové súbory v pracovnom adresári:

```
# rm -v work/build.make_*

```

## Použitie ISO obrazu

### CD

Jednoducho napáľte iso súbor na cd. Ak chcete, môžete postupovať podľa príručky [napaľovania CD](/index.php/CD_Burning "CD Burning").

### USB

Pozrite si informácie o [USB flashke ako inštalačnom médiu](/index.php/USB_flash_installation_media "USB flash installation media").

### GRUB

Pozrite si informácie o [viacbootovateľnej USB jednotke](/index.php/Multiboot_USB_drive#Arch_Linux "Multiboot USB drive").

### grub4dos

Grub4dos je utilita, ktorú je možné využiť na vytvorenie viacbootovateľných USBčiek schopných obsahovať viacero linuxových distribúcií na jednej USB jednotke.

Pre nabootovanie vytvoreného systému nachádzajúcom sa na usb, kde je grub4dos už nainštalovaný, namountujte ISO súbor a skopírujte celý adresár `/arch` do **koreňového adresára usb**. Potom z grub4dos upravte súbor `menu.lst` (musí byť v koreňovom adresári usb) a pridajte tieto riadky:

```
title Archlinux x86_64
kernel /arch/boot/x86_64/vmlinuz archisolabel=<menovka vášho usb>
initrd /arch/boot/x86_64/archiso.img

```

Podľa potreby zmeňte časť `x86_64` a doplňte **skutočnú** menovku usb.

## Inštalácia bez prístupu na internet

Ak si želáte nainštalovať archiso v stave akom je bez internetového pripojenia (napr. [oficiálne mesačné vydanie](https://www.archlinux.org/download/)), alebo ak si neželáte opätovne sťahovať balíčky:

### Inštalácia archisa do nového koreňového adresára

Miesto inštalácie balíčkov za pomoci utilitky `pacstrap`(ktorá sťahuje všetky balíčky zo vzdialených repozitárov a my teraz nemáme na internet prístup) skopírujte prosím *všetko* v Live prostredí do nového koreňového adresára:

```
# time (cp -ax /{usr,bin,lib,lib64,sbin,etc,home,opt,root,srv,var} /mnt)

```

**Note:** Tento príkaz vynecháva niektoré špeciálne adrsáre, ktoré by nemali byť kopírované do nového koreňového adresára.

Potom vytvorte pár adresárov a do koreňového adresára nakopírujte obraz kernelu. Pekne po poradí, aby bola zachovaná integrita nového systému:

```
# mkdir -vm755 /mnt/{boot,dev,run,mnt}
# cp -vaT /run/archiso/bootmnt/arch/boot/$(uname -m)/vmlinuz /mnt/boot/vmlinuz-linux
# mkdir -vm1777 /mnt/tmp
# mkdir -vm555 /mnt/{sys,proc}

```

### Zmena práv (chroot) a konfigurácia základného systému

Teraz si zmeňte práva do novoinštalovaného systému:

```
# arch-chroot /mnt /bin/bash

```

Prosím majte na pamäti, že skôr než budete konfigurovať locale, keymap, ... treba spraviť ešte niečo dôležité, aby ste sa vyhli skúmaniu Live prostredia(inými slovami, prispôsobiť archiso, ktoré nemá súvis s ne-Live prostredím).

#### Obnova konfigurácie journald

[Toto prispôsobenie archisa](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/root/customize_airootfs.sh#n19) bude viesť k ukladaniu systémového žurnálu do pamäte RAM, čo znamená, že žurnál nebude dostupný po reštarte systému:

```
# sed -i 's/Storage=volatile/#Storage=auto/' /etc/systemd/journald.conf

```

#### Obnova konfigurácie pam

[Táto konfigurácia pam-u](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/pam.d/su) síce zničí bezpečnosť vášho nového systému, ale odporúča sa použiť predvolenú konfiguráciu:

 `# nano /etc/pam.d/su` 
```
#%PAM-1.0
auth            sufficient      pam_rootok.so
# Ak chcete implicitne dôverovať užívateľom v skupine "wheel", odkomentujte nasledujúci riadok.
**#auth           sufficient      pam_wheel.so trust use_uid**
# Ak chcete požadovať, aby bol užívateľ členom skupiny "wheel", odkomentujte nasledujúci riadok.
#auth           required        pam_wheel.so use_uid
auth            required        pam_unix.so
account         required        pam_unix.so
session         required        pam_unix.so

```

#### Zmazanie špeciálneho udev pravidla

[Toto pravidlo udev-u](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) automaticky spustí dhcpcd, ak sa nájde nejaké pevné sieťové rozhranie.

```
# rm /etc/udev/rules.d/81-dhcpcd.rules

```

#### Zablokovanie a zmazanie služieb vytvorených archisom

Niektoré služby a súbory boli vytvorené špeciálne pre live prostredie. Zablokujte prosím tieto služby a zmažte nepotrebné súbory pre nový systém:

```
# systemctl disable pacman-init.service choose-mirror.service
# rm -r /etc/systemd/system/{choose-mirror.service,pacman-init.service,etc-pacman.d-gnupg.mount,getty@tty1.service.d}
# rm /etc/systemd/scripts/choose-mirror

```

#### Zmazanie špeciálnych skriptov live prostredia

V archise sa taktiež nachádzajú skripty, ktoré sú nepotrebné pre nový systém:

```
# rm /etc/systemd/system/getty@tty1.service.d/autologin.conf
# rm /root/{.automated_script.sh,.zlogin}
# rm /etc/sudoers.d/g_wheel
# rm /etc/mkinitcpio-archiso.conf
# rm -r /etc/initcpio

```

#### Opravenie prístupových práv k domovskému adresáru roota

**Note:** Tento nedostatok bol zafixovaný vo v17(oficiálne ako mesačné vydanie: 2014.08.01), takže tento krok je potrebný len pri staršom live obraze.

```
# chmod 700 /root

```

#### Nastavte archu heslo

[Pomocný skript](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/root/customize_airootfs.sh#n13) vytvoril pre live prostredie normálneho užívateľa nazvaného `arch`. Užívateľovi `arch` môžete nastaviť heslo pre prihlasovanie(v predvolenom stave nemá `arch` nastavené žiadne heslo) nasledovne: You can set a passwd for user `arch` in order to login with this username(there is no passwd for `arch` by default):

```
# passwd arch

```

Ak však nechcete používať toto používateľské meno, zmažte ho:

```
# userdel -r arch

```

## Pozrite tiež

### Dokumentácia a tutoriály

*   [Projektová stránka Archisa](https://projects.archlinux.org/archiso.git)
*   [Oficiálna dokumentácia](https://projects.archlinux.org/archiso.git/tree/docs)
*   [Návod na vytvorenie vlastného Live Arch Linux USB](http://blog.jak.me/2011/09/07/creating-a-custom-arch-linux-live-usb/)

### Príklad šablony na prispôsobenie

*   [Live DJ distribúcia ArchLinuxu vybudovaná pomocou Archisa](http://didjix.blogspot.com/)