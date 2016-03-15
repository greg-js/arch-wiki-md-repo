Tato stránka popisuje jak opravit počítač, jehož jádro při náběhu zpanikaří (= **kernel panic**, jádro zastaví svoji činnost).

## Contents

*   [1 Řešení problému](#.C5.98e.C5.A1en.C3.AD_probl.C3.A9mu)
*   [2 1\. možnost: Přeinstalace jádra](#1._mo.C5.BEnost:_P.C5.99einstalace_j.C3.A1dra)
    *   [2.1 Spusťte instalační CD](#Spus.C5.A5te_instala.C4.8Dn.C3.AD_CD)
    *   [2.2 Chroot do svého kořenového adresáře](#Chroot_do_sv.C3.A9ho_ko.C5.99enov.C3.A9ho_adres.C3.A1.C5.99e)
    *   [2.3 Návrat k předchozí verzi jádra](#N.C3.A1vrat_k_p.C5.99edchoz.C3.AD_verzi_j.C3.A1dra)
*   [3 2\. možnost: Ověřte konfiguraci zavaděče](#2._mo.C5.BEnost:_Ov.C4.9B.C5.99te_konfiguraci_zavad.C4.9B.C4.8De)
*   [4 Restart](#Restart)

## Řešení problému

Abyste řešení problému usnadnili, ujistěte se, že jádro není v tichém (quiet) režimu. Je-li, odstraňte "quiet" z řádku kernel v konfiguraci GRUBu. Při nabíhání systému ověřujte výstup hned před panikou a rozhodněte, zda je tam jakákoliv užitečná informace. Příčin panik je zřejmě příliš mnoho na to, aby mohly být dobře zdokumentovány v této wiki. Ujistěte se, že konfigurace vašeho systému v /boot je správná a že žádný z hardware počítače není vadný. Pokud věříte, že je panika jádra selháním paniky samotné, následujte níže uvedenou první možnost pro instalaci dřívějšího jádra. Pokud věříte, že konfigurace v /boot může být chybná, následujte možnost 2.

## 1\. možnost: Přeinstalace jádra

Přeinstalace jádra je pravděpodobně ta nejlepší sázka, pokud nedávno nebyly provedeny žádné jiné velké systémové úpravy.

### Spusťte instalační CD

První krok je nabootování instalačního CD. Po startu zadejte <tt>arch</tt>, jako byste instalovali Arch Linux.

```
# arch

```

### Chroot do svého kořenového adresáře

Po nabootování jste v minimálním ale funkčním živém prostředí GNU/Linux s některými základními nástroji. Nyní musít připojit svůj běžný kořenový oddíl do /mnt.

```
# mount /dev/sdXY /mnt

```

Pokud používáte oddělený boot oddíl, nezapomeňte ho připojit také.

```
# mount /dev/sdXZ /mnt/boot

```

Novější jádra používají počáteční ramdisk (initrd) pro nastavení prostředí jádra. Když přeinstalováváte jádro, daný počáteční ramdisk bude pomocí mkinitcpio vytvořen znovu. Jednou z dovedností mkinitcpio je autodetekce modulů jádra, které jsou vyžadovány pro spuštění vašeho počítače. Aby tato autodetekce pracovala, ve vašem chrootu musí být připojeny adresáře /dev, /sys a /proc:

```
# mount -t proc none /mnt/proc
# mount -t sysfs none /mnt/sys
# mount --bind /dev /mnt/dev

```

Nyní provedeme chroot do tohoto oddílu:

```
# chroot /mnt

```

### Návrat k předchozí verzi jádra

Pokud si ponecháváte stažené balíčky pacmana, můžete se lehce navrátit k předchozí verzi. Pokud jste si je neponechali, musíte si najít nějaký způsob, jak nyní na svůj systém dostanete předchozí verzi jádra.

Předpokládejme, že jste si předchozí verze ponechali. Nyní nainstalujeme tu poslední funkční.

```
# pacman -U /var/cache/pacman/pkg/kernel26-2.6.23.*xx-x*.pkg.tar.gz

```

Samozřejmě že si musíte tento řádek poupravit pro vlastní verzi jádra.

V opačném případě se pro balíček poohlédněte na instalačním CD. Například i686 CD verze 2008.06 obsahuje addons/core-pkgs/kernel26-2.6.25.6-1-i686.pkg.tar.gz.

## 2\. možnost: Ověřte konfiguraci zavaděče

Další možnost je chyba v konfiguraci zavaděče operačního systému. Například změna oddílů na pevném disku může zapříčinit změnu pořadí oddílů. Uživatelé GRUBu si mohou vzpomenout, zda se změna oddílů stala nedávno a ověřit si, že řádky *root* a *kernel* skutečně odpovídají novému schéma oddílů.

## Restart

Nyní je ten čas restartovat a zjistit, zda úpravy systému zastavily paniku. Pokud funguje návrat ke starší verzi jádra, nezapomeňte se podívat na arch-newspage, abyste zjistili, co se v daném sestavení jádra nepovedlo.