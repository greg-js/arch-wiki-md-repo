Ext4 je evolucí nejpoužívanějšího souborového systému na Linuxu – Ext3\. V mnoha ohledech je Ext4 více vylepšen oproti Ext3 než byl Ext3 oproti Ext2\. Ext3 vzniklo hlavně přidáním žurnálování do Ext2, ale Ext4 modifikuje důležité datové struktury souborového systému (např. struktury, určené k ukládání dat souborů). Výsledkem je souborový systémem se zdokonaleným návrhem, lepším výkonem, stabilitou a schopnostmi.

Zdroj: [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4) (anglicky)

## Contents

*   [1 Tvorba nových ext4 oddílů](#Tvorba_nov.C3.BDch_ext4_odd.C3.ADl.C5.AF)
*   [2 Migrace z ext3 na ext4](#Migrace_z_ext3_na_ext4)
    *   [2.1 Připojování ext3 oddílů jako ext4 bez konverze](#P.C5.99ipojov.C3.A1n.C3.AD_ext3_odd.C3.ADl.C5.AF_jako_ext4_bez_konverze)
        *   [2.1.1 Princip](#Princip)
        *   [2.1.2 Postup](#Postup)
    *   [2.2 Konverze ext3 oddílů na ext4](#Konverze_ext3_odd.C3.ADl.C5.AF_na_ext4)
        *   [2.2.1 Princip](#Princip_2)
        *   [2.2.2 Požadavky](#Po.C5.BEadavky)
        *   [2.2.3 Postup](#Postup_2)
        *   [2.2.4 Použítí rozšíření (extens) ext4 na soubory](#Pou.C5.BE.C3.ADt.C3.AD_roz.C5.A1.C3.AD.C5.99en.C3.AD_.28extens.29_ext4_na_soubory)
*   [3 Řešení problémů](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9m.C5.AF)
    *   [3.1 Panika jádra](#Panika_j.C3.A1dra)
    *   [3.2 GRUB chyba 13](#GRUB_chyba_13)
    *   [3.3 Poškození dat](#Po.C5.A1kozen.C3.AD_dat)
    *   [3.4 Zvýšení výkonu](#Zv.C3.BD.C5.A1en.C3.AD_v.C3.BDkonu)

## Tvorba nových ext4 oddílů

1.  Aktualizujte svůj systém: `pacman -Syu`
2.  Naformátujte oddíl: `mkfs.ext4 /dev/sdxY` (změňte `sdxY` na název zařízení, které bude formátováno (např. `sda1`))
3.  Připojte jednotku
4.  Přidejte položku do `/etc/fstab` s použitím ext4 jako typu souborového systému

**Tip:** Více parametrů viz man stránky k k mkfs.ext4; editujte `/etc/mke2fs.conf` k prohlédnutí/kofiguraci předvolených nastavení.

## Migrace z ext3 na ext4

Existují dva způsoby, jak přemigrovat oddíly z ext3 na ext4:

*   připojením ext3 oddílů jako ext4 bez konverze (kompatibilita)
*   konverzí ext3 oddílů na ext4 (výkon)

Tyto dva postupy jsou popsány níže.

### Připojování ext3 oddílů jako ext4 bez konverze

#### Princip

Kompromisem mezi úplnou konverzí na ext4 a prostým setrváním na ext3 je připojení existujících ext3 oddílů jako ext4.

**Pro:**

*   Kompatibilita (souborový systém může být nadále připojen jako ext3) – To umožňuje uživatelům přístup k souborovému systému z jiných distribucí/operačních systémů bez podpory ext4 (např. z Windows s ovladači pro ext3).
*   Lepší výkon (i když ne tak moc jako u zcela zkonvertovaného ext4 oddílu) – Viz [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4) (anglicky) pro detaily.

**Proti:**

*   Je použito méně schopností ext4 (pouze ty, které nemění diskový formát, jakými jsou třeba zpožděná alokace [delayed allocation] a alokace více bloků [multiblock allocation]).

**Note:** Mimo relativní novost ext4 (což může být bráno jako risk) **tato technika nemá žádné stinné stránky.**

#### Postup

1.  Editujte soubor `/etc/fstab` a změňte "type" z ext3 na ext4 u všech oddílů, jenž chcete připojit jako ext4.
2.  Znovu připojte ovlivněné oddíly.
3.  To je vše!

### Konverze ext3 oddílů na ext4

#### Princip

Abyste mohli plně využít ext4, musí být dokončen nevratný proces konverze.

**Pro:**

*   Lepší výkon a úžasné nové schopnosti – Viz [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4) (anglicky) pro detaily.

**Proti:**

*   Nelze číst/zapisovat s ovladači pro ext3 (pro Windows není známý žádný ext4 ovladač)
*   Nevratné (ext4 oddíly nemohou být změněny na ext3)

#### Požadavky

**Note:** Patch pro ext4 je standardně začleněn v balíčku Archu pro GRUB (v době psaní článku, ale to se zřejmě nezmění). Jinak by byl pro boot z ext4 oddílu potřeba [GRUB2](/index.php/GRUB2_(%C4%8Cesky) "GRUB2 (Česky)").

**Warning:** Bootování z ext4 oddílu GRUBem není oficiálně podporováno a [GRUB2](/index.php/GRUB2_(%C4%8Cesky) "GRUB2 (Česky)") je stále ve vývoji. I přesto, že GRUB momentálně funguje, je tou "bezpečnou" volbou boot z ext2 nebo ext3 /boot oddílu. **Byli jste varováni!**

**Note:** Je doporučeno použít poslední verzi Arch Linuxu (2009.02). Starší verze (<= 2008.06) obsahují starší verzi `e2fsprogs`, ovšem stačí je aktualizovat příkazem `pacman -S e2fsprogs` po nastavení sítě. Nebo lze použít [SystemRescueCd >= 1.1.4](http://www.sysresccd.org/Download), které je velice praktické a obsahuje odpovídající verzi.

#### Postup

Tyto instrukce byly převzaty z [http://ext4.wiki.kernel.org/index.php/Ext4_Howto](http://ext4.wiki.kernel.org/index.php/Ext4_Howto) (anglicky) a [https://bbs.archlinux.org/viewtopic.php?id=61602](https://bbs.archlinux.org/viewtopic.php?id=61602) (anglicky). Byly vyzkoušeny a potvrzeny jejich autorem dne 16\. ledna 2009.

*   **Aktualizujte!** Proveďte aktualizaci systému, abyste zajistili, že jsou aktuální všechny potřebné balíčky: `pacman -Syu`
*   **[Zálohujte!](/index.php/Backup_programs "Backup programs")** Zazálohujte si všechna data na všech ext3 oddílech, které budou převedeny na ext4\. I přesto, že je ext4 pro běžné použití považováno za "stabilní", je to poměrně nový a neotestovaný souborový systém. Navíc byl tento postup konverze testován pouze na celkem jednoduché konfiguraci; je nemožné otestovat každou ze všech možných konfigurací, kterou může mít uživatel.
*   Editujte `/etc/fstab` a změňte "type" z ext3 na ext4 u všech oddílů, které budou převedeny na ext4.

**Warning:** ext4 je zpětně kompatibilní s ext3, dokud nejsou povolena nová rozšíření [extents]. Pokud má uživatel oddíl sdílený s jiným OS, který zatím neumí číst ext4 oddíly, lze zmíněný oddíl v Archu připojit jako ext4 a stále být schopen ho používat jinde jako ext3... Avšak už ne po učinění dalšího kroku! Všimněte si, že když oddíl není zcela převeden, má použití ext4 méně výhod.

*   Proces konverze s `e2fsprogs` musí být proveden v době, kdy disk není připojen. Pokud převádíte kořenový oddíl (/), nejjednodušší způsob, jak toho dosáhnout, je nabootovat z nějakého livecd, jak bylo popsáno výše v sekci "[Požadavky](#Po.C5.BEadavky)".
    *   Nabootujte livecd (pokud je třeba).
    *   Pro každý oddíl, který má být převeden na ext4:
        *   Ujistěte se, že oddíl **není připojen**.
        *   Spusťte `tune2fs -O extents,uninit_bg,dir_index /dev/oddíl` (kde `/dev/oddíl` je nahrazen cestou k cílovému oddílu, např. `/dev/sda1`)
        *   Spusťte `fsck -fp /dev/the_partition`

**Note:** Uživatel **MUSÍ** provést fsck souborového systému, jinak nebude čitelný! Tento běh fsck je potřebný k navrácení souborového systému do konzistentního stavu. **Najde chyby kontrolních součtů v popisech skupin** – to se očekává. Parametr "-f" vynutí kontrolu, i když se zdá být souborový systém v pořádku. Parametr "-p" řekne fsck, aby provedlo automatickou opravu (jinak je uživatel požádán pro potvrzení u každé chyby).

*   Restartujte Arch Linux!

**Warning:** Po konverzi kořenového oddílu root (/) a pokusu nabootovat může nastat kernel panic. Pokud se to stane, jednoduše restartujte systém za použití 'fallback' ramdisku a znovu vytvořte 'defaultní' počáteční ramdisk: `mkinitcpio -p linux`

#### Použítí rozšíření (extens) ext4 na soubory

Souborový systém je nyní zkonvertován na ext4, ovšem všechny soubory, které byly zapsané před konverzí nevyužívají nových *rozšíření* ext4, např. zrychlení práce s velkými soubory, redukované fragmentace a zvýšené rychlosti kontroly souborového systému. Aby se využilo všech výhod ext4, musí být všechny soubory na disk znovu zapsány. Ve vývoji je nástroj s názvem *e4defrag*, který toto zařídí ; zatím ovšem není dokončený.

Naštěstí lze použít program *chattr*, který přiměje kernel soubory přepsat. Tento program lze použít na všechny soubory a adresáře jednoho oddílu (např. pokud je /home na samostatném oddílu):

```
find /home -xdev -type f -print0 | xargs -0 chattr +e
find /home -xdev -type d -print0 | xargs -0 chattr +e

```

Doporučuje se tento příkaz otestovat nejdříve na několika souborech, zda vše proběhne v pořádku. Také je doporučeno tento souborový systém po konverzi zkontrolovat.

Příkazem *lsattr* je možné zjistit, zda soubory používají nová *rozšíření*. Mělo by se u nich v seznamu atributů objevit písmeno 'e'.

## Řešení problémů

### Panika jádra

Po převodu kořenového oddílu root (/) může po restartu systému nastat panika jádra (kernel panic). Je to způsobeno tím, že počáteční ramdisk detekoval oddíl jako "ext4dev" namísto "ext4". V tomto případě restartujte za pomoci záložního (fallback) ramdisku a vytvořte výchozí ramdisk znovu:

*   Připojit oddíl root v read-write módu; 'XXX' je název oddílu:

```
# mount /dev/XXX / -o remount,rw

```

*   Manuálně připojit oddíl boot na /boot, pokud je na samostatném oddílu.
*   Znovu vytvořit ramdisk :

```
# mkinitcpio -p linux

```

Během procesu vytváření `mkinitcpio` správně zjistí a zahrne moduly ext4 do počátečního ramdisku.

### GRUB chyba 13

Po nedávném updatu jádra při pokusu nabootovat z ext4 /boot oddílu projevila tato chyba GRUBu:

```
Error 13: Invalid or unsupported executable format

```

Řešením je nabootovat z livecd (např. SystemRescueCd) a provést chroot do instalace Arch Linuxu:

```
# mkdir /mnt/arch
# mount -t ext4 /dev/sda1 /mnt/arch
# mount -t proc proc /mnt/arch/proc
# mount -t sysfs sys /mnt/arch/sys
# mount -o bind /dev /mnt/arch/dev

```

```
# chroot /mnt/arch /bin/bash

```

Pokud je /boot na samostatném oddílu, tento oddíl musí být připojen též:

```
# mount -t ext4 /dev/sda2 /boot

```

Poté by měl problém vyřešit následujícím příkazem:

```
# grub-install --recheck /dev/sda

```

### Poškození dat

Po tvrdém restartu se někdy objevila poškozená data. Přečtěte si prosím [Ext4 ztráta dat; vysvětlení a prevence](http://www.h-online.com/open/Ext4-data-loss-explanations-and-workarounds--/news/112892).

Od verze kernelu 2.6.30 je ext4 považován za "bezpečný." Několik záplat zvýšilo robustnost ext4 - i za cenu mírného snížení výkonu. Lze použít nový mount parametr (`auto_da_alloc`), aby se tomuto chování zabránilo. Více informací viz [Linux 2 6 30 - Zlepšení výkonu souborového systému](http://kernelnewbies.org/Linux_2_6_30#head-329ba44b44a7f58c98ae22b8f2730418cdd6630d).

Pro starší verze kernelu, než je 2.6.30 zvažte přidání parametru `rootflags=data=ordered` na řádek `kernel` v souboru GRUBu `menu.lst` jako preventivní opatření.

### Zvýšení výkonu

Od kernelu verze 2.6.30 výkon ext4 poklesl z důvodu změn, které slouží pro zlepšení integrity dat. [[1]](http://www.phoronix.com/scan.php?page=article&item=ext4_then_now&num=1) Uživatelé mohou výkon zvýšit parametrem `nobarrier` při připojování disku, ovšem **může to být nebezpečné** a může to způsobit poškození či ztrátu dat po výpadku proudu. Vypnutí bariér lze provést příkazem `barrier=0` na požadovaném souborovém systému v souboru `/etc/fstab`. Např.:

```
# /dev/sda5    /    ext4    noatime,barrier=0    0    1

```