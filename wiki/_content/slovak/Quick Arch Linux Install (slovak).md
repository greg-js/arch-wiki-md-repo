Tento dokument vás prevedie základnou inštaláciou Archlinuxu. Je založený na inštalačných skriptoch verzie 0.6 (widget).

## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Nevyhnutné veci](#Nevyhnutn.C3.A9_veci)
*   [3 Inštalácia z Arch-CD](#In.C5.A1tal.C3.A1cia_z_Arch-CD)
    *   [3.1 Vytvoriť partície na harddisku](#Vytvori.C5.A5_part.C3.ADcie_na_harddisku)
    *   [3.2 Nastaviť body pripojenia](#Nastavi.C5.A5_body_pripojenia)
    *   [3.3 Vybrať balíčky](#Vybra.C5.A5_bal.C3.AD.C4.8Dky)
    *   [3.4 Inštalovať balíčky](#In.C5.A1talova.C5.A5_bal.C3.AD.C4.8Dky)
    *   [3.5 Inštalovať jadro](#In.C5.A1talova.C5.A5_jadro)
    *   [3.6 Upraviť konfiguračné súbory](#Upravi.C5.A5_konfigura.C4.8Dn.C3.A9_s.C3.BAbory)
    *   [3.7 Inštalovať bootloader](#In.C5.A1talova.C5.A5_bootloader)
    *   [3.8 Pripravený reštartovať](#Pripraven.C3.BD_re.C5.A1tartova.C5.A5)
*   [4 Alternatívne metódy inštalácie](#Alternat.C3.ADvne_met.C3.B3dy_in.C5.A1tal.C3.A1cie)
*   [5 Prvé kroky v Archu](#Prv.C3.A9_kroky_v_Archu)

## Úvod

Toto je rýchle prevedenie inštaláciou pre tých, ktorí ešte nevedia čo je to Arch a čo všetko dokáže. Je napísané hlavne pre tých, ktorí už majú na svojom harddisku existujúcu partíciu Windowsu a chcú si nainštalovať Arch linux bez narušenia inštalácie Windowsu.

Tento sprievodca je pre "normálny" hardware, nič špeciálneho (ako napr. scsi) nie je v tomto dokumente obsiahnuté.

Predpokladá sa, že Windows existuje na prvej partícii harddisku, inak ho grub nebude vedieť nájsť.

## Nevyhnutné veci

*   CD so základnou inštaláciou Archlinuxu (Base-Installation-CD) alebo CD s plnou inštaláciou (Full-Installation-CD). Stiahnite si [odtiaľ](https://www.archlinux.org/download.php).
*   Buď jeden voľný harddisk alebo voľné miesto na jednej partícii. Toto voľné miesto musíte oddeliť od existujúcej partície vo windowse s nástrojmi na úpravu partícií (ako napr. partition magic).

## Inštalácia z Arch-CD

*   Vložte CD do vašej mechaniky, reštartujte a skontrolujte, či váš BIOS bootuje najprv z CD-ROM mechaniky.
*   Teraz by to malo vyzerať takto:

[http://home.arcor.de/Langeland/1.png](http://home.arcor.de/Langeland/1.png) Východzia bootovacia obrazovka Archu

*   Stlačte `Enter`
*   Po skončení bootovacieho procesu, napíšte:

```
/arch/setup

```

Najprv budete inštalovať z CD, takže sieťové ovládače nie sú nutné.

Objaví sa Hlavné Menu:

[http://home.arcor.de/Langeland/6.png](http://home.arcor.de/Langeland/6.png) Hlavné Menu

### Vytvoriť partície na harddisku

Ak máte úplne prázdny harddisk, môžete tieto kroky preskočiť a zvoliť Auto-Partitioning. Prosím majte na pamäti, že týmto vymažete všetky partície z vášho harddisku! Ak niektoré partície chcete ponechať na vašom harddisku, postupujte podľa nasledujúcich krokov:

*   Zvoľte Prepare Hard-Drive.
*   Vyberte Partition Hard-Drive.
*   Zvoľte the Disc you want Arch-Linux to be installed on.
*   Otvorí sa cfdisk-program na úpravu partícií a môžete vytvoriť partície. U základnej inštalácie Archu (Base-Installation) sú potrebné aspoň dve partície:

```
 * jedna swap partícia
 * jedna dátová partícia

```

*   V tomto okamihu displej môže vyzerať asi takto (ak máte ntfs-partíciu pre windows):

[http://home.arcor.de/Langeland/9.png](http://home.arcor.de/Langeland/9.png) cfdisk

*   Nijakým spôsobom sa nedotknite ntfs (alebo vfat) partície, lebo inak môžete stratiť Windows.
*   Typ swap partície by sa mal nastaviť zadaním typu partície 82
*   Ak chcete opustiť cfdisk bez uloženia zmien, tak stlačte quit, inak stlačte write.
*   Po použití cfdisk-u by to malo vyzerať takto:

[http://home.arcor.de/Langeland/10.png](http://home.arcor.de/Langeland/10.png) Usporiadanie partícií

### Nastaviť body pripojenia

*   Zvoľte bod 3: Set Filesystem Mountpoints
*   Zvoľte partíciu ktorú ste označili ako swap
*   Zvoľte tú druhú partíciu pre systém (ktorá bude pripojená ako /)
*   Zvoľte systém súborov ext3
*   Zvoľte DONE !!

*Tento posledný krok je veľmi dôležitý, mnoho ľudí tento krok vynechá, ale žiadna činnosť sa nevykoná, kým nezvolíte DONE - ak to neurobíte, bude sa zdať že inštalácia funguje, ale žiadne súbory sa nenainštalujú*

### Vybrať balíčky

*   Zvoľte CD
*   Teraz by to malo vyzerať takto:

[http://home.arcor.de/Langeland/11.png](http://home.arcor.de/Langeland/11.png) Kategórie balíčkov

*   Nateraz by ste si mali vybrať len základné (base) a editory (editors).
*   Zrejme chcete zvoliť všetky balíčky v daných kategóriách ako východzie
*   Len stlačte OK.

### Inštalovať balíčky

*   Toto je dosť jednoduché: Stačí stlačiť install packages, potom ok a všetko sa skopíruje z CD na harddisk.

### Inštalovať jadro

*   Pokiaľ viete, že nemáte iný hardware, vyberte 2.6 IDE.

### Upraviť konfiguračné súbory

*   Vyberte nano na úpravu súborov

Ak chcete zmeniť layout klávesnice, **musíte upraviť súbor rc.conf**. Napríklad sk je slovenská.

*   nano je ľahké na pochopenie: Ctrl-o uloží súbor, Ctrl-x uloží súbor a opustí nano.
*   Zmeňte riadok s `keymap us` na `keymap sk`

**Musíte upraviť** menu.lst*.

*   Tu môžete vytvoriť váš bootloader. V ňom môžete prepínať medzi windowsom a linuxom.
*   Uvidíte súbor ako je tento:

[http://home.arcor.de/Langeland/13.png](http://home.arcor.de/Langeland/13.png) Menu.lst

*   Všetko by malo byť nastavené správne na bootovanie do archu, už len stačí pridať nasledujúce riadky na koniec, aby ste mali možnosť bootovať windows:

```
title Windows
rootnoverify (hd0,0)
chainloader +1

```

Stlačte Ctrl-O, Ctrl-X a všetko je uložené.

### Inštalovať bootloader

*   Zvoľte grub.
*   Vyberte položku na vrchu zoznamu.

### Pripravený reštartovať

*   Opustite hlavné menu, napíšte reboot a počítač by mal reštartovať.
*   Vyberte CD von z mechaniky.
*   Môžete si vybrať medzi windowsom a archom, prednastavený je arch.

## Alternatívne metódy inštalácie

*   [Fast Arch Install from existing Linux System](/index.php/Fast_Arch_Install_from_existing_Linux_System "Fast Arch Install from existing Linux System")
*   [The Official Arch Linux Installation Guide](https://www.archlinux.org/docs/en/guide/install/arch-install-guide.html)

## Prvé kroky v Archu

*   Prihláste sa ako root.
*   Vykonajte príkaz `passwd` aby ste nastavili pre roota heslo.

```
# passwd

```

*   Pridajte používateľa. Môžete využiť skript adduser. Váš používateľ by mal byť v skupinách users, audio a optical.

```
# adduser

```

Teraz je čas spojazdniť váš internet a začať inštalovať balíčky s Pacman-om. Užite si!