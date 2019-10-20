**Note:** Support for the ARM architecture is provided on [http://archlinuxarm.org/](http://archlinuxarm.org/)

	Raspberry Pi instalace

	První instalace [Raspberry](/index.php/Raspberry "Raspberry") Pi

	Programování

	[Qt5 Raspberry](/index.php?title=Qt5_Raspberry&action=edit&redlink=1 "Qt5 Raspberry (page does not exist)")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Úvod](#Úvod)
    *   [1.1 Co je to Raspberry Pi](#Co_je_to_Raspberry_Pi)
    *   [1.2 Instalace Arch Linux ARM](#Instalace_Arch_Linux_ARM)
        *   [1.2.1 Záloha karty](#Záloha_karty)
        *   [1.2.2 Instalace](#Instalace)
        *   [1.2.3 Home](#Home)
    *   [1.3 První operace](#První_operace)
        *   [1.3.1 Vzdálený SSH přístup](#Vzdálený_SSH_přístup)
        *   [1.3.2 Lokalizace](#Lokalizace)
        *   [1.3.3 Setting the time and date using OpenNTP](#Setting_the_time_and_date_using_OpenNTP)
        *   [1.3.4 Setting the time and date manually](#Setting_the_time_and_date_manually)
        *   [1.3.5 Změna root hesla](#Změna_root_hesla)
        *   [1.3.6 Přidání dalšího uživatele](#Přidání_dalšího_uživatele)
        *   [1.3.7 Sudo](#Sudo)
    *   [1.4 Instalace programů a prostředí](#Instalace_programů_a_prostředí)
        *   [1.4.1 Vyhledávání](#Vyhledávání)
        *   [1.4.2 Shell](#Shell)
        *   [1.4.3 Grafické prostředí](#Grafické_prostředí)

# Úvod

Jak zprovoznit Raspberry Pi (RPi). Stručný přehled.

## Co je to Raspberry Pi

Jedná se o minimalistický počítač postavený na architektuře armv6\. Více informací o tomto projektu naleznete na [http://www.raspberrypi.org/](http://www.raspberrypi.org/) a technickou specifikaci na: [http://cz.farnell.com/raspberry-pi?ref=lookahead](http://cz.farnell.com/raspberry-pi?ref=lookahead)

## Instalace Arch Linux ARM

V tomto návodu budou popsány pouze zásadní momenty odlišné pro RPi. Ostatní postupy jsou totožné s návody pro ArchLinux. Výjimku tvoří pouze základní inicializace a instalace zařízení. Dále se předpokládá, že konfigurace je prováděna na počítači s OS Archlinux.

### Záloha karty

Pokud vlastníte oficielní kartu poskytovanou k vašemu RPi, například [http://cz.farnell.com/samsung/raspberry-pi-prog-4gb-sdcard/memory-sdcard-raspberry-pi-4gb/dp/2113756](http://cz.farnell.com/samsung/raspberry-pi-prog-4gb-sdcard/memory-sdcard-raspberry-pi-4gb/dp/2113756) Doporučuji před instalací systému Arch Linux ARM provést zálohu pomocí `dd`. Cesta musí být zadána k zařízení `/dev/sdX` nikoliv k partišnu /dev/sdc1

```
# dd if=/path/to/sdX of=/home/$USER/backup_RPi.img

```

**Note:** Dochází k bitové kopii karty. Výsledný soubor bude stejně velký jako vaše karta.

**Note:** Karta nesmí být namontována.

**Warning:** Špatné zadání if a of prarmetru může vést k poškození vašich dat.

### Instalace

Instalace probíhá obdobně jako zálohování karty. Stáhněte si image soubor ze stránek Arch Linux ARM [http://archlinuxarm.org/platforms/armv6/raspberry-pi](http://archlinuxarm.org/platforms/armv6/raspberry-pi) Image nakopírujte pomocí `dd`.

```
#dd bs=1M if=/path/to/archlinux.img of=/dev/sdX

```

Po vložení karty do slotu vašeho PPi by měl nabootovat základní systém Arch Linux ARM.

### Home

Stažený obraz disku má přibližně 2GB z toho je /boot 94MB a / 1.8GB. Pokud jste použili větší kartu jak 2GB, tak doporučuji na zbytek karty připojit například /home (popřípadě /usr ...). Volný prostor je třeba naformátovat například pomocí [GParted](/index.php/GParted "GParted"). Při první možné příležitosti (po nabootování RPi nebo po namontování karty v počítači) je třeba upravit `/etc/fstab`

```
# sudo vim /etc/fstab

```

přidat například

```
/dev/mmcblk0p3  /home           ext4    defaults        0       0

```

## První operace

Oficielní postup naleznete zde: [http://archlinuxarm.org/support/guides/system/first-steps](http://archlinuxarm.org/support/guides/system/first-steps) Shrnutí:

### Vzdálený SSH přístup

Pokud nevyužijete HDMI výstup RPi a budete přistupovat k zařízení pomocí SSH platí následující. Root pasword je: `root`. Dopročuji provést výměnu klíčů [SSH keys](/index.php/SSH_keys "SSH keys").

```
~ ssh root@192.168.1.123 (Use Ip your RPi)

```

### Lokalizace

```
# vim /etc/locale.gen

```

odkomentovat `cs_CZ.UTF-8 UTF-8` a `cs_CZ ISO-8859-2`

vygenerování lokalizačních souborů

```
# locale-gen

```

### Setting the time and date using OpenNTP

dopnit

### Setting the time and date manually

doplnit

### Změna root hesla

Po prvním spuštění RPi je nastaveho root heslo na root. Je tedy nutná jeho změna. Provede se po mocí příkazu `passwd`

```
# passwd root

```

### Přidání dalšího uživatele

Pomocí `adduser` přidejte svého uživatele.

```
#adduser

```

### Sudo

Spustit `visudo`

```
# sudo visudo 

```

přidat řádek "UŽIVATEL ALL=(ALL) ALL" pod řádek root ALL=(ALL) ALL

## Instalace programů a prostředí

Následuje stručný přehled balíčků a základních postupů které by se při prvotním zpuštění RPi mohli hodit.

### Vyhledávání

K vyhledávání souborů a složek na disku slouží [mlocate](/index.php/Mlocate "Mlocate").

```
# pacman -S  mlocate

```

po instalaci je nutné obnovit databázi

```
# updatedb

```

### Shell

Pro práci doporučuji [zsh](/index.php/Zsh "Zsh").

```
# pacman -S zsh

```

spustit

```
$ chsh

```

a nastavit

```
/bin/zsh

```

### Grafické prostředí

Je potřeba nainstalovat X server [xorg](/index.php/Xorg "Xorg"):

```
# pacman -S xorg-server xorg-xinit xorg-server-utils xterm xorg-xinit

```

[mesa](/index.php?title=Mesa&action=edit&redlink=1 "Mesa (page does not exist)")

```
# pacman -S mesa

```

Ovladače grafické karty [xf-video](/index.php?title=Xf-video&action=edit&redlink=1 "Xf-video (page does not exist)"):

```
# pacman -Syf xf86-video-fbdev 

```

S čímž souvisí [gamin](/index.php/Gamin "Gamin") a [dbus](/index.php/Dbus "Dbus"):

```
# pacman -S gamin dbus

```

Grafické prostředí [LXDE](/index.php/LXDE "LXDE"):

```
# pacman lxde 

```

dále do souboru `~/.xinitrc` přidat následující řádek:

```
$ vim ~/.xinitrc  (v případě, že nejste root)

```

vložit

```
exec startlxde 

```

Spuštění LXDE prostředí:

```
startx

```