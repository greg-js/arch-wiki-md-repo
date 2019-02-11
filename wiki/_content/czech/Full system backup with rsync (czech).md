Tento [rsync](/index.php/Rsync "Rsync") skript umožňuje vytvoření kompletní zálohy napříč systémy souborů. Je nastaven tak, že kopie (záloha) zahrnuje nedotčené bootovací schopnosti, volitelně lze vyloučit určité vybrané soubory.

Tento postup má výhody před pouhým zkopírovaním osobních dat s vynechávním systémových souborů. Pokud se systém nějak poruší na hlavním oddílu, překonání problému znamená nabootování ze zálohy v porovnání s identifikací a reinstalací postižených programů.

Instrukce byly převzaty z [z toho přízpěvku ve fóru](https://bbs.archlinux.org/viewtopic.php?id=83071).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Soubory](#Soubory)
    *   [1.1 Zálohovací skript](#Zálohovací_skript)
    *   [1.2 Seznam toho, co zahrnout/nezahrnout](#Seznam_toho,_co_zahrnout/nezahrnout)
*   [2 Záloha](#Záloha)
*   [3 Nastavení bootování](#Nastavení_bootování)
    *   [3.1 Úprava fstab](#Úprava_fstab)
    *   [3.2 Instalace boot manažera](#Instalace_boot_manažera)
    *   [3.3 Konfigurace boot manažera](#Konfigurace_boot_manažera)

## Soubory

Jsou potřeba dvě věci: zálohovací skript a soubor uvědějící, které soubory zahrnout/nezahrnout ze zdroje zálohy.

### Zálohovací skript

Tento skript je velmi jednoduchý; používá rsync v archivním režimu, přičemž je zajištěno, že symbolické odkazy, zařízení, práva a vlastnictví aj. jsou zachovány. Vyloučeny jsou soubory odpovídající vzorům ze seznamu co zahrnout/co vyloučit.

Uložte ho jako `rbackup.sh` a nastavte mu atribut spustitelnosti:

 `rbackup.sh` 
```
#!/bin/sh
# rsync backup script

sudo sh -c "
    rsync -av --delete-excluded --exclude-from=backup.lst / $1;
    touch $1/BACKUP
"
```

	Zdroj zálohy; `/`

	V tomto případě se provádí záloha celého kořenu (root).

	Kam zálohovat; `$`1

	Předává se jako parametr skriptu; např. `/media/backup`

	Co zahrnout/nezahrnout; `--exclude-from=backup.lst`

	Tento příklad používá `backup.lst`.

### Seznam toho, co zahrnout/nezahrnout

Jelikož může být obtížné určit, které soubory budou v tomto seznamu, uvádím zde typický zálohovací příklad, který nezahrnuje běžné soubory, které nejsou třeba zázálohovat, jako většina `/dev`. Poznámka: specifikace každého žádaného souboru nebo adresáře v `Include` není třeba; tato sekce pouze slouží jako filter pro specifikaci `Exclude`. Tento soubor je tradičně ve formátu co zahrnout/co nezahrnout programu rsync.

Uložte následující jako `backup.lst`:

 `backup.lst` 
```
# Zahrnout
+ /dev/console
+ /dev/initctl
+ /dev/null
+ /dev/zero

# Vyloučit
- /dev/*
- /proc/*
- /sys/*
- /tmp/*
- *lost+found
- /media/backup/*

```

	Vyloučit

	Obsah systémových adresářů; `/dev`, `/proc`, `/sys` a `/tmp` je vyloučen, protože je vytvářen systémem při startu, zatímco tyto adresáře je třeba zachovat, jelikož *nejsou* vytvářeny při startu. Nakonec, všechny `lost+found` instance jsou vynechány, protože jsou specifické pro oddíl. Pro Archlinux `/var/lib/pacman/sync/*` mohou být rovněž vynechány. To může ušetřit dost času při každém zálohování, jelikož adresář obsahuje hodně malých souborů, které mají tendenci se často měnit. Toto jsou "popisovací" soubory pro každý balíček z repozitářů. Tyto soubory lze vygenerovat znovu pomocí `pacman -Syu`.

**Warning:** nezapomeňte rovněž vynechat připojený adresář, kam budete zálohovat, vyvarujete se tak nekonečné smyčky (v tomto příkladu `**/media/backup/**`).

	Zahrnout

	Dokonce ačkoli `/dev` je vyloučeno, 4 soubory, které nejsou dynamicky vytvářeny pomocí [udev](/index.php/Udev "Udev") musí být zachovány. Jsou to `console`, `initctl`, `null` and `zero`.

## Záloha

Nahraďte `/media/**backup**` podle potřeby, a připojte cílové zařízení:

```
# mount /dev/sdb1 /media/backup

```

**Tip:** pokud není důležitá možnost bootovat ze zálohy, vynechejte předchozí krok a jednoduše zálohujte do libovolného adresáře.

Spusťe zálohovací skript (zakončení pomocí znaku "`/`" je nutné):

```
# ./rbackup.sh /media/backup/

```

## Nastavení bootování

Poté co synchronizace skončila, cílový `/etc/fstab` je třeba upravit a musí být nainstalován boot manažer v cíli zálohy. Konfigurace cílového `/boot/grub/menu.lst` je vyžadována, aby bylo reflektováno nové umístění.

### Úprava fstab

Upravte cílovou fstab:

 `$ nano /media/backup/etc/fstab` 
```
none         /dev/pts      devpts    defaults      0 0
none         /dev/shm      tmpfs     defaults      0 0

*/dev/sda1    /boot         ext4      defaults      0 1
/dev/sda5    /var          ext4      defaults      0 1
/dev/sda6    /usr          ext4      defaults      0 1
/dev/sda7    /             ext4      defaults      0 1
/dev/sda8    /home         ext4      defaults      0 1
/dev/sda9    swap          swap      defaults      0 0*

```

Protože rsync vykonal rekurzivní kopii *celého* kořenového systému, všechny `sda` body připojení jsou problematické a mohou způsobit, že bootování ze zálohy skončí s chybou. V tomto příkladu, všechny problematické položky jsou nahrazeny jednou jedinou:

 `$ nano /media/backup/etc/fstab` 
```
none         /dev/pts      devpts    defaults      0 0
none         /dev/shm      tmpfs     defaults      0 0

/dev/**sdb1**    /             **ext4**      defaults      0 1

```

Jako předtím, nezapomeňte použít správné jméno zařízení a správný systém souborů.

### Instalace boot manažera

Tyto instrukce předpokládají využití [GRUB](/index.php/GRUB "GRUB"), mohou být lehce upraveny pro jiné boot manažery, jako např. [LILO](/index.php/LILO "LILO").

Otevřete Grub konzoli:

```
# grub

```

Přímo instalujte na cílové zařízení:

```
root (hd**1,0**)
setup (hd**1**)

```

	root; `hd 1,0`

	Mělo by odkazovat na umístění souborů Grubu -- v tomto případě, "`hd 1`" znamená druhé uložné zařízení (`/dev/sdb`) a "`0`" je první oddíl (`/dev/sdb*1*`).

	setup; `hd 1`

	Tento příkaz specifikuje, kam se má nainstalovat boot manager. V tomto příkladu je nainstalován do [MBR](/index.php/MBR "MBR") druhého uložného zařízení.

### Konfigurace boot manažera

I když se boot manažer nainstaluje korektně, jeho položky menu jsou pro hlavní systémové oddíly, ne pro oddíl(y) zálohy.

Toto je možné řešit uživatelským `/boot/grub/menu.lst`. Abyste mohli toto udělat, upravte `rbackup.sh` tak aby zkopíroval uživatelský `menu.lst`:

 `rbackup.sh` 
```
#!/bin/sh
# rsync backup script

sudo sh -c "
    rsync -av --delete-excluded --exclude-from=backup.lst / $1;
    **cp ~/custom.menu.lst $1/boot/grub/menu.lst;**
    touch $1/BACKUP
"
```

**Tip:** místo nahrazení `menu.lst` uživatelskou verzi jenom pro zálohu, přidejte položku Grubu která odkazuje na zařízení zálohy nebo jednoduše zeditujete Grub menu během startu.