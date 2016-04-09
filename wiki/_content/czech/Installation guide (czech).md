Tato stránka vás provede procesem instalace [Arch Linuxu](/index.php/Arch_Linux_(%C4%8Cesky) "Arch Linux (Česky)") pomocí [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Před instalací si prosím pročtěte [často kladené otázky](/index.php/FAQ_(%C4%8Cesky) "FAQ (Česky)"). Pokud hledáte podrobnější a více vysvětlující příručku, navštivte [příručku začátečníka](/index.php/Beginners%27_guide_(%C4%8Cesky) "Beginners' guide (Česky)").

Komunitou spravovaná [ArchWiki](/index.php/Main_page_(%C4%8Cesky) "Main page (Česky)") je výborným zdrojem dokumentace, řešení problémů hledejte nejdříve zde. Pokud nemůžete nalézt řešení problému, jsou vám k dispozici [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanál ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) a [fórum](https://bbs.archlinux.org/). Určitě také pročtěte manuálové stránky jakéhokoli příkazu, který vám není povědomý; manuálové stránky se obvykle prohlíží příkazem `man *command*`.

## Contents

*   [1 Stažení](#Sta.C5.BEen.C3.AD)
*   [2 Instalace](#Instalace)
    *   [2.1 Rozložení klávesnice](#Rozlo.C5.BEen.C3.AD_kl.C3.A1vesnice)
    *   [2.2 Rozdělte disk](#Rozd.C4.9Blte_disk)
    *   [2.3 Naformátujte oddíly](#Naform.C3.A1tujte_odd.C3.ADly)
    *   [2.4 Připojte oddíly](#P.C5.99ipojte_odd.C3.ADly)
    *   [2.5 Připojte se k Internetu](#P.C5.99ipojte_se_k_Internetu)
        *   [2.5.1 Bezdrátové připojení](#Bezdr.C3.A1tov.C3.A9_p.C5.99ipojen.C3.AD)
    *   [2.6 Nainstalujte základní systém](#Nainstalujte_z.C3.A1kladn.C3.AD_syst.C3.A9m)
    *   [2.7 Nainstalujte bootloader](#Nainstalujte_bootloader)
        *   [2.7.1 GRUB](#GRUB)
        *   [2.7.2 Syslinux](#Syslinux)
    *   [2.8 Nakonfigurujte systém](#Nakonfigurujte_syst.C3.A9m)
    *   [2.9 Odpojte oddíly a rebootujte](#Odpojte_odd.C3.ADly_a_rebootujte)
*   [3 Po instalaci](#Po_instalaci)
    *   [3.1 Správa uživatelů](#Spr.C3.A1va_u.C5.BEivatel.C5.AF)
    *   [3.2 Správa balíčků](#Spr.C3.A1va_bal.C3.AD.C4.8Dk.C5.AF)
    *   [3.3 Správa služeb](#Spr.C3.A1va_slu.C5.BEeb)
    *   [3.4 Zvuk](#Zvuk)
    *   [3.5 Ovladač grafické karty](#Ovlada.C4.8D_grafick.C3.A9_karty)
    *   [3.6 Display server](#Display_server)
    *   [3.7 Fonty](#Fonty)
*   [4 Závěr](#Z.C3.A1v.C4.9Br)

## Stažení

ISO Arch Linuxu stáhněte z [Arch Linux download page](https://www.archlinux.org/download/).

*   Poskytujeme jediný obraz, který lze nabootovat do živého i686 nebo x86_64 systému určeného pro instalaci Arch Linuxu přes síť. Média obsahující repozitář [core] již nejsou a nebudou poskytovány.
*   Instalační obrazy jsou podepsány a je silně doporučeno před použitím ověřit jejich signaturu. V Arch Linuxu toto můžete provést pomocí `pacman-key -v <iso-file>.sig` 
*   Obraz lze vypálit na CD, připojit jako ISO soubor nebo [zapsat na USB flashdisk](/index.php/USB_Installation_Media "USB Installation Media"). Obraz je určen pouze pro nové instalace; existující Arch Linux systém lze vždy aktualizovat příkazem `pacman -Syu`.

## Instalace

### Rozložení klávesnice

Pro mnohé země a typy klávesnic (včetně té české) jsou již příslušné mapy klávesnic k dispozici a příkaz `loadkeys cz-qwertz` by mohl udělat to co chcete. Další mapy klávesnic můžete nalézt v `/usr/share/kbd/keymaps/` (při použití loadkeys můžete cestu k souboru a příponu vynechat).

### Rozdělte disk

Pro detaily vizte [partitioning](/index.php/Partitioning "Partitioning").

Nezapomeňte vytvořit jakákoliv vrstvená bloková zařízení typu [LVM](/index.php/LVM "LVM"), [LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS") nebo [RAID](/index.php/RAID "RAID").

### Naformátujte oddíly

Pro detaily vizte [zde](/index.php/File_systems#Step_2:_create_the_new_file_system "File systems").

Pokud používáte (U)EFI, nejspíše budete potřebovat oddíl navíc pro hostování Systémového oddílu UEFI. Přečtěte si [tento článek](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface").

### Připojte oddíly

Nyní musíme připojit kořenový oddíl na `/mnt`. Měli byste též vytvořit podadresáře pro jakékoliv další oddíly (`/mnt/boot`, `/mnt/home`, ...) včetně [swapu](/index.php/Swap "Swap") a připojit je, pokud chcete, aby je `genfstab` našel.

### Připojte se k Internetu

Služba DHCP je již povolena pro všehna dostupná síťová rozhraní. Pokud potřebujete nastavit statickou IP adresu nebo použít nějaký nástroj pro správu připojení (např. [Netctl](/index.php/Netctl "Netctl")), měli byste tuto službu nejdříve zastavit: `systemctl stop dhcpcd.service`. Pro více informací navštivte [configuring network](/index.php/Configuring_network "Configuring network").

#### Bezdrátové připojení

Pro nastavení své bezdrátové sítě spusťte `wifi-menu`. Pro podrobnosti vizte [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") a [Netctl](/index.php/Netctl "Netctl").

### Nainstalujte základní systém

Před instalací byste mohli chtít provést změny v `/etc/pacman.d/mirrorlist`, aby byl vámi upřednostňovaný mirror první v seznamu. Tato kopie mirrorlistu bude také nainstalována na váš nový systém přes `pacstrap`, takže má cenu udělat to správně už teď.

Použitím skriptu [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) nainstalujeme základní systém.

```
# pacstrap /mnt base

```

Další balíčky můžete nainstalovat připsáním jejich názvů k výše uvedenému příkazu (oddělujte je pomocí mezer), včetně bootloaderu, chcete-li. Doporučuji společně s balíkem `base` nainstalovat i balík `base-devel`.

### Nainstalujte bootloader

#### [GRUB](/index.php/GRUB2 "GRUB2")

*   Pro BIOS:

```
# arch-chroot /mnt pacman -S grub-bios

```

*   Pro EFI (v některých případech budete namísto uvedeného potřebovat `grub-efi-i386`:

```
# arch-chroot /mnt pacman -S grub-efi-x86_64

```

#### [Syslinux](/index.php/Syslinux "Syslinux")

```
# arch-chroot /mnt pacman -S syslinux

```

### Nakonfigurujte systém

Následujícím příkazem vygenerujete [fstab](/index.php/Fstab "Fstab") (pokud upřednostňujete použití UUID nebo labelů, přidejte přepínač `-U`, respektive `-L`):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

Dále provedeme [chroot](/index.php/Chroot "Chroot") do našeho nově nainstalovaného systému:

```
# arch-chroot /mnt

```

*   Zapište svůj hostname do `/etc/hostname`.
*   Proveďte symlink `/etc/localtime` na `/usr/share/zoneinfo/Zóna/Podzóna`. Nahraďte `Zóna` a `Podzóna` podle svého gusta. Například:

```
# ln -s /usr/share/zoneinfo/Europe/Prague /etc/localtime

```

*   Odkomentujte vybrané locale v `/etc/locale.gen` a vygenerujte ho s `locale-gen`.
*   Nastavte [locale](/index.php/Locale#Setting_system-wide_locale "Locale") v `/etc/locale.conf`.
*   Nastavte [konzolové rozložení klávesnice](/index.php/KEYMAP "KEYMAP") and [konzolový font](/index.php/Fonts#Console_fonts "Fonts") v `/etc/vconsole.conf`
*   Nakonfigurujte `/etc/mkinitcpio.conf` podle potřeby (vizte [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")) a vytvořte startovací RAM disk s:

```
# mkinitcpio -p linux

```

*   Nakonfigurujte bootloader. Pro GRUB vizte [instalaci a konfiguraci GRUBu](/index.php/GRUB#Installation "GRUB"); pro Syslinux vizte [konfiguraci Syslinuxu](/index.php/Syslinux#Configuration "Syslinux").
*   Nastavte heslo uživatele root příkazem `passwd`.
*   Pro nainstalovaný systém znovu nastavte síťové připojení. Vizte [Network configuration](/index.php/Network_configuration "Network configuration") a [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Odpojte oddíly a rebootujte

Pokud jste stále v prostředí chrootu, napište `exit` nebo stiskněte `Ctrl+D` pro jeho opuštění. Dříve jsme připojili potřebné oddíly pod `/mnt`. V tomto kroku je odpojíme:

```
# umount /mnt/{boot,home,}

```

Nakonec restartujte počítač a přihlašte se do nového systému do účtu uživatele root.

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

| Výrobce | Typ | Ovladač | [Multilib](/index.php/Multilib "Multilib") balíček
(pro 32-bit aplikace na Arch x86_64) | Dokumentace |
| **AMD/ATI** | Open source | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-ati-dri](https://www.archlinux.org/packages/?name=lib32-ati-dri) | [ATI](/index.php/ATI "ATI") |
| Proprietární | [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| **Intel** | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| **Nvidia** | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri) | [Nouveau](/index.php/Nouveau "Nouveau") |
| [xf86-video-nv](https://www.archlinux.org/packages/?name=xf86-video-nv) | – | (zastaralý ovladač) |
| Proprietární | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) |

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