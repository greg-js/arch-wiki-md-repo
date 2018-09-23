Related articles

*   [Installation guide (Lietuviškai)](/index.php/Installation_guide_(Lietuvi%C5%A1kai) "Installation guide (Lietuviškai)")
*   [General recommendations](/index.php/General_recommendations "General recommendations")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

Šis puslapis paaiškina kaip atlikti įprastą Arch Linux diegimą į USB raktą. Priešingai nei LiveUSB kuris aprašytas - [USB diegimo laikmena](/index.php/USB_flash_installation_media "USB flash installation media"), rezultate gausime nuolatinę sistemą įdentišką diegiant į kietąjį diską, tiesiog USB laikmenoje.

## Contents

*   [1 Diegimas](#Diegimas)
    *   [1.1 Diegimo patobulinimai](#Diegimo_patobulinimai)
*   [2 Konfigūracija](#Konfig.C5.ABracija)
    *   [2.1 GRUB legacy](#GRUB_legacy)
    *   [2.2 GRUB](#GRUB)
    *   [2.3 Syslinux](#Syslinux)
*   [3 Patarimai](#Patarimai)
    *   [3.1 Jūsų USB dieginio naudojimas keliose mašinose](#J.C5.ABs.C5.B3_USB_dieginio_naudojimas_keliose_ma.C5.A1inose)
        *   [3.1.1 Įvesties tvarkyklės](#.C4.AEvesties_tvarkykl.C4.97s)
        *   [3.1.2 Vaizdo tvarkyklės](#Vaizdo_tvarkykl.C4.97s)
        *   [3.1.3 Nuolatinis blokinio įrenginio pavadinimas](#Nuolatinis_blokinio_.C4.AFrenginio_pavadinimas)
        *   [3.1.4 Branduolio parametrai](#Branduolio_parametrai)
        *   [3.1.5 Įkrovimas iš USB 3 laikmenos](#.C4.AEkrovimas_i.C5.A1_USB_3_laikmenos)
    *   [3.2 Suderinamumas](#Suderinamumas)
    *   [3.3 Disko prieigos minimizacija](#Disko_prieigos_minimizacija)
*   [4 Taip pat žiūrėkite](#Taip_pat_.C5.BEi.C5.ABr.C4.97kite)

## Diegimas

**Note:** Rekomenduojama bent 2 GiB saugojimo vietos. Tilps kuklus paketų rinkinys, ir liks truputis saugojimo vietos.

Yra keletas būdų Arch diegimui į USB laikmėną, priklauso nuo to kokia operacinė sistema yra prieinama:

*   Jei turite prieinamą kitą Linux kompiuterį (nebūtinai su Arch), galite sekti [diegimas iš egzistuojančios Linux](/index.php/Install_from_existing_Linux "Install from existing Linux") instrukcijas.
*   Diegimui į USB laikmeną gali būti naudojamas Arch Linux CD/USB, užkraunant CD/USB ir sekant [diegimo vedlį](/index.php/Installation_guide_(Lietuvi%C5%A1kai) "Installation guide (Lietuviškai)"). Jei užkraunama iš Live USB, diegimas turėtų būti vykdomas į atskirą USB laikmeną.
*   Jei naudojate Windows ar OS X, parsisiųskite VirtualBox, įdiekite VirtualBox Extensions, pridėkite USB laikmeną prie virtualiosios mašinos su Arch (pavyzdžiui paleistos iš iso), naudodamiesi [diegimo vedliu](/index.php/Installation_guide_(Lietuvi%C5%A1kai) "Installation guide (Lietuviškai)") nukreipkite diegimą į USB laikmeną.

### Diegimo patobulinimai

*   Prieš sukurdami pradinį RAM diską `# mkinitcpio -p linux`, prie `/etc/mkinitcpio.conf` pridėkite `block` kablį pri kablių masyvo iškart po udev. Tai svarbu tinkamam moulių užkrovimui ankstyvoje naudotojų ervėje (userspace).
*   Prieš pasirenkant failų sistemą labi rekomenduojama perskaityti vikipedijos straipsnį apie [disko skaitymą/rašymą](/index.php/Improving_performance#Reduce_disk_reads.2Fwrites "Improving performance"). Apibendrinant, [ext4 be žurnalo](http://fenidik.blogspot.com/2010/03/ext4-disable-journal.html) turėtų būti gerai, ją galima sukurti su `# mkfs.ext4 -O "^has_journal" /dev/sdXX`. Akivaizus trūkumas naudojant sistemą su išjungtu žurnalu, tai duomenų praradimas dėl netinkamo atjungimo. Atkreipkite dėmesį, kad USB turį ribotą kiekį įrašymų ir žurnalizavimo sistemą panaudos dalį jų atsinaujinimams . Dėl tos pačiso priežasties, būtų geriausia pamiršti ir swap particiją. Pažymėtina, kad šie dalykai nėra taikomi išoriniam kietąjam diskui.
*   Jeigu ir toliau norite naudoti UFD prietaisą keliaplatformį keičiamą diską, tai galima pasiekti sukuriant particiją su atitinkama failų sistemą (dažniausiai NTFS ar exFAT). Atkreipkite dėmesį, kad duomenų particija tikriausiai turėtų būti prietaise pirmoji, kadangi Windows daro prielaidą, kad laikmenoje gali būti tik viena particija, kitu atveju Windows mielai prijungs EFI sistemos particiją. Nepamirškite įdiegti [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) ir [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). Kai kurie internete esantys įrankai gali leisti perkeisti išimamos laikmenos dalį jūsų UFD įrenginyje. Tai glai apgauti operacines sistemas ir jos jūsų UFD įrenginį laikys išoriniu disku bei leis naudoti kokią tik norite skirsnių sistemą.

**Warning:** Tai veikia ne visuose UFD įrenginiuose ir bandymas naudoti programinę įrangą nepalaikomą jūsų įrenginio gali jį sugadinti. Išimamosios laikmenos dalies perkeitinas **nerekomenduojamas**.

## Konfigūracija

*   Įsitikinkite, kad `/etc/fstab` reikalingą particijos informaciją skirtą `/`, ir visoms kitoms particijoms esančioms USB rakte. Jeigu usb raktas skirtas užkrovimui keliose mašinose, didelė tikimybė, kad prieinamų prietaisų ir kietųjų diskų kiekis gali skirtis. Todėl rekomenduojama naudoti UUID arba etiketes.

Gauti tinkamus jūsų particijoms UUID naudokite **blkid**.

**Note:**

*   Kai GRUB diegiamas į USB raktą, raktas visada bus `hd0,0`.
*   Panašu kad esamos GRUB versijos pagal numatytuosius nustatymus naudos uuid. Sekantys nurodymai skirti GRUB legacy.

### GRUB legacy

`menu.lst`, GRUB legacy konfigūracijos failas, turėtų būti redaguotas, kad (bendrai) atitinktų sekančius nurodymus.

Su statišku `/dev/sda*X*`:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sda1 ro
initrd /boot/initramfs-linux.img

```

Nauojant etiketes jūsų menu.lst turėtų atrodyti taip:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/**Arch** ro
initrd /boot/initramfs-linux.img

```

O nauojant UUID, šitaip:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/3a9f8929-627b-4667-9db4-388c4eaaf9fa ro
initrd /boot/initramfs-linux.img

```

### GRUB

GPT su UEFI dieginiams, įsitikinkite, kad sekate [GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB") ir įtraukėte `--removable` parinktį, kaip nurodyta žemiau, nes kitaip galite sugadinti GRUB dieginius:

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub **--removable** --recheck

```

### Syslinux

Su statišku `/dev/sda*X*`:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sdax ro
        INITRD ../initramfs-linux.img

```

Naudojant jūsų UUID:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=UUID=3a9f8929-627b-4667-9db4-388c4eaaf9fa ro
        INITRD ../initramfs-linux.img

```

## Patarimai

### Jūsų USB dieginio naudojimas keliose mašinose

#### Įvesties tvarkyklės

Laptopo naudojimui (ar naudojimui su lieiamu ekranu) reikės [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) paketo kad veiktų touchpad'as/liečiamas ekranas.

Dėl tiklsuas sudderinimo ir trikčių taisymo, skaitykite [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") straipsnį.

#### Vaizdo tvarkyklės

**Note:** Šiam diegimo tipui, patentuotų vaizdo tvarkyklių naudojimas **nėra** rekomenduojamas.

Daugumos GPU palaikymui, įdiekite [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa), [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu), ir [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau).

#### Nuolatinis blokinio įrenginio pavadinimas

Rekomenduojama naudoti [UUID](/index.php/UUID "UUID") tiek [fstab](/index.php/Fstab "Fstab"), tiek įkrovėjo konfigūracijose. Dėl daugiau detalių žiūrėti [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

Arba galite sukurti udev taisyklė, ka sukurtumėte pasirinktinę simbolinę nuorodą savo usb raktui. Tuomet galėsi naudoti šią nuorodą fstab ir įkroviklio konfigūracijose. Dėl daugiau detalių žiūrėti [udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev").

#### Branduolio parametrai

Gali būti dėl įvairų priežasčių, kaip tuščias ekranas, arba "nėra signalo" klaida, naudojant kai kurias Intel vaizo kortas ir t.t. norėsite išjungti KMS. Tai padarysite pridėdami `nomodeset` kaip branduolio parametrą. Dėl daugiau informacijos žiūrėti [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

**Warning:** Kai kurios[Xorg](/index.php/Xorg "Xorg") tvarkyklės su išjungtu KMS neveiks. Dėl daugiau detalių žiūrėkite vikipedijos straipsnį skirtą atitinkamai tvarkyklei . Nouveau ypač reikia KMS teisingam rezoliucijos nustatymui. Jei pridėsite `nomodeset` kaip prevencinę priemonę, mašinose su Nvidia vaizdo kortomis rezoliuciją turėsite nustatyti rankiniu būdu. Dėl daugiau informacijos žiūrėti [Xrandr](/index.php/Xrandr "Xrandr").

#### Įkrovimas iš USB 3 laikmenos

Žiūrėti [[1]](http://www.wyae.de/docs/boot-usb3/).

### Suderinamumas

Didžiausiam suderinamumui turėtų būti naudojamas atsarginis vaizdas.

### Disko prieigos minimizacija

*   Norėsite sukonfigūruoti [journald](/index.php/Systemd#Journal "Systemd") kad žurnalai būti talpinami RAM, pvz.: sukuriant konfigūracinį failą:

 `/etc/systemd/journald.conf.d/usbstick.conf` 
```
[Journal]
Storage=volatile
RuntimeMaxUse=30M
```

*   Norint išjunti `fsync` irsusijusius sistemos šaukinius interneto naršyklėse, bei kitose programose nerašančiose svarbių deuomenų, naudokite *eatmydata* komanddą iš [libeatmydata](https://aur.archlinux.org/packages/libeatmydata/) tokių šaukinių išvengimui:

```
$ eatmydata firefox

```

## Taip pat žiūrėkite

*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives")