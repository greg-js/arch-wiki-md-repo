[Display manager](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)"), nebo-li česky přihlašovací manažer či správce displeje, je grafická obrazovka, která je zobrazena na konci bootovacího procesu místo shellu. Existuje několik druhů přihlašovacích manažerů, stejně jako je několik správců oken a desktopů. Většinou je lze do určité míry upravovat a měnit jejich vzhled.

## Contents

*   [1 Instalace balíčků](#Instalace_bal.C3.AD.C4.8Dk.C5.AF)
*   [2 Konfigurace zavádění přihlašovacího manažera](#Konfigurace_zav.C3.A1d.C4.9Bn.C3.AD_p.C5.99ihla.C5.A1ovac.C3.ADho_mana.C5.BEera)
    *   [2.1 inittab metoda (doporučeno)](#inittab_metoda_.28doporu.C4.8Deno.29)
        *   [2.1.1 Úprava výchozí úrovně spuštění](#.C3.9Aprava_v.C3.BDchoz.C3.AD_.C3.BArovn.C4.9B_spu.C5.A1t.C4.9Bn.C3.AD)
        *   [2.1.2 Změna přihlašovacího manažeru](#Zm.C4.9Bna_p.C5.99ihla.C5.A1ovac.C3.ADho_mana.C5.BEeru)
    *   [2.2 Daemon metoda](#Daemon_metoda)
*   [3 Problémy](#Probl.C3.A9my)
    *   [3.1 Přepínání run-levelů](#P.C5.99ep.C3.ADn.C3.A1n.C3.AD_run-level.C5.AF)
        *   [3.1.1 Příkazový řádek](#P.C5.99.C3.ADkazov.C3.BD_.C5.99.C3.A1dek)
        *   [3.1.2 GRUB](#GRUB)
        *   [3.1.3 LILO](#LILO)
    *   [3.2 GDM havaruje při odhlašování](#GDM_havaruje_p.C5.99i_odhla.C5.A1ov.C3.A1n.C3.AD)
    *   [3.3 GDM přihlášení jako root](#GDM_p.C5.99ihl.C3.A1.C5.A1en.C3.AD_jako_root)
*   [4 GDM vždy používá předvolenou US-klávesnici](#GDM_v.C5.BEdy_pou.C5.BE.C3.ADv.C3.A1_p.C5.99edvolenou_US-kl.C3.A1vesnici)
*   [5 Vizte též](#Vizte_t.C3.A9.C5.BE)

## Instalace balíčků

Zvolte si a nainstalujte preferovaný přihlašovací manažer:

**Note:** Je zvykem, ovšem není to nutné, zvolit si přihlašovací manažer, který patří ke zvolenému desktopovému prostředí. Pokud desktopové prostředí přihlašovací manažer neobsahuje, obvykle se používá [SLiM](/index.php/SLiM "SLiM").

**XDM:** X Display Manager

```
# pacman -S xorg-xdm

```

**GDM:** [GNOME](/index.php/GNOME "GNOME") Display Manager

```
# pacman -S gdm

```

**[SLiM](/index.php/SLiM "SLiM"):** Simple Login Manager

```
# pacman -S slim

```

**[Qingy](/index.php/Qingy "Qingy"):** DirectFB náhrada getty (je vhodné přidat balíček témat qingy-theme-arch)

```
# pacman -S qingy qingy-theme-arch

```

**Entrance:** Enlightenment Display Manager (momentálně — 07/2010 — není obsažen v repozitářích!)

```
# pacman -S entrance-svn

```

**[CDM](/index.php/CDM "CDM"):** Console Display Manager (balíček je dostupný v repozitáři AUR: [cdm-git](https://aur.archlinux.org/packages/cdm-git/))

## Konfigurace zavádění přihlašovacího manažera

Jsou dva jednoduché způsoby, jak nechat systém zavést přihlašovací manažer:

	`inittab` metoda

	přihlašovací manažer se zavede automaticky po startu a v případě pádu se obnoví.

	[Daemon](/index.php/Daemon "Daemon") metoda

	přihlašovací manažer se zavede automaticky během startu jako daemon. (V současnosti to funguje pouze s Entrance, GDM a SLiM).

Metoda `inittab` je z různých důvodů doporučována. Jedním z nich je, že vám dovolí z [GRUB](/index.php/GRUB "GRUB") nabootovat přímo do framebuffer režimu. Toto je například výhodou, když v X spadne ovladač grafické karty, jelikož nebudete nuceni opravovat systém z živého CD nebo pomocí jiných zbytečně složitých prostředků.

S metodou `inittab` vše, co byste museli udělat, je zmáčknout ve výzvě GRUBu 'e' pro úpravy a prostě přidat preferované číslo run-levelu **3** na konec 'kernel' řádku a nabootujete přímo do framebuffer režimu pro opravu svého systému/X (toto je lépe rozebráno níže).

Při použití metody daemon můžete jednoduše nabootovat do run-levelu **1/S**, který zabrání spuštění daemonů včetně přihlašovacího manažeru. Potom opravíte svůj systém/X a přepnete se do run-levelu **3**. Oboje metody jsou srovnatelně jednoduché.

### `inittab` metoda (doporučeno)

**Warning:** Pokud používáte [KMS](/index.php/KMS "KMS"), můžete mít problém s ovladačem grafické karty. Obrazovka může zamrznout.

Run-levely (úrovně spuštění/běhu) jsou:

```
0    Zastavit
1(S) Jeden uživatel
2    Nepoužito
3    Více uživatelů (předvoleno)
4    Nepoužito
5    X11
6    Restart

```

#### Úprava výchozí úrovně spuštění

Otevřete soubor `/etc/inittab` a najděte řádek, který vypadá takto:

```
id:3:initdefault:

```

Změňte '3' na '5' pro X11:

```
id:5:initdefault:

```

Když nyní zrestartujete počítač, měl by se spustit 'přihlašovací manažer'. Pro jiné přihlašovací manažery se podívejte níže:

#### Změna přihlašovacího manažeru

Otevřete soubor `/etc/inittab` a najděte řádek, který vypadá takto (ke konci):

```
x:5:respawn:/usr/bin/xdm -nodaemon

```

Upravte ho tak, aby odkazoval na vámi zvolený přihlašovací manažer:

**GDM:**

```
x:5:respawn:/usr/sbin/gdm -nodaemon

```

**SLiM:**

```
x:5:respawn:/usr/bin/slim >& /dev/null

```

**Entrance:**

```
x:5:respawn:/usr/sbin/entranced --nodaemon &> /dev/null

```

Když nyní zrestartujete počítač, měl by se spustit přihlašovací manažer podle vaší volby.

### Daemon metoda

Jednoduše potřebujete přidat jméno daemona do svého pole daemonů v souboru `/etc/rc.conf`

Poblíž konce souboru uvidíte řádek, který vypadá podobně jako tento:

```
DAEMONS=(syslogd klogd !pcmcia network netfs crond) # toto je pole daemonů

```

Přidejte na konec jméno daemona vámi zvoleného přihlašovacího manažeru (`entranced`, `gdm`, nebo `slim`):

```
DAEMONS=(syslogd klogd !pcmcia network netfs crond **entranced**)

```

Ujistěte se, že jste zadali jméno daemona přihlašovacího manažeru **na konec** řádku, jinak X později alokuje tty zařízení, které bylo předtím nárokováno getty - (viz `/etc/inittab`). Neumístění přihlašovacího manažera na konec řádku způsobí krach X a není tedy podporováno.

Když nyní zrestartujete počítač, měl by se přihlašovací manažer spustit. V opačném případě se ujistěte, že jste zadali jeho jméno správně. Také se ujistěte, že je nainstalovaný a že se `startx` nezastavuje s chybami.

**Note:** Pokud při použití této metody přihlašovací manažer havaruje nebo X nedokáže rozpoznat žádné vstupní zařízení, je nutné nabootovat do jednouživatelského módu (run-level 1) podle příkladů, uvedených výše a odstranit daemona přihlašovacího manažeru ze souboru `rc.conf`.

## Problémy

### Přepínání run-levelů

#### Příkazový řádek

Pokud chcete vyzkoušet správce obrazovky bez restartu nebo jen změnit konfiguraci X a přihlašovací manažer se stále obnovuje, použijte příkaz:

```
/sbin/telinit <run-level>

```

Pro přepnutí do run-levelu 3 (víceuživatelský):

```
/sbin/telinit 3

```

Pro přepnutí do run-levelu 5 (X11):

```
/sbin/telinit 5

```

Přepínáním se můžete vyhnout restartu systému během testování.

#### GRUB

Do [GRUB](/index.php/GRUB "GRUB") můžete přidat položku menu, která vám umožní bootovat s nebo bez X11:

V souboru `/boot/grub/menu.lst` najděte první záznam kernelu (standardně '# (0) Arch Linux')

```
# (0)  Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz26 root=/dev/sda3 ro
initrd /kernel26.img

```

Můžete jej duplikovat a změnit takto:

```
# (0)  Arch Linux Multi-user
title  Arch Linux Multi-user
root   (hd0,0)
kernel /vmlinuz26 root=/dev/sda3 ro **3**
initrd /kernel26.img

```

```
# (1)  Arch Linux X11
title  Arch Linux X11
root   (hd0,0)
kernel /vmlinuz26 root=/dev/sda3 ro **5**
initrd /kernel26.img

```

Run-level byl přidán na konec, takže jádro ví, v jakém run-levelu se má spustit.

#### LILO

Systém můžete zavést v run-levelu vlastní volby prostě tím, že v bootovací obrazovce [LILO](/index.php/LILO "LILO") vyberete nebo zadáte jméno kernelu a požadovaný run-level za něj přidáte, např.:

```
: Arch 5

```

### GDM havaruje při odhlašování

Pokud se GDM při bootu spustí správně, ale selže po opakovaných pokusech o odhlášení, zkuste přidat tento řádek do sekce daemon v souboru `/etc/gdm/custom.conf`:

```
GdmXserverTimeout=60

```

### GDM přihlášení jako root

Není doporučené přihlašovat se jako root, ovšem v případě potřeby lze do souboru `/etc/gdm/custom.conf` přidat:

```
[security]
AllowRoot=true

```

Po restartu GDM se budete moci přihlásit jako root.

## GDM vždy používá předvolenou US-klávesnici

Klávesnice se vždy přepíná na US verzi, vzhled je resetován po zapojení nové klávesnice.

Řešení: upravit `~/.dmrc`

```
[Desktop]
Language=de_DE.UTF-8 #změnit na váš předvolený jazyk
Layout=de   nodeadkeys #změnit na vaše předvolené rozvržení kláves

```

## Vizte též

*   [SLiM](/index.php/SLiM "SLiM"), [CDM](/index.php/CDM "CDM")