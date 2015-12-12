# Beginners' guide (Česky)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Beginners' guide (Česky)#](https://wiki.archlinux.org/index.php/Talk:Beginners%27_guide_(%C4%8Cesky)))

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**This article or section needs to be [translated](/index.php/ArchWiki:Contributing#Translating "ArchWiki:Contributing").**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Beginners' guide (Česky)#](https://wiki.archlinux.org/index.php/Talk:Beginners%27_guide_(%C4%8Cesky)))

[![Tango-preferences-desktop-locale-modified.png](/images/2/26/Tango-preferences-desktop-locale-modified.png)](/index.php/File:Tango-preferences-desktop-locale-modified.png)

[![Tango-preferences-desktop-locale-modified.png](/images/2/26/Tango-preferences-desktop-locale-modified.png)](/index.php/File:Tango-preferences-desktop-locale-modified.png)

**The [translation](/index.php/ArchWiki:Contributing#Translating "ArchWiki:Contributing") of this article or section does not reflect the original text.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Beginners' guide (Česky)#](https://wiki.archlinux.org/index.php/Talk:Beginners%27_guide_(%C4%8Cesky)))

Související články

*   [Installation Guide (Česky)](/index.php/Installation_Guide_(%C4%8Cesky) "Installation Guide (Česky)")

Toto je detailní příručka popisující instalaci, a konfiguraci plnohodnotného systému Arch Linux. Po kapitolu 3.2.4 je příručka aktualizována, tj. nově přeložena, s ohledem na na vypuštění instalátoru AIF z nových instalačních medií Arch Linuxu.

## Contents

*   [1 Předmluva](#P.C5.99edmluva)
    *   [1.1 Úvod](#.C3.9Avod)
    *   [1.2 License](#License)
    *   [1.3 The Arch Way](#The_Arch_Way)
    *   [1.4 O tomto průvodci](#O_tomto_pr.C5.AFvodci)
*   [2 Příprava na instalaci](#P.C5.99.C3.ADprava_na_instalaci)
    *   [2.1 Získání instalačního média](#Z.C3.ADsk.C3.A1n.C3.AD_instala.C4.8Dn.C3.ADho_m.C3.A9dia)
        *   [2.1.1 Zápis obrazu ISO na CD/DVD nebo Flash disk](#Z.C3.A1pis_obrazu_ISO_na_CD.2FDVD_nebo_Flash_disk)
        *   [2.1.2 Instalace přes síť](#Instalace_p.C5.99es_s.C3.AD.C5.A5)
        *   [2.1.3 Instalace do virtuálního stroje](#Instalace_do_virtu.C3.A1ln.C3.ADho_stroje)
    *   [2.2 Spuštění instalačního média](#Spu.C5.A1t.C4.9Bn.C3.AD_instala.C4.8Dn.C3.ADho_m.C3.A9dia)
        *   [2.2.1 Ověření zda "bootujeme" v UEFI režimu](#Ov.C4.9B.C5.99en.C3.AD_zda_.22bootujeme.22_v_UEFI_re.C5.BEimu)
        *   [2.2.2 Řešení problémů se spuštěním](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF_se_spu.C5.A1t.C4.9Bn.C3.ADm)
*   [3 Instalace](#Instalace)
    *   [3.1 Nastavení jazyka](#Nastaven.C3.AD_jazyka)
    *   [3.2 Nastavení připojení k internetu](#Nastaven.C3.AD_p.C5.99ipojen.C3.AD_k_internetu)
        *   [3.2.1 Připojení síťovým kabelem](#P.C5.99ipojen.C3.AD_s.C3.AD.C5.A5ov.C3.BDm_kabelem)
        *   [3.2.2 Bezdrátové připojení](#Bezdr.C3.A1tov.C3.A9_p.C5.99ipojen.C3.AD)
        *   [3.2.3 Připojení xDSL (PPPoE), analogovým modemem nebo ISDN](#P.C5.99ipojen.C3.AD_xDSL_.28PPPoE.29.2C_analogov.C3.BDm_modemem_nebo_ISDN)
        *   [3.2.4 Připojení za serverem proxy](#P.C5.99ipojen.C3.AD_za_serverem_proxy)
    *   [3.3 Příprava pevného disku](#P.C5.99.C3.ADprava_pevn.C3.A9ho_disku)
        *   [3.3.1 Příklad](#P.C5.99.C3.ADklad)
    *   [3.4 Mount the partitions](#Mount_the_partitions)
    *   [3.5 Výběr balíčků](#V.C3.BDb.C4.9Br_bal.C3.AD.C4.8Dk.C5.AF)
    *   [3.6 Instalace balíčků](#Instalace_bal.C3.AD.C4.8Dk.C5.AF)
    *   [3.7 Konfigurace systému](#Konfigurace_syst.C3.A9mu)
        *   [3.7.1 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [3.7.1.1 Sekce LOCALIZATION (lokalizace)](#Sekce_LOCALIZATION_.28lokalizace.29)
            *   [3.7.1.2 Sekce HARDWARE](#Sekce_HARDWARE)
            *   [3.7.1.3 Sekce NETWORKING](#Sekce_NETWORKING)
            *   [3.7.1.4 Sekce DAEMONS](#Sekce_DAEMONS)
        *   [3.7.2 /etc/fstab](#.2Fetc.2Ffstab)
        *   [3.7.3 **/etc/mkinitcpio.conf**](#.2Fetc.2Fmkinitcpio.conf)
        *   [3.7.4 /etc/modprobe.d/modprobe.conf](#.2Fetc.2Fmodprobe.d.2Fmodprobe.conf)
        *   [3.7.5 /etc/resolv.conf](#.2Fetc.2Fresolv.conf)
        *   [3.7.6 /etc/hosts](#.2Fetc.2Fhosts)
        *   [3.7.7 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [3.7.8 Pacman-Mirror](#Pacman-Mirror)
        *   [3.7.9 Root password (heslo roota)](#Root_password_.28heslo_roota.29)
        *   [3.7.10 Done (Hotovo)](#Done_.28Hotovo.29)
*   [4 Install and configure a bootloader](#Install_and_configure_a_bootloader)
    *   [4.1 For BIOS motherboards](#For_BIOS_motherboards)
        *   [4.1.1 Syslinux](#Syslinux)
        *   [4.1.2 GRUB](#GRUB)
    *   [4.2 For UEFI motherboards](#For_UEFI_motherboards)
        *   [4.2.1 Gummiboot](#Gummiboot)
        *   [4.2.2 GRUB](#GRUB_2)
*   [5 Konfigurace základního systému](#Konfigurace_z.C3.A1kladn.C3.ADho_syst.C3.A9mu)
    *   [5.1 Konfigurace pacman](#Konfigurace_pacman)
    *   [5.2 Konfigurace sítě](#Konfigurace_s.C3.ADt.C4.9B)
        *   [5.2.1 Pevná LAN](#Pevn.C3.A1_LAN)
        *   [5.2.2 Bezdrátová Lan](#Bezdr.C3.A1tov.C3.A1_Lan)
        *   [5.2.3 Analogový Modem](#Analogov.C3.BD_Modem)
        *   [5.2.4 ISDN](#ISDN)
        *   [5.2.5 DSL (PPPoE)](#DSL_.28PPPoE.29)
*   [6 Update systému](#Update_syst.C3.A9mu)
    *   [6.1 Krása modelu Arch rolling release](#Kr.C3.A1sa_modelu_Arch_rolling_release)
    *   [6.2 Seznamte se s pacmanem](#Seznamte_se_s_pacmanem)
    *   [6.3 Přidání uživatele a nastavení skupin](#P.C5.99id.C3.A1n.C3.AD_u.C5.BEivatele_a_nastaven.C3.AD_skupin)
*   [7 Instalace a konfigurace Hardware](#Instalace_a_konfigurace_Hardware)
    *   [7.1 Konfigurace zvukové karty](#Konfigurace_zvukov.C3.A9_karty)
    *   [7.2 Configuring CPU frequency scaling](#Configuring_CPU_frequency_scaling)
    *   [7.3 Additional tweaks for laptops](#Additional_tweaks_for_laptops)
*   [8 Instalace a konfigurace Xorg](#Instalace_a_konfigurace_Xorg)
    *   [8.1 Úprava rozložení klávesnice](#.C3.9Aprava_rozlo.C5.BEen.C3.AD_kl.C3.A1vesnice)
    *   [8.2 Myš](#My.C5.A1)
    *   [8.3 Použití properitních grafických ovladačů(Nvidia, Ati)](#Pou.C5.BEit.C3.AD_properitn.C3.ADch_grafick.C3.BDch_ovlada.C4.8D.C5.AF.28Nvidia.2C_Ati.29)
        *   [8.3.1 Grafické karty Nvidia](#Grafick.C3.A9_karty_Nvidia)
        *   [8.3.2 ATI Graphic Cards](#ATI_Graphic_Cards)
*   [9 Instalace a konfigurace desktopového prostředí](#Instalace_a_konfigurace_desktopov.C3.A9ho_prost.C5.99ed.C3.AD)
    *   [9.1 Nainstalujte fonty](#Nainstalujte_fonty)
    *   [9.2 ~/.xinitrc (znovu)](#.7E.2F.xinitrc_.28znovu.29)
    *   [9.3 GNOME](#GNOME)
        *   [9.3.1 O GNOME](#O_GNOME)
        *   [9.3.2 Instalace](#Instalace_2)
        *   [9.3.3 Užiteční daemoni pro GNOME](#U.C5.BEite.C4.8Dn.C3.AD_daemoni_pro_GNOME)
        *   [9.3.4 Vzhled](#Vzhled)
    *   [9.4 KDE](#KDE)
        *   [9.4.1 O KDE](#O_KDE)
        *   [9.4.2 Instalace](#Instalace_3)
        *   [9.4.3 Užiteční daemoni pro KDE](#U.C5.BEite.C4.8Dn.C3.AD_daemoni_pro_KDE)
    *   [9.5 Xfce](#Xfce)
        *   [9.5.1 O Xfce](#O_Xfce)
        *   [9.5.2 Instalace](#Instalace_4)
        *   [9.5.3 Užiteční daemoni](#U.C5.BEite.C4.8Dn.C3.AD_daemoni)
    *   [9.6 LXDE](#LXDE)
        *   [9.6.1 O LXDE](#O_LXDE)
    *   [9.7 *box](#.2Abox)
        *   [9.7.1 Fluxbox](#Fluxbox)
        *   [9.7.2 Openbox](#Openbox)
    *   [9.8 fvwm2](#fvwm2)
*   [10 Prohlížeč, kodeky, video přehrávač a užitečné aplikace](#Prohl.C3.AD.C5.BEe.C4.8D.2C_kodeky.2C_video_p.C5.99ehr.C3.A1va.C4.8D_a_u.C5.BEite.C4.8Dn.C3.A9_aplikace)
    *   [10.1 Webový prohlížeč](#Webov.C3.BD_prohl.C3.AD.C5.BEe.C4.8D)
    *   [10.2 VLC](#VLC)
    *   [10.3 Užitečné aplikace](#U.C5.BEite.C4.8Dn.C3.A9_aplikace)
*   [11 Další informace](#Dal.C5.A1.C3.AD_informace)

## Předmluva

### Úvod

Vítejte. Tento dokument vás provede procesem instalace a konfigurace [Arch Linuxu](/index.php/Arch_Linux "Arch Linux"), jednoduché, lehké distribuce GNU/Linuxu zaměřené na pokročilejší uživatele. Tento průvodce je určen novým uživatelům, ale může sloužit jako zdroj informací a referenční příručka i ostatním.

Před instalací samotnou není od věci přojít si [FAQ](/index.php/FAQ "FAQ").

**Hlavní vlastnosti Arch Linuxu:**

*   [Jednoduchý](/index.php/The_Arch_Way "The Arch Way") návrh a filozofie
*   [Všechny balíčky](https://www.archlinux.org/packages/) distribuce jsou zkompilované pro architektury [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)") a [x86_64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64")
*   Archlinux uplatňuje tzv. [Rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") model, kdy se všechen instalovaný software průběžně aktualizuje na nejnovější stabilní verzi.
*   Archlinux používá tzv. [BSD style](/index.php/Arch_boot_process "Arch boot process") (BSD styl init skriptů.)
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"): Jednoduchý a silný tvůrce initrd obrazů.
*   [Pacman](/index.php/Pacman "Pacman"), lehký a výkonný [správce balíčků](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") s malými nároky na paměť.
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System"): systém pro vytváření balíčků představuje jednoduchý ale mocný nástroj na kompilaci vlastních balíčků ze zdrojových kódů.
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"): nabízí mnoho tisíc uživateli vytvořených skriptů vytvářejících balíčky a je i příležitostí ke sdílení vašich vlastních tzv. "build skriptů".

### License

Autorská práva Arch Linux, pacman, dokumentaci and konfigrační skripty drží Judd Vinet (Copyright © 2002-2007) a Aaron Griffin (Copyright © 2007-2012). Výše ivedené podleéha licenci [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### The Arch Way

_**Arch je navržený tak, aby byl co [nejjednodušší](/index.php/The_Arch_Way "The Arch Way").**_

"Jednoduchý" v tomto slova smyslu znamená "bez nepotřebných rozšíření, modifikací nebo komplikací". Ve zkratce: elegantní a minimalistický přístup.

### O tomto průvodci

Instalace Archlinuxů probíhá s pomocí [sady instalačních skriptů](https://github.com/falconindy/arch-install-scripts). Tento průvodce shrnuje základy instalačního procesu pomocí těchto skriptů.

**Note:** Archlinux od verze instalačního media 2012.07.15 již nemá AIF, tedy instalátor v tradičním smyslu slova.

V případě jakýchkoli problémů hledejte řešení na komounitou udržované [Arch wiki](/index.php/Main_page "Main page"), která je skvělým zdrojem informací. Pokud nemůžete svou odpověď najít jinde, zkuste [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanál ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) nebo [fórum](https://bbs.archlinux.org/) uživatelů Archlinuxu. Informace o příkazech, které neznáte najdede v `manuálových stránkách`. Stránku k příslušnému příkazu zobrazíte zadáním `man _příkaz_` do konzole.

**Note:** Chcete-li získat správně nainstalovaný a nakonfigurovaný systém, postupujte podle tohoto průvodce co nejpřesněji, takže _prosím_ čtěte pečlivě. Vždy doporučujeme přečíst nejprve celý oddíl, <u>než</u> se pustíte do dílčích kroků.

Tento průvodce je rozdělen na 4 části:

*   [Část I: Příprava na instalaci](#P.C5.99.C3.ADprava_na_instalaci)
*   [Část II: Instalace systému](#Instalace_z.C3.A1kladn.C3.ADho_syst.C3.A9mu)
*   [Část III: Po instalaci](#Po_instalaci)
*   [Část IV: Extra](#Extra)

## Příprava na instalaci

**Note:** Pokud chcete instalovat z již existující instalace GNU/Linuxu postupujte podle [tohoto návodu](/index.php/Install_from_Existing_Linux "Install from Existing Linux") (anglicky). To se vám může hodit zejména pokud chcete instalovat Arch vzdáleně pomocí [VNC](/index.php/VNC "VNC") nebo [SSH](/index.php/SSH "SSH").

### Získání instalačního média

Oficiální instalační médium můžete stáhnout [odsud](https://archlinux.org/download/). V současné době je aktuání instalační médium [2012.09.07](https://www.archlinux.org/news/new-install-medium-20120907/) a tomuto instalačnímu mediu tento průvodce odpovídá.

#### Zápis obrazu ISO na CD/DVD nebo Flash disk

*   "Vypalte" obraz .iso na CD nebo DVD vaším oblíbeným vypalovacím nástrojem.
*   Nebo zapište obraz .iso na USB Flash disk. Jak to udělat se dozvíte [zde](/index.php/USB_Installation_Media "USB Installation Media").

**Note:** Kvalita optických mechanik, stejně jako CD medií, se liší. Doporučujeme vypalovat obraz nižší rychlostí, 4x nebo 2x. Pokud budete mít při instalaci problémy s médiem, zkuste vypálit disk nejmenší možnou rychlostí.

#### Instalace přes síť

Místo vypalování bootovacího média a CD nebo USB disk, můžete také nabootovat .iso obraz přes síť. Tento postup lze použít, v případě, že už máte nastavený server. Více informací najdete v článku [Instalace Archu přes síť](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") (anglicky), pak pokračujte na [Spuštění instalačního média](#Spu.C5.A1t.C4.9Bn.C3.AD_instala.C4.8Dn.C3.ADho_m.C3.A9dia).

#### Instalace do virtuálního stroje

Instalace do [virtuálního stroje](https://en.wikipedia.org/wiki/Virtual_machine "wikipedia:Virtual machine") je vhogná, když se chcete seznámit s Arch Linuxem a postupuem instalace a přitome nechcete opustit váš stávající operační systém a zasahovat do diskových oddílů. Také vám to umožní mít tohoto průvodce pro začátečníky během instalace otevřený v prohlížeči. Někteří uživatelé také shledávají výhodným mít nezávislou instalaci Arch Linuxu ve virtuálním stroji pro testovací účely.

Příklady virtualizačních nástrojů jsou [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

Přesný postup instalace do virtuálního stroje závisí na použitém software, ale obecně sestává z těchto kroků:

1.  Vytvoření virtuálního diskového oddílu pro nový operační systém.
2.  Správná konfigurace parametrů budoucího virtuálního stroje.
3.  Spuštění staženého obrazu .iso z virtuální CD mechaniky virtuálního stroje.
4.  Další kroky podle [Spuštění instalačního média](#Spu.C5.A1t.C4.9Bn.C3.AD_instala.C4.8Dn.C3.ADho_m.C3.A9dia).

Jako další zdroje informací mohou být užitečné tyto články:

*   [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest") (anglicky)
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox") (anglicky)
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive") (anglicky)
*   [Installing Arch Linux in VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware") (anglicky)

### Spuštění instalačního média

Nejprve může být třeba změnit v BIOSu počítače pořadí zařízení ze kterých se počítač postupně spouští. Je-li to třeba, při spuštění počítače stiskněte klávesu pro vstup do BIOSu (obvykle `Delete`, `F1`, `F2`, `F11` nebo `F12`). Až tak učiníte mělo by dojít ke spuštění instalačního média. Pro započetí instalace vyberte v menu "Boot Arch Linux" a stiskněte `Enter`.

**Tip:** Pro základní instalaci je potřeba alespoň 64MB operační paměti.

**Note:** Uživatelé,kteří usilují o instalaci Arch Linuxu vzdáleně přes [SSH](/index.php/SSH "SSH") musí v tomto bodě instalace provést další kroky, které umožní SSH připojení k běžícímu prostředí Live CD. Pokud vás to zajímá, přečtěte si tento [článek](/index.php/Install_from_SSH "Install from SSH") (anglicky).

##### Ověření zda "bootujeme" v UEFI režimu

V případě, že máte základní desku vybavenou [UEFI](/index.php/UEFI "UEFI"), se při spuštění CD/DVD spustí tzv. UEFI shell, který se dotáže zda povolíte spuštění spouštěcího skriptu `startup.nsh`. Spuštění UEFI shellu povolte. Po spuštění instalačního média zkontrolujte, zda jste skutečně "nabootovali" v UEFI režimu. Ještě před použitím `chroot` nahrajte `efivars` jaderný modul a pak zkontrolujte existenci souborů v adresáři `/sys/firmware/efi/vars/`:

```
# modprobe efivars       # before chrooting
# ls -1 /sys/firmware/efi/vars/

```

**Note:** Jaderný modul `efivars` detekuje a pro systém zpřístupní běhové proměnné UEFI systému `/sys/firmware/efi/vars`. Tento modul se **nenahrává automaticky**. Pokud neexistují žádné soubory v `/sys/firmware/efi/vars`, nebyl zřejmě modul zaveden nebo bylo jádro spuštěno s parametrem `noefi`. Tyto proměnné pak upravuje `efibootmgr`, který doplní položky zavaděče do spouštěcí nabídky UEFI systému. Máme-li spuštěno ve standardním BIOS režimu, není při zavedení modulu `efivars` generována žádná chyba. Pro kontrolu, zda jsme skutečně v UEFI režimu, je třeba zkontrolovat soubory v `/sys/firmware/efi/vars`.

**Note:** Ony totiž některé základní desky "jen vypadají", že disponují plnohodnotným UEFI systémem, ale ve skutečnosti bootují standardní BIOS (pozn. překl).

##### Řešení problémů se spuštěním

*   Pokud má váš systém grafickou kartu integrovanou v chipsetu a spuštění instalačního média zkončilo černou obrazovkou, je zřejmě problém v tzv. Kernel Mode Setting ([KMS](/index.php/KMS "KMS")). Tento problém pravděpodobně obejdete tak, že změníte parametry spuštění instalačního médie. Restartujte systém, vyberte v menu instalačního media nabídku, která spouští systém (i686 nebo x86_64) a stiskněte klávesu `Tab`. Tím se dostanete do editačního režimu, kde na úplný konec řádku připište `nomodeset` a stiskněte `Enter`. Pokud nechcete úplně zakázat KMS, zkuste místo toho parametr `video=SVIDEO-1:d`. Podrobnosti viz. tento [článek](/index.php/Intel "Intel").

*   Pokud obrazovka _nezčerná_, ale start systému se "zasekne" ve fázi spuštění jádra, doplňte (viz. o bod výše) na konec řádku parametr `acpi=off`.

## Instalace

Nyní se nacházíte v příkazové řádce, automaticky přihlášený jako root.

### Nastavení jazyka

**Tip:** Toto nastavení není pro většinu uživatelů potřeba. Praktické to může být, pokud chcete během instalace zapisovat konfigurační soubory ve svém jazyce nebo pokud potřebujete například zadat heslo k Wi-Fi včetně znaků diakritiky nebo chcete mít zprávy systému (případné chybové hlášky) ve svém jazyce.

Ve výchozím nastavení je rozložení klávesnice nastaveno na `us`. Pokud máte jiné rozložení klávesnice než [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg") zadejte příkaz:

```
# loadkeys _layout_

```

...kde _layout_ může být například `fr`, `uk`, `be-latin1`, atd. Viz. tento [seznam možných rozložení](/index.php/KEYMAP#Keyboard_layouts "KEYMAP").

**Tip:** Pro češtinu během instalace zadejte: `loadkeys cz-qwertz`.

V souvislosti ze změnou rozložení kláves je obvykle třeba změnit i písmo, protože většina jazyků obsahuje více znaků než [anglická abeceda](https://en.wikipedia.org/wiki/English_alphabet "wikipedia:English alphabet"). Jinak budou neznáme znaky zobrazeny jako čtverečky nebo jiné symboly. Mějte na paměti, že název zakové sady obsahuje velká a malá písmena a musí být zapsán _přesně_, např.:

```
# setfont Lat2-Terminus16

```

**Tip:** Je vhodný i pro češtinu.

Jazyk je ve výchozím nastavení nastaven na angličtinu. Pokud chcete nastavit jazyk pro proces instalace upravte soubor [locale](http://www.greendesktiny.com/support/knowledgebase_detail.php?ref=EUH-483), kde smažte znak `#` na začátku řádku požadovaného jazyka a kódování. Prosíme, vždy takto vyberte alespoň kódování `UTF-8`.

Použijte editor nano, pro češtinu takto:

 `# nano /etc/locale.gen` 

```
cs_CZ.UTF-8 UTF-8
cs_CZ ISO-8859-2
```

Stiskněte `Ctrl+X` pro ukončení editoru, klávesu `Y` pro potvrzení a klávesu `Enter` pro uložení pod stejným názvem, tedy přepsání souboru. Pak spusťte příkazy:

```
# locale-gen
# export LANG=cs_CZ.UTF-8

```

Pamatujte, že národní mapu kláves aktivujete / deaktivujete stiskem `Levý Alt+Levý Shift`.

* * *

### Nastavení připojení k internetu

Při spuštění instalace se automaticky spouští síťový démon `dhcpcd`, který se pokusí konfigurovat připojení k internetu síťovým kabelem, je-li toto dostupné Zkuste tedy "pingnout" nějaký web v internetu, abyste ověřili funkčnost připojení. Google například, vždy běží :-):

 `# ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms
```

Obdržíte-li hlášku `ping: unknown host`, budete muset nastavit síť ručně, jak je vysvětleno níže.

V opačném případě pokračujte kapitolou [Příprava pevného disku](#P.C5.99.C3.ADprava_pevn.C3.A9ho_disku).

#### Připojení síťovým kabelem

Jste-li připojeni síťovým kabelem a démon `dhcpcd` nenakonfiguroval funkční připojení k internetu automaticky, postupujte podle tohoto návodu.

Je-li váš počítač připojen k síti ethernet, existuje téměř vždy jedno síťové rozhraní pojmenované `eth0`. Máte-li více síťových karet, jejich názvy sledují tuto konvenci `eth1`, `eth2` atd..

Pri konfiguraci sítě potřebujete znát tyto parametry platné pro vaši síť:

*   Pevnou IP adresu.
*   Masku podsítě.
*   IP adresu výchozí brány.
*   IP adresu alespoň jednoho DNS serveru.
*   Případně jméno domény (pokud se neacházíte v místní síti, kde na tom nezáleží).

Nejprve aktivujeme síťové rozhraní `eth0`:

```
# ip link set eth0 up

```

Nastavíme mu pevnou IP adresu:

```
# ip addr add <ip address>/<subnetmask> dev <interface>

```

například:

```
# ip addr add 192.168.1.2/24 dev eth0

```

Více možností získáte na manuálové stránce: spusťte příkaz `man ip`.

Nastavíme výchozí bránu:

```
# ip route add default via <ip address>

```

například:

```
# ip route add default via 192.168.1.1

```

V souboru `resolv.conf` nastavíme IP adresy DNS serverů a jméno místní domény:

 `# nano /etc/resolv.conf` 

```
nameserver 61.23.173.5
nameserver 61.95.849.8
search example.com
```

**Note:** V současné době můžete nastavit maximálně 3 různé jmenné (DNS) servery, tj. 3 řádky `nameserver`.

Nyní byste měli mít funkční připojení k inernetu. Není-li tomu tak, konzultujte podrbnou stránku [konfigurace sítě](/index.php/Configuring_Network "Configuring Network") (anglicky).

#### Bezdrátové připojení

Tento postup vám umožní získat během instalace bezdrátové (Wi-Fi) připojení k internetu.

Po spuštění instalačního prostředí máte k dispozici ovladače pro bezdrátová zařízení i nástroje pro jejich konfiguraci. Pro úspěšnou konfiguraci připojení je ovšem důležité je vědět, jaký hardware bezdrátové sítě ve svém počítači. Mějte na paměti, že následující kroky _nastaví síť pouze v instalačním prostředí_. Tyto kroky pak (nebo jinou ekvivalentní formu konfigurace bezdrátové sítě) _bude nutné opakovat_ v nově nainstalovaném systému až ho nakonec spustíme.

Také si uvědomte, že pokud není při instalaci potřeba bezdrátové připojení, můžete následující kroky provést kdykoliv později.

**Note:** Následující příklad používá jako název bezdrátového rozhraní wlan0 a 'linksys' jako ESSID sítě, ke které se připojujeme. Nezapomeňte tyto parametry změnit tak, aby odpovídaly vaší situaci.

Základní postup:

*   Identifikujte bezdrátové rozhraní

```
# lspci | grep -i net

```

nebo, púokud máte USB Wi-Fi zařízení:

```
# lsusb

```

*   Zadáním příkazu `iwconfig`, se ujistěte, že `udev` zavedl správný ovladač zařízení a že ovladač vytvořil síťové rozhraní.

**Note:** Jestli nevidíte výstup podobný tomuto, pak ovladač zařízení nebyl zaveden. V tom případě musíte zavést ovladač sami. Prosím následujte tyto [instrukce](/index.php/Wireless_Setup "Wireless Setup") (anglicky).

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

V tomto příkladě je `wlan0` jméno bezdrátového síťového rozhraní.

*   Zapněte bezdrátové rozhraní příkazem:

```
# ip link set wlan0 up

```

Některé bezdrátové adaptéry mohou kromě kromě ovladačů vyžadovat ještě firmware. Pokud váš adaptér vyžaduje firmware, při zapnutí rozhraní nejspíš dostanete takové chybové hlášení:

 `# ip link set wlan0 up`  `SIOCSIFFLAGS: No such file or directory` 

Pokud si nejste jistí jaký firmware potřebujete, příkazem `/usr/bin/dmesg` zobrazte log jádra a v něm najděte žádost zařízení o zavedení firmwaru.

Toto je například hlášení bezdrátového chipsetu Intel, který važaduje firmware::

 `# dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Pokud neuvidíte žádný výstup, váš bezdrátový adaptér nejspíš firmware nevyžaduje.

**Warning:** Firmware pro bezdrátové adaptéry je naleznete při běhu instalačního prostředí v `/usr/lib/firmware`, ale je potřeba ho ručně přidat do nově instalovaného systému, jinak po restartu nebudete mít k dispozici bezdrátovou síť! _Výběr a instalace balíčků bude popsána později. Ujistěte se, že při výběru nezapomenete nainstalovat jak ovladače tak jejich odpovídající firmware! Informace o požadavcích různých bezdrátových čipů najdete v článku [Wireless Setup](/index.php/Wireless_Setup_(%C4%8Cesky) "Wireless Setup (Česky)")._

Nakonec použijte pro připojení k síti příkaz `wifi-menu` z balíčku nástrojů [netcfg](https://aur.archlinux.org/packages/netcfg/)<sup><small>AUR</small></sup>:

```
# wifi-menu wlan0

```

Nyní byste měli mít k dispozici funkční připojení k internetu. Není-li tomu tak, hledejte řešení [zde](/index.php/Wireless_Setup "Wireless Setup") (anglicky).

#### Připojení xDSL (PPPoE), analogovým modemem nebo ISDN

Máte-li xDSL (ADSL/VDSL) router v režimu bridge, spusťte:

```
# pppoe-setup

```

*   Zadejte uživatelské jméno, které vám přidělil poskytoval připojení.
*   Stiskněte `Enter` pro zadání "eth0".
*   Stiskněte `Enter` pro volbu "no", takže budete připojeni neustále..
*   Zapište `server` (to je nejobvyklejší možnost).
*   Stiskněte `1` pro volbu firewall.
*   Zadejte heslo, které vám přidělil poskytoval připojení.
*   Stiskněte `y` k ukončení průvodce.

Tato nastavení použijete a připojení spustíte příkazem:

```
# pppoe-start

```

Připojení analogovým modem nebo ISDN popisuje tento návod: [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection") (anglicky).

#### Připojení za serverem proxy

Pokud je vaše připojení chráněno (a omezeno) proxy serverem, bude třeba nastavit proměnné prostředí `http_proxy` a `ftp_proxy`. V tom případě se podívejte **[sem](/index.php/Proxy "Proxy")**.

### Příprava pevného disku

**Warning:** Rozdělování pevného disku může zničit vaše data. **Nezapomeňte** si zálohovat důležité soubory.

Úplným začátečníkům doporučujeme použít před instalací Arch Linuxu nějaký grafický nástroj, jako je například [GParted](http://gparted.sourceforge.net/download.php), který lze spustit z některé z "live" distribucí Linuxu, jako jsou [Parted Magic](https://en.wikipedia.org/wiki/Parted_Magic "wikipedia:Parted Magic"), [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu_(operating_system) "wikipedia:Ubuntu (operating system)"), [Linux Mint](https://en.wikipedia.org/wiki/Linux_Mint "wikipedia:Linux Mint"), a další. Viz. stránka [Partitioning](/index.php/Partitioning "Partitioning") (anglicky), kde najdete základní informace i důležitá doporučení pokud jde souborové systémy.

**Note:** `cfdisk` je natolik uživatelsky nepřívětivý, že je i pro zkušeného uživatele rychlejší použít před instalací Gparted. (pozn. překl.)

Pokud jste rozdělení oddílů disku provedli před instalací, můžete přejít k části [Nastavení přípojných bodů](#Nastaven.C3.AD_p.C5.99.C3.ADpojn.C3.BDch_bod.C5.AF).

V opačném případě, vizte následující příklad.

#### Příklad

Instalační medium Arch Linuxu obsahuje tyto nástroje:

*   [cfdisk](https://en.wikipedia.org/wiki/cfdisk "wikipedia:cfdisk") – podporuje pouze [MBR](/index.php/MBR "MBR") tabulky oddílů.

*   [gdisk](https://en.wikipedia.org/wiki/gdisk "wikipedia:gdisk") – podporuje pouze [GPT](/index.php/GPT "GPT") tabulky oddílů.

*   [parted](https://en.wikipedia.org/wiki/parted "wikipedia:parted") – podporuje oboje.

Tento příklad používá nástroj **cfdisk**, ale není problém použít např. **gdisk**, který umožňuje použít GPT tabulku oddílů.

**Note:** Pokud máte základní desku vybavenou [UEFI](/index.php/UEFI "UEFI") musíte vytvořit zvláštní diskový oddíl tzv. _UEFI System partition_. Viz. [tento článek](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface") (anglicky).

**Note:** Pokud budete instalovat zavaděč GRUB v režimu BIOS-GPT, musíte vytvořit "BIOS Boot Partition" o velikosti 2 MiB. Viz. [GRUB#GPT_specific_instructions](/index.php/GRUB#GPT_specific_instructions "GRUB") (anglicky).

**Note:** Pokud instalujete Arch Linux na flash disk, přečtěte si [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key") (anglicky).

**Note:** Pokud neplánujete tzv. "dual boot" spolu s opreačním systémem Windows, doporučujeme použít [GPT](/index.php/GPT "GPT") tabulku oddílů místo [MBR](/index.php/MBR "MBR"). V tom případě budete muset použít pro rozdělení disku **gdisk** nebo **parted**. Seznam výhod tohoto řešení najdete [zde](/index.php/GPT "GPT") (anglicky).

```
# cfdisk /dev/sda

```

**Warning:** Až sem je překlad aktuální. Následuje kus textu z anglické verze.

The example system will contain a 15 GB root (`/`) partition, a 1 GB `swap` partition, and a `/home` partition for the remaining space.

It should be emphasized that partitioning is a personal choice and that this example is only for illustrative purposes. See [Partitioning](/index.php/Partitioning "Partitioning").

**Root:**

*   Choose New (or press `N`) – `Enter` for Primary – type in "15360" – `Enter` for Beginning – `Enter` for Bootable.

**Swap:**

*   Press the down arrow to move to the free space area.
*   Choose New (or press `N`) – `Enter` for Primary – type in "1024" – `Enter` for Beginning.
*   Choose Type (or press `T`) – press any key to scroll down the list – `Enter` for 82.

**Home:**

*   Press the down arrow to move to the free space area.
*   Choose New (or press `N`) – `Enter` for Primary – `Enter` to use the rest of the drive (or you could type in the desired size).

Here's how it should look like:

```
Name    Flags     Part Type    FS Type          [Label]       Size (MB)
-----------------------------------------------------------------------
sda1    Boot       Primary     Linux                             15360
sda2               Primary     Linux swap / Solaris              1024
sda3               Primary     Linux                             133000*

```

Double check and make sure that you are happy with the partition sizes as well as the partition table layout before continuing.

If you would like to start over, you can simply select Quit (or press `Q`) to exit without saving changes and then restart cfdisk.

If you are satisfied, choose Write (or press `Shift+W`) to finalize and to write the partition table to the drive. Type "yes" and choose Quit (or press `Q`) to exit cfdisk without making any more changes.

Simply partitioning is not enough; the partitions also need a [filesystem](/index.php/File_systems "File systems"). To format the partitions with an ext4 filesystem:

**Warning:** Double check and triple check that it's actually `/dev/sda1` that you want to format.

```
# mkfs.ext4 /dev/sda1
# mkfs.ext4 /dev/sda3

```

Format and activate the swap partition:

```
# mkswap /dev/sda2
# swapon /dev/sda2

```

**Warning:** Zde končí vložený aktuální text, následuje starý neaktuální překlad.

### Mount the partitions

Each partition is identified with a number suffix. For example, `sda1` specifies the first partition of the first drive, while `sda` designates the entire drive.

To see the current partition layout:

```
# lsblk /dev/sda

```

Pay attention, because the mounting order is important.

First, mount the root partition on `/mnt`. Following the example above (yours may be different), it would be:

```
# mount /dev/sda1 /mnt

```

Then mount the `/home` partition and any other separate partition (`/boot`, `/var`, etc), if you have any:

```
# mkdir /mnt/home
# mount /dev/sda3 /mnt/home

```

In case you have a separate `/boot` partition:

```
# mkdir /mnt/boot
# mount /dev/sda_X_ /mnt/boot

```

In case you have a UEFI motherboard, mount the UEFI partition:

```
# mkdir /mnt/boot/efi
# mount /dev/sda_X_ /mnt/boot/efi

```

### Výběr balíčků

Všechny balíčky, které se instalují jsou z repozitáře [core]. Balíčky jsou dále rozděleny do skupin **Base** a **Base-devel**. Informace o balíčcích a zběžný popis najdete [zde](https://www.archlinux.org/packages/?repo=Core&arch=i686&limit=all&sort=pkgname).

Nejprve vyberte skupiny balíčků:

**Note:** Skupina **base** je automaticky vybrána. Použijte mezerník k označení nebo odznačení balíčků.

Base 

Balíčky z [core] repozitáře poskytují minimální základní prostředí. Tuto skupinu vyberte vždy a odznačte jen ty balíčky, které opravdu nepotřebujete.

Base-devel 

Dodatečné balíčky z [core], jako`make` a `automake`. Většina začátečníků by měla tuto skupinu vybrat, protože tyto programy nejspíš později bude potřeba.

Po vybrání skupin bude zobrazen seznam všech balíčků k instalaci. Nyní je možné zrušit některé zbytečné programy. Použijte mezerník o označení a odznačení.

**Note:** Pokud chcete připojení k bezdrátové síti, nezapomeňte vybrat balíček **wireless_tools**. Některé bezdrátové adaptéry také potřebují [**ndiswrapper**](/index.php/Wireless_network_configuration#ndiswrapper "Wireless network configuration") a/nebo [**firmware**](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration"). Pokud chcete používat WPA šifrování, budete také potřebovat [**wpa_supplicant**](/index.php/WPA_supplicant "WPA supplicant"). Stránka [Wireless Setup](/index.php/Wireless_Setup_(%C4%8Cesky) "Wireless Setup (Česky)") vám pomůže vybrat správné balíčky pro vaše zařízení. Také zvažte instalaci [**netcfg**](/index.php/Netcfg "Netcfg"), který vám pomůže s konfigurací sítových profilů v novém systému.

Po vybrání potřebných balíčků se vraťte do menu a pokračujte dalším krokem, **Install Packages**.

### Instalace balíčků

_Instalace balíčků_ nainstaluje vybrané balíčky do nového systému. Pokud vyberete jako zdroj CD/USB nainstalují se balíčky přímo z instalačního média. Pokud jste zvolili Netinstall, stáhnou se z internetu nejaktuálnější balíčky.

**Note:** V některých instalátorech budete dotázání, jestli chcete zachovat cache pacmana. Pokud zvolíte ano, budete mít možnost později [downgradovat](/index.php/Downgrade_packages "Downgrade packages") balíček na předchozí verzi, takže tuto volbu doporučujeme (cache je možné kdykoliv v případě potřeby vyčistit).

Po stažení všech balíčků zkontroluje instalátor jejich integritu a nainstaluje je do systému.

### Konfigurace systému

**Tip:** Pečlivé následování průvodce a pochopení jednotlivých voleb je důležité ke správně konfiguraci Arch Linuxu.

V této fázi instalace provedete nastavení vaší nové instalace Arch Linuxu. Předchozí verze instalátoru obsahovaly [hwdetect](/index.php/Hwdetect "Hwdetect"), který sbíral infromace o dostupném hardware a na základě toho generoval konfiguraci systému. Tato funkce byla nahrazena moderním nástrojem **[udev](/index.php/Udev "Udev")**, který by měl zvládnout načíst většinu potřebných modulů automaticky behěm startu systému.

Nejdřív budete dotázání, který editor chcete použit. Vyberte [nano](/index.php/Nano "Nano"), [joe](http://joe-editor.sourceforge.net/) nebo [[Vim|vi]. `nano` je všeobecně považováno za nejjedndušši z uvedených tří editorů. Na wiki stránkách jednotlivých editorů najdete instrukce jak je použít. Dále bude zobrazeno menu se seznamen nejdůležitějších konfiguračních souborů systému.

**Note:** V této fázi je velmi důležité upravit, nebo alespoň otevřít každý ze souborů. Instalační skript spoléhá na váš vstup, než aby vytvořil tyto soubory. Častou chybou je přeskočení těchto kritických kroků konfigurace.

**Nemohl by to dělat instalátor automaticky?**

Skrytí procesu konfigurace systému je v rozporu s _**[filozofií Arch Linuxu](/index.php/The_Arch_Way "The Arch Way")**_. Je pravda, že současné verze jádra a nástrojů pro detekcí hardware nabízejí perfektní podporu auto-konfigurace, Arch ale dává uživatelům možnost konfigurace během instalace za účelem _transparentnosti a kontroly systémových zdrojů_. Když dokončíte úpravy těchto souborů, pochopíte jednduchost ruční konfigurace Arch Linuxu a seznámíte se blíže s jeho základní strukturou, takže budete lépe připraveni na spravování svého nového systému.

#### /etc/rc.conf

Arch Linux používá soubor `/etc/rc.conf` jako základní zdroj systémové konfigurace. Tento jediný soubor obsahuje široké množství nastavení a voleb použitých při startu systému. Jak název napovídá, obsahuje také nastavení pro spouštění souborů /etc/rc* a zdrojovou konfiguraci pro tyto soubory.

* * *

##### Sekce LOCALIZATION (lokalizace)

_**Ukázka sekce LOCALIZATION:**_

```
LOCALE="cs_CZ.utf8"
HARDWARECLOCK="localtime"
USEDIRECTISA="no"
TIMEZONE="Europe/Prague"
KEYMAP="cs"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

```

LOCALE 

Toto nastavuje systémové locales, které se použijí lokalizované aplikace. Seznam dostupných locales získáte příkazem `locale -a` z příkazové řádky.

HARDWARECLOCK 

Určuje, jestli se při startu a ukončení systému mají hardwarové hodiny synchronizovat podle **UTC** nebo **localtime**. UTC je vhodnější, díky jednodušším změnám časových zón a letního času. localtime je nutný, pokud máte na počítači dualboot s Windows, které ukládají čas v localtime (pokud se vám povede přinutit Windows, aby používaly UTC, nastavte zde UTC, ušetříte si problémy s předchodem na letní/zimní čas).

USEDIRECTISA 

Použije při synchronizaci času přímý I/O požadavek místo zápisu do `/dev/rtc`.

TIMEZONE 

Nastavení časové zóny. (Všechny dostupné zóny najdete v `/usr/share/zoneinfo/`).

KEYMAP 

Rozložení klávesnice. Dostupná rozložení jsou v `/usr/share/kbd/keymaps`. Toto rozložení se aplikuje pouze v konzoli, ale už ne v grafickém prostředí!

CONSOLEFONT 

Konzolový font. Dostupné fonty jsou v `/usr/share/kbd/consolefonts/` Výchozí hodnota (prázná) je bezpečná.

CONSOLEMAP 

Definuje mapu konzole, která se má načíst `setfont`em při bootu. Dostupné mapy jsou v `/usr/share/kbd/consoletrans`. Výchozí hodnota (prázdná) je bezpečná.

USECOLOR 

Zvolte "yes", pokud máte barevný monitor a chcete si užívat barviček v konzoli.

* * *

##### Sekce HARDWARE

_**Příklad pro HARDWARE:**_

```
# Scan hardware and load required modules at boot
MOD_AUTOLOAD="yes"
# Module Blacklist - Deprecated
MOD_BLACKLIST=()
#
MODULES=(!net-pf-10 !pcspkr loop)

```

MOD_AUTOLOAD 

Nastavním na hodnotu "yes" se pro detekci hardware použije **udev** . UDev se postará o načtení potřebných modulů a ovladačů pro všechna zařízení. Nastavením na "no" bude systém spoléhat pouze na vaši ruční konfiguraci.

MOD_BLACKLIST 

Tato volba je zastaralá, moduly, které se nemají při startu načítat mohou být umístěny přímo do pole **MODULES=** níže.

MODULES 

Definuje, které dodatečné moduly se mají při bootu načítat. Pokud máte k dispozici disketovou mechaniku, přidejte modul "floppy". Pokud chcete připojovat soubory jako bloková zařízení (tzv. loopback), přidejte "loop". Pokud chcete explicitně zakázat načítání některých modulů, uveďte je s prefixem "!" V tomto příkladě jsou zákázany moduly IPv6 a otravný PC speaker. Pokud jste u MOD_AUTOLOAD yvolili "no", musíte uvést všechny moduly, které může systém potřebovat.

* * *

##### Sekce NETWORKING

HOSTNAME 

Hostname si nastavte dle libosti. Jedná se o název počítače v síti. Ať už nastavíte cokoliv, nezapomeňte pak změnit i záznam v `/etc/hosts`

eth0 

'Ethernet, karta 0'. _Pokud_ používáte **statickou IP adresu**, upravte adresu rozhraní, síťovou masku, a broadcast adresu. Nastavte na eth0="dhcp", pokud chcete použít **DHCP** pro automatickou konfiguraci.

INTERFACES 

Sem uveďte všechna síťová rozhraní. Vícero rozhraní oddělte mezerou, např. (eth0 wlan0)

gateway 

Pokud používáte **statickou IP**, nastave adresu brány. Pokud používáte **DHCP**, můžete toto pole ignorovat. Některé routery ale mohou tuto konfiguraci vyžadovat.

ROUTES 

Pokud používáte statickou **IP**, odstraňte **!** z pole 'gateway'. Pokud používáte **DHCP**, můžete zpravidla nechat tuto proměnnou zakomentovanou vykřičníkem (!). Občas je nutné ale ROUTES a gateway nastavit. Pokud budete mít problémy s připojením, vraťte se k této konfiguraci.

**Příklad s dynamickou IP (_DHCP_):**

```
HOSTNAME="arch"
#eth0="eth0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
eth0="dhcp"
INTERFACES=(eth0)
gateway="default gw 192.168.0.1"
ROUTES=(!gateway)

```

**Příklad se statickou IP:**

```
HOSTNAME="arch"
eth0="eth0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
INTERFACES=(eth0)
gateway="default gw 192.168.0.1"
ROUTES=(gateway)

```

Při použití statické IP, upravte v `/etc/resolv.conf` záznamy o DNS serverech, viz [níže](#.2Fetc.2Fresolv.conf).

**Note:** Pokud se připojujete k bezdrátové síti, je potřeba udělat pár kroků navíc a nastavit nějakého správce sítě, například [netcfg](/index.php/Netcfg "Netcfg") nebo [wicd](/index.php/Wicd "Wicd"). Pro více informací se podívejte do článku [Wireless Setup](/index.php/Wireless_network_configuration#Part_II:_Wireless_management "Wireless network configuration")

**Tip:** Pokud používáte nestandardní velikost MTU (tzv. jumbo frames) a váš hardware tuto funkci podporuje, podívejte se do článku [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames").

* * *

##### Sekce DAEMONS

Toto pole obsahuje seznam názvů skriptů uložených v /etc/rc.d, které se mají spouštět při startu systému. Démoni se spouští v takovém pořadí, v jakém jsou uvedení v poli. Pro urychlení bootu je také možné nastavit asynchronní inicializaci na pozadí.

```
DAEMONS=(network @syslog-ng netfs @crond)

```

*   Jestliže je před názvem skriptu vykřičník (!), skript se nespustí.
*   Jestliže je před názvem zavináč (@), bude skript spuštěn na pozadí - tzn. že systém nebude čekat na úspěšné spuštění démona, ale rovnou přejde ke spouštění dalšího (užitečné pro zrychlení startu systému). Nespouštějte na pozadí démony, kteří jsou vyžadování jinými démony, například "mpd" závisi na "network", proto by spouštění "network" na pozadí mohlo "mpd" rozbít.
*   Pokud po instalaci nové služby chcete, aby se automaticky spouštěla po startu, upravte toto pole.

**Note:** 'BSD-styl' spouštění, který v Archu použiváme, je elegantním řešením toho, co ostatní distribuce řeší různými symlinky do adresáře /etc/init.d.

**O démonech**

Pole [[Sekce DAEMONS]|DAEMONS] není v tuto chvíli potřeba měnit, ale je užitečné vysvětlit, co to vlastně je, protože v pozdějších částech se k nim ještě dostaneme.

_Démon_ je program, který běží na pozadí, čeká na nějaké události a poskytuje různé služby. Dobrým příkladem je webserver, který čeká na požadavek na doručení webové stránky (třeba httpd), nebo SSH server, který čeká na příhlášení uživatele (sshd). Toto jsou příklady plnohodnotných aplikaci, ale existují i malí skrytí démoni, kteří například zapisují informace do logů (syslog, metalog) nebo démon, který poskytuje grafické přihlášení (gdm, kdm, ...). Všechny tyto programy je možné přidat do seznamu démonů a systém je automaticky spustí při startu. Užiteční démoni budou v tomto průvodci ještě zmíněni.

Historicky, výraz _démon_ (angl. daemon) vznikl v MIT na projektu MAC. Vývojáři převzali jméno z _Maxwellova démona_, imaginární bytosti ze slavného myšlenkového pokusu, která sedí na pozadí a třídí molekuly. *nixové systémy převzaly tuto terminologii a vytvořili opačný acronym **d**isk **a**nd **e**xecution **mon**itor.

**Tip:** Všichni démoni v Arch Linuxu jsou drženi v /etc/rc.d/

#### /etc/fstab

**fstab** ( **f**ile **s**ystems **tab**le - tabulka souborových systémů) je soubor, který obsahuje seznam všech dostupných disků a oddílů a určuje, kam a jak se mají připojit. Soubor **/etc/fstab** je nejčastěji používán programem **mount**. Program mount bere souborový systém na zařízení a připojuje ho do hlavního adresářového podstromu. /etc/rc.sysinit volá **mount -a** přibližně ve třech čtvrtinách bootovacího procesu a program mount čte celý /etc/fstab aby zjistil, které oddíly, kam a jak má připojit. Pokud k filesystému přidáte volbu **noauto** /etc/fstab, **mount -a** tento oddíl nepřipojí.

_An example of `/etc/fstab`_

```
# <file system>        <dir>        <type>        <options>                 <dump>    <pass>
none                   /dev/pts     devpts        defaults                       0         0
none                   /dev/shm     tmpfs         defaults                       0         0
/dev/sda1                   /          jfs        defaults,noatime               0         1
/dev/sda2                   /var     reiserfs     defaults,noatime,notail        0         2
/dev/sda3                    swap     swap        defaults                       0         0
/dev/sda4                   /home      jfs        defaults,noatime               0         2

```

**Note:** Volba 'noatime' vypíná zápis informace o posledním čase čtení. Tato volba zvyšuje výkon a snižuje spotřebu energie (viz [[1]](http://kerneltrap.org/node/14148)). Volba 'notail' u ReiserFS vypíná funkci tailpacking. Výsledkem je lepší výkon za cenu trošku horšího využití disku

<file system> 

popisuje bloková zařízení nebo vzdálené souborové systémy, které se mají připojit. Pro standardní připojování, toto pole obsahuje název souboru pro blokové zařízení (vytvořeného programem mknod během bootu), například '/dev/cdrom' nebo '/dev/sda1'.

**Note:** Pokud váš systém má více jak jeden pevný disk, instalátor použije UUID, místo sd_x_ kvůli konzistenci v mapování disků **[Použití UUID](/index.php/Persistent_block_device_naming "Persistent block device naming") má několik výhod a předchází problémům, které mohou nastat, když v budoucnu připojíte další pevný disk.** Kvůli aktivnímu vývoji jádra a udevu se také může měnit pořadí, ve kterém ovladače nahrávají jednotlivé řadiče na desce. Téměř každá deska má vícero řadičů (SATA/IDE) a kvůli zmíněným změnám, se při dalším bootu může /dev/sda jmenovat /dev/sdb a naopak. (Viz [tento článek](/index.php/Persistent_block_device_naming "Persistent block device naming") pro více informací o bezpečném mapování zařízení).

<dir> 

popisuje přípojný bod; adresář, kam se má filesystém přípojit. U swapovacího oddílu uveďte 'swap' (swapovací oddíly nejsou ve skutečnosti připojovány do stromu adresářů)

<type> 

informuje o typu souborového systému. Linux podporuje mnoho souborových systému (seznam všech souborových systémů podporovaných právě běžícím jádrem najdete v /proc/filesystems). Záznam 'swap' určuje, že se jedná o odkládací oddíl. Záznam 'ignore' způsobí, že daná řádka bude ignorována.

<options> 

dodatečné volby pro připojení souborového systému. Jde o čárkami oddělený seznam bez mezer. Každý filesystém může podporovat jiné volby. Dodatečné informace o souborových systémech, najdete v 8\. kapitole manuálových stránek mount.

<dump> 

používá se programem dump(8) a určuje, jestli se daný oddíl má zálohovat nebo ne. Hodnota 0 znamená zálohování vypnuto. _Nástroj dump není součástí výchozí instalace Arch Linuxu._

<pass> 

použivá se programem fsck(8) a určuje, jestli a v jakém pořadí se má při spuštení provádět kontrola integrity souborového systému. Kořenový oddíl by měl mít hodnotu <pass> 1, další oddíly pak 2 nebo 0\. Pokud má více oddílu stejnou hodnotu <pass> a oddíly se nachází na různých fyzických zařízeních, proběhne kontrola paralelně. Pokud jsou oddíly na jednom zařízení, proběhne konrola v takovém pořadí, v jakém jsou záznamy uvedené v tomto souboru.

Více informací najdete v článku o [Fstab](/index.php/Fstab "Fstab").

#### **[/etc/mkinitcpio](/index.php?title=Konfigurace_mkinitcpio&action=edit&redlink=1 "Konfigurace mkinitcpio (page does not exist)").conf**

_Ve většině případů není nutné v tuto chvíli soubor upravovat, ale přečtěte si prosím následující informace._

Tento soubor umožňuje další dolaďování inital ram filesystemu, tzv. initramfs (historicky označovaného jako initial ramdisk, "initrd") pro váš systém. initramfs je zkomprimovaný obraz, který je načítán jádrem při startu. Účelem je poskytnout minimální filesystém s potřebnými nástroji tak, aby jádro mohlo připojit kořenový filesystém. To znamená načíst moduly, které jsou potřeba pro práci s IDE, SCSI nebo SATA zařízeními. Jakmile initramfs načte potřebné moduly, předá kontrolu jádru a bootovaní pokračuje. Z toho důvodu initramfs obsahuje pouze moduly potřebné, pro připojení kořenové filesystému a nemusí obsahovat všechny moduly, které kdy bude potřeba. Většina jaderných modulů bude načteno udevem později během bootovacího procesu z již připojeného kořenového adresáře.

`mkinitcpio` je novou generací **initramfs creation**. Oproti starým skriptům `mkinitrd` a `mkinitramfs` má mnoho výhod:

*   Používá **glibc** a **busybox** jako základ pro ranný uživatelský prostor
*   Umí použít **udev** pro detekci hardware za běhu, takže není potřeba načítat hromady modulů zbytečně
*   Hook-based skripty jsou snadno rozšiřitelné vlastními hooky, které je možné snadno vložit do balíčků bez potřeby upravovat samotný mkinitcpio.
*   Podporuje **lvm2**, **dm-crypt** pro starší šifrování svazků i pro luks, **raid**, **swsusp** a **suspend2**, bootování z **usb mass storage** zařízení a další
*   Mnoho funkcí může být nastaveno z příkazové řádky jádra bez nutnosti generovat nový obraz
*   **mkinitcpio** skript umožňuje vkládat obraz přímo do jádra
*   Díky své flexibilitě není nutné v mnoha případech rekompilovat jádro

Pokud používáte RAID nebo LVM pro kořenový svazek, je nutné nakonfigurovat příslušné HOOKS. Více informací v článcích o [RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") a [/etc/mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio"). Pokud používáte neamerické rozložení klávesnice, přidejte "`keymap`", aby se během bootu mohlo načíst vaše rozložení. Přidejte "`usbinput`", pokud používáte USB klávesnici. Nezapomeňte přidat "`usb`", pokud instalujete Archa na externí disk, flash nebo SD kartu připojenou přes USB:

```
HOOKS="base udev autodetect pata scsi sata usb filesystems keymap usbinput"

```

(Pokud bootování selže a systém vás požádá o heslo pro roota, nebudete ho jinak moci zadat)

Pokud potřebujete podporu pro bootování z USB, FireWire či PCMCIA zařízení, NFS úložíště, softwarevého RAID pole, LVM2 svazku, šifrovaného oddílu nebo podporu pro DSDT, nastavte příslušně HOOKS.

#### /etc/modprobe.d/modprobe.conf

Tento soubor slouží k nastavení speciálních voleb pro jaderné moduly. V této fázi není zpravidla úprava nutná.

#### /etc/resolv.conf

**Note:** Pokud používáte DHCP, můžete tuto část v klidu přeskočit, protože soubor bude vytvořen a odstraněn automaticky DHCP démonem. Toto chování je možné změnit, viz stránky[Network](/index.php/Network#For_DHCP_IP "Network") a [Resolv.conf](/index.php/Resolv.conf "Resolv.conf").

_resolver_ je sada metod ve standardní knihovně C, které umožňují přístup k DNS (Domain Name System). Jednou z hlavních funkcí DNS je překládat doménová jména (např. www.archlinux.org) na IP adresy (66.211.214.131). Konfigurační soubor resolveru /etc/resolv.conf obsahuje informace, které resolver čte, když jej proces poprvé zavolá. Záznamy v tomto souboru jsou mj. adresy serverů, kterých resolver ptá na překlad.

Pokud používáte statickou IP adresu, nastavte v /etc/resolv.conf své DNS servery (nameserver <ip-address>). Můžete vložit libovolný počet záznamů.

Příklad s použitím OpenDNS:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

Pokud používáte router, pravděpodobně budete chtít nastavit jako svůj DNS server právě ten. Příklad:

```
nameserver 192.168.1.1

```

Pokud používáte **DHCP**, můžete také nastavit svůj DHCP server v routeru, nebo povolit automatické získávání od ISP, pokud to váš ISP podporuje.

#### /etc/hosts

Tento soubor spojuje IP adresy s hostnamy a aliasy, jedna řádka na každou adresu. Pro každého hosta by měla být jedna řádka s následující informací:

```
<IP-address> <hostname> [aliasy...]

```

Přidejte svůj _hostname_, ten který jste nastavili v /etc/rc.conf, jako alias, tak, aby záznam vypadal následovně:

```
127.0.0.1   localhost.localdomain   localhost _**vase_hostname**_

```

**Warning:** _Tento formát, **včetně 'localhost' a vašeho hostname** je požadován kvůli kompatibilitě s programy. Pokud jste tedy pojmenovali svůj počítač Arch, bude záznam vypadat:_

```
127.0.0.1   localhost.localdomain   localhost arch

```

Chyby v těchto záznamech mohou vést ke zpomalení sítě nebo nefunkčnosti některých programů. Je to častá chyba začátečníků.

**Note:** Současná verze instalátoru automaticky vloží vaše hostname do tohoto souboru, jakmile upravíte `/etc/rc.conf`. Pokud se tak z nějakého důvodu nestalo, přidejte záznam podle uvedených instrukcí ručně.

Pokud používáte statickou IP, přidejte další řádku se syntaxí: <staticka-IP> <hostname.domainname.org> <hostname>, tedy například:

```
192.168.1.100 _**vase_hostname**_.domain.org  _**vase_hostname**_

```

**Tip:** Pro větší pohodlí si také můžete přidat aliasy pro vaši síť nebo web:

```
64.233.169.103   www.google.com   g
192.168.1.90   media
192.168.1.88   data

```

Ukázka výše vám umožňují otevřít google jednoduše zadáním 'g' jako adresy, a přistupovat k médiovému a data serveru pomocí jmén bez nutnosti pamatovat si a psát jejich IP adresy..

#### /etc/locale.gen

Příkaz `/usr/sbin/locale-gen` čte nastavení z **/etc/locale.gen** a generuje podle toho locales. Ty jsou použity například **glibc** a jinými přeložitelnými programy, aby s vámi komunikovali v preferovaném jazyce, podporovali vaši abecedu, řazení atd.

Standardně je soubor `/etc/locale.gen` prázdný, jen se zakomentovanou dokumentací. `locale-gen` se spouští pouze při aktualizaci glibc, aby vygeneroval nové locales.

Vyberte locales, které potřebujete (odstraňte "#"):

```
en_US ISO-8859-1
en_US.UTF-8
cs_CZ.UTF-8
cs_CZ ISO-8859-2

```

Instalátor nyní spustí locale-gen skript, který vygeneruje locales, které jste zvolili. Locales můžete kdykoliv změnit editací toho souboru a následným spuštěním programu 'locale-gen' jako root.

**Note:** Pokud si nevyberete žádné locales, budete se v systému často setkévat s chybou "The current locale is invalid...". Nejde o nic kritického, systém použije výchozí hodnoty, ale budete toho mít plné logy. Toto je asi nejčastější chyba u nováčků.

#### Pacman-Mirror

Vyberte zrcadlo, které má správce balíčků **`pacman`** používat. Pamatujte, že ftp.archlinux.org je zpomalené na 50KB/s. V čechách můžete použít například mirror na VPSFree:

```
Server = [http://mirrors.vpsfree.cz/archlinux/$repo/os/$arch](http://mirrors.vpsfree.cz/archlinux/$repo/os/$arch)

```

#### Root password (heslo roota)

Nakonec nastavte heslo pro uživatele root. Zvolte heslo, které nezapomenete, protože bez roota se heslo roota mění těžko. Vraťte se do hlavního menu a pokračujte instalací zavaděče.

#### Done (Hotovo)

Když vyberete "Done", systém znovu sestaví obraz jádra a vrátí vás zpátky do menu. Tato operace může chvíli trvat.

## Install and configure a bootloader

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

## Konfigurace základního systému

Nyní Vám ukážeme několik základních postupů. Přihlašte se jako root.

### Konfigurace pacman

Upravte `/etc/pacman.conf`

```
nano -w /etc/pacman.conf

```

a odstraňte '#' před řádkou "Include = /etc/pacman.d/community"- pro přidání dalšího zdroje balíčků, které mohou nabídnout mnoho užitečných aplikací.Nyní upravte `/etc/pacman.d/community` a zvolte mirrory, které jsou umístěné blízko Vás (pokud používáte nano, Ctrl+A označuje oblast, šipka dolů označuje řádky, Ctrl+K ořízne označenou oblast a Ctrl+U vloží). Opakujte to pro všechny soubory v `/etc/pacman.d/`.

### Konfigurace sítě

Obsáhlejší instrukce pro konfigurace sítě lze nalézt [here](/index.php/Network "Network").

#### Pevná LAN

Pokud vše vyšlo dobře, měli by jste mít funkční síť. Zkuste `ping www.google.cz` pro ověření. Pokud se objeví "unknown host" error, Vaše síť není správně nakonfigurována. Zkuste : `ifconfig` měli byste vidět záznam pro `eth0`. Můžete nastavit novou statickou ip s `ifconfig eth0 <ip address> netmask <netmask> up` a defaultní bránu `route add default gw <ip address of the gateway>`. Zkontrolujte, zda `/etc/resolv.conf` obsahuje dns server, pokud ne zapište ji tam. Zkuste Vaši síť znova s `ping www.google.cz`. Pokud vše funguje, upravte `/etc/rc.conf` jak je popsáno v sekci 2.6 (statická ip). Pokud máte dhcp server/router, zkuste `dhcpcd eth0` Pokud vše funguje, upravte `/etc/rc.conf` jak je popsáno v sekci 2.6 (dynamická ip).

#### Bezdrátová Lan

[Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") (TODO) Simplify and generalize it, link only for more advanced stuff

#### Analogový Modem

K použití Hayes-compatible, externího analogového modemu potřebujete minimálně nainstalovat`ppp` balíček. Upravte soubor `/etc/ppp/options` podle svých potřeb pomocí `man pppd`. Budete potřebovat definovat chat skript na vyplnění uživatelského jména a hesla pro ISP po sestavení prvotního spojení. Manuálové stránky pro ppp a chat mají dostatečné příklady pro uspokojivé vytvoření spojení.S udev sériový port je většinou `/dev/tts/0 a /dev/tts/1`.

Místo zápasu s pppd, můžete opt nainstalovat `wvdial` nebo podobný nástroj k snadnému nastavení. Pokud používáte WinModem, který je v základu PCI karta pracující jako analogový modem, měli byste použít informace na LinModem homepage.

#### ISDN

Nastavení ISDN ve 3 krocích:

1.  Instalace a konfigurace hardware
2.  Instalace a konfigurace nástrojů ISDN
3.  Přidání nastavení pro Vašeho ISP

Současné Arch kernely obsahují nezbytné ISND moduly, což znamená, že nemusíte rekompilovat kernel, jedině že byste používali starý ISDN hardware. Po instalaci ISDN karty do vašeho PC nebo připojení ISDN-Box do USB, můžete zkusit načíst moduly s modprobe. Skoro všechny pasivní ISDN PCI karty zvládnou "hisax" modul, který potřebuje dva parametry; typ a protokol. Musíte nastavit protokol na '1', pokud Vaše země používá 1TR6 standart, '2' pokud používáte EuroISDN (EDSS1), '3' pokud jste připojeni k tzv. pronajmuté lince bez D-kanálu a '4'pro US NI1.

Detaily všech nastavení a jak je nastavit jsou v dokumentaci o kernelu, víc specifikací je v isnd podadresáři nebo jsou dostupné online. Typ parametru záleží na kartě; list všech možných typů je k nalezení v README.HiSax dokumentaci. Vyberte si svou kartu a načtěte modul s patřičnými volbami jako toto: `modprobe hisax type=18 protocol=2`

To načte hisax modul pro ELSA Quickstep 1000PCI - použivaná v Německu na EDSS1 protokol. Najdete užitečný výstup v `/var/log/everything.log`, kde byste měli vidět vaší kartu připravenou k práci. Vemte v potaz, že možná budete potřebovat načíst další usb moduly pro práci s externím USB ISDN adaptérem.

Poté co se potvrdí, že vaše karta pracuje s určitým nastavením, můžete přidat modul do `/etc/modprobe.d/modprobe.conf` (nebo do `/etc/modules.conf` pokud užíváte kernel 2.4.x): `alias ippp0 hisax`

```
options hisax type=18 protocol=2

```

Případně můžete použít toto a přidat hisax do pole MODULY(MODULES) v `rc.conf`. Záleží na Vás, ale tento příklad má výhodu v tom, že modul nebude načten, doku není opravdu potřeba.

Tím by mělo být vše funkční. Nyní potřebujete nějaké základní nástroje pro použití.

Nainstalujte balíček `isdn4k-utils` a přečtěte si manuálové stránky k isdnctrl. Tam najdete popis jak vytvořit konfigurační soubor, který může být spojen s isdnctrl, také tam najdete užitečné příklady nastavení. Nezapoměňte přidat Vaše SPID do Vašeho MSN nastavení oddělené mezerou, pokud používáte US NI1.

Po konfiguraci Vaší ISDN karty s isdnctrl, měli byste být schopni se připojit k zařízení, které jste vyplnili jako `PRHONE_OUT` parametr, ale ještě musíte vyplnit uživatelské jméno a heslo do `/etc/ppp/pap-secrets nebo /etc/ppp/chap-secrets` jako byste konfigurovali normální analogovou PPP linku v závislosti jaký protokol Váš ISP používá pro autentizaci. Pokud si nejste jistí, zapište data do obou souborů.

Pokud vše nastavíte správně, měli byste být schopni sestavit vytáčené spojení s isdnctrl přes ippp0 jako uživatel root. Pokud máte nějaký problém, zkontrolujte nejprve soubory log.

#### DSL (PPPoE)

These instructions are only relevant to you if your PC itself is supposed to manage the connection to your ISP. You do not need to do anything but define a correct default gateway if you are using a separate router of some sort to do the grunt work.

Before you can use your DSL online connection, you will have to physically install the network card that is supposed to be connected to the DSL-Modem into your computer. After adding your newly installed network card to the modules.conf/modprobe.conf or the MODULES array, you should install the rp-pppoe package and run the adsl-setup script to configure your connection. After you have entered all the data, you can connect and disconnect your line with

```
/etc/rc.d/adsl start

```

and

```
/etc/rc.d/adsl stop

```

respectively. The setup usually is rather easy and straightforward, but feel free to read the manpages for hints. If you want to automatically dial in on bootup, add adsl to your DAEMONS array.

## Update systému

Update, synchronizaci a **upgrade** celého systému provedete jednoduchým příkazem:

```
pacman -Syu

```

pacman stáhne nejnovější informace o dostupných balíčcích a provede všechny dostupné aktualizace. (Je možné, že budete dotázáni na update samotného správce balíčků pacman. Pokud se tak stane, odpovězte Ano, a po jeho aktualizaci proveďte příkaz pacman -Syu znovu.) V případě, že byl aktualizován kernel, proveďte restart.

**Note:** _**Občas se stane, že je po aktualizaci potřeba ruční zásah do konfigurace; sledujte proto během upgrade výpis na obrazovce, kde se o případných nutných zásazích dočtete. Pokud máte například pomalé připojení a byl by pro vás problém hlídat, kdy začne probíhat samotný upgrade, můžete použít příkaz pacman -Syuw, který dostupné balíčky pouze stáhne, a samotnou instalaci provést později příkazem pacman -Su.**_

##### Krása modelu Arch rolling release

Myslete na to, že Arch je **rolling release** distribuce. To znamená, že neexistuje důvod pro reinstalaci, nebo nějaké šílené laborování při aktualizaci na nejnovější verzi. Úplně jednoduše pravidelným používáním příkazu **pacman -Syu** udržujete váš systém zcela aktuální.

##### Seznamte se s pacmanem

Pacman je ten nejlepší kamarád uživatelů Arch Linuxu. Doporučujeme vám, abyste se s ním dobře seznámili a naučili se ho používat. Zkuste příkaz:

```
man pacman

```

Ve volném čase si projděte také wiki sekci [Pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)").

### Přidání uživatele a nastavení skupin

Pro každodenní práci byste neměli používat účet root. Nejenže je to nepraktické, hlavně je to nebezpečné. Root se používá pro administrátorské úkony. Namísto toho vytvořte běžné uživatelské účty příkazem:

```
adduser

```

Ačkoliv lze bezpečně použít většinu výchozích voleb, asi budete chtít pro využití plnohodnotného desktopu přidat uživatele do doplňujících skupin, jako storage, audio, video, optical a wheel.

Skupiny a příslušní uživatelé jsou definováni v /etc/group.

Zahrnují tyto možnosti:

*   **audio** - používání zvukové karty
*   **wheel** - umožní použít příkaz sudo
*   **storage** - správa úložných zařízení
*   **video** - video a 3D akcelerace
*   **optical** - přístup k optickým zařízením
*   **floppy** - přístup k disketovým jednotkám
*   **lp** - správa tiskových úloh

Více se o skupinách dočtete v sekci [Groups](/index.php/Groups "Groups").

Pro více informací se podívejte také na manuálové stránky usermod a gpasswd.

## Instalace a konfigurace Hardware

### Konfigurace zvukové karty

Vaše zvuková karta by měla fungovat, ale pokud nic neslyšíte, je možné, že je zvuk ztišen. Nainstalujte balíček alsa-utils `pacman -S alsa-utils` a použíte `alsamixer` k nastavení. Zvyšte hlasitost alespoň u master a pcm kanálu (zmáčkněte klávesu M). Ukončete program pomocí klávesy ESC a uložte nastavení pomocí: `alsactl store` Přidejte alsa daemon do `/etc/rc.conf` k automatickému uložení mixeru při startupu.

### Configuring CPU frequency scaling

Moderní procesory umožňují snížit jejich frekvenci a napájení za účelem snížení vyzařování tepla a spotřeby energie. Většinou to vede k tiššímu systému, tudíž i desktopový systém z toho bude těžit. Nainstalujte `cpufrequtils`: `pacman -S cpufrequtils` a přidejte cpufreg do sekce daemons v `/etc/rc.conf`. Upravte konfigurační soubor `/etc/conf.d/cpufreq` a změňte: `governor="conservative"` což dynamicky mění frekvenci cpu, pokud je potřeba (to je bezpečná varianta také na desktopových systémech). Upravte `min_freq` a `max_freq` podle svých představ. Přidejte frequency scalling do `/etc/rc.conf` řádky modules (příklad: speedstep_centrino pro Pentium M processors or powernow-k8 pro Athlon 64). Načtěte moduly: `modprobe <modulname> and start cpufreq with`

```
/etc/rc.d/cpufreq start

```

### Additional tweaks for laptops

Kvůli některým speciálním funkcím musíte zapnout podporu ACPI (příklad: uspání, speciální klávesy...). Nainstalujte acpid: `pacman -S acpid` add it to the daemons in `/etc/rc.conf` (acpid). Spusťte

```
`/etc/rc.d/acpid start`

```

Další dobrou volbou je nainstalování powersave a přidání do sekce daemons `/etc/rc.conf` (powersaved). Powersave obsahuje několik oprav pro suspendování do RAM a standby a také úspora baterie. Spusťte: `/etc/rc.d/powersaved start`

Více informací o Arch Linuxu na různých laptopech můžete nalézt

## Instalace a konfigurace Xorg

Nyní k instalaci Xorg použití pacman. `pacman -S xorg` Nyní ja nainstalován základní balíček pro běh X serveru. Měli byste přidat ovladač Vaší grafické karty (příp. `xf86-video-<name>`). K získání seznamu video ovladačů: `pacman -Ss xf86-video | less` Pokud neznáte jaký typ grafické karty máte, zadejte: `lspci | grep VGA` Nyní spusťte `Xorg -configure` k vytvoření základní konfigurace X serveru. Pokud chcete otestovat konfiguraci, nainstalujte xterm a twm: `pacman -S xterm xorg-twm` přesuňte xorg.conf.new (`mv /root/xorg.conf.new /etc/X11/xorg.conf`) a spusťte `startx`. Ukončete X server pomocí Ctrl+Alt+Backspace. Možná budete potřebovat další úpravy v xorg.conf.

Advanced instructions for Xorg configuration can be found [here](/index.php/Xorg "Xorg")

### Úprava rozložení klávesnice

Můžete změnit rozložení klávesnice. Upravte `/etc/X11/xorg.conf` a přidejte tyto řádky do Input Section (keyboard0):

```
       Option          "XkbLayout"     "cs"
       Option          "XkbVariant"    "nodeadkeys"

```

### Myš

Pokud chcete mít funkční - funkce kolečka - přidejte do sekce Input Section(mouse0):

```
       Option      "ZAxisMapping" "4 5 6 7"

```

### Použití properitních grafických ovladačů(Nvidia, Ati)

#### Grafické karty Nvidia

Nainstalujte ovladač nvidia:

```
pacman -S nvidia

```

Upravte nastavení v `/etc/X11/xorg.conf` sekci Device Section - změňte sekci Driver z `nv` na `nvidia`. Vhodné je také přidat novou sekci:

```
Section "DRI"
       Mode    0666
EndSection

```

Některé užitečné nastavení jsou níže(pozor ne všechny volby nemusí fungovat na vašem systému):

```
       Option          "RenderAccel" "true"
       Option          "NoLogo" "true"
       Option          "AGPFastWrite" "true"
       Option          "EnablePageFlip" "true"

```

Měli byste přidat toto do sekce modulů:

```
Load "glx"

```

Spusťte `modprobe nvidia` k načtení ovladačů a otestujte konfiguraci spuštěním`startx`

Advanced instructions for Nvidia configuration can be found [here](/index.php/NVIDIA "NVIDIA")

#### ATI Graphic Cards

ATI owners have two options for drivers. If you unsure which driver to use try the open source one first. The open source driver will suite most needs along with generally being less problematic.

Install the proprietary ATI Driver with

```
pacman -S ati-fglrx

```

Use the aticonfig tool to modify the xorg.conf. Note: The proprietary driver does not support [AIGLX](/index.php/AIGLX "AIGLX"). To use [Compiz](/index.php/Compiz "Compiz") or [Beryl](/index.php/Beryl "Beryl") with this driver you would need to use XGL.

Install the open source ATI Driver with

```
pacman -S xf86-video-ati

```

Currently the open source driver is not on par with the performance of the proprietary one. It also lacks TV-out, dual-link DVI support, and possibly other features. On the other hand it supports Aiglx and has better dual-head support.

Advanced instructions for ATI configuration can be found [here](/index.php/ATI "ATI").

## Instalace a konfigurace desktopového prostředí

Zatímco **X** Window System poskytuje pouze základní lešení pro tvorbu _grafického uživatelského rozhraní_ (GUI), **desktopové prostředí** (DE) pracuje nad a ve spojení s **X**, aby poskytlo GUI, které je zcela funkční a dynamické. DE typicky poskytuje okenního správce, ikony, applety, okna, panely nástrojů, složky, tapety, balík aplikací a věci jako drag and drop. Konkrétní funkcionalita a návrh každého DE jediněčně ovlivňují celé prostředí a dojem z něj. Tím pádem je volba DE velmi subjektivní a osobní rozhodnutí. Zvolte si nejlepší prostředí pro _vaše_ potřeby.

*   Pokud chcete něco plnohodnotného a podobného Windows a Mac OSX, je dobrá volba **[KDE](#KDE)**
*   Pokud chcete něco trochu více minimalistického, co by více následovalo princip K.I.S.S. (Udržuj to jednoduché a hloupé), je dobrá volba **[GNOME](#GNOME)**
*   **[Xfce](#Xfce)** je obecně vnímáno jako podobné GNOME ale lehčí a méně náročné na systémové zdroje, nicméně je stále vzhledově příjemné a poskytuje velmi kompletní prostředí.
*   **[LXDE](#LXDE)** je minimalistické DE založené na správci oken Openbox. Poskytuje většinu věcí, které jsou potřeba pro moderní desktop, přičemž stále zachovává relativně nízké využití systémových zdrojů. LXDE je dobrá volba pro ty, kteří chtějí rychle nastavit předkonfigurovaný systém s Openbox.

V případě, že chcete nějaké lehčí, méně náročné GUI pro ruční konfiguraci, můžete si zvolit instalaci pouze **okenního správce** (WM). Ten ve spojení s X Window ovládá umístění a vzhled aplikačních oken, ale jeho součástí implicitně **nejsou** věci jako panely, applety, ikony, aplikace atp.

*   Mezi odlehčené plovoucí (okna volně plovou na sobě) WM patří: [**Openbox**](#Openbox), [**Fluxbox**](#Fluxbox), [**fvwm2**](#fvwm2), **Windowmaker, Pekwm,** a **TWM**.
*   Pokud potřebujete něco zcela odlišeného, zkuste **Awesome, ion, wmii, dwm,** nebo **xmonad**.

### Nainstalujte fonty

Ještě před instalací desktopového prostředí/okenního správce byste si mohli přát nainstalovat nějaké vzhledově uspokojující true type fonty. Dobré všestranně použitelné sady fontů jsou Dejavu a bitstream-vera. Také byste mohli chtít sadu fontů Microsoftu, ty jsou obzvlášť populární na webových stránkách.

Instalujte pomocí:

```
# pacman -S ttf-ms-fonts ttf-dejavu ttf-bitstream-vera

```

### ~/.xinitrc (znovu)

Jako **jiný uživatel než root** otevřete soubor /home/uživatelské-jméno/.xinitrc a určete v něm desktopové prostředí, které chcete používat. Toto vám v budoucnu umožní pro spuštění DE/WM vaší volby používat v shellu příkazy **startx/xinit**:

```
$ nano ~/.xinitrc

```

Odkomentujte nebo přidejte '**exec** ..' řádek pro příslušné desktopové prostředí/okenního správce. Některé příklady jsou níže:

Pro desktopové prostředí Xfce4:

```
 exec startxfce4 

```

Pro desktopové prostředí KDE:

```
 exec startkde

```

Příkaz **startkde** nebo **startxfce4** spustí desktopové prostředí KDE nebo Xfce4\. Tento příkaz neskončí svoji činnost, dokud se neodhlásíte z DE. Normálně by tedy shell čekal, než se KDE ukončí, a pak by spustil další příkazy. Předpona "exec" u tohoto příkazu sděluje shellu, že tento příkaz je poslední, takže shell na provedení následujících příkazů nemusí čekat.

Pamatujte si, že ve svém ~/.xinitrc máte mít odkomentovaný pouze jednu řádek s **exec**.

Pokračujte níže instalací DE/WM dle vaší volby.

*   [**GNOME**](#GNOME)
*   [**KDE**](#KDE)
*   [**Xfce**](#Xfce)
*   [**LXDE**](#LXDE)
*   [**Openbox**](#Openbox)
*   [**Fluxbox**](#Fluxbox)
*   [**fvwm2**](#fvwm2)

### GNOME

#### O GNOME

**G**NU **N**etwork **O**bject **M**odel **E**nvironment. Projekt GNOME poskytuje dvě věci: desktopové prostředí GNOME, což je intuitivní a atraktivní desktop pro koncové uživatele, a vývojářskou platformu GNOME, což je rozsáhlý framework pro budování aplikací integrovaných do zbytku desktopu.

#### Instalace

Základní prostředí GNOME nainstalujte pomocí:

```
# pacman -S gnome

```

Můžete nainstalovat i další dodatečné balíky:

```
# pacman -S gnome-extra

```

Je bezpečné zvolit všechny balíky z balíku extra.

#### Užiteční daemoni pro GNOME

Vzpomeňte si, že daemon je program, který běží na pozadí, kde čeká na události a nabízí služby. Daemon **hal** mimo jiné věci automatizuje připojování disků, optických mechanik a USB jednotek. Daemon **fam** umožňuje znázornění změn souborů v GUI v reálném čase, čímž umožňuje okamžitý přístup k nedávno nainstalovaným programům nebo změnám v souborovém systému. Jak **hal** tak **fam** činí uživateli GNOME život jednodušší. Balíčky hal a fam se instalují při instalaci GNOME, ale aby mohly být užitečné, musí být vyvolány.

Můžete nainstalovat grafického správce přihlášení. Pro GNOME je dobrou volbou daemon **gdm**.

Jako root:

```
# pacman -S gdm

```

Také budete téměř jistě chtít daemony **hal** a **fam**.

Spusťte hal a fam:

```
# /etc/rc.d/hal start

```

```
# /etc/rc.d/fam start

```

Přidejte je do sekce DAEMONS ve vašem souboru /etc/rc.conf, aby byli vyvoláni při startu:

```
# nano /etc/rc.conf

```

```
DAEMONS=(syslog-ng network crond alsa **hal fam gdm**)

```

(Pokud upřednostňujete přihlášení do konzole a ruční spouštení X, vynechte gdm.)

Jako běžný uživatel spusťte X:

```
$ startx

```

nebo

```
$ xinit

```

Pokud soubor ~/.xinitrc není nakonfigurovaný pro GNOME, můžete ho vždy spustit pomocí příkazu **xinit** s cestou ke GNOME jako parametr:

```
$ xinit /usr/bin/gnome-session

```

Pokročilé instrukce pro instalaci a konfiguraci GNOME můžete nalézt v samostatném [článku o GNOME](/index.php/GNOME_(%C4%8Cesky) "GNOME (Česky)").

Gratulujeme! Vítejte v desktopovém prostředí GNOME na svém novém systému Arch Linux! Nyní byste si mohli chtít prohlédnout zbytek informací níže. Také by vás mohl zajímat wiki článek [Poinstalační tipy](/index.php/Poinstala%C4%8Dn%C3%AD_tipy "Poinstalační tipy").

#### Vzhled

Ve výchozím nastavení GNOME nepřichází s mnoha tématy a ikonami. Mohli byste chtít nějaký další atraktivní artwork pro GNOME:

Pěkný GTK engine pro témata (součástí balíčku jsou i některá témata, která ho využívají) je Murrine. Nainstalujete ho pomocí:

```
# pacman -S gtk-engine-murrine

```

Jakmile je nainstalovaný, vyberte ho v _Systém -> Volby -> Vzhled -> záložka Téma_.

Repozitáře Arch Linuxu obsahují i další témata a enginy. Nainstalujte následující a podívejte se na ně sami:

```
# pacman -S gtk-engines gtk2-themes-collection gtk-aurora-engine gtk-candido-engine gtk-rezlooks-engine

```

Mnohem více témat, ikon a tapet můžete najít na [Gnome Look](http://www.gnome-look.org).

### KDE

#### O KDE

**K** **D**esktop **E**nvironment. KDE je mocné grafické desktopové prostředí pro pracovní stanice s GNU/Linux a `UNIX`em. Kombinuje jednoduchost použití, moderní funkce a výjimečný grafický návrh s technologickou převahou operačních systémů založených na UNIXu.

#### Instalace

Zvolte si jednu z následujících možností a pokračujte níže s **[Užitečnými daemony pro KDE](#U.C5.BEite.C4.8Dn.C3.AD_daemoni_pro_KDE)**:

1\. Balík **kde** je kompletní vanilkové KDE 4.1 a spočívá v repozitáři [extra].

Nejdříve nainstalujte:

```
# pacman -S zlib shared-mime-info

```

KDE nainstalujte pomocí:

```
# pacman -S kde

```

2\. **KDEmod** je komunitou řízený systém specifický pro Arch Linux, jenž je navrhován pro modularitu a nabízí i volbu mezi KDE 3.5.10 a 4.x.x. Po přidání příslušného repozitáře do /etc/pacman.conf lze KDEmod nainstalovat pacmanem. Stránky projektu včetně kompletních instalačních instrukcí se nacházejí na [http://kdemod.ath.cx/](http://kdemod.ath.cx/).

**Note:** Závislost na celém kdemod3/kdemod-legacy byla odstraněna z oficiálních repozitářů Arch Linuxu. KDEmod není součástí zmíněných repozitářů a žádné standardní programy v Arch Linuxu tento balík nevyužívaly. Pokud chcete nainstalovat kdemod3-complete bez potenciálně problematického obcházení pomocí "vynucených instalací", měli byste nainstalovat balíček libopensync ručně z AUR (Viz [AUR User Guidelines (Česky)#Jak_na_bal.C3.AD.C4.8Dek_z_UNSUPPORTED](/index.php/AUR_User_Guidelines_(%C4%8Cesky)#Jak_na_bal.C3.AD.C4.8Dek_z_UNSUPPORTED "AUR User Guidelines (Česky)")) nebo pomocí programu yaourt (Viz [Yaourt#Easy_Install](/index.php/Yaourt#Easy_Install "Yaourt"), poté yaourt -S libopensync), dokud balíček nebude v repozitářích KDEmod3\. Pokud budete mít problémy, zkuste libopensync-stable (nebo libopensync-unstable pokud jste zoufalí). Jako další možnost by tento problém měla obejít instalace kdemod3-base namísto kdemod3-complete (skupina kdepim, jíž patří tento problém v závislostech, není ve skupině base). Poté můžete jít směrem _vzhůru_ k těm balíčkům, které chcete, namísto jejich odstraňování.

#### Užiteční daemoni pro KDE

KDE bude vyžadovat dameony **hal** (**H**ardware **A**bstraction **L**ayer) a **fam** (**F**ile **A**lteration **M**onitor). Daemon **kdm** (**K** **D**isplay **M**anager) poskytuje **grafické přihlašování**, pokud je vyžadováno.

Vzpomeňte si, že daemon je program, který běží na pozadí, kde čeká na události a nabízí služby. Daemon **hal** mimo jiné věci automatizuje připojování disků, optických mechanik a USB jednotek. Daemon **fam** umožňuje znázornění změn souborů v GUI v reálném čase, čímž umožňuje okamžitý přístup k nedávno nainstalovaným programům nebo změnám v souborovém systému. Jak **hal** tak **fam** činí uživateli KDE život jednodušší. Balíčky hal, fam a kdm se instalují při instalaci KDE, ale aby mohly být užitečné, musí být vyvolány.

* * *

Spusťte hal a fam:

```
# /etc/rc.d/hal start

```

```
# /etc/rc.d/fam start

```

**Note:** Daemon hal automaticky spustí i daemona dbus, na němž závisí.

Otevřete soubor /etc/rc.conf:

```
# nano /etc/rc.conf

```

Do pole DAEMONS přidejte **hal** a **fam**, aby byli vyvoláni po spuštění počítače. Pokud upřednostňujete grafické přihlašování, přidejte také **kdm**:

```
DAEMONS=(syslog-ng network crond alsa **hal fam kdm**)

```

**Note:** Pokud jste namísto normálního KDE nainstalovali KDEmod3, použijte kdm3 namísto kdm.

*   Tato metoda spustí systém v runlevelu 3 (výchozí víceuživatelský mód v /etc/inittab) a poté spustí KDM jako daemona.
*   Někteří uživatelé upřednostňují spouštění správce displeje (jímž je KDM) pomocí /etc/inittab a spuštěním systému v runlevelu 5 (grafický víceuživatelský mód). Pro více informací viz [Přidání správce přihlášení (KDM, GDM nebo XDM)](/index.php/Display_Manager_(%C4%8Cesky) "Display Manager (Česky)").
*   Pokud se chcete přihlašovat **do konzole** v runlevelu 3 a spouštět X ručně, vynechte kdm nebo ho zakomentujte výkřičníkem (!).

Teď zkuste jako běžný uživatel spustit X Server:

```
$ startx

```

nebo

```
$ xinit

```

Pokročilé instrukce pro instalaci a konfiguraci KDE můžete nalézt v samostatném [článku o KDE](/index.php/KDE_(%C4%8Cesky) "KDE (Česky)").

Gratulujeme! Vítejte v desktopovém prostředí KDE na svém novém systému Arch Linux! Nyní byste si mohli chtít prohlédnout zbytek informací níže. Také by vás mohl zajímat wiki článek [Poinstalační tipy](/index.php/Poinstala%C4%8Dn%C3%AD_tipy "Poinstalační tipy").

### Xfce

#### O Xfce

Prostředí pro **X** bez cholesterolu. Xfce je, stejně jako GNOME nebo KDE, desktopové prostředí, ale má za cíl být při zachování vzhledové líbivosti a jednoduchosti použití rychlé a odlehčené. Obsahuje balík aplikací jako správce oken, správce souborů, panel, aplikace kořenového okna atd. Xfce je napsáno s použitím toolkitu GTK2 (stejně jako GNOME) a obsahuje vlastní vývojářské prostředí podobné jiným velkým DE. Na rozdíl od GNOME nebo KDE, Xfce je odlehčené a navržené spíše kolem CDE než kolem Windows nebo Mac. Má mnohem pomalejší vývojový cyklus, ale je velmi stabilní a rychlé. Xfce je výborné pro starší hardware a bude skvěle pracovat i na novějších strojích.

#### Instalace

Nainstalujte Xfce:

```
# pacman -S xfce4 

```

Můžete si také přát nainstalovat témata a dodatečné aplikace:

```
# pacman -S xfce4-goodies gtk2-themes-collection

```

**Note:** Součástí skupiny **xfce4-goodies** je **xfce4-xfapplet-plugin** (plugin který umožňuje použití GNOME appletů v panelu Xfce4) a ten závisí na balíku **gnome-panel**, který zas závisí na **gnome-desktop**. Toto byste před instalací měli brát v úvahu, protože to znamená značný počet dalších závislostí.

Pokud si po přihlášení přejete obdivovat "Tipy a triky", nainstalujte balíček **fortune-mod**:

```
# pacman -S fortune-mod

```

#### Užiteční daemoni

Vzpomeňte si, že daemon je program, který běží na pozadí, kde čeká na události a nabízí služby. Daemon **hal** mimo jiné věci automatizuje připojování disků, optických mechanik a USB jednotek. Daemon **fam** umožňuje znázornění změn souborů v GUI v reálném čase, čímž umožňuje okamžitý přístup k nedávno nainstalovaným programům nebo změnám v souborovém systému. Balíčky hal a fam se instalují při instalaci Xfce, ale aby mohly být užitečné, musí být vyvolány.

Spusťte hal a fam:

```
# /etc/rc.d/hal start

```

```
# /etc/rc.d/fam start

```

**Note:** Daemon hal automaticky spustí i daemona dbus, na němž závisí.

Otevřete soubor /etc/rc.conf:

```
# nano /etc/rc.conf

```

Do pole DAEMONS přidejte **hal** a **fam**, aby byli vyvoláni po spuštení počítače.

Pokročilé instrukce pro instalaci a konfiguraci Xfce můžete nalézt v samostatném [článku o Xfce](/index.php/Xfce_(%C4%8Cesky) "Xfce (Česky)").

Pokud chcete nainstalovat správce přihlášení, vizte [Přidání správce přihlášení (KDM, GDM nebo XDM)](/index.php/Display_Manager_(%C4%8Cesky) "Display Manager (Česky)"). V opačném případě se můžete přihlásit v konzoli a spustit:

```
 $ startxfce4

```

Gratulujeme! Vítejte v desktopovém prostředí Xfce na svém novém systému Arch Linux! Nyní byste si mohli chtít prohlédnout zbytek informací níže. Také by vás mohl zajímat wiki článek [Poinstalační tipy](/index.php/Poinstala%C4%8Dn%C3%AD_tipy "Poinstalační tipy").

### LXDE

#### O LXDE

LXDE (_L_ightweight _X_11 _D_esktop _E_nvironment) je nový projekt zaměřený na poskytnutí moderního desktopového prostředí, které má za cíl být odlehčené, rychlé, intuitivní a funkční při zachování nízkého využití systémových zdrojů. LXDE je od ostatních desktopových prostředí odlišné, jelikož každá část LXDE je oddělená a nezávislá aplikace a může být lehce nahrazena jinými programy. Tento modulární návrh eliminuje všechny nepotřebné závislosti a poskytuje větší flexibilitu. Detaily a snímky obrazovky jsou dostupné na [http://lxde.org/](http://lxde.org/)

LXDE poskytuje:

1.  Správce oken OpenBox
2.  Správce souborů PCManFM
3.  Systémový panel LXpanel
4.  Správce sezení LXSession
5.  Přepínač GTK+ témat LXAppearance
6.  Prohlížeč obrázků GPicView
7.  Jednoduchý textový editor Leafpad
8.  XArchiver: Odlehčený a rychlý archivátor souborů založený na GTK+
9.  LXNM (stále ve vývoji): Odlehčený správce sítí pro LXDE podporující bezdrátová spojení

Tyto všestranné nástroje kombinují rychlé nastavení, modularitu a jednoduchost.

Instalujte LXDE pomocí:

```
# pacman -S lxde

```

Přidejte:

```
exec startlxde

```

do svého ~/.xinitrc a spusťte ho pomocí _startx_ nebo _xinit_

Další informace jsou dostupné ve wiki [článku o LXDE](/index.php/LXDE "LXDE").

### *box

#### Fluxbox

Fluxbox © je další okenní správce pro X. Je založený na kódu Blackbox 0.61.1\. Fluxbox vypadá jako Blackbox a pracuje se styly, barvami, umístěním oken a podobnými věcmi naprosto stejně (100% kompatibilita témat a stylů).

Nainstalujte Fluxbox pomocí:

```
# pacman -S fluxbox fluxconf

```

Pokud používáte GDM/KDM, nové sezení pro Fluxbox bude přidáno automaticky. Případně otevřete soubor .xinitrc svého uživatele a přidejte do něj následující:

Více informací je dostupných v samostatném [článku o Fluxboxu](/index.php/FLUXBOX_(%C4%8Cesky) "FLUXBOX (Česky)").

#### Openbox

Openbox je rychlý, odlehčený, rozšiřitelný a standardy splňující okenní správce.

Openbox pracuje s vašimi aplikacemi a činí váš desktop snadněji ovladatelným. Toto je způsobeno tím, že přístup k jeho vývoji byl opačný k tomu, co se zdá být běžné u okenních správců. Openbox byl nejdříve napsán tak, aby splňoval standardy a správně pracoval. Až tehdy, když toho bylo dosaženo, se team přesunul k uživatelskému rozhranní.

Openbox je plně funkční jako samostatné pracovní prostředí, případně může být také použit jako náhrada za výchozího okenního správce v desktopových prostředích GNOME nebo KDE.

Nainstalujte openbox pomocí:

```
# pacman -S openbox

```

Též jsou dostupné přídavné konfigurační nástroje, pokud jsou žádoucí:

```
# pacman -S obconf obmenu

```

Jakmile je openbox nainstalován, obdržíte zprávu, že máte zkopírovat soubory menu.xml a rc.xml do ~/.config/openbox ve svém domovském adresáři:

```
# su - _vaše-uživatelské-jméno_
$ mkdir -p ~/.config/openbox/
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox/
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox/

```

**rc.xml** je hlavní konfigurační soubor pro OpenBox. Může být upravován ručně (nebo můžete použít OBconf). **menu.xml** konfiguruje menu pravého tlačítka.

Do OpenBoxu se můžete přihlásit skrze grafické přihlášení pomocí KDM/GDM nebo ze shellu pomocí příkazu **startx**. V pozdějším případě budete muset otevřít svůj soubor ~/.xinitrc (jako běžný uživatel) a přidat následující:

```
exec openbox-session

```

Také ze shellu můžete OpenBox spustit pomocí **xinit**:

```
$ xinit /usr/bin/openbox-session

```

*   Openbox může být také použit jako okenní manažer pro GNOME, KDE a Xfce.

Pro KDM už nezbývá nic na práci; u KDM již je openbox v seznamu sezení.

Mezi užitečné odlehčené programy pro OpenBox patří:

*   PyPanel nebo LXpanel, pokud chcete panel
*   feh pokud chcete změnit pozadí
*   ROX pokud chcete jednoduchého správce souborů (mimo jiné poskytuje i jednoduché ikony)
*   PcmanFM – odlehčený ale všestranný správce souborů (též zahrnuje funkci ikon na ploše)
*   iDesk (dostupný v [AUR](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)")) pro ikony na ploše

Více informací je dostupných v samostatném [článku o Obenboxu](/index.php/OpenBox_(%C4%8Cesky) "OpenBox (Česky)").

### fvwm2

FVWM je velmi schopný okenní správce s podporou virtuálních ploch pro systém X Window splňující ICCCM. Vývoj je aktivní a podpora je výtečná.

Nainstalujte fvwm2 pomocí:

```
# pacman -S fvwm 

```

fvwm bude automaticky vypsán v menu sezení KDM/GDM. Případně přidejte do souboru .xinitrc svého uživatele řádek:

```
exec fvwm

```

## Prohlížeč, kodeky, video přehrávač a užitečné aplikace

### Webový prohlížeč

Věčně populární webový prohlížeč Firefox je dostupný skrze pacmana, nicméně nepoužívá své oficiální označení, a tak se program při otevření objevuje pod svým vývojovým názvem _Gran Paradiso_.

Instalujte pomocí:

```
# pacman -S firefox

```

Dále si určitě nainstalujte 'flashplugin', 'mplayer', 'mplayer-plugin', a balíky 'codecs' pro plnohodnotný zážitek z webu:

```
# pacman -S flashplugin mplayer mplayer-plugin codecs

```

_Pro nováčky: Pokud máte x86_64 verzi Arch Linuxu, nepoužívejte u pacmanu volbu `flashplugin` zmíněnou výše nebo obdržíte chybové hlášení. Adobe nyní nabízí 64-bitovou verzi Flash pluginu. Podívejte se prosím na [článek o instalaci Flashe na Arch64](/index.php?title=Instalace_Flashe_na_Arch64_(%C4%8Cesky)&action=edit&redlink=1 "Instalace Flashe na Arch64 (Česky) (page does not exist)")._

*   _Poznámka: Povedlo se mi zprovoznit pluginy pouze symlinkováním všeho z '/usr/lib/mozilla/plugins' do '~/.mozilla/plugins', přesněji tedy spuštením příkazu '`mkdir ~/.mozilla/plugins && ln -s /usr/lib/mozilla/plugins/* ~/.mozilla/plugins`'._

(Balíček codecs obsahuje většinu kodeků, včetně těch pro Win32, Quicktime a Realplayer9 obsah.)

### VLC

VLC Player je všestranný přehrávač multimedií, který zvládá mnoho různých formátů, ať už z disku nebo ze souboru. Poskytuje také možnost přenášet multimédia přes LAN (lokální síť). Instalujte pomocí:

```
# pacman -S vlc

```

Knihovna libdvdcss poskytuje podporu pro dekódování chráněných DVD. Před instalací se ujistěte, že je používání libdvdcss ve vaší zemi legální!

```
# pacman -S libdvdcss

```

### Užitečné aplikace

Pro více aplikací se podívejte na článek [užitečné aplikace](/index.php/Common_Applications_(%C4%8Cesky) "Common Applications (Česky)").

## Další informace

Další informace a podporu můžete nalézt na [domovské stránce](https://www.archlinux.org), [wiki](/index.php/Main_page "Main page"), [fóru](https://bbs.archlinux.org), [IRC kanálu](/index.php/ArchChannel "ArchChannel") nebo [mailing listech](https://www.archlinux.org/mailman/listinfo/).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(Česky)&oldid=411532](https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(Česky)&oldid=411532)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Getting and installing Arch (Česky)](/index.php/Category:Getting_and_installing_Arch_(%C4%8Cesky) "Category:Getting and installing Arch (Česky)")
*   [About Arch (Česky)](/index.php/Category:About_Arch_(%C4%8Cesky) "Category:About Arch (Česky)")