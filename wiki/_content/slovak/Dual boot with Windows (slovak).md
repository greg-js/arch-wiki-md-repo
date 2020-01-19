## Windows a Arch - duálne bootovanie

V tomto príklade, nainštalujeme najprv Windows, a potom súčasne GRUB boot-loader s Arch, aby sme povolili duálne bootovanie.

Inštalácia bude štandardná, ale je tu pár vecí, na ktoré treba pamätať:

1\. Musíme použiť logické partície z vašich súčasných partícií, pretože naraz súčasne môžu byť iba 4 primárne partície na disk.

2\. Zapamätajte si ako sa zapisujú partície s číslami: "sda1, sda2... sda8", poznamenajte si, ktorá partícia patrí ktorému číslu. Napríklad:

	sda1 

	Windows - 30GB bude postačujúce. Veľa nových hier prekračujúcich 10GB, si vyžaduje ďalšie miesto.

	sda2 

	`/boot` - 100MB je dosť (optimálne)

	sda3 

	`/` - okolo 25GB je vhodné

	sda4 

	swap - medzi 1024MB a 4096MB (optimálne)

	sda5 

	`/home` - použiť zvyšok miesta na disku (optimálne)

Je dôležité si poznamenať, že 1024 cylinder obmedzuje staršie BIOSy. To znamená, že BIOS nemôže pristupovať k dátam za hranicou 1024-ho cylindra (okolo 8.5GB), takže /boot partícia musí byť 8.5GB (miesto pred Windows partíciou). [GParted LiveCD](http://gparted.sourceforge.net/livecd.php) alebo diskový rozdeľovací nástroj zo [SystemRescueCd](http://www.sysresccd.org/Main_Page) sú užitočné pre presúvanie a zmenu veľkosti partícií.

3\. Ak sa inštaluje GRUB, musíte si nastaviť `/boot/grub/menu.lst`), a **uistiť sa, že GRUB sa inštaluje na `/boot` (alebo root (`/`) ak nevytvoríte oddelenú partíciu pre `/boot`)**. *Inštalovaním GRUB na vašu Windows partíciu, môžete sposobiť, že Windows nebude bootovať*. O tom hovoria 3 riadky na konci súboru, "chainloading" = zreťazenie pre bootovanie ostatných OS, môže byť všeobecne odkomentovaný, ak sledujete už hore popísaný postup, ktorý zahrnie windows bootovací bod pripojenia na hd0,0 alebo sda1\. Týmto dostanete niečo také:

**Note:** Uvedené inštrukcie sú v konflikte s inštaláciou GRUB zdokumentované v [GRUB#Všeobecné poznámky pre inštaláciu bootloadera](/index.php/GRUB#Všeobecné_poznámky_pre_inštaláciu_bootloadera "GRUB"), ktoré hovoria, že GRUB by sa mal inštalovať na MBR alebo na prvú partíciu rozpoznanú väčšinou typov BIOSov.

**Note:** Je tiež možné inštalovať GRUB na MBR (`/dev/sda`). Toto funguje najlepšie s Windows 7.

```
# Windows XP
title Windows XP
rootnoverify (hd0,0)
chainloader +1

```

Časti tejto položky sú nasledujúce:

	title Windows XP 

	Môže byť ľubovoľné, čo sa vám páči; zobrazí sa len na GRUB bootovacej obrazovke

	rootnoverify (hd0,0) 

	Pamätajte, že čísla partícií, ktoré sme popísali, sú zapísané ako čísla partície vašej windows partície. To nastaví windows boot ako root, napriek tomu, že GRUB to nemôže prečítať.

	chainloader +1 

	Zavolá Windows boot loadera, ktorý je stále v našom prípade v MBR, aj keď GRUB sám nemôže bootovať Windows.

*   Súbor je načítavaný zhora nadol, takže systém číta prvé will be the one to automatically boot, ak žiadne klávesy nie sú stlačené, počas bootovacej obrazovky GRUB.
*   GRUB používa indexovací systém od nuly, na popis diskov a partícií, ktoré sú rozličných konvencií, potom môžete použiť nasledovné:

```
Prvý disk, prvá partícia=sda1=hd0,0
Prvý disk, druhá partícia=sda2=hd0,1
Druhý disk, prvá partícia=sdb1=hd1,0

```