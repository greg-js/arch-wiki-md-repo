Následuje seznam často kladených dotazů k 64-bitovému Archlinuxu (Arch64)

## Contents

*   [1 Jak nainstaluji Arch64?](#Jak_nainstaluji_Arch64?)
*   [2 Do jaké míry je Arch64 hotový? Budu v něm mít všechny své balíčky z 32-bitového Archlinuxu?](#Do_jaké_míry_je_Arch64_hotový?_Budu_v_něm_mít_všechny_své_balíčky_z_32-bitového_Archlinuxu?)
*   [3 Znamená 64-bitová architektura znatelné zvýšení rychlosti prostředí?](#Znamená_64-bitová_architektura_znatelné_zvýšení_rychlosti_prostředí?)
*   [4 Jak mohu nahlásit chybu?](#Jak_mohu_nahlásit_chybu?)
*   [5 Co mi v Arch64 bude scházet?](#Co_mi_v_Arch64_bude_scházet?)
*   [6 Můžu v Arch64 sestavovat 32-bitové balíčky pro i686?](#Můžu_v_Arch64_sestavovat_32-bitové_balíčky_pro_i686?)
*   [7 Můžu v Arch64 provozovat 32-bitové aplikace?](#Můžu_v_Arch64_provozovat_32-bitové_aplikace?)
*   [8 Můžu aktualizovat/přepnout svůj systém z i686 na x86_64 bez přeinstalace?](#Můžu_aktualizovat/přepnout_svůj_systém_z_i686_na_x86_64_bez_přeinstalace?)

## Jak nainstaluji Arch64?

Stačí použít naše [oficiální instalační ISO CD](https://www.archlinux.org/download/).

## Do jaké míry je Arch64 hotový? Budu v něm mít všechny své balíčky z 32-bitového Archlinuxu?

Repositáře Core+Extra už jsou portované a skoro všechny balíčky aktuální (jsou pro představu vydávány jen hodiny, maximálně několik dní po vydání 32-bitových). Snažíme se portovat i repositář Community.

Arch64 je již teď plně připravený pro každodenní použití na serveru i na desktopu.

## Znamená 64-bitová architektura znatelné zvýšení rychlosti prostředí?

Pro aplikace, které využívají 64-bitové registry CPU (velké databáze atp.) to platí ve většině případů. Některé multimediální aplikace poběží také znatelně rychleji. Pokud víte o aplikaci, o které je známo, že je rychlejší, když používá rozšíření SSE3, můžete si balíček vytvořit sami. My kompilujeme *pouze* s podporou SSE2 (from march=x86_64) a -O2 optimalizacemi. Pro další informace si přečtěte [http://forums.gentoo.org/viewtopic.php?t=221045](http://forums.gentoo.org/viewtopic.php?t=221045) nebo [http://www.thejemreport.com/mambo/content/view/74/74/](http://www.thejemreport.com/mambo/content/view/74/74/) .

## Jak mohu nahlásit chybu?

Jednoduše použijte flyspray, ale (pokud si myslíte, že je problém způsobený portováním na 64-bitovou architekturu) v poli pro architekturu vyberte x86_64.

## Co mi v Arch64 bude scházet?

O následujících aplikacích je známé, že nejsou 64-bitově kompatibilní:

*   Aplikace s uzavřenými zdrojovými kódy jako TeamSpeak a některé hry
*   Balíčky, které obsahují kód v 32-bitovém x86 assembleru (některé emulátory jako zsnes a syslinux), i když alespoň zsnes je dostupný jako 32-bitová binárka pro Arch64 v [AUR](/index.php/ArchLinux_User-community_Repository_(AUR)_(%C4%8Cesky) "ArchLinux User-community Repository (AUR) (Česky)").
*   [Wine](/index.php/Wine "Wine") (na x86_64 portu se pracuje)
*   Skype je možné používat a je dostupný jako 32bit binárka na [AUR](/index.php/ArchLinux_User-community_Repository_(AUR)_(%C4%8Cesky) "ArchLinux User-community Repository (AUR) (Česky)").

Téměř všechno ostatní by mělo být přenositelné. Pokud vám v našem portu schází některý balíček z Arch32 a víte, že se zkompiluje na x86_64 (např. jste ho našli v jiné 64-bitové distribuci bez použití 32-bitových knihoven), kontaktujte vývojáře.

## Můžu v Arch64 sestavovat 32-bitové balíčky pro i686?

Ano. Potřebujete funkční i686 chroot (jako rychlý způsob jeho instalace uvnitř Arch64 je doporučována instalace s i686 ISO obrazem "quickinstall", případně viz [32bit chroot](/index.php/32bit_chroot_(%C4%8Cesky) "32bit chroot (Česky)")). Nainstalujte balíček "linux32", aby se chroot choval jako opravdový 32-bitový systém. Poté (pod rootem) použijte tento skript pro přihlášení do chroot prostředí:

```
#!/bin/bash
mount --bind /dev /path-to-your-chroot/dev
mount --bind /dev/pts /path-to-your-chroot/dev/pts
mount --bind /dev/shm /path-to-your-chroot/dev/shm
mount -t proc none /path-to-your-chroot/proc
mount -t sysfs none /path-to-your-chroot/sys
linux32 chroot /path-to-your-chroot

```

Pokud necháváte zdrojové kódy na hostitelském x86_64 systému, můžete přidat

```
"mount --bind /cesta-k-zdrojovým-kódům /cesta-k-chrootu/cesta-k-zdrojovým-kódům" 

```

aby zdrojové kódy pro sestavení balíčků byly sdíleny mezi hostitelským a chrootovaným systémem.

## Můžu v Arch64 provozovat 32-bitové aplikace?

Ano!

1.  Můžete nainstalovat knihovny lib32-* z repozitáře Community, takže váš systém bude obsahovat dvě verze knihoven.
2.  Nebo můžete vytvořit chroot s 32-bitovým systémem:

Nabootujte do Arch64, spusťte X server, otevřete terminál.

```
$ xhost +local:
$ su
# mount /dev/sda1 /mnt/arch32
# mount --bind /proc /mnt/arch32/proc
# chroot /mnt/arch32
# su <vaše-32bitové-uživatelské-jméno>
$ /usr/bin/příkaz-jaký-chcete  # nebo např.: /opt/mozilla/bin/firefox

```

Některé 32-bitové aplikace (třeba OpenOffice) mohou vyžadovat dodatečné bindování. Aby bylo zajištěno vše, co potřebujete pro 32-bitové aplikace, můžete do rc.local vložit následující řádky (za předpokladu, že je /mnt/arch32 je připojeno v fstab):

```
mount --bind /dev /mnt/arch32/dev
mount --bind /dev/pts /mnt/arch32/dev/pts
mount --bind /dev/shm /mnt/arch32/dev/shm
mount --bind /proc /mnt/arch32/proc
mount --bind /proc/bus/usb /mnt/arch32/proc/bus/usb
mount --bind /sys /mnt/arch32/sys
mount --bind /tmp /mnt/arch32/tmp
# zakomentujte následující řádek pokud nepoužíváte stejný domovský adresář
mount --bind /home /mnt/arch32/home

```

Poté můžete napsat do terminálu:

```
$ xhost +localhost
$ sudo chroot /mnt/arch32 su <vaše-32bitové-uživatelské-jméno> /opt/openoffice/program/soffice

```

## Můžu aktualizovat/přepnout svůj systém z i686 na x86_64 bez přeinstalace?

Ne. Nicméně můžete spustit systém s instalačním CD Arch64, připojit disk, zazálohovat vše, co chcete ponechat a není to 32-bitová binárka (např.: /home, /etc) a začít s instalací.