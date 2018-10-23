Tato stránka vás provede procesem instalace [Arch Linuxu](/index.php/Arch_Linux_(%C4%8Cesky) "Arch Linux (Česky)") pomocí [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Před instalací si prosím pročtěte [často kladené otázky](/index.php/FAQ_(%C4%8Cesky) "FAQ (Česky)"). Pokud hledáte podrobnější a více vysvětlující příručku, navštivte [příručku začátečníka](/index.php/Beginners%27_guide_(%C4%8Cesky) "Beginners' guide (Česky)").

Komunitou spravovaná [ArchWiki](/index.php/Main_page_(%C4%8Cesky) "Main page (Česky)") je výborným zdrojem dokumentace, řešení problémů hledejte nejdříve zde. Pokud nemůžete nalézt řešení problému, jsou vám k dispozici [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanál ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) a [fórum](https://bbs.archlinux.org/). Určitě také pročtěte manuálové stránky jakéhokoli příkazu, který vám není povědomý; manuálové stránky se obvykle prohlíží příkazem `man *command*`.

## Contents

*   [1 Před instalací](#P.C5.99ed_instalac.C3.AD)
    *   [1.1 UEFI](#UEFI)
    *   [1.2 Rozložení klávesnice](#Rozlo.C5.BEen.C3.AD_kl.C3.A1vesnice)
    *   [1.3 Připojte se k Internetu](#P.C5.99ipojte_se_k_Internetu)
        *   [1.3.1 Bezdrátové připojení](#Bezdr.C3.A1tov.C3.A9_p.C5.99ipojen.C3.AD)
    *   [1.4 Nastavte systémový čas](#Nastavte_syst.C3.A9mov.C3.BD_.C4.8Das)
    *   [1.5 Rozdělte disk](#Rozd.C4.9Blte_disk)
    *   [1.6 Naformátujte oddíly](#Naform.C3.A1tujte_odd.C3.ADly)
    *   [1.7 Připojte oddíly](#P.C5.99ipojte_odd.C3.ADly)
*   [2 Instalace](#Instalace)
    *   [2.1 Vyberte mirrory](#Vyberte_mirrory)
    *   [2.2 Nainstalujte základní systém](#Nainstalujte_z.C3.A1kladn.C3.AD_syst.C3.A9m)
*   [3 Nakonfigurujte systém](#Nakonfigurujte_syst.C3.A9m)
    *   [3.1 fstab](#fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Časové pásmo](#.C4.8Casov.C3.A9_p.C3.A1smo)
    *   [3.4 Lokalizace](#Lokalizace)
    *   [3.5 Hostname](#Hostname)
    *   [3.6 Nastavení síte](#Nastaven.C3.AD_s.C3.ADte)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root heslo](#Root_heslo)
    *   [3.9 Boot loader](#Boot_loader)
    *   [3.10 Restart](#Restart)
*   [4 Po instalaci](#Po_instalaci)
    *   [4.1 Správa uživatelů](#Spr.C3.A1va_u.C5.BEivatel.C5.AF)
    *   [4.2 Správa balíčků](#Spr.C3.A1va_bal.C3.AD.C4.8Dk.C5.AF)
    *   [4.3 Správa služeb](#Spr.C3.A1va_slu.C5.BEeb)
    *   [4.4 Zvuk](#Zvuk)
    *   [4.5 Ovladač grafické karty](#Ovlada.C4.8D_grafick.C3.A9_karty)
    *   [4.6 Display server](#Display_server)
    *   [4.7 Fonty](#Fonty)
*   [5 Závěr](#Z.C3.A1v.C4.9Br)

## Před instalací

Arch Linux by měl být spustitelný na libovolném počítači kompatibilním s [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") s min. 512 MB RAM. Základní instalace se všemi balíčky ze skupiny [base](https://www.archlinux.org/groups/x86_64/base/) by měla zabírat méně než 800 MB místa na disku.

ISO Arch Linuxu stáhněte z [Arch Linux download page](https://www.archlinux.org/download/).

*   Poskytujeme jediný obraz, který lze nabootovat do živého i686 nebo x86_64 systému určeného pro instalaci Arch Linuxu přes síť. Média obsahující repozitář [core] již nejsou a nebudou poskytovány.
*   Instalační obrazy jsou podepsány a je silně doporučeno před použitím ověřit jejich signaturu. V Arch Linuxu toto můžete provést pomocí `$ pacman-key -v <iso-file>.sig` 
*   Obraz lze vypálit na CD, připojit jako ISO soubor nebo [zapsat na USB flashdisk](/index.php/USB_Installation_Media "USB Installation Media"). Obraz je určen pouze pro nové instalace; existující Arch Linux systém lze vždy aktualizovat příkazem `pacman -Syu`.

Po zavedení systému budete přihlášeni jako root uživatel se [Zsh](/index.php/Zsh "Zsh") shellem.

Pro úpravu nebo vytvoření konfiguračních souborů je možné použít nástroje [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") nebo [vim](/index.php/Vim#Usage "Vim")

### UEFI

Pokud máte základní desku s [UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") firmvérem a nastaven UEFI režim, ověřte, zda je systém zavedený v UEFI režimu zkontrolováním [efivars](/index.php/Efivars "Efivars"):

```
# ls /sys/firmware/efi/efivars

```

### Rozložení klávesnice

Pro mnohé země a typy klávesnic (včetně té české) jsou již příslušné mapy klávesnic k dispozici a příkaz `loadkeys cz-qwertz` by mohl udělat to co chcete. Další mapy klávesnic můžete nalézt v `/usr/share/kbd/keymaps/` (při použití loadkeys můžete cestu k souboru a příponu vynechat).

### Připojte se k Internetu

Služba DHCP je již povolena pro všechna dostupná síťová rozhraní. Ověřte funkčnost připojení, např. příkazem:

```
# ping archlinux.org 

```

Pokud potřebujete nastavit statickou IP adresu nebo použít nějaký nástroj pro správu připojení (např. [Netctl](/index.php/Netctl "Netctl")), měli byste tuto službu nejdříve zastavit (nahraďte `enp0s25` správným síťovým rozhraním):

```
# systemctl stop dhcpcd@*enp0s25*.service

```

Pro více informací navštivte [Network configuration](/index.php/Network_configuration "Network configuration").

#### Bezdrátové připojení

Pro výpis dostupných sítí a vytvoření připojení na zvoleném síťovém rozhraní použijte příkaz (nahraďte `wlp2s0` síťovým rozhraním bezdrátového adaptéru):

```
# wifi-menu -o *wlp2s0*

```

Výsledný konfigurační soubor bude uložen v `/etc/netctl`. Pro podrobnosti vizte [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Nastavte systémový čas

Použijte [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") pro nastavení přesného času:

```
# timedatectl set-ntp true

```

Chcete-li zkontrolovat stav služby, použijte `timedatectl status`.

### Rozdělte disk

Pro úpravu a vytvoření [partition table](/index.php/Partition_table "Partition table") (tabulka oddílů) použijte [fdisk](/index.php/Fdisk "Fdisk"), [cfdisk](/index.php/Cfdisk "Cfdisk") nebo [parted](/index.php/Parted "Parted") pro [MBR](/index.php/MBR "MBR") a [GPT](/index.php/GPT "GPT"), nebo [gdisk](/index.php/Gdisk "Gdisk") (pouze GPT).

Alespoň jeden oddíl musí být dostupný pro kořenový adresář `/`. Pokud používáte UEFI, budete potřebovat další oddíl pro hostování [EFI system partition](/index.php/EFI_system_partition "EFI system partition"). Také mohou být zapotřebí další oddíly, např. [GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") na BIOS/GPT konfiguraci.

Nezapomeňte vytvořit jakákoliv vrstvená bloková zařízení typu [LVM](/index.php/LVM "LVM"), [LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS") nebo [RAID](/index.php/RAID "RAID"), pokud je požadujete.

Pro detaily vizte [Partitioning](/index.php/Partitioning "Partitioning").

### Naformátujte oddíly

Naformátovaní oddílu jako [ext4](/index.php/Ext4 "Ext4"):

```
# mkfs.ext4 /dev/sd*xY*

```

Naformátovaní [swap](/index.php/Swap "Swap") oddílu:

```
# mkswap /dev/sd*xY*

```

Naformátovaní oddílu jako FAT32 (EFI System Partition):

```
# mkfs.fat -F32 /dev/sd*xY*

```

Pro detaily vizte [zde](/index.php/File_systems#Create_a_file_system "File systems") a [zde](/index.php/Swap "Swap").

### Připojte oddíly

Nyní připojte kořenový oddíl na `/mnt`. Poté vytvořte podadresáře pro jakékoliv další oddíly a připojte je (`/mnt/boot`, `/mnt/home`, ...) a aktivujte [swap](/index.php/Swap "Swap") oddíl přes `swapon`, pokud chcete, aby je `genfstab` našel.

## Instalace

### Vyberte mirrory

Před instalací byste mohli chtít provést změny v `/etc/pacman.d/mirrorlist`, aby byl vámi upřednostňovaný mirror první v seznamu. Tato kopie mirrorlistu bude také nainstalována na váš nový systém přes `pacstrap`, takže má cenu udělat to správně už teď.

### Nainstalujte základní systém

Použitím skriptu [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) nainstalujete základní systém.

```
# pacstrap /mnt base

```

Další balíčky můžete nainstalovat připsáním jejich názvů k výše uvedenému příkazu (oddělujte je pomocí mezer), včetně bootloaderu, chcete-li. Doporučuje se společně s balíkem `base` nainstalovat i balík `base-devel`.

## Nakonfigurujte systém

### fstab

Vygenerujte [fstab](/index.php/Fstab "Fstab") soubor (pokud upřednostňujete použití UUID nebo labelů, použijte přepínač `-U`, respektive `-L`):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

Poté skontrolujte výsledek v `/mnt/etc/fstab` a pokud jsou v něm chyby, opravte je.

### Chroot

Proveďte [chroot](/index.php/Chroot "Chroot") do nově nainstalovaného systému:

```
# arch-chroot /mnt

```

### Časové pásmo

Nastavte [časové pásmo](/index.php/Time_zone "Time zone") vytvořením symlinku `/etc/localtime` na `/usr/share/zoneinfo/Zóna/Podzóna`. Nahraďte `Zóna` a `Podzóna` podle svého gusta. Například:

```
# ln -sf /usr/share/zoneinfo/Europe/Prague /etc/localtime

```

Spusťte `hwclock` pro vygenerovaní `/etc/adjtime`. Pokud je zvolen UTC standard, ostatní operační systémy (Windows) musí být nastaveny stejně. Pro více informací vizte [System time](/index.php/System_time "System time").

```
# hwclock --systohc --*utc*

```

### Lokalizace

Odkomentujte vybrané locale v `/etc/locale.gen` a vygenerujte je:

```
# locale-gen

```

Zapište předvolenou lokalizaci ve formátu `LANG=*your_locale*` do `/etc/locale.conf`. Například:

```
LANG=cs_CZ.UTF-8 

```

Pokud chcete, nastavte [konzolové rozložení klávesnice](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") a [konzolový font](/index.php/Fonts#Console_fonts "Fonts") v `/etc/vconsole.conf`

### Hostname

Zapište [hostname](/index.php/Hostname "Hostname") do `/etc/hostname` a `/etc/hosts`. Například:

```
# echo mojezarizeni > /etc/hostname
# echo 127.0.0.1   mojezarizeni.localdomain  mojezarizeni >> /etc/hosts

```

### Nastavení síte

Pro nainstalovaný systém znovu nastavte síťové připojení. Pokud chcete zapnout DHCP na všech kabelových síťových rozhraních (jako při startu systému), použijte příkaz:

```
# systemctl enable dhcpcd.service

```

Pro podrobnosti vizte [Network configuration](/index.php/Network_configuration "Network configuration") a [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Initramfs

Pokud jste udělali změny v [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"), vytvořte nový startovací RAM disk:

```
# mkinitcpio -p linux

```

### Root heslo

Nastavte heslo pro užívatele root:

```
# passwd

```

### Boot loader

Nainstalujte a nakonfigurujte [boot loader](/index.php/Category:Boot_loaders "Category:Boot loaders") (zavaděč). Na výběr jsou např. [GRUB (Česky)](/index.php/GRUB_(%C4%8Cesky) "GRUB (Česky)") (BIOS/UEFI), [rEFInd](/index.php/REFInd "REFInd"), [systemd-boot](/index.php/Systemd-boot "Systemd-boot") (pouze UEFI) a [syslinux](/index.php/Syslinux "Syslinux") (pouze BIOS).

Pokud máte procesor Intel, nainstalujte i balíček [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) a [povolte aktualizace mikrokódu.](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

### Restart

Pokud jste stále v prostředí chrootu, napište `exit` nebo stiskněte `Ctrl+D` pro jeho opuštění.

Dříve jsme připojili potřebné oddíly pod `/mnt`. V tomto kroku je odpojíme:

```
# umount -R /mnt

```

Nakonec restartujte počítač příkazem `reboot` a přihlašte se do nového systému do účtu uživatele root.

## Po instalaci

### Správa uživatelů

Vytvořte uživatelské účty podle vaší potřeby, jak je popsáno v [User management](/index.php/Users_and_groups#User_management "Users and groups"). Účet root není dobré používat pro běžné použití, nebo ho zpřístupňovat přes [SSH](/index.php/SSH "SSH"). Účet root by měl být používán pouze pro účely správy systému.

### Správa balíčků

Vizte [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)") a [Často kladené otázky](/index.php/FAQ_(%C4%8Cesky)#Spr.C3.A1va_bal.C3.AD.C4.8Dk.C5.AF "FAQ (Česky)") pro informace ohledně instalace, aktualizace a správy balíčků.

### Správa služeb

Arch Linux používá init systém [systemd](/index.php/Systemd "Systemd"), který je také správcem systémových služeb pro Linux. Pro správu systému Arch Linux je určitě dobré naučit se alespoň jeho základy. systemd se ovládá pomocí příkazu `systemctl`. Přečtěte si prosím [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd") pro více informací.

### Zvuk

[ALSA](/index.php/ALSA_(%C4%8Cesky) "ALSA (Česky)") obvykle funguje bez jakékoli konfigurace. Jen je potřeba ji zapnout (*unmute*). Nainstalujte balíček [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (který obsahuje `alsamixer`) a následujte [tyto](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture") instrukce.

ALSA je obsažena v kernelu a je to doporučený systém. Pokud nefunguje, můžete zkusit [OSS](/index.php/OSS "OSS"). Pokud máte na zvuk zvláštní požadavky, podívejte se na [Sound system](/index.php/Sound_system "Sound system") pro přehled různých článků.

### Ovladač grafické karty

Linuxové jádro obsahuje open-source video ovladače a podporuje hardwarově akcelerované framebuffery. Pro OpenGL a 2D akceleraci v X11 je však nutná podpora ze strany uživatelských aplikací.

Pokud nevíte, který chipset je na vašem stroji dostupný, spusťte:

```
$ lspci | grep VGA

```

Pro kompletní seznam open-source video ovladačů prohledejte databázi balíčků:

```
$ pacman -Ss xf86-video | less

```

Ovladač `vesa` je obecným ovladačem nastavujícím rozlišení, který funguje se skoro každým GPU, ale neposkytuje 2D ani 3D akceleraci. Pokud lepší ovladač není k dispozici nebo jeho načtení selže, Xorg použije právě vesa. Pro instalaci spusťte:

```
# pacman -S xf86-video-vesa

```

Aby fungovala akcelerace a často aby se zpřístupnila všechna rozlišení, která umí GPU nastavit, je nutné použít patřičný ovladač:

| Brand | Type | Driver | OpenGL | OpenGL ([Multilib](/index.php/Multilib "Multilib")) | Documentation |
| AMD / ATI | Open source | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [AMDGPU](/index.php/AMDGPU "AMDGPU") |
| [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [ATI](/index.php/ATI "ATI") |
| Proprietary | [catalyst](https://aur.archlinux.org/packages/catalyst/) | [catalyst-libgl](https://aur.archlinux.org/packages/catalyst-libgl/) | [lib32-catalyst-libgl](https://aur.archlinux.org/packages/lib32-catalyst-libgl/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| Intel | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| NVIDIA | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Nouveau](/index.php/Nouveau "Nouveau") |
| Proprietary | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) | [nvidia-340xx-utils](https://www.archlinux.org/packages/?name=nvidia-340xx-utils) | [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) |

### Display server

X Window System, běžně označovaný jako X11 nebo X, je síťový a display protokol poskytující windowing systém pro bitmapová zobrazovací zařízení. Je to v podstatě standard pro implementaci grafických prostředí. Pro podrobnosti vizte [Xorg](/index.php/Xorg_(%C4%8Cesky) "Xorg (Česky)").

[Wayland](/index.php/Wayland "Wayland") je nový display server protokol, je dostupná referenční implementace Weston. V této rané fázi vývoje je zde ze strany aplikací velmi málo podpory.

### Fonty

Možná budete chtít nainstalovat TrueType fonty, v základu jsou dostupné pouze neškálovatelné bitmapové fonty. DejaVu je balík obsahující několik velmi kvalitních všeobecných fontů s dobrou podporou [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode"):

```
# pacman -S ttf-dejavu

```

Pro instalační instrukce a návrhy fontů vizte [Fonts](/index.php/Fonts "Fonts"), pro informace o konfiguraci vykreslování fontů vizte [Font configuration](/index.php/Font_configuration "Font configuration").

## Závěr

Navštivte [seznam aplikací](/index.php/List_of_applications_(%C4%8Cesky) "List of applications (Česky)"), které by vás mohly zajímat.

Navštivte [poinstalačního průvodce](/index.php/General_recommendations_(%C4%8Cesky) "General recommendations (Česky)") obsahující informace o nastavení touchpadu, vykreslování fontů apod.