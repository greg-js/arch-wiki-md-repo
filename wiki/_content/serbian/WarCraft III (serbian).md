## Contents

*   [1 Увoд](#.D0.A3.D0.B2o.D0.B4)
*   [2 Instaliranje Wine-a](#Instaliranje_Wine-a)
*   [3 Podesavanje Wine-a](#Podesavanje_Wine-a)
    *   [3.1 Windows verzija](#Windows_verzija)
    *   [3.2 Zvuk](#Zvuk)
    *   [3.3 Uredjaji](#Uredjaji)
*   [4 Instalacija](#Instalacija)
    *   [4.1 Instaliranje Warcraft III: The Reign of Chaos](#Instaliranje_Warcraft_III:_The_Reign_of_Chaos)
    *   [4.2 Instaliranje Warcraft III: The Frozen Throne-a](#Instaliranje_Warcraft_III:_The_Frozen_Throne-a)
    *   [4.3 Osvezavanje na najskoriju verziju](#Osvezavanje_na_najskoriju_verziju)
*   [5 Trikovi nakon instalacije](#Trikovi_nakon_instalacije)
    *   [5.1 Onemogucavanje intro filmova](#Onemogucavanje_intro_filmova)
    *   [5.2 Rezolucija za siroke monitore (widescreen)](#Rezolucija_za_siroke_monitore_.28widescreen.29)
    *   [5.3 Alt kombinacija tastera](#Alt_kombinacija_tastera)
        *   [5.3.1 GNOME](#GNOME)
        *   [5.3.2 KDE](#KDE)
*   [6 Pokretanje WarCraft-a III](#Pokretanje_WarCraft-a_III)
    *   [6.1 WarCraft III: The Reign of Chaos](#WarCraft_III:_The_Reign_of_Chaos)
    *   [6.2 WarCraft III: The Frozen Throne](#WarCraft_III:_The_Frozen_Throne)

## Увoд

Warcraft III je strateska igra u realnom vremenu napravljena od strane Blizzard Entertainment-a. Ovaj clanak ce opisati kako da ga instalirate i pokrecete njegov dodatak, The Frozen Throne, na Arch Linux-u koristeci [Wine](/index.php/Wine "Wine"). WarCraft III se moze pokretati sa punom OpenGL podrskom.

## Instaliranje Wine-a

Wine je dostupan u [extra] repozitorijumu:

```
pacman -S wine

```

Ako vam treba dalja pomoc, proverite [Wine](/index.php/Wine "Wine") clanak. Takodje izvrsite 'winecfg' komandu i podesite nekoliko opcija prema vasim potrebama pre pokretanja instalacionog CD-a. WarCraft III specificna Wine verzija postoji u AUR-u, i to oba stabilna verzija i verzija u razvoju. Pogledajte [ovde](https://aur.archlinux.org/packages.php?ID=33231) i [ovde](https://aur.archlinux.org/packages.php?ID=27298) za vise informacija.

## Podesavanje Wine-a

Sada cemo objasniti kako da podesite Wine pre instaliranja WarCraft-a III i Frozen Throne-a.

### Windows verzija

Da bi omogucili da zastita za kopiranje radi pod Wine-om, morate da podesite vasu Windows verziju na 2000 ili XP.

### Zvuk

Oba [OSS](/index.php/OSS "OSS") i [ALSA](/index.php/ALSA "ALSA") rade. Ako imate problema sa ALSA-om, mozete da predjete na OSS. Medjutim, postoji mogucnost da OSS pravi zastoje svake tri sekunde pa iz tog razloga nije preporucljiv za upotrebu.

### Uredjaji

Da bi zastita od kopiranja radila, morate da dodate CD-ROM uredjaj: Dodajte uredjaj, podesite stazu na /media/cdrom (ili na ono sto koristite kada mountujete CD) i promenite tip uredjaja na "CD-ROM".

## Instalacija

Sledeci proces ce detaljno objasniti kako da instalirate WarCraft III i ekspanziju The Frozen Throne, i na kraju cemo izvrsiti apdejtovanje na najskoriju verziju.

### Instaliranje Warcraft III: The Reign of Chaos

Ovo je krajnje jednostavno. **NEMOJTE** da koristite krekovanu verziju ove igrice.

*   Stavite CD you jedinicu i mountujte je (ili dozvolite masini da sama mountuje ako je tako podesena).
*   Otvorite terminal i udjite u direktorijum CD-a.
*   Izvrsite

```
wine install.exe

```

*   Pratite dijaloske boksove instalacije i unesite vas CD kljuc kad vas upita za njega.
*   Ne zaboravite da napustite direktorijum jer mozete da imate problema sa izbacivanjem CD-a iz racunara.

### Instaliranje Warcraft III: The Frozen Throne-a

Pratite istu proceduru kao gore i koristite CD-a od Frozen Throne-a umesto.

### Osvezavanje na najskoriju verziju

Mozete da probate da osvezite preko Battle.net-a ili upotrebom oficijalne zakrpe. U prvom resenju jednostavno pritisnite Battle.net dugme u glavnom meniju nakon sto je igra startovala. Uverite se da ste procitali savete za nakon instalacije pre nego sto pokrenete WarCraft III po prvi put. Ako zelite da patch-ujete bez da ste konektovani na internet, pratite sledece korake:

*   Pogledajte [ovde](http://us.blizzard.com/support/article.xml?articleId=20673) za zakrpu.
*   Preuzmite najskoriji patch i sacuvajte ga u direktorijumu u koji ste instalirali Warcraft III.
*   Otvorite terminal, predjite u taj direktorijum i pokrenite zakrpu sa:

```
wine <patchname>.exe

```

Ako imate zakrpljenu verziju 1.22 ili vise, ne treba vam vise CD da bi ste pokrenuli igru.

## Trikovi nakon instalacije

Postoje neke stvari koje bi trebali da podesite pre pokretanja Warcrafta po prvi put jer mogu biti uzrok nekim problemima. Ako neki od sledecih registarskih kljuceva ili vrednosti ne postoje, jednostavno ih napravite.

### Onemogucavanje intro filmova

Filmovi se ne prikazuju ispravno i ne mogu se prekinuti. Zbog toga cemo ih podesiti kao da su vec vidjeni.

*   Otvorite terminal i izvrsite komandu

```
regedit

```

*   Idite na

```
HKEY_CURRENT_USER\Software\Blizzard Entertainment\Warcraft III\Misc

```

*   Podesite "seenintromovie" to "1".

### Rezolucija za siroke monitore (widescreen)

Warcraft III ne podrzava rezolucije za siroke ekrane. Ako zelite da koriste tu rezoluciju morate da je podesite rucno u registru. Imajte na umu da cete izgubiti podesavanje ako podesite novu rezoluciju u opcijama u samom Warcraft-u jer ce to prepisati rucna podesavanja u registru.

*   Otvorite terminal i izvrsite

```
regedit

```

*   Idite na

```
HKEY_CURRENT_USER\Software\Blizzard Entertainment\Warcraft III\Video

```

*   Podesite "resheigth" i "reswidth" prema vasoj zelji. Imate mogucnost da unesete decimalne i heksadecimalne vrednosti. Najzgodnije je uneti decimalnu vrednost.

### Alt kombinacija tastera

Ako volite da koristite [Alt] + levi klik za signale po mini mapi i koristite [KDE](/index.php/KDE "KDE") ili [GNOME](/index.php/GNOME "GNOME") primeticete da ova funkcija ne radi zbog precica na tastaturi sa [Alt] koje vase desktop okruzenje koristi.

#### GNOME

Opcija za promenu ove precice se nalazi u *System > Preferences > Windows*.

#### KDE

Udjite u KDE kontrolni centar, prosirite Desktop, kliknite na behavior, zatim kliknite na window actions tab. Mozete da iskljucite alt kombinacije tastera. Ako zelite napravite podesavanja specificna za zasebne prozore, kliknite na window specific settings pod window behavior na strani.

## Pokretanje WarCraft-a III

Sada mozete da pokrenete Warcraft III. Mozete da proverite da li vam je instaler napravio ikonu za startovanje u vasem meniju za aplikacije. Ako jeste, mozete da je upotrebite. Ako imate problema, proverite komandu za startovanje Warcraft-a III. Staza do vaseg Warcraft III direktorijuma moze varirati u zavisnosti od vaseg wine direktorijuma i instalacione lokacije Warcraft-a III.

#### WarCraft III: The Reign of Chaos

```
wine ~/.wine/drive_c/Program\ Files/Warcraft\ III/war3.exe -opengl

```

#### WarCraft III: The Frozen Throne

```
wine ~/.wine/drive_c/Program\ Files/Warcraft\ III/Frozen\ Throne.exe -opengl

```

Ne treba vam -opengl parametar ako vam je Direcd3D renderovanje dovoljno brzo. Ovo morate sami da istestirate i zakljucite.