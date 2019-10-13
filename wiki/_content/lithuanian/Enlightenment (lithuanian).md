E17 yra Enlightenment (Švietimas) grafinės aplinkos Gamybos Leidimas Nr. 17 (DR17). Ši aplinka yra dar labai ankstyvoje stadijoje - nėra sulaukus net alpha versijos - todėl šiuo metu vyksta aktyvus jos vystymas. Nepaisant to, ji yra gana stabili ir nemažai vartotojų ją naudoja kasdieniam darbui.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 E17 Įdiegimas](#E17_Įdiegimas)
    *   [1.1 Iš bendruomeninio repozito (SVN paveikslai)](#Iš_bendruomeninio_repozito_(SVN_paveikslai))
    *   [1.2 Kompiliavimas ir pakavimas su ArchE17 skriptu](#Kompiliavimas_ir_pakavimas_su_ArchE17_skriptu)
*   [2 E17 Paleidimas](#E17_Paleidimas)
*   [3 Temų Įdiegimas](#Temų_Įdiegimas)
*   [4 DUK](#DUK)
    *   [4.1 Kas atsitiko Entrance ?](#Kas_atsitiko_Entrance_?)
*   [5 Problemų Sprendimas](#Problemų_Sprendimas)
    *   [5.1 Pelės Žymeklis](#Pelės_Žymeklis)
    *   [5.2 Ekrano atrakinimas neveikia](#Ekrano_atrakinimas_neveikia)
    *   [5.3 Neįskaitomi šriftai](#Neįskaitomi_šriftai)
*   [6 Nuorodos](#Nuorodos)

## E17 Įdiegimas

### Iš bendruomeninio repozito (SVN paveikslai)

**Note:** Įsitikinkite, jog jūsų `/etc/pacman.conf` yra įjungtas Bendruomeninis Repozitas ([community repository](/index.php/Community_repository "Community repository")).

Norint įdiegti e17:

```
pacman -S e-svn

```

Norint įdiegti papildomus e17 modulius ir programas:

```
pacman -S e17-extra-svn

```

Taip pat galite įdiegti papildomus šriftus (žr. [Fonts (Lietuviškai)](/index.php?title=Fonts_(Lietuvi%C5%A1kai)&action=edit&redlink=1 "Fonts (Lietuviškai) (page does not exist)")). [Šriftai rekomenduojami grafinėms aplinkoms](/index.php?title=Fonts_(Lietuvi%C5%A1kai)&action=edit&redlink=1 "Fonts (Lietuviškai) (page does not exist)")

Jeigu jums reikia e17 paketo, kuris dar nėra patalpintas bendruomeniniame repozite, patikrinkite, ar jo nėra [AUR](/index.php/AUR "AUR").

**Warning:** Kadangi e17 visdar yra alpha lygio rekomenduojama saugoti praeitų versijų paketus, jei kartais tektų nužeminti versiją, iškilus problemoms.

### Kompiliavimas ir pakavimas su ArchE17 skriptu

Nedidelio python skripto [ArchE17](https://dev.archlinux.org/~ronald/e17.html) pagalba galite patys kurti savo Arch Linux e17 paketus.

## E17 Paleidimas

Jei naudojate `startx` arba paprastą Grafikos Tvarkyklę ([Display manager](/index.php/Display_manager "Display manager")) kaip XDM ar [SLiM](/index.php/SLiM "SLiM"), pridėkite arba atkomentuokite tokią eilutę [xinitrc](/index.php/Xinitrc "Xinitrc") faile:

```
exec enlightenment_start

```

Sudėtingesnės tvarkyklės kaip [GDM](/index.php/GDM "GDM") ar [KDM](/index.php/KDM "KDM") aptiks E17 automatiškai dėka `/usr/share/xsessions/enlightenment.desktop` failo, kuris priklauso `e-svn` paketui.

## Temų Įdiegimas

Daugiau e17 temų galite rasti:

*   [https://www.enlightenment-themes.org/](https://www.enlightenment-themes.org/)

Įdiegti temas (.edj formato) galite pasirinkę System > Themes.

Taip pat galite pakeisti ir etk įrankių komplekto (to, kurį naudoja exhibit) išvaizdą. Tam naudokite komandą `etk_prefs`.

## DUK

### Kas atsitiko Entrance ?

`entrance` - grafikos tvarkyklė paremta EFL, daugiau nebepalaikoma, todėl buvo panaikinta iš paketų sarašo.

## Problemų Sprendimas

Jei susiduriate su neaiškiomis problemomis, iš pradžių imkitės keltos veiksmų:

1.  Pabandykit ar problema išlieka pasirinkus standartinę temą
2.  Pasidarykite atsarginę `~/.e` kopiją ir panaikinkite originalą (pvz: `mv ~/.e ~/.e.back`).

Jei esate įsitikinę, jog radote klaidą, kuo greičiau apie ją praneškite.

### Pelės Žymeklis

Jei X skundžiasi, jog neranda X pelės žymeklių, įdiekite [libxcursor](https://www.archlinux.org/packages/?name=libxcursor) paketą.

### Ekrano atrakinimas neveikia

Jei screenlock nepriima slaptažodžio, pridėkite šią eilutę `/etc/pam.d/enlightenment` faile:

```
auth required pam_unix_auth.so

```

### Neįskaitomi šriftai

Jei šriftai ekrane rodomi per maži ir yra neįskaitomi, įdiekite šiuos paketus:

```
pacman -S ttf-ms-fonts ttf-dejavu ttf-bitstream-vera

```

## Nuorodos

*   [exchange.enlightenment.org](http://exchange.enlightenment.org/)
*   [e17-stuff.org](http://e17-stuff.org/)