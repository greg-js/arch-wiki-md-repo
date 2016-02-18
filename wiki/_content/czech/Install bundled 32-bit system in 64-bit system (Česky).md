Instalace Arch64 svázaná s 32bit systémem

Tento článek je určený především pro ty, kdo opravdu potřebují používat 32bitové aplikace. Protože Arch64 se snaží být čistě 64bitovou distribucí, bývá občas problém sehnat knihovny pro 32bit emulaci. Tento postup vytvoří čistě 32bitovou instalaci ArchLinuxu ve vaší stávající 64bitové.

## Contents

*   [1 Instalace základních balíčků](#Instalace_z.C3.A1kladn.C3.ADch_bal.C3.AD.C4.8Dk.C5.AF)
*   [2 /etc/rc.d/arch32 rc skript](#.2Fetc.2Frc.d.2Farch32_rc_skript)
*   [3 Konfigurace](#Konfigurace)
*   [4 Spouštění 32bitových aplikací z 64bitového systému](#Spou.C5.A1t.C4.9Bn.C3.AD_32bitov.C3.BDch_aplikac.C3.AD_z_64bitov.C3.A9ho_syst.C3.A9mu)
    *   [4.1 Stáhněte a nainstalujte schroot](#St.C3.A1hn.C4.9Bte_a_nainstalujte_schroot)
    *   [4.2 Nastavení](#Nastaven.C3.AD)
    *   [4.3 Spuštění aplikací](#Spu.C5.A1t.C4.9Bn.C3.AD_aplikac.C3.AD)
    *   [4.4 Zvuk](#Zvuk)

## Instalace základních balíčků

Nejprve vytvoříme místo, kam stahovat a instalovat balíčky:

```
mkdir /opt/arch32

```

V libovolném editoru (třeba *nano*) upravte soubor */etc/pacman.d/core*, případně (u pacmana>=3.1) */etc/pacman.d/mirrorlist*:

```
nano /etc/pacman.d/core
nano /etc/pacman.d/mirrorlist

```

V těchto souborech nahraďte *x86_64* za *i686* (raději u více serverů, ale teoreticky stačí i jen jeden)

**Nezapomeňte nakonec vrátit tyto soubory do původního stavu!!!**

Dále je vhodné vytvořit pro 32bitovou instalaci samostatný log. **Opět nezapomeňte po skončení tohoto návodu následující změnu zase vrátit zpátky.**

```
nano /etc/pacman.conf

```

Upravte položku 'LogFile' podle potřeby (například */var/log/pacman_32.log*).

Aktuální verze pacmana vyžaduje vytvořit adresářovou strukturu pro databázi:

```
mkdir -p /opt/arch32/var/lib/pacman

```

Nyní proveďte aktualizaci repozitářů:

```
pacman --root /opt/arch32 -Sy

```

A teď už můžeme nainstalovat základní balíčky (pokud nehodláte v chrootu kompilovat balíčky, můžete skupinu *base-devel* vynechat):

```
pacman --root /opt/arch32 -S base base-devel

```

**Nyní vraťte zpátky změny v nastavení pacmana - /etc/pacman.d/core resp. /etc/pacman.d/mirrorlist a /etc/pacman.conf**.

## /etc/rc.d/arch32 rc skript

Pro spuštění 32bitového prostředí při bootování vytvořte v /etc/rc.d skript a nazvěte ho *arch32*:

```
nano /etc/rc.d/arch32

```

```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

case $1 in
    start)
        stat_busy "Starting Arch32 chroot"
        mount --bind /proc /opt/arch32/proc
        mount --bind /proc/bus/usb /opt/arch32/proc/bus/usb
        mount --bind /dev /opt/arch32/dev
        mount --bind /dev/pts /opt/arch32/dev/pts
        mount --bind /dev/shm /opt/arch32/dev/shm
        mount --bind /sys /opt/arch32/sys
        mount --bind /tmp /opt/arch32/tmp
        mount --bind /home /opt/arch32/home
        add_daemon arch32
        stat_done
        ;;
    stop)
        stat_busy "Stopping Arch32 chroot"
        umount /opt/arch32/proc/bus/usb
        umount /opt/arch32/proc
        umount /opt/arch32/dev/pts
        umount /opt/arch32/dev/shm
        umount /opt/arch32/dev
        umount /opt/arch32/sys
        umount /opt/arch32/tmp
        umount /opt/arch32/home
        rm_daemon arch32
        stat_done
        ;;
    restart)
        $0 stop
        sleep 1
        $0 start
        ;;
    *)
        echo "usage: $0 {start|stop|restart}"
esac
exit 0

```

Ještě udělejte soubor spustitelným:

```
chmod +x /etc/rc.d/arch32

```

A přidejte daemona do */etc/rc.conf*:

```
DAEMONS=(syslog-ng network netfs crond arch32 gdm)

```

## Konfigurace

Nejprve je nutné zkopírovat pár souborů s nastavením

```
cd /opt/arch32/etc

cp /etc/passwd* ./
cp /etc/shadow* ./
cp /etc/group* ./
cp /etc/rc.conf ./
ln /etc/resolv.conf ./
cp -a /etc/localtime ./
cp /etc/locale.gen ./
cp /etc/profile.d/locale.sh profile.d
cp /etc/mtab ./

```

Abychom zabránili kolizi binárek, je nutné upravit ještě nastavení 32bitového pacmana. Adresářovou strukturu pro pacmana není nutné vytvářet, tu si pacman udělá sám.

```
nano /opt/arch32/etc/pacman.conf
[options]
LogFile     = /var/log/pacman_32.log
DBPath      = /var/lib/pacman_32
CacheDir    = /var/cache/pacman_32

```

a následně:

```
mv /opt/arch32/var/lib/pacman /opt/arch32/var/lib/pacman_32
mv /opt/arch32/var/cache/pacman /opt/arch32/var/cache/pacman_32

```

Nyní můžete chrootovat do 32bitového systému (jako root):

```
/etc/rc.d/arch32 start
xhost +
chroot /opt/arch32

```

Ještě poslední doladění:

```
/usr/sbin/locale-gen
pacman -S ttf-bitstream-vera ttf-ms-fonts

```

Samozřejmě můžete nainstalovat libovolné jiné fonty, ale je nutné nainstaloval alespoň jedno písmo, jinak nebudou fungovat grafické aplikace.

Nyní můžete nainstalovat libovolné aplikace podle potřeby:

```
pacman -S acroread opera
pacman -S mozilla-firefox
pacman -S libxmu flashplugin
pacman -S mplayer-plugin

```

Pokud ještě chcete získat nějaké do místo navíc, můžete smazat stažené balíčky:

```
pacman -Scc

```

A ještě můžete odstranit pár drobností. **Nezapomeňte, že /home adresář je provázaný s vaším normálním /home adresářem! Dávejte pozor na to co mažete!!!**

```
rmdir /home/ftp

```

```
pacman -Rd mkinitcpio

```

## Spouštění 32bitových aplikací z 64bitového systému

### Stáhněte a nainstalujte schroot

Nainstalujte *schroot* z repozitáře *community*:

```
pacman -S schroot

```

### Nastavení

Schroot již obsahuje připravené nastavení pro Arch32 chroot. Pouze zkontrolujte, že nastavení v /etc/schroot/schroot.conf v sekci [Arch32] odpovídá vašemu skutečnému nastavení.

### Spuštění aplikací

Pro spuštění 32bitové aplikace instalované v chrootu použijte:

```
schroot -p opera -notrayicon

```

Tento příklad spustí Operu, instalovanou v 32bitovém chrootu bez ikony v tray.

### Zvuk

Nejpoužívanější aplikací v 32 bitovém systému je flash, například pro YouTube. Aby flash ve Firefoxu přehrával hudbu, otevřete terminál a chrootujte do 32bitového systému:

```
chroot /opt/arch32

```

Odtud nainstalujte *alsa-oss*:

```
pacman -S alsa-oss

```

Potom napište:

```
export FIREFOX_DSP="aoss"

```

A spusťte Firefox