**Tip:** Tato stránka je součástí několikastránkového článku *Beginners' Guide (Česky)*. **[Klikněte zde](/index.php/Beginners%27_guide "Beginners' guide")**, pokud byste raději chtěli číst celý článek vcelku.

Tento článek Vás provede procesem instalace [Arch Linuxu](/index.php/Arch_Linux_(%C4%8Cesky) "Arch Linux (Česky)") pomocí [Arch Install Scripts](https://github.com/falconindy/arch-install-scripts). Před instalací si prosím pročtěte [často kladené otázky](/index.php/FAQ_(%C4%8Cesky) "FAQ (Česky)").

Komunitou spravovaná [ArchWiki](/index.php/Main_page_(%C4%8Cesky) "Main page (Česky)") je primárním zdrojem, na který byste se měli obrátit v případě problémů. [IRC kanál](/index.php/IRC_channel "IRC channel") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) a [fórum](https://bbs.archlinux.org/) jsou také výbornými zdroji, pokud odpověď nelze najít jinde. V souladu s [Arch Way](/index.php/The_Arch_Way_(%C4%8Cesky) "The Arch Way (Česky)") Vás nabádáme, abyste použili příkaz `man *příkaz*` pro přečtení manuálové stránky jakéhokoliv příkazu, se kterým nejste obeznámeni.

## Contents

*   [1 Příprava](#P.C5.99.C3.ADprava)
    *   [1.1 Systémové požadavky](#Syst.C3.A9mov.C3.A9_po.C5.BEadavky)
    *   [1.2 Vypalte nebo zapište nejnovější instalační médium](#Vypalte_nebo_zapi.C5.A1te_nejnov.C4.9Bj.C5.A1.C3.AD_instala.C4.8Dn.C3.AD_m.C3.A9dium)
        *   [1.2.1 Instalace po síti](#Instalace_po_s.C3.ADti)
        *   [1.2.2 Instalace ve virtuálním stroji](#Instalace_ve_virtu.C3.A1ln.C3.ADm_stroji)
    *   [1.3 Bootování instalačního média](#Bootov.C3.A1n.C3.AD_instala.C4.8Dn.C3.ADho_m.C3.A9dia)
        *   [1.3.1 Testování, jestli jste nabootovali pomocí UEFI](#Testov.C3.A1n.C3.AD.2C_jestli_jste_nabootovali_pomoc.C3.AD_UEFI)
        *   [1.3.2 Problémy při bootování](#Probl.C3.A9my_p.C5.99i_bootov.C3.A1n.C3.AD)

## Příprava

**Note:** Pokud chcete instalovat z existující instalace libovolné GNU/Linux distribuce, přečtěte si prosím [tento článek](/index.php/Install_from_existing_Linux "Install from existing Linux"). Tohle může být užitečné obzvláště pokud plánujete instalovat Arch vzdáleně pomocí [VNC](/index.php/VNC "VNC") nebo [SSH](/index.php/SSH "SSH"). Pokud plánujete vzdálenou instalaci pomocí SSH, přečtěte si prosím [Install from SSH](/index.php/Install_from_SSH "Install from SSH") pro dodatečné tipy.

### Systémové požadavky

Arch Linux by měl běžet na libovolném i686 kompatibilním stroji s alespoň 64 MB RAM. Základní instalace se všemi balíčky ze skupiny [base](https://www.archlinux.org/groups/x86_64/base/) zabere asi 500 MB místa na disku. Pokud pracujete s omezeným diskovým prostorem, velikost instalace může být podstatně osekána, ale musíte vědět, co děláte.

### Vypalte nebo zapište nejnovější instalační médium

Nejnovější vydání instalačního média lze získat ze stránky [Download](https://archlinux.org/download/). Poznamenejme, že jediný ISO obraz podporuje 32 i 64-bit architektury. Nový ISO obraz je vydáván přibližně jednou za měsíc a je doporučeno použít vždy nejnovější ISO obraz.

*   Vypalte ISO obraz na CD nebo DVD pomocí Vámi preferovaného software.

**Note:** Kvalita optických mechanik a disků samotných se velmi liší. Obecně je doporučeno použít nižší rychlost zápisu pro spolehlivá vypálení. Pokud zaznamenáte neočekávané chování disku, zkuste vypálit obraz nejnižší možnou rychlostí.

*   Nebo můžete ISO obraz zapsat na USB flash disk. Vizte [USB Installation Media](/index.php/USB_Installation_Media "USB Installation Media") pro podrobné instrukce.

#### Instalace po síti

Místo zápisu instalačního média na CD, DVD nebo flash disk, můžete alternativně nabootovat ISO obraz přes síť. To funguje dobře, pokud již máte nastaven server. Přečtěte si prosím [tento článek](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") pro více informací, a poté přeskočte na [Bootování instalačního média](#Bootov.C3.A1n.C3.AD_instala.C4.8Dn.C3.ADho_m.C3.A9dia).

#### Instalace ve virtuálním stroji

Instalace ve [virtuálním stroji](https://en.wikipedia.org/wiki/Virtual_machine "wikipedia:Virtual machine") je dobrým způsobem, jak se seznámit s Arch Linuxem a jeho instalací bez opouštění současného operačního systému a přerozdělování oddílů na disku. Také umožní mít tohoto průvodce otevřeného v prohlížeči během instalace. Někteří uživatelé ocení mít nezávislý systém Arch Linux ve virtuálním stroji pro testovací účely.

Příklady virtualizačního software jsou [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen") a [Parallels](/index.php/Parallels "Parallels").

Přesná procedura přípravy virtuálního stroje závisí na použitém software, ale obecně se drží těchto kroků:

1.  Vytvořit obraz virtuálního disku pro operační systém.
2.  Správně nastavit parametry virtuálního stroje.
3.  Nabootovat stažený ISO obraz pomocí virtuální CD mechaniky.
4.  Přeskočit na [Bootování instalačního média](#Bootov.C3.A1n.C3.AD_instala.C4.8Dn.C3.ADho_m.C3.A9dia).

Následující články (anglicky) mohou být užitečné:

*   [Arch Linux as VirtualBox guest](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox")
*   [Arch Linux as VirtualBox guest on a physical drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Arch Linux as VMware guest](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

### Bootování instalačního média

Nejprve musíte změnit pořadí bootování v BIOSu Vašeho počítače. Během [POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") fáze musíte zmáčknout určitou klávesu (obvykle `Delete`, `F1`, `F2`, `F11` nebo `F12`). Poté v menu vyberte *Boot Arch Linux* a zmáčkněte `Enter`.

Po nabootování do instalačního prostředí je Váš shell [Zsh](/index.php/Zsh_(%C4%8Cesky) "Zsh (Česky)"), který poskytuje pokročilé Tab doplňování (*Tab completion*) a další funkce jako součást [grml konfigurace](http://grml.org/zsh/).

#### Testování, jestli jste nabootovali pomocí UEFI

Pokud Vaše základní deska podporuje [UEFI](/index.php/UEFI "UEFI") a pokud je UEFI povolen (a preferován oproti BIOS), instalační CD/USB automaticky spustí Arch Linux jádro (EFISTUB pomocí Gummiboot Boot Manager). Pro zkontrolování, zda jste nabootovali pomocí UEFI, stačí zkontrolovat, zda byl adresář `/sys/firmware/efi` vytvořen:

```
# ls -1 /sys/firmware/efi

```

#### Problémy při bootování

*   Pokud máte integrovanou grafickou kartu Intel a obrazovka při bootování zčerná, pravděpodobně se jedná o problém s [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Možným řešením může být rebootování a zmáčknutí `e` nad volbou, kterou chcete bootovat (i686 nebo x86_64). Na konec řetězce přidejte `nomodeset` a zmáčkněte `Enter`. Alternativně můžete zkusit `video=SVIDEO-1:d`, což nezakáže *Kernel Mode Setting*. Také můžete zkusit `i915.modeset=0`. Vizte [Intel (Česky)](/index.php/Intel_(%C4%8Cesky) "Intel (Česky)") pro více informací.

*   Pokud obrazovka nezčerná a bootovací proces se zasekne při zavádění jádra, zmáčněte `Tab` nad volbou v menu, připište `acpi=off` na konec řetězce a zmáčkněte `Enter`.