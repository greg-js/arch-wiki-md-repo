## Contents

*   [1 Premessa](#Premessa)
*   [2 Specifiche hardware](#Specifiche_hardware)
*   [3 Preparazione](#Preparazione)
    *   [3.1 Creare un device usb avviabile](#Creare_un_device_usb_avviabile)
*   [4 Configurazione del sistema](#Configurazione_del_sistema)
    *   [4.1 Ethernet](#Ethernet)
    *   [4.2 Wireless](#Wireless)
    *   [4.3 Touchpad](#Touchpad)
    *   [4.4 Acpi](#Acpi)
        *   [4.4.1 Asus OSD](#Asus_OSD)
    *   [4.5 Audio](#Audio)
    *   [4.6 Webcam](#Webcam)
    *   [4.7 CPU frequency scaling](#CPU_frequency_scaling)
    *   [4.8 Limitare le scritture su SSD](#Limitare_le_scritture_su_SSD)
    *   [4.9 Fonts LCD](#Fonts_LCD)
*   [5 Collegamenti utili](#Collegamenti_utili)

# Premessa

È richiesta una buona conoscenza di Arch Linux e di GNU/Linux in generale. Conviene anche conoscere l'inglese ed avere un bel pò di pazienza.

Questa guida è adattabile anche al modello 901 e successivi, con hardware simile o possibilmente uguale.

# Specifiche hardware

```
   * CPU: 1.6GHz N270 Intel Atom
   * RAM: 1024 MB, DDR2 667 MHz
   * ports: 3x USB 2.0, VGA
   * LAN/ethernet: Atheros L1e 10/100 Mbit
   * WLAN: Wi-Fi 802.11 a/b/g
   * Webcam 0.3 Mpix
   * Card reader: SD, SDHC, MMC
   * touchpad: "Multi-touch" elantech
   * display: 1024x600 8.9"
   * weight: 0,99 kg
   * battery: Li-ion, 4 Hours, 4400mAh
   * SDD: 8GB
   * Graphics: Intel 945GME chipset

```

```
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev 03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
00:1b.0 Audio device: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 2 (rev 02)
00:1c.3 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 4 (rev 02)
00:1d.0 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #3 (rev 02)
00:1d.3 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #4 (rev 02)
00:1d.7 USB Controller: Intel Corporation 82801G (ICH7 Family) USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA IDE Controller (rev 02)
01:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
02:00.0 Ethernet controller: Atheros Communications Inc. AR242x 802.11abg Wireless PCI Express Adapter (rev 01)

```

# Preparazione

Prendete una pendrive o una SD e scaricate l’ultima l’immagine core di Arch.

Torrent:

```
[ftp://ftp.archlinux.org/iso/2009.02/archlinux-2009.02-core-i686.img.torrent](ftp://ftp.archlinux.org/iso/2009.02/archlinux-2009.02-core-i686.img.torrent)

```

Download:

```
wget -c [http://mi.mirror.garr.it/mirrors/archlinux/iso/2009.02/archlinux-2009.02-core-i686.img](http://mi.mirror.garr.it/mirrors/archlinux/iso/2009.02/archlinux-2009.02-core-i686.img)

```

## Creare un device usb avviabile

Quando l’avete scaricate andate in un terminale e digitate

```
fdisk -l

```

E individuate il device della pendrive (solitamente sdb o sdc)

Ora dovete eseguire questo semplicissimo comando per copiare l’immagine sulla pendrive

```
dd if=/percorso/immagine/arch.img of=/dev/sdb bs=1M

```

Cambiare percorso e device a seconda del risultato di fdisk.

# Configurazione del sistema

Installate il pacchetto laptop-mode-tools, alsa e il demone acpid

```
pacman -S laptop-mode-tools alsa-utils acpid

```

Editate il file /etc/rc.conf per apportare alcuni cambiamenti

```
nano /etc/rc.conf

```

Nella sezione MODULES aggiungete eeepc-laptop.

Nella sezione DAEMONS aggiungete acpid, alsa e laptop-mode.

Se non lo avete già fatto è necessario installare yaourt e sudo. Inoltre create un utente normale, senza privilegi di root.

## Ethernet

Driver incluso nel kernel.

## Wireless

Driver già incluso nel kernel.

## Touchpad

Funzionante sin da subito, senza xorg.conf. Installiamo synaptics, evdev e xorg.

```
pacman -S xf86-input-synaptics xf86-video-intel xf86-input-evdev xorg

```

## Acpi

Funzionante con i moduli del kernel.

### Asus OSD

Incluse nei moduli del kernel.

## Audio

Se non lo avete già precedentemente installato:

```
pacman -S alsa-utils

```

Eseguire il comando alsaconf da root:

```
alsaconf

```

Con alsamixer è possibile aggiustare i livelli del volume, per salvarli usare alsactl store (tutto da root).

## Webcam

Perfettamente funzionante.

## CPU frequency scaling

È possibile usare laptop-mode-tools oppure cpufrequtils, ma laptop-mode-tools fornisce molte più configurazioni per i portatili quindi è particolarmente consigliato.

_Laptop mode tools:_

Installare il pacchetto laptop-mode-tools

```
pacman -S laptop-mode-tools

```

In /etc/laptop-mode/ si trovano tutte le configurazioni disponibili, in maggior modo in /etc/laptop-mode/conf.d/cpufreq.conf è presente la configurazione per lo scaling della CPU.

Aggiungere in /etc/rc.conf il demone laptop-mode nella riga DAEMONS.

_Cpufrequtils:_

Installare il pacchetto cpufrequtils

```
pacman -S cpufrequtils

```

Con il comando cpufreq-info potete controllare la frequenza minima e massima dei processore, dopodichè modificate /etc/conf.d/cpufreq

```
nano /etc/conf.d/cpufreq

```

Inserire il governatore che si preferisce e settare la frequenza minima e massima rispettivamente a 800MHz e 1600MHz.

```
nano /etc/rc.conf

```

In /etc/rc.conf aggiungere nella riga DAEMONS cpufreq.

_Valido per qualsiasi scelta:_ Aggiungiamo in MODULES cpufreq_conservative, cpufreq_powersave o cpufreq_userspace in base a ciò che ci serve.

## Limitare le scritture su SSD

Editare il file /etc/fstab inserendo queste righe

```
nano /etc/fstab

```

```
 tmpfs      /tmp            tmpfs        defaults,size=50%           0    0

```

Notate che i valori possono essere cambiati a piacimento (50% è metà memoria RAM).. dato che quello è il limite che può assumere la cartella nella RAM (quindi non esagerate se volete evitare casini). Se il valore size non viene impostato viene comunque limitato a metà della vostra RAM.

Aggiungere anche l'opzione noatime a tutte le partizioni dell'SSD.

Modificare il file `/etc/sysctl.d/30-writeback.conf` e aggiungere:

```
 vm.dirty_writeback_centisecs = 1500

```

## Fonts LCD

Nei monitor LCD la resa dei caratteri può essere peggiore rispetto ai CRT (tubo catodico)

Se non siete soddisfatti e volete risolvere questo inconveniente agite in questo modo:

```
pacman -Rdcn cairo libxft fontconfig freetype2
yaourt -S cairo-ubuntu
ln -s /etc/fonts/conf.avail/10-autohint.conf /etc/fonts/conf.d/10-autohint.conf

```

Abbiamo così installato i pacchetti patchati alla ubuntu.

**ATTENZIONE**: eseguite questi comandi nella stessa sessione di X senò quando lo riavvierete non partirà e sarete costretti ad usare la riga di comando per aggiustare il sistema.

Ora configuriamoli.

```
gedit ~/.fonts.conf

```

e incolliamoci queste righe:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
 <match target="font" >
  <test compare="more" name="weight" >
   <const>medium</const>
  </test>
  <edit mode="assign" name="autohint" >
   <bool>false</bool>
  </edit>
 </match>
</fontconfig>

```

Ora in GNOME andate in Sistema > Preferenze > Aspetto | Tipi di carattere > Dettagli.. e impostiamo:

```
96 punti per pollice
Sfumatura Subpixel (LCD)
Approssimazione (Hinting) Media
Ordine subpixel RGB.

```

Ora se vogliamo modifichiamo anche i caratteri, io per esempio ho impostato i seguenti:

```
Applicazioni > Dejavu Sans Book 8
Documenti > Dejavu Sans Book 8
Scrivania > Dejavu Sans Book 8
Titolo finestre > Dejavu Sans Bold 8
Larghezza fissa > Dejavu Sans Mono Book 8

```

Se usate OpenOffice apritelo. Andate in Strumenti > Opzioni > Vista e modificate "Elimina effetto scalettatura" da 8 a 1 pixel.

Quando avete completato tutto riavviate X. Notate che potrebbe essere necessario modificare alcune impostazioni dei font in qualche programma.

# Collegamenti utili

Potete dare un'occhiata a questi wiki per informazioni più generali di Arch su Eee PC.

*   [Asus_Eee_PC](/index.php/Asus_Eee_PC "Asus Eee PC")
*   [Installing_Arch_Linux_on_the_Asus_EEE_PC](/index.php/Installing_Arch_Linux_on_the_Asus_EEE_PC "Installing Arch Linux on the Asus EEE PC")
*   [Asus_Eee_PC_901](/index.php/Asus_Eee_PC_901 "Asus Eee PC 901")
*   [[1]](http://ugaciaka.wordpress.com/2008/10/13/tmpfs-ramdisk-perfetta/)