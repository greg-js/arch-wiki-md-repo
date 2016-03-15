## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Instalace balíčku grub2](#Instalace_bal.C3.AD.C4.8Dku_grub2)
*   [3 Instalace nebo obnova GRUBu do hlavního spouštěcího záznamu (MBR)](#Instalace_nebo_obnova_GRUBu_do_hlavn.C3.ADho_spou.C5.A1t.C4.9Bc.C3.ADho_z.C3.A1znamu_.28MBR.29)
*   [4 Konfigurace zavaděče](#Konfigurace_zavad.C4.9B.C4.8De)
    *   [4.1 Dual booting](#Dual_booting)
        *   [4.1.1 Dual booting s Windows](#Dual_booting_s_Windows)
        *   [4.1.2 Dual booting s jinými distribucemi Linuxu](#Dual_booting_s_jin.C3.BDmi_distribucemi_Linuxu)
*   [5 Tipy a triky](#Tipy_a_triky)
    *   [5.1 Barvy v menu](#Barvy_v_menu)
*   [6 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
*   [7 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)

## Úvod

**Varování:** Příští generace GRand Unified Bootloader (GRUB2) je stále pod vývojem a proto platí všechny obvyklé body. GRUB2 může zavařit váš počítač, zapálit váš dům nebo sníst vaši kočku. Byli jste varováni! Pro většinu lidí kromě těch s exotičtějšími konfiguracemi by GRUB2 měl prostě fungovat.

Mezi GRUBem a GRUB2 proběhly změny v příkazech. Než budete pokračovat, můžete se s nimi chtít seznámit. Např.: "find" bylo změněno na "search".

[http://grub.enbug.org/CommandList](http://grub.enbug.org/CommandList)

## Instalace balíčku grub2

Nejdříve nainstalujte grub2 pomocí pacmana:

```
# pacman -S grub2

```

Upravte konfigurační soubor grub2 podle svého nastavení. "Starý" soubor menu.lst je nahrazen novým souborem pod názvem grub.cfg.

```
# nano /boot/grub/grub.cfg

```

***Poznámka:** Používejte hd[a-z] pro ide a sd[a-z] pro scsi a sata*

Zde je příklad jednoduchého konfiguračního souboru:

```
# Config file for GRUB2 - The GNU GRand Unified Bootloader
# /boot/grub/grub.cfg

# DEVICE NAME CONVERSIONS
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,2)
#  /dev/sda3       (hd0,3)
#

# Timeout for menu
set timeout=5

# Set default boot entry as Entry 0
set default=0

# (0) Arch Linux
menuentry "Arch Linux" {
set root=(hd0,1)
linux /vmlinuz26 root=/dev/sda1 ro
initrd /kernel26.img
}

## (1) Windows
#menuentry "Windows" {
#set root=(hd0,3)
#chainloader +1
#}

```

Pokud nemáte zvlášť oddělený bootovací oddíl, musí být do grub.cfg přidáno '`/boot`'. Příklad:

```
# (0) Arch Linux
menuentry "Arch Linux" {
set root=(hd0,1)
linux /boot/vmlinuz26 root=/dev/sda1 ro
initrd /boot/kernel26.img
}

```

## Instalace nebo obnova GRUBu do hlavního spouštěcího záznamu (MBR)

GRUB může být nainstalován buď z live prostředí nebo přímo z běžící instalace Arch Linuxu.

Ve většině případů je instalace grub2 tak jednoduchá jako spuštění příkazu **grub-install** pod rootem:

```
# grub-install /dev/sda

```

kde /dev/sda je cíl instalace (v tomto případě MBR prvního SATA disku).

Pokud toto selže s chybou:

```
grub-probe: error: Cannot get the real path of `/dev/fd0'
Auto-detection of a filesystem module failed.
Please specify the module with the option `--modules' explicitly.

```

Zkuste do parametrů přidat `--recheck` takto:

```
# grub-install --recheck /dev/sda

```

Případně byste měli být schopni nainstalovat grub2 nabootováním do systému a spuštěním příkazu **grub** pod rootem:

```
# grub
{tato sekce je stále nedokončená, měly by být přidány další kroky!!!}

```

(grub2 nemá interaktivní prompt)

## Konfigurace zavaděče

Konfigurace grubu se provádí v tomto souboru:

```
/boot/grub/grub.cfg

```

Tato část zatím není kompletní, můžete sem přidat všechny chybějící konfigurační volby!

*   *(hdn,m)* – je oddíl *m* na disku *n*, čísla oddílů začínají od 1, čísla disků začínají od 0
*   *set default=n* –je výchozí položka pro zavedení, jenž je automaticky zvolena po časovém limitu pro akce od uživatele
*   *set timeout=m* –čas *m* v sekundách, po který se má čekat na výběr uživatele, než je zavedena výchozí položka
*   *menuentry "str"{volby položky}* – titulek *str* pro položku a základní rozvržení
*   *set root=(hdn,m)* –základní diskový oddíl, kde je uloženo jádro
*   *linux /path ro root=/dev/device initrd /initrd.img* – volbu root použijte, pokud kernel není umístěn v /
*   *chainloader +1* – nastaví root jako aktivní a předá řízení jeho zavaděči (pro Windows, např.)

Pro UUID záznamy:

```
bash-3.2# blkid

```

### Dual booting

Toto jsou dvě nejčastější cesty konfigurace souboru grub.cfg. Pro složitější účely sem klidně můžete přidat vysvětlení.

#### Dual booting s Windows

Přidejte toto na konec /boot/grub/grub.cfg. Předpokládá se zde, že váš oddíl s Windows je [s/h]da3.

```
# (2) Windows XP
menuentry "Windows XP" {
set root=(hd0,3)
chainloader +1
}

```

Poznámka: Přestože se v to obecně věří, Windows 2000 a pozdější nemusí být na prvním oddílu, aby se spustily. Pokud oddíl s Windows změní číslo (např. když přidáte nový oddíl před oddíl s Windows), musíte upravit soubor boot.ini, abyste odrazili tuto změnu (viz [tento článek](http://vlaurie.com/computers2/Articles/bootini.htm) pro detaily o tom, jak to udělat).

#### Dual booting s jinými distribucemi Linuxu

Toto se provede přesně tím samým způsobem, jak je zaveden Arch Linux. Zde předpokládáme, že další distribuce je na oddílu [s/h]da2.

```
menuentry "Other Linux" {
set root=(hd0,2)
linux /boot/vmlinuz (add other options here as required)
initrd /boot/initrd.img (if the other kernel uses/needs one)
}

```

## Tipy a triky

### Barvy v menu

Pro změnu barev v GRUB2 uveďte v /boot/grub/grub.cfg tyto dvě volby:

```
set menu_color_normal=light-blue/black
set menu_color_highlight=light-cyan/blue

```

Toto jsou výchozí barvy pro verzi GRUB-legacy v Arch Linuxu. Dostupné barvy jsou zatím nezdokumentované, ale pravděpodobně se shodují s barvami GRUB-legacy.

## Řešení problémů

Sem by měla být přidána všechna řešení problémů.

## Další zdroje

*   [GRUB Homepage](http://www.gnu.org/software/grub/)
*   [GRUB wiki](http://grub.enbug.org/)