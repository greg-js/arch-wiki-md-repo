<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Úvod](#Úvod)
*   [2 Instalace](#Instalace)
    *   [2.1 Instalace Arch Linuxu na LVM](#Instalace_Arch_Linuxu_na_LVM)
    *   [2.2 Rozdělení disků](#Rozdělení_disků)
    *   [2.3 Vytvoření fyzických zařízení](#Vytvoření_fyzických_zařízení)
    *   [2.4 Vytvoření skupin(y) svazků](#Vytvoření_skupin(y)_svazků)
    *   [2.5 Vytvoření logických svazků](#Vytvoření_logických_svazků)
    *   [2.6 Vytvoření systému souborů a připojení logického svazku](#Vytvoření_systému_souborů_a_připojení_logického_svazku)
    *   [2.7 Důležité informace](#Důležité_informace)
*   [3 Nastavení](#Nastavení)
    *   [3.1 Rozšíření logického svazku](#Rozšíření_logického_svazku)
    *   [3.2 Zmenšení logického svazku](#Zmenšení_logického_svazku)
    *   [3.3 Přidání diskového oddílu do skupiny svazků](#Přidání_diskového_oddílu_do_skupiny_svazků)
    *   [3.4 Odebrání diskového oddílu ze skupiny svazků](#Odebrání_diskového_oddílu_ze_skupiny_svazků)
    *   [3.5 Snímky](#Snímky)
        *   [3.5.1 Úvod](#Úvod_2)
        *   [3.5.2 Nastavení](#Nastavení_2)
*   [4 Řešení problémů](#Řešení_problémů)
    *   [4.1 LVM příkazy nefungují](#LVM_příkazy_nefungují)
    *   [4.2 Výpis nastavení přípojných bodů systému souborů nezobrazuje logické svazky](#Výpis_nastavení_přípojných_bodů_systému_souborů_nezobrazuje_logické_svazky)
*   [5 Tipy a triky](#Tipy_a_triky)
*   [6 Další zdroje](#Další_zdroje)

# Úvod

LVM je správce logických svazků pro Linux. LVM vytváří abstrakci nad fyzickým úložištěm dat v podobě virtuálních oddílů, které lze snadněji upravovat. Základní termíny při práci s LVM jsou:

*   **Fyzické zařízení (PV)**: je diskový oddíl (celý pevný disk či loopback soubor), na kterém lze vytvářet skupiny svazků. Fyzické zařízení má speciální hlavičku a je dále rozděleno do fyzických bloků. Fyzické oddíly lze chápat jako obdobu fyzických bloků disku.
*   **Skupina svazků (VG)**: je skupina fyzických zařízení použitých jako úložiště, tedy jeden disk. Skupiny svazků obsahují logické svazky. Skupinu svazků lze chápat jako obdobu pevného disku.
*   **Logické svazky (LV)**: jsou logické či virtuální diskové oddíly, ze kterých se skládá skupina svazků. Tyto logické svazky jsou dále tvořeny fyzickými bloky. Logické svazky lze chápat jako běžné diskové oddíly.
*   **Fyzický blok (PE)**: je malá část disku (obvykle 4 MB), kterou lze přidělit logickému svazku. Fyzické bloky lze chápat jako části disku, které lze přidělit libovolnému diskovému oddílu.

Správa logických svazků LVM je snazší, než správa běžných diskových oddílů:

*   *Libovolný počet* pevných disků lze použit jako jeden velký disk (VG).
*   Diskové oddíly (LV) mohou *přesahovat* na několik pevných disků. Logický svazek může mít velikost celého diskového úložiště (tj. všech pevných disků v něm).
*   Je možné *libovolně* vytářet, rušit a měnit velikost diskových oddílů (LV) a disků (VG). Na umístění logického svazku ve skupině svazků nezáleží tak, jako je tomu s běžnými diskovými oddíly.
*   Lze měnit vělikost, vytvářet a rušit diskové oddíly (LV) a disky (VG) *za běhu* systému. Systémy souborů je pak stále nutné zvětšit či zmenšit. Některé z nich toto za běhu také umožňují.
*   Disky (VG) a diskové oddíly (LV) lze libovolně *pojmenovat*.
*   Je možné vytvořit malé diskové oddíly (LV) a ty zvětšovat *dynamicky* podle míry zaplnění daty. Zvětšení systému souborů musí být stále provedeno ručně. Některé systéstémy souborů toto umožňují za běhu.
*   ...

Příklad:

```
**Fyzické disky**

  Disk1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
    |Oddíl1 50 GB (Fyzické zařízení)|Oddíl2 80 GB (Fyzické zařízení)   |
    |/dev/sda1                      |/dev/sda2                         |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _| _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

  Disk2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
    |Partition1 120 GB (Fyzické zařízení)            |
    |/dev/sdb1                                       |
    | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

```
**LVM logické svazky**

  Skupina svazků 1 (/dev/MeUloziste/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
    |Logický svazek1 15 GB |Logický svazek2 35 GB     |Logický svazek3 200 GB       |
    |/dev/MeUloziste/root  |/dev/MeUloziste/home      |/dev/MeUloziste/media        |
    |_ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

Shrnutí: LVM umožňuje použít veškerou kapacitu disků jako jeden velký disk (skupinu svazků) a tuto pak flexibilněji rozdělit mezi oddíly (logické svazky).

# Instalace

Nejprve je potřeba načíst příslušný jaderný modul:

```
# modprobe dm-mod

```

Pokud už máte Arch Linux nainstalovaný a pouze chcete přidat či vyzkoušet LVM, přeskočte na [rozdělení disků](#Rozdělení_disků).

#### Instalace Arch Linuxu na LVM

Před spuštěním instalačních skritpů Arch Linuxu (/arch/setup), je potřeba rozdělit disk(y) nástrojem `cfdisk` (či jiným Vámi oblíbeným). Protože grub legacy (tj. s verzí menší než 1.0) neumí bootovat z logického svazku LVM, nemůžete vytvořit oddíl `/boot` na LVM. Vytvořte tedy samostatný bootovací oddíl. Za dostatečnou velikost se považuje 100MB. Alternativně můžete použít zavaděč lilo nebo grub 2 (od verze 1.95).

#### Rozdělení disků

Dalším krokem je vytvoření diskového oddílu pro LVM. Pro tento oddíl použijte systém souborů typu *Linux LVM*, tedy id oddílu 0x8e (typ systému souborů: 8e). Na každém disku, kde chcete použít LVM, stačí vytvořit jeden diskový oddíl typu LVM. Ten bude využit pro logické svazky, volte tedy vhodnou velikost. Pokud chcete používat pouze LVM, využijte pro diskový oddíl LVM veškeré volné místo na každém disku.

**Tip:** Lze nastavit, aby se všechny LVM oddíly na všech discích tvářily jako jeden velký disk.

#### Vytvoření fyzických zařízení

Nyní je třeba inicializovat vytvořené LVM diskové oddíly. Příkazem `fdisk -l` zjistěte, které diskové oddíly mají typ systému souborů *Linux LVM* a vytvořte z nich fyzické zařízení LVM:

```
# pvcreate /dev/sda2

```

Nahraďte `/dev/sda2` všemi oddíly, ze kterých chcete vytvořit fyzické zařízení LVM. Tento příkaz vytvoří LVM hlavičku na daných diskových oddílech. Vytvořená fyzická zařízení můžete sledovat příkazem:

```
# pvdisplay

```

#### Vytvoření skupin(y) svazků

V dalším kroku vytvoříte na fyzickém zařízení skupinu svazků. Nejprve vytvořte skupinu svazků na jednom z nových fyzických zařízení. Poté můžete přidat všechna ostatní fyzická zařízení, která chcete do skupiny svazků zahrnout:

```
# vgcreate VolGroup00 /dev/sda2
# vgextend VolGroup00 /dev/sdb1

```

Namísto VolGroup00 můžete použít libovolné jméno skupiny svazků, kterou chcete vytvořit. Růst skupiny svazků můžete sledovat příkazem:

```
# vgdisplay

```

**Note:** Pokud chcete, můžete vytvořit více skupin svazků. Celé Vaše datové úložiště se pak však nebude tvářit jako jeden disk.

#### Vytvoření logických svazků

Nyní nastal čas vytvořit ve skupině svazků logické svazky. Toho dosáhnete spuštěním následujícího příkazu, ve kterém určujete jméno nového logického svazku, jeho velikost a skupinu svazků, ve které má být vytvořen:

```
# lvcreate -L 10G VolGroup00 -n lvolhome

```

Dojde k vytvoření logického svazku, ke kterému můžete přistupovat jako k `/dev/mapper/Volgroup00-lvolhome` nebo `/dev/VolGroup00/lvolhome`. Stejně jako při vytváření skupiny svazků i pro logický svazek můžete použít libovolné jméno.

Při vytváření oddílu swap na logickém svazku použijte následující příkaz:

```
# lvcreate -C y -L 10G VolGroup00 -n lvolswap

```

Parametr `-C y` určuje, že má být vytvořen souvislý oddíl. To znamená, že se swap oddíl nerozdrobí mezi více disků, či několik nesouvislých fyzických bloků.

Pokud chcete vyplnit vytvářeným logickým svazkem zbytek místa ve skupině svazků, použijte následující příkaz:

```
# lvcreate -l +100%FREE VolGroup00 -n lvolmedia

```

Logické svazky můžete sledovat příkazem:

```
# lvdisplay

```

**Note:** Pro funkčnost předchozích příkazů může být pořeba načíst modul *device-mapper*. Toho docílíte příkazem **modprobe dm-mod**.

**Tip:** Pro začátek můžete vytvořit relativně malé logické svazky a ty rozšiřovat až podle potřeby. Jednoduše nechte ve skupině svazků volné místo.

#### Vytvoření systému souborů a připojení logického svazku

Vytvořené logické svazky najdete ve složce `/dev/mapper/` a `/dev/YourVolumeGroupName`. Pokud je nemůžete najít, použijte následující příkazy pro zavedení modulu vytváření uzlů zařízení a pro aktivaci skupin svazků:

```
# modprobe dm-mod
# vgchange -ay

```

Nyní můžete na logických svazcích vytvořit systémy souborů. Poté už jen připojíte logické svazky jako běžné diskové oddíly. (Pokud právě instalujete Arch linux, tento krok přeskočte. K připojení logických svazků využijte instalátor, ve kterém vyberte vytvořené LVM oddíly.):

```
# mkfs.ext3 /dev/mapper/VolGroup00-lvolhome
# mount /dev/mapper/VolGroup00-lvolhome /home

```

Pokud instalujete Arch Linux, spusťte /arch/setup, vyberte volbu *Prepare Hard Drive* a pak přímo krok 3 *Set Filesystem Mountpoints* a ***přečtěte si sekci [Důležité informace](#Důležité_informace) před tím, než budete s instalací systému pokračovat!***

### Důležité informace

Při používání Arch Linuxu s LVM, či instalaci na LVM dbejte na následující (v závorkách jsou uvedena odpovídající menu instalátoru):

*   Při výběru přípojných bodů vybírejte pouze nově vytvořené logické svazky (použijte: `/dev/mapper/Volgroup00-lvolhome`).
    NEVYBÍREJTE skutečné oddíly, na kterých jsou logické svazky vytvořeny. Tedy nepoužívejte: `/dev/sda2`. (*Set Filesystem Mountpoints*)
*   Změňte volbu *USELVM="no"* na *USELVM="yes"* v souboru `/etc/rc.conf`. (*Configure System*)
*   Přidejte *lvm2* do sekce HOOKS v souboru `/etc/mkinitcpio.conf` těsně před *filesystems*, aby kernel dokázal najít LVM oddíly při bootu. Pokud chcete využívat LVM snímky, přidejte *dm-snapshot* do proměnné MODULES. (*Configure System*)
*   Pokud jste na logický svazek umístili i systém souborů kořenového adresáře ( "/" ), znovu sestavte obraz kernelu (*/boot/kernel26.img*) s využitím upraveného souboru `/etc/mkinitcpio.conf`. Tím umožníte zavaděči nalezení oddílu root při bootu. Využijte k tomu níže uvedený příkaz: (*Configure System*)

```
     mkinitcpio -g /boot/kernel26.img 

```

*   V konfiguračním systému zavaděče grub: `/boot/grub/menu.lst` použijte správný oddíl pro root, například: (*Install Bootloader*)

```
     ...
     (0) Arch Linux
     title  Arch Linux
     root   (hd0,0)
     kernel /vmlinuz26 **root=/dev/mapper/VolGroup00-lvolroot** resume=/dev/mapper/VolGroup00-lvolswap ro
     initrd /kernel26.img
     ...

```

*   Pokud používáte LILO nastavte ho obdobně: `/etc/lilo.conf`:

```
     image=/boot/vmlinuz26
       label=arch
       append="**root=/dev/mapper/VolGroup00-lvolroot** resume=/dev/mapper/VolGroup00-lvolswap ro"
       initrd=/boot/kernel26.img

```

# Nastavení

## Rozšíření logického svazku

Nejprve je třeba zvětšit logický svazek a pak ještě zbývá zvětšit systém souborů, aby využil nově vytvořené místo. Řekněme, že máme logický svazek o velikosti 15 GB, na kterém je systém souborů ext3\. Tento chceme zvětšit na 20 GB. Musíme tedy udělat následující:

```
# lvextend -L 20G VolGroup00/lvolhome
# resize2fs /dev/VolGroup00/lvolhome

```

Lze také využít příkaz `lvresize` namísto `lvextend`:

```
# lvresize -L +5G VolGroup00/lvolhome

```

Pokud chcete vyplnit veškeré zbývající volné místo ve skupině svazků, použijte následující příkaz:

```
# lvextend -l +100%FREE VolGroup00/lvolhome

```

**Warning:** Ne všechny souborové systémy podporují zvětšení beze ztráty dat, či zvětšení za běhu.

**Note:** Pokud nezvětšíte systém souborů, bude jemu odpovídající oddíl stále stejně velký. Logický svazek pak bude mít novou velikost a bude částečně nevyužitý.

## Zmenšení logického svazku

Protože nejspíše máte systém souborů tak velký jako logický svazek, na kterém je umístěn, je nejprve nutné zmenšit systém souborů. Podle toho, jaký systém souborů používáte, může být nejprve nutné systém souborů odpojit. Řekněme, že máme logický svazek o velikosti 15 GB, na kterém je systém souborů ext3\. Tento svazek chceme zmenšit na 10 GB. Musíme tedy udělat následující:

```
# resize2fs /dev/VolGroup00/lvolhome 9G
# lvreduce -L 10G VolGroup00/lvolhome
# resize2fs /dev/VolGroup00/lvolhome

```

Lze také využít příkaz `lvresize` namísto `lvreduce`:

```
# lvresize -L -5G VolGroup00/lvolhome

```

V příkladě jsme zmenšili systém souborů více, než bylo potřeba. Učinili jsme tak proto, abychom náhodně nesmazali některé z posledních bloků systému souborů. Zbývá tedy ještě zvětšit systém souborů tak, aby vyplnil zbývající místo na logickém svazku.

**Warning:** Zmenšujte systém souborů pouze o tolik, aby zbylo dost místa pro uložená data.

**Warning:** Ne všechny systémy souborů umožňují zmenšení beze ztráty dat, či zmenšení za běhu.

## Přidání diskového oddílu do skupiny svazků

Aby bylo možné přidat oddíl do skupiny svazků, musíte nejprve změnit jeho typ na *Linux LVM* (například nástrojem `cfdisk`). Poté zbývá ještě vytvořit z oddílu fyzické zařízení a rozšířit o něj skupinu svazků:

```
# pvcreate /dev/sdb1
# vgextend VolGroup00 /dev/sdb1

```

Tím jste získali volné místo ve skupině svazků, které může být využito logickými svazky.

**Tip:** Přidané diskové oddíly se mohou nacházet na libovolných discích.

## Odebrání diskového oddílu ze skupiny svazků

Při odebírání diskového oddílu ze skupiny svazků je potřeba přesunout všechna data, která se na něm nachází, na jiný diskový oddíl. LVM toto umožňuje následovně:

```
# pvmove /dev/sdb1

```

Pokud chete přesunout data na určité fyzické zařízení, použijte následující příkaz:

```
# pvmove /dev/sdb1 /dev/sdf1

```

Poté můžete odebrat fyzické zařízení ze skupiny oddílů:

```
# vgreduce myVg /dev/sdb1

```

Nebo také můžete odstranit všechna prázdná fyzická zařízení:

```
# vgreduce --all vg0

```

Konečně, pokud chcete využívat diskový oddíl pro jiné učely, a zabránit tomu, aby byl chápán jako fyzické zařízení LVM, použijte následující příkaz:

```
# pvremove /dev/sdb1

```

## Snímky

#### Úvod

LVM umožuje efektivnější vytvářní snímků systému, než klasické metody zálohování. Pro tento účel používá techniku kopírování při zápisu. Na počátku obsahuje snímek pouze pevné odkazy na inody skutečných dat. Dokud zůstávají data nezměněna, snímek tedy pouze obsahuje odkazy inodů a nikoliv samotná data. V okamžiku, kdy změníte soubor (či adresář), na který snímek odkazuje, LVM automaticky naklonuje data tak, že snímek odkazuje na starou kopii a aktivní systém souborů odkazuje na novou. Takto je možné vytvořit snímek 35 GB dat, který využije jen 2 GB prostoru navíc, pokud tedy nezměníte více jak 2 GB původních dat (či dat ve snímku).

#### Nastavení

Snímek logického svazku vytvoříte obdobně jako samotný logický svazek:

```
# lvcreate --size 100M --snapshot --name snap01 /dev/mapper/vg0-pv

```

Takto můžete změnit méně než 100 MB dat, než se svazek snímku zaplní.

Aby systém nabootoval, je potřeba mít v proměnné MODULES souboru `/etc/mkinitcpio.conf` uveden modul *dm-snapshot*. Pokud toto provedete na již používaném systému, nezapomeňte přegenerovat obraz jádra:

```
# mkinitcpio -g /boot/kernel26.img

```

TODO: Skripty automatizující snímky kořenového systému souborů před updatováním systému, což umožní pozdější návrat k předchozímu stavu. Úprava `menu.lst`, aby šlo bootovat snímky (samostatný článek?).

Primárním účelem snímku je poskytnout zmraženou kopii systému souborů pro účel zálohování. Obzvláště pro dlouhoběžící zálohovací úlohy tak lze dosáhnout mnohem konzistentnějšího obrazu systému souborů, než při přímém zálohování diskového oddílu.

# Řešení problémů

#### LVM příkazy nefungují

*   Načtěte správný jaderný modul:

```
# modprobe dm-mod

```

*   Zkuste předcházet příkazy slovem *lvm* následovně:

```
# lvm pvdisplay

```

#### Výpis nastavení přípojných bodů systému souborů nezobrazuje logické svazky

Pokud instalujete systém někam, kde už existuje LVM skupina svazků, může se stát, že i po vykonání příkazu `modprobe dm-mod` nepůjde zobrazit seznam logických svazků.

V takovém případě musíte ještě spustit příkaz:

```
# vgchange -ay <skupina svazků>

```

Takto aktivujete skupinu svazků a zpřístupníte logické svazky.

# Tipy a triky

TODO:

# Další zdroje

Další články týkající se LVM na Archwiki:

*   [Installing with software RAID or LVM](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM")
*   [RAID encryption LVM](/index.php/RAID_Encryption_LVM "RAID Encryption LVM")

Externí zdroje:

*   [LVM na Wikipedii (anglicky)](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux) "wikipedia:Logical Volume Manager (Linux)")
*   [LVM HOWTO na tldp.org (anglicky)](http://tldp.org/HOWTO/LVM-HOWTO/)
*   [LVM na wiki.gentoo.org (anglicky)](http://wiki.gentoo.org/wiki/LVM)
*   [LVM2 zrcadlení vs. MD raid 1 (anglicky)](http://www.joshbryan.com/blog/2008/01/02/lvm2-mirrors-vs-md-raid-1)